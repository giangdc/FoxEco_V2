# Test Data Catalog — v1.0 · Module NTF

> Tạo bởi: analyze-requirements (**stage: analyze**).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.

## Module NTF — Thông báo (DOC-v1.0-01 §D6/§D7 · DOC-v1.0-02 §2/§3.2 · DOC-v1.0-04 · DOC-v1.0-06)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Sự kiện kích hoạt | Fixture | 8 sự kiện có SC: ghép ngay · khớp tuyến · lấy hàng · đã giao · hoàn tất · huỷ · quá hạn (+ nhận quà ở `GIFT`) | sự kiện không thuộc `NTF-01..09` | ⚠ **danh sách chính thức CHƯA CHỐT** — `KP-07` có **12 hàng** ứng viên (`C-NTF-01`) | `§D6` L317-327 · KP-07 |
| Người nhận thông báo | Runtime | theo cột "Người nhận" của `§D6` (1 hoặc 2 người/sự kiện) | người ngoài đơn nhận được thông báo | **`NTF-04/05/06` có 2 người nhận** ⇒ phải kiểm cả 2 | `§D6` L317-327 |
| Nội dung thông báo | Master | text theo `§D6`; ⚠ `NTF-08` Figma **cụ thể hơn** BRD | ⛔ **chứa số điện thoại** (vi phạm `OPR-07`) | **`NTF-01` nhắc "SĐT đã được lộ" nhưng KHÔNG chứa số** — ranh giới hợp lệ/vi phạm | `§D6` L317-327 · `OPR-07` L343 · KP-07 hàng #8 |
| Kênh gửi | Runtime | **in-app** + **push** | thiếu 1 trong 2 kênh | **push là kênh dễ lọt SĐT** (nội dung do backend đẩy, không qua UI) | `§D6` L315 |
| Nhóm thời gian | Runtime | `Hôm nay` · `Hôm qua` · `Tuần này` | — | **thông báo cũ hơn 1 tuần → nhóm nào? (chưa có nguồn)** | `DOC-v1.0-02` §3.2 |
| Trạng thái đọc/chưa đọc | Runtime | chấm đỏ theo **từng item** | chấm đỏ theo cả nhóm | **cần item đã đọc + chưa đọc trong CÙNG 1 nhóm** để phân biệt (đúng cấu hình ảnh Figma) | KP-01 §8 KB-NTF-01 · `DOC-v1.0-04` `3e626d39…` |
| Cơ chế "Đánh dấu đã đọc" | Runtime | ⚠ **chưa chốt** mark-all hay mark-per-item (`C-NTF-03a` Open) | — | — (⛔ không assert) | KP-01 §8 KB-NTF-01 |
| Số thông báo trong danh sách | Fixture | ≥1 thông báo | — | **0 (empty state — `C-ORD-06`)** · **dài hơn 1 trang (kích hoạt lazy-load)**; ⛔ không assert số item/trang | KP-01 §8 KB-NTF-02 · `C-ORD-06` |
| Chấm đỏ ở chuông (header) | Runtime | hiện khi có ≥1 thông báo chưa đọc | hiện khi đã đọc hết · không hiện khi còn chưa đọc | **ranh giới: đọc thông báo chưa đọc cuối cùng → chấm đỏ phải tắt** | `DOC-v1.0-02` §2 dòng "Header" |
| Text `NTF-06` | Master | ⚠ **2 nguồn 2 text:** BRD *"Đơn đã hoàn tất — cảm ơn bạn!"* ⟷ PRD+Figma *"Đơn đã hoàn thành — **đánh giá ngay**"* | — | ⚠ bản PRD+Figma dùng từ "đánh giá" trong khi rating đã defer (`C-GIFT-01`) | `§D6` L324 · KP-07 hàng #6 |
| Loại thông báo ngoài BRD | — | ⚠ `KP-07` hàng **#10** (*"Sắp đến khung giờ hẹn giao"*) có bằng chứng **cả Demo và Figma** nhưng KHÔNG có trong `§D6` | — | — (ứng viên BRD sót — chờ `C-NTF-01`) | KP-07 hàng #10 |
| Loại thông báo đã loại | — | ⛔ **#6b** *"nhận đánh giá 5 sao"* (`C-GIFT-01`) · ⛔ **#11** *"cộng đồng đạt mốc X đơn / CO₂"* (`C-USR-01`) — dùng làm assert-absent | 2 loại này xuất hiện trên app → ngoài scope v1.0 | — | KP-07 hàng #6b/#11 |

## Ghi chú chung
- **`Loại data`:** `Fixture` = QC tạo bằng cách kích hoạt sự kiện nghiệp vụ (đăng tin · ghép · lấy hàng · giao · huỷ) · `Runtime` = app sinh (nội dung, người nhận, trạng thái đọc, nhóm thời gian) · `Master` = text cố định.
- ⭐ **Module này KHÔNG có trường nhập nào** — mọi thông báo là **hệ quả của sự kiện ở module khác** ⇒ để phủ 16 SC cần **chạy trọn 1 vòng đời đơn** (`ORD` → `ASN` → `DLV` → `GIFT`) + **1 lượt huỷ** (`CNL`) + **1 tin quá hạn** (nhờ dev seed). ⇒ Chạy `NTF` **cuối lô** để tận dụng thông báo đã phát sinh.
- ⚠️ **Boundary quan trọng nhất là nội dung thông báo:** `NTF-01` **được phép nhắc** *"SĐT đã được lộ"* nhưng ⛔ **không được chứa số điện thoại** — đây là ranh giới hợp lệ/vi phạm của `SC-NTF-008` (P1). Kiểm **cả in-app và push**.
- ⚠️ **Cần 2 loại tài khoản cho chấm đỏ:** (a) có thông báo **đã đọc + chưa đọc trong cùng 1 nhóm thời gian** (`SC-NTF-010`); (b) **chưa có thông báo nào** (`SC-NTF-015` empty state).
- ⛔ **Không assert:** danh sách loại thông báo (chưa chốt — `C-NTF-01`) · cơ chế nút "Đánh dấu đã đọc" (`C-NTF-03a`) · số item/trang khi lazy-load · nhóm cho thông báo cũ hơn 1 tuần · độ trễ thông báo khớp tuyến (`C-NTF-02`).
