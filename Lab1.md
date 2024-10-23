# LAB1 - PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG


## 1. Phân tích kiến trúc:
 - Đề xuất kiến trúc cho hệ thống Payroll:Hệ thống Payroll sẽ sử dụng kiến trúc phân lớp bao gồm 4 thành phần chính: UI, Business Logic, Persistence Layer, và Integration. 
 - Tại sao chọn kiến trúc này:
    + Tính mô-đun và bảo trì dễ dàng : Việc phân tách các chức năng lớp riêng biệt cho phép thay đổi hoặc mở rộng từng lớp mà không ảnh hưởng đến các lớp khác.
   + Tính linh hoạt : Kiến trúc phân lớp cho phép mở rộng hệ thống một cách linh hoạt, đặc biệt là khi hệ thống cần tích hợp các dịch vụ bên ngoài (ví dụ: ngân hàng).
   + Bảo mật : Với kiến ​​trúc phân lớp, các dữ liệu nhạy cảm như thông tin nhân viên và thanh toán có thể được quản lý kín ở lớp logic và lưu trữ.
 - Ý nghĩa các thành phần:
   + UI: Xử lý giao diện người dùng.
   + Business Logic: Các chức năng chính của hệ thống như tính toán thanh toán.
   + Persistence Layer: Tương tác với cơ sở dữ liệu.
   + Integration: Quản lý việc giao tiếp với các hệ thống bên ngoài như ngân hàng cho thanh toán trực tiếp.
