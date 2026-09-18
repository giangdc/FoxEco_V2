---
id: v1.1/GIFT-qua-cam-on/scenario-map
title: Test Scenario Map — v1.1 · Module GIFT
type: scenario-map
version: v1.1
sprint: 1
module: GIFT
counts:
  req: 9
  sc: 14
  new: 2
  modified: 6
  carried: 6
  deprecated: 0
  p1: 0
  p2: 9
  p3: 5
status: ANALYZED
updated: 2026-09-17
---

# Test Scenario Map — v1.1 · Module GIFT

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module GIFT **tính tới v1.1** (bao gồm CARRIED từ v1.0).
> Parent: `v1.0/GIFT-qua-cam-on/` — 6 SC không đổi (CARRIED), 6 SC MODIFIED (giữ ID v1.0), 2 SC NEW.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Delta lần này fan-out theo: 2 vế phủ định độc lập của trạng thái `RETURNED` (bề mặt ⟷ số liệu) · mỗi chuỗi text chính thức mới = 1 assert siết vào SC sẵn có, ⛔ không tách SC mới chỉ vì có thêm chữ.
> Trần: bộ đếm "Đơn đã giúp" còn hiện ở `USR` và `HOME` — ⛔ không nhân bản SC, chỉ cross-ref.

## Tổng quan
- Tổng số scenarios (tính tới v1.1): **14** (NEW: 2, MODIFIED: 6, CARRIED: 6)
- Phân bổ priority: P1: 0 | P2: 9 | P3: 5
- Delta lớn nhất: **3 SC dạng `[GAP]` của v1.0 hết gap cùng lúc** (`SC-GIFT-007` · `SC-GIFT-008` · `SC-GIFT-011`) nhờ `AC-26.1.01` + `EMP-08` + `BR14-03` — module này là nơi PRD lấp gap dày nhất so với kích cỡ.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### GIFT — Quà cảm ơn (delta v1.1)

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-GIFT-013 | Đơn RETURNED không mở bước tặng quà | REQ-GIFT-009 | DOC-v1.1-01 §8.14 Pre-Conditions · §6.2 AC-24.2.01 | Đơn kết thúc ở trạng thái `RETURNED` (đã đi hết nhánh hoàn hàng `FR09`) | Người gửi mở đơn đó từ "Đơn của tôi" | **KHÔNG** có nút tặng quà ở bất kỳ đâu trên màn; đơn hiển thị **lý do hoàn hàng** và vẫn nằm trong lịch sử đơn | P2 | Business Rule | NEW |
| SC-GIFT-014 | Đơn RETURNED không cộng vào "Đơn đã giúp" | REQ-GIFT-009 | DOC-v1.1-01 §8.14.1 BR14-04 · §6.2 AC-24.2.01 · AC-26.1.01 | Người vận chuyển có **N** đơn `COMPLETED` (ghi lại số trước) và vừa có thêm **1** đơn kết thúc `RETURNED` | Mở Trang cá nhân, đọc chỉ số "Đơn đã giúp" | Chỉ số vẫn là **N**, ⛔ không phải N+1 — đơn `RETURNED` không được tính | P2 | Business Rule | NEW |
| SC-GIFT-002 | Đúng 4 loại quà, đúng tên chính thức | REQ-GIFT-001 | DOC-v1.1-01 §8.14.1 BR14-01 | Đơn vừa chuyển `COMPLETED`, người gửi đang ở màn Tặng quà | Đọc danh sách quà hiển thị | Đúng **4** loại và đúng **tên**: bông hoa · ly cà phê · gấu bông · vương miện. ⛔ Không assert bằng số lượng đơn thuần | P2 | Functional | MODIFIED |
| SC-GIFT-003 | Gửi quà → popup đúng text chính thức | REQ-GIFT-002 | DOC-v1.1-01 §8.14.1 BR14-02 · §6.2 AC-24.1.01 | Đang ở màn Tặng quà của 1 đơn `COMPLETED` | Chọn 1 loại quà và bấm gửi | Quà gửi **ngay**, không có bước xác nhận của người nhận quà; popup hiện **đúng chuỗi** "Cảm ơn của bạn đã được gửi" **và có nút về trang chủ** | P2 | Functional | MODIFIED |
| SC-GIFT-006 | Card đếm quà theo từng loại + tổng đúng | REQ-GIFT-004 | DOC-v1.1-01 §6.2 AC-26.1.01 | Người vận chuyển đã nhận **5** quà gồm ít nhất 2 loại khác nhau | Mở Trang cá nhân → màn "Quà đã nhận" | Card đếm hiển thị **theo từng loại**, tổng = **5**; loại có `count = 0` không hiện card | P2 | Functional | MODIFIED |
| SC-GIFT-007 | Danh sách lịch sử nhận quà *(hết gap)* | REQ-GIFT-004 | DOC-v1.1-01 §6.2 AC-26.1.01 | Người vận chuyển đã nhận ≥ 2 quà ở các thời điểm khác nhau | Mở màn "Quà đã nhận", cuộn hết màn | **CÓ** danh sách lịch sử nhận quà (không chỉ card đếm) — `AC-26.1.01`: *"kèm lịch sử nhận quà"* | P2 | Functional | MODIFIED |
| SC-GIFT-008 | Empty state "Quà đã nhận" đúng text *(hết gap)* | REQ-GIFT-007 | DOC-v1.1-01 §8.17.1 EMP-08 · §6.2 AC-26.2.01 | Tài khoản **chưa từng nhận quà nào** | Mở Trang cá nhân → màn "Quà đã nhận" | Hiện **đúng chuỗi** "Chưa nhận được quà nào"; thống kê hiện **0 đơn đã giúp / 0 quà đã nhận**; **KHÔNG có CTA** (cột CTA của `EMP-08` = `—`) | P3 | UI | MODIFIED |
| SC-GIFT-011 | Không có sao/điểm/tier/chỉ số môi trường *(hết gap)* | REQ-GIFT-005 | DOC-v1.1-01 §8.14.1 BR14-03 · §4 SCOPES Out of Scope | Đơn `COMPLETED`, đi hết luồng tặng quà và mở Trang cá nhân | Rà toàn bộ màn Tặng quà · popup cảm ơn · "Quà đã nhận" · Trang cá nhân | **KHÔNG** có chấm sao 1–5, **KHÔNG** điểm, **KHÔNG** tier/xếp hạng, **KHÔNG** chỉ số môi trường ở bất kỳ đâu. ⚠ Nếu thấy ★ leftover → là **defect** (xem `SC-ACT-013`) | P3 | Business Rule | MODIFIED |

