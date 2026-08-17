# Java Comparator and Comparable

> [!abstract] Định nghĩa
> **`Comparable`** và **`Comparator`** là hai interface được sử dụng để định nghĩa quy tắc sắp xếp các đối tượng tùy chỉnh trong Java (thường dùng cùng các Collections như `TreeSet`, `TreeMap` hoặc các thuật toán sắp xếp của `Collections.sort()`).

---

## Bảng tham chiếu so sánh

| Interface | Phương thức cần triển khai | Vị trí định nghĩa | Mục đích sử dụng |
| --- | --- | --- | --- |
| **`Comparable<T>`** | `compareTo(T o)` | Ngay bên trong lớp của đối tượng cần sắp xếp. | Định nghĩa thứ tự sắp xếp tự nhiên (mặc định). |
| **`Comparator<T>`** | `compare(T o1, T o2)` | Trong một lớp tách biệt (hoặc sử dụng Lambda Expression). | Định nghĩa nhiều quy tắc sắp xếp linh hoạt khác nhau. |

---

## 1. Sử dụng Comparable (Sắp xếp tự nhiên)

```java
// ✅ Nên làm (Do): Triển khai Comparable cho lớp dữ liệu để sắp xếp mặc định theo 1 thuộc tính chính.
public class Student implements Comparable<Student> {
    private String name;
    private int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Student other) {
        // Trả về số âm nếu nhỏ hơn, 0 nếu bằng, số dương nếu lớn hơn
        return Integer.compare(this.age, other.age); // Sắp xếp theo tuổi tăng dần
    }
}
```

---

## 2. Sử dụng Comparator (Sắp xếp tùy chỉnh)

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class SortExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("An", 20));
        students.add(new Student("Bình", 18));

        // ✅ Nên làm (Do): Sử dụng Lambda Expression để tạo Comparator nhanh và ngắn gọn.
        Comparator<Student> nameComparator = (s1, s2) -> s1.getName().compareTo(s2.getName());
        
        // Hoặc dùng Comparator.comparing tiện lợi
        Collections.sort(students, Comparator.comparing(Student::getName));
    }
}
```

---

## Lưu ý

> [!warning]
> - Đối với phương thức `compareTo(T o)`:
>   - Trả về số âm ($< 0$): Đối tượng hiện tại nhỏ hơn `o` (đứng trước).
>   - Trả về số không ($= 0$): Hai đối tượng bằng nhau.
>   - Trả về số dương ($> 0$): Đối tượng hiện tại lớn hơn `o` (đứng sau).
> - Hãy cẩn thận tránh tràn số (integer overflow) khi thực hiện phép trừ trực tiếp để so sánh (ví dụ: `this.id - other.id` có thể bị lỗi nếu có giá trị âm lớn). Khuyên dùng các hàm static Helper như `Integer.compare(x, y)`.
