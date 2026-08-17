# Java Vector Class

> [!abstract] Định nghĩa
> `Vector` là một lớp cổ điển (legacy class) triển khai interface `List`, sử dụng một mảng động tương tự như `ArrayList`. Điểm khác biệt lớn nhất là tất cả các phương thức của `Vector` đều được **đồng bộ hóa (synchronized)** để đảm bảo an toàn đa luồng.

---

## Bảng tham chiếu các phương thức & Khởi tạo

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `new Vector<>()` | Khởi tạo mặc định | Tạo một `Vector` trống có dung lượng mặc định là 10. | Khởi tạo cơ bản | Đồng bộ hóa toàn bộ |
| `addElement(E obj)` | Thêm phần tử | Thêm phần tử `obj` vào cuối Vector (tương đương `add(e)`). | Thao tác legacy | Dùng trong các API cũ |
| `capacity()` | Lấy dung lượng | Trả về dung lượng bộ nhớ hiện tại của Vector. | Kiểm tra bộ nhớ | Khác với `size()` |

---

## Ví dụ / Example

```java
import java.util.Vector;

public class VectorExample {
    public static void main(String[] args) {
        // ❌ Không nên làm (Don't): Sử dụng Vector trong các ứng dụng đơn luồng vì chi phí đồng bộ hóa làm giảm hiệu năng.
        Vector<String> vector = new Vector<>();

        vector.add("One");
        vector.addElement("Two"); // Hàm legacy đặc trưng

        System.out.println(vector.capacity()); // 10
    }
}
```

---

## Lưu ý

> [!warning]
> - **Hiệu năng:** Do đồng bộ hóa ở mọi phương thức, `Vector` chạy chậm hơn `ArrayList` rất nhiều.
> - **Thay thế:** Nếu cần cấu trúc mảng động an toàn đa luồng (thread-safe), khuyến khích sử dụng **`CopyOnWriteArrayList`** hoặc sử dụng wrapper **`Collections.synchronizedList()`** thay vì dùng `Vector`.
