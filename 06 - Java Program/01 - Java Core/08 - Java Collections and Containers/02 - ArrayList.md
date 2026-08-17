# Java ArrayList

> [!abstract] Định nghĩa
> `ArrayList` là lớp triển khai (implementation) phổ biến nhất của interface `List`, sử dụng một **mảng động (resizable array)** để lưu trữ các phần tử. Khi số lượng phần tử vượt quá dung lượng hiện tại, nó tự động tăng kích thước lên khoảng 1.5 lần.

---

## Bảng tham chiếu các phương thức & Khởi tạo

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `new ArrayList<>()` | Khởi tạo mặc định | Tạo một `ArrayList` trống với dung lượng ban đầu là 10. | Khởi tạo cơ bản | Dung lượng tự tăng khi đầy |
| `new ArrayList<>(int capacity)` | Khởi tạo với dung lượng | Tạo một `ArrayList` với dung lượng ban đầu là `capacity`. | Khởi tạo tối ưu | Giảm thiểu số lần cấp phát lại bộ nhớ |
| `ensureCapacity(int minCapacity)` | Đảm bảo dung lượng | Tăng dung lượng tối thiểu của mảng để chứa `minCapacity` phần tử. | Tối ưu hóa | Gọi trước khi add số lượng lớn phần tử |
| `trimToSize()` | Thu nhỏ dung lượng | Thu nhỏ dung lượng của `ArrayList` về đúng kích thước thực tế hiện tại. | Tối ưu bộ nhớ | Dùng khi danh sách không thay đổi nữa |

---

## Ví dụ / Example

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Định cấu hình dung lượng ban đầu nếu biết trước số phần tử tối thiểu để tránh re-allocation.
        ArrayList<String> list = new ArrayList<>(100);

        list.add("Java");
        list.add("Python");

        // 1. ensureCapacity(int minCapacity)
        list.ensureCapacity(150); // Đảm bảo chứa được ít nhất 150 phần tử không bị resize

        // 2. trimToSize()
        list.trimToSize(); // Thu nhỏ dung lượng mảng trong Heap về đúng 2 (kích thước thực tế)
    }
}
```

---

## Lưu ý

> [!warning]
> - **Hiệu năng:** `ArrayList` có hiệu năng tìm kiếm ngẫu nhiên rất nhanh ($O(1)$) qua `get(index)`. Tuy nhiên, việc chèn hoặc xóa phần tử ở vị trí giữa hoặc đầu danh sách rất chậm ($O(n)$) do phải dịch chuyển các phần tử còn lại trong mảng.
> - **Thread-safety:** `ArrayList` không đồng bộ (non-synchronized), nghĩa là không an toàn trong môi trường đa luồng (non thread-safe). Nếu cần thread-safe, dùng `Collections.synchronizedList()` hoặc `CopyOnWriteArrayList`.
