# Requirement Traceability — v1.1 · Module GIFT

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation` của `DOC-v1.1-01` = `FR<NN>` / `BR<FF>-NN` / `AC-{US}.{Scenario}.{Case}` ⇒ **Schema A**.
> Chỉ chứa REQ **NEW + MODIFIED** của lượt delta này. REQ CARRIED nguyên trạng — xem `v1.0/GIFT-qua-cam-on/requirement_traceability.md`.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module GIFT — DOC-v1.1-01

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-GIFT-009 | `FR14` Pre-Conditions, `BR14-04`, `AC-24.2.01` | `DOC-v1.1-01` §8.14 (trang 48-49) · §8.14.1 BR14-04 · §6.2 AC-24.2.01 (trang 25) | SC-GIFT-013, SC-GIFT-014 | — |
| REQ-GIFT-001 *(MODIFIED)* | `BR14-01`, `AC-24.1.01` | `DOC-v1.1-01` §8.14.1 BR14-01 (trang 49) · §6.2 AC-24.1.01 (trang 25) | SC-GIFT-001, SC-GIFT-002 | — |
| REQ-GIFT-002 *(MODIFIED)* | `BR14-02`, `AC-24.1.01` | `DOC-v1.1-01` §8.14.1 BR14-02 (trang 49) · §6.2 AC-24.1.01 (trang 25) | SC-GIFT-003, SC-GIFT-004 | C-GIFT-03 |
| REQ-GIFT-004 *(MODIFIED)* | `AC-26.1.01`, `BR14-04` | `DOC-v1.1-01` §6.2 AC-26.1.01 (trang 27) · §8.14.1 BR14-04 | SC-GIFT-006, SC-GIFT-007 | C-GIFT-03 |
| REQ-GIFT-005 *(MODIFIED)* | `BR14-03`, `AC-24.1.01`, `AC-26.1.01`, §4 SCOPES | `DOC-v1.1-01` §8.14.1 BR14-03 (trang 49) · §4 SCOPES Out of Scope (trang 9) | SC-GIFT-011 | C-GIFT-01 |
| REQ-GIFT-007 *(MODIFIED)* | `EMP-08`, `AC-26.2.01` | `DOC-v1.1-01` §8.17.1 EMP-08 (trang 51) · §6.2 AC-26.2.01 (trang 27) | SC-GIFT-008 | C-ORD-06 |

> ℹ️ `REQ-GIFT-003` · `REQ-GIFT-006` · `REQ-GIFT-008` **CARRIED không đổi** — PRD không nhắc tới nút đổi nhãn sau khi gửi quà, lỗi back-navigation, hay chi tiết `NTF-07` ngoài việc liệt kê nó.

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-GIFT-009 · Đơn RETURNED không mở bước tặng quà và không cộng "Đơn đã giúp"
📍 `DOC-v1.1-01 §8.14 dòng Pre-Conditions · trang 48-49` · `§8.14.1 BR14-04 · trang 49` · `§6.2 AC-24.2.01 · trang 25`  ·  Clarif: —

> Nguồn #1 — FR14 Pre-Conditions (§8.14):
> "Đơn ở COMPLETED (đơn RETURNED không mở bước này)"

> Nguồn #2 — BR14-04 (§8.14.1, trang 49):
> ""Đơn đã giúp" chỉ tính đơn COMPLETED — đơn RETURNED không được tính."

> Nguồn #3 — AC-24.2.01 (§6.2, trang 25):
> "Given: Đơn kết thúc ở trạng thái RETURNED. When: Người gửi mở đơn. Then: Không có nút tặng quà (không có giao dịch giúp đỡ hoàn tất). Đơn hiển thị lý do hoàn hàng và nằm trong lịch sử đơn, nhưng không cộng vào "Đơn đã giúp" của người vận chuyển."

↳ **Ghi chú:** ⭐ **REQ MỚI — sinh ra từ một trạng thái mà v1.0 chưa hề có.** `RETURNED` là kết cục mới do `FR09` (cầm hàng về / hoàn hàng) mang tới, đã phân tích ở `DLV` (`SC-DLV-053..056`). Ở `GIFT`, nó tạo **hai vế phủ định độc lập nhau** nên tách 2 SC: (a) **bề mặt** — không có nút tặng quà; (b) **số liệu** — không cộng vào bộ đếm "Đơn đã giúp". Vế (b) quan trọng hơn vế (a) vì nó **âm thầm**: một đơn hoàn hàng lọt vào bộ đếm sẽ không ai thấy cho tới khi đối soát số. ⚠️ **Phụ thuộc `DLV`:** cả 2 SC cần đơn đi hết nhánh `RETURNING → RETURNED`, mà nhánh đó có thể chưa build trên STG (xem `RISK-DLV-08` cùng họ) ⇒ xem `RISK-GIFT-06`. Vế (b) còn chạm `USR` (`SC-USR-005`/`SC-USR-012` — 2 chỉ số đóng góp) và `ACT`/`HOME` (card "Đóng góp của bạn") — ⛔ không nhân bản SC, chỉ ghi cross-ref.

---

### REQ-GIFT-001 · Đúng 4 loại quà, nay có tên chính thức *(MODIFIED)*
📍 `DOC-v1.1-01 §8.14.1 BR14-01 · trang 49` · `§6.2 AC-24.1.01 · trang 25`  ·  Clarif: —

> Nguồn (v1.0) — `DOC-v1.0-01 §D3 GIFT-01 · L258` + `§A7 L107-108`:
> "Người gửi tặng quà ảo cảm ơn người vận chuyển sau khi đơn hoàn thành. 4 loại quà phi vật chất."

> Nguồn (v1.1) — BR14-01 (§8.14.1, trang 49):
> "4 loại quà: bông hoa · ly cà phê · gấu bông · vương miện — biểu tượng phi vật chất, không quy đổi tiền, không qua thanh toán trong ứng dụng."

↳ **Ghi chú (diff):** v1.0 biết *"có 4 loại"* nhưng **tên 4 loại lấy từ quan sát app/Figma**, không từ tài liệu ⇒ `SC-GIFT-002` chỉ assert được **số lượng**, không assert được **danh tính**. Nay PRD liệt kê đủ tên bằng chữ ⇒ `SC-GIFT-002` siết thành **assert đúng 4 tên, đúng thứ tự liệt kê**. Đây là dạng nâng cấp rẻ nhưng bắt được lỗi thật: nếu dev đổi "gấu bông" thành icon khác mà TC chỉ đếm 4 thì không ai phát hiện.

---

### REQ-GIFT-002 · Gửi ngay không cần xác nhận + popup có text chính thức *(MODIFIED)*
📍 `DOC-v1.1-01 §8.14.1 BR14-02 · trang 49` · `§6.2 AC-24.1.01 · trang 25`  ·  Clarif: `C-GIFT-03`

> Nguồn (v1.0) — `DOC-v1.0-01 §D4 BR-GIFT-01 · L271`:
> "Quà gửi một chiều, không cần người nhận xác nhận."

> Nguồn (v1.1) #1 — BR14-02 (§8.14.1, trang 49):
> "Gửi ngay, không cần bước xác nhận của người nhận quà; hiện popup "Cảm ơn của bạn đã được gửi"."

> Nguồn (v1.1) #2 — AC-24.1.01 Then (§6.2, trang 25):
> "Quà được gửi ngay, không cần bước xác nhận của người nhận quà. Hiện popup "Cảm ơn của bạn đã được gửi" và nút về trang chủ. Người vận chuyển nhận NTF-07 và thấy quà trong "Quà đã nhận". Không có thang điểm hay đánh giá sao ở bất kỳ đâu trong luồng này."

↳ **Ghi chú (diff):** Cơ chế *"một chiều"* không đổi; **cái mới là chuỗi text chính xác** — `"Cảm ơn của bạn đã được gửi"`. Đây là vế (a) của `C-GIFT-03` (mở 2026-09-07, hỏi đúng câu *"text popup sau khi gửi quà là gì"*) ⇒ **Resolved**. `AC-24.1.01` còn thêm **nút về trang chủ** trên popup — chi tiết v1.0 không có. ⇒ `SC-GIFT-003` đổi Then từ *"hiện popup cảm ơn"* (mơ hồ, PASS bằng bất kỳ popup nào) thành **assert verbatim chuỗi + assert có nút về trang chủ**.

---

### REQ-GIFT-004 · Màn "Quà đã nhận": card đếm theo loại + có lịch sử nhận quà *(MODIFIED)*
📍 `DOC-v1.1-01 §6.2 AC-26.1.01 · trang 27` · `§8.14.1 BR14-04`  ·  Clarif: `C-GIFT-03`

> Nguồn (v1.0) — `DOC-v1.0-01 §D1b US-D20 · L196` + `KP-01 §6 KB-GIFT-03`:
> "Người vận chuyển xem 'Quà đã nhận'. (Có danh sách lịch sử hay chỉ card đếm — chưa rõ.)"

> Nguồn (v1.1) — AC-26.1.01 (§6.2, trang 27):
> "Given: Người vận chuyển đã hoàn tất 7 đơn và nhận 5 quà. When: Người vận chuyển mở trang cá nhân. Then: Hiển thị số "Đơn đã giúp" = 7 (không tính đơn RETURNED) và card đếm quà theo từng loại, tổng 5, kèm lịch sử nhận quà. Không có điểm, tier, xếp hạng hay quy đổi tiền."

↳ **Ghi chú (diff):** Đây là vế (b) của `C-GIFT-03` — *"có 'danh sách lịch sử nhận quà' hay không"* ⇒ **Resolved: CÓ**. `SC-GIFT-007` ở v1.0 là SC dạng `[GAP]` (*ghi nhận không rõ có danh sách hay không*), nay **hết gap** và lật thành assert khẳng định ⇒ nâng **P3 → P2**. `AC-26.1.01` còn cho một **ví dụ số cụ thể** (7 đơn / 5 quà) rất tiện làm test data — và quan trọng hơn, nó gắn luôn mệnh đề *"(không tính đơn RETURNED)"* vào đúng chỗ bộ đếm, tức `BR14-04` không phải rule rời mà là thuộc tính của chính màn này.

---

### REQ-GIFT-005 · Không có sao/điểm/tier — nay là loại trừ vĩnh viễn, không phải hoãn tới phase sau *(MODIFIED)*
📍 `DOC-v1.1-01 §8.14.1 BR14-03 · trang 49` · `§4 SCOPES dòng Out of Scope · trang 9`  ·  Clarif: `C-GIFT-01`

> Nguồn (v1.0) — `DOC-v1.0-01 §D3 RAT-01/02 · L256` ⇒ `C-GIFT-01` Resolved: *"Out of scope **v1.0**; v1.0 chỉ có Quà ảo"*.

> Nguồn (v1.1) #1 — BR14-03 (§8.14.1, trang 49):
> "Không có chấm sao 1–5, không điểm, không tier/xếp hạng, không chỉ số môi trường."

> Nguồn (v1.1) #2 — §4 SCOPES, Out of Scope (trang 9):
> "Đánh giá sao 1–5 và mọi hình thức xếp hạng/tier/điểm thưởng — thay bằng quà ảo"

↳ **Ghi chú (diff):** 🔴 **Khác biệt tinh nhưng đổi hẳn cách viết TC.** v1.0 kết luận *"out of scope **v1.0**"* — hàm ý *"có thể có ở version sau"* ⇒ `SC-GIFT-011` chỉ dám **ghi nhận** rằng chưa thấy sao. v1.1 đưa nó vào **Out of Scope của cả sản phẩm**, dùng chữ *"thay bằng quà ảo"* (thay thế, không phải hoãn) và `BR14-03` liệt kê thêm **"không chỉ số môi trường"** — thứ v1.0 chưa nhắc. ⇒ `SC-GIFT-011` hết `[GAP]`, trở thành **assert-absent khẳng định**: không sao, không điểm, không tier, **không chỉ số môi trường** ở bất kỳ đâu trong luồng. ⚠️ Cross-ref: `ACT` có `SC-ACT-013` — **★★★★★ leftover trên card Hoàn thành** — nay là **defect xác nhận**, không còn là "dấu vết của phase sau".

---

### REQ-GIFT-007 · Empty state "Quà đã nhận" có text chính thức *(MODIFIED)*
📍 `DOC-v1.1-01 §8.17.1 EMP-08 · trang 51` · `§6.2 AC-26.2.01 · trang 27`  ·  Clarif: `C-ORD-06`

> Nguồn (v1.0) — `DOC-v1.0-06 KP-02 §5 dòng C-ORD-06` ⇒ text empty state **chưa chốt** (từng Resolved 2026-07-28 rồi **REVERT** 2026-07-29 vì chốt không kèm bằng chứng).

> Nguồn (v1.1) #1 — EMP-08 (§8.17.1, trang 51):
> "Trang cá nhân | Thống kê hiện 0 đơn đã giúp / 0 quà đã nhận; màn "Quà đã nhận" hiện "Chưa nhận được quà nào" | —"

> Nguồn (v1.1) #2 — AC-26.2.01 Then (§6.2, trang 27):
> "Thống kê hiển thị 0 đơn đã giúp và 0 quà đã nhận; màn "Quà đã nhận" hiển thị "Chưa nhận được quà nào"."

↳ **Ghi chú (diff):** `C-ORD-06` (home canonical ở module `ACT`) là CL **lan rộng nhất về số SC** — 5 màn / 6 SC — và từng bị revert vì lần chốt trước **không kèm bằng chứng**. Lần này bằng chứng là **tài liệu đã phê duyệt**, liệt kê đủ 8 empty state kèm text, ⇒ Resolved bền. Phần thuộc `GIFT` là `EMP-08`; ⇒ `SC-GIFT-008` hết `[GAP]`, assert verbatim `"Chưa nhận được quà nào"`. ⚠️ `EMP-08` **không có CTA** (cột CTA = `—`) — đây cũng là điều phải assert, vì `BR17-01` cho phép *tối đa* 1 CTA nên "không có" là một lựa chọn thiết kế cụ thể, không phải thiếu sót.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
