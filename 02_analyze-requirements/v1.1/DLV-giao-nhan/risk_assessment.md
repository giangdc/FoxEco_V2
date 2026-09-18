---
id: v1.1/DLV-giao-nhan/risk
title: Risk Assessment — v1.1 · Module DLV
type: risk-assessment
version: v1.1
sprint: 1
module: DLV
counts:
  cl: 8
  risk: 11
  cl_open: 0
  cl_resolved: 7
status: ANALYZED
updated: 2026-09-17
---

# Risk Assessment — v1.1 · Module DLV (DELTA)

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (7 dòng, `RISK-DLV-01..07`) xem `v1.0/DLV-giao-nhan/risk_assessment.md` — KHÔNG lặp lại ở đây. **ID mới bắt đầu từ `RISK-DLV-08`** (v1.0 đã dùng hết tới `-07`).
> ℹ️ `cl_open (0) + cl_resolved (7) = 7 < cl (8)` — **đúng, không lệch cộng**: chỉ còn `C-DLV-08` ở trạng thái **🟡 Partially Resolved** — câu (d) đã đóng 2026-09-17 (role admin ngoài scope phase này), còn (a)(b) **không hỏi BA nữa** mà tự xác minh bằng vibe-check block LỊCH SỬ. `C-DLV-05`/`C-DLV-06` Resolved 2026-09-17; **`C-DLV-07` Resolved 2026-09-17 (vòng 2)** ⇒ `DLV` hết CL Open.

