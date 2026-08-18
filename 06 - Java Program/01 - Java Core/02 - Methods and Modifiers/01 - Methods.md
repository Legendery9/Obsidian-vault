# Java Methods

> [!abstract] Định nghĩa
> **Method (Phương thức)** là một khối mã lệnh thực hiện một công việc cụ thể, có khả năng tái sử dụng cao và được gọi thông qua tên của phương thức đó. Phương thức có thể đi kèm các từ khóa bổ nghĩa để tùy chỉnh hành vi và tầm vực hoạt động (xem chi tiết tại [[02 - Modifiers]]).

---

## Các thành phần cấu trúc phương thức trong Class

Mặc dù được định nghĩa trực tiếp trong Class, các thành phần sau đóng vai trò định hình hành vi và dữ liệu cho phương thức hoặc đối tượng:

| Thành phần | Đặc điểm | Tác dụng | Ví dụ |
| --- | --- | --- | --- |
| `main()` | `public static void main(String[] args)` | Điểm khởi chạy của chương trình (chạy đầu tiên bởi JVM). | `public static void main(...)` |
| **Constructor** | Trùng tên class hoàn toàn, không có kiểu trả về. | Khởi tạo đối tượng (object) trong Heap memory. | `User(String name) { this.name = name; }` |
| **Field** | Khai báo trong class ngoài method. | Lưu trữ thuộc tính/trạng thái dữ liệu của đối tượng hoặc lớp. | `private String name;` |
| **Code Block** | Bọc bởi `{}` | Nhóm các dòng lệnh thực hiện chung logic. | `{ this.count = 0; }` |

---

## Quy tắc sử dụng Comments (Chú thích) trong mã nguồn

Comments giúp giải thích logic phức tạp của các phương thức hoặc lớp mà không ảnh hưởng đến việc biên dịch:

- `// Single-line comment`: Chú thích một dòng duy nhất.
- `/* Multi-line comment */`: Chú thích trên nhiều dòng.
- `/** JavaDoc comment */`: Chú thích tài liệu hóa, hỗ trợ sinh tài liệu API (sử dụng các thẻ như `@param`, `@return` để giải thích cho các phương thức).

> [!info] Ví dụ Javadoc chuẩn cho phương thức
> ```java
> /**
>  * Tính tổng hai số nguyên.
>  * 
>  * @param a Số thứ nhất
>  * @param b Số thứ hai
>  * @return Tổng của a và b
>  */
> public int sum(int a, int b) {
>     return a + b;
> }
> ```
