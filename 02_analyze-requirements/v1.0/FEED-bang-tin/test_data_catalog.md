# Test Data Catalog — v1.0 · Module FEED

> Tạo bởi: analyze-requirements (**stage: analyze**).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.

## Module FEED — Bảng tin & Chi tiết tin (DOC-v1.0-01 · DOC-v1.0-02)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Tin trong Bảng tin | Fixture | tin **NEED** ở trạng thái `POSTED` (Chờ ghép) do tài khoản khác đăng | tin **OFFER** (tuyến Carrier — KHÔNG lên bảng tin) · tin `MATCHED`/`IN_TRANSIT` (bị ẩn theo `OPR-03`/`OPR-08`) | **0 tin (empty state)** · **1 tin** · **≥2 tin (phân biệt mở đúng tin)** | `DOC-v1.0-02` §2 · `US-D11` §D1b L185 · `OPR-03` §D7 L339 |
| Chủ tin (quan hệ với người xem) | Fixture | tin của **người khác** → card không badge, có CTA | tin của **chính mình** → phải có badge + ⛔ không được có CTA (`OPR-05`) | **tin mà người xem là Người nhận được khai** (chủ thể thứ ba — `§7 dòng 9`) | `DOC-v1.0-02` §3.3 đoạn 3/5 · §7 dòng 9 |
| Loại hàng (trên card + chi tiết) | Master | 1 trong 8 chip app STG, mặc định `Giấy tờ, hồ sơ` | ⛔ **"Tài liệu"** — nhãn của tài liệu, **KHÔNG tồn tại trên app** | — (tập hữu hạn 8 giá trị) | `D8.1` §D8.1 L357 · `DOC-v1.0-06` KP-01 §10.2 KB-VIBE-01 |
| Giá trị hàng | Master | `Giá trị thấp` / `vừa` / `cao` | rỗng (chưa chọn — chặn ở B1 khi đăng) | **`cao` → banner cảnh báo (xem `REQ-ORD-004`)** | `D8.1` §D8.1 L359 |
| Ghi chú | Fixture | text ≤ 300 ký tự | > 300 ký tự (chặn khi đăng) | **rỗng (không ghi chú) → chi tiết tin hiện gì?** · **300 ký tự (hợp lệ)** | `D8.1` §D8.1 L358 |
| Ảnh sản phẩm | Fixture | 1 ảnh JPG/PNG ≤ 5MB | — | **KHÔNG có ảnh → ảnh mặc định (`SC-FEED-008`)** | `D8.1` §D8.1 L360 |
| Thời gian đăng (trên card) | Runtime | timestamp lúc đăng tin | — | — (⛔ không assert giá trị tuyệt đối) | `DOC-v1.0-02` §3.3 đoạn 3 |
| Điểm Lấy hàng / Giao hàng | Fixture | địa chỉ văn phòng chọn từ dropdown autocomplete | text gõ tay không chọn gợi ý (không được lưu) | **2 địa chỉ trùng nhau → chặn khi đăng (`D8.1` "phải khác địa chỉ lấy hàng")** | `D8.1` §D8.1 L364/L369 · `DOC-v1.0-06` KP-01 §3 KB-ORD-06 |
| Khoảng cách "~X km" | Runtime | số ước tính **tĩnh** trong khung placeholder | — | — (⛔ không assert giá trị, không assert bản đồ thật) | `DOC-v1.0-02` §3.4 dòng "Lộ trình" · §7 dòng 10 |
| SĐT người gửi (Chi tiết tin) | Runtime | ⛔ **KHÔNG được hiển thị khi trạng thái = Chờ ghép** (`BR-CON-02`) | SĐT hiện sẵn + nút "Gọi" ở Chờ ghép → **bug** (`SC-FEED-010`) | **ranh giới Chờ ghép → Đã ghép: đúng thời điểm SĐT được phép lộ** | `BR-CON-02` §A5 L78 · `OPR-07` §D7 L343 |
| Khung giờ mong muốn | Fixture | khoảng giờ do người đăng chọn (≥30 phút) | — | **cách nhau đúng 30 phút (biên hợp lệ)** | `D8.1` §D8.1 L372 |

## Ghi chú chung
- **`Loại data`:** `Fixture` = QC tự tạo bằng cách đăng tin (module `ORD`) · `Master` = danh mục hệ thống (chip loại hàng/giá trị) · `Runtime` = sinh khi chạy (timestamp, khoảng cách, quyết định lộ SĐT).
- ⚠️ **Bẫy dữ liệu lớn nhất của cả dự án nằm ở dòng "Loại hàng":** tài liệu (`D8.1`) ghi danh mục `Tài liệu · Đồ điện tử · Thực phẩm · Quà tặng · Khác` (5 giá trị), PRD (`§3.5.1`) ghi 8 chip, còn **app STG có 8 chip và KHÔNG có chip nào tên "Tài liệu"** — mặc định là **`Giấy tờ, hồ sơ`** (`DOC-v1.0-06` KP-01 §10.2 `KB-VIBE-01`, có screenshot). Mọi TC đợt cũ nhắc "Tài liệu" đều **sai chữ**. ⛔ Dùng `Giấy tờ, hồ sơ` cho tới khi BA trả lời (`C-ORD-09`).
- **Bộ dữ liệu tối thiểu để chạy module:** 3 tài khoản (A chủ tin · B người xem · C người nhận được khai) + ≥2 tin NEED `POSTED` + 1 tin không ảnh + 1 tin không ghi chú + 1 tin OFFER (để verify **không** lên bảng tin).
- ⛔ **Không assert** giá trị `~X km`, thời gian đăng, và nội dung ảnh mặc định.
