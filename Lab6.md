# LAB6 -  Thiết kế các lớp  trong "HỆ THỐNG PAYROLL SYSTEM"
## 1. Login :
a. Xác định đúng các operations và methods :
  - Operations:
    + Hiển thị giao diện đăng nhập.
    + Gửi thông tin đăng nhập đến hệ thống xác thực.
  - Methods:
    + getInput(): Map<String, String> - Lấy thông tin username và password từ người dùng.
    + submitLogin(): boolean - Gửi thông tin đăng nhập đến AuthenticationService.

![Diagram](https://www.planttext.com/api/plantuml/png/V991JiCm44NtFiMe6uhKNY12LIiL92HOvGHkCar7E7OqCov2Y9Enu4XS0ITD4v4Miil_BpF_s_d-_5gBMjPOEoClv863eBc1BUx98nJEYg30FZ0yXIhvKP9g4sCwxwG-1AxXtK3t98AzhJ63N9byrSjDeby3bnEvGdtqJTJvRGRFjhaxcOiUMlMKn5rDskrgmLq83gqt7-SKcwW7z4g5LGe-HpvIWKCYExeudyPRN2HB2-xhneKtn773MHc6KkB9Q_zsfJ2dZ9TbjwYMdFnVboH7aTHaKoWTSL9vk1r6r_ML0pLYnfjOBbT_d4W6Cq5V2XICPMjR9pDpdMsd3AtJXumQsSklqom1Us9crcbm-nlz0000__y30000)

b.Xác định các trạng thái : 
  - Trạng thái chính của Employee
    + Chưa đăng nhập (NotLoggedIn): Nhân viên chưa được xác thực.
    + Đã đăng nhập (LoggedIn): Nhân viên đã được xác thực và có phiên làm việc.
    + Phiên hết hạn (SessionExpired): Phiên đăng nhập của nhân viên đã hết hạn.
      
![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTnTcQUGb5-SIfNj5QiWgwkdO9VVebFVdfwQefd7XSN4WSi2UTOAIIMbcIavfLa9YUMf6feSg4e2qujBixCptEjACWiIaq1AYw628HavgRcbvO0bQEfGBCOgACerH7L0Yw7rBmKa9C10000__y30000)
  - Mô tả trạng thái
     + Trạng thái chính: NotLoggedIn, LoggedIn, SessionExpired.
     + Thay đổi dựa trên xác thực và thời gian phiên làm việc.

## 2. Maintain Timecard : 
a. Xác định đúng các operations và methods : 
  - Lớp TimecardForm:
     + Operations:
         * Nhận dữ liệu thẻ chấm công từ người dùng.
         * Gửi dữ liệu đến hệ thống xử lý.
      + Methods:
         * getTimecardInput(): Timecard - Lấy thông tin ngày và giờ làm việc.
         * submitTimecard(): boolean - Gửi dữ liệu thẻ chấm công đến TimecardController.
   - Lớp TimecardController:
      + Operations:
         * Xác thực thông tin thẻ chấm công.
         * Lưu thẻ chấm công vào cơ sở dữ liệu.
      + Methods:
         * validateTimecard(timecard: Timecard): boolean - Kiểm tra dữ liệu thẻ chấm công hợp lệ không.
         * saveTimecard(timecard: Timecard): void - Lưu thẻ chấm công vào bảng Timecards.
   - Lớp Timecard:
       + Operations:
         * Quản lý thông tin thẻ chấm công.
         * Cung cấp báo cáo thông tin.
      + Methods:
         * getSummary(): String - Trả về thông tin tổng quan của thẻ chấm công.
         * update(hoursWorked: float): void - Cập nhật giờ làm.

![Diagram](https://www.planttext.com/api/plantuml/png/d591QWCn3Bpx5IANfeTyO0ybq538eQSKUbPYRM9YMujbBuJIb_NG9_KBjPUDisq2XHfiZ3IQaSR--lXSIiGGaxDAZiP3O25r1ojgZIVOMHGXWPO3FAFnCMzuCOvs63GaoGZCU3NWQkA9WuCt1SFI6Ac1LJx7m85Ja5SEHz8Dj9OnZeaznJF3sdSfpk-RIZb296sTgQW2s39RGg_UVpVno3u6jfP2RQL7QqexjJwEbulEX75KnFuFVCz6Nyl_OtvodUKJqJh7izKNLpR9EGodCkuc1kFtOofrXNn-JJZfgZvb88lHi9U3wKJzUAh5uk6MRGtCXBoUp9JbSAPkGASCfUxij01wFNWeCxNCPEMVVGC00F__0m00)

b.Xác định các trạng thái :
   - Trạng thái chính của Timecard
      + Mới tạo (New): Thẻ chấm công vừa được khởi tạo và chứa dữ liệu từ người dùng.
      + Đã xác thực (Validated): Dữ liệu thẻ chấm công đã được kiểm tra.
      + Đã lưu (Saved): Thẻ chấm công được lưu vào cơ sở dữ liệu thành công.

![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTnTcQUGb5-SIfNj5QiWgwkdO9VQZaN5v00Sy8ISp9J4ajIKnIi5CgWx93CtDJanA8K3KqkX3H8SN1Y6LXXCP16KWGH1Ya0Mi7ba9gN0h8O0000__y30000)

## 3.Run Payroll :
- Lớp PayrollController:
    + Operations:
       * Điều phối quy trình tính lương.
       * Xử lý lương với ngân hàng hoặc máy in.
    + Methods:
       * calculatePaychecks(): List<Paycheck> - Tính toán danh sách lương dựa trên thẻ chấm công.
       * processPaycheck(paycheck: Paycheck): void - Gửi paycheck đến ngân hàng hoặc máy in.
 - Lớp Paycheck:
     + Operations:
       * Quản lý thông tin lương của từng nhân viên.
       * Theo dõi trạng thái xử lý lương.
    + Methods:
       * generate(amount: float, employeeId: int): void - Tạo paycheck với số tiền và thông tin nhân viên.
       * getDetails(): Map<String, String> - Trả về thông tin paycheck.
  - Lớp BankSystem:
      + Operations:
         * Xử lý giao dịch ngân hàng cho các paycheck.
      + Methods:
         * deposit(aPaycheck: Paycheck, intoBank: BankInformation): void - Gửi paycheck vào tài khoản ngân hàng.
  - Lớp PrintService:
     + Operations:
        * In phiếu lương cho nhân viên.
     + Methods:
        * print(aPaycheck: Paycheck, onPrinter: String): void - In paycheck ra máy in được chỉ định.

![Diagram](https://www.planttext.com/api/plantuml/png/T9DHRi8m38RVUmgBbtKINA1226sy8B49ZHDagO68DAbY1mbDEzaUTgHTOMbe2hJGbxP__NzsRFVlvtTEB1pxIcTqK0QS9SoUO85RPH2a5aH8iBKEFho1jJWvgpLu2jz4YCnYHD9VhU7cZWw-CeYN55fwBHX3YDoZF53-NC1A4K-JCcj3QsSb4YKvhzk70f8Kd4UhokpxAc_yqAKJbVM62zXgAxZLiAgrFI4komAKIMeuDdigOCDEcLqhxj2W2yNcDvnn7v7gI2PU80kbuz7UH3qzCySjUtQfzqMOm-P4Z5LNSOcr9SMvM0-EEsvosSPJHEVIX3bKWfKrmqw4JBn1TrGIEtRTYFV9raG7kjI10R6NiOCQKM6lRSvw3c_lllgy01jIjqWETQJGNjMK3TTbCfbTXbd0I3eCOo0GfanxWJHwOBpgQh0Icf8WBSyZpqs_xhlEnGmJj1EZNb2V69iVWkQ1tFnU_m000F__0m00)
