# Software Requirements Specification (SRS)

**Tên hệ thống:** Kho tri thức hỗ trợ học thuật  
**Phiên bản:** 0.1 — bản nháp  
**Trạng thái:** Chờ nhóm xác nhận phạm vi, dữ liệu và tiêu chí  
**Ngày:** 18/11/2026  
**Nguồn:** Mô tả đề tài của người dùng; PROJECT_BRIEF.md chưa được điền.

## 1. Giới thiệu

### 1.1 Mục đích

Tài liệu mô tả yêu cầu phần mềm sơ bộ cho nền tảng hỗ trợ sinh viên và giảng viên tìm, hiểu, hỏi đáp và ôn tập dựa trên kho tài liệu học thuật. Đây là căn cứ phối hợp cho product, BA, design, engineering và QA; chưa phải baseline được phê duyệt.

### 1.2 Phạm vi sản phẩm

- **Academic Assistant:** hỏi đáp chuyên sâu theo môn/tài liệu, có nguồn dẫn.
- **Learning Assistant:** giải thích khái niệm và gợi ý ôn tập dựa trên tài liệu.
- **Knowledge Hub:** tìm kiếm, duyệt và tổng hợp tài liệu.

**Giả định MVP:** ưu tiên một luồng hỏi đáp có trích dẫn, mở được nguồn và xử lý được trường hợp thiếu nguồn. Quản lý tài liệu có thể dùng corpus nạp sẵn. Phạm vi này phải được PO/người phụ trách xác nhận.

### 1.3 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| RAG | Tìm nội dung liên quan trong kho trước khi mô hình tạo câu trả lời. |
| Tài liệu nguồn | Giáo trình, slide, đề cương hoặc tài liệu tham khảo được phép sử dụng. |
| Trích dẫn | Liên kết tới tài liệu/đoạn hỗ trợ cho câu trả lời. |
| Curator | Người quản lý hoặc duyệt tài liệu trong kho. |

### 1.4 Tài liệu liên quan

- `requirements.md`: danh sách FR/NFR và quy tắc nghiệp vụ.
- `assumptions-risk-register.md`: giả định, rủi ro và quyết định cần chốt.
- `use-cases.md`: luồng sử dụng và ngoại lệ.

## 2. Mô tả tổng thể

### 2.1 Actor

Sinh viên tìm/hỏi/học/ôn; giảng viên tìm hoặc cung cấp tài liệu; quản trị viên/curator quản lý tài liệu. Danh tính, vai trò, quyền và tích hợp SSO chưa được xác nhận.

### 2.2 Môi trường vận hành

**TBD:** web hay mobile, trình duyệt, hosting, cơ sở dữ liệu/kho vector, mô hình AI/API, xác thực, môi trường demo/production. Không giả định stack cụ thể.

### 2.3 Ràng buộc và giả định

- Chỉ dùng tài liệu có quyền truy cập/quyền sử dụng hợp lệ.
- Mục tiêu đề tài nêu ≥80% trên tập test; định nghĩa và kết quả chưa có.
- Tài liệu truy xuất là dữ liệu không đáng tin đối với chỉ dẫn hệ thống; tài liệu không được tự cấp quyền hay gọi công cụ.
- Yêu cầu pháp lý, chính sách dữ liệu và điều kiện dịch vụ ngoài cần đơn vị có thẩm quyền xác nhận.

## 3. Yêu cầu giao diện ngoài

### 3.1 Giao diện người dùng

Giao diện dự kiến gồm: chọn môn/phạm vi, ô tìm kiếm/nhập câu hỏi, trạng thái xử lý, câu trả lời, trích dẫn mở được, thông báo thiếu nguồn/lỗi và phản hồi tùy chọn. Giao diện curator chỉ nằm trong MVP nếu được xác nhận. Tiếng Việt là ngôn ngữ dự kiến.

### 3.2 Giao diện phần mềm và truyền thông

Có thể cần kết nối mô hình ngôn ngữ, kho tài liệu/tìm kiếm và xác thực. Nhà cung cấp, API, giao thức, định dạng tải tệp, giới hạn kích thước, timeout, retry và mã lỗi đều **TBD**; sẽ được bổ sung sau quyết định kiến trúc.

## 4. Yêu cầu chức năng cấp hệ thống

Danh sách chuẩn nằm trong `requirements.md`:

