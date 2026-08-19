# Java Format Specifiers

> [!abstract] Định nghĩa
> **Format Specifier (Trình định dạng)** trong Java là một chuỗi ký tự bắt đầu bằng ký tự `%` dùng để định nghĩa cách biểu diễn dữ liệu (chuỗi, số nguyên, số thực, ngày tháng...) dưới dạng chuỗi văn bản theo một khuôn mẫu mong muốn. Cơ chế này được sử dụng chủ yếu trong các phương thức của `String`, `PrintStream` (như `System.out.printf`) và class `Formatter`.

---

## 1. Cấu trúc tổng quát

Cú pháp tổng quát của một Format Specifier trong Java được định nghĩa như sau:

```text
%[argument_index$][flags][width][.precision]conversion
```

Giải thích chi tiết các thành phần trong cấu trúc trên:

> [!info] Các thành phần của Format Specifier
> | Thành phần | Ý nghĩa | Bắt buộc? | Ví dụ & Tác dụng |
> | :--- | :--- | :--- | :--- |
> | **`argument_index$`** | Chỉ định vị trí tham số (bắt đầu từ `1$`) sẽ được format, dùng khi muốn tham chiếu lại hoặc đổi thứ tự tham số. | Không | `%2$s` lấy tham số thứ hai; `%1$d` lấy tham số thứ nhất. |
> | **`flags`** | Cờ định dạng bổ sung (căn trái `-`, luôn hiện dấu `+`, đệm số 0 `0`, phân tách hàng nghìn `,`, bao đóng số âm `(`...). | Không | `%-10s` (căn trái), `%+d` (luôn hiển thị dấu dương/âm). |
> | **`width`** | Độ rộng tối thiểu của kết quả (số lượng ký tự tối thiểu hiển thị ra). Nếu dữ liệu ngắn hơn, hệ thống tự động chèn khoảng trắng hoặc số `0`. | Không | `%10d` (chuỗi dài tối thiểu 10 ký tự, căn phải). |
> | **`.precision`** | Số chữ số thập phân (với số thực) hoặc số ký tự tối đa được lấy (với chuỗi). | Không | `%.2f` (lấy 2 số sau dấu phẩy); `%.5s` (chỉ lấy tối đa 5 ký tự đầu). |
> | **`conversion`** | Ký tự quy định kiểu dữ liệu/định dạng đầu ra (`s`, `d`, `f`, `x`, `n`...). | **Bắt buộc** | `%s` (chuỗi), `%d` (số nguyên), `%f` (số thực). |

---

## 2. Bảng Format Specifiers (conversion) đầy đủ

Dưới đây là các conversion characters phổ biến và thường dùng nhất trong Java:

