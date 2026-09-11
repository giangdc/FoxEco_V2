# Requirement Traceability — v1.0 · Module DLV

> Tạo bởi: analyze-requirements (INIT 2026-09-07) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation: FR/VR` ⇒ **Schema A**.
> 📌 Module chứa **ma trận nhãn nút × 5 trạng thái × 3 vai trò** (15 ô) — mục giá trị nhất của knowledge pack, hoàn toàn không có trong BRD/PRD.
> ⚠️ **3 REQ có gap SC chủ đích** (`PUP-03` ảnh hàng · `GPS-01` vị trí · `COST-01` chi phí) — nhánh phụ, PM chưa chốt scope ⇒ ghi ở `CHANGELOG §3`, ⛔ không tạo SC rác.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module DLV — DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-04 · DOC-v1.0-06

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-DLV-001 | `US-D09` | `DOC-v1.0-01` §D1b L178 · §D2 L232 · `DOC-v1.0-02` §3.6 | SC-DLV-016 | — |
| REQ-DLV-002 | — (không có ID doc gốc — ma trận từ `QA-obs` + Figma) | `DOC-v1.0-06` KP-01 §5.1 KB-DLV-01 · `DOC-v1.0-04` (15 ô, hash tiêu biểu `dc8cf987…`, `2e2ff7bc…`, `8563adc1…`, `19490aa9…`) | SC-DLV-001..015 | — |
| REQ-DLV-003 | — | `DOC-v1.0-06` KP-01 §5.1 (bảng popup) · `DOC-v1.0-02` §6 (L191) · §4.3 | SC-DLV-017, SC-DLV-018, SC-DLV-019, SC-DLV-020 | — |
| REQ-DLV-004 | `US-D09` | `DOC-v1.0-01` §D1b L178 | SC-DLV-021 | — |
| REQ-DLV-005 | `DLV-03`, `BR-INT-03`, `US-D14`, `US-D21` | `DOC-v1.0-01` §D3 L255 · §A5 L79 · §D1b L193 · L197 · `DOC-v1.0-02` §5.2 | SC-DLV-022 | C-DLV-01 |
| REQ-DLV-006 | — | `DOC-v1.0-02` §5.2 dòng "Sau khi xác nhận" | SC-DLV-023 | — |
| REQ-DLV-007 | `DLV-03`, `BR-CNF-04`, `US-D14` | `DOC-v1.0-01` §D3 L255 · §D4 L266 · §D1b L193 · §D5 L295 | SC-DLV-024 | — |
| REQ-DLV-008 | — | `DOC-v1.0-02` §5.3 · §7 dòng 11 · `DOC-v1.0-06` KP-01 §5 KB-DLV-03 | SC-DLV-025 | C-DLV-03 |
| REQ-DLV-009 | `US-D05`, `US-D08` | `DOC-v1.0-01` §D1b L167 · L177 · `DOC-v1.0-02` §3.6 · §4.3 · §5.2 | SC-DLV-026, SC-DLV-027, SC-DLV-028 | — |
| REQ-DLV-010 | `ORD-04`, `US-D09` | `DOC-v1.0-01` §D3 L243 · §D1b L178 · `DOC-v1.0-02` §3.6 dòng "Lịch sử" | SC-DLV-029 | — |
| REQ-DLV-011 | — | `DOC-v1.0-02` §3.6 dòng "Lộ trình" | — (gap có chủ đích: trùng `SC-FEED-009`) | C-FEED-01 |
| REQ-DLV-012 | `PUP-03`, `BR-CNF-01` | `DOC-v1.0-01` §D3 L250 · §D4 L265 · §D2 L213 | — (gap có chủ đích — `CHANGELOG §3`) | — |
| REQ-DLV-013 | `GPS-01` | `DOC-v1.0-01` §D3 L251 · §D2 L215 · §D5 L311 · `DOC-v1.0-06` KP-01 §5 KB-DLV-04 | — (gap có chủ đích — `CHANGELOG §3`) | C-DLV-02 |
| REQ-DLV-014 | `COST-01`, `BR-COST-01` | `DOC-v1.0-01` §D3 L256 · §D4 L267 · §A2 L15 | — (gap có chủ đích — `CHANGELOG §3`) | — |
| REQ-DLV-015 | `BR-ASN-03` | `DOC-v1.0-01` §D4 L264 · §D5 L294 · `DOC-v1.0-06` KP-01 §5 KB-DLV-05 | — (SC ở `CNL` — `SC-CNL-005`) | C-CNL-01 |
| REQ-DLV-016 | — | `DOC-v1.0-02` §3.6 · §4.3 · §5.2 (nhãn phụ theo vai) | SC-DLV-030 | — |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-DLV-001 · Thanh 5 mốc trạng thái
📍 `DOC-v1.0-01 §D1b US-D09 · L178` · `§D2 · L232` · `DOC-v1.0-02 §3.6`  ·  Clarif: —

> Nguồn #1 — `US-D09` (§D1b L178):
> "timeline theo dõi 5 mốc (Chờ ghép · Lấy hàng · Đang giao · Đã giao · Hoàn thành), mỗi bước ghi timestamp"

> Nguồn #2 — `DOC-v1.0-02` §3.6:
> "Thanh 5 bước trạng thái | Chờ ghép → Lấy hàng → Đang giao → Đã giao → Hoàn thành"

↳ **Ghi chú:** **2 nguồn đồng thuận** cả tên và thứ tự 5 mốc ⇒ assert được. ⚠️ **Bẫy thuật ngữ:** mốc thứ 2 là **"Lấy hàng"** nhưng trạng thái backend/badge là **"Đã ghép" (`MATCHED`)** — cùng một trạng thái, 2 chữ (`DOC-v1.0-06` KP-01 §5.1 ghi rõ). ⇒ ⛔ đừng đòi badge và thanh mốc cùng một chữ.

---

### REQ-DLV-002 · Ma trận nhãn nút × 5 trạng thái × 3 vai trò (15 ô)
📍 `DOC-v1.0-06 KP-01 §5.1 KB-DLV-01` · `DOC-v1.0-04` (15 ô có ảnh xác nhận)  ·  Clarif: —

> Nguồn — `DOC-v1.0-06` KP-01 §5.1 `KB-DLV-01` (trích 5 hàng trạng thái):
> "| 1 | **Chờ ghép** | `Đang chờ người vận chuyển nhận đơn` — disable<br>+ `Chỉnh sửa` / `Huỷ đơn` | `Tôi mang giúp được` — enable *(ở màn Chi tiết tin)* | `Đang chờ người vận chuyển nhận đơn` — disable<br>+ `Huỷ đơn` |"
> "| 2 | **Đã ghép**<br>*(stepper hiển thị "Lấy hàng")* | `Đã ghép · chờ shipper lấy hàng` — disable<br>+ `Huỷ đơn` | `✓ Tôi đã lấy hàng` — enable<br>+ `✕ Huỷ nhận đơn` (→ popup lý do bắt buộc) | `Đã có người vận chuyển · chờ lấy hàng` — disable<br>+ `Huỷ đơn` |"
> "| 3 | **Đang giao** | `Đang giao đến người nhận` — disable | `Đã giao cho người nhận` — enable | `✓ Đơn đang trên đường đến bạn` — disable |"
> "| 4 | **Đã giao** | `✓ Đã giao · chờ người nhận xác nhận` — disable | `✓ Đã giao · chờ người nhận xác nhận` — disable | `Xác nhận đã nhận hàng` — **enable (duy nhất)** |"
> "| 5 | **Hoàn thành** | `✓ Cảm ơn người vận chuyển` — enable<br>→ sau khi gửi quà đổi thành `Bạn đã đánh giá` (disable) | `✓ Đơn đã hoàn thành ✓` — disable | `Đơn đã hoàn thành ✓` — disable |"

↳ **Ghi chú:** ⭐ **Mục giá trị nhất của cả bộ knowledge pack** — *"hoàn toàn không có trong BRD/PRD/demo docx, do QA cung cấp từ testing trực tiếp rồi **đối chiếu xác nhận độc lập từng ô qua ảnh Figma** (mỗi ô có 1–3 ảnh xác nhận)"*. ⇒ Đủ 2 nguồn theo `§Custom Rules §10.1` ⇒ assert được **cả nhãn text và trạng thái enable/disable**. Fan-out **15 SC (1 ô = 1 SC)** theo Scenario Sufficiency Rule (mỗi role × mỗi state) — đây là fan-out lớn nhất dự án và là chỗ đợt cũ thiếu nhất (`DLV` đợt cũ chỉ có 14 SC cho **toàn module**). ⚠️ Ma trận **chỉ áp cho màn Theo dõi đơn** (role-aware), ⛔ KHÔNG áp cho màn Chi tiết tin public.

---

### REQ-DLV-003 · Popup xác nhận cho mọi hành động enable
📍 `DOC-v1.0-06 KP-01 §5.1 (bảng popup)` · `DOC-v1.0-02 §6 · L191` · `§4.3`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-06` KP-01 §5.1:
> "**Popup xác nhận** — mọi hành động "enable" của Carrier/Receiver đều đi qua 1 popup title cố định `Xác nhận` trước khi đổi trạng thái thật (không chuyển ngay khi bấm nút nền):"
> "| Carrier — Tôi đã lấy hàng | *"Bạn xác nhận đã lấy hàng từ người gửi và bắt đầu giao?"* |"
> "| Carrier — Đã giao cho người nhận | *"Bạn xác nhận đã giao hàng tận tay người nhận?"* |"
> "| Receiver — Xác nhận đã nhận hàng | *"Bạn xác nhận đã nhận được hàng từ người vận chuyển?"* |"

