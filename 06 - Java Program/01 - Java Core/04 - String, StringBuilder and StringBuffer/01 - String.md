# Java String

> [!abstract] Định nghĩa
> **String** là một lớp đặc biệt trong Java đại diện cho chuỗi ký tự bất biến (immutable). Mọi sự thay đổi trên chuỗi String thực tế đều tạo ra một đối tượng hoàn toàn mới trên bộ nhớ Heap (xem giải pháp thay thế hiệu quả tại [[02 - StringBuilder]] và [[03 - StringBuffer]]).

---

## 1. Tính chất Immutability và String Pool

Khi bạn tạo một đối tượng String dạng literal, Java sẽ lưu trữ nó trong một phân vùng bộ nhớ đặc biệt trên Heap gọi là **String Pool** để tiết kiệm tài nguyên:

```java
String s1 = "Hello";
String s2 = "Hello";
String s3 = new String("Hello");

System.out.println(s1 == s2); // true (Cùng trỏ vào 1 đối tượng trong String Pool)
System.out.println(s1 == s3); // false (s3 trỏ vào đối tượng mới tạo ngoài Pool)
```

- **`intern()`**: Phương thức này giúp đẩy một chuỗi tạo bằng `new String()` vào trong String Pool và trả về tham chiếu từ Pool đó.

---

## 2. Bảng tra cứu các phương thức String đầy đủ

