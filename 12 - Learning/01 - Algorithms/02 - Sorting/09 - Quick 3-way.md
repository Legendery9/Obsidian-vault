# Quick Sort 3-way (Sắp xếp nhanh 3 đoạn)

---

## Định nghĩa
Quick Sort 3-way (Dijkstra's 3-way partitioning) là một biến thể tối ưu hóa của Quick Sort, chia mảng thành 3 phần thay vì 2 phần xung quanh pivot: phần nhỏ hơn pivot, phần bằng pivot, và phần lớn hơn pivot.

---

## Tác dụng
- **Tối ưu cực độ với mảng nhiều phần tử trùng lặp (Few Unique Keys):** Khi mảng có nhiều giá trị lặp lại, Quick Sort truyền thống vẫn mất công chia đôi các phần tử bằng nhau, trong khi 3-way gom toàn bộ các phần tử bằng nhau vào giữa và bỏ qua không cần đệ quy chúng, giúp đưa độ phức tạp về $O(N)$ trong trường hợp mảng chỉ có các khóa trùng nhau.

---

## FLOW
Ý tưởng chính (Giải thuật phân hoạch 3 đường của Dijkstra):
Sử dụng 3 con trỏ: `lt` (nhỏ hơn), `gt` (lớn hơn), và `i` (đang xét).
Coi `v` là giá trị pivot:
- Nếu `arr[i] < v`: Hoán đổi `arr[i]` và `arr[lt]`, tăng cả `i` và `lt`.
- Nếu `arr[i] > v`: Hoán đổi `arr[i]` và `arr[gt]`, giảm `gt` (không tăng `i` vì phần tử hoán đổi từ sau về chưa được xét).
- Nếu `arr[i] == v`: Tăng `i`.

---

## Code triển khai (Java)
```java
public class QuickSort3Way {
    public static void sort(int[] arr, int low, int high) {
        if (low >= high) return;

        int lt = low;
        int gt = high;
        int v = arr[low]; // Chọn phần tử đầu làm pivot
        int i = low + 1;

        while (i <= gt) {
            if (arr[i] < v) {
                swap(arr, lt++, i++);
            } else if (arr[i] > v) {
                swap(arr, i, gt--);
            } else {
                i++;
            }
        }

        // Sau vòng lặp, arr[low..lt-1] < v = arr[lt..gt] < arr[gt+1..high]
        sort(arr, low, lt - 1);
        sort(arr, gt + 1, high);
    }

    private static void swap(int[] arr, int a, int b) {
        int temp = arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }
}
```

---

## Lưu ý
> [!important] Ứng dụng thực tế
> Giải thuật phân hoạch 3 đường này được sử dụng mặc định trong các thư viện chuẩn của nhiều ngôn ngữ (Ví dụ: phương thức sắp xếp các kiểu dữ liệu nguyên thủy của Java - Dual-Pivot QuickSort) nhờ khả năng chống lại sự suy hao hiệu năng khi dữ liệu bị trùng lặp nhiều.
