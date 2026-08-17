# Java TreeMap

> [!abstract] Định nghĩa
> `TreeMap` là lớp triển khai của interface `NavigableMap` (kế thừa từ `SortedMap`), sử dụng cấu trúc **cây đỏ-đen (red-black tree)** để lưu trữ. Nó tự động sắp xếp các cặp key-value theo thứ tự tăng dần của các **Key**.

---

## Bảng tham chiếu các phương thức bổ sung (từ Sorted/NavigableMap)

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `new TreeMap<>()` | Khởi tạo mặc định | Tạo một `TreeMap` rỗng sắp xếp theo thứ tự tự nhiên của khóa. | Khởi tạo cơ bản | Khóa phải triển khai `Comparable` |
| `firstKey()` | Khóa nhỏ nhất | Trả về khóa nhỏ nhất hiện có trong Map. | Tra cứu giới hạn | Ném `NoSuchElementException` nếu rỗng |
| `lastKey()` | Khóa lớn nhất | Trả về khóa lớn nhất hiện có trong Map. | Tra cứu giới hạn | Ném `NoSuchElementException` nếu rỗng |
| `higherKey(K key)` | Khóa lớn hơn | Trả về khóa nhỏ nhất trong số các khóa lớn hơn hẳn `key`. | Tìm kiếm động | Trả về `null` nếu không có |
| `lowerKey(K key)` | Khóa nhỏ hơn | Trả về khóa lớn nhất trong số các khóa nhỏ hơn hẳn `key`. | Tìm kiếm động | Trả về `null` nếu không có |

---

## Ví dụ / Example

```java
import java.util.TreeMap;

public class TreeMapExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Sử dụng TreeMap khi cần các cặp dữ liệu tự động sắp xếp theo thứ tự của Key.
        TreeMap<String, String> map = new TreeMap<>();
        
        map.put("Zebra", "Stripes");
        map.put("Apple", "Fruit");
        map.put("Banana", "Yellow");

        System.out.println(map); // In ra: {Apple=Fruit, Banana=Yellow, Zebra=Stripes} (Sắp xếp A-Z theo Key)

        // 1. firstKey / lastKey
        String first = map.firstKey(); // "Apple"
        String last = map.lastKey(); // "Zebra"

        // 2. higherKey
        String next = map.higherKey("Banana"); // "Zebra"
    }
}
```

---

## Lưu ý

> [!warning]
> - **Hiệu năng:** Do phải cân bằng lại cây nhị phân mỗi khi thực hiện thay đổi dữ liệu, các thao tác `put()`, `get()`, `remove()` của `TreeMap` chậm hơn nhiều so với `HashMap`, với độ phức tạp thuật toán là **$O(\log n)$**.
> - **Key không được null:** Khác với `HashMap`, `TreeMap` **không cho phép khóa `null`** (ném lỗi `NullPointerException` ngay lập tức). Các khóa thêm vào bắt buộc phải so sánh được với nhau.
