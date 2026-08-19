# Lọc, Biến đổi và Thu gom (Filter - Map - Collect)

> [!info] Yêu cầu
> Lọc một danh sách các đối tượng theo một điều kiện cụ thể (Filter), sau đó trích xuất lấy một thuộc tính nhất định của các đối tượng thỏa mãn (Map), rồi thu gom toàn bộ kết quả thành một Collection mới như List hoặc Set (Collect).

---

## Giải pháp triển khai

### Cách 1: Sử dụng Stream API (Khuyên dùng)
```java
import java.util.List;
import java.util.Set;
import java.util.stream.Collectors;

public class FilterMapCollectStream {
    
    // Lấy danh sách tên của các học sinh có điểm GPA >= 3.5
    public static List<String> getTopStudentNames(List<Student> students) {
        return students.stream()
                       .filter(student -> student.getGpa() >= 3.5) // Lọc học sinh giỏi
                       .map(Student::getName)                     // Trích xuất lấy tên
                       .collect(Collectors.toList());             // Thu gom về List
    }

    // Lấy tập hợp (Set) các ID của học sinh giỏi (để đảm bảo không trùng lặp)
    public static Set<Integer> getTopStudentIds(List<Student> students) {
        return students.stream()
                       .filter(student -> student.getGpa() >= 3.5)
                       .map(Student::getId)
                       .collect(Collectors.toSet());              // Thu gom về Set
    }
}
```

### Cách 2: Sử dụng Vòng lặp truyền thống (`for-each`)
```java
import java.util.ArrayList;
import java.util.List;

public class FilterMapCollectLoop {
    public static List<String> getTopStudentNames(List<Student> students) {
        List<String> names = new ArrayList<>(); // Phải tự khởi tạo danh sách chứa kết quả
        
        for (Student student : students) {
            if (student.getGpa() >= 3.5) {      // Thao tác Filter
                names.add(student.getName());   // Thao tác Map và thêm vào danh sách kết quả
            }
        }
        return names;
    }
}
```

---

## Giải thích chi tiết

Chuỗi lệnh Stream hoạt động theo mô hình đường ống (Pipeline):
1. **`stream()`**: Chuyển đổi Collection ban đầu thành một Stream dữ liệu để xử lý tuần tự hoặc song song.
2. **`filter(Predicate<T>)`**: Lọc các phần tử. Nhận vào một biểu thức Lambda trả về `boolean`. Chỉ các phần tử trả về `true` mới được đi tiếp qua đường ống.
3. **`map(Function<T, R>)`**: Ánh xạ/Chuyển đổi kiểu dữ liệu. Phương thức này biến đổi mỗi phần tử kiểu `T` thành một phần tử kiểu `R` (trong ví dụ là từ thực thể `Student` thành chuỗi `String` tên học sinh).
4. **`collect(Collector)`**: Thao tác thu gom dữ liệu cuối cùng (terminal operation) để đóng gói dữ liệu Stream thành một Collection cụ thể (`List`, `Set`, `Map`...).

---

## So sánh Ưu & Nhược điểm

- **Stream API:** 
  - *Ưu điểm:* Cú pháp dạng chuỗi (fluent API) rất trực quan, phản ánh đúng luồng tư duy xử lý dữ liệu. Dễ dàng bảo trì và mở rộng thêm các bước trung gian (như sắp xếp, giới hạn số lượng).
  - *Nhược điểm:* Đọc hiểu khó hơn nếu chưa quen với mô hình Lambda và Stream.
- **Vòng lặp truyền thống:**
  - *Ưu điểm:* Không phát sinh chi phí trung gian của Stream, tối ưu bộ nhớ. Dễ dàng debug bằng cách đặt breakpoint bên trong vòng lặp.
  - *Nhược điểm:* Phải tự quản lý việc khởi tạo Collection kết quả và viết nhiều mã mẫu (boilerplate code).
