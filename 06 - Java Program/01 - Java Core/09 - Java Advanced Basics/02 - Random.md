# Java Random (Tạo số ngẫu nhiên)

> [!abstract] Định nghĩa
> **`Random`** là một lớp thuộc gói `java.util`, cung cấp công cụ sinh chuỗi các số giả ngẫu nhiên (pseudo-random numbers) phục vụ cho các bài toán mô phỏng, trò chơi, hoặc sinh dữ liệu mẫu thông thường.

---

## 1. Bảng tham chiếu các phương thức và Constructor của Random

| Method / Constructor | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `Random()` | Constructor không tham số | Khởi tạo bộ sinh số ngẫu nhiên sử dụng seed mặc định (thường lấy theo thời gian hệ thống hiện tại). | Khởi tạo | Tạo ra các chuỗi số ngẫu nhiên khác nhau giữa các lần chạy. |
| `Random(long seed)` | Constructor nhận hạt giống (seed) | Khởi tạo bộ sinh số ngẫu nhiên với một giá trị `seed` cố định. | Khởi tạo | Cùng một `seed` sẽ sinh ra chuỗi số ngẫu nhiên hoàn toàn giống hệt nhau ở mọi lần chạy (tính tái lập). |
| `nextInt()` | Sinh số nguyên ngẫu nhiên | Trả về một số nguyên `int` ngẫu nhiên trong toàn bộ phạm vi giá trị của kiểu `int`. | Sinh dữ liệu | Nhận giá trị từ $-2^{31}$ đến $2^{31}-1$. |
| `nextInt(int bound)` | Sinh số nguyên trong khoảng | Trả về một số nguyên `int` ngẫu nhiên nằm trong khoảng từ `0` (bao gồm) đến `bound` (không bao gồm): $[0, \text{bound})$. | Sinh dữ liệu | `bound` phải lớn hơn `0`, nếu không sẽ ném ra `IllegalArgumentException`. |
| `nextLong()` | Sinh số nguyên lớn ngẫu nhiên | Trả về một số nguyên `long` ngẫu nhiên trong toàn bộ phạm vi giá trị của kiểu `long`. | Sinh dữ liệu | Thường dùng cho các định danh lớn hoặc timestamp ngẫu nhiên. |
| `nextDouble()` | Sinh số thực ngẫu nhiên | Trả về một số thực kiểu `double` ngẫu nhiên nằm trong khoảng từ $0.0$ (bao gồm) đến $1.0$ (không bao gồm): $[0.0, 1.0)$. | Sinh dữ liệu | Rất hữu ích khi cần tính tỷ lệ phần trăm hoặc xác suất. |
| `nextBoolean()` | Sinh giá trị boolean ngẫu nhiên | Trả về giá trị logic ngẫu nhiên là `true` hoặc `false` với xác suất tương đương nhau (50/50). | Sinh dữ liệu | Giống như trò chơi tung đồng xu. |

---

## 2. Ví dụ thực tế sử dụng lớp Random

```java
import java.util.Random;

public class RandomDemo {
    public static void main(String[] args) {
        // 1. Khởi tạo Random không seed (mặc định)
        Random rand = new Random();

        // Sinh các kiểu dữ liệu khác nhau
        int randomInt = rand.nextInt();
        double randomDouble = rand.nextDouble(); // Khoảng [0.0, 1.0)
        boolean randomBool = rand.nextBoolean();

        // 2. Sinh số nguyên trong một khoảng cụ thể [min, max]
        // ✅ Nên làm (Do): Sử dụng công thức chính xác để lấy số trong khoảng chỉ định
        int min = 10;
        int max = 50;
        int randomInRange = rand.nextInt((max - min) + 1) + min; // Khoảng [10, 50]
        System.out.println("Random [10, 50]: " + randomInRange);

        // 3. Sử dụng Seed để đảm bảo tính tái lập kết quả (phục vụ viết Unit Test hoặc kiểm thử)
        Random fixedRand1 = new Random(999L);
        Random fixedRand2 = new Random(999L);
        
        System.out.println("fixedRand1: " + fixedRand1.nextInt(100)); // Luôn ra cùng 1 kết quả
        System.out.println("fixedRand2: " + fixedRand2.nextInt(100)); // Trùng khớp kết quả với fixedRand1
    }
}
```

---

## 3. Lưu ý quan trọng về bảo mật và đa luồng

> [!warning]
> - **Không an sau bảo mật (Non-cryptographically secure):** Lớp `Random` sinh số giả ngẫu nhiên có thể dự đoán được chuỗi tiếp theo nếu biết seed. Vì vậy, **không sử dụng** `Random` để tạo mật khẩu, OTP, token bảo mật. Thay vào đó, bắt buộc sử dụng **`java.security.SecureRandom`**.
> - **Hiệu năng đa luồng:** Lớp `Random` an toàn với đa luồng (thread-safe), nhưng việc nhiều luồng tranh chấp tài nguyên trên một đối tượng `Random` duy nhất sẽ gây giảm hiệu năng. Trong môi trường đa luồng, khuyến khích sử dụng **`java.util.concurrent.ThreadLocalRandom.current()`** thay thế.
