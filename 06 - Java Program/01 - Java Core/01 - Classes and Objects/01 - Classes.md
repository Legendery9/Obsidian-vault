# Java Classes

> [!abstract] Định nghĩa
> **Class (Lớp)** là một bản thiết kế (blueprint) hoặc khuôn mẫu định nghĩa các thuộc tính (fields) và hành vi (methods) chung cho các đối tượng. Lớp dùng để khởi tạo các đối tượng cụ thể (xem chi tiết tại [[02 - Objects]]).

---

## Cấu trúc thành phần cơ bản của Class

| Thành phần | Ký hiệu / Khai báo | Phạm vi / Vị trí | Tác dụng |
| --- | --- | --- | --- |
| **Package** | `package com.example;` | Dòng đầu tiên của source file | Nhóm các class liên quan thành một namespace tránh trùng tên. |
| **Import** | `import java.util.List;` | Sau package, trước khai báo class | Sử dụng các class thuộc package khác không cần chỉ định đường dẫn tuyệt đối. |
| **Class** | `public class Student {}` | Trong file `.java` cùng tên | Định nghĩa cấu trúc dữ liệu và hành vi của đối tượng. |

> [!info] Ví dụ cấu trúc tệp Java tiêu chuẩn
> ```java
> // ✅ Nên làm (Do): Đặt tên file khớp chính xác với public class bên trong.
> // HelloWorld.java
> package com.example;
> 
> import java.util.Date;
> 
> public class HelloWorld {
>     public void sayHello() {
>         System.out.println("Hello, World!");
>     }
> }
> ```

---

## Phân loại Class và Cấu trúc kế thừa

### 1. Abstract Class (Lớp trừu tượng)
- Không thể khởi tạo đối tượng trực tiếp bằng từ khóa `new`.
- Thường dùng làm lớp cha để định nghĩa các thuộc tính chung và bắt buộc lớp con triển khai (override) các phương thức trừu tượng.

```java
// ✅ Nên làm (Do): Sử dụng abstract class khi muốn chia sẻ code chung giữa các lớp con liên quan mật thiết.
abstract class Animal {
    abstract void makeVoid(); // Method trừu tượng không có thân hàm.
    
    void sleep() {
        System.out.println("Sleeping..."); // Method thông thường có thể kế thừa trực tiếp.
    }
}

class Dog extends Animal {
    @Override
    void makeVoid() {
        System.out.println("Woof");
    }
}
```

### 2. Interface (Giao diện)
- Là một "bản hợp đồng" định nghĩa các hành vi mà class triển khai bắt buộc phải thực hiện.
- Hỗ trợ đa kế thừa hành vi trong Java (một class có thể `implements` nhiều interface).

```java
interface Flyable {
    void fly(); // Mặc định là public abstract.
}

// ✅ Nên làm (Do): Triển khai interface để thiết lập hợp đồng hành vi cho các class không cùng phân hệ kế thừa.
class Bird implements Flyable {
    @Override
    public void fly() {
        System.out.println("Bird is flying...");
    }
}
```

### 3. Final Class (Lớp cuối cùng)
- Ngăn cản hoàn toàn việc kế thừa từ lớp này.

```java
// ❌ Không nên làm (Don't): Cố gắng kế thừa từ final class sẽ gây lỗi biên dịch.
final class MathUtil {}
// class AdvancedMath extends MathUtil {} // LỖI BIÊN DỊCH!
```

---

## Các kiểu dữ liệu Class đặc biệt

### 1. Record (Java 14+)
- Lớp bất biến (immutable) dùng để lưu trữ dữ liệu nhanh chóng, tự động sinh ra các hàm `getter` (dưới tên thuộc tính), `equals()`, `hashCode()`, và `toString()`.

```java
// ✅ Nên làm (Do): Sử dụng record cho các DTO (Data Transfer Objects) hoặc lớp chứa dữ liệu đơn thuần.
record UserDto(String username, int age) {}
```

### 2. Enum (Kiểu liệt kê)
- Tập hợp cố định các hằng số.

```java
enum Role {
    ADMIN, 
    USER, 
    GUEST
}
```

---

## Nested Classes (Lớp lồng nhau)

Lớp được khai báo bên trong một lớp khác nhằm mục đích tăng tính đóng gói.

| Loại Nested Class | Cách khai báo | Liên kết bộ nhớ |
| --- | --- | --- |
| **Static Nested Class** | `static class Inner {}` | Thuộc về Class ngoài, không cần đối tượng lớp ngoài. |
| **Inner Class (Non-static)** | `class Inner {}` | Thuộc về đối tượng lớp ngoài, phải khởi tạo lớp ngoài trước. |
| **Anonymous Class** | `new InterfaceName() {}` | Lớp không tên, định nghĩa và khởi tạo ngay tại chỗ (thường dùng một lần). |

> [!note] Lời giải & Ví dụ Anonymous Class
> ```java
> Runnable r = new Runnable() {
>     @Override
>     public void run() {
>         System.out.println("Running in anonymous class");
>     }
> };
> ```

---

## Lưu ý quan trọng

> [!warning]
> - Một tệp nguồn Java (`.java`) chỉ có thể chứa tối đa **một class public**, và tên tệp bắt buộc phải trùng khớp hoàn toàn với tên class public đó.
> - Việc sử dụng lạm dụng Anonymous Class có thể làm giảm khả năng đọc code. Trong Java 8+, khuyến khích sử dụng **Lambda Expression** thay thế cho Anonymous Class khi interface chỉ có một phương thức trừu tượng (Functional Interface).
