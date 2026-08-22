# General Prompt Rules

---

## Định nghĩa
Đây là bộ quy tắc chung áp dụng cho mọi hoạt động tương tác, xử lý thông tin, lập trình, hoặc quản lý tài liệu trong Vault. Quy tắc này có hiệu lực cao nhất và bao trùm tất cả các chủ đề.

---

## 1. Cách hỏi câu hỏi xác thực và uỷ quyền từ người dùng

Mọi câu hỏi tương tác với người dùng để xác nhận hành động hoặc yêu cầu cấp quyền đều phải tuân thủ nghiêm ngặt các định dạng sau:

### 1.1. Ngôn ngữ sử dụng
- Toàn bộ các câu hỏi xác thực hoặc uỷ quyền phải được viết bằng **tiếng Việt** tự nhiên, rõ ràng, dễ hiểu đối với người dùng bình thường không có chuyên môn lập trình.
- **Tuyệt đối không** sử dụng mã lệnh (code block), câu lệnh điều kiện, hay cấu trúc lập trình trong nội dung câu hỏi dưới mọi hình thức.

### 1.2. Quy trình xác thực (Verification / Confirmation)
- Dùng khi cần người dùng xác nhận một hành động cụ thể (ví dụ: xóa file, ghi đè nội dung quan trọng).
- Câu hỏi phải ở dạng lựa chọn **yes/no**.
- **Ví dụ tiêu chuẩn:**
  > Bạn có muốn tôi xoá file `temp_data.csv` không? (yes/no)

### 1.3. Quy trình uỷ quyền (Authorization / Permission Request)
- Dùng khi cần người dùng cho phép thực hiện một quyền hạn cụ thể trước khi thực thi.
- Câu hỏi uỷ quyền bắt buộc phải làm rõ 3 yếu tố sau:
  1. **Quyền muốn được cấp:** (đọc, ghi, xoá, sửa đổi...).
  2. **Đối tượng tác động:** (file, folder hoặc nội dung cụ thể nào).
  3. **Mục đích sử dụng:** (sẽ làm gì với quyền hạn đó và kết quả mong đợi).
- **Ví dụ tiêu chuẩn:**
  > Tôi cần quyền **ghi** vào file `02 - Rules for working with Obsidian folders and notes.md` để **thêm quy tắc xử lý nội dung sai vị trí**. Bạn có đồng ý cấp quyền này không? (yes/no)
