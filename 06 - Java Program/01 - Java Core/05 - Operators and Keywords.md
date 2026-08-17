# Java Operators and Keywords

> [!abstract] Định nghĩa
> **Operator (Toán tử)** là các ký hiệu đặc biệt dùng để thực hiện các phép toán số học, so sánh, logic trên các biến hoặc giá trị.
> **Keyword (Từ khóa)** là các từ được dành riêng bởi Java, có ý nghĩa và chức năng xác định để điều khiển chương trình và cấu trúc hướng đối tượng.

---

## Các nhóm toán tử chính

### 1. Toán tử số học & Gán giá trị
- Số học: `+`, `-`, `*`, `/`, `%` (chia lấy dư), `++` (tăng 1), `--` (giảm 1).
- Gán: `=`, `+=`, `-=`, `*=`, `/=`, `%=`.

> [!warning] Toán tử một ngôi tăng/giảm (`++`/`--`)
> Phân biệt cách thực thi của tiền tố (prefix) và hậu tố (postfix):
> - **Tiền tố (`++a`):** Tăng giá trị trước, sau đó mới dùng giá trị trong phép toán.
> - **Hậu tố (`a++`):** Dùng giá trị hiện tại trong phép toán trước, sau đó mới tăng giá trị lên.
> ```java
> int a = 10;
> int b = ++a; // a = 11, b = 11
> 
> int x = 10;
> int y = x++; // x = 11, y = 10
> ```

### 2. Toán tử so sánh & Logic
- So sánh: `==` (bằng), `!=` (khác), `>`, `<`, `>=`, `<=`.
- Logic: `&&` (AND ngắn mạch), `||` (OR ngắn mạch), `!` (NOT phủ định), `^` (XOR logic).

> [!info] Tính chất ngắn mạch (Short-Circuit)
> - Với `&&`: Nếu điều kiện bên trái sai, Java lập tức kết luận cả biểu thức sai mà không cần tính toán điều kiện bên phải.
> - Với `||`: Nếu điều kiện bên trái đúng, Java lập tức kết luận cả biểu thức đúng mà không cần tính toán điều kiện bên phải.
> ```java
> // ✅ Nên làm (Do): Sử dụng ngắn mạch để tránh lỗi NullPointerException.
> if (user != null && user.getAge() > 18) {
>     // Nếu user là null, biểu thức dừng lại ngay, không chạy getAge() tránh bị lỗi NullPointer.
> }
> ```

### 3. Toán tử trên Bit (Bitwise & Shift Operators)
- Bitwise: `&` (AND bit), `|` (OR bit), `^` (XOR bit), `~` (NOT bit).
- Dịch bit: 
  - `<<` (Dịch trái - tương đương nhân với 2 lũy thừa).
  - `>>` (Dịch phải giữ dấu - tương đương chia cho 2 lũy thừa).
  - `>>>` (Dịch phải không dấu - luôn chèn số 0 ở bên trái).

---

## Bảng thứ tự ưu tiên của toán tử (Precedence)

Khi một biểu thức chứa nhiều toán tử, chúng được thực thi theo thứ tự ưu tiên sau (từ cao xuống thấp):

| Thứ tự | Toán tử | Miêu tả |
| --- | --- | --- |
| 1 | `()` | Các dấu ngoặc đơn (Luôn ưu tiên cao nhất). |
| 2 | `[]` `.` | Truy cập mảng, gọi phương thức đối tượng. |
| 3 | `++` `--` `!` `~` | Toán tử một ngôi, phủ định logic/bit. |
| 4 | `*` `/` `%` | Nhân, chia, chia lấy dư. |
| 5 | `+` `-` | Cộng, trừ. |
| 6 | `<<` `>>` `>>>` | Dịch chuyển bit. |
| 7 | `<` `<=` `>` `>=` `instanceof` | So sánh quan hệ, kiểm tra kiểu dữ liệu. |
| 8 | `==` `!=` | So sánh bằng và khác. |
| 9 | `&` | Bitwise AND. |
| 10 | `^` | Bitwise XOR. |
| 11 | `|` | Bitwise OR. |
| 12 | `&&` | Logic AND. |
| 13 | `||` | Logic OR. |
| 14 | `?:` | Toán tử ba ngôi. |
| 15 | `=` `+=` `-=` `*=` `/=` | Các toán tử gán (Ưu tiên thấp nhất). |

---

## Từ khóa hướng đối tượng cốt lõi (Keywords)

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
| `return` | Thoát khỏi phương thức và trả về giá trị. | `return result;` |

> [!note] Lời giải so sánh: `extends` vs `implements`
> - `extends` đại diện cho quan hệ **IS-A** (Kế thừa mã nguồn và trạng thái từ một lớp cha duy nhất).
> - `implements` đại diện cho quan hệ **CAN-DO** (Cam kết thực hiện hành vi, một class có thể implements nhiều interface khác nhau).
