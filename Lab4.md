# LAB4 - Thiết kế các ca sử dụng cho hệ thống "Payroll System"

## 1. Login
### 1.1 Mô tả tương tác giữa các đối tượng thiết kế:
   - Đối tượng chính:
     - `LoginForm`: Giao diện nơi người dùng nhập thông tin đăng nhập.
     - `AuthenticationService`: Kiểm tra thông tin đăng nhập.
     - `Employee`: Đại diện cho người dùng sau khi đăng nhập thành công.
   - Quy trình:
     - Người dùng nhập thông tin đăng nhập vào `LoginForm`.
     - `LoginForm` chuyển thông tin đăng nhập đến `AuthenticationService`.
     - Nếu thông tin hợp lệ, `AuthenticationService` tạo phiên làm việc cho `Employee`.

### 1.2. Đơn giản hóa sơ đồ tuần tự bằng hệ thống con:
   - Hệ thống con: `Authentication Subsystem`.
   - Cách tiếp cận: Chuyển toàn bộ logic xác thực ra khỏi giao diện, tập trung vào `AuthenticationService`.
![Diagram](https://www.planttext.com/api/plantuml/png/R96nJiCm48RtUufJTrw00JK3PQbOKYHMOwp6gcDRjbFHcO6PYRKL0rAb3aXCoS3WleYVW5VWab8r0JnOFl_V_VVB_ce-npum5wfIWLz8ZSvu0Om7u_362mUMHCcbPJhWQ6hcKa-CAqV8F4udGpMhGY4qrIn8etFXbfABZipo8NbPMcLMuY1I0T3EmhCByiHpl2vIlRCOYlYXvnWerVvv_qX7tGb04A5PJkXLQdOILt5R8K_rMuKFSSEfCpNl78WuShUdwvulC1LmTXf3-gj5bPedG5g7Vif71hDKRmpQGiQjHXNN9IubSRm7Tjb_tEuYqOFKxTYrBf2tEWZbHN_oud3yDy0VNz9VvAyt4VeUnhIr7_aD003__mC0)
### 1.3. Mô tả hành vi liên quan đến lưu trữ:
   - Dữ liệu liên quan:
     - Tên người dùng và mật khẩu được truy xuất từ `UserDatabase`.
     - Thông tin phiên làm việc được lưu tạm thời trong bộ nhớ ứng dụng.

### 1.4. Tinh chỉnh mô tả luồng sự kiện:
   - Người dùng mở `LoginForm`.
   - Nhập tên người dùng và mật khẩu.
   - `LoginForm` gửi thông tin đến `AuthenticationService`.
   - `AuthenticationService` kiểm tra thông tin trong `UserDatabase`.
   - Nếu thông tin hợp lệ:
      - Tạo đối tượng `Employee`.
      - Hiển thị thông báo đăng nhập thành công.
   - Nếu không hợp lệ, hiển thị thông báo lỗi.

### 1.5. Hợp nhất các lớp và hệ thống con:
   - Các lớp liên quan:
     - `LoginForm`: Quản lý giao diện nhập liệu của người dùng.
     - `AuthenticationService`: Quản lý việc xác thực đăng nhập.
     - `Employee`: Đại diện cho người dùng đã được xác thực.

## 2. Trường hợp sử dụng: Duy trì thẻ chấm công
### 2.1. Mô tả tương tác giữa các đối tượng thiết kế:
   - Đối tượng chính:
     - `TimecardForm`: Giao diện để nhập giờ làm việc.
     - `TimecardController`: Xử lý logic nghiệp vụ liên quan đến thẻ chấm công.
     - `Timecard`: Lưu trữ thông tin về giờ làm việc.
   - Quy trình:
     1. Nhân viên nhập thông tin vào `TimecardForm`.
     2. Thông tin được chuyển đến `TimecardController`.
     3. `TimecardController` xử lý dữ liệu và lưu vào cơ sở dữ liệu qua `DatabaseService`.

### 2.2. Đơn giản hóa sơ đồ tuần tự bằng hệ thống con:
   - Hệ thống con: `Timecard Management Subsystem`.
   - Cách tiếp cận: Phân tách rõ ràng giữa việc nhập liệu (`TimecardForm`) và logic nghiệp vụ (`TimecardController`).
![Diagram](https://www.planttext.com/api/plantuml/png/RD4zJiCm50VmtQTuwiu5652bXBO3Oaa7LjUnY5L_HBPJYPc1WKFG38mL837XeKEatiCdu0eybxQgfIuUddx_zo7_XktOUMfzfoHnIw716iS9PTvOk5MjD4-SanQ1OAAbsiDeBXHdrDOJOzK8g8Fvv38eZFRMICdjFojoLb9F5zJnYjkLO7nloegGurIuki7MS0ttJVpPjE2RuLi_WiSTFLO2C7pV5R1K9YYJBz1FOzW8g6Fu02bYUEak-kBa7uQU9HA-s7dgGCeAoTtkipjVO3Mi3R1T3ow6joo4FEkhq_8QvA71MZVv0kd06KQVzrU5r-EKnT2RF33ckaw_z0S00F__0m00)
### 2.3. Mô tả hành vi liên quan đến lưu trữ:
   - Dữ liệu liên quan: Thông tin giờ làm việc được lưu trữ trong bảng `Timecards` của cơ sở dữ liệu.

### 2.4. Tinh chỉnh mô tả luồng sự kiện:
   - Nhân viên mở `TimecardForm`.
   - Nhập thông tin về ngày làm việc và số giờ làm.
   - Nhấn "Lưu" để gửi thông tin đến `TimecardController`.
   - `TimecardController` xác thực dữ liệu và lưu vào `DatabaseService`.
   - Hiển thị thông báo lưu thành công.

### 2.5. Hợp nhất các lớp và hệ thống con:
   - Các lớp liên quan:
     - `TimecardForm`: Quản lý giao diện nhập thông tin giờ làm việc.
     - `TimecardController`: Xử lý các nghiệp vụ liên quan đến thẻ chấm công.
     - `Timecard`: Lưu trữ thông tin về giờ làm việc của nhân viên.

## 3. Trường hợp sử dụng: Chạy bảng lương
### 3.1. Mô tả tương tác giữa các đối tượng thiết kế:
   - Đối tượng chính:
     - `PayrollController`: Điều phối quá trình tính lương.
     - `BankSystem`: Xử lý các giao dịch ngân hàng.
     - `PrintService`: Quản lý việc in phiếu lương.
     - `Paycheck`: Lưu trữ thông tin về lương của nhân viên.
   - Quy trình:
     - `PayrollController` truy xuất thông tin từ thẻ chấm công và tính toán lương.
     - Gửi kết quả tính toán đến `BankSystem` hoặc `PrintService`.

### 3.2. Đơn giản hóa sơ đồ tuần tự bằng hệ thống con:
   - Hệ thống con: `Payroll Processing Subsystem`.
   - Cách tiếp cận: Phân chia rõ ràng giữa xử lý giao dịch ngân hàng (`BankSystem`) và in phiếu lương (`PrintService`).
![Diagram](https://www.planttext.com/api/plantuml/png/V58zJiCm5DvzYgViN801LUc0a1WgfGEhvLgnbVIvE4wbp8nCt822AYIWWe4f6JeOzHu-0LVW9Q7GLe27Pyll-tkMFvhre73SkdAQioBJ2DOKad7XZ8KegGedfp3CZSWYDYEO5dh6qK4qufKrUJuqwDfTsWXu0QFXFYhccFKYNJjE3aIiHfT8EzT2zln30A-4acJUDNd5s7ucE3eXJpY6EDGl3jvlGlrGmcLPWRF-6HKulwAQRrut2qmPGRU4yr0l2QNy6wRWQ6wdGjs0eBgSWcYljt1U4NwyAqGm0ouqJtH4vUyGvje_8kEvWx7YhQ_n2wGW731j-yhVaY3GwaNZX3HFGxFIknaeVtD5ucL5EqAcJAZliQCHOHlzmYy4sOPwXP1gRc0IcckXcCmB2MS8CwL3lIw_f_vn7VtZglyW_kxRFHZDfBwUIkA43QYqt-WJ003__mC0)
### 3.3. Mô tả hành vi liên quan đến lưu trữ:
   - Dữ liệu liên quan:
     - Thông tin lương sau khi tính toán được lưu trong bảng `Paychecks`.
     - Các giao dịch ngân hàng được ghi nhận trong `TransactionLog`.

### 3.4. Tinh chỉnh mô tả luồng sự kiện:
   - `PayrollController` bắt đầu quy trình tính lương.
   - Lấy thông tin từ bảng `Timecards`.
   - Tính lương cho từng nhân viên theo loại (theo giờ, cố định, hoặc hoa hồng).
   - Tạo đối tượng `Paycheck` cho mỗi nhân viên.
   - Gửi thông tin:
      - Đến `BankSystem` để thực hiện chuyển khoản.
      - Hoặc đến `PrintService` để in phiếu lương.

### 3.5. Hợp nhất các lớp và hệ thống con:
   - Các lớp liên quan:
     - `PayrollController`: Điều phối việc tính toán và xử lý lương.
     - `BankSystem`: Quản lý giao dịch ngân hàng.
     - `PrintService`: Xử lý việc in phiếu lương.
     - `Paycheck`: Lưu thông tin chi tiết về lương của nhân viên.
