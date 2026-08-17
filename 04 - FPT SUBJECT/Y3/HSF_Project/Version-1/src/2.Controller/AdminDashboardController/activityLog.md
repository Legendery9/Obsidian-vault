# 🎮 Method: activityLog (GET /admin/activity-log)

> [!abstract] Phân loại
> **Class:** `AdminDashboardController` | **Loại:** `Controller Method` — Admin-only GET handler
> **Package:** `com.example.groupproject.controller`

## 🗺️ Ánh xạ
- **HTTP Method:** `GET`
- **URL:** `/admin/activity-log`
- **Trả về view:** `admin/activity-log`
- **Quyền truy cập:** Chỉ `ADMIN` role

## 🎯 Tác dụng
Hiển thị trang Activity Log đầy đủ (searchable). Hiện tại đây là placeholder — chức năng đầy đủ được ghi chú là "coming in next sprint".

## 💉 Dependencies
- `AuthService authService` — kiểm tra role ADMIN

## 📥 Parameters & 📤 Return

```java
public String activityLog(HttpSession session)
// Return: "admin/activity-log"
```

**Return:** `String` — `"admin/activity-log"`
