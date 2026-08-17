# 00 - Thymeleaf Reference Table

Tài liệu này cung cấp bảng tham chiếu tổng hợp các biểu thức cú pháp và thuộc tính cấu hình cốt lõi của công cụ tạo mẫu Thymeleaf theo nguyên lý 20/80, tích hợp chặt chẽ với Spring Boot MVC.

---

## 1. Cú pháp Biểu thức (Standard Expression Syntax)

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `${...}` | Biểu thức biến (Variable Expression). | Truy xuất và hiển thị dữ liệu từ các thuộc tính (model attributes) truyền từ Controller sang. | Đặt trực tiếp trong thuộc tính Thymeleaf. Ví dụ: `<p th:text="${user.name}">Tên</p>`. | Hỗ trợ truy cập thuộc tính lồng nhau qua toán tử chấm (`user.address.street`). |
| `*{...}` | Biểu thức chọn biến (Selection Expression). | Truy xuất thuộc tính của đối tượng đã được chọn từ thẻ cha thông qua thuộc tính `th:object`. | Sử dụng trong các thẻ con của khối chứa `th:object`. Ví dụ: `<div th:object="${user}"><p th:text="*{name}"></p></div>`. | Tiện lợi khi tạo biểu mẫu nhập liệu (form) liên kết đối tượng dữ liệu. |
| `#{...}` | Biểu thức thông điệp (Message Expression). | Lấy chuỗi thông điệp đa ngôn ngữ (Localization/i18n) từ tệp cấu hình `.properties`. | Ví dụ: `<h1 th:text="#{home.welcome.title}">Chào mừng</h1>`. | Phụ thuộc vào cấu hình các tệp tài nguyên ngôn ngữ (như `messages_vi.properties`, `messages_en.properties`). |
| `@{...}` | Biểu thức URL liên kết (Link URL Expression). | Tạo các đường dẫn URL động, tự động bổ sung ngữ cảnh context path của ứng dụng web. | Ví dụ cho link tĩnh: `<a th:href="@{/css/style.css}">`. Ví dụ link động có biến: `<a th:href="@{/users/detail(id=${user.id})}">`. | Luôn khuyên dùng biểu thức này thay vì viết URL tĩnh để tránh lỗi đường dẫn khi deploy ứng dụng lên server. |
| `~{...}` | Biểu thức phân đoạn (Fragment Expression). | Tham chiếu tới các phân đoạn mã HTML (fragments) để tái sử dụng bố cục (layout layouts). | Thường dùng kết hợp với `th:replace` hoặc `th:insert`. Ví dụ: `<div th:replace="~{fragments/header :: main-nav}"></div>`. | Hỗ trợ truyền tham số vào fragment để hiển thị tùy biến. |

---

## 2. Các Thuộc tính cốt lõi (Standard Attribute Processors)

### A. Xuất dữ liệu & Điều kiện

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `th:text` | Xuất chữ thuần túy. | Ghi đè nội dung hiển thị của thẻ bằng dữ liệu đã được escape ký tự HTML (an toàn XSS). | Ví dụ: `<span th:text="${message}">Nội dung</span>`. | Nếu biểu thức trả về `null`, nội dung thẻ sẽ bị xóa trống. |
| `th:utext` | Xuất HTML chưa escape. | Ghi đè nội dung và render các thẻ HTML nằm trong chuỗi dữ liệu (Unescaped Text). | Ví dụ: `<div th:utext="${htmlContent}">Nội dung</div>`. | [!WARNING] Cực kỳ nguy hiểm nếu chuỗi HTML chứa dữ liệu nhập từ người dùng không được lọc, dễ bị hack XSS. |
| `th:if` | Điều kiện hiển thị (Đúng). | Render và hiển thị thẻ HTML chứa nó chỉ khi giá trị điều kiện trả về `true` hoặc truthy. | Ví dụ: `<div th:if="${user.isAdmin}">Quản trị viên</div>`. | Các giá trị `false`, `null`, `0`, `"false"` đều được đánh giá là sai và thẻ sẽ bị ẩn khỏi DOM. |
| `th:unless` | Điều kiện hiển thị (Ngược). | Ngược lại của `th:if`, chỉ hiển thị thẻ khi giá trị điều kiện trả về `false` hoặc falsy. | Ví dụ: `<div th:unless="${user.isLoggedIn}">Khách</div>`. | Hoạt động như phủ định (`!condition`). |
| `th:switch` / `th:case` | Rẽ nhánh đa điều kiện. | So sánh giá trị biểu thức trong `th:switch` với các giá trị trong `th:case`. | Thẻ con nào khớp sẽ hiển thị, các thẻ case khác bị loại bỏ. Case mặc định dùng dấu sao `*`. | Xem ví dụ minh họa chi tiết ở phần dưới bài viết. |