> [!info] Bảng ký tự Conversion & Flags phổ biến
> | Specifier | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
> | :--- | :--- | :--- | :--- | :--- |
> | **`%s`** | Định dạng chuỗi (String) | Biểu diễn giá trị dưới dạng chuỗi, tự động gọi `toString()` với đối tượng truyền vào. | `%s`, `%10s` (căn phải rộng 10), `%-10s` (căn trái rộng 10) | Nếu đối tượng truyền vào là `null`, kết quả in ra là `"null"`. |
> | **`%d`** | Định dạng số nguyên (decimal) | Biểu diễn số nguyên ở hệ cơ số 10. | `%d`, `%5d`, `%05d` (đệm số 0 cho đủ 5 chữ số) | Chỉ dùng cho số nguyên (`int`, `long`, `short`, `byte`), truyền số thực sẽ gây lỗi `IllegalFormatConversionException`. |
> | **`%f`** | Định dạng số thực (floating point) | Biểu diễn số thực dưới dạng thập phân. | `%f`, `%.2f` (lấy 2 chữ số thập phân), `%10.2f` | Mặc định hiển thị 6 chữ số thập phân nếu không chỉ định cụ thể `.precision`. |
> | **`%e` / `%E`** | Định dạng khoa học (scientific notation) | Biểu diễn số thực theo dạng ký hiệu khoa học ($a.bcE\pm xx$). | `%e`, `%.3e` (lấy 3 chữ số phần thập phân) | Ký tự `%E` viết hoa sẽ in ra chữ `E` viết hoa ở phần mũ. |
> | **`%x` / `%X`** | Định dạng hệ 16 (hexadecimal) | Biểu diễn số nguyên dưới dạng thập lục phân (hệ 16). | `%x`, `%08x` (đệm 0 rộng 8 ký tự), `%X` (in chữ hoa) | Chỉ dùng cho số nguyên. Không tự động thêm tiền tố `0x` trừ khi dùng kèm flag `#` (`%#x`). |
> | **`%o`** | Định dạng hệ 8 (octal) | Biểu diễn số nguyên dưới dạng bát phân (hệ 8). | `%o`, `%05o` | Chỉ áp dụng cho số nguyên. |
> | **`%c`** | Định dạng ký tự (character) | Biểu diễn một ký tự Unicode đơn lẻ. | `%c`, `%C` (tự động chuyển ký tự sang viết hoa) | Tham số phải là kiểu `char`, `Character` hoặc số nguyên đại diện cho mã Unicode hợp lệ. |
> | **`%b`** | Định dạng boolean | Biểu diễn giá trị logic (`true`/`false`). | `%b`, `%B` (in hoa thành `TRUE`/`FALSE`) | Với giá trị khác kiểu `Boolean` hoặc `boolean`: nếu là `null` kết quả là `false`, các trường hợp còn lại đều trả về `true`. |
> | **`%n`** | Xuống dòng | Chèn ký tự xuống dòng phù hợp với hệ điều hành đang chạy (Line separator). | `%n` | Nên dùng `%n` thay thế cho `\n` để đảm bảo tính tương thích đa nền tảng (Windows dùng `\r\n`, Unix dùng `\n`). |
> | **`%%`** | Ký tự `%` literal | Hiển thị ký tự `%` trong chuỗi kết quả. | `%%` | Không nhận bất kỳ tham số nào đi kèm. |
> | **`%,d`** | Số nguyên phân tách hàng nghìn | Thêm dấu phân tách hàng nghìn vào số nguyên. | `%,d` | Ký tự phân tách phụ thuộc vào cấu hình hệ thống (`Locale`). Ví dụ Mỹ là `,`, Việt Nam/Đức là `.`. |
> | **`%+d`** | Luôn hiển thị dấu | Luôn in kèm dấu cộng `+` trước số dương và dấu trừ `-` trước số âm. | `%+d`, `%+f` | Áp dụng hiệu quả cho cả số nguyên và số thực. |

---

## 3. Ví dụ chi tiết cho từng Specifier

Dưới đây là các ví dụ code Java cụ thể cho từng specifier, mô tả rõ đầu vào và kết quả đầu ra thực tế:

### Ví dụ `%s` (String)
```java
String name = "Long";
String s1 = String.format("Hello %s", name);          // Kết quả: "Hello Long"
String s2 = String.format("Hello %10s", name);        // Kết quả: "Hello       Long" (độ rộng 10, căn phải)
String s3 = String.format("Hello %-10s!", name);      // Kết quả: "Hello Long      !" (độ rộng 10, căn trái)
String s4 = String.format("Data: %s", (Object) null); // Kết quả: "Data: null"
```

### Ví dụ `%d` (Decimal Integer)
```java
int score = 95;
String d1 = String.format("Score: %d", score);     // Kết quả: "Score: 95"
String d2 = String.format("Score: %5d", score);    // Kết quả: "Score:    95" (rộng 5, căn phải)
String d3 = String.format("Score: %-5d!", score);  // Kết quả: "Score: 95   !" (rộng 5, căn trái)
String d4 = String.format("Score: %05d", score);   // Kết quả: "Score: 00095" (đệm số 0 rộng 5)
```

### Ví dụ `%f` (Floating Point)
```java
double pi = 3.14159265;
String f1 = String.format("PI: %f", pi);       // Kết quả: "PI: 3.141593" (mặc định 6 chữ số thập phân, tự làm tròn)
String f2 = String.format("PI: %.2f", pi);     // Kết quả: "PI: 3.14" (lấy 2 chữ số thập phân)
String f3 = String.format("PI: %8.3f", pi);    // Kết quả: "PI:    3.142" (độ rộng 8, lấy 3 chữ số thập phân)
```

### Ví dụ `%e` / `%E` (Scientific Notation)
```java
double number = 12345.6789;
String e1 = String.format("%e", number);   // Kết quả: "1.234568e+04"
String e2 = String.format("%.3E", number); // Kết quả: "1.235E+04" (lấy 3 số thập phân, chữ E viết hoa)
```

### Ví dụ `%x` / `%X` (Hexadecimal)
```java
int decimal = 255;
String x1 = String.format("Hex: %x", decimal);    // Kết quả: "Hex: ff"
String x2 = String.format("Hex: %X", decimal);    // Kết quả: "Hex: FF"
String x3 = String.format("Hex: %04x", decimal);  // Kết quả: "Hex: 00ff" (đệm 0 độ rộng 4)
String x4 = String.format("Hex: %#X", decimal);   // Kết quả: "Hex: 0XFF" (thêm tiền tố 0X bằng flag #)
```

