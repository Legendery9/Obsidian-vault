# Markup trong Obsidian

---

## Định nghĩa
Markup là hệ thống ký pháp Markdown (kết hợp các mở rộng riêng của Obsidian) dùng để định dạng văn bản ghi chú.

---

## Tác dụng
- **Tạo cấu trúc rõ ràng:** Phân tách ghi chú thành các cấp tiêu đề và danh sách logic.
- **Tăng tốc ghi chép:** Định dạng văn bản nhanh chóng bằng bàn phím mà không cần chuột.
- **Tương thích cao:** File ghi chú lưu dưới dạng `.md` thuần túy, dễ dàng mở và đọc bằng bất kỳ trình chỉnh sửa văn bản nào.

---

## Bảng tham chiếu

### 1. Định dạng văn bản cơ bản

| Cú pháp | Kết quả hiển thị | Ý nghĩa |
| :--- | :--- | :--- |
| `**Chữ đậm**` | **Chữ đậm** | Nhấn mạnh mạnh mẽ |
| `*Chữ nghiêng*` | *Chữ nghiêng* | Nhấn mạnh nhẹ |
| `==Chữ nổi bật==` | ==Chữ nổi bật== | Highlight thông tin (Obsidian-specific) |
| `~~Chữ gạch ngang~~` | ~~Chữ gạch ngang~~ | Nội dung đã xóa bỏ / lỗi thời |
| ``inline code`` | `inline code` | Định dạng biến, lệnh, hoặc code ngắn trên cùng dòng |

### 2. Danh sách & Checklists

| Cú pháp Markdown | Mô tả |
| :--- | :--- |
| `- Phần tử 1` | Danh sách không thứ tự (Unordered List) |
| `1. Phần tử 1` | Danh sách có thứ tự (Ordered List) |
| `- [ ] Task cần làm` | Checklist nhiệm vụ chưa hoàn thành |
| `- [x] Task đã xong` | Checklist nhiệm vụ đã hoàn thành |

### 3. Liên kết & Hình ảnh (Obsidian)

| Cú pháp | Ví dụ hiển thị | Ý nghĩa |
| :--- | :--- | :--- |
| `[[Tên trang]]` | [[01 - Callout]] | Tạo liên kết nội bộ đến trang khác trong vault |
| `[[Tên trang#Heading]]` | [[01 - Callout#Ví dụ]] | Liên kết trực tiếp đến một Heading cụ thể |
| `[[Tên trang\|Tên hiển thị]]` | [[01 - Callout|Xem callouts]] | Đổi tên hiển thị của liên kết |
| `![[image.png]]` | (Hình ảnh được nhúng trực tiếp) | Nhúng trực tiếp file hình ảnh/tài liệu từ vault |
| `[Google](https://google.com)` | [Google](https://google.com) | Liên kết ngoài (External Link) |

---

## Ví dụ

### Cú pháp tạo Bảng (Table)
```markdown
| Cột 1 | Cột 2 |
| :--- | :--- |
| Nội dung 1 | Nội dung 2 |
```

### Cú pháp tạo Khối mã (Code Block) có Highlight
Sử dụng 3 dấu backticks kèm theo tên ngôn ngữ lập trình ở đầu khối:
````markdown
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```
````

---

## Lưu ý
> [!note] Đóng ngoặc đúng chuẩn
> Mọi liên kết nội bộ `[[...]]` và liên kết ngoài `[...]` cần đảm bảo đóng mở ngoặc đầy đủ để tránh làm đứt gãy định dạng của toàn bộ ghi chú phía dưới.
