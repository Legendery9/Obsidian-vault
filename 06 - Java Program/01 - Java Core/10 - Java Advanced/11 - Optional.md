# Java Optional

> [!abstract] Định nghĩa
> **`java.util.Optional<T>`** là một lớp wrapper chứa tối đa một giá trị phi-null (non-null value). Lớp này được giới thiệu trong Java 8 nhằm mục đích cung cấp giải pháp an toàn thay thế cho giá trị trả về có khả năng bị `null`, giúp tránh các lỗi `NullPointerException` (NPE) và giảm thiểu số lượng mã kiểm tra `if (obj != null)`.

---

## 1. Tác dụng
- **Lập trình an toàn:** Ép người gọi phương thức phải chủ động xử lý trường hợp dữ liệu bị khuyết (empty) thay vì âm thầm nhận về giá trị null.
- **Fluent API:** Hỗ trợ xử lý giá trị khuyết một cách thanh lịch thông qua lập trình hàm (functional style with map, filter, orElse).

---

## 2. Bảng tham chiếu các phương thức cốt lõi

| Method | Kiểu trả về | Tác dụng | Lưu ý |
| :--- | :--- | :--- | :--- |
| `empty()` | `Optional<T>` | Tạo một đối tượng `Optional` rỗng. | |
| `of(T value)` | `Optional<T>` | Tạo `Optional` chứa `value`. | Ném ngay `NullPointerException` nếu `value` là `null`. |
| `ofNullable(T value)` | `Optional<T>` | Tạo `Optional` chứa `value`. Trả về `Optional.empty()` nếu `value` là `null`. | Cách tạo an toàn nhất khi chưa chắc chắn biến có null hay không. |
| `isPresent()` | `boolean` | Trả về `true` nếu có giá trị bên trong. | |
| `isEmpty()` | `boolean` | Trả về `true` nếu không có giá trị bên trong (Java 11+). | |
| `get()` | `T` | Lấy giá trị bên trong ra ngoài. | Ném `NoSuchElementException` nếu Optional đang rỗng. Hạn chế dùng trực tiếp mà không kiểm tra. |
| `ifPresent(Consumer action)` | `void` | Thực thi khối lệnh `action` nếu có giá trị. | Tránh viết `if (opt.isPresent()) { doSomething(opt.get()); }` |
| `ifPresentOrElse(action, emptyAction)`| `void` | Thực thi `action` nếu có giá trị, ngược lại chạy `emptyAction` (Java 9+). | Phù hợp cho xử lý hai nhánh rõ ràng. |
| `orElse(T other)` | `T` | Trả về giá trị nếu có, ngược lại trả về giá trị mặc định `other`. | Giá trị mặc định `other` được tạo ra bất kể Optional rỗng hay không. |
| `orElseGet(Supplier s)` | `T` | Trả về giá trị nếu có, ngược lại chạy hàm `s` để sinh giá trị mặc định. | Tốt hơn `orElse` nếu việc tạo giá trị mặc định tốn hiệu năng (lazy evaluation). |
| `orElseThrow()` | `T` | Trả về giá trị nếu có, ngược lại ném ngoại lệ mặc định (Java 10+). | |
| `orElseThrow(Supplier ex)` | `T` | Trả về giá trị nếu có, ngược lại ném ngoại lệ tùy chỉnh sinh từ `ex`. | Khuyên dùng trong các tầng Service/API. |
| `filter(Predicate p)` | `Optional<T>` | Lọc giá trị bên trong. Nếu thỏa mãn điều kiện trả về chính nó, ngược lại trả về `empty()`. | |
| `map(Function mapper)` | `Optional<U>` | Biến đổi giá trị bên trong sang kiểu dữ liệu mới. | |
| `flatMap(Function mapper)`| `Optional<U>` | Biến đổi giá trị bên trong và tự động làm phẳng (flatten) nếu hàm mapper trả về một Optional. | Tránh tình trạng nhận về kiểu lồng nhau `Optional<Optional<U>>`. |

---

## 3. Ví dụ minh họa

### 3.1. Tạo và lấy giá trị an toàn
```java
import java.util.Optional;

public class OptionalBasicExample {
    public static void main(String[] args) {
        String name = null;

        // 1. Khởi tạo an toàn bằng ofNullable
        Optional<String> nameOpt = Optional.ofNullable(name);

        // 2. Sử dụng orElseGet để gán giá trị mặc định một cách lười biếng (Lazy Evaluation)
        String value = nameOpt.orElseGet(() -> "Default Name");
        System.out.println("Tên: " + value); // Output: Default Name

        // 3. Sử dụng ifPresentOrElse (Java 9+)
        nameOpt.ifPresentOrElse(
            n -> System.out.println("Tên tìm thấy: " + n),
            () -> System.out.println("Không tìm thấy tên!") // Chạy nhánh này
        );
    }
}
```

### 3.2. Chaining xử lý (Map, Filter)
```java
import java.util.Optional;

class User {
    private String email;
    public User(String email) { this.email = email; }
    public String getEmail() { return email; }
}

public class OptionalChainExample {
    public static void main(String[] args) {
        User user = new User("admin@gmail.com");
        Optional<User> userOpt = Optional.of(user);

        // Trích xuất email, lọc xem có phải gmail không, sau đó in ra hoặc ném lỗi
        String gmail = userOpt.map(User::getEmail)                   // Chuyển User -> String email
                              .filter(email -> email.endsWith("@gmail.com")) // Lọc điều kiện
                              .orElseThrow(() -> new IllegalArgumentException("Không phải Gmail hợp lệ!"));

        System.out.println("Gmail hợp lệ: " + gmail); // Output: admin@gmail.com
    }
}
```

---

## 4. Lưu ý quan trọng (Đoạn mã nên/không nên làm)

> [!warning]
> - ❌ **ĐỪNG bao giờ** sử dụng `Optional` làm kiểu dữ liệu cho các trường (fields) trong một Class (vì `Optional` không hỗ trợ Serialization và gây phình kích thước bộ nhớ không cần thiết).
> - ❌ **ĐỪNG** truyền `Optional` làm tham số đầu vào cho các phương thức (hãy truyền trực tiếp đối tượng hoặc giá trị có thể null, hoặc thiết kế nạp chồng phương thức).
> - ✅ **NÊN** dùng `Optional` duy nhất cho **kiểu trả về (return type)** của các phương thức tìm kiếm/truy vấn để cảnh báo cho người gọi hàm biết rằng kết quả có thể rỗng.
