# Java Objects

> [!abstract] Định nghĩa
> **Object (Đối tượng)** là một thực thể cụ thể (instance) được tạo ra từ bản thiết kế [[01 - Classes|Class]], sở hữu trạng thái (properties/fields) và hành vi (methods) riêng, được cấp phát vùng nhớ độc lập trong Heap memory.

---

## 1. Khởi tạo đối tượng (Instantiation)

Để tạo một đối tượng từ một Class, ta sử dụng từ khóa `new` kết hợp với **Constructor** của lớp đó:

```java
// ✅ Nên làm (Do): Khai báo và khởi tạo đối tượng trực tiếp
Student student = new Student("An", 20);
```

### Quá trình khởi chạy khi gọi `new`:
1. **Cấp phát bộ nhớ:** JVM cấp phát một vùng nhớ đủ lớn trên **Heap memory** để chứa tất cả các thuộc tính của đối tượng.
2. **Khởi tạo giá trị mặc định:** Tất cả các thuộc tính của đối tượng được gán giá trị mặc định (`0`, `false`, `null`).
3. **Chạy Constructor:** JVM thực thi mã nguồn bên trong Constructor để gán các giá trị tùy chỉnh được truyền vào.
4. **Trả về tham chiếu:** Toán tử `new` trả về địa chỉ vùng nhớ (tham chiếu) của đối tượng vừa tạo, được gán vào biến tham chiếu (ví dụ: biến `student` nằm trên bộ nhớ Stack).

---

## 2. Quản lý đối tượng trên bộ nhớ Stack và Heap

Hiểu cách JVM phân tách bộ nhớ khi làm việc với đối tượng giúp tránh các lỗi logic về tham chiếu:

```java
Student s1 = new Student("Bình");
Student s2 = s1; // s2 trỏ cùng vùng nhớ với s1 trên Heap!
s2.setName("Cường");

System.out.println(s1.getName()); // In ra "Cường" vì cả hai biến cùng trỏ vào một đối tượng.
```

- **Stack Memory:** Lưu trữ biến tham chiếu (`s1`, `s2`). Biến tham chiếu này chỉ chứa địa chỉ của đối tượng chứ không chứa chính đối tượng đó.
- **Heap Memory:** Lưu trữ đối tượng thực tế `new Student("Bình")`.

---

## 3. Vòng đời đối tượng và thu hồi bộ nhớ (Garbage Collection)

- **Vòng đời:** Bắt đầu khi đối tượng được tạo bằng `new` và kết thúc khi đối tượng không còn được sử dụng (không còn biến tham chiếu nào trỏ tới nó).
- **Garbage Collector (GC):** Bộ dọn rác của Java chạy ngầm và tự động giải phóng các vùng nhớ Heap của các đối tượng không còn bất kỳ liên kết tham chiếu nào trỏ tới, giúp lập trình viên không phải giải phóng bộ nhớ thủ công như C/C++.

```java
Student s = new Student("Dũng");
s = null; // Đối tượng "Dũng" giờ đây không còn tham chiếu nào trỏ tới, sẽ bị GC thu hồi ở lần chạy tiếp theo.
```

---

## 4. Bảng tham chiếu các từ khóa/phương thức thường dùng

