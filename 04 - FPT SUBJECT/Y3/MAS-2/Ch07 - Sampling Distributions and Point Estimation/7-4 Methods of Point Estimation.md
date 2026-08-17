---
tags:
  - MAS291
  - Chapter7
  - PointEstimation
  - MLE
  - MOM
aliases:
  - Methods of Point Estimation
  - MLE
  - Method of Moments
  - Phương pháp hợp lý tối đa
  - Phương pháp moment
---

# 7.4 Các Phương Pháp Ước Lượng Điểm (Methods of Point Estimation)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> Có hai phương pháp chính để xây dựng ước lượng điểm có hệ thống:
> 1. **Ước lượng hợp lý tối đa (Maximum Likelihood Estimation — MLE)**
> 2. **Phương pháp moment (Method of Moments — MOM)**

### Ý nghĩa thực hành

- **MLE** là phương pháp phổ biến nhất — tìm giá trị tham số **làm cho dữ liệu quan sát được xảy ra với xác suất cao nhất**.
- **MOM** là phương pháp trực quan và đơn giản hơn — **cân bằng moment mẫu với moment tổng thể**.

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $L(\theta)$ | Hàm hợp lý (Likelihood Function) |
| $\ell(\theta)$ | Hàm log-hợp lý (Log-Likelihood Function) |
| $\hat{\theta}_{MLE}$ | Ước lượng hợp lý tối đa (Maximum Likelihood Estimate) |
| $f(x;\theta)$ | Hàm mật độ/xác suất phụ thuộc tham số $\theta$ |
| $\mu'_k$ | Moment thứ $k$ của tổng thể (Population $k$-th Moment) |
| $m_k$ | Moment thứ $k$ của mẫu (Sample $k$-th Moment) |

---

## 3. Phân loại và Công thức

### 3.1 Ước lượng Hợp Lý Tối Đa (Maximum Likelihood Estimation — MLE)

#### Nguyên tắc

Cho mẫu quan sát $x_1, x_2, \ldots, x_n$, **hàm hợp lý (Likelihood Function)** là:

$$L(\theta) = \prod_{i=1}^n f(x_i; \theta)$$

$\hat{\theta}_{MLE}$ là giá trị $\theta$ **tối đa hóa** $L(\theta)$.

#### Quy trình tìm MLE

1. Viết $L(\theta) = \prod f(x_i; \theta)$.
2. Lấy logarithm: $\ell(\theta) = \ln L(\theta) = \sum \ln f(x_i; \theta)$.
3. Đặt $\dfrac{d\ell}{d\theta} = 0$ và giải tìm $\hat{\theta}_{MLE}$.
4. Kiểm tra đây là cực đại (kiểm tra đạo hàm bậc 2 hoặc theo lý luận).

> [!note] Tại sao lấy logarithm?
> $\ln L(\theta)$ và $L(\theta)$ đạt cực đại tại cùng $\theta$, nhưng $\ln$ biến tích thành tổng — dễ tính đạo hàm hơn nhiều.

#### Tính chất của MLE

- **Nhất quán**: $\hat{\theta}_{MLE} \xrightarrow{p} \theta$ khi $n \to \infty$.
- **Bất biến (Invariance)**: Nếu $\hat{\theta}_{MLE}$ là MLE của $\theta$, thì $g(\hat{\theta}_{MLE})$ là MLE của $g(\theta)$.
- **Tiệm cận hiệu quả**: Với $n$ lớn, MLE xấp xỉ đạt cận Cramér-Rao.

---

### 3.2 Phương Pháp Moment (Method of Moments — MOM)

#### Nguyên tắc

Cân bằng **moment tổng thể** với **moment mẫu**:

$$\mu'_k = \frac{1}{n}\sum_{i=1}^n x_i^k, \quad k = 1, 2, \ldots$$

Giải hệ phương trình để tìm ước lượng viên.

Moment thứ $k$ của tổng thể:

$$\mu'_k = E(X^k)$$

Moment thứ $k$ của mẫu:

$$m_k = \frac{1}{n}\sum_{i=1}^n x_i^k$$

#### Đặt $\mu'_k = m_k$ và giải hệ phương trình.

---

### 3.3 MLE cho một số phân phối thông dụng

#### Phân phối chuẩn $N(\mu, \sigma^2)$

$$\hat{\mu}_{MLE} = \bar{x} = \frac{1}{n}\sum x_i$$

$$\hat{\sigma}^2_{MLE} = \frac{1}{n}\sum (x_i - \bar{x})^2 \quad \text{(lệch — dùng } n \text{ không phải } n-1)}$$

> [!warning]
> $\hat{\sigma}^2_{MLE}$ là ước lượng **lệch** của $\sigma^2$! Trong thực hành, dùng $S^2 = \dfrac{1}{n-1}\sum(x_i-\bar{x})^2$ để có ước lượng không lệch.

#### Phân phối Poisson với tham số $\lambda$

$$\hat{\lambda}_{MLE} = \bar{x}$$

#### Phân phối mũ (Exponential) với tham số $\lambda$

$$\hat{\lambda}_{MLE} = \frac{1}{\bar{x}}$$

---

## 4. Ví dụ minh họa

### Ví dụ 1 (Dễ)

> **Exercise:** A random sample from an exponential distribution $f(x;\lambda) = \lambda e^{-\lambda x}$, $x > 0$ yields observations: $x_1 = 2, x_2 = 5, x_3 = 3$. Find the MLE of $\lambda$.

**Tóm tắt bài toán:** MLE của $\lambda$ trong phân phối mũ.

