---
tags:
  - MAS291
  - Chapter4
  - GammaDistribution
  - ErlangDistribution
aliases:
  - Erlang Distribution
  - Gamma Distribution
  - Phân phối Gamma
  - Phân phối Erlang
---

# 4.9 Phân Phối Erlang và Gamma (Erlang and Gamma Distributions)

## 1. Định nghĩa và tóm gọn

> [!abstract] Định nghĩa
> **Phân phối Gamma** là phân phối liên tục tổng quát hóa phân phối mũ. Nó mô tả thời gian chờ cho đến khi xảy ra **$r$ sự kiện Poisson**.
>
> **Phân phối Erlang** là trường hợp đặc biệt của Gamma với $r$ là số nguyên dương.

### Ý nghĩa thực hành

- Được dùng trong: lý thuyết hàng đợi, phân tích độ tin cậy, mô hình thời gian phục vụ.
- Gamma tổng quát hơn Erlang (cho phép $r$ không nguyên).

---

## 2. Ký hiệu và các tham số tham gia

> [!info] Ký hiệu

| Ký hiệu | Tên tiếng Việt (English) |
|:-------:|:------------------------|
| $r$ | Số sự kiện cần chờ (Number of Events — shape parameter); $r > 0$ |
| $\lambda$ | Tốc độ sự kiện (Rate Parameter); $\lambda > 0$ |
| $X \sim \text{Gamma}(r, \lambda)$ | $X$ tuân theo phân phối Gamma |
| $\Gamma(r)$ | Hàm Gamma: $\Gamma(r) = \int_0^\infty x^{r-1}e^{-x}dx$ |

---

## 3. Phân loại và Công thức

### 3.1 Phân phối Gamma — $X \sim \text{Gamma}(r, \lambda)$

**PDF:**

$$f(x) = \frac{\lambda^r x^{r-1} e^{-\lambda x}}{\Gamma(r)}, \quad x > 0$$

**Kỳ vọng và Phương sai:**

$$E(X) = \frac{r}{\lambda} \qquad \text{Var}(X) = \frac{r}{\lambda^2}$$

### 3.2 Quan hệ với các phân phối khác

- Khi $r = 1$: $\text{Gamma}(1, \lambda) = \text{Exponential}(\lambda)$.
- Khi $r$ là số nguyên: Gamma = Erlang.
- Khi $r = n/2$ và $\lambda = 1/2$: $\text{Gamma}(n/2, 1/2) = \chi^2_n$ (chi-bình phương).

---

## 4. Ví dụ minh họa

### Ví dụ 1

> **Exercise:** The time until the 3rd customer arrives at a store follows a Gamma distribution with $r = 3$ and $\lambda = 2$ customers/minute. Find the mean and variance of the waiting time.

**Giải:**

$$E(X) = \frac{r}{\lambda} = \frac{3}{2} = 1.5 \text{ phút}$$

$$\text{Var}(X) = \frac{r}{\lambda^2} = \frac{3}{4} = 0.75 \text{ phút}^2$$

**Kết luận:** Trung bình chờ $1.5$ phút để $3$ khách hàng đến; độ lệch chuẩn $= \sqrt{0.75} \approx 0.866$ phút.
