# Java Iterator and ListIterator

> [!abstract] Định nghĩa
> **`Iterator`** là một interface cung cấp các phương thức để duyệt qua bất kỳ cấu trúc dữ liệu `Collection` nào theo một chiều từ đầu đến cuối.
> **`ListIterator`** là một interface con của `Iterator`, chỉ dành riêng cho cấu trúc kiểu `List`, cho phép duyệt danh sách theo hai chiều (tiến và lùi) và thay đổi phần tử khi duyệt.

---

## Bảng tham chiếu các phương thức cốt lõi

### 1. Iterator Methods
| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `hasNext()` | Kiểm tra tiếp theo | Trả về `true` nếu vẫn còn phần tử tiếp theo. | Vòng lặp duyệt | Tránh lỗi `NoSuchElementException` |
| `next()` | Lấy phần tử kế | Trả về phần tử tiếp theo trong lượt duyệt và chuyển con trỏ đi tới. | Duyệt phần tử | Ném lỗi nếu hết phần tử |
| `remove()` | Xóa phần tử | Loại bỏ phần tử cuối cùng được trả về bởi `next()`. | Xóa an toàn | Tránh lỗi `ConcurrentModificationException` |

### 2. ListIterator Methods (Bổ sung cho List)
- `hasPrevious()` / `previous()`: Kiểm tra và lấy phần tử trước đó (duyệt ngược).
- `set(E e)`: Thay thế phần tử cuối cùng trả về bởi `next()` hoặc `previous()` bằng `e`.
- `add(E e)`: Chèn phần tử `e` vào ngay trước vị trí con trỏ hiện tại.

---

## Ví dụ / Example

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class IteratorExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>(List.of("A", "B", "C"));

        // ✅ Nên làm (Do): Sử dụng Iterator để xóa phần tử khi đang duyệt danh sách.
        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) {
            String value = iterator.next();
            if (value.equals("B")) {
                iterator.remove(); // Xóa an toàn
            }
        }

        // ❌ Không nên làm (Don't): Xóa phần tử trực tiếp từ list bằng list.remove() trong vòng lặp for-each.
        // for (String s : list) {
        //     if (s.equals("A")) list.remove(s); // Ném lỗi ConcurrentModificationException!
        // }
    }
}
```

---

## Lưu ý

> [!warning]
> - Nếu bạn thay đổi cấu trúc của Collection (thêm, xóa phần tử trực tiếp qua collection) trong khi đang duyệt bằng `Iterator`, chương trình sẽ lập tức ném lỗi **`ConcurrentModificationException`** (cơ chế fail-fast). Do đó, bắt buộc phải sử dụng phương thức `remove()` của chính đối tượng `Iterator`.
