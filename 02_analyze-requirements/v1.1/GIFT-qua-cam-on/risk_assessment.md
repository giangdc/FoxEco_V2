---
id: v1.1/GIFT-qua-cam-on/risk
title: Risk Assessment — v1.1 · Module GIFT
type: risk-assessment
version: v1.1
sprint: 1
module: GIFT
counts:
  cl: 4
  risk: 6
  cl_open: 0
  cl_resolved: 4
status: ANALYZED
updated: 2026-09-17
---

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (5 dòng, `RISK-GIFT-01..05`) xem `v1.0/GIFT-qua-cam-on/risk_assessment.md` — KHÔNG lặp lại ở đây. **ID mới bắt đầu từ `RISK-GIFT-06`.**

## Tổng quan
| Module | Risk Level | Rủi ro chính (delta v1.1) |
|--------|-----------|--------------|
| GIFT | **Low** (không đổi) | Module được PRD lấp gap dày nhất so với kích cỡ — 3 SC `[GAP]` hết gap cùng lúc. Rủi ro còn lại là **phụ thuộc ngoài**: 2 SC mới cần đơn ở `RETURNED`, mà nhánh hoàn hàng thuộc `DLV`/`FR09` có thể chưa build trên STG |

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-GIFT-06 | GIFT / Phụ thuộc nhánh hoàn hàng | **(risk mới)** `SC-GIFT-013`/`SC-GIFT-014` cần đơn kết thúc ở `RETURNED` — trạng thái **hoàn toàn mới ở v1.1**, do `FR09` của `DLV` sinh ra. Nếu app STG chưa build nhánh này thì **không seed được tiền đề**, và cái bẫy là 2 SC đều là **vế phủ định** ⇒ rất dễ bị đánh PASS oan (*"không thấy nút tặng quà"* — đúng, vì không có đơn `RETURNED` nào để mở) | Medium | `DOC-v1.1-01` §8.14 Pre-Conditions · §6.2 AC-24.2.01 · đối chiếu `v1.1/DLV-giao-nhan/risk_assessment.md RISK-DLV-08` (app có thể chưa build lại theo PRD) | `SC-GIFT-013`, `SC-GIFT-014` | ⛔ **Verdict đúng khi không seed được là `BLOCKED`, KHÔNG phải PASS.** Chạy sau khi `vibe-test` xác nhận nhánh `FR09` đã có trên STG; gộp lô với `SC-DLV-053..056` | Open | REQ-GIFT-009, SC-GIFT-013, SC-GIFT-014 |
| RISK-GIFT-02 | GIFT / Bộ đếm đóng góp | *(cập nhật Why)* Bộ đếm "Đơn đã giúp" nay có **rule loại trừ** (`BR14-04` — không tính `RETURNED`) và cùng một con số hiển thị ở **3 màn** (Trang cá nhân · card "Đóng góp của bạn" ở `HOME` · `USR`) ⇒ nguy cơ 3 màn tính theo 3 công thức | Medium | `DOC-v1.1-01` §8.14.1 BR14-04 · §6.2 AC-26.1.01 vs `v1.0` KB-GIFT-02 | `SC-GIFT-014` là ô phân định; cross-check `SC-USR-005`/`SC-USR-012` + `SC-HOME-008` | Khi generate TC, 3 SC ở 3 module phải dùng **cùng 1 đơn `RETURNED`** để so 3 màn trong 1 lượt | Open | REQ-GIFT-004, REQ-GIFT-009, SC-GIFT-014 |
| RISK-GIFT-05 | GIFT / Sao & xếp hạng | *(cập nhật Status)* v1.0 ghi nhận *"out of scope **v1.0**"* — để ngỏ khả năng có ở phase sau ⇒ ★ leftover trên card có thể bị bỏ qua như "dấu vết hợp lệ". PRD v1.1 đưa vào **Out of Scope của cả sản phẩm** (*"thay bằng quà ảo"*) | Low → **Resolved** | `DOC-v1.1-01` §4 SCOPES Out of Scope · §8.14.1 BR14-03 | `SC-GIFT-011` (assert-absent 4 bề mặt) | `SC-ACT-013` (★ leftover) nay là **defect xác nhận** — log bug, ⛔ không diễn giải là "phase sau" | **Resolved** | REQ-GIFT-005, SC-GIFT-011 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-GIFT-01 | Rating 1–5 sao (`RAT-01/02`) có thuộc v1.0? | ✅ **Resolved 2026-09-15 — nâng cấp: out of scope VĨNH VIỄN, không phải hoãn tới phase sau** | 2026-07-27 | REQ-GIFT-005 |
| C-GIFT-03 | Text popup sau khi gửi quà + có "danh sách lịch sử nhận quà" hay không | ✅ **Resolved 2026-09-15 — cả 2 vế** | 2026-09-07 | REQ-GIFT-002, REQ-GIFT-004 |
| C-GIFT-02 | Nút back màn "Tặng quà" nhảy sang màn của đơn khác | ✅ **Resolved 2026-09-16 — BA: lỗi của demo; quy tắc là back về màn hình trước đó** | kế thừa 2026-07-29 | REQ-GIFT-006, SC-GIFT-010 |
| C-GIFT-04 | Tặng quà: mỗi đơn mấy lần · bỏ qua rồi tặng lại sau được không / có hạn không · đã tặng thì mở đơn thấy gì · NTF-06 có dẫn thẳng tới màn Tặng quà | ✅ **Resolved 2026-09-17 (vòng 2) — BA trả lời đủ (1)(2)(3)(4), hết mâu thuẫn `C-ACT-01`** | 2026-09-16 | REQ-GIFT-001, REQ-GIFT-002, SC-GIFT-001, SC-GIFT-005 |

