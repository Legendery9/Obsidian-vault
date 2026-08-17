# Java PriorityQueue

> [!abstract] Định nghĩa
> `PriorityQueue` là một lớp triển khai của `Queue`, sử dụng cấu trúc **đống nhị phân (binary heap)**. Thay vì lấy phần tử theo thứ tự FIFO, nó tự động sắp xếp và lấy ra phần tử có **độ ưu tiên cao nhất** trước (mặc định là phần tử nhỏ nhất).

---

## Bảng tham chiếu các phương thức & Khởi tạo

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `new PriorityQueue<>()` | Khởi tạo tự nhiên | Tạo `PriorityQueue` sắp xếp các phần tử theo thứ tự tự nhiên (tăng dần). | Khởi tạo cơ bản | Đối tượng phải triển khai `Comparable` |
| `new PriorityQueue`(int cap, Comparator c) | Khởi tạo với so sánh | Tạo `PriorityQueue` sắp xếp theo bộ so sánh `Comparator` tùy chỉnh. | Định nghĩa độ ưu tiên | Tùy biến linh hoạt |

---

## Ví dụ / Example

```java
import java.util.PriorityQueue;

public class PriorityQueueExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Sử dụng PriorityQueue khi cần xử lý các tác vụ có độ ưu tiên (như lập lịch luồng CPU).
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        pq.offer(30);
        pq.offer(10);
        pq.offer(20);

        // Mặc định phần tử nhỏ nhất có độ ưu tiên cao nhất
        System.out.println(pq.poll()); // 10
        System.out.println(pq.poll()); // 20
        System.out.println(pq.poll()); // 30
    }
}
```

---

## Lưu ý

> [!warning]
> - **Hiệu năng:** Phương thức `offer()` và `poll()` có độ phức tạp là **$O(\log n)$**, trong khi phương thức `peek()` có độ phức tạp là **$O(1)$**.
> - **Hạn chế:** Không cho phép lưu trữ giá trị `null` và không đảm bảo thứ tự duyệt qua bằng vòng lặp `for-each` (chỉ đảm bảo phần tử đầu tiên lấy ra có độ ưu tiên cao nhất).
