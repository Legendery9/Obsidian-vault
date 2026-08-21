[Oracle Java Documentation](https://docs.oracle.com/en/java/)

# Special Statements

> [!abstract] Định nghĩa
> **Special Statements** (câu lệnh đặc biệt) là các câu lệnh có vai trò chuyên biệt trong Java, giải quyết các bài toán đặc thù như: đồng bộ hóa đa luồng (Multi-threading), trả về giá trị trong switch thế hệ mới, thoát khỏi vòng lặp lồng nhau phức tạp, gỡ lỗi phát triển (Debugging), hoặc đơn giản hóa việc kiểm tra kiểu dữ liệu.

---

## 1. Bảng tham chiếu các Statements đặc biệt

| Statement | Definition | Tác dụng | Lưu ý |
| :--- | :--- | :--- | :--- |
| `synchronized` (block) | Khối mã đồng bộ hóa. | Khóa một đối tượng monitor lock để tại một thời điểm chỉ một luồng (thread) được chạy đoạn mã bên trong. | Giúp bảo vệ dữ liệu dùng chung (Thread-safe). Tránh lạm dụng gây thắt nút cổ chai hiệu năng hoặc gây lỗi khóa vòng (`Deadlock`). |
| `synchronized` (method) | Phương thức đồng bộ hóa. | Khóa toàn bộ phương thức, sử dụng chính instance gọi hàm (`this`) hoặc Class làm khóa giám sát. | Tương đương với việc bao bọc toàn bộ thân hàm bằng khối `synchronized(this)`. |
| `yield` | Lệnh trả về giá trị trong Switch Expression. | Trả về một giá trị cụ thể từ một khối case có nhiều dòng lệnh trong biểu thức `switch` (Java 12+). | Không sử dụng được trong Switch Statement truyền thống. Khối case kết thúc bằng `yield` không cần dùng thêm `break`. |
| `break {label}` | Lệnh break có nhãn. | Thoát ngay lập tức ra khỏi vòng lặp ngoài được chỉ định bởi nhãn `{label}` tương ứng. | Thường dùng để ngắt hoàn toàn hệ thống vòng lặp lồng nhau khi tìm thấy kết quả. |
| `continue {label}` | Lệnh continue có nhãn. | Bỏ qua phần mã còn lại và nhảy tới chu kỳ tiếp theo của vòng lặp ngoài được chỉ định nhãn tương ứng. | Giúp chuyển tiếp nhanh vòng lặp ngoài mà không cần chạy hết vòng lặp trong. |
| `assert expression;` | Lệnh khẳng định giả định (Assertion). | Kiểm tra giả thiết logic trong quá trình chạy thử. Nếu `expression` trả về `false`, JVM ném ra `AssertionError`. | Mặc định bị JVM tắt. Chỉ hoạt động khi chạy Java với cờ kích hoạt `-ea` (`-enableassertions`). |
| `obj instanceof Type var` | Kiểm tra kiểu và ép kiểu tự động (Pattern Matching - Java 16+). | Kiểm tra xem đối tượng `obj` có thuộc kiểu `Type` hay không, nếu đúng tự động gán vào biến cục bộ `var`. | Giúp loại bỏ bước ép kiểu thủ công dài dòng và loại trừ nguy cơ ném lỗi `ClassCastException`. |

---

## 2. Ví dụ thực tế

### Labeled Break và Labeled Continue

Ví dụ dưới đây minh họa cách sử dụng nhãn (Label) để điều khiển luồng của hai vòng lặp lồng nhau:

```java
public class LabeledLoopDemo {
    public void searchInMatrix(int[][] matrix, int target) {
        boolean found = false;

        // Đặt nhãn cho vòng lặp ngoài cùng
        outerLoop: 
        for (int row = 0; row < matrix.length; row++) {
            for (int col = 0; col < matrix[row].length; col++) {
                if (matrix[row][col] == target) {
                    found = true;
                    System.out.println("Tìm thấy " + target + " tại tọa độ (" + row + ", " + col + ")");
                    break outerLoop; // Thoát hoàn toàn khỏi cả 2 vòng lặp ngay lập tức
                }
            }
        }

        if (!found) {
            System.out.println("Không tìm thấy " + target);
        }
    }

    public void printCoordinatesWithoutDuplicates(int[][] matrix) {
        outer: 
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[i].length; j++) {
                if (matrix[i][j] < 0) {
                    System.out.println("Gặp số âm tại hàng " + i + ". Bỏ qua hàng này.");
                    continue outer; // Bỏ qua phần còn lại của hàng i, nhảy sang hàng i+1 tiếp theo
                }
                System.out.print("(" + i + "," + j + ") ");
            }
        }
    }
}
```

### Yield, Synchronized, Assert và Pattern Matching

```java
public class SpecialStatementsDemo {
    private int counter = 0;

    // Synchronized Method
    public synchronized void increment() {
        counter++;
    }

    public void demonstrate(Object obj) {
        // 1. Yield in Switch Expression
        int value = 3;
        String description = switch (value) {
            case 1 -> "Một";
            case 2 -> "Hai";
            default -> {
                System.out.println("Tính toán trường hợp mặc định...");
                yield "Khác"; // Trả về giá trị cho case mặc định có nhiều lệnh
            }
        };

        // 2. Instanceof Pattern Matching (Java 16+)
        if (obj instanceof String text) {
            // Tự động khai báo biến 'text' kiểu String và ép kiểu trực tiếp nếu thỏa mãn
            System.out.println("Chiều dài chuỗi: " + text.length());
        }

        // 3. Assertion
        int age = -5;
        // Kiểm tra giả định age >= 0. Nếu sai, ném AssertionError kèm mô tả lỗi.
        assert age >= 0 : "Tuổi không thể là số âm: " + age; 
    }
}
```

### Quy chuẩn lập trình (Do / Don't)

```java
// ✅ Nên làm (Do)
// Sử dụng instanceof pattern matching để tự động ép kiểu một cách sạch sẽ, ngắn gọn.
if (obj instanceof Integer number) {
    int doubled = number * 2;
}
```

```java
// ❌ Không nên làm (Don't)
// Tránh sử dụng kiểu ép kiểu truyền thống dài dòng và dễ phát sinh lỗi ClassCastException.
if (obj instanceof Integer) {
    Integer number = (Integer) obj; // Ép kiểu thủ công dư thừa
    int doubled = number * 2;
}

// Tránh sử dụng 'assert' để kiểm định tham số đầu vào của các public API/method quan trọng.
public void setSalary(double salary) {
    // SAI: assert có thể bị tắt khi chạy production, làm mất hiệu lực validate!
    assert salary > 0 : "Lương phải lớn hơn 0"; 
}
```

---

## 3. Lưu ý quan trọng

> [!warning] Cơ chế hoạt động của Assert
> Câu lệnh `assert` là công cụ dùng trong giai đoạn phát triển và kiểm thử nội bộ để phát hiện các giả định lập trình không hợp lệ. Khi triển khai hệ thống lên môi trường Production, JVM mặc định chạy không kích hoạt Assertion (bỏ qua lệnh `assert`), do đó không được dùng `assert` để thực thi logic nghiệp vụ thực tế hoặc kiểm tra lỗi bảo mật của người dùng.
