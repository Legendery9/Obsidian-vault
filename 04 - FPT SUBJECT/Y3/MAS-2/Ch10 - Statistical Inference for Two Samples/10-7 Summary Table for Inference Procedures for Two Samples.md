---
tags:
  - MAS291
  - Chapter10
  - TwoSamples
  - Summary
aliases:
  - Two-sample Summary Table
  - Bảng tóm tắt suy diễn hai mẫu
---

# 10.7 Bảng Tóm Tắt Suy Diễn Hai Mẫu (Summary Table for Two-Sample Inference)

## Bảng tóm tắt

| Tham số | Điều kiện | Test Statistic | Phân phối | Link |
|:-------:|:---------:|:--------------:|:---------:|:----:|
| $\mu_1-\mu_2$ | $\sigma_1,\sigma_2$ biết | $Z_0 = \dfrac{(\bar{x}_1-\bar{x}_2)-\Delta_0}{\sqrt{\sigma_1^2/n_1+\sigma_2^2/n_2}}$ | $N(0,1)$ | [[10-1 Inference on the Difference in Means - Variances Known]] |
| $\mu_1-\mu_2$ | $\sigma$ chưa biết, $\sigma_1^2=\sigma_2^2$ | $t_0 = \dfrac{(\bar{x}_1-\bar{x}_2)-\Delta_0}{s_p\sqrt{1/n_1+1/n_2}}$ | $t_{n_1+n_2-2}$ | [[10-2 Inference on the Difference in Means - Variances Unknown]] |
| $\mu_1-\mu_2$ | $\sigma$ chưa biết, $\sigma_1^2\ne\sigma_2^2$ | $t_0 = \dfrac{(\bar{x}_1-\bar{x}_2)-\Delta_0}{\sqrt{s_1^2/n_1+s_2^2/n_2}}$ | $t_{df_{Welch}}$ | [[10-2 Inference on the Difference in Means - Variances Unknown]] |
| $\mu_D$ | Ghép cặp | $t_0 = \dfrac{\bar{d}-\Delta_0}{s_d/\sqrt{n}}$ | $t_{n-1}$ | [[10-4 Paired t-Test]] |
| $\sigma_1^2/\sigma_2^2$ | Cả hai chuẩn | $F_0 = s_1^2/s_2^2$ | $F_{n_1-1,n_2-1}$ | [[10-5 Inference on the Variances of Two Normal Distributions]] |
| $p_1-p_2$ | Mẫu lớn | $Z_0 = \dfrac{\hat{p}_1-\hat{p}_2}{\sqrt{\hat{p}(1-\hat{p})(1/n_1+1/n_2)}}$ | $N(0,1)$ | [[10-6 Inference on Two Population Proportions]] |

## Sơ đồ chọn phương pháp

```
Mẫu ghép cặp?
├── Có → Paired t-test (10-4)
└── Không → Hai mẫu độc lập
    ├── So sánh μ1 - μ2
    │   ├── σ1, σ2 biết → Z-test (10-1)
    │   └── σ1, σ2 chưa biết
    │       ├── Kiểm định F (10-5): σ1² = σ2²?
    │       │   ├── Có → Pooled t-test (10-2)
    │       │   └── Không → Welch's t-test (10-2)
    ├── So sánh σ1²/σ2² → F-test (10-5)
    └── So sánh p1 - p2 → Two-proportion Z-test (10-6)
```
