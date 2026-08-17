# Package Overview — com.example.groupproject

> [!abstract]
> Toàn bộ source code của ứng dụng **TalentHub** nằm trong package gốc `com.example.groupproject`. Cấu trúc được tổ chức theo kiến trúc **Layered Architecture** (phân tầng rõ ràng), bao gồm 7 package con.

---

## 📁 Cấu trúc Package

```
com.example.groupproject/
├── GroupProjectApplication.java   ← Entry point
├── config/       ← Cấu hình Spring MVC, Security, Data init
├── controller/   ← Nhận HTTP request, điều phối luồng xử lý
├── dto/          ← Data Transfer Object (form input / view output)
├── entity/       ← JPA Entity — ánh xạ với bảng database
├── exception/    ← Custom Exception classes
├── repository/   ← Spring Data JPA — truy vấn database
└── service/      ← Business logic
```

---

## 🗂️ Vai Trò Từng Package

| Package | Vai trò | Annotation chính |
|---|---|---|
| `config` | Cấu hình runtime của ứng dụng | `@Configuration`, `@Component` |
| `controller` | Xử lý HTTP request/response | `@Controller`, `@GetMapping`, `@PostMapping` |
| `dto` | Đóng gói dữ liệu truyền giữa các tầng | `@Valid`, `@NotBlank` |
| `entity` | Định nghĩa schema database | `@Entity`, `@Table`, `@Id` |
| `exception` | Custom exception cho business rule | `extends RuntimeException` |
| `repository` | Interface truy vấn database | `extends JpaRepository` |
| `service` | Xử lý business logic | `@Service`, `@Transactional` |

---

## 🔄 Luồng Dữ Liệu Tổng Quát

```
HTTP Request
    ↓
[controller] ← nhận request, validate DTO
    ↓
[service]    ← xử lý business logic, gọi repository
    ↓
[repository] ← truy vấn database qua JPA
    ↓
[entity]     ← object ánh xạ với database row
    ↑
[dto]        ← wrap data trả về cho view
    ↑
[controller] → trả về View (Thymeleaf template)
```

> [!note]
> Chi tiết từng package xem tại các note con trong thư mục này.