**Giải:**

**Bước 1:** Hàm hợp lý:

$$L(\lambda) = \prod_{i=1}^3 \lambda e^{-\lambda x_i} = \lambda^3 e^{-\lambda(2+5+3)} = \lambda^3 e^{-10\lambda}$$

**Bước 2:** Log-hợp lý:

$$\ell(\lambda) = 3\ln\lambda - 10\lambda$$

**Bước 3:** Đặt đạo hàm bằng $0$:

$$\frac{d\ell}{d\lambda} = \frac{3}{\lambda} - 10 = 0 \Rightarrow \hat{\lambda}_{MLE} = \frac{3}{10} = 0.3$$

**Kiểm tra:** $\dfrac{d^2\ell}{d\lambda^2} = -3/\lambda^2 < 0$ → cực đại ✓

**Kết luận:** $\hat{\lambda}_{MLE} = \dfrac{n}{\sum x_i} = \dfrac{3}{10} = 0.3 = \dfrac{1}{\bar{x}}$.

---

### Ví dụ 2 (Trung bình)

> **Exercise:** A sample of $n = 4$ observations from $N(\mu, \sigma^2)$: $x_1 = 8, x_2 = 12, x_3 = 10, x_4 = 14$. Find the MLE of $\mu$ and $\sigma^2$, and compare $\hat{\sigma}^2_{MLE}$ with the unbiased $s^2$.

**Tóm tắt bài toán:** MLE của $\mu$ và $\sigma^2$ cho phân phối chuẩn.

**Giải:**

**Bước 1:** PDF: $f(x;\mu,\sigma^2) = \dfrac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}$

**Bước 2:** Log-hợp lý:

$$\ell(\mu,\sigma^2) = -\frac{n}{2}\ln(2\pi) - \frac{n}{2}\ln\sigma^2 - \frac{1}{2\sigma^2}\sum(x_i-\mu)^2$$

**Bước 3:** Tối ưu hóa theo $\mu$: $\hat{\mu}_{MLE} = \bar{x} = \dfrac{8+12+10+14}{4} = 11$

**Bước 4:** Tối ưu hóa theo $\sigma^2$: $\hat{\sigma}^2_{MLE} = \dfrac{1}{n}\sum(x_i-\bar{x})^2$

$$\sum(x_i-11)^2 = (8-11)^2 + (12-11)^2 + (10-11)^2 + (14-11)^2 = 9+1+1+9 = 20$$

$$\hat{\sigma}^2_{MLE} = \frac{20}{4} = 5$$

**Ước lượng không lệch:**

$$s^2 = \frac{20}{4-1} = \frac{20}{3} \approx 6.67$$

**So sánh:** $\hat{\sigma}^2_{MLE} = 5 < s^2 = 6.67$ — MLE ước lượng **thấp hơn** vì dùng $n$ thay $n-1$.

---

### Ví dụ 3 (Khó)

> **Exercise:** A Bernoulli random variable has $P(X = 1) = p$ and $P(X = 0) = 1-p$. From $n = 20$ trials, $x = 14$ successes are observed.
>
> (a) Find the MLE of $p$.  
> (b) Using the invariance of MLE, find the MLE of $p(1-p)$.  
> (c) Find the Method of Moments estimator of $p$ and compare with MLE.

**Tóm tắt bài toán:** MLE và MOM cho phân phối Bernoulli.

$$n = 20,\quad x = 14 \text{ (số thành công)}$$

**(a) MLE của $p$:**

$$L(p) = \prod_{i=1}^n p^{x_i}(1-p)^{1-x_i} = p^{14}(1-p)^6$$

$$\ell(p) = 14\ln p + 6\ln(1-p)$$

$$\frac{d\ell}{dp} = \frac{14}{p} - \frac{6}{1-p} = 0$$

$$14(1-p) = 6p \Rightarrow 14 - 14p = 6p \Rightarrow 14 = 20p$$

$$\boxed{\hat{p}_{MLE} = \frac{14}{20} = 0.7 = \hat{p}}$$

**(b) MLE của $p(1-p)$ (tính chất bất biến):**

$$\widehat{p(1-p)}_{MLE} = \hat{p}_{MLE}(1-\hat{p}_{MLE}) = 0.7 \times 0.3 = 0.21$$

**(c) MOM của $p$:**

Moment thứ nhất của $X \sim$ Bernoulli$(p)$: $E(X) = p$.

Moment mẫu thứ nhất: $m_1 = \bar{x} = 14/20 = 0.7$.

Đặt $p = m_1$: $\hat{p}_{MOM} = 0.7$.

**So sánh:** $\hat{p}_{MLE} = \hat{p}_{MOM} = 0.7$ — trong trường hợp này hai phương pháp cho cùng kết quả.

> [!note]
> Với phân phối Bernoulli và Poisson, MLE và MOM cho cùng ước lượng. Với phân phối phức tạp hơn (ví dụ: phân phối Beta, Gamma), hai phương pháp có thể cho kết quả khác nhau.

> [!warning] Sai lầm thường gặp
> - **Quên $\ln$ khi tính MLE**: Luôn lấy $\ln L(\theta)$ để biến tích thành tổng dễ tính đạo hàm.
> - **Nhầm $\hat{\sigma}^2_{MLE}$ với $s^2$**: MLE dùng $n$; ước lượng không lệch dùng $n-1$.
> - **Quên tính chất bất biến của MLE**: Nếu cần MLE của $g(\theta)$, chỉ cần tính $g(\hat{\theta}_{MLE})$ — không cần tối ưu hóa lại từ đầu.