1. Chọn phạm vi, tìm và duyệt tài liệu: FR-001, FR-002, FR-008.
2. Hỏi đáp, trích dẫn, xử lý thiếu nguồn: FR-003–005, FR-014.
3. Giải thích/ôn tập: FR-006–007.
4. Nạp và lập chỉ mục: FR-009–010.
5. Phân quyền: FR-011.
6. Phản hồi/lịch sử tùy phạm vi: FR-012–013.

### 4.1 Luồng hỏi đáp chuẩn

1. Người dùng chọn môn/phạm vi tài liệu.
2. Người dùng nhập câu hỏi.
3. Hệ thống xác minh quyền và truy xuất đoạn liên quan trong phạm vi.
4. Hệ thống xác định bằng chứng có đủ để trả lời hay không.
5. Nếu đủ, hệ thống tạo câu trả lời kèm trích dẫn; nếu thiếu, nêu rõ giới hạn.
6. Người dùng mở trích dẫn để đối chiếu.

## 5. Yêu cầu dữ liệu

### 5.1 Thực thể dự kiến

- **User:** định danh, vai trò, quyền môn học (nếu cần xác thực).
- **Course/Scope:** mã, tên, trạng thái.
- **Document:** mã, tiêu đề, loại, môn, nguồn/chủ sở hữu, phiên bản, ngày hiệu lực, quyền, trạng thái xử lý.
- **Passage:** mã đoạn, tài liệu/phiên bản, nội dung trích xuất, trang/slide nếu xác định được.
- **Question/Answer:** câu hỏi, câu trả lời, nguồn, thời điểm, trạng thái và phản hồi nếu bật lưu.

### 5.2 Chất lượng và vòng đời

Phải giữ liên kết đoạn trích về đúng tài liệu và phiên bản; trạng thái xử lý phải phản ánh đúng; dữ liệu lỗi không được trình bày là sẵn sàng. Thời hạn lưu, sao lưu, xóa, phân loại dữ liệu và quyền sử dụng còn TBD, cần chốt trước khi dùng dữ liệu thật.

## 6. Yêu cầu phi chức năng

- **NFR-001 Chất lượng AI:** mục tiêu đề tài ≥80% trên tập test; rubric/cách tính/cỡ mẫu TBD. Đánh giá riêng độ đúng câu trả lời và trích dẫn.
- **NFR-002 Hiệu năng:** latency, tải đồng thời, kích thước tệp TBD.
- **NFR-003 Bảo mật:** không truy xuất/trả tài liệu vượt quyền; kiểm tra quyền ở mọi đường truy cập.
- **NFR-004 Riêng tư:** tối thiểu hóa dữ liệu; không gửi dữ liệu nhạy cảm ra dịch vụ ngoài khi chưa được duyệt; retention/xóa TBD.
- **NFR-005 Khả dụng:** trạng thái, lỗi, thiếu nguồn hiển thị rõ; hỗ trợ tiếng Việt là yêu cầu dự kiến.
- **NFR-006 Truy vết:** xác định được tài liệu/phiên bản/đoạn làm nguồn trong giới hạn log được duyệt.
- **NFR-007 Tương thích:** nền tảng, trình duyệt và định dạng hỗ trợ TBD.
- **NFR-008 Chi phí:** ngân sách/lượt và giới hạn gọi mô hình TBD.

## 7. Tiêu chí nghiệm thu cấp hệ thống

1. Người dùng có quyền hỏi trên tài liệu đã nạp và nhận câu trả lời kèm nguồn mở được.
2. Khi thiếu bằng chứng, hệ thống báo rõ; không tạo nội dung hoặc trích dẫn giả.
3. Test truy cập chéo chứng minh người dùng không lấy được tài liệu ngoài quyền.
4. Có bộ test đóng băng và rubric được duyệt; chỉ kết luận đạt ≥80% sau khi đo và lưu bằng chứng thực tế.
5. Nạp tài liệu thể hiện đúng trạng thái thành công/thất bại; dữ liệu lỗi không được đánh dấu sẵn sàng.

## 8. Traceability và điểm mở

Liên kết chi tiết Use Case → yêu cầu → test nằm trong `use-cases.md` và `requirements.md`. Trước khi baseline, nhóm cần xác nhận: MVP, actor/quyền, nguồn và định dạng dữ liệu, cách tính ≥80%, nền tảng, hiệu năng, chính sách dữ liệu và ngân sách.