> Nguồn #2 — `DOC-v1.0-02` §6 (L191):
> "Mọi bước chuyển trạng thái (trừ bước đăng tin ban đầu) đều đi qua modal xác nhận 2 nút (Huỷ/Xác nhận) — không có bước nào tự động trôi mà không cần người dùng bấm xác nhận."

↳ **Ghi chú:** **2 nguồn đồng thuận** + **nguyên văn 3 popup** ⇒ assert được text. Fan-out 4 SC: 3 popup (mỗi popup 1 SC vì text khác nhau) + 1 SC nhánh **bấm Huỷ → không đổi trạng thái** (nhánh này quan trọng: mọi transition đều **không thể quay lại** sau khi xác nhận).

---

### REQ-DLV-004 · Thứ tự bắt buộc: "Tôi đã lấy hàng" trước "Đã giao"
📍 `DOC-v1.0-01 §D1b US-D09 · L178`  ·  Clarif: —

> "Không thể bấm "Đã giao" trước khi "Tôi đã lấy hàng"; timeline theo dõi 5 mốc (Chờ ghép · Lấy hàng · Đang giao · Đã giao · Hoàn thành), mỗi bước ghi timestamp"

↳ **Ghi chú:** Rule state-machine cơ bản. ⚠️ Trên UI, rule này **đã được thể hiện bằng ma trận nút** (`REQ-DLV-002`): ở trạng thái "Đã ghép" Carrier chỉ có nút *"Tôi đã lấy hàng"*, nút *"Đã giao"* **chưa tồn tại** ⇒ `SC-DLV-021` (P1) kiểm chứng **không có đường nào bỏ qua bước**, kể cả qua điều hướng khác. Nếu app cho nhảy bước thì đó là lỗi state-machine nghiêm trọng (đơn "đã giao" mà chưa từng lấy hàng).

