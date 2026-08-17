---
tags:
  - MAS291
  - Chapter10
  - TwoSamples
  - TTest
  - ConfidenceInterval
aliases:
  - Difference in Means Unknown Variance
  - Welch t-test
  - Two-sample t-test
  - Suy diễn hiệu trung bình không biết phương sai
---

# 10.2 Suy Diễn về Hiệu Trung Bình — Không Biết Phương Sai (Inference on $\mu_1 - \mu_2$, Variances Unknown)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> Suy diễn về $\mu_1 - \mu_2$ khi **phương sai tổng thể chưa biết** — dùng phân phối **$t$**.
>
> Có hai trường hợp tùy theo phương sai bằng nhau hay không:
> 1. **Pooled t-test** ($\sigma_1^2 = \sigma_2^2$, Equal Variances Assumed)
> 2. **Welch's t-test** ($\sigma_1^2 \ne \sigma_2^2$, Unequal Variances)

### Điều kiện áp dụng

- Hai mẫu **độc lập** ngẫu nhiên.
- $\sigma_1^2$ và $\sigma_2^2$ **chưa biết**.
- Cả hai tổng thể chuẩn hoặc $n_1, n_2$ đủ lớn ($\ge 30$).

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $s_1^2, s_2^2$ | Phương sai mẫu (Sample Variances) |
| $s_p^2$ | Phương sai mẫu gộp (Pooled Sample Variance) |
| $df$ | Bậc tự do (Degrees of Freedom) |
| $\Delta_0$ | Hiệu trung bình giả định (Hypothesized Difference); thường $\Delta_0 = 0$ |

---

## 3. Phân loại và Công thức

### 3.1 Trường hợp 1 — Phương sai bằng nhau ($\sigma_1^2 = \sigma_2^2$): Pooled t-test

**Phương sai mẫu gộp (Pooled Sample Variance):**

$$s_p^2 = \frac{(n_1-1)s_1^2 + (n_2-1)s_2^2}{n_1 + n_2 - 2}$$

**Thống kê kiểm định:**

$$t_0 = \frac{(\bar{x}_1 - \bar{x}_2) - \Delta_0}{s_p\sqrt{1/n_1 + 1/n_2}}, \quad df = n_1 + n_2 - 2$$

**Khoảng tin cậy:**

$$(\bar{x}_1 - \bar{x}_2) \pm t_{\alpha/2,\,n_1+n_2-2} \cdot s_p\sqrt{\frac{1}{n_1} + \frac{1}{n_2}}$$

---

### 3.2 Trường hợp 2 — Phương sai KHÔNG bằng nhau ($\sigma_1^2 \ne \sigma_2^2$): Welch's t-test

**Thống kê kiểm định:**

$$t_0 = \frac{(\bar{x}_1 - \bar{x}_2) - \Delta_0}{\sqrt{s_1^2/n_1 + s_2^2/n_2}}$$

**Bậc tự do (công thức Welch-Satterthwaite):**

$$df = \frac{\left(\dfrac{s_1^2}{n_1} + \dfrac{s_2^2}{n_2}\right)^2}{\dfrac{(s_1^2/n_1)^2}{n_1-1} + \dfrac{(s_2^2/n_2)^2}{n_2-1}}$$

(Làm tròn xuống số nguyên gần nhất)

**Khoảng tin cậy:**

$$(\bar{x}_1 - \bar{x}_2) \pm t_{\alpha/2,\,df} \cdot \sqrt{\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}}$$

> [!tip] Nên dùng loại nào?
> - **Không chắc phương sai bằng nhau**: Dùng **Welch's t-test** — an toàn hơn, ít giả định hơn.
> - **Biết chắc phương sai bằng nhau** (qua kiểm định F hoặc lý thuyết): Dùng **Pooled t-test** — chính xác hơn khi giả định đúng.
> - Trong thực hành hiện đại: Welch's t-test được ưa chuộng hơn.

### 3.3 Miền bác bỏ (giống cho cả hai loại)

| Dạng $H_1$ | Miền bác bỏ |
|:----------:|:-----------:|
| $\mu_1 - \mu_2 \ne \Delta_0$ | $\|t_0\| > t_{\alpha/2,\,df}$ |
| $\mu_1 - \mu_2 > \Delta_0$ | $t_0 > t_{\alpha,\,df}$ |
| $\mu_1 - \mu_2 < \Delta_0$ | $t_0 < -t_{\alpha,\,df}$ |

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ — Pooled t-test)

> **Exercise:** Two groups of students are taught by different methods. Group A ($n_1 = 10$): $\bar{x}_1 = 78$, $s_1 = 6$. Group B ($n_2 = 12$): $\bar{x}_2 = 74$, $s_2 = 7$. Assume equal variances. At $\alpha = 0.05$, test whether the methods produce different results.

**Giải:**

$$H_0: \mu_1 - \mu_2 = 0 \qquad H_1: \mu_1 - \mu_2 \ne 0$$

**Phương sai gộp:**

$$s_p^2 = \frac{(10-1)(36) + (12-1)(49)}{10+12-2} = \frac{324 + 539}{20} = \frac{863}{20} = 43.15$$

$$s_p = \sqrt{43.15} = 6.57$$

