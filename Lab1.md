#
1. Phân tích kiến trúc:
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
