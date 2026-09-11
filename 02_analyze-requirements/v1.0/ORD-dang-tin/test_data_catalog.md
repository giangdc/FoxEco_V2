# Test Data Catalog — v1.0 · Module ORD

> Tạo bởi: analyze-requirements (**stage: analyze** — sinh sớm để generate-tc dùng cho EP/BVA).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.
> ⚠️ Đây là catalog **dày nhất dự án** — 2 form (NEED wizard 3 bước + OFFER 1 trang) với 14 + 8 trường.

## Module ORD — Đăng tin NEED (wizard 3 bước) · `DOC-v1.0-01 §D8.1`

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Loại hàng | Master | 1 trong **8 chip app STG**, mặc định **`Giấy tờ, hồ sơ`** | ⛔ **`Tài liệu`** — nhãn của tài liệu, KHÔNG tồn tại trên app | **không tái hiện được trạng thái "chưa chọn"** (chip không deselect) | `D8.1` L357 · `DOC-v1.0-06` KP-01 §10.2/§10.3 |
| Ghi chú | Fixture | text ≤ 300 ký tự · rỗng (tuỳ chọn) | > 300 ký tự | **300 (hợp lệ), 301 (chặn)** · **rỗng (hợp lệ)** | `D8.1` L358 |
| Giá trị hàng | Master | `Thấp` / `Vừa` / `Cao` | rỗng (→ nút "Tiếp theo" disabled) | **`Cao` → banner cảnh báo** · **rỗng → chặn bước** | `D8.1` L359 · KP-01 §3 KB-ORD-05 · §10.4 |
| Ảnh sản phẩm | Fixture | 1 ảnh JPG/PNG ≤ 5MB · rỗng (tuỳ chọn) | > 5MB · định dạng ≠ JPG/PNG · ảnh thứ 2 | **đúng 5MB (hợp lệ), 5MB+1B (chặn)** · **0 ảnh (hợp lệ)** · **2 ảnh (chặn)** | `D8.1` L360 |
| Tên người gửi | Master | pre-fill từ hồ sơ, **chỉ đọc** | ⚠ app cho sửa và **xoá trắng khi chạm** → bug (`SC-ORD-015`) | **sau khi bị xoá trắng: không tự phục hồi trong cùng phiên** | `D8.1` L362 · KP-01 §10.5 |
| SĐT người gửi | Master | pre-fill từ tài khoản, SĐT VN hợp lệ | ⚠ **tự đổi giá trị giữa phiên** (`0000142378` → `0964633313`) → nghi vấn bug | — | `D8.1` L363 · KP-01 §10.10 |
| Địa chỉ lấy hàng | Master | pre-fill nơi làm việc (spec: `Tòa nhà Lô B3, KCX Tân Thuận, Q.7`), ≤ 200 ký tự | rỗng khi submit (→ chặn) · ⚠ app **không pre-fill** → gap (`SC-ORD-016`) | **200 ký tự (hợp lệ), 201 (chặn)** · **hồ sơ chưa có nơi làm việc → chưa rõ** | `D8.1` L364 · KP-01 §10.6 |
| Email công ty người nhận | Fixture | email đúng định dạng + tên miền nội bộ **tồn tại trong danh bạ** (STG: `stag_anhdc4@fpt.com`) | sai định dạng (thiếu `@`) · ngoài tên miền nội bộ · rỗng | **đúng định dạng nội bộ nhưng KHÔNG có trong danh bạ → thông báo "Không tìm thấy · nhập thủ công"** | `D8.1` L366 · `US-D18` L168 · KP-01 §10.8 |
| Tên người nhận | Runtime→Fixture | auto-fill từ danh bạ; hoặc nhập tay 2–60 ký tự | rỗng · 1 ký tự · 61 ký tự | **2 (hợp lệ), 1 (chặn), 60 (hợp lệ), 61 (chặn)** | `D8.1` L367 |
| SĐT người nhận | Runtime→Fixture | 10 số, bắt đầu bằng `0` | 9 số · 11 số · không bắt đầu `0` · có chữ · rỗng · ⚠ `0000286248` (do app auto-fill) bị app tự báo không hợp lệ | **10 số (hợp lệ), 9 và 11 (chặn)** | `D8.1` L368 · KP-01 §10.9 |
| Địa chỉ giao hàng | Fixture | chọn từ dropdown autocomplete, **khác** địa chỉ lấy hàng | rỗng · **trùng địa chỉ lấy hàng** (→ chặn) · gõ text mà không chạm chọn gợi ý (→ không lưu) | **trùng đúng địa chỉ lấy hàng (chặn)** | `D8.1` L369 · KP-01 §3 KB-ORD-06 |
| Từ ngày | Fixture | hôm nay (default) hoặc ngày tương lai | ngày quá khứ | **hôm nay (hợp lệ)** · **hôm qua (chặn)** | `D8.1` L370 |
| Đến ngày | Fixture | ≥ Từ ngày | < Từ ngày | **= Từ ngày (hợp lệ)** · **Từ ngày − 1 (chặn)** · **đã trôi qua → tin `EXPIRED`** | `D8.1` L371 · `US-D04` L166 |
| Khung giờ (từ – đến) | Fixture | đến > từ, cách **≥ 30 phút**; ⛔ **chọn TƯƠNG ĐỐI so với "now"** | đến ≤ từ · cách < 30 phút · khung giờ đã trôi qua (→ "phải muộn hơn hiện tại") | **đúng 30 phút (hợp lệ), 29 phút (chặn)** | `D8.1` L372 · KP-01 §10.11 |
| Xác nhận điều khoản | Fixture | đã tick → nút "Đăng tin ngay" bật | **chưa tick → chặn đăng** | **mặc định = CHƯA tick** (BRD+app) ⟷ PRD ghi "tick sẵn" → `C-ORD-12` | `D8.1` L373 · `ORD-09` L245 · KP-01 §10.7 |

