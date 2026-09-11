---
id: v1.0/GIFT-qua-cam-on/scenario-map
title: Test Scenario Map — v1.0 · Module GIFT
type: scenario-map
version: v1.0
sprint: 1
module: GIFT
counts:
  req: 8
  sc: 12
  new: 12
  modified: 0
  carried: 0
  deprecated: 0
  p1: 0
  p2: 6
  p3: 6
status: ANALYZED
updated: 2026-09-07
---

# Test Scenario Map — v1.0 · Module GIFT

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module GIFT.
> ⚠️ **P1 = 0 có chủ đích:** quà ảo là *"tính năng tương tác xã hội, không bắt buộc"* (`DOC-v1.0-02` §3.8) — không chặn luồng nghiệp vụ nào. Nhưng **toàn module phụ thuộc `SC-DLV-023`** (đơn phải tới "Hoàn thành").

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Fan-out mỗi role · state-transition · lớp EP · boundary · nhánh lỗi = 1 SC.
> Module fan-out theo **state của nút tặng quà** (chưa gửi / đã gửi) và **điều kiện hiển thị card đếm** (count > 0 / count = 0).

## Tổng quan
- Tổng số scenarios: **12** (NEW: 12, MODIFIED: 0, CARRIED: 0, DEPRECATED: 0)
- Phân bổ priority: P1: 0 | P2: 6 | P3: 6
- 5/12 SC là dạng `[GAP]` — module có nhiều thành phần **1 nguồn** hoặc **chưa chốt** (danh sách lịch sử · empty state · nút back · rating).

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### GIFT — Quà cảm ơn

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-GIFT-001 | Mở màn Tặng quà sau Hoàn thành | REQ-GIFT-001 | DOC-v1.0-01 §A7 L107 · KP-01 §5.1 (ô 5·Sender) | Đơn ở trạng thái "Hoàn thành"; tài khoản **Người gửi**, chưa gửi quà | Bấm nút "✓ Cảm ơn người vận chuyển" | Mở màn "Tặng quà" với 4 lựa chọn quà | P2 | Functional | NEW |
| SC-GIFT-002 | Đúng 4 loại quà | REQ-GIFT-001 | DOC-v1.0-01 §A7 L108 · §D3 GIFT-01 L258 · DOC-v1.0-02 §3.8 | Đang ở màn "Tặng quà" | Đối chiếu danh mục quà | Đúng **4 loại**: Bông hoa · Ly cà phê · Gấu bông · Vương miện (không thừa, không thiếu) | P2 | UI | NEW |
| SC-GIFT-003 | Gửi quà → popup cảm ơn | REQ-GIFT-002 | DOC-v1.0-02 §3.8 · DOC-v1.0-01 §D1b US-D15 L194 | Đang ở màn "Tặng quà" | Chọn 1 loại quà rồi xác nhận gửi | Hiện modal "Đã gửi lời cảm ơn!"; ⛔ KHÔNG có bước chờ Carrier xác nhận (⚠ `US-D15` ghi text khác: "Cảm ơn của bạn đã được gửi" — C-GIFT-03) | P2 | Functional | NEW |
| SC-GIFT-004 | Không quy đổi tiền / thanh toán | REQ-GIFT-002 | DOC-v1.0-01 §D4 BR-GIFT-01 L271 · §A7 L111 | Đang ở màn "Tặng quà" | Rà toàn màn tìm giá tiền, ví, cổng thanh toán, quy đổi điểm | KHÔNG có bất kỳ thành phần thanh toán/quy đổi tiền nào (quà là biểu tượng phi vật chất) | P3 | Business Rule | NEW |
| SC-GIFT-005 | Nút đổi nhãn sau khi gửi quà | REQ-GIFT-003 | DOC-v1.0-06 KP-01 §6 KB-GIFT-01 · §5.1 (ô 5·Sender) | Sender vừa gửi quà thành công cho 1 đơn | Quay lại màn Theo dõi đơn của đơn đó | Nút đổi nhãn thành "Bạn đã đánh giá" và **disable** — không gửi quà lại được cho cùng đơn | P2 | Business Rule | NEW |
| SC-GIFT-006 | Card đếm chỉ hiện loại count > 0 | REQ-GIFT-004 | DOC-v1.0-06 KP-01 §6 KB-GIFT-03 · DOC-v1.0-01 §D1b US-D20 L196 | Tài khoản Carrier đã nhận **2 trong 4 loại** quà | Mở màn "Quà đã nhận" (từ menu ở Cá nhân) | Card đếm chỉ hiển thị **2 loại đã nhận** kèm số lượng; 2 loại chưa nhận **KHÔNG hiện**, kể cả dạng "0" | P2 | Business Rule | NEW |
| SC-GIFT-007 | [GAP] Danh sách lịch sử nhận quà | REQ-GIFT-004 | DOC-v1.0-01 §D1b US-D20 L196 (1 nguồn văn bản) | `US-D20` nêu có "danh sách lịch sử nhận quà" nhưng chưa có ảnh Figma/app xác nhận | Mở màn "Quà đã nhận", tìm danh sách lịch sử | GHI NHẬN có/không có danh sách lịch sử; nếu KHÔNG có → báo về `C-GIFT-03`, ⛔ không im lặng bỏ qua | P3 | UI | NEW |
| SC-GIFT-008 | [GAP] Empty state "Quà đã nhận" | REQ-GIFT-007 | DOC-v1.0-06 KP-02 §5 · C-ORD-06 | Tài khoản **chưa nhận quà nào** (cả 4 loại count = 0 ⇒ không load loại nào) | Mở màn "Quà đã nhận" | GHI NHẬN hiển thị thực tế; ⛔ KHÔNG assert text — chưa có đặc tả (C-ORD-06 Open) | P3 | UI | NEW |
| SC-GIFT-009 | Back từ "Quà đã nhận" | REQ-GIFT-006 | DOC-v1.0-06 KP-01 §6 KB-GIFT-03 | Đang ở màn "Quà đã nhận" (mở từ menu ở Cá nhân) | Bấm icon quay lại ở header | Về đúng màn Cá nhân | P3 | Functional | NEW |
| SC-GIFT-010 | [GAP·bug] Back từ "Tặng quà" nhảy sai màn | REQ-GIFT-006 | DOC-v1.0-06 KP-01 §6 KB-GIFT-04 | Đang ở màn "Tặng quà" mở từ 1 đơn "Hoàn thành" thật (không phải item mẫu demo) | Bấm nút back (←) | Về đúng màn trước đó (Theo dõi đơn / Đơn của tôi). ⚠ Đã quan sát nhảy sang "Xác nhận đã nhận hàng" của **đơn khác** — nếu tái hiện trên app thật → log bug (C-GIFT-02) | P3 | Functional | NEW |
| SC-GIFT-011 | [GAP] Không có chấm sao 1–5 ở v1.0 | REQ-GIFT-005 | DOC-v1.0-01 §A5 BR-INT-06 L82 · §A8 L125 · KP-01 §6 KB-GIFT-02 | `RAT-01/02` nêu đánh giá 1–5 sao; `C-GIFT-01` Resolved: out of scope v1.0 | Rà luồng sau "Hoàn thành" (Theo dõi đơn · Tặng quà · Cá nhân) tìm màn/control chấm sao | GHI NHẬN GAP: không tồn tại màn chấm sao/nhận xét ở v1.0 (đúng phạm vi). ⛔ KHÔNG viết TC chấm sao | P3 | Business Rule | NEW |
| SC-GIFT-012 | Thông báo cho Carrier khi nhận quà | REQ-GIFT-008 | DOC-v1.0-01 §D6 NTF-07 L325 · §A7 L109 | Sender vừa gửi quà cho Carrier B | B kiểm tra thông báo | B nhận thông báo "Bạn nhận được một món quà cảm ơn 🎁 — mở Trang cá nhân để xem"; bấm vào → mở Trang cá nhân | P2 | Functional | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-GIFT-001 / SC-GIFT-002 — Mở màn Tặng quà · đúng 4 loại quà

