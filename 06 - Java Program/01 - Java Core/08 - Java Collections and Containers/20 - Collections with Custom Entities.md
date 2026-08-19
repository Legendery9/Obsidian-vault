# Java Collections with Custom Entities

> [!abstract] Định nghĩa
> Khi làm việc với Java Collections, ta không chỉ lưu trữ các kiểu dữ liệu nguyên thủy đóng gói (`List<Integer>`, `Set<String>`) mà còn lưu trữ các đối tượng tự định nghĩa (**Entities** hay **Custom Objects** như `List<Student>`, `Map<String, Student>`). Việc cấu hình đúng các phương thức cốt lõi của Entity quyết định hành vi chính xác của Collection.

---

## 1. Lưu ý khi dùng Entity làm phần tử hoặc khoá (Key)

### 1.1. Bắt buộc Override `equals()` và `hashCode()`
Mặc định, lớp `Object` trong Java so sánh hai đối tượng dựa trên địa chỉ tham chiếu vùng nhớ (toán tử `==`). 
- **Tại sao cần override?** Nếu ta muốn hai đối tượng khác vùng nhớ nhưng có cùng dữ liệu thuộc tính (ví dụ: cùng `id`) được coi là bằng nhau trong các thao tác tìm kiếm (`contains()`, `indexOf()`, `remove()`), ta phải override `equals()`.
- **Quy tắc Hashing:** Nếu hai đối tượng bằng nhau theo `equals()`, thì mã băm `hashCode()` của chúng **bắt buộc phải giống nhau**. Điều này đặc biệt quan trọng khi sử dụng entity làm phần tử trong `HashSet` hoặc làm khóa (Key) trong `HashMap`. Nếu không cài đặt đúng, các collection dạng băm sẽ không thể định vị chính xác phần tử và dẫn đến lưu trữ trùng lặp dữ liệu.

### 1.2. Implement `Comparable` hoặc dùng `Comparator`
Các cấu trúc dữ liệu có tính chất tự sắp xếp (như `TreeSet`, `TreeMap`) hoặc các thao tác sắp xếp (`Collections.sort()`, `List.sort()`) yêu cầu xác định cách so sánh độ lớn giữa các đối tượng.
- **`Comparable` (So sánh tự nhiên - Natural Ordering):** Lớp Entity triển khai interface `Comparable<T>` và override phương thức `compareTo()`. Thích hợp khi thực thể có một tiêu chí sắp xếp mặc định rõ ràng (ví dụ: theo `id` tăng dần).
- **`Comparator` (So sánh tùy chỉnh):** Sử dụng các bộ so sánh ngoài lớp thực thể, linh hoạt khi cần sắp xếp theo nhiều tiêu chí khác nhau (theo tên, theo tuổi, theo điểm số).

---

## 2. Ví dụ Code triển khai hoàn chỉnh

### Lớp Entity `Student` chuẩn hóa

```java
import java.util.Objects;

public class Student implements Comparable<Student> {
    private int id;
    private String name;
    private double gpa;

    public Student(int id, String name, double gpa) {
        this.id = id;
        this.name = name;
        this.gpa = gpa;
    }

    public int getId() { return id; }
    public String getName() { return name; }
    public double getGpa() { return gpa; }

    // 1. Override equals: Định nghĩa hai học sinh trùng ID là một học sinh duy nhất
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return id == student.id;
    }

    // 2. Override hashCode: Bắt buộc đi kèm với equals
    @Override
    public int hashCode() {
        return Objects.hash(id);
    }

    // 3. Implement Comparable: Sắp xếp mặc định theo ID tăng dần
    @Override
    public int compareTo(Student other) {
        return Integer.compare(this.id, other.id);
    }

    @Override
    public String toString() {
        return "Student{id=" + id + ", name='" + name + "', gpa=" + gpa + "}";
    }
}
```

### Sử dụng Entity với các Collection

```java
import java.util.*;

public class CollectionEntityExample {
    public static void main(String[] args) {
        // Tạo một số đối tượng Student
        Student s1 = new Student(1, "An", 3.2);
        Student s2 = new Student(2, "Bình", 3.8);
        Student s3 = new Student(1, "An Nguyễn", 3.5); // Trùng ID với s1

        // ==========================================
        // 1. Thao tác trên List (Kiểm tra chứa và tìm kiếm)
        // ==========================================
        List<Student> list = new ArrayList<>();
        list.add(s1);
        list.add(s2);

        // contains() sử dụng equals() để so sánh
        boolean hasS3 = list.contains(s3); 
        System.out.println("List chứa s3 (trùng ID với s1): " + hasS3); // Output: true

        // ==========================================
        // 2. Thao tác trên Set (Loại bỏ trùng lặp nhờ hashCode & equals)
        // ==========================================
        Set<Student> hashSet = new HashSet<>();
        hashSet.add(s1);
        hashSet.add(s2);
        hashSet.add(s3); // Trùng ID với s1 -> Sẽ bị loại bỏ, không thêm vào được

        System.out.println("Kích thước HashSet (kỳ vọng là 2): " + hashSet.size()); 
        // Output: 2

        // ==========================================
        // 3. Sắp xếp tự nhiên (Comparable) và Sắp xếp tùy chỉnh (Comparator)
        // ==========================================
        List<Student> students = new ArrayList<>(Arrays.asList(s2, s1));
        
        // Sắp xếp tự nhiên theo ID (sử dụng compareTo của Student)
        Collections.sort(students);
        System.out.println("Sắp xếp theo ID tăng dần (Comparable): " + students);
        
        // Sắp xếp tùy chỉnh theo GPA giảm dần (sử dụng Comparator)
        students.sort(new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                return Double.compare(o2.getGpa(), o1.getGpa());
            }
        });
        // Hoặc viết ngắn gọn bằng Lambda: students.sort((a, b) -> Double.compare(b.getGpa(), a.getGpa()));
        System.out.println("Sắp xếp theo GPA giảm dần (Comparator): " + students);
    }
}
```

---

## 3. Lưu ý quan trọng

> [!important]
> - **Khi sử dụng đối tượng làm khóa (Key) trong Map:** Đối tượng làm Key nên là **bất biến (immutable)** (các trường dữ liệu tạo nên `hashCode` không được thay đổi giá trị sau khi thêm vào Map). Nếu một đối tượng làm Key bị thay đổi thuộc tính định danh, mã băm `hashCode()` của nó sẽ thay đổi, khiến ta không bao giờ tìm lại được value tương ứng trong Map (gây rò rỉ bộ nhớ).
