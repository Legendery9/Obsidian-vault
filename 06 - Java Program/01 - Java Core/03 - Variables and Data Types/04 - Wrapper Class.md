# Java Wrapper Classes

> [!abstract] Định nghĩa
> **Wrapper Class** là các lớp đối tượng bọc tương ứng cho 8 kiểu dữ liệu nguyên thủy (xem [[03 - Primitive]]), cho phép sử dụng các kiểu nguyên thủy này dưới dạng đối tượng trong các cấu trúc hướng đối tượng (như Collections Framework, Generics).

---

## 1. Khái niệm Autoboxing và Unboxing

JVM hỗ trợ việc chuyển đổi tự động giữa kiểu nguyên thủy và đối tượng Wrapper tương ứng:

- **Autoboxing:** Tự động chuyển đổi từ kiểu dữ liệu nguyên thủy sang đối tượng Wrapper tương ứng.
- **Unboxing:** Tự động chuyển đổi ngược lại từ đối tượng Wrapper sang kiểu dữ liệu nguyên thủy.

```java
// Autoboxing: Primitive -> Wrapper Object
Integer ageObj = 25; // Tương đương: Integer.valueOf(25)

// Unboxing: Wrapper Object -> Primitive
int agePri = ageObj; // Tương đương: ageObj.intValue()
```

---

## 2. Bảng tham chiếu các phương thức Wrapper Classes phổ biến

| Class                       | Method / Statement                                 | Definition                                               | Tác dụng                                | Cách dùng / Phạm vi                                                                     |
| --------------------------- | -------------------------------------------------- | -------------------------------------------------------- | --------------------------------------- | --------------------------------------------------------------------------------------- |
| **Integer / Double / Long** | `parseInt(String s)` / `parseDouble` / `parseLong` | Phân tích cú pháp chuỗi thành số nguyên thủy.            | Đổi String $\rightarrow$ Số nguyên thủy | Ném `NumberFormatException` nếu chuỗi lỗi định dạng.                                    |
| **Integer / Double / Long** | `valueOf(String s)` / `valueOf(primitive)`         | Trả về đối tượng Wrapper tương ứng.                      | Tạo đối tượng Wrapper                   | Có cơ chế Cache cho giá trị nhỏ (-128 đến 127) để tối ưu bộ nhớ.                        |
| **Integer / Double / Long** | `intValue()` / `doubleValue()` / `longValue()`     | Chuyển Wrapper object thành kiểu nguyên thủy.            | Unboxing thủ công                       | Thường được tự động thực hiện bởi JVM.                                                  |
| **Integer / Double / Long** | `compareTo(T another)`                             | So sánh giá trị của hai Wrapper object.                  | So sánh lớn/nhỏ                         | Trả về $< 0$ nếu nhỏ hơn, $0$ nếu bằng, $> 0$ nếu lớn hơn.                              |
| **Integer / Double / Long** | `MAX_VALUE` / `MIN_VALUE`                          | Hằng số giá trị lớn nhất và nhỏ nhất của kiểu đó.        | Kiểm tra giới hạn                       | Static final constants.                                                                 |
| **Character**               | `isDigit(char ch)`                                 | Kiểm tra xem ký tự có phải là chữ số hay không.          | Kiểm tra ký tự                          | Trả về `boolean`.                                                                       |
| **Character**               | `isLetter(char ch)`                                | Kiểm tra xem ký tự có phải là chữ cái hay không.         | Kiểm tra ký tự                          | Trả về `boolean`.                                                                       |
| **Character**               | `isWhitespace(char ch)`                            | Kiểm tra ký tự có phải khoảng trắng (space/tab/newline). | Kiểm tra ký tự                          | Trả về `boolean`.                                                                       |
| **Character**               | `toUpperCase(char ch)` / `toLowerCase`             | Chuyển đổi hoa/thường cho ký tự.                         | Biến đổi                                | Trả về `char`.                                                                          |
| **Boolean**                 | `parseBoolean(String s)`                           | Phân tích cú pháp chuỗi thành boolean nguyên thủy.       | Đổi String $\rightarrow$ Boolean        | Trả về `true` nếu chuỗi là `"true"` (không phân biệt hoa thường), ngược lại là `false`. |

---

## 3. Ví dụ thực tế sử dụng các Wrapper Classes

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

## 4. Lưu ý quan trọng khi so sánh Wrapper Objects

> [!warning] Luôn so sánh giá trị bằng equals() thay vì ==
> Các đối tượng Wrapper là các Object thực sự trên Heap. Sử dụng toán tử `==` sẽ so sánh địa chỉ vùng nhớ chứ không so sánh giá trị thực tế của chúng, dẫn đến kết quả sai lệch (ngoại trừ các số nhỏ từ -128 đến 127 được JVM lưu trong bộ nhớ đệm Cache).
> ```java
> // ❌ Không nên làm (Don't): So sánh hai đối tượng Wrapper bằng ==
> Integer a = 200;
> Integer b = 200;
> System.out.println(a == b); // Trả về false! (Do trỏ tới 2 đối tượng khác nhau trên Heap).
> 
> // ✅ Nên làm (Do): Sử dụng equals() để so sánh giá trị thực tế của đối tượng.
> System.out.println(a.equals(b)); // Trả về true!
> ```
