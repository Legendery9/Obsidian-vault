# Java UUID

> [!abstract] Định nghĩa
> **`java.util.UUID`** đại diện cho một mã định danh duy nhất toàn cầu (Universally Unique Identifier) dài 128-bit. Một UUID được đảm bảo tính độc bản cực kỳ cao trên toàn hệ thống mà không cần thông qua một bộ điều phối trung tâm nào.

---

## 1. Tác dụng
- **Tạo khoá chính (Primary Key):** Phù hợp cho cơ sở dữ liệu phân tán (NoSQL hoặc SQL phân mảnh), nơi các bộ đếm tự tăng (`auto-increment`) truyền thống dễ bị xung đột dữ liệu khi gộp các phân vùng lại.
- **Mã hoá tài nguyên bảo mật:** Sử dụng làm tên tệp tin tải lên server, mã kích hoạt tài khoản, mã token giao dịch nhằm tránh việc kẻ xấu đoán được ID tuần tự.

---

## 2. Bảng tham chiếu các phương thức cốt lõi

| Method | Kiểu trả về | Tác dụng | Ví dụ |
| :--- | :--- | :--- | :--- |
| `randomUUID()` | `UUID` | Phương thức tĩnh sinh ngẫu nhiên một UUID phiên bản 4 (v4) dựa trên bộ sinh số ngẫu nhiên bảo mật. | `UUID.randomUUID()` |
| `nameUUIDFromBytes(byte[] name)`| `UUID` | Phương thức tĩnh tạo UUID phiên bản 3 (v3) dựa trên dữ liệu đầu vào. Cùng một đầu vào sẽ luôn cho ra cùng một UUID giống nhau. | `UUID.nameUUIDFromBytes("user1".getBytes())` |
| `fromString(String name)` | `UUID` | Phân tích cú pháp một chuỗi UUID tiêu chuẩn (dạng 36 ký tự) để chuyển đổi ngược lại thành đối tượng UUID. | `UUID.fromString("123e4567-e89b-12d3-a456-426614174000")` |
| `toString()` | `String` | Biểu diễn đối tượng UUID thành chuỗi văn bản 36 ký tự (gồm 32 ký tự chữ số/chữ cái Hex và 4 dấu gạch ngang `-`). | `uuid.toString()` |

---

## 3. Ví dụ minh họa

```java
import java.util.UUID;

public class UuidExample {
    public static void main(String[] args) {
        // 1. Sinh UUID ngẫu nhiên (v4) - Thường dùng nhất
        UUID randomId = UUID.randomUUID();
        System.out.println("UUID ngẫu nhiên: " + randomId);
        // Ví dụ Output: f81d4fae-7dec-11d0-a765-00a0c91e6bf6

        // 2. Chuyển đổi thành dạng String để lưu trữ
        String uuidStr = randomId.toString();
        System.out.println("UUID dưới dạng String (36 ký tự): " + uuidStr);

        // 3. Phục hồi lại đối tượng UUID từ String
        UUID recoveredId = UUID.fromString(uuidStr);
        System.out.println("Phục hồi thành công: " + recoveredId.equals(randomId)); // true

        // 4. Sinh UUID định danh tĩnh (v3) từ dữ liệu đầu vào cố định
        String name = "system_user_1001";
        UUID staticId1 = UUID.nameUUIDFromBytes(name.getBytes());
        UUID staticId2 = UUID.nameUUIDFromBytes(name.getBytes());
        System.out.println("UUID tĩnh lần 1: " + staticId1);
        System.out.println("UUID tĩnh lần 2: " + staticId2);
        System.out.println("Hai UUID giống nhau: " + staticId1.equals(staticId2)); // true
    }
}
```

---

## 4. Lưu ý

> [!tip] Lưu trữ cơ sở dữ liệu hiệu quả
> Chuỗi UUID dạng văn bản dài 36 ký tự chiếm dụng khá nhiều dung lượng bộ nhớ. Trong các hệ thống cơ sở dữ liệu lớn (như MySQL, PostgreSQL), để tối ưu hóa hiệu năng đánh chỉ mục (index), bạn nên lưu trữ UUID dưới dạng trường **`BINARY(16)`** (chỉ chiếm 16 bytes bộ nhớ) thay vì trường `VARCHAR(36)`.
