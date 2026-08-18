# Merge Sort (Sắp xếp trộn)

---

## Định nghĩa
Sắp xếp trộn (Merge Sort) là một thuật toán sắp xếp dựa trên kỹ thuật Chia để trị (Divide and Conquer), hoạt động bằng cách chia mảng thành các mảng con nhỏ hơn cho đến khi còn 1 phần tử, sau đó trộn (merge) các mảng con đã sắp xếp đó lại với nhau để tạo thành mảng kết quả hoàn chỉnh.

---

## Tác dụng
- **Độ ổn định hiệu năng:** Độ phức tạp thời gian luôn là $O(N \log N)$ bất kể mảng đầu vào ở trạng thái nào (ngẫu nhiên, đã sort, ngược).
- **Tính ổn định (Stable):** Bảo toàn thứ tự ban đầu của các phần tử trùng lặp.

---

## FLOW
Ý tưởng chính:
1. **Chia (Divide):** Tìm chỉ số giữa `mid` và chia mảng thành hai nửa: `left` (từ `l` đến `mid`) và `right` (từ `mid+1` đến `r`).
2. **Trị (Conquer):** Tiếp tục gọi đệ quy sắp xếp hai nửa `left` và `right`.
3. **Trộn (Combine/Merge):** Gộp hai nửa đã sắp xếp lại với nhau bằng cách so sánh từng phần tử đầu tiên của mỗi nửa và đưa phần tử nhỏ hơn vào mảng tạm thời.

---

## Code triển khai (Java)
```java
public class MergeSort {
    public static void sort(int[] arr, int l, int r) {
        if (l < r) {
            int mid = l + (r - l) / 2;

            // Đệ quy chia đôi mảng
            sort(arr, l, mid);
            sort(arr, mid + 1, r);

            // Trộn hai nửa đã sắp xếp
            merge(arr, l, mid, r);
        }
    }

    private static void merge(int[] arr, int l, int mid, int r) {
        // Tìm kích thước của hai mảng con cần trộn
        int n1 = mid - l + 1;
        int n2 = r - mid;

        // Tạo các mảng tạm thời
        int[] L = new int[n1];
        int[] R = new int[n2];

        // Sao chép dữ liệu vào mảng tạm
        System.arraycopy(arr, l, L, 0, n1);
        System.arraycopy(arr, mid + 1, R, 0, n2);

        // Trộn các mảng tạm lại
        int i = 0, j = 0, k = l;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k++] = L[i++];
            } else {
                arr[k++] = R[j++];
            }
        }

        // Sao chép các phần tử còn lại của L[] và R[] nếu có
        while (i < n1) arr[k++] = L[i++];
        while (j < n2) arr[k++] = R[j++];
    }
}
```

---

## Lưu ý
> [!warning] Nhược điểm về bộ nhớ
> Merge Sort không phải là thuật toán sắp xếp tại chỗ (in-place). Nó yêu cầu một lượng bộ nhớ phụ trợ bằng kích thước mảng gốc ($O(N)$ không gian) để lưu trữ các mảng tạm khi trộn. Điều này có thể gây tràn bộ nhớ đối với các hệ thống có tài nguyên RAM hạn chế.
