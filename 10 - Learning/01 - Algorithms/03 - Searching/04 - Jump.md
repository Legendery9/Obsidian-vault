# Jump Search (Tìm kiếm nhảy)

---

## Định nghĩa
Tìm kiếm nhảy (Jump Search) là thuật toán tìm kiếm trên mảng đã sắp xếp, hoạt động bằng cách nhảy qua các khối có kích thước cố định $m$ để xác định khối chứa phần tử mục tiêu, sau đó thực hiện tìm kiếm tuần tự (Linear Search) bên trong khối đó.

---

## Tác dụng
- **Hiệu quả khi so sánh đắt đỏ:** So với Binary Search nhảy qua lại liên tục, Jump Search chỉ nhảy tiến một chiều, giúp giảm thiểu chi phí dịch chuyển con trỏ đọc trên các thiết bị lưu trữ vật lý (như ổ đĩa quang, băng từ).

---

## FLOW
Ý tưởng chính:
1. Xác định kích thước bước nhảy tối ưu: $step = \sqrt{N}$ (với $N$ là kích thước mảng).
2. Nhảy từ vị trí $0$, $step$, $2 \cdot step$... cho đến khi tìm thấy vị trí `arr[i] >= x` hoặc vượt quá kích thước mảng.
3. Thực hiện Linear Search ngược từ vị trí vừa tìm thấy về vị trí nhảy trước đó (`i - step`).
4. Trả về chỉ số nếu tìm thấy, ngược lại trả về `-1`.

---

## Code triển khai (Java)
```java
public class JumpSearch {
    public static int search(int[] arr, int x) {
        int n = arr.length;
        int step = (int) Math.floor(Math.sqrt(n));

        // Tìm block chứa phần tử cần tìm
        int prev = 0;
        int limit = Math.min(step, n);
        while (arr[limit - 1] < x) {
            prev = step;
            step += (int) Math.floor(Math.sqrt(n));
            if (prev >= n) {
                return -1;
            }
            limit = Math.min(step, n);
        }

        // Thực hiện tìm kiếm tuần tự từ prev đến limit
        while (arr[prev] < x) {
            prev++;
            // Nếu đã vượt sang block tiếp theo hoặc hết mảng
            if (prev == limit) {
                return -1;
            }
        }

        // Nếu tìm thấy phần tử
        if (arr[prev] == x) {
            return prev;
        }

        return -1;
    }
}
```

---

## Lưu ý
> [!info] Kích thước bước nhảy tối ưu
> Bằng chứng toán học chỉ ra rằng kích thước bước nhảy $step = \sqrt{N}$ cho phép thuật toán đạt độ phức tạp thời gian tối ưu nhất là $O(\sqrt{N})$.
