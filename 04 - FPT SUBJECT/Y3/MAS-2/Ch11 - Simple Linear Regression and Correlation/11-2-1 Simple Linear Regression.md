# Simple Linear Regression

> [!abstract]
> **Simple Linear Regression (SLR)** là phương pháp thống kê dùng để mô hình hóa mối quan hệ tuyến tính giữa **một biến độc lập** \(X\) và **một biến phụ thuộc** \(Y\), đồng thời dự đoán giá trị của \(Y\) từ \(X\).

---

# Model

Mô hình hồi quy tổng thể:

$$
Y=\beta_0+\beta_1X+\varepsilon
$$

Mô hình hồi quy ước lượng từ mẫu:

$$
\hat{Y}=b_0+b_1X
$$

Trong đó:

| Ký hiệu         | Ý nghĩa                                        |
| --------------- | ---------------------------------------------- |
| \(Y\)           | Biến phụ thuộc (Dependent Variable)            |
| \(X\)           | Biến độc lập (Independent Variable)            |
| $(\beta_0)$     | Hệ số chặn của tổng thể (Population Intercept) |
| $(\beta_1)$     | Hệ số góc của tổng thể (Population Slope)      |
| $(b_0$)         | Hệ số chặn ước lượng từ mẫu                    |
| $(b_1$)         | Hệ số góc ước lượng từ mẫu                     |
| $(\varepsilon)$ | Sai số ngẫu nhiên (epsilon)                    |

---

# Assumptions

> [!note]
> Các giả định dưới đây cần được thỏa mãn để mô hình hồi quy và các kiểm định thống kê có giá trị.

1. Mối quan hệ giữa \(X\) và \(Y\) là **tuyến tính**.

2. Các quan sát độc lập.

3. Sai số có kỳ vọng bằng 0.

$$
E(\varepsilon)=0
$$

4. Sai số có phương sai không đổi (Homoscedasticity).

$$
Var(\varepsilon)=\sigma^2
$$

5. Sai số phân phối chuẩn.

$$
\varepsilon \sim N(0,\sigma^2)
$$

---

# Conditions

Áp dụng khi:

- Chỉ có **một biến độc lập**.
- Hai biến đều là dữ liệu định lượng.
- Scatter Plot cho thấy xu hướng gần tuyến tính.
- Các quan sát độc lập.
- Không có quá nhiều Outliers.
- Sai số gần phân phối chuẩn nếu thực hiện kiểm định hoặc lập khoảng tin cậy.

---

# Formulas

## Estimated Regression Equation

$$
\hat{Y}=b_0+b_1X
$$

## Slope

$$
b_1=
\frac{\sum(x_i-\bar{x})(y_i-\bar{y})}
{\sum(x_i-\bar{x})^2}
$$

## Intercept

$$
b_0=\bar{y}-b_1\bar{x}
$$

## Error Sum of Squares

$$
SSE=\sum(y_i-\hat{y}_i)^2
$$

## Mean Square Error

$$
MSE=\frac{SSE}{n-2}
$$

## Standard Error of Slope

$$
SE(b_1)=
\sqrt{
\frac{MSE}
{\sum(x_i-\bar{x})^2}
}
$$

## Coefficient of Determination

$$
R^2=\frac{SSR}{SST}
=1-\frac{SSE}{SST}
$$

---

# Derivation

Mục tiêu của hồi quy tuyến tính là tìm đường thẳng sao cho tổng bình phương sai số là nhỏ nhất.

Hàm mục tiêu:

$$
SSE=\sum(y_i-\hat{y}_i)^2
$$

Trong đó

$$
\hat{y}_i=b_0+b_1x_i
$$

Thay vào:

$$
SSE=
\sum
(y_i-b_0-b_1x_i)^2
$$

Lấy đạo hàm riêng theo $(b_0)$ và $(b_1)$, đặt bằng 0:

$$
\frac{\partial SSE}{\partial b_0}=0
$$

$$
\frac{\partial SSE}{\partial b_1}=0
$$