### Ví dụ `%o` (Octal)
```java
int decimal = 100;
String o1 = String.format("Octal: %o", decimal);   // Kết quả: "Octal: 144"
```

### Ví dụ `%c` (Character)
```java
char ch = 'a';
String c1 = String.format("Char: %c", ch);       // Kết quả: "Char: a"
String c2 = String.format("Char: %C", ch);       // Kết quả: "Char: A" (in hoa tự động)
String c3 = String.format("Char: %c", 65);       // Kết quả: "Char: A" (truyền mã Unicode/ASCII)
```

### Ví dụ `%b` (Boolean)
```java
String b1 = String.format("Bool: %b", true);           // Kết quả: "Bool: true"
String b2 = String.format("Bool: %b", (Object) null);  // Kết quả: "Bool: false" (null tương đương false)
String b3 = String.format("Bool: %b", "hello");        // Kết quả: "Bool: true" (không phải Boolean/null -> true)
```

### Ví dụ `%n` & `%%` (New Line & Literal %)
```java
String msg = String.format("Hoàn thành: 100%% %nXuống dòng mới!"); 
// Kết quả (trên Windows): 
// "Hoàn thành: 100% 
// Xuống dòng mới!"
```

### Ví dụ `%,d` & `%+d` (Separator & Signs)
```java
int money = 1000000;
int change = 50;
String s1 = String.format("Balance: %,d USD", money); // Kết quả: "Balance: 1,000,000 USD" (với US Locale)
String s2 = String.format("Delta: %+d", change);       // Kết quả: "Delta: +50"
String s3 = String.format("Delta: %+d", -25);          // Kết quả: "Delta: -25"
```

---

## 4. Các phương thức và lớp sử dụng Format Specifiers

Java cung cấp nhiều cách thức để định dạng chuỗi tuỳ thuộc vào nhu cầu lưu trữ hoặc hiển thị trực tiếp.

> [!info] Bảng so sánh các phương thức định dạng
> | Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
> | :--- | :--- | :--- | :--- | :--- |
> | **`String.format()`** | Phương thức static của lớp `String`. | Tạo và trả về chuỗi mới đã được định dạng, không in trực tiếp ra màn hình. | `String.format(format, args...)` | Thích hợp khi cần lưu trữ chuỗi hoặc truyền chuỗi làm giá trị trả về của hàm. |
> | **`System.out.printf()`** | Phương thức của đối tượng `PrintStream` (`System.out`). | Định dạng và ghi trực tiếp chuỗi kết quả ra màn hình console. | `System.out.printf(format, args...)` | Thực chất gọi tới `Formatter` nội bộ. Có thể dùng dạng chain vì trả về đối tượng `PrintStream`. |
> | **`Formatter`** | Lớp nền tảng thuộc gói `java.util`. | Ghi nội dung định dạng trực tiếp vào một luồng/bộ đệm đầu ra (`Appendable` như `StringBuilder`, file...). | `new Formatter(buffer).format(format, args...)` | Phù hợp khi muốn ghi log hoặc xây dựng luồng văn bản lớn hiệu năng cao. Phải đóng (`close()`) sau khi dùng. |
> | **`String.formatted()`** | Phương thức instance của lớp `String` (từ Java 15). | Gọi trực tiếp trên chuỗi định dạng mẫu thay vì gọi thông qua hàm static. | `formatPattern.formatted(args...)` | Cú pháp gọn gàng hơn `String.format()`. Yêu cầu phiên bản Java 15 trở lên. |

### Ví dụ minh hoạ thực tế từng phương thức

#### 1. Sử dụng `String.format()`
Dùng khi bạn muốn lưu trữ kết quả định dạng vào biến để sử dụng sau (ví dụ: hiển thị lên giao diện hoặc gửi qua API):
```java
public class StringFormatDemo {
    public static String buildWelcomeMessage(String username, int loginCount) {
        // Trả về chuỗi định dạng để xử lý tiếp, không in ra console
        return String.format("Chào mừng %s! Đây là lần đăng nhập thứ %03d của bạn.", username, loginCount);
    }

    public static void main(String[] args) {
        String msg = buildWelcomeMessage("hoang_nam", 5);
        System.out.println(msg); // Chào mừng hoang_nam! Đây là lần đăng nhập thứ 005 của bạn.
    }
}
```

#### 2. Sử dụng `System.out.printf()`
Dùng khi bạn chỉ muốn in nhanh kết quả định dạng ra console để debug hoặc hiển thị giao diện dòng lệnh:
```java
public class PrintfDemo {
    public static void main(String[] args) {
        double score = 8.75;
        // In trực tiếp ra console, dùng %n để xuống dòng
        System.out.printf("Điểm của bạn là: %.1f%n", score); // Điểm của bạn là: 8.8
    }
}
```