#### Source Detail per Scenario (verbatim quotes)

##### SC-GIFT-013 / SC-GIFT-014 — Hai vế phủ định của trạng thái RETURNED
📍 `DOC-v1.1-01 §6.2 AC-24.2.01 "Đơn hoàn hàng không mở bước tặng quà" · trang 25` · `§8.14.1 BR14-04 · trang 49`

> `AC-24.2.01`: "Given: Đơn kết thúc ở trạng thái RETURNED. When: Người gửi mở đơn. Then: Không có nút tặng quà (không có giao dịch giúp đỡ hoàn tất). Đơn hiển thị lý do hoàn hàng và nằm trong lịch sử đơn, nhưng không cộng vào "Đơn đã giúp" của người vận chuyển."

> `BR14-04`: ""Đơn đã giúp" chỉ tính đơn COMPLETED — đơn RETURNED không được tính."

**Analyst Note:** Một AC, **hai lỗi khác hẳn nhau về cách phát hiện** ⇒ tách 2 SC, không gộp. `SC-GIFT-013` là lỗi **nhìn thấy được** (nút thừa trên màn) — tester mở đơn là biết ngay. `SC-GIFT-014` là lỗi **âm thầm**: bộ đếm sai 1 đơn không ai nhận ra bằng mắt, phải **ghi số trước rồi so sau** — vì vậy Given của nó bắt buộc phải có bước *"ghi lại số trước"*, ⛔ không viết kiểu *"kiểm tra số đúng"*. ⚠️ **Cả 2 SC phụ thuộc nhánh `RETURNING → RETURNED` của `DLV` (`FR09`)** — nếu app STG chưa build nhánh đó thì **không seed được tiền đề** và verdict đúng là **BLOCKED**, ⛔ không PASS (không có đơn `RETURNED` nào thì "không thấy nút tặng quà" chẳng chứng minh điều gì). Xem `RISK-GIFT-06`. Cross-ref chỉ số: `USR` (2 chỉ số đóng góp) · `HOME` (card "Đóng góp của bạn") — cùng bộ đếm, ⛔ không nhân bản SC.

