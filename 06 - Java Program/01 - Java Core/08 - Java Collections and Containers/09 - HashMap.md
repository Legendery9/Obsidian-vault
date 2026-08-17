# Java HashMap

> [!abstract] Định nghĩa
> `HashMap` là lớp triển khai phổ biến nhất của interface `Map`, lưu trữ dữ liệu dưới dạng bảng băm (hash table). Nó cho phép chứa khóa `null` và giá trị `null`, đồng thời không đảm bảo thứ tự của các cặp key-value theo thời gian.

---

## Bảng tham chiếu các phương thức & Khởi tạo

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `new HashMap<>()` | Khởi tạo mặc định | Tạo một `HashMap` trống, dung lượng ban đầu là 16 và hệ số tải (load factor) là 0.75. | Khởi tạo cơ bản | Phổ biến nhất |
| `new HashMap`(int capacity) | Khởi tạo với dung lượng | Tạo một `HashMap` với dung lượng ban đầu được cấu hình trước. | Tối ưu hóa | Giảm số lần re-hash khi map lớn |
| `putIfAbsent(K k, V v)` | Thêm nếu chưa có | Thêm cặp `k-v` vào Map nếu khóa `k` chưa tồn tại hoặc đang nhận giá trị `null`. | Thêm an toàn | Không ghi đè lên value cũ |

---

## Ví dụ / Example

```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Sử dụng HashMap khi cần tra cứu dữ liệu cực nhanh theo Key và không cần thứ tự.
        HashMap<String, Integer> scores = new HashMap<>();

        scores.put("An", 90);
        scores.put("Bình", 85);
        scores.put(null, 100); // Hợp lệ, HashMap cho phép 1 key null.

        // 1. putIfAbsent
        scores.putIfAbsent("An", 95); // Bị bỏ qua vì key "An" đã tồn tại với value 90

        System.out.println(scores.get("An")); // 90
    }
}
```

---

## Lưu ý

> [!warning]
> - **Hiệu năng:** Độ phức tạp thuật toán trung bình của các thao tác `put()`, `get()`, `remove()` là **$O(1)$**.
> - **Giải quyết xung đột băm (Hash Collision):** Từ Java 8+, nếu nhiều key bị trùng chỉ số băm và danh sách liên kết tại bucket đó vượt quá 8 phần tử, cấu trúc danh sách liên kết sẽ tự động chuyển đổi thành **Cây đỏ-đen (Red-Black Tree)** để nâng hiệu suất tra cứu từ $O(n)$ lên $O(\log n)$.
