
# LAB3 - AN TOÀN VÀ BẢO MẬT HỆ THỐNG THÔNG TIN

## 1. Thông tin sinh viên

- **Họ và tên:** Nguyễn Thị Thanh Thảo
- **MSSV:** 1050070046
- **Mã lớp:** 11_ĐH_TMĐT
- **Tên lab:** LAB3: Nhận diện và ứng phó các mối đe dọa đến an toàn thông tin
- **Repository:** LAB_AT_BMHTTT

## 2. Môi trường thực hành

| Thành phần | Phiên bản |
|---|---|
| Windows | Windows 11] |
| VMware | [Phiên bản] |
| Python | 3.14.7 |
| Wireshark | 4.6.8 |


- **Video:**: https://youtu.be/B52A7G1XwkQ

## 3. Mục tiêu

- Phân biệt Vulnerability, Threat, Risk và Attack.
- Phân tích mã độc, xác thực, keylogging, persistence, DoS/DDoS, sniffing và phishing.
- Sử dụng Defender, Event Log, Sysmon, Autoruns, Process Explorer và Wireshark.
- Thu thập bằng chứng, kiểm tra SHA-256 và thực hiện Incident Response.

## 4. Cách dựng môi trường

1. Khởi động máy ảo Windows trên VMware.
2. Kiểm tra phiên bản và công cụ thực hành.
3. Chuẩn bị thư mục lưu output, log và evidence.
4. Thực hiện các tình huống theo phạm vi LAB3.

## 5. Tình huống và kết quả

| Nội dung | Kết quả |
|---|---|
| Khái niệm và nguồn đe dọa | [PASS/FAIL] |
| Defender và EICAR | [PASS/FAIL] |
| Xác thực và mật khẩu | [PASS/FAIL] |
| Backdoor và Persistence | [PASS/FAIL] |
| DoS/DDoS và Mail Bombing | [PASS/FAIL] |
| Sniffing và MITM | [PASS/FAIL] |
| Social Engineering/Phishing | [PASS/FAIL] |
| Incident Response | [PASS/FAIL] |
| SHA-256 | [PASS/FAIL] |
| Defense-in-Depth | [PASS/FAIL] |

## 6. Cấu trúc thư mục

```text
LAB3/
├── README.md
├── [BaoCao].docx
├── evidence_sha256.csv
├── outputs/
└── screenshots/
```

## 7. Lỗi gặp phải và cách khắc phục

- **Lỗi:** [Mô tả lỗi]
- **Nguyên nhân:** [Nguyên nhân]
- **Khắc phục:** [Cách khắc phục]

## 8. Bằng chứng và an toàn

- Ảnh chụp trực tiếp từ VM/PC.
- Output và log đã làm sạch, khớp timestamp bài lab.
- Không upload mật khẩu, token, cookie, dữ liệu cá nhân hoặc file bị Defender quarantine.
- Không thực hiện DDoS, mail bombing, spoofing hoặc MITM ngoài phạm vi lab.
- Không chỉnh `local_load_test.py` để hướng đến mục tiêu khác `127.0.0.1:8080`.

## 9. Kiểm tra trước khi nộp

- [ ] Đã commit/push toàn bộ file.
- [ ] Có báo cáo Word đúng tên yêu cầu.
- [ ] Có `evidence_sha256.csv`.
- [ ] Đã kiểm tra quyền truy cập repository ở chế độ Public.
- [ ] Đã dán URL repository vào Google Classroom.
