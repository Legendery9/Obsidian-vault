# Java Basic Image Management (Quản lý Hình ảnh cơ bản)

> [!abstract] Định nghĩa
> Java hỗ trợ xử lý hình ảnh cơ bản thông qua gói **`javax.imageio`** (chủ yếu là lớp `ImageIO`) và **`java.awt.image.BufferedImage`**. Lớp này cho phép lập trình viên dễ dàng đọc, ghi, chuyển đổi định dạng và thực hiện các thao tác xử lý điểm ảnh (pixel) đơn giản mà không cần thư viện bên ngoài.

---

## 1. Bảng tham chiếu các phương thức xử lý hình ảnh phổ biến

| Lớp | Method / Statement | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
| --- | --- | --- | --- | --- | --- |
| **ImageIO** | `ImageIO.read(File input)` | Đọc ảnh từ tệp | Tải ảnh từ đường dẫn tệp tin và trả về một đối tượng `BufferedImage`. | Đọc ảnh | Ném `IOException` nếu tệp lỗi hoặc không tìm thấy. |
| **ImageIO** | `ImageIO.read(URL input)` | Đọc ảnh từ URL | Tải ảnh từ một địa chỉ web trực tuyến. | Đọc ảnh | Cần xử lý kết nối mạng và lỗi IO. |
| **ImageIO** | `ImageIO.write(RenderedImage im, String format, File output)` | Ghi ảnh xuống đĩa | Lưu đối tượng ảnh xuống đĩa theo định dạng chỉ định (ví dụ: `"png"`, `"jpg"`). | Ghi ảnh | Định dạng viết thường (không phân biệt hoa thường). |
| **BufferedImage** | `getWidth()` | Lấy chiều rộng | Trả về số lượng điểm ảnh theo chiều ngang. | Truy xuất thuộc tính | Trả về kiểu dữ liệu `int`. |
| **BufferedImage** | `getHeight()` | Lấy chiều cao | Trả về số lượng điểm ảnh theo chiều dọc. | Truy xuất thuộc tính | Trả về kiểu dữ liệu `int`. |
| **BufferedImage** | `getRGB(int x, int y)` | Lấy màu sắc điểm ảnh | Trả về mã màu dạng ARGB (Alpha-Red-Green-Blue) tại tọa độ `(x, y)`. | Xử lý điểm ảnh | Tọa độ tính từ `0` đến `width-1`/`height-1`. |
| **BufferedImage** | `setRGB(int x, int y, int rgb)` | Thay đổi màu điểm ảnh | Gán mã màu ARGB mới cho điểm ảnh tại tọa độ `(x, y)`. | Xử lý điểm ảnh | Thay đổi trực tiếp trên đối tượng BufferedImage hiện tại. |

---

## 2. Ví dụ thực tế: Đọc, ghi và biến đổi điểm ảnh đơn giản

Dưới đây là chương trình Java hoàn chỉnh minh họa việc đọc một tệp ảnh, lấy kích thước, đổi màu một pixel và ghi đè sang định dạng khác.

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;
import java.net.URL;

public class ImageProcessorDemo {
    public static void main(String[] args) {
        try {
            // 1. Đọc ảnh từ file hệ thống
            File inputFile = new File("input.jpg");
            if (!inputFile.exists()) {
                System.out.println("Tệp input.jpg không tồn tại. Đang tải ảnh mẫu từ URL...");
                // Đọc ảnh dự phòng từ URL
                URL imageUrl = new URL("https://images.unsplash.com/photo-1579546929518-9e396f3cc809");
                BufferedImage webImg = ImageIO.read(imageUrl);
                ImageIO.write(webImg, "jpg", inputFile);
            }

            BufferedImage image = ImageIO.read(inputFile);

            // 2. Lấy thông tin cơ bản của bức ảnh
            int width = image.getWidth();
            int height = image.getHeight();
            System.out.printf("Ảnh gốc: %d x %d pixels\n", width, height);

            // 3. Xử lý điểm ảnh đơn giản (Ví dụ: Vẽ một điểm màu đỏ tại góc 10x10)
            // Màu đỏ dạng ARGB: Alpha=255 (FF), Red=255 (FF), Green=0 (00), Blue=0 (00)
            int redColor = (255 << 24) | (255 << 16) | (0 << 8) | 0; 
            image.setRGB(10, 10, redColor);

            // 4. Ghi ảnh sang định dạng PNG
            File outputFile = new File("output.png");
            // ✅ Nên làm (Do): Chọn đúng định dạng viết để nén tối ưu (PNG là lossless)
            boolean success = ImageIO.write(image, "png", outputFile);
            if (success) {
                System.out.println("Đã ghi ảnh mới thành công tại: " + outputFile.getAbsolutePath());
            } else {
                System.err.println("Không tìm thấy bộ ghi (writer) phù hợp cho định dạng PNG!");
            }

        } catch (IOException e) {
            // ❌ Tránh (Don't): Bỏ qua ngoại lệ hoặc chỉ printStackTrace mà không có log rõ ràng
            System.err.println("Lỗi trong quá trình xử lý hình ảnh: " + e.getMessage());
        }
    }
}
```

---

## 3. Lưu ý quan trọng

> [!warning]
> - **Chất lượng nén hình ảnh:** Khi ghi ảnh JPEG (`ImageIO.write`), chất lượng nén mặc định có thể làm giảm độ sắc nét của ảnh. Nếu cần độ chính xác cao hoặc giữ độ trong suốt (transparency), hãy dùng định dạng **PNG**.
> - **Giải phóng tài nguyên hệ thống:** Khi làm việc với nhiều ảnh dung lượng lớn, hãy giải phóng tài nguyên đồ họa nếu có dùng lớp `Graphics` bằng phương thức `graphics.dispose()`.
