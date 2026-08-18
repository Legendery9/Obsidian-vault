# Java Keywords

> [!abstract] Định nghĩa
> **Keyword (Từ khóa)** là các từ được dành riêng bởi ngôn ngữ Java, có ý nghĩa và chức năng xác định để điều khiển chương trình và cấu trúc hướng đối tượng. Chúng ta không thể sử dụng từ khóa để đặt tên cho các biến, lớp, hay phương thức (để hiểu cách kết hợp với các phép toán, xem [[01 - Operators]]).

---

## 1. Từ khóa hướng đối tượng cốt lõi (Keywords)

Các từ khóa sau đóng vai trò quyết định cấu trúc kế thừa và hành vi của lớp/đối tượng trong Java:

| Từ khóa | Ý nghĩa kỹ thuật | Ví dụ thực tế |
| --- | --- | --- |
| `extends` | Khai báo class con kế thừa class cha. | `class Dog extends Animal` |
| `implements` | Triển khai giao diện (interface). | `class User implements Runnable` |
| `this` | Tham chiếu tới đối tượng (object) hiện tại. | `this.name = name;` |
| `super` | Tham chiếu tới các thành phần của lớp cha. | `super.makeSound();` hoặc `super();` |
| `new` | Khởi tạo đối tượng mới trên Heap memory. | `User user = new User();` |
| `instanceof` | Kiểm tra kiểu thực tế của đối tượng. | `if (obj instanceof User)` |
| `throw` | Chủ động ném một Exception cụ thể. | `throw new IllegalArgumentException();` |
| `throws` | Khai báo phương thức có thể ném Exception ra ngoài. | `public void run() throws IOException {}` |
| `return` | Thoát khỏi phương thức và trả về giá trị (nếu có). | `return result;` |

---

## 2. Phân biệt quan hệ kế thừa: `extends` vs `implements`

> [!note] So sánh cốt lõi
> - **`extends`** đại diện cho quan hệ **IS-A** (Là một): Thể hiện sự kế thừa mã nguồn và trạng thái từ một lớp cha duy nhất (Java không hỗ trợ đa kế thừa lớp).
> - **`implements`** đại diện cho quan hệ **CAN-DO** (Có thể làm): Thể hiện cam kết thực hiện hành vi do interface đặt ra. Một class có thể implements nhiều interface khác nhau để tăng tính đa hình.
