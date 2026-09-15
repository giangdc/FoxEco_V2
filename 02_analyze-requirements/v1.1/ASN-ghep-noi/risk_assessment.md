---
id: v1.1/ASN-ghep-noi/risk
title: Risk Assessment — v1.1 · Module ASN
type: risk-assessment
version: v1.1
sprint: 1
module: ASN
counts:
  cl: 0
  risk: 1
  cl_open: 0
  cl_resolved: 0
status: ANALYZED
updated: 2026-09-15
---

# Risk Assessment — v1.1 · Module ASN

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module ASN của v1.1 (delta).
> Chỉ ghi risk MỚI hoặc risk MODIFIED (đổi Status/Solution) so với v1.0. Risk không đổi → xem `v1.0/ASN-ghep-noi/risk_assessment.md`, không lặp lại.

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| ASN | **High** (không đổi so với v1.0) | Vẫn là module rủi ro cao nhất do double-accept + bảo mật liên hệ; riêng auto-match đã được PRD v1.1 chốt phần lớn tham số (`RISK-ASN-04`/`06` → Resolved), rủi ro còn lại chuyển sang "giá trị cấu hình trần thông báo chưa có số cứng" (risk mới) |

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-ASN-04 | ASN / Auto-match | *(cập nhật Status)* 3 tham số auto-match — 2/3 đã chốt: định nghĩa khớp (điểm + ngày overlap + buổi overlap) và chu kỳ quét (≤60s); còn "ngưỡng gộp thông báo" chuyển sang risk mới `RISK-ASN-08` | High → **hạ mức, xem RISK-ASN-08** | `DOC-v1.1-01` §8.4 BR04-01/02 · §9 NFR-04 | `SC-ASN-011` (đủ 4 nhánh a-d theo overlap thật) | Đã Resolved qua PRD v1.1; ghi ràng buộc `CHANGELOG §2` | **Resolved** | REQ-ASN-007, SC-ASN-011 |
| RISK-ASN-06 | ASN / Ưu tiên gợi ý | *(cập nhật Status)* Tiêu chí "độ gần tuyến" — trước đây coi là vô hiệu (nhị phân, không còn thang đo); PRD xác nhận vẫn là tầng ưu tiên số 1, có hiệu lực dù nhị phân | Medium → **Resolved** | `DOC-v1.1-01` §8.3 BR03-06 | `SC-ASN-015` (2 tầng ưu tiên) | Đã làm rõ qua PRD v1.1, không cần hỏi BA thêm | **Resolved** | REQ-ASN-009, SC-ASN-015 |
| RISK-ASN-02 | ASN / Double-accept | *(cập nhật Solution)* Nhánh cạnh tranh thật vẫn khó test bằng manual — nhưng giờ có ngưỡng + phương pháp chính thức để giao cho automation | High (không đổi) | `DOC-v1.1-01` §9 NFR-06 (50 request đồng thời, 0% trùng, concurrency test trên staging) | `SC-ASN-006` nhánh (b) | **Cập nhật:** giao nhánh cạnh tranh thật cho automation/backend concurrency test theo đúng ngưỡng NFR-06, không còn "đề xuất" chung chung như v1.0 | Open (nhánh manual) / **có hướng automation rõ ràng** | REQ-ASN-003, SC-ASN-006 |
| RISK-ASN-05 | ASN / Realtime | *(cập nhật Solution)* Bằng chứng đồng bộ realtime trước đây chỉ từ demo giả lập — giờ có ngưỡng định lượng để test thật | Medium (không đổi) | `DOC-v1.1-01` §9 NFR-08 (≤5 giây) | `SC-ASN-008` | **Cập nhật:** dùng ngưỡng ≤5s làm oracle pass/fail khi test trên 3 thiết bị thật, thay vì chỉ quan sát định tính | Open — chờ chạy test thật để xác nhận đạt ngưỡng | REQ-ASN-005, SC-ASN-008 |
| RISK-ASN-08 | ASN / Auto-match | **(risk mới)** Ngưỡng "trần thông báo khớp/ngày" (BR04-04) không có số cứng trong PRD ("do admin cấu hình") ⇒ không viết được TC boundary chính xác cho đến khi có giá trị thật | Medium | `DOC-v1.1-01 §8.4 BR04-04 · page 38` | `SC-ASN-014` | Hỏi admin/vận hành giá trị cấu hình thật trước generate-tc; tạm viết TC ở mức "đạt ngưỡng X (biến)/chưa đạt" không hardcode số | Open (non-blocking) | REQ-ASN-008, SC-ASN-014 |

## Clarifications (home của CL quote — layout v2)

> Không có CL mới ở lượt delta này. `C-NTF-02` (home canonical tại ASN) và `C-ASN-03` giữ nguyên trạng thái như v1.0 — xem `v1.0/ASN-ghep-noi/risk_assessment.md`. `C-NTF-02` **không đóng hẳn**: 2/3 tham số đã Resolved qua `RISK-ASN-04`, phần "ngưỡng gộp thông báo" chuyển thành `RISK-ASN-08` (risk mới, không phải CL) vì đây là thiếu **giá trị cấu hình vận hành**, không phải thiếu **định nghĩa nghiệp vụ**.

## Khuyến nghị tổng thể
1. **Không còn blocker cứng cho auto-match** — `RISK-ASN-04`/`RISK-ASN-06` đã Resolved qua PRD v1.1, coverage `SC-ASN-011`/`SC-ASN-015` có thể viết đầy đủ 4 nhánh + 2 tầng ưu tiên.
2. **Trước generate-tc:** xác nhận giá trị cấu hình thật của `RISK-ASN-08` (trần thông báo/ngày) với admin/vận hành — không hardcode số, không tái sử dụng mốc 3/5/6 cũ (mốc đó thuộc rule khác — trần gợi ý/carrier, không đổi).
3. **Ưu tiên chuyển cho automation:** nhánh cạnh tranh thật của `SC-ASN-006` (concurrency 50 request) và mốc ≤5s của `SC-ASN-008` — cả hai giờ có ngưỡng đo được rõ ràng (NFR-06, NFR-08), phù hợp hơn cho backend/integration test so với manual.
4. **SC mới `SC-ASN-019`** cần công cụ gọi API trực tiếp (Postman/tương đương) — không thực hiện được thuần qua UI, lập kế hoạch môi trường trước khi execute.
