# Java Variables and Data Types

> [!abstract] Định nghĩa
> **Biến (Variable)** là một vùng nhớ được định danh dùng để lưu trữ dữ liệu tạm thời trong quá trình thực thi chương trình.
> **Kiểu dữ liệu (Data Type)** phân loại dữ liệu lưu trữ, chỉ định lượng bộ nhớ cấp phát và tập hợp các phép toán hợp lệ trên biến đó.

---

## 1. Phân loại biến theo Phạm vi (Scopes)

| Loại biến | Vị trí khai báo | Phạm vi hoạt động | Lưu trữ tại bộ nhớ | Giá trị mặc định |
| --- | --- | --- | --- | --- |
| **Local Variable** | Trong phương thức, constructor hoặc block lệnh. | Chỉ bên trong cặp ngoặc `{}` khai báo biến. | **Stack Memory** | Không có (Bắt buộc khởi tạo trước khi dùng). |
| **Instance Variable** | Trong class, bên ngoài các phương thức. | Trong toàn bộ đối tượng (Object instance). | **Heap Memory** | Có (Số = `0`, Boolean = `false`, Object = `null`). |
| **Static Variable** | Trong class kèm theo từ khóa `static`. | Trong toàn bộ lớp, các đối tượng dùng chung một vùng nhớ. | **Method Area** | Có giá trị mặc định giống Instance Variable. |
| **Parameter** | Trong danh sách tham số phương thức. | Chỉ sử dụng được trong phương thức nhận tham số. | **Stack Memory** | Không có (Nhận giá trị khi phương thức được gọi). |

---

## 2. Các kiểu dữ liệu nguyên thủy (Primitive Types)

| Kiểu dữ liệu | Số bit | Phạm vi giá trị | Mục đích phổ biến |
| --- | --- | --- | --- |
| `byte` | 8 | -128 → 127 | Tiết kiệm bộ nhớ (mảng dữ liệu thô). |
| `short` | 16 | -32,768 → 32,767 | Dùng trong lập trình nhúng, hệ thống nhỏ. |
| `int` | 32 | -2³¹ → 2³¹-1 | Kiểu số nguyên mặc định được dùng nhiều nhất. |
| `long` | 64 | -2⁶³ → 2⁶³-1 | Số nguyên lớn (ID database, timestamp). **Cần hậu tố L**. |
| `float` | 32 | ±1.4E-45 → ±3.4E38 | Số thực độ chính xác đơn. **Cần hậu tố f**. |
| `double` | 64 | ±4.9E-324 → ±1.8E308 | Số thực mặc định độ chính xác kép. |
| `char` | 16 | 0 → 65,535 (Ký tự Unicode) | Lưu trữ một ký tự đơn (nháy đơn `'A'`). |
| `boolean` | Phụ thuộc JVM | `true` hoặc `false` | Điều kiện rẽ nhánh. |

---

## 3. Wrapper Classes

Wrapper Classes cho phép sử dụng kiểu nguyên thủy dưới dạng các đối tượng.

### Bảng tham chiếu các phương thức Wrapper Classes phổ biến

