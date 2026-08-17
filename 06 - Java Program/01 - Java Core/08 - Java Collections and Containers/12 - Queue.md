# Java Queue Interface

> [!abstract] Định nghĩa
> `Queue` là một interface con của `Collection`, đại diện cho cấu trúc dữ liệu hàng đợi hoạt động theo nguyên tắc **FIFO (First In, First Out - Vào trước, Ra trước)**. Phần tử được thêm vào cuối hàng đợi và được lấy ra từ đầu hàng đợi.

---

## Bảng tham chiếu các phương thức cốt lõi

Java cung cấp hai bộ phương thức để thao tác với Queue, một bộ sẽ ném ngoại lệ (Exception) khi thất bại, bộ còn lại trả về giá trị đặc biệt (`null` hoặc `false`):

| Thao tác | Ném Exception khi lỗi | Trả về giá trị đặc biệt (Khuyên dùng) | Tác dụng |
| --- | --- | --- | --- |
| **Thêm vào (Enqueue)** | `add(e)` (Ném lỗi nếu đầy) | `offer(e)` (Trả về `false` nếu đầy) | Thêm phần tử `e` vào cuối hàng đợi. |
| **Lấy ra & Xóa (Dequeue)** | `remove()` (Ném lỗi nếu rỗng) | `poll()` (Trả về `null` nếu rỗng) | Lấy ra và xóa phần tử đầu hàng đợi. |
| **Xem trước (Peek)** | `element()` (Ném lỗi nếu rỗng) | `peek()` (Trả về `null` nếu rỗng) | Xem phần tử đầu hàng đợi nhưng không xóa. |

---

## Ví dụ / Example

```java
import java.util.LinkedList;
import java.util.Queue;

public class QueueExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Sử dụng LinkedList làm hàng đợi thông thường
        Queue<String> queue = new LinkedList<>();

        // 1. offer(E e)
        queue.offer("A");
        queue.offer("B"); // ["A", "B"]

        // 2. peek()
        String first = queue.peek(); // "A" (Vẫn nằm trong hàng đợi)

        // 3. poll()
        String removed = queue.poll(); // "A" (Bị loại bỏ khỏi hàng đợi)
        
        System.out.println(queue); // ["B"]
    }
}
```

---

## Lưu ý

> [!warning]
> - Tránh chèn giá trị `null` vào hàng đợi `Queue` vì phương thức `poll()` và `peek()` trả về `null` để báo hiệu hàng đợi trống. Nếu chứa phần tử `null`, bạn sẽ không thể phân biệt giữa hàng đợi trống và hàng đợi chứa giá trị `null`.
