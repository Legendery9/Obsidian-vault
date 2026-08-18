# Breadth-First Search (Duyệt theo chiều rộng)

---

## Định nghĩa
Duyệt theo chiều rộng (BFS - Breadth-First Search) là giải thuật duyệt hoặc tìm kiếm trên đồ thị, bắt đầu từ một đỉnh gốc và duyệt tất cả các đỉnh lân cận ở cấp độ hiện tại trước khi chuyển sang các đỉnh ở cấp độ sâu hơn.

---

## Tác dụng
- **Tìm đường đi ngắn nhất:** Trên đồ thị không trọng số (hoặc trọng số bằng nhau), BFS đảm bảo tìm được đường đi ngắn nhất (ít cạnh nhất) từ đỉnh nguồn tới mọi đỉnh khác.

---

## FLOW
Ý tưởng chính:
Sử dụng cấu trúc dữ liệu **Hàng đợi (Queue)** để quản lý các đỉnh chuẩn bị duyệt và một mảng `visited` để đánh dấu tránh duyệt lặp lại.
1. Đưa đỉnh gốc vào Queue và đánh dấu đã duyệt (`visited = true`).
2. Trong khi Queue không rỗng:
   - Lấy đỉnh `u` ra khỏi đầu Queue.
   - Xét tất cả các đỉnh kề `v` với `u` mà chưa được duyệt.
   - Đưa `v` vào Queue và đánh dấu `visited[v] = true`.

---

## Code triển khai (Java)
```java
import java.util.*;

public class BFS {
    public static void search(List<List<Integer>> adj, int startNode) {
        int V = adj.size();
        boolean[] visited = new boolean[V];
        Queue<Integer> queue = new LinkedList<>();

        // Khởi tạo đỉnh bắt đầu
        visited[startNode] = true;
        queue.add(startNode);

        while (!queue.isEmpty()) {
            int curr = queue.poll();
            System.out.print(curr + " ");

            // Duyệt qua các đỉnh kề
            for (int neighbor : adj.get(curr)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
    }
}
```

---

## Lưu ý
> [!important] Ứng dụng thực tế
> BFS được ứng dụng trong thuật toán tìm cây khung nhỏ nhất, tìm các thành phần liên thông của đồ thị, hoặc trong các thuật toán trí tuệ nhân tạo đơn giản để tìm kiếm trạng thái (như giải mê cung).
