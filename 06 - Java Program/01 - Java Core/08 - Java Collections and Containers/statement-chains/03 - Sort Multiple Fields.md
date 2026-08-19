# Sắp xếp theo Nhiều Tiêu chí (Sort Multiple Fields)

> [!info] Yêu cầu
> Sắp xếp một danh sách các đối tượng theo nhiều trường thuộc tính ưu tiên (ví dụ: sắp xếp học sinh theo tên tăng dần A-Z; nếu trùng tên, ưu tiên học sinh có điểm GPA giảm dần).

---

## Giải pháp triển khai

### Cách 1: Sử dụng Stream API và Comparator Chaining (Khuyên dùng)
```java
import java.util.Comparator;
import java.util.List;
import java.util.stream.Collectors;

public class SortMultipleFieldsStream {
    public static List<Student> sortByNameAndGpa(List<Student> students) {
        return students.stream()
                       .sorted(
                           Comparator.comparing(Student::getName) // Tiêu chí 1: Tên tăng dần
                                     .thenComparing(
                                         Comparator.comparingDouble(Student::getGpa)
                                                   .reversed() // Tiêu chí 2: GPA giảm dần
                                     )
                       )
                       .collect(Collectors.toList()); // Trả về danh sách mới đã sắp xếp
    }
}
```

### Cách 2: Sắp xếp tại chỗ trên List hiện tại (In-place sort)
```java
import java.util.Comparator;
import java.util.List;

public class SortMultipleFieldsInPlace {
    public static void sortInPlace(List<Student> students) {
        // Thay đổi trực tiếp vị trí phần tử trong danh sách truyền vào
        students.sort(
            Comparator.comparing(Student::getName)
                      .thenComparing(Student::getGpa, Comparator.reverseOrder())
        );
    }
}
```

---

## Giải thích chi tiết

- **`Comparator.comparing(Function)`**: Tạo ra một đối tượng `Comparator` dựa trên thuộc tính được trích xuất (trong ví dụ là `Student::getName`). Mặc định sắp xếp theo thứ tự tăng dần.
- **`thenComparing(Comparator)`**: Chuỗi hóa tiêu chí. Nếu tiêu chí thứ nhất so sánh ra kết quả bằng nhau (`compare == 0`), JVM sẽ chuyển sang sử dụng tiêu chí so sánh thứ hai được cấu hình trong `thenComparing`.
- **`reversed()`**: Đảo ngược thứ tự sắp xếp của Comparator liền trước nó (biến tăng dần thành giảm dần).
- **`Comparator.comparingDouble()`**: Chuyên biệt cho kiểu nguyên thủy `double`, tránh việc auto-boxing không cần thiết lên `Double`, giúp cải thiện hiệu năng khi xử lý danh sách lớn.

---

## Lưu ý

> [!warning]
> - Phương thức `Stream.sorted()` không làm thay đổi danh sách ban đầu mà tạo ra một danh sách mới. Ngược lại, `List.sort()` sẽ thay đổi trực tiếp cấu trúc của danh sách truyền vào.
> - Các trường thuộc tính dùng để so sánh (như `name`) không được phép mang giá trị `null`, nếu không sẽ ném ra lỗi `NullPointerException`. Để an toàn với giá trị null, ta có thể dùng `Comparator.nullsFirst` hoặc `Comparator.nullsLast`:
>   ```java
>   Comparator.comparing(Student::getName, Comparator.nullsLast(String::compareTo))
>   ```
