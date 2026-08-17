# Java TreeSet

> [!abstract] Định nghĩa
> `TreeSet` là lớp triển khai của `NavigableSet` (kế thừa từ `SortedSet`), sử dụng cấu trúc **cây đỏ-đen (red-black tree)** để lưu trữ các phần tử. Nó duy trì các phần tử theo **thứ tự sắp xếp tự nhiên (natural ordering)** hoặc theo một bộ so sánh **`Comparator`** tự định nghĩa.

---

## Bảng tham chiếu các phương thức bổ sung (từ Sorted/NavigableSet)

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `new TreeSet<>()` | Khởi tạo tự nhiên | Tạo một `TreeSet` trống, sắp xếp theo thứ tự tự nhiên (ví dụ: số tăng dần, chữ cái A-Z). | Khởi tạo cơ bản | Đối tượng phải implements `Comparable` |
| `new TreeSet`(Comparator c) | Khởi tạo với so sánh | Tạo một `TreeSet` sắp xếp theo quy tắc tùy chỉnh của `Comparator`. | Sắp xếp tùy chọn | Dùng cho các Class tự tạo |
| `first()` | Lấy phần tử nhỏ nhất | Trả về phần tử đầu tiên (nhỏ nhất) hiện tại. | Tra cứu giới hạn | Ném `NoSuchElementException` nếu rỗng |
| `last()` | Lấy phần tử lớn nhất | Trả về phần tử cuối cùng (lớn nhất) hiện tại. | Tra cứu giới hạn | Ném `NoSuchElementException` nếu rỗng |
| `higher(E e)` | Lấy phần tử lớn hơn | Trả về phần tử nhỏ nhất trong số các phần tử lớn hơn hẳn `e`. | Tra cứu động | Trả về `null` nếu không có |
| `lower(E e)` | Lấy phần tử nhỏ hơn | Trả về phần tử lớn nhất trong số các phần tử nhỏ hơn hẳn `e`. | Tra cứu động | Trả về `null` nếu không có |

---

## Ví dụ / Example

```java
import java.util.TreeSet;

public class TreeSetExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Sử dụng TreeSet khi cần các phần tử luôn được SẮP XẾP TỰ ĐỘNG khi thêm vào.
        TreeSet<Integer> set = new TreeSet<>();
        
        set.add(40);
        set.add(10);
        set.add(30);

        System.out.println(set); // In ra: [10, 30, 40] (Tự sắp xếp tăng dần)

        // 1. first / last
        int min = set.first(); // 10
        int max = set.last(); // 40

        // 2. higher / lower
        Integer high = set.higher(30); // 40
        Integer low = set.lower(30); // 10
    }
}
```

---

## Lưu ý

> [!warning]
> - **Hiệu năng:** Do phải cân bằng lại cây nhị phân mỗi khi thêm/sửa/xóa, hiệu năng của `TreeSet` chậm hơn nhiều so với `HashSet`, với độ phức tạp thuật toán là **$O(\log n)$**.
> - **Ràng buộc phần tử:** Các phần tử thêm vào `TreeSet` bắt buộc phải triển khai interface `Comparable` (hoặc phải truyền `Comparator` vào constructor của `TreeSet`). Nếu không, chương trình sẽ ném ra lỗi `ClassCastException` lúc chạy.
