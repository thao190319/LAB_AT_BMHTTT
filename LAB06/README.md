# 🛡️ pfSense Network Security Lab: Firewall Policy, Captive Portal & DMZ Implementation

Repository này lưu trữ tài liệu hướng dẫn, sơ đồ triển khai và file cấu hình mẫu (`config.xml`) cho bài Thực hành Tường lửa pfSense và Hệ thống xác thực Captive Portal trong môi trường mạng doanh nghiệp giả lập.

---

## 🎯 Mục Tiêu Bài Lab (Lab Objectives)

* **Thiết kế & Phân vùng Mạng (Network Segmentation):** Xây dựng mô hình mạng gồm các vùng LAN, DMZ, MGMT và WAN độc lập.
* **Tích hợp Tường lửa & Xác thực (Authentication):** Cấu hình Captive Portal trên vùng LAN tích hợp xác thực người dùng qua Active Directory (LDAP/AD).
* **Kiểm soát Truy cập Chi tiết (Access Control Lists - ACLs):** Thiết lập quy tắc tường lửa (Firewall Rules) lọc lưu lượng theo Địa chỉ IP (Aliases), Cổng dịch vụ (Ports) và Khung giờ làm việc (Schedules).
* **Bảo vệ Vùng DMZ (DMZ Hardening):** Triển khai chính sách một chiều (LAN $\rightarrow$ DMZ) và chặn hoàn toàn kết nối ngược lại từ DMZ vào vùng LAN nội bộ.
* **Phân tích Cơ chế Tường lửa:** So sánh chuyên sâu hành vi xử lý lưu lượng **Block vs Reject** và kỹ năng đọc nhật ký (**Firewall Logs & State Table**).

---

## 📐 Mô Hình Mạng (Network Topology)

Mô hình mạng bao gồm các vùng chức năng chính:
* **LAN (10.6.0.0/24):** Vùng mạng người dùng nội bộ (`Client-A`, `Client-B`, `DC01 - Active Directory/DNS`).
* **DMZ (172.16.6.0/24):** Vùng chứa các dịch vụ Web công cộng (`GENERAL_SITE`, `JOB_SITE`, `SOCIAL_SITE`, `RESTRICTED_SITE`).
* **MGMT (10.6.100.0/24):** Vùng quản trị hệ thống độc lập an toàn.
* **pfSense Gateway:** Đóng vai trò là Tường lửa trung tâm, Router và Captive Portal Gateway.

---

## 📋 Tóm Tắt 7 Kịch Bản Kiểm Thử (Lab Scenarios)

| Kịch bản | Tên kịch bản | Nội dung kiểm thử & Yêu cầu kỹ thuật |
| :---: | :--- | :--- |
| **01** | **Xác thực Captive Portal qua AD** | Cấu hình Captive Portal trên LAN, tích hợp LDAP kết nối Active Directory. Xác thực thành công tài khoản domain trước khi cấp quyền truy cập Internet/DMZ. |
| **02** | **Cấu hình Alias & Lọc IP/Port** | Tạo Aliases gom nhóm máy trạm (`CLIENT_A`, `POLICY_CLIENTS`) và Web Servers. Viết rule chặn `CLIENT_A` truy cập `JOB_SITE` (Port 80) nhưng cho phép truy cập `GENERAL_SITE`. |
| **03** | **Quản lý Truy cập theo Giờ (Schedule)** | Cấu hình Time Schedule (`WORK_HOURS`, `LUNCH`). Cho phép `CLIENT_B` truy cập `SOCIAL_SITE` duy nhất trong giờ nghỉ trưa và tự động chặn ngoài giờ. |
| **04** | **Phân quyền Group Policy (Role-based)** | Định nghĩa nhóm `POLICY_CLIENTS`. Cho phép nhóm chỉ truy cập các cổng Web chuẩn (`WEB_PORTS`: 80, 443) trong giờ làm việc và chặn toàn bộ các lưu lượng/trang web khác (`RESTRICTED_SITE`). |
| **05** | **Cô lập Vùng DMZ (DMZ Isolation)** | Cho phép chiều truy cập từ LAN sang DMZ (`GENERAL_SITE`), nhưng chặn hoàn toàn kết nối chủ động từ server DMZ (`Kali Linux`) ngược về máy chủ LAN (`DC01`). |
| **06** | **So sánh cơ chế Block & Reject** | Thử nghiệm chặn kết nối TCP Port 80 từ Client-A đến JOB_SITE: <br>- **Block:** Âm thầm thả gói tin, client chờ hết thời gian gian phản hồi (`Connection timed out` ~30s). <br>- **Reject:** Ngắt kết nối tức thì bằng gói TCP RST (`Connection refused` <1s). |
| **07** | **Đọc Firewall Log & State Table** | Bật logging trên các rule quan trọng. Lọc Log theo IP Source (`10.6.0.21`), đối chiếu thông tin Interface/Action/Port. Quan sát và quản lý bảng trạng thái kết nối (`State Table`). |
