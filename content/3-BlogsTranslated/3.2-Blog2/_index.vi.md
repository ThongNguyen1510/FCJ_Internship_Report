---
title: "Blog 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Healthcare Data Lake: Tìm hiểu sâu về Amazon Cognito và ABAC

### 1. Giới thiệu về Healthcare Data Lake và Bảo mật
Xây dựng một data lake trong lĩnh vực y tế đòi hỏi phải tuân thủ nghiêm ngặt các quy định như HIPAA và GDPR. Kho lưu trữ tập trung chứa Thông tin Sức khỏe Cá nhân (PHI) và Hồ sơ Sức khỏe Điện tử (EHR) vô cùng nhạy cảm. Kiểm soát truy cập ở mức độ chi tiết là một yêu cầu bảo mật bắt buộc.

Amazon Web Services (AWS) cung cấp nhiều công cụ bảo mật, nhưng việc triển khai kiểm soát truy cập dựa trên vai trò tĩnh (RBAC) thường dẫn đến sự gia tăng quá mức các chính sách và vai trò IAM. Để khắc phục vấn đề về khả năng mở rộng này, kiến trúc đám mây hiện đại sử dụng **Kiểm soát truy cập dựa trên thuộc tính (ABAC)**, giúp phân quyền động dựa trên các thuộc tính (thẻ tag) được gắn vào người dùng, tài nguyên và phiên API.

---

### 2. Xác thực với Amazon Cognito
Amazon Cognito đóng vai trò là nhà cung cấp danh tính (IdP) chính để xác thực khách hàng:
- **User Pools**: Quản lý danh bạ người dùng, đăng ký và đăng nhập. Các thuộc tính như `department`, `hospital-id` và `role` được nhúng dưới dạng các claim trong mã thông báo JSON Web Token (JWT).
- **Identity Pools (Federated Identities)**: Chuyển đổi Cognito JWT thành thông tin xác thực AWS IAM tạm thời. Khi liên kết, các claim của Cognito có thể được ánh xạ tới các thẻ principal tag của IAM.

---

### 3. Triển khai ABAC (Attribute-Based Access Control)
ABAC tận dụng các thẻ tag được gắn vào thông tin xác thực IAM (principal tags) và tài nguyên AWS mục tiêu (ví dụ: các đối tượng trong S3 bucket hoặc các cột cơ sở dữ liệu).
Dưới đây là một ví dụ về chính sách IAM mẫu giới hạn quyền truy cập tài nguyên S3 bằng principal tag:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:PutObject"],
      "Resource": "arn:aws:s3:::healthcare-data-lake-prod/*",
      "Condition": {
        "StringEquals": {
          "s3:ExistingObjectTag/HospitalID": "${aws:PrincipalTag/HospitalID}"
        }
      }
    }
  ]
}
```

Trong chính sách này, quyền truy cập chỉ được cấp nếu thẻ tag `HospitalID` của đối tượng S3 khớp với thẻ tag `HospitalID` của người dùng đang gửi yêu cầu. Điều này giúp giảm số lượng chính sách IAM cần thiết vì một chính sách duy nhất có thể tự động thích ứng với bất kỳ định danh bệnh viện nào.

---

### 4. Các bài học chính
- **Khả năng mở rộng**: ABAC đơn giản hóa đáng kể việc quản lý quyền của người dùng khi tổ chức mở rộng quy mô.
- **Bảo mật động**: Các thẻ tài nguyên kết hợp với thông tin danh tính cung cấp khả năng bảo vệ động, thời gian thực cho thông tin nhạy cảm của bệnh nhân.

