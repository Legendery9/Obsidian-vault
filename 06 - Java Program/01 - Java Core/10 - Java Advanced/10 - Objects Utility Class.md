# Java Objects Utility Class

> [!abstract] Định nghĩa
> **`java.util.Objects`** là một lớp tiện ích (`utility class`) bao gồm các phương thức tĩnh (`static`) dùng để thao tác trên các đối tượng. Các phương thức này được thiết kế để chống lại lỗi `NullPointerException` (NPE) và cung cấp các hàm helper ngắn gọn cho việc kiểm tra, so sánh, và tính toán mã băm.
> 
> *Lưu ý: Lớp này khác với khái niệm đối tượng tổng quát được trình bày tại [[02 - Objects]].*

---

## 1. Tác dụng
- **Null-safety:** Thực hiện so sánh hoặc lấy mã băm mà không sợ đối tượng bị null gây crash ứng dụng.
- **Validate tham số:** Kiểm tra tính hợp lệ của tham số đầu vào trong constructor hoặc setter một cách ngắn gọn.
- **Tạo boilerplate code sạch hơn:** Giúp sinh mã tự động cho `equals()` và `hashCode()` hiệu quả.

---

## 2. Bảng tham chiếu các phương thức thông dụng

| Method | Kiểu trả về | Tác dụng | Ví dụ |
| :--- | :--- | :--- | :--- |
| `equals(Object a, Object b)` | `boolean` | So sánh hai đối tượng, an toàn tuyệt đối nếu một hoặc cả hai đối tượng là `null`. | `Objects.equals(x, y)` |
| `deepEquals(Object a, Object b)`| `boolean` | So sánh sâu hai đối tượng (thích hợp cho so sánh mảng hai chiều hoặc lồng nhau). | `Objects.deepEquals(arr1, arr2)` |
| `hashCode(Object o)` | `int` | Trả về mã băm của đối tượng. Trả về $0$ nếu đối tượng là `null`. | `Objects.hashCode(obj)` |
| `hash(Object... values)` | `int` | Tạo mã băm tổng hợp cho một chuỗi các giá trị thuộc tính. | `Objects.hash(id, name, age)` |
| `isNull(Object obj)` | `boolean` | Kiểm tra đối tượng có bằng `null` hay không. | `Objects.isNull(obj)` |
| `nonNull(Object obj)` | `boolean` | Kiểm tra đối tượng có khác `null` hay không. | `Objects.nonNull(obj)` |
| `requireNonNull(T obj)` | `T` | Kiểm tra xem đối tượng có null không. Nếu có, ném ngay `NullPointerException`. | `this.name = Objects.requireNonNull(name);` |
| `requireNonNull(T obj, String msg)`| `T` | Giống như trên nhưng cho phép định nghĩa thông báo lỗi khi ném ngoại lệ. | `Objects.requireNonNull(name, "Name không được null")` |
| `toString(Object o, String def)`| `String` | Chuyển đối tượng sang chuỗi. Trả về `def` nếu đối tượng là `null`. | `Objects.toString(str, "Trống")` |

---

## 3. Ví dụ minh họa

```java
import java.util.Objects;

public class ObjectsUtilityExample {
    private String title;
    private String description;

    public ObjectsUtilityExample(String title, String description) {
        // 1. requireNonNull: Validate tham số đầu vào ngay khi khởi tạo
        this.title = Objects.requireNonNull(title, "Title không được phép để null!");
        
        // 2. toString với giá trị mặc định nếu null
        this.description = Objects.toString(description, "Không có mô tả.");
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        ObjectsUtilityExample other = (ObjectsUtilityExample) o;
        
        // 3. Objects.equals: So sánh an toàn không lo NullPointerException
        return Objects.equals(this.title, other.title) && 
               Objects.equals(this.description, other.description);
    }

    @Override
    public int hashCode() {
        // 4. Objects.hash: Sinh mã băm tổng hợp cực kỳ nhanh và chuẩn xác
        return Objects.hash(title, description);
    }

    public static void main(String[] args) {
        String s1 = null;
        String s2 = "Hello";

        // 5. Kiểm tra nhanh bằng isNull / nonNull
        System.out.println("s1 là null: " + Objects.isNull(s1)); // true
        System.out.println("s2 khác null: " + Objects.nonNull(s2)); // true

        // 6. So sánh null-safe
        System.out.println("s1 equals s2: " + Objects.equals(s1, s2)); // false (không ném Exception)
    }
}
```

---

## 4. Lưu ý

> [!tip]
> - Sử dụng `Objects.requireNonNull()` ở đầu các phương thức công khai hoặc hàm tạo là một phương pháp lập trình phòng vệ tốt (Fail-fast principle), giúp phát hiện lỗi sai dữ liệu sớm nhất có thể trước khi dữ liệu lỗi đó đi sâu vào logic nghiệp vụ của hệ thống.
