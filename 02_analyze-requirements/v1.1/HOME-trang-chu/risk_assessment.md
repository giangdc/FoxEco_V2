---
id: v1.1/HOME-trang-chu/risk
title: Risk Assessment — v1.1 · Module HOME
type: risk-assessment
version: v1.1
sprint: 1
module: HOME
counts:
  cl: 6
  risk: 7
  cl_open: 0
  cl_resolved: 6
status: ANALYZED
updated: 2026-09-17
---

# Risk Assessment — v1.1 · Module HOME (DELTA)

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (5 dòng, không đổi trừ ghi chú dưới) xem `v1.0/HOME-trang-chu/risk_assessment.md` — KHÔNG lặp lại ở đây.

> ℹ️ `cl_open (0) + cl_resolved (6) = 6 = cl (6)` — **khớp, HOME hết điểm treo** (2026-09-17): `C-HOME-04` đóng ở **vòng 3** (BA: *"giữ nguyên nhé"*), `C-HOME-06` đóng ở **vòng 2** (Accepted theo đề nghị BA). *(Ghi chú cũ "2 CL Partially không thuộc 2 ô đó" hết hiệu lực.)*

## Tổng quan
| Module | Risk Level | Rủi ro chính (delta v1.1) |
|--------|-----------|--------------|
| HOME | **Medium** (không đổi so với v1.0) | 2 rủi ro lớn nhất của v1.0 đã **Resolved** (`RISK-HOME-01` mâu thuẫn 1-vs-5 tin → PRD chốt 5; `RISK-HOME-04` icon vai trò → QC xác nhận 1 icon chung), nhưng mở 2 rủi ro mới cùng loại "không kiểm được bằng manual": `RISK-HOME-06` NFR01 p95 < 2s cần load-test riêng · `RISK-HOME-07` 3 empty state cần tài khoản hoàn toàn trắng |

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
| C-HOME-04 | "Khu vực của người dùng" (lọc "Tin mới", empty state `EMP-01`) xác định bằng gì và so khớp thế nào | ✅ **Resolved 2026-09-17 (vòng 3)** — tin NEED load TOÀN QUỐC (không lọc khu vực), khu vực chỉ dùng khớp tuyến (`ASN`); chuỗi empty state `EMP-01`/`EMP-04` **giữ nguyên theo PRD** (BA) | 2026-09-16 | REQ-HOME-011, SC-HOME-019, SC-HOME-025, SC-FEED-013 |
| C-HOME-05 | Trang chủ khi không có đơn đang chạy: **ẩn** section "Đơn của tôi" (C-HOME-02, demo) hay **hiện empty state** `EMP-02` — `SC-HOME-010` ⟷ `SC-HOME-026` đang mâu thuẫn | ✅ **Resolved 2026-09-17 — HIỆN empty state `EMP-02`, không ẩn** (BA) ⇒ `SC-HOME-010` DEPRECATED | 2026-09-16 | REQ-HOME-005, REQ-HOME-012, SC-HOME-010, SC-HOME-026 |
| C-HOME-06 | Số liệu hero + cộng đồng ("N đơn đã giúp", "N đơn · M người"): phạm vi và công thức đếm | ✅ **Resolved 2026-09-17 (vòng 2) — Accepted**, BA đề nghị bỏ qua định nghĩa chi tiết "người tham gia" | 2026-09-16 | REQ-HOME-004, REQ-HOME-012, SC-HOME-008, SC-HOME-027, SC-HOME-029, SC-HOME-030 |

### C-HOME-02 · Section "Đơn của tôi" — ẩn theo điều kiện hay theo vai trò? *(RESOLVED 2026-09-15)*

⛔ **Cập nhật 2026-09-17 — vế *"ẩn section khi không có đơn"* HẾT HIỆU LỰC** (BA chốt `C-HOME-05`: **hiện empty state `EMP-02`**). Phần còn hiệu lực: nội dung section **không phụ thuộc vai trò** (nhãn vai `SC-HOME-011..013` vẫn đúng). Ảnh `HOME_03` (demo không có section) nay là **lệch demo ↔ rule**, không phải oracle.

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

