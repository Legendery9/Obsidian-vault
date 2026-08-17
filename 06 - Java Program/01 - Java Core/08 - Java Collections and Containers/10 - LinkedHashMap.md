# Java LinkedHashMap

> [!abstract] Định nghĩa
> `LinkedHashMap` là lớp con của `HashMap`, duy trì một **danh sách liên kết kép (doubly-linked list)** chạy qua tất cả các Entry của nó. Nhờ đó, nó bảo toàn được **thứ tự chèn (insertion-order)** hoặc **thứ tự truy cập gần nhất (access-order)**.

---

## Bảng tham chiếu các phương thức & Khởi tạo

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `new LinkedHashMap<>()` | Khởi tạo mặc định | Tạo một `LinkedHashMap` rỗng, sắp xếp theo thứ tự chèn. | Khởi tạo cơ bản | Mặc định |
| `new LinkedHashMap`(int cap, float lf, boolean accessOrder) | Khởi tạo nâng cao | Tạo Map. Nếu `accessOrder` là `true`, các phần tử được truy xuất gần nhất sẽ tự động được đẩy về cuối. | Thiết kế bộ nhớ Cache | Thường dùng làm LRU Cache |

---

## Ví dụ / Example

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class LinkedHashMapExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Sử dụng LinkedHashMap khi cần lưu dữ liệu dạng Map và duyệt qua các phần tử đúng theo thứ tự đưa vào.
        Map<String, String> map = new LinkedHashMap<>();
        
        map.put("One", "1");
        map.put("Two", "2");
        map.put("Three", "3");

        // Luôn in ra: Key: One, Key: Two, Key: Three
        for (String key : map.keySet()) {
            System.out.println("Key: " + key);
        }
    }
}
```

---

## Lưu ý

> [!warning]
> - **Hiệu năng:** Tốc độ tương đương `HashMap` với độ phức tạp **$O(1)$**, nhưng tốn thêm một phần nhỏ chi phí để cập nhật các liên kết trỏ của danh sách liên kết khi thực hiện ghi dữ liệu.
> - **Ứng dụng thực tế:** Nhờ tham số `accessOrder`, `LinkedHashMap` là cấu trúc lý tưởng để cài đặt bộ nhớ đệm giải thuật **LRU (Least Recently Used) Cache** bằng cách ghi đè phương thức `removeEldestEntry()`.
