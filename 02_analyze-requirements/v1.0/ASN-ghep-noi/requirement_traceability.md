# Requirement Traceability — v1.0 · Module ASN

> Tạo bởi: analyze-requirements (INIT 2026-09-07) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation: FR/VR` ⇒ **Schema A**.
> ⚠️ **Ranh giới với `FEED`:** file này phủ **rule ghép nối** (engine + state-transition). Bề mặt hiển thị Bảng tin/Chi tiết tin (gồm 2 bug lộ SĐT / CTA với chủ tin) thuộc `FEED`.
> 📌 **Module rủi ro cao nhất dự án** — chứa rule cạnh tranh (double-accept), rule bảo mật liên hệ, và engine auto-match chưa chốt tham số.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module ASN — DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-06

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-ASN-001 | `ASN-01`, `BR-CON-01`, `US-D07` | `DOC-v1.0-01` §D3 L247 · §A5 L77 · §D1b L176 · `DOC-v1.0-02` §4.2 | SC-ASN-001, SC-ASN-002, SC-ASN-003 | — |
| REQ-ASN-002 | `BR-CON-02`, `OPR-07`, `US-D08` | `DOC-v1.0-01` §A5 L78 · §D7 L343 · §D1b L177 | SC-ASN-004, SC-ASN-005 | C-ASN-01 |
| REQ-ASN-003 | `ASN-03`, `OPR-03` | `DOC-v1.0-01` §D3 L249 · §D7 L339 · §D5 L293 | SC-ASN-006 | — |
| REQ-ASN-004 | `OPR-03`, `OPR-08` | `DOC-v1.0-01` §D7 L339 · L344 | SC-ASN-007 | — |
| REQ-ASN-005 | `BR-INT-05` | `DOC-v1.0-02` §4.2 · `DOC-v1.0-01` §A5 L81 | SC-ASN-008 | — |
| REQ-ASN-006 | `MTCH-01`, `BR-MTCH-01`, `US-D12`, `US-D13` | `DOC-v1.0-01` §D3 L254 · §D4 L270 · §D1b L186-187 | SC-ASN-009, SC-ASN-010 | C-NTF-02 |
| REQ-ASN-007 | `OPR-02` | `DOC-v1.0-01` §D7 L338 · `DOC-v1.0-06` KP-01 §4 KB-ASN-04 | SC-ASN-011 | C-NTF-02 |
| REQ-ASN-008 | `OPR-01`, `OPR-06` | `DOC-v1.0-01` §D7 L337 · L342 · `DOC-v1.0-06` KP-01 §4 KB-ASN-03 | SC-ASN-013, SC-ASN-014 | C-NTF-02 |
| REQ-ASN-009 | `OPR-04` | `DOC-v1.0-01` §D7 L340 | SC-ASN-015, SC-ASN-016 | — |
| REQ-ASN-010 | `OPR-05` | `DOC-v1.0-01` §D7 L341 · `DOC-v1.0-06` KP-01 §4 KB-ASN-02 | SC-ASN-012 | C-ASN-02 |
| REQ-ASN-011 | `OPR-08`, `OPR-09` | `DOC-v1.0-01` §D7 L344 · L345 | SC-ASN-017 | — |
| REQ-ASN-012 | — | `DOC-v1.0-06` KP-01 §4 KB-ASN-05 · KP-02 §5 | SC-ASN-018 | C-ASN-03 |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-ASN-001 · Bấm "Tôi mang giúp được" → ghép NGAY (không cần chủ tin duyệt)
📍 `DOC-v1.0-01 §D3 ASN-01 · L247` · `§A5 BR-CON-01 · L77` · `§D1b US-D07 · L176` · `DOC-v1.0-02 §4.2`  ·  Clarif: —

> Nguồn #1 — `ASN-01` (§D3 L247):
> "ASN-01 | Bày tỏ quan tâm / đề nghị mang giúp | Gửi tới chủ tin push + in-app"

> Nguồn #2 — `BR-CON-01` (§A5 L77):
> "BR-CON-01 | Người B bấm "Tôi mang giúp được" → hệ thống ghép ngay, không cần bước chủ tin duyệt"

> Nguồn #3 — `DOC-v1.0-02` §4.2:
> "Bấm "Tôi mang giúp được" → hiện modal xác nhận:"
> "Modal "Xác nhận mang giúp" — SĐT hai bên sẽ được lộ sau khi xác nhận"
> "Bấm Xác nhận → đơn chuyển trạng thái "Đã ghép""

↳ **Ghi chú:** ⚠️ **BRD mâu thuẫn nội bộ về cơ chế ghép.** `BR-CON-01` + `§A5` sơ đồ L62-64 nói **ghép NGAY, không cần chủ tin duyệt**; nhưng `ASN-02` (§D3 L248) nói *"Chủ tin chấp nhận 1 người"* và `§D2` L209 vẽ bước *"[SENDER] Xem hồ sơ tin cậy CARRIER → "Chấp nhận""*. `DOC-v1.0-02` §4.2 (bề mặt thật) khớp `BR-CON-01`: chỉ có **modal xác nhận của chính Carrier**, không có bước duyệt của Sender. ⇒ Chốt theo `BR-CON-01` + PRD; ghi lệch vào `CHANGELOG §2`. Fan-out 3 SC: hành động+modal · nhánh Huỷ modal · ghép ngay không cần duyệt.

---

### REQ-ASN-002 · Lộ SĐT sau ghép — đúng 2 người trong cặp
📍 `DOC-v1.0-01 §A5 BR-CON-02 · L78` · `§D7 OPR-07 · L343` · `§D1b US-D08 · L177`  ·  Clarif: `C-ASN-01`

> Nguồn #1 — `BR-CON-02` (§A5 L78):
> "BR-CON-02 | Sau khi ghép: lộ SĐT + kênh liên hệ cho đúng 2 người trong cặp ghép; trước khi ghép không lộ SĐT"

> Nguồn #2 — `OPR-07` (§D7 L343):
> "OPR-07 | Lộ liên hệ có kiểm soát | SĐT chỉ lộ sau khi ghép, chỉ cho đúng 2 người trong cặp; không đưa SĐT vào nội bộ push"

> Nguồn #3 — `US-D08` (§D1b L177):
> "Sau MATCHED, màn Theo dõi đơn gom 2 cụm "Người gửi" & "Người nhận" (tên/SĐT/địa chỉ) hiển thị xuyên suốt tới khi hoàn tất; SĐT chỉ lộ sau khi ghép"

↳ **Ghi chú:** **3 nguồn đồng thuận** — rule bảo mật mạnh nhất dự án. Hai chiều kiểm tra: **(a)** sau ghép, 2 người trong cặp **thấy** SĐT (`SC-ASN-004`); **(b)** người thứ ba **không thấy** (`SC-ASN-005`). ⚠️ Vế *"trước khi ghép không lộ"* đã có **bằng chứng app vi phạm** ở màn Chi tiết tin — SC bắt lỗi đó nằm ở `FEED` (`SC-FEED-010`), ⛔ không nhân bản sang đây. Lưu ý `US-D08` gom **"Người gửi" & "Người nhận"** cho Carrier — tức Carrier thấy SĐT của **2 đầu**, khác Sender/Receiver chỉ thấy 1 đầu (chi tiết ở `DLV` `REQ-DLV-009`).

---

### REQ-ASN-003 · 1 tin — 1 cặp ghép, chống double-accept
📍 `DOC-v1.0-01 §D3 ASN-03 · L249` · `§D7 OPR-03 · L339` · `§D5 · L293`  ·  Clarif: —

> Nguồn #1 — `ASN-03` (§D3 L249):
> "ASN-03 | Chống ghép trùng | 1 tin chỉ 1 cặp active (DB constraint + tx lock)"

> Nguồn #2 — `OPR-03` (§D7 L339):
> "OPR-03 | 1 tin — 1 cặp ghép | Ghép ngay cho người bấm "Tôi mang giúp được" đầu tiên; ngay khi có người nhận, tin bị ẩn khỏi bảng tin và không ai bấm "Tôi mang giúp được" được nữa (chống double-accept)"

> Nguồn #3 — `DOC-v1.0-01` §D5 L293:
> "Nhiều người cùng nhận 1 tin | Chủ tin chọn; chống double-accept bằng tx lock"

↳ **Ghi chú:** ⚠️ **Nguồn #3 lệch cơ chế:** `§D5` nói *"Chủ tin chọn"* (có bước duyệt) trong khi `OPR-03` nói *"ghép ngay cho người bấm đầu tiên"* — cùng một mâu thuẫn với `REQ-ASN-001`. Chốt theo `OPR-03` (**first-come**). Đây là SC **khó thực thi nhất dự án**: cần 2 Carrier bấm **gần đồng thời** ⇒ 2 thiết bị/2 phiên + phối hợp thời điểm (xem `risk_assessment.md` `RISK-ASN-02`).

---

### REQ-ASN-004 · Tin ẩn khỏi bảng tin và khỏi luồng gợi ý sau khi ghép
📍 `DOC-v1.0-01 §D7 OPR-03 · L339` · `OPR-08 · L344`  ·  Clarif: —

> Nguồn #1 — `OPR-03` (§D7 L339):
> "ngay khi có người nhận, tin bị ẩn khỏi bảng tin và không ai bấm "Tôi mang giúp được" được nữa"

> Nguồn #2 — `OPR-08` (§D7 L344):
> "OPR-08 | Vòng đời tin trong luồng khớp | Tin đang MATCHED/IN_TRANSIT không xuất hiện ở gợi ý cho carrier khác; tin huỷ bởi carrier quay lại "Chờ ghép" và được khớp lại"

↳ **Ghi chú:** Hai bề mặt của cùng rule: **bảng tin** (`OPR-03`) và **luồng gợi ý/thông báo khớp** (`OPR-08`) ⇒ `SC-ASN-007` phủ cả 2 bề mặt trong 1 SC vì cùng 1 hành vi nguyên tử (tin rời khỏi tập khả dụng). ⚠️ Hệ quả cho `FEED`: bảng tin **có thể rỗng** dù hệ thống đang nhiều đơn (đã ghi ở `FEED/CHANGELOG §2` ràng buộc 7).

---

### REQ-ASN-005 · Đồng bộ realtime 3 vai khi ghép
📍 `DOC-v1.0-02 §4.2` · `DOC-v1.0-01 §A5 BR-INT-05 · L81`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-02` §4.2:
> "Bấm Xác nhận → đơn chuyển trạng thái "Đã ghép"; CẢ 3 khung (Người gửi / Người vận chuyển / Người nhận) đổi trạng thái tức thời — đây là điểm nhấn chính của bản demo (đồng bộ dữ liệu thời gian thực)."

