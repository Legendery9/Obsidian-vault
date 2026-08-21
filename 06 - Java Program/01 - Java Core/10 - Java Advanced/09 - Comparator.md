# Java Comparator Interface

> [!abstract] Định nghĩa
> **`java.util.Comparator`** là một functional interface dùng để định nghĩa quy tắc so sánh tùy chỉnh giữa hai đối tượng. Nó độc lập với lớp của đối tượng được so sánh (khác với `Comparable` định nghĩa so sánh tự nhiên bên trong chính thực thể - xem thêm tại [[19 - Comparator and Comparable]]).

---

## 1. Tác dụng
- **Sắp xếp linh hoạt:** Cho phép định nghĩa nhiều kịch bản sắp xếp khác nhau trên cùng một tập dữ liệu (ví dụ: sắp xếp học sinh theo điểm, theo tên, hoặc theo ngày sinh).
- **Không xâm lấn mã nguồn:** Không yêu cầu lớp Entity phải triển khai interface nào hay thay đổi code hiện có.

---

## 2. Bảng tham chiếu phương thức cốt lõi (Java 8+)

| Method | Kiểu trả về | Tác dụng | Cách dùng |
| :--- | :--- | :--- | :--- |
| `compare(T o1, T o2)` | `int` | Phương thức trừu tượng duy nhất cần triển khai. Trả về số âm nếu $o1 < o2$, số dương nếu $o1 > o2$, và $0$ nếu bằng nhau. | Quy tắc so sánh thủ công. |
| `reversed()` | `Comparator<T>`| Tạo bộ so sánh đảo ngược lại quy tắc cũ. | Dùng để đổi từ tăng dần sang giảm dần. |
| `thenComparing(Comparator<T> other)`| `Comparator<T>`| Thực hiện so sánh bằng `other` nếu kết quả so sánh trước đó bằng nhau. | Sắp xếp theo nhiều tiêu chí. |
| `comparing(Function extractor)` | `Comparator<T>`| Phương thức tĩnh tạo bộ so sánh dựa trên thuộc tính được trích xuất. | Sử dụng Method Reference (ví dụ: `Student::getName`). |
| `comparingInt(ToIntFunction extractor)`| `Comparator<T>`| Tạo bộ so sánh tối ưu cho trường số nguyên. | Tránh tự động đóng gói (autoboxing) kiểu `int`. |
| `comparingDouble(ToDoubleFunction extractor)`| `Comparator<T>`| Tạo bộ so sánh tối ưu cho số thực `double`. | Tránh tự động đóng gói kiểu `double`. |
| `naturalOrder()` | `Comparator<T>`| Trả về bộ so sánh theo thứ tự tự nhiên của lớp triển khai `Comparable`. | Sắp xếp thông thường. |
| `reverseOrder()` | `Comparator<T>`| Trả về bộ so sánh nghịch đảo thứ tự tự nhiên. | Sắp xếp giảm dần mặc định. |
| `nullsFirst(Comparator<T> comp)`| `Comparator<T>`| Đẩy các phần tử mang giá trị `null` lên đầu danh sách. | An toàn khi danh sách chứa giá trị null. |
| `nullsLast(Comparator<T> comp)` | `Comparator<T>`| Đẩy các phần tử mang giá trị `null` xuống cuối danh sách. | An toàn khi danh sách chứa giá trị null. |

---

## 3. Ví dụ minh họa

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

public class ComparatorExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>(Arrays.asList(
            new Student(1, "Bình", 3.2),
            new Student(2, "An", 3.8),
            new Student(3, "Bình", 3.5),
            new Student(4, null, 3.0) // Chứa tên null để test null safety
        ));

        // 1. Khởi tạo Comparator bằng Lambda & Method Reference
        Comparator<Student> byGpa = Comparator.comparingDouble(Student::getGpa);
        
        // 2. Chaining: Sắp xếp theo tên (an toàn với null), nếu trùng tên thì sắp theo GPA giảm dần
        Comparator<Student> complexComparator = Comparator.comparing(
            Student::getName, 
            Comparator.nullsLast(Comparator.naturalOrder()) // Tên null xuống cuối
        ).thenComparing(
            Comparator.comparingDouble(Student::getGpa).reversed()
        );

        students.sort(complexComparator);
        
        for (Student s : students) {
            System.out.println(s);
        }
    }
}
```

---

## 4. Lưu ý

> [!important]
> - Nên sử dụng các phương thức tĩnh chuyên biệt như `comparingInt`, `comparingDouble` thay vì `comparing` thông thường khi so sánh kiểu dữ liệu nguyên thủy để tránh làm giảm hiệu năng hệ thống do thao tác boxing/unboxing liên tục.
> - Hãy cẩn thận khi sử dụng các thuộc tính có thể mang giá trị `null` trong so sánh. Luôn bọc chúng bằng `Comparator.nullsFirst` hoặc `Comparator.nullsLast` để tránh lỗi `NullPointerException` lúc runtime.
