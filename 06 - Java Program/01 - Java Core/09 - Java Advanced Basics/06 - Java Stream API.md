# Java Stream API

> [!abstract] Định nghĩa
> **`Stream API`** (giới thiệu từ Java 8) là một công cụ mạnh mẽ thuộc gói `java.util.stream` dùng để xử lý các tập hợp dữ liệu (Collections, Arrays) theo phong cách lập trình khai báo (declarative programming). Một luồng xử lý (Stream pipeline) gồm 3 phần chính:
> 1. **Nguồn dữ liệu (Source):** Ví dụ: `list.stream()`, `Arrays.stream(arr)`.
> 2. **Các thao tác trung gian (Intermediate Operations):** Lọc, biến đổi dữ liệu, trả về một Stream mới (lazy evaluation).
> 3. **Thao tác đầu cuối (Terminal Operation):** Kết xuất kết quả hoặc thực thi hành động, đóng Stream lại.

---

## 1. Bảng tham chiếu các phương thức Stream API phổ biến

| Loại thao tác | Method / Statement | Tác dụng | Cách dùng / Đầu vào | Lưu ý |
| --- | --- | --- | --- | --- |
| **Trung gian** | `filter(Predicate<T> p)` | Lọc các phần tử thỏa mãn điều kiện logic `p`. | Nhận biểu thức Lambda trả về boolean. | Trả về Stream chứa phần tử đã lọc. |
| **Trung gian** | `map(Function<T, R> f)` | Ánh xạ biến đổi kiểu hoặc giá trị phần tử từ `T` sang `R`. | Nhận hàm ánh xạ. | Rất phổ biến để trích xuất thuộc tính đối tượng. |
| **Trung gian** | `flatMap(Function<T, Stream<R>> f)` | Làm phẳng (flatten) các Stream con thành một Stream duy nhất. | Nhận hàm trả về một Stream. | Dùng khi phần tử chứa một List con bên trong. |
| **Trung gian** | `distinct()` | Loại bỏ các phần tử trùng lặp. | Dựa trên phương thức `equals()`. | Thao tác trạng thái (stateful), ảnh hưởng hiệu năng. |
| **Trung gian** | `sorted()` / `sorted(Comparator<T> c)` | Sắp xếp phần tử tăng dần hoặc theo tiêu chí `c`. | Không tham số hoặc nhận Comparator. | Stateful operation. Tránh dùng với luồng vô tận. |
| **Đầu cuối** | `collect(Collector<T, A, R> c)` | Thu thập dữ liệu Stream vào Collection (List, Set, Map). | Thường dùng qua `Collectors.toList()`. | Đóng Stream sau khi thực thi. |
| **Đầu cuối** | `forEach(Consumer<T> c)` | Thực thi hành động `c` trên từng phần tử. | Thao tác trên từng phần tử. | Thường chỉ dùng để in kết quả (`System.out::println`). |
| **Đầu cuối** | `count()` | Đếm và trả về tổng số phần tử còn lại trong luồng. | Trả về kiểu số nguyên `long`. | Thao tác đầu cuối. |
| **Đầu cuối** | `anyMatch(Predicate<T> p)` | Kiểm tra xem có ít nhất một phần tử thỏa mãn điều kiện `p`. | Trả về `boolean`. | Dừng kiểm tra ngay khi tìm thấy phần tử đầu tiên thỏa mãn. |

---

## 2. Ví dụ thực tế: Chuỗi biến đổi dữ liệu (Stream Pipeline)

Dưới đây là một ví dụ hoàn chỉnh minh họa cách sử dụng Stream API để lọc danh sách nhân viên, chuyển đổi kiểu, sắp xếp và thu thập kết quả.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

class Employee {
    private String name;
    private int age;
    private double salary;

    public Employee(String name, int age, double salary) {
        this.name = name;
        this.age = age;
        this.salary = salary;
    }

    public String getName() { return name; }
    public int getAge() { return age; }
    public double getSalary() { return salary; }
}

public class StreamPipelineDemo {
    public static void main(String[] args) {
        List<Employee> employees = Arrays.asList(
            new Employee("An", 25, 1200),
            new Employee("Bình", 32, 2500),
            new Employee("Cường", 28, 1800),
            new Employee("Dũng", 40, 3000),
            new Employee("An", 25, 1200) // Trùng lặp
        );

        // ✅ Nên làm (Do): Sử dụng Stream pipeline rõ ràng, phân dòng hợp lý để dễ đọc
        List<String> highSalaryNames = employees.stream()
            .filter(emp -> emp.getSalary() >= 1500)       // Lọc lương >= 1500: [Bình, Cường, Dũng]
            .distinct()                                   // Loại trùng lặp
            .sorted((e1, e2) -> Double.compare(e2.getSalary(), e1.getSalary())) // Sắp xếp lương giảm dần
            .map(Employee::getName)                       // Lấy tên: ["Dũng", "Bình", "Cường"]
            .collect(Collectors.toList());                // Thu thập thành List

        System.out.println("Nhân viên lương cao (giảm dần): " + highSalaryNames);

        // Kiểm tra nhanh điều kiện
        boolean hasSenior = employees.stream().anyMatch(emp -> emp.getAge() > 35);
        System.out.println("Có nhân viên lớn tuổi (>35) không? " + hasSenior); // true
    }
}
```

---

## 3. Lưu ý quan trọng

> [!warning]
> - **Stream không thể tái sử dụng:** Một luồng chỉ được duyệt qua một lần duy nhất. Sau khi gọi thao tác đầu cuối (Terminal Operation), Stream sẽ bị đóng lại. Bất kỳ nỗ lực gọi thao tác nào trên Stream đã đóng đều ném ra ngoại lệ runtime `IllegalStateException`.
> - **Hiệu quả lười (Lazy Evaluation):** Các thao tác trung gian sẽ không chạy cho đến khi thao tác đầu cuối được gọi. Điều này giúp tối ưu hóa hiệu năng (ví dụ: chỉ chạy lọc các phần tử cần thiết).
