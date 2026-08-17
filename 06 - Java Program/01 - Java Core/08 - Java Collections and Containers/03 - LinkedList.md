# Java LinkedList

> [!abstract] Định nghĩa
> `LinkedList` là lớp triển khai của cả hai interface `List` và `Deque`, sử dụng cấu trúc **danh sách liên kết kép (doubly linked list)** để lưu trữ các phần tử. Mỗi phần tử là một Node chứa dữ liệu và liên kết tới Node trước và Node sau nó.

---

## Bảng tham chiếu các phương thức đặc trưng (từ Deque)

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `addFirst(E e)` | Thêm vào đầu | Chèn phần tử `e` vào vị trí đầu tiên của danh sách. | Thao tác đầu cuối | Tốc độ $O(1)$ |
| `addLast(E e)` | Thêm vào cuối | Chèn phần tử `e` vào vị trí cuối cùng của danh sách. | Thao tác đầu cuối | Tốc độ $O(1)$, tương tự `add(e)` |
| `getFirst()` | Lấy phần tử đầu | Lấy phần tử đầu tiên trong danh sách. | Thao tác đầu cuối | Ném `NoSuchElementException` nếu rỗng |
| `getLast()` | Lấy phần tử cuối | Lấy phần tử cuối cùng trong danh sách. | Thao tác đầu cuối | Ném `NoSuchElementException` nếu rỗng |
| `removeFirst()` | Xóa đầu | Xóa và trả về phần tử đầu tiên của danh sách. | Thao tác đầu cuối | Ném `NoSuchElementException` nếu rỗng |
| `removeLast()` | Xóa cuối | Xóa và trả về phần tử cuối cùng của danh sách. | Thao tác đầu cuối | Ném `NoSuchElementException` nếu rỗng |
| `peekFirst()` | Xem đầu | Lấy phần tử đầu nhưng không xóa. | Thao tác an toàn | Trả về `null` nếu danh sách rỗng |
| `peekLast()` | Xem cuối | Lấy phần tử cuối nhưng không xóa. | Thao tác an toàn | Trả về `null` nếu danh sách rỗng |

---

## Ví dụ / Example

```java
import java.util.LinkedList;

public class LinkedListExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Sử dụng LinkedList khi ứng dụng chủ yếu thêm/xóa phần tử ở hai đầu (hàng đợi/ngăn xếp).
        LinkedList<String> list = new LinkedList<>();

        // 1. addFirst / addLast
        list.addLast("Item 2");
        list.addFirst("Item 1"); // ["Item 1", "Item 2"]

        // 2. getFirst / getLast
        String first = list.getFirst(); // "Item 1"

        // 3. removeFirst / removeLast
        list.removeFirst(); // ["Item 2"]
        
        // 4. peekFirst / peekLast
        String peek = list.peekFirst(); // "Item 2"
    }
}
```

---

## Lưu ý

> [!warning]
> - **Hiệu năng:** Việc thêm/xóa ở hai đầu hoặc tại vị trí hiện tại có độ phức tạp là $O(1)$. Tuy nhiên, việc truy xuất ngẫu nhiên `get(index)` mất $O(n)$ vì phải duyệt tuần tự từ đầu hoặc cuối danh sách tới vị trí đó.
> - **Tiêu hao bộ nhớ:** `LinkedList` tốn bộ nhớ hơn `ArrayList` vì mỗi Node phải lưu trữ thêm hai tham chiếu con trỏ trỏ tới Node trước và Node sau.