---

### REQ-DLV-005 · CHỈ Receiver được xác nhận "Đã nhận hàng"
📍 `DOC-v1.0-01 §D3 DLV-03 · L255` · `§A5 BR-INT-03 · L79` · `§D1b US-D14 · L193` · `US-D21 · L197` · `DOC-v1.0-02 §5.2`  ·  Clarif: `C-DLV-01`

> Nguồn #1 — MÂU THUẪN (`DLV-03` §D3 L255):
> "DLV-03 | **RECEIVER/SENDER** xác nhận đã nhận | Quá N giờ chưa xác nhận → nhắc → admin hỗ trợ"

> Nguồn #2 — (`BR-INT-03` §A5 L79):
> "BR-INT-03 | Hoàn thành cần **người nhận** xác nhận đã nhận hàng; nếu không xác nhận → nhắc + admin hỗ trợ"

> Nguồn #3 — (`US-D21` §D1b L197):
> "**chỉ Receiver mới thấy & bấm được** "Xác nhận đã nhận hàng""

> Nguồn #4 — (`DOC-v1.0-02` §5.2):
> "⇒ Đây là quyền hạn ĐẶC BIỆT DUY NHẤT của vai trò Người nhận: chỉ Người nhận mới có thể chốt đơn "Hoàn thành" — Người vận chuyển chỉ đưa đơn tới "Đã giao" rồi phải chờ."