> Nguồn #2 — `BR-INT-05` (§A5 L81):
> "BR-INT-05 | Huỷ sau khi MATCHED phải có lý do (bắt buộc), ghi rõ ai huỷ + **đồng bộ realtime cả 3 bên**"

↳ **Ghi chú:** ⚠️ **Cẩn trọng nguồn:** câu của `DOC-v1.0-02` mô tả **điểm nhấn của bản demo** — và bản demo *"chỉ mô phỏng MỘT đơn hàng duy nhất cho cả 3 khung xem cùng lúc"* (`§1.4`), tức 3 khung là 3 view của **cùng 1 state trong bộ nhớ**, không chứng minh được đồng bộ **qua backend giữa 3 thiết bị thật**. `BR-INT-05` yêu cầu realtime nhưng cho **luồng huỷ**. ⇒ `SC-ASN-008` viết theo yêu cầu nghiệp vụ, ghi rõ cần **3 phiên/thiết bị khác nhau** để thực sự kiểm chứng.

---

### REQ-ASN-006 · Auto-match tuyến OFFER ↔ tin NEED
📍 `DOC-v1.0-01 §D3 MTCH-01 · L254` · `§D4 BR-MTCH-01 · L270` · `§D1b US-D12/US-D13 · L186-187`  ·  Clarif: `C-NTF-02`

