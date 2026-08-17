---
tags:
  - MAS291
  - Chapter7
  - PointEstimation
  - UnbiasedEstimator
  - MSE
aliases:
  - General Concepts Point Estimation
  - Khái niệm chung ước lượng điểm
---

# 7.3 Các Khái Niệm Chung về Ước Lượng Điểm (General Concepts of Point Estimation)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> Phần này xây dựng **hệ thống tiêu chí đánh giá** chất lượng của ước lượng viên: tính không lệch, hiệu quả, và nhất quán.

### Ý nghĩa thống kê

- Có nhiều ước lượng viên khác nhau cho cùng một tham số — cần tiêu chí để chọn ước lượng viên **tốt nhất**.
- Ba tiêu chí chính: **Không lệch (Unbiased)**, **Hiệu quả (Efficient)**, **Nhất quán (Consistent)**.

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $\theta$ | Tham số tổng thể (Parameter) |
| $\hat{\theta}$ | Ước lượng viên (Estimator) |
| $B(\hat{\theta})$ | Độ lệch (Bias): $B(\hat{\theta}) = E(\hat{\theta}) - \theta$ |
| $MSE(\hat{\theta})$ | Sai số bình phương trung bình (Mean Square Error) |
| $\text{Var}(\hat{\theta})$ | Phương sai của ước lượng viên (Variance of Estimator) |
| $CRLB$ | Cận Cramér-Rao (Cramér-Rao Lower Bound) |
| $e(\hat{\theta}_1, \hat{\theta}_2)$ | Hiệu quả tương đối (Relative Efficiency) |

---

## 3. Phân loại và Công thức

### 3.1 Không lệch (Unbiasedness)

$$B(\hat{\theta}) = E(\hat{\theta}) - \theta = 0 \quad \Leftrightarrow \quad E(\hat{\theta}) = \theta$$

**Ví dụ:**
- $E(\bar{X}) = \mu$ → $\bar{X}$ không lệch cho $\mu$ ✓
- $E(S^2) = \sigma^2$ với $S^2 = \dfrac{1}{n-1}\sum(X_i-\bar{X})^2$ → $S^2$ không lệch cho $\sigma^2$ ✓
- $E\!\left(\dfrac{1}{n}\sum(X_i-\bar{X})^2\right) = \dfrac{n-1}{n}\sigma^2 \ne \sigma^2$ → ước lượng lệch ✗

---

### 3.2 Hiệu quả tương đối (Relative Efficiency)

Với hai ước lượng viên không lệch $\hat{\theta}_1$ và $\hat{\theta}_2$:

$$e(\hat{\theta}_1, \hat{\theta}_2) = \frac{\text{Var}(\hat{\theta}_2)}{\text{Var}(\hat{\theta}_1)}$$

- Nếu $e > 1$: $\hat{\theta}_1$ hiệu quả hơn $\hat{\theta}_2$ (phương sai nhỏ hơn).
- Nếu $e < 1$: $\hat{\theta}_2$ hiệu quả hơn.

---

### 3.3 Sai số bình phương trung bình (MSE)

$$MSE(\hat{\theta}) = E[(\hat{\theta} - \theta)^2] = \text{Var}(\hat{\theta}) + [B(\hat{\theta})]^2$$

- MSE đo **tổng sai số**: biến động (variance) + lệch (bias).
- Với ước lượng không lệch: $MSE(\hat{\theta}) = \text{Var}(\hat{\theta})$.

> [!note] Đánh đổi Bias-Variance
> Đôi khi một ước lượng **lệch một chút** nhưng có **phương sai rất nhỏ** có thể có $MSE$ tổng thể **nhỏ hơn** ước lượng không lệch có phương sai lớn. Đây là đánh đổi bias-variance cổ điển.

---

### 3.4 Nhất quán (Consistency)

Ước lượng viên $\hat{\theta}_n$ là **nhất quán** nếu với mọi $\epsilon > 0$:

$$\lim_{n \to \infty} P(|\hat{\theta}_n - \theta| > \epsilon) = 0$$

Ký hiệu: $\hat{\theta}_n \xrightarrow{p} \theta$ (hội tụ theo xác suất).

**Điều kiện đủ:** Nếu $E(\hat{\theta}_n) \to \theta$ và $\text{Var}(\hat{\theta}_n) \to 0$ khi $n \to \infty$, thì $\hat{\theta}_n$ nhất quán.

Ví dụ: $\bar{X}$ nhất quán cho $\mu$ vì $\text{Var}(\bar{X}) = \sigma^2/n \to 0$ khi $n \to \infty$.

---

### 3.5 Tóm tắt tiêu chí ước lượng viên

| Tiêu chí | Định nghĩa | Ký hiệu kiểm tra |
|:---------|:----------|:----------------:|
| Không lệch | $E(\hat{\theta}) = \theta$ | $B(\hat{\theta}) = 0$ |
| Hiệu quả | Phương sai nhỏ nhất trong lớp không lệch | $\text{Var}(\hat{\theta})$ nhỏ nhất |
| Nhất quán | $\hat{\theta}_n \xrightarrow{p} \theta$ khi $n \to \infty$ | $\text{Var} \to 0$ và $B \to 0$ |
| Tối thiểu MSE | MSE nhỏ nhất | $MSE(\hat{\theta})$ nhỏ nhất |

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** Show that the sample mean $\bar{X}$ is an unbiased estimator of the population mean $\mu$ and compute its MSE.

**Giải:**

**Không lệch:**

$$E(\bar{X}) = E\!\left(\frac{1}{n}\sum_{i=1}^n X_i\right) = \frac{1}{n}\sum_{i=1}^n E(X_i) = \frac{1}{n} \times n\mu = \mu \quad \checkmark$$

