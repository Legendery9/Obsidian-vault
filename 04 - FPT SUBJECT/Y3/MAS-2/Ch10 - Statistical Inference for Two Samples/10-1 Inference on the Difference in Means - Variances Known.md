---
tags:
  - MAS291
  - Chapter10
  - TwoSamples
  - ZTest
  - ConfidenceInterval
aliases:
  - Difference in Means Known Variance
  - Suy diễn hiệu trung bình biết phương sai
---

# 10.1 Suy Diễn về Hiệu Trung Bình — Biết Phương Sai (Inference on $\mu_1 - \mu_2$, Variances Known)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> Suy diễn về $\mu_1 - \mu_2$ khi **cả hai phương sai tổng thể $\sigma_1^2$ và $\sigma_2^2$ đã biết** — dùng phân phối **$Z$ chuẩn**.

### Điều kiện áp dụng

- Hai mẫu **độc lập** ngẫu nhiên.
- $\sigma_1^2$ và $\sigma_2^2$ **đã biết**.
- Cả hai tổng thể chuẩn, **hoặc** $n_1 \ge 30$ và $n_2 \ge 30$.

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $\mu_1, \mu_2$ | Trung bình tổng thể 1 và 2 (Population Means) |
| $\sigma_1^2, \sigma_2^2$ | Phương sai tổng thể đã biết (Known Population Variances) |
| $n_1, n_2$ | Cỡ mẫu (Sample Sizes) |
| $\bar{X}_1, \bar{X}_2$ | Trung bình mẫu (Sample Means) |
| $\Delta_0$ | Hiệu trung bình giả định (Hypothesized Difference); thường $\Delta_0 = 0$ |
| $Z_0$ | Giá trị thống kê kiểm định Z (Z Test Statistic) |

---

## 3. Phân loại và Công thức

### 3.1 Phân phối mẫu của $\bar{X}_1 - \bar{X}_2$

$$\bar{X}_1 - \bar{X}_2 \sim N\!\left(\mu_1 - \mu_2,\; \frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}\right)$$

### 3.2 Kiểm định giả thuyết (Z-test)

**Thống kê kiểm định:**

$$Z_0 = \frac{(\bar{x}_1 - \bar{x}_2) - \Delta_0}{\sqrt{\sigma_1^2/n_1 + \sigma_2^2/n_2}}$$

**Miền bác bỏ:**

|          Dạng $H_1$          |       Miền bác bỏ        |  $p$-value   |
| :--------------------------: | :----------------------: | :----------: |
| $\mu_1 - \mu_2 \ne \Delta_0$ | $\|Z_0\| > z_{\alpha/2}$ | $2P(Z >Z_0)$ |
|  $\mu_1 - \mu_2 > \Delta_0$  |     $Z_0 > z_\alpha$     | $P(Z > Z_0)$ |
|  $\mu_1 - \mu_2 < \Delta_0$  |    $Z_0 < -z_\alpha$     | $P(Z < Z_0)$ |

### 3.3 Khoảng tin cậy (Z-interval)

**Khoảng tin cậy $100(1-\alpha)\%$ hai phía cho $\mu_1 - \mu_2$:**

$$(\bar{x}_1 - \bar{x}_2) \pm z_{\alpha/2}\sqrt{\frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}}$$

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** Two types of light bulbs are tested. Type A: $n_1 = 50$, $\bar{x}_1 = 1200$ hours, $\sigma_1 = 100$ hours. Type B: $n_2 = 50$, $\bar{x}_2 = 1150$ hours, $\sigma_2 = 120$ hours. At $\alpha = 0.05$, test whether the mean lifetimes differ.

**Giải:**

$$H_0: \mu_1 - \mu_2 = 0 \qquad H_1: \mu_1 - \mu_2 \ne 0$$

$$Z_0 = \frac{(1200 - 1150) - 0}{\sqrt{100^2/50 + 120^2/50}} = \frac{50}{\sqrt{200 + 288}} = \frac{50}{\sqrt{488}} = \frac{50}{22.09} \approx 2.263$$

