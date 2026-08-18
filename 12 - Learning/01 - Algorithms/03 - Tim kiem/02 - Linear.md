# Linear Search (Tìm kiếm tuần tự)

---

## Định nghĩa
Tìm kiếm tuần tự (Linear Search) là giải thuật tìm kiếm đơn giản nhất, hoạt động bằng cách duyệt qua từng phần tử của danh sách từ đầu đến cuối cho đến khi tìm thấy phần tử mong muốn hoặc duyệt hết danh sách.

---

## Tác dụng
- **Không yêu cầu sắp xếp:** Tiện lợi khi dữ liệu đầu vào ngẫu nhiên và ta chỉ cần tìm kiếm một vài lần.
- **Dễ triển khai:** Phù hợp với mọi cấu trúc dữ liệu cơ bản (mảng, danh sách liên kết).

---

## FLOW
Ý tưởng chính:
1. Bắt đầu từ phần tử đầu tiên của mảng (chỉ số `i = 0`).
2. So sánh phần tử hiện tại `arr[i]` với giá trị cần tìm `x`.
3. Nếu `arr[i] == x`, trả về chỉ số `i`.
4. Nếu không, tăng `i` lên 1 và lặp lại bước 2.
5. Nếu duyệt hết mảng mà không tìm thấy, trả về `-1`.

---

## Code triển khai (Java)
```java
public class LinearSearch {
    public static int search(int[] arr, int x) {
        int n = arr.length;
        for (int i = 0; i < n; i++) {
            if (arr[i] == x) {
                return i; // Tìm thấy, trả về vị trí
            }
        }
        return -1; // Không tìm thấy
    }
}
```

---

## Lưu ý
> [!warning] Hạn chế với dữ liệu lớn
> Do độ phức tạp thời gian tệ nhất là $O(N)$, Linear Search sẽ cực kỳ chậm khi tìm kiếm trên các tập dữ liệu có hàng triệu bản ghi. Hãy cân nhắc sắp xếp dữ liệu và dùng các giải thuật tối ưu hơn khi có nhu cầu tìm kiếm lặp lại nhiều lần.
