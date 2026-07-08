---
title: "Blog 4"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 3.4. </b> "
---

# Triển khai kiểm soát truy cập chi tiết với Amazon Cognito User Pool

### 1. Định nghĩa Kiểm soát truy cập chi tiết (FGAC)
Trong các ứng dụng đa người thuê (multi-tenant) và hệ thống doanh nghiệp, nguyên tắc bảo mật quy định rằng người dùng chỉ được xem và sửa đổi tài nguyên thuộc về tổ chức, phòng ban hoặc cấp độ thẩm quyền của họ. Đây được gọi là **Kiểm soát truy cập chi tiết (FGAC)**.

Amazon Cognito User Pools, kết hợp với API Gateway và AWS IAM, cung cấp một bộ công cụ mạnh mẽ để thực thi các chính sách FGAC trên các API REST.

---

### 2. Cognito User Groups và Thuộc tính Tùy chỉnh (Custom Attributes)
Để triển khai FGAC, chúng ta định nghĩa các thuộc tính tùy chỉnh bên trong Amazon Cognito User Pool:
- `custom:tenant_id`: Xác định không gian làm việc của tổ chức mà người dùng trực thuộc.
- `custom:clearance_level`: Phân loại vai trò của người dùng (ví dụ: Admin, ReadOnly).

Khi người dùng xác thực thành công, các thuộc tính này sẽ được nhúng trực tiếp vào các claim của mã thông báo ID JWT.

---

### 3. Các mô hình tích hợp API Gateway
Chúng ta có thể thực thi các quy tắc ủy quyền tại lớp API Gateway bằng hai mô hình chính:
1. **Cognito Authorizer**: API Gateway tự động kiểm tra chữ ký của token Cognito JWT và xác thực thời gian hết hạn. Tuy nhiên, logic định tuyến dựa trên các thuộc tính tùy chỉnh phải được xử lý bên trong Lambda.
2. **Lambda Authorizer**: Một hàm Lambda tùy chỉnh chặn token, phân tích các thuộc tính tùy chỉnh và tạo động một chính sách IAM để trả về cho API Gateway.

Dưới đây là một đoạn mã của Lambda Authorizer (Python) tạo chính sách IAM giới hạn theo `tenant_id`:

```python
def generate_policy(principal_id, effect, resource, tenant_id):
    auth_response = {
        'principalId': principal_id,
        'policyDocument': {
            'Version': '2012-10-17',
            'Statement': [{
                'Action': 'execute-api:Invoke',
                'Effect': effect,
                'Resource': resource
            }]
        },
        'context': {
            'tenantId': tenant_id
        }
    }
    return auth_response
```

Hàm Lambda xử lý nghiệp vụ phía sau có thể đọc `requestContext.authorizer.tenantId` để truy vấn cơ sở dữ liệu và chỉ trả về bản ghi khớp với ID tenant đó.

---

### 4. Tóm tắt
Kết hợp các thuộc tính tùy chỉnh của Cognito với Lambda Authorizer cung cấp một ranh giới an toàn tuyệt đối giữa các tenant, bảo vệ dữ liệu khỏi các truy vấn trái phép hoặc rò rỉ dữ liệu chéo.

