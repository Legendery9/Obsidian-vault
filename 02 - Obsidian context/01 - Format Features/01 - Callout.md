# Callout trong Obsidian

---

## Định nghĩa
Callouts là các hộp thông tin được định dạng đặc biệt nhằm làm nổi bật nội dung trong Obsidian. Chúng giúp phân tách thông tin quan trọng khỏi luồng văn bản chính bằng màu sắc và biểu tượng trực quan.

---

## Tác dụng
- **Tăng tính trực quan:** Giúp người đọc dễ dàng quét qua các phần ghi chú quan trọng.
- **Phân loại thông tin:** Tự động phân chia thông tin thành các nhóm chức năng khác nhau (ghi chú, cảnh báo, ví dụ, câu hỏi).
- **Tiết kiệm không gian:** Hỗ trợ tính năng thu gọn/mở rộng để ẩn bớt nội dung dài.

---

## Bảng tham chiếu

| Loại Callout | Từ khóa (Syntax) | Ý nghĩa & Mục đích sử dụng | Màu sắc hiển thị |
| :--- | :--- | :--- | :--- |
| **Ghi chú** | `[!note]` | Thông tin bổ sung, ghi chú bên lề | Xanh dương nhạt |
| **Tóm tắt** | `[!abstract]`, `[!summary]`, `[!tldr]` | Tóm tắt ý chính, phần đọc nhanh | Xanh lục nhạt / Teal |
| **Thông tin** | `[!info]` | Thông tin bổ trợ chi tiết | Xanh dương |
| **Gợi ý** | `[!todo]` | Việc cần làm, nhiệm vụ cần hoàn thành | Xanh dương đậm |
| **Mẹo / Tip** | `[!tip]`, `[!hint]`, `[!important]` | Lời khuyên, mẹo nhỏ, thông tin quan trọng | Xanh lá |
| **Thành công** | `[!success]`, `[!check]`, `[!done]` | Kết quả đúng, nhiệm vụ đã hoàn tất | Xanh lá đậm |
| **Câu hỏi** | `[!question]`, `[!help]`, `[!faq]` | Câu hỏi cần giải đáp, hỗ trợ | Vàng / Cam |
| **Cảnh báo** | `[!warning]`, `[!caution]`, `[!attention]` | Lưu ý quan trọng, cần cẩn trọng | Cam / Đỏ |
| **Thất bại** | `[!failure]`, `[!fail]`, `[!missing]` | Lỗi, phần thiếu sót | Đỏ |
| **Nguy hiểm** | `[!danger]`, `[!error]` | Cảnh báo nghiêm trọng, nguy hiểm | Đỏ đậm |
| **Lỗi hệ thống** | `[!bug]` | Lỗi code, lỗi hệ thống cần fix | Đỏ tươi |
| **Trích dẫn** | `[!quote]`, `[!cite]` | Trích dẫn câu nói, tài liệu | Xám |
| **Ví dụ** | `[!example]` | Ví dụ minh họa thực tế | Tím |

---

## Ví dụ

### Cú pháp viết Callout cơ bản
```markdown
> [!note] Tiêu đề ghi chú
> Đây là nội dung bên trong của callout ghi chú.
> Có thể xuống dòng bằng cách tiếp tục sử dụng ký tự `>`.
```

### Ví dụ Callout có thể thu gọn (Foldable)
- Thêm dấu `-` ngay sau từ khóa để mặc định **thu gọn**:
  ```markdown
  > [!info]- Tiêu đề mặc định thu gọn
  > Nội dung này sẽ ẩn đi cho đến khi click mở.
  ```
- Thêm dấu `+` ngay sau từ khóa để mặc định **mở**:
  ```markdown
  > [!info]+ Tiêu đề mặc định mở
  > Nội dung này sẽ luôn hiển thị ban đầu và có thể đóng lại.
  ```

---

## Lưu ý
> [!warning] Quy tắc viết Callout đúng chuẩn
> - Luôn có khoảng trắng giữa dấu ngoặc vuông đóng `]` và tiêu đề callout (Ví dụ: `> [!tip] Mẹo nhỏ` thay vì `> [!tip]Mẹo nhỏ`).
> - Có thể lồng các callout vào nhau bằng cách tăng số lượng ký tự `>` (Ví dụ: `>> [!warning]`).
