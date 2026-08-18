# Java Primitive Types

> [!abstract] Định nghĩa
> **Kiểu dữ liệu nguyên thủy (Primitive Types)** là các kiểu dữ liệu cơ bản được xây dựng sẵn trong Java, lưu trữ trực tiếp các giá trị thô trên bộ nhớ Stack. Java cung cấp 8 kiểu dữ liệu nguyên thủy để tối ưu hóa hiệu năng hệ thống. Mỗi kiểu nguyên thủy đều có một đối tượng bọc tương ứng (xem chi tiết tại [[04 - Wrapper Class]]).

---

## 1. Bảng chi tiết 8 kiểu dữ liệu nguyên thủy

| Kiểu dữ liệu | Số bit | Phạm vi giá trị | Giá trị mặc định | Mục đích phổ biến |
| --- | --- | --- | --- | --- |
| `byte` | 8 | -128 $\rightarrow$ 127 | `0` | Tiết kiệm bộ nhớ (mảng dữ liệu thô, luồng I/O). |
| `short` | 16 | -32,768 $\rightarrow$ 32,767 | `0` | Dùng trong lập trình nhúng, hệ thống phần cứng nhỏ. |
| `int` | 32 | $-2^{31} \rightarrow 2^{31}-1$ | `0` | Kiểu số nguyên mặc định được dùng nhiều nhất. |
| `long` | 64 | $-2^{63} \rightarrow 2^{63}-1$ | `0L` | Số nguyên lớn (ID database, timestamp). **Cần hậu tố L**. |
| `float` | 32 | $\pm1.4\text{E}-45 \rightarrow \pm3.4\text{E}38$ | `0.0f` | Số thực độ chính xác đơn. **Cần hậu tố f**. |
| `double` | 64 | $\pm4.9\text{E}-324 \rightarrow \pm1.8\text{E}308$ | `0.0d` | Số thực mặc định độ chính xác kép. |
| `char` | 16 | $0 \rightarrow 65,535$ (Unicode) | `'\u0000'` | Lưu trữ một ký tự đơn (khai báo nháy đơn `'A'`). |
| `boolean` | JVM quyết định | `true` hoặc `false` | `false` | Điều kiện rẽ nhánh logic. |

---

## 2. Lưu ý về hậu tố số nguyên và số thực

- **Hậu tố `L` hoặc `l` cho kiểu `long`:** Mặc định Java hiểu các số nguyên viết ra là kiểu `int`. Nếu số nguyên vượt quá phạm vi của `int`, ta phải thêm hậu tố `L` hoặc `l` (khuyến khích dùng chữ hoa `L` để tránh nhầm với số `1`).
- **Hậu tố `f` hoặc `F` cho kiểu `float`:** Mặc định Java hiểu các số thực có phần thập phân viết ra là kiểu `double`. Muốn gán cho biến `float` bắt buộc phải thêm hậu tố `f` hoặc `F`.

```java
// ✅ Nên làm (Do): Sử dụng hậu tố chính xác.
long databaseId = 9876543210L; 
float temperature = 36.5f;

// ❌ Không nên làm (Don't): Thiếu hậu tố gây lỗi biên dịch.
// long badId = 9876543210; // LỖI: Integer number too large!
// float badTemp = 36.5;    // LỖI: Type mismatch: cannot convert from double to float!
```
