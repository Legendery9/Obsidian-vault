# Java Deque Interface

> [!abstract] Định nghĩa
> `Deque` (Double Ended Queue - phát âm là "deck") là interface con của `Queue`, đại diện cho **hàng đợi hai đầu**. Nó cho phép chèn và xóa các phần tử ở cả đầu (head) và cuối (tail) danh sách. Do đó, Deque có thể đóng vai trò vừa là **FIFO Queue** vừa là **LIFO Stack**.

---

## Bảng tham chiếu các phương thức đầu cuối

| Thao tác | Đầu (First / Head) | Cuối (Last / Tail) | Tác dụng |
| --- | --- | --- | --- |
| **Thêm vào** | `addFirst(e)` / `offerFirst(e)` | `addLast(e)` / `offerLast(e)` | Thêm phần tử vào đầu hoặc cuối Deque. |
| **Lấy ra & Xóa** | `removeFirst()` / `pollFirst()` | `removeLast()` / `pollLast()` | Lấy ra và loại bỏ phần tử ở hai đầu. |
| **Xem trước** | `getFirst()` / `peekFirst()` | `getLast()` / `peekLast()` | Xem phần tử ở hai đầu mà không xóa. |

### Các phương thức ngăn xếp LIFO (Stack) tương ứng:
- `push(e)`: Tương đương `addFirst(e)`.
- `pop()`: Tương đương `removeFirst()`.
- `peek()`: Tương đương `peekFirst()`.

---

## Ví dụ / Example

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class DequeExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Sử dụng ArrayDeque làm Stack thay thế cho lớp cổ điển Stack
        Deque<String> stack = new ArrayDeque<>();

        // 1. push(E e) - Đẩy phần tử vào đỉnh ngăn xếp
        stack.push("First");
        stack.push("Second"); // ["Second", "First"]

        // 2. peek() - Xem phần tử đỉnh
        String top = stack.peek(); // "Second"

        // 3. pop() - Lấy và xóa phần tử đỉnh
        String popped = stack.pop(); // "Second"
    }
}
```

---

## Lưu ý

> [!warning]
> - Tránh sử dụng class cổ điển `java.util.Stack` vì nó sử dụng cơ chế đồng bộ hóa luồng (synchronized) không cần thiết, làm giảm hiệu năng. Hãy sử dụng **`ArrayDeque`** như một Stack chuyên dụng.
