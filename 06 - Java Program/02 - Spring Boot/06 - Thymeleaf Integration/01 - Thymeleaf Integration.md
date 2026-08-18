# Thymeleaf Integration

> [!abstract] Định nghĩa
> **Thymeleaf** là một công cụ xử lý mẫu HTML hiện đại (template engine), tích hợp chặt chẽ với Spring Boot để render dữ liệu phía server (Server-Side Rendering) thông qua các thuộc tính mở rộng HTML chuẩn.

---

## 1. Khai báo và Các cú pháp biểu thức (Expressions)

Để sử dụng Thymeleaf, bắt buộc khai báo namespace ở thẻ `<html>`:

```html
<html xmlns:th="http://www.thymeleaf.org">
```

### 5 Loại biểu thức cốt lõi của Thymeleaf:

| Cú pháp | Loại biểu thức | Tác dụng | Ví dụ |
| --- | --- | --- | --- |
| **`${...}`** | Variable Expression | Lấy dữ liệu thuộc tính từ `Model` gửi từ Controller. | `th:text="${user.name}"` |
| **`*{...}`** | Selection Expression | Lấy thuộc tính của đối tượng được chỉ định ở `th:object`. | `th:field="*{email}"` |
| **`@{...}`** | Link URL Expression | Xử lý đường dẫn tĩnh, động và Controller mappings. | `th:href="@{/css/style.css}"` |
| **`#{...}`** | Message Expression | Đọc dữ liệu quốc tế hóa từ file cấu hình `.properties`. | `th:text="#{welcome.title}"` |
| **`~{...}`** | Fragment Expression | Nhúng hoặc kế thừa các khối layout HTML dùng chung. | `th:replace="~{layout/header}"` |

---

## 2. Bảng thuộc tính (Attributes) thông dụng trong Thymeleaf

| Thuộc tính HTML | Tác dụng | Ví dụ |
| --- | --- | --- |
| `th:text` | Gán nội dung dạng văn bản thô (Tự động escape mã độc HTML). | `<p th:text="${msg}"></p>` |
| `th:utext` | Gán nội dung HTML (Không escape). | `<div th:utext="${rawHtml}"></div>` |
| `th:value` | Gán giá trị mặc định cho thẻ input, option. | `<input th:value="${user.id}">` |
| `th:if` / `th:unless` | Hiển thị thẻ HTML nếu điều kiện đúng / sai. | `<span th:if="${user.isAdmin}">Admin</span>` |
| `th:each` | Vòng lặp duyệt qua một tập hợp dữ liệu. | `<li th:each="u : ${users}" th:text="${u}"></li>` |
| `th:object` | Khai báo đối tượng gốc xử lý dữ liệu cho Form. | `<form th:object="${loginForm}">` |
| `th:field` | Liên kết trường thuộc tính hai chiều với đối tượng form. | `<input th:field="*{username}">` |
| `th:errors` | Kết xuất văn bản lỗi validation tương ứng của field. | `<span th:errors="*{username}"></span>` |

---

## 3. Quản lý vòng lặp và Trạng thái lặp (Iteration Status)

Khi sử dụng `th:each`, ta có thể khai báo thêm biến thứ hai để kiểm soát trạng thái của vòng lặp:

```html
<table>
    <tr th:each="user, status : ${users}">
        <!-- status.count: Số thứ tự bắt đầu từ 1 -->
        <td th:text="${status.count}"></td>
        <td th:text="${user.name}"></td>
        <!-- status.even: Trả về true nếu là dòng số chẵn -->
        <td th:text="${status.even ? 'Dòng Chẵn' : 'Dòng Lẻ'}"></td>
    </tr>
</table>
```

Các thuộc tính của biến trạng thái lặp (`status`):
- `index`: Chỉ số bắt đầu từ 0.
- `count`: Chỉ số bắt đầu từ 1.
- `size`: Tổng số lượng phần tử trong collection.
- `even` / `odd`: Kiểm tra hàng chẵn / hàng lẻ.
- `first` / `last`: Kiểm tra có phải phần tử đầu tiên / cuối cùng không.

---

## 4. Xây dựng Layout dùng chung (Fragments)

Để tránh lặp lại mã nguồn ở các trang (như Header, Footer), sử dụng cơ chế `th:fragment` và `th:replace` (hoặc `th:insert`):

### Bước 1: Định nghĩa fragment (`templates/fragments/header.html`)
```html
<header th:fragment="main-header">
    <h1>Hệ Thống Quản Lý Thiết Bị</h1>
    <nav>
        <a th:href="@{/devices}">Thiết bị</a> | <a th:href="@{/categories}">Danh mục</a>
    </nav>
</header>
```

### Bước 2: Sử dụng fragment ở trang khác (`templates/devices.html`)
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Devices</title>
</head>
<body>
    <!-- th:replace sẽ thay thế hoàn toàn thẻ div này bằng thẻ header định nghĩa ở trên -->
    <div th:replace="~{fragments/header :: main-header}"></div>
    
    <h2>Danh sách thiết bị</h2>
</body>
</html>
```