**Source Quote:**
> "Sau khi đơn hoàn tất, người gửi tặng quà ảo cảm ơn người vận chuyển"
> "4 loại quà: bông hoa, ly cà phê, gấu bông, vương miện — biểu tượng phi vật chất"
> (`DOC-v1.0-02` §3.8): "4 lựa chọn quà: 🌷 Bông hoa · ☕ Ly cà phê · 🧸 Gấu bông · 👑 Vương miện."

**Source Location:** `DOC-v1.0-01 §A7 "Phần thưởng — Quà ảo" · bullet 1-2 · L107-108` ⟷ `DOC-v1.0-02 §3.8 "Màn hình Tặng quà"`

**Analyst Note:** 3 nguồn đồng thuận cả số lượng và tên 4 loại ⇒ assert được danh mục đóng (**không thừa, không thiếu**). ⚠️ **Toàn module phụ thuộc tiền đề "Hoàn thành"** — cần chạy xong `SC-DLV-023` trước; nếu Receiver không chốt được đơn thì `GIFT` blocked hoàn toàn.

##### SC-GIFT-003 / SC-GIFT-004 — Gửi ngay + popup · không quy đổi tiền

**Source Quote:**
> `US-D15` (§D1b L194): "chọn quà → gửi ngay không cần bước xác nhận → popup **"Cảm ơn của bạn đã được gửi"** → nút "Về trang chủ""
> PRD (`§3.8`): "Xác nhận → modal **"Đã gửi lời cảm ơn!"** — tính năng tương tác xã hội, không bắt buộc."
> `BR-GIFT-01` (§D4 L271): "Quà cảm ơn là biểu tượng phi vật chất, **không quy đổi tiền, không qua thanh toán in-app**"

