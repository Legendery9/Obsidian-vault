## Checklist tổng
- [x] Tạo folder `12 - Combined Practice` trong `01 - Java Core`
- [x] Viết file `01 - Matrix Operations.md` (Tạo, nhập, lấy, cộng, trừ, nhân ma trận) ✅ 2026-08-19
- [x] Viết file `02 - File and Folder Operations.md` (Tạo, ghi, đọc, copy, di chuyển file/folder) ✅ 2026-08-19
- [x] Viết file `03 - Date Validation.md` (Validate chuỗi ngày thành LocalDate với 3 định dạng, xử lý năm nhuận) ✅ 2026-08-19

## Quy tắc áp dụng (tóm tắt)
- **Cấu trúc mỗi file:**
  1. Giải thích và phân tích yêu cầu (bao gồm edge cases).
  2. FLOW hoặc sơ đồ liên kết giữa các statement/method (heading `## FLOW`).
  3. Các thư viện cần sử dụng (import).
  4. Code block hoàn chỉnh, class và method chạy được, viết ngắn gọn (tinh thần 20/80 nhưng code phải hoàn chỉnh).
  5. Tuân thủ `[[01 - Java Code Conventions]]`.
  6. Ghi chú/Lưu ý.
  7. Mỗi hành vi yêu cầu có 1 method riêng biệt để xử lý, không gộp.

## Nhật ký thay đổi
### [2026-08-19 14:14]
- **Đã làm:** Khởi tạo file log tiến trình riêng cho phần Combined Practice.

### [2026-08-19 14:16]
- **Đã làm:**
  - Viết file `01 - Matrix Operations.md` thực hiện các thao tác ma trận chuẩn và kiểm soát ngoại lệ.
  - Viết file `02 - File and Folder Operations.md` triển khai các tác vụ quản lý file bằng NIO.2 kèm đệ quy chuyển đổi folder.
  - Viết file `03 - Date Validation.md` cài đặt validate chuỗi ngày nghiêm ngặt (strict pattern matching) bao gồm xử lý năm nhuận.

## Trạng thái hiện tại
- **Đã hoàn thành:** 100%
- **Đang làm dở / chưa làm tới:** Không có.

## Lưu ý
- Các mã nguồn đều được kiểm tra tính biên dịch chặt chẽ, tối ưu hóa bằng try-with-resources đối với I/O và kiểm tra điều kiện đầu vào (fail-fast) đối với các tham số ma trận/ngày tháng.
