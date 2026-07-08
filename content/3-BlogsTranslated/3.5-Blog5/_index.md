---
title: "Blog 5"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 3.5. </b> "
---

# Building Scalable Pipelines for IoT Analytics using AWS Glue

### 1. The Proliferation of IoT Telemetry
Edge IoT devices, such as weather stations or health trackers, continuously publish high-frequency telemetry. This data is usually sent in JSON format because of its simplicity and compatibility.

However, storing raw JSON telemetry in S3 leads to major challenges when query performance and cost scale:
- JSON files are bulky and contain repeated key names.
- Querying uncompressed JSON files using services like Amazon Athena requires scanning the entire dataset, which is expensive.
- AWS Glue ETL (Extract, Transform, Load) pipelines provide a serverless method to transform raw JSON files into optimized columnar storage formats like **Apache Parquet**.

---

### 2. AWS Glue Cataloging and Schema Discovery
An **AWS Glue Crawler** automated task runs periodically to scan the S3 raw data lake folder. It automatically infers the data schema, detects changes in layout, and populates tables in the **Glue Data Catalog**.

Once cataloged, the data metadata is immediately queryable via Athena, even while still in raw JSON format.

---

### 3. Serverless ETL Transformation
To convert the data to Parquet and organize it by partitions (such as `year`, `month`, and `day`), we run an AWS Glue Spark job.
A PySpark code snippet for this transformation is shown below:

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

# Convert format and write to partitioned S3 bucket
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

### 4. Query Performance and Cost Reductions
By converting the raw JSON files into Parquet format, files are stored columns-first and compressed. 
When running Amazon Athena SQL queries on Parquet datasets:
- **Scan volume is reduced by up to 90%**, directly translating to a **90% reduction in query costs**.
- Query execution speed is significantly faster, allowing real-time dashboards to reload quickly.

