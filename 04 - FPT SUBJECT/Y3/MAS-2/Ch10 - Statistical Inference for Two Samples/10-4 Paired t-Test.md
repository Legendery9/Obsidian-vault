---
tags:
  - MAS291
  - Chapter10
  - TwoSamples
  - PairedTTest
aliases:
  - Paired t-test
  - Kiểm định t ghép cặp
  - Matched Pairs
---

# 10.4 Kiểm Định t Ghép Cặp (Paired t-Test)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> **Kiểm định t ghép cặp (Paired t-test)** được dùng khi hai mẫu **không độc lập** mà được ghép theo cặp — ví dụ: đo cùng một đối tượng trước và sau can thiệp.

### Ý nghĩa thống kê

Thay vì so sánh hai mẫu trực tiếp, ta tính **hiệu trong mỗi cặp** $d_i = x_{i1} - x_{i2}$ và kiểm định về $\mu_D = \mu_1 - \mu_2$. Điều này **loại bỏ biến động giữa các đối tượng**, tăng độ nhạy.

### So sánh với Two-sample t-test

| | Paired t-test | Two-sample t-test |
|:--|:--:|:--:|
| Cấu trúc mẫu | Ghép cặp (correlated) | Độc lập |
| Biến số phân tích | $d_i = x_{i1} - x_{i2}$ | $\bar{x}_1 - \bar{x}_2$ |
| Bậc tự do | $n - 1$ | $n_1 + n_2 - 2$ hoặc Welch |
| Hiệu quả khi | Có tương quan cao giữa cặp | Hai mẫu thực sự độc lập |

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $d_i = x_{i1} - x_{i2}$ | Hiệu trong cặp thứ $i$ (Paired Difference) |
| $n$ | Số cặp (Number of Pairs) |
| $\bar{d}$ | Trung bình các hiệu (Mean of Differences) |
| $s_d$ | Độ lệch chuẩn các hiệu (Standard Deviation of Differences) |
| $\mu_D$ | Hiệu trung bình tổng thể (True Mean Difference) |
| $\Delta_0$ | Hiệu giả định (Hypothesized Difference); thường $\Delta_0 = 0$ |

---

## 3. Phân loại và Công thức

### 3.1 Thống kê tóm tắt các hiệu

$$\bar{d} = \frac{1}{n}\sum_{i=1}^n d_i \qquad s_d = \sqrt{\frac{\sum(d_i - \bar{d})^2}{n-1}}$$

### 3.2 Kiểm định giả thuyết (Paired t-test)

**Thống kê kiểm định:**

$$t_0 = \frac{\bar{d} - \Delta_0}{s_d/\sqrt{n}}, \quad df = n-1$$

**Miền bác bỏ:**

| Dạng $H_1$ | Miền bác bỏ |
|:----------:|:-----------:|
| $\mu_D \ne \Delta_0$ | $\|t_0\| > t_{\alpha/2,\,n-1}$ |
| $\mu_D > \Delta_0$ | $t_0 > t_{\alpha,\,n-1}$ |
| $\mu_D < \Delta_0$ | $t_0 < -t_{\alpha,\,n-1}$ |

### 3.3 Khoảng tin cậy cho $\mu_D$

$$\bar{d} \pm t_{\alpha/2,\,n-1} \cdot \frac{s_d}{\sqrt{n}}$$

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** A researcher tests whether a new training program improves performance. 8 employees are tested before and after the program:
>
> | Employee | Before | After |
> |:--------:|:------:|:-----:|
> | 1 | 75 | 80 |
> | 2 | 68 | 72 |
> | 3 | 82 | 85 |
> | 4 | 77 | 78 |
> | 5 | 70 | 76 |
> | 6 | 85 | 89 |
> | 7 | 73 | 79 |
> | 8 | 80 | 84 |
>
> At $\alpha = 0.05$, test whether the program improves performance (one-tailed).

**Giải:**

**Tính $d_i = \text{After} - \text{Before}$:**

$d_i$: 5, 4, 3, 1, 6, 4, 6, 4

$$\bar{d} = \frac{5+4+3+1+6+4+6+4}{8} = \frac{33}{8} = 4.125$$

$$s_d = \sqrt{\frac{\sum(d_i - 4.125)^2}{7}} = \sqrt{\frac{(0.875)^2 + (-0.125)^2 + \ldots}{7}}$$

$\sum(d_i - \bar{d})^2 = 0.765 + 0.015 + 1.266 + 9.765 + 3.515 + 0.015 + 3.515 + 0.015 = 18.875$

$$s_d = \sqrt{18.875/7} = \sqrt{2.696} = 1.642$$