**Source Location:** `DOC-v1.0-01 §D1b · US-D15 · L194` ⟷ `DOC-v1.0-02 §3.8` ⟷ `DOC-v1.0-01 §D4 · BR-GIFT-01 · L271`

**Analyst Note:** ⚠️ **Hai lệch cần phân biệt:** (a) **text popup** — `US-D15` *"Cảm ơn của bạn đã được gửi"* ⟷ PRD+Figma *"Đã gửi lời cảm ơn!"* ⇒ chốt theo bề mặt (PRD+Figma), mở `C-GIFT-03`; (b) **luồng** — `US-D15` nói *"không cần bước xác nhận"* nhưng PRD có bước *"Xác nhận →"* ⇒ hiểu đúng là **không cần Carrier xác nhận**, Sender vẫn phải xác nhận. `SC-GIFT-004` là assert-absent cho `NT-03` (không thanh toán) ở phạm vi màn này.

##### SC-GIFT-005 — Nút đổi nhãn "Bạn đã đánh giá" sau khi gửi

**Source Quote:**
> "Ở trạng thái Hoàn thành, Sender thấy nút `✓ Cảm ơn người vận chuyển` (enable). Sau khi chọn 1 loại quà và gửi thành công, nút **đổi nhãn thành `Bạn đã đánh giá` (disable, không gửi lại được)**."

**Source Location:** `DOC-v1.0-06 KP-01 §6 "KB-GIFT-01" · đoạn 1` (đồng thuận `KP-01 §5.1` ma trận ô 5·Sender)

**Analyst Note:** **Phát hiện hoàn toàn ngoài tài liệu** (`QA-obs` + Figma popup) — đợt cũ đã sinh REQ riêng. Rule mang 2 hệ quả: **chỉ tặng quà 1 lần/đơn** (nút disable) và nhãn dùng từ *"đánh giá"* cho hành động tặng quà ⇒ **củng cố `C-GIFT-01`** (quà ảo **thay cho** chấm sao). ⛔ Không hiểu nhãn này là bằng chứng có tính năng rating.

##### SC-GIFT-006 / SC-GIFT-007 — Card đếm có điều kiện · [GAP] danh sách lịch sử

**Source Quote:**
> "Card đếm theo 4 loại quà (bông hoa / ly cà phê / gấu bông / vương miện) nhưng **chỉ hiển thị loại đã thực sự nhận (count > 0)** — loại chưa nhận lần nào thì **không load, không hiện dạng "0"**."
> "⚠ Thành phần "Danh sách lịch sử" **chỉ có bằng chứng văn bản US-D20**, chưa có ảnh Figma/app → **cần vibe-test xác nhận**. Nếu app không có → mở clarification, không im lặng bỏ qua."

**Source Location:** `DOC-v1.0-06 KP-01 §6 "KB-GIFT-03" · đoạn 1 và ghi chú`

**Analyst Note:** ⚠️ **Hai mức bằng chứng trong 1 REQ:** card đếm có `QA-obs` (kèm **điều chỉnh so với hiểu ban đầu** — trước tưởng luôn hiện đủ 4 loại) ⇒ assert được rule count>0; **danh sách lịch sử** chỉ 1 nguồn văn bản ⇒ theo `§Custom Rules §10.1` chỉ ghi nhận (`SC-GIFT-007`), và nguồn **tự yêu cầu** không được im lặng bỏ qua ⇒ SC này bắt buộc phải có.

##### SC-GIFT-008 — [GAP] Empty state màn "Quà đã nhận"