> Nguồn #5 — PHÁN QUYẾT (`DOC-v1.0-06` KP-01 §5 `KB-DLV-02`):
> "Ảnh Figma xác nhận nhất quán qua 5 ảnh: nút chỉ active với Receiver; Sender/Carrier cùng bước "Đã giao" chỉ thấy nhãn disabled."

↳ **Ghi chú:** ⭐ **BRD mâu thuẫn nội bộ:** `DLV-03` (§D3) ghi **RECEIVER/SENDER**, còn `BR-INT-03` (§A5) + `US-D21` + PRD §5.2 + **5 ảnh Figma** đều chốt **Receiver-only**. `C-DLV-01` Resolved 2026-07-24: **Receiver-only** (4 nguồn thắng 1). ⇒ `SC-DLV-022` (P1) assert Sender/Carrier **disable** ở trạng thái "Đã giao"; đã trùng khớp ô #4 của ma trận (`SC-DLV-010/011/012`) ⇒ `SC-DLV-022` là SC **bảo vệ kết luận** ở góc nhìn quyền hạn, không phải bản sao của ô ma trận.

---

### REQ-DLV-006 · Sau khi Receiver xác nhận → "Hoàn thành" NGAY
📍 `DOC-v1.0-02 §5.2 · bảng · dòng "Sau khi xác nhận"`  ·  Clarif: —

> "Sau khi xác nhận | Đơn chuyển "Hoàn thành" NGAY LẬP TỨC, lịch sử ghi "Hoàn thành & đã đánh giá""

↳ **Ghi chú:** ⚠️ Chuỗi lịch sử *"Hoàn thành & đã đánh giá"* nhắc **"đã đánh giá"** trong khi rating 1–5 sao đã bị `C-GIFT-01` loại khỏi v1.0 ⇒ đây là **UI leftover** cùng loại với `★★★★★` ở card `ACT` (`SC-ACT-013`). ⇒ `SC-DLV-023` assert trạng thái **"Hoàn thành" ngay lập tức** (không có bước chờ), ⛔ không assert chuỗi *"đã đánh giá"*.

---

### REQ-DLV-007 · Quá 2 giờ chưa xác nhận → nhắc; thêm 2 giờ → admin hỗ trợ
📍 `DOC-v1.0-01 §D4 BR-CNF-04 · L266` · `§D1b US-D14 · L193` · `§D3 DLV-03 · L255` · `§D5 · L295`  ·  Clarif: —

> Nguồn #1 — `BR-CNF-04` (§D4 L266):
> "BR-CNF-04 | RECEIVER không xác nhận 2 giờ → nhắc; thêm 2 giờ → admin hỗ trợ"

> Nguồn #2 — `US-D14` (§D1b L193):
> "Chỉ xác nhận được sau khi Carrier đã bấm "Đã giao"; quá 2 giờ không xác nhận → hệ thống nhắc, thêm 2 giờ → admin hỗ trợ"

> Nguồn #3 — `DOC-v1.0-01` §D5 L295:
> "Người nhận vắng mặt | "Đã giao" + ảnh hiện trường; 2 giờ không xác nhận → admin hỗ trợ"

↳ **Ghi chú:** **3 nguồn đồng thuận về mốc 2 giờ** (khác `DLV-03` chỉ ghi *"Quá N giờ"*). ⚠️ **Chi phí thực thi rất cao:** cần chờ **2 giờ** rồi **4 giờ** thực tế, hoặc nhờ dev đổi giờ hệ thống / seed timestamp. ⇒ `SC-DLV-024` viết dạng GAP/deferred: ghi rõ tiền đề thời gian, ⛔ không khai coverage nếu chưa chạy đủ mốc (xem `risk_assessment.md` `RISK-DLV-04`). Nhánh *"admin hỗ trợ"* chỉ verify được **hệ quả phía end-user** vì Admin Portal out of scope (`C-TS-01`).

---

### REQ-DLV-008 · Màn xác nhận nhận hàng dùng bản MODAL ĐƠN GIẢN
📍 `DOC-v1.0-02 §5.3` · `§7 dòng 11` · `DOC-v1.0-06 KP-01 §5 KB-DLV-03`  ·  Clarif: `C-DLV-03`

