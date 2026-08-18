# Thuật toán Kosaraju (Thành phần liên thông mạnh bằng 2 DFS)

---

## Định nghĩa
Thuật toán Kosaraju dùng để tìm các thành phần liên thông mạnh (SCC) của một đồ thị có hướng bằng cách thực hiện hai lần duyệt DFS: lần thứ nhất trên đồ thị gốc và lần thứ hai trên đồ thị chuyển vị (transposed graph).

---

## Tác dụng
- **Tìm SCC dễ hiểu:** So với Tarjan lưu giữ nhiều chỉ số phức tạp (`dfn` và `low`), Kosaraju dễ hiểu và dễ code hơn nhờ tận dụng tính chất đối xứng của đồ thị chuyển vị.

---

## FLOW
Ý tưởng chính (Duyệt DFS hai lần):
1. **Lần DFS thứ nhất:** Duyệt DFS trên đồ thị gốc. Khi một đỉnh hoàn thành xong nhánh đệ quy (duyệt xong các đỉnh con), đẩy đỉnh đó vào một Stack để ghi nhận thứ tự hoàn thành.
2. **Chuyển vị đồ thị:** Tạo đồ thị đảo chiều $G^T$ bằng cách đổi hướng tất cả các cạnh của đồ thị ban đầu (cạnh $u \to v$ thành $v \to u$).
3. **Lần DFS thứ hai:** Lần lượt lấy các đỉnh ra khỏi Stack. Nếu đỉnh đó chưa được duyệt ở lần 2, thực hiện DFS trên đồ thị chuyển vị $G^T$. Tất cả các đỉnh được khám phá từ nhánh DFS này tạo thành một thành phần liên thông mạnh (SCC).

---

## Code triển khai (Java)
```java
import java.util.*;

public class Kosaraju {
    private void dfs1(int u, List<List<Integer>> adj, boolean[] visited, Stack<Integer> stack) {
        visited[u] = true;
        for (int v : adj.get(u)) {
            if (!visited[v]) {
                dfs1(v, adj, visited, stack);
            }
        }
        stack.push(u); // Đẩy vào Stack khi kết thúc đệ quy
    }

    private void dfs2(int u, List<List<Integer>> adjT, boolean[] visited, List<Integer> scc) {
        visited[u] = true;
        scc.add(u);
        for (int v : adjT.get(u)) {
            if (!visited[v]) {
                dfs2(v, adjT, visited, scc);
            }
        }
    }

    private List<List<Integer>> transpose(List<List<Integer>> adj) {
        int V = adj.size();
        List<List<Integer>> adjT = new ArrayList<>();
        for (int i = 0; i < V; i++) adjT.add(new ArrayList<>());

        for (int u = 0; u < V; u++) {
            for (int v : adj.get(u)) {
                adjT.get(v).add(u); // Đảo chiều cạnh
            }
        }
        return adjT;
    }

    public List<List<Integer>> findSCCs(List<List<Integer>> adj) {
        int V = adj.size();
        Stack<Integer> stack = new Stack<>();
        boolean[] visited = new boolean[V];

        // 1. Chạy DFS lần 1 để lấy thứ tự hoàn thành
        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                dfs1(i, adj, visited, stack);
            }
        }

        // 2. Chuyển vị đồ thị
        List<List<Integer>> adjT = transpose(adj);

        // 3. Chạy DFS lần 2 trên đồ thị chuyển vị
        Arrays.fill(visited, false);
        List<List<Integer>> sccs = new ArrayList<>();

        while (!stack.isEmpty()) {
            int u = stack.pop();
            if (!visited[u]) {
                List<Integer> scc = new ArrayList<>();
                dfs2(u, adjT, visited, scc);
                sccs.add(scc);
            }
        }
        return sccs;
    }
}
```

---

## Lưu ý
> [!important] So sánh Kosaraju vs Tarjan
> - Cả hai đều đạt độ phức tạp thời gian $O(V + E)$.
> - **Kosaraju:** Cần 2 lượt DFS và thêm chi phí bộ nhớ để đảo chiều đồ thị.
> - **Tarjan:** Chỉ cần 1 lượt DFS và ít tốn bộ nhớ hơn, nên trong môi trường công nghiệp thực tế thường ưa chuộng Tarjan hơn.