#### 3. Sử dụng `Formatter`
Dùng khi cần ghép nhiều chuỗi định dạng vào một bộ đệm (`StringBuilder`) hoặc ghi trực tiếp vào file mà không muốn sinh ra nhiều đối tượng String trung gian:
```java
import java.util.Formatter;

public class FormatterDemo {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder();
        // Gắn Formatter vào StringBuilder sb
        try (Formatter formatter = new Formatter(sb)) {
            formatter.format("Học phần: %s%n", "Lập trình Java");
            formatter.format("Thời lượng: %d giờ%n", 45);
        } // Tự động đóng formatter và giải phóng tài nguyên
        
        System.out.print(sb.toString());
        // Kết quả in ra:
        // Học phần: Lập trình Java
        // Thời lượng: 45 giờ
    }
}
```

#### 4. Sử dụng `String.formatted()` (Java 15+)
Giúp chuỗi định dạng trông tự nhiên hơn, đặc biệt khi làm việc với Text Blocks (Multiline Strings):
```java
public class FormattedMethodDemo {
    public static void main(String[] args) {
        String name = "Mai";
        int age = 20;

        // Gọi trực tiếp .formatted() trên String pattern
        String info = "Tên: %s, Tuổi: %d".formatted(name, age);
        System.out.println(info); // Tên: Mai, Tuổi: 20

        // Kết hợp cực tốt với Text Blocks từ Java 15
        String jsonTemplate = """
            {
                "name": "%s",
                "age": %d
            }
            """.formatted(name, age);
        System.out.println(jsonTemplate);
    }
}
```

---

## 5. Các lưu ý quan trọng (Best Practices & Common Gotchas)

> [!warning] Lỗi thường gặp và Quy tắc hiệu năng
> - **Lỗi khác biệt kiểu dữ liệu (`IllegalFormatConversionException`):** Java kiểm tra kiểu dữ liệu của tham số truyền vào tại thời điểm chạy. Nếu bạn truyền một String vào specifier `%d` (ví dụ: `String.format("%d", "123")`), JVM sẽ ném ra lỗi `IllegalFormatConversionException`.
> - **Sự khác biệt giữa `%b` với giá trị non-boolean:** Đối với `%b`, bất kỳ giá trị nào **khác `null`** đều được định dạng thành `"true"`, ngay cả khi đó là một chuỗi rỗng `""` hoặc số `0`. Do đó, cần cực kỳ cẩn thận khi sử dụng `%b` cho các kiểu dữ liệu không phải `Boolean`.
> - **Sử dụng `%n` thay cho `\n`:** Luôn luôn sử dụng `%n` trong các chuỗi định dạng thay vì `\n`. `%n` đại diện cho ký tự xuống dòng chuẩn của hệ điều hành hiện tại (Windows là `\r\n`, Linux/macOS là `\n`), đảm bảo chuỗi hiển thị chính xác trên mọi môi trường.
> - **Vấn đề Locale với số thực:** Khi định dạng số thực (`%f`) hoặc phân tách hàng nghìn (`%,d`), ký tự hiển thị (dấu chấm hoặc dấu phẩy) phụ thuộc vào **Locale** mặc định của JVM. Nếu muốn kết quả nhất quán trên mọi máy tính, hãy truyền `Locale.US` vào hàm format: `String.format(Locale.US, "%.2f", 3.14)`.
> - **Tránh định dạng trong vòng lặp hiệu năng cao:** Các phương thức như `String.format()` hay `printf()` bên dưới đều phải biên dịch chuỗi format pattern. Nếu sử dụng liên tục trong vòng lặp lớn, hãy cân nhắc sử dụng `StringBuilder` thông thường hoặc dùng một đối tượng `Formatter` duy nhất tái sử dụng để tăng hiệu suất.

### Coding Convention Do / Don't

```java
// ✅ Nên làm (Do)
// Sử dụng %n để xuống dòng tương thích đa nền tảng và dùng đúng kiểu dữ liệu
System.out.printf("Tên: %s%nTuổi: %d%n", "Hoàng", 25);
```

```java
// ❌ Không nên làm (Don't)
// Sử dụng \n có thể gây lỗi hiển thị trên một số hệ điều hành và truyền sai kiểu dữ liệu gây crash ở runtime
System.out.printf("Tên: %s\nTuổi: %d\n", "Hoàng", "25"); // Gây lỗi IllegalFormatConversionException
```
