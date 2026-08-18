# Java File I/O (Đọc và ghi tệp tin)

> [!abstract] Định nghĩa
> Java cung cấp hai mô hình xử lý nhập xuất tệp tin (File I/O):
> - **Java IO (`java.io`):** Mô hình luồng dữ liệu truyền thống (Stream/Reader/Writer), xử lý tuần tự chặn luồng (blocking I/O).
> - **Java NIO.2 (`java.nio.file` từ Java 7+):** Sử dụng các lớp tiện ích hiện đại `Files` và `Path`, giúp thao tác với hệ thống tập tin dễ dàng, trực quan và hiệu quả hơn.

---

## 1. Bảng tham chiếu các phương thức File I/O phổ biến

| Thư viện | Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- | --- |
| **Path** | `Path.of(String path)` | Khai báo đường dẫn | Khởi tạo đối tượng `Path` trỏ đến tệp tin hoặc thư mục. | Khai báo | Thay thế cho `Paths.get(URI)` từ Java 11+. |
| **Files** | `Files.exists(Path p)` | Kiểm tra tồn tại | Kiểm tra xem tệp tin/thư mục tại đường dẫn `p` có tồn tại trên đĩa không. | Kiểm tra | Tránh lỗi `FileNotFoundException` khi đọc. |
| **Files** | `Files.readString(Path p)` | Đọc nhanh chuỗi văn bản | Đọc toàn bộ nội dung của tệp tin và trả về dưới dạng một chuỗi `String`. | Tệp tin nhỏ-vừa | Có thể gây tràn bộ nhớ (`OutOfMemoryError`) nếu tệp quá lớn. |
| **Files** | `Files.writeString(Path p, CharSequence charSeq)` | Ghi nhanh chuỗi | Ghi trực tiếp toàn bộ chuỗi văn bản vào tệp tin. | Tệp tin nhỏ-vừa | Mặc định sẽ ghi đè nội dung file nếu đã tồn tại. |
| **Files** | `Files.readAllLines(Path p)` | Đọc tất cả dòng | Đọc toàn bộ các dòng trong tệp tin thành danh sách `List<String>`. | Tệp tin nhỏ-vừa | Tiện lợi khi phân tích dòng văn bản đơn giản. |
| **Files** | `Files.deleteIfExists(Path p)` | Xóa an toàn | Xóa tệp tin/thư mục nếu nó tồn tại. | Xóa tài nguyên | Trả về `true` nếu xóa thành công, `false` nếu tệp không tồn tại. |
| **BufferedReader** | `readLine()` | Đọc từng dòng tối ưu | Đọc một dòng văn bản từ luồng đọc, giúp tiết kiệm bộ nhớ cho tệp lớn. | Tệp tin lớn | Trả về `null` khi đọc tới cuối tệp tin (EOF). |
| **BufferedWriter** | `write(String str)` | Ghi dữ liệu bộ đệm | Ghi chuỗi văn bản vào bộ đệm của luồng ghi. | Tệp tin lớn | Cần gọi `flush()` hoặc `close()` để đảm bảo dữ liệu ghi hẳn xuống đĩa. |

---

## 2. Ví dụ thực tế: Đọc ghi tệp tin nhỏ và tệp tin lớn

Dưới đây là mã nguồn Java hoàn chỉnh minh họa cả hai cách tiếp cận: Đọc/Ghi nhanh tệp tin nhỏ và Đọc/Ghi tối ưu bằng bộ đệm cho các tệp tin lớn.

```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;

public class FileIoOperationsDemo {
    public static void main(String[] args) {
        Path textPath = Path.of("sample_small.txt");

        // === 1. ĐỌC/GHI NHANH VỚI TỆP TIN NHỎ (Java NIO) ===
        try {
            // Ghi chuỗi văn bản nhanh
            Files.writeString(textPath, "Xin chào thế giới Java File I/O!\nDòng thứ hai.");
            System.out.println("Đã ghi file nhỏ thành công.");

            // Kiểm tra tồn tại và đọc nhanh
            if (Files.exists(textPath)) {
                String content = Files.readString(textPath);
                System.out.println("Nội dung đọc được:\n" + content);

                // Đọc thành List các dòng
                List<String> lines = Files.readAllLines(textPath);
                System.out.println("Số dòng trong file: " + lines.size());
            }
        } catch (IOException e) {
            System.err.println("Lỗi thao tác tệp nhỏ: " + e.getMessage());
        }

        // === 2. ĐỌC/GHI VỚI BỘ ĐỆM CHO TỆP LỚN (try-with-resources) ===
        String largeFileName = "large_data.log";

        // ✅ Nên làm (Do): Sử dụng try-with-resources để tự động giải phóng BufferedReader/Writer
        System.out.println("\nĐang ghi tệp lớn bằng BufferedWriter...");
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(largeFileName))) {
            for (int i = 1; i <= 5; i++) {
                writer.write("Dòng nhật ký hệ thống thứ " + i + "\n");
            }
            // Không cần gọi writer.close() thủ công vì try-with-resources sẽ tự đóng
        } catch (IOException e) {
            System.err.println("Lỗi ghi tệp lớn: " + e.getMessage());
        }

        System.out.println("Đang đọc tệp lớn bằng BufferedReader...");
        try (BufferedReader reader = new BufferedReader(new FileReader(largeFileName))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println("Dòng đọc được: " + line);
            }
        } catch (IOException e) {
            System.err.println("Lỗi đọc tệp lớn: " + e.getMessage());
        } finally {
            // Xóa tệp dọn dẹp môi trường
            try {
                Files.deleteIfExists(Path.of(largeFileName));
                Files.deleteIfExists(textPath);
            } catch (IOException ignored) {}
        }
    }
}
```

---

## 3. Lưu ý quan trọng

> [!warning]
> - **Giải phóng tài nguyên (Resource Leak):** Luôn đóng các luồng dữ liệu (Streams, Readers, Writers) sau khi dùng xong để tránh làm khóa tệp tin hoặc tiêu hao bộ nhớ hệ thống. Khuyên dùng cấu trúc **try-with-resources** để đảm bảo tài nguyên tự động đóng kể cả khi xảy ra lỗi.
> - **Tránh OutOfMemory với Files.readString():** Phương thức này tải toàn bộ nội dung tệp tin trực tiếp vào Heap Memory. Đừng bao giờ áp dụng nó cho các tệp tin có dung lượng lớn (từ hàng chục Megabytes trở lên).
