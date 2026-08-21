# Java DateTimeFormatter

> [!abstract] Định nghĩa
> **`java.time.format.DateTimeFormatter`** là lớp dùng để định dạng (format - chuyển đối tượng thành String) và phân tích cú pháp (parse - chuyển String thành đối tượng) các giá trị ngày giờ trong Java 8+ (xem chi tiết lớp ngày tháng tại [[03 - LocalDate]]). Lớp này là **bất biến (immutable) và an toàn luồng (thread-safe)**, thay thế hoàn toàn cho `SimpleDateFormat` cũ vốn không an toàn khi dùng đa luồng.

---

## 1. Bảng ký tự Pattern phổ biến

| Ký tự | Ý nghĩa | Ví dụ |
| :--- | :--- | :--- |
| `y` / `yyyy` | Năm | `2026` |
| `M` / `MM` | Tháng (dạng số) | `8` hoặc `08` |
| `MMM` | Tháng (dạng chữ viết tắt) | `Aug` (tiếng Anh) hoặc `Thg 8` (tiếng Việt) |
| `MMMM` | Tháng (dạng chữ đầy đủ) | `August` hoặc `Tháng tám` |
| `d` / `dd` | Ngày trong tháng | `9` hoặc `09` |
| `H` / `HH` | Giờ trong ngày (0-23) | `14` |
| `h` / `hh` | Giờ sáng/chiều (1-12) | `02` (đi kèm AM/PM) |
| `m` / `mm` | Phút | `05` |
| `s` / `ss` | Giây | `59` |
| `a` | Dấu hiệu AM/PM | `PM` |

---

## 2. Bảng tham chiếu các phương thức cốt lõi

| Method | Kiểu trả về | Tác dụng | Ví dụ |
| :--- | :--- | :--- | :--- |
| `ofPattern(String pattern)` | `DateTimeFormatter` | Tạo một bộ định dạng tùy chỉnh theo chuỗi mẫu `pattern`. | `DateTimeFormatter.ofPattern("dd/MM/yyyy")` |
| `ofPattern(pattern, Locale)`| `DateTimeFormatter` | Tạo bộ định dạng có áp dụng ngôn ngữ `Locale` (dành cho tháng dạng chữ `MMM`/`MMMM`). | `DateTimeFormatter.ofPattern("dd-MMM-yyyy", Locale.ENGLISH)` |
| `format(TemporalAccessor t)`| `String` | Chuyển đổi đối tượng ngày giờ `t` thành chuỗi ký tự theo mẫu đã cấu hình. | `formatter.format(LocalDate.now())` |
| `parse(CharSequence text)` | `TemporalAccessor` | Phân tích cú pháp chuỗi `text` để trích xuất thông tin thời gian thô. | `formatter.parse("19-08-2026")` |

---

## 3. Ví dụ minh họa

### 3.1. Chuyển đổi LocalDate ↔ String
```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

public class DateTimeFormatExample {
    public static void main(String[] args) {
        LocalDate today = LocalDate.now();

        // 1. Định dạng (LocalDate -> String)
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
        String formattedDate = today.format(formatter); // Hoặc: formatter.format(today)
        System.out.println("Ngày định dạng: " + formattedDate); // Ví dụ: 19/08/2026

        // 2. Phân tích cú pháp (String -> LocalDate)
        String dateStr = "25/12/2026";
        LocalDate parsedDate = LocalDate.parse(dateStr, formatter);
        System.out.println("Ngày parse được: " + parsedDate); // 2026-12-25
    }
}
```

### 3.2. Sử dụng Locale cho định dạng tháng chữ (`MMM` hoặc `MMMM`)
```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.util.Locale;

public class LocaleDateTimeExample {
    public static void main(String[] args) {
        String input = "29-Feb-2024"; // Năm nhuận có ngày 29/02
        
        // Cần truyền Locale.ENGLISH để nhận diện chữ viết tắt "Feb" thay vì ngôn ngữ mặc định của máy
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MMM-yyyy", Locale.ENGLISH);
        
        LocalDate date = LocalDate.parse(input, formatter);
        System.out.println("Parse Locale thành công: " + date); // 2024-02-29
    }
}
```

---

## 4. Lưu ý

> [!important]
> - Do `DateTimeFormatter` là an toàn luồng, bạn nên khai báo nó dưới dạng **hằng số `static final`** trong các class tiện ích để tái sử dụng, giúp tránh việc khởi tạo đối tượng nhiều lần gây lãng phí bộ nhớ.
> - Lớp `DateTimeFormatter` sẽ ném ra ngoại lệ `DateTimeParseException` nếu chuỗi đầu vào không khớp hoàn toàn với định dạng mẫu pattern hoặc chứa ngày tháng phi lý (ví dụ: ngày 30 tháng 2).
