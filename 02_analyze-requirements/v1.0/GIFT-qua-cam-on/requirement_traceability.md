# Requirement Traceability — v1.0 · Module GIFT

> Tạo bởi: analyze-requirements (INIT 2026-09-07) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation: FR/VR` ⇒ **Schema A**.
> 📌 **"Đánh giá" trong scope Phase 1 của PM = Quà ảo** (`C-GIFT-01` Resolved) — không phải chấm sao.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module GIFT — DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-04 · DOC-v1.0-06

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-GIFT-001 | `GIFT-01`, `US-D15` | `DOC-v1.0-01` §D3 L258 · §A7 L107-108 · §D1b L194 · `DOC-v1.0-02` §3.8 | SC-GIFT-001, SC-GIFT-002 | — |
| REQ-GIFT-002 | `BR-GIFT-01`, `BR-INT-06`, `US-D15` | `DOC-v1.0-01` §D4 L271 · §A5 L82 · §A7 L109/L111 · §D1b L194 · `DOC-v1.0-02` §3.8 | SC-GIFT-003, SC-GIFT-004 | — |
| REQ-GIFT-003 | — (không có ID doc gốc — phát hiện từ `QA-obs` + Figma) | `DOC-v1.0-06` KP-01 §6 KB-GIFT-01 · KP-01 §5.1 (ô 5·Sender) | SC-GIFT-005 | — |
| REQ-GIFT-004 | `US-D20` | `DOC-v1.0-01` §D1b L196 · §A7 L110 · `DOC-v1.0-06` KP-01 §6 KB-GIFT-03 | SC-GIFT-006, SC-GIFT-007 | C-GIFT-03 |
| REQ-GIFT-005 | `RAT-01/02` | `DOC-v1.0-01` §D3 L256 · §A5 L82 · §A8 L125 · `DOC-v1.0-06` KP-01 §6 KB-GIFT-02 | SC-GIFT-011 | C-GIFT-01 |
| REQ-GIFT-006 | — | `DOC-v1.0-06` KP-01 §6 KB-GIFT-03 · KB-GIFT-04 | SC-GIFT-009, SC-GIFT-010 | C-GIFT-02 |
| REQ-GIFT-007 | — | `DOC-v1.0-06` KP-02 §5 dòng `C-ORD-06` | SC-GIFT-008 | C-ORD-06 |
| REQ-GIFT-008 | `NTF-07` | `DOC-v1.0-01` §D6 L325 · §A7 L109 · §D1b L194 | SC-GIFT-012 | C-NTF-01 |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-GIFT-001 · Tặng quà cảm ơn Carrier — 4 loại quà, sau khi Hoàn thành
📍 `DOC-v1.0-01 §D3 GIFT-01 · L258` · `§A7 · L107-108` · `§D1b US-D15 · L194` · `DOC-v1.0-02 §3.8`  ·  Clarif: —

> Nguồn #1 — `GIFT-01` (§D3 L258):
> "GIFT-01 | Tặng quà cảm ơn Carrier | 4 loại quà phi vật chất (KHÔNG thanh toán); gửi không cần xác nhận; tổng hợp ở "Quà đã nhận""

> Nguồn #2 — `DOC-v1.0-01` §A7 L107-108:
> "Sau khi đơn hoàn tất, người gửi tặng quà ảo cảm ơn người vận chuyển"
> "4 loại quà: bông hoa, ly cà phê, gấu bông, vương miện — biểu tượng phi vật chất"

> Nguồn #3 — `DOC-v1.0-02` §3.8:
> "4 lựa chọn quà: 🌷 Bông hoa · ☕ Ly cà phê · 🧸 Gấu bông · 👑 Vương miện."

↳ **Ghi chú:** **3 nguồn đồng thuận** cả số lượng (4) và **danh mục tên quà** ⇒ assert được. Tiền đề: đơn phải ở **"Hoàn thành"** (`§A7` L107) ⇒ phụ thuộc `SC-DLV-023` (Receiver xác nhận → Hoàn thành ngay); nếu SC đó FAIL thì cả module `GIFT` bị blocked. Bề mặt nút mở màn Tặng quà = ô 5·Sender của ma trận (`SC-DLV-013`).

---

### REQ-GIFT-002 · Gửi ngay không cần xác nhận, không quy đổi tiền
📍 `DOC-v1.0-01 §D4 BR-GIFT-01 · L271` · `§A5 BR-INT-06 · L82` · `§A7 · L109/L111` · `§D1b US-D15 · L194` · `DOC-v1.0-02 §3.8`  ·  Clarif: —

> Nguồn #1 — `BR-GIFT-01` (§D4 L271):
> "BR-GIFT-01 | Quà cảm ơn là biểu tượng phi vật chất, không quy đổi tiền, không qua thanh toán in-app"

> Nguồn #2 — `DOC-v1.0-01` §A7 L109:
> "Gửi ngay, không cần bước xác nhận; người nhận thấy thông báo "Bạn nhận được một món quà cảm ơn""

> Nguồn #3 — `US-D15` (§D1b L194):
> "chọn quà → gửi ngay không cần bước xác nhận → popup "Cảm ơn của bạn đã được gửi" → nút "Về trang chủ"; Carrier nhận thông báo "Bạn nhận được một món quà cảm ơn" → mở Trang cá nhân"

> Nguồn #4 — `DOC-v1.0-02` §3.8:
> "Xác nhận → modal "Đã gửi lời cảm ơn!" — tính năng tương tác xã hội, không bắt buộc."

↳ **Ghi chú:** ⚠️ **Hai nguồn cho 2 text popup khác nhau:** `US-D15` = *"Cảm ơn của bạn đã được gửi"* ⟷ PRD §3.8 + Figma (`KB-GIFT-01`) = *"Đã gửi lời cảm ơn!"* ⇒ lệch câu chữ; chốt theo **PRD + Figma** (2 nguồn bề mặt), mở `C-GIFT-03`. ⚠️ Cũng lệch về **luồng**: `US-D15` nói *"gửi ngay không cần bước xác nhận"* nhưng PRD §3.8 lại có bước *"Xác nhận →"* ⇒ hiểu đúng: **không cần Carrier xác nhận** (không phải không cần Sender xác nhận). Vế *"không quy đổi tiền"* → `SC-GIFT-004` assert-absent.

---

### REQ-GIFT-003 · Nút đổi nhãn "Cảm ơn người vận chuyển" → "Bạn đã đánh giá"
📍 `DOC-v1.0-06 KP-01 §6 KB-GIFT-01` · `KP-01 §5.1 (ô 5·Sender)`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-06` KP-01 §6 `KB-GIFT-01`:
> "Ở trạng thái Hoàn thành, Sender thấy nút `✓ Cảm ơn người vận chuyển` (enable). Sau khi chọn 1 loại quà và gửi thành công, nút **đổi nhãn thành `Bạn đã đánh giá` (disable, không gửi lại được)**."
> "Nguồn: `QA-obs` 2026-07-24 + `Figma` (popup *"Đã gửi lời cảm ơn!"*) — **phát hiện mới, chưa từng có ở BRD/PRD/demo**"

