# Open-Source SOC Lab: Monitoring & Incident Response Automation

![SOC Architecture](https://github.com/dphu27/SOC-Lab/blob/main/SOC%20Architecture.png)

## 📝 Tổng quan dự án
Dự án này tập trung vào việc thiết kế và triển khai một hệ thống Trung tâm Điều hành An ninh mạng (SOC) hoàn chỉnh dựa trên các công cụ mã nguồn mở. Hệ thống không chỉ dừng lại ở việc giám sát (Monitoring) mà còn tự động hóa quy trình phản ứng (Automation Response) đối với các sự cố an ninh mạng thực tế.

**Mục tiêu chính:**
- Xây dựng hạ tầng giám sát tập trung.
- Tự động hóa việc phân tích và xử lý cảnh báo.
- Mô phỏng và xây dựng kịch bản phát hiện cho các kỹ thuật tấn công phổ biến (MITRE ATT&CK).

## 🛠 Tech Stack
Hệ thống được tích hợp từ các thành phần mạnh mẽ:
- **SIEM:** [Wazuh](https://wazuh.com/) (Giám sát log, phát hiện xâm nhập, kiểm tra tính tuân thủ).
- **Logging & Visualization:** [ELK Stack](https://www.elastic.co/elastic-stack) (Elasticsearch, Logstash, Kibana).
- **SOAR:** [Shuffle](https://shuffler.io/) (Tự động hóa quy trình phản ứng - Workflow Automation).
- **Case Management:** [TheHive](https://thehive-project.org/) (Quản lý sự cố và cộng tác điều tra).
- **Threat Intelligence:** [MISP](https://www.misp-project.org/) & [Cortex](https://github.com/TheHive-Project/Cortex).
- **Infrastructure:** pfSense (Firewall), Snort (IDS/IPS), Docker, VMware/Proxmox.

## 🏗 Kiến trúc hệ thống
Hệ thống được thiết kế theo mô hình phân lớp nhằm đảm bảo tính bảo mật và khả năng mở rộng:
1. **Data Collection:** Agent (Wazuh, Sysmon) thu thập log từ Endpoint (Windows, Linux).
2. **Processing & Analysis:** Wazuh Manager phân tích log dựa trên các Rule-set.
3. **Automation Flow:** Khi có cảnh báo mức độ cao, Wazuh gửi Webhook tới Shuffle.
4. **Enrichment & Response:** Shuffle truy vấn Threat Intel (MISP/Cortex) và tự động tạo Ticket trên TheHive để Analyst xử lý.

## 🛡 Các kịch bản tấn công & phòng thủ (Use Cases)
Dưới đây là các kịch bản thực tế đã được triển khai và kiểm thử trong Lab:

### 1. Tấn công hạ tầng mạng (Layer 2)
- **Kịch bản:** DHCP Starvation & Rogue DHCP.
- **Phát hiện:** Sử dụng Suricata để phát hiện các gói tin DHCP bất thường và cảnh báo về SIEM.
- **Xử lý:** Cấu hình Alert Level cao trên Wazuh để thông báo ngay lập tức cho quản trị viên.

### 2. Tấn công chiếm quyền điều khiển (Malware/Rootkit)
- **Kịch bản:** Cài đặt Rootkit (Adrishya) trên Linux server.
- **Phát hiện:** Sử dụng tính năng **FIM (File Integrity Monitoring)** và **Rootcheck** của Wazuh để phát hiện sự thay đổi bất thường trong nhân hệ điều hành.

### 3. Tấn công ứng dụng Web & Brute Force
- **Kịch bản:** File Upload, Command Injection (trên DVWA) và SSH Brute Force.
- **Phản ứng tự động:** Shuffle nhận cảnh báo từ Wazuh, tự động trích xuất IP kẻ tấn công và thực hiện chặn (Block IP) trên Firewall pfSense thông qua API và thông qua tính năng Active Response của Wazuh.

## 🚀 Kết quả đạt được
- Tối ưu hóa quy trình xử lý sự cố: Giảm thời gian từ lúc phát hiện đến khi có Ticket (MTTD) xuống dưới 1 phút.
- Xây dựng được bộ quy tắc (Custom Rules).
- Tích hợp thành công luồng dữ liệu Threat Intelligence giúp làm giàu thông tin cảnh báo tự động.

## 📖 Tài liệu liên quan
- [Link xem báo cáo đồ án chi tiết (https://github.com/dphu27/SOC-Lab/blob/main/SOC-Lab.pdf)]

