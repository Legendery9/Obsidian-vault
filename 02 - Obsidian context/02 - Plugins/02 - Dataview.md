# Dataview trong Obsidian

---

## Định nghĩa
Dataview là một công cụ truy vấn mạnh mẽ biến Obsidian vault của bạn thành một cơ sở dữ liệu có thể tìm kiếm, liệt kê, và tổng hợp thông tin từ metadata (frontmatter/inline fields) của các ghi chú.

---

## Tác dụng
- **Tự động hóa danh sách:** Tạo danh sách các bài viết chưa hoàn thành, các cuốn sách đang đọc, v.v.
- **Truy vấn theo điều kiện:** Lọc ghi chú dựa trên tags, folder, ngày tạo, trạng thái.
- **Trình bày đa dạng:** Hiển thị kết quả dưới dạng List, Table, Task, hoặc Calendar.

---

## Bảng tham chiếu

### Cú pháp truy vấn cơ bản (Dataview Query Language - DQL)

| Từ khóa | Ý nghĩa | Ví dụ |
| :--- | :--- | :--- |
| `LIST` | Hiển thị kết quả dạng danh sách | `LIST` |
| `TABLE` | Hiển thị dạng bảng với các cột dữ liệu | `TABLE file.ctime AS "Ngày tạo"` |
| `TASK` | Hiển thị các checklist nhiệm vụ | `TASK` |
| `FROM` | Xác định nguồn (tags, folders, links) | `FROM #java` hoặc `FROM "06 - Java Program"` |
| `WHERE` | Điều kiện lọc dữ liệu | `WHERE file.mtime > date(today) - dur(7 days)` |
| `SORT` | Sắp xếp kết quả | `SORT file.name ASC` hoặc `SORT rating DESC` |
| `GROUP BY` | Gom nhóm kết quả | `GROUP BY file.folder` |

---

## Ví dụ

### 1. Truy vấn danh sách ghi chú có tag `#java` được tạo gần đây
```markdown
```dataview
LIST
FROM #java
SORT file.ctime DESC
LIMIT 5
```
```

### 2. Truy vấn dạng bảng quản lý dự án hoặc môn học
```markdown
```dataview
TABLE status AS "Trạng thái", priority AS "Độ ưu tiên"
FROM "Project"
WHERE status != "Completed"
SORT priority DESC
```
```

---

## Lưu ý
> [!important] Metadata định nghĩa
> Để Dataview hoạt động tốt, hãy khai báo metadata ở đầu file bằng cú pháp YAML Frontmatter:
> ```yaml
> ---
> tag: java
> status: "In Progress"
> priority: 3
> ---
> ```
