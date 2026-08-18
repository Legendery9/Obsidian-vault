# Các Nguyên tắc Lập trình Cốt lõi (Programming Principles)

---

## Định nghĩa
Các nguyên tắc lập trình là tập hợp các triết lý thiết kế và quy tắc thực hành tốt nhất (best practices) được đúc kết bởi các kỹ sư phần mềm hàng đầu thế giới, nhằm định hướng việc viết mã nguồn sạch, dễ bảo trì và dễ mở rộng.

---

## Tác dụng
- **Viết mã nguồn sạch (Clean Code):** Giúp mã nguồn dễ đọc hiểu đối với các lập trình viên khác trong nhóm.
- **Tối ưu hóa khả năng bảo trì:** Giảm chi phí thời gian sửa lỗi (debugging) khi hệ thống phát triển lớn hơn.
- **Mở rộng tính năng dễ dàng:** Hạn chế tối đa việc phá vỡ cấu trúc code cũ khi thêm các yêu cầu nghiệp vụ mới.

---

## Bảng tham chiếu

### 1. 4 Tính chất cốt lõi của Lập trình Hướng đối tượng (OOP)

| Tính chất | Ý nghĩa tóm tắt | Ví dụ ứng dụng |
| :--- | :--- | :--- |
| **Đóng gói (Encapsulation)** | Che giấu chi tiết triển khai bên trong đối tượng, chỉ lộ ra các phương thức giao tiếp công khai. | Sử dụng phạm vi truy cập `private` cho biến và cung cấp các hàm `getter`/`setter`. |
| **Kế thừa (Inheritance)** | Cho phép một lớp con tái sử dụng và mở rộng các thuộc tính, phương thức của lớp cha. | Lớp `Dog` kế thừa từ lớp `Animal`. |
| **Đa hình (Polymorphism)** | Cho phép các đối tượng khác nhau phản hồi cùng một thông điệp theo các cách khác nhau. | Ghi đè phương thức (Method Overriding) hoặc nạp chồng phương thức (Method Overloading). |
| **Trừu tượng (Abstraction)** | Tập trung vào những đặc điểm cốt lõi của đối tượng, bỏ qua những chi tiết không cần thiết. | Sử dụng `Interface` hoặc `Abstract Class` làm bộ khung thiết kế. |

### 2. Nguyên tắc SOLID (Thiết kế hướng đối tượng nâng cao)

| Chữ cái | Tên nguyên tắc | Ý nghĩa cốt lõi |
| :---: | :--- | :--- |
| **S** | Single Responsibility | Một class chỉ nên giữ **duy nhất một trách nhiệm** (chỉ có một lý do để thay đổi). |
| **O** | Open/Closed | Class nên **mở để mở rộng** (nhờ kế thừa/interface) nhưng **đóng để chỉnh sửa** trực tiếp code cũ. |
| **L** | Liskov Substitution | Lớp con phải có khả năng **thay thế hoàn toàn** lớp cha mà không làm hỏng tính đúng đắn của chương trình. |
| **I** | Interface Segregation | Nên chia nhỏ các interface lớn thành nhiều **interface nhỏ chuyên biệt**, tránh ép class implement các hàm thừa. |
| **D** | Dependency Inversion | Các module cấp cao không nên phụ thuộc vào module cấp thấp. Cả hai nên phụ thuộc vào **sự trừu tượng (abstraction/interface)**. |

### 3. Các nguyên tắc phát triển phần mềm kinh điển

| Nguyên tắc | Viết tắt của | Triết lý hành động |
| :--- | :--- | :--- |
| **DRY** | Don't Repeat Yourself | Đừng bao giờ viết lặp lại cùng một đoạn code. Hãy gom chúng thành hàm, class hoặc thư viện dùng chung. |
| **KISS** | Keep It Simple, Stupid | Giữ cho mã nguồn đơn giản nhất có thể. Tránh việc thiết kế quá phức tạp (over-engineering) cho các bài toán đơn giản. |
| **YAGNI** | You Aren't Gonna Need It | Đừng viết code cho những tính năng dự phòng mà bạn "nghĩ" là tương lai sẽ cần tới. Chỉ viết khi thực sự có yêu cầu. |

---

## Ví dụ

### So sánh Do/Don't áp dụng nguyên tắc DRY (Viết code sạch)

#### ❌ Don't (Viết lặp code)
```java
public class OrderService {
    public void createOrder() {
        System.out.println("LOG: " + LocalDateTime.now() + " - Đang tạo đơn hàng...");
        // Logic tạo đơn hàng
    }

    public void cancelOrder() {
        System.out.println("LOG: " + LocalDateTime.now() + " - Đang hủy đơn hàng...");
        // Logic hủy đơn hàng
    }
}
```

####  Do (Áp dụng DRY gom hàm log dùng chung)
```java
public class OrderService {
    private void log(String message) {
        System.out.println("LOG: " + LocalDateTime.now() + " - " + message);
    }

    public void createOrder() {
        log("Đang tạo đơn hàng...");
        // Logic tạo đơn hàng
    }

    public void cancelOrder() {
        log("Đang hủy đơn hàng...");
        // Logic hủy đơn hàng
    }
}
```

---

## Lưu ý
> [!important] Sự cân bằng khi áp dụng nguyên tắc
> Đừng cố gắng áp dụng tất cả các nguyên tắc một cách máy móc. Đôi khi việc cố tuân thủ SOLID quá mức có thể khiến cấu trúc dự án của bạn bị phân mảnh thành quá nhiều class và interface nhỏ, gây khó khăn cho việc đọc và theo dõi luồng code. Hãy luôn cân bằng giữa độ phức tạp và tính bảo trì.
