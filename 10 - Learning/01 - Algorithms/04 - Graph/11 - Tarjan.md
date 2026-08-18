# Thuật toán Tarjan (Thành phần liên thông mạnh)

---

## Định nghĩa
Thuật toán Tarjan là giải thuật dựa trên DFS dùng để tìm các thành phần liên thông mạnh (SCC - Strongly Connected Components) trong một đồ thị có hướng bằng cách gán cho mỗi đỉnh một chỉ số thứ tự duyệt và một chỉ số liên kết thấp nhất.

---

## Tác dụng
- **Phân nhóm liên thông mạnh:** Giúp tìm nhóm các trang web liên kết chéo mạnh mẽ với nhau, nhóm người dùng tương tác khép kín trong mạng xã hội, hoặc thu gọn đồ thị phức tạp thành đồ thị không chu trình phục vụ cho các giải thuật phân tích sâu hơn.

---

## FLOW
Ý tưởng chính (Duyệt DFS một lần duy nhất):
Mỗi đỉnh $u$ duy trì 2 thuộc tính:
- `dfn[u]`: Thứ tự duyệt DFS (chỉ số thời gian khám phá đầu tiên).
- `low[u]`: Chỉ số nhỏ nhất có thể đi tới từ cây con DFS gốc $u$.
Quy trình:
1. Duyệt DFS qua các đỉnh chưa thăm. Khi duyệt tới đỉnh $u$, đặt `dfn[u] = low[u] = timer++`, đồng thời đẩy $u$ vào một Stack tạm và đánh dấu nằm trong Stack.
2. Với mỗi đỉnh kề $v$ của $u$:
   - Nếu $v$ chưa thăm: gọi đệ quy DFS trên $v$, sau đó cập nhật `low[u] = min(low[u], low[v])`.
   - Nếu $v$ đã thăm và đang nằm trong Stack: cập nhật `low[u] = min(low[u], dfn[v])`.
3. Khi duyệt xong tất cả các nhánh từ $u$, nếu `dfn[u] == low[u]`:
   - Lần lượt lấy các đỉnh trong Stack ra ngoài cho đến khi lấy được chính đỉnh $u$.
   - Tập hợp các đỉnh vừa lấy ra tạo thành một thành phần liên thông mạnh (SCC) có gốc là $u$.

---

## Code triển khai (Java)
```java
import java.util.*;

public class Tarjan {
    private int timer = 0;
    private List<List<Integer>> adj;
    private int[] dfn, low;
    private boolean[] inStack;
    private Stack<Integer> stack;
    private List<List<Integer>> sccs;

    public List<List<Integer>> findSCCs(List<List<Integer>> adj) {
        int V = adj.size();
        this.adj = adj;
        dfn = new int[V];
        low = new int[V];
        inStack = new boolean[V];
        stack = new Stack<>();
        sccs = new ArrayList<>();
        Arrays.fill(dfn, -1);

        for (int i = 0; i < V; i++) {
            if (dfn[i] == -1) {
                dfs(i);
            }
        }
        return sccs;
    }

    private void dfs(int u) {
        dfn[u] = low[u] = timer++;
        stack.push(u);
        inStack[u] = true;

        for (int v : adj.get(u)) {
            if (dfn[v] == -1) {
                dfs(v);
                low[u] = Math.min(low[u], low[v]);
            } else if (inStack[v]) {
                low[u] = Math.min(low[u], dfn[v]);
            }
        }

        // Nếu u là đỉnh gốc của một SCC
        if (dfn[u] == low[u]) {
            List<Integer> scc = new ArrayList<>();
            while (true) {
                int v = stack.pop();
                inStack[v] = false;
                scc.add(v);
                if (u == v) break;
            }
            sccs.add(scc);
        }
    }
}
```

---

## Lưu ý
> [!important] Hiệu năng tối ưu
> Do chỉ sử dụng một lần duyệt DFS duy nhất, thuật toán Tarjan có độ phức tạp thời gian cực kỳ tối ưu là $O(V + E)$, giúp xử lý hiệu quả các đồ thị mạng xã hội hay các tập dữ liệu liên thông lớn.
