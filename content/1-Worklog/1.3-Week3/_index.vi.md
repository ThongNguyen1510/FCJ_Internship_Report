---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Tìm hiểu nền tảng mạng ảo VPC và các thành phần định tuyến trên AWS.
* Triển khai kiến trúc mạng hai lớp cô lập an toàn sử dụng public/private subnet.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | Tìm hiểu cấu trúc mạng Amazon VPC: CIDR block, Subnet (Public/Private), Route Table và Internet Gateway (IGW). | 04/05/2026 | 04/05/2026 | <https://docs.aws.amazon.com/vpc/> |
| 3 | Cấu hình NAT Gateway để cho phép các máy chủ trong Private Subnet truy cập internet tải bản cập nhật. | 05/05/2026 | 05/05/2026 | <https://docs.aws.amazon.com/vpc/> |
| 4 | So sánh và thực hành cấu hình bảo mật: Security Group (stateful) vs Network ACL (stateless). | 06/05/2026 | 06/05/2026 | <https://docs.aws.amazon.com/vpc/> |
| 5 | Khởi chạy máy chủ EC2 trong Private Subnet và thiết lập kết nối gián tiếp qua Bastion Host ở Public Subnet. | 07/05/2026 | 07/05/2026 | <https://docs.aws.amazon.com/vpc/> |
| 6 | Sử dụng VPC Reachability Analyzer để kiểm định định tuyến và tìm lỗi cấu hình mạng. | 08/05/2026 | 08/05/2026 | <https://docs.aws.amazon.com/vpc/> |

### Kết quả đạt được trong tuần 3:

* Tự thiết kế và cấu hình hoàn chỉnh một hệ thống mạng ảo VPC tùy chỉnh từ đầu.
* Nắm vững nguyên lý bảo mật nhiều lớp giữa các lớp mạng công cộng và nội bộ.