**Source Quote:**
> "**C-ORD-06** | Empty state của 3 màn (Hoạt động · **Quà đã nhận** · Thông báo) khi không có data"

**Source Location:** `DOC-v1.0-06 KP-02 §5 · bảng "Nhóm Open" · dòng "C-ORD-06"` (home canonical: `ACT-hoat-dong/risk_assessment.md`)

**Analyst Note:** Ở module này empty state **đặc biệt dễ gặp** vì rule *"chỉ hiện loại count > 0"*: tài khoản chưa nhận quà nào ⇒ **cả 4 loại đều không load** ⇒ màn rỗng hoàn toàn (không phải "4 số 0"). ⛔ Không assert text — CL từng bị revert vì chốt theo mô tả chat (`KP-02 §6`).

##### SC-GIFT-009 / SC-GIFT-010 — Back từ "Quà đã nhận" · [GAP·bug] back từ "Tặng quà"

**Source Quote:**
> "Ngoài ra có `Danh sách lịch sử` nhận quà và icon quay lại ở header (→ về màn Cá nhân)."
> "Bấm back (←) từ màn "Tặng quà" (mở từ item mẫu tab "Đã hoàn thành") nhảy tới màn "Xác nhận đã nhận hàng" của **một đơn KHÁC không liên quan**, thay vì quay về "Đơn của tôi"."

**Source Location:** `DOC-v1.0-06 KP-01 §6 "KB-GIFT-03"` và `"KB-GIFT-04"`

**Analyst Note:** 2 hành vi back khác nhau ⇒ 2 SC. ⚠️ `KB-GIFT-04` phát hiện trong ngữ cảnh *"item mẫu tab Đã hoàn thành"* của **bản demo** ⇒ rất có thể là **giới hạn demo** (item mẫu tĩnh chưa wiring back-stack, chính nguồn cũng đánh giá vậy) ⇒ Given của `SC-GIFT-010` yêu cầu **đơn thật**, ⛔ không kết luận bug từ dữ liệu mẫu.

##### SC-GIFT-011 — [GAP] Không có chấm sao 1–5 ở v1.0

**Source Quote:**
> Mâu thuẫn (`RAT-01/02` §D3 L256): "RAT-01/02 | Đánh giá 2 chiều | 1–5 sao + nhận xét"
> Rule (`BR-INT-06` §A5 L82): "**Không đánh giá sao**; ghi nhận thiện chí bằng quà ảo…"
> Rule (`§A8` L125): "**KHÔNG có chấm sao/đánh giá**, KHÔNG có chặn (block) người dùng."

**Source Location:** `DOC-v1.0-01 §D3 · RAT-01/02 · L256` ⟷ `§A5 · BR-INT-06 · L82` ⟷ `§A8 · L125` ⟷ phán quyết `DOC-v1.0-06 KP-01 §6 "KB-GIFT-02"`

**Analyst Note:** ⭐ **BRD mâu thuẫn 3-1** — 3 nguồn nói không có chấm sao, 1 nguồn (`RAT-01/02`) nói có. `C-GIFT-01` Resolved 2026-07-27: **out of scope v1.0**. 📌 **Hệ quả scope quan trọng nhất của cả dự án:** *"Đánh giá"* trong 5 luồng Phase 1 của PM = **Quà ảo** (`KP-03 §3` dòng 5). SC assert-absent trên **3 bề mặt** (Theo dõi đơn · Tặng quà · Cá nhân) để chốt trạng thái cho version sau.

##### SC-GIFT-012 — Thông báo cho Carrier khi nhận quà

**Source Quote:**
> "NTF-07 | Người gửi tặng quà ảo | Người vận chuyển | "Bạn nhận được một món quà cảm ơn 🎁 — mở Trang cá nhân để xem""

**Source Location:** `DOC-v1.0-01 §D6 "Thông báo (Notifications)" · bảng · NTF-07 · L325`

**Analyst Note:** `KP-07` (bảng unified 3 nguồn) xếp hàng #7 với ghi chú *"Dùng cho REQ-GIFT-001 (trong scope v1.0)"* và Figma khớp gần BRD ⇒ đây là **1 trong ít loại thông báo KHÔNG bị tranh chấp** bởi `C-NTF-01` ⇒ assert được text phần đầu. Cơ chế màn Thông báo (nhóm thời gian · chấm đỏ · phân trang) thuộc `NTF`.

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| — | *(không có — v1.0 là version đầu của chuỗi phân tích mới)* | — | — | — | — |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