**Thống kê kiểm định:**

$$t_0 = \frac{78 - 74}{6.57\sqrt{1/10 + 1/12}} = \frac{4}{6.57 \times 0.4282} = \frac{4}{2.813} = 1.422$$

**Miền bác bỏ:** $t_{\alpha/2,\,df} = t_{0.025,\,20} = 2.086$. Vì $|1.422| < 2.086$ → **Không bác bỏ $H_0$**.

**Kết luận:** Không có đủ bằng chứng thống kê để kết luận hai phương pháp giảng dạy cho kết quả khác nhau ở mức ý nghĩa $5\%$.

---

### Ví dụ 2 (Trung bình — Welch's t-test)

> **Exercise:** Compare fuel efficiency (mpg) of two car brands. Brand X: $n_1 = 15$, $\bar{x}_1 = 32.5$, $s_1 = 4.2$ mpg. Brand Y: $n_2 = 18$, $\bar{x}_2 = 29.8$, $s_2 = 6.1$ mpg. Do NOT assume equal variances. At $\alpha = 0.05$, test $H_1: \mu_1 > \mu_2$.

**Giải:**

$$SE = \sqrt{\frac{4.2^2}{15} + \frac{6.1^2}{18}} = \sqrt{\frac{17.64}{15} + \frac{37.21}{18}} = \sqrt{1.176 + 2.067} = \sqrt{3.243} = 1.801$$

$$t_0 = \frac{(32.5 - 29.8) - 0}{1.801} = \frac{2.7}{1.801} = 1.499$$

**Bậc tự do (Welch):**

$$df = \frac{(1.176 + 2.067)^2}{(1.176)^2/14 + (2.067)^2/17} = \frac{(3.243)^2}{0.09879 + 0.2512} = \frac{10.517}{0.3500} \approx 30.05 \Rightarrow df = 30$$

**Miền bác bỏ:** $t_{\alpha,\,30} = t_{0.05,\,30} = 1.697$. Vì $1.499 < 1.697$ → **Không bác bỏ $H_0$**.

**Tính $p$-value:** $P(t_{30} > 1.499) \approx 0.072 > 0.05$.

**Kết luận:** Không có đủ bằng chứng ở mức $5\%$ để kết luận Brand X tiết kiệm nhiên liệu hơn Brand Y.

---

### Ví dụ 3 (Khó — So sánh Pooled vs Welch)

> **Exercise:** Analyze tensile strength of two alloys. Alloy 1 ($n_1 = 12$): $\bar{x}_1 = 3250$ psi, $s_1 = 85$ psi. Alloy 2 ($n_2 = 10$): $\bar{x}_2 = 3190$ psi, $s_2 = 125$ psi. At $\alpha = 0.05$:
>
> (a) Perform a pooled t-test assuming equal variances.  
> (b) Perform Welch's t-test without assuming equal variances.  
> (c) Construct a 95% CI using Welch's method.

**(a) Pooled t-test ($df = 20$):**

$$s_p^2 = \frac{11 \times 7225 + 9 \times 15625}{20} = \frac{79475 + 140625}{20} = \frac{220100}{20} = 11005$$

$$s_p = 104.9, \qquad t_0 = \frac{60}{104.9\sqrt{1/12+1/10}} = \frac{60}{104.9 \times 0.4282} = \frac{60}{44.92} = 1.336$$

$t_{0.025,20} = 2.086 > 1.336$ → Không bác bỏ $H_0$.

**(b) Welch's t-test:**

$$SE = \sqrt{\frac{85^2}{12} + \frac{125^2}{10}} = \sqrt{601.6 + 1562.5} = \sqrt{2164.1} = 46.52$$

$$t_0 = \frac{60}{46.52} = 1.290$$

$$df = \frac{(601.6 + 1562.5)^2}{601.6^2/11 + 1562.5^2/9} = \frac{(2164.1)^2}{32872 + 271267} = \frac{4,682,929}{304139} \approx 15.4 \Rightarrow df = 15$$

$t_{0.025,15} = 2.131 > 1.290$ → Không bác bỏ $H_0$.

**(c) CI 95% (Welch):**

$$60 \pm 2.131 \times 46.52 = 60 \pm 99.2 = (-39.2, 159.2) \text{ psi}$$

Khoảng tin cậy chứa $0$ → xác nhận không bác bỏ $H_0$.

**So sánh kết quả:** Cả hai phương pháp đều cho cùng kết luận, nhưng Welch's t-test cho $df = 15$ (nhỏ hơn) và $t_{critical} = 2.131$ (lớn hơn) → khó bác bỏ $H_0$ hơn một chút. Đây là giá của việc không giả định phương sai bằng nhau.

> [!warning] Sai lầm thường gặp
> - **Dùng pooled khi phương sai rất khác nhau** ($s_1$ và $s_2$ chênh lệch nhiều): Kết quả sai lệch.
> - **Dùng $df = n_1 + n_2 - 2$ cho Welch's test**: Phải dùng công thức Welch-Satterthwaite.
> - **Nhầm khoảng tin cậy một phía với hai phía**: Một phía dùng $t_\alpha$; hai phía dùng $t_{\alpha/2}$.
