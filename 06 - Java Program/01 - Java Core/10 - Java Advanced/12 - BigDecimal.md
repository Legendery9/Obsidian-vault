# Java BigDecimal

> [!abstract] Định nghĩa
> **`java.math.BigDecimal`** là một lớp bất biến (immutable), đại diện cho các số thực có độ chính xác tùy ý và có dấu. Lớp này được thiết kế để giải quyết triệt để lỗi sai số làm tròn dấu phẩy động của kiểu `float` và `double` (chuẩn IEEE 754), thường được dùng trong lập trình tính toán tiền tệ, tài chính, hoặc đo lường khoa học chính xác.

---

## 1. Vấn đề sai số của `double` (Tại sao cần BigDecimal?)

Trong Java, các phép tính số thực cơ bản với `double` có thể dẫn đến kết quả bất ngờ do cơ chế lưu trữ nhị phân không thể biểu diễn chính xác một số số thập phân:

```java
double a = 0.1;
double b = 0.2;
System.out.println(a + b); // Output: 0.30000000000000004 (Sai số!)
```

`BigDecimal` loại bỏ hoàn toàn hiện tượng này bằng cách lưu trữ số dưới dạng số nguyên không giới hạn chiều dài và một số mũ quy định vị trí dấu phẩy thập phân.

---

## 2. Bảng tham chiếu các phương thức quan trọng

| Method | Kiểu trả về | Tác dụng | Lưu ý |
| :--- | :--- | :--- | :--- |
| `BigDecimal(String val)` | Constructor | Khởi tạo `BigDecimal` từ chuỗi. | **Khuyên dùng nhất** vì nó bảo toàn chính xác giá trị truyền vào. |
| `BigDecimal(double val)` | Constructor | Khởi tạo từ số thực `double`. | ❌ **Không nên dùng** vì nó vẫn kéo theo sai số nội tại của kiểu double vào BigDecimal. |
| `BigDecimal.valueOf(double d)`| `BigDecimal` | Phương thức tĩnh tạo BigDecimal từ double. | An toàn hơn constructor `double` vì nó tự động dùng `Double.toString(d)` để chuyển đổi trước. |
| `add(BigDecimal val)` | `BigDecimal` | Phép cộng: $this + val$. | Trả về đối tượng `BigDecimal` mới do tính chất bất biến. |
| `subtract(BigDecimal val)` | `BigDecimal` | Phép trừ: $this - val$. | |
| `multiply(BigDecimal val)` | `BigDecimal` | Phép nhân: $this \times val$. | |
| `divide(BigDecimal divisor)` | `BigDecimal` | Phép chia: $this \div divisor$. | Ném ra `ArithmeticException` nếu kết quả là số thập phân vô hạn tuần hoàn (như $1 \div 3$). |
| `divide(BigDecimal div, int scale, RoundingMode mode)`| `BigDecimal` | Phép chia có định vị chữ số thập phân (`scale`) và chế độ làm tròn (`RoundingMode`). | **Bắt buộc dùng** khi thực hiện phép chia để tránh crash chương trình. |
| `setScale(int scale, RoundingMode mode)`| `BigDecimal` | Thiết lập số lượng chữ số sau dấu phẩy thập phân và áp dụng làm tròn. | Dùng để làm tròn giá trị cuối cùng hiển thị cho người dùng. |
| `compareTo(BigDecimal val)` | `int` | So sánh giá trị toán học của hai đối tượng. | Trả về $-1$ (nhỏ hơn), $0$ (bằng nhau), $1$ (lớn hơn). Bỏ qua độ dài phần thập phân (ví dụ `1.0` so sánh bằng `1.00`). |
| `equals(Object o)` | `boolean` | So sánh hai đối tượng BigDecimal. | Nhạy cảm với cấu trúc băm (Coi `1.0` khác `1.00` vì khác `scale`). Tránh dùng để so sánh giá trị toán học. |

---

## 3. Ví dụ minh họa

```java
import java.math.BigDecimal;
import java.math.RoundingMode;

public class BigDecimalExample {
    public static void main(String[] args) {
        // 1. Khởi tạo: Luôn sử dụng String constructor
        BigDecimal price = new BigDecimal("100.05");
        BigDecimal taxRate = new BigDecimal("0.08"); // Thuế 8%

        // 2. Phép tính Cộng, Trừ, Nhân
        BigDecimal tax = price.multiply(taxRate); // 100.05 * 0.08 = 8.004
        BigDecimal total = price.add(tax);        // 100.05 + 8.004 = 108.054
        
        System.out.println("Thuế: " + tax);
        System.out.println("Tổng cộng (chưa làm tròn): " + total);

        // 3. Phép chia: Bắt buộc chỉ định scale và RoundingMode
        BigDecimal divisor = new BigDecimal("3");
        BigDecimal splitAmount = total.divide(divisor, 2, RoundingMode.HALF_UP); // Chia 3, lấy 2 chữ số thập phân, làm tròn lên
        System.out.println("Chia 3 làm tròn: " + splitAmount); // 108.054 / 3 = 36.018 -> 36.02

        // 4. Định dạng lại tỷ lệ thập phân (Rounding)
        BigDecimal finalTotal = total.setScale(2, RoundingMode.HALF_UP); // Làm tròn tổng tiền về 2 chữ số thập phân: 108.05
        System.out.println("Tổng cộng làm tròn: " + finalTotal);

        // 5. So sánh giá trị: Luôn dùng compareTo thay vì equals
        BigDecimal num1 = new BigDecimal("1.0");
        BigDecimal num2 = new BigDecimal("1.00");
        
        System.out.println("So sánh equals: " + num1.equals(num2)); // false (vì khác scale)
        System.out.println("So sánh compareTo: " + (num1.compareTo(num2) == 0)); // true (bằng nhau về giá trị toán học)
    }
}
```

---

## 4. Lưu ý

> [!important]
> - **Nguyên tắc bất biến (Immutability):** Giống như lớp `String`, các phép tính toán trên `BigDecimal` không làm thay đổi giá trị của đối tượng hiện tại mà luôn sinh ra một đối tượng `BigDecimal` mới chứa kết quả. Do đó, bạn phải gán lại kết quả:
>   `amount = amount.add(bonus);` thay vì viết `amount.add(bonus);` suông.
