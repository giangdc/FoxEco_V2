# Test Data Catalog — v1.0 · Module DLV

> Tạo bởi: analyze-requirements (**stage: analyze**).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.

## Module DLV — Giao nhận & Theo dõi đơn (DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-04 · DOC-v1.0-06)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Trạng thái đơn | Fixture | `Chờ ghép` · `Đã ghép` · `Đang giao` · `Đã giao` · `Hoàn thành` | `Đã huỷ` · `Hết hạn` (ngoài luồng giao nhận) | **5 trạng thái = 5 tiền đề bắt buộc cho ma trận nút** (⛔ thiếu 1 trạng thái là thiếu 3 SC) | KP-01 §5.1 KB-DLV-01 · `§D2` L232 |
| Vai trò tài khoản với đơn | Fixture | `Sender` (chủ tin) · `Carrier` (người nhận mang giúp) · `Receiver` (người nhận được khai) | tài khoản không thuộc đơn (không có màn Theo dõi đơn) | **3 vai × 5 trạng thái = 15 ô ma trận** ⇒ cần **3 tài khoản** dùng chung 1 đơn | KP-01 §5.1 KB-DLV-01 |
| Nhãn nút / nhãn trạng thái | Runtime | text đúng theo ô ma trận (vd `✓ Tôi đã lấy hàng`, `Đã ghép · chờ shipper lấy hàng`) | nhãn lệch ô ma trận | **ô 4·Receiver = nút enable DUY NHẤT trong 15 ô** | KP-01 §5.1 KB-DLV-01 |
| Trạng thái enable/disable | Runtime | enable đúng 4 ô (1·Carrier, 2·Carrier, 3·Carrier, 4·Receiver, 5·Sender) | enable ở ô lẽ ra disable → vi phạm quyền hạn | **ô 4: Sender/Carrier disable, Receiver enable** — điểm phân định `C-DLV-01` | KP-01 §5.1 KB-DLV-01 · `BR-INT-03` L79 |
| Nội dung popup xác nhận | Master | 3 câu nguyên văn: *"Bạn xác nhận đã lấy hàng từ người gửi và bắt đầu giao?"* · *"Bạn xác nhận đã giao hàng tận tay người nhận?"* · *"Bạn xác nhận đã nhận được hàng từ người vận chuyển?"* | popup thiếu / đổi trạng thái ngay không qua popup | **title popup cố định = "Xác nhận"** (cả 3 hành động) | KP-01 §5.1 (bảng popup) · `DOC-v1.0-02` §6 L191 |
| Thanh 5 mốc trạng thái | Runtime | `Chờ ghép → Lấy hàng → Đang giao → Đã giao → Hoàn thành` | thứ tự lệch · thiếu mốc | ⚠ **mốc 2 = "Lấy hàng"** nhưng badge = **"Đã ghép"** (2 chữ cho 1 trạng thái `MATCHED`) | `US-D09` L178 · `§D2` L232 · KP-01 §5.1 |
| Mốc LỊCH SỬ | Runtime | `Đăng tin → Ghép thành công → Lấy hàng → Đã giao → Hoàn thành` + timestamp mỗi mốc | thiếu timestamp · thiếu mốc | ⚠ **danh sách KHÁC thanh trạng thái** (có "Đăng tin", "Ghép thành công") | `DOC-v1.0-02` §3.6 dòng "Lịch sử" · `US-D09` L178 |
| Cụm liên hệ theo vai | Runtime | Sender → cụm "Người vận chuyển" · Carrier → **cả 2 cụm** "NGƯỜI GỬI" + "NGƯỜI NHẬN" · Receiver → chỉ cụm "NGƯỜI GIAO HÀNG" | cụm hiện **trước** khi ghép (→ vi phạm `BR-CON-02`) · Receiver thấy thông tin Người gửi | **ranh giới `Chờ ghép` → `Đã ghép`** = thời điểm cụm liên hệ xuất hiện | `DOC-v1.0-02` §3.6/§4.3/§5.2 · `US-D08` L177 |
| Nhãn phụ màn Theo dõi đơn | Runtime | `Tôi gửi hàng` (Sender) · `Tôi giao hàng` (Carrier) · `Tôi nhận hàng` (Receiver) | nhãn không khớp vai đang đăng nhập | — (tập hữu hạn 3 giá trị) | `DOC-v1.0-02` §3.6/§4.3/§5.2 (tiêu đề section) |
| Thời gian chờ Receiver xác nhận | Runtime | < 2 giờ (chưa nhắc) | — | **2 giờ → nhắc** · **4 giờ (2+2) → admin hỗ trợ** ⇒ ⛔ **cần chờ thật hoặc dev seed timestamp** | `BR-CNF-04` L266 · `US-D14` L193 |
| Ảnh bằng chứng (form đầy đủ) | — | ⛔ **KHÔNG tồn tại ở v1.0** — dùng làm giá trị assert-absent cho `SC-DLV-025` | form đầy đủ xuất hiện → ngoài scope v1.0 (`C-DLV-03`) | — | `DOC-v1.0-02` §5.3 · KP-01 §5 KB-DLV-03 |
| Điểm uy tín carrier (★4.9) | — | ⛔ **KHÔNG tồn tại ở v1.0** — assert-absent (cùng nhóm `C-USR-01`) | — | — | `DOC-v1.0-02` §5.3 dòng "Thông tin Carrier" · `C-USR-01` |
| Chia sẻ vị trí (GPS) | — | ⚠ **chưa chốt mặc định bật/tắt** (`C-DLV-02` Open); ma trận nút ô "Đang giao" không có control này | — | — | `GPS-01` L251 · KP-01 §5 KB-DLV-04 |
| Chi phí đối soát | — | ⚠ **không có bề mặt UI trong 82 ảnh Figma và ma trận nút** | — | — | `COST-01` L256 · `BR-COST-01` L267 |

