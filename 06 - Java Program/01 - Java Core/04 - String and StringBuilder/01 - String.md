# Java String

> [!abstract] Định nghĩa
> **String** là một lớp đặc biệt trong Java đại diện cho chuỗi ký tự bất biến (immutable). Mọi sự thay đổi trên chuỗi String thực tế đều tạo ra một đối tượng hoàn toàn mới trên bộ nhớ Heap (xem giải pháp thay thế hiệu quả tại [[02 - StringBuilder]]).

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

## 2. Bảng tra cứu các phương thức String thông dụng

| Phương thức | Kiểu trả về | Tác dụng |
| --- | --- | --- |
| `length()` | `int` | Trả về độ dài chuỗi ký tự. |
| `charAt(int index)` | `char` | Lấy ký tự tại vị trí index chỉ định (bắt đầu từ `0`). |
| `contains(CharSequence s)` | `boolean` | Kiểm tra chuỗi con có tồn tại hay không. |
| `equals(Object anObject)` | `boolean` | So sánh nội dung hai chuỗi (nhạy cảm hoa/thường). |
| `equalsIgnoreCase(String s)` | `boolean` | So sánh nội dung bỏ qua chữ hoa thường. |
| `substring(int beginIndex, int endIndex)` | `String` | Trích xuất chuỗi con (không lấy phần tử tại `endIndex`). |
| `trim()` | `String` | Loại bỏ khoảng trắng ở hai đầu chuỗi. |
| `split(String regex)` | `String[]` | Phân tách chuỗi thành mảng dựa theo biểu thức chính quy. |
| `matches(String regex)` | `boolean` | So khớp toàn bộ chuỗi với mẫu regex. |
| `intern()` | `String` | Đưa chuỗi vào String Pool và trả về tham chiếu từ Pool. |

---

## 3. Phương thức String mới từ Java 11+

| Phương thức | Tác dụng |
| --- | --- |
| `isBlank()` | Trả về `true` nếu chuỗi rỗng hoặc chỉ chứa toàn khoảng trắng (khác với `isEmpty()`). |
| `strip()` | Loại bỏ khoảng trắng Unicode ở đầu và cuối chuỗi (chuẩn hơn `trim()`). |
| `repeat(int count)` | Lặp lại chuỗi `count` lần. |
| `lines()` | Trả về một `Stream<String>` phân tách chuỗi theo từng dòng. |

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