### C-GIFT-03 · Text popup + danh sách lịch sử nhận quà *(RESOLVED 2026-09-15 — cả 2 vế)*

📍 `DOC-v1.1-01 §8.14.1 BR14-02 · trang 49` · `§6.2 AC-26.1.01 · trang 27`

> Vế (a) — `BR14-02`: "Gửi ngay, không cần bước xác nhận của người nhận quà; hiện popup "Cảm ơn của bạn đã được gửi"."

> Vế (b) — `AC-26.1.01`: "…card đếm quà theo từng loại, tổng 5, kèm lịch sử nhận quà."

↳ **Ghi chú:** CL mở 2026-09-07 với **hai câu hỏi trong một dòng** — PRD trả lời cả hai ở 2 chỗ khác nhau. Vế (a): chuỗi chính xác `"Cảm ơn của bạn đã được gửi"`, kèm chi tiết mới **có nút về trang chủ** (`AC-24.1.01`). Vế (b): **CÓ** danh sách lịch sử ⇒ `SC-GIFT-007` hết `[GAP]`, nâng P3 → P2. ⚠️ Rule *"loại `count = 0` không hiện card"* (`SC-GIFT-006`) **KHÔNG** nằm trong PRD — nó vẫn đứng trên quan sát app v1.0 (`KB-GIFT-03`); ghi rõ để người sau không tưởng rule đó cũng có nguồn tài liệu.

### C-GIFT-01 · Rating 1–5 sao *(RESOLVED 2026-09-15 — nâng cấp phán quyết)*

📍 `DOC-v1.1-01 §4 SCOPES dòng Out of Scope · trang 9` · `§8.14.1 BR14-03 · trang 49`

> ↪ *Quote `Đánh giá sao 1–5 và mọi hình thức xếp…` — home ở `requirement_traceability.md` · `REQ-GIFT-005` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

> "BR14-03 | Không có chấm sao 1–5, không điểm, không tier/xếp hạng, không chỉ số môi trường."

↳ **Ghi chú:** Phán quyết v1.0 là *"Out of scope **v1.0**"* — hai chữ "v1.0" khiến mọi dấu vết sao trong app đọc được thành *"tính năng phase sau lộ sớm"*, tức **không phải bug**. PRD v1.1 đóng cửa hẳn: mục Out of Scope của **cả sản phẩm**, dùng chữ *"thay bằng"* (thay thế) chứ không phải "hoãn". ⇒ Mọi ★/điểm/tier/chỉ số môi trường còn sót lại **đều là defect**. `BR14-03` còn liệt kê thêm **"chỉ số môi trường"** — thứ v1.0 chưa nhắc nhưng đợt phân tích cũ từng thấy (`KP-04`: *"điểm/CO₂"*).

> ⚠️ `C-ORD-06` (text empty state) có **home canonical ở module `ACT`** — phần `EMP-08` thuộc `GIFT` chỉ **tham chiếu**, xem `v1.1/ACT-hoat-dong/risk_assessment.md`.

### C-GIFT-02 · ↳ BA trả lời 2026-09-16 *(→ RESOLVED)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `GIFT` · cột "Câu trả lời BA" · 2026-09-16

> "-> đây là demo lỗi thôi, quy tăc là back về màn hình trước đó"