| Nhóm chức năng            | Phương thức                                                 | Kiểu trả về      | Tác dụng                                             | Ví dụ                                                        |
| :------------------------ | :---------------------------------------------------------- | :--------------- | :--------------------------------------------------- | :----------------------------------------------------------- |
| **So sánh & Kiểm tra**    | `equals(Object obj)`                                        | `boolean`        | So sánh nội dung 2 chuỗi (nhạy chữ hoa/thường).      | `"abc".equals("ABC")` $\to$ `false`                          |
|                           | `equalsIgnoreCase(String another)`                          | `boolean`        | So sánh nội dung bỏ qua hoa/thường.                  | `"abc".equalsIgnoreCase("ABC")` $\to$ `true`                 |
|                           | `compareTo(String another)`                                 | `int`            | So sánh theo thứ tự từ điển (ASCII).                 | `"apple".compareTo("banana")` $\to$ `< 0`                    |
|                           | `compareToIgnoreCase(String another)`                       | `int`            | So sánh từ điển bỏ qua hoa/thường.                   | `"Apple".compareToIgnoreCase("banana")` $\to$ `< 0`          |
|                           | `contentEquals(CharSequence cs)`                            | `boolean`        | So sánh nội dung với `StringBuffer`/`StringBuilder`. | `"abc".contentEquals(new StringBuilder("abc"))` $\to$ `true` |
|                           | `isEmpty()`                                                 | `boolean`        | Kiểm tra chuỗi có độ dài bằng 0 hay không.           | `"".isEmpty()` $\to$ `true`                                  |
|                           | `isBlank()`                                                 | `boolean`        | Kiểm tra chuỗi rỗng hoặc chỉ chứa toàn khoảng trắng. | `"   ".isBlank()` $\to$ `true`                               |
|                           | `startsWith(String prefix)`                                 | `boolean`        | Kiểm tra chuỗi có bắt đầu bằng `prefix` không.       | `"Java".startsWith("Ja")` $\to$ `true`                       |
|                           | `endsWith(String suffix)`                                   | `boolean`        | Kiểm tra chuỗi có kết thúc bằng `suffix` không.      | `"Java".endsWith("va")` $\to$ `true`                         |
|                           | `matches(String regex)`                                     | `boolean`        | So khớp chuỗi với biểu thức chính quy (regex).       | `"123".matches("\\d+")` $\to$ `true`                         |
| **Tìm kiếm & Trích xuất** | `length()`                                                  | `int`            | Trả về số ký tự trong chuỗi.                         | `"Java".length()` $\to$ `4`                                  |
|                           | `charAt(int index)`                                         | `char`           | Lấy ký tự tại vị trí index (0-indexed).              | `"Java".charAt(2)` $\to$ `'v'`                               |
|                           | `indexOf(String str)`                                       | `int`            | Tìm vị trí xuất hiện đầu tiên của `str`.             | `"Java".indexOf("a")` $\to$ `1`                              |
|                           | `lastIndexOf(String str)`                                   | `int`            | Tìm vị trí xuất hiện cuối cùng của `str`.            | `"Java".lastIndexOf("a")` $\to$ `3`                          |
|                           | `contains(CharSequence s)`                                  | `boolean`        | Kiểm tra chuỗi có chứa `s` không.                    | `"Java".contains("av")` $\to$ `true`                         |
|                           | `substring(int begin)`                                      | `String`         | Trích xuất chuỗi con từ `begin` đến hết.             | `"Hello".substring(2)` $\to$ `"llo"`                         |
|                           | `substring(int begin, int end)`                             | `String`         | Trích xuất chuỗi con từ `begin` đến trước `end`.     | `"Hello".substring(1, 4)` $\to$ `"ell"`                      |
| **Biến đổi & Định dạng**  | `replace(char old, char new)`                               | `String`         | Thay thế tất cả ký tự `old` bằng `new`.              | `"Java".replace('a', 'o')` $\to$ `"Jovo"`                    |
|                           | `replace(CharSequence target, CharSequence replacement)`    | `String`         | Thay thế chuỗi con khớp chính xác.                   | `"Hello".replace("ll", "y")` $\to$ `"Heyo"`                  |
|                           | `replaceAll(String regex, String repl)`                     | `String`         | Thay thế tất cả chuỗi khớp regex.                    | `"a1b2".replaceAll("\\d", "*")` $\to$ `"a*b*"`               |
|                           | `replaceFirst(String regex, String repl)`                   | `String`         | Thay thế chuỗi đầu tiên khớp regex.                  | `"a1b2".replaceFirst("\\d", "*")` $\to$ `"a*b2"`             |
|                           | `toUpperCase()`                                             | `String`         | Chuyển toàn bộ chuỗi thành chữ hoa.                  | `"Java".toUpperCase()` $\to$ `"JAVA"`                        |
|                           | `toLowerCase()`                                             | `String`         | Chuyển toàn bộ chuỗi thành chữ thường.               | `"Java".toLowerCase()` $\to$ `"java"`                        |
|                           | `trim()`                                                    | `String`         | Loại bỏ khoảng trắng ở hai đầu chuỗi.                | `" a ".trim()` $\to$ `"a"`                                   |
|                           | `strip()`                                                   | `String`         | Loại bỏ khoảng trắng Unicode ở hai đầu.              | `"\u2000a\u2000".strip()` $\to$ `"a"`                        |
|                           | `stripLeading()`                                            | `String`         | Loại bỏ khoảng trắng ở đầu chuỗi.                    | `" a".stripLeading()` $\to$ `"a"`                            |
|                           | `stripTrailing()`                                           | `String`         | Loại bỏ khoảng trắng ở cuối chuỗi.                   | `"a ".stripTrailing()` $\to$ `"a"`                           |
|                           | `concat(String str)`                                        | `String`         | Nối chuỗi `str` vào cuối chuỗi hiện tại.             | `"a".concat("b")` $\to$ `"ab"`                               |
|                           | `repeat(int count)`                                         | `String`         | Lặp lại chuỗi `count` lần.                           | `"a".repeat(3)` $\to$ `"aaa"`                                |
|                           | `String.format(String fmt, Object... args)`                 | `String`         | Định dạng chuỗi tĩnh theo chuẩn C-style (Xem chi tiết [[03 - Format Specifiers\|Format Specifiers]]).             | `String.format("%s: %d", "A", 1)` $\to$ `"A: 1"`             |
|                           | `formatted(Object... args)`                                 | `String`         | Định dạng chuỗi không tĩnh (Java 15+) (Xem chi tiết [[03 - Format Specifiers\|Format Specifiers]]).               | `"%s: %d".formatted("A", 1)` $\to$ `"A: 1"`                  |
| **Chuyển đổi & Khác**     | `split(String regex)`                                       | `String[]`       | Phân tách chuỗi thành mảng theo regex.               | `"a-b".split("-")` $\to$ `["a", "b"]`                        |
|                           | `split(String regex, int limit)`                            | `String[]`       | Phân tách chuỗi với giới hạn số phần tử.             | `"a-b-c".split("-", 2)` $\to$ `["a", "b-c"]`                 |
|                           | `String.join(CharSequence delim, CharSequence... elements)` | `String`         | Ghép các phần tử lại với nhau bằng dấu phân tách.    | `String.join("-", "a", "b")` $\to$ `"a-b"`                   |
|                           | `toCharArray()`                                             | `char[]`         | Chuyển chuỗi thành mảng ký tự.                       | `"Hi".toCharArray()` $\to$ `['H', 'i']`                      |
|                           | `valueOf(Object obj)`                                       | `String`         | Chuyển đối tượng/kiểu nguyên thủy sang String.       | `String.valueOf(123)` $\to$ `"123"`                          |
|                           | `chars()`                                                   | `IntStream`      | Trả về stream các mã ASCII/Unicode của ký tự.        | `"A".chars()` $\to$ Stream chứa `65`                         |
|                           | `getBytes()`                                                | `byte[]`         | Mã hóa chuỗi thành mảng byte (default charset).      | `"A".getBytes()` $\to$ `[65]`                                |
|                           | `lines()`                                                   | `Stream<String>` | Tách chuỗi theo các dòng.                            | `"a\nb".lines()` $\to$ Stream `["a", "b"]`                   |
|                           | `intern()`                                                  | `String`         | Đưa chuỗi vào String Pool và trả về tham chiếu.      | `s.intern()` $\to$ Tham chiếu trong pool                     |

