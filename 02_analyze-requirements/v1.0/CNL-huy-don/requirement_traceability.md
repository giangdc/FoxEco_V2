# Requirement Traceability — v1.0 · Module CNL

> Tạo bởi: analyze-requirements (INIT 2026-09-07) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation: FR/VR` ⇒ **Schema A**.
> 📌 **Home canonical của `C-CNL-01`** (màn Báo sự cố) và `C-CNL-02` (log LỊCH SỬ khi huỷ).
> ⚠️ Module này PM xếp **out of scope Phase 1** (`KP-03 §3.1`) nhưng scope lượt phân tích = **toàn bộ 11 module** (quyết định 2026-09-07) ⇒ vẫn phân tích đầy đủ.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module CNL — DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-06

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-CNL-001 | `CNL-01`, `BR-CNL-01`, `US-D16`, `OPR-11` | `DOC-v1.0-01` §D3 L257 · §D4 L268 · §D1b L195 · §D7 L347 | SC-CNL-001, SC-CNL-002, SC-CNL-003 | — |
| REQ-CNL-002 | `VAL-04` | `DOC-v1.0-01` §D8.3 L395 · `DOC-v1.0-06` KP-01 §7 KB-CNL-02 | SC-CNL-004, SC-CNL-012 | — |
| REQ-CNL-003 | `OPR-11`, `BR-ASN-03` | `DOC-v1.0-01` §D7 L347 · §D4 L264 · §D5 L294 | SC-CNL-005, SC-CNL-006 | C-CNL-01 |
| REQ-CNL-004 | `OPR-09`, `US-D16` | `DOC-v1.0-01` §D7 L345 · §D1b L195 | SC-CNL-007 | — |
| REQ-CNL-005 | `BR-INT-05`, `CNL-01`, `TS-01` | `DOC-v1.0-01` §A5 L81 · §D3 L257 · §D2 L233 · §A8 L121 | SC-CNL-008, SC-CNL-011, SC-CNL-013 | — |
| REQ-CNL-006 | — (override hành vi hiện tại) | `DOC-v1.0-06` KP-01 §7 KB-CNL-01 · KP-02 §2 | SC-CNL-009, SC-CNL-010 | C-CNL-02 |
| REQ-CNL-007 | `BR-ASN-03` | `DOC-v1.0-01` §D2 L233 (`[INCIDENT]`) · `DOC-v1.0-06` KP-01 §5 KB-DLV-05 | — (gap có chủ đích — `CHANGELOG §3`) | C-CNL-01 |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-CNL-001 · Huỷ đơn kèm lý do bắt buộc (POSTED / MATCHED)
📍 `DOC-v1.0-01 §D3 CNL-01 · L257` · `§D4 BR-CNL-01 · L268` · `§D1b US-D16 · L195` · `§D7 OPR-11 · L347`  ·  Clarif: —

> Nguồn #1 — `CNL-01` (§D3 L257):
> "CNL-01 | Huỷ đơn kèm lý do | Lý do bắt buộc; ghi actor (Sender/Carrier/Receiver); đồng bộ realtime; Carrier huỷ → về POSTED"

> Nguồn #2 — `BR-CNL-01` (§D4 L268):
> "BR-CNL-01 | Huỷ đơn bắt buộc có lý do; hệ thống ghi rõ vai trò người huỷ + đồng bộ cho cả 3 bên"

> Nguồn #3 — `US-D16` (§D1b L195):
> "Huỷ được ở POSTED/MATCHED; popup huỷ bắt buộc nhập lý do (nút Xác nhận khoá tới khi có lý do); đơn huỷ ghi rõ ai huỷ (Người gửi/Người vận chuyển/Người nhận) + lý do, đồng bộ realtime cho cả 3 bên; Carrier huỷ nhận → đơn trả lại bảng tin (về "Chờ ghép"); sau IN_TRANSIT phải tạo báo cáo sự cố"

> Nguồn #4 — `OPR-11` (§D7 L347):
> "OPR-11 | Điều kiện huỷ đơn | Chỉ được huỷ khi chưa ai nhận ("Chờ ghép") hoặc đang "Lấy hàng" (đã ghép, chưa lấy được hàng); đã lấy hàng → sang "Đang giao" thì KHÔNG ai được huỷ"

↳ **Ghi chú:** **4 nguồn đồng thuận**, `US-D16` là nguồn đầy đủ nhất (nêu cả rule *"nút Xác nhận khoá tới khi có lý do"*). Fan-out 3 SC: huỷ ở `POSTED` · huỷ ở `MATCHED` · rule khoá nút Xác nhận. ⚠️ Lưu ý ranh giới trạng thái của `OPR-11` dùng **tên mốc UI** (*"đang Lấy hàng"* = `MATCHED`, *"Đang giao"* = `IN_TRANSIT`) — cùng bẫy thuật ngữ đã ghi ở `DLV`.

---

### REQ-CNL-002 · Lý do huỷ tối thiểu 5 ký tự (`VAL-04`)
📍 `DOC-v1.0-01 §D8.3 VAL-04 · L395` · `DOC-v1.0-06 KP-01 §7 KB-CNL-02`  ·  Clarif: —

> Nguồn #1 — `VAL-04` (§D8.3 L395):
> "VAL-04 | Huỷ đơn: bắt buộc nhập lý do (tối thiểu 5 ký tự) mới bật nút Xác nhận"

> Nguồn #2 — HÀNH VI THẬT (`DOC-v1.0-06` KP-01 §7 `KB-CNL-02`):
> "**Thực tế UI (CA live-verify):** chỉ chặn khi để **rỗng**; nhập 4 ký tự vẫn bật nút, và **không trim khoảng trắng trước khi đếm** (5 dấu cách vẫn qua)."

↳ **Ghi chú:** ⭐ **2 gap đã live-verify** (Chrome MCP 2026-07-29): **(a)** ngưỡng 5 ký tự **không được enforce** (4 ký tự vẫn qua); **(b)** **không trim khoảng trắng** (5 dấu cách vẫn qua) — gap (b) còn vi phạm `VAL-03` (*"Tự cắt khoảng trắng đầu/cuối"*). ⇒ 2 SC viết theo **spec** (`SC-CNL-004`, `SC-CNL-012`), **dự kiến FAIL** — đợt cũ đã cố ý viết TC bắt 2 gap này (`KP-05 §4`).

---

### REQ-CNL-003 · Không huỷ được từ "Đang giao" trở đi
📍 `DOC-v1.0-01 §D7 OPR-11 · L347` · `§D4 BR-ASN-03 · L264` · `§D5 · L294`  ·  Clarif: `C-CNL-01`

> Nguồn #1 — `OPR-11` (§D7 L347):
> "đã lấy hàng → sang "Đang giao" thì KHÔNG ai được huỷ"

> Nguồn #2 — `BR-ASN-03` (§D4 L264):
> "BR-ASN-03 | Sau khi nhận hàng (IN_TRANSIT) không hủy thường → phải tạo sự cố"

> Nguồn #3 — `DOC-v1.0-01` §D5 L294:
> "Sau khi nhận, hàng hỏng/mất | Tạo sự cố, không cho COMPLETED thường; dùng timeline + ảnh làm bằng chứng"

↳ **Ghi chú:** **3 nguồn đồng thuận** về vế **chặn huỷ**; vế *"phải tạo sự cố"* thì màn "Báo sự cố" **chưa có đặc tả và out of scope v1.0** (`C-CNL-01` Resolved) ⇒ `SC-CNL-005` assert **chặn huỷ** (P1, có oracle rõ), `SC-CNL-006` chỉ **ghi nhận** rằng không có bề mặt tạo sự cố. ⚠️ Rule này áp cho **cả 3 vai** — `OPR-11` ghi *"KHÔNG **ai** được huỷ"*.

---

### REQ-CNL-004 · Carrier huỷ nhận khi "Đã ghép" → đơn về "Chờ ghép"
📍 `DOC-v1.0-01 §D7 OPR-09 · L345` · `§D1b US-D16 · L195`  ·  Clarif: —

> Nguồn #1 — `OPR-09` (§D7 L345):
> "OPR-09 | Carrier huỷ khi chưa lấy hàng → trả đơn về bảng tin | Người vận chuyển huỷ ở trạng thái Đã ghép (chưa "Tôi đã lấy hàng") → đơn tự động về "Chờ ghép" và hiển thị lại trên bảng tin cho người khác nhận"

> Nguồn #2 — `US-D16` (§D1b L195):
> "Carrier huỷ nhận → đơn trả lại bảng tin (về "Chờ ghép")"

↳ **Ghi chú:** ⚠️ **Phân biệt 2 hành động huỷ khác nhau** (dễ trộn nhất của module): **"Huỷ đơn"** (Sender/Receiver → đơn `CANCELLED`, kết thúc) ⟷ **"Huỷ nhận đơn"** (Carrier → đơn **quay lại `POSTED`**, tiếp tục sống). Nhãn nút cũng khác: `Huỷ đơn` vs `✕ Huỷ nhận đơn` (`KB-DLV-01` ô 2). SC ở đây phủ **hành động + đổi trạng thái**; hệ quả *"ghép lại được bởi người khác"* đã có SC ở `ASN` (`SC-ASN-017`) ⇒ ⛔ không nhân bản.

---

### REQ-CNL-005 · Ghi rõ vai trò người huỷ + lý do + đồng bộ realtime 3 bên
📍 `DOC-v1.0-01 §A5 BR-INT-05 · L81` · `§D3 CNL-01 · L257` · `§D2 · L233` · `§A8 TS-01 · L121`  ·  Clarif: —

> Nguồn #1 — `BR-INT-05` (§A5 L81):
> "BR-INT-05 | Huỷ sau khi MATCHED phải có lý do (bắt buộc), ghi rõ ai huỷ + đồng bộ realtime cả 3 bên"

> Nguồn #2 — `DOC-v1.0-01` §D2 L233:
> "Ngoài luồng: [CANCELLED "Đã huỷ"] — bắt buộc lý do; ghi rõ ai huỷ (Sender/Carrier/Receiver); đồng bộ realtime cả 3 bên; Carrier huỷ → trả đơn về "Chờ ghép""

> Nguồn #3 — `TS-01` (§A8 L121):
> "TS-01 | Ghi log toàn bộ tương tác: ai đăng, ai nhận, mốc thời gian, đổi trạng thái, huỷ (kèm lý do + ai huỷ)"

↳ **Ghi chú:** **3 nguồn đồng thuận** — và `TS-01` nâng đây thành **yêu cầu audit**, không chỉ là hiển thị. Fan-out 3 SC: ghi rõ vai trò + lý do (`SC-CNL-008`) · đồng bộ realtime 3 bên (`SC-CNL-011`) · **ma trận quyền huỷ theo vai × trạng thái** (`SC-CNL-013`, nguồn `§D4` permission matrix L285). ⚠️ Mâu thuẫn với hành vi thật: `KB-CNL-01` cho thấy **hiện KHÔNG ghi log** ⇒ xem `REQ-CNL-006`.

---

### REQ-CNL-006 · Huỷ đơn / Huỷ nhận đơn PHẢI ghi log LỊCH SỬ (override)
📍 `DOC-v1.0-06 KP-01 §7 KB-CNL-01` · `KP-02 §2`  ·  Clarif: `C-CNL-02`

> Nguồn — `DOC-v1.0-06` KP-01 §7 `KB-CNL-01` (live-verify 2026-07-29):
> "- **Huỷ đơn** (Sender/Receiver) → **không ghi log nào** vào block LỊCH SỬ, chỉ hiện banner đỏ *"Đơn hàng đã bị huỷ"*"
> "- **Huỷ nhận đơn** (Carrier) → tệ hơn: **XOÁ LUÔN dòng "Ghép thành công"** khỏi LỊCH SỬ"
> "User chốt: *"huy don va huy nhan don hien tai cu luu log lich su nha"* → **LỊCH SỬ phải ghi log cho cả 2 hành động; hành vi hiện tại là GAP cần dev bổ sung.**"

↳ **Ghi chú:** ⭐ **REQ do QA/user ban hành để OVERRIDE hành vi hiện tại** (`C-CNL-02` Resolved theo hướng override 2026-07-30). Hai gap khác mức độ: **huỷ đơn** = *thiếu* log; **huỷ nhận đơn** = **XOÁ log đã có** — nghiêm trọng hơn vì vi phạm trực tiếp `BR-INT-04` (*"Timeline tương tác không sửa được sau khi ghi (audit)"*) và `TS-02`. ⇒ 2 SC riêng (`SC-CNL-009`, `SC-CNL-010`), **dự kiến FAIL**; đợt cũ đã cố ý viết TC bắt gap này (`KP-05 §4`).

---

### REQ-CNL-007 · Màn "Báo sự cố" (Incident) — out of scope v1.0
📍 `DOC-v1.0-01 §D2 · L233` · `DOC-v1.0-06 KP-01 §5 KB-DLV-05`  ·  Clarif: `C-CNL-01`

> Nguồn #1 — `DOC-v1.0-01` §D2 L233:
> "Ngoài luồng: [CANCELLED "Đã huỷ"]… · [EXPIRED] · **[INCIDENT]**"

> Nguồn #2 — `DOC-v1.0-06` KP-01 §5 `KB-DLV-05`:
> "Màn "Báo sự cố" chưa có đặc tả — out of scope v1.0"

↳ **Ghi chú:** **Gap SC có chủ đích.** Trạng thái `[INCIDENT]` **có tên trong sơ đồ vòng đời** và `BR-ASN-03` yêu cầu *"phải tạo sự cố"*, nhưng **không tài liệu nào mô tả field/màn** ⇒ `C-CNL-01` Resolved: out of scope v1.0. Theo `§Custom Rules §10.1` ⛔ không viết SC khẳng định; `SC-CNL-006` (thuộc `REQ-CNL-003`) đã ghi nhận sự thiếu vắng bề mặt này ⇒ không cần SC riêng, ghi nợ ở `CHANGELOG §3`.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
