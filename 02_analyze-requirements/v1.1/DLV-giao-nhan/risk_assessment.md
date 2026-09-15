---
id: v1.1/DLV-giao-nhan/risk
title: Risk Assessment — v1.1 · Module DLV
type: risk-assessment
version: v1.1
sprint: 1
module: DLV
counts:
  cl: 4
  risk: 11
  cl_open: 1
  cl_resolved: 3
status: ANALYZED
updated: 2026-09-15
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
| RISK-DLV-05 | DLV / Nhánh phụ scope | *(cập nhật Status)* 3 REQ không SC của v1.0 — `PUP-03` (ảnh lúc lấy hàng) đã **Resolved** qua `BR06-01`; `GPS-01` (chia sẻ vị trí) và `COST-01` (chi phí) **KHÔNG được PRD v1.1 nhắc tới** (đã rà toàn văn §1-§9, không có mục nào về GPS/vị trí/chi phí ghi nhận) — vẫn Pending | Medium → **1/3 Resolved, 2/3 vẫn Pending** | `DOC-v1.1-01` §8.6.1 BR06-01 (resolve PUP-03) — rà toàn văn không thấy GPS-01/COST-01 | `SC-DLV-035/036` (đã có) cho PUP-03; `GPS-01`/`COST-01` tiếp tục gap có chủ đích | Không viết SC cho `GPS-01`/`COST-01` — vẫn ngoài scope tới khi PM chốt | Pending (2/3) | REQ-DLV-012 (Resolved), REQ-DLV-013, REQ-DLV-014 (không đổi) |
| RISK-DLV-08 | DLV / Xác nhận giao hàng | *(cập nhật Status)* `REQ-DLV-017` (`FR07`) mở rộng lớn từ 1 nút+popup sang form đầy đủ 4 loại đối tượng nhận — nguy cơ app STG **chưa build lại** theo PRD mới ⇒ 6 SC mới (`SC-DLV-037..042`) FAIL hàng loạt vì lý do "app chưa cập nhật", không phải bug thật | High → **Partially confirmed** | `DOC-v1.1-01` §8.7 vs demo `foxeco_demo/FoxEcoQC` (2026-09-15) | Vibe-test 1 lượt màn "Xác nhận giao hàng" trước `generate-tc`, đối chiếu đúng 4 loại đối tượng nhận có tồn tại chưa | **Cấu trúc UI đã khớp** — ảnh `00_input/v1.1/design/DLV_01..03` xác nhận form có đủ 4 lựa chọn "Giao cho" (Người nhận/Uỷ quyền/Quầy lễ tân/Quầy bảo vệ), field động theo lựa chọn đúng `BR07-03..05`. **CHƯA verify được luồng submit end-to-end** — ô "Ảnh bằng chứng" trong demo là dropzone không thao tác được (click không mở file picker, không tăng đếm 0/5) nên không xác nhận được nút "Xác nhận đã giao hàng" có thực sự chuyển trạng thái DELIVERED hay không; đây là giới hạn công cụ demo, không phải bug PRD | Partially confirmed (cấu trúc UI OK, luồng submit chưa verify — vẫn cần 1 lượt trên STG thật có upload ảnh thật trước `generate-tc`) | REQ-DLV-017, SC-DLV-037..042 |
| RISK-DLV-09 | DLV / Audit log | **(risk mới)** `NFR-07` (log append-only, không API sửa/xoá) chính thức hoá yêu cầu mà bug đã biết (`RISK-TS-01`, huỷ nhận đơn xoá dòng "Ghép thành công") đang **vi phạm trực tiếp** — SC mới `SC-DLV-062` dự kiến FAIL cho tới khi bug được fix | High | `DOC-v1.1-01` §9 NFR-07 vs `v1.0/TS-trust-safety/risk_assessment.md RISK-TS-01` | `SC-DLV-062` (P1) | Cross-ref bug đã log (nếu có) ở `05_bug-reports/`; nếu chưa log → ưu tiên log-bug trước execute | Open — dự kiến FAIL có chủ đích cho tới khi fix | REQ-DLV-022, SC-DLV-062 |
| RISK-DLV-10 | DLV / Tiền đề thời gian mới | **(risk mới)** `SC-DLV-048` (4h/24h giữ hàng tại quầy) và `SC-DLV-054` (24h quá hẹn cầm hàng về) cùng nhóm khó như `RISK-DLV-04` cũ (`SC-DLV-024`) — cần thời gian thực hoặc seed timestamp, dễ bị "đánh PASS cho xong" | Medium | `DOC-v1.1-01` §8.8.1 BR08-06 · §8.9.1 BR09-04 | `SC-DLV-048`, `SC-DLV-054` | Gộp kế hoạch chạy chung với `SC-DLV-024`/`SC-TS-006` (cùng nhóm tiền đề thời gian dài) | Open | REQ-DLV-018, REQ-DLV-019, SC-DLV-048, SC-DLV-054 |
| RISK-DLV-11 | DLV / Ảnh lúc lấy hàng | **(risk mới, phát hiện qua vibe-check demo 2026-09-15)** `C-DLV-04` đã Resolved theo PRD (`BR06-01` — ảnh lúc lấy hàng tồn tại, tuỳ chọn, trần 5) nhưng **demo hiện tại KHÔNG có field đính ảnh** ở popup "Tôi đã lấy hàng" — chỉ có 2 nút Huỷ/Xác nhận đơn giản, giống hệt bản v1.0 chưa cập nhật | Medium | So khớp `DOC-v1.1-01 §8.6.1 BR06-01` vs ảnh `00_input/v1.1/design/DLV_07_toidalayhang_popup_khongco_anhluclayhang.png` | `SC-DLV-035` (có ảnh), `SC-DLV-036` (không ảnh) | Cùng pattern `RISK-DLV-08` — verify lại trên STG thật trước `generate-tc`; nếu STG cũng thiếu field này thì đây là **defect** (PRD/app lệch), không phải TC sai | Open (cần vibe-test STG xác nhận) | REQ-DLV-012, SC-DLV-035, SC-DLV-036 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-DLV-04 | Ảnh lúc lấy hàng (`PUP-03`) có tồn tại ở app không, tuỳ chọn hay bắt buộc? | ✅ **Resolved 2026-09-15** | mở cùng lượt (chỉ để ghi nhận resolve) | REQ-DLV-012, SC-DLV-035, SC-DLV-036 |

