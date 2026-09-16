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
  cl_open: 4
  cl_resolved: 4
status: ANALYZED
updated: 2026-09-16
---

# Risk Assessment — v1.1 · Module DLV (DELTA)

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (7 dòng, `RISK-DLV-01..07`) xem `v1.0/DLV-giao-nhan/risk_assessment.md` — KHÔNG lặp lại ở đây. **ID mới bắt đầu từ `RISK-DLV-08`** (v1.0 đã dùng hết tới `-07`).

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
| C-DLV-05 | Hẹn giao lại (RESCHEDULED): tự về IN_TRANSIT hay Carrier bấm; RESCHEDULED → RETURNING ai/đâu; giới hạn số lần hẹn; timeline 5 mốc hiển thị các trạng thái mới | 🔴 **Open (mới 2026-09-16)** | 2026-09-16 | REQ-DLV-019, REQ-DLV-002, SC-DLV-016, SC-DLV-031, SC-DLV-050 |
| C-DLV-06 | Màn "Không liên lạc được người nhận": modal 2 hướng hay danh sách 4 nhánh; thứ tự chốt bảo vệ ⟷ quầy lễ tân; lựa chọn "người uỷ quyền đã khai sẵn" nằm ở đâu | 🔴 **Open (mới 2026-09-16)** | 2026-09-16 | REQ-DLV-018, SC-DLV-043 |
| C-DLV-07 | "Nhắc" + "chuyển admin hỗ trợ" (2h/4h · 4h/cuối ngày/24h · 24h quá hẹn): thông báo nào, "cuối ngày" mấy giờ, đơn có đổi trạng thái/nhãn không khi không có công cụ admin | 🔴 **Open (mới 2026-09-16)** | 2026-09-16 | REQ-DLV-018, REQ-DLV-019, SC-DLV-024, SC-DLV-048, SC-DLV-054 |
| C-DLV-08 | Chọn "Quầy lễ tân/Quầy bảo vệ" **trực tiếp** ở màn Xác nhận giao hàng khác gì đi qua luồng "Không liên lạc được" (cờ, thông báo, "Uỷ quyền bởi") | 🔴 **Open (mới 2026-09-16)** | 2026-09-16 | REQ-DLV-017, REQ-DLV-018, SC-DLV-039, SC-DLV-045 |

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

### C-DLV-05 · Hẹn giao lại — cơ chế chuyển trạng thái *(OPEN — mới 2026-09-16)*

📍 `DOC-v1.1-01 §6.2 AC-18.1.01 · trang 23` · `§8.9.1 BR09-05 · trang 42` · `§8.12.2 dòng RESCHEDULED · trang 45` · `§8.12.3 dòng RESCHEDULED · trang 46` · `§5.1 "Timeline theo dõi 5 mốc" · trang 10`

> `AC-18.1.01`: "…Đơn sang RESCHEDULED (không tính là huỷ đơn), lưu lịch hẹn vào đơn. Người gửi và người nhận nhận NTF-13. Theo lịch hẹn, đơn quay lại IN_TRANSIT để người vận chuyển giao lại."

> `§8.12.2`: "RESCHEDULED | Hẹn giao lại | … | → IN_TRANSIT (theo lịch hẹn) · RETURNING · INCIDENT"

> `§8.12.3`: "RESCHEDULED | Xem lịch hẹn giao lại | Giao lại theo lịch (mở lại màn giao hàng) | Xem lịch hẹn"

> `§5.1`: "Timeline theo dõi 5 mốc: Chờ ghép · Lấy hàng · Đang giao · Đã giao · Hoàn thành"

↳ **Ghi chú:** (a) *"Theo lịch hẹn, đơn quay lại IN_TRANSIT"* — **hệ thống tự chuyển** đúng giờ hẹn, hay **Carrier bấm "Giao lại"** (§8.12.3)? Carrier có giao **sớm hơn** lịch hẹn được không? (`SC-DLV-050` đang giả định Carrier bấm.) (b) Chuyển tiếp **RESCHEDULED → RETURNING** có trong từ điển nhưng **không AC nào** mô tả: ai bấm, từ màn nào, có nhập lịch hẹn mới? (c) Hẹn giao lại **được mấy lần** — không giới hạn? (d) Timeline chỉ có **5 mốc** trong khi đơn có thể đi qua RESCHEDULED / RETURNING / RETURNED / INCIDENT — các trạng thái này hiện **ở mốc nào / nhãn gì** trên thanh tiến trình (`SC-DLV-016`)?

