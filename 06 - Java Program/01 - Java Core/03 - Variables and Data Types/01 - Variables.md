# Java Variables

> [!abstract] Định nghĩa
> **Biến (Variable)** là một vùng nhớ được định danh dùng để lưu trữ dữ liệu tạm thời trong quá trình thực thi chương trình. Biến phải được khai báo kèm theo một kiểu dữ liệu cụ thể (xem chi tiết tại [[02 - Data Types]]).

---

## 1. Phân loại biến theo Phạm vi (Scopes)

Trong Java, phạm vi hoạt động và thời gian sống của biến được xác định bởi vị trí khai báo của chúng:

| Loại biến | Vị trí khai báo | Phạm vi hoạt động | Lưu trữ tại bộ nhớ | Giá trị mặc định |
| --- | --- | --- | --- | --- |
| **Local Variable** | Trong phương thức, constructor hoặc block lệnh `{}`. | Chỉ bên trong cặp ngoặc `{}` khai báo biến. | **Stack Memory** | Không có (Bắt buộc phải khởi tạo giá trị trước khi dùng). |
| **Instance Variable** | Trong class, bên ngoài các phương thức. | Trong toàn bộ đối tượng (Object instance). | **Heap Memory** | Có (Số = `0`, Boolean = `false`, Object = `null`). |
| **Static Variable** | Trong class kèm theo từ khóa `static`. | Trong toàn bộ lớp, các đối tượng dùng chung một vùng nhớ. | **Method Area** | Có giá trị mặc định giống Instance Variable. |
| **Parameter** | Trong danh sách tham số phương thức. | Chỉ sử dụng được trong phương thức nhận tham số. | **Stack Memory** | Không có (Nhận giá trị khi phương thức được gọi). |

---

## 2. Phân biệt bộ nhớ Stack và Heap

Các biến được lưu trữ tại các phân vùng bộ nhớ khác nhau tùy theo phân loại của chúng:

| Đặc tính | Bộ nhớ Stack | Bộ nhớ Heap |
| --- | --- | --- |
| **Dữ liệu lưu trữ** | Các biến cục bộ (Local variables), tham số (parameters), và các lệnh gọi hàm. | Tất cả đối tượng (Objects) và các biến thực thể (Instance variables) của đối tượng đó. |
| **Cơ chế hoạt động** | LIFO (Last In First Out), tự giải phóng vùng nhớ khi phương thức kết thúc. | Quản lý tự động bởi Garbage Collector (Bộ dọn rác) khi đối tượng không còn tham chiếu nào trỏ tới. |
| **Tốc độ truy cập** | Cực kỳ nhanh. | Chậm hơn do cần giải quyết địa chỉ tham chiếu. |
| **Dung lượng** | Giới hạn nhỏ (Dễ gặp lỗi `StackOverflowError` khi đệ quy vô hạn). | Rất lớn (Dễ gặp lỗi `OutOfMemoryError` khi tạo quá nhiều đối tượng mà không được giải phóng). |
