---
title: "Blog 5"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 3.5. </b> "
---

# Xây dựng quy trình xử lý dữ liệu quy mô lớn cho IoT Analytics với AWS Glue

### 1. Sự gia tăng của dữ liệu IoT Telemetry
Các thiết bị biên IoT, chẳng hạn như trạm thời tiết hoặc thiết bị theo dõi sức khỏe, liên tục gửi dữ liệu đo lường tần suất cao. Dữ liệu này thường được gửi ở định dạng JSON vì tính đơn giản và khả năng tương thích cao.

Tuy nhiên, việc lưu trữ thô dữ liệu JSON trong S3 dẫn đến các thách thức lớn khi mở rộng hệ thống:
- Các tệp JSON khá cồng kềnh và chứa nhiều trường thông tin lặp đi lặp lại.
- Truy vấn các tệp JSON không nén bằng các dịch vụ như Amazon Athena yêu cầu quét toàn bộ tập dữ liệu, gây tốn kém chi phí.
- Quy trình **AWS Glue ETL** (Extract, Transform, Load) cung cấp giải pháp serverless để chuyển đổi các tệp JSON thô thành các định dạng lưu trữ cột được tối ưu hóa như **Apache Parquet**.

---

### 2. Khám phá Schema và Lập danh mục dữ liệu với AWS Glue Catalog
Một tác vụ tự động của **AWS Glue Crawler** được định cấu hình chạy định kỳ để quét thư mục chứa dữ liệu thô trên S3. Nó tự động suy luận schema (lược đồ dữ liệu), phát hiện các thay đổi cấu trúc và điền thông tin vào bảng trong **Glue Data Catalog**.

Sau khi được lập danh mục, siêu dữ liệu (metadata) của tệp thô có thể được truy vấn ngay lập tức qua Athena.

---

### 3. Chuyển đổi dữ liệu Serverless với ETL
Để chuyển đổi dữ liệu sang định dạng Parquet và tổ chức theo các phân vùng (chẳng hạn như `year`, `month` và `day`), chúng ta chạy một tiến trình AWS Glue Spark.
Dưới đây là một đoạn mã PySpark thực hiện quá trình chuyển đổi này:

```python
import sys
from awsglue.transforms import *
from awsglue.utils import getResolvedOptions
from pyspark.context import SparkContext
from awsglue.context import GlueContext
from awsglue.job import Job

glueContext = GlueContext(SparkContext.getOrCreate())
datasource = glueContext.create_dynamic_frame.from_catalog(
    database = "weather_lake", 
    table_name = "raw_telemetry"
)

# Chuyển đổi định dạng và ghi vào S3 bucket đã phân vùng
glueContext.write_dynamic_frame.from_options(
    frame = datasource,
    connection_type = "s3",
    connection_options = {
        "path": "s3://weather-lake-parquet-prod/",
        "partitionKeys": ["year", "month", "device_id"]
    },
    format = "parquet"
)
```

---

### 4. Hiệu suất truy vấn và Giảm thiểu chi phí
Bằng cách chuyển đổi các tệp JSON thô thành định dạng Parquet, dữ liệu sẽ được lưu trữ theo cột và nén tối ưu.
Khi thực hiện các truy vấn SQL trên Amazon Athena đối với dữ liệu Parquet:
- **Dung lượng quét dữ liệu giảm đến 90%**, giúp **giảm trực tiếp 90% chi phí truy vấn**.
- Tốc độ thực thi truy vấn nhanh hơn đáng kể, giúp các dashboard hiển thị dữ liệu tức thời.