### C-DLV-06 · Cấu trúc màn "Không liên lạc được người nhận" *(OPEN — mới 2026-09-16)*

📍 `DOC-v1.1-01 §8.8.1 BR08-02 · trang 41` ⟷ `§6.2 AC-16.1.01 · trang 22` · `§6.2 AC-17.1.01 · trang 22` · `§8.8.2 dòng "Phương án xử lý" · trang 42`

> `BR08-02`: "Thứ tự ưu tiên xử lý (màn hình sắp xếp đúng thứ tự này): (1) giao cho người uỷ quyền người gửi đã khai sẵn → (2) liên hệ người gửi xin uỷ quyền người khác → (3) gửi quầy lễ tân/chốt bảo vệ → (4) cầm hàng về."

> `AC-16.1.01`: "Hiện modal hai hướng: (1) Liên hệ người gửi, (2) Xử lý đơn hàng."

> `AC-17.1.01`: "…màn "Xử lý đơn hàng" với 3 lựa chọn theo thứ tự ưu tiên: gửi chốt bảo vệ · gửi quầy lễ tân · cầm hàng về."

↳ **Ghi chú:** 3 chỗ trong PRD mô tả **3 cấu trúc khác nhau**: `BR08-02` là **1 danh sách 4 bước** (lễ tân **trước** bảo vệ); `AC-16.1.01` là **modal 2 hướng**; `AC-17.1.01` + `§8.8.2` đặt **chốt bảo vệ trước** quầy lễ tân. Và bước (1) *"giao cho người uỷ quyền đã khai sẵn"* **không xuất hiện** ở modal lẫn màn Xử lý đơn hàng. `SC-DLV-043` đang assert theo `BR08-02` ⇒ rất có thể FAIL oan. Demo 2026-09-15 (`DLV_04`/`DLV_05`) cho thấy dạng modal 2 hướng. **Hỏi:** (a) cấu trúc chuẩn là modal 2 hướng + màn 3 lựa chọn? (b) thứ tự đúng: bảo vệ → lễ tân, hay lễ tân → bảo vệ? (c) người uỷ quyền đã khai sẵn chọn ở đâu — chính là lựa chọn "Người được uỷ quyền" (có prefill) ở màn Xác nhận giao hàng?

### C-DLV-07 · "Nhắc" và "chuyển admin hỗ trợ" — hệ quả quan sát được *(OPEN — mới 2026-09-16)*

📍 `DOC-v1.1-01 §6.2 AC-23.2.01 · trang 25` · `§8.8.1 BR08-06 · trang 41` · `§8.9.1 BR09-04 · trang 42` · `§8.13.1 (15 dòng, không có dòng nhắc) · trang 47` · BA trả lời `C-CNL-03` 2026-09-16

> `AC-23.2.01`: "Sau 2 giờ: hệ thống nhắc người nhận. Sau 2 giờ tiếp: chuyển đơn sang diện admin hỗ trợ. Đơn không tự chuyển COMPLETED."

> `BR08-06`: "Thời hạn giữ hàng tại quầy: nhắc người nhận sau 4 giờ và cuối ngày; sau 24 giờ chưa xác nhận thì chuyển admin hỗ trợ."

> `BR09-04`: "…quá lịch hẹn 24 giờ mà đơn chưa đóng thì chuyển admin hỗ trợ."

↳ **Ghi chú:** PRD có **3 bộ mốc nhắc** nhưng danh mục thông báo chính thức (15 loại) **không có loại "nhắc"** nào. Và BA vừa trả lời `C-CNL-03`: *"không có màn hình hay tool, dev hỗ trợ tay"*. **Hỏi:** (a) "nhắc" là **push/in-app** không? Nội dung câu nhắc? Có phải loại thông báo thứ 16 chưa có trong danh mục? (b) "cuối ngày" là **mấy giờ**? (c) "chuyển admin hỗ trợ" có làm **đơn đổi trạng thái / nhãn / cờ** gì mà người dùng nhìn thấy không, hay chỉ là log nội bộ? (d) Các mốc 2h/4h/24h **đã được build** chưa — nếu chưa thì `SC-DLV-024/048/054` để **out of scope** thay vì chờ thời gian thực.