**Giả thuyết:**

$$H_0: \mu_D = 0 \qquad H_1: \mu_D > 0 \quad \text{(chương trình cải thiện hiệu suất)}$$

**Thống kê kiểm định:**

$$t_0 = \frac{4.125 - 0}{1.642/\sqrt{8}} = \frac{4.125}{0.5806} = 7.105$$

**Miền bác bỏ:** $t_{0.05,\,7} = 1.895$. Vì $7.105 > 1.895$ → **Bác bỏ $H_0$**.

**Kết luận:** Có đủ bằng chứng thống kê để kết luận **chương trình đào tạo cải thiện hiệu suất** ở mức ý nghĩa $5\%$.

---

### Ví dụ 2 (Trung bình)

> **Exercise:** Using the data from Example 1, construct a 95% CI for the mean improvement $\mu_D$.

**Giải:**

$$\bar{d} \pm t_{0.025,\,7} \cdot \frac{s_d}{\sqrt{n}} = 4.125 \pm 2.365 \times \frac{1.642}{\sqrt{8}} = 4.125 \pm 2.365 \times 0.5806 = 4.125 \pm 1.373$$

$$CI = (2.75, 5.50)$$

**Kết luận:** Chúng ta tin tưởng 95% rằng chương trình đào tạo cải thiện hiệu suất trung bình **từ 2.75 đến 5.50 điểm**.

---

### Ví dụ 3 (Khó)

> **Exercise:** A quality engineer measures the diameter (mm) of 10 parts using two different gauges to check calibration:
>
> | Part | Gauge A | Gauge B | $d_i = A - B$ |
> |:----:|:-------:|:-------:|:-------------:|
> | 1 | 25.12 | 25.10 | +0.02 |
> | 2 | 25.08 | 25.11 | −0.03 |
> | 3 | 25.15 | 25.13 | +0.02 |
> | 4 | 25.10 | 25.09 | +0.01 |
> | 5 | 25.11 | 25.12 | −0.01 |
> | 6 | 25.14 | 25.13 | +0.01 |
> | 7 | 25.09 | 25.10 | −0.01 |
> | 8 | 25.13 | 25.11 | +0.02 |
> | 9 | 25.12 | 25.14 | −0.02 |
> | 10 | 25.11 | 25.10 | +0.01 |
>
> At $\alpha = 0.05$, test whether the two gauges give **different** readings on average.

**Giải:**

$$d_i: +0.02, -0.03, +0.02, +0.01, -0.01, +0.01, -0.01, +0.02, -0.02, +0.01$$

$$\bar{d} = \frac{0.02 - 0.03 + 0.02 + 0.01 - 0.01 + 0.01 - 0.01 + 0.02 - 0.02 + 0.01}{10} = \frac{0.02}{10} = 0.002 \text{ mm}$$

$$\sum(d_i - 0.002)^2 = (0.018)^2 + (-0.032)^2 + (0.018)^2 + (0.008)^2 + (-0.012)^2 + \ldots$$

$= 0.000324 + 0.001024 + 0.000324 + 0.000064 + 0.000144 + 0.000064 + 0.000144 + 0.000324 + 0.000484 + 0.000064 = 0.002960$

$$s_d = \sqrt{0.002960/9} = \sqrt{0.000329} = 0.01814 \text{ mm}$$

**Giả thuyết:**

$$H_0: \mu_D = 0 \qquad H_1: \mu_D \ne 0 \quad \text{(hai phía)}$$

**Thống kê kiểm định:**

$$t_0 = \frac{0.002}{0.01814/\sqrt{10}} = \frac{0.002}{0.005736} = 0.349$$

**Miền bác bỏ:** $t_{0.025,\,9} = 2.262$. Vì $|0.349| < 2.262$ → **Không bác bỏ $H_0$**.

**Kết luận:** Không có đủ bằng chứng thống kê để kết luận hai đồng hồ đo cho kết quả **khác nhau có ý nghĩa thống kê** ở mức $5\%$. Hai dụng cụ đo xấp xỉ hiệu chỉnh giống nhau.

> [!warning] Sai lầm thường gặp
> - **Dùng two-sample t-test thay paired t-test**: Khi dữ liệu ghép cặp (trước-sau, so sánh cùng đối tượng), phải dùng paired t-test.
> - **Nhầm $\mu_D > 0$ với $\mu_2 > \mu_1$**: Phụ thuộc vào định nghĩa $d_i = x_1 - x_2$ hay $x_2 - x_1$.
> - **Bậc tự do là $n-1$ chứ không phải $n_1+n_2-2$**: Paired t-test chỉ có $n$ cặp.
