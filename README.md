# Court Sport - Website Quản Lý Đặt Sân Bóng Đá Và Cầu Lông

## Thông Tin Đồ Án
* **Trường:** Đại học Hùng Vương TP. Hồ Chí Minh[cite: 2]
* **Khoa:** Kỹ thuật - Công nghệ[cite: 2]
* **Môn học:** Lập trình Web[cite: 2]
* **Lớp:** CT07A[cite: 2]
* **Giảng viên hướng dẫn:** TS. Lê Duy Tân[cite: 2]
* **Nhóm thực hiện:** 4AN1PM[cite: 2]
* **Thời gian thực hiện:** Năm học 2025-2026[cite: 2]

---

## Thành Viên Nhóm & Phân Công Nhiệm Vụ

Hệ thống đánh giá đóng góp công việc nội bộ đạt sự đồng thuận 100% cho tất cả các thành viên[cite: 2]:

| STT | Họ và Tên | MSSV | Nhiệm Vụ Đảm Nhiệm | Mức Độ Đóng Góp |
| :---: | :--- | :---: | :--- | :---: |
| 1 | **Phan Huỳnh Phi Long** | 2305CT2242 | Trưởng nhóm, Đảm nhiệm phần Frontend[cite: 2] | 100%[cite: 2] |
| 2 | **Võ Bá Huy** | 2305CT2318 | Lập trình Backend, Thiết kế bản thuyết trình PowerPoint[cite: 2] | 100%[cite: 2] |
| 3 | **Nguyễn Huy Đạt** | 2305CT2334 | Xử lý các chức năng nghiệp vụ CRUD, Viết báo cáo Word[cite: 2] | 100%[cite: 2] |
| 4 | **Hồ Lữ Anh Kiệt** | 2305CT0199 | Viết báo cáo Word, Hỗ trợ thiết kế bản thuyết trình PowerPoint[cite: 2] | 100%[cite: 2] |
| 5 | **Nguyễn Thiên Bảo** | 2305CT0628 | Thiết kế và cấu hình hệ thống Database[cite: 2] | 100%[cite: 2] |

---

## Giới Thiệu Đề Tài
Hiện nay, phần lớn các cơ sở kinh doanh sân thể thao vẫn áp dụng hình thức quản lý thủ công hoặc qua điện thoại, dẫn đến việc nhầm lẫn lịch, mất thời gian và khó tra cứu thông tin[cite: 2]. Website **Court Sport** ra đời nhằm cung cấp nền tảng trực tuyến giúp người dùng dễ dàng tìm kiếm, đặt sân, thanh toán theo thời gian thực và hỗ trợ các đơn vị quản lý vận hành kinh doanh hiệu quả[cite: 2].

### Đối Tượng Sử Dụng Hệ Thống
1. **Khách hàng:** Đăng ký/đăng nhập, tìm kiếm sân trống, xem lịch, đặt sân và thanh toán[cite: 2].
2. **Quản lý:** Quản lý sân thuộc chi nhánh, quản lý đơn đặt và theo dõi doanh thu chi nhánh[cite: 2].
3. **Chủ kinh doanh:** Quản lý chuỗi chi nhánh, cấu hình giá, khung giờ, nhân viên và xem báo cáo tổng[cite: 2].
4. **Quản trị viên (Admin):** Quản trị toàn bộ hệ thống, tài khoản và phân quyền người dùng[cite: 2].

---

## Yêu Cầu Kỹ Thuật (Non-functional Requirements)
* **Kiến trúc:** Phát triển theo mô hình chuẩn **MVC** (Model - DAO - Servlet/Controller - JSP View)[cite: 2].
* **Backend:** Xử lý Request/Response bằng **Java Servlet** kết nối qua **JDBC**[cite: 2].
* **Frontend:** Giao diện hiển thị động bằng **JSP**, thiết kế responsive thân thiện trên mọi thiết bị[cite: 2].
* **Database:** Hệ quản trị cơ sở dữ liệu **MySQL**, sử dụng cấu trúc Engine **InnoDB** và bảng mã **utf8mb4_unicode_ci**[cite: 2].

---

## Kiến Trúc Cơ Sở Dữ Liệu (`BookingFieldDB`)

Hệ thống bao gồm **07 bảng dữ liệu** được thiết kế chuẩn hóa chặt chẽ[cite: 2]:
1. `roles`: Lưu trữ cấu hình vai trò hệ thống (ADMIN, USER...)[cite: 2].
2. `users`: Quản lý thông tin tài khoản, mật khẩu băm bảo mật và điểm thưởng (`reward_points`)[cite: 2].
3. `categories`: Danh mục bộ môn thể thao (Bóng đá, Cầu lông...)[cite: 2].
4. `fields`: Danh sách các sân đấu thực tế kèm đơn giá và trạng thái (AVAILABLE, MAINTENANCE...)[cite: 2].
5. `time_slots`: Cấu hình các ca/khung giờ cố định trong ngày[cite: 2].
6. `bookings`: Đơn đặt sân chi tiết của khách hàng[cite: 2].
7. `payments`: Biên lai thanh toán dòng tiền ('CASH', 'QR_CODE', 'BANK_TRANSFER')[cite: 2].

### Sơ đồ Thực thể - Liên kết (ERD)
Sơ đồ quan hệ thực tế giữa các bảng dữ liệu trong hệ thống[cite: 2]:

![Sơ đồ ERD](https://images.squarespace-cdn.com/content/v1/5f3dfd683692df460b642646/1720510191834-8KDR61GNGD55VWS9W6CP/image_71f1c7.jpg)

> **Quy Tắc Vàng Chống Trùng Lịch (Real-time Validation):**
> Hệ thống áp dụng ràng buộc duy nhất `CONSTRAINT uq_realtime_booking UNIQUE (field_id, booking_date, slot_id)`[cite: 2]. Ràng buộc này đảm bảo tại một sân, vào một ca giờ của một ngày cụ thể, chỉ chấp nhận duy nhất một đơn đặt thành công[cite: 2].

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