### C-HOME-04 · "Khu vực của người dùng" *(RESOLVED 2026-09-17 — đóng ở vòng 3)*

📍 `DOC-v1.1-01 §6.2 AC-11.1.01 / AC-11.2.01 · trang 19-20` · `§5.1 Workflow "[BẢNG TIN]" · trang 10` · `§8.17.1 EMP-01 / EMP-04 · trang 51` ⟷ BA trả lời `C-USR-05(b)` 2026-09-16

> `AC-11.1.01`: "Given: Trong khu vực của người dùng có 12 tin NEED đang ở POSTED."

> `§5.1`: "[BẢNG TIN]   Hiển thị cho CBNV cùng khu vực / thuận tuyến"

> `EMP-04`: "Bảng tin (cả hai tab) | "Chưa có tin nào" + gợi ý mở rộng khu vực hoặc đăng tin"

↳ **Ghi chú:** "Khu vực" là **điều kiện lọc** của "Tin mới" và Bảng tin nhưng PRD **không định nghĩa** ở đâu (không có trong bảng thuật ngữ `§2.2`). BA vừa nói *"khu vực/văn phòng load theo địa chỉ mặc định"* — mà địa chỉ mặc định là **văn bản tự do** ⇒ không thể là khoá lọc tin cậy. **Hỏi:** (a) khu vực = **tỉnh/thành** (34 tỉnh — Executive Summary), **văn phòng** (từ HRIS), hay suy từ **địa chỉ mặc định**? (b) Tin NEED so khớp khu vực theo **điểm lấy**, **điểm giao** hay cả hai? (c) Người dùng **đổi/mở rộng** khu vực ở đâu (*"gợi ý mở rộng khu vực"*)? (d) Không có khu vực (hồ sơ trống) thì thấy tin toàn quốc? ⛔ Chưa chốt thì `SC-HOME-019`/`025` **không dựng được Given** ("12 tin trong khu vực").

### C-HOME-05 · Section "Đơn của tôi" khi trống — ẩn hay empty state? *(RESOLVED 2026-09-17)*

📍 `DOC-v1.1-01 §8.17.1 EMP-02 · trang 51` ⟷ `C-HOME-02` Resolved 2026-09-15 (ảnh `00_input/v1.1/design/HOME_03_trangchu_carrier_chuanhandon_khong-donmoitoi.png`)

> `EMP-02`: "Trang chủ — Đơn của tôi | "Bạn chưa có đơn nào đang chạy" | "Tạo đơn gửi hàng""

↳ **Ghi chú:** Phát hiện khi rà chéo 2 SC cùng module: `C-HOME-02` chốt (theo demo) section "Đơn của tôi" **ẩn hẳn** khi tài khoản không có đơn ⇒ `SC-HOME-010` assert *không có section*; trong khi `SC-HOME-026` (theo `EMP-02`) assert section **hiện empty state** kèm CTA "Tạo đơn gửi hàng". **Hai SC không thể cùng PASS.** Có thể phân biệt theo điều kiện (vd *chưa từng có đơn* ⟷ *có đơn nhưng đã đóng hết*) nhưng PRD không nói. **Hỏi BA:** khi không có đơn đang chạy thì Trang chủ **ẩn** section hay **hiện** `EMP-02`? Nếu tuỳ điều kiện thì điều kiện là gì? ⛔ Chưa chốt: cả 2 SC hạ xuống **ghi nhận**.

### C-HOME-06 · Số liệu hero & cộng đồng *(RESOLVED 2026-09-17 — vòng 2, Accepted; xem ↳ vòng 2 bên dưới)*

📍 `DOC-v1.1-01 §7.1 Sơ đồ "Hero "N đơn đã giúp" + số liệu cộng đồng" · trang 30` · `§6.2 AC-26.2.01 · trang 27` · `§8.17.1 EMP-03 · trang 51` · `§8.14.1 BR14-04 · trang 48`

