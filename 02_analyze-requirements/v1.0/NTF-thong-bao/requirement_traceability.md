# Requirement Traceability — v1.0 · Module NTF

> Tạo bởi: analyze-requirements (INIT 2026-09-07) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation: FR/VR` ⇒ **Schema A**.
> 📌 **Home canonical của `C-NTF-01`** (danh sách loại thông báo chính thức — 3 nguồn, bảng unified 12 hàng ở `KP-07`) và **`C-NTF-03`** (đánh dấu đã đọc + phân trang).
> ⚠️ Rule **khớp tuyến** (`C-NTF-02`) tuy mang nhãn `NTF` nhưng nội dung là engine ghép nối ⇒ home canonical ở `ASN`.
> ⚠️ Module này PM xếp **out of scope Phase 1** (`KP-03 §3.1`) nhưng scope lượt phân tích = toàn bộ 11 module.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module NTF — DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-04 · DOC-v1.0-06

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-NTF-001 | `NTF-01`, `NTF-02` | `DOC-v1.0-01` §D6 L319-320 · `DOC-v1.0-02` §3.2 | SC-NTF-001 | C-NTF-01 |
| REQ-NTF-002 | `NTF-03` | `DOC-v1.0-01` §D6 L321 · §D1b `US-D12` L186 | SC-NTF-002 | C-NTF-01, C-NTF-02 |
| REQ-NTF-003 | `NTF-04`, `NTF-05`, `NTF-06` | `DOC-v1.0-01` §D6 L322-324 | SC-NTF-003, SC-NTF-004, SC-NTF-005 | C-NTF-01 |
| REQ-NTF-004 | `NTF-08`, `NTF-09` | `DOC-v1.0-01` §D6 L326-327 · `DOC-v1.0-06` KP-07 hàng #8/#9 | SC-NTF-006, SC-NTF-007 | C-NTF-01 |
| REQ-NTF-005 | `OPR-07`, `NTF` header (§D6 L315) | `DOC-v1.0-01` §D7 L343 · §D6 L315 | SC-NTF-008 | — |
| REQ-NTF-006 | — (bảng §3.2 không đánh số) | `DOC-v1.0-02` §3.2 · `DOC-v1.0-04` ảnh `3e626d39…` | SC-NTF-009 | — |
| REQ-NTF-007 | — | `DOC-v1.0-06` KP-01 §8 KB-NTF-01 · `DOC-v1.0-04` ảnh `3e626d39…` | SC-NTF-010, SC-NTF-011 | C-NTF-03 |
| REQ-NTF-008 | — | `DOC-v1.0-06` KP-01 §8 KB-NTF-02 | SC-NTF-012 | C-NTF-03 |
| REQ-NTF-009 | — (bảng §2 không đánh số) | `DOC-v1.0-02` §2 dòng "Header" | SC-NTF-013 | — |
| REQ-NTF-010 | `NTF-01..09` (toàn bộ) | `DOC-v1.0-01` §D6 L317-327 · `DOC-v1.0-02` §3.2 · `DOC-v1.0-06` KP-07 | SC-NTF-014 | C-NTF-01 |
| REQ-NTF-011 | — | `DOC-v1.0-06` KP-02 §5 dòng `C-ORD-06` · `KP-05 §3` (#6) | SC-NTF-015, SC-NTF-016 | C-ORD-06 |
| — | `NTF-07` (nhận quà ảo) | `DOC-v1.0-01` §D6 L325 | — (SC ở `GIFT` — `SC-GIFT-012`) | C-NTF-01 |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-NTF-001 · Thông báo khi ghép ngay (`NTF-01` Sender · `NTF-02` Receiver)
📍 `DOC-v1.0-01 §D6 · L319-320` · `DOC-v1.0-02 §3.2`  ·  Clarif: `C-NTF-01`

> Nguồn #1 — `DOC-v1.0-01` §D6 L319-320:
> "NTF-01 | Có người bấm "Tôi mang giúp được" → ghép ngay | Người gửi | "Đã có người nhận mang giúp đơn của bạn — SĐT đã được lộ để liên hệ""
> "NTF-02 | Đơn được ghép (MATCHED) | Người nhận | "Đơn gửi tới bạn đã có người vận chuyển nhận giao""

> Nguồn #2 — MÂU THUẪN (`DOC-v1.0-02` §3.2):
> "Có người muốn mang giúp đơn của bạn | "[Tên] ngỏ ý mang giúp '...'. Xác nhận để lộ SĐT.""

↳ **Ghi chú:** ⚠️ **Hai nguồn mô tả 2 CƠ CHẾ khác nhau, không chỉ khác câu chữ:** BRD `NTF-01` = **ghép ngay + SĐT đã lộ**; PRD = *"ngỏ ý"* + *"Xác nhận để lộ SĐT"* (tức có bước duyệt). `KP-07` hàng #1 ghi rõ: *"BRD vs Demo khác nhau về THỜI ĐIỂM lộ SĐT (ghép ngay vs cần xác nhận thêm) — liên quan C-ASN-01"*. ⇒ Chốt theo **BRD + `BR-CON-01`** (đã quyết ở `ASN`: **ghép ngay**) ⇒ SC assert nội dung `NTF-01`/`NTF-02` của BRD. Fan-out 1 SC phủ 2 người nhận (Sender + Receiver) vì cùng 1 sự kiện kích hoạt.

---

### REQ-NTF-002 · Thông báo khớp tuyến OFFER (`NTF-03` Carrier)
📍 `DOC-v1.0-01 §D6 · L321` · `§D1b US-D12 · L186`  ·  Clarif: `C-NTF-01`, `C-NTF-02`

> Nguồn #1 — `NTF-03` (§D6 L321):
> "NTF-03 | Hệ thống khớp tuyến OFFER với 1 tin NEED | Người vận chuyển | "Tìm thấy đơn hàng phù hợp tuyến của bạn — xem chi tiết để nhận giao""

> Nguồn #2 — `US-D12` (§D1b L186):
> "hệ thống đẩy thông báo "Tìm thấy đơn hàng phù hợp tuyến của bạn"; bấm vào thông báo → mở màn chi tiết tin cần vận chuyển đó"

> Nguồn #3 — `DOC-v1.0-06` KP-07 hàng #3 (Figma):
> ""Tìm thấy đơn hàng phù hợp tuyến của bạn" — "Có người cần gửi... trùng tuyến bạn đã đăng..." (khớp gần với BRD NTF-03 hơn Demo)"

↳ **Ghi chú:** **3 nguồn gần đồng thuận text** (Figma khớp BRD hơn PRD) ⇒ assert được phần đầu câu. ⚠️ **Phụ thuộc `C-NTF-02`** (chưa chốt chu kỳ quét khớp) ⇒ ⛔ không assert **độ trễ** nhận thông báo. Hành vi *"bấm thông báo → mở chi tiết tin"* trùng `SC-ASN-009` ⇒ SC ở đây assert **nội dung thông báo**, SC ở `ASN` assert **luồng ghép**.

---

### REQ-NTF-003 · Thông báo theo mốc vận chuyển (`NTF-04`/`NTF-05`/`NTF-06`)
📍 `DOC-v1.0-01 §D6 · L322-324`  ·  Clarif: `C-NTF-01`

> "NTF-04 | Carrier bấm "Tôi đã lấy hàng" (IN_TRANSIT) | Người gửi · Người nhận | "Người vận chuyển đã lấy hàng và bắt đầu giao""
> "NTF-05 | Carrier bấm "Đã giao cho người nhận" (DELIVERED) | Người nhận · Người gửi | "Đơn đã được giao — vui lòng xác nhận đã nhận hàng""
> "NTF-06 | Người nhận "Xác nhận đã nhận hàng" (COMPLETED) | Người gửi · Người vận chuyển | "Đơn đã hoàn tất — cảm ơn bạn!""

↳ **Ghi chú:** 3 thông báo gắn với **3 state-transition** của `DLV` ⇒ 3 SC riêng (fan-out theo state-transition). Mỗi thông báo có **2 người nhận** ⇒ Then phải kiểm cả 2. ⚠️ `KP-07` cho biết: hàng #4 (`NTF-04`) *"Không quan sát trong 82 ảnh"*, hàng #5 (`NTF-05`) PRD *"Không có mục riêng"*, hàng #6 (`NTF-06`) Figma **khớp Y HỆT** PRD (*"Đơn đã hoàn thành — đánh giá ngay"*) ⇒ **mức bằng chứng không đều**; `NTF-06` có nguy cơ dùng text *"đánh giá ngay"* trong khi rating đã defer (`C-GIFT-01`).

---

### REQ-NTF-004 · Thông báo huỷ đơn và tin quá hạn (`NTF-08`/`NTF-09`)
📍 `DOC-v1.0-01 §D6 · L326-327` · `DOC-v1.0-06 KP-07 hàng #8/#9`  ·  Clarif: `C-NTF-01`

