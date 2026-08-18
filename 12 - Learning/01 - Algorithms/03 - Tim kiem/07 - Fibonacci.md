# Fibonacci Search (Tìm kiếm Fibonacci)

---

## Định nghĩa
Tìm kiếm Fibonacci (Fibonacci Search) là thuật toán tìm kiếm trên mảng đã sắp xếp sử dụng các số Fibonacci để phân chia phạm vi tìm kiếm.

---

## Tác dụng
- **Tránh phép nhân và phép chia:** Khác với Binary Search (cần phép chia `/ 2` hoặc phép dịch bit) hay Interpolation Search (cần phép nhân/chia số thực), Fibonacci Search chỉ sử dụng phép cộng và phép trừ cơ bản. Điều này có lợi thế lớn trên các CPU thế hệ cũ hoặc vi điều khiển cấp thấp không có bộ tính toán nhân chia phần cứng.
- **Tối ưu bộ đệm:** Tập trung tìm kiếm ở các vùng dữ liệu có xu hướng thu hẹp một chiều, thân thiện với hệ thống Cache.

---

## FLOW
Ý tưởng chính:
1. Tìm số Fibonacci nhỏ nhất lớn hơn hoặc bằng kích thước mảng $N$. Gọi số đó là $F_k$. Hai số liền trước nó là $F_{k-1}$ và $F_{k-2}$.
2. Dùng $F_{k-2}$ làm khoảng dịch chuyển từ mốc cơ sở `offset` để kiểm tra phần tử tại vị trí `i = min(offset + F_{k-2}, N - 1)`.
3. So sánh `arr[i]` với `x`:
   - Nếu bằng, trả về `i`.
   - Nếu lớn hơn `x`, dịch chuyển phạm vi sang trái bằng cách lùi dãy số Fibonacci đi 2 bước.
   - Nếu nhỏ hơn `x`, dịch chuyển phạm vi sang phải bằng cách lùi dãy số Fibonacci đi 1 bước và cập nhật `offset = i`.

---

## Code triển khai (Java)
```java
public class FibonacciSearch {
    public static int search(int[] arr, int x) {
        int n = arr.length;

        // Khởi tạo các số Fibonacci
        int fibM2 = 0; // F(k-2)
        int fibM1 = 1; // F(k-1)
        int fibM = fibM2 + fibM1; // F(k)

        // Tìm số Fibonacci lớn nhất nhỏ hơn hoặc bằng n
        while (fibM < n) {
            fibM2 = fibM1;
            fibM1 = fibM;
            fibM = fibM2 + fibM1;
        }

        int offset = -1;

        // Trong khi vẫn còn phần tử để xét
        while (fibM > 1) {
            // Kiểm tra xem fibM2 có phải là chỉ số hợp lệ không
            int i = Math.min(offset + fibM2, n - 1);

            // Nếu x lớn hơn, dịch chuyển offset và lùi 1 bước Fibonacci
            if (arr[i] < x) {
                fibM = fibM1;
                fibM1 = fibM2;
                fibM2 = fibM - fibM1;
                offset = i;
            }
            // Nếu x nhỏ hơn, lùi 2 bước Fibonacci
            else if (arr[i] > x) {
                fibM = fibM2;
                fibM1 = fibM1 - fibM2;
                fibM2 = fibM - fibM1;
            }
            // Tìm thấy
            else {
                return i;
            }
        }

        // So sánh phần tử cuối cùng
        if (fibM1 == 1 && arr[offset + 1] == x) {
            return offset + 1;
        }

        return -1;
    }
}
```

---

## Lưu ý
> [!info] So sánh độ phức tạp
> Độ phức tạp thời gian tệ nhất và trung bình của Fibonacci Search đều là $O(\log N)$, tương đương với Binary Search nhưng có thể cho hiệu năng thực tế tối ưu hơn trên các phần cứng bị hạn chế năng lực tính toán dấu phẩy động hoặc phép chia.