> `AC-26.2.01`: "Trên trang chủ, hero hiện "0 · Chưa có đóng góp nào" và cụm cộng đồng hiện "0 đơn · 0 người" nếu hệ thống chưa có dữ liệu."

> ↪ *Quote `BR14-04` — home ở `../GIFT-qua-cam-on/test_scenario_map.md` (không chép lại — tránh lặp home, health-check G-03 2026-09-17)*

↳ **Ghi chú:** (a) Hero "N đơn đã giúp" của vai **Sender/Receiver** (không bao giờ "giúp") hiện gì — luôn 0? (b) Cụm cộng đồng **"N đơn · M người"**: N = số đơn **COMPLETED toàn hệ thống** hay trong **khu vực**? M = số **người đã giúp** (Carrier distinct) hay **mọi người tham gia**? Có tính đơn RETURNED? (c) Cập nhật **realtime** hay theo chu kỳ? ⛔ Không có công thức thì `SC-HOME-008`/`027` chỉ assert được ô = 0 với tài khoản trắng, không assert được số > 0.

### C-HOME-04 · ↳ BA trả lời 2026-09-17 *(→ PARTIALLY RESOLVED — hỏi vòng 2)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `HOME` · cột "Câu trả lời BA"

> "a. suy tu mặc định nhé
> b. cả 2
> c. hiện tại lấy theo data từ file, thêm thì dev bổ sung trong db thôi
> d. ụa tin là load toàn quốc mà, đâu load theo khu vực? Tìa liệu có mô tả à"

↳ **Ghi chú:** (a)(b)(c) mô tả **cách tính khu vực** (suy từ địa chỉ mặc định = văn phòng trong `location_address_catalog.xlsx`; so cả điểm lấy lẫn điểm giao; danh mục do dev thêm trong DB, người dùng không tự mở rộng). Nhưng (d) nói **tin load toàn quốc, không lọc theo khu vực** — và hỏi ngược tài liệu có mô tả không. ⇒ **Câu trả lời tự mâu thuẫn**: nếu không lọc thì (a)(b) dùng vào đâu? PRD **có** mô tả lọc theo khu vực ở 4 chỗ: `AC-11.1.01` *"Trong khu vực của người dùng có 12 tin NEED"*, `AC-11.2.01`/`EMP-01` *"Chưa có tin nào trong khu vực của bạn"*, `§5.1` *"Hiển thị cho CBNV cùng khu vực / thuận tuyến"*, `EMP-04` *"gợi ý mở rộng khu vực"*. ⇒ **Hỏi vòng 2** (xem sheet `HOME` dòng `C-HOME-04 (vòng 2)`). **Tạm thời:** `SC-HOME-019`/`025` và `SC-FEED-001`/`013` viết Given **toàn quốc** theo câu (d) — câu rõ ràng nhất; ⛔ chưa assert chữ *"trong khu vực của bạn"* và câu *"gợi ý mở rộng khu vực"* cho tới khi chốt.

### C-HOME-04 · ↳ BA trả lời vòng 2, 2026-09-17 *(→ PARTIALLY RESOLVED — còn 1 câu)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `HOME` dòng `C-HOME-04 (vòng 2)`

> "1. đúng
> 2. Chỉ dùng cho khớp tuyến
> 3.
> 4. mới nhất toàn quốc lên trước"