### B. Vòng lặp & Biểu mẫu

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `th:each` | Vòng lặp duyệt danh sách. | Lặp qua các phần tử của một Collection (List, Map, Set, Array) và nhân bản thẻ HTML tương ứng. | Ví dụ: `<li th:each="user : ${users}" th:text="${user.name}"></li>`. | Có thể lấy đối tượng trạng thái lặp (iteration status) bằng cách khai báo thêm biến. Ví dụ: `th:each="user, iterStat : ${users}"`. |
| `th:object` | Khai báo đối tượng biểu mẫu. | Chọn một đối tượng dữ liệu làm gốc để liên kết dữ liệu form. | Thường khai báo ở thẻ `<form>`. Ví dụ: `<form th:action="@{/save}" th:object="${newUser}" method="POST">`. | Các input con bên trong form sẽ sử dụng `*{...}` để trích xuất thuộc tính đối tượng này. |
| `th:field` | Liên kết trường nhập liệu. | Tạo tự động các thuộc tính `id`, `name`, và gán `value` cho thẻ input tương ứng với thuộc tính của đối tượng form. | Ví dụ: `<input type="text" th:field="*{email}">`. | Trong Spring MVC, `th:field` hỗ trợ cơ chế tự động validate dữ liệu (Spring Validation) hiển thị lỗi. |
| `th:errors` | Hiển thị thông báo lỗi. | Hiển thị các lỗi validation liên quan đến trường nhập liệu được chỉ định. | Ví dụ: `<span th:if="${#fields.hasErrors('email')}" th:errors="*{email}">Lỗi email</span>`. | Chỉ hiển thị nếu có lỗi xảy ra sau quá trình submit form. |

### C. Tùy biến thuộc tính HTML & Bố cục

| Tag / Statement / Method | Definition | Tác dụng | Cách dùng / Phạm vi | Lưu ý |
|---|---|---|---|---|
| `th:classappend` | Thêm class CSS động. | Thêm trực tiếp các class CSS vào thuộc tính `class` có sẵn của thẻ mà không ghi đè chúng. | Ví dụ thêm class active cho menu: `<a class="nav-link" th:classappend="${currentPage == 'home'} ? 'active'">`. | Rất tiện để giữ lại các class định dạng CSS cơ bản của framework như Bootstrap. |
| `th:attr` / `th:attrappend` | Thêm thuộc tính HTML động. | Thiết lập giá trị cho các thuộc tính HTML chuẩn hoặc tùy biến. | Thường dùng viết gộp các thuộc tính. Nhưng khuyến nghị sử dụng thuộc tính đặc thù hơn như `th:disabled`, `th:checked`. | Ví dụ: `<button th:disabled="${!isFormValid}">Gửi</button>`. |
| `th:fragment` | Định nghĩa phân đoạn. | Đặt tên định danh cho một vùng giao diện để có thể gọi tái sử dụng ở các trang khác. | Ví dụ định nghĩa footer chung: `<footer th:fragment="app-footer">...</footer>`. | Thường đặt trong thư mục `templates/fragments/`. |
| `th:replace` | Thay thế phân đoạn. | Thay thế hoàn toàn thẻ chứa thuộc tính này bằng nội dung của fragment được gọi tới. | Ví dụ: `<div th:replace="~{fragments/header :: header-fragment}"></div>`. | Thẻ `<div>` khai báo ngoài sẽ bị xóa bỏ hoàn toàn trong mã nguồn render cuối cùng. |
| `th:insert` | Chèn phân đoạn vào trong. | Chèn nội dung của fragment được gọi vào làm con bên trong thẻ chứa nó. | Ví dụ: `<div th:insert="~{fragments/header :: header-fragment}"></div>`. | Thẻ `<div>` khai báo ngoài vẫn được giữ lại và bao bọc lấy fragment con. |

---

## Ví dụ thực tế: Liên kết Biểu mẫu (Spring Boot Form Binding)

Dưới đây là một form đăng ký sản phẩm, liên kết với đối tượng Java `Product` gửi từ Controller.