---

##### SC-GIFT-002 / SC-GIFT-003 — Tên 4 loại quà và text popup nay là chuỗi chính thức
📍 `DOC-v1.1-01 §8.14.1 BR14-01 / BR14-02 · trang 49` · `§6.2 AC-24.1.01 · trang 25`

> `BR14-01`: "4 loại quà: bông hoa · ly cà phê · gấu bông · vương miện — biểu tượng phi vật chất, không quy đổi tiền, không qua thanh toán trong ứng dụng."

> `BR14-02`: "Gửi ngay, không cần bước xác nhận của người nhận quà; hiện popup "Cảm ơn của bạn đã được gửi"."

**Analyst Note (diff):** Hai SC này **không đổi hành vi, chỉ đổi độ chặt của Then** — và đó đúng là loại nâng cấp rẻ nhất mà bắt được lỗi thật. v1.0 assert *"có đúng 4 loại quà"* (PASS kể cả khi dev đổi gấu bông thành icon khác) và *"hiện popup cảm ơn"* (PASS với bất kỳ popup nào). Nay assert **danh tính** và **chuỗi verbatim**. `AC-24.1.01` bổ sung chi tiết v1.0 không có: popup **có nút về trang chủ**. ⚠️ Đây là vế (a) của `C-GIFT-03` ⇒ Resolved.

---

##### SC-GIFT-006 / SC-GIFT-007 — Màn "Quà đã nhận": card đếm + lịch sử
📍 `DOC-v1.1-01 §6.2 AC-26.1.01 · trang 27`

> "Then: Hiển thị số "Đơn đã giúp" = 7 (không tính đơn RETURNED) và card đếm quà theo từng loại, tổng 5, kèm lịch sử nhận quà. Không có điểm, tier, xếp hạng hay quy đổi tiền."

**Analyst Note (diff):** ⭐ `SC-GIFT-007` **hết `[GAP]`** — đây là vế (b) của `C-GIFT-03` (*"có danh sách lịch sử nhận quà hay không"*), nay trả lời dứt khoát **CÓ** ⇒ nâng **P3 → P2** vì từ "ghi nhận" thành "assert khẳng định". `SC-GIFT-006` giữ nguyên rule *"loại `count = 0` không hiện card"* (nguồn v1.0 `KB-GIFT-03`) — PRD **không mâu thuẫn** nhưng cũng **không nhắc lại**, nên rule đó vẫn đứng trên quan sát app; ghi rõ ở đây để người sau không tưởng nó cũng có nguồn PRD. `AC-26.1.01` cho sẵn bộ số ví dụ (7 đơn / 5 quà) — dùng thẳng làm test data.

---

##### SC-GIFT-008 — `EMP-08`: text chính thức + KHÔNG có CTA
📍 `DOC-v1.1-01 §8.17.1 bảng Danh mục empty state, dòng EMP-08 · trang 51`

> "EMP-08 | Trang cá nhân | Thống kê hiện 0 đơn đã giúp / 0 quà đã nhận; màn "Quà đã nhận" hiện "Chưa nhận được quà nào" | —"