↳ **KẾT LUẬN (theo BA) 2026-09-17:** (1) XÁC NHẬN DỨT ĐIỂM — "Tin mới" ở Trang chủ/Bảng tin hiển thị tin NEED **TOÀN QUỐC**, **KHÔNG lọc theo khu vực** (thay thế mọi suy đoán trước đó, hết mâu thuẫn). (2) khái niệm "khu vực suy từ địa chỉ mặc định" (đã chốt ở vòng 1) **CHỈ dùng để khớp tuyến** (module `ASN`), **KHÔNG dùng để lọc** Tin mới/Bảng tin — vậy (a)(b) của vòng 1 vẫn đúng nhưng chỉ áp dụng cho `ASN`, không áp dụng cho `HOME`/`FEED`. (4) thứ tự tin: **MỚI NHẤT lên trước**, trên phạm vi toàn quốc. **CÒN TREO (3):** BA để trống câu "giữ chữ 'Chưa có tin nào trong khu vực của bạn' (`EMP-01`) không? 'Gợi ý mở rộng khu vực' (`EMP-04`) còn không, là nút hay chữ?" — vì đã xác định KHÔNG lọc khu vực, 2 câu chữ `EMP-01`/`EMP-04` gần như chắc chắn **không còn phù hợp** (PRD viết theo giả định có lọc khu vực) nhưng cần BA xác nhận dứt điểm chuỗi empty state thay thế trước khi viết TC cho `SC-HOME-019/025` nhánh 0 tin. `SC-HOME-019/025`, `SC-FEED-001/013` chốt Given **toàn quốc**, chữ empty state vẫn tạm ghi nhận chờ (3). *(→ câu (3) đã được BA trả lời ở **vòng 3** ngay dưới — rào "tạm ghi nhận" hết hiệu lực từ 2026-09-17.)*

### C-HOME-04 · ↳ BA trả lời vòng 3, 2026-09-17 *(→ RESOLVED — đóng hẳn)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `HOME` dòng `C-HOME-04 (vòng 3)` · QC GiangDC2 chuyển lời BA 2026-09-17

> "giữ nguyên nhé"

↳ **KẾT LUẬN (theo BA) 2026-09-17 — `C-HOME-04` ĐÓNG HẲN:** câu (3) duy nhất còn treo đã có trả lời — **GIỮ NGUYÊN chuỗi empty state đúng như PRD đang viết**: `EMP-01` giữ chữ *"Chưa có tin nào trong khu vực của bạn"* (Trang chủ — "Tin mới") và `EMP-04` giữ chữ *"Chưa có tin nào"* + *gợi ý mở rộng khu vực hoặc đăng tin* (Bảng tin). ⇒ `SC-HOME-025` và `SC-FEED-013` **assert cứng chuỗi theo PRD**, bỏ rào *"tạm ghi nhận chữ"*. ⚠️ **Mâu thuẫn copy ⟷ logic là CÓ CHỦ ĐÍCH, KHÔNG mở lại CL:** danh sách tin load **toàn quốc** (chốt vòng 2) nhưng chữ empty state vẫn nói *"trong khu vực của bạn"* / *"mở rộng khu vực"* — BA chọn giữ nguyên ⇒ đây là **quyết định thiết kế**, không phải defect; TC assert đúng chữ PRD, STG hiện chữ khác ⇒ FAIL (lệch tài liệu), **không** tự sửa oracle. ℹ️ PRD không nói *"gợi ý mở rộng khu vực"* là **nút hay chữ**, BA trả lời "giữ nguyên" nên không có thêm đặc tả ⇒ TC assert **nội dung chữ**, **ghi nhận** dạng hiển thị thực tế (nút / plain text) lúc chạy, không FAIL vì hình thức.

### C-HOME-05 · ↳ BA trả lời 2026-09-17 *(→ RESOLVED)*

> "hiện emp state chứ ko ẩn nhé"

↳ **Ghi chú:** Khi tài khoản **không có đơn đang chạy**, section "Đơn của tôi" **hiện empty state `EMP-02`** ("Bạn chưa có đơn nào đang chạy" + CTA "Tạo đơn gửi hàng"), **không ẩn**. ⇒ `SC-HOME-026` assert cứng; `SC-HOME-010` (v1.0 — *section không hiển thị*) **DEPRECATED**, thay bằng `SC-HOME-026` (cùng Given, Then ngược). Vế *"ẩn theo điều kiện"* của `C-HOME-02` hết hiệu lực — xem ghi chú đầu mục `C-HOME-02`. Demo (`HOME_03`) đang ẩn ⇒ STG ẩn là **defect**.

### C-HOME-06 · ↳ BA trả lời 2026-09-17 *(→ PARTIALLY RESOLVED — vòng 2 thấp)*

> "a. 0
> b. toàn hệ thống, người tham gia
> c. realtime"

