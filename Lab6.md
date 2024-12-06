# LAB6 -  Thiết kế các lớp  trong "HỆ THỐNG PAYROLL SYSTEM"
## 1. Login :
a. Xác định đúng các operations và methods :
   - Lớp LoginForm: 
     + Operations:
       * Hiển thị giao diện đăng nhập.
       * Gửi thông tin đăng nhập đến hệ thống xác thực.
     + Methods:
       * getInput(): Map<String, String> - Lấy thông tin username và password từ người dùng.
       * submitLogin(): boolean - Gửi thông tin đăng nhập đến AuthenticationService.
  - Lớp AuthenticationService:
      + Operations:
        * Xác thực thông tin đăng nhập.
        * Xử lý lỗi xác thực.
      + Methods:
        * authenticate(username: String, password: String): Employee - Trả về thông tin nhân viên nếu xác thực thành công, null nếu thất bại.
  - Lớp Employee:
      + Operations:
        * Quản lý thông tin nhân viên đã xác thực.
        * Truy xuất thông tin cơ bản của nhân viên.
      + Methods:
        * getDetails(): Map<String, String> - Trả về thông tin cơ bản như ID, tên, vai trò.
        * isSessionActive(): boolean - Kiểm tra phiên đăng nhập còn hiệu lực không.
