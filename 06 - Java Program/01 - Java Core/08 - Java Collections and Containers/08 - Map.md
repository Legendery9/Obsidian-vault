# Java Map Interface

> [!abstract] Định nghĩa
> `Map` là một interface độc lập (không kế thừa `Collection`), đại diện cho cấu trúc dữ liệu lưu trữ dưới dạng cặp khóa-giá trị **(Key - Value Pairs)**. Mỗi Key là duy nhất và trỏ tới tối đa một Value tương ứng.

---

## Bảng tham chiếu các phương thức cốt lõi

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `put(K key, V value)` | Thêm/Cập nhật | Lưu cặp `key-value` vào Map. Nếu key đã có, ghi đè value cũ. | Lưu dữ liệu | Trả về value cũ hoặc `null` |
| `get(Object key)` | Lấy dữ liệu | Lấy giá trị ứng với `key`. | Tra cứu | Trả về `null` nếu key không có |
| `getOrDefault(Object k, V def)` | Lấy có giá trị mặc định | Lấy giá trị ứng với `k`, nếu không có trả về `def`. | Tra cứu an toàn | Tránh được NullPointerException |
| `remove(Object key)` | Xóa theo key | Loại bỏ cặp dữ liệu có khóa là `key`. | Xóa dữ liệu | Trả về value bị xóa |
| `containsKey(Object key)` | Kiểm tra khóa | Trả về `true` nếu khóa `key` tồn tại trong Map. | Kiểm tra nhanh | Tốc độ rất nhanh tùy implementation |
| `containsValue(Object val)` | Kiểm tra giá trị | Trả về `true` nếu có ít nhất một key trỏ tới `val`. | Kiểm tra | Chậm hơn `containsKey` ($O(n)$) |
| `keySet()` | Lấy tập hợp khóa | Trả về một `Set<K>` chứa toàn bộ các keys của Map. | Duyệt dữ liệu | Thay đổi trên Set này ảnh hưởng trực tiếp tới Map |
| `values()` | Lấy tập hợp giá trị | Trả về một `Collection<V>` chứa toàn bộ values. | Duyệt dữ liệu | Cho phép chứa các giá trị trùng lặp |
| `entrySet()` | Lấy tập hợp cặp dữ liệu | Trả về `Set<Map.Entry<K, V>>` chứa các cặp key-value. | Duyệt dữ liệu | Tối ưu nhất khi muốn duyệt cả Key & Value |

---

## Ví dụ / Example

```java
import java.util.HashMap;
import java.util.Map;

public class MapExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Khai báo bằng Interface Map để code linh hoạt hơn
        Map<Integer, String> map = new HashMap<>();

        // 1. put(K key, V value)
        map.put(1, "One");
        map.put(2, "Two");

        // 2. get(Object key)
        String val = map.get(1); // "One"

        // 3. getOrDefault
        String valDefault = map.getOrDefault(3, "Unknown"); // "Unknown"

        // 4. containsKey / containsValue
        boolean hasKey = map.containsKey(2); // true
        boolean hasValue = map.containsValue("Three"); // false

        // 5. entrySet() dùng để duyệt Map hiệu quả nhất
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
        }
    }
}
```

---

## Lưu ý

> [!warning]
> - Đối tượng sử dụng làm **Key** bắt buộc phải triển khai chính xác các phương thức `equals()` và `hashCode()` và nên là đối tượng bất biến (như `String`, `Integer`) để tránh thay đổi giá trị băm trong thời gian chạy gây mất dữ liệu.
