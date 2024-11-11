# LAB2 - PHÂN TÍCH CA SỬ DỤNG

## 1. Phân tích ca sử dụng Create Administrative Report:
- Xác định các lớp phân tích cho ca sử dụng: Trong ca sử dụng " Create Administrative Report" , các lớp phân tích chính sẽ bao gồm:
  + PayrollAdministrator: Người dùng hệ thống có quyền tạo và lưu báo cáo hành chính.
  + ReportCriteria: Lớp lưu trữ các tiêu chí cho báo cáo, bao gồm loại báo cáo, ngày bắt đầu/kết thúc và tên nhân viên.
  + ReportGenerator: Lớp chịu trách nhiệm tạo báo cáo dựa trên các tiêu chí được cung cấp.
  + Report: Lớp đại diện cho báo cáo cuối cùng được tạo, có thể được xem và lưu trữ.
  + FileManager: Quản lý việc lưu trữ báo cáo, bao gồm yêu cầu nhập tên và vị trí lưu báo cáo.

- Mô tả hành vi thông qua biểu đồ sequence:![Sequence Diagram](https://www.planttext.com/api/plantuml/png/T9B1IWCn48RlUOgX9ptu0ZsKbe9wK2dYnMFS3TrWcfGaM-ZPauW7tq0H4GeBUdHpy13nFV84leAJhMopBLucCCpt__CF-N6VGsEfjkLC47FD9MXb612QMQMXDw5BhOI0KJxZaXkhARPxG0sCuW0XpGC70pXdSwNjM7FBDAVGXqk_AY4BzMi9DjHF2guybWmBsPfjwICcMUE0-BYKquY_pC7oHghmrOx6XcX5aBte-a4Ut3i5g_rA9c9_4f5Sf-Z3CG_k1cUAuEuI_kl1Fwz3RF8USi5EgQHJfhjXnVTRcR1xrdyiqI-uUxbFKYhnFIj2NM7GkE32Fy8Y-kE-LQFsdsbweXroswezpabtFuHKuXSNlSN0s9058KCcy_WpVW400F__0m00)
- Xác định một số thuộc tính và quan hệ giữa các lớp phân tích:
  + Lớp PayrollAdministrator:
    * Nhiệm vụ: Yêu cầu tạo báo cáo và có thể lưu báo cáo.
    * Thuộc tính: adminID, name.
    * Quan hệ: Kết nối với ReportCriteria để nhập tiêu chí và với FileManager để lưu báo cáo.
  + Lớp ReportCriteria:
    * Nhiệm vụ: Lưu trữ tiêu chí báo cáo như loại báo cáo, ngày bắt đầu/kết thúc và tên nhân viên.
    * Thuộc tính: reportType, startDate, endDate, employeeNames.
    * Quan hệ: Cung cấp thông tin cho ReportGenerator để tạo báo cáo.
  + Lớp ReportGenerator:
    * Nhiệm vụ: Tạo báo cáo dựa trên tiêu chí từ ReportCriteria.
    * Thuộc tính: reportID, generationDate
    * Quan hệ: Nhận tiêu chí từ ReportCriteria và tạo đối tượng Report.+ 
  + Lớp Report:
    * Nhiệm vụ: Đại diện cho báo cáo cuối cùng có thể xem hoặc lưu trữ.
    * Thuộc tính: content, format, createdDate.
    * Quan hệ: Được tạo bởi ReportGenerator và có thể được lưu bởi FileManager.
  + Lớp FileManager:
    * Nhiệm vụ: Quản lý việc lưu báo cáo theo tên và vị trí được cung cấp.
    * Thuộc tính: filePath, fileName.
    * Quan hệ: Nhận thông tin từ PayrollAdministrator để lưu Report.
- Biểu đồ lớp mô tả các lớp phân tích:

  ![Class Diagram](https://www.planttext.com/api/plantuml/png/X59BRi8m4DtFANo1NA6Y8W9r0KA82uoI0IpiSJIUBgAg9-k28_KA1CUGr6hLtPlFUpDlxE-lwo8gYhvx1_5YsKY818t36CqEUmdElRRUieqgg47C1nXJ6Rpdtkg46Jt19sJIdheWkXIh91PpkwJaeUyeXMbYZJf6nEs4VUT2JxGTD6CfkYQc-HAZQjxYD1Pju2HMK3EZ2Qp4cl0nYCSHDa83f_r9N5b76sGyqMFUSSZiKC_FO9kT_tgegdefZW75RQQEfpCedKuz_qtvkpvp0dDNCouiXbUu_u4R0000__y30000)
- Giải thích biểu đồ lớp trong hệ thống Create Administrative Report:
  + PayrollAdministrator cung cấp tiêu chí báo cáo qua ReportCriteria và yêu cầu ReportGenerator tạo báo cáo.
  + ReportGenerator tạo báo cáo dựa trên thông tin từ ReportCriteria và cung cấp Report cuối cùng.
  + PayrollAdministrator có thể lưu Report thông qua FileManager, nơi quản lý tên và vị trí lưu trữ.
## 2. Phân tích ca sử dụng Create Employee Report:
- Xác định các lớp phân tích cho ca sử dụng: Trong ca sử dụng " Create Employee Report" , các lớp phân tích chính sẽ bao gồm:
  + Employee: Đại diện cho nhân viên, người sẽ khởi tạo báo cáo.
  + ReportCriteria: Lưu trữ các tiêu chí báo cáo mà nhân viên nhập vào, bao gồm loại báo cáo, ngày bắt đầu và kết thúc.
  + ProjectDatabase: Cung cấp thông tin về các dự án và mã phí liên quan, sử dụng cho báo cáo dự án.
  + ReportGenerator: Tạo báo cáo dựa trên các tiêu chí mà nhân viên đã nhập.
  + Report: Đại diện cho báo cáo cuối cùng mà nhân viên có thể xem hoặc lưu.
  + FileManager: Quản lý việc lưu trữ báo cáo, bao gồm yêu cầu nhân viên nhập tên và vị trí lưu báo cáo.
- Mô tả hành vi thông qua biểu đồ sequence:![Sequence Diagram](https://www.planttext.com/api/plantuml/png/T9AzJiCm58LtFyLLftRW1HXGKVaR0274mkWcLXD8xCXsAdLcGeY1Do122AbI91X9XWv6l8UVW5VWEgtoHraSwShVEUSUvwTSZPMcKgTnHDHjo44AnGZrj90mE8oJI2mO6m1LiEzcX5GVsDc3IvO8gISor4o657RXsYnJy6pnbeAsHIPWQl3my22zkqXVI773F7r0DPrInH2Vf7pcyDS4VCe3K2Rp0eZD2oI1oS6tvGUOZCEGssA5He4j7tdZKLyOaRxsjh0deItlE6XKUTZcjoNoUdBCE9FKTT29hCDgUvUqltP3r2B8NdKhgk9JqD8iUKji8-78TV6zv0t_zOJ9gzwR9peA8tP6EPqnsNsVwFizRR53RJuNcqP7f4srVCy3M-Iug0iuDyymT_wODw_K_ZDjL_I7x5lLvPnsyo4aMdukw3qkZ0CU439ct7U_xoy0003__mC0)
- Xác định một số thuộc tính và quan hệ giữa các lớp phân tích:
  + Lớp Employee:
    * Nhiệm vụ: Khởi tạo và cung cấp tiêu chí báo cáo, chọn mã phí (nếu báo cáo theo dự án), và có thể lưu báo cáo nếu cần.
    * Thuộc tính: employeeID, name.
    * Quan hệ: Tương tác với ReportCriteria để cung cấp thông tin báo cáo và FileManager để lưu báo cáo.
  + ReportCriteria :
    * Nhiệm vụ: Lưu trữ thông tin về loại báo cáo, ngày bắt đầu/kết thúc, và mã phí (nếu chọn báo cáo dự án).
    * Thuộc tính: reportType, startDate, endDate, projectChargeNumber.
    * Quan hệ: Gửi thông tin báo cáo đến ReportGenerator để tạo báo cáo.
   + Lớp ProjectDatabase :
     * Nhiệm vụ: Cung cấp danh sách mã phí dự án khi nhân viên chọn loại báo cáo theo dự án.
     * Thuộc tính: projectChargeNumbers.
     * Quan hệ: Kết nối với ReportCriteria để gửi mã phí liên quan đến dự án.
   + Lớp ReportGenerator :
     * Nhiệm vụ: Sử dụng tiêu chí từ ReportCriteria để tạo báo cáo, trả về đối tượng Report.
     * Thuộc tính: reportID, generationDate.
     * Quan hệ: Nhận tiêu chí từ ReportCriteria và tạo đối tượng Report.
   + Lớp Report :
     * Nhiệm vụ: Lưu trữ nội dung báo cáo, có thể xem và lưu nếu nhân viên yêu cầu.
     * Thuộc tính: content, format, createdDate.
     * Quan hệ: Được tạo bởi ReportGenerator và có thể lưu qua FileManager.
   + Lớp FileManager:
     * Nhiệm vụ: Quản lý việc lưu trữ báo cáo theo tên và vị trí được cung cấp.
     * Thuộc tính: filePath, fileName.
     * Quan hệ: Nhận thông tin từ Employee để lưu Report.
- Biểu đồ lớp mô tả các lớp phân tích:
    ![Class Diagram](https://www.planttext.com/api/plantuml/png/R591Ri8m4Bpx5Vv0lb0XGLjnA48L7rZ24Dp6ThHU3gZgothWINoXmJ4ciNBR6S_kUCU-_LqNGOZbR5iLletJx0DKtL88-jLshRy0-aTfNMaak5v5wCX2_Qga_KJdMPPi16meTN0aTvSE4KQZ5Sc0u0wvxjX_ePRbYRZ1vcptu7BqEnoOnFDaThfBCnmQx-B8tBeTvlOaxIay5fbn2wLTajRU2Pp4-kZPqb3MZDxdC3LxCoq-o563nnsFFRCbEMMmIPdbPAlgfOXE5Ka-5Ja1LIRorCnr5o7CcK-vqI9glDH8hnRzyzt_p3y0003__mC0)
- Giải thích biểu đồ lớp trong hệ thống Create Employee Report:
  + Employee khởi tạo yêu cầu tạo báo cáo qua ReportCriteria và có thể lưu báo cáo qua FileManager.
  + ReportCriteria nhận thông tin từ Employee và gửi đến ReportGenerator để tạo báo cáo. Nếu báo cáo theo dự án, ReportCriteria sẽ kết nối với ProjectDatabase để nhận mã phí dự án.
  + ReportGenerator tạo báo cáo Report dựa trên các tiêu chí nhận từ ReportCriteria.
  + FileManager quản lý việc lưu trữ Report cuối cùng nếu nhân viên yêu cầu lưu. 
## 3. Phân tích ca sử dụng Login
- Xác định các lớp phân tích cho ca sử dụng: Trong ca sử dụng " Login" , các lớp phân tích chính sẽ bao gồm:
  + User: Đại diện cho người dùng (diễn viên), là người thực hiện đăng nhập.
  + LoginForm: Biểu mẫu đăng nhập nơi người dùng nhập thông tin tên và mật khẩu.
  + AuthenticationService: Xác thực thông tin đăng nhập bằng cách kiểm tra tên và mật khẩu của người dùng.
  + SessionManager: Quản lý phiên đăng nhập của người dùng sau khi xác thực thành công.
  + ErrorDisplay: Hiển thị thông báo lỗi nếu tên hoặc mật khẩu không hợp lệ.
- Mô tả hành vi thông qua biểu đồ sequence:![Sequence Diagram](https://www.planttext.com/api/plantuml/png/N8yzRW8n48Lxd-A92YIum1OHD5H0Wv1ehSN25dYCx5au02V82I1begI8HCKM5EOYUmAkW4s11Ctyls_qRlMb7rXwhknQX9KXU1SKX2pPURHcGVaMPC0Wz-8HqVl0o2qD3Pst1SPDVO2DHuAElwHn_RpkQGdIpVbl8pBWJJ1vRC3nXrwFiOr7s5GnLcdmNOcdAYC65Mj5R4h9nj5K-QqfLO5v_2h1kgd_SugdXEDaersbpoIjwc8ZGzWvl-Y8lg95Dde7003__mC0)
- Xác định một số thuộc tính và quan hệ giữa các lớp phân tích:
 Lớp User:

Nhiệm vụ: Cung cấp thông tin đăng nhập (tên và mật khẩu).
Thuộc tính: userID, username, password.
Quan hệ: Tương tác với LoginForm để nhập thông tin đăng nhập.
Lớp LoginForm:

Nhiệm vụ: Thu thập thông tin đăng nhập từ người dùng và chuyển tới AuthenticationService để xác thực.
Thuộc tính: inputUsername, inputPassword.
Quan hệ: Nhận dữ liệu từ User và gửi đến AuthenticationService để xác thực.
Lớp AuthenticationService:

Nhiệm vụ: Kiểm tra tên và mật khẩu từ LoginForm để xác thực người dùng.
Thuộc tính: userDatabase (chứa thông tin người dùng hợp lệ).
Quan hệ: Nhận thông tin từ LoginForm, kiểm tra và gửi phản hồi về trạng thái đăng nhập.
Lớp SessionManager:

Nhiệm vụ: Khởi tạo phiên làm việc cho người dùng sau khi xác thực thành công.
Thuộc tính: sessionID, userID, sessionExpiry.
Quan hệ: Tương tác với AuthenticationService để thiết lập phiên cho người dùng đã đăng nhập thành công.
Lớp ErrorDisplay:

Nhiệm vụ: Hiển thị thông báo lỗi nếu thông tin đăng nhập không hợp lệ.
Thuộc tính: errorMessage.
Quan hệ: Nhận thông tin từ AuthenticationService khi xảy ra lỗi xác thực.
- Biểu đồ lớp mô tả các lớp phân tích:

  ![Class Diagram](https://www.planttext.com/api/plantuml/png/P93D3S8m38NldY8BT0LKH2z8SE5d04EjAY9rgjXL3uZ9E30IAv2qfRJYPlkzPt_9-_dAHJ5eMpkGcsKJl11S7OgOir0mTp0cCsqi6MlgcoQAdGybF61qxdnbUO-CrPHmQRHMfRfH-JaBLBoWq6pl9b19h1QTJBE3TpHB7Kd4UXv3CdJROc4VfFIMausWCTlpPzbgWGSBrgH-aVwLyIn0Jboc7_e0003__mC0)
## 4. Phân tích ca sử dụng Maintain Employee Information

## 5. Phân tích ca sử dụng Maintain Purchase Order

## 6. Phân tích ca sử dụng Run Payroll
