# Java LocalDate (Quản lý Ngày tháng hiện đại)

> [!abstract] Định nghĩa
> **`LocalDate`** là một lớp bất biến (immutable) và an toàn luồng (thread-safe) thuộc gói `java.time` (được giới thiệu từ Java 8). Lớp này đại diện cho một ngày cụ thể (năm-tháng-ngày) mà không có múi giờ (timezone) và không có giờ/phút/giây. Nó được thiết kế để hoàn toàn thay thế các lớp cũ đã lỗi thời và không an toàn luồng như `java.util.Date` và `java.util.Calendar`.

---

## 1. Tại sao nên dùng `LocalDate` thay thế `Date`/`Calendar` cũ?

- **Tính bất biến (Immutability):** `LocalDate` không thể thay đổi giá trị sau khi tạo. Mọi thao tác sửa đổi ngày đều trả về một đối tượng `LocalDate` mới.
- **An toàn luồng (Thread-safe):** Nhờ tính bất biến, `LocalDate` an toàn khi sử dụng trong môi trường đa luồng mà không cần đồng bộ hóa.
- **API rõ ràng, trực quan:** Cung cấp các phương thức tính toán ngày tháng tự nhiên, dễ đọc.
- **Không chứa múi giờ (Timezone-free):** Hạn chế các lỗi sai lệch giờ do lệch múi giờ (nếu cần múi giờ, hãy sử dụng `ZonedDateTime` hoặc `OffsetDateTime`).

---

## 2. Bảng tham chiếu các phương thức `LocalDate` phổ biến

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| :--- | :--- | :--- | :--- | :--- |
| `LocalDate.now()` | Lấy ngày hiện tại | Khởi tạo đối tượng `LocalDate` trỏ đến ngày hôm nay theo giờ hệ thống. | Khởi tạo | Sử dụng múi giờ mặc định của JVM. |
| `LocalDate.of(int year, int month, int day)` | Khởi tạo ngày cụ thể | Tạo đối tượng ngày bằng cách truyền trực tiếp các giá trị năm, tháng, ngày. | Khởi tạo | Ném ra `DateTimeException` nếu ngày truyền vào không hợp lệ (VD: 30/02). |
| `LocalDate.parse(CharSequence text)` | Phân tích chuỗi thành ngày | Chuyển đổi một chuỗi văn bản định dạng chuẩn ISO-8601 (`yyyy-MM-dd`) thành ngày. | Khởi tạo / Parse | Ném ra `DateTimeParseException` nếu chuỗi sai định dạng. |
| `plusDays(long days)` / `minusDays(long days)` | Cộng/Trừ số ngày | Tăng hoặc giảm số ngày chỉ định của đối tượng hiện tại và trả về đối tượng mới. | Tính toán ngày | Đối tượng ban đầu không thay đổi giá trị (Bất biến). |
| `plusMonths(long months)` / `minusMonths(long months)` | Cộng/Trừ số tháng | Tăng hoặc giảm số tháng chỉ định của đối tượng hiện tại và trả về đối tượng mới. | Tính toán ngày | JVM tự động xử lý ngày cuối tháng (VD: 31/08 - 1 tháng = 30/07). |
| `isBefore(ChronoLocalDate other)` | So sánh ngày đứng trước | Kiểm tra xem ngày hiện tại có đứng trước ngày được truyền vào hay không. | So sánh | Trả về `boolean`. |
| `isAfter(ChronoLocalDate other)` | So sánh ngày đứng sau | Kiểm tra xem ngày hiện tại có đứng sau ngày được truyền vào hay không. | So sánh | Trả về `boolean`. |
| `isEqual(ChronoLocalDate other)` | So sánh hai ngày bằng nhau | Kiểm tra xem hai ngày có cùng thời điểm hay không. | So sánh | Tương tự như phương thức `equals()`. |
| `getDayOfWeek()` | Lấy ngày trong tuần | Trả về đối tượng enum `DayOfWeek` đại diện cho thứ trong tuần (MONDAY đến SUNDAY). | Truy xuất | Có thể dùng `.getValue()` để lấy số từ 1 đến 7. |
| `format(DateTimeFormatter formatter)` | Định dạng ngày thành chuỗi | Chuyển đổi đối tượng `LocalDate` thành chuỗi văn bản theo định dạng tùy chỉnh. | Xuất dữ liệu | Kết hợp sử dụng lớp `java.time.format.DateTimeFormatter`. |

