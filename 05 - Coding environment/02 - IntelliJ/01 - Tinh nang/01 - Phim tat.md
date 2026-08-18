# Phím tắt IntelliJ IDEA

---

## Định nghĩa
IntelliJ IDEA là một môi trường phát triển tích hợp (IDE) chuyên dụng cho ngôn ngữ Java và các ngôn ngữ máy ảo JVM (Kotlin, Scala, Groovy), được phát triển bởi JetBrains.

---

## Tác dụng
- **Tối ưu hiệu năng viết code:** Hệ thống gợi ý thông minh (Smart Completion) và sửa lỗi tự động giúp lập trình viên viết code nhanh và ít lỗi hơn.
- **Tiết kiệm thời gian thao tác:** Sử dụng thuần thục phím tắt giúp hạn chế dùng chuột, tập trung tối đa vào luồng tư duy lập trình.

---

## Bảng tham chiếu

### 1. Tìm kiếm & Di chuyển nhanh

| Tính năng | Phím tắt | Tác dụng thực tế |
| :--- | :--- | :--- |
| **Search Everywhere** | `Shift` (nhấn 2 lần) | Tìm kiếm mọi thứ: Class, File, Settings, Actions... |
| **Find Action** | `Ctrl + Shift + A` | Tìm nhanh một tính năng/lệnh của IDE mà không nhớ menu |
| **Navigate to Class** | `Ctrl + N` | Tìm nhanh một class Java trong toàn project |
| **Navigate to File** | `Ctrl + Shift + N` | Tìm nhanh bất kỳ tệp tin nào (XML, Properties, MD...) |
| **Go to Declaration** | `Ctrl + B` (hoặc `Ctrl + Click`) | Đi đến nơi khai báo của biến, hàm hoặc class |
| **Go to Implementation**| `Ctrl + Alt + B` | Nhảy trực tiếp đến class triển khai (implement) interface |
| **Find Usages** | `Alt + F7` | Liệt kê tất cả những nơi đang sử dụng class/hàm/biến này |
| **Recent Files** | `Ctrl + E` | Mở danh sách các file vừa chỉnh sửa gần đây |

### 2. Sinh Code & Tái cấu trúc (Refactoring)

| Tính năng | Phím tắt | Tác dụng thực tế |
| :--- | :--- | :--- |
| **Generate Code** | `Alt + Insert` | Sinh nhanh Constructor, Getter/Setter, `toString()`, `equals()`... |
| **Quick Fix / Intentions**| `Alt + Enter` | Tự động sửa lỗi, import thư viện, sửa gợi ý cảnh báo |
| **Rename** | `Shift + F6` | Đổi tên biến/hàm/class an toàn trên phạm vi toàn project |
| **Reformat Code** | `Ctrl + Alt + L` | Định dạng căn lề thụt dòng chuẩn hóa code tự động |
| **Optimize Imports** | `Ctrl + Alt + O` | Dọn dẹp, xóa bỏ các import thừa và sắp xếp lại gọn gàng |
| **Surround With** | `Ctrl + Alt + T` | Bọc nhanh khối code trong `if-else`, `try-catch`, `for`... |
| **Extract Method** | `Ctrl + Alt + M` | Tách đoạn code được bôi đen thành một hàm riêng biệt |
| **Extract Variable** | `Ctrl + Alt + V` | Tách biểu thức tính toán thành một biến độc lập |

### 3. Debug & Kiểm thử

| Tính năng | Phím tắt | Tác dụng thực tế |
| :--- | :--- | :--- |
| **Start Debug** | `Shift + F9` | Chạy chương trình ở chế độ gỡ lỗi (Debug mode) |
| **Step Over** | `F8` | Đi tới dòng tiếp theo (không chui vào hàm) |
| **Step Into** | `F7` | Đi sâu vào bên trong thân hàm đang gọi |
| **Evaluate Expression** | `Alt + F8` | Tính toán giá trị hoặc chạy thử mã Java trực tiếp khi đang dừng ở breakpoint |
| **Resume Program** | `F9` | Tiếp tục chạy chương trình cho đến breakpoint tiếp theo |

---

## Ví dụ

### Ví dụ về Postfix Completion (Gõ tắt thông minh)
Trong IntelliJ, bạn có thể biến một biểu thức thành cấu trúc code hoàn chỉnh bằng cách gõ đuôi:
- Gõ: `list.for` + `Tab` → Tự động tạo vòng lặp: `for (Object o : list) {}`
- Gõ: `obj.null` + `Tab` → Tự động tạo check null: `if (obj == null) {}`
- Gõ: `true.if` + `Tab` → Tự động tạo: `if (true) {}`

---

## Lưu ý
> [!tip] Tra cứu phím tắt nhanh
> Để xem và thay đổi toàn bộ phím tắt hoặc chuyển đổi sơ đồ phím tắt sang kiểu Eclipse/NetBeans, bạn truy cập: **File** → **Settings** → **Keymap**.