$z_{\alpha/2} = z_{0.025} = 1.960$. Vì $|Z_0| = 2.263 > 1.960$ → **Bác bỏ $H_0$**.

**Tính $p$-value:** $p = 2P(Z > 2.263) = 2 \times 0.0118 = 0.024$.

**Kết luận:** Có đủ bằng chứng thống kê ($p = 0.024 < 0.05$) để kết luận tuổi thọ trung bình hai loại bóng đèn **khác nhau**.

---

### Ví dụ 2 (Trung bình)

> **Exercise:** Using the data from Example 1, construct a 95% confidence interval for $\mu_1 - \mu_2$.

**Giải:**

$$(\bar{x}_1 - \bar{x}_2) \pm z_{\alpha/2}\sqrt{\frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}} = 50 \pm 1.960 \times 22.09 = 50 \pm 43.30 = (6.70, 93.30)$$

**Kết luận:** Chúng ta tin tưởng 95% rằng loại A có tuổi thọ trung bình **cao hơn loại B từ 6.7 đến 93.3 giờ**.

Vì khoảng tin cậy **không chứa 0** → xác nhận kết quả kiểm định: hai loại bóng khác nhau có ý nghĩa thống kê.

---

### Ví dụ 3 (Khó)

> **Exercise:** A researcher compares exam scores between two universities. University 1: $n_1 = 40$, $\bar{x}_1 = 72$, $\sigma_1 = 8$. University 2: $n_2 = 35$, $\bar{x}_2 = 75$, $\sigma_2 = 10$. At $\alpha = 0.01$:
>
> (a) Test $H_1: \mu_2 > \mu_1$ (one-tailed).  
> (b) Compute a 99% CI for $\mu_1 - \mu_2$.  
> (c) Interpret the relationship between (a) and (b).

**Giải:**

$$SE = \sqrt{\frac{64}{40} + \frac{100}{35}} = \sqrt{1.6 + 2.857} = \sqrt{4.457} = 2.111$$

**(a) Kiểm định một phía phải:** $H_0: \mu_1 - \mu_2 = 0$, $H_1: \mu_1 - \mu_2 < 0$ (tức là $\mu_2 > \mu_1$):

$$Z_0 = \frac{(72 - 75) - 0}{2.111} = \frac{-3}{2.111} = -1.421$$

Miền bác bỏ: $Z_0 < -z_{0.01} = -2.326$. Vì $-1.421 > -2.326$ → **Không bác bỏ $H_0$** ở $\alpha = 0.01$.

**(b) CI 99% hai phía:**

$$72 - 75 \pm 2.576 \times 2.111 = -3 \pm 5.438 = (-8.44, 2.44)$$

**(c) Diễn giải:**

Khoảng tin cậy 99% $(-8.44, 2.44)$ **chứa 0** → phù hợp với kết luận không bác bỏ $H_0$ ở mức ý nghĩa $1\%$. Không có đủ bằng chứng ở mức $1\%$ để kết luận University 2 có điểm cao hơn.

> [!note]
> Nếu dùng $\alpha = 0.05$ (one-tailed): $-1.421 < -1.645$? Không → vẫn không bác bỏ $H_0$. $p$-value $= P(Z < -1.421) \approx 0.078 > 0.05$.

> [!warning] Sai lầm thường gặp
> - **Dùng t-test khi $\sigma$ đã biết**: Khi $\sigma_1, \sigma_2$ đã biết, luôn dùng Z-test (không phải t-test).
> - **Nhầm $\sigma^2$ với $s^2$**: Ký hiệu $\sigma^2$ = phương sai **tổng thể đã biết**; $s^2$ = phương sai mẫu.
> - **Sai chiều kiểm định**: Kiểm tra kỹ $H_1$ để biết kiểm định phía phải, trái, hay hai phía.