- Biểu đồ Package:
![Package Digaram](https://www.planttext.com/api/plantuml/png/Z9D1Qy8m583l_HKFp_CFU1YoYmWoTfYmQvQ69bXVNPiKPNZslFCOw4G6Wip3BhEC7GB-Z_o2_OKbnMgBZjb32NalxttvNlkJVJSJIMAf-g6Nz0H272NC6n3Q8m63MhTTWqSFW8OaIQ3Rxf0HY_CTzxG4YS0N9fiWOB1Tc-n5WAy_CTWbN7EpMGr0Sls10KXR_jvivdP9RM3H1-hsRUxO6tk7fbSg4SXilquK25e6A29veCfoPx8LXFeBGXUpEDnn3I0rsMANSgjNo456UeOGRjVRcGL9zHI6nT5pu6vOd8X4CgGCSe8oNobOfUjirmfaRB9tyDqhT70AaEjNX5Je9HQCiHh1K5a0MU3iK2_EmckZP45Cf8Ym35RQhe9P9vG3DzayL_Kit7fY9sQo9zlhtf9Pbv6UYk809tk93ufKqp5mz-5wUY0hlfbw_VBK-1hGilO5ZFHI0JMRDxKVXtSYtLKvajmewtK3bKvYQYrXsVPVzOxSDFwpKhwcrsJekx_d5m00__y30000)

## 2. Cơ chế phân tích:
- Các cơ chế cần giải quyết trong bài toán bao gồm:
  + Cơ chế xử lý bảng chấm công: Hệ thống cần ghi lại thời gian làm việc của nhân viên và tính số giờ làm thêm theo đúng quy định.
  + Cơ chế tính toán lương: Hệ thống phải có khả năng tính chính xác lương của nhân viên theo giờ, nhân viên hưởng lương cố định và nhân viên hưởng hoa hồng.
  + Cơ chế chọn phương thức thanh toán: Mỗi nhân viên có thể chọn phương thức thanh toán khác nhau (chuyển khoản hoặc nhận trực tiếp).
  + Cơ chế báo cáo: Cần cung cấp báo cáo về số giờ làm việc, tổng lương và chi tiết liên quan cho từng nhân viên.
  + Tích hợp với cơ sở dữ liệu cũ: Hệ thống phải tích hợp với cơ sở dữ liệu cũ và kiểm tra sự hợp lệ.
    
## 3. Phân tích ca sử dụng Payment:
- Xác định các lớp phân tích:Trong ca sử dụng "Payment" , các lớp phân tích chính sẽ bao gồm:
  + Employee : Đại diện cho nhân viên nhận lương.
  + PaymentMethod: Quản lý cách thức mà nhân viên nhận lương (chuyển khoản, tiền mặt, ...).
  + Payroll : Quản lý dữ liệu về tiền lương, thuế, và các khoản khấu trừ.
  + PaymentProcessor: Thực hiện các giao dịch thanh toán, tích hợp với hệ thống ngân hàng hoặc các dịch vụ bên ngoài.
  + Bank: Đối tượng đại diện cho hệ thống ngân hàng được tích hợp để thực hiện việc chuyển khoản.
-  Mô tả được hành vi thông qua biểu đồ sequence:
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/T98nJiCm58Ptd-AfEnVeW0e8iG3gm02ZvLgnrUGvIXoad821YPc585M8IfL0Oee71gFUmoVW2hmaBMbHc2mz_T___F_sj_kSv9PdjaXYbiyrGcPooRYm9eFHfVBF2BVQBt44F8UZPinOUy318PmcQMnAAM4CDtvPW0ZrIm6eGhr2YDTlwmeZzYiYOChBpCGnwSz3lIZ1Al-14LZToxUIJfr8j1VIAZCZvjfN0huUWhj71Qdg0F88xbNGmMbgZQ-GxOEzqpGpGkOvNNuCLuIz2r0wk3iSedin6Hnpd1Dq5jnAGzbdtU701lUe0QEcC-MVA4jB3QzlisoQsZDfI0MYwMNm9ds59mIddOS5cuMwQyDN-c-SRQ4xx_NVVcLeFqMf5vPD9CwQV_43003__mC0)
- Xác định một số thuộc tính và quan hệ giữa các lớp phân tích:
     +  Lớp Employee  :
         * Nhiệm vụ : Đại diện cho nhân viên yêu cầu thanh toán lương và nhận lương.
         * Thuộc tính :employeeID, name, bankAccount.
         * Quan hệ :Kết nối với Payroll để nhận thông tin về bảng lương và trạng thái thanh toán.
     + Lớp Payroll  :
         * Nhiệm vụ : Quản lý dữ liệu về tiền lương, thuế, khấu trừ và trạng thái thanh toán.
         * Thuộc tính :salaryAmount, taxDeduction, paymentStatus.
         * Quan hệ :Kết nối với Nhân viên để quản lý thông tin lương của nhân viên, kết nối PaymentMethod để xác định phương thức thanh toán, kết nối với PaymentProcessor để xử lý thanh toán.
     + Lớp PaymentMethod :
         * Nhiệm vụ : Lưu trữ và quản lý phương thức thanh toán cho nhân viên (Ví dụ: chuyển tài khoản ngân hàng, tiền mặt).
         * Thuộc tính :methodType, bankAccount.
         * Quan hệ :Kết nối với Payroll để xác định cách thức thanh toán khi có yêu cầu của nhân viên.
     + Lớp PaymentProcessor :
         * Nhiệm vụ : Xử lý các giao dịch thanh toán, tương tác với các hệ thống ngân hàng để thực hiện giao dịch.
         * Thuộc tính :transactionID, paymentDate.
         * Quan hệ :Kết nối PaymentMethod để xử lý thanh toán theo phương thức đã xác định, kết nối với Ngân hàng để thực hiện các giao dịch thanh toán.
     + Lớp Bank :
         * Nhiệm vụ : Thực hiện các giao dịch thanh toán tiền qua ngân hàng, chuyển tiền vào tài khoản của nhân viên.
         * Thuộc tính :bankID ,accountNumber.
         * Quan hệ :Kết nối với PaymentProcessor để nhận và xử lý yêu cầu thanh toán giao dịch.
           
- Biểu đồ lớp mô tả lớp phân tích:

