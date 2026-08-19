# Java StringBuffer

> [!abstract] Định nghĩa
> **StringBuffer** là một lớp đại diện cho chuỗi ký tự động (mutable) tương tự như `StringBuilder`. Điểm khác biệt cốt lõi là các phương thức của `StringBuffer` được đồng bộ hóa (synchronized), đảm bảo **an toàn luồng (thread-safe)** khi sử dụng trong môi trường đa luồng.

---

## 1. Tác dụng
- **Xử lý chuỗi động đa luồng:** Khi nhiều luồng cùng thao tác và thay đổi nội dung của một chuỗi chung, `StringBuffer` ngăn chặn hiện tượng tranh chấp dữ liệu (race conditions).
- **Tránh tạo rác bộ nhớ:** Tương tự `StringBuilder`, `StringBuffer` sửa đổi chuỗi trực tiếp trên cùng một vùng đệm mà không tạo ra các đối tượng `String` trung gian.

---

## 2. So sánh StringBuffer vs StringBuilder

| Tiêu chí | StringBuilder | StringBuffer |
| :--- | :--- | :--- |
| **Thread-safety** | ❌ Không an toàn luồng (Không đồng bộ hóa). |  An toàn luồng (Các phương thức được gắn `synchronized`). |
| **Hiệu năng** | ⚡ Nhanh hơn (Không chịu chi phí khóa đồng bộ). | 🐢 Chậm hơn (Mất thêm chi phí để đồng bộ hóa luồng). |
| **Cú pháp** | Tương đồng hoàn toàn. | Tương đồng hoàn toàn. |
| **Khi nào nên dùng** | Môi trường đơn luồng (hầu hết các trường hợp thông thường, ví dụ: trong một phương thức cục bộ). | Môi trường đa luồng (ví dụ: dùng chung tài nguyên giữa các luồng chạy song song). |

---

## 3. Bảng tham chiếu các phương thức cốt lõi

Tất cả các phương thức dưới đây đều có hành vi giống hệt `StringBuilder` nhưng được đồng bộ hóa.

| Method / Statement | Definition | Tác dụng | Lưu ý |
| :--- | :--- | :--- | :--- |
| `append(Object obj)` | Thêm vào cuối | Nối biểu diễn chuỗi của `obj` vào cuối chuỗi hiện tại. | Trả về chính đối tượng `StringBuffer` để xâu chuỗi lệnh (method chaining). |
| `insert(int offset, Object obj)`| Chèn tại vị trí | Chèn biểu diễn chuỗi của `obj` vào vị trí `offset`. | Đẩy phần còn lại của chuỗi sang phải. |
| `replace(int start, int end, String str)`| Thay thế đoạn | Thay thế chuỗi con từ `start` đến trước `end` bằng `str`. | Ném `StringIndexOutOfBoundsException` nếu chỉ số sai. |
| `delete(int start, int end)` | Xóa đoạn | Xóa các ký tự từ `start` đến trước `end`. | Thay đổi trực tiếp chiều dài của chuỗi. |
| `deleteCharAt(int index)` | Xóa ký tự | Xóa ký tự tại vị trí `index`. | Tiện lợi khi xóa ký tự cuối cùng (ví dụ: dấu phẩy thừa). |
| `reverse()` | Đảo ngược | Đảo ngược thứ tự các ký tự trong chuỗi. | Thay đổi trực tiếp chuỗi gốc. |
| `toString()` | Chuyển sang String | Xuất ra đối tượng `String` bất biến chứa nội dung hiện tại. | Tạo một đối tượng String mới từ bộ đệm. |

---

## 4. Ví dụ minh họa

```java
public class StringBufferExample {
    public static void main(String[] args) {
        // ✅ Nên làm (Do): Sử dụng StringBuffer khi dùng chung giữa các Thread
        StringBuffer buffer = new StringBuffer("Java");

        // 1. append
        buffer.append(" Core").append(" Tutorial"); // "Java Core Tutorial"

        // 2. insert
        buffer.insert(4, " Standard"); // "Java Standard Core Tutorial"

        // 3. replace
        buffer.replace(14, 18, "SE"); // "Java Standard SE Tutorial"

        // 4. delete
        buffer.delete(4, 13); // "Java SE Tutorial"

        // 5. reverse
        buffer.reverse(); // "lairotuT ES avaJ"
        buffer.reverse(); // Trả lại: "Java SE Tutorial"

        // 6. toString
        String result = buffer.toString(); // "Java SE Tutorial"
        System.out.println(result);
    }
}
```

---

## 5. Lưu ý

> [!warning]
> - Do chi phí đồng bộ hóa (synchronization overhead), bạn **không nên** lạm dụng `StringBuffer` trong các phương thức cục bộ đơn luồng. Hãy luôn ưu tiên sử dụng `StringBuilder` để đạt hiệu năng tối ưu.
