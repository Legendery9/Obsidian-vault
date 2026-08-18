# Latex Suite trong Obsidian

---

## Định nghĩa
Latex Suite là một plugin hỗ trợ soạn thảo nâng cao dành cho những ai thường xuyên viết công thức toán học bằng LaTeX trong Obsidian. Nó hoạt động bằng cách cung cấp các snippets (đoạn viết tắt) và cơ chế tự động điền (auto-complete) thông minh.

---

## Tác dụng
- **Tốc độ gõ vượt trội:** Chuyển đổi các từ khóa viết tắt ngắn thành cú pháp LaTeX phức tạp ngay lập tức.
- **Tự động đóng ngoặc thông minh:** Tự động hoàn thành các cặp ngoặc phức tạp như `\left( ... \right)`.
- **Rút gọn thao tác:** Giảm số lần gõ phím xuống tới 60-70% khi viết các công thức phức tạp.

---

## Bảng tham chiếu

### Các Snippets mặc định phổ biến trong Latex Suite

| Từ khóa gõ tắt | Kết quả LaTeX | Ký hiệu hiển thị |
| :--- | :--- | :--- |
| `mk` | `$...$` | Tạo Inline Math |
| `dm` | `$$ ... $$` | Tạo Block Math |
| `//` | `\frac{}{}` | Phân số nhanh |
| `sr` | `\sqrt{}` | Căn bậc hai |
| `sq` | `^2` | Lũy thừa 2 (Bình phương) |
| `cb` | `^3` | Lũy thừa 3 (Lập phương) |
| `lim` | `\lim_{x \to \infty}` | Giới hạn |
| `sum` | `\sum_{i=1}^{n}` | Tổng Sigma |

---

## Ví dụ
- Thay vì gõ: `$$ \frac{x}{y} $$`
- Bạn chỉ cần gõ trong môi trường toán học: `x//y` + phím `Tab` → hệ thống tự động sinh ra: `\frac{x}{y}`.
- Để viết căn bậc hai của x, chỉ cần gõ `srx` + phím `Tab` → tự động chuyển thành `\sqrt{x}`.

---

## Lưu ý
> [!tip] Tùy chỉnh Snippets riêng
> Bạn có thể mở phần cài đặt của Latex Suite để định nghĩa thêm các snippets cá nhân hóa trong mục cấu hình JSON của plugin tùy theo nhu cầu học tập hoặc nghiên cứu của mình.
