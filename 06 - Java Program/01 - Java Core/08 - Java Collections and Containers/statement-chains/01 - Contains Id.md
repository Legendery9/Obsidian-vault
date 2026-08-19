# Kiểm tra Danh sách chứa ID (Contains ID)

> [!info] Yêu cầu
> Kiểm tra xem một danh sách các đối tượng (Entity) có chứa ít nhất một phần tử có trường định danh (ID) bằng với giá trị cần tìm hay không.

---

## Giải pháp triển khai

### Cách 1: Sử dụng Stream API (`anyMatch`) - Khuyên dùng
```java
import java.util.List;

public class ContainsIdStream {
    public static boolean hasId(List<Student> list, int targetId) {
        // Sử dụng anyMatch để kiểm tra điều kiện
        return list.stream()
                   .anyMatch(student -> student.getId() == targetId);
    }
}
```

### Cách 2: Sử dụng Vòng lặp truyền thống (`for-each`)
```java
import java.util.List;

public class ContainsIdLoop {
    public static boolean hasId(List<Student> list, int targetId) {
        // Duyệt tuyến tính qua từng phần tử
        for (Student student : list) {
            if (student.getId() == targetId) {
                return true; // Trả về ngay khi tìm thấy
            }
        }
        return false;
    }
}
```

---

## Giải thích chi tiết

- **Cơ chế hoạt động:** cả hai phương thức đều thực hiện tìm kiếm tuyến tính với độ phức tạp thời gian là $O(n)$ trong trường hợp xấu nhất (phải duyệt hết danh sách).
- **Tính chất Short-circuiting (Đánh giá ngắn mạch):**
  - Trong Stream API, `anyMatch` là một thao tác ngắn mạch (short-circuiting terminal operation). Ngay khi tìm thấy phần tử đầu tiên thỏa mãn lambda expression, nó sẽ dừng duyệt và trả về `true`.
  - Vòng lặp `for-each` đạt được điều này nhờ câu lệnh `return true;` nằm bên trong khối lệnh `if`.

---

## So sánh Ưu & Nhược điểm

| Tiêu chí | Stream API (`anyMatch`) | Vòng lặp truyền thống |
| :--- | :--- | :--- |
| **Độ ngắn gọn** | ⚡ Rất ngắn (chỉ 1 dòng lệnh). | 🐢 Dài dòng hơn (cần tạo cấu trúc lặp). |
| **Đọc hiểu** | Dễ hiểu theo ngôn ngữ tự nhiên (khai báo - declarative). | Dễ hiểu với người mới bắt đầu (mô tả các bước thực hiện - imperative). |
| **Hiệu năng** | Có một chút chi phí khởi tạo Stream (không đáng kể trong phần lớn trường hợp). | Đạt hiệu năng tối đa (không có chi phí phụ). |