## Ghi chú chung
- **`Loại data`:** `Fixture` = QC tạo bằng cách đẩy đơn qua các trạng thái (cần 3 tài khoản phối hợp) · `Runtime` = app sinh theo trạng thái + vai · `Master` = text cố định trong app (popup, nhãn).
- ⭐ **Chi phí thiết lập cao nhất dự án:** để phủ 15 ô ma trận cần **1 đơn đi qua đủ 5 trạng thái** × **3 tài khoản** đăng nhập song song. Trạng thái là **một chiều, không lùi được** (mọi transition qua popup xác nhận, không có nút undo) ⇒ **mỗi trạng thái phải xem bằng cả 3 vai TRƯỚC KHI đẩy sang trạng thái kế tiếp**; bỏ sót 1 vai ở 1 trạng thái là phải tạo đơn mới từ đầu.
- ⚠️ **Hai danh sách mốc khác nhau** — thanh trạng thái (5 mốc, bắt đầu "Chờ ghép") ⟷ block Lịch sử (5 mốc, bắt đầu "Đăng tin", có "Ghép thành công"). ⛔ Đừng dùng lẫn khi viết TC completeness.
- ⚠️ **`SC-DLV-029` (lịch sử) phải chạy trên đơn đi thẳng tới Hoàn thành** — `C-CNL-02` ghi nhận hành vi hiện tại: **huỷ nhận đơn XOÁ dòng "Ghép thành công"** khỏi LỊCH SỬ ⇒ đơn từng bị huỷ nhận sẽ thiếu mốc.
- ⚠️ **`SC-DLV-024` cần 2 giờ + 4 giờ thực tế** hoặc dev seed timestamp ⇒ lên kế hoạch riêng, ⛔ không "đánh PASS cho xong".
- **3 giá trị assert-absent quan trọng:** ảnh bằng chứng · điểm uy tín carrier · control chia sẻ vị trí — cả 3 **không thuộc v1.0**, dùng để chứng minh app đúng scope.