## Tổng quan
| Module | Risk Level | Rủi ro chính (delta v1.1) |
|--------|-----------|--------------|
| DLV | **High** (không đổi so với v1.0) | Module delta nặng nhất (34 SC mới). 2 rủi ro High mới: `RISK-DLV-08` màn "Xác nhận giao hàng" mở rộng 4 loại đối tượng nhận — cấu trúc UI đã khớp nhưng **luồng submit chưa verify end-to-end**; `RISK-DLV-09` `NFR-07` log append-only đụng thẳng bug audit đã biết (`RISK-TS-01`) ⇒ `SC-DLV-062` dự kiến FAIL |

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-DLV-05 | DLV / Nhánh phụ scope | *(cập nhật Status 2026-09-16)* 3 REQ không SC của v1.0 — `PUP-03` (ảnh lúc lấy hàng) **Resolved** qua `BR06-01`; `GPS-01` (chia sẻ vị trí) **Resolved — BA 2026-09-16: "Không có chức năng này"**; `COST-01` (chi phí) **Resolved — out of scope**: `§4 Out of Scope` ghi rõ *"Thanh toán, ví điện tử, ghi nhận chi phí vận chuyển"* (⚠️ đính chính: bản 2026-09-15 ghi *"PRD không nhắc"* là **sai**) | Medium → **Resolved (3/3)** | `DOC-v1.1-01` §8.6.1 BR06-01 · §4 SCOPES Out of Scope (trang 9) · BA trả lời `C-DLV-02` 2026-09-16 | `SC-DLV-035/036` cho PUP-03; `GPS-01`/`COST-01` **không viết SC** — ngoài scope đã chốt | Nếu STG có bề mặt chia sẻ vị trí / nhập chi phí ⇒ log finding *"tính năng ngoài scope"* | **Resolved** | REQ-DLV-012, REQ-DLV-013, REQ-DLV-014 |
| RISK-DLV-08 | DLV / Xác nhận giao hàng | *(cập nhật Status — lần 2)* `REQ-DLV-017` (`FR07`) mở rộng lớn từ 1 nút+popup sang form đầy đủ 4 loại đối tượng nhận — nguy cơ app STG **chưa build lại** theo PRD mới ⇒ 6 SC mới (`SC-DLV-037..042`) FAIL hàng loạt vì lý do "app chưa cập nhật", không phải bug thật | High → Partially confirmed → **Confirmed qua demo (2026-09-16)** | `DOC-v1.1-01` §8.7 vs demo `foxeco_demo/FoxEcoQC` (2026-09-15, 2026-09-16) | Vibe-test 1 lượt màn "Xác nhận giao hàng" trước `generate-tc`, đối chiếu đúng 4 loại đối tượng nhận có tồn tại chưa | **Cấu trúc UI đã khớp** (2026-09-15) — 4 lựa chọn "Giao cho" đúng `BR07-03..05`. **2026-09-16 — luồng submit end-to-end ĐÃ verify được**: dropzone "Ảnh bằng chứng" hoạt động (khác nhận định 2026-09-15 — lần này click đúng `<input type=file>` ẩn phía sau, chọn ảnh thành công, bộ đếm lên `1/5`), nút "Xác nhận đã giao hàng" bật lên và bấm được, đơn chuyển đúng `IN_TRANSIT → DELIVERED → COMPLETED` sau khi Receiver xác nhận. Toàn bộ chu trình Carrier nhận đơn → lấy hàng (có ảnh) → giao hàng (có ảnh + chọn "Người nhận") → Receiver xác nhận chạy đúng, không lỗi | **Confirmed qua demo** — cấu trúc + luồng submit đều khớp PRD; khuyến nghị 1 lượt double-check nhanh trên STG thật trước khi hardening automation locator (đúng caveat chung), nhưng không còn là blocker | REQ-DLV-017, SC-DLV-037..042 |
| RISK-DLV-09 | DLV / Audit log | **(risk mới)** `NFR-07` (log append-only, không API sửa/xoá) chính thức hoá yêu cầu mà bug đã biết (`RISK-TS-01`, huỷ nhận đơn xoá dòng "Ghép thành công") đang **vi phạm trực tiếp** — SC mới `SC-DLV-062` dự kiến FAIL cho tới khi bug được fix | High | `DOC-v1.1-01` §9 NFR-07 vs `v1.0/TS-trust-safety/risk_assessment.md RISK-TS-01` | `SC-DLV-062` (P1) | Cross-ref bug đã log (nếu có) ở `05_bug-reports/`; nếu chưa log → ưu tiên log-bug trước execute | Open — dự kiến FAIL có chủ đích cho tới khi fix | REQ-DLV-022, SC-DLV-062 |
| RISK-DLV-10 | DLV / Tiền đề thời gian mới | **(risk mới)** `SC-DLV-048` (4h/24h giữ hàng tại quầy) và `SC-DLV-054` (24h quá hẹn cầm hàng về) cùng nhóm khó như `RISK-DLV-04` cũ (`SC-DLV-024`) — cần thời gian thực hoặc seed timestamp, dễ bị "đánh PASS cho xong" | Medium | `DOC-v1.1-01` §8.8.1 BR08-06 · §8.9.1 BR09-04 | `SC-DLV-048`, `SC-DLV-054` | Gộp kế hoạch chạy chung với `SC-DLV-024`/`SC-TS-006` (cùng nhóm tiền đề thời gian dài) | Open | REQ-DLV-018, REQ-DLV-019, SC-DLV-048, SC-DLV-054 |
| RISK-DLV-11 | DLV / Ảnh lúc lấy hàng | **(phát hiện qua vibe-check demo 2026-09-15, tái xác nhận 2026-09-16)** `C-DLV-04` đã Resolved theo PRD (`BR06-01` — ảnh lúc lấy hàng tồn tại, tuỳ chọn, trần 5) nhưng **demo hiện tại KHÔNG có field đính ảnh** ở popup "Tôi đã lấy hàng" — chỉ có 2 nút Huỷ/Xác nhận đơn giản, giống hệt bản v1.0 chưa cập nhật | Medium | So khớp `DOC-v1.1-01 §8.6.1 BR06-01` vs ảnh `00_input/v1.1/design/DLV_07_toidalayhang_popup_khongco_anhluclayhang.png` | `SC-DLV-035` (có ảnh), `SC-DLV-036` (không ảnh) | Cùng pattern `RISK-DLV-08` — verify lại trên STG thật trước `generate-tc`; nếu STG cũng thiếu field này thì đây là **defect** (PRD/app lệch), không phải TC sai | Open (cần vibe-test STG xác nhận) | REQ-DLV-012, SC-DLV-035, SC-DLV-036 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-DLV-04 | Ảnh lúc lấy hàng (`PUP-03`) có tồn tại ở app không, tuỳ chọn hay bắt buộc? | ✅ **Resolved 2026-09-15** | mở cùng lượt (chỉ để ghi nhận resolve) | REQ-DLV-012, SC-DLV-035, SC-DLV-036 |
| C-DLV-02 | Chia sẻ vị trí (`GPS-01`) mặc định bật hay tắt (bản gốc `v1.0/DLV-giao-nhan/`) | ✅ **Resolved 2026-09-16 — BA: "Không có chức năng này"** ⇒ out of scope | kế thừa 2026-07 | REQ-DLV-013 |
| C-DLV-05 | Hẹn giao lại (RESCHEDULED): tự về IN_TRANSIT hay Carrier bấm; RESCHEDULED → RETURNING ai/đâu; giới hạn số lần hẹn; timeline 5 mốc hiển thị các trạng thái mới | ✅ **Resolved 2026-09-17** — (d) timeline giữ 5 mốc cố định, không nhãn phụ, xác nhận là thiết kế | 2026-09-17 | REQ-DLV-019, REQ-DLV-002, SC-DLV-016, SC-DLV-031, SC-DLV-050 |
| C-DLV-06 | Màn "Không liên lạc được người nhận": modal 2 hướng hay danh sách 4 nhánh; thứ tự chốt bảo vệ ⟷ quầy lễ tân; lựa chọn "người uỷ quyền đã khai sẵn" nằm ở đâu | ✅ **Resolved 2026-09-17** — cấu trúc 4 tầng xác nhận chuẩn; 2 ô quầy bắt buộc, chỉ ghi chú | 2026-09-17 | REQ-DLV-018, SC-DLV-043 |
| C-DLV-07 | "Nhắc" + "chuyển admin hỗ trợ" (2h/4h · 4h/cuối ngày/24h · 24h quá hẹn): thông báo nào, "cuối ngày" mấy giờ, đơn có đổi trạng thái/nhãn không khi không có công cụ admin | ✅ **Resolved 2026-09-17 (vòng 2)** — BA: hệ thống **CHỈ gửi remind**, không đổi trạng thái/nhãn; vế "chuyển admin hỗ trợ" **out of scope phase này** | 2026-09-16 | REQ-DLV-018, REQ-DLV-019, SC-DLV-024, SC-DLV-048, SC-DLV-054 |
| C-DLV-08 | Chọn "Quầy lễ tân/Quầy bảo vệ" **trực tiếp** ở màn Xác nhận giao hàng khác gì đi qua luồng "Không liên lạc được" (cờ, thông báo, "Uỷ quyền bởi") | 🟡 **Partially Resolved 2026-09-17 (vòng 4)** — (d) hạn giữ hàng/chuyển admin **out of scope phase này** (BA); còn (a)(b) cờ + `NTF-05`/`NTF-11` — **QA tự xác minh qua block LỊCH SỬ**, không hỏi BA nữa | 2026-09-16 | REQ-DLV-017, REQ-DLV-018, SC-DLV-039, SC-DLV-045 |