> Nguồn #2 — `DOC-v1.0-06` KP-01 §5.1 (ma trận, ô 5·Sender):
> "`✓ Cảm ơn người vận chuyển` — enable<br>→ sau khi gửi quà đổi thành `Bạn đã đánh giá` (disable)"

↳ **Ghi chú:** **Phát hiện hoàn toàn ngoài tài liệu** (`QA-obs` + Figma), đợt cũ đã sinh REQ riêng cho nó (`REQ-GIFT-003` cũ). Rule mang **2 hệ quả nghiệp vụ**: (a) **chỉ gửi quà được 1 lần / đơn** (nút disable sau khi gửi); (b) nhãn *"Bạn đã đánh giá"* dùng từ **"đánh giá"** cho hành động **tặng quà** ⇒ củng cố `C-GIFT-01` (v1.0 dùng quà ảo **thay cho** chấm sao). ⛔ Không hiểu nhãn này là có tính năng rating.

---

### REQ-GIFT-004 · Màn "Quà đã nhận" — card đếm có điều kiện + lịch sử
📍 `DOC-v1.0-01 §D1b US-D20 · L196` · `§A7 · L110` · `DOC-v1.0-06 KP-01 §6 KB-GIFT-03`  ·  Clarif: `C-GIFT-03`

> Nguồn #1 — `US-D20` (§D1b L196):
> "màn Quà đã nhận hiển thị 1 card đếm số bông hoa/ly cà phê/gấu bông/vương miện + danh sách lịch sử nhận quà"

