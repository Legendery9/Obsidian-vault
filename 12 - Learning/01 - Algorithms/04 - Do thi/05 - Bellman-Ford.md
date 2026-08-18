# Thuật toán Bellman-Ford (Đường đi ngắn nhất có cạnh âm)

---

## Định nghĩa
Thuật toán Bellman-Ford tìm đường đi ngắn nhất từ một đỉnh nguồn tới mọi đỉnh khác trên đồ thị có hướng hoặc vô hướng, hỗ trợ các cạnh mang trọng số âm và có khả năng phát hiện các chu trình trọng số âm.

---

## Tác dụng
- **Xử lý cạnh trọng số âm:** Khắc phục điểm yếu lớn nhất của Dijkstra.
- **Phát hiện chu trình âm:** Rất quan trọng trong các bài toán quy đổi tiền tệ để phát hiện cơ hội kiếm lời chênh lệch vô hạn (arbitrage loop) bằng cách quy đổi vòng tròn.

---

## FLOW
Ý tưởng chính (Duyệt tối ưu hóa cạnh toàn bộ):
Một đường đi ngắn nhất không đi qua chu trình âm sẽ đi qua tối đa $V-1$ cạnh.
1. Khởi tạo `dist[source] = 0`, các đỉnh khác là $\infty$.
2. Lặp $V-1$ lần:
   - Duyệt qua **tất cả các cạnh** $(u, v)$ có trọng số $w$ trên đồ thị.
   - Thực hiện tối ưu hóa (Relaxation): Nếu `dist[u] + w < dist[v]` thì cập nhật `dist[v] = dist[u] + w`.
3. Kiểm tra chu trình âm (Vòng lặp thứ $V$):
   - Duyệt lại toàn bộ cạnh một lần nữa.
   - Nếu vẫn tồn tại cạnh $(u, v)$ mà `dist[u] + w < dist[v]`, chứng tỏ đồ thị chứa chu trình âm.

---

## Code triển khai (Java)
```java
import java.util.*;

public class BellmanFord {
    static class Edge {
        int src, dest, weight;
        Edge(int src, int dest, int weight) {
            this.src = src;
            this.dest = dest;
            this.weight = weight;
        }
    }

    public static boolean getShortestPath(List<Edge> edges, int V, int source, int[] dist) {
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[source] = 0;

        // 1. Tối ưu hóa các cạnh V - 1 lần
        for (int i = 1; i < V; i++) {
            for (Edge edge : edges) {
                int u = edge.src;
                int v = edge.dest;
                int w = edge.weight;
                if (dist[u] != Integer.MAX_VALUE && dist[u] + w < dist[v]) {
                    dist[v] = dist[u] + w;
                }
            }
        }

        // 2. Kiểm tra chu trình âm
        for (Edge edge : edges) {
            int u = edge.src;
            int v = edge.dest;
            int w = edge.weight;
            if (dist[u] != Integer.MAX_VALUE && dist[u] + w < dist[v]) {
                System.out.println("Đồ thị chứa chu trình âm!");
                return false; // Phát hiện chu trình âm
            }
        }
        return true;
    }
}
```

---

## Lưu ý
> [!warning] Đánh đổi hiệu năng
> Độ phức tạp thời gian của Bellman-Ford là $O(V \cdot E)$, chậm hơn nhiều so với Dijkstra ($O((V+E) \log V)$). Chỉ nên dùng Bellman-Ford khi chắc chắn đồ thị có các cạnh mang trọng số âm.