↳ **Ghi chú:** Back nhảy sang đơn khác là **lỗi của demo**, không phải hành vi được chấp nhận. Rule: nút back (←) ở màn "Tặng quà" **quay về đúng màn đã mở nó** (vd tab "Đã hoàn thành" của Đơn của tôi — theo `C-ACT-01` BA vừa chốt; hoặc màn Theo dõi đơn). ⇒ `SC-GIFT-010` hết `[GAP·bug]` dạng chờ: Then assert back về màn trước đó; STG nhảy sang màn/đơn khác ⇒ **bug** (mức cao — có thể thao tác nhầm đơn khác). ⚠️ Ghi chú 2026-09-16 trước đó *"tái hiện với đơn thật"* là **trên demo** ⇒ không mâu thuẫn với câu trả lời BA.

### C-GIFT-04 · Vòng đời bước tặng quà *(RESOLVED 2026-09-17 — vòng 2)*

📍 `DOC-v1.1-01 §6.2 AC-24.1.01 · trang 26` · `§8.10 Post-Conditions · trang 43` · `§8.12.3 dòng COMPLETED · trang 46` ⟷ BA trả lời `C-ACT-01` 2026-09-16

> `AC-24.1.01`: "Quà được gửi ngay, không cần bước xác nhận của người nhận quà. Hiện popup "Cảm ơn của bạn đã được gửi" và nút về trang chủ."

> `§8.12.3`: "COMPLETED | Tặng quà cảm ơn | Xem quà đã nhận | Xem lịch sử"

↳ **Ghi chú:** BA vừa chốt *"hoàn thành **chưa tặng quà** thì ra màn Tặng quà"* ⇒ ngầm định có trạng thái **đã tặng / chưa tặng**. PRD không nói: (a) mỗi đơn tặng được **1 lần** hay nhiều lần? (b) Sender **bỏ qua** (thoát màn Tặng quà) thì vào lại tặng **sau** được không, **có thời hạn** không? (c) Đã tặng rồi thì mở đơn thấy gì — nút đổi nhãn (`SC-GIFT-005`, nguồn chỉ là `QA-obs` v1.0) thành chữ gì, có hiện **loại quà đã tặng** không? (d) Chạm `NTF-06` (*"Đơn đã hoàn tất"*) ở vai Sender có mở thẳng màn Tặng quà không?

### C-GIFT-04 · ↳ BA trả lời 2026-09-17 *(→ PARTIALLY RESOLVED — hỏi vòng 2)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `GIFT`

> "a. 1 lần rồi đóng ko cho tặng nữa
> b. không nhé
> c. "

↳ **Ghi chú:** (a) **Chốt:** mỗi đơn tặng quà **đúng 1 lần**, gửi xong **đóng**, không tặng lại ⇒ `SC-GIFT-005` (*nút disable, không gửi lại được*) nay có nguồn BA thay cho `QA-obs` — phần *"không gửi lại được"* assert cứng; **nhãn nút** (*"Bạn đã đánh giá"*) vẫn chỉ từ `QA-obs` v1.0 ⇒ chờ (c). (b) *"không nhé"* trả lời cho câu gộp *"vào lại tặng sau được không? Có thời hạn không?"* ⇒ **2 cách hiểu**: *không cho tặng sau* **hoặc** *không có thời hạn*. ⚠️ Nếu hiểu *không cho tặng sau* thì **mâu thuẫn** `C-ACT-01` (BA 2026-09-16: *"hoàn thành chưa tặng quà thì ra màn tặng quà"* — tức đơn Hoàn thành chưa tặng vẫn mở lại được màn Tặng quà). (c)(d) BA để trống. ⇒ **Hỏi vòng 2** (sheet `GIFT` dòng `C-GIFT-04 (vòng 2)`). `SC-GIFT-001` giữ nguyên (mở Tặng quà lần đầu).

### C-GIFT-04 · ↳ BA trả lời vòng 2, 2026-09-17 *(→ RESOLVED)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `GIFT` dòng `C-GIFT-04 (vòng 2)`

> "1. có nhé, không có thời hạn
> 2. Chỉ hiện bạn đã đánh giá thôi + disable (nếu chưa có UI thì vào tìm lại thông tin nhé )
> 3. Theo dõi đơn nhé, như
> 4. tặng quà nhé nếu chưa tặng, nếu đã tặng rồi thì ra màn hình theo dõi đơn"