| Statement/Method | Definition | Tác dụng | Cách dùng/Phạm vi | Lưu ý |
| :--- | :--- | :--- | :--- | :--- |
| `new` | Toán tử khởi tạo đối tượng | Cấp phát bộ nhớ Heap và chạy constructor để tạo đối tượng mới. | `Student s = new Student();` | Kích hoạt constructor tương ứng. |
| `this` | Tham chiếu đối tượng hiện tại | Trỏ tới chính đối tượng đang thực thi phương thức/constructor. | `this.name = name;` hoặc `this();` | Không dùng được trong static context. |
| `instanceof` | Toán tử so sánh kiểu | Kiểm tra một đối tượng có thuộc lớp/interface cụ thể không. | `if (obj instanceof Student) {...}` | Trả về boolean. Hỗ trợ Pattern Matching từ Java 14+. |
| `equals()` | Phương thức so sánh nội dung | So sánh giá trị logic của hai đối tượng. | `s1.equals(s2)` | Mặc định so sánh tham chiếu. Cần override cho custom class. |
| `hashCode()` | Phương thức băm | Trả về mã băm (số nguyên) đại diện cho đối tượng. | `int hash = s.hashCode();` | Phải đồng bộ với `equals()` theo đúng Java Contract. |
| `toString()` | Phương thức chuyển chuỗi | Trả về biểu diễn dạng chuỗi của đối tượng. | `System.out.println(s.toString());` | Mặc định in ra `ClassName@hexHash`. Nên override. |
| `getClass()` | Phương thức lấy lớp runtime | Trả về đối tượng `Class` biểu diễn kiểu thực tế của đối tượng. | `Class<?> clazz = s.getClass();` | Thuộc Reflection API, không thể override. |
| `clone()` | Phương thức sao chép | Tạo bản sao của đối tượng (mặc định shallow copy). | `Student copy = (Student) s.clone();` | Lớp phải implement `Cloneable`, ném `CloneNotSupportedException`. |
| `finalize()` | Phương thức hủy dọn dẹp | Gọi trước khi đối tượng bị GC thu hồi để giải phóng tài nguyên. | Tự động gọi bởi GC (protected method). | **Đã deprecated từ Java 9** và bị gỡ bỏ, khuyên dùng `try-with-resources`. |
| `==` vs `equals()` | Toán tử vs Phương thức | So sánh tham chiếu địa chỉ (`==`) và so sánh giá trị logic (`equals()`). | `s1 == s2` so với `s1.equals(s2)` | String/Wrapper class luôn dùng `equals()` để so sánh giá trị. |

---

## 5. Ví dụ minh họa

Dưới đây là mã nguồn minh họa chi tiết cách sử dụng các từ khóa và phương thức trên:

```java
import java.util.Objects;

public class ObjectReferenceDemo {
    public static void main(String[] args) {
        // 1. new: Khởi tạo đối tượng
        Student s1 = new Student("An", 20);
        Student s2 = new Student("An", 20);
        Student s3 = s1; // Tham chiếu s3 trỏ cùng vùng nhớ với s1

        // 2. So sánh == vs equals()
        System.out.println("s1 == s2: " + (s1 == s2));      // false (khác vùng nhớ Heap)
        System.out.println("s1 == s3: " + (s1 == s3));      // true (cùng tham chiếu địa chỉ)
        System.out.println("s1.equals(s2): " + s1.equals(s2)); // true (cùng nội dung nhờ override equals)

        // 3. hashCode()
        System.out.println("s1.hashCode(): " + s1.hashCode());
        System.out.println("s2.hashCode(): " + s2.hashCode()); // Giống s1.hashCode() vì equals() == true

        // 4. toString()
        System.out.println("s1.toString(): " + s1); // Tự động gọi toString()

        // 5. getClass()
        System.out.println("Lớp thực tế của s1: " + s1.getClass().getName());

        // 6. instanceof
        Object obj = "Hello Java";
        if (obj instanceof String) {
            System.out.println("obj là String");
            // Java 14+ Pattern Matching:
            if (obj instanceof String str) {
                System.out.println("Chiều dài chuỗi: " + str.length());
            }
        }

        // 7. clone()
        try {
            Student s1Clone = (Student) s1.clone();
            System.out.println("Clone thành công: " + s1Clone);
            System.out.println("s1Clone == s1: " + (s1Clone == s1)); // false
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}

class Student implements Cloneable {
    private String name;
    private int age;

    public Student(String name, int age) {
        // this: Tham chiếu đối tượng hiện tại
        this.name = name;
        this.age = age;
    }

    // equals() và hashCode()
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return age == student.age && Objects.equals(name, student.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }

    // toString()
    @Override
    public String toString() {
        return "Student{name='" + name + "', age=" + age + "}";
    }

    // clone()
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    // finalize() - deprecated
    @Override
    @Deprecated(since = "9")
    protected void finalize() throws Throwable {
        try {
            System.out.println("Dọn dẹp tài nguyên đối tượng: " + name);
        } finally {
            super.finalize();
        }
    }
}
```
