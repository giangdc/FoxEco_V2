# Test Data Catalog — v1.0 · Module CNL

> Tạo bởi: analyze-requirements (**stage: analyze**).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.

## Module CNL — Huỷ đơn / Huỷ nhận đơn (DOC-v1.0-01 §D3/§D4/§D7/§D8.3 · DOC-v1.0-06)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Trạng thái đơn khi huỷ | Fixture | `Chờ ghép` (POSTED) · `Đã ghép` (MATCHED) | `Đang giao` (IN_TRANSIT) trở đi → **không ai huỷ được** · `Hoàn thành` · `Đã huỷ` | **`Đã ghép` → `Đang giao`** = ranh giới mất quyền huỷ | `OPR-11` L347 · `US-D16` L195 |
| Hành động huỷ | Fixture | **"Huỷ đơn"** (Sender/Receiver → `CANCELLED`) ⟷ **"✕ Huỷ nhận đơn"** (Carrier → về `POSTED`) | dùng lẫn 2 hành động | ⚠ **2 hành động khác kết quả** — điểm dễ trộn nhất của module | `OPR-09` L345 · `KB-DLV-01` ô 2·Carrier |
| Vai trò người huỷ | Fixture | `Sender` · `Carrier` · `Receiver` (theo permission matrix) | vai không có quyền ở trạng thái đó | **`Admin` — có trong matrix nhưng ⛔ không test được** (Admin Portal out of scope) | `§D4` permission matrix L285 · `C-TS-01` |
| Lý do huỷ | Fixture | text **≥ 5 ký tự** (spec `VAL-04`) | rỗng (app chặn đúng) | **4 ký tự (spec chặn — ⚠ app CHO QUA)** · **5 ký tự (hợp lệ)** · **5 dấu cách (spec chặn sau trim — ⚠ app CHO QUA)** | `VAL-04` L395 · `VAL-03` L394 · KP-01 §7 KB-CNL-02 |
| Trạng thái nút "Xác nhận" trong popup | Runtime | khoá khi lý do rỗng; bật khi lý do hợp lệ | bật khi lý do < 5 ký tự → **gap** (`SC-CNL-004`) | **ranh giới 4 ↔ 5 ký tự** | `US-D16` L195 · `VAL-04` L395 |
| Đơn sau khi "Huỷ đơn" | Runtime | trạng thái `Đã huỷ`; ⛔ **không hiển thị ở cả 2 tab màn Hoạt động** | vẫn hiện ở Bảng tin / màn Hoạt động | — | `§D2` L233 · KP-01 §3 KB-ORD-07 (#7) |
| Đơn sau khi "Huỷ nhận đơn" | Runtime | trạng thái về `Chờ ghép`; **hiện lại trên Bảng tin**; ghép lại được | chuyển `Đã huỷ` (sai) · không hiện lại trên Bảng tin | — | `OPR-09` L345 · `OPR-08` L344 |
| Log LỊCH SỬ sau khi huỷ | Runtime | ⚠ **spec: phải CÓ dòng log** (vai + lý do) | app hiện: **không ghi log** (huỷ đơn) · **XOÁ dòng "Ghép thành công"** (huỷ nhận đơn) → 2 bug | **dòng "Ghép thành công" phải CÒN sau khi huỷ nhận** (`BR-INT-04` audit) | KP-01 §7 KB-CNL-01 · `BR-INT-04` L80 · `TS-01/TS-02` L121-122 |
| Banner sau khi huỷ | Runtime | banner đỏ *"Đơn hàng đã bị huỷ"* | — | — (⚠ banner **không thay thế** được log LỊCH SỬ) | KP-01 §7 KB-CNL-01 |
| Số phiên/thiết bị đồng thời | Fixture | 3 phiên (Sender · Carrier · Receiver) trên 3 tài khoản khác nhau | 1 phiên đổi vai (không kiểm chứng được realtime) | **3 phiên cho `SC-CNL-011`** | `BR-INT-05` L81 · `§D2` L233 |
| Màn "Báo sự cố" | — | ⛔ **KHÔNG tồn tại ở v1.0** — assert-absent cho `SC-CNL-006` | — | — | `§D2` L233 (`[INCIDENT]`) · KP-01 §5 KB-DLV-05 · `C-CNL-01` |

## Ghi chú chung
- **`Loại data`:** `Fixture` = QC tạo (đơn ở trạng thái cần + tài khoản đúng vai + lý do nhập tay) · `Runtime` = app sinh (trạng thái sau huỷ, log, banner, trạng thái nút).
- ⭐ **Boundary quan trọng nhất của module là chuỗi lý do huỷ:** `rỗng` (app chặn đúng) → **`4 ký tự`** (spec chặn, **app cho qua** → bug) → `5 ký tự` (hợp lệ) → **`5 dấu cách`** (spec chặn sau trim, **app cho qua** → bug). Đây là 4 mốc phải test đủ; 2 mốc giữa là 2 bug đã live-verify.
- ⚠️ **Phân biệt nghiêm ngặt 2 hành động huỷ** — "Huỷ đơn" kết thúc đơn (`CANCELLED`); "Huỷ nhận đơn" **trả đơn về `POSTED`** để người khác nhận. Trộn 2 hành động là lỗi thiết kế TC dễ mắc nhất ở module này.
- ⚠️ **Đơn "Đã huỷ" biến mất khỏi màn Hoạt động** (`KB-ORD-07` #7) ⇒ sau khi chạy SC huỷ thì **không xem lại được đơn đó từ phía user**; muốn verify log thì phải mở block LỊCH SỬ **trước khi** rời màn Theo dõi đơn.
- **Tiền đề cần seed:** đơn ở `POSTED` · đơn ở `MATCHED` · đơn ở `IN_TRANSIT` (cho `SC-CNL-005`) + **3 tài khoản 3 vai** + **3 phiên đồng thời** (cho `SC-CNL-011`).
