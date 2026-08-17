# Java Regex and String Matching

> [!abstract] Định nghĩa
> **Regular Expression (Regex - Biểu thức chính quy)** là một chuỗi ký tự tạo thành một mẫu tìm kiếm (search pattern), dùng để tìm kiếm, so khớp (matching), thay thế và validate tính hợp lệ của chuỗi văn bản.
> Java hỗ trợ xử lý Regex thông qua các lớp thuộc gói **`java.util.regex`** (chủ yếu là `Pattern` và `Matcher`).

---

## 1. Các lớp cốt lõi: Pattern và Matcher

Để xử lý Regex nâng cao, Java cung cấp hai lớp chính:

1. **`Pattern`:** Đối tượng đại diện cho biểu thức chính quy đã được biên dịch (compiled regex).
2. **`Matcher`:** Công cụ thực hiện các phép so khớp trên một chuỗi cụ thể dựa trên `Pattern` đã tạo.

### Bảng tham chiếu API của Pattern và Matcher

| Class | Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- | --- |
| **Pattern** | `Pattern.compile(String regex)` | Biên dịch mẫu regex | Tạo đối tượng `Pattern` đại diện cho biểu thức. | Khởi tạo | Tải một lần để dùng nhiều lần |
| **Pattern** | `matcher(CharSequence input)` | Tạo Matcher | Tạo đối tượng `Matcher` để so khớp trên chuỗi `input`. | Khởi tạo công cụ | Gắn với một chuỗi đầu vào |
| **Matcher** | `matches()` | So khớp toàn bộ | Trả về `true` nếu toàn bộ chuỗi khớp với mẫu regex. | Xác thực dữ liệu | Khớp toàn bộ chuỗi |
| **Matcher** | `find()` | Tìm kiếm chuỗi con | Tìm kiếm chuỗi con tiếp theo khớp với mẫu regex. | Tìm kiếm lặp | Trả về `true` mỗi lần tìm thấy |
| **Matcher** | `group()` | Lấy chuỗi khớp | Trả về chuỗi con đã tìm thấy ở lần so khớp `find()` trước đó. | Trích xuất dữ liệu | Chỉ gọi được sau khi `find()` trả về true |
| **Matcher** | `replaceAll(String replacement)` | Thay thế tất cả | Thay thế tất cả các chuỗi con khớp với regex bằng `replacement`. | Thay thế | Tiện lợi hơn làm việc thủ công |

---

## 2. Bảng tham chiếu String Regex API

Lớp `String` trong Java tích hợp sẵn các phương thức hỗ trợ Regex tiện lợi:

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `matches(String regex)` | So khớp nhanh | Kiểm tra xem toàn bộ chuỗi hiện tại có khớp với `regex` không. | Xác thực nhanh | Thực chất gọi `Pattern.matches()` |
| `replaceAll(regex, replacement)` | Thay thế chuỗi | Thay thế tất cả ký tự khớp bằng `replacement`. | Sửa đổi chuỗi | Trả về chuỗi mới |
| `split(String regex)` | Tách chuỗi | Tách chuỗi thành mảng dựa trên ký tự phân tách `regex`. | Phân tích cú pháp | Rất mạnh khi tách dấu cách |

---

## 3. Bảng ký tự Regex và Mẫu phổ biến

> [!info] Bảng cú pháp ký hiệu Regex
> | Ký tự / Mẫu | Ý nghĩa | Ví dụ khớp |
> | --- | --- | --- |
> | `.` | Bất kỳ ký tự đơn nào. | `a.b` khớp `acb` |
> | `^` | Bắt đầu chuỗi. | `^Admin` khớp chuỗi bắt đầu bằng Admin |
> | `$` | Kết thúc chuỗi. | `end$` khớp chuỗi kết thúc bằng end |
> | `\d` | Một chữ số (tương đương `[0-9]`). **Trong Java viết là `\\d`**. | `\\d{3}` khớp `123` |
> | `\D` | Ký tự không phải số. **Trong Java viết là `\\D`**. | `\\D` khớp `a` |
> | `\w` | Ký tự chữ, số hoặc dấu gạch dưới. | `\\w` khớp `a`, `1`, `_` |
> | `\W` | Ký tự đặc biệt (không phải chữ/số). | `\\W` khớp `@`, `#` |
> | `\s` | Khoảng trắng (space, tab, xuống dòng). | `\\s` khớp khoảng trắng |
> | `*` | Xuất hiện từ 0 hoặc nhiều lần. | `ab*` khớp `a`, `ab`, `abbb` |
> | `+` | Xuất hiện từ 1 hoặc nhiều lần. | `ab+` khớp `ab`, `abbb` |
> | `?` | Xuất hiện 0 hoặc 1 lần. | `ab?` khớp `a`, `ab` |
> | `{n}` | Xuất hiện đúng `n` lần. | `\\d{3}` khớp `456` |
> | `{n,m}` | Xuất hiện từ `n` đến `m` lần. | `\\d{3,5}` khớp `1234` |

---

## 4. Ví dụ / Example

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class RegexDemo {
    private static final Pattern PHONE_PATTERN = Pattern.compile("^0\\d{9}$");
    private static final Pattern WORD_PATTERN = Pattern.compile("\\b\\w+\\b");

    public static void main(String[] args) {
        // 1. matches() - Validate
        boolean isValid = PHONE_PATTERN.matcher("0123456789").matches(); // true

        // 2. find() và group() - Tìm kiếm và trích xuất tất cả từ trong chuỗi
        String text = "Java is fun";
        Matcher matcher = WORD_PATTERN.matcher(text);
        while (matcher.find()) {
            System.out.println("Từ tìm thấy: " + matcher.group()); // "Java", "is", "fun"
        }

        // 3. String Regex API
        String csv = "Apple, Banana, Orange";
        String[] fruits = csv.split(",\\s*"); // Tách bằng dấu phẩy và khoảng trắng tùy chọn

        String cleanText = "A1 B2 C3".replaceAll("\\d", ""); // "A B C"
    }
}
```

---

## Lưu ý quan trọng

> [!warning]
> - Do ký tự `\` là ký tự thoát (escape character) trong String Java, nên khi viết các mẫu Regex chứa `\`, bắt buộc phải viết **double backslash (`\\`)** (ví dụ: `\\d`, `\\w`, `\\s`).
> - Tránh dùng `Pattern.matches(regex, input)` liên tục trong các vòng lặp lớn vì phương thức static này tự biên dịch lại Regex mỗi lần gọi, làm giảm nghiêm trọng hiệu năng hệ thống. Hãy khởi tạo `Pattern` tĩnh (`static final`) trước.
