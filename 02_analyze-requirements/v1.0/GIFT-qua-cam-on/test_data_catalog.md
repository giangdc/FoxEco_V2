# Test Data Catalog — v1.0 · Module GIFT

> Tạo bởi: analyze-requirements (**stage: analyze**).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.

## Module GIFT — Quà cảm ơn (DOC-v1.0-01 §A7/§D3/§D4 · DOC-v1.0-02 §3.8 · DOC-v1.0-06)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Trạng thái đơn (tiền đề) | Fixture | **`Hoàn thành`** (bắt buộc) | mọi trạng thái khác — nút tặng quà chưa tồn tại | **`Đã giao` → `Hoàn thành`** = ranh giới mở được màn Tặng quà | `§A7` L107 · KP-01 §5.1 (ô 5·Sender) |
| Loại quà | Master | 1 trong 4: `Bông hoa` · `Ly cà phê` · `Gấu bông` · `Vương miện` | loại thứ 5 · không chọn loại nào | — (tập đóng 4 giá trị) | `§A7` L108 · `GIFT-01` L258 · `DOC-v1.0-02` §3.8 |
| Số lần gửi quà / đơn | Runtime | **1 lần** | gửi lần 2 cho cùng đơn (nút đã disable) | **lần 1 (enable) → lần 2 (disable)** | KP-01 §6 KB-GIFT-01 |
| Nhãn nút của Sender | Runtime | `✓ Cảm ơn người vận chuyển` (trước gửi, enable) → `Bạn đã đánh giá` (sau gửi, disable) | nhãn không đổi sau khi gửi | **thời điểm đổi nhãn = ngay sau khi gửi thành công** | KP-01 §6 KB-GIFT-01 · §5.1 ô 5·Sender |
| Text popup sau khi gửi | Master | ⚠ **2 nguồn 2 text:** `Đã gửi lời cảm ơn!` (PRD+Figma — dùng bản này) ⟷ `Cảm ơn của bạn đã được gửi` (`US-D15`) | — | — (chốt theo PRD+Figma; `C-GIFT-03`) | `DOC-v1.0-02` §3.8 · `US-D15` L194 |
| Số loại quà đã nhận (Carrier) | Runtime | 1..4 loại có `count > 0` | — | **0 loại (màn rỗng hoàn toàn — `SC-GIFT-008`)** · **2/4 loại (kiểm rule count>0 — `SC-GIFT-006`)** · **4/4 loại** | KP-01 §6 KB-GIFT-03 · `US-D20` L196 |
| Số lượng mỗi loại quà | Runtime | số nguyên > 0 | hiển thị dạng `0` cho loại chưa nhận → sai rule | **1 (vừa nhận lần đầu)** | KP-01 §6 KB-GIFT-03 |
| Danh sách lịch sử nhận quà | Runtime | ⚠ **chỉ có 1 nguồn văn bản** (`US-D20`), chưa có ảnh/app → ghi nhận, không assert | — | — | `US-D20` L196 · KP-01 §6 KB-GIFT-03 (ghi chú) |
| Thanh toán / quy đổi tiền | — | ⛔ **KHÔNG tồn tại** — giá trị assert-absent cho `SC-GIFT-004` | mọi thành phần giá tiền/ví/cổng thanh toán | — | `BR-GIFT-01` L271 · `NT-03` L15 · `§A7` L111 |
| Màn chấm sao 1–5 | — | ⛔ **KHÔNG tồn tại ở v1.0** — assert-absent cho `SC-GIFT-011` | màn/control chấm sao xuất hiện | — | `BR-INT-06` L82 · `§A8` L125 · `C-GIFT-01` |
| Text thông báo nhận quà | Master | "Bạn nhận được một món quà cảm ơn 🎁 — mở Trang cá nhân để xem" | — | ⚠ Figma bổ sung dòng 2: *"[Tên] đã gửi tặng bạn một món quà..."* | `NTF-07` L325 · KP-07 hàng #7 |

## Ghi chú chung
- **`Loại data`:** `Fixture` = QC tạo (đẩy đơn tới "Hoàn thành" — cần phối hợp 3 vai) · `Master` = danh mục/text cố định · `Runtime` = app sinh (số đếm quà, nhãn nút, số lần gửi).
- ⭐ **Tiền đề chi phối toàn module:** đơn phải ở **"Hoàn thành"**, tức phải chạy xong `SC-DLV-023` (Receiver xác nhận). ⛔ Không có đơn Hoàn thành thì **12/12 SC blocked**.
- ⚠️ **Ba trạng thái tài khoản Carrier cần seed để phủ card đếm:** (a) **0 loại** quà (màn rỗng hoàn toàn — không phải "4 số 0") · (b) **2/4 loại** (kiểm rule *chỉ hiện loại count>0*) · (c) tuỳ chọn **4/4 loại**.
- ⚠️ **Nút tặng quà chỉ dùng được 1 lần/đơn** ⇒ mỗi lần test `SC-GIFT-003`/`SC-GIFT-005` **tiêu 1 đơn Hoàn thành**; lên kế hoạch số đơn cần seed tương ứng.
- **3 giá trị assert-absent:** thanh toán/quy đổi tiền · màn chấm sao 1–5 · (gián tiếp) điểm uy tín — cả 3 **không thuộc v1.0**, dùng để chứng minh app đúng scope.
