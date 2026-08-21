[Oracle Java Documentation](https://docs.oracle.com/en/java/)

# Exception Handling and Built-in Exceptions

> [!abstract] Định nghĩa
> **Exception Handling Statements** (câu lệnh xử lý ngoại lệ) là cơ chế xử lý các tình huống bất thường xảy ra trong quá trình chạy chương trình (Runtime), giúp ứng dụng không bị dừng đột ngột (crash) và có thể khôi phục trạng thái hoạt động hoặc đưa ra thông báo lỗi thân thiện.

---

## 1. Cấu trúc thử & bắt lỗi (Exception Handling Statements)

Java cung cấp 5 từ khóa chính phục vụ cho việc bắt và xử lý ngoại lệ cùng cấu trúc `try-with-resources` tự động giải phóng tài nguyên.

### Bảng tham chiếu các câu lệnh xử lý lỗi

| Statement | Definition | Tác dụng | Lưu ý |
| :--- | :--- | :--- | :--- |
| `try` | Khối thử nghiệm mã nguồn. | Bao bọc đoạn mã lệnh có khả năng ném ra (throw) ngoại lệ. | Không thể đứng độc lập. Phải đi kèm ít nhất một khối `catch` hoặc một khối `finally`. |
| `catch` | Khối xử lý ngoại lệ. | Bắt giữ ngoại lệ tương thích được ném ra từ khối `try` để xử lý. | - Có thể viết nhiều khối `catch` liên tiếp.<br>- Phải khai báo từ lớp Exception con đến lớp cha.<br>- Hỗ trợ Multi-catch (Java 7+): `catch (AException \| BException e)`. |
| `finally` | Khối dọn dẹp tài nguyên. | Luôn luôn thực thi sau khi thoát khỏi khối `try-catch` bất kể có ngoại lệ xảy ra hay không. | Vẫn chạy ngay cả khi trong khối `try` hoặc `catch` chứa câu lệnh `return` hoặc `throw`. Thường dùng để đóng kết nối cơ sở dữ liệu, file stream. |
| `try-with-resources` | Khối try quản lý tài nguyên. | Tự động đóng các tài nguyên được khai báo trong ngoặc đơn của `try` sau khi kết thúc khối lệnh. | Các tài nguyên khai báo phải triển khai interface `java.lang.AutoCloseable` hoặc `java.io.Closeable`. |
| `throw` | Lệnh chủ động ném lỗi. | Kích hoạt và ném ra một đối tượng ngoại lệ cụ thể tại vị trí mong muốn. | Thường dùng để ném ngoại lệ khi dữ liệu đầu vào vi phạm quy tắc logic nghiệp vụ (business logic). |
| `throws` | Khai báo lỗi ở phương thức. | Khai báo ở phần chữ ký phương thức để cảnh báo bên gọi phương thức này rằng nó có thể ném ra Checked Exception. | Phương thức gọi bắt buộc phải bao bọc trong `try-catch` hoặc tiếp tục khai báo `throws` ở phương thức của mình. |

---

## 2. Các Exception & Error có sẵn trong Java (JDK Built-in)

Dưới đây là bảng liệt kê các ngoại lệ (`Exception`) và lỗi hệ thống (`Error`) phổ biến nhất nằm trong thư viện chuẩn của Java Development Kit (JDK), không yêu cầu thêm thư viện ngoài.

### Bảng tham chiếu JDK Exceptions & Errors

| Exception / Error | Gói (Package) | Phân loại | Khi nào xảy ra | Ví dụ code gây lỗi |
| :--- | :--- | :--- | :--- | :--- |
| `Exception` | `java.lang` | Checked | Lớp cha của các ngoại lệ cần kiểm tra (phải dùng try-catch hoặc `throws`). | Thường kế thừa lớp này khi tự tạo Checked Exception tùy chỉnh. |
| `RuntimeException` | `java.lang` | Unchecked | Lớp cha của toàn bộ các ngoại lệ xảy ra trong quá trình chạy (không bắt buộc xử lý thủ công). | Thường kế thừa lớp này khi tự tạo Unchecked Exception tùy chỉnh. |
| `NullPointerException` | `java.lang` | Unchecked | Khi cố gắng truy cập thuộc tính hoặc gọi phương thức trên một biến tham chiếu trỏ tới `null`. | `String str = null;`<br>`str.length();` |
| `ArrayIndexOutOfBoundsException` | `java.lang` | Unchecked | Khi truy cập chỉ số phần tử mảng nằm ngoài giới hạn (chỉ số âm hoặc $\ge$ chiều dài mảng). | `int[] arr = {1, 2};`<br>`int val = arr[5];` |
| `ArithmeticException` | `java.lang` | Unchecked | Khi xảy ra lỗi tính toán bất thường (ví dụ: phép chia số nguyên cho số $0$). | `int a = 10 / 0;` |
| `ClassCastException` | `java.lang` | Unchecked | Khi cố tình ép kiểu một đối tượng sang một lớp con mà thực tế nó không tương thích. | `Object obj = "Hello";`<br>`Integer num = (Integer) obj;` |
| `NumberFormatException` | `java.lang` | Unchecked | Khi chuyển đổi chuỗi String thành kiểu số nhưng chuỗi không đúng định dạng. | `int num = Integer.parseInt("abc");` |
| `IllegalArgumentException` | `java.lang` | Unchecked | Khi truyền tham số không phù hợp hoặc không đúng định dạng cho phương thức. | `Thread.sleep(-100);` |
| `IllegalStateException` | `java.lang` | Unchecked | Khi trạng thái của đối tượng hoặc hệ thống chưa sẵn sàng để thực hiện lệnh gọi phương thức. | Gọi phương thức trên `Stream` đã bị đóng trước đó. |
| `IOException` | `java.io` | Checked | Lỗi tổng quát trong quá trình nhập xuất dữ liệu (đọc ghi file hỏng, ngắt kết nối mạng). | Đọc dữ liệu từ file nhưng kết nối đĩa cứng bị ngắt giữa chừng. |
| `FileNotFoundException` | `java.io` | Checked | Khi cố gắng truy cập tệp tin bằng đường dẫn không tồn tại trên hệ thống lưu trữ. | `new FileReader("missing_file.txt");` |
| `InterruptedException` | `java.lang` | Checked | Khi một luồng (thread) đang bị tạm dừng (ngủ/chờ) nhưng bị luồng khác gửi yêu cầu ngắt. | `Thread.sleep(1000); // Bị ngắt bởi Thread.interrupt()` |
| `UnsupportedOperationException` | `java.lang` | Unchecked | Khi một phương thức được gọi không được hỗ trợ bởi đối tượng hiện tại. | Gọi `add()` trên một danh sách chỉ đọc (`List.of(...)`). |
| `StackOverflowError` | `java.lang` | Error | Lỗi cạn kiệt ngăn xếp bộ nhớ (Stack memory) của luồng, do đệ quy vô hạn. | `public void recurse() { recurse(); }` |
| `OutOfMemoryError` | `java.lang` | Error | Lỗi cạn kiệt bộ nhớ Heap khi JVM không thể cấp phát thêm RAM cho các đối tượng mới. | Tạo mảng khổng lồ liên tục mà không giải phóng bộ nhớ. |

---

## 3. Ví dụ thực tế

Dưới đây là một ví dụ hoàn chỉnh chứa mã nguồn gây lỗi, cơ chế bắt và xử lý ngoại lệ an toàn:

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ExceptionHandlingDemo {

    // 1. Sử dụng try-catch-finally truyền thống và throws
    public void readFileOldWay(String path) throws IOException {
        BufferedReader reader = null;
        try {
            reader = new BufferedReader(new FileReader(path));
            System.out.println(reader.readLine());
        } catch (IOException e) {
            System.err.println("Lỗi khi đọc file: " + e.getMessage());
            throw e; // Tiếp tục ném lỗi lên cấp trên
        } finally {
            // Đóng tài nguyên thủ công, dễ bỏ quên hoặc phát sinh thêm lỗi trong finally
            if (reader != null) {
                reader.close();
            }
        }
    }

    // 2. Sử dụng try-with-resources (Do - Khuyên dùng)
    public void readFileModernWay(String path) {
        // Tài nguyên tự động đóng an toàn khi kết thúc khối try
        try (BufferedReader reader = new BufferedReader(new FileReader(path))) {
            System.out.println(reader.readLine());
        } catch (IOException e) {
            System.err.println("Xử lý lỗi đọc file: " + e.getMessage());
        }
    }

    // 3. Ví dụ gây lỗi Runtime và ném IllegalArgumentException
    public void registerUser(String username, int age) {
        if (username == null || username.isBlank()) {
            throw new IllegalArgumentException("Tên người dùng không được để trống!");
        }
        if (age < 18) {
            throw new IllegalArgumentException("Người dùng phải từ 18 tuổi trở lên!");
        }
        System.out.println("Đăng ký thành công: " + username);
    }
}
```

### Quy chuẩn lập trình (Do / Don't)

```java
// ✅ Nên làm (Do)
// Sử dụng try-with-resources cho tất cả các đối tượng tài nguyên (AutoCloseable).
try (var connection = database.getConnection()) {
    // Thao tác với DB
} catch (SQLException e) {
    logger.error("Database error occurred", e); // Ghi log chi tiết lỗi kèm StackTrace
}
```

```java
// ❌ Không nên làm (Don't)
// Tránh việc nuốt chửng ngoại lệ bằng khối catch rỗng mà không xử lý hoặc ghi log.
try {
    int value = Integer.parseInt(input);
} catch (NumberFormatException e) {
    // Không làm gì cả - khiến lỗi biến mất một cách bí ẩn, rất khó debug!
}
```
