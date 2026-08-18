# Exponential Search (Tìm kiếm lũy thừa)

---

## Định nghĩa
Tìm kiếm lũy thừa (Exponential Search) là thuật toán tìm kiếm trên mảng đã sắp xếp, hoạt động bằng cách nhanh chóng xác định một phạm vi (dải chỉ số) chứa phần tử mục tiêu bằng cách tăng chỉ số theo cấp số nhân (lũy thừa của 2), sau đó thực hiện Tìm kiếm nhị phân (Binary Search) trong dải chỉ số đó.

---

## Tác dụng
- **Tối ưu cho mảng kích thước vô hạn/không xác định:** Rất hữu ích khi ta không biết trước kích thước cuối cùng của mảng (ví dụ: luồng dữ liệu liên tục từ mạng - stream).
- **Hiệu quả khi mục tiêu nằm ở đầu mảng:** Tốc độ tìm kiếm nhanh hơn Binary Search thông thường nếu phần tử cần tìm nằm ở vị trí nhỏ gần đầu mảng.

---

## FLOW
Ý tưởng chính:
1. Nếu phần tử đầu tiên `arr[0]` là giá trị cần tìm, trả về `0`.
2. Khởi tạo chỉ số tìm kiếm `i = 1`.
3. Trong khi `i < n` và `arr[i] <= x`, nhân đôi chỉ số: `i = i * 2`.
4. Gọi **Binary Search** trên phân mảng từ `i/2` đến vị trí nhỏ hơn giữa `i` và `n-1`.

---

## Code triển khai (Java)
```java
import java.util.Arrays;

public class ExponentialSearch {
    public static int search(int[] arr, int x) {
        int n = arr.length;
        if (n == 0) return -1;
        if (arr[0] == x) return 0;

        // Tìm phạm vi cho Binary Search bằng cách nhân đôi chỉ số
        int i = 1;
        while (i < n && arr[i] <= x) {
            i = i * 2;
        }

        // Gọi Binary Search trên phạm vi tìm thấy
        int low = i / 2;
        int high = Math.min(i, n - 1);
        
        return binarySearch(arr, low, high, x);
    }

    private static int binarySearch(int[] arr, int low, int high, int x) {
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (arr[mid] == x) return mid;
            if (arr[mid] < x) low = mid + 1;
            else high = mid - 1;
        }
        return -1;
    }
}
```

---

## Lưu ý
> [!info] Độ phức tạp thời gian
> Độ phức tạp thời gian của Exponential Search là $O(\log i)$ với $i$ là vị trí thực tế của phần tử cần tìm trong mảng. Điều này làm cho nó cực kỳ hiệu quả khi $i$ nhỏ hơn rất nhiều so với kích thước $N$ của toàn bộ mảng.
