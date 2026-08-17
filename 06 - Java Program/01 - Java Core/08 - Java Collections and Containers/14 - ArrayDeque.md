# Java ArrayDeque

> [!abstract] Định nghĩa
> `ArrayDeque` là một lớp triển khai trực tiếp của interface `Deque` sử dụng một **mảng động vòng (circular array)**. Nó không có giới hạn dung lượng và là cấu trúc dữ liệu tối ưu nhất của Java để thay thế cho cả `Stack` và `Queue`.

---

## Bảng tham chiếu các phương thức & Khởi tạo

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `new ArrayDeque<>()` | Khởi tạo mặc định | Tạo một `ArrayDeque` rỗng có dung lượng ban đầu là 16. | Khởi tạo cơ bản | Khuyên dùng |
| `new ArrayDeque`(int numElements) | Khởi tạo với dung lượng | Tạo một `ArrayDeque` đủ lớn để chứa số phần tử chỉ định không bị resize. | Tối ưu hóa | Tránh cấp phát bộ nhớ lại |

---

## Ví dụ / Example

```java
import java.util.ArrayDeque;

public class ArrayDequeExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Sử dụng ArrayDeque để triển khai hàng đợi hai đầu có hiệu năng cực cao.
        ArrayDeque<Integer> queue = new ArrayDeque<>();

        // Thao tác Queue FIFO
        queue.offer(1);
        queue.offer(2);
        
        System.out.println(queue.poll()); // 1

        // Thao tác Stack LIFO
        queue.push(3);
        queue.push(4);

        System.out.println(queue.pop()); // 4
    }
}
```

---

## Lưu ý

> [!warning]
> - **Hiệu năng:** `ArrayDeque` nhanh hơn `Stack` khi sử dụng làm ngăn xếp và nhanh hơn `LinkedList` khi sử dụng làm hàng đợi do không tốn chi phí quản lý các con trỏ Node trên Heap. Hầu hết các thao tác đều là **$O(1)$** khấu hao.
> - **Hạn chế:** `ArrayDeque` không cho phép chứa giá trị `null` và không hỗ trợ truy cập ngẫu nhiên qua chỉ số index (không có `get(index)`).
