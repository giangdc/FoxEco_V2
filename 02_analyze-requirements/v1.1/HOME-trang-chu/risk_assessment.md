# Risk Assessment — v1.1 · Module HOME (DELTA)

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (5 dòng, không đổi trừ ghi chú dưới) xem `v1.0/HOME-trang-chu/risk_assessment.md` — KHÔNG lặp lại ở đây.

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-HOME-01 | HOME / Section "Tin mới" | *(cập nhật Status)* Mâu thuẫn **1 vs 5** tin giữa PRD-demo cũ và BRD — PRD chính thức v1.1 xác nhận **5**, kèm 3 điều kiện lọc (MATCHED/EXPIRED/của chính mình) trước đây không ai đặc tả | High → **Resolved** | `DOC-v1.1-01` §6.2 AC-11.1.01 (trang 19) | `SC-HOME-019` assert đúng 5 tin + 3 lớp lọc | Đã Resolved qua PRD v1.1 — `C-HOME-03` đóng, ghi ràng buộc `CHANGELOG §2` | **Resolved** | REQ-HOME-011, SC-HOME-019, SC-HOME-021 |
| RISK-HOME-04 | HOME / Header | *(cập nhật Status)* "Icon vai trò" có trong doc nhưng không có mapping icon↔vai — trước đây phải ghi nhận dạng GAP, không dám assert | Low → **Resolved** | Xác nhận trực tiếp từ QC GiangDC2, 2026-09-15 | `SC-HOME-004` assert cứng 1 icon chung | QC xác nhận: **chỉ 1 icon dùng chung cho cả 3 vai trò**, không có mapping icon↔vai — `KP-05 §3 dòng 5` (quan sát cũ) sai | **Resolved** | REQ-HOME-002, SC-HOME-004 |
| RISK-HOME-06 | HOME / Hiệu năng | **(risk mới)** NFR01 (< 2 giây p95, 1.000 user đồng thời) không kiểm chứng được bằng manual/vibe-test — cần môi trường load-test riêng, chưa có lịch | Medium | `DOC-v1.1-01` §9 NFR01 | `SC-HOME-028` (ghi nhận yêu cầu, defer automation) | Giao cho automation/load-test trước go-live; TC manual chỉ ghi nhận yêu cầu, không assert số đo | Open (non-blocking, cần môi trường) | REQ-HOME-013, SC-HOME-028 |
| RISK-HOME-07 | HOME / Empty state | **(risk mới)** 3 empty state mới (`EMP-01/02/03`) phụ thuộc dữ liệu tài khoản **hoàn toàn trống** (0 đơn, 0 đóng góp cộng đồng) — khó seed trên STG nếu account dùng chung đã có lịch sử | Low | `DOC-v1.1-01` §8.17.1 | `SC-HOME-025/026/027` | Cần tài khoản mới tinh (chưa từng đăng/giao đơn) cho 3 SC này; ghi ở `test_data_catalog.md` | Open (non-blocking) | REQ-HOME-012, SC-HOME-025, SC-HOME-026, SC-HOME-027 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-HOME-03 | Section "Tin mới" hiển thị **1 tin** hay **5 tin**? | ✅ **Resolved 2026-09-15** | kế thừa `KP-05 §2.1` (2026-07) | REQ-HOME-011, SC-HOME-019 |
| C-HOME-02 | Section "Đơn của tôi" ẩn theo **điều kiện có đơn** hay theo **vai trò**? | ✅ **Resolved 2026-09-15** (qua app thật, không cần BA) | kế thừa từ v1.0 (mở 2026-09-07) | REQ-HOME-005 |
| C-HOME-01 | Icon vai trò ở header (mapping) + lệch tagline banner giữa 2 doc | ✅ **Resolved 2026-09-15** (cả (a) và (b)) | kế thừa từ v1.0 (mở 2026-09-07) | REQ-HOME-002, REQ-HOME-003 |

### C-HOME-02 · Section "Đơn của tôi" — ẩn theo điều kiện hay theo vai trò? *(RESOLVED 2026-09-15)*

**Home canonical gốc:** `v1.0/HOME-trang-chu/risk_assessment.md` (giữ nguyên làm hồ sơ lịch sử — mục này ghi bước RESOLVE, không sửa file v1.0).

**Bằng chứng mới (app thật, qua demo `https://giangdc.github.io/foxeco_demo/FoxEcoQC` — dùng thay Figma cho v1.1 theo chỉ đạo QC 2026-09-15):**
> Ảnh `00_input/v1.1/design/HOME_03_trangchu_carrier_chuanhandon_khong-donmoitoi.png` — vai Carrier, **chưa nhận đơn nào** (trạng thái "Chờ ghép", chưa bấm "Nhận mang giúp đơn này") → Trang chủ **KHÔNG có section "Đơn của tôi"**, nhảy thẳng từ card "Đóng góp của bạn" xuống "Tin mới".
> Ảnh `00_input/v1.1/design/HOME_04_trangchu_carrier_codondaghep_donctoi_hien_CHOME02.png` — cùng vai Carrier, **sau khi** bấm "Nhận mang giúp đơn này" → xác nhận (đơn chuyển "Đã ghép") → Trang chủ **CÓ section "Đơn của tôi"**, nhãn **"Giao:"**.

**Source Location:** ảnh chụp trực tiếp app demo, 2026-09-15 (không phải trích văn bản doc).

