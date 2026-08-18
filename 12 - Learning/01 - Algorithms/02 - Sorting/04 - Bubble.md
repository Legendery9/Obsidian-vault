# Bubble Sort (Sắp xếp nổi bọt)

---

## Định nghĩa
Sắp xếp nổi bọt (Bubble Sort) là thuật toán sắp xếp hoạt động bằng cách lặp lại việc duyệt qua mảng cần sắp xếp, so sánh từng cặp phần tử kề nhau và hoán đổi chúng nếu chúng đứng sai thứ tự cho đến khi không còn cặp nào sai thứ tự nữa.

---

## Tác dụng
- **Phát hiện mảng đã sắp xếp:** Dễ dàng tối ưu hóa để dừng sớm nếu mảng đã được sắp xếp sẵn (độ phức tạp tốt nhất đạt $O(N)$).

---

## FLOW
Ý tưởng chính:
1. Duyệt mảng liên tục qua nhiều vòng.
2. Ở mỗi vòng duyệt, so sánh các cặp kề nhau `(arr[j], arr[j+1])`.
3. Nếu phần tử trước lớn hơn phần tử sau, hoán đổi chúng (phần tử lớn hơn sẽ "nổi" dần về phía cuối mảng).
4. Sử dụng một cờ hiệu `swapped` để kiểm tra xem có xảy ra hoán đổi nào trong vòng duyệt hiện tại không. Nếu không có hoán đổi nào, dừng thuật toán sớm.

---

## Code triển khai (Java)
```java
public class BubbleSort {
    public static void sort(int[] arr) {
        int n = arr.length;
        boolean swapped;
        for (int i = 0; i < n - 1; i++) {
            swapped = false;
            for (int j = 0; j < n - 1 - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Hoán đổi
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }
            // Nếu không có phần tử nào hoán đổi, mảng đã sắp xếp
            if (!swapped) break;
        }
    }
}
```

---

## Lưu ý
> [!warning] Tốc độ thực tế chậm nhất
> Mặc dù dễ viết và dễ hiểu, Bubble Sort là thuật toán sắp xếp thực tế chậm nhất trong các thuật toán cơ bản do số lượng phép hoán đổi quá nhiều, làm mất thời gian thao tác ghi trên RAM.
