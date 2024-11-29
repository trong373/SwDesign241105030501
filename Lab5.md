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
![Diagram](https://www.planttext.com/api/plantuml/png/X9CnJiCm58RtdCBgL2IuG8IgGX48GIL4uG2kyvHOJPw3xGHLY04nC7C011rOa2eniD0C3AcuHqx05R13sgQqWYn9tllzlJ_-uw_iewqqbJg9GaSDE18f53Wif4gHO-5pt1So8bSECLUYG2ADm2KzBJdwPJ4soaiXlQMYIleHryqDbwI2UywrKn5t4Xq0QiwevW9x85FEeAAdDEGUrT2Hu5aD3LNpzyJDbN5cnAuG8L0i8QRBVJmrXNBjOLrN-LkOOGoKwWZKKeIL2HO06vo0ZBW12MoQJcquPTRscj5pPW_ATLsAr0TPGSiDhZghjieTiZ90RoPIF_TLtNpGkS7iKKtxL44j7kMIBestPuQjgbKsVT3sPML73TZMBNWHzzPMQtrKBcaS5DcO4ntaR-WJRNwOwVtqrZnYK4p6SSDP7x4brYqRq9bCXYGj9izOfw7_-Lfa3vnu-JlwV-6MuhF6yX6IYsHOP3U6QE7iFqVBQHd6KL1aZ-RhYib8a3ZW-GkIC7-AICgBx8urdBO9oHwLRm000F__0m00)
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
![Diagram](https://www.planttext.com/api/plantuml/png/X9BDIiGm58NtVOfBLnMS5oWo33ee0mg20xfDqqiR9pybIGiYFimWBWK5LtRXek1xz0by1TEV6PtQmQmk9oVVoRt9L_anCvPecmlkcHMJe9L1Zt9Y32oPG4fqVAgqW7iFt4fLhisrqYkCGrX8YmdgTiFaaM0sE0YXK2ps7hm1uqH9gnNdg7jIGJYBYSMD8R1z4MxFEDYnKXo9x298yOzxFBeFH95nTOUuS6Ukh6OoQULCgrkaTg2sVOOmLtd4yGTvsPddn9A86Ep9FSBvBqXsr54EDzxfJhUz6Fn9_TMhIzkP_6Go7HbZ2FvPNJupi6dr9XEmxkreMhy_2Q2Du7iZeszGWnuSvwPQKuUforSAedg4s5LGhULUn78xVF_yyoNVVuKPohZvMTy0003__mC0)
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
![Diagram](https://www.planttext.com/api/plantuml/png/T99DQiCm48NtFiMGLGlD1Km98Ic5G1U5v08JUMgBoAEWdu0fNPGkUef2i-Y-wtYHHI7ty0bwXSgfdRJvqKA2ftdlqqZwBjTzwz0udwl8pYI3qPOYeT1QkCV2QAM6cbszae772C8Gg8HNw2WKN50-LxeW6YKnZ9sHd5x6SAFzLD6sE2KcyrihCXApquPsDtgAzl2jqZ2FNLiPS-tP_GCc0HQ4CE_39Z8dWIO9AaxHKXFg6jd6S2UjksxBUit9NIlOqwS-CErm0-JPcCn2YXt98Di7ChUUJuPT7NGImWTQAqAkKuyVejlj7JKLGsTYV06BQlN1uBAgV9EGIcHGN-yvB6HLlehEcR3skkkGQhNKCCzajLfxK9lFpPBJSxu_hGRhCFD5LRu4Ue0zyzxS9qxgB_O3003__mC0)
### 4. Database Management Subsystem
- Mục đích: Cung cấp các dịch vụ quản lý dữ liệu cho hệ thống.
- Thành phần:
  - `PayrollDBManager:` Lớp singleton chịu trách nhiệm truy cập và quản lý cơ sở dữ liệu ObjectStore.
  - `Transaction:` Quản lý các hoạt động trong cơ sở dữ liệu theo giao dịch.
  - `Map:` Cấu trúc lưu trữ key-value cho dữ liệu nhân viên, thẻ chấm công và lệnh mua hàng.
- Tương tác chính:
  - Khởi tạo hoặc truy xuất dữ liệu qua `PayrollDBManager`.
  - Thực hiện các thao tác lưu, cập nhật, và xóa đối tượng (như `Employee`, `Timecard`, `Paycheck`).

![Diagram](https://www.planttext.com/api/plantuml/png/Z991IiGm58RtEKMOrRYO2nGfmr0HGK5mBl0cVKx397abIOKYhbru2F447g0BTzwZ9_0AfZLncCuWPb78-yENxxtcg_jOEW_MDrenjvE6MtB8X0Bd-2sqbfGgLZTWO8kMFp8Ubh087Wlmi067yxECFv0inwX6UqzMhoqO1y9BCdCqNlesutVUIhCDXrT42i6m9nQlkT2reXOnucMP3ezR0neF2a5fN_Y5hAL60RQC48pCgqDOHOrr6I-esIWSAsLe9HJ2TyyAVOiAnUvl5cXgZFyFR1nY7DU46MIkfVFdQGRvcFhOJ4fJSpzf7VLIcdJpuTAZVxPOv5E7ZCyk9H0l--v5L5nyld7NTw_3_fqhsNVFpOnDlGTEiZmP9icJON9aIpJbyDQ-0G00__y30000)
### 5. Security Subsystem
- Mục đích: Bảo vệ dữ liệu và duy trì quyền truy cập an toàn.
- Thành phần:
  - `ISecureUser:` Xác thực quyền truy cập của người dùng trong hệ thống.
  - `SecurityAccess:` Xử lý các quyền như đọc, ghi, hoặc xóa dữ liệu.
- Tương tác chính:
  - `SecurityAccess` xác định quyền của người dùng đối với các thực thể như `Timecard` hoặc `Paycheck`.
  -  Hạn chế truy cập trái phép dựa trên vai trò người dùng.

![Diagram](https://www.planttext.com/api/plantuml/png/R96nJiCm48PtFyKf4qZq1QAgAZ15Oa2ja5WjzoWMgPtUdP4inC2ZC30oi3O30q-I9-0LC6dIj51lT_RttM_xk_wSicYIi2eLFrW7v1cLAJKppD44iXBFZS5KFYb8wn79tiLhf9LbjjxnIM2aOf73NCYwvHbe8wdVrwSvN7XVedOjlYJjP2ly1nAo3sJm2Fgikan56mfl4je5iZj3Mr823XhL43M7AyiotcvE1kci6zmP-np5eLbYDPWJ--TvHgF9VheSijklLmDotzGV1jOXDlMBouvHizsziyjcyrRrXq4eH33DvhtAr1JTulUJVW000F__0m00)

