# Test Data Catalog — v1.0 · Module TS

> Tạo bởi: analyze-requirements (**stage: analyze**).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.
> ⚠️ Module **phần lớn backend/Admin** ⇒ catalog mỏng: không có trường nhập, chỉ có dữ liệu **dẫn xuất từ log** và các giá trị **assert-absent**.

## Module TS — Trust & Safety (DOC-v1.0-01 §A5/§A8/§D4/§D5 · DOC-v1.0-06)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Mốc trong LỊCH SỬ | Runtime | `Đăng tin` → `Ghép thành công` → `Lấy hàng` → `Đã giao` → `Hoàn thành`, mỗi mốc có timestamp | thiếu mốc · thiếu timestamp | ⚠ **đơn từng bị huỷ nhận → thiếu mốc "Ghép thành công"** (bug `SC-CNL-010`) ⇒ Given phải là đơn **đi thẳng** | `TS-01` L121 · `ORD-04` L243 · `US-D09` L178 |
| Actor của mỗi mốc | Runtime | ghi rõ ai thực hiện (ai đăng · ai nhận · ai đổi trạng thái · ai huỷ) | mốc không có actor | **mốc huỷ phải có `actor` + `lý do`** — nhóm thông tin thứ 5 của `TS-01`, hiện app **không ghi** | `TS-01` L121 · KP-01 §7 KB-CNL-01 |
| Tính bất biến của log | Runtime | mọi dòng log đã ghi **không bị xoá/sửa** bởi bất kỳ hành động nào | huỷ nhận đơn **XOÁ** dòng "Ghép thành công" → **vi phạm `TS-02`+`BR-INT-04`** | **hành động phải thử:** huỷ nhận đơn · huỷ đơn · sửa tin (khi còn Chờ ghép) | `TS-02` L122 · `BR-INT-04` L80 · KP-01 §7 KB-CNL-01 |
| Consent điều khoản | Fixture | checkbox bắt buộc ở **luồng đăng tin** (NEED B3 + form OFFER) | không có checkbox ở luồng đăng | ⚠ **luồng ghép: chỉ có modal xác nhận lộ SĐT, KHÔNG có consent điều khoản** — rule `§A8` yêu cầu cả 2 | `§A8` L115 · `ORD-09` L245 · `D8.1` L373 · `D8.2` L386 |
| Thời gian chờ → "admin hỗ trợ" | Runtime | < 2 giờ: chưa nhắc | — | **2 giờ → nhắc** · **4 giờ (2+2) → admin hỗ trợ** ⇒ **cùng tiền đề `SC-DLV-024`**, chạy 1 lần dùng cho 2 SC | `BR-CNF-04` L266 · `TS-03` L123 |
| Cơ chế chặn (block) người dùng | — | ⛔ **KHÔNG tồn tại ở v1.0** — assert-absent cho `SC-TS-005` | chức năng chặn/báo cáo user xuất hiện → ngoài phạm vi `§A8` | — | `§A8` L125 |
| Chấm sao / đánh giá | — | ⛔ **KHÔNG tồn tại ở v1.0** — SC đã ở `GIFT` (`SC-GIFT-011`), ⛔ không nhân bản | — | — | `§A8` L125 · `C-GIFT-01` |
| Bề mặt Admin Web Portal | — | ⛔ **KHÔNG có đặc tả UI** ⇒ out of scope v1.0; cột `Admin` trong permission matrix `§D4` **không test được** | — | — | `§A3` L29 · `§D4` L279-286 · KP-01 §9 KB-TS-01 · `C-TS-01` |

## Ghi chú chung
- **`Loại data`:** `Runtime` = dữ liệu log do hệ thống sinh (không nhập được) · `Fixture` = QC tạo (đăng tin để có consent, đẩy đơn để có mốc) · **module này KHÔNG có `Master`**.
- ⭐ **Boundary quan trọng nhất là tập hành động thử ở `SC-TS-003`:** không chỉ *huỷ nhận đơn* (đã biết vi phạm) mà còn **huỷ đơn** và **sửa tin** — mục đích là tìm xem còn đường nào khác cũng làm thay đổi log. Đây là điểm khác biệt so với `SC-CNL-010` (chỉ kiểm 1 hành động).
- ⚠️ **`SC-TS-001`/`SC-TS-002` phải chạy trên đơn đi THẲNG tới Hoàn thành** — đơn từng bị huỷ nhận sẽ thiếu mốc "Ghép thành công" do bug ở `CNL`, dẫn tới chẩn đoán sai.
- ⚠️ **`SC-TS-006` dùng chung tiền đề với `SC-DLV-024`** (chờ 2 giờ + 2 giờ, hoặc dev seed timestamp) ⇒ lên kế hoạch **chạy 1 lần, lấy dữ liệu cho cả 2 SC**.
- **4 giá trị assert-absent của module:** cơ chế chặn user · chấm sao · bề mặt Admin Portal · (gián tiếp) consent ở luồng ghép. Cả 4 dùng để chứng minh app **đúng phạm vi v1.0**, không phải để log bug.
