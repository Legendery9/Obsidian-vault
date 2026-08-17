# Java String and StringBuilder

> [!abstract] Định nghĩa
> **String** là một lớp đặc biệt đại diện cho chuỗi ký tự bất biến (immutable).
> **StringBuilder** và **StringBuffer** là các lớp đại diện cho chuỗi ký tự động (mutable), cho phép thay đổi nội dung trực tiếp trên đối tượng ban đầu mà không tạo ra đối tượng mới trên Heap.

---

## Tính chất Immutability và String Pool

Khi bạn tạo một String literal, Java sẽ lưu trữ nó trong một vùng nhớ đặc biệt trên Heap gọi là **String Pool**:

```java
String s1 = "Hello";
String s2 = "Hello";
String s3 = new String("Hello");

System.out.println(s1 == s2); // true (Cùng trỏ vào 1 đối tượng trong String Pool)
System.out.println(s1 == s3); // false (s3 trỏ vào 1 đối tượng mới tạo trên Heap ngoài Pool)
```

> [!warning] Tính chất bất biến (Immutability)
> Mọi thao tác sửa đổi chuỗi String không thay đổi giá trị của đối tượng hiện tại, mà thực chất tạo ra một đối tượng String hoàn toàn mới trên bộ nhớ.
> ```java
> // ❌ Không nên làm (Don't): Nối chuỗi bằng toán tử + trong vòng lặp lớn, gây tràn bộ nhớ Heap.
> String text = "";
> for (int i = 0; i < 1000; i++) {
>     text += i; // Tạo ra 1000 đối tượng rác trên Heap!
> }
> 
> // ✅ Nên làm (Do): Sử dụng StringBuilder cho các phép toán thay đổi chuỗi liên tục.
> StringBuilder sb = new StringBuilder();
> for (int i = 0; i < 1000; i++) {
>     sb.append(i);
> }
> String text = sb.toString(); // Chỉ tạo duy nhất một đối tượng String kết quả.
> ```

---

## Bảng tra cứu các phương thức String thông dụng

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

## Phương thức String mới từ Java 11+

| Phương thức | Tác dụng |
| --- | --- |
| `isBlank()` | Trả về `true` nếu chuỗi rỗng hoặc chỉ chứa toàn khoảng trắng (khác với `isEmpty()`). |
| `strip()` | Loại bỏ khoảng trắng Unicode ở đầu và cuối chuỗi (chuẩn hơn `trim()`). |
| `repeat(int count)` | Lặp lại chuỗi `count` lần. |
| `lines()` | Trả về một `Stream<String>` phân tách chuỗi theo từng dòng. |

---

## So sánh String vs StringBuilder vs StringBuffer

| Tiêu chí | String | StringBuilder | StringBuffer |
| --- | --- | --- | --- |
| **Tính khả biến** | Bất biến (Immutable) | Khả biến (Mutable) | Khả biến (Mutable) |
| **Đồng bộ hóa (Thread-Safe)** | ✅ (Do bất biến) | ❌ (Không đồng bộ) | ✅ (Synchronized methods) |
| **Hiệu năng (Speed)** | Chậm khi sửa đổi | Cực nhanh | Chậm hơn StringBuilder |
| **Phạm vi khuyên dùng** | Hằng số, chuỗi ít đổi. | Đơn luồng cần xử lý chuỗi nhiều. | Đa luồng cần đồng bộ xử lý chuỗi. |

---

## Phương thức phổ biến của StringBuilder / StringBuffer

Các hàm này thực thi trực tiếp trên đối tượng ban đầu:

- `append(String str)`: Nối thêm chuỗi vào cuối.
- `insert(int offset, String str)`: Chèn chuỗi tại vị trí chỉ định.
- `delete(int start, int end)`: Xóa ký tự từ vị trí `start` đến trước `end`.
- `reverse()`: Đảo ngược thứ tự chuỗi ký tự.

---

## Chuyển đổi dữ liệu

### 1. Số ↔ String
- **Số → String:** `String.valueOf(number)` hoặc `Integer.toString(number)`.
- **String → Số:** `Integer.parseInt(str)` hoặc `Double.parseDouble(str)`.

```java
// ✅ Nên làm (Do): Chuyển đổi an toàn và bắt lỗi NumberFormatException đề phòng chuỗi sai định dạng.
try {
    int value = Integer.parseInt("123a");
} catch (NumberFormatException e) {
    System.out.println("Chuỗi không phải là số hợp lệ!");
}
```
