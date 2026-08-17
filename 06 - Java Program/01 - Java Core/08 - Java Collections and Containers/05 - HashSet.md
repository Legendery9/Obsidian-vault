# Java HashSet

> [!abstract] Định nghĩa
> `HashSet` là lớp triển khai phổ biến nhất của interface `Set`, sử dụng một **bảng băm (hash table)** (thực chất là một đối tượng `HashMap` chạy ngầm bên dưới) để lưu trữ các phần tử. Nó không đảm bảo bất kỳ thứ tự nào của phần tử theo thời gian.

---

## Bảng tham chiếu các phương thức & Khởi tạo

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `new HashSet<>()` | Khởi tạo mặc định | Tạo một `HashSet` trống, dung lượng ban đầu là 16 và hệ số tải (load factor) là 0.75. | Khởi tạo cơ bản | Phổ biến nhất |
| `new HashSet<>(int initialCapacity)` | Khởi tạo với dung lượng | Tạo một `HashSet` với dung lượng ban đầu chỉ định. | Tối ưu hóa | Tránh băm lại (re-hashing) nhiều lần |
| `new HashSet<>(Collection<? extends E> c)` | Khởi tạo từ Collection | Tạo một `HashSet` chứa các phần tử của collection `c`. | Lọc trùng nhanh | Tự động loại bỏ phần tử trùng trong `c` |

---

## Ví dụ / Example

```java
import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;

public class HashSetExample {
    public static void main(String[] args) {
        List<String> listWithDuplicates = new ArrayList<>();
        listWithDuplicates.add("A");
        listWithDuplicates.add("B");
        listWithDuplicates.add("A");

        // ✅ Nên làm (Do): Sử dụng HashSet để lọc trùng nhanh từ một List sẵn có
        HashSet<String> uniqueSet = new HashSet<>(listWithDuplicates);
        
        System.out.println(uniqueSet); // ["A", "B"] (Thứ tự không cố định)
    }
}
```

---

## Lưu ý

> [!warning]
> - **Hiệu năng:** Tất cả các thao tác cơ bản như `add()`, `remove()`, `contains()` đều có hiệu năng cực nhanh là **$O(1)$** trong trường hợp hàm băm phân bổ đều.
> - **Yêu cầu đối tượng:** Để `HashSet` hoạt động chính xác, các đối tượng lưu trữ bên trong phải cài đặt đúng phương thức `hashCode()` và `equals()`. Nếu hai đối tượng có `equals()` trả về `true` thì bắt buộc `hashCode()` của chúng cũng phải trả về cùng một số nguyên.
