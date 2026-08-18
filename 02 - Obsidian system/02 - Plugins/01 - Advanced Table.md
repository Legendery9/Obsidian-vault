# Advanced Tables in Obsidian

---

## Định nghĩa
Advanced Tables là một plugin bên thứ ba giúp tối ưu hóa việc tạo, chỉnh sửa và định dạng bảng dữ liệu trong Obsidian một cách tự động.

---

## Tác dụng
- **Tự động căn chỉnh:** Định dạng độ rộng cột tự động dựa trên độ dài của văn bản bên trong khi gõ.
- **Dễ dàng điều hướng:** Dùng phím `Tab` và `Enter` để nhảy qua lại giữa các ô và các dòng giống như Excel.
- **Thao tác nhanh:** Thêm, xóa, di chuyển cột/dòng bằng các phím tắt nhanh.
- **Sắp xếp dữ liệu:** Hỗ trợ sort dữ liệu của bảng theo cột tăng/giảm dần.

---

## Bảng tham chiếu

### Phím tắt thao tác bảng nhanh

| Tổ hợp phím | Hành động | Tác dụng |
| :--- | :--- | :--- |
| `Tab` | Nhảy sang ô bên phải | Chuyển đến ô tiếp theo và định dạng lại bảng |
| `Shift + Tab` | Nhảy sang ô bên trái | Quay lại ô phía trước |
| `Enter` | Xuống dòng dưới | Tạo dòng mới ngay dưới dòng hiện tại |
| `Alt + Mũi tên Lên/Xuống` | Di chuyển dòng | Đổi vị trí dòng hiện tại lên trên hoặc xuống dưới |
| `Alt + Mũi tên Trái/Phải` | Di chuyển cột | Đổi vị trí cột hiện tại sang trái hoặc sang phải |
| `Ctrl + Alt + D` | Delete Row | Xóa dòng hiện tại |
| `Ctrl + Alt + C` | Delete Column | Xóa cột hiện tại |

---

## Ví dụ
Khi gõ cú pháp tạo bảng thô:
```markdown
|Tên|Tuổi|
|---|---|
|An|20|
```
Nhấn phím `Tab` tại bất kỳ ô nào, Advanced Tables sẽ tự động định dạng thành:
```markdown
| Tên | Tuổi |
| :-- | :--- |
| An  | 20   |
```

---

## Lưu ý
> [!info] Bật tính năng
> Đảm bảo phím tắt hoạt động bằng cách kiểm tra nút bảng phụ trợ ở thanh công cụ bên phải (Advanced Tables Sidebar) sau khi cài đặt plugin.
