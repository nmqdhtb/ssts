# Yêu cầu chức năng (Functional Requirements)

**Dự án:** Kho tri thức hỗ trợ học thuật — Academic Assistant, Learning Assistant, Knowledge Hub  
**Trạng thái:** Bản nháp để nhóm xác nhận  
**Nguồn:** Mô tả đề tài do người dùng cung cấp; `00_control/PROJECT_BRIEF.md` vẫn là template.  
**Ngày:** 18/11/2026

## 1. Phạm vi và actor

Đề tài hướng tới việc giúp sinh viên và giảng viên tìm, hiểu và tổng hợp tài liệu học thuật đang phân tán. Các actor giả định: **Sinh viên** (tìm, hỏi, học, ôn); **Giảng viên** (tìm/tổng hợp, có thể cung cấp tài liệu); **Quản trị viên/curator** (quản lý nguồn, metadata, phiên bản và trạng thái xử lý). Quyền cụ thể chưa được xác nhận.

**Giả định MVP:** ưu tiên hỏi đáp theo tài liệu đã nạp, có dẫn nguồn; tìm/mở nguồn hỗ trợ luồng chính. Learning Assistant và quản trị tài liệu nâng cao cần PO xác nhận phạm vi.

Ưu tiên: Must = cần cho lát cắt MVP; Should = quan trọng; Could = mở rộng.

## 2. Yêu cầu chức năng

| ID | Mô tả | Actor | Ưu tiên | Tiêu chí chấp nhận |
|---|---|---|---|---|
| FR-001 | Chọn môn học/phạm vi tài liệu trước khi tìm kiếm hoặc hỏi đáp. | SV, GV | Must | Nội dung truy xuất giới hạn trong phạm vi đã chọn; nếu chưa chọn, yêu cầu chọn hoặc nêu rõ phạm vi mặc định đã được duyệt. |
| FR-002 | Tìm tài liệu theo từ khóa, lọc theo môn, loại, nguồn/giảng viên và phiên bản nếu metadata có. | SV, GV | Should | Kết quả hiển thị metadata có sẵn và chỉ gồm tài liệu được phép xem. |
| FR-003 | Nhận câu hỏi tự nhiên và tìm các đoạn liên quan trong tài liệu được phép truy cập. | SV, GV | Must | Không tìm hoặc dùng nguồn ngoài quyền/phạm vi. |
| FR-004 | Tạo câu trả lời dựa trên nội dung truy xuất và gắn trích dẫn tới tài liệu/đoạn nguồn. | SV, GV | Must | Trích dẫn mở được; không đủ bằng chứng thì nêu rõ, không bịa câu trả lời hoặc nguồn. |
| FR-005 | Mở nguồn trích dẫn để xem tài liệu và vị trí trang/slide nếu xác định được. | SV, GV | Must | Nguồn trỏ đúng tài liệu/phiên bản; không tự tạo số trang khi thiếu dữ liệu vị trí. |
| FR-006 | Giải thích khái niệm theo tài liệu, có thể yêu cầu cách giải thích đơn giản hơn hoặc ví dụ. | SV | Should | Có nguồn; phân biệt nội dung tài liệu với ví dụ do AI tạo. |
| FR-007 | Tạo câu hỏi ôn tập/gợi ý chủ đề ôn từ tài liệu đã chọn. | SV | Could | Câu hỏi/chủ đề truy vết được về nguồn; cho phép yêu cầu tạo lại. |
| FR-008 | Duyệt tài liệu theo môn học/chủ đề. | SV, GV | Should | Chỉ hiện tài liệu được phép; trạng thái và metadata tối thiểu rõ ràng. |
| FR-009 | Curator nạp tài liệu được hỗ trợ và khai báo môn, loại, nguồn, phiên bản, quyền truy cập. | Curator | Must cho ingestion; nếu không thì dùng corpus nạp sẵn | Tài liệu thiếu quyền/metadata hoặc chưa xử lý không được hiển thị là sẵn sàng. |
| FR-010 | Trích xuất và lập chỉ mục tài liệu cho tìm kiếm/hỏi đáp. | Hệ thống | Must | Có trạng thái chờ/đang xử lý/thành công/thất bại; lỗi có thể nhận biết và xử lý lại. |
| FR-011 | Phân quyền tài liệu theo vai trò/phạm vi môn học cấu hình. | Tất cả | Must | Người không có quyền không thể tìm, mở nguồn, tải hoặc lấy nội dung qua câu trả lời/API. |
| FR-012 | Gửi phản hồi hữu ích/không hữu ích, kèm lý do tùy chọn. | SV, GV | Should | Phản hồi gắn đúng câu trả lời và chỉ người được phép xem. |
| FR-013 | Xem lại lịch sử hỏi đáp trong phiên/tài khoản nếu chức năng được bật. | SV, GV | Could | Chỉ xem lịch sử của mình; tuân thủ chính sách lưu/xóa đã duyệt. |
| FR-014 | Thông báo rõ khi ngoài phạm vi, thiếu nguồn, lỗi truy xuất hoặc lỗi xử lý tài liệu. | Tất cả | Must | Nêu giới hạn và bước tiếp theo; không khẳng định độ tin cậy không có căn cứ. |

