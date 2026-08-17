# Spring Boot Troubleshooting Guide

> [!abstract] Định nghĩa
> Hướng dẫn này tổng hợp các lỗi lập trình phổ biến (Exceptions) khi xây dựng ứng dụng Spring Boot và định nghĩa chính xác về các mã lỗi HTTP thường gặp cùng cách xử lý thực tế.

---

## 1. Các lỗi lập trình Spring Boot thường gặp

### Lỗi 1: `No default constructor for entity`
- **Nguyên nhân:** Lớp được đánh dấu `@Entity` thiếu constructor rỗng (không tham số), khiến Hibernate không thể khởi tạo thực thể khi map dữ liệu từ Database lên Object.
- **Khắc phục:** Khai báo thêm constructor không tham số public/protected, hoặc sử dụng `@NoArgsConstructor` của Lombok.

### Lỗi 2: `Unsatisfied dependency expressed through constructor parameter`
- **Nguyên nhân:** Spring Boot Container không thể tìm thấy hoặc khởi tạo được Bean tương ứng để inject vào một class khác (thường do thiếu `@Service`, `@Repository` ở class đích, hoặc tên thuộc tính truy vấn trong Repository không giống như khai báo trong Entity).
- **Khắc phục:** 
  1. Kiểm tra xem class đích đã được đánh dấu bằng các annotation thích hợp (`@Service`, `@Repository`, `@Component`) để Spring quét thành Bean chưa.
  2. Kiểm tra lại cấu pháp các tham số/tên thuộc tính trong Query Method của Repository xem có khớp hoàn toàn với thuộc tính trong Entity không.

### Lỗi 3: `every '@Entity' class must declare or inherit at least one '@Id' or '@EmbeddedId' property`
- **Nguyên nhân:** Class `@Entity` chưa khai báo khóa chính hoặc import sai thư viện `@Id` (Ví dụ lấy nhầm `@Id` của Spring Data `org.springframework.data.annotation.Id` thay vì `@Id` của Jakarta Persistence `jakarta.persistence.Id`).
- **Khắc phục:** Đảm bảo import đúng `jakarta.persistence.Id` và đánh dấu khóa chính cho thực thể.

### Lỗi 4: `Port 8080 was already in use`
- **Nguyên nhân:** Cổng 8080 đang bị chiếm dụng bởi một tiến trình (instance) khác đang chạy ngầm của chính ứng dụng cũ hoặc của phần mềm khác.
- **Khắc phục:**
  - **Cách 1: Đổi cổng chạy trong `application.properties`:**
    ```properties
    server.port=8081
    ```
  - **Cách 2: Tìm và tắt tiến trình đang chiếm dụng cổng trên Windows:**
    1. Mở Command Prompt (cmd) bằng quyền Admin và gõ lệnh để tìm PID (Process ID):
       ```cmd
       netstat -ano | findstr :8080
       ```
    2. Tắt tiến trình chiếm dụng bằng PID tìm thấy:
       ```cmd
       taskkill /PID <MÃ_PID> /F
       ```

---

## 2. Giải nghĩa mã lỗi HTTP tiêu chuẩn

> [!warning] Lưu ý phân biệt mã lỗi
> Hãy đảm bảo phân biệt rõ ràng giữa lỗi do Client gửi sai định dạng (400) và lỗi do Server không tìm thấy tài nguyên (404):

### 1. HTTP 400 - Bad Request
- **Ý nghĩa:** Server không thể hiểu hoặc xử lý yêu cầu do lỗi cú pháp từ phía Client.
- **Lý do phổ biến:** Truyền tham số thiếu, sai định dạng kiểu dữ liệu (ví dụ truyền chuỗi `"abc"` vào biến số nguyên `age`), hoặc dữ liệu JSON gửi lên bị sai cú pháp.

### 2. HTTP 404 - Not Found
- **Ý nghĩa:** Server không tìm thấy tài nguyên/đường dẫn được yêu cầu từ Client.
- **Lý do phổ biến:** Sai đường dẫn URL, hoặc không tìm thấy các file tĩnh (CSS, JS, Hình ảnh) tại vị trí chỉ định.

### 3. HTTP 500 - Internal Server Error
- **Ý nghĩa:** Lỗi xử lý bên trong Server khi thực thi mã nguồn.
- **Lý do phổ biến:** Xảy ra lỗi ngoại lệ chưa được xử lý trong Java (ví dụ `NullPointerException`, lỗi kết nối database, lỗi truy vấn SQL sai cú pháp).

### 4. HTTP 429 - Too Many Requests
- **Ý nghĩa:** Client đã gửi quá nhiều yêu cầu trong một khoảng thời gian ngắn, vượt ngưỡng giới hạn tần suất (Rate Limit) cho phép của server.
- **Lý do phổ biến:** Tần suất click double của người dùng, hoặc các cuộc tấn công spam API/DDoS.