> Nguồn #1 — `NTF-08` (§D6 L326):
> "NTF-08 | Đơn bị huỷ (kèm lý do) | Các bên còn lại của đơn | "Đơn đã bị huỷ bởi [vai trò] — lý do: […]""

> Nguồn #2 — `NTF-09` (§D6 L327):
> "NTF-09 | Tin quá hạn chưa ghép | Người đăng tin | "Tin của bạn đã quá hạn — gỡ hoặc đăng lại nếu vẫn cần""

> Nguồn #3 — `DOC-v1.0-06` KP-07 hàng #8 (Figma, cụ thể hơn BRD):
> ""Đơn của bạn đã bị người vận chuyển huỷ" — "Lý do: 'bận họp gấp'. Đơn đang chờ người vận chuyển mới..." (Figma cụ thể hơn BRD (thêm câu "đang chờ người mới")), dùng làm verbatim ưu tiên"

↳ **Ghi chú:** `NTF-08` có **2 mức chi tiết**: BRD dùng template `[vai trò]` + `[…]`; Figma thêm câu *"Đơn đang chờ người vận chuyển mới..."* (chỉ đúng cho nhánh **Carrier huỷ nhận** → đơn về `POSTED`, xem `SC-CNL-007`) ⇒ `KP-07` đề nghị dùng Figma làm verbatim ưu tiên. `NTF-09` gắn với `SC-ORD-045` (tin tự hết hạn) ⇒ tiền đề cần đơn quá hạn (⛔ không seed được qua UI).

