# Java Modifiers

> [!abstract] Định nghĩa
> **Modifier (Từ khóa bổ nghĩa)** xác định phạm vi truy cập (Access Modifier) hoặc các đặc tính đặc biệt của biến/hàm/lớp (Non-access Modifier) nhằm phục vụ thiết kế hướng đối tượng và tối ưu hóa tài nguyên.

---

## 1. Từ khóa bổ nghĩa truy cập (Access Modifiers)

Access modifiers quyết định tầm vực hoạt động (visibility) của các thành phần (class, biến, [[01 - Methods|phương thức]]):

| Modifier | Cùng Class | Cùng Package | Lớp con (Inherited) | Toàn dự án |
| --- | --- | --- | --- | --- |
| `private` | ✅ | ❌ | ❌ | ❌ |
| *default* (Không ghi) | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ (Qua kế thừa) | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

> [!warning] Quy tắc đóng gói dữ liệu (Encapsulation)
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

## 2. Từ khóa bổ nghĩa phi truy cập (Non-access Modifiers)

Các từ khóa điều khiển hành vi đặc biệt của biến, phương thức, class:

### 1. `static`
- Thành phần thuộc về lớp, không phụ thuộc vào đối tượng cụ thể. Có thể gọi trực tiếp thông qua tên Class mà không cần khởi tạo đối tượng mới bằng từ khóa `new`.

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

### 2. `final`
- **Với Class:** Ngăn cản hoàn toàn việc kế thừa từ lớp này.
- **Với Method:** Ngăn cản lớp con ghi đè (override) phương thức.
- **Với Biến:** Biến trở thành hằng số (không được phép gán lại giá trị lần thứ hai).

### 3. `abstract`
- Khai báo lớp hoặc phương thức chưa hoàn thiện, bắt buộc lớp con kế thừa triển khai chi tiết.

### 4. `synchronized` và `volatile` (Hỗ trợ đa luồng)
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

### 5. `transient`
- Ngăn chặn việc tuần tự hóa (serialization) các thuộc tính nhạy cảm như mật khẩu hoặc dữ liệu tạm thời khi truyền qua mạng/lưu file.

```java
import java.io.Serializable;

public class User implements Serializable {
    private String username;
    private transient String password; // ✅ Nên làm (Do): Sử dụng transient để bảo vệ thông tin bảo mật.
}
```

### 6. `native`
- Đánh dấu phương thức được cài đặt bằng các ngôn ngữ hệ thống khác (C/C++), tương tác trực tiếp với phần cứng thông qua Java Native Interface (JNI).