**Analyst Note:** Đây chính xác là phép thử mà `v1.0/HOME-trang-chu/risk_assessment.md` §Khuyến nghị #2 đã chỉ ra: *"`SC-HOME-012` (nhãn 'Giao:' của Carrier) chính là ô phân định; chạy nó trước sẽ trả lời được CL này mà không cần BA."* Đã chạy đúng ô phân định đó (Carrier ĐANG có đơn) — kết quả xác nhận **Nguồn A/B đúng (ẩn theo điều kiện có đơn)**, **Nguồn C sai (KHÔNG phải ẩn theo vai trò)**. `KP-05 §3 #3` (quan sát cũ cho rằng Carrier không bao giờ thấy section này) bị bác bỏ bởi hành vi app thật. **RESOLVE theo app thật** — `SC-HOME-009`/`SC-HOME-010`/`SC-HOME-012` có thể assert cứng theo điều kiện có đơn, không cần rào "ghi nhận, không assert" nữa.

⚠️ Vẫn khuyến nghị double-check nhanh trên STG thật (không chỉ demo) trước khi hardening automation locator, vì demo lịch sử được đánh dấu "reference-only" ở v1.0 — nhưng với mức độ rõ ràng của bằng chứng này (2 ảnh đối chứng trực tiếp, đúng kịch bản phân định), **không coi là blocker** cho `generate-tc`.

### C-HOME-01 · Icon vai trò header + tagline banner *(RESOLVED 2026-09-15)*

**Home canonical gốc:** `v1.0/HOME-trang-chu/risk_assessment.md` (giữ nguyên làm hồ sơ lịch sử).

**(b) Tagline:**
> Ảnh `00_input/v1.1/design/HOME_01_trangchu_sender_default.png`, `HOME_02_trangchu_receiver_tinmoi.png`, `HOME_04_trangchu_carrier_codondaghep_donctoi_hien_CHOME02.png` — cả 3 vai trò đều hiển thị banner *"Tiện đường — Giúp đồng nghiệp"*, khớp nguyên văn `DOC-v1.0-02 §2` (PRD), KHÔNG khớp `DOC-v1.0-01 §A3 L29` ("Đồng nghiệp giúp nhau", BRD). **Chốt dùng bản PRD** — nhất quán với nguyên tắc "PRD thắng khi mô tả chi tiết màn hình" (`MASTER-MEMORY §2`).

**(a) Icon mapping theo vai trò:**
↳ **Ghi chú (2026-09-15):** Lượt trước có thử chụp icon header trên demo nhưng bị bác bỏ vì nhầm với panel điều khiển demo (không phải UI thật). Sau đó **QC GiangDC2 xác nhận trực tiếp** (không qua demo, dựa trên hiểu biết thật về app): **chỉ có 1 icon dùng chung cho cả 3 vai trò, KHÔNG phân biệt Sender/Carrier/Receiver** — tức `DOC-v1.0-06 KP-05 §3 dòng 5` (quan sát cũ cho rằng "icon khác nhau theo vai") là **sai/lỗi thời**. `C-HOME-01(a)` **RESOLVE theo xác nhận QC** — không cần hỏi BA nữa. `SC-HOME-004` chuyển từ dạng ghi nhận (GAP) sang assert cứng: **1 icon chung cho mọi vai trò**, không có mapping icon↔vai.

> ⚠️ `RISK-HOME-06` (NFR01) và `RISK-HOME-07` (empty state) không đổi — xem bảng risk phía trên.

### C-HOME-03 · Section "Tin mới" — 1 tin hay 5 tin? *(RESOLVED)*

📍 `DOC-v1.1-01 §6.2 AC-11.1.01 · trang 19`

> "Given: Trong khu vực của người dùng có 12 tin NEED đang ở POSTED. When: Mở trang chủ. Then: Khối 'Tin mới' hiển thị đúng 5 tin mới nhất..."

↳ **Ghi chú:** PRD chính thức `DOC-v1.1-01` — độc lập với cả PRD-demo cũ (`DOC-v1.0-02` §3.1, "1 tin") lẫn BRD (`DOC-v1.0-01 US-D06`, "5 tin") — xác nhận **5 tin**, đồng thời bổ sung 3 điều kiện lọc (MATCHED/EXPIRED/của chính mình) mà không nguồn v1.0 nào có. **Resolved theo PRD v1.1, thắng cả 2 nguồn cũ theo thứ tự ưu tiên `MASTER-MEMORY §2`.**

## Khuyến nghị tổng thể
1. **`C-HOME-03` không còn là blocker** — `SC-HOME-019`/`SC-HOME-021` có thể viết TC assert số cứng (5 tin) thay vì ghi nhận.
2. **`C-HOME-02` không còn là blocker** — `SC-HOME-009`/`SC-HOME-010`/`SC-HOME-012` có thể assert cứng theo điều kiện có đơn (xem bằng chứng ảnh ở mục CL trên).
3. **Trước generate-tc:** chuẩn bị ≥1 tài khoản "sạch" (0 lịch sử) cho 3 SC empty state (`SC-HOME-025/026/027`) — xem `test_data_catalog.md`.
4. **`RISK-HOME-06`** (perf NFR01) không đưa vào TC manual — chuyển thẳng cho `execute-maintain`/automation khi có môi trường load-test.
5. **`C-HOME-01` không còn là blocker** — (b) tagline dùng text PRD "Tiện đường — Giúp đồng nghiệp"; (a) icon vai trò đã có xác nhận QC (1 icon chung, không phân biệt vai trò) — `SC-HOME-004` có thể viết TC assert cứng thay vì dạng GAP/ghi nhận.