> Nguồn #2 — `DOC-v1.0-01` §A7 L110:
> "Trang cá nhân tổng hợp tổng số đơn đã giúp + số quà ảo đã nhận (đếm theo loại) + lịch sử nhận quà"

> Nguồn #3 — `DOC-v1.0-06` KP-01 §6 `KB-GIFT-03`:
> "Card đếm theo 4 loại quà… nhưng **chỉ hiển thị loại đã thực sự nhận (count > 0)** — loại chưa nhận lần nào thì **không load, không hiện dạng "0"**."
> "⚠ Thành phần "Danh sách lịch sử" **chỉ có bằng chứng văn bản US-D20**, chưa có ảnh Figma/app → **cần vibe-test xác nhận**. Nếu app không có → mở clarification, không im lặng bỏ qua."

↳ **Ghi chú:** ⚠️ **Hai mức bằng chứng khác nhau trong cùng REQ:** **card đếm** có `QA-obs` xác nhận (kèm rule *"chỉ hiện loại count > 0"* — trái với hiểu ban đầu là luôn hiện đủ 4 loại) ⇒ assert được; **danh sách lịch sử** chỉ có **1 nguồn văn bản** (`US-D20`), chưa có ảnh/app ⇒ theo `§Custom Rules §10.1` chỉ được SC dạng ghi nhận (`SC-GIFT-007`) + `C-GIFT-03`.

---

### REQ-GIFT-005 · Rating 1–5 sao — out of scope v1.0
📍 `DOC-v1.0-01 §D3 RAT-01/02 · L256` · `§A5 BR-INT-06 · L82` · `§A8 · L125` · `DOC-v1.0-06 KP-01 §6 KB-GIFT-02`  ·  Clarif: `C-GIFT-01`

> Nguồn #1 — MÂU THUẪN (`RAT-01/02` §D3 L256):
> "RAT-01/02 | Đánh giá 2 chiều | 1–5 sao + nhận xét"

> Nguồn #2 — (`BR-INT-06` §A5 L82):
> "BR-INT-06 | **Không đánh giá sao**; ghi nhận thiện chí bằng quà ảo người gửi tặng người vận chuyển sau khi hoàn tất"

> Nguồn #3 — (`DOC-v1.0-01` §A8 L125):
> "Phạm vi hiện tại: chỉ ghi log + admin can thiệp hỗ trợ. **KHÔNG có chấm sao/đánh giá**, KHÔNG có chặn (block) người dùng."

> Nguồn #4 — PHÁN QUYẾT (`DOC-v1.0-06` KP-01 §6 `KB-GIFT-02`):
> "BA/PO xác nhận: **phase sau** — v1.0 chỉ có Quà ảo (`GIFT-01`), chưa có màn chấm sao. Chuỗi `★★★★★ Đã đánh giá` trên card là UI leftover."

↳ **Ghi chú:** ⭐ **BRD mâu thuẫn nội bộ 3-1:** `RAT-01/02` (§D3) ghi có rating 1–5 sao; `BR-INT-06` (§A5) + `§A8` (L125) + `§A7` (L111) đều nói **không có chấm sao**. `C-GIFT-01` Resolved 2026-07-27: **out of scope v1.0**. ⇒ 📌 **Hệ quả scope quan trọng nhất:** *"Đánh giá"* trong 5 luồng Phase 1 của PM = **Quà ảo**, không phải chấm sao (`KP-03 §3`). `SC-GIFT-011` là GAP finding assert-absent màn chấm sao.

