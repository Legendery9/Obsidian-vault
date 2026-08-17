# Java Set Interface

> [!abstract] Định nghĩa
> `Set` là một interface con của `Collection`, đại diện cho một tập hợp các phần tử **không trùng lặp (no duplicate elements)**. Set không duy trì chỉ số index của phần tử, do đó bạn không thể truy cập ngẫu nhiên qua chỉ số như List.

---

## Bảng tham chiếu các phương thức cốt lõi

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `add(E e)` | Thêm phần tử | Thêm phần tử `e` vào tập hợp nếu chưa tồn tại. | Thêm dữ liệu | Trả về `false` nếu phần tử đã có |
| `remove(Object o)` | Xóa phần tử | Loại bỏ phần tử `o` khỏi tập hợp. | Xóa dữ liệu | Dựa trên `equals()` để xác định |
| `contains(Object o)` | Kiểm tra tồn tại | Kiểm tra xem `o` có nằm trong tập hợp hay không. | Tìm kiếm | Rất nhanh ở các class triển khai cụ thể |
| `size()` | Lấy kích thước | Trả về số lượng phần tử hiện tại. | Kiểm tra | Trả về kiểu `int` |
| `isEmpty()` | Kiểm tra rỗng | Trả về `true` nếu tập hợp trống. | Kiểm tra | Thường dùng để validation |
| `clear()` | Xóa toàn bộ | Loại bỏ tất cả phần tử khỏi tập hợp. | Dọn dẹp | Làm sạch tập hợp |

---

## Ví dụ / Example

```java
import java.util.HashSet;
import java.util.Set;

public class SetExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Sử dụng Set để lọc trùng lặp dữ liệu tự động
        Set<String> set = new HashSet<>();

        // 1. add(E e)
        boolean isAdded1 = set.add("Apple"); // true
        boolean isAdded2 = set.add("Apple"); // false (Bị bỏ qua do trùng lặp)
        set.add("Banana");

        // 2. contains(Object o)
        boolean hasApple = set.contains("Apple"); // true

        // 3. remove(Object o)
        set.remove("Banana"); // Tập hợp chỉ còn ["Apple"]

        // 4. size()
        int size = set.size(); // 1
    }
}
```

---

## Lưu ý

> [!warning]
> - `Set` không hỗ trợ phương thức `get(int index)`. Để duyệt qua các phần tử của Set, bắt buộc phải sử dụng **vòng lặp `for-each`** hoặc dùng **`Iterator`**.
> - Tính trùng lặp được xác định bằng phương thức `equals()` và `hashCode()` của đối tượng phần tử.