### C-DLV-04 · Ảnh lúc lấy hàng — tuỳ chọn hay bắt buộc? *(RESOLVED)*

📍 `DOC-v1.1-01 §8.6.1 BR06-01 · trang 38`

> "BR06-01 | Ảnh lúc lấy hàng là tuỳ chọn nhưng được khuyến nghị mạnh; tối đa 5 ảnh."

↳ **Ghi chú:** PRD chính thức resolve gap có chủ đích của v1.0 (`RISK-DLV-05` — PM chưa trả lời `KP-05 §1` câu #2). Kết luận: **tồn tại**, **tuỳ chọn**, trần **5 ảnh**. Không blocking, chỉ ghi nhận.

> ⚠️ `C-DLV-01` (Receiver-only, Resolved v1.0) và `C-DLV-02` (GPS-01 mặc định bật/tắt, Open) **không đổi** ở lượt này — xem `v1.0/DLV-giao-nhan/risk_assessment.md`.

## Khuyến nghị tổng thể
1. **`RISK-DLV-08` hạ 1 bậc, KHÔNG còn là blocker cứng** — vibe-check qua demo 2026-09-15 xác nhận cấu trúc UI màn "Xác nhận giao hàng" đã khớp PRD (4 loại đối tượng nhận). Vẫn cần **1 lượt xác nhận trên STG thật có upload ảnh thật** trước `generate-tc` vì demo không cho verify được submit end-to-end (dropzone ảnh không hoạt động).
2. **`RISK-DLV-11` (mới)** — popup "Tôi đã lấy hàng" trên demo thiếu field ảnh mà PRD đã resolve (`BR06-01`); verify cùng lượt STG ở mục #1.
3. **`SC-DLV-062` (log append-only) là SC quan trọng nhất về nghiệp vụ** — đối chiếu trực tiếp với bug đã biết ở `TS`; nếu chưa fix, dự kiến FAIL có chủ đích (giống pattern `SC-TS-003`/`RISK-TS-01`).
4. **Gộp lịch chạy các SC cần tiền đề thời gian dài:** `SC-DLV-024` (2h/4h, v1.0) + `SC-DLV-048` (4h/24h) + `SC-DLV-054` (24h) + `SC-TS-006` (v1.0) — cùng 1 kế hoạch seed timestamp hoặc chờ thời gian thực, tránh chạy rời rạc nhiều lần.
5. **`GPS-01`/`COST-01` tiếp tục ngoài scope** — không viết SC, không cần hỏi lại PM trừ khi có tài liệu mới.
6. **⚠️ Chưa chụp được màn trạng thái `RESCHEDULED`/`RETURNING`/nhóm đóng** (`SC-DLV-031/032/033`) — luồng "Xử lý đơn hàng" bị chặn ở đúng ô ảnh bằng chứng nói trên nên không đi hết tới trạng thái cuối trên demo; đã có bằng chứng cấu trúc FORM (`00_input/v1.1/design/DLV_05/06`), còn thiếu bằng chứng MÀN HÌNH KẾT QUẢ — bổ sung khi có STG thật.
