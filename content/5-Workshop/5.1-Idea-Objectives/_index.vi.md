---
title: "Ý tưởng & Mục tiêu"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---


### 1. Bối cảnh & Bài toán
Các doanh nghiệp hoặc cá nhân cần một hệ thống giám sát thời gian thực để biết website của họ có đang hoạt động hay bị sập (downtime). Giải pháp cần tự động hóa, chi phí cực thấp (hoặc miễn phí) và cảnh báo ngay lập tức.

*   **Khách hàng:** Quản trị viên hệ thống (SysAdmin), DevOps Team, Chủ website.
*   **Giải pháp:** Xây dựng hệ thống Serverless tự động ping website mỗi 5 phút, lưu trữ độ trễ (latency) làm lịch sử và lập tức bắn Email cảnh báo nếu website không phản hồi.

### 2. Tiêu chí thành công
*   **Infrastructure as Code:** Hệ thống triển khai 100% tự động bằng Code (Terraform).
*   **Lưu trữ dữ liệu:** Lưu lịch sử ping thành công vào Database.
*   **Độ trễ cảnh báo:** Nhận được Email cảnh báo trong vòng 1 phút kể từ khi website bị sập.
