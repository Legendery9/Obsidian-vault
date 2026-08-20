# Excel to Markdown Table trong Obsidian

---

## Định nghĩa
Excel to Markdown Table là một plugin tiện ích giúp tự động chuyển đổi dữ liệu được sao chép (Copy) từ Microsoft Excel, Google Sheets, hoặc LibreOffice Calc thành bảng định dạng Markdown chuẩn khi dán (Paste) vào Obsidian.

---

## Tác dụng
- **Tiết kiệm thời gian:** Không cần phải viết thủ công từng ký tự `|` hay `-` khi muốn tạo bảng từ nguồn dữ liệu có sẵn.
- **Giữ nguyên cấu trúc:** Chuyển đổi chính xác số hàng, số cột và nội dung text từ bảng tính sang Markdown.
- **Tiện lợi:** Hoạt động ngầm ngay khi thực hiện thao tác dán thông thường (`Ctrl + V`).

---

## Bảng tham chiếu

### Cách hoạt động & Phím tắt liên quan

| Thao tác nguồn | Thao tác đích | Kết quả |
| :--- | :--- | :--- |
| **Ctrl + C** (Tại Excel/Google Sheets) | **Ctrl + V** (Tại Obsidian) | Tự động chuyển đổi thành bảng Markdown |
| **Ctrl + C** (Tại Excel/Google Sheets) | **Ctrl + Shift + V** (Tại Obsidian) | Dán văn bản thô dạng tab-separated (không tạo bảng) |

---

## Ví dụ
Dữ liệu copy từ Excel:
```tsv
Môn học	Điểm
Toán	9
Văn	8
```
Khi nhấn `Ctrl + V` trong Obsidian, plugin tự động biên dịch thành:
```markdown
| Môn học | Điểm |
| :--- | :--- |
| Toán | 9 |
| Văn | 8 |
```

---

## Lưu ý
> [!warning] Lỗi xuống dòng trong ô
> Nếu một ô (cell) trong Excel chứa dữ liệu có ký tự xuống dòng (Alt + Enter), bảng Markdown sau khi dán có thể bị lỗi vỡ hàng. Nên loại bỏ xuống dòng trong ô trước khi copy.