---

## 3. Ví dụ minh họa chi tiết theo nhóm

### 3.1. So sánh & Kiểm tra
```java
public class StringCompareExample {
    public static void main(String[] args) {
        String s1 = "Java Programming";
        
        // 1. So sánh nội dung bằng equals / equalsIgnoreCase
        boolean isEqual = s1.equals("java programming"); // false
        boolean isEqualIgnore = s1.equalsIgnoreCase("java programming"); // true

        // 2. So sánh thứ tự từ điển bằng compareTo
        int diff = "Apple".compareTo("Banana"); // Trả về số âm vì 'A' đứng trước 'B'

        // 3. So sánh với StringBuilder bằng contentEquals
        StringBuilder sb = new StringBuilder("Java Programming");
        boolean isContentEqual = s1.contentEquals(sb); // true

        // 4. Kiểm tra rỗng (isEmpty) và trống (isBlank)
        String spaces = "   ";
        System.out.println(spaces.isEmpty()); // false (độ dài > 0)
        System.out.println(spaces.isBlank()); // true (chỉ chứa khoảng trắng)

        // 5. Kiểm tra bắt đầu/kết thúc
        boolean start = s1.startsWith("Java"); // true
        boolean end = s1.endsWith("ing"); // true
    }
}
```

### 3.2. Tìm kiếm & Trích xuất
```java
public class StringSearchExample {
    public static void main(String[] args) {
        String filepath = "project/src/main/App.java";

        // 1. Tìm vị trí của ký tự/chuỗi con
        int firstSlash = filepath.indexOf("/"); // 7
        int lastSlash = filepath.lastIndexOf("/"); // 16
        int notFound = filepath.indexOf("test"); // -1

        // 2. Kiểm tra chứa chuỗi con
        boolean containsApp = filepath.contains("App"); // true

        // 3. Trích xuất substring
        String folder = filepath.substring(0, firstSlash); // "project"
        String filename = filepath.substring(lastSlash + 1); // "App.java"
    }
}
```

### 3.3. Biến đổi & Định dạng
```java
public class StringTransformExample {
    public static void main(String[] args) {
        String raw = "  Hello 123 World!  ";

        // 1. Thay thế replace / replaceAll
        String replaced = raw.replace("123", "Java"); // "  Hello Java World!  "
        String noDigits = raw.replaceAll("\\d", ""); // "  Hello  World!  "

        // 2. Cắt khoảng trắng trim / strip
        String trimmed = raw.trim(); // "Hello 123 World!"
        
        // 3. Định dạng String.format và formatted (Java 15+)
        String formatted1 = String.format("Học %s trong %d ngày", "Java", 30);
        String formatted2 = "Học %s trong %d ngày".formatted("Java", 30);
        
        // 4. Lặp lại chuỗi
        String repeated = "A".repeat(3); // "AAA"
    }
}
```

### 3.4. Chuyển đổi & Phân tách
```java
import java.util.Arrays;

public class StringConvertExample {
    public static void main(String[] args) {
        String csv = "apple,banana,orange";

        // 1. Phân tách split
        String[] fruits = csv.split(","); // ["apple", "banana", "orange"]
        String[] limited = csv.split(",", 2); // ["apple", "banana,orange"]

        // 2. Ghép chuỗi String.join
        String joined = String.join(" | ", fruits); // "apple | banana | orange"

        // 3. Chuỗi sang mảng ký tự toCharArray
        char[] chars = "Hi".toCharArray(); // ['H', 'i']

        // 4. Giá trị sang String valueOf
        String score = String.valueOf(9.5); // "9.5"
    }
}
```

---

## 4. Chuyển đổi dữ liệu Số ↔ String

- **Số $\rightarrow$ String:** Sử dụng `String.valueOf(number)` hoặc `Integer.toString(number)`.
- **String $\rightarrow$ Số:** Sử dụng `Integer.parseInt(str)` hoặc `Double.parseDouble(str)`.

```java
// ✅ Nên làm (Do): Chuyển đổi an toàn và bắt lỗi NumberFormatException đề phòng chuỗi sai định dạng.
try {
    int value = Integer.parseInt("123a");
} catch (NumberFormatException e) {
    System.out.println("Chuỗi không phải là số hợp lệ!");
}
```
