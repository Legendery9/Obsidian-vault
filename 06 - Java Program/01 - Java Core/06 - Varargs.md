# Java Variable Arguments (Varargs)

> [!abstract] Định nghĩa
> **Variable Arguments (Varargs)** ký hiệu là `...`, cho phép truyền một số lượng tham số linh hoạt (từ 0, 1, đến nhiều tham số cùng kiểu) vào trong phương thức mà không cần tạo mảng thủ công.

---

## Bản chất và Cách hoạt động

Khi trình biên dịch gặp cú pháp `...`, nó tự động biên dịch và chuyển đổi tham số đó thành một mảng thông thường:

```java
// Khai báo Varargs
public void printNames(String... names) {
    // Bên trong phương thức, "names" thực chất là một mảng String[]
    for (String name : names) {
        System.out.println(name);
    }
}
```

Trình biên dịch Java sẽ tự động chuyển các cách gọi hàm thành mảng:
- `printNames()` → Biên dịch thành `printNames(new String[]{})` (mảng rỗng).
- `printNames("An")` → Biên dịch thành `printNames(new String[]{"An"})`.
- `printNames("An", "Bình")` → Biên dịch thành `printNames(new String[]{"An", "Bình"})`.

---

## So sánh: Varargs vs Mảng thông thường (Array Parameter)

| Đặc tính | Array Parameter | Varargs |
| --- | --- | --- |
| **Cách gọi phương thức** | Bắt buộc khởi tạo mảng (`new String[]{"a", "b"}`) | Truyền trực tiếp các đối số rời nhau (`"a"`, `"b"`) |
| **Tính linh hoạt** | Kém linh hoạt, viết code dài dòng | Rất linh hoạt, mã nguồn sạch sẽ hơn |
| **Bên trong phương thức** | Là một mảng | Là một mảng |
| **Truyền 0 đối số** | Bắt buộc truyền `null` hoặc mảng rỗng | Gọi trống không cần đối số |

---

## Quy tắc bắt buộc khi sử dụng Varargs

Khi thiết kế phương thức có sử dụng Varargs, bạn phải tuân thủ nghiêm ngặt 2 quy tắc sau:

### Quy tắc 1: Tham số Varargs phải nằm cuối cùng trong danh sách tham số

Nếu có nhiều tham số, Varargs bắt buộc phải đặt ở vị trí cuối cùng của phương thức để Java có thể phân biệt các đối số truyền vào.

```java
// ✅ Nên làm (Do): Varargs đặt ở cuối danh sách.
public void assignSkills(String jobTitle, String... skills) {
    // ...
}

// ❌ Không nên làm (Don't): Đặt Varargs lên trước các tham số khác gây lỗi biên dịch.
// public void badAssign(String... skills, String jobTitle) { // LỖI BIÊN DỊCH!
// }
```

### Quy tắc 2: Chỉ được phép có tối đa duy nhất 1 tham số Varargs trong một phương thức

```java
// ❌ Không nên làm (Don't): Khai báo 2 tham số Varargs trong cùng 1 method.
// public void logDetails(String... names, int... ages) { // LỖI BIÊN DỊCH!
// }
```

---

## Khả năng tương thích nâng cao

Phương thức nhận Varargs hoàn toàn chấp nhận một mảng được tạo sẵn truyền vào trực tiếp:

```java
String[] skillsArray = {"Java", "Spring Boot", "SQL"};
// Truyền trực tiếp mảng thay vì truyền rời rạc
assignSkills("Backend Developer", skillsArray);
```