Giải hệ phương trình chuẩn (Normal Equations), thu được:

$$
b_1=
\frac{\sum(x_i-\bar{x})(y_i-\bar{y})}
{\sum(x_i-\bar{x})^2}
$$

$$
b_0=\bar{y}-b_1\bar{x}
$$

---

# Hypothesis Test for Slope

Thông thường chỉ kiểm định hệ số góc.

## Hypotheses

$$
H_0:\beta_1=0
$$

(Không tồn tại mối quan hệ tuyến tính.)

$$
H_1:\beta_1\neq0
$$

(Tồn tại mối quan hệ tuyến tính.)

---

## Test Statistic

$$
t_0=
\frac{b_1}
{SE(b_1)}
$$

với

$$
t_0\sim t(n-2)
$$

---

# Decision Rule

Với mức ý nghĩa $(\alpha)$:

Nếu

$$
|t_0|>t_{\alpha/2,n-2}
$$

thì **bác bỏ** $(H_0)$.

Hoặc

Nếu

$$
P\text{-value}<\alpha
$$

thì **bác bỏ** $(H_0)$.

---

# Rejection Region

## Two-tailed Test

$$
|t_0|>t_{\alpha/2,n-2}
$$

## Right-tailed Test

$$
t_0>t_{\alpha,n-2}
$$

## Left-tailed Test

$$
t_0<-t_{\alpha,n-2}
$$

---

# Interpretation of Coefficients

## Intercept

\(b_0\) là giá trị dự đoán của \(Y\) khi

$$
X=0
$$

## Slope

Nếu

$$
b_1>0
$$

thì khi \(X\) tăng 1 đơn vị, \(Y\) trung bình tăng khoảng \(b_1\) đơn vị.

Nếu

$$
b_1<0
$$

thì khi \(X\) tăng 1 đơn vị, \(Y\) trung bình giảm khoảng \(|b_1|\) đơn vị.

---

# Interpretation of \(R^2\)

| Giá trị | Ý nghĩa |
|----------|----------|
| Gần 1 | Mô hình giải thích tốt dữ liệu |
| Gần 0 | Mô hình giải thích kém |
| 0.60 | Khoảng 60% biến thiên của \(Y\) được giải thích bởi \(X\) |

---

# Remarks

> [!warning]
> - Tương quan không đồng nghĩa với quan hệ nhân quả (Correlation does **not** imply causation).
> - Không nên ngoại suy (Extrapolation) ngoài phạm vi dữ liệu đã quan sát.
> - Outliers có thể ảnh hưởng mạnh đến đường hồi quy.
> - \(R^2\) cao không đảm bảo mô hình phù hợp nếu các giả định bị vi phạm.

---

# Result Interpretation

Ví dụ kết quả:

$$
\hat{GPA}=3.75-0.018X
$$

với

- P-value = 0.003
- $(R^2=0.42)$

Diễn giải:

- Khi số giờ làm thêm tăng **1 giờ/tuần**, GPA trung bình giảm khoảng **0.018 điểm**.
- Vì **P-value < 0.05**, có đủ bằng chứng thống kê rằng số giờ làm thêm có ảnh hưởng đến GPA.
- Giá trị \(R^2=0.42\) cho thấy khoảng **42%** biến thiên của GPA được giải thích bởi số giờ làm thêm; phần còn lại do các yếu tố khác.

---

# Excel Output

Sau khi chạy **Data Analysis → Regression**, cần đọc các mục sau:

| Output         | Ý nghĩa                               |
| -------------- | ------------------------------------- |
| Intercept      | Hệ số chặn                            |
| X Variable     | Hệ số góc                             |
| P-value        | Kiểm định ý nghĩa của hệ số           |
| R Square       | Hệ số xác định                        |
| Standard Error | Sai số chuẩn                          |
| ANOVA          | Kiểm định ý nghĩa của toàn bộ mô hình |

> [!info]
> Trong các bài tập MAS291, ba kết quả được sử dụng nhiều nhất là:
>
> - **Regression Equation**
> - **P-value**
> - **R Square**