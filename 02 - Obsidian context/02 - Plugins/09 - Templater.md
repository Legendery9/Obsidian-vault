# Templater trong Obsidian

---

## Định nghĩa
Templater là một plugin khởi tạo mẫu ghi chú nâng cao, cho phép bạn tự động hóa việc chèn ngày tháng, tên tiêu đề file, các biến hệ thống hoặc thậm chí chạy code JavaScript để tạo ra các cấu trúc nội dung động.

---

## Tác dụng
- **Tự động điền dữ liệu:** Điền tiêu đề, ngày giờ tạo, thư mục lưu trữ ngay khi tạo ghi chú mới.
- **Tiêu chuẩn hóa ghi chú:** Đảm bảo mọi file ghi chú của cùng một chủ đề (Ví dụ: bài học, dự án) đều có chung một cấu trúc chuẩn.
- **Tích hợp mạnh mẽ:** Hỗ trợ chạy các câu lệnh JS trực tiếp trong file template để thao tác với các file hệ thống hoặc API ngoài.

---

## Bảng tham chiếu

### Các thẻ lệnh cơ bản của Templater

| Cú pháp thẻ lệnh | Ý nghĩa chức năng |
| :--- | :--- |
| `<% tp.file.title %>` | Lấy tiêu đề hiện tại của file ghi chú |
| `<% tp.file.creation_date("YYYY-MM-DD") %>` | Lấy ngày tạo file theo định dạng mong muốn |
| `<% tp.date.now("YYYY-MM-DD HH:mm") %>` | Lấy thời gian hiện tại khi chèn template |
| `<% tp.web.daily_quote() %>` | Tự động lấy một câu trích dẫn ngẫu nhiên trên Internet |
| `<%* ... %>` | Môi trường viết mã JavaScript để thực thi logic (JS Execution Command) |

---

## Ví dụ
Cấu trúc một Template ghi chú học tập hàng ngày:
```markdown
---
date: <% tp.file.creation_date("YYYY-MM-DD HH:mm") %>
tag: learning
---
# Ghi chú: <% tp.file.title %>

---
## Mục tiêu bài học hôm nay
- [ ] 

## Nội dung chi tiết
```

---

## Lưu ý
> [!warning] Cách chạy Templater
> Hãy đảm bảo bạn cấu hình thư mục chứa các Template của mình trong phần cài đặt của plugin Templater và sử dụng phím tắt (mặc định: `Alt + N` để mở danh sách chọn chèn template nhanh).
