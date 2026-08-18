# Ternary Search (Tìm kiếm tam phân)

---

## Định nghĩa
Tìm kiếm tam phân (Ternary Search) là một giải thuật chia để trị hoạt động trên mảng đã sắp xếp, bằng cách chia phạm vi tìm kiếm thành 3 phần bằng nhau thông qua 2 điểm chốt giữa (mid1 và mid2) để thu hẹp phạm vi tìm kiếm.

---

## Tác dụng
- **Tối ưu hóa tìm cực trị (Hàm lồi/lõm):** Phổ biến nhất không phải để tìm kiếm trên mảng thường, mà để tìm giá trị lớn nhất hoặc nhỏ nhất của một hàm số đơn điệu đơn cực trị (Unimodal function) trong toán học và tin học.

---

## FLOW
Ý tưởng chính:
1. Xác định hai con trỏ `low` và `high`.
2. Tính toán hai điểm chia giữa:
   - `mid1 = low + (high - low) / 3`
   - `mid2 = high - (high - low) / 3`
3. So sánh phần tử tại `mid1` và `mid2` với giá trị cần tìm `x`:
   - Nếu `arr[mid1] == x`, trả về `mid1`.
   - Nếu `arr[mid2] == x`, trả về `mid2`.
   - Nếu `x < arr[mid1]`, thu hẹp phạm vi về đoạn bên trái: `high = mid1 - 1`.
   - Nếu `x > arr[mid2]`, thu hẹp phạm vi về đoạn bên phải: `low = mid2 + 1`.
   - Nếu không, `x` nằm ở đoạn giữa: `low = mid1 + 1`, `high = mid2 - 1`.

---

## Code triển khai (Java)
```java
public class TernarySearch {
    public static int search(int[] arr, int x) {
        int low = 0;
        int high = arr.length - 1;

        while (low <= high) {
            int mid1 = low + (high - low) / 3;
            int mid2 = high - (high - low) / 3;

            if (arr[mid1] == x) return mid1;
            if (arr[mid2] == x) return mid2;

            if (x < arr[mid1]) {
                high = mid1 - 1;
            } else if (x > arr[mid2]) {
                low = mid2 + 1;
            } else {
                low = mid1 + 1;
                high = mid2 - 1;
            }
        }
        return -1;
    }
}
```

---

## Lưu ý
> [!warning] Tại sao ít dùng hơn Binary Search trên mảng phẳng?
> Mặc dù Ternary Search chia mảng thành 3 phần, độ phức tạp thời gian vẫn là $O(\log_3 N)$. Trong thực tế, số phép so sánh ở mỗi vòng lặp của Ternary Search là 4 (nhiều hơn so với 2 của Binary Search), dẫn đến việc nó chạy chậm hơn Binary Search thông thường trên các mảng phẳng trong bộ nhớ.
