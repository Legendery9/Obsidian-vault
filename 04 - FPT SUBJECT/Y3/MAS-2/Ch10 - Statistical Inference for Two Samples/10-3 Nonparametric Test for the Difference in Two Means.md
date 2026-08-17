---
tags:
  - MAS291
  - Chapter10
  - NonParametric
aliases:
  - Nonparametric Test Two Means
  - Wilcoxon Rank-Sum Test
---

# 10.3 Kiểm Định Phi Tham Số cho Hiệu Hai Trung Bình (Nonparametric Test for Difference in Two Means)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> Khi điều kiện tổng thể chuẩn **không đáp ứng** và cỡ mẫu nhỏ, có thể dùng **kiểm định phi tham số (nonparametric test)** để so sánh hai vị trí trung tâm mà không cần giả định phân phối.

### Phương pháp phổ biến nhất

**Kiểm định Wilcoxon Rank-Sum (Mann-Whitney U Test)** — kiểm định dựa trên thứ hạng thay vì giá trị thực.

### Khi nào dùng phi tham số?

- Tổng thể **không chuẩn** và $n$ nhỏ.
- Dữ liệu dạng **thứ tự (ordinal)**.
- Có **ngoại lệ** ảnh hưởng lớn đến t-test.

---

## 2. Công thức Wilcoxon Rank-Sum

1. **Kết hợp** hai mẫu và **xếp hạng** từ nhỏ đến lớn ($1$ đến $n_1+n_2$).
2. **Tính tổng thứ hạng** của mẫu có kích thước nhỏ hơn: $W$.
3. **Giá trị kỳ vọng và phương sai** của $W$ (khi $H_0$ đúng):

$$\mu_W = \frac{n_1(n_1+n_2+1)}{2} \qquad \sigma_W^2 = \frac{n_1 n_2 (n_1+n_2+1)}{12}$$

4. Với mẫu lớn ($n_1, n_2 \ge 8$), xấp xỉ chuẩn:

$$Z = \frac{W - \mu_W}{\sigma_W} \approx N(0,1)$$

---

## 3. Ví dụ minh họa

> **Exercise:** Sample A: 12, 18, 15, 20, 14. Sample B: 22, 25, 19, 28, 21, 24. At $\alpha = 0.05$, test whether the two samples come from populations with the same location.

**Giải:**

**Kết hợp và xếp hạng** (tổng cộng $n = 11$):

| Giá trị | 12 | 14 | 15 | 18 | 19 | 20 | 21 | 22 | 24 | 25 | 28 |
|:-------:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| Hạng | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |
| Nhóm | A | A | A | A | B | A | B | B | B | B | B |

**Tổng hạng của A** ($n_1 = 5$): $W = 1+2+3+4+6 = 16$

$$\mu_W = \frac{5(11+1)}{2} = 30 \qquad \sigma_W^2 = \frac{5 \times 6 \times 12}{12} = 30 \Rightarrow \sigma_W = 5.477$$

$$Z = \frac{16 - 30}{5.477} = \frac{-14}{5.477} = -2.556$$

$p\text{-value} = 2P(Z < -2.556) = 2 \times 0.0053 = 0.0106 < 0.05$ → **Bác bỏ $H_0$**.

**Kết luận:** Có đủ bằng chứng thống kê để kết luận hai mẫu đến từ các tổng thể có vị trí trung tâm **khác nhau**.

> [!note]
> Đây chỉ là tóm tắt cơ bản. Kiểm định phi tham số là chủ đề nâng cao không thường xuất hiện trong đề thi MAS291 cơ bản.
