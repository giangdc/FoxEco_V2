---
id: v1.0/CNL-huy-don/scenario-map
title: Test Scenario Map — v1.0 · Module CNL
type: scenario-map
version: v1.0
sprint: 1
module: CNL
counts:
  req: 7
  sc: 13
  new: 13
  modified: 0
  carried: 0
  deprecated: 0
  p1: 4
  p2: 7
  p3: 2
  req_without_sc: 1
status: ANALYZED
updated: 2026-09-07
---

# Test Scenario Map — v1.0 · Module CNL

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module CNL.
> ⚠️ `req_without_sc: 1` — `REQ-CNL-007` (màn Báo sự cố) gap có chủ đích, ghi ở `CHANGELOG §3`.
> ⭐ **4 SC dự kiến FAIL** (`SC-CNL-004`, `SC-CNL-009`, `SC-CNL-010`, `SC-CNL-012`) — đều là gap đã **live-verify** ở đợt cũ, FAIL là kết quả đúng.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Fan-out mỗi role · **mỗi state-transition** · lớp EP · boundary · nhánh lỗi = 1 SC.
> Module fan-out theo **trạng thái được phép huỷ** (`POSTED` / `MATCHED` / `IN_TRANSIT`+) và **2 hành động huỷ khác nhau** ("Huỷ đơn" ⟷ "Huỷ nhận đơn").

