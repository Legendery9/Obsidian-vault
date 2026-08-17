---
tags:
  - MAS291
  - Chapter10
  - TwoSamples
  - Proportion
  - ZTest
aliases:
  - Two-proportion Z-test
  - Inference on Two Proportions
  - Kiểm định hai tỷ lệ
---

# 10.6 Suy Diễn về Hai Tỷ Lệ Tổng Thể (Inference on Two Population Proportions)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> Suy diễn về **hiệu hai tỷ lệ** $p_1 - p_2$ từ hai mẫu độc lập lớn — dùng phân phối **$Z$ xấp xỉ**.

### Điều kiện áp dụng (mẫu lớn)

- $n_1\hat{p}_1 \ge 5$, $n_1(1-\hat{p}_1) \ge 5$
- $n_2\hat{p}_2 \ge 5$, $n_2(1-\hat{p}_2) \ge 5$

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $p_1, p_2$ | Tỷ lệ tổng thể (Population Proportions) |
| $\hat{p}_1 = X_1/n_1$ | Tỷ lệ mẫu 1 (Sample Proportion 1) |
| $\hat{p}_2 = X_2/n_2$ | Tỷ lệ mẫu 2 (Sample Proportion 2) |
| $\hat{p}$ | Tỷ lệ mẫu gộp (Pooled Sample Proportion) |

---

## 3. Phân loại và Công thức

### 3.1 Kiểm định giả thuyết $H_0: p_1 = p_2$

**Tỷ lệ mẫu gộp (Pooled Proportion):**

$$\hat{p} = \frac{X_1 + X_2}{n_1 + n_2}$$

**Thống kê kiểm định:**

$$Z_0 = \frac{\hat{p}_1 - \hat{p}_2}{\sqrt{\hat{p}(1-\hat{p})\left(\dfrac{1}{n_1} + \dfrac{1}{n_2}\right)}}$$

> [!warning]
> Khi kiểm định $H_0: p_1 = p_2 = p$ (chưa biết), dùng **tỷ lệ gộp $\hat{p}$** trong mẫu số. Khi xây dựng CI, dùng $\hat{p}_1$ và $\hat{p}_2$ riêng biệt.

### 3.2 Khoảng tin cậy cho $p_1 - p_2$

$$(\hat{p}_1 - \hat{p}_2) \pm z_{\alpha/2}\sqrt{\frac{\hat{p}_1(1-\hat{p}_1)}{n_1} + \frac{\hat{p}_2(1-\hat{p}_2)}{n_2}}$$

### 3.3 Miền bác bỏ

| Dạng $H_1$ | Miền bác bỏ |
|:----------:|:-----------:|
| $p_1 \ne p_2$ | $\|Z_0\| > z_{\alpha/2}$ |
| $p_1 > p_2$ | $Z_0 > z_\alpha$ |
| $p_1 < p_2$ | $Z_0 < -z_\alpha$ |

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** Two factories produce light bulbs. Factory 1: $n_1 = 200$, $X_1 = 15$ defective. Factory 2: $n_2 = 250$, $X_2 = 25$ defective. At $\alpha = 0.05$, test whether defect rates differ.

**Giải:**

$$\hat{p}_1 = 15/200 = 0.075 \qquad \hat{p}_2 = 25/250 = 0.100$$

$$\hat{p} = \frac{15+25}{200+250} = \frac{40}{450} = 0.0889$$

**Kiểm tra điều kiện:** $n_1\hat{p}_1 = 15 \ge 5$ ✓, $n_2\hat{p}_2 = 25 \ge 5$ ✓

$$Z_0 = \frac{0.075 - 0.100}{\sqrt{0.0889 \times 0.9111 \times (1/200 + 1/250)}} = \frac{-0.025}{\sqrt{0.08096 \times 0.009}} = \frac{-0.025}{\sqrt{0.000729}} = \frac{-0.025}{0.02700} = -0.926$$

**Miền bác bỏ:** $|Z_0| = 0.926 < z_{0.025} = 1.960$ → **Không bác bỏ $H_0$**.

**Kết luận:** Không có đủ bằng chứng để kết luận tỷ lệ lỗi hai nhà máy **khác nhau** ở mức ý nghĩa $5\%$.

---

### Ví dụ 2 (Trung bình — CI)

> **Exercise:** Using data from Example 1, construct a 95% CI for $p_1 - p_2$.

**Giải:**

$$(\hat{p}_1 - \hat{p}_2) \pm z_{0.025}\sqrt{\frac{\hat{p}_1(1-\hat{p}_1)}{n_1} + \frac{\hat{p}_2(1-\hat{p}_2)}{n_2}}$$

$$= -0.025 \pm 1.960\sqrt{\frac{0.075 \times 0.925}{200} + \frac{0.100 \times 0.900}{250}}$$

$$= -0.025 \pm 1.960\sqrt{0.000347 + 0.000360}$$

$$= -0.025 \pm 1.960 \times 0.02659 = -0.025 \pm 0.0521$$

$$CI = (-0.077, 0.027)$$

Khoảng tin cậy chứa $0$ → phù hợp với kết luận không bác bỏ $H_0$.

---

### Ví dụ 3 (Khó)

> **Exercise:** A pharmaceutical company claims its new drug has a higher success rate than the standard treatment. Standard: $n_1 = 150$, $X_1 = 105$ successes. New drug: $n_2 = 180$, $X_2 = 140$ successes. At $\alpha = 0.01$, test $H_1: p_2 > p_1$.

**Giải:**

$$\hat{p}_1 = 105/150 = 0.700 \qquad \hat{p}_2 = 140/180 = 0.778$$

$$\hat{p} = \frac{105+140}{150+180} = \frac{245}{330} = 0.742$$

**Kiểm tra điều kiện:** $n_1\hat{p}_1 = 105 \ge 5$ ✓, $n_2\hat{p}_2 = 140 \ge 5$ ✓

$$Z_0 = \frac{0.700 - 0.778}{\sqrt{0.742 \times 0.258 \times (1/150 + 1/180)}} = \frac{-0.078}{\sqrt{0.1914 \times 0.01222}} = \frac{-0.078}{\sqrt{0.002339}} = \frac{-0.078}{0.04837} = -1.613$$

**Giả thuyết $H_1: p_2 > p_1$** tương đương $H_1: p_1 - p_2 < 0$:

**Miền bác bỏ:** $Z_0 < -z_{0.01} = -2.326$. Vì $-1.613 > -2.326$ → **Không bác bỏ $H_0$** ở $\alpha = 0.01$.

**Tính $p$-value:** $P(Z < -1.613) \approx 0.053$.

**Kết luận:** $p\text{-value} = 0.053 > \alpha = 0.01$ → Không có đủ bằng chứng ở mức $1\%$ để kết luận thuốc mới có tỷ lệ thành công cao hơn.

> [!note]
> Nếu dùng $\alpha = 0.05$: vẫn không bác bỏ vì $0.053 > 0.05$. Kết quả rất gần biên — cần cỡ mẫu lớn hơn để có kết luận rõ ràng hơn.

> [!warning] Sai lầm thường gặp
> - **Dùng $\hat{p}_1, \hat{p}_2$ riêng biệt khi kiểm định**: Phải dùng tỷ lệ gộp $\hat{p}$ trong mẫu số của $Z_0$.
> - **Nhầm khi xây dựng CI**: CI dùng $\hat{p}_1$ và $\hat{p}_2$ riêng (không gộp).
> - **Không kiểm tra điều kiện mẫu lớn** trước khi áp dụng xấp xỉ chuẩn.
