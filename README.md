# Court Sport - Website Quản Lý Đặt Sân Bóng Đá Và Cầu Lông

## Thông Tin Đồ Án
* **Trường:** Đại học Hùng Vương TP. Hồ Chí Minh
* **Khoa:** Kỹ thuật - Công nghệ
* **Môn học:** Lập trình Web
* **Lớp:** CT07A
* **Giảng viên hướng dẫn:** TS. Lê Duy Tân
* **Nhóm thực hiện:** 4AN1PM
* **Thời gian thực hiện:** Năm học 2025-2026

---

## Thành Viên Nhóm & Phân Công Nhiệm Vụ

Hệ thống đánh giá đóng góp công việc nội bộ đạt sự đồng thuận 100% cho tất cả các thành viên:

| STT | Họ và Tên | MSSV | Nhiệm Vụ Đảm Nhiệm | Mức Độ Đóng Góp |
| :---: | :--- | :---: | :--- | :---: |
| 1 | **Phan Huỳnh Phi Long** | 2305CT2242 | Trưởng nhóm, Đảm nhiệm phần Frontend | 100% |
| 2 | **Võ Bá Huy** | 2305CT2318 | Lập trình Backend, Thiết kế bản thuyết trình PowerPoint | 100% |
| 3 | **Nguyễn Huy Đạt** | 2305CT2334 | Xử lý các chức năng nghiệp vụ CRUD, Viết báo cáo Word | 100% |
| 4 | **Hồ Lữ Anh Kiệt** | 2305CT0199 | Viết báo cáo Word, Hỗ trợ thiết kế bản thuyết trình PowerPoint | 100% |
| 5 | **Nguyễn Thiên Bảo** | 2305CT0628 | Thiết kế và cấu hình hệ thống Database | 100% |

---

## Giới Thiệu Đề Tài
Hiện nay, phần lớn các cơ sở kinh doanh sân thể thao vẫn áp dụng hình thức quản lý thủ công hoặc qua điện thoại, dẫn đến việc nhầm lẫn lịch, mất thời gian và khó tra cứu thông tin. Website **Court Sport** ra đời nhằm cung cấp nền tảng trực tuyến giúp người dùng dễ dàng tìm kiếm, đặt sân, thanh toán theo thời gian thực và hỗ trợ các đơn vị quản lý vận hành kinh doanh hiệu quả.

### Đối Tượng Sử Dụng Hệ Thống
1. **Khách hàng:** Đăng ký/đăng nhập, tìm kiếm sân trống, xem lịch, đặt sân và thanh toán.
2. **Quản lý:** Quản lý sân thuộc chi nhánh, quản lý đơn đặt và theo dõi doanh thu chi nhánh.
3. **Chủ kinh doanh:** Quản lý chuỗi chi nhánh, cấu hình giá, khung giờ, nhân viên và xem báo cáo tổng.
4. **Quản trị viên (Admin):** Quản trị toàn bộ hệ thống, tài khoản và phân quyền người dùng.

---

## Yêu Cầu Kỹ Thuật (Non-functional Requirements)
* **Kiến trúc:** Phát triển theo mô hình chuẩn **MVC** (Model - DAO - Servlet/Controller - JSP View).
* **Backend:** Xử lý Request/Response bằng **Java Servlet** kết nối qua **JDBC**.
* **Frontend:** Giao diện hiển thị động bằng **JSP**, thiết kế responsive thân thiện trên mọi thiết bị.
* **Database:** Hệ quản trị cơ sở dữ liệu **MySQL**, sử dụng cấu trúc Engine **InnoDB** và bảng mã **utf8mb4_unicode_ci**.

---

## Kiến Trúc Cơ Sở Dữ Liệu (`BookingFieldDB`)

Hệ thống bao gồm **07 bảng dữ liệu** được thiết kế chuẩn hóa chặt chẽ:
1. `roles`: Lưu trữ cấu hình vai trò hệ thống (ADMIN, USER...).
2. `users`: Quản lý thông tin tài khoản, mật khẩu băm bảo mật và điểm thưởng (`reward_points`).
3. `categories`: Danh mục bộ môn thể thao (Bóng đá, Cầu lông...).
4. `fields`: Danh sách các sân đấu thực tế kèm đơn giá và trạng thái (AVAILABLE, MAINTENANCE...).
5. `time_slots`: Cấu hình các ca/khung giờ cố định trong ngày.
6. `bookings`: Đơn đặt sân chi tiết của khách hàng.
7. `payments`: Biên lai thanh toán dòng tiền ('CASH', 'QR_CODE', 'BANK_TRANSFER').

### Sơ đồ Thực thể - Liên kết (ERD)
Sơ đồ quan hệ thực tế giữa các bảng dữ liệu trong hệ thống:

![Sơ đồ ERD]<img width="952" height="630" alt="anh" src="https://github.com/user-attachments/assets/82e08585-20ca-4041-8080-9004c8060494" />


> **Quy Tắc Vàng (Real-time Validation):**
> Hệ thống áp dụng ràng buộc duy nhất `CONSTRAINT uq_realtime_booking UNIQUE (field_id, booking_date, slot_id)`. Ràng buộc này đảm bảo tại một sân, vào một ca giờ của một ngày cụ thể, chỉ chấp nhận duy nhất một đơn đặt thành công.

---

## Hướng Dẫn Cài Đặt & Chạy Dự Án

### 1. Khởi tạo Database
* Mở MySQL Server của bạn (qua XAMPP, MySQL Workbench hoặc DBeaver).
* Import và thực thi toàn bộ nội dung file script `mysql.sql` để tạo cấu trúc cơ sở dữ liệu `BookingFieldDB` cùng dữ liệu cấu hình mẫu.

### 2. Cấu hình Connection
* Mở project bằng NetBeans hoặc các IDE Java hỗ trợ.
* Tìm đến file kết nối cơ sở dữ liệu trong mã nguồn (thuộc tầng DAO/Util) để cập nhật thông tin `user` và `password` MySQL tương thích với máy của bạn.

### 3. Khởi chạy Ứng dụng
* Deploy project lên bộ Web Server Container (khuyên dùng **Apache Tomcat 8.5/9.0**).
* Thực hiện tác vụ `Clean and Build` dự án, sau đó nhấn `Run` để kiểm thử phần mềm trên trình duyệt.