![Class Diagram](https://www.planttext.com/api/plantuml/png/V55BYW8n4DtNANA1li4WEhGB5oE2Su4oNQ2OJvEgm8J1axcO8ta5JQmMHPXTtg_oAhcS_-Oic2Hx1tmy19CY4rY7p6RfHnSBaVa5Opf32bTzWm4zjSCEmt5XRSn1u0IQtM19qJcDCZfCPU6RfnA2FpqDsSeXXaQCM3m5sGfAvfSnbTwaQ8av9fqd2GDZIsiRpVSez9R-8jd7GQE-WUyo_bF-yqQglUfw1Tvjw-ntbAhvyJuVNJURDePfyubywVzGdyHxFNXRjLfg4u0vXQ5-q1K00F__0m00)
- Giải thích biểu đồ lớp trong hệ thống Payment :
     + Employee  yêu cầu nhận lương, trong khi xử lý Payroll  thông tin về lương và trạng thái thanh toán.
     + PaymentMethod được chỉ định cách thanh toán lương,  PaymentProcessor xử lý thanh toán qua Bank .
     + Bank thực hiện chuyển tiền vào tài khoản của nhân viên.
## 4.Phân tích ca sử dụng Maintain Timecard
- Xác định các lớp phân tích cho ca sử dụng Maintain Timecard:
     + Employee : Đại diện cho nhân viên ghi nhận số giờ làm việc.
     + Timecard : Quản lý thông tin về thời gian làm việc của nhân viên.
     + TimecardManager : Chịu trách nhiệm lưu trữ và xử lý các yêu cầu liên quan đến việc thêm, cập nhật, và truy xuất bảng chấm công.
     + Payroll  : Sử dụng thông tin từ bảng chấm công để tính toán lương cho nhân viên.
       
- Mô tả hành vi thông qua biểu đồ sequence:
  ![Sequence Diagram](https://www.planttext.com/api/plantuml/png/V971IiGm48RlUOfXxxw01raHRxfus8FNc8Occ2PBsYxi4tZUimXRYnT1h208pS53fEynJ-0hE5tPqeNLIyA4-Rxyato7psbUS5-KcM7vhRRWNIuP5uNpC9cf-6XXgUEpdG3FuRG_PcoxmT49d6SBurPImZ7C5BOl2yWnh27L61x0n4r6B8OxmOP6WkOwauBxXA0vjfK3vR3z422s0jjx2hZ1jhOf2AgUCX3ntQPi04UIIsvvAZsvBhgc_1VRjH9znLVU6KFKsVZI1CChc3vnkQUWme7fcguYtOuz6E8wLkBNPlVdALJSMFLtej5BZXrB3FUQYk4Rm6FxHeaE30fVwrZJqZKOQj7dBHcRIflqN_i3003__mC0)
- Xác định được nhiệm vụ của từng lớp phân tích:
     + Lớp Employee :
       * Nhiệm vụ: 
          * Nhập số giờ làm việc và gửi thông tin này cho hệ thống.
          * Yêu cầu tạo hoặc cập nhật Timecard của mình.
     + Lớp Timecard :
       * Nhiệm vụ:
          * Lưu trữ thông tin về ngày làm việc và số giờ làm việc của Employee.
          * Cập nhật hoặc tạo mới thông tin bảng chấm công khi có yêu cầu từ Employee.
     + Lớp TimecardManager :
       * Nhiệm vụ:
          * Quản lý việc lưu trữ và xử lý các Timecard.
          * Nhận yêu cầu từ Timecard để lưu bảng chấm công và cập nhật dữ liệu cho Payroll.
     + Lớp Payroll :
       * Nhiệm vụ:
         * Cập nhật thông tin từ Timecard để tính toán lương cho Employee.
         * Xác nhận việc cập nhật dữ liệu Timecard thành công.
- Thuộc tính và quan hệ giữa các lớp phân tích
   + Employee: Liên kết với Timecard để ghi lại số giờ làm việc.
   + Timecard: Quản lý thông tin số giờ làm việc, và liên kết với TimecardManager để lưu trữ dữ liệu.
   + TimecardManager: Quản lý các thao tác lưu trữ, cập nhật Timecard, và kết nối với Payroll để sử dụng số giờ làm việc tính lương.
   + Payroll: Sử dụng dữ liệu từ Timecard để tính lương và phản hồi lại cho TimecardManager về trạng thái tính lương.
     
- Biểu đồ lớp mô tả các lớp phân tích:
  
  ![Class Diagram](https://www.planttext.com/api/plantuml/png/P91D2i9034RtESLSe3SGgL0NBWGNWklG2LewFv9a5aKycGkFv1Mq9LIgkoIyBtdazNZMeiXQOW3fk-Gu2q4RKCHjupNaWSZTmBdAaRMxPceJHe8x67li8hN8tbYFIbDnoONbbBad_m_lCU6Ps39gKzl_qT8Ytz011yuX62mOa8TDp2Nf8jsWuXYQvLTLjPulmkov69i8_8gDZDq5g2dvyKrl0000__y30000)
- Giải thích biểu đồ lớp
   + Employee : Ghi lại số giờ làm việc vào Timecard và gửi dữ liệu đến TimecardManager để lưu trữ.
   + Timecard : Quản lý các thông tin về thời gian làm việc, gồm số giờ làm và ngày làm việc. Dữ liệu này được gửi đến TimecardManager để lưu trữ và cập nhật cho bảng lương.
   + TimecardManager : Chịu trách nhiệm lưu trữ thông tin bảng chấm công và gửi thông tin này cho Payroll để tính lương.
   + Payroll : Tính toán lương dựa trên thông tin chấm công do TimecardManager cung cấp.
