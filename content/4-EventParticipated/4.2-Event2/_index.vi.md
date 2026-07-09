---
title: "Event 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# FCAJ Community Day - Conference Call

### Thông tin sự kiện
*   **Tên sự kiện:** FCAJ Community Day - Conference Call
*   **Thời gian:** Thứ Bảy, ngày 23 tháng 5, từ 9:00 AM đến 12:00 PM (GMT+7) (Đón khách từ 8:30 AM)
*   **Địa điểm:** Tòa nhà Bitexco Financial Tower, Thành phố Hồ Chí Minh (Tầng 36)
*   **Mục tiêu:** Nghiên cứu sâu về ứng dụng AI dựa trên ngữ cảnh, phát triển sản phẩm thực tế trong cuộc thi hackathon, kiến trúc phân phối biên CloudFront, tính phi định tính của LLM và hệ thống Multi-Agent cấp doanh nghiệp.

---

### Chi tiết các phiên thảo luận

#### ☁️ 8:30 - 9:00 AM | Đón khách & Ổn định chỗ ngồi
*   Các thành viên và khách mời tập trung tại tầng 36 tòa nhà Bitexco để check-in, giao lưu và thiết lập môi trường chuẩn bị cho sự kiện.

#### ☁️ 09:00 - 09:30 AM | Context Is Everything: Making AI Actually Work for You
*   **Định nghĩa về Ngữ cảnh:** Phân tích lý do tại sao các mô hình AI thường gặp hiện tượng "ảo tưởng" (hallucination) khi thiếu dữ liệu nền tảng và ý nghĩa thực sự của "ngữ cảnh" đối với kiến trúc Transformer.
*   **Bộ não AI thứ hai:** Trình bày sự dịch chuyển từ kỹ thuật prompt đơn thuần sang bộ nhớ ngữ cảnh ngữ nghĩa (Semantic Memory) dựa trên Vector.
*   **Tư duy thực tế:** Cách tối ưu hóa kết quả đầu ra của AI thông qua việc chủ động cung cấp dữ liệu ngữ cảnh (nhờ RAG hoặc siêu dữ liệu).
*   **Q&A:** Định hướng cho sinh viên các phương pháp thiết kế ứng dụng AI hiểu ngữ cảnh.

#### ☁️ 09:30 - 10:00 AM | 36 hrs with LotusHacks – Building UTMorpho from Idea to Reality
*   **Trải nghiệm Hackathon:** Chia sẻ quá trình tham gia cuộc thi lập trình tăng tốc **LotusHacks** kéo dài 36 giờ liên tục.
*   **Hành trình phát triển ý tưởng:** Quá trình thảo luận từ xuất phát điểm chưa có gì đến khi xây dựng thành công ý tưởng cốt lõi, xác định bài toán thực tế và thiết kế sản phẩm **UTMorpho**.
*   **Lập trình dưới áp lực cao:** Kinh nghiệm vượt qua các rào cản về thời gian, giải quyết mâu thuẫn kỹ thuật trong nhóm và bài học từ những phiên bản lỗi đầu tiên.
*   **Demo & Định hướng:** Demo chạy thực tế sản phẩm UTMorpho, các bài học công nghệ đắt giá và lộ trình nâng cấp sản phẩm tiếp theo.

#### ☁️ 10:00 - 10:40 AM | From Edge To Origin: CloudFront as Your Foundation
*   **Các loại tải trên CloudFront:** Hướng dẫn cấu hình tối ưu hóa phân phối cho cả trang web tĩnh (SPA) và các API động đòi hỏi tính bảo mật cao.
*   **Tối ưu hóa tại điểm biên:** Sử dụng cơ chế cache của CloudFront, nén dữ liệu (Brotli/Gzip) và tùy chỉnh header để giảm thiểu thời gian phản hồi của API gốc.
*   **Hiệu năng & Bảo mật biên:** Triển khai tích hợp AWS WAF và AWS Shield tại điểm biên để ngăn chặn sớm các cuộc tấn công DDoS và truy cập trái phép.

