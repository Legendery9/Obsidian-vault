# Java Data Types

> [!abstract] Định nghĩa
> **Kiểu dữ liệu (Data Type)** phân loại dữ liệu lưu trữ, chỉ định lượng bộ nhớ cấp phát và tập hợp các phép toán hợp lệ trên biến đó.

---

## 1. Phân loại Kiểu dữ liệu trong Java

Java chia làm 2 nhóm kiểu dữ liệu chính:

1. **Kiểu dữ liệu nguyên thủy (Primitive Types):** Lưu trữ giá trị thực tế trực tiếp trong bộ nhớ Stack. Có 8 kiểu dữ liệu nguyên thủy (xem chi tiết tại [[03 - Primitive]]).
2. **Kiểu dữ liệu tham chiếu (Reference Types):** Lưu trữ địa chỉ tham chiếu (địa chỉ vùng nhớ Heap) trỏ đến đối tượng thực tế. Bao gồm:
   - Các Class (ví dụ: [[04 - Wrapper Class|Wrapper Classes]], [[01 - String|String]], custom classes).
   - Interfaces.
   - Arrays (Mảng).

---

## 2. Ép kiểu dữ liệu (Type Casting)

Ép kiểu là việc chuyển đổi giá trị từ kiểu dữ liệu này sang kiểu dữ liệu khác.

### 2.1. Ép kiểu ngầm định (Widening / Implicit Casting)
- Diễn ra tự động khi chuyển từ kiểu dữ liệu có kích thước nhỏ hơn sang kiểu dữ liệu có kích thước lớn hơn (không gây mất mát dữ liệu).
- Thứ tự: `byte` $\rightarrow$ `short` $\rightarrow$ `char` $\rightarrow$ `int` $\rightarrow$ `long` $\rightarrow$ `float` $\rightarrow$ `double`.

```java
int myInt = 9;
double myDouble = myInt; // Tự động ép kiểu thành 9.0
```

### 2.2. Ép kiểu tường minh (Narrowing / Explicit Casting)
- Phải thực hiện thủ công bằng cách đặt kiểu dữ liệu mong muốn trong dấu ngoặc đơn `()` trước giá trị/biến khi chuyển từ kiểu lớn hơn sang kiểu nhỏ hơn.
- Có thể gây mất mát dữ liệu (mất phần thập phân hoặc tràn số).
- Thứ tự: `double` $\rightarrow$ `float` $\rightarrow$ `long` $\rightarrow$ `int` $\rightarrow$ `char` $\rightarrow$ `short` $\rightarrow$ `byte`.

```java
// ✅ Nên làm (Do): Ép kiểu tường minh có chủ đích và lường trước mất mát dữ liệu.
double myDouble = 9.78;
int myInt = (int) myDouble; // myInt = 9 (mất phần thập phân .78)
```
