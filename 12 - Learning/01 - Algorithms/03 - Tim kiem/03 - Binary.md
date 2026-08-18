# Binary Search (Tìm kiếm nhị phân)

---

## Định nghĩa
Tìm kiếm nhị phân (Binary Search) là một thuật toán hiệu quả hoạt động trên nguyên lý chia để trị, liên tục chia đôi phạm vi tìm kiếm của mảng đã được sắp xếp để xác định vị trí của phần tử cần tìm.

---

## Tác dụng
- **Tốc độ vượt trội:** Giảm phạm vi tìm kiếm theo lũy thừa của 2, giúp tìm kiếm trong mảng có 1 triệu phần tử chỉ mất tối đa khoảng 20 phép so sánh ($O(\log N)$).

---

## FLOW
Ý tưởng chính:
1. Xác định hai con trỏ giới hạn: `low = 0` và `high = n - 1`.
2. Trong khi `low <= high`:
   - Tìm chỉ số ở giữa: `mid = low + (high - low) / 2`.
   - Nếu `arr[mid] == x`, trả về `mid`.
   - Nếu `arr[mid] < x`, thu hẹp phạm vi sang nửa phải: `low = mid + 1`.
   - Nếu `arr[mid] > x`, thu hẹp phạm vi sang nửa trái: `high = mid - 1`.
3. Nếu vòng lặp kết thúc mà không tìm thấy, trả về `-1`.

---

## Code triển khai (Java)
```java
public class BinarySearch {
    public static int search(int[] arr, int x) {
        int low = 0;
        int high = arr.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            // Kiểm tra xem x có ở vị trí giữa không
            if (arr[mid] == x) {
                return mid;
            }

            // Nếu x lớn hơn, bỏ qua nửa trái
            if (arr[mid] < x) {
                low = mid + 1;
            } 
            // Nếu x nhỏ hơn, bỏ qua nửa phải
            else {
                high = mid - 1;
            }
        }
        return -1;
    }
}
```

---

## Lưu ý
> [!important] Tránh lỗi tràn số (Integer Overflow)
> Khi tính chỉ số giữa, cách viết phổ biến `mid = (low + high) / 2` có thể gây ra lỗi tràn số nguyên (Integer Overflow) trong Java nếu tổng của `low` và `high` lớn hơn giá trị tối đa của kiểu số nguyên `Integer.MAX_VALUE`. 
> - **Cách viết đúng chuẩn:** `int mid = low + (high - low) / 2;`
