# Java LinkedHashSet

> [!abstract] Định nghĩa
> `LinkedHashSet` là một lớp con của `HashSet`, kế thừa cấu trúc bảng băm nhưng bổ sung thêm một **danh sách liên kết kép (doubly-linked list)** chạy xuyên qua toàn bộ phần tử. Nhờ đó, nó duy trì chính xác **thứ tự chèn (insertion order)** của các phần tử.

---

## Bảng tham chiếu các phương thức & Khởi tạo

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `new LinkedHashSet<>()` | Khởi tạo mặc định | Tạo một `LinkedHashSet` trống, duy trì thứ tự chèn. | Khởi tạo cơ bản | Giống `HashSet` nhưng có thứ tự |
| `new LinkedHashSet`(int capacity) | Khởi tạo với dung lượng | Tạo một `LinkedHashSet` với dung lượng ban đầu được cấu hình trước. | Tối ưu hóa | Tránh resize |

---

## Ví dụ / Example

```java
import java.util.LinkedHashSet;
import java.util.Set;

public class LinkedHashSetExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Sử dụng LinkedHashSet khi cần lọc trùng nhưng bắt buộc phải GIỮ NGUYÊN THỨ TỰ đưa vào.
        Set<String> set = new LinkedHashSet<>();
        
        set.add("Zebra");
        set.add("Apple");
        set.add("Mango");
        
        // In ra màn hình luôn theo đúng thứ tự chèn: [Zebra, Apple, Mango]
        System.out.println(set); 
    }
}
```

---

## Lưu ý

> [!warning]
> - **Hiệu năng:** Độ phức tạp cho các thao tác thêm, xóa, tìm kiếm vẫn là **$O(1)$**, nhưng chậm hơn một chút so với `HashSet` do phải tốn chi phí CPU duy trì các con trỏ liên kết kép.
> - **Tốn bộ nhớ:** Tiêu hao bộ nhớ nhiều hơn `HashSet` vì mỗi phần tử phải chứa thêm thông tin liên kết trước/sau.
