# Requirement Traceability — v1.1 · Module NTF (Delta)

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation` của `DOC-v1.1-01`: `FR<NN>` / `BR<FF>-NN` / `AC-{US}.{Scenario}.{Case}` / `NFR-NN` ⇒ **Schema A**.
> ⚠️ File này **CHỈ chứa REQ NEW + MODIFIED của v1.1**. REQ CARRIED (REQ-NTF-001, 002, 004, 006, 007, 008, 009, 011) giữ nguyên như `v1.0/NTF-thong-bao/requirement_traceability.md` — KHÔNG duplicate ở đây, xem bảng CARRIED cuối §1.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module NTF — DOC-v1.1-01 (NEW + MODIFIED)

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-NTF-003 | `FR13`, bảng §8.13.1 dòng `NTF-06` | `DOC-v1.1-01` §8.13.1 · page 48 | SC-NTF-005 (MODIFIED) | — (resolved) |
| REQ-NTF-005 | `FR13`, bảng §8.13.1 (toàn bộ 15 dòng) | `DOC-v1.1-01` §8.13.1 · page 47-48 | SC-NTF-008 (MODIFIED) | — |
| REQ-NTF-010 | `FR13`, §8.13.1 | `DOC-v1.1-01` §8.13 · §8.13.1 · page 47-48 | SC-NTF-014 (MODIFIED) | C-NTF-01 (resolved) |
| REQ-NTF-012 | `FR13` — `NTF-10`..`NTF-15` | `DOC-v1.1-01` §8.13.1 · page 48 | SC-NTF-017..022 (NEW) | — |

### REQ CARRIED (không đổi — xem `v1.0/NTF-thong-bao/requirement_traceability.md`)
REQ-NTF-001, REQ-NTF-002, REQ-NTF-004, REQ-NTF-006, REQ-NTF-007, REQ-NTF-008, REQ-NTF-009, REQ-NTF-011.

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-NTF-003 · Thông báo theo mốc vận chuyển (`NTF-04`/`NTF-05`/`NTF-06`) — MODIFIED
📍 `DOC-v1.1-01 §8.13.1 · page 48` · Clarif: — (phần `NTF-06` được resolve, không còn gắn `C-NTF-01`)

**Source Quote (old) — `DOC-v1.0-01` §D6 L324 (v1.0):**
> "NTF-06 | Người nhận "Xác nhận đã nhận hàng" (COMPLETED) | Người gửi · Người vận chuyển | "Đơn đã hoàn tất — cảm ơn bạn!""
> (mâu thuẫn với `DOC-v1.0-06 KP-07` hàng #6 — Figma/PRD-demo ghi *"Đơn đã hoàn thành — đánh giá ngay"*)

**Source Quote (new) — `DOC-v1.1-01` §8.13.1 · page 48:**
> "NTF-06 | Người nhận xác nhận đã nhận hàng (COMPLETED) | Người gửi · Người vận chuyển | "Đơn đã hoàn tất — cảm ơn bạn!""

↳ **Ghi chú (diff):** PRD chính thức v1.1 dùng **đúng bản BRD cũ** ("cảm ơn bạn!"), không dùng từ "đánh giá" của bản Figma/PRD-demo cũ. Vì bản Figma/PRD-demo trước đây là nguồn phi chính thức (`DOC-v1.0-02`/`DOC-v1.0-04`) trong khi `DOC-v1.1-01` là PRD chính thức có phê duyệt (§12 Approval), quyết định dùng **DOC-v1.1-01 làm nguồn thắng** cho text `NTF-06` kể từ v1.1. `SC-NTF-005` chuyển từ "ghi nhận, không assert" sang **assert đúng text**.

---

### REQ-NTF-005 · SĐT KHÔNG được đưa vào nội dung push — MODIFIED (mở rộng phạm vi)
📍 `DOC-v1.1-01 §8.13.1 · page 47-48` · Clarif: —

**Source Quote (old) — `DOC-v1.0-01` §D7 OPR-07 · L343 (v1.0, vẫn còn hiệu lực):**
> "SĐT chỉ lộ sau khi ghép, chỉ cho đúng 2 người trong cặp; không đưa SĐT vào nội dung push"

**Source Quote (new) — `DOC-v1.1-01` §8.13.1, đối chiếu toàn bộ 15 dòng nội dung mẫu:**
> "NTF-10 | Giao cho người được uỷ quyền | Người nhận · Người gửi | "Hàng đã được giao cho {tên người nhận thay} (uỷ quyền bởi {người gửi/người nhận}) — có ảnh bằng chứng""
> "NTF-11 | Gửi tại quầy lễ tân / bảo vệ | Người nhận · Người gửi | "Hàng đang được giữ tại {quầy lễ tân/bảo vệ} — người giữ: {tên} — vui lòng nhận trong hôm nay""
> "NTF-12 | Người vận chuyển không liên lạc được người nhận | Người gửi | "Người vận chuyển không liên lạc được người nhận — cần bạn xác nhận uỷ quyền cho người khác nhận hàng""

↳ **Ghi chú (diff):** Đối chiếu **cả 15 dòng nội dung mẫu** của bảng `§8.13.1` (không chỉ 9 dòng cũ): không dòng nào — kể cả 6 dòng mới `NTF-10..15` — chứa số điện thoại trong nội dung, kể cả các tình huống nhạy cảm nhất (giao cho người thay, không liên lạc được). Rule `OPR-07`/`NFR12` (Privacy — "Dữ liệu người nhận thay chỉ dùng làm bằng chứng bàn giao; không xuất hiện ở bất kỳ báo cáo/thống kê nào ngoài tài liệu") tiếp tục có hiệu lực. `SC-NTF-008` mở rộng Given để phủ đủ 15 sự kiện.

---

### REQ-NTF-010 · Danh sách loại thông báo chính thức — MODIFIED (RESOLVED)
📍 `DOC-v1.1-01 §8.13 · §8.13.1 · page 47-48` · Clarif: `C-NTF-01` → **Resolved 2026-09-15**

**Source Quote (old) — ambiguous, `DOC-v1.0-01` §D6 L315 (v1.0):**
> "Danh sách sự kiện bắn thông báo dựa trên flow & màn hình hiện có của prototype. **Nháp — chờ BA review & bổ sung.**"

**Source Quote (new) — `DOC-v1.1-01` §8.13 · page 47:**
> "Description | Thông báo đẩy và trong ứng dụng theo các sự kiện của vòng đời đơn, đảm bảo ba vai trò luôn biết chuyện gì đang xảy ra mà không phải gọi điện hỏi nhau."

> "§8.13.1 Danh mục thông báo" — bảng 15 dòng `NTF-01`..`NTF-15` (ID | Sự kiện kích hoạt | Người nhận | Nội dung (mẫu)), page 48.

↳ **Ghi chú (diff):** PRD chính thức **chốt dứt điểm** danh mục thông báo — thay thế hoàn toàn tình trạng "Nháp — chờ BA review" của BRD cũ. `C-NTF-01` (Open từ 2026-07, High risk, CL lớn nhất module) **Resolved 2026-09-15**: danh mục chính thức = **15 sự kiện** (9 sự kiện cũ NTF-01..09 giữ nguyên nội dung/người nhận, cộng 6 sự kiện mới NTF-10..15 gắn với nhánh xử lý giao hàng không thành công của `DLV` FR08/FR09). Hàng "#10 Sắp đến khung giờ hẹn giao" mà `KP-07` từng nghi BRD sót — PRD v1.1 **không đưa vào danh mục chính thức** ⇒ xác nhận đây KHÔNG phải sự kiện chính thức của v1.1, đóng luôn nghi vấn đó. `SC-NTF-014` chuyển từ "[GAP] ghi nhận, không assert" sang **assert đủ 15 loại theo danh mục chính thức**.

---

### REQ-NTF-012 · Thông báo cho nhánh xử lý giao hàng không thành công (`NTF-10`..`NTF-15`) — NEW
📍 `DOC-v1.1-01 §8.13.1 · page 48` · Clarif: —

**Source Quote:**
> "NTF-10 | Giao cho người được uỷ quyền | Người nhận · Người gửi | "Hàng đã được giao cho {tên người nhận thay} (uỷ quyền bởi {người gửi/người nhận}) — có ảnh bằng chứng""
> "NTF-11 | Gửi tại quầy lễ tân / bảo vệ | Người nhận · Người gửi | "Hàng đang được giữ tại {quầy lễ tân/bảo vệ} — người giữ: {tên} — vui lòng nhận trong hôm nay""
> "NTF-12 | Người vận chuyển không liên lạc được người nhận | Người gửi | "Người vận chuyển không liên lạc được người nhận — cần bạn xác nhận uỷ quyền cho người khác nhận hàng""
> "NTF-13 | Người vận chuyển chọn hẹn giao lại (RESCHEDULED) | Người nhận · Người gửi | "Người vận chuyển sẽ giao lại vào {ngày · giờ} tại {nơi hẹn}""
> "NTF-14 | Người vận chuyển chọn trả hàng về người gửi (RETURNING) | Người gửi · Người nhận | "Hàng được cầm về — vui lòng nhận lại vào {ngày · giờ} tại {nơi hẹn}""
> "NTF-15 | Người gửi xác nhận đã nhận lại hàng (RETURNED) | Người vận chuyển · Người nhận | "Đơn đã đóng — hàng đã được trả lại người gửi""

↳ **Ghi chú:** 6 sự kiện **hoàn toàn mới**, không tồn tại ở v1.0 — vì v1.0 không có đặc tả chi tiết cho nhánh "không liên lạc được người nhận" (chỉ có ma trận 15 ô chung chung từ QA-obs+Figma). Đây là hệ quả trực tiếp của FR08 ("Xử lý khi không liên lạc được người nhận") và FR09 ("Cầm hàng về: hẹn giao lại / hoàn hàng") — 2 luồng nghiệp vụ đang được phân tích delta song song ở module `DLV`. **Module NTF chỉ test đúng sự kiện có bắn thông báo, đúng người nhận, đúng nội dung** — KHÔNG lặp lại test luồng nghiệp vụ giao nhận (đã có SC ở `DLV`). Fan-out 6 SC riêng theo nguyên tắc mỗi state-transition/nhánh = 1 SC.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
