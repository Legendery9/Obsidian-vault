# Java Operators

> [!abstract] Định nghĩa
> **Operator (Toán tử)** là các ký hiệu đặc biệt dùng để thực hiện các phép toán số học, so sánh, logic trên các biến hoặc giá trị trong chương trình. Để phân biệt cấu trúc điều khiển của ngôn ngữ, xem thêm tại [[02 - Keywords]].

---

## 1. Các nhóm toán tử chính

### 1.1. Toán tử số học & Gán giá trị
- **Số học:** `+`, `-`, `*`, `/`, `%` (chia lấy dư), `++` (tăng 1 đơn vị), `--` (giảm 1 đơn vị).
- **Gán:** `=`, `+=`, `-=`, `*=`, `/=`, `%=`.

> [!warning] Toán tử một ngôi tăng/giảm (`++`/`--`)
> Phân biệt cách thực thi của tiền tố (prefix) và hậu tố (postfix):
> - **Tiền tố (`++a`):** Tăng giá trị trước, sau đó mới sử dụng giá trị trong phép toán.
> - **Hậu tố (`a++`):** Dùng giá trị hiện tại trong phép toán trước, sau đó mới tăng giá trị lên.
> ```java
> int a = 10;
> int b = ++a; // a = 11, b = 11
> 
> int x = 10;
> int y = x++; // x = 11, y = 10
> ```

### 1.2. Toán tử so sánh & Logic
- **So sánh:** `==` (bằng), `!=` (khác), `>`, `<`, `>=`, `<=`.
- **Logic:** `&&` (AND ngắn mạch), `||` (OR ngắn mạch), `!` (NOT phủ định), `^` (XOR logic).

> [!info] Tính chất ngắn mạch (Short-Circuit)
> - Với `&&`: Nếu điều kiện bên trái sai, Java lập tức kết luận cả biểu thức là sai mà không cần tính toán điều kiện bên phải.
> - Với `||`: Nếu điều kiện bên trái đúng, Java lập tức kết luận cả biểu thức là đúng mà không cần tính toán điều kiện bên phải.
> ```java
> // ✅ Nên làm (Do): Sử dụng ngắn mạch để tránh lỗi NullPointerException.
> if (user != null && user.getAge() > 18) {
>     // Nếu user là null, biểu thức dừng lại ngay, không chạy getAge() tránh lỗi NullPointerException.
> }
> ```

### 1.3. Toán tử trên Bit (Bitwise & Shift Operators)
- **Bitwise:** `&` (AND bit), `|` (OR bit), `^` (XOR bit), `~` (NOT bit).
- **Dịch bit:** 
  - `<<` (Dịch trái - tương đương nhân với $2^{\text{shift\_amount}}$).
  - `>>` (Dịch phải giữ dấu - tương đương chia cho $2^{\text{shift\_amount}}$).
  - `>>>` (Dịch phải không dấu - luôn chèn số `0` ở bên trái).

---

## 2. Bảng thứ tự ưu tiên của toán tử (Precedence)

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
