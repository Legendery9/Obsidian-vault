# Excalidraw trong Obsidian

---

## Định nghĩa
Excalidraw là một công cụ bảng vẽ tay trực quan được tích hợp trực tiếp dưới dạng plugin trong Obsidian, cho phép bạn phác thảo sơ đồ, biểu đồ và ghi chú trực quan bằng hình vẽ.

---

## Tác dụng
- **Vẽ sơ đồ tư duy:** Phác thảo nhanh các kiến thức phức tạp dạng hình ảnh, sơ đồ khối.
- **Tương thích cao:** File vẽ được lưu dưới dạng văn bản `.excalidraw.md` chứa dữ liệu đồ họa, có thể chuyển đổi thành SVG hoặc PNG.
- **Liên kết hai chiều:** Có thể chèn liên kết Wiki `[[Trang ghi chú]]` trực tiếp vào các hình vẽ trên bảng vẽ để nhảy đến ghi chú liên quan.

---

## Bảng tham chiếu

### Phím tắt vẽ nhanh trong Excalidraw

| Phím tắt | Công cụ tương ứng | Tác dụng |
| :--- | :--- | :--- |
| `1` hoặc `V` | Selection tool | Chọn và di chuyển hình vẽ |
| `2` hoặc `R` | Rectangle | Vẽ hình chữ nhật |
| `3` hoặc `O` | Diamond | Vẽ hình thoi (dùng trong lưu đồ quyết định) |
| `4` hoặc `E` | Ellipse | Vẽ hình tròn / elip |
| `5` hoặc `A` | Arrow | Vẽ mũi tên kết nối các đối tượng |
| `6` hoặc `L` | Line | Vẽ đường thẳng |
| `7` hoặc `P` | Draw / Pen | Vẽ tự do bằng bút vẽ tay |
| `8` hoặc `T` | Text | Chèn văn bản vào bảng vẽ |

---

## Ví dụ
Sơ đồ khối đơn giản mô tả luồng logic (Flow):
- Đối tượng hình chữ nhật **[Bắt đầu]** kết nối bằng phím tắt `5` (Mũi tên) sang đối tượng **[Xử lý]** và kết thúc tại hình tròn **[Hoàn thành]**.
- Có thể viết chữ lên mũi tên hoặc liên kết trực tiếp một nút bấm tới ghi chú `[[06 - Java Program]]` bằng cách nhấn chuột phải vào đối tượng chọn **Link**.

---

## Lưu ý
> [!info] Nhúng hình vẽ vào ghi chú Markdown
> Bạn có thể nhúng hình vẽ Excalidraw vào file ghi chú thường của mình bằng cú pháp: `![[my-diagram.excalidraw]]`.
