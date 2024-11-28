# LAB5 - Thiết kế các hệ thống con trong hệ thống "Payroll System"

### 1. Authentication Subsystem
- Mục đích: Xử lý việc đăng nhập và xác thực người dùng.
- Thành phần:
  - `LoginForm:` Giao diện nhập thông tin đăng nhập.
  - `AuthenticationService:` Kiểm tra thông tin đăng nhập, xác thực dựa trên cơ sở dữ liệu người dùng.
  - `ISecureUser:` Giao diện quản lý phiên đăng nhập của người dùng.
  - `UserDatabase:` Lưu trữ thông tin người dùng.
- Tương tác chính: 
  - Người dùng nhập thông tin đăng nhập vào `LoginForm`.
  - `LoginForm` chuyển thông tin đến `AuthenticationService`.
  - `AuthenticationService` xác thực thông tin, trả về phiên người dùng nếu hợp lệ.

### 2. Timecard Management Subsystem
- Mục đích: Quản lý việc ghi lại giờ làm việc của nhân viên.
- Thành phần:
  - `TimecardForm:` Giao diện nhập liệu thời gian làm việc.
  - `TimecardController:` Xử lý logic nghiệp vụ liên quan đến thẻ chấm công.
  - `IProjectManagementDatabase:` Truy xuất và cập nhật dữ liệu dự án.
  - `Timecard:` Thực thể lưu trữ thông tin giờ làm việc.
- Tương tác chính:
  - Nhân viên nhập giờ làm việc thông qua `TimecardForm`.
  - `TimecardController` xác minh và cập nhật thông tin vào `IProjectManagementDatabase`.
  - Thẻ chấm công được lưu vào cơ sở dữ liệu thông qua lớp `PayrollDBManager`.

### 3. Payroll Processing Subsystem
- Mục đích: Xử lý bảng lương cho nhân viên.
- Thành phần:
  - `PayrollController:` Điều phối việc tính toán lương.
  - `IBankSystem:` Thực hiện giao dịch ngân hàng.
  - `IPrintService:` In phiếu lương cho nhân viên.
  - `PayrollDBManager:` Quản lý dữ liệu bảng lương và lưu trữ thông tin liên quan.
  - `Paycheck:` Thực thể lưu trữ thông tin về lương của nhân viên.
- Tương tác chính:
  - `PayrollController` lấy dữ liệu thẻ chấm công từ `PayrollDBManager`.
  - Tính toán lương dựa trên loại nhân viên (theo giờ, cố định, hoặc hoa hồng).
  - Lưu phiếu lương (`Paycheck`) vào cơ sở dữ liệu.
  - Gửi thông tin lương đến `IBankSystem` hoặc `IPrintService`.

### 4. Database Management Subsystem
- Mục đích: Cung cấp các dịch vụ quản lý dữ liệu cho hệ thống.
- Thành phần:
  - `PayrollDBManager:` Lớp singleton chịu trách nhiệm truy cập và quản lý cơ sở dữ liệu ObjectStore.
  - `Transaction:` Quản lý các hoạt động trong cơ sở dữ liệu theo giao dịch.
  - `Map:` Cấu trúc lưu trữ key-value cho dữ liệu nhân viên, thẻ chấm công và lệnh mua hàng.
- Tương tác chính:
  - Khởi tạo hoặc truy xuất dữ liệu qua `PayrollDBManager`.
  - Thực hiện các thao tác lưu, cập nhật, và xóa đối tượng (như `Employee`, `Timecard`, `Paycheck`).

### 5. Security Subsystem
- Mục đích: Bảo vệ dữ liệu và duy trì quyền truy cập an toàn.
- Thành phần:
  - `ISecureUser:` Xác thực quyền truy cập của người dùng trong hệ thống.
  - `SecurityAccess:` Xử lý các quyền như đọc, ghi, hoặc xóa dữ liệu.
- Tương tác chính:
  - `SecurityAccess` xác định quyền của người dùng đối với các thực thể như `Timecard` hoặc `Paycheck`.
  -  Hạn chế truy cập trái phép dựa trên vai trò người dùng.


