# Thuật toán Floyd-Warshall (Đường đi ngắn nhất giữa mọi cặp đỉnh)

---

## Định nghĩa
Thuật toán Floyd-Warshall là một giải thuật Quy hoạch động (Dynamic Programming) dùng để tìm đường đi ngắn nhất giữa **mọi cặp đỉnh** (all-pairs shortest path) trên đồ thị có hướng hoặc vô hướng, chấp nhận cạnh âm nhưng không có chu trình âm.

---

## Tác dụng
- **Tìm kiếm toàn cục:** Hữu ích khi cần xây dựng bảng khoảng cách toàn bộ giữa mọi địa điểm trong một khu vực để phục vụ cho các truy vấn tra cứu nhanh sau đó (như bảng khoảng cách giữa các thành phố).

---

## FLOW
Ý tưởng chính:
Xét một tập các đỉnh trung gian từ $1$ đến $k$. Khoảng cách ngắn nhất từ $i$ đến $j$ sử dụng các đỉnh trung gian trong tập $\{1, 2, ..., k\}$ được tối ưu hóa bằng công thức quy hoạch động:
$$
dist[i][j] = \min(dist[i][j], dist[i][k] + dist[k][j])
$$
Với mỗi đỉnh $k$ đóng vai trò là đỉnh trung gian đi qua từ $i$ đến $j$:
- Duyệt qua mọi cặp đỉnh $i$ và $j$, cập nhật lại khoảng cách ngắn nhất nếu đi qua $k$ tối ưu hơn đi trực tiếp.

---

## Code triển khai (Java)
```java
public class FloydWarshall {
    final static int INF = 99999; // Đại diện cho vô cùng để tránh tràn số khi cộng

    public static void compute(int[][] graph, int V) {
        int[][] dist = new int[V][V];

        // Khởi tạo ma trận khoảng cách ban đầu bằng ma trận kề
        for (int i = 0; i < V; i++) {
            System.arraycopy(graph[i], 0, dist[i], 0, V);
        }

        // Lặp đỉnh trung gian k từ 0 đến V-1
        for (int k = 0; k < V; k++) {
            // Duyệt đỉnh nguồn i
            for (int i = 0; i < V; i++) {
                // Duyệt đỉnh đích j
                for (int j = 0; j < V; j++) {
                    // Nếu k là đỉnh trung gian giúp tối ưu đường đi từ i tới j
                    if (dist[i][k] + dist[k][j] < dist[i][j]) {
                        dist[i][j] = dist[i][k] + dist[k][j];
                    }
                }
            }
        }
    }
}
```

---

## Lưu ý
> [!warning] Giới hạn bộ nhớ và thời gian
> Do độ phức tạp thời gian đạt $O(V^3)$ và không gian lưu trữ ma trận kề là $O(V^2)$, Floyd-Warshall chỉ phù hợp cho các đồ thị có quy mô nhỏ (thường số đỉnh $V \le 400$). Với các đồ thị lớn và thưa, việc chạy Dijkstra $V$ lần kết hợp với Priority Queue ($O(V \cdot (V + E) \log V)$) sẽ cho hiệu năng tốt hơn nhiều.
