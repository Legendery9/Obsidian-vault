# Gom nhóm đối tượng (Grouping By)

> [!info] Yêu cầu
> Phân loại và gom nhóm một danh sách các đối tượng thành một `Map`, trong đó khóa (Key) là giá trị thuộc tính phân loại và giá trị (Value) là danh sách các đối tượng thuộc nhóm đó.

---

## Giải pháp triển khai

Giả sử thực thể `Student` có thêm trường thuộc tính `classroom` (kiểu `String`) đại diện cho lớp học của học sinh.

### Cách 1: Sử dụng Stream API (`Collectors.groupingBy`) - Khuyên dùng
```java
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class GroupingByStream {
    public static Map<String, List<Student>> groupByClassroom(List<Student> students) {
        return students.stream()
                       .collect(
                           Collectors.groupingBy(Student::getClassroom) // Gom nhóm theo lớp
                       );
    }
}
```

### Cách 2: Sử dụng Vòng lặp truyền thống (`for-each`)
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class GroupingByLoop {
    public static Map<String, List<Student>> groupByClassroom(List<Student> students) {
        Map<String, List<Student>> map = new HashMap<>();
        
        for (Student student : students) {
            String classroom = student.getClassroom();
            
            // Nếu nhóm chưa tồn tại trong map, khởi tạo một danh sách mới
            map.computeIfAbsent(classroom, k -> new ArrayList<>())
               .add(student); // Thêm học sinh vào nhóm tương ứng
        }
        return map;
    }
}
```

---

## Giải thích chi tiết

- **`Collectors.groupingBy(Classifier)`**: Là một hàm gom tụ (Collector) cực kỳ mạnh mẽ. Nó nhận vào một hàm phân loại (classifier function) để quyết định phần tử sẽ thuộc về khóa nào trong `Map` kết quả.
- **`Map.computeIfAbsent(Key, Function)`**: Trong cách viết vòng lặp truyền thống, phương thức này của Java 8 giúp rút ngắn đáng kể code. Nếu khóa chưa tồn tại trong Map, nó tự động áp dụng hàm lambda để khởi tạo value (trong ví dụ là `new ArrayList<>()`), đưa vào Map, và trả về tham chiếu của value đó để ta tiếp tục gọi `.add()`.

---

## So sánh Hiệu năng & Cách viết

| Tiêu chí | Stream API (`groupingBy`) | Vòng lặp truyền thống |
| :--- | :--- | :--- |
| **Độ phức tạp code**| ⚡ Cực kỳ ngắn gọn, giảm thiểu lỗi logic thủ công. | Dài hơn, cần tự viết mã kiểm tra sự tồn tại của Key. |
| **Tính linh hoạt** | Có thể lồng ghép gom nhóm đa cấp bằng cách truyền thêm Collector phụ (downstream collector), ví dụ: đếm số học sinh mỗi lớp. | Rất phức tạp khi cần gom nhóm nhiều tầng hoặc tính toán gom tụ sâu. |
| **Kiểu Map trả về** | Mặc định là `HashMap`. Có thể tùy biến sang `TreeMap` hoặc `LinkedHashMap` bằng cách truyền supplier. | Tự do định nghĩa lớp triển khai của `Map` ngay từ lúc khởi tạo. |
