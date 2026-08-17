1. Định nghĩa:
	1. Simple Linear Regression (SLR) là phương pháp thống kê dùng để mô hình hóa mối quan hệ tuyến tính giữa **một biến độc lập** \(X\) và **một biến phụ thuộc** \(Y\), đồng thời dự đoán giá trị của \(Y\) từ \(X\).
2. Tóm tắt đề:
	1. X: Số giờ làm
	2. Y: GPA
	3. n = 51
3. Tính mean của X và Y
	1. $\mu_x=18.25490196$
	2. $\mu_y=7.584117647$
4. Theo Công thức regression
	1. Giải thích:
		1. Slope: Giá trị GPA thay đổi bao nhiêu đơn vị khi số giờ làm tăng 1
		2. Intercept: Dự đoán số giờ làm thêm mỗi tuần
	2. Ta có:$$Y=\beta_0+\beta_1X+\varepsilon$$
		1. Công thức trên không có sai số ngẫu nhiên vì nó không dùng để mô tả chính xác điểm số của một cá nhân riêng lẻ, mà dùng để **dự báo mức GPA trung bình** của các sinh viên dựa trên số giờ làm thêm của họ.
	3. Suy ra phương trình tuyến tính:
$$\text{GPA} = 7.3579 + 0.0124 \times \text{Số giờ làm thêm}$$
	4. Với: 
		1. $\beta_1(Slope)=\frac{\sum(x_i-\bar{x})(y_i-\bar{y})}{\sum(x_i-\bar{x})^2}= \frac{n\sum(XY) - \sum X \sum Y}{n\sum(X^2) - (\sum X)^2}$
		2. $\beta_0(Intercept)=\bar{y}-\beta_1\bar{x}$
	5. Thay vào
		1. $\beta_1 = \frac{51 \times 7245.2 - 931 \times 386.79}{51 \times 31877 - 931^2} = \frac{9403.71}{758966} \approx 0.01239016$
		=> Điều này cho thấy có một mối tương quan thuận nhẹ giữa số giờ làm thêm và GPA trong tập dữ liệu hiện tại.
		2. $\beta_0 = 7.5841176 - (0.01239016 \times 18.254902) \approx 7.3579365$
	6. Phương trình tuyến tính
		1. $\text{GPA} = 7.35794 + 0.01239 \times \text{Thời gian làm thêm}$
5. Sử dụng Lệnh exel:
```
"=LINEST(C2:C52, B2:B52, TRUE, TRUE)"
```
6. bảng hiện (sau khi thực hiện ):

| Theo $\beta_1$                                                                   | Hệ số góc (Slope) | Hệ số chặn (Intercept) | Theo $\beta_2$                                                                                |
| -------------------------------------------------------------------------------- | ----------------- | ---------------------- | --------------------------------------------------------------------------------------------- |
| Slope: Tăng 1 giá trị ảnh hưởng đến bao nhiêu GPA                                | 0.01239015977     | 7.357936495            | Intercept: Dự đoán Tại slope = 0                                                              |
| Sai số chuẩn của Slope: <br>Độ chính xác của ước lượng (giao động nhiều hay ít). | 0.007174125568    | 0.1793587659           | Sai số chuẩn của Intercept:<br>Độ chính xác của ước lượng hệ số.                              |
| $R^2$ (Coefficient of Determination): Hệ số xác định % ảnh hưởng đến GPA.        | 0.05737948836     | 0.8751752881           | Sai số chuẩn của ước lượng (Standard Error of Regression) lệch bao nhiêu điểm so với thực tế. |
| F Statistic: để kiểm định:<br>$H_0: \beta_1=0$                                   | 2.982743209       | 49                     | Degrees of Freedom (df): có 51 sv                                                             |
| Regression SS (SSR):<br>Phần biến thiên được mô hình giải thích.                 | 2.28457783        | 37.53065746            | Residual SS (SSE - Error Sum of Squares):<br>Phần không giải thích được.                      |
Vì SSE > SSR nên mô hình chỉ giải thích được rất it biến thiên của GPA.
7. Lời khuyên:
### Mặc dù dữ liệu cho thấy làm thêm không làm giảm GPA (thậm chí có xu hướng tăng nhẹ), mức độ ảnh hưởng này là rất nhỏ và R-squared thấp (0.007) cho thấy thời gian làm thêm không giải thích được nhiều sự biến thiên của GPA. Do đó, bạn nên giữ số giờ làm thêm ở mức hợp lý (ví dụ: dưới 25-30 giờ/tuần) để đảm bảo sức khỏe, tránh quá tải và duy trì kết quả học tập ổn định.