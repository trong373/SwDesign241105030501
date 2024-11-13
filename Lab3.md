# LAB3 - Xác định các phần tử thiết kế của hệ thống “Payroll System”

## 1. Subsystem context diagrams:
 a. BankSystem:
 - Biểu đồ Ngữ Cảnh:
   ![Context Diagram](https://www.planttext.com/api/plantuml/png/L90zYiCm48LxdM8k4BPF4OB1R6jmiwsYY4ZO7YsM752TCbLk46TP5WBfjfAB5Cf5vWHxXPL3VaWvxxtl3Ro_uJotZhUkQsfcAutG6YiP5ywqK73VcheklNMo0MwXA6zEnh5wojbTpflFsdWfHp5dh2XXCaikJE6TXfC67uyT20e_7QmqDx2aOIiK2DLv6ZO8bJ8Klf1bLx0OmO_O2q15uOGlZ5DnZmcDlxY2jtHI-7QmeD3h6vu_tgRic5h4thnqN7OKpfZQum5XhUCH6PjBN8vR_0C00F__0m00)
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

   ![Context Diagram](https://www.planttext.com/api/plantuml/png/N8yn3e8m58Rtdk9Tm0iu61RYIiBYsjH66iihQOi9n_06uc92GkBW10D33VVW15x10ih0zbw-x_zVtgVj0cEfjdagYJaB1AqC9vHPfI6YXLPIneMnF0Lg88h_H0kqCTSNmVWCvlc7mpIJgk0J2Wc9OjZi5WUsi1_QMa3XgXpOq3noy7UpH0nDbuFidts99xBeKzI73gvaWCdGr3ZwDd4tJ82vrqeEbmEhIdXV_Og-mzqHBi9LI4Z0yJZ-_WK00F__0m00)
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
  
    ![Context Diagram](https://www.planttext.com/api/plantuml/png/RCynJiCm50RWtQVuBy056527Hh1KYfI9yTMnwa3yNDalI9aPUugM0QbI1oGcF33u93u1Lo29wCRoXlT_-gN_9tsleb2GmVKgFdUCuADHfCK7r3G6t_VD6CKuK4JTN9FWduoM3J7jZ3CiQnBQKZIBsgp_MENslH_DygsKgXlStCqnRl6OpmDq-NeVuF8RzZPVq9RqWNnaDPDPDXEyB-dIeIMsYFcexNzywQqc_D2LzCeGMz9XklcJTv1fr9L2Mm-s-SHuwVAPbLePRkVjlm000F__0m00)
- Giải thích các thành phần trong biểu đồ ngữ cảnh ProjectManagementDatabase:
  + PayrollSystem:
    * Hệ thống bảng lương yêu cầu thông tin về mã phí dự án để tính toán báo cáo lương hoặc tạo báo cáo chi tiết về các dự án mà nhân viên tham gia.
    * Sau khi nhận thông tin từ ProjectManagementDatabase, hệ thống sẽ hiển thị cho nhân viên nếu cần thiết.
  + ProjectManagementDatabase:
    * Là cơ sở dữ liệu quản lý các dự án, lưu trữ thông tin chi tiết về các mã phí và dự án mà nhân viên tham gia.
    * Nó gửi thông tin về mã phí dự án theo yêu cầu từ PayrollSystem.
  + Employee:
    * Nhân viên có thể xem thông tin về các mã phí dự án khi hệ thống bảng lương hiển thị thông tin này.