| Class | Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- | --- |
| **Integer / Double / Long** | `parseInt(String s)` / `parseDouble` / `parseLong` | Phân tích cú pháp chuỗi thành số nguyên thủy. | Đổi String → Số | Ném `NumberFormatException` nếu chuỗi lỗi |
| **Integer / Double / Long** | `valueOf(String s)` / `valueOf(primitive)` | Trả về đối tượng Wrapper tương ứng. | Tạo đối tượng Wrapper | Có cơ chế Cache cho giá trị nhỏ (-128 đến 127) |
| **Integer / Double / Long** | `intValue()` / `doubleValue()` / `longValue()` | Chuyển Wrapper object thành kiểu nguyên thủy. | Unboxing thủ công | Thường được tự động thực hiện bởi JVM |
| **Integer / Double / Long** | `compareTo(T another)` | So sánh giá trị của hai Wrapper object. | So sánh lớn/nhỏ | Trả về `< 0` nếu nhỏ hơn, `0` nếu bằng, `> 0` nếu lớn hơn |
| **Integer / Double / Long** | `MAX_VALUE` / `MIN_VALUE` | Hằng số giá trị lớn nhất và nhỏ nhất của kiểu đó. | Kiểm tra giới hạn | Static final constants |
| **Character** | `isDigit(char ch)` | Kiểm tra xem ký tự có phải là chữ số hay không. | Kiểm tra ký tự | Trả về `boolean` |
| **Character** | `isLetter(char ch)` | Kiểm tra xem ký tự có phải là chữ cái hay không. | Kiểm tra ký tự | Trả về `boolean` |
| **Character** | `isWhitespace(char ch)` | Kiểm tra ký tự có phải khoảng trắng (space/tab). | Kiểm tra ký tự | Trả về `boolean` |
| **Character** | `toUpperCase(char ch)` / `toLowerCase` | Chuyển đổi hoa/thường cho ký tự. | Biến đổi | Trả về `char` |
| **Boolean** | `parseBoolean(String s)` | Phân tích cú pháp chuỗi thành boolean nguyên thủy. | Đổi String → Boolean | Trả về `true` nếu chuỗi là `"true"` (không phân biệt hoa thường), ngược lại là `false` |

---

## 4. Ví dụ / Example

```java
public class WrapperExample {
    public static void main(String[] args) {
        // 1. Phân tích chuỗi (String -> Primitive)
        int age = Integer.parseInt("20");
        double price = Double.parseDouble("19.99");

        // 2. valueOf và So sánh compareTo
        Integer score1 = Integer.valueOf(95);
        Integer score2 = Integer.valueOf("80");
        int compResult = score1.compareTo(score2); // > 0 vì 95 > 80

        // 3. Giới hạn MAX/MIN
        int maxInt = Integer.MAX_VALUE; // 2147483647

        // 4. Character Helpers
        boolean isDigit = Character.isDigit('5'); // true
        boolean isLetter = Character.isLetter('@'); // false
        char upper = Character.toUpperCase('a'); // 'A'

        // 5. Boolean Parser
        boolean isTrue = Boolean.parseBoolean("TrUe"); // true
    }
}
```

---

## 5. Phân biệt bộ nhớ Stack và Heap

| Đặc tính | Bộ nhớ Stack | Bộ nhớ Heap |
| --- | --- | --- |
| **Dữ liệu lưu trữ** | Local variables, parameters, lệnh gọi hàm. | Tất cả Objects (bao gồm Instance variables). |
| **Cơ chế hoạt động** | LIFO (Last In First Out), tự giải phóng vùng nhớ khi kết thúc method. | Quản lý tự động bởi Garbage Collector (Bộ dọn rác) khi đối tượng không còn tham chiếu nào trỏ tới. |
| **Tốc độ truy cập** | Cực kỳ nhanh. | Chậm hơn do cần giải quyết địa chỉ tham chiếu. |
| **Dung lượng** | Giới hạn nhỏ (Dễ gặp lỗi `StackOverflowError` khi đệ quy vô hạn). | Rất lớn (Dễ gặp lỗi `OutOfMemoryError` khi tạo quá nhiều object không thu hồi). |

---

## Lưu ý quan trọng

> [!warning]
> - Tránh việc so sánh hai đối tượng Wrapper bằng toán tử `==`. Luôn sử dụng hàm `equals()` để so sánh giá trị bên trong của chúng.
> ```java
> // ❌ Không nên làm (Don't)
> Integer a = 200;
> Integer b = 200;
> System.out.println(a == b); // Trả về false! (Do so sánh hai địa chỉ vùng nhớ khác nhau).
> 
> // ✅ Nên làm (Do)
> System.out.println(a.equals(b)); // Trả về true!
> ```
