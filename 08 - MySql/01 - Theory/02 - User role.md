# Vai trò của Người dùng trong Hệ thống Cơ sở dữ liệu

---

## Định nghĩa
Trong một hệ quản trị cơ sở dữ liệu (DBMS), người dùng được phân chia thành các nhóm vai trò khác nhau tùy thuộc vào mức độ tương tác, mục đích công việc và đặc quyền bảo mật của họ đối với dữ liệu.

---

## Tác dụng
- **Đảm bảo bảo mật:** Áp dụng nguyên tắc đặc quyền tối thiểu (least privilege), ngăn chặn người dùng truy cập trái phép vào các bảng dữ liệu nhạy cảm.
- **Phân định trách nhiệm:** Phân chia rõ ràng công việc thiết kế, vận hành và khai thác cơ sở dữ liệu.
- **Tối ưu hóa tài nguyên:** Tránh xung đột tài nguyên hệ thống do truy vấn sai mục đích từ những người dùng không có chuyên môn.

---

## Bảng tham chiếu

### Phân loại các nhóm người dùng chính

| Nhóm vai trò | Mô tả công việc | Đặc quyền chính (Privileges) | Công cụ thường dùng |
| :--- | :--- | :--- | :--- |
| **Database Administrators (DBA)** | - Người quản trị toàn bộ hệ thống cơ sở dữ liệu.<br>- Quản lý tài nguyên, bảo mật, sao lưu và khôi phục dữ liệu. | `ALL PRIVILEGES`, `GRANT OPTION`, `CREATE USER`, `SHUTDOWN` | MySQL Workbench CLI, pgAdmin, Command Line |
| **Database Designers** | - Người phân tích yêu cầu nghiệp vụ và thiết kế mô hình dữ liệu (ERD).<br>- Xác định thực thể, quan hệ và các ràng buộc dữ liệu. | `CREATE`, `ALTER`, `DROP` trên cấu trúc bảng (DDL) | dbdiagram.io, Draw.io, Erwin |
| **Application Programmers** | - Lập trình viên phát triển ứng dụng kết nối tới DB.<br>- Viết các câu lệnh CRUD, tối ưu hóa câu query. | `SELECT`, `INSERT`, `UPDATE`, `DELETE` trên dữ liệu (DML) | IntelliJ IDEA, VS Code, DBeaver |
| **End Users (Người dùng cuối)** | - Người khai thác dữ liệu trực tiếp.<br>- Bao gồm người dùng thông thường (chỉ xem báo cáo) hoặc chuyên gia phân tích (viết truy vấn phức tạp). | Thường chỉ có quyền `SELECT` trên một số view hoặc bảng cụ thể. | BI Tools (Tableau, PowerBI), Excel |

---

## Ví dụ

### Cú pháp SQL phân quyền cơ bản trong MySQL

#### 1. Tạo người dùng mới
```sql
CREATE USER 'dev_user'@'localhost' IDENTIFIED BY 'secure_password';
```

#### 2. Phân quyền chỉ đọc (Read-only) cho người dùng cuối
```sql
GRANT SELECT ON company_db.employees TO 'dev_user'@'localhost';
```

#### 3. Cập nhật quyền lập tức
```sql
FLUSH PRIVILEGES;
```

---

## Lưu ý
> [!warning] Bảo mật tài khoản Root
> Tuyệt đối không sử dụng tài khoản `root` của cơ sở dữ liệu cho các ứng dụng chạy trong môi trường Production. Hãy tạo các tài khoản riêng biệt với đặc quyền tối thiểu để giảm thiểu thiệt hại nếu ứng dụng bị tấn công SQL Injection.