$$B(\bar{X}) = E(\bar{X}) - \mu = 0 \quad \checkmark$$

**MSE:**

$$MSE(\bar{X}) = \text{Var}(\bar{X}) + [B(\bar{X})]^2 = \frac{\sigma^2}{n} + 0 = \frac{\sigma^2}{n}$$

**Kết luận:** $\bar{X}$ không lệch và $MSE(\bar{X}) = \sigma^2/n$ giảm khi $n$ tăng — nhất quán.

---

### Ví dụ 2 (Trung bình)

> **Exercise:** Consider two estimators of $\mu$ from a sample of size $n$:
> - $\hat{\mu}_1 = \bar{X}$ (sample mean)
> - $\hat{\mu}_2 = \frac{X_1 + X_2}{2}$ (average of first two observations only)
>
> (a) Show both are unbiased. (b) Calculate relative efficiency. (c) Which is better and why?

**Giải:**

**(a) Kiểm tra không lệch:**

$$E(\hat{\mu}_1) = \mu \quad \checkmark \qquad E(\hat{\mu}_2) = \frac{\mu + \mu}{2} = \mu \quad \checkmark$$

**(b) Phương sai:**

$$\text{Var}(\hat{\mu}_1) = \frac{\sigma^2}{n} \qquad \text{Var}(\hat{\mu}_2) = \frac{\sigma^2}{4}\cdot 2 = \frac{\sigma^2}{2}$$

Hiệu quả tương đối:

$$e(\hat{\mu}_1, \hat{\mu}_2) = \frac{\text{Var}(\hat{\mu}_2)}{\text{Var}(\hat{\mu}_1)} = \frac{\sigma^2/2}{\sigma^2/n} = \frac{n}{2}$$

**(c) Kết luận:** Với $n \ge 2$, $e \ge 1$, tức $\hat{\mu}_1 = \bar{X}$ **hiệu quả hơn** $\hat{\mu}_2$ (dùng ít thông tin hơn). Hiệu quả tương đối $= n/2$ tăng theo $n$ — $\bar{X}$ càng tốt hơn $\hat{\mu}_2$ khi mẫu càng lớn.

---

### Ví dụ 3 (Khó)

> **Exercise:** Consider estimating $\sigma^2$ using two estimators:
> - $S^2 = \dfrac{1}{n-1}\sum(X_i - \bar{X})^2$ (unbiased)
> - $\tilde{\sigma}^2 = \dfrac{1}{n}\sum(X_i - \bar{X})^2$ (biased, MLE for normal population)
>
> (a) Find $E(\tilde{\sigma}^2)$ and $B(\tilde{\sigma}^2)$.  
> (b) Find $\text{Var}(\tilde{\sigma}^2)$ and $MSE(\tilde{\sigma}^2)$ for a normal population.  
> (c) Compare $MSE(S^2)$ and $MSE(\tilde{\sigma}^2)$ for $n = 5$.

**Giải:**

**(a) Độ lệch của $\tilde{\sigma}^2$:**

$$\tilde{\sigma}^2 = \frac{n-1}{n} S^2 \Rightarrow E(\tilde{\sigma}^2) = \frac{n-1}{n}\sigma^2$$

$$B(\tilde{\sigma}^2) = \frac{n-1}{n}\sigma^2 - \sigma^2 = -\frac{\sigma^2}{n} \quad \text{(lệch âm — ước lượng thấp)}$$

**(b) Phương sai và MSE của $\tilde{\sigma}^2$:**

Với tổng thể chuẩn: $\text{Var}(S^2) = \dfrac{2\sigma^4}{n-1}$

$$\text{Var}(\tilde{\sigma}^2) = \left(\frac{n-1}{n}\right)^2 \text{Var}(S^2) = \frac{(n-1)^2}{n^2} \times \frac{2\sigma^4}{n-1} = \frac{2(n-1)\sigma^4}{n^2}$$

$$MSE(\tilde{\sigma}^2) = \frac{2(n-1)\sigma^4}{n^2} + \frac{\sigma^4}{n^2} = \frac{(2n-1)\sigma^4}{n^2}$$

**(c) So sánh với $n = 5$:**

$$MSE(S^2) = \text{Var}(S^2) = \frac{2\sigma^4}{n-1} = \frac{2\sigma^4}{4} = \frac{\sigma^4}{2} = 0.5\sigma^4$$

$$MSE(\tilde{\sigma}^2) = \frac{(2 \times 5 - 1)\sigma^4}{25} = \frac{9\sigma^4}{25} = 0.36\sigma^4$$

**Kết luận:** $MSE(\tilde{\sigma}^2) = 0.36\sigma^4 < MSE(S^2) = 0.5\sigma^4$ với $n = 5$!

Ước lượng **lệch** $\tilde{\sigma}^2$ có $MSE$ **nhỏ hơn** ước lượng không lệch $S^2$. Đây minh họa nguyên tắc đánh đổi bias-variance: đôi khi chấp nhận một chút lệch để đổi lấy phương sai nhỏ hơn, tổng thể $MSE$ nhỏ hơn.

> [!warning] Sai lầm thường gặp
> - **Nghĩ rằng ước lượng không lệch luôn tốt hơn ước lượng lệch**: Sai — cần so sánh $MSE$ tổng thể.
> - **Nhầm "hiệu quả" với "nhanh/gọn"**: Trong thống kê, "hiệu quả" = phương sai nhỏ nhất trong lớp không lệch.
> - **Quên kiểm tra nhất quán**: Ước lượng tốt cần hội tụ về tham số khi $n \to \infty$.