> Nguồn #1 — HAI BIẾN THỂ (`DOC-v1.0-02` §5.3):
> "Trong quá trình khảo sát, phát hiện thêm một biến thể đầy đủ hơn của hành động xác nhận nhận hàng… — có thể là bản thiết kế đầy đủ dự kiến, trong khi modal đơn giản ở Mục 5.2 là bản rút gọn"
> "Thông tin Carrier | Tên + đơn vị/phòng ban + điểm uy tín (vd: Trần Thị Lan, Marketing, ★4.9)"
> "Ảnh bằng chứng (khuyến nghị) | "Chụp ảnh hàng khi nhận — làm bằng chứng khi có tranh chấp""

> Nguồn #2 — PHÁN QUYẾT (`DOC-v1.0-06` KP-01 §5 `KB-DLV-03`):
> "BA/PO chốt **theo Figma = modal đơn giản** (`Xác nhận` / *"Bạn xác nhận đã nhận được hàng từ người vận chuyển?"* / 2 nút Huỷ–Xác nhận). Form đầy đủ **không áp dụng ở v1.0**."

↳ **Ghi chú:** `C-DLV-03` Resolved 2026-07-27: **modal đơn giản**; form đầy đủ (có ảnh bằng chứng + điểm uy tín carrier) **không áp dụng v1.0**. ⇒ `SC-DLV-025` assert modal đơn giản **và** assert **không có** ảnh bằng chứng/điểm uy tín. ⚠️ Form đầy đủ có **điểm uy tín ★4.9** — cùng nhóm với `C-USR-01` (điểm uy tín đã defer) ⇒ 2 clarification củng cố nhau.

---

### REQ-DLV-009 · Cụm liên hệ hiển thị theo vai trò
📍 `DOC-v1.0-01 §D1b US-D05 · L167` · `US-D08 · L177` · `DOC-v1.0-02 §3.6` · `§4.3` · `§5.2`  ·  Clarif: —

> Nguồn #1 — Sender (`DOC-v1.0-02` §3.6):
> "Liên hệ Người vận chuyển | Chỉ hiện sau khi ghép: tên + SĐT + nút Gọi"

> Nguồn #2 — Carrier (`DOC-v1.0-02` §4.3):
> "Liên hệ 2 phía | Hiển thị cả "NGƯỜI GỬI" và "NGƯỜI NHẬN" (tên + SĐT + nút Gọi) — vai trò trung gian cần liên hệ cả 2 đầu"

> Nguồn #3 — Receiver (`DOC-v1.0-02` §5.2):
> "Liên hệ | Sau khi ghép: chỉ hiện "NGƯỜI GIAO HÀNG" (tên carrier + SĐT + Gọi) — không hiện lại thông tin Người gửi"

> Nguồn #4 — (`US-D05` §D1b L167):
> "Thông tin người nhận hiển thị cố định trên màn Theo dõi đơn ở mọi trạng thái (MATCHED → IN_TRANSIT → DELIVERED)"

↳ **Ghi chú:** ⚠️ **`US-D05` xung đột với `§5.2`/`§3.6`:** `US-D05` nói **Sender** thấy *"thông tin người nhận… ở mọi trạng thái"*, nhưng `§3.6` (màn Sender) chỉ liệt kê cụm *"Liên hệ Người vận chuyển"*. Có thể cả 2 đúng (Sender thấy **cả** Carrier và Receiver) nhưng ⛔ không nguồn nào nói tường minh ⇒ `SC-DLV-026` assert **cụm Carrier** (có nguồn rõ) và ghi nhận thêm cụm Người nhận nếu có, không assert. Fan-out **3 SC (1/vai)** vì 3 vai có 3 tập cụm liên hệ khác nhau.

---

