# Java Advanced Basics

> [!abstract] Định nghĩa
> Note này cung cấp kiến thức nền tảng thực tế về hai chủ đề nâng cao quan trọng trong Java Core:
> - **Java Stream API (Java 8+):** Xử lý tập hợp dữ liệu theo phong cách khai báo (declarative style).
> - **Java File I/O (`java.nio.file` và `java.io`):** Đọc và ghi tệp tin, thư mục trong hệ thống.

---

## 1. Java Stream API

Stream API cho phép xử lý dữ liệu song song hoặc tuần tự một cách ngắn gọn bằng cách chuỗi các phương thức (pipeline).

### Bảng tham chiếu các phương thức Stream API phổ biến

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `filter(Predicate<T> p)` | Lọc dữ liệu | Giữ lại các phần tử thỏa mãn điều kiện `p`. | Thao tác trung gian | Trả về một Stream mới |
| `map(Function<T, R> f)` | Ánh xạ biến đổi | Biến đổi kiểu hoặc giá trị phần tử từ `T` sang `R`. | Thao tác trung gian | Thường dùng để lấy thuộc tính |
| `sorted()` / `sorted(comp)` | Sắp xếp | Sắp xếp các phần tử của Stream (tự nhiên hoặc qua comparator). | Thao tác trung gian | Có thể ảnh hưởng hiệu năng nếu Stream lớn |
| `collect(Collector c)` | Thu thập dữ liệu | Kết xuất các phần tử Stream thành Collection (List, Set, Map). | Thao tác đầu cuối | Đóng Stream sau khi gọi |
| `forEach(Consumer<T> c)` | Duyệt phần tử | Thực thi hành động `c` trên từng phần tử. | Thao tác đầu cuối | Đóng Stream, không dùng để biến đổi |
| `count()` | Đếm phần tử | Trả về số lượng phần tử trong Stream dưới dạng `long`. | Thao tác đầu cuối | Đóng Stream |

### Ví dụ / Example

```java
import java.util.List;
import java.util.stream.Collectors;

public class StreamDemo {
    public static void main(String[] args) {
        List<String> names = List.of("An", "Bình", "Cường", "Dũng");

        // ✅ Nên làm (Do): Sử dụng Stream để xử lý dữ liệu khai báo, dễ đọc
        List<String> result = names.stream()
            .filter(name -> name.length() > 3) // Lọc: ["Bình", "Cường", "Dũng"]
            .sorted()                          // Sắp xếp: ["Bình", "Cường", "Dũng"]
            .map(String::toUpperCase)          // Ánh xạ: ["BÌNH", "CƯỜNG", "DŨNG"]
            .collect(Collectors.toList());      // Thu thập vào List

        // In số lượng phần tử
        long count = names.stream().filter(n -> n.startsWith("A")).count(); // 1
    }
}
```

---

## 2. Java File I/O (Đọc/Ghi tệp tin)

Java cung cấp nhiều cách đọc ghi file. Phương pháp hiện đại nhất là sử dụng gói `java.nio.file` kết hợp với `Files` và `Path`.

### Bảng tham chiếu các phương thức File I/O phổ biến

| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `Path.of(String path)` | Khai báo đường dẫn | Tạo đối tượng `Path` trỏ tới đường dẫn tệp tin/thư mục. | Khai báo | Thay thế cho `Paths.get()` |
| `Files.writeString(p, str)` | Ghi nhanh chuỗi | Ghi toàn bộ chuỗi `str` vào tệp tin chỉ định ở `p`. | Ghi tệp tin nhỏ | Ghi đè file nếu đã có sẵn |
| `Files.readString(p)` | Đọc nhanh chuỗi | Đọc toàn bộ nội dung tệp tin thành một chuỗi `String`. | Đọc tệp tin nhỏ | Có thể gây tràn bộ nhớ với tệp rất lớn |
| `Files.exists(p)` | Kiểm tra tồn tại | Trả về `true` nếu đường dẫn `p` tồn tại trên đĩa. | Kiểm tra | Tránh lỗi FileNotFoundError |
| `BufferedReader.readLine()` | Đọc từng dòng | Đọc một dòng văn bản từ tệp tin lớn. | Đọc tối ưu | Trả về `null` khi hết file |
| `BufferedWriter.write(str)` | Ghi dòng | Ghi chuỗi văn bản vào luồng ghi tệp tin. | Ghi tối ưu | Cần gọi `flush()` hoặc `close()` để ghi thực tế |

### Ví dụ / Example

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class FileIoDemo {
    public static void main(String[] args) {
        Path path = Path.of("example.txt");

        // 1. Files.writeString và readString
        try {
            Files.writeString(path, "Dữ liệu mẫu!");
            if (Files.exists(path)) {
                String content = Files.readString(path);
                System.out.println("Nội dung: " + content);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

        // 2. BufferedReader và BufferedWriter (Tối ưu cho tệp lớn)
        // ✅ Nên làm (Do): Sử dụng try-with-resources để tự động giải phóng tài nguyên hệ thống.
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("large.txt"))) {
            writer.write("Dòng 1\n");
            writer.write("Dòng 2\n");
        } catch (IOException e) {
            e.printStackTrace();
        }

        try (BufferedReader reader = new BufferedReader(new FileReader("large.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println("Đọc dòng: " + line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

## 3. Quản lý Hình ảnh (Images) cơ bản trong Java

### Bảng tham chiếu ImageIO
| Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- |
| `ImageIO.read(File input)` | Đọc ảnh | Đọc file ảnh và trả về đối tượng `BufferedImage`. | Đọc ảnh | Ném `IOException` nếu file lỗi |
| `ImageIO.write(im, format, out)` | Ghi ảnh | Ghi đối tượng ảnh xuống đĩa dưới định dạng chỉ định. | Ghi ảnh | Ví dụ định dạng: `"png"`, `"jpg"` |

### Ví dụ / Example

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class ImageLoader {
    public static void main(String[] args) {
        try {
            // ✅ Nên làm (Do): Đọc ảnh an toàn
            BufferedImage img = ImageIO.read(new File("input.jpg"));
            
            // Ghi ảnh sang định dạng khác
            ImageIO.write(img, "png", new File("output.png"));
        } catch (IOException e) {
            System.err.println("Lỗi xử lý ảnh: " + e.getMessage());
        }
    }
}
```

---

## Lưu ý quan trọng

> [!warning]
> - **Đóng tài nguyên:** Luôn giải phóng các luồng đọc/ghi (Streams, Reader, Writer) sau khi sử dụng để tránh lỗi chiếm dụng tài nguyên hệ thống. Hãy ưu tiên sử dụng cấu trúc **try-with-resources** (từ Java 7+).
> - **Stream không thể tái sử dụng:** Một Stream sau khi đã gọi Terminal Operation (như `collect()` hay `forEach()`) sẽ tự động đóng lại. Nếu cố tình sử dụng lại Stream đó, chương trình sẽ ném ra lỗi `IllegalStateException`.
