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
    * Thuộc tính: adminID, name.
    * Quan hệ: Kết nối với ReportCriteria để nhập tiêu chí và với FileManager để lưu báo cáo.
  + Lớp ReportCriteria:
    * Thuộc tính: reportType, startDate, endDate, employeeNames.
    * Quan hệ: Cung cấp thông tin cho ReportGenerator để tạo báo cáo.
  + Lớp ReportGenerator:
    * Thuộc tính: reportID, generationDate
    * Quan hệ: Nhận tiêu chí từ ReportCriteria và tạo đối tượng Report.+ 
  + Lớp Report:
    * Thuộc tính: content, format, createdDate.
    * Quan hệ: Được tạo bởi ReportGenerator và có thể được lưu bởi FileManager.
  + Lớp FileManager:
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
    * Thuộc tính: employeeID, name.
    * Quan hệ: Tương tác với ReportCriteria để cung cấp thông tin báo cáo và FileManager để lưu báo cáo.
  + ReportCriteria :
    * Thuộc tính: reportType, startDate, endDate, projectChargeNumber.
    * Quan hệ: Gửi thông tin báo cáo đến ReportGenerator để tạo báo cáo.
   + Lớp ProjectDatabase :
     * Thuộc tính: projectChargeNumbers.
     * Quan hệ: Kết nối với ReportCriteria để gửi mã phí liên quan đến dự án.
   + Lớp ReportGenerator :
     * Thuộc tính: reportID, generationDate.
     * Quan hệ: Nhận tiêu chí từ ReportCriteria và tạo đối tượng Report.
   + Lớp Report :
     * Thuộc tính: content, format, createdDate.
     * Quan hệ: Được tạo bởi ReportGenerator và có thể lưu qua FileManager.
   + Lớp FileManager:
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
  + User: Đại diện cho người dùng, là người thực hiện đăng nhập.
  + LoginForm: Biểu mẫu đăng nhập nơi người dùng nhập thông tin tên và mật khẩu.
  + AuthenticationService: Xác thực thông tin đăng nhập bằng cách kiểm tra tên và mật khẩu của người dùng.
  + SessionManager: Quản lý phiên đăng nhập của người dùng sau khi xác thực thành công.
  + ErrorDisplay: Hiển thị thông báo lỗi nếu tên hoặc mật khẩu không hợp lệ.
