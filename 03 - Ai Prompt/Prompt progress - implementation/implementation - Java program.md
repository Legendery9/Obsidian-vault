## Checklist tổng
- [x] Đọc và lập kế hoạch tái cấu trúc hệ thống tệp
- [x] Viết file `implementation_plan.md` và được người dùng duyệt
- [x] Tạo thư mục con mới: `01 - Java Core`, `02 - Spring Boot`, `03 - JavaFX`
- [x] Tạo các file ghi chú Java Core mới (10 file)
- [x] Tạo các file ghi chú Spring Boot mới (9 file)
- [x] Tạo file ghi chú JavaFX mới (1 file)
- [x] Dọn dẹp và xóa các tệp/thư mục phân mảnh cũ (Xóa 37 file rỗng và các thư mục cũ)
- [x] Đổi tên thư mục cha thành `06 - Java Program` để đồng bộ
- [x] Xác minh hiển thị và liên kết chéo trong Obsidian
- [x] `08 - Java Collections and Containers` — bổ sung các collection còn thiếu
- [x] `08 - Java Collections and Containers` — bảng method/statement đầy đủ cho từng collection
- [x] `09 - Java Advanced Basics` — bảng method/statement đầy đủ cho các thư viện liên quan ✅ 2026-08-16
- [x] `07 - Regex and String Matching` — bảng method/statement đầy đủ cho các thư viện regex/string ✅ 2026-08-16
- [x] `03 - Variables and Data Types` — bảng method/statement đầy đủ cho Wrapper Classes
- [x] Thêm file `11 - Math.md` (hoặc tên phù hợp hơn nếu cần)

## Quy tắc áp dụng (tóm tắt)
- **Chuẩn hóa đặt tên:** Sử dụng định dạng `{index} - {context}` cho thư mục và tệp tin.
- **Khử trùng lặp:** Không lặp lại kiến thức, dùng Obsidian wikilink `[[tên-file]]` để tham chiếu.
- **Nguyên tắc 20/80:** Nội dung ngắn gọn, tập trung 20% cốt lõi đem lại 80% giá trị.
- **Định dạng Visual:** Phân tách heading bằng `---`. Sử dụng callouts thích hợp (`[!abstract]`, `[!info]`, `[!warning]`, `[!note]`). Ví dụ code dùng block `java` và trình bày đối lập Do/Don't.

## Nhật ký thay đổi
### [2026-08-16 10:30]
- **Đã làm:** Phân tích vault, lập kế hoạch chi tiết, khởi tạo task list và file tiến trình.
- **Đã thêm:** Khởi tạo `03 Ai Prompt/Prompt progress/implementation.md`.

### [2026-08-16 10:36]
- **Đã làm:** 
  - Tạo cấu trúc thư mục mới: `01 - Java Core`, `02 - Spring Boot`, `03 - JavaFX`.
  - Tạo và hoàn thiện 10 file ghi chú chất lượng cao cho `01 - Java Core` (hợp nhất từ 28 file phân mảnh).
  - Tạo và hoàn thiện 9 file ghi chú chất lượng cao cho `02 - Spring Boot` (hợp nhất từ 68 file phân mảnh).
  - Tạo và hoàn thiện 1 file ghi chú chất lượng cao cho `03 - JavaFX` (hợp nhất từ 9 file rỗng/phân mảnh).
  - Xóa bỏ hoàn toàn 37 file rỗng (0 bytes) và các thư mục cũ `01 1.Java overall`, `02 2.Spring web`, `03 6.JavaFX`.
  - Đổi tên thư mục gốc từ `06 Java Program` sang `06 - Java Program`.
  - Cập nhật nhật ký tiến trình.
- **Đã thay đổi:** Định dạng và cấu trúc lại toàn bộ vault phần Java Program.

### [2026-08-16 11:25]
- **Đã làm:** Bắt đầu phiên làm việc thứ hai để bổ sung chi tiết các collection còn thiếu, bảng method tham chiếu đầy đủ cho Collections, Advanced Basics, Regex, Wrapper Classes và thêm file Math mới.

### [2026-08-16 11:32]
- **Đã làm:**
  - Tạo thư mục con mới `08 - Java Collections and Containers` trong `01 - Java Core/` và viết 19 file ghi chú chi tiết về các collection.
  - Cập nhật tệp `09 - Java Advanced Basics.md` với bảng phương thức cho Stream API, Files, Path, BufferedReader, và ImageIO.
  - Cập nhật tệp `07 - Regex and String Matching.md` với bảng API cho Pattern, Matcher, String Regex API và cú pháp Regex.
  - Cập nhật tệp `03 - Variables and Data Types.md` với bảng phương thức cho các Wrapper Classes (Integer, Double, Long, Character, Boolean).
  - Tạo tệp `11 - Math and Numbers.md` chứa hằng số và phương thức của lớp `Math`.
- **Đã thay đổi:** Nâng cấp chi tiết kỹ thuật cho toàn bộ tệp ghi chú Java Core.

## Trạng thái hiện tại
- **Đã hoàn thành:** 100% checklist và yêu cầu bổ sung của vault "06 - Java Program".
- **Đang làm dở / chưa làm tới:** Không có.

## Lưu ý
- Đã sửa lỗi logic quan trọng trong phần HTTP Status Code (đảo ngược mã 400 và 404 trong tệp HTML gốc).
- Đã thêm cấu hình mẫu try-with-resources để giải phóng tài nguyên File I/O và nguyên tắc sử dụng hằng số an toàn với Wrapper Classes.
- Lưu ý đặc biệt về `Math.round` với số thực âm đã được đưa vào tệp Math.
