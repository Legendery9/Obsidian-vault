---
tags:
  - MAS291
  - Chapter6
  - DescriptiveStatistics
  - BoxPlot
  - IQR
aliases:
  - Box Plot
  - Biểu đồ hộp
  - Box-and-Whisker Plot
---

# 6.4 Biểu Đồ Hộp (Box Plots)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> **Biểu đồ hộp (Box Plot** hay **Box-and-Whisker Plot)** là biểu đồ thống kê mô tả phân phối dữ liệu thông qua **5 số tóm tắt (Five-Number Summary)** và phát hiện **ngoại lệ (outliers)**.

### Ý nghĩa thống kê

- Thể hiện **vị trí trung tâm** (median), **độ phân tán** (IQR), và **hình dạng** (lệch hay đối xứng).
- Dễ dàng **so sánh nhiều nhóm** cạnh nhau.
- Phát hiện **ngoại lệ** một cách trực quan.

### Cấu trúc biểu đồ hộp

```
        |--whisker--|  [  Q1  |  median  |  Q3  ]  |--whisker--|  *outlier
Min hợp lệ          Q1                  Q3          Max hợp lệ
```

- **Hộp (Box):** Từ $Q_1$ đến $Q_3$, chứa **50% dữ liệu trung tâm**.
- **Đường median:** Đường nằm trong hộp tại $Q_2$.
- **Râu (Whiskers):** Kéo từ $Q_1$ đến Min hợp lệ (và từ $Q_3$ đến Max hợp lệ).
- **Dấu $*$ hoặc $\circ$:** Ngoại lệ, vẽ riêng ngoài râu.

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $Q_1$ | Tứ phân vị thứ nhất (First Quartile — 25th Percentile) |
| $Q_2$ | Trung vị (Median — 50th Percentile) |
| $Q_3$ | Tứ phân vị thứ ba (Third Quartile — 75th Percentile) |
| $IQR$ | Khoảng tứ phân vị (Interquartile Range): $IQR = Q_3 - Q_1$ |
| Lower Fence | Hàng rào dưới (Lower Fence): $Q_1 - 1.5 \times IQR$ |
| Upper Fence | Hàng rào trên (Upper Fence): $Q_3 + 1.5 \times IQR$ |

---

## 3. Phân loại và Công thức

### 3.1 Tóm tắt 5 số (Five-Number Summary)

$$\{Q_0, Q_1, Q_2, Q_3, Q_4\} = \{\text{Min}, Q_1, \text{Median}, Q_3, \text{Max}\}$$

### 3.2 Tính tứ phân vị — Phương pháp $(n+1)$

$$\text{Position}(Q_1) = \frac{n+1}{4} \qquad \text{Position}(Q_2) = \frac{n+1}{2} \qquad \text{Position}(Q_3) = \frac{3(n+1)}{4}$$

Nếu vị trí không phải số nguyên, dùng **nội suy tuyến tính**:

Ví dụ: Vị trí $= 3.5$ → giá trị = $x_{(3)} + 0.5 \times (x_{(4)} - x_{(3)})$

### 3.3 Phát hiện ngoại lệ

$$\text{Lower Fence} = Q_1 - 1.5 \times IQR$$

$$\text{Upper Fence} = Q_3 + 1.5 \times IQR$$

- Nếu $x_i < \text{Lower Fence}$ hoặc $x_i > \text{Upper Fence}$: **ngoại lệ (outlier)**.
- Râu dưới kéo đến: **Min hợp lệ** (giá trị nhỏ nhất ≥ Lower Fence).
- Râu trên kéo đến: **Max hợp lệ** (giá trị lớn nhất ≤ Upper Fence).

### 3.4 Đọc hình dạng phân phối từ boxplot

| Hình dạng | Dấu hiệu trên boxplot |
|:---------|:---------------------|
| Đối xứng | Median ở giữa hộp; hai râu gần bằng nhau |
| Lệch phải (Right-skewed) | Median lệch về trái; râu phải dài hơn |
| Lệch trái (Left-skewed) | Median lệch về phải; râu trái dài hơn |

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** The following data represent the scores of 11 students on a math exam (already sorted): 12, 15, 18, 20, 22, 25, 27, 30, 32, 35, 40. Compute the five-number summary, IQR, fences, and identify any outliers.

**Tóm tắt bài toán:** $n = 11$, tính tóm tắt 5 số và kiểm tra ngoại lệ.

**Giải:**

$$n = 11 \quad \Rightarrow \quad \text{Position}(Q_1) = \frac{12}{4} = 3 \quad \text{Position}(Q_2) = \frac{12}{2} = 6 \quad \text{Position}(Q_3) = \frac{36}{4} = 9$$

$$Q_1 = x_{(3)} = 18 \qquad Q_2 = x_{(6)} = 25 \qquad Q_3 = x_{(9)} = 32$$

$$IQR = 32 - 18 = 14$$

$$\text{Lower Fence} = 18 - 1.5 \times 14 = 18 - 21 = -3$$

$$\text{Upper Fence} = 32 + 1.5 \times 14 = 32 + 21 = 53$$

