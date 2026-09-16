---
id: v1.1/GIFT-qua-cam-on/risk
title: Risk Assessment — v1.1 · Module GIFT
type: risk-assessment
version: v1.1
sprint: 1
module: GIFT
counts:
  cl: 3
  risk: 6
  cl_open: 1
  cl_resolved: 2
status: ANALYZED
updated: 2026-09-16
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
| C-GIFT-02 | Nút back màn "Tặng quà" nhảy sang màn của đơn khác | 🔴 **Open — tái hiện với đơn thật 2026-09-16, ưu tiên cao hơn** | kế thừa 2026-07-29 | REQ-GIFT-006 |

### C-GIFT-03 · Text popup + danh sách lịch sử nhận quà *(RESOLVED 2026-09-15 — cả 2 vế)*

📍 `DOC-v1.1-01 §8.14.1 BR14-02 · trang 49` · `§6.2 AC-26.1.01 · trang 27`

> Vế (a) — `BR14-02`: "Gửi ngay, không cần bước xác nhận của người nhận quà; hiện popup "Cảm ơn của bạn đã được gửi"."

> Vế (b) — `AC-26.1.01`: "…card đếm quà theo từng loại, tổng 5, kèm lịch sử nhận quà."

↳ **Ghi chú:** CL mở 2026-09-07 với **hai câu hỏi trong một dòng** — PRD trả lời cả hai ở 2 chỗ khác nhau. Vế (a): chuỗi chính xác `"Cảm ơn của bạn đã được gửi"`, kèm chi tiết mới **có nút về trang chủ** (`AC-24.1.01`). Vế (b): **CÓ** danh sách lịch sử ⇒ `SC-GIFT-007` hết `[GAP]`, nâng P3 → P2. ⚠️ Rule *"loại `count = 0` không hiện card"* (`SC-GIFT-006`) **KHÔNG** nằm trong PRD — nó vẫn đứng trên quan sát app v1.0 (`KB-GIFT-03`); ghi rõ để người sau không tưởng rule đó cũng có nguồn tài liệu.

### C-GIFT-01 · Rating 1–5 sao *(RESOLVED 2026-09-15 — nâng cấp phán quyết)*

📍 `DOC-v1.1-01 §4 SCOPES dòng Out of Scope · trang 9` · `§8.14.1 BR14-03 · trang 49`

> "Đánh giá sao 1–5 và mọi hình thức xếp hạng/tier/điểm thưởng — thay bằng quà ảo"

> "BR14-03 | Không có chấm sao 1–5, không điểm, không tier/xếp hạng, không chỉ số môi trường."

↳ **Ghi chú:** Phán quyết v1.0 là *"Out of scope **v1.0**"* — hai chữ "v1.0" khiến mọi dấu vết sao trong app đọc được thành *"tính năng phase sau lộ sớm"*, tức **không phải bug**. PRD v1.1 đóng cửa hẳn: mục Out of Scope của **cả sản phẩm**, dùng chữ *"thay bằng"* (thay thế) chứ không phải "hoãn". ⇒ Mọi ★/điểm/tier/chỉ số môi trường còn sót lại **đều là defect**. `BR14-03` còn liệt kê thêm **"chỉ số môi trường"** — thứ v1.0 chưa nhắc nhưng đợt phân tích cũ từng thấy (`KP-04`: *"điểm/CO₂"*).

> ⚠️ `C-ORD-06` (text empty state) có **home canonical ở module `ACT`** — phần `EMP-08` thuộc `GIFT` chỉ **tham chiếu**, xem `v1.1/ACT-hoat-dong/risk_assessment.md`.

## Khuyến nghị tổng thể
1. **⛔ Không chạy `SC-GIFT-013`/`SC-GIFT-014` trước khi xác nhận nhánh `RETURNING → RETURNED` đã có trên STG** — cả 2 là vế phủ định, không có tiền đề thì PASS là PASS oan (`RISK-GIFT-06`). Gộp lô với `SC-DLV-053..056`.
2. **Chạy `SC-GIFT-014` cùng lượt với `SC-USR-005`/`SC-USR-012` và `SC-HOME-008`** — cùng một bộ đếm hiển thị ở 3 màn; dùng chung 1 đơn `RETURNED` để so 3 màn trong 1 lượt thay vì seed 3 lần (`RISK-GIFT-02`).
3. **`SC-ACT-013` (★ leftover) nay đủ căn cứ log bug** — `BR14-03` + §4 Out of Scope. ⛔ Không diễn giải là "dấu vết phase sau".
4. **3 SC hết `[GAP]` cần viết lại Then hẳn, không chỉ sửa chữ** (`SC-GIFT-007` · `SC-GIFT-008` · `SC-GIFT-011`) — từ *ghi nhận* sang *assert khẳng định*; `generate-tc` phải regenerate, ⛔ không patch TC cũ.
5. **`C-GIFT-02` vẫn Open, nay ưu tiên cao hơn** — vibe-check demo 2026-09-16 tái hiện được lỗi back-navigation với **đơn thật** (không chỉ item mẫu), loại bỏ giả thuyết "giới hạn demo". Cần verify khẩn trên STG thật trước `generate-tc`; xem chi tiết `v1.0/GIFT-qua-cam-on/risk_assessment.md`.
