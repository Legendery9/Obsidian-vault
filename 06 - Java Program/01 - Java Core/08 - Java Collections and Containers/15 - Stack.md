# Java Stack Class

> [!abstract] Định nghĩa
> `Stack` là một lớp cổ điển (legacy class) trong gói `java.util` kế thừa từ lớp `Vector`, triển khai cấu trúc dữ liệu ngăn xếp **LIFO (Last In, First Out - Vào sau, Ra trước)**.

---

## Bảng tham chiếu các phương thức

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `push(E item)` | Đẩy phần tử | Đưa phần tử `item` vào đỉnh ngăn xếp. | Thao tác Stack | Trả về chính `item` đó |
| `pop()` | Lấy ra & Xóa | Lấy ra và loại bỏ phần tử ở đỉnh ngăn xếp. | Thao tác Stack | Ném `EmptyStackException` nếu rỗng |
| `peek()` | Xem đỉnh | Lấy phần tử đỉnh ngăn xếp nhưng không xóa. | Tra cứu nhanh | Ném `EmptyStackException` nếu rỗng |
| `empty()` | Kiểm tra rỗng | Trả về `true` nếu ngăn xếp không chứa phần tử nào. | Kiểm tra | Thay thế cho `isEmpty()` của Vector |
| `search(Object o)` | Tìm vị trí | Trả về khoảng cách 1-based từ đỉnh ngăn xếp đến phần tử `o`. | Tìm kiếm | Trả về `-1` nếu không tìm thấy |

---

## Ví dụ / Example

```java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        // ❌ Không nên làm (Don't): Dùng lớp Stack cổ điển trong các dự án mới vì hiệu năng kém do đồng bộ.
        Stack<String> stack = new Stack<>();

        stack.push("Base");
        stack.push("Top");

        System.out.println(stack.peek()); // "Top"
        System.out.println(stack.pop()); // "Top" (Bị loại bỏ)

        // 1. search(Object o)
        int position = stack.search("Base"); // Trả về 1 (cách đỉnh 1 khoảng đơn vị)
    }
}
```

---

## Lưu ý

> [!warning]
> - **Hiệu năng kém:** Lớp `Stack` kế thừa từ `Vector`, do đó tất cả các phương thức của nó đều được **đồng bộ hóa (synchronized)**. Điều này gây tốn hiệu năng khi chạy đơn luồng.
> - **Lời khuyên:** Thay vì sử dụng `Stack`, hãy sử dụng **`ArrayDeque`** (ví dụ: `Deque<T> stack = new ArrayDeque<>();`) để làm cấu trúc ngăn xếp tối ưu và nhanh hơn.
