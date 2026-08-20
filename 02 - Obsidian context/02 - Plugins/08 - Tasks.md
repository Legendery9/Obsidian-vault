# Tasks trong Obsidian

---

## Định nghĩa
Tasks là plugin quản lý tác vụ toàn diện cho phép theo dõi, thêm thuộc tính (ngày đến hạn, ngày bắt đầu, độ ưu tiên, độ lặp lại) và truy vấn các checklist nhiệm vụ (`- [ ]`) trên toàn bộ vault.

---

## Tác dụng
- **Quản lý nhiệm vụ tập trung:** Ghi nhiệm vụ rải rác ở các file bài học khác nhau nhưng hiển thị tập trung tại một trang Dashboard duy nhất.
- **Thêm siêu dữ liệu cho tác vụ:** Thiết lập deadline, lịch nhắc nhở trực quan.
- **Truy vấn mạnh mẽ:** Lọc các task cần làm trong ngày hôm nay, hoặc các task đã quá hạn.

---

## Bảng tham chiếu

### Các ký hiệu thuộc tính của Task

| Biểu tượng thuộc tính | Tên thuộc tính | Mô tả |
| :--- | :--- | :--- |
| `📅 YYYY-MM-DD` | Due date | Ngày phải hoàn thành nhiệm vụ |
| `⏳ YYYY-MM-DD` | Scheduled date | Ngày dự kiến bắt đầu làm |
| `🛫 YYYY-MM-DD` | Start date | Ngày thực tế bắt đầu thực hiện |
| `➕ YYYY-MM-DD` | Created date | Ngày khởi tạo task |
| `🔁 every day/week` | Recurrence | Nhiệm vụ lặp lại định kỳ |
| `🔺`, `🔼`, `🔽` | Priority | Độ ưu tiên (Cao, Trung bình, Thấp) |

---

## Ví dụ

### Cú pháp tạo Task đầy đủ thuộc tính
```markdown
- [ ] Hoàn thành bài tập SQL 📅 2026-08-20 ⏳ 2026-08-19 🔺
```

### Cú pháp Truy vấn Task cần làm trong tuần này
```tasks
not done
due before 2026-08-25
sort by due
```

---

## Lưu ý
> [!important] Kích hoạt chế độ gõ nhanh
> Sử dụng tổ hợp phím tắt nhanh (mặc định là `Ctrl + Alt + T` hoặc cấu hình trong Hotkeys) để mở hộp thoại điền thông tin tác vụ một cách trực quan mà không cần gõ emoji thuộc tính bằng tay.