↳ **KẾT LUẬN (theo BA) 2026-09-17:** (1) Sender thoát màn "Tặng quà" **KHÔNG gửi** rồi vào lại **SAU VẪN tặng được**, **KHÔNG có thời hạn** ⇒ **giải toả mâu thuẫn với `C-ACT-01`** — câu (b) ở lượt trả lời đầu ("không nhé") phải hiểu là *"không có thời hạn"*, KHÔNG phải *"không cho tặng sau"*; đơn Hoàn thành chưa tặng luôn mở lại được màn "Tặng quà" bất kể vào lại lúc nào — khớp `C-ACT-01`. "Đóng" ở câu (a) chỉ tính từ lúc **BẤM GỬI** tặng, không phải từ lúc thoát màn. (2) Sau khi đã tặng: nút đổi thành **"Bạn đã đánh giá"**, **DISABLE** (không bấm lại được) — BA chưa có ảnh UI đính kèm, sẽ bổ sung khi có (theo dõi ở `§3 Nợ đang mở`). (3) Tap card đơn Hoàn thành **ĐÃ** tặng quà (mọi vai) → mở màn **"Theo dõi đơn"** (không mở lại "Tặng quà") — khớp `C-ACT-03`. (4) Chạm `NTF-06` "Đơn đã hoàn tất" (vai Sender): **CHƯA** tặng → mở thẳng **"Tặng quà"**; **ĐÃ** tặng → mở **"Theo dõi đơn"**. `SC-GIFT-005` nay có nguồn BA đầy đủ cho cả 2 vế (không gửi lại được + nhãn nút "Bạn đã đánh giá" + disable); `SC-ACT-009/010` (tap card đã tặng) hết gap. Đã thử vibe-check demo 2026-09-17 để đối chứng trực quan nút "Bạn đã đánh giá" nhưng **KHÔNG tới được trạng thái "Hoàn thành"** — màn "Xác nhận đã giao" bắt buộc tối thiểu 1 "Ảnh bằng chứng" và ô tải ảnh trong bản demo này không mở được trình chọn file (không phản hồi thao tác click), chặn giữa luồng trước khi tới bước tặng quà. Không ảnh hưởng việc đóng CL vì đã có câu trả lời BA bằng lời cho cả 4 ý; ảnh UI "Bạn đã đánh giá" xin BA/QA bổ sung khi có STG thật.

↳ **Cập nhật 2026-09-17 (BA đính kèm ảnh mới):** `00_input/v1.1/design/gift_tang_qua_man_doncuatoi.png` — màn "Đơn của tôi" tab "Đã hoàn thành": card đơn ĐÃ tặng quà hiện badge nhỏ **"🎖 Đã tặng quà"** ngay trên card (không cần mở chi tiết); card đơn CHƯA tặng quà (vd "Gửi thuốc/y tế") hiện dòng gợi ý **"Chạm để tặng quà"**. ⚠️ Đây là UI ở **màn danh sách "Đơn của tôi"**, KHÁC với nút "Bạn đã đánh giá" (disable) được mô tả nằm **trong màn "Tặng quà"/chi tiết đơn** — 2 vị trí UI khác nhau cho cùng 1 trạng thái "đã tặng quà", cả hai đều cần assert riêng. Ảnh này bổ sung test data cho `SC-GIFT-001`/card list ở `ACT`/`HOME` ("Đơn đã giúp"), KHÔNG thay thế nợ ảnh nút "Bạn đã đánh giá" trong màn Tặng quà (vẫn còn treo, xem `CHANGELOG §3` nợ #4).

## Khuyến nghị tổng thể
1. **⛔ Không chạy `SC-GIFT-013`/`SC-GIFT-014` trước khi xác nhận nhánh `RETURNING → RETURNED` đã có trên STG** — cả 2 là vế phủ định, không có tiền đề thì PASS là PASS oan (`RISK-GIFT-06`). Gộp lô với `SC-DLV-053..056`.
2. **Chạy `SC-GIFT-014` cùng lượt với `SC-USR-005`/`SC-USR-012` và `SC-HOME-008`** — cùng một bộ đếm hiển thị ở 3 màn; dùng chung 1 đơn `RETURNED` để so 3 màn trong 1 lượt thay vì seed 3 lần (`RISK-GIFT-02`).
3. **`SC-ACT-013` (★ leftover) nay đủ căn cứ log bug** — `BR14-03` + §4 Out of Scope. ⛔ Không diễn giải là "dấu vết phase sau".
4. **3 SC hết `[GAP]` cần viết lại Then hẳn, không chỉ sửa chữ** (`SC-GIFT-007` · `SC-GIFT-008` · `SC-GIFT-011`) — từ *ghi nhận* sang *assert khẳng định*; `generate-tc` phải regenerate, ⛔ không patch TC cũ.
5. ✅ **`C-GIFT-02` Resolved 2026-09-16 (BA)** — back nhảy sai màn là **lỗi của demo**; rule: back về **màn hình trước đó**. `SC-GIFT-010` assert theo rule; STG còn nhảy sang đơn/màn khác ⇒ bug. Việc mới: `C-GIFT-04` (vòng đời bước tặng quà).