---

## 3. Ví dụ minh họa thực tế

Dưới đây là đoạn mã nguồn Java hoàn chỉnh, minh họa chi tiết tất cả các thao tác phổ biến trên lớp `LocalDate`:

```java
import java.time.LocalDate;
import java.time.DayOfWeek;
import java.time.format.DateTimeFormatter;
import java.time.temporal.ChronoUnit;

public class LocalDateDemo {
    public static void main(String[] args) {
        // 1. Khởi tạo ngày
        LocalDate today = LocalDate.now();
        System.out.println("1. Ngày hiện tại (now): " + today);

        LocalDate specificDate = LocalDate.of(2026, 8, 18);
        System.out.println("2. Ngày cụ thể (of): " + specificDate);

        LocalDate parsedDate = LocalDate.parse("2026-12-25");
        System.out.println("3. Ngày chuyển từ chuỗi (parse): " + parsedDate);

        // 2. Tính toán cộng/trừ ngày tháng
        LocalDate nextWeek = today.plusDays(7);
        LocalDate lastMonth = today.minusMonths(1);
        System.out.println("\n--- Tính toán ngày ---");
        System.out.println("Hôm nay: " + today);
        System.out.println("7 ngày sau: " + nextWeek);
        System.out.println("1 tháng trước: " + lastMonth);

        // Minh họa tính bất biến (Immutability)
        System.out.println("Ngày gốc 'today' vẫn giữ nguyên: " + today);

        // 3. So sánh ngày
        System.out.println("\n--- So sánh ngày ---");
        boolean isBefore = specificDate.isBefore(parsedDate);
        boolean isAfter = specificDate.isAfter(parsedDate);
        boolean isEqual = specificDate.isEqual(LocalDate.of(2026, 8, 18));

        System.out.println(specificDate + " đứng trước " + parsedDate + "? -> " + isBefore);
        System.out.println(specificDate + " đứng sau " + parsedDate + "? -> " + isAfter);
        System.out.println(specificDate + " bằng ngày 2026-08-18? -> " + isEqual);

        // Tính khoảng cách giữa hai ngày bằng ChronoUnit
        long daysBetween = ChronoUnit.DAYS.between(specificDate, parsedDate);
        System.out.println("Số ngày chênh lệch giữa " + specificDate + " và " + parsedDate + " là: " + daysBetween + " ngày");

        // 4. Truy xuất thông tin chi tiết
        System.out.println("\n--- Truy xuất thông tin ---");
        DayOfWeek dayOfWeek = specificDate.getDayOfWeek();
        int dayOfMonth = specificDate.getDayOfMonth();
        int monthValue = specificDate.getMonthValue();
        int year = specificDate.getYear();

        System.out.println("Thứ trong tuần: " + dayOfWeek + " (Giá trị số: " + dayOfWeek.getValue() + ")");
        System.out.println("Ngày trong tháng: " + dayOfMonth);
        System.out.println("Tháng: " + monthValue);
        System.out.println("Năm: " + year);
        System.out.println("Năm nhuận? " + specificDate.isLeapYear());

        // 5. Định dạng ngày tháng bằng DateTimeFormatter
        System.out.println("\n--- Định dạng ngày tháng ---");
        DateTimeFormatter vietnameseFormatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
        String formattedDate = specificDate.format(vietnameseFormatter);
        System.out.println("Ngày định dạng dd/MM/yyyy: " + formattedDate);

        // Phân tích chuỗi định dạng tùy chỉnh
        LocalDate parsedCustom = LocalDate.parse("31/12/2026", vietnameseFormatter);
        System.out.println("Ngày phân tích từ chuỗi dd/MM/yyyy: " + parsedCustom);
    }
}
```

---

## 4. Liên hệ và Tránh trùng lặp

> [!note]
> - Lớp `LocalDate` chỉ quản lý thông tin ngày tháng (không có giờ). Nếu bạn cần quản lý cả giờ/phút/giây, hãy sử dụng **`LocalDateTime`**. Nếu chỉ cần giờ/phút/giây mà không quan tâm ngày tháng, hãy dùng **`LocalTime`**.
> - Cả ba lớp này đều nằm trong gói `java.time` và chia sẻ mô hình thiết kế bất biến tương tự nhau.