## Tổng quan
- Tổng số scenarios: **13** (NEW: 13, MODIFIED: 0, CARRIED: 0, DEPRECATED: 0)
- Phân bổ priority: P1: 4 | P2: 7 | P3: 2
- ⚠️ Module PM xếp **out of scope Phase 1** nhưng đợt cũ **vẫn viết 27 TC** (sheet `TC_08`); lượt này phân tích đầy đủ theo quyết định scope 2026-09-07.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### CNL — Huỷ đơn / Huỷ nhận đơn

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-CNL-001 | Huỷ đơn ở "Chờ ghép" | REQ-CNL-001 | DOC-v1.0-01 §D1b US-D16 L195 · §D7 OPR-11 L347 | Đơn ở "Chờ ghép"; tài khoản **Người gửi** | Bấm "Huỷ đơn" → popup hiện → nhập lý do hợp lệ → Xác nhận | Đơn chuyển "Đã huỷ"; đơn KHÔNG còn trên Bảng tin | P1 | Functional | NEW |
| SC-CNL-002 | Huỷ đơn ở "Đã ghép" | REQ-CNL-001 | DOC-v1.0-01 §A5 BR-INT-05 L81 · §D7 OPR-11 L347 | Đơn ở "Đã ghép" (Carrier chưa lấy hàng); tài khoản Người gửi | Bấm "Huỷ đơn" → nhập lý do → Xác nhận | Đơn chuyển "Đã huỷ"; cả Carrier và Receiver thấy đơn đã huỷ | P1 | Functional | NEW |
| SC-CNL-003 | Nút Xác nhận khoá tới khi có lý do | REQ-CNL-001 | DOC-v1.0-01 §D1b US-D16 L195 | Popup huỷ đơn đang mở, ô lý do **để trống** | Quan sát nút "Xác nhận" rồi nhập lý do | Nút "Xác nhận" bị khoá khi lý do rỗng; nhập lý do hợp lệ thì nút bật | P2 | Business Rule | NEW |
| SC-CNL-004 | [GAP·bug] Lý do tối thiểu 5 ký tự | REQ-CNL-002 | DOC-v1.0-01 §D8.3 VAL-04 L395 · KP-01 §7 KB-CNL-02 | Popup huỷ đơn đang mở | Nhập lý do **4 ký tự** rồi quan sát nút Xác nhận; sau đó nhập 5 ký tự | 4 ký tự: nút Xác nhận **bị khoá** (VAL-04). ⚠ Dự kiến FAIL — app hiện chỉ chặn khi rỗng → log bug | P2 | Business Rule | NEW |
| SC-CNL-005 | Không huỷ được từ "Đang giao" | REQ-CNL-003 | DOC-v1.0-01 §D7 OPR-11 L347 · §D4 BR-ASN-03 L264 | Đơn ở "Đang giao" (Carrier đã bấm "Tôi đã lấy hàng") | Lần lượt bằng cả 3 vai: tìm nút/đường huỷ đơn | KHÔNG vai nào huỷ được đơn (`OPR-11`: *"KHÔNG ai được huỷ"*) | P1 | Business Rule | NEW |
| SC-CNL-006 | [GAP] Không có bề mặt tạo sự cố | REQ-CNL-003 | DOC-v1.0-01 §D4 BR-ASN-03 L264 · KP-01 §5 KB-DLV-05 | Đơn ở "Đang giao"; `BR-ASN-03` yêu cầu *"phải tạo sự cố"* thay cho huỷ thường | Rà màn Theo dõi đơn cả 3 vai tìm chức năng "Báo sự cố" | GHI NHẬN GAP: không tồn tại bề mặt tạo sự cố ở v1.0 (đúng phạm vi — C-CNL-01). ⛔ KHÔNG viết TC luồng sự cố | P3 | Business Rule | NEW |
| SC-CNL-007 | Carrier huỷ nhận → đơn về "Chờ ghép" | REQ-CNL-004 | DOC-v1.0-01 §D7 OPR-09 L345 · §D1b US-D16 L195 | Đơn ở "Đã ghép"; tài khoản **Carrier**, chưa bấm "Tôi đã lấy hàng" | Bấm "✕ Huỷ nhận đơn" → popup lý do bắt buộc → Xác nhận | Đơn về "Chờ ghép" và hiển thị lại trên Bảng tin; ⛔ đơn KHÔNG chuyển "Đã huỷ" | P1 | Business Rule | NEW |
| SC-CNL-008 | Ghi rõ vai trò người huỷ + lý do | REQ-CNL-005 | DOC-v1.0-01 §D2 L233 · §D3 CNL-01 L257 | Đơn vừa bị huỷ bởi 1 vai xác định | Các bên còn lại mở đơn / thông báo | Hiển thị rõ **ai huỷ** (Người gửi / Người vận chuyển / Người nhận) **và lý do** đã nhập | P2 | Business Rule | NEW |
| SC-CNL-009 | [GAP·bug] Huỷ đơn phải ghi log LỊCH SỬ | REQ-CNL-006 | DOC-v1.0-06 KP-01 §7 KB-CNL-01 · KP-02 §2 | Đơn ở "Chờ ghép"/"Đã ghép"; block LỊCH SỬ đang có các mốc trước đó | Sender (hoặc Receiver) huỷ đơn, rồi mở block LỊCH SỬ | Có **dòng log mới** ghi hành động huỷ (kèm vai + lý do). ⚠ Dự kiến FAIL — app hiện chỉ hiện banner đỏ, không ghi log → log bug | P2 | Business Rule | NEW |
| SC-CNL-010 | [GAP·bug] Huỷ nhận đơn KHÔNG được xoá log | REQ-CNL-006 | DOC-v1.0-06 KP-01 §7 KB-CNL-01 · DOC-v1.0-01 §A5 BR-INT-04 L80 | Đơn ở "Đã ghép"; LỊCH SỬ **đã có** dòng "Ghép thành công" | Carrier huỷ nhận đơn, rồi mở block LỊCH SỬ | Dòng "Ghép thành công" **VẪN CÒN** + có thêm dòng log huỷ nhận. ⚠ Dự kiến FAIL — app hiện **XOÁ** dòng "Ghép thành công" (vi phạm `BR-INT-04` audit) → log bug | P2 | Business Rule | NEW |
| SC-CNL-011 | Đồng bộ realtime 3 bên khi huỷ | REQ-CNL-005 | DOC-v1.0-01 §A5 BR-INT-05 L81 · §D2 L233 | Đơn "Đã ghép" mở đồng thời trên 3 phiên/thiết bị (Sender · Carrier · Receiver) | 1 vai huỷ đơn | Cả 3 phiên cập nhật trạng thái huỷ mà không cần làm mới thủ công | P2 | Functional | NEW |
| SC-CNL-012 | [GAP·bug] Không trim khoảng trắng khi đếm lý do | REQ-CNL-002 | DOC-v1.0-01 §D8.3 VAL-03 L394 · VAL-04 L395 · KP-01 §7 KB-CNL-02 | Popup huỷ đơn đang mở | Nhập lý do gồm **5 dấu cách** rồi quan sát nút Xác nhận | Nút Xác nhận **bị khoá** (sau khi trim thì lý do rỗng — `VAL-03`+`VAL-04`). ⚠ Dự kiến FAIL — app hiện cho qua → log bug | P3 | Business Rule | NEW |
| SC-CNL-013 | Ma trận quyền huỷ theo vai × trạng thái | REQ-CNL-005 | DOC-v1.0-01 §D4 (permission matrix) L285 · §D7 OPR-11 L347 | Có đơn ở từng trạng thái `Chờ ghép` · `Đã ghép` · `Đang giao` | Với mỗi trạng thái, kiểm quyền huỷ của cả 3 vai | Khớp permission matrix: Sender/Receiver huỷ được **trước IN_TRANSIT**; Carrier "huỷ nhận" → về Chờ ghép; từ "Đang giao" **không vai nào** huỷ được | P2 | Business Rule | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-CNL-001 / SC-CNL-002 / SC-CNL-003 — Huỷ đơn ở POSTED · MATCHED · rule khoá nút Xác nhận