---

### REQ-NTF-005 · SĐT KHÔNG được đưa vào nội dung push
📍 `DOC-v1.0-01 §D7 OPR-07 · L343` · `§D6 · L315`  ·  Clarif: —

> Nguồn #1 — `OPR-07` (§D7 L343):
> "SĐT chỉ lộ sau khi ghép, chỉ cho đúng 2 người trong cặp; **không đưa SĐT vào nội dung push**"

> Nguồn #2 — `DOC-v1.0-01` §D6 L315:
> "Kênh: in-app + push (**SĐT chỉ lộ sau khi ghép, không đưa vào nội dung push**)"

↳ **Ghi chú:** **2 nguồn đồng thuận** — rule bảo mật, và là **REQ duy nhất P1 của module**. ⚠️ Đáng chú ý: `NTF-01` có text *"SĐT đã được lộ để liên hệ"* — **nhắc tới việc SĐT đã lộ nhưng không chứa số** ⇒ đúng rule; TC phải phân biệt *"nhắc SĐT"* (được) ⟷ *"chứa số điện thoại"* (không được). Kiểm trên **cả 2 kênh** in-app và push.

---

### REQ-NTF-006 · Màn Thông báo — nhóm theo mốc thời gian
📍 `DOC-v1.0-02 §3.2` · `DOC-v1.0-04 ảnh 3e626d39…`  ·  Clarif: —

> "Thông báo — nhóm theo Hôm nay / Hôm qua / Tuần này"

↳ **Ghi chú:** Nguồn duy nhất là **dòng tiêu đề ảnh** của PRD §3.2 (+ ảnh Figma `3e626d39…` xác nhận có nhóm "Hôm nay"). ⚠️ **Không nguồn nào nói** thông báo cũ hơn 1 tuần thì vào nhóm nào ⇒ Then chỉ assert 3 nhóm được nêu tên, ⛔ không suy diễn nhóm thứ tư.

---

### REQ-NTF-007 · Chấm đỏ chưa đọc + nút "Đánh dấu đã đọc"
📍 `DOC-v1.0-06 KP-01 §8 KB-NTF-01` · `DOC-v1.0-04 ảnh 3e626d39…`  ·  Clarif: `C-NTF-03`

> "Ảnh Figma `3e626d398e3a616a45f5c638df62be830d2f4357`: 2 thông báo mới nhất có chấm đỏ riêng, 2 thông báo cũ hơn **cùng nhóm "Hôm nay"** thì không → gợi ý trạng thái đã-đọc/chưa-đọc theo item."
> "🔴 **Không chứng minh được cơ chế tương tác**: bấm nút "Đánh dấu đã đọc" là mark-all hay mark-per-item? → chờ BA. Clarification `C-NTF-03(a)` Open."

**Source Location:** `DOC-v1.0-06 KP-01 §8 "KB-NTF-01"`

↳ **Ghi chú:** ⚠️ **Bằng chứng GIÁN TIẾP** — nguồn tự ghi rõ vậy: ảnh cho thấy chấm đỏ **theo từng item** (2 item mới có, 2 item cũ cùng nhóm không có) nhưng **không chứng minh cơ chế tương tác**. ⇒ `SC-NTF-010` assert **trạng thái hiển thị** (chấm đỏ theo item — có bằng chứng ảnh); `SC-NTF-011` **chỉ ghi nhận** cơ chế nút "Đánh dấu đã đọc" (mark-all vs mark-per-item — `C-NTF-03(a)` Open).

---

### REQ-NTF-008 · Scroll / lazy-load danh sách Thông báo
📍 `DOC-v1.0-06 KP-01 §8 KB-NTF-02`  ·  Clarif: `C-NTF-03`

> "Không có đặc tả phân trang ở bất kỳ tài liệu nào. QA GiangDC2 xác nhận (2026-07-29): đây là **hành vi UI nền tảng bắt buộc** cho danh sách lớn, không cần BA xác nhận riêng như một business rule."
> "Clarification: `C-NTF-03(b)` N/A — không phải điểm cần clarification"