**Analyst Note (diff):** Phần thuộc `GIFT` của `C-ORD-06` (home canonical ở `ACT`) — CL từng **Resolved rồi REVERT** vì lần chốt trước không kèm bằng chứng. Lần này nguồn là tài liệu đã phê duyệt ⇒ bền. ⚠️ **Cột CTA của `EMP-08` là `—`, và đó là một assert thật:** `BR17-01` cho phép *"tối đa một CTA"* nên "không có CTA" là lựa chọn thiết kế có chủ đích, không phải thiếu sót — nếu app hiện nút gì đó ở đây thì **sai spec**. Đối chiếu: `EMP-01`/`EMP-02`/`EMP-04`/`EMP-05` **có** CTA, `EMP-03`/`EMP-06`/`EMP-07`/`EMP-08` **không**.

---

##### SC-GIFT-011 — Loại trừ sao/điểm/tier nay là vĩnh viễn, không phải hoãn
📍 `DOC-v1.1-01 §8.14.1 BR14-03 · trang 49` · `§4 SCOPES dòng Out of Scope · trang 9`

> `BR14-03`: "Không có chấm sao 1–5, không điểm, không tier/xếp hạng, không chỉ số môi trường."

> §4 SCOPES Out of Scope: "Đánh giá sao 1–5 và mọi hình thức xếp hạng/tier/điểm thưởng — thay bằng quà ảo"

**Analyst Note (diff):** 🔴 v1.0 kết luận *"out of scope **v1.0**"* — chữ "v1.0" để ngỏ khả năng có ở phase sau ⇒ `SC-GIFT-011` chỉ dám **ghi nhận**. v1.1 dùng chữ **"thay bằng quà ảo"** ở mục Out of Scope của **cả sản phẩm** ⇒ đây là **quyết định thiết kế vĩnh viễn**, và `BR14-03` bổ sung *"không chỉ số môi trường"* (v1.0 chưa nhắc — `KP-04` ghi đợt cũ từng có "điểm/CO₂"). ⇒ SC hết `[GAP]`, thành **assert-absent khẳng định** trên 4 bề mặt. ⚠️ **Hệ quả sang `ACT`:** `SC-ACT-013` (★★★★★ leftover trên card tab Hoàn thành) nay là **defect xác nhận**, không còn là "dấu vết hợp lệ của phase sau" — xem `v1.1/ACT-hoat-dong/`.

---

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| SC-GIFT-001 | Mở màn Tặng quà sau Hoàn thành | GIFT | v1.0 | P2 | → `v1.0/GIFT-qua-cam-on/test_scenario_map.md` — `FR14` Trigger xác nhận lại |
| SC-GIFT-004 | Không quy đổi tiền / thanh toán | GIFT | v1.0 | P3 | → như trên — `BR14-01` xác nhận lại nguyên văn |
| SC-GIFT-005 | Nút đổi nhãn sau khi gửi quà | GIFT | v1.0 | P2 | → như trên — *(2026-09-17)* ✅ **`C-GIFT-04` Resolved 2026-09-17 (vòng 2), đủ (1)–(4):** sau khi **BẤM GỬI** thì nút đổi nhãn **"Bạn đã đánh giá"** + **DISABLE** ⇒ nhãn nút nay có nguồn BA, ⛔ không còn là `QA-obs`. ⚠️ Phân biệt: *"đóng"* tính từ lúc **bấm gửi**, KHÔNG phải từ lúc thoát màn — thoát giữa chừng thì **vẫn tặng lại được, không thời hạn** (hết mâu thuẫn với `C-ACT-01`) |
| SC-GIFT-009 | Back từ "Quà đã nhận" | GIFT | v1.0 | P3 | → như trên |
| SC-GIFT-010 | [GAP·bug] Back từ "Tặng quà" nhảy sai màn | GIFT | v1.0 | P3 | → như trên — ✅ **2026-09-16 BA: lỗi demo; rule = back về màn hình trước đó** (`C-GIFT-02` Resolved) ⇒ Then assert back về đúng màn đã mở "Tặng quà"; nhảy sang đơn/màn khác = **bug** |
| SC-GIFT-012 | Thông báo cho Carrier khi nhận quà | GIFT | v1.0 | P2 | → như trên — `NTF-07` nay nằm trong danh mục 15 loại chính thức (`NTF` v1.1) |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
