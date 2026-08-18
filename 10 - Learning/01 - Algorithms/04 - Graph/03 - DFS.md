# Depth-First Search (Duyệt theo chiều sâu)

---

## Định nghĩa
Duyệt theo chiều sâu (DFS - Depth-First Search) là giải thuật duyệt hoặc tìm kiếm trên đồ thị, bắt đầu từ một đỉnh gốc và đi xa nhất có thể dọc theo mỗi nhánh trước khi quay lui (backtracking).

---

## Tác dụng
- **Kiểm tra liên thông và chu trình:** Rất mạnh mẽ trong việc phát hiện chu trình (cycle) trong đồ thị, sắp xếp topo, hoặc tìm các thành phần liên thông mạnh.

---

## FLOW
Ý tưởng chính:
Sử dụng đệ quy (hoặc cấu trúc dữ liệu **Ngăn xếp - Stack** tự quản lý) kết hợp mảng `visited` để ghi nhớ trạng thái các đỉnh.
1. Bắt đầu từ đỉnh gốc `u`. Đánh dấu `visited[u] = true`.
2. Xét từng đỉnh kề `v` với `u`.
3. Nếu `v` chưa được duyệt, gọi đệ quy DFS trên đỉnh `v`.
4. Nếu tất cả các nhánh từ `u` đã đi hết, quay lui về đỉnh trước đó.

---

## Code triển khai (Java)
```java
import java.util.*;

public class DFS {
    public static void search(List<List<Integer>> adj, int startNode) {
        int V = adj.size();
        boolean[] visited = new boolean[V];
        dfsHelper(adj, startNode, visited);
    }

    private static void dfsHelper(List<List<Integer>> adj, int curr, boolean[] visited) {
        visited[curr] = true;
        System.out.print(curr + " ");

        // Đệ quy duyệt qua các đỉnh kề
        for (int neighbor : adj.get(curr)) {
            if (!visited[neighbor]) {
                dfsHelper(adj, neighbor, visited);
            }
        }
    }
}
```

---

## Lưu ý
> [!caution] Nguy cơ tràn Stack đệ quy (StackOverflow)
> Nếu đồ thị quá lớn và có cấu trúc dạng một đường thẳng dài (đồ thị suy biến), việc đệ quy DFS sâu sẽ dễ dẫn đến lỗi tràn bộ nhớ Stack (`StackOverflowError` trong Java). 
> - **Khắc phục:** Chuyển sang sử dụng vòng lặp `while` kết hợp cấu trúc dữ liệu `Stack` tự định nghĩa lưu trên bộ nhớ Heap.