**Source Location:** `DOC-v1.0-06 KP-01 §8 "KB-NTF-02"`

↳ **Ghi chú:** *(Implicit — không có đặc tả, QA quyết định là yêu cầu UI nền tảng.)* `C-NTF-03(b)` được đánh **N/A** (không phải điểm cần BA chốt) ⇒ viết SC được, nhưng ⛔ không assert **kích thước trang** (bao nhiêu item/lần load) vì không có nguồn. Cùng bản chất với vấn đề chưa có đặc tả ở `ACT` (danh sách đơn nhiều).

---

### REQ-NTF-009 · Chuông ở header + chấm đỏ khi có tin chưa đọc
📍 `DOC-v1.0-02 §2 · dòng "Header"`  ·  Clarif: —

> "Header | Icon vai trò + "Xin chào, [Tên]" + chuông thông báo (chấm đỏ khi có tin chưa đọc)"

↳ **Ghi chú:** Bề mặt chuông thuộc `HOME` (`SC-HOME-005/006` assert **có/không có chấm đỏ**); SC ở module này (`SC-NTF-013`) assert **tính đồng bộ**: chấm đỏ ở chuông khớp với **số thông báo chưa đọc thật** trong danh sách ⇒ 2 module, 2 góc nhìn, không trùng.

---

### REQ-NTF-010 · Danh sách loại thông báo chính thức — 3 nguồn chưa hợp nhất
📍 `DOC-v1.0-01 §D6 · L317-327` · `DOC-v1.0-02 §3.2` · `DOC-v1.0-06 KP-07` (bảng unified 12 hàng)  ·  Clarif: `C-NTF-01`

> Nguồn #1 — BRD tự khai (`§D6` L315):
> "Danh sách sự kiện bắn thông báo dựa trên flow & màn hình hiện có của prototype. **Nháp — chờ BA review & bổ sung.**"

> Nguồn #2 — `DOC-v1.0-06` KP-07 (khuyến nghị):
> "**Khuyến nghị cho BA/PO:** chọn 1 trong 3 hướng — (a) dùng nguyên BRD D6 (9 loại, NTF-01..09) làm chuẩn… (b) dùng Figma + Demo… (c) hợp nhất cả 3 thành danh sách mới ~10 loại (bỏ #6b, #11 theo 2 clarification đã resolved; giữ lại #10 "nhắc khung giờ" vì có bằng chứng UI thật). Cho tới khi BA chọn, generate-tc tạm dùng **hướng (c)** làm baseline vì có bằng chứng UI thật nhiều nhất."

↳ **Ghi chú:** ⭐ **CL lớn nhất của module.** 3 nguồn cho **3 danh sách khác nhau**; `KP-07` đã lập **bảng unified 12 hàng sự kiện × 3 nguồn** để BA chọn 1 lần — **BA chưa trả lời**. 2 hàng đã loại được nhờ CL khác: #6b (*"nhận đánh giá 5 sao"* — `C-GIFT-01`), #11 (*"cộng đồng đạt mốc X đơn / CO₂"* — `C-USR-01`). Hàng **#10 (*"Sắp đến khung giờ hẹn giao"*) có bằng chứng ở CẢ Demo và Figma nhưng KHÔNG có trong BRD `§D6`** ⇒ khả năng cao BRD sót. ⇒ `SC-NTF-014` ghi nhận danh sách thật trên app, ⛔ không assert danh sách nào là đúng.

---

### REQ-NTF-011 · Empty state + nút back màn Thông báo
📍 `DOC-v1.0-06 KP-02 §5 dòng "C-ORD-06"` · `KP-05 §3 (#6)`  ·  Clarif: `C-ORD-06`

> Nguồn #1 — `C-ORD-06` (`KP-02` §5):
> "Empty state của 3 màn (Hoạt động · Quà đã nhận · **Thông báo**) khi không có data"

> Nguồn #2 — `KP-05` §3 (#6):
> "6 | Nút back (←) ở màn Thông báo quay về Trang chủ | Thuộc bề mặt màn Thông báo"

↳ **Ghi chú:** *(Implicit cho empty state — không có quote đặc tả text.)* Màn Thông báo là **màn thứ ba** của `C-ORD-06` (home canonical ở `ACT`). Nút back là **1 trong 6 nhóm case "chưa có nguồn tài liệu"** của đợt cũ (`KP-05 §3`) — nay có nguồn nền tảng ở `DOC-v1.0-02` §2 (*"màn hình con… chỉ có nút quay lại (←)"*) ⇒ `SC-NTF-016` viết được nhưng đích *"về Trang chủ"* là **suy diễn** (chuông mở từ header Trang chủ), ghi rõ trong Analyst Note.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