↳ **Ghi chú:** (a) Tài khoản **chưa từng giúp đơn nào** (chỉ làm Người gửi/Người nhận) ⇒ hero **luôn 0** dù đã có đơn Hoàn thành ⇒ **+`SC-HOME-029`**. (b) Cụm cộng đồng: **N = đơn toàn hệ thống** (không lọc khu vực), **M = số người tham gia**. (c) **Realtime** ⇒ **+`SC-HOME-030`** (đơn Hoàn thành ⇒ N tăng 1 ngay khi mở lại Trang chủ). ⚠️ Còn mơ hồ, hỏi vòng 2 (thấp, không chặn): *"người tham gia"* = người **distinct** xuất hiện trong đơn Hoàn thành ở **cả 3 vai**, chỉ Người vận chuyển, hay mọi CBNV đã dùng app? N có tính đơn **Đã trả người gửi** (`BR14-04` loại khỏi *"đơn đã giúp"* cá nhân — cộng đồng có áp giống)? ⇒ `SC-HOME-030` chỉ assert **N**, ⛔ không assert M.

### C-HOME-06 · ↳ BA trả lời vòng 2, 2026-09-17 *(→ RESOLVED — Accepted)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `HOME` dòng `C-HOME-06 (vòng 2)`

> "cái này bỏ qua được không, chưa có đặc tả cụ thẻ ? Ver này đâu có update gì chỗ này"

↳ **KẾT LUẬN 2026-09-17:** BA đề nghị **BỎ QUA** câu hỏi vòng 2 — không có đặc tả cụ thể cho "người tham gia", và v1.1 không cập nhật gì ở phần này. **CHẤP NHẬN theo đề nghị BA (Accepted/Deferred):** giữ nguyên hiểu biết đã có (a) hero tài khoản chưa từng giúp = 0 (b) N = đơn toàn hệ thống, M = người tham gia (chưa định nghĩa chi tiết) (c) realtime. `SC-HOME-008/030` giữ nguyên mức assert hiện có (không assert giá trị chính xác của M) — đây là **giới hạn đã biết, chấp nhận được**, không phải gap còn chờ trả lời. `C-HOME-06` ĐÓNG.

## Khuyến nghị tổng thể
1. **`C-HOME-03` không còn là blocker** — `SC-HOME-019`/`SC-HOME-021` có thể viết TC assert số cứng (5 tin) thay vì ghi nhận.
2. **`C-HOME-02` không còn là blocker** — `SC-HOME-009`/`SC-HOME-012` assert cứng. ⛔ *(2026-09-17)* `SC-HOME-010` DEPRECATED theo `C-HOME-05` — khi không có đơn thì assert `SC-HOME-026` (empty state).
3. **Trước generate-tc:** chuẩn bị ≥1 tài khoản "sạch" (0 lịch sử) cho 3 SC empty state (`SC-HOME-025/026/027`) — xem `test_data_catalog.md`.
4. **`RISK-HOME-06`** (perf NFR01) không đưa vào TC manual — chuyển thẳng cho `execute-maintain`/automation khi có môi trường load-test.
5. **`C-HOME-01` không còn là blocker** — (b) tagline dùng text PRD "Tiện đường — Giúp đồng nghiệp"; (a) icon vai trò đã có xác nhận QC (1 icon chung, không phân biệt vai trò) — `SC-HOME-004` có thể viết TC assert cứng thay vì dạng GAP/ghi nhận.
6. ✅ **`C-HOME-05` Resolved 2026-09-17** — hết mâu thuẫn `SC-HOME-010` ⟷ `026`: hiện empty state.
7. ✅ **`HOME` HẾT điểm hỏi BA (2026-09-17)** — `C-HOME-04` đóng ở vòng 3 (Given **toàn quốc** + chuỗi empty state **giữ nguyên chữ PRD**), `C-HOME-06` đóng ở vòng 2 (Accepted — không assert `M` "người tham gia"). `generate-tc` chạy được cho **toàn bộ 28 SC còn hiệu lực**, kể cả nhánh 0 tin của `SC-HOME-019/025`.