Không có giá trị nào ngoài $[-3, 53]$ → **Không có ngoại lệ**.

**Tóm tắt 5 số:** $\{12, 18, 25, 32, 40\}$

**Hình dạng:** Median = 25 ở gần giữa hộp [18, 32]; hai râu tương đối cân đối → phân phối **khá đối xứng**.

---

### Ví dụ 2 (Trung bình)

> **Exercise:** Monthly salary (in \$1000) of 10 employees: 3.5, 4.0, 4.2, 4.5, 4.8, 5.0, 5.3, 5.8, 6.2, 12.5. Construct the five-number summary, detect outliers, and describe the shape.

**Tóm tắt bài toán:** $n = 10$, có thể có ngoại lệ.

$$\text{Position}(Q_1) = \frac{11}{4} = 2.75 \Rightarrow Q_1 = 4.0 + 0.75(4.2 - 4.0) = 4.0 + 0.15 = 4.15$$

$$\text{Position}(Q_3) = \frac{33}{4} = 8.25 \Rightarrow Q_3 = 5.8 + 0.25(6.2 - 5.8) = 5.8 + 0.10 = 5.90$$

$$\text{Position}(Q_2) = 5.5 \Rightarrow Q_2 = \frac{4.8 + 5.0}{2} = 4.9$$

$$IQR = 5.90 - 4.15 = 1.75$$

$$\text{Upper Fence} = 5.90 + 1.5 \times 1.75 = 5.90 + 2.625 = 8.525$$

$$\text{Lower Fence} = 4.15 - 1.5 \times 1.75 = 4.15 - 2.625 = 1.525$$

Kiểm tra: $12.5 > 8.525$ → **$12.5$ là ngoại lệ** (một nhân viên lương rất cao).

**Tóm tắt 5 số:** $\{\text{Min}=3.5, Q_1=4.15, Q_2=4.9, Q_3=5.90, \text{Max hợp lệ}=6.2\}$, ngoại lệ: $12.5$.

**Hình dạng:** Lệch phải do ngoại lệ $12.5$. Median $4.9$ thấp hơn trung bình, phản ánh ảnh hưởng của ngoại lệ.

---

### Ví dụ 3 (Khó)

> **Exercise:** A quality engineer wants to compare the output (units/hour) of two production lines using boxplots. Line 1 ($n=12$): 45, 48, 52, 50, 47, 53, 55, 49, 51, 58, 46, 54. Line 2 ($n=12$): 38, 42, 65, 44, 41, 48, 43, 46, 39, 50, 63, 45.
>
> (a) Compute five-number summary for each.  
> (b) Identify outliers.  
> (c) Compare distributions.

**Giải:**

**Line 1 — Sắp xếp:** 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 58.

$$Q_1 = \frac{47+48}{2} = 47.5 \quad Q_2 = \frac{50+51}{2} = 50.5 \quad Q_3 = \frac{53+54}{2} = 53.5$$

$$IQR_1 = 53.5 - 47.5 = 6.0$$

$$\text{Fences}_1: [47.5 - 9, 53.5 + 9] = [38.5, 62.5] \quad \text{Không có ngoại lệ}$$

**Line 2 — Sắp xếp:** 38, 39, 41, 42, 43, 44, 45, 46, 48, 50, 63, 65.

$$Q_1 = \frac{41+42}{2} = 41.5 \quad Q_2 = \frac{44+45}{2} = 44.5 \quad Q_3 = \frac{48+50}{2} = 49.0$$

$$IQR_2 = 49.0 - 41.5 = 7.5$$

$$\text{Upper Fence}_2 = 49.0 + 11.25 = 60.25$$

$$\text{Lower Fence}_2 = 41.5 - 11.25 = 30.25$$

**Ngoại lệ Line 2:** $63 > 60.25$ và $65 > 60.25$ → **63 và 65 là ngoại lệ**.

**So sánh:**

| | Line 1 | Line 2 |
|:--|:------:|:------:|
| Min | 45 | 38 |
| $Q_1$ | 47.5 | 41.5 |
| Median | 50.5 | 44.5 |
| $Q_3$ | 53.5 | 49.0 |
| Max | 58 | 50 (hợp lệ) |
| Outliers | Không có | 63, 65 |
| $IQR$ | 6.0 | 7.5 |

**Kết luận:**
- **Line 1** có năng suất trung vị cao hơn ($50.5$ so với $44.5$) và ổn định hơn (ít ngoại lệ, IQR nhỏ hơn).
- **Line 2** có hai ngoại lệ cao đột xuất ($63, 65$) — có thể do sự kiện đặc biệt. Ngoài các ngoại lệ, Line 2 hoạt động **kém hơn và kém ổn định hơn** Line 1.

> [!warning] Sai lầm thường gặp
> - **Râu kéo đến Min/Max** chứ không đến Lower/Upper Fence — râu phải dừng ở giá trị hợp lệ cuối cùng.
> - **Quên nội suy** khi vị trí tứ phân vị không phải số nguyên.
> - **Nhầm "không có outlier" với "phân phối tốt"**: Không có ngoại lệ không nghĩa là không có vấn đề gì.
