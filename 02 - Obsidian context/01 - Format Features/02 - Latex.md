# LaTeX trong Obsidian

---

## Định nghĩa
LaTeX trong Obsidian là cú pháp viết công thức toán học và biểu thức khoa học, được hỗ trợ bởi công cụ kết xuất MathJax/KaTeX.

---

## Tác dụng
- **Biểu diễn ký hiệu phức tạp:** Giúp viết các ký hiệu toán học, vật lý, hóa học một cách chính xác mà text thường không làm được.
- **Trình bày chuyên nghiệp:** Đảm bảo công thức toán học được hiển thị đẹp mắt, quy chuẩn.

---

## Bảng tham chiếu

### 1. Phép toán & Ký hiệu cơ bản

| Cú pháp LaTeX | Kết quả hiển thị | Ý nghĩa |
| :--- | :--- | :--- |
| `\frac{a}{b}` | $\frac{a}{b}$ | Phân số |
| `\sqrt{a}` | $\sqrt{a}$ | Căn bậc hai |
| `\sqrt[n]{a}` | $\sqrt[n]{a}$ | Căn bậc n |
| `x^{a}` | $x^{a}$ | Lũy thừa |
| `x_{i}` | $x_{i}$ | Chỉ số dưới (subscript) |
| `\sum_{a}^{b}` | $\sum_{a}^{b}$ | Tổng Sigma |
| `\prod_{a}^{b}` | $\prod_{a}^{b}$ | Tích Pi |
| `\int_{a}^{b}` | $\int_{a}^{b}$ | Tích phân |
| `\lim_{x \to \infty}` | $\lim_{x \to \infty}$ | Giới hạn |
| `\pm` | $\pm$ | Cộng trừ |
| `\approx` | $\approx$ | Xấp xỉ |
| `\ne` | $\ne$ | Không bằng / Khác |
| `\ge`, `\le` | $\ge$, $\le$ | Lớn hơn hoặc bằng, nhỏ hơn hoặc bằng |

### 2. Tập hợp & Logic học

| Cú pháp LaTeX | Kết quả hiển thị | Ý nghĩa |
| :--- | :--- | :--- |
| `\forall` | $\forall$ | Với mọi |
| `\exists` | $\exists$ | Tồn tại |
| `\in`, `\notin` | $\in$, $\notin$ | Thuộc, không thuộc |
| `\subset`, `\subseteq` | $\subset$, $\subseteq$ | Tập con, tập con hoặc bằng |
| `\cap`, `\cup` | $\cap$, $\cup$ | Giao, hợp |
| `\emptyset` | $\emptyset$ | Tập hợp rỗng |
| `\mathbb{N}`, `\mathbb{Z}` | $\mathbb{N}$, $\mathbb{Z}$ | Tập số tự nhiên, tập số nguyên |
| `\mathbb{Q}`, `\mathbb{R}` | $\mathbb{Q}$, $\mathbb{R}$ | Tập số hữu tỉ, tập số thực |

### 3. Mũi tên & Ký hiệu phân nhánh

| Cú pháp LaTeX | Kết quả hiển thị | Ý nghĩa |
| :--- | :--- | :--- |
| `\to`, `\leftarrow` | $\to$, $\leftarrow$ | Mũi tên chỉ phải, trái |
| `\leftrightarrow` | $\leftrightarrow$ | Mũi tên hai chiều |
| `\Rightarrow` | $\Rightarrow$ | Suy ra (Implies) |
| `\Leftarrow` | $\Leftarrow$ | Tương đương trái |
| `\Leftrightarrow` | $\Leftrightarrow$ | Tương đương hai chiều (If and only if) |

### 4. Định dạng khối & Trình bày nhiều dòng

| Kiểu môi trường | Mô tả |
| :--- | :--- |
| `\begin{aligned} ... \end{aligned}` | Căn lề các dòng công thức theo ký tự `&` |
| `\begin{cases} ... \end{cases}` | Viết hệ phương trình hoặc hàm số phân nhánh |
| `\begin{matrix} ... \end{matrix}` | Tạo ma trận cơ bản |
| `\begin{pmatrix} ... \end{pmatrix}` | Tạo ma trận bọc trong dấu ngoặc đơn `()` |
| `\begin{bmatrix} ... \end{bmatrix}` | Tạo ma trận bọc trong dấu ngoặc vuông `[]` |

---

## Ví dụ

### Công thức viết cùng dòng (Inline Math)
Sử dụng một cặp dấu `$` bao quanh công thức:
- Cú pháp: `Hàm số $f(x) = a^2 + b^2$ luôn có nghiệm.`
- Kết quả: Hàm số $f(x) = a^2 + b^2$ luôn có nghiệm.

### Công thức viết dạng khối (Block Math)
Sử dụng cặp dấu song song `$$` trên dòng riêng biệt:
- Cú pháp:
  ```latex
  $$
  f(x) = \begin{cases} 
  x^2 & \text{nếu } x \ge 0 \\ 
  -x  & \text{nếu } x < 0 
  \end{cases}
  $$
  ```
- Kết quả:
  $$
  f(x) = \begin{cases} 
  x^2 & \text{nếu } x \ge 0 \\ 
  -x  & \text{nếu } x < 0 
  \end{cases}
  $$

---

## Lưu ý
> [!caution] Lỗi cú pháp LaTeX thường gặp
> - **Không để khoảng trắng** ngay sau dấu `$` mở hoặc trước dấu `$` đóng cho Inline Math (Ví dụ: `$ x + y $` là sai, `$x+y$` là đúng).
> - Để hiển thị ký tự đặc biệt như `{` hay `}` trong LaTeX, phải thêm dấu gạch chéo ngược `\` phía trước (Ví dụ: `\{a, b\}` hiển thị $\{a, b\}$).
