# Test Data Catalog — v1.0 · Module FEED

> Tạo bởi: analyze-requirements (**stage: analyze**).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.

## Module FEED — Bảng tin & Chi tiết tin (DOC-v1.0-01 · DOC-v1.0-02)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Tin trong Bảng tin | Fixture | tin **NEED** ở trạng thái `POSTED` (Chờ ghép) do tài khoản khác đăng | tin **OFFER** (tuyến Carrier — KHÔNG lên bảng tin) · tin `MATCHED`/`IN_TRANSIT` (bị ẩn theo `OPR-03`/`OPR-08`) | **0 tin (empty state)** · **1 tin** · **≥2 tin (phân biệt mở đúng tin)** | `DOC-v1.0-02` §2 · `US-D11` §D1b L185 · `OPR-03` §D7 L339 |
| Chủ tin (quan hệ với người xem) | Fixture | tin của **người khác** → card không badge, có CTA | tin của **chính mình** → phải có badge + ⛔ không được có CTA (`OPR-05`) | **tin mà người xem là Người nhận được khai** (chủ thể thứ ba — `§7 dòng 9`) | `DOC-v1.0-02` §3.3 đoạn 3/5 · §7 dòng 9 |
| Loại hàng (trên card + chi tiết) | Master | 1 trong 8 giá trị, mặc định **`Tài liệu`** (BA chốt 2026-09-16, `C-ORD-09`) | nhãn khác danh mục PRD (vd `Giấy tờ, hồ sơ` quan sát app 2026-07 ⇒ **defect UI**) | — (tập hữu hạn 8 giá trị) | `DOC-v1.1-01` §8.1.4 · BA trả lời `C-ORD-09` 2026-09-16 |
| Giá trị hàng | Master | `Giá trị thấp` / `vừa` / `cao` | rỗng (chưa chọn — chặn ở B1 khi đăng) | **`cao` → banner cảnh báo (xem `REQ-ORD-004`)** | `D8.1` §D8.1 L359 |
| Ghi chú | Fixture | text ≤ 300 ký tự | > 300 ký tự (chặn khi đăng) | **rỗng (không ghi chú) → chi tiết tin hiện gì?** · **300 ký tự (hợp lệ)** | `D8.1` §D8.1 L358 |
| Ảnh sản phẩm | Fixture | 1 ảnh JPG/PNG ≤ 5MB | — | **KHÔNG có ảnh → ảnh mặc định (`SC-FEED-008`)** | `D8.1` §D8.1 L360 |
| Thời gian đăng (trên card) | Runtime | timestamp lúc đăng tin | — | — (⛔ không assert giá trị tuyệt đối) | `DOC-v1.0-02` §3.3 đoạn 3 |
| Điểm Lấy hàng / Giao hàng | Fixture | địa chỉ văn phòng chọn từ dropdown autocomplete | text gõ tay không chọn gợi ý (không được lưu) | **2 địa chỉ trùng nhau → chặn khi đăng (`D8.1` "phải khác địa chỉ lấy hàng")** | `D8.1` §D8.1 L364/L369 · `DOC-v1.0-06` KP-01 §3 KB-ORD-06 |
| Khoảng cách "~X km" | Runtime | ảnh bản đồ **tĩnh có vẽ tuyến**, km tính **điểm nhận → điểm giao** (BA 2026-09-17) — ⛔ không assert giá trị | — | văn phòng **thiếu toạ độ** ⇒ placeholder + thông báo + **"0km"** (`SC-FEED-015`). ⚠️ File `DOC-v1.1-04`: 61 dòng thiếu lat/lng · 34 dòng ngoài VN · 399 `MISSING` ⇒ `C-FEED-05` | BA trả lời `C-FEED-01(b)` · `C-FEED-02` 2026-09-17 · `DOC-v1.0-02` §3.4 |
| SĐT người gửi (Chi tiết tin) | Runtime | ⛔ **KHÔNG được hiển thị khi trạng thái = Chờ ghép** (`BR-CON-02`) | SĐT hiện sẵn + nút "Gọi" ở Chờ ghép → **bug** (`SC-FEED-010`) | **ranh giới Chờ ghép → Đã ghép: đúng thời điểm SĐT được phép lộ** | `BR-CON-02` §A5 L78 · `OPR-07` §D7 L343 |
| Họ tên người gửi · địa chỉ lấy/giao (Chi tiết tin, trước ghép) | Runtime | **hiển thị** (tên + địa chỉ đầy đủ theo data đã đăng) ở Chờ ghép | — | chỉ SĐT bị ẩn trước ghép | BA trả lời `C-FEED-04` 2026-09-17 (PRD `BR03-03`/`NFR-10` chưa cập nhật) |
| Khung giờ mong muốn | Fixture | khoảng giờ do người đăng chọn (≥30 phút) | — | **cách nhau đúng 30 phút (biên hợp lệ)** | `D8.1` §D8.1 L372 |

## Ghi chú chung
- **`Loại data`:** `Fixture` = QC tự tạo bằng cách đăng tin (module `ORD`) · `Master` = danh mục hệ thống (chip loại hàng/giá trị) · `Runtime` = sinh khi chạy (timestamp, khoảng cách, quyết định lộ SĐT).
- ⚠️ **Dòng "Loại hàng" — đã chốt 2026-09-16:** nhãn chuẩn là **`Tài liệu`** (BA, `C-ORD-09`). Ghi chú cũ *"app không có chip Tài liệu ⇒ dùng Giấy tờ, hồ sơ"* **HẾT HIỆU LỰC** — app còn hiện `Giấy tờ, hồ sơ` là **defect UI**, ⛔ không sửa TC theo app.
- **Bộ dữ liệu tối thiểu để chạy module:** 3 tài khoản (A chủ tin · B người xem · C người nhận được khai) + ≥2 tin NEED `POSTED` + 1 tin không ảnh + 1 tin không ghi chú + 1 tin OFFER (để verify **không** lên bảng tin).
- ⛔ **Không assert** giá trị `~X km`, thời gian đăng, và nội dung ảnh mặc định.