### REQ-DLV-010 · Lịch sử timeline mốc sự kiện
📍 `DOC-v1.0-02 §3.6 · dòng "Lịch sử"` · `DOC-v1.0-01 §D3 ORD-04 · L243` · `§D1b US-D09 · L178`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-02` §3.6:
> "Lịch sử | Timeline mốc sự kiện: Đăng tin → Ghép thành công → Lấy hàng → Đã giao → Hoàn thành"

> Nguồn #2 — `US-D09` (§D1b L178):
> "mỗi bước ghi timestamp"

↳ **Ghi chú:** ⚠️ **Danh sách mốc LỊCH SỬ khác danh sách 5 mốc TRẠNG THÁI**: Lịch sử bắt đầu bằng **"Đăng tin"** và có **"Ghép thành công"**, trong khi thanh trạng thái bắt đầu bằng *"Chờ ghép"* và mốc 2 là *"Lấy hàng"* ⇒ 2 danh sách khác nhau, ⛔ đừng dùng lẫn. Mốc **"Đăng tin"** đã có SC ở `ORD` (`SC-ORD-046`) ⇒ `SC-DLV-029` phủ các mốc **phát sinh theo state-transition** của giao nhận. Cross-ref `TS-01`/`TS-02` (log không sửa được) và ⚠️ `C-CNL-02` (huỷ đơn **hiện không ghi log**, thậm chí **xoá** dòng "Ghép thành công").

---

### REQ-DLV-011 · Lộ trình + khung bản đồ ở màn Theo dõi đơn
📍 `DOC-v1.0-02 §3.6 · dòng "Lộ trình"`  ·  Clarif: `C-FEED-01`

> "Lộ trình | Điểm Lấy hàng / Giao hàng + "Bản đồ · ~X km""

↳ **Ghi chú:** **Gap SC có chủ đích** — hành vi **trùng hoàn toàn** với khung bản đồ ở màn Chi tiết tin đã có `SC-FEED-009` (placeholder tĩnh, không assert `~X km`). Theo Scenario Sufficiency Rule (**trần: duplicate → không tạo SC rác**) ⇒ không tạo SC mới; ghi ở `CHANGELOG §3` để lượt sau biết đây là quyết định, không phải bỏ sót. Nếu `C-FEED-01(b)` chốt có bản đồ thật thì mở SC riêng cho màn này.

---

### REQ-DLV-012 · Chụp ảnh hàng lúc nhận (tuỳ chọn) — `PUP-03`
📍 `DOC-v1.0-01 §D3 PUP-03 · L250` · `§D4 BR-CNF-01 · L265` · `§D2 · L213`  ·  Clarif: —

> Nguồn #1 — `PUP-03` (§D3 L250):
> "PUP-03 | Chụp ảnh hàng lúc nhận | Tùy chọn (khuyến nghị) — lưu S3, gắn timeline làm bằng chứng"

> Nguồn #2 — `BR-CNF-01` (§D4 L265):
> "BR-CNF-01 | Ảnh hàng lúc nhận tùy chọn nhưng khuyến nghị mạnh — bằng chứng chính khi tranh chấp"

↳ **Ghi chú:** **Gap SC có chủ đích.** Lý do: **(a)** PM **chưa trả lời** luồng xác nhận nhận hàng có gồm ảnh bằng chứng hay không (`KP-05 §1` câu #2 — vẫn treo tới 2026-07-30); **(b)** `C-DLV-03` đã chốt màn xác nhận dùng **modal đơn giản không có ảnh bằng chứng** ⇒ bề mặt để chụp ảnh **có thể không tồn tại ở v1.0**; **(c)** ma trận `KB-DLV-01` (15 ô, có ảnh Figma) **không thấy** nút chụp ảnh ở bất kỳ ô nào. ⇒ Theo `§Custom Rules §10.1`, ⛔ không viết SC khẳng định; ghi nợ ở `CHANGELOG §3` chờ PM chốt scope.

---

### REQ-DLV-013 · Chia sẻ vị trí khi đang giao — `GPS-01`
📍 `DOC-v1.0-01 §D3 GPS-01 · L251` · `§D2 · L215` · `§D5 · L311` · `DOC-v1.0-06 KP-01 §5 KB-DLV-04`  ·  Clarif: `C-DLV-02`

> Nguồn #1 — `GPS-01` (§D3 L251):
> "GPS-01 | Chia sẻ vị trí khi đang giao | Tùy chọn; chỉ active khi đang giao; xóa sau khi đóng"

> Nguồn #2 — `DOC-v1.0-01` §D5 L311 (chính BRD tự hỏi):
> "Chia sẻ vị trí mặc định bật/tắt?"

> Nguồn #3 — `DOC-v1.0-06` KP-01 §5 `KB-DLV-04`:
> "BRD tự nêu câu hỏi mở. BA/PO trả lời "phase sau" nhưng **chưa cho giá trị cụ thể**."

↳ **Ghi chú:** **Gap SC có chủ đích.** `C-DLV-02` **Open (non-blocking)**: BA nói *"phase sau"* nhưng chưa cho giá trị mặc định bật/tắt. Cộng thêm: ma trận `KB-DLV-01` ở trạng thái **"Đang giao"** (ô #3) chỉ có nút *"Đã giao cho người nhận"* của Carrier — **không có** control chia sẻ vị trí ⇒ bề mặt có thể không tồn tại. ⇒ ⛔ không viết SC khẳng định; ghi nợ `CHANGELOG §3`.

---

### REQ-DLV-014 · Ghi nhận chi phí đối soát offline — `COST-01`
📍 `DOC-v1.0-01 §D3 COST-01 · L256` · `§D4 BR-COST-01 · L267` · `§A2 NT-03 · L15`  ·  Clarif: —

> Nguồn #1 — `COST-01` (§D3 L256):
> "COST-01 | (Tùy chọn) ghi nhận chi phí | Bản ghi tham khảo; app KHÔNG thanh toán; đối soát offline"

> Nguồn #2 — `BR-COST-01` (§D4 L267):
> "BR-COST-01 | App không xử lý tiền; chỉ ghi con số hai bên tự khai (tùy chọn)"

> Nguồn #3 — `NT-03` (§A2 L15):
> "KHÔNG có thanh toán | Không ví, không cổng thanh toán. Chi phí (nếu có) hai bên tự đối soát offline; app chỉ ghi nhận (tùy chọn)"

↳ **Ghi chú:** **Gap SC có chủ đích.** 3 nguồn đồng thuận về **nguyên tắc** (app không xử lý tiền) nhưng **không nguồn nào mô tả bề mặt UI** để ghi nhận con số; ma trận `KB-DLV-01` và 82 ảnh Figma **không có** màn/field nhập chi phí. Đây cũng thuộc câu hỏi treo `KP-05 §1` #2 (nhánh phụ DLV). ⇒ ⛔ không viết SC khẳng định; ghi nợ `CHANGELOG §3`.

---

### REQ-DLV-015 · Sau khi lấy hàng (IN_TRANSIT) không huỷ thường → tạo sự cố
📍 `DOC-v1.0-01 §D4 BR-ASN-03 · L264` · `§D5 · L294` · `DOC-v1.0-06 KP-01 §5 KB-DLV-05`  ·  Clarif: `C-CNL-01`

> Nguồn #1 — `BR-ASN-03` (§D4 L264):
> "BR-ASN-03 | Sau khi nhận hàng (IN_TRANSIT) không hủy thường → phải tạo sự cố"

> Nguồn #2 — `DOC-v1.0-01` §D5 L294:
> "Sau khi nhận, hàng hỏng/mất | Tạo sự cố, không cho COMPLETED thường; dùng timeline + ảnh làm bằng chứng"

> Nguồn #3 — `DOC-v1.0-06` KP-01 §5 `KB-DLV-05`:
> "Màn "Báo sự cố" chưa có đặc tả — out of scope v1.0"

↳ **Ghi chú:** REQ thuộc ranh giới `DLV` ⟷ `CNL`. **SC nằm ở `CNL`** (`SC-CNL-005`: không huỷ được từ "Đang giao" trở đi) vì hành động là **huỷ**; còn nhánh *"phải tạo sự cố"* thì màn "Báo sự cố" **out of scope v1.0** (`C-CNL-01` Resolved) ⇒ chỉ assert được **vế chặn huỷ**, ⛔ không assert luồng tạo sự cố. Ghi ở đây để traceability không đứt.

---

### REQ-DLV-016 · Nhãn phụ màn Theo dõi đơn theo vai trò
📍 `DOC-v1.0-02 §3.6` · `§4.3` · `§5.2` (tiêu đề section)  ·  Clarif: —

> "3.6. Màn hình Theo dõi đơn (nhãn phụ "Tôi gửi hàng")"
> "4.3. Màn hình Theo dõi đơn (nhãn phụ "Tôi giao hàng")"
> "5.2. Màn hình Theo dõi đơn (nhãn phụ "Tôi nhận hàng") — hành động chính của vai trò này"

↳ **Ghi chú:** Nguồn là **3 tiêu đề section** của PRD (không phải nội dung bảng) ⇒ neo bằng heading. 3 nhãn cho 3 vai: `Tôi gửi hàng` · `Tôi giao hàng` · `Tôi nhận hàng`. Đây là **cách nhanh nhất để tester biết đang xem bằng vai nào** ⇒ hữu ích làm oracle phụ cho 15 SC ma trận. Gộp 1 SC (`SC-DLV-030`) với 3 nhánh vai trong Then vì cùng 1 hành vi hiển thị nguyên tử.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
