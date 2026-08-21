[Oracle Java Documentation](https://docs.oracle.com/en/java/)

# Conditions and Loops

> [!abstract] Định nghĩa
> **Conditions and Loops** (cấu trúc điều kiện và vòng lặp) là các câu lệnh kiểm soát luồng thực thi (Control Flow) của chương trình Java. Chúng cho phép chương trình đưa ra quyết định rẽ nhánh dựa trên điều kiện logic, hoặc lặp lại một khối lệnh nhiều lần dựa trên trạng thái của dữ liệu.

---

## 1. Cấu trúc rẽ nhánh (Conditions & Branching)

Cấu trúc rẽ nhánh cho phép chương trình thực thi các khối mã khác nhau dựa trên kết quả của biểu thức điều kiện (phải trả về kiểu `boolean`).

### Bảng tham chiếu cấu trúc rẽ nhánh

| Statement / Operator | Definition | Tác dụng | Lưu ý |
| :--- | :--- | :--- | :--- |
| `if` | Câu lệnh điều kiện cơ bản. | Thực thi khối mã lệnh bên trong nếu biểu thức điều kiện trả về `true`. | Biểu thức điều kiện bắt buộc phải là kiểu `boolean`. |
| `else if` | Nhánh điều kiện bổ sung. | Kiểm tra điều kiện phụ tiếp theo nếu tất cả các điều kiện trước đó trả về `false`. | Có thể khai báo nhiều `else if` liên tiếp trong một cấu trúc điều kiện. |
| `else` | Nhánh mặc định cuối cùng. | Thực thi khối mã lệnh khi tất cả các điều kiện `if` và `else if` trước đó đều `false`. | Luôn đứng cuối cấu trúc điều kiện và không đi kèm biểu thức điều kiện. |
| `switch` (Statement) | Cấu trúc lựa chọn truyền thống. | So khớp giá trị biểu thức với các nhãn `case` để nhảy trực tiếp tới khối mã thực thi tương ứng. | Cần câu lệnh `break` để thoát khỏi switch, tránh trôi code (fall-through). Hỗ trợ byte, short, char, int, String, Enum và các Wrapper classes. |
| `switch` (Expression) | Biểu thức switch (Java 14+). | Sử dụng toán tử `->` để trả về trực tiếp giá trị từ các nhánh lựa chọn mà không cần dùng `break`. | Tránh lỗi fall-through mặc định. Bắt buộc phải bao quát toàn bộ trường hợp (`exhaustive`), thường cần nhánh `default`. |
| `?:` | Toán tử ba ngôi. | Trả về giá trị 1 nếu điều kiện đúng, ngược lại trả về giá trị 2. Thay thế ngắn gọn cho `if-else`. | Cú pháp: `biểu_thức_boolean ? giá_trị_1 : giá_trị_2;`. Tránh lồng nhau quá nhiều lớp vì sẽ gây khó đọc. |

### Ví dụ minh họa rẽ nhánh

```java
public class BranchingDemo {
    public void checkScore(int score) {
        // 1. Cấu trúc if-else-if
        if (score >= 90) {
            System.out.println("Xuất sắc");
        } else if (score >= 70) {
            System.out.println("Khá");
        } else {
            System.out.println("Trung bình / Yếu");
        }

        // 2. Toán tử ba ngôi
        String result = (score >= 50) ? "Đỗ" : "Trượt";
        System.out.println("Kết quả: " + result);
    }

    public void printDayOfWeek(int day) {
        // 3. Switch Expression (Java 14+) - Khuyên dùng vì cú pháp gọn gàng và an toàn
        String dayName = switch (day) {
            case 1 -> "Thứ Hai";
            case 2 -> "Thứ Ba";
            case 3 -> "Thứ Tư";
            case 4 -> "Thứ Năm";
            case 5 -> "Thứ Sáu";
            case 6, 7 -> "Cuối Tuần";
            default -> throw new IllegalArgumentException("Ngày không hợp lệ: " + day);
        };
        System.out.println("Hôm nay là: " + dayName);
    }
}
```

---

## 2. Cấu trúc vòng lặp (Loops)

Vòng lặp cho phép lặp lại một khối mã lệnh cho đến khi điều kiện kiểm tra không còn thỏa mãn.

### Bảng tham chiếu các cấu trúc vòng lặp

| Statement | Definition | Tác dụng | Lưu ý |
| :--- | :--- | :--- | :--- |
| `for` | Vòng lặp đếm số lần biết trước. | Tích hợp khởi tạo biến lặp, điều kiện kiểm tra, và bước tăng/giảm trên cùng một dòng. | Thích hợp nhất khi biết trước chính xác số lần lặp. |
| `for-each` | Vòng lặp nâng cao (Enhanced for). | Duyệt tuần tự từ đầu đến cuối các phần tử của mảng hoặc một Collection (triển khai `Iterable`). | Không thể lấy chỉ số index hiện tại hoặc thay đổi cấu trúc Collection (thêm/xóa phần tử) khi đang lặp. |
| `while` | Vòng lặp kiểm tra trước. | Lặp lại khối lệnh liên tục khi điều kiện kiểm tra vẫn còn trả về `true`. | Khối lệnh có thể không chạy lần nào nếu điều kiện ban đầu bị sai (`false`). |
| `do-while` | Vòng lặp kiểm tra sau. | Thực thi khối lệnh trước một lần, sau đó mới kiểm tra điều kiện để quyết định lặp tiếp. | Đảm bảo khối lệnh luôn được thực thi ít nhất một lần. |

### Ví dụ minh họa vòng lặp

```java
import java.util.List;

public class LoopDemo {
    public void demonstrate() {
        // 1. Vòng lặp for cơ bản
        for (int i = 0; i < 5; i++) {
            System.out.print(i + " "); // In ra: 0 1 2 3 4
        }
        System.out.println();

        // 2. Vòng lặp for-each (Enhanced for loop)
        List<String> items = List.of("A", "B", "C");
        for (String item : items) {
            System.out.print(item + " "); // In ra: A B C
        }
        System.out.println();

        // 3. Vòng lặp while
        int count = 0;
        while (count < 3) {
            System.out.print(count + " "); // In ra: 0 1 2
            count++;
        }
        System.out.println();

        // 4. Vòng lặp do-while
        int num = 10;
        do {
            System.out.println("Chạy ít nhất một lần ngay cả khi num = " + num);
        } while (num < 5);
    }
}
```

---

## 3. Điều khiển vòng lặp (Loop Control)

Các câu lệnh này can thiệp và làm thay đổi luồng thực thi thông thường của vòng lặp.

### Bảng tham chiếu các lệnh điều khiển

| Statement | Tác dụng | Phạm vi tác động | Lưu ý |
| :--- | :--- | :--- | :--- |
| `break` | Thoát khỏi vòng lặp hoặc khối lệnh `switch` chứa nó ngay lập tức. | Vòng lặp hoặc switch ở cấp hiện tại gần nhất. | Bỏ qua mọi lệnh phía sau và kết thúc chu kỳ lặp hoàn toàn. |
| `continue` | Bỏ qua phần mã lệnh còn lại của chu kỳ lặp hiện tại để chuyển sang chu kỳ tiếp theo. | Vòng lặp ở cấp hiện tại gần nhất. | Với vòng lặp `for`, điều hướng trực tiếp tới bước cập nhật biến lặp. Với `while`, điều hướng trực tiếp tới bước kiểm tra điều kiện. |

### Ví dụ minh họa điều khiển vòng lặp

```java
public class LoopControlDemo {
    public void demonstrate() {
        // Sử dụng break
        for (int i = 1; i <= 10; i++) {
            if (i == 5) {
                break; // Thoát vòng lặp ngay khi i = 5
            }
            System.out.print(i + " "); // In ra: 1 2 3 4
        }
        System.out.println();

        // Sử dụng continue
        for (int i = 1; i <= 5; i++) {
            if (i == 3) {
                continue; // Bỏ qua in giá trị 3, chuyển sang i = 4
            }
            System.out.print(i + " "); // In ra: 1 2 4 5
        }
        System.out.println();
    }
}
```

### Quy chuẩn lập trình (Do / Don't)

```java
// ✅ Nên làm (Do)
// Sử dụng switch expression mới thay thế switch truyền thống để tránh trôi code (fall-through) ngoài ý muốn.
String grade = switch (score) {
    case 10 -> "A+";
    case 9 -> "A";
    default -> "B/C/D";
};
```

```java
// ❌ Không nên làm (Don't)
// Tránh lạm dụng switch truyền thống mà quên viết break ở mỗi case, trừ khi cố ý tạo logic fall-through.
switch (status) {
    case 1:
        System.out.println("Bắt đầu");
        // Lỗi: Quên break làm code trôi xuống case tiếp theo
    case 2:
        System.out.println("Đang xử lý");
}
```