## 3. Quy tắc nghiệp vụ

- **BR-001:** Câu trả lời học thuật cần bằng chứng từ nguồn được phép; thiếu bằng chứng thì nêu giới hạn.
- **BR-002:** Quyền truy cập áp dụng cả lúc tìm kiếm, sinh câu trả lời, mở trích dẫn và tải tài liệu.
- **BR-003:** Không tự gộp các phiên bản tài liệu khác nhau; giữ liên kết về phiên bản nguồn.
- **BR-004:** Phân biệt trích dẫn/nội dung nguồn với phần diễn giải hoặc ví dụ do AI tạo.
- **BR-005:** Đề tài nêu mục tiêu độ chính xác **≥80% trên tập kiểm thử**. Chưa có định nghĩa metric, rubric, tập dữ liệu hay kết quả; đây là mục tiêu cần xác nhận, không phải thành tích đã đạt.

## 4. Yêu cầu phi chức năng sơ bộ

- **NFR-001 Chất lượng AI:** đánh giá trên tập kiểm thử đóng băng theo rubric được duyệt; báo riêng độ đúng nội dung và độ đúng trích dẫn. Ngưỡng đề tài nêu: ≥80%, cách tính TBD.
- **NFR-002 Hiệu năng:** latency, tải đồng thời, giới hạn kích thước tài liệu: TBD.
- **NFR-003 Bảo mật:** không truy xuất/trả tài liệu vượt quyền; khóa API không lưu trong mã nguồn.
- **NFR-004 Riêng tư:** tối thiểu hóa dữ liệu; việc gửi dữ liệu tới dịch vụ ngoài, retention và xóa cần phê duyệt.
- **NFR-005 Khả dụng:** nêu rõ trạng thái, lỗi và thiếu nguồn bằng tiếng Việt (ngôn ngữ dự kiến, cần xác nhận).
- **NFR-006 Truy vết:** có thể lần về tài liệu/phiên bản/đoạn nguồn trong phạm vi log được duyệt.

## 5. Câu hỏi cần chốt

1. MVP demo cả ba mô-đun hay tập trung hỏi đáp có trích dẫn?
2. Ai tải, duyệt và sở hữu tài liệu? Nguồn nào có quyền sử dụng?
3. “Độ chính xác ≥80%” được chấm theo rubric nào, trên tập câu hỏi nào và bởi ai?
4. Có yêu cầu đăng nhập, tích hợp hệ thống trường, lịch sử hội thoại hoặc phản hồi không?
5. Định dạng dữ liệu, nền tảng, ngân sách, thời hạn và latency mục tiêu là gì?

## 6. Traceability sơ bộ

| Yêu cầu | Use case | Kiểm thử dự kiến |
|---|---|---|
| FR-001, FR-003–005, FR-014 | UC-01 | TC-UC01-01…05 |
| FR-002, FR-008 | UC-02 | TC-UC02-01…03 |
| FR-006–007 | UC-03 | TC-UC03-01…03 |
| FR-009–010 | UC-04 | TC-UC04-01…03 |
| FR-011 | UC-05 | TC-UC05-01…03 |
| FR-012–013 | UC-06 | TC-UC06-01…03 |

Mã test là dự kiến, chưa có test case hoặc kết quả chạy thực tế.