- Mô tả hành vi thông qua biểu đồ sequence:![Sequence Diagram](https://www.planttext.com/api/plantuml/png/N8yzRW8n48Lxd-A92YIum1OHD5H0Wv1ehSN25dYCx5au02V82I1begI8HCKM5EOYUmAkW4s11Ctyls_qRlMb7rXwhknQX9KXU1SKX2pPURHcGVaMPC0Wz-8HqVl0o2qD3Pst1SPDVO2DHuAElwHn_RpkQGdIpVbl8pBWJJ1vRC3nXrwFiOr7s5GnLcdmNOcdAYC65Mj5R4h9nj5K-QqfLO5v_2h1kgd_SugdXEDaersbpoIjwc8ZGzWvl-Y8lg95Dde7003__mC0)
- Xác định một số thuộc tính và quan hệ giữa các lớp phân tích:
  + Lớp User:
    * Thuộc tính: userID, username, password.
    * Quan hệ: Tương tác với LoginForm để nhập thông tin đăng nhập.
  + Lớp LoginForm:
    * Thuộc tính: inputUsername, inputPassword.
    * Quan hệ: Nhận dữ liệu từ User và gửi đến AuthenticationService để xác thực.
  + Lớp AuthenticationService:
    * Thuộc tính: userDatabase .
    * Quan hệ: Nhận thông tin từ LoginForm, kiểm tra và gửi phản hồi về trạng thái đăng nhập.
  + Lớp SessionManager:
    * Thuộc tính: sessionID, userID, sessionExpiry.
    * Quan hệ: Tương tác với AuthenticationService để thiết lập phiên cho người dùng đã đăng nhập thành công.
  + Lớp ErrorDisplay:
    * Thuộc tính: errorMessage.
    * Quan hệ: Nhận thông tin từ AuthenticationService khi xảy ra lỗi xác thực.
- Biểu đồ lớp mô tả các lớp phân tích:
  ![Class Diagram](https://www.planttext.com/api/plantuml/png/V5DBJiCm4Dtd55uc4hr05gX0YuH49KJL0mp9j5WuTfYnMoh4oLXm9Aw0xNoQfX7P97upy-RD6-Vt-sVE5iYwIYNy9hKWmvWK2fZ5Xf74PoByCnFE7nuMkLXRadet03LKE89hNtqmLFRmLz9IFfgTrFU6gfvNwjhPpJHFZ3sDoKHy2gCK5lQEi4Hj9IXEipPKIguL76ElPsIdR4hnbOjROnI2pawARfnz3GG5M6dq6cal2poRUW4MNe2zk1NKROizA5c2nM7xiHbN5pvalO1J_pKo-yOhqB0RsCqDFEdu1TWcBpzgISTSUC7OkKJe3ssFzBpOgsa3RN8LDNJ95me6fYs932qQctl96C2Lh_8aesNngpd4chGwZqVEUCzci-l1xSX5JMOlIsIX0YXAj20L9wUKK32zlDmReaiEmtVBIQOp0yTe0RaWV7V8bZjR6nF3HogtpUQpV_Y6Gn1QHzepkQBmPCAGsFen7E5ea3D31nAYfzs5Zlr3FNe1oTpF6FxQFm000F__0m00)

- Ý nghĩa của biểu đồ lớp trong hệ thống "Login":
  + User nhập thông tin đăng nhập và chuyển tới LoginForm.
  + LoginForm truyền thông tin đăng nhập tới AuthenticationService để kiểm tra.
  + AuthenticationService xác thực thông tin đăng nhập:
    * Nếu thành công: AuthenticationService gọi SessionManager để tạo phiên làm việc, và trả về thông báo đăng nhập thành công cho LoginForm.
    * Nếu thất bại: AuthenticationService trả về thông báo lỗi cho LoginForm, và LoginForm yêu cầu ErrorDisplay hiển thị lỗi cho người dùng.
## 4. Phân tích ca sử dụng Maintain Employee Information
- Xác định các lớp phân tích cho ca sử dụng: Trong ca sử dụng "Maintain Employee Information" , các lớp phân tích chính sẽ bao gồm:
  + Payroll Administrator: Thực hiện thao tác quản lý nhân viên thông qua yêu cầu tới hệ thống.
  + Employee: Lưu trữ thông tin chi tiết của từng nhân viên.
  + EmployeeManager: Thực hiện các thao tác nghiệp vụ cần thiết để duy trì thông tin nhân viên.
  + Database: Lưu trữ và quản lý dữ liệu lâu dài của nhân viên.
- Mô tả hành vi thông qua biểu đồ sequence:
  ![Sequence Diagram](https://www.planttext.com/api/plantuml/png/v5KnRzD06DtzApvrQgGqtJEWDhWII20n10d6o_aKdte-M_QvQaQK0I64H6S620XLH48WmPGREZZg_xXVm5_WEpjjV0vEqvabYPptFh_tlUVp7trrb2cIgZmINdRA9QHnnZn2LPp2Cp99Oo6EWuXBdgcKs8iaW_A2bo2BKvuGgU0aIaGyOUmfaMJCIj3gfmFpYI8ZaZ7xlp_moZbmyE06suU7eT7l953y-aP1BgTo3Fl7GN3uF0c8OeS-4qonZaU4GXK147bxw_PfUmtaddSZ4y4bgmylYtaEr2mkSr1XyHjlgt2O38lF4ivuCPV_6fyZ33bVanOEx2lyx8A8pMB6kx2yCFejATszwVPwlKvToEtO8O9ZO2knZts8ZFx0wr1_q8SdrpzRfVe3EAXFV57CS9cXMNoN85QyJp84QjdhmUjj3AkvemA587OUEQuSDfD1cKOLq8w1R8Blo0ItG8s-9BidijvVStF3D9_0UOuerPvRoEeHT3PMEapDuWkS6VsgBOHDFu-uqLExFcp1FLg6iILLUcrwcmuToWY5IXY7tCqmZUsghcUG6VqH0gD_W41zh_EjxQ4DCJkto25kAnDuPPsg1tt7Ecs2_uSwEK-rFM0GYG5IE2z-tUMiphNmfgdb-sA6gGJeAdUis2DiMb6szMHvKUENUkvJbgO1bto29yuHDiM-iVu2003__mC0)
- Xác định một số thuộc tính và quan hệ giữa các lớp phân tích:
  + Lớp Payroll Administrator:
    * Thuộc tính: adminID,name,role.
    * Quan hệ: Gửi yêu cầu quản lý nhân viên đến EmployeeManager để thực hiện các thao tác cần thiết.
  + Lớp Employee:
    * Thuộc tính:employeeID, name, employeeType, address, socialSecurityNumber, standardTaxDeductions, otherDeductions, phoneNumber, hourlyRate, salary, commissionRate, hourLimit.
    * Quan hệ: Được quản lý bởi EmployeeManager trong suốt các thao tác thêm, cập nhật, và xóa.
  + Lớp EmployeeManager:
    * Thuộc tính: employeeList.
    * Quan hệ:Nhận yêu cầu từ Payroll Administrator và thực hiện các thao tác nghiệp vụ cần thiết. Tương tác với Database để lưu trữ, truy xuất và cập nhật dữ liệu nhân viên.
  + Lớp Database:
    * Thuộc tính: employeeRecords.
    * Quan hệ: Nhận các yêu cầu lưu trữ, truy xuất, và cập nhật từ EmployeeManager. Cung cấp khả năng lưu trữ lâu dài cho dữ liệu nhân viên.
- Biểu đồ lớp mô tả các lớp phân tích:
  ![Class Diagram](https://www.planttext.com/api/plantuml/png/d5HTQi9047xFAVPHeLuWY5X82uAMebvWp8wwk3zXPcCRIa_MXnwfL-YcJMARn52QXn2--URRcMyc-_7sFcSFv7EZ8pufAyWnHga6Pl481JcjRwLHLh4dy8x4IoJ2Cn5Geeia5XjFoXugr8B15XGaBj1hL6dVcKox0h7HmmhuYsJDtHPPEmHI4ZAtK7Qf0ht1D2VbYuVSx93Q50zM0iajF2SeyzGhPuDCulATnehZ_17fQZGxEekzsaUNaoxMuB6Lmg21YXQOEcCKSpYX9wEKMYgZV8DtB5s1XGDInzbbc64iolUqfiw-AA9qhOP6okvTt8YDOt5sIbQyF9EXf8RQdTbDHP6B0HM96WTLVjFtoifXSXsj4WveaNxKkKX6u-u69k1X1zpTm3McZcIOxWgoQTrMsp66SxU3QmqJ1XNiIHZguhVNtqNzrt43TAeZzowiS1X0sAy1wuDDlR__P3BhB5eSzCilZjgHajtu70jbVHXCwbayAN_iPJVtmaKqcgELvVtq2G00__y30000)
- Ý nghĩa của biểu đồ lớp trong hệ thống " Maintain Employee Information":
  + PayrollAdministrator tương tác EmployeeManager để quản lý nhân viên.
  + EmployeeManager tương tác với cả hai để quản lý hồ sơ nhân viên Employee và Database xử lý lưu trữ.
## 5. Phân tích ca sử dụng Maintain Purchase Order
- Xác định các lớp phân tích cho ca sử dụng: Trong ca sử dụng "Maintain Purchase Order" , các lớp phân tích chính sẽ bao gồm:
  + CommissionedEmployee: Quản lý đơn đặt hàng của mình thông qua PurchaseOrderManager.
  + PurchaseOrderManager: Xử lý yêu cầu thêm, cập nhật hoặc xóa đơn đặt hàng của nhân viên và tương tác với PurchaseOrder để lưu trữ hoặc xóa thông tin.
  + PurchaseOrder: Chứa thông tin chi tiết của đơn hàng, liên kết với Customer để cung cấp thông tin khách hàng.
  + Customer: Cung cấp thông tin liên hệ và địa chỉ thanh toán cho PurchaseOrder.
- Mô tả hành vi thông qua biểu đồ sequence:
  ![Sequence Diagram](https://www.planttext.com/api/plantuml/png/t9GnIyD05CVtV8etwY3k3bA81GThEoXqFIv7BzXSujr5sb4wYJWukpI8GuU2e5CpE5pfzxXFu5VmvG9wRMfnDaEEaD_xl_V_lv3FygEbD94wJuQ1kee5o5InW52TIWZJ98cLYbF1edQI3TCnOq0KXEqWmvAOnXaH6dgvf9merfKHanqYo8392kjrExzpDH04OHiEZYiKZY3ajdmGGF6OKH3BYHZ0NYWPqUpmCekguuGDcMRxGK266kfNtxhWX0F0gz93MHG_WdDk5_CCD3VlgAVHul9nLGZWPYe6ZbwR8KU8siMBN-5hzhf8NTX5aVewaDZoAMxqzjGIyxobW8cezbBx-wEN3QrT9hQXQqvaFePHZgpUmlr8zas1AwdQ2xZEnxQy5Q2hMkeckZ5JVCHKgi2uAPfHdCQsd60DBlVUuPIda74pozp2xmG7PSivQPfn3LnhlMkBlgkprMlkinjXrr_HFmxR5nYPjsQe7j2Oiey5Q-Evt5fuhtuINm000F__0m00)
- Xác định một số thuộc tính và quan hệ giữa các lớp phân tích:
  + Lớp CommissionedEmployee:
    * Thuộc tính:employeeID, name.
    * Quan hệ: Kết nối với PurchaseOrder để quản lý đơn đặt hàng của mình.
  + Lớp PurchaseOrder:
    * Thuộc tính: orderID, contact, billingAddress, productList, date, status.
    * Quan hệ: Kết nối với CommissionedEmployee để xác nhận quyền truy cập và quản lý đơn hàng.
  + Lớp PurchaseOrderManager :
    * Thuộc tính:orderDatabase.
    * Quan hệ: Tương tác với CommissionedEmployee để thực hiện các thao tác thêm, sửa, và xóa đơn đặt hàng. Quản lý các quy trình kiểm tra và xác thực quyền truy cập của nhân viên.
  + Lớp Customer:
   * Thuộc tính:customerID, contactInfo, billingAddress.
   * Quan hệ: Liên kết với PurchaseOrder để lưu thông tin chi tiết liên quan đến khách hàng.
- Biểu đồ lớp mô tả các lớp phân tích:
  
  ![Class Diagram](https://www.planttext.com/api/plantuml/png/f991IiGm58RtESMxG2zGf8pCA0meYfuWayPEc3IfoOjGn4EuTZFYGXYO2xJ8B2hUeoVm2gQrj5Ix4Do4b_VoV-z_IJxBmymYDUXIIUn6A33QSi8ajHRcEas5jK8h7f-acTGvvt1F00BWtNQv2E4QZL19crOqvQC4wn5N57tfL6gAv85q7IwTOMjg-OM9kUdGkeb_S9bMI1akrOqUvLT2IXyVnx7XrevAcT6nOtWcB8RGh4VVnMXeicWjDMkRy_U0Re1CcpodYYPZhnv0LxxUjHaTZmRCt5dKQIzbtVP_athwv2i5GJJjEuIaBlS2ychdWDN5goEJvtu1l1ADonlDFeExQWkthYvU5CZgROnejVsq8KXHxHHiwkA0W7Nv9FvesKk75l3--F6iO5rj_THanbNS_DWl0000__y30000)
- Ý nghĩa của biểu đồ lớp trong hệ thống " Maintain Purchase Order":
  + CommissionedEmployee gửi yêu cầu tới PurchaseOrderManager để quản lý đơn đặt hàng.
  + PurchaseOrderManager thực hiện các thao tác tạo, cập nhật và xóa trên các đối tượng PurchaseOrder.
  + PurchaseOrder chứa thông tin đơn hàng và liên kết với Customer để truy cập thông tin khách hàng.
  + Customer cung cấp thông tin liên hệ và địa chỉ thanh toán cho PurchaseOrder.
## 6. Phân tích ca sử dụng Run Payroll
- Xác định các lớp phân tích cho ca sử dụng: Trong ca sử dụng "Run Payroll" , các lớp phân tích chính sẽ bao gồm:
  + PayrollSystem: Đại diện cho hệ thống thực hiện các hoạt động tính toán và thanh toán lương cho nhân viên.
  + Employee: Đối tượng nhân viên, chứa các thông tin cá nhân cần thiết cho việc tính lương và phương thức thanh toán.
  + Timecard: Lưu trữ dữ liệu về giờ làm việc của nhân viên, bao gồm cả giờ làm thêm, dùng để tính lương.
  + PurchaseOrder: Đại diện cho các đơn đặt hàng hoặc giao dịch của nhân viên, dùng để tính các khoản hoa hồng nếu có.
  + BankSystem: Hệ thống ngân hàng xử lý giao dịch chuyển khoản nếu nhân viên chọn phương thức thanh toán qua chuyển khoản.
  + Paycheck: Đại diện cho phiếu lương hoặc các giao dịch thanh toán được tạo cho nhân viên.
- Mô tả hành vi thông qua biểu đồ sequence:
  ![Sequence Diagram](https://www.planttext.com/api/plantuml/png/X5F1YjH04BtdA-geCFw01rbc610K9fWWNjjEasucwSuctOivU_Iq9n4HPrn4L0PS58JqOG-zx7_q5-mlMDqxwoIBO227TBtt-jMhohMzEEeqQRMfgwHR2mcjwbX2g5OjfAHlLLLbVQTP3QI3D4iQn0eg6Y8rBEkcKZrZeRISL79HCqhQ8bJonQIKcfPoqh5LMx0sYgwcTT9JpkWwbgRKEP7hWvbvbYHf1WyUeIru24-ujny5N9vw-qwMyCp8M_zxr191J_tmkOU2I0wTsr8EahjF4aw4-oQ1-k6B1Cr3LIktbKcbL0FFlNqleFRshHZ34y3dHZbVe7JUcXvU6Rn0mqi_dA47ol6h1kf-oN84JrTtu9UdLriPd0-_DN2tGUezwOSBWzIVzyVCq6ZkTcYmklg1f18ARyy9w3OqK0flFq3bDlLihnd5Pj1mDr2el3qJCpXn6rW7PmPftdwF-gJ2vFbUKsEKN-auYI0QqUTuBD1Q0roXNGh71cz7ObGPEOsH-66hudsuLmqNiQMzyGD-SJkSXGcPeR7cds1MTUo_7YatlRUl9NQemX3ks9fd4rkbjpk1iH4LSdmJzg4C0uwn_QNE3zc_mAN19V33JevfD_vaaOHtDAh72eL0no6F5p8vGc3uu_u0003__mC0)
- Xác định một số thuộc tính và quan hệ giữa các lớp phân tích:
  + Lớp PayrollSystem:
    * Thuộc tính: payrollDate, payFrequency.
    * Quan hệ: Tương tác với các lớp Employee, Timecard, PurchaseOrder, và BankSystem để lấy thông tin và xử lý các thanh toán.
  + Lớp Employee:
    * Thuộc tính: employeeID, salary, benefits, paymentMethod.
    * Quan hệ: Kết nối với PayrollSystem để nhận lương, và có quan hệ với Timecard và PurchaseOrder để xác định dữ liệu tính toán lương.
   + Lớp Timecard:
     * Thuộc tính: hoursWorked, overtimeHours, date.
     * Quan hệ: Kết nối với Employee và PayrollSystem để cung cấp dữ liệu lương.
   + Lớp PurchaseOrder:
     * Thuộc tính: orderID, amount, commission.
     * Quan hệ: Kết nối với Employee và PayrollSystem để tính lương dựa trên hoa hồng.
   + Lớp BankSystem:
     * Thuộc tính:transactionID, transactionStatus.
     * Quan hệ: Tương tác với PayrollSystem để xử lý và xác nhận giao dịch chuyển khoản.
   + Lớp Paycheck:
     * Thuộc tính: paycheckID, grossPay, netPay, deductions.
     * Quan hệ: Được tạo bởi PayrollSystem và cung cấp cho Employee khi phương thức thanh toán là qua thư hoặc nhận trực tiếp.
- Biểu đồ lớp mô tả các lớp phân tích:
  
  ![Class Diagram](https://www.planttext.com/api/plantuml/png/Z9F1JiCm38RlVOfe9pZq1NP04neJEo0cRHBda7fhr2OPjZDK8PwC0u_4Av1stPfqa-1IDVRV_xCTz-VhUqOiaRsfCwgq5UW8CbLB8h6I3RgwNZV4OCH79aGkziVON39CHViyHHS8RnwiQgPYpQZjBYI4G6zxbvlRx3FhZH_CldODGEy9_N4vZxxD1SbQOh1Rr4vo5ta52rlDbCW2su3b9-3I5IaS5EW3X09Y-4ORK1AB7buwZ_JYi88YHha380VbOvkE4qNSkH0xu9FXqcvT35fvLAKaUCO2iAUvzdtKfpJEMuuPoXcZYRIpGxH39PPZthsqLN9NZDAIL1nyHiWeisR9dfAvxT4f8DeCegGjsQWIL3KiH7SS4NPXZoX8uxPiQ22D553u3a1fenOm3FX4EjBJRSppks6DfcAYBOTl59DurrnEhgZFznxK2A5IE01T4wRtzfSwclg_oZYFBwWLGcWps9ux6HVgwI9zKTvHCmDRj3_nBm000F__0m00)
- Ý nghĩa của biểu đồ lớp trong hệ thống "Run Payroll":
  + PayrollSystem là trung tâm của quy trình Run Payroll, lấy dữ liệu từ Employee, Timecard, và PurchaseOrder.
  + Employee chứa thông tin cá nhân và lương, sử dụng Timecard và PurchaseOrder để cung cấp thông tin cần thiết cho PayrollSystem.
  + BankSystem xử lý các giao dịch ngân hàng khi phương thức thanh toán là chuyển khoản.
  + Paycheck chứa thông tin phiếu lương, được tạo bởi PayrollSystem khi thanh toán qua thư hoặc trực tiếp.
