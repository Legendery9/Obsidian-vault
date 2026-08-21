[Oracle Java Documentation](https://docs.oracle.com/en/java/)

# Declaration Statements

> [!abstract] Định nghĩa
> **Declaration Statements** (câu lệnh khai báo) là các câu lệnh dùng để thiết lập sự tồn tại của một biến, hằng số, mảng, hoặc đối tượng trong chương trình Java. Nó thông báo cho JVM biết kiểu dữ liệu, tên định danh, và phạm vi sử dụng của đối tượng đó để cấp phát bộ nhớ phù hợp.

---

## 1. Bảng tham chiếu các Statements tạo & khai báo

| Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| :--- | :--- | :--- | :--- | :--- |
| `type name;` | Khai báo biến không khởi tạo giá trị. | Dành vùng nhớ cho biến với kiểu dữ liệu `type`. | Biến cục bộ (local variable) hoặc thuộc tính lớp (field). | Local variable bắt buộc phải gán giá trị trước khi đọc, nếu không sẽ bị lỗi biên dịch. Field nhận giá trị mặc định (`0`, `false`, `null`). |
| `type name = value;` | Khai báo và khởi tạo giá trị ban đầu. | Thiết lập giá trị ngay khi tạo biến để sử dụng an toàn. | Biến cục bộ, thuộc tính lớp, hằng số. | Giá trị `value` phải tương thích với kiểu dữ liệu `type`. |
| `final type name = value;` | Khai báo hằng số (hằng tham chiếu hoặc giá trị). | Ngăn cấm thay đổi giá trị hoặc địa chỉ tham chiếu sau khi đã gán lần đầu. | Biến cục bộ, thuộc tính lớp, tham số phương thức (`final parameter`). | Với đối tượng, `final` chỉ giữ cố định địa chỉ tham chiếu (reference), trạng thái bên trong đối tượng vẫn có thể chỉnh sửa được. |
| `type[] name;` | Khai báo biến kiểu mảng. | Chuẩn bị vùng chứa để lưu trữ danh sách các phần tử có cùng kiểu dữ liệu. | Mọi phạm vi khai báo biến. | Cú pháp `type[] name` được khuyến khích hơn `type name[]` vì thể hiện rõ kiểu dữ liệu của biến là mảng. |
| `new ClassName(...)` | Khởi tạo đối tượng (Instance creation). | Cấp phát bộ nhớ Heap cho đối tượng mới và chạy hàm dựng (Constructor). | Tạo đối tượng mới để gán cho biến tham chiếu hoặc truyền làm tham số. | Trả về tham chiếu đến đối tượng trong bộ nhớ Heap. |
| `type v1 = w1, v2 = w2;` | Khai báo nhiều biến cùng kiểu trên một dòng. | Khai báo nhanh nhiều biến có chung kiểu dữ liệu, giúp code ngắn gọn. | Thường dùng cho biến cục bộ (ví dụ: tọa độ `int x = 0, y = 0;`). | Tránh dùng khi các biến không liên quan trực tiếp, vì sẽ làm code khó đọc và khó viết comment giải thích. |
| `var name = value;` | Suy luận kiểu dữ liệu cục bộ (Local Variable Type Inference - Java 10+). | Tự động xác định kiểu dữ liệu thực tế dựa trên giá trị khởi tạo `value`. | Chỉ dùng cho biến cục bộ được khởi tạo giá trị ngay tại dòng khai báo. | Không thể dùng cho: thuộc tính lớp (fields), tham số phương thức, kiểu trả về, gán giá trị `null` trực tiếp, hoặc khai báo không khởi tạo. |

---

## 2. Ví dụ thực tế

Dưới đây là mã nguồn minh họa các cách khai báo biến và đối tượng trong Java:

```java
import java.util.ArrayList;
import java.util.List;

public class DeclarationDemo {
    // Thuộc tính lớp (Fields) - Tự động nhận giá trị mặc định
    private int defaultInt;       // = 0
    private String defaultRef;    // = null

    public void demonstrate() {
        // 1. Khai báo tiêu chuẩn và hằng số
        int count;
        count = 10; // Gán giá trị sau
        
        final double PI = 3.14159; // Hằng số primitive
        final List<String> names = new ArrayList<>(); // Hằng số tham chiếu
        names.add("An"); // ✅ Hoạt động bình thường (thay đổi trạng thái bên trong)
        // names = new ArrayList<>(); // ❌ LỖI BIÊN DỊCH: Không thể gán lại tham chiếu mới

        // 2. Khai báo mảng
        int[] numbers = new int[5]; // Khởi tạo mảng có 5 phần tử (mặc định = 0)
        
        // 3. Sử dụng var (Java 10+)
        var message = "Hello World"; // Trình biên dịch tự hiểu là String
        var list = new ArrayList<Integer>(); // Rút gọn kiểu Generic dài dòng
    }
}
```

### Quy chuẩn lập trình (Do / Don't)

```java
// ✅ Nên làm (Do)
// Khai báo mảng với dấu ngoặc vuông đặt ngay sau kiểu dữ liệu để thể hiện rõ kiểu mảng.
int[] scores = new int[10];

// Khai báo biến cục bộ nào thì khởi tạo luôn biến đó hoặc đặt gần nơi sử dụng nhất.
int totalUserCount = 0;
```

```java
// ❌ Không nên làm (Don't)
// Tránh đặt dấu ngoặc vuông sau tên biến theo phong cách C/C++ cũ.
int scores[] = new int[10];

// Tránh khai báo nhiều biến không liên quan hoặc kiểu dữ liệu phức tạp trên cùng một dòng.
double salary = 1000.0, taxRate = 0.1, netPay; 
```

---

## 3. Lưu ý quan trọng

> [!warning] Giới hạn và ngoại lệ của `var`
> Từ khóa `var` không phải là một kiểu dữ liệu động (như `var` trong JavaScript hay `dynamic` trong C#). Java vẫn là ngôn ngữ định kiểu tĩnh (strongly typed). Trình biên dịch chỉ thay thế `var` bằng kiểu dữ liệu thực tế tại thời điểm biên dịch.
> - **Don't:** Không dùng `var` khi kiểu dữ liệu bên phải không tường minh hoặc làm code khó hiểu.
>   `var data = service.getData(); // Khó đoán data thuộc kiểu gì`
> - **Do:** Dùng `var` khi vế phải đã thể hiện rõ kiểu dữ liệu.
>   `var customer = new Customer(); // Tường minh và sạch code`
