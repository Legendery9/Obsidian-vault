---
tags:
  - MAS291
  - Chapter8
  - ConfidenceInterval
aliases:
  - Guidelines for CI
  - Hướng dẫn xây dựng khoảng tin cậy
---

# 8.7 Hướng Dẫn Xây Dựng Khoảng Tin Cậy (Guidelines for Constructing CIs)

## 1. Định nghĩa và tóm gọn

> [!abstract] Tóm lược
> Phần này cung cấp **hướng dẫn tổng hợp** để chọn đúng phương pháp xây dựng khoảng tin cậy dựa trên đặc điểm của bài toán.

---

## 2. Sơ đồ chọn phương pháp

```
Tham số cần ước lượng?
├── Trung bình μ
│   ├── σ đã biết → Dùng Z → [[8.2.Khoảng tin cậy cho μ - Biết phương sai]]
│   └── σ chưa biết
│       ├── Tổng thể chuẩn hoặc n ≥ 30 → Dùng t → [[8.3.Khoảng tin cậy cho μ -
│		│	Không biết phương sai]]
│       └── n nhỏ, tổng thể không chuẩn → Dùng phương pháp phi tham số
├── Tỷ lệ p
│   └── n đủ lớn (np̂ ≥ 5, n(1-p̂) ≥ 5) → Dùng Z → [[8.5.Khoảng tin cậy cho tỷ lệ 
│		tổng thể]]
└── Phương sai σ²
    └── Tổng thể chuẩn → Dùng χ² → [[8.4.Khoảng tin cậy cho phương sai]]
```

---

## 3. Tóm tắt công thức

| Tham số | Điều kiện | Thống kê | Công thức CI hai phía |
|:-------:|:---------:|:--------:|:---------------------:|
| $\mu$ | $\sigma$ biết | $Z$ | $\bar{x} \pm z_{\alpha/2}\frac{\sigma}{\sqrt{n}}$ |
| $\mu$ | $\sigma$ chưa biết | $t_{n-1}$ | $\bar{x} \pm t_{\alpha/2,n-1}\frac{s}{\sqrt{n}}$ |
| $\sigma^2$ | Tổng thể chuẩn | $\chi^2_{n-1}$ | $\left[\frac{(n-1)s^2}{\chi^2_{\alpha/2}}, \frac{(n-1)s^2}{\chi^2_{1-\alpha/2}}\right]$ |
| $p$ | $n\hat{p} \ge 5$, $n(1-\hat{p}) \ge 5$ | $Z$ | $\hat{p} \pm z_{\alpha/2}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}$ |

---

## 4. Các lưu ý quan trọng

> [!warning] Checklist trước khi tính khoảng tin cậy
> 1. ✅ Xác định **tham số cần ước lượng** ($\mu$, $p$, hay $\sigma^2$)?
> 2. ✅ **Có biết $\sigma$** không? → Z hoặc $t$?
> 3. ✅ **Điều kiện tổng thể**: chuẩn hay không chuẩn? $n$ lớn hay nhỏ?
> 4. ✅ **Một phía hay hai phía?** → Khác nhau ở $z_\alpha$ vs $z_{\alpha/2}$, $t_\alpha$ vs $t_{\alpha/2}$.
> 5. ✅ Khi tính cỡ mẫu: **luôn làm tròn lên (ceiling)**.

> [!tip] Quy tắc ngón tay cái
> - Mẫu nhỏ + $\sigma$ chưa biết + tổng thể chuẩn → **$t$-interval**
> - Mẫu lớn ($n \ge 30$) + $\sigma$ chưa biết → **$t$-interval** vẫn đúng (không cần chuyển sang $Z$)
> - Mẫu lớn + $\sigma$ biết → **$Z$-interval**
