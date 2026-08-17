# Spring Boot Validation

> [!abstract] Định nghĩa
> **Validation (Xác thực dữ liệu)** đảm bảo dữ liệu gửi từ Client lên Server tuân thủ các quy tắc nghiệp vụ trước khi xử lý. 
> Spring Boot thực hiện xác thực thông qua thư viện Hibernate Validator (cài đặt của đặc tả **Jakarta Bean Validation**).

---

## 1. Các annotation xác thực phổ biến (`jakarta.validation.constraints`)

### So sánh @NotNull vs @NotEmpty vs @NotBlank

| Annotation | Giá trị `null` | Chuỗi rỗng `""` | Chuỗi khoảng trắng `" "` | Dùng cho kiểu |
| --- | --- | --- | --- | --- |
| **`@NotNull`** | ❌ Bị lỗi | ✅ Hợp lệ | ✅ Hợp lệ | Mọi đối tượng. |
| **`@NotEmpty`** | ❌ Bị lỗi | ❌ Bị lỗi | ✅ Hợp lệ | String, Collection, Array. |
| **`@NotBlank`** | ❌ Bị lỗi | ❌ Bị lỗi | ❌ Bị lỗi | Chỉ dành riêng cho String. |

### Các ràng buộc dữ liệu khác:

- **Dành cho Số:**
  - `@Min(value)` / `@Max(value)`: Giá trị tối thiểu / tối đa.
  - `@Positive` / `@Negative`: Số phải lớn hơn 0 / nhỏ hơn 0.
  - `@PositiveOrZero` / `@NegativeOrZero`: Số phải $\ge 0$ / $\le 0$.
- **Dành cho Ngày tháng:**
  - `@Past` / `@Future`: Thời gian phải ở trong quá khứ / tương lai so với hiện tại.
  - `@PastOrPresent` / `@FutureOrPresent`: Quá khứ hoặc hiện tại / Tương lai hoặc hiện tại.
- **Dành cho String đặc biệt:**
  - `@Email`: Kiểm tra định dạng hòm thư điện tử hợp lệ.
  - `@Pattern(regexp)`: Kiểm tra khớp biểu thức chính quy (Regex).
  - `@Size(min, max)`: Giới hạn số ký tự hoặc số lượng phần tử.

```java
// ✅ Nên làm (Do): Sử dụng các annotation chặt chẽ cho model dữ liệu.
public class RegisterForm {
    @NotBlank(message = "Tên đăng nhập không được bỏ trống")
    @Size(min = 3, max = 20, message = "Tên phải từ 3 đến 20 ký tự")
    private String username;

    @Email(message = "Email không hợp lệ")
    private String email;

    @Min(value = 18, message = "Tuổi đăng ký tối thiểu phải từ 18 tuổi")
    private int age;
}
```

---

## 2. Kích hoạt Validation bằng `@Valid` và `@Validated`

Để Spring Boot bắt đầu kiểm tra các điều kiện ràng buộc trong Controller, ta sử dụng `@Valid`:

```java
@PostMapping("/register")
public String processRegister(
    @Valid @ModelAttribute("user") RegisterForm form, 
    BindingResult result
) {
    if (result.hasErrors()) {
        return "register-form";
    }
    return "redirect:/success";
}
```

> [!important] Quy tắc vàng về vị trí của `BindingResult`
> Đối số **`BindingResult`** bắt buộc phải khai báo **ngay sau** đối tượng được đánh dấu `@Valid` hoặc `@Validated`. Nếu chèn các tham số khác như `Model` vào giữa, Spring Boot sẽ ném lỗi `MethodArgumentNotValidException` và crash luồng chạy.
> ```java
> // ✅ Nên làm (Do)
> public String save(@Valid User user, BindingResult result, Model model) {}
> 
> // ❌ Không nên làm (Don't)
> public String save(@Valid User user, Model model, BindingResult result) {} // LỖI CRASH HỆ THỐNG!
> ```

---

## 3. Các phương thức kiểm tra lỗi của `BindingResult`

- `hasErrors()`: Trả về `true` nếu đối tượng có bất kỳ lỗi xác thực nào.
- `hasFieldErrors(fieldName)`: Kiểm tra một field cụ thể có bị lỗi hay không.
- `getFieldError(fieldName)`: Lấy thông tin lỗi (`FieldError`) đầu tiên của field đó.
- `rejectValue(fieldName, errorCode, defaultMessage)`: Chủ động đăng ký thêm một lỗi tùy chỉnh (custom validation error) cho một field cụ thể (ví dụ: lỗi trùng lặp dữ liệu từ database).

```java
if (userRepository.existsByEmail(form.getEmail())) {
    // Chủ động ném lỗi trùng email vào BindingResult
    result.rejectValue("email", "duplicate.email", "Địa chỉ email đã được sử dụng");
}
```

---

## 4. Hiển thị lỗi trên giao diện Thymeleaf

Sử dụng thuộc tính `th:errors` và `th:errorclass` để kết xuất lỗi ra HTML:

```html
<form th:action="@{/register}" th:object="${user}" method="post">
    <div>
        <label>Tên đăng nhập:</label>
        <!-- th:errorclass tự động thêm class CSS "is-invalid" nếu field username có lỗi validation -->
        <input type="text" th:field="*{username}" th:errorclass="is-invalid">
        
        <!-- th:errors hiển thị chuỗi message lỗi cấu hình trong Java Model -->
        <div th:if="${#fields.hasErrors('username')}" th:errors="*{username}" class="error-msg"></div>
    </div>
</form>
```
