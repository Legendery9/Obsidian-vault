# Java System Class

> [!abstract] Định nghĩa
> **`java.lang.System`** là một lớp final không thể khởi tạo, cung cấp các trường dữ liệu và phương thức tĩnh để tương tác với hệ thống, máy ảo Java (JVM), hệ điều hành và luồng đầu vào/đầu ra tiêu chuẩn.

---

## 1. Tác dụng
- **Đo lường thời gian & hiệu năng:** Theo dõi thời gian thực hiện của mã nguồn.
- **Sao chép mảng hiệu năng cao:** Sử dụng mã máy (native code) trực tiếp để copy dữ liệu mảng.
- **Truy cập cấu hình môi trường:** Lấy biến hệ điều hành hoặc thiết lập tham số cho JVM.
- **Quản lý dòng I/O chuẩn:** Sử dụng `System.out` để ghi log ra màn hình, `System.err` để ghi lỗi, và `System.in` để nhận phím bấm đầu vào.

---

## 2. Bảng tham chiếu các phương thức thông dụng

| Method | Kiểu trả về | Tác dụng | Lưu ý |
| :--- | :--- | :--- | :--- |
| `currentTimeMillis()` | `long` | Trả về thời gian hiện tại tính bằng mili-giây kể từ mốc Epoch (00:00:00 UTC ngày 1/1/1970). | Thường dùng để lấy mốc thời gian ngày giờ hiện tại. |
| `nanoTime()` | `long` | Trả về thời gian đo bằng nano-giây từ một mốc thời gian tùy ý của JVM. | Dùng duy nhất để đo khoảng thời gian chạy code, không dùng làm mốc lịch ngày tháng. |
| `arraycopy(src, srcPos, dest, destPos, len)`| `void` | Sao chép một phần mảng nguồn `src` sang mảng đích `dest` cực kỳ nhanh. | Được triển khai dưới dạng native code nên tốc độ tối ưu hơn nhiều so với vòng lặp thủ công. |
| `getenv(String name)` | `String` | Lấy giá trị của một biến môi trường hệ điều hành. | Trả về `null` nếu biến không tồn tại. |
| `getProperty(String key)`| `String` | Lấy giá trị thuộc tính hệ thống của máy ảo JVM. | Ví dụ lấy hệ điều hành: `os.name`, thư mục người dùng: `user.home`. |
| `gc()` | `void` | Gợi ý (request) JVM thực hiện tiến trình dọn rác giải phóng bộ nhớ. | Chỉ mang tính chất đề xuất, JVM tự quyết định thời điểm dọn rác thực tế. |
| `exit(int status)` | `void` | Dừng hoạt động và thoát máy ảo JVM hiện tại. | Trạng thái `0` là thoát thành công, khác `0` đại diện cho thoát do có lỗi. |

---

## 3. Ví dụ minh họa

```java
import java.util.Arrays;

public class SystemClassExample {
    public static void main(String[] args) {
        // 1. Đo hiệu năng chạy code bằng nanoTime
        long start = System.nanoTime();
        
        // Đoạn code giả lập chạy tốn thời gian
        for (int i = 0; i < 1_000_000; i++) {
            Math.sin(i);
        }
        
        long duration = System.nanoTime() - start;
        System.out.println("Thời gian chạy: " + (duration / 1_000_000.0) + " ms");

        // 2. Sao chép mảng nhanh bằng arraycopy
        int[] src = {1, 2, 3, 4, 5};
        int[] dest = new int[5];
        System.arraycopy(src, 1, dest, 2, 3); // Copy {2, 3, 4} từ src[1] sang dest[2]
        System.out.println("Mảng đích sau khi copy: " + Arrays.toString(dest)); // Output: [0, 0, 2, 3, 4]

        // 3. Lấy thuộc tính hệ thống và biến môi trường
        String osName = System.getProperty("os.name");
        String userHome = System.getProperty("user.home");
        String pathEnv = System.getenv("PATH");

        System.out.println("Hệ điều hành: " + osName);
        System.out.println("Thư mục người dùng: " + userHome);
    }
}
```

---

## 4. Lưu ý

> [!caution]
> - Tránh lạm dụng `System.exit(status)` trong các ứng dụng Web hoặc ứng dụng chạy trên Container (như Tomcat, WildFly) vì lệnh này sẽ tắt toàn bộ Server ứng dụng chứ không chỉ dừng luồng nghiệp vụ hiện tại.
