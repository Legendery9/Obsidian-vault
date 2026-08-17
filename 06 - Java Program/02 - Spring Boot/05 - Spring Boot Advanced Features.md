# Spring Boot Advanced Features

> [!abstract] Định nghĩa
> Note này cung cấp hướng dẫn thực tế về các tính năng bất đồng bộ, lập lịch, xử lý giao dịch cơ sở dữ liệu, quản lý vòng đời Bean nâng cao, và tích hợp gửi Email tự động trong Spring Boot.

---

## 1. Lập lịch tự động (Scheduling)

Kích hoạt bằng cách khai báo `@EnableScheduling` tại cấu hình lớp chính, sau đó đánh dấu các hàm chạy tự động bằng `@Scheduled`.

- **`fixedRate`:** Khoảng thời gian định kỳ tính từ lúc bắt đầu tác vụ cũ đến khi bắt đầu tác vụ tiếp theo (Có thể chồng chéo).
- **`fixedDelay`:** Khoảng thời gian định kỳ tính từ khi tác vụ cũ kết thúc hoàn toàn đến khi bắt đầu tác vụ tiếp theo (Không chồng chéo).
- **`cron`:** Biểu thức cron biểu diễn lịch chạy cụ thể.

> [!warning] Quy tắc viết hàm Scheduled
> Phương thức được đánh dấu `@Scheduled` bắt buộc phải có kiểu trả về là **`void`** và **không nhận bất kỳ tham số đầu vào nào**.
> ```java
> @Component
> public class BackupJob {
>     // Chạy vào 0 giờ sáng mỗi ngày
>     @Scheduled(cron = "0 0 0 * * *")
>     public void runBackup() {
>         System.out.println("Running database backup...");
>     }
> }
> ```

---

## 2. Bất đồng bộ (Async) & Sự kiện (Events)

### Chạy bất đồng bộ `@Async`
Cho phép đẩy tác vụ tốn thời gian chạy trên một Thread pool riêng biệt để trả kết quả về cho Client ngay lập tức. Cần cấu hình `@EnableAsync` ở lớp chạy chính.

```java
@Service
public class ReportService {
    @Async
    public void exportLargeExcel() {
        // Tác vụ nặng chạy ngầm dưới nền...
    }
}
```

### Sử dụng Spring Event Bus để tách biệt Module (Decoupling)
Spring hỗ trợ mô hình Observer Pattern cho phép phát đi thông điệp và lắng nghe sự kiện:

```java
// 1. Định nghĩa sự kiện
public class UserRegisteredEvent {
    private final String username;
    public UserRegisteredEvent(String username) { this.username = username; }
    public String getUsername() { return username; }
}

// 2. Publish sự kiện
@Autowired
private ApplicationEventPublisher publisher;

public void registerUser(String name) {
    publisher.publishEvent(new UserRegisteredEvent(name));
}

// 3. Lắng nghe sự kiện (Có thể kết hợp chạy nền bất đồng bộ)
@Component
public class NotificationListener {
    @Async
    @EventListener
    public void handleRegistration(UserRegisteredEvent event) {
        System.out.println("Gửi email chào mừng thành viên: " + event.getUsername());
    }
}
```

---

## 3. Quản lý giao dịch cơ sở dữ liệu (`@Transactional`)

Được khai báo ở tầng Service để đảm bảo tính nguyên tử (ACID) của giao dịch. Toàn bộ các thao tác dữ liệu bên trong phương thức thành công thì hệ thống thực hiện **COMMIT**, nếu xảy ra bất kỳ lỗi Runtime Exception nào hệ thống tự động **ROLLBACK** lại toàn bộ trạng thái trước giao dịch.

```java
@Service
public class BankService {
    @Transactional
    public void transferMoney(Long fromId, Long toId, double amount) {
        accountRepository.withdraw(fromId, amount);
        accountRepository.deposit(toId, amount); // Nếu hàm này lỗi, withdraw trước đó tự rollback.
    }
}
```

---

## 4. Quản lý Beans nâng cao

- **`@Primary`:** Chỉ định Bean được ưu tiên cao nhất khi tiêm (inject) nếu có nhiều Bean cùng triển khai một Interface.
- **`@Lazy`:** Chỉ khởi tạo Bean khi thực sự có lời gọi sử dụng nó lần đầu, giúp tăng tốc độ khởi động ứng dụng.
- **`@Profile`:** Chỉ tải Bean khi ứng dụng chạy ở môi trường tương ứng (ví dụ: `@Profile("dev")` vs `@Profile("prod")`).
- **`@ControllerAdvice`:** Lớp xử lý trung tâm, dùng để khai báo bộ bắt lỗi toàn cục bằng `@ExceptionHandler` hoặc khai báo các thuộc tính chung cho toàn bộ controller.

---

## 5. Tự động hóa gửi Email (`JavaMailSender`)

Để gửi email, ta thêm dependency `spring-boot-starter-mail` và cấu hình hòm thư trong `application.properties`:

```properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=your_gmail@gmail.com
spring.mail.password=your_app_password
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```

> [!important] Cảnh báo về bảo mật Gmail
> Không sử dụng mật khẩu đăng nhập Gmail thông thường. Bạn bắt buộc phải bật xác thực 2 bước (2FA) trên tài khoản Google và tạo **Google App Password (Mật khẩu ứng dụng)** để điền vào phần `spring.mail.password`.

### Gửi Email HTML nâng cao với file đính kèm

```java
import jakarta.mail.internet.MimeMessage;
import org.springframework.mail.javamail.JavaMailSender;
import org.springframework.mail.javamail.MimeMessageHelper;
import java.io.File;

@Service
public class EmailService {
    @Autowired
    private JavaMailSender mailSender;

    public void sendEmailWithAttachment(String to, String subject, String htmlContent, File file) {
        try {
            MimeMessage message = mailSender.createMimeMessage();
            MimeMessageHelper helper = new MimeMessageHelper(message, true, "UTF-8");

            helper.setTo(to);
            helper.setSubject(subject);
            helper.setText(htmlContent, true); // true chỉ định nội dung là HTML
            helper.addAttachment(file.getName(), file);

            mailSender.send(message);
        } catch (Exception e) {
            throw new RuntimeException("Lỗi gửi email: ", e);
        }
    }
}
```
