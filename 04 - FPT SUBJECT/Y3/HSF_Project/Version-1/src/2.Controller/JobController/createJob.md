# 🎮 Method: createJob (GET /jobs/new)

> [!abstract] Phân loại
> **Class:** `JobController` | **Loại:** `Controller Method` — HR/Admin GET handler
> **Package:** `com.example.groupproject.controller`
> **Base mapping:** `@RequestMapping("/jobs")`

## 🗺️ Ánh xạ
- **HTTP Method:** `GET`
- **URL:** `/jobs/new`
- **Trả về view:** `jobs/form`
- **Quyền truy cập:** `ADMIN` hoặc `HR_MANAGER` (kiểm tra bởi `AuthInterceptor` cho path `/jobs/**`)

## 🎯 Tác dụng
Hiển thị form tạo Job Posting mới. Hiện tại là placeholder — form đầy đủ "coming in next sprint".

## 📥 Parameters & 📤 Return

```java
public String createJob()
// Return: "jobs/form"
```

**Return:** `String` — `"jobs/form"` (không có dependency inject, không có parameters)
