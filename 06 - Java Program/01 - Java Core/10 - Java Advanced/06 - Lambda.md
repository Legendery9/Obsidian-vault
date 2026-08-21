[Oracle Java Documentation](https://docs.oracle.com/en/java/)

# Lambda Expressions

> [!abstract] Định nghĩa
> **Lambda Expression** (biểu thức Lambda, giới thiệu từ Java 8) là một hàm ẩn danh (anonymous function) - tức là một hàm không có tên định danh, không có kiểu trả về khai báo hiển thị, và không thuộc về một lớp cụ thể nào. Lambda cung cấp giải pháp ngắn gọn để triển khai trực tiếp các **Functional Interface** (interface chỉ có một phương thức trừu tượng duy nhất) thay vì phải viết các lớp nặc danh (Anonymous Class) dài dòng (xem chi tiết tại [[01 - Classes]]).

---

## 1. Cú pháp tổng quát

Cú pháp của biểu thức Lambda gồm ba thành phần chính: **Tham số**, toán tử Lambda `->`, và **Thân hàm**.

- **Dạng biểu thức đơn (Expression body):**
  `(parameters) -> expression`
- **Dạng khối lệnh (Block body):**
  `(parameters) -> { statements; }`

### Liên kết với Functional Interface

Một biểu thức Lambda chỉ có thể được sử dụng làm kiểu dữ liệu của một đối tượng triển khai **Functional Interface** (giao diện chức năng). Các Functional Interface phổ biến trong JDK bao gồm:
- `java.lang.Runnable` (phương thức `run()`)
- `java.util.Comparator` (phương thức `compare()` - xem thêm tại [[19 - Comparator and Comparable]] và [[09 - Comparator]])
- `java.util.function.Predicate` (phương thức `test()`)
- `java.util.function.Consumer` (phương thức `accept()`)
- `java.util.function.Function` (phương thức `apply()`)

---

## 2. Bảng tham chiếu cú pháp Lambda phổ biến

| Dạng tham số / Thân hàm | Cú pháp Lambda | Giải thích | Ví dụ minh họa |
| :--- | :--- | :--- | :--- |
| **Không tham số** | `() -> expression` | Dùng cho các phương thức trừu tượng không nhận đầu vào. | `() -> System.out.println("Hello")` |
| **Một tham số (rút gọn)** | `x -> expression` | Bỏ qua cặp ngoặc đơn `()` khi chỉ có đúng 1 tham số duy nhất. | `str -> str.toUpperCase()` |
| **Một tham số (đầy đủ)** | `(Type x) -> expression` | Khai báo tường minh kiểu dữ liệu của tham số. | `(String str) -> str.toUpperCase()` |
| **Nhiều tham số** | `(x, y) -> expression` | Bắt buộc phải đặt danh sách tham số trong cặp ngoặc đơn `()`. | `(a, b) -> a + b` |
| **Thân hàm đơn (Expression)** | `(...) -> expression` | Tự động trả về giá trị của biểu thức, không sử dụng cặp ngoặc nhọn `{}` và từ khóa `return`. | `(x, y) -> x * y` |
| **Thân hàm khối lệnh (Block)** | `(...) -> { statements; return val; }` | Thân hàm chứa nhiều câu lệnh trong cặp `{}`. Bắt buộc có `return` nếu phương thức yêu cầu trả về giá trị. | `(x, y) -> { int sum = x + y; return sum; }` |

---

## 3. Ví dụ thực tế

Dưới đây là mã nguồn minh họa các cách sử dụng biểu thức Lambda trong thực tế:

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class LambdaDemo {
    public void demonstrate() {
        // 1. Sử dụng Lambda với Runnable
        Runnable task = () -> System.out.println("Đang chạy luồng song song...");
        new Thread(task).start();

        // 2. Sử dụng Lambda sắp xếp với Comparator
        List<String> names = new ArrayList<>(List.of("Cường", "An", "Bình"));
        
        // Sắp xếp theo thứ tự bảng chữ cái
        Collections.sort(names, (s1, s2) -> s1.compareTo(s2));
        System.out.println("Đã sắp xếp: " + names); // [An, Bình, Cường]

        // 3. Sử dụng Lambda kết hợp Stream API
        names.stream()
             .filter(name -> name.startsWith("A")) // Lọc tên bắt đầu bằng "A"
             .forEach(name -> System.out.println("Tên lọc: " + name));
    }
}
```

### Quy chuẩn lập trình (Do / Don't)

```java
// ✅ Nên làm (Do)
// Sử dụng biểu thức Lambda ngắn gọn, rõ ràng.
names.forEach(name -> System.out.println(name));

// Khuyên dùng Method Reference (tham chiếu phương thức) khi Lambda chỉ làm nhiệm vụ gọi trực tiếp phương thức có sẵn.
names.forEach(System.out::println);
```

```java
// ❌ Không nên làm (Don't)
// Tránh viết khối logic quá dài dòng, phức tạp bên trong Lambda. Nó làm mất đi tính rõ ràng và sạch sẽ của code.
names.forEach(name -> {
    String upper = name.toUpperCase();
    if (upper.startsWith("A")) {
        System.out.println("Hợp lệ: " + upper);
    } else {
        System.out.println("Không hợp lệ: " + upper);
    }
}); // Nên tách logic phức tạp này ra thành một phương thức riêng
```

---

## 4. Lưu ý quan trọng

### Biến effectively final khi dùng trong Lambda

> [!warning] Quy tắc Enclosing Scope Variables
> Biến cục bộ khai báo bên ngoài phương thức bao quanh nhưng được sử dụng bên trong khối Lambda bắt buộc phải là **hằng số (`final`)** hoặc **effectively final** (biến không bị gán lại giá trị sau khi đã được khởi tạo).
> ```java
> int limit = 10;
> Runnable r = () -> System.out.println(limit); // ✅ Hợp lệ: limit là effectively final
> // limit = 20; // ❌ LỖI BIÊN DỊCH nếu bỏ comment dòng này vì limit bị thay đổi giá trị
> ```

### So sánh phạm vi của `this` (Lambda vs Anonymous Class)

> [!note] Từ khóa `this`
> - **Trong Lambda Expression:** Lambda không tạo ra phạm vi scope mới cho đối tượng. Từ khóa `this` trong Lambda tham chiếu đến **chính instance của Class chứa khối Lambda đó** (lexical scoping).
> - **Trong Anonymous Class:** Từ khóa `this` đại diện cho **chính thực thể lớp nặc danh** đang được khởi tạo tại chỗ.
