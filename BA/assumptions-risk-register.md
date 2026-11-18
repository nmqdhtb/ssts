# Sổ đăng ký giả định và rủi ro

**Dự án:** Kho tri thức hỗ trợ học thuật  
**Trạng thái:** Bản nháp — cần nhóm xác nhận  
**Nguồn:** Mô tả đề tài trong trao đổi; PROJECT_BRIEF.md chưa được điền.  
**Ngày:** 18/11/2026

## 1. Giả định

| ID | Giả định (chưa phải dữ kiện) | Cách kiểm chứng | Owner đề xuất | Trạng thái |
|---|---|---|---|---|
| A-01 | Sinh viên là nhóm người dùng ưu tiên; giảng viên là nhóm phụ. | PO xác nhận persona; phỏng vấn/khảo sát người dùng. | PM/Research | Chưa xác nhận |
| A-02 | Có thể dùng một tập tài liệu hợp lệ, có quyền truy cập và metadata tối thiểu. | Kiểm kê tài liệu, chủ sở hữu, quyền, phiên bản và định dạng. | Data/BA | Chưa xác nhận |
| A-03 | Lát cắt MVP là hỏi đáp theo tài liệu có trích dẫn và xử lý “không đủ nguồn”. | PO chốt phạm vi; Tech Lead ước lượng. | PO/Tech | Chưa xác nhận |
| A-04 | Mục tiêu ≥80% là kết quả đánh giá trên tập kiểm thử, không phải cam kết mọi câu hỏi thực tế. | Chốt rubric, tập test, cỡ mẫu, người chấm và cách tính. | QA/AI | Chưa xác nhận |
| A-05 | Sản phẩm cần hỗ trợ tiếng Việt. | Xác nhận với chủ nhiệm đề tài/người dùng. | PM/Design | Chưa xác nhận |
| A-06 | Nếu chưa có SSO/tích hợp trường, demo có thể dùng tài khoản đơn giản hoặc corpus nạp sẵn. | Xác nhận yêu cầu demo và hệ thống hiện có. | Tech Lead | Chưa xác nhận |
| A-07 | Định dạng đầu vào có thể gồm PDF, slide và văn bản; chưa biết định dạng nào thực sự dùng được. | Kiểm kê và thử trích xuất trên mẫu đại diện. | Data Engineer | Chưa xác nhận |

## 2. Rủi ro

Thang K/A: Thấp, Trung bình, Cao. Mức đánh giá sơ bộ, cần nhóm rà soát.

| ID | Kịch bản | K | A | Ưu tiên | Giảm thiểu đề xuất | Owner |
|---|---|---:|---:|---:|---|---|
| R-01 | AI trả lời sai/bịa khi nguồn không chứa đáp án. | Cao | Cao | Cao | RAG có nguồn; từ chối khi thiếu bằng chứng; test câu hỏi ngoài phạm vi. | AI/QA |
| R-02 | Trích dẫn sai nội dung, trang hoặc phiên bản. | TB | Cao | Cao | Kiểm tra riêng citation accuracy; lưu ID/phiên bản/vị trí; không bịa trang. | Data/AI/QA |
| R-03 | Tài liệu bản quyền hoặc quyền sử dụng chưa rõ bị nạp. | TB | Cao | Cao | Ghi chủ sở hữu/quyền trước ingestion; chỉ dùng nguồn được phép; xin xác nhận đơn vị quản lý. | PM/Data |
| R-04 | Dữ liệu cá nhân/nội bộ lộ qua tìm kiếm, mô hình hoặc log. | Thấp–TB | Cao | Cao | Tối thiểu hóa/ẩn danh; kiểm soát quyền; không gửi ra ngoài khi chưa duyệt; xác định retention/xóa. | Security/Data |
| R-05 | Lỗi phân quyền khiến người dùng xem tài liệu môn/lớp khác. | TB | Cao | Cao | Kiểm tra quyền tại truy xuất, API và mở nguồn; test truy cập chéo. | Backend/Security/QA |
| R-06 | PDF scan, bảng hoặc công thức trích xuất kém gây câu trả lời sai. | Cao | TB–Cao | Cao | Thử trên mẫu thực; đánh dấu chất lượng extraction; duyệt tài liệu lỗi trước khi dùng. | Data Engineer |
| R-07 | Tập test nhỏ/thiên lệch khiến kết quả ≥80% gây hiểu nhầm. | TB | Cao | Cao | Bao phủ môn và dạng câu hỏi; có trường hợp thiếu đáp án; đóng băng dữ liệu/rubric; báo giới hạn. | QA/AI |
| R-08 | Prompt injection trong tài liệu làm mô hình bỏ qua chỉ dẫn an toàn hoặc tiết lộ dữ liệu. | Thấp–TB | Cao | TB–Cao | Coi tài liệu là dữ liệu không tin cậy; không cho tài liệu gọi tool; kiểm thử injection/exfiltration. | AI/Security |
| R-09 | Chi phí hoặc độ trễ AI vượt khả năng demo/vận hành. | TB | TB | TB | Đo latency/chi phí trên luồng thực; giới hạn token/tần suất; chọn mô hình theo ngân sách. | Tech/AI |
| R-10 | Ba mô-đun vượt quá thời gian/nhân lực. | Cao | Cao | Cao | Chốt một lát cắt MVP; đưa phần còn lại vào backlog; demo sớm. | PM/PO |
| R-11 | Người dùng coi nội dung AI là chỉ dẫn học thuật chính thức. | TB | TB–Cao | TB–Cao | Hiển thị nguồn/giới hạn; khuyến khích đối chiếu tài liệu/giảng viên; tránh khẳng định quá mức. | Product/Design |
| R-12 | Nhiều bản tài liệu cũ/trùng gây câu trả lời mâu thuẫn. | TB | TB–Cao | TB–Cao | Quản lý phiên bản, ngày hiệu lực và trạng thái thay thế; quy tắc chọn bản cần được duyệt. | Curator/Data |

## 3. Cần người phụ trách quyết định

- Phạm vi MVP và actor ưu tiên.
- Corpus, quyền sử dụng, định dạng và người duyệt tài liệu.
- Định nghĩa ngưỡng ≥80%, bộ đánh giá và người xác nhận kết quả.
- Mô hình AI, điều kiện gửi dữ liệu ra ngoài, ngân sách và giới hạn chi phí.
- Đăng nhập/phân quyền, lưu lịch sử, log, retention và xóa dữ liệu.

Không có rủi ro nào được đánh dấu đã xử lý; các kiểm soát trên là đề xuất.
