# Java List Interface

> [!abstract] Định nghĩa
> `List` là một interface con của `Collection`, đại diện cho một danh sách có thứ tự (ordered collection), cho phép lưu trữ các phần tử trùng lặp (duplicate elements) và truy cập phần tử thông qua chỉ số index (0-indexed).

---

## Bảng tham chiếu các phương thức cốt lõi

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `add(E e)` | Thêm phần tử | Thêm phần tử `e` vào cuối danh sách. | Thêm dữ liệu | Luôn trả về `true` |
| `add(int index, E element)` | Chèn phần tử | Chèn `element` tại vị trí `index`. | Chèn xen kẽ | Đẩy các phần tử phía sau sang phải |
| `get(int index)` | Lấy phần tử | Truy xuất phần tử tại vị trí `index`. | Lấy dữ liệu | Ném `IndexOutOfBoundsException` nếu index sai |
| `set(int index, E element)` | Thay thế phần tử | Thay thế phần tử tại `index` bằng `element`. | Cập nhật | Trả về phần tử cũ bị thay thế |
| `remove(int index)` | Xóa theo chỉ số | Xóa phần tử tại vị trí `index`. | Xóa dữ liệu | Dịch chuyển các phần tử sau sang trái |
| `remove(Object o)` | Xóa theo đối tượng | Xóa phần tử đầu tiên trùng khớp với `o`. | Xóa dữ liệu | Dựa trên hàm `equals()` để so khớp |
| `size()` | Lấy kích thước | Trả về số lượng phần tử hiện tại. | Kiểm tra | Trả về kiểu `int` |
| `isEmpty()` | Kiểm tra rỗng | Trả về `true` nếu danh sách không có phần tử nào. | Kiểm tra | Tốt hơn so sánh `size() == 0` |
| `contains(Object o)` | Kiểm tra tồn tại | Kiểm tra xem `o` có nằm trong danh sách không. | Tìm kiếm nhanh | Dựa trên hàm `equals()` để so khớp |
| `clear()` | Xóa toàn bộ | Loại bỏ tất cả các phần tử khỏi danh sách. | Dọn dẹp | Danh sách trở về rỗng (size = 0) |

---

## Ví dụ / Example

```java
import java.util.ArrayList;
import java.util.List;

public class ListExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Khai báo bằng Interface List để tăng tính linh hoạt
        List<String> list = new ArrayList<>();

        // 1. add(E e)
        list.add("Apple");
        list.add("Banana");

        // 2. add(int index, E element)
        list.add(1, "Orange"); // ["Apple", "Orange", "Banana"]

        // 3. get(int index)
        String first = list.get(0); // "Apple"

        // 4. set(int index, E element)
        list.set(2, "Mango"); // ["Apple", "Orange", "Mango"]

        // 5. remove(int index)
        list.remove(1); // ["Apple", "Mango"]

        // 6. remove(Object o)
        list.remove("Mango"); // ["Apple"]

        // 7. size()
        int size = list.size(); // 1

        // 8. isEmpty()
        boolean empty = list.isEmpty(); // false

        // 9. contains(Object o)
        boolean hasApple = list.contains("Apple"); // true

        // 10. clear()
        list.clear(); // []
    }
}
```

---

## Lưu ý

> [!warning]
> - Truy cập ngẫu nhiên (`get(index)`) của `List` có hiệu năng khác nhau tùy thuộc vào Class triển khai nó (`ArrayList` là $O(1)$ còn `LinkedList` là $O(n)$).
> - Khi gọi `remove(Object o)` hoặc `contains(Object o)`, đối tượng phần tử phải cài đặt đúng phương thức `equals()`.
