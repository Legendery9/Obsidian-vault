# Java Methods and Modifiers

> [!abstract] Định nghĩa
> **Method (Phương thức)** là một khối mã lệnh thực hiện một công việc cụ thể, có thể tái sử dụng và được gọi thông qua tên của phương thức đó.
> **Modifier (Từ khóa bổ nghĩa)** xác định phạm vi truy cập (Access Modifier) hoặc các đặc tính đặc biệt của biến/hàm/lớp (Non-access Modifier).

---

## Các thành phần cấu trúc phương thức

| Thành phần | Đặc điểm | Tác dụng | Ví dụ |
| --- | --- | --- | --- |
| `main()` | `public static void main(String[] args)` | Điểm khởi chạy của chương trình (chạy đầu tiên bởi JVM). | `public static void main(...)` |
| **Constructor** | Trùng tên class hoàn toàn, không có kiểu trả về. | Khởi tạo đối tượng (object) trong Heap memory. | `User(String name) { this.name = name; }` |
| **Field** | Khai báo trong class ngoài method. | Lưu trữ thuộc tính/trạng thái dữ liệu của đối tượng hoặc lớp. | `private String name;` |
| **Code Block** | Bọc bởi `{}` | Nhóm các dòng lệnh thực hiện chung logic. | `{ this.count = 0; }` |

---

## Từ khóa bổ nghĩa truy cập (Access Modifiers)

Access modifiers quyết định tầm vực hoạt động (visibility) của thành phần dữ liệu:

| Modifier | Cùng Class | Cùng Package | Lớp con (Inherited) | Toàn dự án |
| --- | --- | --- | --- | --- |
| `private` | ✅ | ❌ | ❌ | ❌ |
| *default* (Không ghi) | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ (Qua kế thừa) | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

> [!warning] Quy tắc đóng gói dữ liệu
> Luôn khai báo biến (fields) ở phạm vi tối thiểu nhất (thường là `private`) và truy xuất thông qua các hàm `getter`/`setter` công khai để đảm bảo tính an toàn dữ liệu.
> ```java
> // ✅ Nên làm (Do): Đóng gói dữ liệu bảo vệ biến trạng thái.
> public class User {
>     private String username;
>     
>     public String getUsername() {
>         return this.username;
>     }
> }
> 
> // ❌ Không nên làm (Don't): Tránh khai báo biến public trực tiếp trong class trừ khi là hằng số.
> public class BadUser {
>     public String username; // Dễ bị thay đổi tuỳ tiện từ bên ngoài.
> }
> ```

---

## Từ khóa bổ nghĩa phi truy cập (Non-access Modifiers)

Các từ khóa điều khiển hành vi đặc biệt của biến, hàm, class:

### 1. static
- Thành phần thuộc về lớp, không phụ thuộc vào đối tượng cụ thể. Có thể gọi trực tiếp thông qua tên Class mà không cần dùng từ khóa `new`.

```java
// ✅ Nên làm (Do): Sử dụng static cho các biến đếm, hằng số dùng chung, hoặc các hàm tiện ích.
public class MathUtil {
    public static final double PI = 3.14159;
    
    public static int add(int a, int b) {
        return a + b;
    }
}
// Gọi hàm tiện ích: MathUtil.add(5, 10);
```

### 2. final
- **Với Class:** Ngăn cản kế thừa.
- **Với Method:** Ngăn cản ghi đè (override).
- **Với Biến:** Biến trở thành hằng số (không được phép gán lại giá trị lần thứ hai).

### 3. abstract
- Khai báo lớp hoặc phương thức chưa hoàn thiện, bắt buộc lớp con triển khai chi tiết.

### 4. synchronized và volatile (Đa luồng)
- `synchronized`: Khoá phương thức hoặc khối lệnh, chỉ cho phép duy nhất một luồng (thread) truy cập tại một thời điểm.
- `volatile`: Đảm bảo giá trị biến được đọc trực tiếp từ bộ nhớ RAM chính thay vì CPU cache, giúp đồng bộ hóa tức thì dữ liệu giữa các thread.

```java
public class ThreadCounter {
    private volatile boolean running = true;

    public synchronized void increment() {
        // ✅ Nên làm (Do): Dùng synchronized để tránh xung đột race condition trong môi trường đa luồng.
    }
}
```

### 5. transient
- Ngăn chặn việc tuần tự hóa (serialization) các thuộc tính nhạy cảm như mật khẩu hoặc dữ liệu tạm thời.

```java
public class User implements Serializable {
    private String username;
    private transient String password; // ✅ Nên làm (Do): Sử dụng transient để bảo vệ thông tin bảo mật khi lưu file/truyền mạng.
}
```

### 6. native
- Đánh dấu phương thức được cài đặt bằng các ngôn ngữ hệ thống khác (C/C++), tương tác trực tiếp với phần cứng thông qua Java Native Interface (JNI).

---

## Lưu ý về Comments (Chú thích)

- `// Single-line comment`: Chú thích một dòng.
- `/* Multi-line comment */`: Chú thích nhiều dòng.
- `/** JavaDoc comment */`: Chú thích tài liệu hóa, hỗ trợ sinh tài liệu API (sử dụng các thẻ như `@param`, `@return`).

> [!info] Ví dụ Javadoc chuẩn
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
