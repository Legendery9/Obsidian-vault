# Java Math and Numbers

> [!abstract] Định nghĩa
> Lớp **`java.lang.Math`** cung cấp các hằng số và phương thức static để thực hiện các phép toán cơ bản như lượng giác, logarit, lũy thừa, căn bậc hai và làm tròn số.
> **`StrictMath`** tương tự như `Math` nhưng đảm bảo kết quả tính toán số thực hoàn toàn giống nhau trên mọi nền tảng phần cứng (tuân thủ chặt chẽ chuẩn IEEE 754), đánh đổi bằng tốc độ thực thi chậm hơn.

---

## Bảng tham chiếu các phương thức Math phổ biến

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `Math.PI` | Hằng số Pi | Hằng số tỷ lệ chu vi đường tròn so với đường kính ($\approx 3.14159$). | Hằng số toán học | Kiểu `double`, static final |
| `Math.E` | Hằng số Euler | Cơ số của logarit tự nhiên ($\approx 2.71828$). | Hằng số toán học | Kiểu `double`, static final |
| `Math.abs(x)` | Trị tuyệt đối | Trả về giá trị tuyệt đối (luôn dương) của `x`. | Số học cơ bản | Hỗ trợ kiểu `int`, `long`, `float`, `double` |
| `Math.max(a, b)` / `min` | Lớn nhất / Nhỏ nhất | Trả về số lớn nhất hoặc nhỏ nhất trong hai số `a` và `b`. | So sánh | Hỗ trợ nhiều kiểu dữ liệu số |
| `Math.pow(base, exp)` | Lũy thừa | Trả về lũy thừa của `base` với số mũ `exp` ($base^{exp}$). | Số học cơ bản | Nhận và trả về kiểu `double` |
| `Math.sqrt(x)` | Căn bậc hai | Trả về căn bậc hai của `x` ($\sqrt{x}$). | Số học cơ bản | Trả về `NaN` (Not a Number) nếu `x < 0` |
| `Math.random()` | Tạo số ngẫu nhiên | Trả về một số thực ngẫu nhiên từ $0.0$ đến sát $1.0$ ($[0.0, 1.0)$). | Ngẫu nhiên | Thường nhân thêm hệ số để đổi khoảng |
| `Math.ceil(x)` | Làm tròn lên | Trả về số nguyên nhỏ nhất lớn hơn hoặc bằng `x` (làm tròn lên). | Làm tròn số | Trả về kiểu `double` |
| `Math.floor(x)` | Làm tròn xuống | Trả về số nguyên lớn nhất nhỏ hơn hoặc bằng `x` (làm tròn xuống). | Làm tròn số | Trả về kiểu `double` |
| `Math.round(x)` | Làm tròn toán học | Làm tròn `x` tới số nguyên gần nhất (bằng cách cộng $0.5$ và lấy phần nguyên). | Làm tròn số | Trả về `int` nếu input là `float`, trả về `long` nếu là `double` |

---

## Ví dụ / Example

```java
public class MathExample {
    public static void main(String[] args) {
        // 1. Trị tuyệt đối & Lớn nhất/Nhỏ nhất
        int absolute = Math.abs(-10); // 10
        int maximum = Math.max(5, 20); // 20

        // 2. Lũy thừa & Căn bậc hai
        double power = Math.pow(2, 3); // 8.0 (2^3)
        double squareRoot = Math.sqrt(16); // 4.0

        // 3. Số ngẫu nhiên trong khoảng [1, 10]
        // ✅ Nên làm (Do): Ép kiểu int sau khi nhân hệ số để lấy số nguyên ngẫu nhiên
        int randomNum = (int) (Math.random() * 10) + 1;

        // 4. Làm tròn số
        double val = 5.4;
        double ceilVal = Math.ceil(val);   // 6.0 (Làm tròn lên)
        double floorVal = Math.floor(val); // 5.0 (Làm tròn xuống)
        long roundedVal = Math.round(val);   // 5 (Làm tròn toán học)

        // 5. Khác biệt của round khi truyền float vs double
        float fVal = 5.6f;
        int roundedFloat = Math.round(fVal); // Trả về kiểu int: 6
        
        double dVal = 5.6;
        long roundedDouble = Math.round(dVal); // Trả về kiểu long: 6
    }
}
```

---

## Lưu ý quan trọng

> [!warning] Làm tròn số thực âm với Math.round
> Phương thức `Math.round` hoạt động bằng cách cộng thêm $0.5$ rồi lấy sàn của số thực (`Math.floor(x + 0.5)`). Hãy lưu ý kết quả khi làm việc với số âm:
> - `Math.round(-1.5)` $\rightarrow$ cộng $0.5$ thành $-1.0 \rightarrow$ làm tròn thành **`-1`** (chứ không phải `-2`).
> - `Math.round(-1.6)` $\rightarrow$ cộng $0.5$ thành $-1.1 \rightarrow$ làm tròn thành **`-2`**.