#### ☁️ 10:40 - 10:55 AM | Friendly AI Assistant with Amazon Quick
*   **Quick Chat Agent:** Giao diện trò chuyện thông minh cho phép người dùng truy vấn dữ liệu kinh doanh và phân tích xu hướng bằng ngôn ngữ tự nhiên.
*   **Quick Flows:** Thiết lập các quy trình tự động hóa nghiệp vụ thông qua câu lệnh tự nhiên mà không cần viết mã backend.
*   **Quick Spaces:** Không gian làm việc chung giúp kết nối các phát hiện của cá nhân thành kho kiến thức dùng chung cho tổ chức.
*   **Quick Sight:** Tự động tạo lập biểu đồ và báo cáo quản trị từ kho dữ liệu thô bằng các mô tả đơn giản.

#### ☕ 10:55 - 11:00 AM | Giải lao (Break)

#### ☁️ 11:00 - 11:30 AM | Non-Determinism of "Deterministic" LLM Settings
*   **Cơ chế chọn Token:** Cách các mô hình LLM dự đoán và chọn từ tiếp theo dựa trên xác suất phân phối.
*   **Lầm tưởng về tính định tính:** Phân tích lý do tại sao cấu hình `Temperature=0` vẫn không thể đảm bảo kết quả đầu ra giống nhau 100% khi chạy thực tế trên các hệ thống production.
*   **Yếu tố phần cứng:** Làm rõ sự ảnh hưởng từ việc tối ưu hóa tính toán song song trên GPU, lập lịch luồng (thread scheduling) và xử lý hàng loạt (batching) gây ra sai số ngẫu nhiên nhỏ.
*   **Biện pháp khắc phục:** Sử dụng các bộ kiểm tra định dạng đầu ra (như cấu trúc JSON schema) và thiết lập vòng lặp thử lại (retry loops) để chuẩn hóa kết quả.

#### ☁️ 11:30 AM - 12:00 PM | Enterprise-Grade Multi-Agent System: Startup Credit Scoring
*   **Bài toán tín dụng:** Sự không tương thích giữa các chỉ số đánh giá của ngân hàng truyền thống và cấu trúc dữ liệu tăng trưởng nhanh của các startup.
*   **So sánh kiến trúc:** Đánh giá hạn chế của mô hình Single Agent trong các bài toán phức tạp đòi hỏi tuân thủ pháp lý cao.
*   **Hội đồng tín dụng ảo (Virtual Credit Committee):** Bản thiết kế hệ thống nhiều AI Agent chuyên biệt (Agent phân tích, Agent đánh giá rủi ro, Agent kiểm soát tuân thủ) phối hợp thẩm định hồ sơ vay.
*   **ROI & Lộ trình triển khai:** Cách cấu hình rào cản bảo mật (guardrails) đảm bảo tính pháp lý và lộ trình đưa hệ thống Multi-Agent vào vận hành thực tế.

---

### Những gì học được
1.  **Dữ liệu ngữ cảnh quyết định chất lượng:** Prompt tốt chỉ là bước đầu; các ứng dụng AI cấp doanh nghiệp bắt buộc phải có cơ chế truy xuất ngữ cảnh (RAG) để đảm bảo thông tin chính xác.
2.  **Bảo mật phân phối biên:** Sử dụng CloudFront làm nền tảng giúp tăng tốc độ tải trang toàn cầu đồng thời làm tấm khiên chặn đứng các truy cập phá hoại từ biên.
3.  **Chấp nhận tính bất định của LLM:** Khi thiết kế hệ thống phần mềm tích hợp LLM, kỹ sư phải lập trình phòng ngừa việc kết quả trả về không đồng nhất bằng các bộ parser kiểm tra định dạng chặt chẽ.
4.  **Sức mạnh của Multi-Agent:** Chia nhỏ các quy trình nghiệp vụ phức tạp cho nhiều AI Agent chuyên hóa giúp cải thiện đáng kể độ tin cậy và hiệu năng của hệ thống GenAI.

### Ứng dụng vào công việc
*   **Cấu hình API gốc:** Áp dụng mô hình định tuyến và nén dữ liệu của CloudFront để tối ưu hóa thời gian phản hồi của backend giám sát.
*   **Định dạng dữ liệu AI:** Sử dụng JSON schema và kiểm định định dạng nghiêm ngặt khi xây dựng các tác vụ tự động hóa xử lý log bằng AI.
*   **Phát triển Multi-Agent:** Nghiên cứu phân chia các tác vụ phân tích cảnh báo hệ thống cho các agent chuyên môn hóa khác nhau.
