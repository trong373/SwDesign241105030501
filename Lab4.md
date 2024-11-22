# LAB4 - Thiết kế các ca sử dụng cho hệ thống "Payroll System"

## 1. Login
### 1.1 Mô tả tương tác giữa các đối tượng thiết kế:
   - Đối tượng chính:
     - `LoginForm`: Giao diện nơi người dùng nhập thông tin đăng nhập.
     - `AuthenticationService`: Kiểm tra thông tin đăng nhập.
     - `Employee`: Đại diện cho người dùng sau khi đăng nhập thành công.
   - Quy trình:
     1. Người dùng nhập thông tin đăng nhập vào `LoginForm`.
     2. `LoginForm` chuyển thông tin đăng nhập đến `AuthenticationService`.
     3. Nếu thông tin hợp lệ, `AuthenticationService` tạo phiên làm việc cho `Employee`.

### 1.2. Đơn giản hóa sơ đồ tuần tự bằng hệ thống con:
   - Hệ thống con: `Authentication Subsystem`.
   - Cách tiếp cận: Chuyển toàn bộ logic xác thực ra khỏi giao diện, tập trung vào `AuthenticationService`.

### 1.3. Mô tả hành vi liên quan đến lưu trữ:
   - Dữ liệu liên quan:
     - Tên người dùng và mật khẩu được truy xuất từ `UserDatabase`.
     - Thông tin phiên làm việc được lưu tạm thời trong bộ nhớ ứng dụng.

### 1.4. Tinh chỉnh mô tả luồng sự kiện:
   1. Người dùng mở `LoginForm`.
   2. Nhập tên người dùng và mật khẩu.
   3. `LoginForm` gửi thông tin đến `AuthenticationService`.
   4. `AuthenticationService` kiểm tra thông tin trong `UserDatabase`.
   5. Nếu thông tin hợp lệ:
      - Tạo đối tượng `Employee`.
      - Hiển thị thông báo đăng nhập thành công.
   6. Nếu không hợp lệ, hiển thị thông báo lỗi.

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

### 2.3. Mô tả hành vi liên quan đến lưu trữ:
   - Dữ liệu liên quan: Thông tin giờ làm việc được lưu trữ trong bảng `Timecards` của cơ sở dữ liệu.

### 2.4. Tinh chỉnh mô tả luồng sự kiện:
   1. Nhân viên mở `TimecardForm`.
   2. Nhập thông tin về ngày làm việc và số giờ làm.
   3. Nhấn "Lưu" để gửi thông tin đến `TimecardController`.
   4. `TimecardController` xác thực dữ liệu và lưu vào `DatabaseService`.
   5. Hiển thị thông báo lưu thành công.

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
     1. `PayrollController` truy xuất thông tin từ thẻ chấm công và tính toán lương.
     2. Gửi kết quả tính toán đến `BankSystem` hoặc `PrintService`.

### 3.2. Đơn giản hóa sơ đồ tuần tự bằng hệ thống con:
   - Hệ thống con: `Payroll Processing Subsystem`.
   - Cách tiếp cận: Phân chia rõ ràng giữa xử lý giao dịch ngân hàng (`BankSystem`) và in phiếu lương (`PrintService`).

### 3.3. Mô tả hành vi liên quan đến lưu trữ:
   - Dữ liệu liên quan:
     - Thông tin lương sau khi tính toán được lưu trong bảng `Paychecks`.
     - Các giao dịch ngân hàng được ghi nhận trong `TransactionLog`.

### 3.4. Tinh chỉnh mô tả luồng sự kiện:
   1. `PayrollController` bắt đầu quy trình tính lương.
   2. Lấy thông tin từ bảng `Timecards`.
   3. Tính lương cho từng nhân viên theo loại (theo giờ, cố định, hoặc hoa hồng).
   4. Tạo đối tượng `Paycheck` cho mỗi nhân viên.
   5. Gửi thông tin:
      - Đến `BankSystem` để thực hiện chuyển khoản.
      - Hoặc đến `PrintService` để in phiếu lương.

### 3.5. Hợp nhất các lớp và hệ thống con:
   - Các lớp liên quan:
     - `PayrollController`: Điều phối việc tính toán và xử lý lương.
     - `BankSystem`: Quản lý giao dịch ngân hàng.
     - `PrintService`: Xử lý việc in phiếu lương.
     - `Paycheck`: Lưu thông tin chi tiết về lương của nhân viên.
