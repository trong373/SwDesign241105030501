# LAB3 - Xác định các phần tử thiết kế của hệ thống “Payroll System”

## 1. Biểu đồ ngữ cảnh hệ thống con:
 a. BankSystem:
 - Biểu đồ Ngữ Cảnh:
   ![Context Diagram](https://www.planttext.com/api/plantuml/png/TCmnIWGn5CRnFgVuIYq6-oqMMHXiXPqBP6EO33FpefbaOP0j5aihR-0g8YpOMKsABU95SWAlO0ABg63xV-_xVVh3-M2viQxlsD0s1AC7oHWNLXiiEBNBSR2o1n-mM1vpsLztUfGonv8PAIodkfEuvAFHNNTSt3ByAKKnJmXck8Z-hS4OzWuYJgyETSCrhgA_5mf2kJ7wEqAhT9oUAJ5vLUJrRs-6ogGFhAFVeetJmUB6vV2JEwbKUAJ4XdUgpoeLfnUBLPnspUctF4UPCPLVi0ex_Q_syP0E15BXYR1kmfxOvWi00F__0m00)
- Giải thích các thành phần trong biểu đồ ngữ cảnh BankSystem:
  + PayrollSystem:
    * Đây là hệ thống bảng lương chính, gửi các yêu cầu thanh toán lương qua ngân hàng.
    * Các yêu cầu này bao gồm việc tạo giao dịch chuyển khoản cho các nhân viên được thanh toán qua tài khoản ngân hàng.
  + BankSystem:
    * Hệ thống ngân hàng xử lý các giao dịch chuyển khoản cho nhân viên.
    * Sau khi xử lý xong, hệ thống sẽ gửi xác nhận trạng thái giao dịch (thành công hoặc thất bại) về cho PayrollSystem.
    * Nếu giao dịch thành công, hệ thống ngân hàng sẽ thông báo cho nhân viên.
  + Employee:
    * Nhân viên nhận thông báo về giao dịch chuyển khoản thành công từ hệ thống ngân hàng.
      
b. PrintService:
 - Biểu đồ Ngữ Cảnh:

   ![Context Diagram](https://www.planttext.com/api/plantuml/png/R90_IWGn6CNxdE9TO2zW8TiCjWjZOPlDXaamaqYI4O9OMti31n51MBImoXHRHFOUEO5NC1d_eApjU-_ttiVtFksMpbFhXruHTourh76S4CgyiLZHO8rIRN2Uzw0Eg_RBQVeBPGBdLMpm7RTIUsxd80Ynd7cgEyK_ZPRRIyauhWXGYh0u_giVuIHFMucGdWQm71y7b7FMETxh3ch_iXzrDwE_eLhoGsxoz0mbytGpuEqsnvr6dyPGQcOEYyF9ipGoQ97ZLjSrBzAT5c3fzV-jfY2dehfOfz5KH9Y2mEVuuCarMNAzgQ_y0000__y30000)
 - Giải thích các thành phần trong biểu đồ ngữ cảnh PrintService:
   + PayrollSystem:
     * Là hệ thống bảng lương chính, chịu trách nhiệm gửi yêu cầu in phiếu lương cho PrintService khi phương thức thanh toán không phải là chuyển khoản.
     * Sau khi nhận được xác nhận từ PrintService, hệ thống bảng lương cập nhật trạng thái thanh toán.
   + PrintService:
     * Hệ thống in ấn phiếu lương cho nhân viên. Nó xử lý các yêu cầu in từ PayrollSystem.
     * Sau khi in phiếu lương thành công, nó gửi phiếu lương đến nhân viên và trả về trạng thái in cho hệ thống bảng lương.
   + Employee:
     * Nhân viên nhận phiếu lương từ hệ thống PrintService nếu phương thức thanh toán là nhận trực tiếp hoặc qua thư.
       
c. ProjectManagementDatabase:
- Biểu đồ Ngữ Cảnh:
  
    ![Context Diagram](https://www.planttext.com/api/plantuml/png/ZD0zQW9150VmVaxnlu0Ni0Y2RYaiR9gKB-jZDSx7ClCci8Y74H4Xa4AmYaMAEOady0gPbJG1arY-hnz_tkNqEGf2NgBHAYmN5ju5LbIByoYfyqxhgWl21XHGLlWU5QRLhcFkkmMKybmBsKOpIkzUSZ4bImqRjZ8XeMSAZ9K2Uc8mUFXZQuYdz1PHdp_s4IPjqSxJEsRdqm5fOw_4hxTNkSh4EDgc9tRjRQBuDyIZZnrUis0XytJCdEJdt1-Z-9dYbh5M8xQp_l5V0000__y30000)
- Giải thích các thành phần trong biểu đồ ngữ cảnh ProjectManagementDatabase:
  + PayrollSystem:
    * Hệ thống bảng lương yêu cầu thông tin về mã phí dự án để tính toán báo cáo lương hoặc tạo báo cáo chi tiết về các dự án mà nhân viên tham gia.
    * Sau khi nhận thông tin từ ProjectManagementDatabase, hệ thống sẽ hiển thị cho nhân viên nếu cần thiết.
  + ProjectManagementDatabase:
    * Là cơ sở dữ liệu quản lý các dự án, lưu trữ thông tin chi tiết về các mã phí và dự án mà nhân viên tham gia.
    * Nó gửi thông tin về mã phí dự án theo yêu cầu từ PayrollSystem.
  + Employee:
    * Nhân viên có thể xem thông tin về các mã phí dự án khi hệ thống bảng lương hiển thị thông tin này.


## 2. Ánh xạ Lớp Phân Tích đến Phần Tử Thiết Kế:

a. Employee :
- Lớp phân tích: 
  + Nhiệm vụ: Lưu trữ thông tin về nhân viên, bao gồm lương, phúc lợi và phương thức thanh toán.
- Phần tử thiết kế:
  + EmployeeDAO: Data Access Object để truy cập dữ liệu nhân viên từ cơ sở dữ liệu.
  + EmployeeService: Lớp dịch vụ để xử lý logic nghiệp vụ liên quan đến nhân viên, như tính toán phúc lợi hoặc xác minh thông tin.
  + EmployeeController: Lớp bộ điều khiển để xử lý các yêu cầu từ giao diện người dùng liên quan đến thông tin nhân viên.

b. Timecard :
- Lớp phân tích: 
  + Nhiệm vụ: Lưu trữ thông tin về giờ làm việc của nhân viên, bao gồm giờ làm thêm.
- Phần tử thiết kế:
  + TimecardDAO: Data Access Object để truy cập dữ liệu bảng chấm công từ cơ sở dữ liệu.
  + TimecardService: Lớp dịch vụ xử lý nghiệp vụ liên quan đến bảng chấm công, bao gồm việc thêm mới, cập nhật và truy vấn dữ liệu bảng chấm công.
  + TimecardController: Lớp bộ điều khiển xử lý yêu cầu từ giao diện người dùng về việc nhập, cập nhật và xóa bảng chấm công.

c. PurchaseOrder :
- Lớp phân tích:
  + Nhiệm vụ: Lưu trữ thông tin về các đơn đặt hàng của nhân viên hưởng hoa hồng.
- Phần tử thiết kế:
  + PurchaseOrderDAO: Data Access Object để truy cập dữ liệu đơn đặt hàng từ cơ sở dữ liệu.
  + PurchaseOrderService: Lớp dịch vụ xử lý nghiệp vụ liên quan đến đơn đặt hàng, bao gồm tính toán hoa hồng cho nhân viên.
  + PurchaseOrderController: Lớp bộ điều khiển xử lý các yêu cầu từ giao diện người dùng liên quan đến quản lý đơn đặt hàng.

d. PayrollSystem :
- Lớp phân tích:
  - Nhiệm vụ: Quản lý toàn bộ quy trình xử lý bảng lương, bao gồm tính toán lương và xử lý thanh toán.
- Phần tử thiết kế:
  - PayrollService: Lớp dịch vụ xử lý nghiệp vụ chính của hệ thống bảng lương, bao gồm tính toán lương dựa trên giờ làm, đơn đặt hàng và các khoản khấu trừ.
  - PayrollController: Lớp bộ điều khiển xử lý các yêu cầu liên quan đến quy trình bảng lương từ giao diện người dùng.
  - PayrollScheduler: Thành phần để tự động khởi chạy bảng lương vào thứ Sáu hàng tuần và ngày làm việc cuối cùng của tháng.

e. BankSystem :
- Lớp phân tích:
  + Nhiệm vụ: Thực hiện các giao dịch thanh toán trực tiếp vào tài khoản ngân hàng của nhân viên.
- Phần tử thiết kế:
  + BankAdapter: Adapter để tích hợp với hệ thống ngân hàng bên ngoài, xử lý các giao dịch ngân hàng.
  + BankService: Lớp dịch vụ xử lý các thao tác với hệ thống ngân hàng, như gửi yêu cầu giao dịch và xác minh trạng thái.

f. Paycheck :
- Lớp phân tích: 
  + Nhiệm vụ: Lưu trữ thông tin chi tiết về phiếu lương của nhân viên, bao gồm các khoản khấu trừ.
- Phần tử thiết kế:
  + PaycheckGenerator: Lớp để tạo phiếu lương cho nhân viên dựa trên các thông tin về lương, giờ làm, và khấu trừ.
  + PaycheckPrinter: Lớp xử lý việc in phiếu lương nếu phương thức nhận lương không phải là chuyển khoản.

g. ProjectManagementDatabase :
- Lớp phân tích: 
  - Nhiệm vụ: Lưu trữ thông tin về các dự án mà nhân viên tham gia.
- Phần tử thiết kế:
  - ProjectDAO: Data Access Object để truy cập thông tin dự án từ cơ sở dữ liệu.
  - ProjectService: Lớp dịch vụ xử lý các yêu cầu về thông tin dự án, như lấy danh sách mã phí dự án hoặc thông tin chi tiết về dự án.

# Tóm tắt Ánh xạ Lớp Phân Tích đến Phần Tử Thiết Kế

| Lớp Phân Tích              | Phần Tử Thiết Kế                                                                                          |
|----------------------------|-----------------------------------------------------------------------------------------------------------|
| `Employee`                 | `EmployeeDAO`, `EmployeeService`, `EmployeeController`                                                    |
| `Timecard`                 | `TimecardDAO`, `TimecardService`, `TimecardController`                                                    |
| `PurchaseOrder`            | `PurchaseOrderDAO`, `PurchaseOrderService`, `PurchaseOrderController`                                     |
| `PayrollSystem`            | `PayrollService`, `PayrollController`, `PayrollScheduler`                                                 |
| `BankSystem`               | `BankAdapter`, `BankService`                                                                              |
| `Paycheck`                 | `PaycheckGenerator`, `PaycheckPrinter`                                                                    |
| `ProjectManagementDatabase`| `ProjectDAO`, `ProjectService`                                                                            |

## 3. Ánh xạ các phần tử thiết kế vào các gói:
Dưới đây là cách ánh xạ lại các phần tử thiết kế của hệ thống Payroll System mà không cần sử dụng gói `entity`, thay vào đó sẽ gộp các lớp đại diện dữ liệu vào gói `model` hoặc `dao` tùy thuộc vào vai trò của chúng:

a. Package `model`:
- Mô tả: Chứa các lớp đại diện cho dữ liệu chính trong hệ thống, bao gồm cả dữ liệu nhân viên, bảng chấm công, đơn đặt hàng và phiếu lương.
- Các phần tử thiết kế:
  + `Employee`: Đại diện cho thông tin của nhân viên.
  + `Timecard`: Đại diện cho thông tin của bảng chấm công.
  + `PurchaseOrder`: Đại diện cho thông tin của đơn đặt hàng.
  + `Paycheck`: Đại diện cho phiếu lương của nhân viên.

b. Package `dao`:
- Mô tả: Chứa các lớp quản lý việc truy cập và thao tác với cơ sở dữ liệu.
- Các phần tử thiết kế:
  + `EmployeeDAO`: Truy cập và thao tác dữ liệu nhân viên trong cơ sở dữ liệu.
  + `TimecardDAO`: Truy cập và thao tác dữ liệu bảng chấm công trong cơ sở dữ liệu.
  + `PurchaseOrderDAO`: Truy cập và thao tác dữ liệu đơn đặt hàng trong cơ sở dữ liệu.
  + `ProjectDAO`: Truy cập và thao tác dữ liệu về các dự án trong cơ sở dữ liệu.

c. Package `service`:
- Mô tả: Chứa các lớp xử lý logic nghiệp vụ chính của hệ thống.
- Các phần tử thiết kế:
  + `EmployeeService`: Xử lý các nghiệp vụ liên quan đến nhân viên như tính toán phúc lợi.
  + `TimecardService`: Xử lý các nghiệp vụ liên quan đến bảng chấm công như thêm, sửa và xóa dữ liệu.
  + `PurchaseOrderService`: Xử lý các nghiệp vụ liên quan đến đơn đặt hàng như tính toán hoa hồng.
  + `PayrollService`: Xử lý các nghiệp vụ chính của hệ thống bảng lương, bao gồm tính toán lương.
  + `BankService`: Xử lý giao dịch với hệ thống ngân hàng.
  + `ProjectService`: Xử lý các yêu cầu về thông tin dự án từ hệ thống bảng lương hoặc nhân viên.

d. Package `controller`:
- Mô tả: Chứa các lớp xử lý yêu cầu từ giao diện người dùng hoặc từ các hệ thống bên ngoài, điều hướng các yêu cầu đến các lớp dịch vụ.
- Các phần tử thiết kế:
  + `EmployeeController`: Xử lý các yêu cầu từ giao diện người dùng liên quan đến thông tin nhân viên.
  + `TimecardController`: Xử lý các yêu cầu từ giao diện người dùng về việc quản lý bảng chấm công.
  + `PurchaseOrderController`: Xử lý các yêu cầu từ giao diện người dùng về quản lý đơn đặt hàng.
  + `PayrollController`: Xử lý các yêu cầu từ giao diện người dùng liên quan đến quy trình bảng lương.

e. Package `adapter` :
- Mô tả: Chứa các lớp chịu trách nhiệm tích hợp và kết nối với các hệ thống bên ngoài.
- Các phần tử thiết kế:
  + `BankAdapter`: Adapter để tích hợp với hệ thống ngân hàng bên ngoài, xử lý giao dịch chuyển khoản.

f. Package `utility` :
- Mô tả: Chứa các lớp hỗ trợ, các chức năng chung không thuộc về các lớp dịch vụ hoặc bộ điều khiển cụ thể.
- Các phần tử thiết kế:
  + `PaycheckGenerator`: Lớp tạo phiếu lương cho nhân viên dựa trên thông tin lương và khấu trừ.
  + `PaycheckPrinter`: Lớp in phiếu lương nếu phương thức nhận lương không phải là chuyển khoản.

h. Package `scheduler` :
- Mô tả: Chứa các lớp quản lý việc tự động hóa các tác vụ như tính toán bảng lương.
- Các phần tử thiết kế:
  + `PayrollScheduler`: Lập lịch tự động cho việc chạy bảng lương theo thời gian biểu định trước.

# Tóm tắt Ánh xạ các Phần Tử Thiết Kế 

| Package              | Các phần tử thiết kế                                                                                        |
|----------------------|-------------------------------------------------------------------------------------------------------------|
| `model`               | `Employee`, `Timecard`, `PurchaseOrder`, `Paycheck`                                                         |
| `dao`                 | `EmployeeDAO`, `TimecardDAO`, `PurchaseOrderDAO`, `ProjectDAO`                                              |
| `service`             | `EmployeeService`, `TimecardService`, `PurchaseOrderService`, `PayrollService`, `BankService`, `ProjectService` |
| `controller`          | `EmployeeController`, `TimecardController`, `PurchaseOrderController`, `PayrollController`                  |
| `adapter`             | `BankAdapter`                                                                                               |
| `utility`             | `PaycheckGenerator`, `PaycheckPrinter`                                                                      |
| `scheduler`           | `PayrollScheduler`                                                                                          |

## 4.Vẽ biểu đồ mô tả các layers trong hệ thống và quan hệ giữa chúng:

![Diagram](https://www.planttext.com/api/plantuml/png/T9D1IWCn58RtESMZ-rx0XRHL474KjIg2T17JE8PEav1a2eEuSk7A8mXs8O9Gx5O7SJ4mzvWJU0KpwLGdqvfLUE___hpy8T_fLqSRh4myZf0UCGvAQ8gGn6I4GmgjGqKrvGOR9ZW4EA6g1JS8xBeurLJ1BZTKNM521u1kQrnNoeYHTTYMu4Q9AA9gi2ZqgPemQ-3nlLWpJhM6G8ICD2pyPcLpXYCsT0VwJjlOOEWIulIUpJ6LGZCZL59PEEa-bhAShUbnYJNzHVj70IoB5NmW_ABbLo9gjpUz0603Jl9vFkKXc6nAW8Vvl4WV6GopTnuYJ-hOPLOMF2_I6KJP9oJPQmoa-7Y9qL_VgHivMMYdI1-OFUQQ5UczX4cHFgCLcMDhSLfkp-hlnc0KXc6Hla5Kyl4_Q2tNye8gJihnPj97wog7rTEtNBbZDXWFyZIBHEgXMop8vx6TiuGcsPC0r--j8niFjeQj53tKeNnO_f0V0000__y30000)
