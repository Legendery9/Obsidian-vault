# Loại bỏ Trùng lặp theo Trường (Remove Duplicates by Field)

> [!info] Yêu cầu
> Loại bỏ các đối tượng trùng lặp trong một danh sách dựa trên giá trị của một trường cụ thể (ví dụ: loại bỏ các học sinh trùng ID, chỉ giữ lại học sinh đầu tiên xuất hiện trong danh sách).

---

## Giải pháp triển khai

### Cách 1: Sử dụng Stream API kết hợp với Set trạng thái (Khuyên dùng)
```java
import java.util.List;
import java.util.Set;
import java.util.concurrent.ConcurrentHashMap;
import java.util.function.Predicate;
import java.util.stream.Collectors;

public class RemoveDuplicatesStream {

    // Hàm tiện ích tạo Predicate lọc phần tử dựa trên thuộc tính
    public static <T> Predicate<T> distinctByKey(java.util.function.Function<? super T, ?> keyExtractor) {
        Set<Object> seen = ConcurrentHashMap.newKeySet();
        return t -> seen.add(keyExtractor.apply(t)); // Trả về true nếu chưa từng thấy key này
    }

    public static List<Student> removeDuplicates(List<Student> students) {
        return students.stream()
                       .filter(distinctByKey(Student::getId)) // Lọc theo ID học sinh
                       .collect(Collectors.toList());
    }
}
```

### Cách 2: Sử dụng Vòng lặp truyền thống (`for-each` kết hợp `Set`)
```java
import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;
import java.util.Set;

public class RemoveDuplicatesLoop {
    public static List<Student> removeDuplicates(List<Student> students) {
        List<Student> result = new ArrayList<>();
        Set<Integer> seenIds = new HashSet<>(); // Lưu trữ các ID đã xử lý
        
        for (Student student : students) {
            // Thêm ID vào Set. Nếu Set chưa chứa ID này (trả về true), ta thêm học sinh vào kết quả
            if (seenIds.add(student.getId())) {
                result.add(student);
            }
        }
        return result;
    }
}
```

---

## Giải thích chi tiết

- **`distinct()` mặc định của Stream:** Stream API hỗ trợ phương thức `.distinct()`. Tuy nhiên, phương thức này dựa trên `equals()` toàn bộ đối tượng để loại bỏ trùng lặp. Khi ta chỉ muốn loại bỏ dựa trên một trường cụ thể (ví dụ: `id`) mà không muốn override hoặc không thể thay đổi `equals()` của thực thể, ta phải dùng giải pháp tùy biến ở trên.
- **Cơ chế hoạt động của `distinctByKey`:**
  - `ConcurrentHashMap.newKeySet()` tạo ra một Set an toàn luồng.
  - Hàm `seen.add(...)` trả về `true` nếu phần tử chưa tồn tại trong Set và tiến hành thêm vào. Trả về `false` nếu phần tử đã có sẵn.
  - Bộ lọc `.filter()` sẽ chỉ giữ lại các đối tượng mà hàm `distinctByKey` trả về `true` (tức là thuộc tính định danh chưa từng được ghi nhận trước đó).

---

## So sánh Ưu & Nhược điểm

- **Sử dụng Stream + `distinctByKey`:**
  - *Ưu điểm:* Có thể tái sử dụng hàm `distinctByKey` cho bất kỳ kiểu dữ liệu và trường thuộc tính nào. Giữ nguyên tính chất viết code dạng khai báo (declarative) nối chuỗi.
  - *Nhược điểm:* Cần viết thêm một hàm helper phụ trợ `distinctByKey`.
- **Sử dụng Vòng lặp + Set:**
  - *Ưu điểm:* Cực kỳ trực quan, dễ hiểu đối với tất cả lập trình viên. Không cần cấu trúc helper phức tạp.
  - *Nhược điểm:* Phải viết lại cấu trúc lặp và Set trạng thái mỗi khi cần áp dụng cho một bài toán/thực thể khác.
