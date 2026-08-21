# Java Collection Interface

> [!abstract] Định nghĩa
> **`java.util.Collection`** là interface gốc (root interface) trong hệ thống phân cấp Collection Framework. Nó định nghĩa các hành vi chung nhất cho các cấu trúc dữ liệu dạng tập hợp (ngoại trừ Map).

---

## 1. Phân biệt Collection (Interface) vs Collections (Class)

- **`Collection` (Interface):** Là một giao diện lập trình định nghĩa các phương thức cốt lõi mà các cấu trúc dữ liệu con như `List`, `Set`, `Queue` phải triển khai (xem chi tiết tại [[01 - List]] và [[04 - Set]]).
- **`Collections` (Utility Class):** Là một lớp tiện ích (`java.util.Collections`) chỉ chứa các phương thức tĩnh (`static`) dùng để thao tác trên các collection như sắp xếp (`sort`), đảo ngược (`reverse`), tìm kiếm nhị phân (`binarySearch`), hay tạo các collection bất biến (`unmodifiableList`).

---

## 2. Bảng tham chiếu phương thức của Collection Interface

Các phương thức này được kế thừa và dùng chung bởi mọi lớp con triển khai `Collection` (như `ArrayList`, `HashSet`).

| Method / Statement | Kiểu trả về | Tác dụng | Cách dùng / Lưu ý |
| :--- | :--- | :--- | :--- |
| `add(E e)` | `boolean` | Thêm phần tử `e` vào tập hợp. | Trả về `false` nếu phần tử đã tồn tại (ở `Set`). |
| `addAll(Collection<? extends E> c)`| `boolean` | Thêm toàn bộ phần tử của `c` vào tập hợp hiện tại. | Thao tác hợp nhất dữ liệu (Union). |
| `remove(Object o)` | `boolean` | Xóa phần tử `o` khỏi tập hợp. | Dựa vào `equals()` để xác định phần tử cần xóa. |
| `removeAll(Collection<?> c)` | `boolean` | Xóa tất cả phần tử thuộc `c` ra khỏi tập hợp hiện tại. | Thao tác hiệu (Difference). |
| `retainAll(Collection<?> c)` | `boolean` | Chỉ giữ lại các phần tử cũng thuộc `c`. | Thao tác giao (Intersection). |
| `contains(Object o)` | `boolean` | Kiểm tra xem `o` có nằm trong tập hợp hay không. | Trả về `true`/`false`. |
| `containsAll(Collection<?> c)` | `boolean` | Kiểm tra tập hợp hiện tại có chứa toàn bộ phần tử của `c`. | Kiểm tra tập con (Subset). |
| `size()` | `int` | Trả về số lượng phần tử hiện tại. | |
| `isEmpty()` | `boolean` | Kiểm tra tập hợp có rỗng hay không. | |
| `clear()` | `void` | Xóa sạch toàn bộ phần tử. | |
| `toArray()` | `Object[]` | Chuyển đổi tập hợp thành mảng thông thường. | Thường dùng `toArray(T[] a)` để giữ đúng kiểu dữ liệu. |
| `iterator()` | `Iterator<E>` | Trả về đối tượng duyệt qua các phần tử. | Hỗ trợ duyệt và xóa an toàn trong vòng lặp. |
| `stream()` | `Stream<E>` | Chuyển tập hợp thành luồng dữ liệu Stream. | Cung cấp khả năng xử lý song song/tuần tự. |

---

## 3. Ví dụ minh họa

```java
import java.util.ArrayList;
import java.util.Collection;
import java.util.HashSet;
import java.util.List;

public class CollectionInterfaceExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Khai báo bằng interface Collection để dễ dàng hoán đổi cấu trúc lưu trữ bên dưới
        Collection<String> col1 = new ArrayList<>();
        col1.add("Java");
        col1.add("Python");

        Collection<String> col2 = new HashSet<>();
        col2.add("C++");
        col2.add("Java");

        // 1. addAll (Union)
        col1.addAll(col2); // col1 lúc này chứa: ["Java", "Python", "C++", "Java"] (ArrayList cho phép trùng)

        // 2. containsAll
        System.out.println("col1 chứa toàn bộ col2: " + col1.containsAll(col2)); // true

        // 3. retainAll (Giao hai tập hợp)
        col1.retainAll(col2); // col1 giữ lại những phần tử có trong col2: ["Java", "C++", "Java"]

        // 4. Chuyển sang mảng toArray
        String[] arr = col1.toArray(new String[0]);
        
        // 5. clear
        col1.clear();
        System.out.println("col1 trống: " + col1.isEmpty()); // true
    }
}
```

---

## 4. Lưu ý

> [!warning]
> - Một số phương thức của `Collection` như `add` hay `remove` có thể ném ra `UnsupportedOperationException` nếu cấu trúc dữ liệu bên dưới là bất biến (ví dụ tạo bởi `List.of()` hoặc `Collections.unmodifiableCollection()`).
