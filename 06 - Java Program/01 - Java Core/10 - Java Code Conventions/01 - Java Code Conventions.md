# Java Code Conventions

> [!abstract] Định nghĩa
> **Quy ước viết mã (Code Conventions)** là tập hợp các hướng dẫn định dạng, quy tắc đặt tên và thực hành lập trình tốt giúp mã nguồn Java thống nhất, sạch sẽ, chuyên nghiệp và dễ bảo trì. Tài liệu này tuân thủ chuẩn quy ước truyền thống của Sun Microsystems / Oracle.

---

## 1. Quy tắc đặt tên (Naming Conventions)

| Thành phần | Quy tắc viết | Ví dụ | Ghi chú |
| --- | --- | --- | --- |
| **Class / Interface** | PascalCase | `Student`, `UserRepository` | Danh từ hoặc cụm danh từ. |
| **Method** | camelCase | `calculateSalary()`, `save()` | Động từ hoặc cụm động từ. |
| **Variable / Parameter** | camelCase | `totalAmount`, `age` | Ngắn gọn, có ý nghĩa, tránh viết tắt bừa bãi. |
| **Constant (Hằng số)** | UPPER_SNAKE_CASE | `MAX_COUNT`, `DEFAULT_PORT` | Viết hoa toàn bộ, cách nhau bằng `_`. |
| **Package** | Viết thường toàn bộ | `com.company.service` | Nên dùng tên miền ngược của tổ chức làm tiền tố. |

```java
// ✅ Nên làm (Do): Đặt tên đúng chuẩn, phản ánh rõ mục đích.
public class PaymentService {
    public static final int MAX_RETRY = 3;
    private double currentBalance;

    public void processPayment(double amount) {
        // ...
    }
}
```

---

## 2. Tổ chức tệp nguồn (File Organization)
Mỗi file nguồn Java nên có cấu trúc tuần tự rõ ràng từ trên xuống dưới như sau:
1. **Khai báo Package** (`package com.example;`)
2. **Các dòng Import** (Nhóm có thứ tự: thư viện Java standard trước, sau đó tới thư viện bên thứ ba và nội bộ).
3. **Khai báo Class chính** (Public class).
4. **Các biến thuộc lớp (Class fields):**
   - Biến static public
   - Biến static protected
   - Biến static default/private
   - Biến instance public/protected/private
5. **Các Constructors**
6. **Các Phương thức (Methods):** Sắp xếp theo nhóm chức năng hoặc mức độ liên quan, thay vì sắp xếp theo bảng chữ cái.

---

## 3. Thụt lề và Khoảng trắng (Indentation & Whitespace)
- **Thụt lề:** Sử dụng đúng **4 khoảng trắng (spaces)** cho mỗi cấp độ thụt lề. Tránh dùng tab để đảm bảo giao diện hiển thị đồng nhất trên mọi trình soạn thảo.
- **Độ dài dòng:** Giới hạn tối đa **80 ký tự** trên một dòng đối với mã nguồn thông thường và **70 ký tự** đối với tài liệu (JavaDoc). Nếu dòng quá dài, thực hiện ngắt dòng sau dấu phẩy hoặc trước toán tử.
- **Khoảng trắng:**
  - Có khoảng trắng giữa từ khóa điều khiển và dấu mở ngoặc: `if (condition)` chứ không viết `if(condition)`.
  - Có khoảng trắng trước và sau các toán tử nhị phân: `a = b + c;`.

```java
// ✅ Nên làm (Do): Định dạng khoảng trắng chuẩn và thụt lề 4 space rõ ràng.
if (score >= 50) {
    System.out.println("Passed with score: " + score);
} else {
    System.out.println("Failed");
}
```

---

## 4. Thực hành lập trình tốt (Best Practices)
- **Tránh biến toàn cục:** Luôn khai báo biến cục bộ ở phạm vi nhỏ nhất gần nơi sử dụng đầu tiên.
- **Tránh ép kiểu ngầm định phức tạp:** Hãy viết tường minh các phép toán để tránh nhầm lẫn về kiểu dữ liệu.
- **Tránh nhầm lẫn về thứ tự ưu tiên của toán tử:** Nếu một câu điều kiện chứa từ hai toán tử so sánh trở lên, hãy sử dụng `()` để nhóm từng biểu thức so sánh.
- **Xử lý Exception:** Không bao giờ nuốt các Exception mà không ghi log hay xử lý (Empty catch block).

```java
// ❌ Không nên làm (Don't): Bỏ trống khối catch làm mất thông tin lỗi hệ thống.
try {
    readFile();
} catch (IOException e) {
    // Không làm gì cả - RẤT NGUY HIỂM!
}

// ✅ Nên làm (Do): Ghi log lỗi hoặc ném ra runtime exception tương ứng.
try {
    readFile();
} catch (IOException e) {
    logger.error("Lỗi đọc file cấu hình", e);
    throw new RuntimeException("Lỗi hệ thống không thể khởi chạy", e);
}
```

---

## 5. Sử dụng chú thích mã nguồn (comments)
- **Ngôn ngữ:** tiếng việt.
- **Tại các vị trí:**
	- Trước `header` của tất cả các `class` (Trừ `constructor`, `getter` và `setter`), luôn chú thích: 
		- Tên class: `{Class Name}`.
		- Phiên bản:  `{Phiên bản Java}`
		- Date tạo class: ` Date of code` 
		- Latest: `{Latest Date}`.
		- Bản quyền: `{Tên người dùng}`.
		- mã sinh viên: `{HE\d{6}$}`.
		- Mục đích: `{Mục đích file}`.
	- Statement gọi `hàm`.
	- Statement có `điều kiện rẽ nhánh`
- **Sử dụng các ký tự đặc biệt:**

| Marker   | Ý nghĩa               | Code::Blocks    |
| -------- | --------------------- | --------------- |
| TODO     | Việc cần làm          | ✅               |
| FIXME    | Cần sửa lỗi           | ✅               |
| XXX      | Đáng nghi/cần xem lại | ✅               |
| NOTE     | Ghi chú               | ⚠️ tùy cấu hình |
| HACK     | Code workaround       | ⚠️ tùy cấu hình |
| BUG      | Lỗi đã biết           | ⚠️ tùy cấu hình |
| WARNING  | Cảnh báo              | ⚠️ tùy cấu hình |
| OPTIMIZE | Cần tối ưu            | ⚠️ tùy cấu hình |
