# Worked Examples

---

# Example 1 (Easy)

## Exercise

**Problem Summary**

A researcher wants to investigate whether the number of hours students study each week can predict their final exam scores.

Five students were observed.

| Study Hours (X) | Exam Score (Y) |
|----------------:|---------------:|
| 2 | 60 |
| 4 | 68 |
| 6 | 75 |
| 8 | 83 |
| 10 | 91 |

Find the simple linear regression equation and interpret the slope.

---

## Solution

### Bước 1. Xác định mô hình

Ta cần xây dựng phương trình hồi quy tuyến tính:

$$
\hat{Y}=b_0+b_1X
$$

Trong đó:

- \(X\): số giờ học.
- \(Y\): điểm thi.

---

### Bước 2. Lý do chọn công thức

Đề bài yêu cầu tìm đường thẳng mô tả mối quan hệ giữa **một biến độc lập** và **một biến phụ thuộc**, vì vậy sử dụng **Simple Linear Regression**.

Ta cần tính:

$$
b_1=
\frac{\sum(x_i-\bar{x})(y_i-\bar{y})}
{\sum(x_i-\bar{x})^2}
$$

và

$$
b_0=\bar y-b_1\bar x
$$

---

### Bước 3. Tính trung bình

$$
\bar x=\frac{2+4+6+8+10}{5}=6
$$

$$
\bar y=\frac{60+68+75+83+91}{5}=75.4
$$

---

### Bước 4. Tính hệ số góc

Lập bảng:

| $(x_i-\bar x)$ | $(y_i-\bar y)$ | Tích |
| -------------: | -------------: | ---: |
|             -4 |          -15.4 | 61.6 |
|             -2 |           -7.4 | 14.8 |
|              0 |           -0.4 |    0 |
|              2 |            7.6 | 15.2 |
|              4 |           15.6 | 62.4 |

$$
\sum(x_i-\bar x)(y_i-\bar y)=154
$$

$$
\sum(x_i-\bar x)^2=40
$$

Do đó

$$
b_1=\frac{154}{40}=3.85
$$

---

### Bước 5. Tính hệ số chặn

$$
b_0=75.4-3.85(6)
$$

$$
b_0=52.3
$$

---

### Bước 6. Phương trình hồi quy

$$
\boxed{\hat Y=52.3+3.85X}
$$

---

### Diễn giải kết quả

Hệ số góc bằng

$$
3.85
$$

nghĩa là:

> Khi số giờ học tăng thêm **1 giờ**, điểm thi trung bình dự đoán tăng khoảng **3.85 điểm**.

---

### Kết luận

Có mối quan hệ tuyến tính dương giữa số giờ học và điểm thi.

---

# Example 2 (Medium)

## Exercise

**Problem Summary**

A company investigates whether employees' weekly overtime hours affect their productivity score.

The regression output from Excel is:

| Statistic | Value |
|-----------|------:|
| Intercept | 82.6 |
| Slope | -1.25 |
| P-value | 0.012 |
| R Square | 0.56 |

Interpret the regression model and determine whether overtime significantly affects productivity at the 5% significance level.

---

## Solution

### Bước 1. Lý do chọn công thức

Đề bài đã cung cấp kết quả hồi quy từ Excel.

Do đó không cần tính lại hệ số mà chỉ cần:

- Viết phương trình.
- Kiểm định ý nghĩa hệ số góc.
- Diễn giải kết quả.

---

### Bước 2. Viết phương trình hồi quy

Từ bảng Regression Output:

$$
b_0=82.6
$$

$$
b_1=-1.25
$$

Suy ra

$$
\boxed{\hat Y=82.6-1.25X}
$$

---

### Bước 3. Kiểm định hệ số góc

Giả thuyết

$$
H_0:\beta_1=0
$$

$$
H_1:\beta_1\ne0
$$

Cho

$$
P=0.012
$$

Mức ý nghĩa

$$
\alpha=0.05
$$

Vì

$$
0.012<0.05
$$

nên bác bỏ

$$
H_0
$$

---

### Bước 4. Giải thích từng bước

Điều này cho thấy hệ số góc khác 0 một cách có ý nghĩa thống kê.

Do đó số giờ làm thêm có ảnh hưởng đến năng suất.

---

### Bước 5. Diễn giải hệ số góc

Hệ số góc

$$
-1.25
$$

nghĩa là:

Mỗi giờ làm thêm tăng thêm sẽ làm điểm năng suất trung bình giảm khoảng **1.25 điểm**.

---

### Bước 6. Diễn giải \(R^2\)

$$
R^2=0.56
$$

Có nghĩa:

56% sự biến động của năng suất được giải thích bởi số giờ làm thêm.

44% còn lại do các yếu tố khác.

---

### Kết luận

Có đủ bằng chứng thống kê để kết luận số giờ làm thêm ảnh hưởng đến năng suất làm việc.

---

# Example 3 (Difficult)

## Exercise

**Problem Summary**

A university studies whether the number of weekly part-time working hours influences students' GPA.

The regression output is:

| Statistic | Value |
|-----------|------:|
| Intercept | 3.82 |
| Slope | -0.018 |
| Standard Error of Slope | 0.006 |
| Sample Size | 40 |

Test whether working hours significantly affect GPA at the 5% significance level.

---

## Solution

### Bước 1. Lý do chọn công thức

Đề bài yêu cầu kiểm định xem hệ số góc có bằng 0 hay không.

Do đó sử dụng kiểm định

$$
t=\frac{b_1}{SE(b_1)}
$$

---

### Bước 2. Đặt giả thuyết

$$
H_0:\beta_1=0
$$

$$
H_1:\beta_1\ne0
$$

---

### Bước 3. Tính thống kê kiểm định

Cho

$$
b_1=-0.018
$$

$$
SE(b_1)=0.006
$$

Suy ra

$$
t_0=\frac{-0.018}{0.006}
$$

$$
t_0=-3.00
$$

---

### Bước 4. Xác định miền bác bỏ

Bậc tự do

$$
df=n-2=38
$$

Với

$$
\alpha=0.05
$$

Tra bảng

$$
t_{0.025,38}\approx2.024
$$

Miền bác bỏ:

$$
|t|>2.024
$$

---

### Bước 5. Ra quyết định

Ta có

$$
|t_0|=3.00
$$

và

$$
3.00>2.024
$$

Do đó bác bỏ

$$
H_0
$$

---

### Bước 6. Viết phương trình hồi quy

$$
\boxed{\hat{GPA}=3.82-0.018X}
$$

---

### Bước 7. Diễn giải kết quả

Hệ số góc âm cho thấy:

Mỗi giờ làm thêm tăng thêm mỗi tuần sẽ làm GPA trung bình giảm khoảng **0.018 điểm**.

Việc kiểm định cho thấy hệ số góc có ý nghĩa thống kê.

Điều này chứng tỏ số giờ làm thêm có ảnh hưởng đáng kể đến GPA.

---

### Kết luận

Ở mức ý nghĩa 5%, có đủ bằng chứng để kết luận số giờ làm thêm có ảnh hưởng tiêu cực đến GPA của sinh viên. Tuy nhiên, đây chỉ là mối quan hệ thống kê; chưa thể khẳng định quan hệ nhân quả vì GPA còn chịu tác động của nhiều yếu tố khác như thời gian học, năng lực cá nhân và phương pháp học.