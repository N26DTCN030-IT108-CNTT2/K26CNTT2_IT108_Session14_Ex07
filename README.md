# K26CNTT2_IT108_Session14_Ex07😊

# 💻 Báo cáo Bài tập: Giải cứu Dữ liệu Nhóm Startup CampusPay & Thiết lập Hybrid Workflow
**Môn học:** Nhập Môn Công Nghệ Thông Tin (Buổi 15: Không gian cộng tác đám mây)  
**Học viên:** Lê Hồ Thanh Thảo (N26DTCN030)  
**Repository:** `K26CNTT2_IT108_Session14_Ex07`

---

## 1. Mục tiêu
- Phân biệt đặc điểm và rủi ro giữa **Local Storage** và **Cloud Storage** trong thực tế làm việc nhóm dự án Startup.
- Phát hiện các nguyên nhân cốt lõi gây mất dữ liệu và đề xuất mô hình **Hybrid Workflow** khắc phục triệt để.

---

## 2. Bối cảnh & Vấn đề
> **Tình huống:** Nhóm 5 sinh viên xây dựng startup **"CampusPay"** (ví điện tử cho sinh viên PTIT) lưu toàn bộ tài liệu cốt lõi trên máy tính cá nhân của trưởng nhóm. Một tuần trước ngày pitching, ổ cứng laptop trưởng nhóm bị hỏng khiến toàn bộ 3 tháng làm việc biến mất hoàn toàn, khiến nhóm mất cơ hội tranh giải.

---

## 3. Yêu cầu đầu ra

### Phần 1: Phân tích vấn đề

#### 1. Đánh giá rủi ro và Nguyên nhân gốc rễ cho từng hạng mục tài liệu
| Hạng mục tài liệu | Rủi ro mất mát (%) | Nguyên nhân gốc rễ (Tổ chức / Công nghệ) | Xếp loại |
| :--- | :---: | :--- | :---: |
| **Business Plan** (20 trang trên `D:/CampusPay/Plan/`) | **100%** | **Công nghệ:** Lưu trữ cục bộ đơn điểm (`Single Point of Failure`), không có bản sao dự phòng trên Cloud. | **Cao (Critical)** |
| **Mã nguồn giao diện HTML/CSS** (trên USB của thành viên A) | **80%** | **Tổ chức & Công nghệ:** Phụ thuộc vào thiết bị ngoại vi dễ thất lạc, hỏng hóc; thiếu cơ chế quản lý tập trung. | **Cao (High)** |
| **Database danh sách test user** (trên Excel cá nhân thành viên B) | **70%** | **Tổ chức:** Phân mảnh dữ liệu, lưu trữ rời rạc trên máy cá nhân không đồng bộ thời gian thực. | **Trung bình (Medium)** |
| **Slide Pitch PowerPoint** (trên Zalo Cloud `v7_final_FINAL`) | **50%** | **Tổ chức:** Đặt tên file thủ công hỗn loạn, không kiểm soát được đâu là phiên bản chuẩn xác nhất. | **Trung bình (Medium)** |
| **Tài liệu SRS** (gửi qua lại qua Email đính kèm) | **60%** | **Tổ chức:** Giao tiếp qua kênh rời rạc, làm đứt gãy luồng quản lý phiên bản tài liệu. | **Trung bình (Medium)** |

#### 2. Hiện tượng "23 phiên bản file tồn tại trên nhiều thiết bị"
* **Tên gọi kỹ thuật:** Hiện tượng **Phân mảnh phiên bản (Version Fragmentation / "DLL Hell" / File Chaos)** kết hợp với hậu quả của việc **Thiếu hệ thống Quản lý Cấu hình (Configuration Management)**.
* **Nguyên nhân:** Do nhóm giao tiếp thủ công qua Zalo, mỗi thành viên chỉnh sửa độc lập trên máy cá nhân rồi truyền tay nhau tệp tin mà không có một cơ chế đồng bộ tự động hay kho lưu trữ chung trung tâm (`Centralized/Cloud Repository`).
* **Hậu quả trong dự án thực tế:** Gây xung đột mã nguồn (`Merge Conflict`), mất thời gian ráp nối thủ công, dễ đưa nhầm phiên bản lỗi lên bản demo chính thức, và làm suy giảm nghiêm trọng hiệu suất làm việc nhóm.

---

### Phần 2: Sửa lỗi & Nghiệm thu

#### 3. Thiết kế Quy trình Hybrid Workflow cho nhóm CampusPay
Mô hình kết hợp tối ưu giữa tốc độ của ổ cứng cục bộ (`SSD Local`) và tính an toàn, đồng bộ của đám mây (`Cloud Workspace` như Google Drive / OneDrive):

```text
 1. ẠO & SỬA FILE (Local SSD)
    [Lập trình viên viết code / sửa file trên máy cá nhân (SSD ~3000 MB/s)]
                   │
                   ▼ (Nhấn Ctrl+S)
 2. TỰ ĐỘNG ĐỒNG BỘ (Auto Sync)
    [Phần mềm Cloud chạy ngầm tự động phát hiện thay đổi và đẩy gói dữ liệu lên mây]
                   │
                   ▼
 3. AN TOÀN TRÊN ĐÁM MÂY (Cloud Storage)
    [Dữ liệu được lưu trữ an toàn, sinh Version History và đồng bộ đa thiết bị]
```
Phần mềm đề xuất: Google Drive for Desktop hoặc OneDrive.

Thư mục được Sync: Thư mục dự án cốt lõi (C:/CampusPay_Project/).

Thư mục KHÔNG nên Sync: Thư mục chứa game, phim ảnh cá nhân, tệp hệ thống tạm thời (temp, cache, node_modules nặng) để tránh làm tràn dung lượng Cloud và gây treo phần mềm đồng bộ.

4. Giải quyết "Bẫy dữ liệu" khi gập máy trước khi Sync hoàn tất
Biểu tượng hiển thị trên File Explorer:

Khi file đang sửa: Hiển thị biểu tượng vòng xoay xanh (Syncing / Pending).

Nếu gập máy khi chưa xong: Trạng thái hiển thị dấu chấm than hoặc biểu tượng hàng đợi ngắt kết nối do mạng yếu/mất kết nối đột ngột.

Hệ thống xử lý: Tiến trình đồng bộ bị treo giữa chừng, dữ liệu trên mây chưa được cập nhật phiên bản mới nhất từ Local.

Giải pháp cho thành viên trước khi tắt máy:

Mở khay hệ thống (System Tray) kiểm tra biểu tượng Cloud để đảm bảo hiển thị tích xanh (Up to date / Synced).

Tuyệt đối không gập máy hoặc ngắt mạng ngay sau khi bấm Ctrl+S khi đang có file dung lượng lớn hoặc đường truyền Internet không ổn định.
