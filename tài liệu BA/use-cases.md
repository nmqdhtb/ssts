# Đặc tả Use Case

**Dự án:** Kho tri thức hỗ trợ học thuật  
**Trạng thái:** Bản nháp — cần xác nhận cùng phạm vi MVP  
**Ngày:** 18/11/2026  
**Actor giả định:** Sinh viên, giảng viên, quản trị viên/curator.

## UC-01 — Hỏi đáp học thuật có trích dẫn

- **Mục tiêu:** Nhận câu trả lời dựa trên tài liệu môn học và tự kiểm tra nguồn.
- **Actor chính:** Sinh viên hoặc giảng viên.
- **Tiền điều kiện:** Actor có quyền; có tài liệu đã xử lý trong phạm vi.
- **Kích hoạt:** Actor mở Academic Assistant và gửi câu hỏi.
- **Hậu điều kiện:** Câu trả lời và nguồn hiển thị; liên kết tới tài liệu/phiên bản/đoạn được giữ theo chính sách.
- **Yêu cầu:** FR-001, FR-003–005, FR-011, FR-014.

**Luồng chính:** (1) Chọn môn/phạm vi. (2) Nhập câu hỏi. (3) Hệ thống kiểm tra quyền và truy xuất nguồn. (4) Đánh giá nguồn đủ liên quan. (5) Tạo câu trả lời có trích dẫn. (6) Actor mở nguồn đối chiếu.

**Ngoại lệ:**

- Chưa chọn phạm vi → yêu cầu chọn hoặc dùng mặc định đã duyệt.
- Không có nguồn đủ → nêu rõ thiếu dữ liệu, gợi ý sửa câu hỏi/chọn phạm vi; không bịa đáp án.
- Không có quyền → từ chối, không tiết lộ tiêu đề/nội dung bị hạn chế.
- Tìm kiếm/mô hình lỗi → báo lỗi và cho thử lại; không hiển thị câu trả lời dở dang như hoàn chỉnh.
- Có nhiều phiên bản → áp dụng quy tắc đã cấu hình hoặc yêu cầu chọn; không âm thầm gộp nội dung.
- Không có số trang → hiển thị tài liệu/đoạn xác định được, không bịa vị trí.

## UC-02 — Tìm và duyệt tài liệu

- **Mục tiêu:** Tìm tài liệu theo từ khóa và metadata.
- **Actor:** Sinh viên hoặc giảng viên.
- **Tiền điều kiện:** Tài liệu đã lập chỉ mục và actor có quyền xem.
- **Luồng chính:** nhập từ khóa → chọn bộ lọc tùy chọn → hệ thống tìm trong phạm vi quyền → hiển thị metadata → actor mở tài liệu.
- **Ngoại lệ:** Không có kết quả thì gợi ý bỏ bộ lọc; tài liệu ngoài quyền bị loại; tài liệu lỗi xử lý không được trình bày là sẵn sàng.
- **Yêu cầu:** FR-001, FR-002, FR-008, FR-011.

## UC-03 — Học và ôn tập

- **Mục tiêu:** Hiểu khái niệm hoặc tạo câu hỏi ôn dựa trên tài liệu.
- **Actor:** Sinh viên.
- **Tiền điều kiện:** Có tài liệu trong phạm vi và quyền truy cập hợp lệ.
- **Luồng chính:** chọn môn/tài liệu → chọn giải thích hoặc ôn tập → nhập chủ đề/mức độ nếu cần → hệ thống truy xuất nguồn → tạo nội dung kèm nguồn → sinh viên xem hoặc yêu cầu làm rõ/tạo lại.
- **Ngoại lệ:** Chủ đề ngoài tài liệu thì báo giới hạn; yêu cầu mơ hồ thì hỏi làm rõ; ví dụ AI tạo phải phân biệt với nội dung nguồn.
- **Yêu cầu:** FR-006, FR-007, FR-011, FR-014.

## UC-04 — Nạp tài liệu

- **Mục tiêu:** Đưa tài liệu được phép vào kho phục vụ tìm kiếm/hỏi đáp.
- **Actor:** Quản trị viên/curator.
- **Tiền điều kiện:** Actor được cấp quyền; quyền sử dụng và định dạng hợp lệ.
- **Luồng chính:** chọn tệp → khai báo môn, loại, nguồn, phiên bản, quyền → hệ thống kiểm tra → trích xuất/lập chỉ mục → hiển thị trạng thái → curator duyệt nếu quy trình yêu cầu.
- **Ngoại lệ:** Định dạng không hỗ trợ, tệp hỏng, thiếu metadata/quyền, trùng phiên bản hoặc trích xuất lỗi → không đánh dấu sẵn sàng; hiển thị nguyên nhân.
- **Yêu cầu:** FR-009, FR-010, FR-011.

## UC-05 — Kiểm soát truy cập

- **Mục tiêu:** Chỉ người được phép mới xem hoặc dùng tài liệu làm nguồn.
- **Actor:** Sinh viên, giảng viên, curator; hệ thống xác thực/phân quyền hỗ trợ nếu có.
- **Tiền điều kiện:** Vai trò và quyền tài liệu đã cấu hình.
- **Luồng chính:** hệ thống xác định actor → kiểm tra quyền với tài liệu/phạm vi → cho phép thao tác hợp lệ → ghi nhận sự kiện tối thiểu theo chính sách.
- **Ngoại lệ:** Chưa đăng nhập/hết phiên, quyền không rõ hoặc bị thu hồi → từ chối an toàn; không dùng đoạn đó trong câu trả lời.
- **Yêu cầu:** FR-011; NFR-003, NFR-004.

## UC-06 — Gửi phản hồi/xem lịch sử (tùy phạm vi)

- **Mục tiêu:** Gửi phản hồi chất lượng và xem lại trao đổi.
- **Actor:** Sinh viên hoặc giảng viên.
- **Tiền điều kiện:** Chức năng được bật và chính sách lưu trữ được phê duyệt.
- **Luồng chính:** đánh giá câu trả lời hoặc mở lịch sử → hệ thống lưu/hiển thị dữ liệu đúng actor.
- **Ngoại lệ:** Lưu lỗi thì báo và cho thử lại; lịch sử hết hạn/đã xóa thì không khôi phục; chức năng chưa duyệt thì không thu thập dữ liệu.
- **Yêu cầu:** FR-012, FR-013.

## Traceability và test dự kiến

| Use case | Yêu cầu | Test case dự kiến (chưa chạy) |
|---|---|---|
| UC-01 | FR-001, FR-003–005, FR-011, FR-014 | TC-UC01-01 nguồn đúng; -02 thiếu nguồn; -03 mở trích dẫn; -04 từ chối quyền; -05 lỗi dịch vụ. |
| UC-02 | FR-001, FR-002, FR-008, FR-011 | TC-UC02-01 tìm/lọc; -02 không kết quả; -03 lọc quyền. |
| UC-03 | FR-006–007, FR-011, FR-014 | TC-UC03-01 giải thích có nguồn; -02 ôn tập; -03 chủ đề ngoài nguồn. |
| UC-04 | FR-009–010 | TC-UC04-01 nạp thành công; -02 tệp lỗi; -03 thiếu metadata/quyền. |
| UC-05 | FR-011 | TC-UC05-01 quyền hợp lệ; -02 truy cập chéo; -03 quyền bị thu hồi. |
| UC-06 | FR-012–013 | TC-UC06-01 gửi phản hồi; -02 đúng lịch sử; -03 dữ liệu hết hạn/xóa. |