### C-DLV-08 · Giao quầy trực tiếp ⟷ giao quầy qua luồng "Không liên lạc được" *(OPEN — mới 2026-09-16)*

📍 `DOC-v1.1-01 §8.7.1 BR07-01 / BR07-05 · trang 39` · `§8.7 Post-Conditions · trang 39` ⟷ `§8.8 Post-Conditions · trang 41` · `§8.13.1 NTF-05 / NTF-11 · trang 47`

> `BR07-01`: "Bắt buộc chọn 1 trong 4 đối tượng nhận: Người nhận · Người được uỷ quyền · Quầy lễ tân · Quầy bảo vệ."

> `BR07-05`: "Trường "Uỷ quyền bởi" tự sinh: "Người nhận" khi đến từ màn Xác nhận giao hàng, "Người gửi" khi đến từ màn Liên hệ người gửi. Chỉ đọc."

> `§8.8` Post-Conditions: "Đơn được gắn cờ không liên lạc được người nhận và đi tiếp theo nhánh đã chọn…"

↳ **Ghi chú:** Có **2 đường** để gửi hàng ở quầy: chọn "Quầy lễ tân/Quầy bảo vệ" **ngay ở màn Xác nhận giao hàng** (`SC-DLV-039`), hoặc qua **"Không liên lạc được → Xử lý đơn hàng"** (`SC-DLV-045`). PRD chỉ nói đường thứ hai gắn **cờ không liên lạc được** + `NTF-11`. **Hỏi:** đường thứ nhất (a) **có gắn cờ** không? (b) gửi **`NTF-05`** hay **`NTF-11`**? (c) dòng *"Uỷ quyền bởi: Người nhận"* có hiện không (vô nghĩa với quầy)? (d) có áp **thời hạn giữ hàng tại quầy 4h/24h** (`BR08-06`) không?

## Khuyến nghị tổng thể
1. ✅ **`RISK-DLV-08` nay Confirmed qua demo, KHÔNG còn là blocker** — vibe-check 2026-09-15 xác nhận cấu trúc UI, vibe-check 2026-09-16 xác nhận thêm luồng submit end-to-end chạy đúng (đính ảnh, chọn đối tượng nhận, chuyển trạng thái DELIVERED → COMPLETED). Vẫn khuyến nghị 1 lượt double-check nhanh trên STG thật trước khi hardening automation locator, nhưng không chặn `generate-tc`.
1b. ✅ **`C-DLV-02` Resolved 2026-09-16 (BA)** — *"Không có chức năng này"* ⇒ `GPS-01` out of scope, khớp quan sát demo (màn "Đang giao" không có control vị trí). Không cần PM xác nhận thêm.
2. **`RISK-DLV-11` (mới)** — popup "Tôi đã lấy hàng" trên demo thiếu field ảnh mà PRD đã resolve (`BR06-01`); verify cùng lượt STG ở mục #1.
3. **`SC-DLV-062` (log append-only) là SC quan trọng nhất về nghiệp vụ** — đối chiếu trực tiếp với bug đã biết ở `TS`; nếu chưa fix, dự kiến FAIL có chủ đích (giống pattern `SC-TS-003`/`RISK-TS-01`).
4. **Gộp lịch chạy các SC cần tiền đề thời gian dài:** `SC-DLV-024` (2h/4h, v1.0) + `SC-DLV-048` (4h/24h) + `SC-DLV-054` (24h) + `SC-TS-006` (v1.0) — cùng 1 kế hoạch seed timestamp hoặc chờ thời gian thực, tránh chạy rời rạc nhiều lần.
5. **`GPS-01`/`COST-01` tiếp tục ngoài scope** — không viết SC, không cần hỏi lại PM trừ khi có tài liệu mới.
6. **⚠️ Chưa chụp được màn trạng thái `RESCHEDULED`/`RETURNING`/nhóm đóng** (`SC-DLV-031/032/033`) — luồng "Xử lý đơn hàng" bị chặn ở đúng ô ảnh bằng chứng nói trên nên không đi hết tới trạng thái cuối trên demo; đã có bằng chứng cấu trúc FORM (`00_input/v1.1/design/DLV_05/06`), còn thiếu bằng chứng MÀN HÌNH KẾT QUẢ — bổ sung khi có STG thật.