### C-DLV-04 · Ảnh lúc lấy hàng — tuỳ chọn hay bắt buộc? *(RESOLVED)*

📍 `DOC-v1.1-01 §8.6.1 BR06-01 · trang 38`

> ↪ *Quote `BR06-01` — home ở `requirement_traceability.md` · `REQ-DLV-012` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

↳ **Ghi chú:** PRD chính thức resolve gap có chủ đích của v1.0 (`RISK-DLV-05` — PM chưa trả lời `KP-05 §1` câu #2). Kết luận: **tồn tại**, **tuỳ chọn**, trần **5 ảnh**. Không blocking, chỉ ghi nhận.

> ⚠️ `C-DLV-01` (Receiver-only, Resolved v1.0) **không đổi**. `C-DLV-02` **Resolved 2026-09-16** (xem khối trả lời BA dưới) — bản gốc `v1.0/DLV-giao-nhan/risk_assessment.md` giữ nguyên làm hồ sơ lịch sử.
> ↳ **Cập nhật 2026-09-16 — bằng chứng phụ cho `C-DLV-02` (KHÔNG resolve):** Vibe-check qua demo, đẩy 1 đơn thật tới trạng thái `IN_TRANSIT` ("Đang giao") ở vai Carrier — màn "Theo dõi đơn" tại trạng thái này **không có bất kỳ control chia sẻ vị trí nào** (không toggle, không nút, không banner). Củng cố thêm nghi vấn v1.0 rằng bề mặt GPS-01 **không tồn tại** trên app hiện tại. Đây là quan sát phủ định (không thấy tính năng) nên **không đủ để Resolve** — vẫn cần PM xác nhận chính thức có đưa GPS-01 vào scope v1.1 hay không.

### C-DLV-02 · ↳ BA trả lời 2026-09-16 *(→ RESOLVED)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `DLV` · cột "Câu trả lời BA" · 2026-09-16

> "Không có chức năng này"

↳ **Ghi chú:** Chia sẻ vị trí khi đang giao (`GPS-01`) **không có trong sản phẩm** — khớp quan sát demo 2026-09-16 (màn "Đang giao" không có control vị trí) và khớp `§4 Out of Scope` (*"Ghép nối tự động nâng cao theo độ gần địa lý bằng bản đồ/toạ độ"*). ⇒ `REQ-DLV-013` **out of scope đã chốt**, không còn là *"gap có chủ đích chờ PM"*; `RISK-DLV-05` đóng 3/3. ⚠️ Không nhầm với **bản đồ ở Chi tiết tin** (`C-FEED-01(b)` — BA xác nhận **có** bản đồ thật): đó là bản đồ tuyến tĩnh, không phải chia sẻ vị trí realtime.

### C-DLV-05 · Hẹn giao lại — cơ chế chuyển trạng thái *(RESOLVED 2026-09-17 — vòng 3)*

📍 `DOC-v1.1-01 §6.2 AC-18.1.01 · trang 23` · `§8.9.1 BR09-05 · trang 42` · `§8.12.2 dòng RESCHEDULED · trang 45` · `§8.12.3 dòng RESCHEDULED · trang 46` · `§5.1 "Timeline theo dõi 5 mốc" · trang 10`

> `AC-18.1.01`: "…Đơn sang RESCHEDULED (không tính là huỷ đơn), lưu lịch hẹn vào đơn. Người gửi và người nhận nhận NTF-13. Theo lịch hẹn, đơn quay lại IN_TRANSIT để người vận chuyển giao lại."

> `§8.12.2`: "RESCHEDULED | Hẹn giao lại | … | → IN_TRANSIT (theo lịch hẹn) · RETURNING · INCIDENT"

> `§8.12.3`: "RESCHEDULED | Xem lịch hẹn giao lại | Giao lại theo lịch (mở lại màn giao hàng) | Xem lịch hẹn"

> `§5.1`: "Timeline theo dõi 5 mốc: Chờ ghép · Lấy hàng · Đang giao · Đã giao · Hoàn thành"

↳ **Ghi chú:** (a) *"Theo lịch hẹn, đơn quay lại IN_TRANSIT"* — **hệ thống tự chuyển** đúng giờ hẹn, hay **Carrier bấm "Giao lại"** (§8.12.3)? Carrier có giao **sớm hơn** lịch hẹn được không? (`SC-DLV-050` đang giả định Carrier bấm.) (b) Chuyển tiếp **RESCHEDULED → RETURNING** có trong từ điển nhưng **không AC nào** mô tả: ai bấm, từ màn nào, có nhập lịch hẹn mới? (c) Hẹn giao lại **được mấy lần** — không giới hạn? (d) Timeline chỉ có **5 mốc** trong khi đơn có thể đi qua RESCHEDULED / RETURNING / RETURNED / INCIDENT — các trạng thái này hiện **ở mốc nào / nhãn gì** trên thanh tiến trình (`SC-DLV-016`)?

↳ **BA trả lời 2026-09-16 + vibe-check demo 2026-09-17 (Playwright MCP, tái xác nhận vibe-check 2026-09-15 đã có ở `DLV_06`):** (a) BA "đúng" — hệ thống/Carrier: đã thao tác demo, Carrier chọn "Cầm hàng về" → "Tôi sẽ giao lại sau" hiện khối "Hẹn trả hàng" (Ngày hẹn + Từ/Đến giờ + Nơi nhận lại hàng) do CHÍNH Carrier tự nhập ngay tại màn "Xử lý đơn hàng" — không phải hệ thống tự sinh giờ hẹn, và không thấy gate chặn theo giờ (Carrier có thể chọn bất kỳ lúc nào). (b) BA "người vận chuyển chọn Cầm hàng về" — khớp: nhánh RESCHEDULED→RETURNING đi qua đúng lựa chọn "Cầm hàng về" → "Tôi sẽ trả về cho người gửi" ở cùng màn "Xử lý đơn hàng". (c) BA "không giới hạn" — không thấy bộ đếm/giới hạn số lần hẹn trên UI, khớp câu trả lời. (d) BA "đang giao" — thanh tiến trình vẫn giữ nguyên 5 mốc cũ, không có mốc phụ cho RESCHEDULED/RETURNING, trạng thái đơn vẫn hiển thị "Đang giao" xuyên suốt — khớp quan sát demo. **Còn treo (d):** BA trả lời ngắn gọn "đang giao" nhưng chưa xác nhận rõ đây là quyết định thiết kế (giữ nguyên 5 mốc vĩnh viễn) hay chỉ là giới hạn demo chưa cập nhật UI — cần BA xác nhận dứt điểm trước `generate-tc` để quyết TC có assert "vẫn hiện Đang giao" hay chờ UI mới.

↳ **BA trả lời 2026-09-17 (vòng 3, câu (d) duy nhất còn treo):** "đúng nhé" — xác nhận đây LÀ quyết định thiết kế (không phải giới hạn demo): timeline giữ nguyên **5 mốc cố định** (Chờ ghép/Lấy hàng/Đang giao/Đã giao/Hoàn thành), **KHÔNG** có nhãn phụ cho RESCHEDULED/RETURNING/RETURNED/INCIDENT — các trạng thái này đi "ẩn" phía sau nhãn "Đang giao" trên timeline. `SC-DLV-016` assert được: timeline luôn hiện đúng 5 mốc, mốc "Đang giao" active xuyên suốt kể cả khi đơn thực chất đang ở RESCHEDULED/RETURNING. `C-DLV-05` ĐÓNG HẲN 2026-09-17.

### C-DLV-06 · Cấu trúc màn "Không liên lạc được người nhận" *(RESOLVED 2026-09-17 — vòng 3)*

📍 `DOC-v1.1-01 §8.8.1 BR08-02 · trang 41` ⟷ `§6.2 AC-16.1.01 · trang 22` · `§6.2 AC-17.1.01 · trang 22` · `§8.8.2 dòng "Phương án xử lý" · trang 42`

> `BR08-02`: "Thứ tự ưu tiên xử lý (màn hình sắp xếp đúng thứ tự này): (1) giao cho người uỷ quyền người gửi đã khai sẵn → (2) liên hệ người gửi xin uỷ quyền người khác → (3) gửi quầy lễ tân/chốt bảo vệ → (4) cầm hàng về."

> `AC-16.1.01`: "Hiện modal hai hướng: (1) Liên hệ người gửi, (2) Xử lý đơn hàng."

> `AC-17.1.01`: "…màn "Xử lý đơn hàng" với 3 lựa chọn theo thứ tự ưu tiên: gửi chốt bảo vệ · gửi quầy lễ tân · cầm hàng về."

↳ **Ghi chú:** 3 chỗ trong PRD mô tả **3 cấu trúc khác nhau**: `BR08-02` là **1 danh sách 4 bước** (lễ tân **trước** bảo vệ); `AC-16.1.01` là **modal 2 hướng**; `AC-17.1.01` + `§8.8.2` đặt **chốt bảo vệ trước** quầy lễ tân. Và bước (1) *"giao cho người uỷ quyền đã khai sẵn"* **không xuất hiện** ở modal lẫn màn Xử lý đơn hàng. `SC-DLV-043` đang assert theo `BR08-02` ⇒ rất có thể FAIL oan. Demo 2026-09-15 (`DLV_04`/`DLV_05`) cho thấy dạng modal 2 hướng. **Hỏi:** (a) cấu trúc chuẩn là modal 2 hướng + màn 3 lựa chọn? (b) thứ tự đúng: bảo vệ → lễ tân, hay lễ tân → bảo vệ? (c) người uỷ quyền đã khai sẵn chọn ở đâu — chính là lựa chọn "Người được uỷ quyền" (có prefill) ở màn Xác nhận giao hàng?

↳ **BA trả lời 2026-09-16 ("Vào link demo, thao tác vào các btn... đặt lại câu hỏi sau") + vibe-check demo 2026-09-17 (Playwright MCP), đối chiếu ảnh `DLV_04/05` đã có từ 2026-09-15:** đã thao tác đủ 4 tầng màn hình. Cấu trúc quan sát được: (1) màn "Xác nhận đã giao" → nút "Không thể liên lạc cho người nhận?" → (2) MÀN (không phải modal) "Liên hệ người gửi" — hiện SĐT người gửi + nút Gọi + field "Giao cho *: Người được uỷ quyền / Quầy lễ tân / Quầy bảo vệ" NGAY TẠI ĐÂY + nút "Không thể liên lạc với người gửi và người nhận?" → (3) MODAL 2 hướng "Chưa liên lạc được?" ("Tôi sẽ chờ & gọi lại" / "Xử lý đơn hàng") → (4) màn "Xử lý đơn hàng" với 3 phương án ĐÚNG THỨ TỰ: "Gửi tại chốt bảo vệ" (trước) → "Gửi tại quầy lễ tân" (sau) → "Cầm hàng về". **Bổ sung quan sát (ảnh `DLV_04`, chưa ghi ở lượt trước):** khi chọn "Quầy lễ tân"/"Quầy bảo vệ" ở tầng (2), UI hiện thêm khối "NGƯỜI NHẬN TẠI QUẦY" với 2 ô "Họ tên người trực quầy" + "Số điện thoại" — chưa rõ bắt buộc hay tuỳ chọn, PRD không nhắc tới. (a) Cấu trúc thật là chuỗi **4 tầng** (màn→màn→modal→màn), KHÔNG phải chỉ "modal 2 hướng" đơn thuần như `AC-16.1.01`. (b) Thứ tự bảo vệ-trước-lễ-tân khớp `AC-17.1.01`/`§8.8.2`, NGƯỢC `BR08-02` — đề nghị BA xác nhận `BR08-02` lỗi thời để sửa PRD. (c) Bước "giao cho người uỷ quyền đã khai sẵn" = đúng field "Giao cho" ở tầng (2), gộp chung với 2 lựa chọn quầy, không tách riêng bước như `BR08-02`. **Còn treo:** đề nghị BA XÁC NHẬN cấu trúc 4 tầng trên là chuẩn (không phải giới hạn riêng của demo) để dùng làm oracle chính thức cho `SC-DLV-043`; câu hỏi mới (d): 2 ô "Họ tên người trực quầy"/"SĐT" có bắt buộc không, có dùng để gọi xác nhận lại không?

↳ **BA trả lời 2026-09-17 (vòng 3) + tái vibe-check demo (Playwright MCP):** BA: "trên UI có dấu * bắt buộc mà" + "Chỉ lưu ghi chú nhé, chỉ người nhận mới được xác nhận". Đã thao tác thật: chọn "Quầy lễ tân" trực tiếp ở màn "Xác nhận đã giao" → khối "NGƯỜI NHẬN TẠI QUẦY \*" hiện 2 ô "Họ tên người trực quầy" + "Số điện thoại". Bấm "Xác nhận đã giao hàng" khi để TRỐNG cả 2 ô (và chưa đính ảnh) → **form KHÔNG submit được**, vẫn ở nguyên màn — xác nhận dấu `*` là ràng buộc THẬT (không chỉ trang trí UI), khớp câu trả lời BA. Vế "chỉ lưu ghi chú, chỉ người nhận mới được xác nhận" — BA xác nhận 2 ô này chỉ có vai trò **ghi chú tham khảo cho Carrier** (không phải trigger gọi xác nhận tự động), và bước "xác nhận đã nhận hàng" tại quầy vẫn phải do **chính Người nhận** thực hiện (không phải Carrier tự xác nhận thay). **`C-DLV-06` ĐÓNG HẲN 2026-09-17** — `SC-DLV-043` dùng cấu trúc 4 tầng làm oracle chính thức; thêm rule 2 ô bắt buộc cho `SC-DLV-039`/`SC-DLV-045`.

### C-DLV-07 · "Nhắc" và "chuyển admin hỗ trợ" — hệ quả quan sát được *(RESOLVED 2026-09-17 — đóng ở vòng 2)*

📍 `DOC-v1.1-01 §6.2 AC-23.2.01 · trang 25` · `§8.8.1 BR08-06 · trang 41` · `§8.9.1 BR09-04 · trang 42` · `§8.13.1 (15 dòng, không có dòng nhắc) · trang 47` · BA trả lời `C-CNL-03` 2026-09-16

> `AC-23.2.01`: "Sau 2 giờ: hệ thống nhắc người nhận. Sau 2 giờ tiếp: chuyển đơn sang diện admin hỗ trợ. Đơn không tự chuyển COMPLETED."

> `BR08-06`: "Thời hạn giữ hàng tại quầy: nhắc người nhận sau 4 giờ và cuối ngày; sau 24 giờ chưa xác nhận thì chuyển admin hỗ trợ."

> `BR09-04`: "…quá lịch hẹn 24 giờ mà đơn chưa đóng thì chuyển admin hỗ trợ."

↳ **Ghi chú:** PRD có **3 bộ mốc nhắc** nhưng danh mục thông báo chính thức (15 loại) **không có loại "nhắc"** nào. Và BA vừa trả lời `C-CNL-03`: *"không có màn hình hay tool, dev hỗ trợ tay"*. **Hỏi:** (a) "nhắc" là **push/in-app** không? Nội dung câu nhắc? Có phải loại thông báo thứ 16 chưa có trong danh mục? (b) "cuối ngày" là **mấy giờ**? (c) "chuyển admin hỗ trợ" có làm **đơn đổi trạng thái / nhãn / cờ** gì mà người dùng nhìn thấy không, hay chỉ là log nội bộ? (d) Các mốc 2h/4h/24h **đã được build** chưa — nếu chưa thì `SC-DLV-024/048/054` để **out of scope** thay vì chờ thời gian thực.

↳ **BA trả lời 2026-09-16 ("Vào link demo... đặt lại câu hỏi sau") + vibe-check demo 2026-09-17 (Playwright MCP):** đã rà toàn bộ các màn thao tác được (Chờ ghép/Đã ghép/Lấy hàng/Đang giao/Xác nhận đã giao/Liên hệ người gửi/Xử lý đơn hàng/Cầm hàng về) — **KHÔNG** thấy bất kỳ UI, banner, hay copy nào liên quan "nhắc" (reminder) hay "chuyển admin hỗ trợ". Đây là rule time-based (2h/4h/24h) nên bản demo tĩnh (không có đồng hồ thật chạy nền) không thể mô phỏng được. **Giữ nguyên toàn bộ câu hỏi gốc** — cần BA/Dev trả lời trực tiếp bằng lời, demo không giúp được cho CL này. *(→ đã được BA trả lời ở **vòng 2** ngay dưới, 2026-09-17.)*

↳ **BA trả lời 2026-09-17 (vòng 2 — QC GiangDC2 chuyển lời BA):**

> "không chỉ gởi remind thôi nhé"

↳ **KẾT LUẬN (theo BA) 2026-09-17 — `C-DLV-07` ĐÓNG HẲN:** câu đọc đúng là ***"Không, chỉ gửi remind thôi nhé"*** (QC GiangDC2 xác nhận nghĩa 2026-09-17), khớp câu trả lời `C-DLV-08` cùng lượt (*"phase này các chỗ liên quan đến role admin chưa làm"*) và khớp `C-CNL-03` (không có màn/tool admin). ⇒ **(c)** Tại mọi mốc (2h/4h · 4h/cuối ngày/24h · 24h quá hẹn) hệ thống **CHỈ gửi thông báo nhắc** — đơn **KHÔNG** đổi trạng thái, **KHÔNG** gắn nhãn/cờ nào người dùng nhìn thấy; vế *"chuyển đơn sang diện admin hỗ trợ"* (`AC-23.2.01`, `BR08-06`, `BR09-04`) **chưa build ở phase này ⇒ OUT OF SCOPE v1.1**, không viết assert. **(d)** `SC-DLV-024/048/054` **không còn chờ bề mặt admin** — chỉ còn tiền đề thời gian thực cho phần nhắc; phần assert được ngay: **đơn KHÔNG tự chuyển "Hoàn thành"** sau các mốc (`AC-23.2.01` câu cuối). ⚠️ **Giới hạn đã biết, CHẤP NHẬN — không mở CL mới:** BA không nói rõ **(a)** kênh nhắc (push hay in-app) + nguyên văn câu nhắc — danh mục 15 loại thông báo `§8.13.1` vẫn **không có loại "nhắc"**; và **(b)** *"cuối ngày"* là **mấy giờ**. ⇒ TC assert **có thông báo nhắc gửi tới người nhận** sau mốc, **GHI NHẬN** kênh + nguyên văn + giờ thực tế lúc chạy; **không** assert giờ cụ thể của "cuối ngày", **không** FAIL vì kênh hiển thị.

### C-DLV-08 · Giao quầy trực tiếp ⟷ giao quầy qua luồng "Không liên lạc được" *(PARTIALLY RESOLVED 2026-09-17 — chờ BA vòng 2)*

📍 `DOC-v1.1-01 §8.7.1 BR07-01 / BR07-05 · trang 39` · `§8.7 Post-Conditions · trang 39` ⟷ `§8.8 Post-Conditions · trang 41` · `§8.13.1 NTF-05 / NTF-11 · trang 47`

> `BR07-01`: "Bắt buộc chọn 1 trong 4 đối tượng nhận: Người nhận · Người được uỷ quyền · Quầy lễ tân · Quầy bảo vệ."

> `BR07-05`: "Trường "Uỷ quyền bởi" tự sinh: "Người nhận" khi đến từ màn Xác nhận giao hàng, "Người gửi" khi đến từ màn Liên hệ người gửi. Chỉ đọc."

> `§8.8` Post-Conditions: "Đơn được gắn cờ không liên lạc được người nhận và đi tiếp theo nhánh đã chọn…"

↳ **Ghi chú:** Có **2 đường** để gửi hàng ở quầy: chọn "Quầy lễ tân/Quầy bảo vệ" **ngay ở màn Xác nhận giao hàng** (`SC-DLV-039`), hoặc qua **"Không liên lạc được → Xử lý đơn hàng"** (`SC-DLV-045`). PRD chỉ nói đường thứ hai gắn **cờ không liên lạc được** + `NTF-11`. **Hỏi:** đường thứ nhất (a) **có gắn cờ** không? (b) gửi **`NTF-05`** hay **`NTF-11`**? (c) dòng *"Uỷ quyền bởi: Người nhận"* có hiện không (vô nghĩa với quầy)? (d) có áp **thời hạn giữ hàng tại quầy 4h/24h** (`BR08-06`) không?

↳ **BA trả lời 2026-09-16 ("Vào link demo... đặt lại câu hỏi sau") + vibe-check demo 2026-09-17 (Playwright MCP), đối chiếu ảnh `DLV_03` đã có từ 2026-09-15:** xác nhận có ĐƯỜNG THỨ 2 độc lập — ngay tại màn "Xác nhận đã giao" (KHÔNG cần bấm "Không thể liên lạc cho người nhận?"), field "Giao cho *" đã có sẵn 4 lựa chọn: Người nhận / Người được uỷ quyền / Quầy lễ tân / Quầy bảo vệ — chọn thẳng "Quầy lễ tân"/"Quầy bảo vệ" tại đây. Ảnh `DLV_03` cho thấy khi chọn quầy ở đường này CŨNG hiện khối "NGƯỜI NHẬN TẠI QUẦY" (Họ tên người trực quầy + SĐT) **giống hệt** đường thứ 2 (`DLV_04`) — vậy 2 đường đòi cùng bộ field bổ sung ở bước chọn quầy, không có gì phân biệt hình thức ngoài việc có/không có cảnh báo "Không thể liên lạc cho người nhận?" phía trên. `BR07-05` (đã có trong PRD) cho biết trường "Uỷ quyền bởi" tự sinh theo MÀN VÀO (không theo loại đối tượng nhận) ⇒ câu (c) gần như đã có câu trả lời từ chính PRD: chọn quầy ở đường thứ 1 (từ "Xác nhận đã giao") thì "Uỷ quyền bởi" vẫn hiện "Người nhận" dù chọn quầy — nhưng đây là suy luận từ text PRD, QA CHƯA tự tay xác nhận bằng cách submit thật (bị chặn bởi ô "Ảnh bằng chứng" không mở được file picker trong demo). **Còn treo (a)(b)(d):** không quan sát được flag/NTF/hạn giữ hàng qua demo tĩnh (không có notification log, không hiển thị flag ẩn) — cần BA/Dev trả lời trực tiếp.

↳ **BA trả lời 2026-09-17 (vòng 3):** "sẽ lưu thông tin tại Block lịch sử nhé (có thể mở link demo để xem lại)" — gợi ý câu trả lời cho (a)/(b) **nằm sẵn trong log** của block LỊCH SỬ trên màn Theo dõi đơn (dòng ghi khi chọn quầy), không phải BA tự mô tả bằng lời. ⚠️ **Chưa xử lý xong** — cần vibe-check lại: mở block LỊCH SỬ sau khi chọn "Quầy lễ tân"/"Quầy bảo vệ" trực tiếp ở màn "Xác nhận đã giao", đọc đúng câu log để xác định có cờ "không liên lạc được" hay dòng nào tương đương NTF-05/NTF-11 không. Câu (d) thời hạn giữ hàng 4h/24h vẫn chưa có câu trả lời — demo tĩnh không mô phỏng được rule time-based, cần hỏi thêm. *(→ (d) đã được BA trả lời ở **vòng 4** ngay dưới, 2026-09-17.)*

↳ **BA trả lời 2026-09-17 (vòng 4 — QC GiangDC2 chuyển lời BA):**

> "phase này các chỗ liên quan đến role admin chưa làm nhé"

↳ **KẾT LUẬN (theo BA) 2026-09-17 — đóng câu (d), `C-DLV-08` vẫn 🟡 Partially:** **(d)** thời hạn giữ hàng tại quầy **4h/24h → chuyển admin** (`BR08-06`) **OUT OF SCOPE v1.1** — mọi bề mặt liên quan **role admin chưa build ở phase này**; khớp `C-DLV-07` cùng lượt (chỉ gửi remind) và `C-CNL-03` (dev xử lý tay ngoài app). ⇒ `SC-DLV-039`/`SC-DLV-045` **không assert** hạn giữ hàng / chuyển admin; `SC-DLV-048` chỉ assert 2 mốc **nhắc**. **CÒN TREO (a)(b)** — đường chọn quầy **trực tiếp** có gắn **cờ "không liên lạc được"** không và bắn **`NTF-05`** hay **`NTF-11`**: BA đã chỉ chỗ tự đọc ở vòng 3 (*"sẽ lưu thông tin tại Block lịch sử"*) ⇒ **KHÔNG hỏi BA nữa**, xử bằng **vibe-check demo**: chọn "Quầy lễ tân"/"Quầy bảo vệ" trực tiếp ở màn "Xác nhận đã giao" → mở block **LỊCH SỬ** trên màn Theo dõi đơn → đọc đúng câu log. Tới lúc đó `SC-DLV-039` ⟷ `SC-DLV-045` mới phân biệt được kết quả mong đợi; hiện **ghi nhận**, không assert cờ/NTF.

## Khuyến nghị tổng thể
1. ✅ **`RISK-DLV-08` nay Confirmed qua demo, KHÔNG còn là blocker** — vibe-check 2026-09-15 xác nhận cấu trúc UI, vibe-check 2026-09-16 xác nhận thêm luồng submit end-to-end chạy đúng (đính ảnh, chọn đối tượng nhận, chuyển trạng thái DELIVERED → COMPLETED). Vẫn khuyến nghị 1 lượt double-check nhanh trên STG thật trước khi hardening automation locator, nhưng không chặn `generate-tc`.
1b. ✅ **`C-DLV-02` Resolved 2026-09-16 (BA)** — *"Không có chức năng này"* ⇒ `GPS-01` out of scope, khớp quan sát demo (màn "Đang giao" không có control vị trí). Không cần PM xác nhận thêm.
2. **`RISK-DLV-11` (mới)** — popup "Tôi đã lấy hàng" trên demo thiếu field ảnh mà PRD đã resolve (`BR06-01`); verify cùng lượt STG ở mục #1.
3. **`SC-DLV-062` (log append-only) là SC quan trọng nhất về nghiệp vụ** — đối chiếu trực tiếp với bug đã biết ở `TS`; nếu chưa fix, dự kiến FAIL có chủ đích (giống pattern `SC-TS-003`/`RISK-TS-01`).
4. **Gộp lịch chạy các SC cần tiền đề thời gian dài:** `SC-DLV-024` (2h/4h, v1.0) + `SC-DLV-048` (4h/24h) + `SC-DLV-054` (24h) + `SC-TS-006` (v1.0) — cùng 1 kế hoạch seed timestamp hoặc chờ thời gian thực, tránh chạy rời rạc nhiều lần. **Cập nhật 2026-09-17 (`C-DLV-07`/`C-DLV-08` BA):** phạm vi assert của nhóm này **thu hẹp** — chỉ còn *"có gửi thông báo nhắc"* + *"đơn KHÔNG tự đóng"*; vế **chuyển admin hỗ trợ** và **hạn giữ hàng tại quầy** là **out of scope v1.1** (role admin chưa build), không assert, không log bug khi không thấy.
5. **`GPS-01`/`COST-01` tiếp tục ngoài scope** — không viết SC, không cần hỏi lại PM trừ khi có tài liệu mới.
6. **⚠️ Chưa chụp được màn trạng thái `RESCHEDULED`/`RETURNING`/nhóm đóng** (`SC-DLV-031/032/033`) — luồng "Xử lý đơn hàng" bị chặn ở đúng ô ảnh bằng chứng nói trên nên không đi hết tới trạng thái cuối trên demo; đã có bằng chứng cấu trúc FORM (`00_input/v1.1/design/DLV_05/06`), còn thiếu bằng chứng MÀN HÌNH KẾT QUẢ — bổ sung khi có STG thật.
7. ✅ **`DLV` hết CL Open (2026-09-17)** — `C-DLV-07` đóng ở vòng 2 (chỉ gửi remind), `C-DLV-08` chỉ còn (a)(b) và **tự xác minh bằng vibe-check block LỊCH SỬ**, không phải chờ BA. `generate-tc` chạy được toàn bộ 64 SC nếu `SC-DLV-039/045` tạm **ghi nhận** cờ/`NTF` thay vì assert.