**Source Quote:**
> "Huỷ được ở POSTED/MATCHED; popup huỷ bắt buộc nhập lý do (nút Xác nhận khoá tới khi có lý do); đơn huỷ ghi rõ ai huỷ (Người gửi/Người vận chuyển/Người nhận) + lý do, đồng bộ realtime cho cả 3 bên; Carrier huỷ nhận → đơn trả lại bảng tin (về "Chờ ghép"); sau IN_TRANSIT phải tạo báo cáo sự cố"

**Source Location:** `DOC-v1.0-01 §D1b · US-D16 · Acceptance Criteria · L195`

**Analyst Note:** `US-D16` là **AC đầy đủ nhất** của module (nêu cả 5 rule trong 1 dòng) ⇒ fan-out thành nhiều SC. Tách `POSTED` và `MATCHED` thành 2 SC vì **hệ quả khác nhau**: huỷ ở `POSTED` chỉ ảnh hưởng chủ tin; huỷ ở `MATCHED` ảnh hưởng **cả Carrier và Receiver** (đã có cặp ghép, đã lộ SĐT). ⚠️ `BR-INT-05` (§A5 L81) chỉ nói *"Huỷ **sau khi MATCHED** phải có lý do"* — nhưng `BR-CNL-01`+`US-D16` yêu cầu lý do cho **mọi** lượt huỷ ⇒ chọn bản rộng hơn.

##### SC-CNL-004 / SC-CNL-012 — [GAP·bug] `VAL-04` không được enforce

**Source Quote:**
> Spec (`VAL-04` §D8.3 L395): "Huỷ đơn: bắt buộc nhập lý do (**tối thiểu 5 ký tự**) mới bật nút Xác nhận"
> Spec (`VAL-03` §D8.3 L394): "Tự cắt khoảng trắng đầu/cuối; chuẩn hoá SĐT… trước khi lưu"
> Hành vi (`KP-01` §7 `KB-CNL-02`): "**Thực tế UI (CA live-verify):** chỉ chặn khi để **rỗng**; nhập 4 ký tự vẫn bật nút, và **không trim khoảng trắng trước khi đếm** (5 dấu cách vẫn qua)."

**Source Location:** `DOC-v1.0-01 §D8.3 · VAL-04 · L395` và `VAL-03 · L394` ⟷ `DOC-v1.0-06 KP-01 §7 "KB-CNL-02"` (live-verify Chrome MCP 2026-07-29)

**Analyst Note:** ⭐ **2 gap đã live-verify**, tách 2 SC vì là **2 lỗi khác nhau**: (a) **ngưỡng 5 ký tự** không enforce (`SC-CNL-004`); (b) **không trim** trước khi đếm (`SC-CNL-012`) — gap (b) vi phạm **cả `VAL-03` và `VAL-04`**. Cả 2 viết theo **spec** ⇒ **dự kiến FAIL**; đợt cũ đã cố ý viết TC bắt 2 gap này (`KP-05 §4` — *"4 test case CỐ Ý viết để FAIL"*). ⛔ Không sửa expected cho PASS.

##### SC-CNL-005 / SC-CNL-006 — Chặn huỷ từ "Đang giao" · [GAP] không có bề mặt tạo sự cố

**Source Quote:**
> "đã lấy hàng → sang "Đang giao" thì **KHÔNG ai được huỷ**"
> "BR-ASN-03 | Sau khi nhận hàng (IN_TRANSIT) không hủy thường → **phải tạo sự cố**"
> "Màn "Báo sự cố" chưa có đặc tả — out of scope v1.0"

**Source Location:** `DOC-v1.0-01 §D7 · OPR-11 · L347` · `§D4 · BR-ASN-03 · L264` ⟷ `DOC-v1.0-06 KP-01 §5 "KB-DLV-05"`

**Analyst Note:** Vế **chặn huỷ** có 3 nguồn đồng thuận ⇒ `SC-CNL-005` P1 với oracle rõ, và phải kiểm **cả 3 vai** (`OPR-11` viết *"KHÔNG **ai** được huỷ"*). Vế **tạo sự cố** thì màn "Báo sự cố" out of scope (`C-CNL-01`) ⇒ `SC-CNL-006` chỉ **ghi nhận sự thiếu vắng** theo `§Custom Rules §10.1` bước 3 — đây là **gap có chủ đích của sản phẩm**, không phải bug.

##### SC-CNL-007 — Carrier huỷ nhận → đơn về "Chờ ghép"