```html
<!-- Khai báo đối tượng th:object="${product}" -->
<form th:action="@{/admin/products/save}" th:object="${product}" method="POST">
    
    <!-- Trường ẩn lưu ID sản phẩm (khi cập nhật) -->
    <input type="hidden" th:field="*{id}">

    <div class="form-group">
        <label for="productName">Tên sản phẩm:</label>
        <!-- th:field tự sinh ra id="productName" và name="productName" -->
        <input type="text" id="productName" th:field="*{name}" class="form-control">
        <!-- Hiển thị lỗi validate nếu có -->
        <div class="error-msg" th:if="${#fields.hasErrors('name')}" th:errors="*{name}">Lỗi tên</div>
    </div>

    <div class="form-group">
        <label for="price">Giá bán (USD):</label>
        <input type="number" id="price" th:field="*{price}" class="form-control">
        <div class="error-msg" th:if="${#fields.hasErrors('price')}" th:errors="*{price}">Lỗi giá</div>
    </div>

    <div class="form-group">
        <label>Trạng thái sản phẩm:</label>
        <div>
            <!-- th:field tự động tích chọn checkbox nếu isAvailable là true -->
            <input type="checkbox" id="isAvailable" th:field="*{isAvailable}">
            <label for="isAvailable">Đang kinh doanh</label>
        </div>
    </div>

    <button type="submit" class="btn btn-primary">Lưu sản phẩm</button>
</form>
```

---

## Ví dụ thực tế: Duyệt danh sách & Cú pháp Switch-Case

Duyệt danh sách đơn hàng của khách hàng, hiển thị màu sắc trạng thái khác nhau tương ứng với từng tình trạng của đơn hàng.

```html
<table>
    <thead>
        <tr>
            <th>STT</th>
            <th>Mã đơn hàng</th>
            <th>Tên khách hàng</th>
            <th>Trạng thái</th>
        </tr>
    </thead>
    <tbody>
        <!-- Duyệt danh sách orders, iterStat lưu trạng thái đếm -->
        <tr th:each="order, iterStat : ${orders}">
            <!-- Hiển thị số thứ tự tăng dần từ 1 -->
            <td th:text="${iterStat.count}">1</td>
            <td th:text="${order.code}">ORD-001</td>
            <td th:text="${order.customerName}">Nguyễn Văn A</td>
            
            <!-- Cấu trúc Switch-Case phân loại trạng thái -->
            <td th:switch="${order.status}">
                <span th:case="'PENDING'" class="badge badge-warning">Chờ xử lý</span>
                <span th:case="'SHIPPING'" class="badge badge-info">Đang giao</span>
                <span th:case="'DELIVERED'" class="badge badge-success">Đã giao</span>
                <span th:case="'CANCELLED'" class="badge badge-danger">Đã hủy</span>
                <span th:case="*" class="badge badge-secondary">Không xác định</span>
            </td>
        </tr>
        <!-- Hiển thị dòng thông báo nếu danh sách đơn hàng trống -->
        <tr th:if="${#lists.isEmpty(orders)}">
            <td colspan="4" style="text-align: center; color: gray;">Không có đơn hàng nào.</td>
        </tr>
    </tbody>
</table>
```

---

## Ví dụ thực tế: Tái sử dụng Layout với Fragment

### Bước 1: Định nghĩa layout chung (ví dụ: `templates/layout/main-layout.html`)
```html
<!DOCTYPE html>
<html lang="vi" th:fragment="base-layout(contentPage)">
<head>
    <meta charset="UTF-8">
    <title>Trang Quản Trị Hệ Thống</title>
    <!-- CSS dùng chung -->
    <link rel="stylesheet" th:href="@{/css/admin.css}">
</head>
<body>

    <!-- Header chung -->
    <header th:replace="~{fragments/header :: header-nav}"></header>

    <!-- Nội dung thay đổi động giữa các trang -->
    <main class="container">
        <!-- Chèn trang nội dung con truyền vào qua tham số -->
        <div th:replace="${contentPage}"></div>
    </main>

    <!-- Footer chung -->
    <footer th:replace="~{fragments/footer :: footer-info}"></footer>

</body>
</html>
```

### Bước 2: Viết nội dung trang con (ví dụ: `templates/admin/dashboard.html`)
```html
<!-- Kế thừa base-layout và truyền phần nội dung con qua fragment expression -->
<div th:replace="~{layout/main-layout :: base-layout(~{:: #dashboard-content})}">
    
    <!-- Đoạn mã nội dung con sẽ được truyền đi -->
    <div id="dashboard-content">
        <h2>Bảng Điều Khiển Hệ Thống</h2>
        <div class="metrics">
            <div class="metric-card">Tổng doanh thu: 1,500$</div>
            <div class="metric-card">Thành viên mới: 120</div>
        </div>
    </div>

</div>
```