> Nguồn #1 — `MTCH-01` (§D3 L254):
> "MTCH-01 | Tự khớp tuyến OFFER ↔ NEED | Trùng điểm lấy & điểm giao → đẩy thông báo cho Carrier duyệt "Nhận giao""

> Nguồn #2 — `BR-MTCH-01` (§D4 L270):
> "BR-MTCH-01 | OFFER khớp NEED khi trùng điểm lấy & điểm giao; tuyến OFFER không hiển thị công khai"

> Nguồn #3 — `US-D12` (§D1b L186):
> "Khi một tin NEED trùng điểm lấy & điểm giao với tuyến → hệ thống đẩy thông báo "Tìm thấy đơn hàng phù hợp tuyến của bạn"; bấm vào thông báo → mở màn chi tiết tin cần vận chuyển đó"

> Nguồn #4 — `US-D13` (§D1b L187):
> "Tại chi tiết tin NEED phù hợp có nút "Nhận giao"; bấm → ghép (MATCHED) → lộ liên hệ 2 bên → vào màn Theo dõi đơn"

↳ **Ghi chú:** **4 nguồn đồng thuận** về luồng: khớp → thông báo → Carrier mở chi tiết → bấm **"Nhận giao"** → MATCHED. Lưu ý nút ở đây là **"Nhận giao"** (khác **"Tôi mang giúp được"** của luồng NEED thủ công) ⇒ 2 nút, 2 luồng, ⛔ đừng dùng lẫn tên. ⚠️ **Scope:** PM chưa trả lời auto-match có thuộc Phase 1 hay không (`KP-05 §1` câu #1) nhưng scope lượt này = **toàn bộ 11 module** ⇒ vẫn phân tích; đợt cũ có 1 scenario **không có TC** vì lý do này.

---

### REQ-ASN-007 · Điều kiện khớp — trùng điểm lấy & giao + giao nhau khung giờ
📍 `DOC-v1.0-01 §D7 OPR-02 · L338` · `DOC-v1.0-06 KP-01 §4 KB-ASN-04`  ·  Clarif: `C-NTF-02`

> Nguồn #1 — `OPR-02` (§D7 L338):
> "OPR-02 | Điều kiện khớp | Chỉ khớp khi trùng điểm lấy & điểm giao (cùng khu vực/tuyến) và giao nhau về khung giờ"

> Nguồn #2 — `DOC-v1.0-06` KP-01 §4 `KB-ASN-04` (BA trả lời):
> "= **trùng địa chỉ giao hàng đã chọn** + **khung giờ phù hợp**. **KHÔNG dùng bán kính GPS / khoảng cách địa lý.**"
> "🔴 Còn thiếu: "khung giờ phù hợp" là trùng hoàn toàn hay có độ lệch cho phép? Chu kỳ quét khớp? Ngưỡng gộp thông báo?"

↳ **Ghi chú:** `C-NTF-02` **Partially Resolved**: đã chốt **không dùng bán kính GPS** (khớp bằng **địa chỉ đã chọn**, khớp chuỗi/ID văn phòng); **chưa chốt** định nghĩa *"khung giờ phù hợp"* (trùng hoàn toàn vs có độ lệch) và chu kỳ quét. ⇒ `SC-ASN-011` (negative) chỉ assert được nhánh **địa chỉ không trùng**; nhánh **khung giờ không giao nhau** viết ở mức "không giao nhau hoàn toàn" (2 khung tách rời), ⛔ không test biên độ lệch. ⚠️ Chính BRD tự ghi *"Nháp — chờ BA review & bổ sung"* ở đầu §D7 (L333).

---

### REQ-ASN-008 · Trần gợi ý và trần thông báo khớp
📍 `DOC-v1.0-01 §D7 OPR-01 · L337` · `OPR-06 · L342` · `DOC-v1.0-06 KP-01 §4 KB-ASN-03`  ·  Clarif: `C-NTF-02`

> Nguồn #1 — `OPR-01` (§D7 L337):
> "OPR-01 | Trần số tin gợi ý cho 1 carrier | Mỗi người vận chuyển chỉ nhận thông báo tối đa 5 tin cần gửi phù hợp (mới & gần tuyến nhất); tránh làm phiền/spam"

> Nguồn #2 — `OPR-06` (§D7 L342):
> "OPR-06 | Trần thông báo khớp / ngày | Giới hạn số lần bắn thông báo khớp cho mỗi carrier trong ngày (ngưỡng admin cấu hình)"

> Nguồn #3 — PHÁN QUYẾT (`DOC-v1.0-06` KP-01 §4 `KB-ASN-03`):
> "Không phải "5 thông báo/ngày" cộng dồn — tính **riêng theo từng tin**."
> "⚠ Giá trị test 3/5/6 tin là **giá trị chốt**, không phải mock."

↳ **Ghi chú:** ⭐ **`OPR-06` đã bị BA đảo kết luận.** BA xác nhận 2026-07-29: trần = **5 thông báo cho MỖI tin OFFER**, **KHÔNG** cộng dồn theo ngày ⇒ scenario cũ `SC-NTF-006` (*"trần thông báo khớp/ngày"*) bị **DEPRECATED** ở đợt cũ và thay bằng rule mới. Lượt này: `SC-ASN-013` phủ `OPR-01` (trần **5 tin gợi ý**), `SC-ASN-014` phủ trần **5 thông báo/tin** theo `KB-ASN-03`. Biên test **3 / 5 / 6** là giá trị chốt của BA ⇒ dùng đúng 3 mốc này cho BVA.

---

### REQ-ASN-009 · Ưu tiên gợi ý + loại tin quá hạn khỏi luồng khớp
📍 `DOC-v1.0-01 §D7 OPR-04 · L340`  ·  Clarif: —

> "OPR-04 | Ưu tiên gợi ý | Sắp xếp theo độ gần tuyến → thời gian đăng (mới trước); tin quá hạn loại khỏi luồng khớp"

↳ **Ghi chú:** Hai rule trong 1 dòng ⇒ 2 SC. ⚠️ **Rule sắp xếp gần như không kiểm chứng được ở v1.0**: *"độ gần tuyến"* mà `KB-ASN-04` đã chốt là **khớp địa chỉ đã chọn, không dùng khoảng cách địa lý** ⇒ "độ gần" trở thành **nhị phân** (trùng/không trùng), không còn thứ tự để sắp xếp ⇒ tiêu chí thứ hai (**thời gian đăng, mới trước**) là tiêu chí duy nhất kiểm chứng được. `SC-ASN-015` vì thế để P3 và chỉ assert thứ tự theo thời gian đăng.

---

### REQ-ASN-010 · Không tự khớp với chính mình
📍 `DOC-v1.0-01 §D7 OPR-05 · L341` · `DOC-v1.0-06 KP-01 §4 KB-ASN-02`  ·  Clarif: `C-ASN-02`

> Nguồn #1 — `OPR-05` (§D7 L341):
> "OPR-05 | Không tự khớp với chính mình | Không gợi ý tin do chính người đó đăng; người gửi ≠ người vận chuyển của cùng một đơn"

> Nguồn #2 — PHÁN QUYẾT (`DOC-v1.0-06` KP-01 §4 `KB-ASN-02`):
> "BA/PO xác nhận **không được phép** — hành vi prototype là bug."
> "⚠ Lưu ý phạm vi: bug này ở màn **Chi tiết tin** (public), khác màn **Theo dõi đơn** (đã role-aware đúng)."

↳ **Ghi chú:** `OPR-05` có **2 mệnh đề**: **(a)** engine *"không gợi ý tin do chính người đó đăng"* → `SC-ASN-012` (module này); **(b)** *"người gửi ≠ người vận chuyển của cùng một đơn"* → bề mặt CTA, đã có SC ở `FEED` (`SC-FEED-011/012`). ⛔ Không nhân bản SC giữa 2 module. `SC-ASN-012` để **P1** vì nếu engine gợi ý tin của chính mình thì user có thể tự ghép và làm sai lệch mọi số liệu match.

---

### REQ-ASN-011 · Carrier huỷ nhận → tin về "Chờ ghép" và khớp lại được
📍 `DOC-v1.0-01 §D7 OPR-08 · L344` · `OPR-09 · L345`  ·  Clarif: —

> Nguồn #1 — `OPR-08` (§D7 L344):
> "tin huỷ bởi carrier quay lại "Chờ ghép" và được khớp lại"

> Nguồn #2 — `OPR-09` (§D7 L345):
> "OPR-09 | Carrier huỷ khi chưa lấy hàng → trả đơn về bảng tin | Người vận chuyển huỷ ở trạng thái Đã ghép (chưa "Tôi đã lấy hàng") → đơn tự động về "Chờ ghép" và hiển thị lại trên bảng tin cho người khác nhận"

↳ **Ghi chú:** 2 nguồn đồng thuận. Ranh giới trạng thái rõ: **chỉ khi chưa "Tôi đã lấy hàng"** (tức còn `MATCHED`, chưa `IN_TRANSIT`). SC ở đây phủ **hệ quả phía ghép nối** (tin trở lại tập khả dụng và **ghép lại được** bởi người khác); còn **hành động huỷ + popup lý do** thuộc `CNL` (`REQ-CNL-004`) ⇒ 2 module, 2 SC, không trùng.

---

### REQ-ASN-012 · Wizard đăng tin không tạo listing độc lập trong feed
📍 `DOC-v1.0-06 KP-01 §4 KB-ASN-05` · `KP-02 §5`  ·  Clarif: `C-ASN-03`

> "Ghi nhận trên prototype. Chưa rõ là giới hạn kiến trúc bản demo (chấp nhận được) hay hành vi cần fix."

**Source Location:** `DOC-v1.0-06 KP-01 §4 "KB-ASN-05" · đoạn 1`

↳ **Ghi chú:** *(Implicit — không có quote đặc tả, chỉ có ghi nhận quan sát.)* Nghi vấn: tin đăng qua wizard **không xuất hiện thành listing độc lập** trong feed của Carrier/Receiver. Rất có thể là **giới hạn của bản demo** (demo chỉ mô phỏng 1 đơn, `DOC-v1.0-02` §7 dòng 3: *"Đăng tin mới sẽ ghi đè đơn đang có"*) ⇒ `C-ASN-03` Open, cần xác nhận lại **khi có backend thật**. `SC-ASN-018` ghi nhận, ⛔ không kết luận bug.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