---

### REQ-GIFT-006 · Điều hướng màn "Quà đã nhận" và màn "Tặng quà"
📍 `DOC-v1.0-06 KP-01 §6 KB-GIFT-03` · `KB-GIFT-04`  ·  Clarif: `C-GIFT-02`

> Nguồn #1 — `KB-GIFT-03`:
> "Ngoài ra có `Danh sách lịch sử` nhận quà và icon quay lại ở header (→ về màn Cá nhân)."

> Nguồn #2 — `KB-GIFT-04` (🔴 nghi vấn bug):
> "Bấm back (←) từ màn "Tặng quà" (mở từ item mẫu tab "Đã hoàn thành") nhảy tới màn "Xác nhận đã nhận hàng" của **một đơn KHÁC không liên quan**, thay vì quay về "Đơn của tôi"."
> "Clarification: `C-GIFT-02` Open — nhiều khả năng là giới hạn của bản demo (item mẫu tĩnh chưa wiring back-stack), CA đánh giá không nghiêm trọng."

↳ **Ghi chú:** Hai hành vi back khác nhau: **màn "Quà đã nhận"** → về Cá nhân (`QA-obs`, hành vi đúng) và **màn "Tặng quà"** → nhảy sai màn (nghi vấn bug, `C-GIFT-02` Open). ⚠️ Ngữ cảnh phát hiện là *"item mẫu tab Đã hoàn thành"* của bản demo ⇒ có thể là **giới hạn demo**, cần verify trên app STG với đơn thật ⇒ `SC-GIFT-010` ghi nhận, ⛔ không kết luận bug ngay.

---

### REQ-GIFT-007 · Empty state màn "Quà đã nhận"
📍 `DOC-v1.0-06 KP-02 §5 · dòng "C-ORD-06"`  ·  Clarif: `C-ORD-06`

> "**C-ORD-06** | Empty state của 3 màn (Hoạt động · **Quà đã nhận** · Thông báo) khi không có data"

↳ **Ghi chú:** *(Implicit — không có quote đặc tả text.)* Màn "Quà đã nhận" là **màn thứ hai** trong danh sách `C-ORD-06` (home canonical ở `ACT`). ⚠️ Ở module này empty state **đặc biệt dễ gặp**: rule *"chỉ hiện loại count > 0"* (`KB-GIFT-03`) nghĩa là tài khoản chưa nhận quà nào thì **cả 4 loại đều không load** ⇒ màn rỗng hoàn toàn. `SC-GIFT-008` ghi nhận, ⛔ không assert text.

---

### REQ-GIFT-008 · Thông báo cho Carrier khi nhận quà (`NTF-07`)
📍 `DOC-v1.0-01 §D6 NTF-07 · L325` · `§A7 · L109` · `§D1b US-D15 · L194`  ·  Clarif: `C-NTF-01`

> Nguồn #1 — `NTF-07` (§D6 L325):
> "NTF-07 | Người gửi tặng quà ảo | Người vận chuyển | "Bạn nhận được một món quà cảm ơn 🎁 — mở Trang cá nhân để xem""

> Nguồn #2 — `DOC-v1.0-01` §A7 L109:
> "người nhận thấy thông báo "Bạn nhận được một món quà cảm ơn""

> Nguồn #3 — `DOC-v1.0-06` KP-07 (bảng unified, hàng #7):
> "Figma thực tế: "Bạn nhận được một món quà cảm ơn 🎁" — "[Tên] đã gửi tặng bạn một món quà..." (khớp gần BRD)"

↳ **Ghi chú:** **3 nguồn gần đồng thuận text** ⇒ assert được phần đầu câu. `KP-07` xếp hàng #7 là *"Dùng cho REQ-GIFT-001 (trong scope v1.0)"* — tức đây là **1 trong ít loại thông báo không bị tranh chấp** của `C-NTF-01`. SC ở đây phủ **hệ quả của hành động tặng quà**; cơ chế màn Thông báo (nhóm thời gian, chấm đỏ, phân trang) thuộc `NTF`.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
