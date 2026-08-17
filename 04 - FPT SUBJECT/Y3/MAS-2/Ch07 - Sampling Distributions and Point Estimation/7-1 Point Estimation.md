---
tags:
  - MAS291
  - Chapter7
  - PointEstimation
aliases:
  - Point Estimation
  - Ước lượng điểm
---

# 7.1 Ước Lượng Điểm (Point Estimation)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> **Ước lượng điểm (Point Estimation)** là phương pháp dùng một **giá trị đơn lẻ** (gọi là **ước lượng điểm** hay **estimate**) tính từ dữ liệu mẫu để ước lượng **tham số tổng thể** chưa biết.

### Ý nghĩa thống kê

- **Tham số (Parameter):** Đặc trưng của tổng thể — cố định nhưng chưa biết (ví dụ: $\mu$, $\sigma^2$, $p$).
- **Thống kê (Statistic):** Hàm của dữ liệu mẫu — được tính từ mẫu và là **biến ngẫu nhiên** (ví dụ: $\bar{X}$, $S^2$, $\hat{p}$).
- **Ước lượng viên (Estimator):** Công thức/quy tắc tính thống kê dùng để ước lượng tham số.
- **Ước lượng (Estimate):** Giá trị cụ thể của ước lượng viên khi áp dụng vào một mẫu cụ thể.

### Diễn giải trực quan

| Khái niệm | Ký hiệu | Ví dụ |
|:---------|:-------:|:------|
| Tham số (chưa biết) | $\mu$, $\sigma^2$, $p$ | Chiều cao trung bình thật của toàn bộ sinh viên |
| Ước lượng viên (công thức) | $\bar{X}$, $S^2$, $\hat{p}$ | Công thức tính trung bình mẫu |
| Ước lượng (giá trị cụ thể) | $\bar{x}$, $s^2$, $\hat{p}$ | $\bar{x} = 168.5$ cm từ mẫu cụ thể |

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $\theta$ | Tham số tổng thể chưa biết (Unknown Population Parameter) |
| $\hat{\theta}$ | Ước lượng viên của $\theta$ (Estimator of $\theta$) |
| $\mu$ | Trung bình tổng thể (Population Mean) |
| $\bar{X}$ | Trung bình mẫu — ước lượng viên của $\mu$ (Sample Mean — Estimator) |
| $\bar{x}$ | Giá trị trung bình mẫu cụ thể (Sample Mean — Estimate) |
| $\sigma^2$ | Phương sai tổng thể (Population Variance) |
| $S^2$ | Phương sai mẫu — ước lượng viên của $\sigma^2$ (Sample Variance — Estimator) |
| $p$ | Tỷ lệ tổng thể (Population Proportion) |
| $\hat{p}$ | Tỷ lệ mẫu — ước lượng viên của $p$ (Sample Proportion — Estimator) |
| $B(\hat{\theta})$ | Độ lệch (Bias): $B(\hat{\theta}) = E(\hat{\theta}) - \theta$ |
| $MSE(\hat{\theta})$ | Sai số bình phương trung bình (Mean Square Error) |

---

## 3. Phân loại và Công thức

### 3.1 Các ước lượng viên thường dùng

| Tham số $\theta$ | Ước lượng viên $\hat{\theta}$ | Công thức |
|:----------------:|:----------------------------:|:---------:|
| $\mu$ | $\bar{X}$ | $\bar{X} = \dfrac{1}{n}\sum_{i=1}^n X_i$ |
| $\sigma^2$ | $S^2$ | $S^2 = \dfrac{1}{n-1}\sum_{i=1}^n (X_i - \bar{X})^2$ |
| $\sigma$ | $S$ | $S = \sqrt{S^2}$ |
| $p$ | $\hat{p}$ | $\hat{p} = X/n$ (với $X$ = số "thành công") |

---

### 3.2 Tính chất của ước lượng viên tốt

#### (a) Không lệch (Unbiased)

Ước lượng viên $\hat{\theta}$ là **không lệch** nếu:

$$E(\hat{\theta}) = \theta$$

- $\bar{X}$ là ước lượng viên **không lệch** của $\mu$: $E(\bar{X}) = \mu$ ✓
- $S^2 = \dfrac{1}{n-1}\sum(X_i - \bar{X})^2$ là ước lượng viên **không lệch** của $\sigma^2$ ✓