## Module ORD — Đăng tin OFFER (form 1 trang) · `DOC-v1.0-01 §D8.2`

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Tên người giao | Master | pre-fill từ tài khoản, chỉ đọc | — | — | `D8.2` L379 |
| SĐT người giao | Master | pre-fill, SĐT VN hợp lệ | — | — | `D8.2` L380 |
| Điểm xuất phát (A) | Master→Fixture | pre-fill nơi làm việc, ≤ 200 ký tự, **user sửa được** | rỗng khi submit | **200 (hợp lệ), 201 (chặn)** · **hệ thống chưa có thông tin → spec CHO PHÉP để trống ban đầu** | `D8.2` L381 |
| Điểm đến (B) | Fixture | địa chỉ khác Điểm xuất phát | rỗng · **trùng Điểm xuất phát** (→ chặn) | **trùng đúng Điểm xuất phát (chặn)** | `D8.2` L382 |
| Từ ngày / Đến ngày | Fixture | như luồng NEED (default hôm nay, Đến ≥ Từ, không quá khứ) | ngày quá khứ · Đến < Từ | **= nhau (hợp lệ)** | `D8.2` L383-384 |
| Thời gian di chuyển | Fixture | đến > từ, cách ≥ 30 phút (default spec `17:30 – 18:30`) | cách < 30 phút · đến ≤ từ | **đúng 30 phút (hợp lệ), 29 (chặn)** | `D8.2` L385 |
| Xác nhận điều khoản | Fixture | đã tick → nút đăng bật | chưa tick → chặn | **mặc định = chưa tick** | `D8.2` L386 |

## Ghi chú chung
- **`Loại data`:** `Master` = từ hồ sơ nhân viên / danh mục hệ thống (⛔ QC không seed được, xác nhận giá trị thật ở vibe-test) · `Fixture` = QC tự nhập/tạo · `Runtime` = app tự sinh (auto-fill từ danh bạ → sau đó QC có thể sửa nên ghi `Runtime→Fixture`).
- ⭐ **Hai bẫy dữ liệu quan trọng nhất của cả dự án nằm ở module này:**
  1. **Chip "Loại hàng":** BRD ghi 5 giá trị (có `Tài liệu`), PRD ghi 8 chip (có `Tài liệu`), **app STG có 8 chip và KHÔNG có chip nào tên `Tài liệu`** — mặc định là **`Giấy tờ, hồ sơ`** (`KP-01` §10.2, có screenshot VR-002 `TC_04.5` FAIL). Mọi TC đợt cũ nhắc "Tài liệu" đều **sai chữ**. ⛔ Dùng nhãn app cho tới khi BA trả lời `C-ORD-09`.
  2. **Khung giờ:** ⛔ **KHÔNG hardcode giờ**. App validate theo **đồng hồ thật**, giá trị mặc định hết hạn nếu form mở lâu (~15 phút) và app tự bật *"phải muộn hơn hiện tại"* (`KP-01` §10.11). Ba nguồn còn cho 3 giá trị mặc định khác nhau (`17:00–18:30` BRD · `05:00 PM–06:30 PM` PRD · `11:10–11:40` app) ⇒ ⛔ không assert mặc định cứng.
- **Địa chỉ (cả NEED và OFFER) là `Fixture` nhưng phải chạm chọn gợi ý mới lưu** (`KB-ORD-06`) ⇒ với automation: `set text` đơn thuần **không lưu giá trị**, phải tap suggestion; dropdown gợi ý *"không expose locator phân biệt"* nên có thể phải tap theo toạ độ (`KP-01` §10.12).
- **Bộ dữ liệu tối thiểu để chạy module:** 1 tài khoản có hồ sơ đầy đủ (tên + SĐT + nơi làm việc) · 1 email nội bộ **có** trong danh bạ · 1 email nội bộ **không** có trong danh bạ · 1 ảnh JPG ≤5MB + 1 ảnh >5MB + 1 file không phải ảnh · 1 tin có "Đến ngày" đã trôi qua (cho `SC-ORD-045` — **khó seed**, nhờ dev).