**Source Quote:**
> "OPR-09 | Carrier huỷ khi chưa lấy hàng → trả đơn về bảng tin | Người vận chuyển huỷ ở trạng thái Đã ghép (chưa "Tôi đã lấy hàng") → đơn tự động về "Chờ ghép" và hiển thị lại trên bảng tin cho người khác nhận"

**Source Location:** `DOC-v1.0-01 §D7 · OPR-09 · L345` (đồng thuận `§D1b · US-D16 · L195`)

**Analyst Note:** ⚠️ **Điểm dễ trộn nhất của module:** *"Huỷ đơn"* (Sender/Receiver → `CANCELLED`, đơn kết thúc) ⟷ *"Huỷ nhận đơn"* (Carrier → đơn **về `POSTED`**, tiếp tục sống). Nhãn nút cũng khác: `Huỷ đơn` vs `✕ Huỷ nhận đơn` (`KB-DLV-01` ô 2·Carrier). Then có mệnh đề phủ định *"đơn KHÔNG chuyển Đã huỷ"* để chặn đúng lỗi hiểu sai này. Hệ quả *"ghép lại được bởi người khác"* đã có SC ở `ASN` (`SC-ASN-017`) ⇒ ⛔ không nhân bản.

##### SC-CNL-008 / SC-CNL-011 / SC-CNL-013 — Ghi vai trò + lý do · realtime 3 bên · ma trận quyền

**Source Quote:**
> "Ngoài luồng: [CANCELLED "Đã huỷ"] — bắt buộc lý do; ghi rõ ai huỷ (Sender/Carrier/Receiver); đồng bộ realtime cả 3 bên; Carrier huỷ → trả đơn về "Chờ ghép""
> (`§D4` permission matrix L285): "Huỷ đơn (bắt buộc lý do) | ✓ trước IN_TRANSIT | ✓ → về Chờ ghép | ✓ trước IN_TRANSIT | ✓"

**Source Location:** `DOC-v1.0-01 §D2 · block code 2 · L233` và `§D4 · bảng Permission Matrix · L285`

**Analyst Note:** `§D4` permission matrix cho **ma trận quyền huỷ 4 vai × trạng thái** ⇒ `SC-CNL-013` là SC tổng hợp (không trùng `SC-CNL-001/002/005/007` vì nó kiểm **toàn bộ ma trận trong 1 lượt so sánh**, phát hiện được ô "lẽ ra không được huỷ mà vẫn huỷ được"). ⚠️ Cột `Admin` của matrix (*"✓"*) **không test được** — Admin Portal out of scope (`C-TS-01`). `SC-CNL-011` cần **3 phiên/thiết bị** như `SC-ASN-008`.

##### SC-CNL-009 / SC-CNL-010 — [GAP·bug] Log LỊCH SỬ khi huỷ

**Source Quote:**
> "- **Huỷ đơn** (Sender/Receiver) → **không ghi log nào** vào block LỊCH SỬ, chỉ hiện banner đỏ *"Đơn hàng đã bị huỷ"*"
> "- **Huỷ nhận đơn** (Carrier) → tệ hơn: **XOÁ LUÔN dòng "Ghép thành công"** khỏi LỊCH SỬ"
> "User chốt: *"huy don va huy nhan don hien tai cu luu log lich su nha"* → **LỊCH SỬ phải ghi log cho cả 2 hành động; hành vi hiện tại là GAP cần dev bổ sung.**"
> Rule bị vi phạm (`BR-INT-04` §A5 L80): "Timeline tương tác không sửa được sau khi ghi (audit)"

**Source Location:** `DOC-v1.0-06 KP-01 §7 "KB-CNL-01"` (live-verify Chrome MCP 2026-07-29 + user chốt) ⟷ `DOC-v1.0-01 §A5 · BR-INT-04 · L80`

**Analyst Note:** ⭐ **REQ do QA/user ban hành để override hành vi hiện tại** (`C-CNL-02` Resolved theo hướng override). **2 gap khác mức độ:** `SC-CNL-009` = *thiếu* log (vi phạm `TS-01`); `SC-CNL-010` = **XOÁ log đã có** — nghiêm trọng hơn vì vi phạm trực tiếp `BR-INT-04` (*"không sửa được sau khi ghi"*) và `TS-02` (audit trail). ⇒ 2 SC riêng, **dự kiến FAIL**. ⚠️ Liên hệ chéo: `SC-DLV-029` (timeline đủ mốc) phải chạy trên đơn **đi thẳng tới Hoàn thành**, vì đơn từng bị huỷ nhận sẽ **thiếu mốc "Ghép thành công"** do bug này.

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| — | *(không có — v1.0 là version đầu của chuỗi phân tích mới)* | — | — | — | — |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