![Diagram](https://www.planttext.com/api/plantuml/png/V991JiCm44NtFiMe6uhKNY12LIiL92HOvGHkCar7E7OqCov2Y9Enu4XS0ITD4v4Miil_BpF_s_d-_5gBMjPOEoClv863eBc1BUx98nJEYg30FZ0yXIhvKP9g4sCwxwG-1AxXtK3t98AzhJ63N9byrSjDeby3bnEvGdtqJTJvRGRFjhaxcOiUMlMKn5rDskrgmLq83gqt7-SKcwW7z4g5LGe-HpvIWKCYExeudyPRN2HB2-xhneKtn773MHc6KkB9Q_zsfJ2dZ9TbjwYMdFnVboH7aTHaKoWTSL9vk1r6r_ML0pLYnfjOBbT_d4W6Cq5V2XICPMjR9pDpdMsd3AtJXumQsSklqom1Us9crcbm-nlz0000__y30000)

b. Xác định các trạng thái : 
  - Trạng thái chính của Employee:
    + Chưa đăng nhập (NotLoggedIn): Nhân viên chưa được xác thực.
    + Đã đăng nhập (LoggedIn): Nhân viên đã được xác thực và có phiên làm việc.
    + Phiên hết hạn (SessionExpired): Phiên đăng nhập của nhân viên đã hết hạn.
      
![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTnTcQUGb5-SIfNj5QiWgwkdO9VVebFVdfwQefd7XSN4WSi2UTOAIIMbcIavfLa9YUMf6feSg4e2qujBixCptEjACWiIaq1AYw628HavgRcbvO0bQEfGBCOgACerH7L0Yw7rBmKa9C10000__y30000)
  - Mô tả trạng thái:
     + Trạng thái chính: NotLoggedIn, LoggedIn, SessionExpired.
     + Thay đổi dựa trên xác thực và thời gian phiên làm việc.

c. Xác định các thuộc tính :
  - Lớp LoginForm:
    + Thuộc tính:
      * username: String - Tên đăng nhập của người dùng.
      * password: String - Mật khẩu của người dùng.
  - Lớp AuthenticationService:
    + Thuộc tính: (Không có thuộc tính vì đây là lớp xử lý logic.)
  - Lớp Employee:
    + Thuộc tính:
      * id: int - ID duy nhất của nhân viên.
      * name: String - Tên đầy đủ của nhân viên.
      * role: String - Vai trò hoặc chức danh của nhân viên.
      * isActive: boolean - Trạng thái phiên đăng nhập (true nếu đang hoạt động).

![Diagram](https://www.planttext.com/api/plantuml/png/T951JiD034NtSmeh6rQzG1UebO0LkvvWchYjnSGJsPvM2FLaNN0ahe0JGXAaugN_-z_spDVjSwCMnKgRWhuHWsJ5y01FU216g5DKHON83TW9II2Q2UsBUVEG1LxpqKr57Ork38FXf_kIfOMF04Cv8HnRNCFE_Nm468NE-KkMPY5SVsEsnMUoKHsDCkzGpbIZHyx4Szkb_8uupI4F8ZPOrAZydRuG9AVx0kcsDZgxkC_EH1vMczv6C0rxwOaw3VF9gzNZFvkleLBaHg4MR7ev9gt2VRPFcQvpew0LOV-9cSO6S2IgiF7W_XE_0G00__y30000)

d. Xác định các phụ thuộc và quan hệ kết hợp:
   - Phụ thuộc:
     + LoginForm phụ thuộc vào AuthenticationService vì nó gọi phương thức authenticate() để xác thực người dùng.
     + AuthenticationService phụ thuộc vào Employee vì nó trả về đối tượng nhân viên sau khi xác thực thành công.
   - Quan hệ kết hợp:
     + Employee không có kết hợp với LoginForm hoặc AuthenticationService, vì nhân viên chỉ là kết quả trả về sau quá trình xác thực.


![Diagram](https://www.planttext.com/api/plantuml/png/T59BJiCm4Dtx5ADkQAMg1uXGrKe52GbMFO7ZJCE8P1pPuoA4E1aBZiGLcAJvj42zV9_nynj_VtvjejWWgQvCV266u2EQ6zZXWHZ1LJP6Z62v07b62c150kL953pu08--L5EAAhLgD9tXXDxxKCExWUwe8h2jCOEz-hc47czK_kf3CU83KQ8yS9DaliZWoJQt9thPozQZBgQy9kakRAMvznLQFd7cOmYqJPgUXPmLyhp7S2I7OpWxiJZ_dNJv9-DYcdjNDvL_msaKgOfOO3WzVF7qSo9et0jYc1EtJkY8Po-QYjcXMAhYzMeqtxZ20Xla0jbHlqVDxHrrHKGpRMgrMb-fAOEPbX9dvd-wDOuzg3QWfC0gt-YzxR_w0G00__y30000)
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

b. Xác định các trạng thái :
   - Trạng thái chính của Timecard
      + Mới tạo (New): Thẻ chấm công vừa được khởi tạo và chứa dữ liệu từ người dùng.
      + Đã xác thực (Validated): Dữ liệu thẻ chấm công đã được kiểm tra.
      + Đã lưu (Saved): Thẻ chấm công được lưu vào cơ sở dữ liệu thành công.

![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTnTcQUGb5-SIfNj5QiWgwkdO9VQZaN5v00Sy8ISp9J4ajIKnIi5CgWx93CtDJanA8K3KqkX3H8SN1Y6LXXCP16KWGH1Ya0Mi7ba9gN0h8O0000__y30000)
  - Mô tả trạng thái:
    + Trạng thái chính: New, Validated, Saved.
    + Thay đổi khi dữ liệu thẻ chấm công được nhập, xác thực, và lưu thành công.
      
c. Xác định các thuộc tính :
   - Lớp TimecardForm:
     + Thuộc tính:
       * date: Date - Ngày chấm công.
       * hoursWorked: float - Số giờ làm việc trong ngày.
   - Lớp TimecardController:
     + Thuộc tính: (Không có thuộc tính vì đây là lớp xử lý logic.)
   - Lớp Timecard:
     + Thuộc tính:
       * date: Date - Ngày làm việc.
       * hoursWorked: float - Số giờ làm việc được ghi nhận.
       * employeeId: int - ID của nhân viên liên kết với thẻ chấm công.
       * status: String - Trạng thái của thẻ chấm công (New, Validated, Saved).

![Diagram](https://www.planttext.com/api/plantuml/png/d54nJWD13Ept5TOrLFd05IXI8YIAL21HcwoFMsLl7TdUI0ZbPHGyYI_Wky0fa5HOsYrsTiQUyUVxnr8DnUgGW-vI0M6bS0Dhwb8Xs6PK9GKi4Qod981cafwh-MF70XjCnVp0OnfeYnAXgjFGHS94de4xbW7U0amLqQY5jT_mKzz8prNqYML7iOKkCng4ur-j5HSJpfbaLBp4_zddXD2mp_nATE-0cviPdfDLRU710oWlavGtdgCIocY9Y_Pfh-6NwyNYzjheBJHA9PwDxUDY4wvyFLSOUGVCQVHssepYWRG9InSRz_W5003__mC0)

d. Xác định các phụ thuộc và quan hệ kết hợp:
   - Phụ thuộc:
     + TimecardForm phụ thuộc vào TimecardController vì nó gọi phương thức validateTimecard() và saveTimecard().
     + TimecardController phụ thuộc vào Timecard vì nó xử lý và lưu trữ thẻ chấm công.
   - Quan hệ kết hợp:
     + Timecard có kết hợp với Employee thông qua employeeId, biểu thị mỗi thẻ chấm công thuộc về một nhân viên.

![Diagram](https://www.planttext.com/api/plantuml/png/X59BRi903Dtd51QRjWiuG1O8gRGIYwwerBMJ61WnCqOp7YHKzMHTz4YzGXtofGLrf4J9FFlvsS_Vdr-BA1WaEPl5lV4GE59s1qlQ64zGMeoH8g2lG7Pa0g18C4KIlTnmW1SqNlI1L-Een511Yfg6IfATatlWcOE3zmpEfqAX79RwRlxRwnsd4DyuxAdAOMCPfGMs91tFoX-It3_aGyKs9gR2cJwiZYYOBQ5N-e_VQXxPIs1hAVIQZcXDhQjdaFPZA3NYx8hYyP-48vkgwV6FY9lZk3sF3Y5ti7mYMYcW3WmfwgQacCDQRVBRCPdES9sSmt2gPzFWWwQdbh3NP7hcxhI0HqSN_4rh_SvKT21VaIzDkpXApwL1CUnZTh4EizdycYCvJ7IBuYIxWerJwi3EjQPKRSSe3wRJ-T2PHXTasMyZ24-oXQgir_u7003__mC0)
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

b. Xác định các trạng thái :
  - Trạng thái chính của Paycheck
     + Chưa xử lý (Unprocessed): Paycheck được tạo nhưng chưa được xử lý.
     + Đang xử lý (Processing): Paycheck đang được gửi đến hệ thống ngân hàng hoặc dịch vụ in.
     + Hoàn tất (Completed): Paycheck đã được xử lý xong.
       
![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTnTcQUGb5-SIfNj5QiWgwkdK9eNa5HVd9gSN5g2XSN4WSi6G3XPUQbArWffAVcfHObbgHgQ78XYOEKEUVd5kIabW0rMIb03GX8h4pEI4tE1Yf6o8BK0ktbSaZDIm6v1W000F__0m00)
  - Mô tả trạng thái:
     + Trạng thái chính: Unprocessed, Processing, Completed.
     + Thay đổi khi paycheck được tạo, xử lý, và hoàn tất.

c. Xác định các thuộc tính :
   - Lớp PayrollController:
    + Thuộc tính: (Không có thuộc tính vì đây là lớp xử lý logic.)
   - Lớp Paycheck:
     + Thuộc tính:
        * amount: float - Tổng số tiền lương.
        * employeeId: int - ID của nhân viên nhận lương.
        * status: String - Trạng thái của paycheck (Unprocessed, Processing, Completed).
   - Lớp BankSystem:
     + Thuộc tính: (Không có thuộc tính vì đây là lớp xử lý giao dịch.)
   - Lớp PrintService:
     + Thuộc tính: (Không có thuộc tính vì đây là lớp xử lý in ấn.)
   - Lớp BankInformation:
     + Thuộc tính:
       * name: String - Tên ngân hàng.
       * routingNumber: String - Số định tuyến ngân hàng.

![Diagram](https://www.planttext.com/api/plantuml/png/T58xRiCm3Drz2Y9Bfrp0Gn6qNR8KHNq2nMPg8H9ba5I0eEZ9ElH8lK8b9N4Sf_4YuF5zg2V_Vl-iH0rhzAwIdINW85Wzm0jkBI6qpeYWWA4Ej4VBO5JPRg8cS1iOtYF1cpbmS0wY9859ygh8plXp8CqdCdnM0DNNPDxssEuAd3_ZGoIjOUk2qOAS1kW75mw8wwu6ItePfDqrIWrDMee-YcAqVpAqQmwYwEUvYQiDyjwsUCo-5gqftSmRjO76rSXudCPCbkCGDQ6lqM-GHqws76jaTCLEUZj8TTlBSlbuQQE6HSjez5JxmA75_0YBEyB9FPDKa3g1uMoc0JPfVazxLSM_wY4pa8l14RpDx708ObLcfBbviKgaLGh9_ziV0000__y30000)

d. Xác định các phụ thuộc và quan hệ kết hợp:
   - Phụ thuộc:
     + PayrollController phụ thuộc vào Paycheck vì nó tạo và xử lý đối tượng này.
     + PayrollController phụ thuộc vào BankSystem và PrintService vì nó gửi paycheck đến ngân hàng hoặc in phiếu lương.
     + BankSystem phụ thuộc vào BankInformation để thực hiện giao dịch.
   - Quan hệ kết hợp:
     + Paycheck có kết hợp với Employee thông qua employeeId, biểu thị mỗi paycheck thuộc về một nhân viên.

![Diagram](https://www.planttext.com/api/plantuml/png/T5DDJlCm4Dtd5ADkA1BY01522DWWVVg4w0ccpXIiEdRa6IDLY9Enu4XSWOdhfAQ5R1AzcVVU_ENhu_E61QEatZMyjHvYO6hEu9usrXCOXyp4WBu3UI4R0KMYNITHS1CYF2KFZxYBmJb8h0HKUfDf4tuNl8nlYl3MG7uCEfCS2ccAUI6pvULv2_yiozM4N0EKv246GynJO3cKZnOcIBclmNRGl5VMEJ8xOX-IbnOsBg3ieHAXVd1XH_JGjM2zL14TZ2HkOQKT--Sgy4oUebQ__A5wSImrbpMnv9u4hSlD5j53oRVejwiT2_LpqHqDWQqiyV6avOlH88oSDZCVl6wZHx715zjg6EeaAuglrj2iFOpWxyh1PmR5gSeJnIF7MTHZJ_MywZd7a4JX_wbV7vHp__ErQR_aE_B6bfDJhs1izk3cz9mkBwyFcsvXOIAX56gv6kB57yHgtafbDMQOJWiam5hZVt5_JFHNzh2VO1ROWwUUPRryb7GidgKqgI9FMlKED3Dn-IibecSq8xveRhIuyVV-1W00__y30000)
