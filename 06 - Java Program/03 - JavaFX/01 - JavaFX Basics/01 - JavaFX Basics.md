# JavaFX Basics

> [!abstract] Định nghĩa
> **JavaFX** là một nền tảng đồ họa (graphics platform) của Java dùng để xây dựng các ứng dụng desktop (Desktop Applications) với giao diện người dùng phong phú (Rich Client Applications).

---

## 1. Kiến trúc cơ bản: Stage, Scene và Node

Giao diện người dùng trong JavaFX được tổ chức theo mô hình rạp hát (Theater metaphor):

```text
    Stage (Cửa sổ ứng dụng)
      └─ Scene (Nền giao diện chứa các thành phần)
           └─ Parent Layout (BorderPane, VBox, HBox...)
                └─ Nodes (Button, Label, TextField...)
```

- **`Stage`:** Cửa sổ chính của ứng dụng (do nền tảng JavaFX cung cấp khi khởi chạy ứng dụng).
- **`Scene`:** Vùng chứa các thành phần đồ họa của giao diện. Một Stage chỉ có thể hiển thị một Scene tại một thời điểm.
- **`Node`:** Các thành phần giao diện nhỏ nhất (Controls như Button, TextField hoặc Layouts như VBox, Gridpane).

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.StackPane;
import javafx.stage.Stage;

public class MyJavaFxApp extends Application {
    @Override
    public void start(Stage primaryStage) {
        Button btn = new Button("Nhấn vào đây");
        StackPane root = new StackPane(btn);
        
        // Tạo một Scene có kích thước 300x250 và đặt root layout vào
        Scene scene = new Scene(root, 300, 250);
        
        primaryStage.setTitle("JavaFX Demo");
        primaryStage.setScene(scene); // Đặt Scene vào Stage
        primaryStage.show();          // Hiển thị cửa sổ
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

---

## 2. Các Control nhập liệu thông dụng (UI Controls)

| Control | Tên lớp Java | Mục đích sử dụng | Ví dụ code |
| --- | --- | --- | --- |
| **Label** | `Label` | Hiển thị văn bản chỉ đọc (không cho sửa). | `Label label = new Label("Username:");` |
| **TextField** | `TextField` | Nhập văn bản một dòng. | `TextField txt = new TextField();` |
| **Button** | `Button` | Tạo nút bấm thực thi sự kiện. | `Button btn = new Button("Submit");` |
| **ImageView** | `ImageView` | Hiển thị hình ảnh từ nguồn dẫn. | `ImageView img = new ImageView(image);` |

```java
// ✅ Nên làm (Do): Sử dụng prompt text để gợi ý cho người dùng nhập dữ liệu.
TextField nameField = new TextField();
nameField.setPromptText("Nhập tên đăng nhập...");
```

---

## 3. Cấu hình module JavaFX (`module-info.java`)

Khi chạy ứng dụng JavaFX từ phiên bản Java 9 trở lên, bạn cần khai báo các module trong tệp `module-info.java` đặt ở thư mục gốc của package:

```java
module com.example.myjavafxapp {
    requires javafx.controls;
    requires javafx.fxml;

    opens com.example.myjavafxapp to javafx.graphics, javafx.fxml;
    exports com.example.myjavafxapp;
}
```

---

## 4. Các thư viện mở rộng phổ biến của JavaFX

Để xây dựng ứng dụng chuyên nghiệp, nhà phát triển thường tích hợp thêm các thư viện sau:

- **BootstrapFX:** Thư viện CSS hỗ trợ áp dụng các class style giống hệt Bootstrap vào JavaFX controls.
- **ControlsFX:** Cung cấp các controls nâng cao chất lượng cao (như AutoCompleteTextField, BreadCrumbBar, PopOver).
- **FormsFX:** Giúp thiết lập và sinh nhanh các form nhập liệu có kiểm duyệt dữ liệu tự động.
- **Ikonli:** Hỗ trợ tích hợp hàng ngàn icon từ FontAwesome, MaterialDesign vào JavaFX.
- **ValidatorFX:** Hỗ trợ xác thực tính hợp lệ dữ liệu nhập của form trực quan.
- **FXGL:** Framework phát triển game 2D nhẹ nhàng viết bằng JavaFX.