> [!note]
> Tại sao mẫu số của $S^2$ là $n-1$ chứ không phải $n$? Vì dùng $n$ ở mẫu số cho ước lượng **lệch** — ước lượng thấp hơn $\sigma^2$ thật sự. Dùng $n-1$ (Hiệu chỉnh Bessel — Bessel's correction) cho ước lượng không lệch.

#### (b) Phương sai nhỏ nhất (Minimum Variance)

Trong số các ước lượng viên không lệch, ước lượng viên **hiệu quả nhất** là ước lượng có **phương sai nhỏ nhất**.

$$\text{Var}(\bar{X}) = \frac{\sigma^2}{n}$$

#### (c) Sai số bình phương trung bình (Mean Square Error — MSE)

$$MSE(\hat{\theta}) = \text{Var}(\hat{\theta}) + [B(\hat{\theta})]^2$$

Trong đó $B(\hat{\theta}) = E(\hat{\theta}) - \theta$ là **độ lệch (bias)**.

- Nếu ước lượng không lệch: $MSE(\hat{\theta}) = \text{Var}(\hat{\theta})$.
- MSE là thước đo tổng hợp: đánh đổi giữa lệch và phương sai.

#### (d) Nhất quán (Consistent)

Ước lượng viên $\hat{\theta}$ là **nhất quán** nếu khi $n \to \infty$, $\hat{\theta} \to \theta$ (hội tụ theo xác suất). Ví dụ: $\bar{X}$ nhất quán với $\mu$.

---

### 3.3 Sai số chuẩn (Standard Error)

**Sai số chuẩn (Standard Error — SE)** của ước lượng viên $\hat{\theta}$ là:

$$SE(\hat{\theta}) = \sqrt{\text{Var}(\hat{\theta})}$$

Ví dụ:

$$SE(\bar{X}) = \frac{\sigma}{\sqrt{n}} \quad \text{(hoặc xấp xỉ } \frac{s}{\sqrt{n}} \text{ khi } \sigma \text{ chưa biết)}$$

> [!note]
> Sai số chuẩn **giảm** khi tăng $n$. Đây là lý do tăng cỡ mẫu cải thiện độ chính xác ước lượng.

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** A random sample of **$n = 10$ students'** exam scores is: 72, 85, 90, 78, 88, 76, 83, 91, 69, 84. Compute the point estimates of the population mean $\mu$ and population variance $\sigma^2$.

**Tóm tắt bài toán:** Tính $\bar{x}$ và $s^2$ từ dữ liệu thô.

**Giải:**

**Bước 1:** Tính $\bar{x}$:

$$\bar{x} = \frac{72+85+90+78+88+76+83+91+69+84}{10} = \frac{816}{10} = 81.6$$

**Bước 2:** Tính $s^2$:

$$\sum (x_i - \bar{x})^2 = (72-81.6)^2 + (85-81.6)^2 + \ldots$$

| $x_i$ | $x_i - \bar{x}$ | $(x_i-\bar{x})^2$ |
|:-----:|:---------------:|:-----------------:|
| 72 | $-9.6$ | 92.16 |
| 85 | $+3.4$ | 11.56 |
| 90 | $+8.4$ | 70.56 |
| 78 | $-3.6$ | 12.96 |
| 88 | $+6.4$ | 40.96 |
| 76 | $-5.6$ | 31.36 |
| 83 | $+1.4$ | 1.96 |
| 91 | $+9.4$ | 88.36 |
| 69 | $-12.6$ | 158.76 |
| 84 | $+2.4$ | 5.76 |

$$\sum (x_i - \bar{x})^2 = 514.4$$

$$s^2 = \frac{514.4}{10-1} = \frac{514.4}{9} = 57.16$$

$$s = \sqrt{57.16} \approx 7.56$$

**Kết luận:** Ước lượng điểm của trung bình tổng thể là $\hat{\mu} = \bar{x} = 81.6$ điểm; ước lượng điểm của phương sai tổng thể là $\hat{\sigma}^2 = s^2 = 57.16$.

---

### Ví dụ 2 (Trung bình)

> **Exercise:** Explain why the sample variance uses $n-1$ in the denominator instead of $n$. If a sample of $n = 5$ values has $\sum x_i = 50$ and $\sum x_i^2 = 520$, compute: (a) $\bar{x}$, (b) $s^2$ using the computational formula, (c) the biased estimator $\tilde{\sigma}^2 = \dfrac{1}{n}\sum(x_i-\bar{x})^2$ and compare.

**Tóm tắt bài toán:** Giải thích lý do $n-1$ và so sánh $s^2$ với ước lượng lệch.

**Giải:**

**(a) Tính $\bar{x}$:**

$$\bar{x} = \frac{\sum x_i}{n} = \frac{50}{5} = 10$$

**(b) Công thức tính nhanh $s^2$:**

$$s^2 = \frac{\sum x_i^2 - n\bar{x}^2}{n-1} = \frac{520 - 5 \times 100}{4} = \frac{520 - 500}{4} = \frac{20}{4} = 5$$

**(c) Ước lượng lệch:**

$$\tilde{\sigma}^2 = \frac{n-1}{n} \times s^2 = \frac{4}{5} \times 5 = 4$$

**So sánh:** $s^2 = 5 > \tilde{\sigma}^2 = 4$ — ước lượng lệch **ước lượng thấp** phương sai tổng thể. Dùng $n-1$ ở mẫu số hiệu chỉnh sự lệch này.

**Giải thích lý do $n-1$:** Khi tính $\sum(x_i - \bar{x})^2$, ta thay $\mu$ bằng $\bar{x}$. Điều này "khóa" một bậc tự do vì $\sum(x_i - \bar{x}) = 0$ luôn đúng. Chỉ còn $n-1$ bậc tự do để ước lượng phương sai — chia cho $n-1$ bù đắp sự co rút này.

---

### Ví dụ 3 (Khó)

> **Exercise:** Three estimators of $\mu$ are proposed from a sample of $n$ observations:
> - $\hat{\mu}_1 = \bar{X}$ (sample mean)
> - $\hat{\mu}_2 = X_1$ (first observation only)
> - $\hat{\mu}_3 = \frac{X_1 + X_n}{2}$ (average of first and last)
>
> (a) Show that all three are unbiased for $\mu$.  
> (b) Compare their variances. Which is the best estimator and why?  
> (c) Calculate $MSE(\hat{\mu}_2)$ if these estimators are unbiased.

**Tóm tắt bài toán:** So sánh ba ước lượng viên không lệch về phương sai (hiệu quả).

**(a) Không lệch:**

$$E(\hat{\mu}_1) = E(\bar{X}) = \mu \quad \checkmark$$

$$E(\hat{\mu}_2) = E(X_1) = \mu \quad \checkmark \quad \text{(vì mẫu ngẫu nhiên)}$$

$$E(\hat{\mu}_3) = \frac{E(X_1) + E(X_n)}{2} = \frac{\mu + \mu}{2} = \mu \quad \checkmark$$

**Cả ba đều không lệch.**

**(b) Phương sai:**

$$\text{Var}(\hat{\mu}_1) = \text{Var}(\bar{X}) = \frac{\sigma^2}{n}$$

$$\text{Var}(\hat{\mu}_2) = \text{Var}(X_1) = \sigma^2$$

$$\text{Var}(\hat{\mu}_3) = \frac{1}{4}[\text{Var}(X_1) + \text{Var}(X_n)] = \frac{1}{4}[\sigma^2 + \sigma^2] = \frac{\sigma^2}{2}$$

So sánh: $\dfrac{\sigma^2}{n} \le \dfrac{\sigma^2}{2} \le \sigma^2$ (với $n \ge 2$).

**Kết luận:** $\hat{\mu}_1 = \bar{X}$ có phương sai nhỏ nhất — là ước lượng viên **hiệu quả nhất** trong ba cái.

**(c) $MSE(\hat{\mu}_2)$:**

Vì $\hat{\mu}_2$ không lệch: $B(\hat{\mu}_2) = 0$.

$$MSE(\hat{\mu}_2) = \text{Var}(\hat{\mu}_2) + [B(\hat{\mu}_2)]^2 = \sigma^2 + 0 = \sigma^2$$

**Kết luận:** Dùng chỉ một quan sát để ước lượng $\mu$ có $MSE = \sigma^2$ — lớn hơn nhiều so với $\bar{X}$ với $MSE = \sigma^2/n$. Đây là lý do tại sao tăng $n$ quan trọng.

> [!warning] Sai lầm thường gặp
> - **Dùng $n$ thay vì $n-1$** trong công thức $s^2$ — cho ước lượng lệch.
> - **Nhầm lẫn ước lượng viên và ước lượng**: $S^2$ (chữ in) là biến ngẫu nhiên (estimator); $s^2$ (chữ thường) là giá trị số cụ thể (estimate).
> - **Cho rằng ước lượng không lệch là tốt nhất**: Không lệch là cần thiết nhưng không đủ — cần kết hợp với phương sai nhỏ (tiêu chí $MSE$).
