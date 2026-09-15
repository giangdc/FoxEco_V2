---
id: v1.1/NTF-thong-bao/risk
title: Risk Assessment — v1.1 · Module NTF (Delta)
type: risk-assessment
version: v1.1
sprint: 1
module: NTF
counts:
  cl: 0
  risk: 1
  cl_open: 0
  cl_resolved: 0
status: ANALYZED
updated: 2026-09-15
---

# Risk Assessment — v1.1 · Module NTF (Delta)

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk **mới** của module NTF ở v1.1.
> 🔑 `counts:` chỉ đếm CL/RISK **mới mở** ở lượt này. Risk/CL CARRIED (không đổi) xem `v1.0/NTF-thong-bao/risk_assessment.md`; risk/CL **đổi Status** liệt kê lại đầy đủ ở đây (không phải mới, nhưng cần cập nhật authoritative).

## Tổng quan
| Module | Risk Level | Rủi ro chính (delta v1.1) |
|--------|-----------|--------------|
| NTF | **Low** (giảm từ Medium) | Nguy cơ lớn nhất của v1.0 (danh mục thông báo chưa chốt) đã Resolved. Rủi ro còn lại: 6 sự kiện mới cần tiền đề nghiệp vụ từ `DLV` mới quan sát được |

## Cập nhật Status risk/CL đã có (không phải RISK/CL mới — ghi lại đầy đủ vì đổi Status)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-NTF-01 | NTF / Danh mục thông báo | (mô tả gốc xem v1.0) — 3 nguồn 3 danh sách, BRD tự khai "Nháp" | High | `DOC-v1.1-01 §8.13.1` | `SC-NTF-014` giờ **assert** đủ 15 loại | **Đã resolve**: PRD v1.1 FR13 §8.13.1 chốt 15 sự kiện chính thức, ngày 2026-09-15 | **Resolved** | REQ-NTF-010, SC-NTF-014 |
| RISK-NTF-04 | NTF / Text `NTF-06` | (mô tả gốc xem v1.0) — 2 nguồn 2 text | Medium | `DOC-v1.1-01 §8.13.1` dòng `NTF-06` | `SC-NTF-005` giờ **assert** đúng text | PRD v1.1 dùng đúng bản BRD cũ ("cảm ơn bạn!"), loại bỏ nghi vấn "đánh giá ngay" | **Resolved** | REQ-NTF-003, SC-NTF-005 |
| RISK-NTF-02 | NTF / Bảo mật push | (mô tả gốc xem v1.0) — push dễ lọt SĐT nhất | High | `DOC-v1.1-01 §8.13.1` (đối chiếu đủ 15 dòng, không dòng nào có SĐT) | `SC-NTF-008` mở rộng phạm vi sang **15 sự kiện** | Chạy sớm, phủ đủ 15 sự kiện kể cả 6 sự kiện mới; FAIL → log bug P1 | Open (mở rộng phạm vi, chưa test) | REQ-NTF-005, SC-NTF-008 |

## RISK mới (delta v1.1)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-NTF-07 | NTF / Tiền đề 6 sự kiện mới | 6 sự kiện `NTF-10..15` chỉ phát sinh khi đơn đi qua nhánh phụ FR08/FR09 của `DLV` (không liên lạc được người nhận → gửi quầy/uỷ quyền → cầm hàng về → hẹn giao lại/hoàn hàng) — tiền đề dựng tốn công hơn nhánh chính, dễ bị bỏ qua khi lên lịch test | Medium | `DOC-v1.1-01 §8.13.1` + phụ thuộc `DLV-giao-nhan/test_scenario_map.md` (delta v1.1) | `SC-NTF-017..022` | Chạy `NTF` **cùng lô** với vibe-test nhánh FR08/FR09 của `DLV`, không seed riêng cho NTF | Open | REQ-NTF-012, SC-NTF-017..022 |

## Cập nhật Clarifications đã đổi Status (home canonical vẫn ở đây)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-NTF-01 | 🔴 Danh sách loại thông báo chính thức (3 nguồn, nay đã hợp nhất) | ✅ **Resolved 2026-09-15** — chính thức **15 sự kiện** theo `DOC-v1.1-01 §8.13.1` | 2026-09-15 (mở từ 2026-07) | REQ-NTF-001..004, REQ-NTF-010, REQ-NTF-012 |

### C-NTF-01 · 🔴 Danh sách loại thông báo chính thức — RESOLVED 2026-09-15

**Source Quote (resolve):**
> "§8.13.1 Danh mục thông báo" — bảng 15 dòng `NTF-01`..`NTF-15` (ID | Sự kiện kích hoạt | Người nhận | Nội dung mẫu), `DOC-v1.1-01` page 48.

**Source Location:** `DOC-v1.1-01 §8.13.1 · page 48`

**Analyst Note:** Resolved theo PRD chính thức (đã qua Approval §12), thay thế hoàn toàn 3 nguồn mâu thuẫn cũ (BRD tự nhận "Nháp", PRD-demo, Figma). 9 sự kiện cũ (`NTF-01..09`) giữ nguyên nội dung/người nhận đúng bản BRD; 6 sự kiện mới (`NTF-10..15`) bổ sung cho nhánh xử lý giao hàng không thành công. Hàng "Sắp đến khung giờ hẹn giao" mà `KP-07` (v1.0) nghi ngờ BRD bỏ sót — **không** có trong danh mục chính thức v1.1 ⇒ xác nhận không phải sự kiện chính thức, đóng nghi vấn cũ.

⚠️ **Kết luận bị đảo:** kết luận cũ *"⛔ KHÔNG assert danh mục / danh sách loại thông báo"* (`v1.0/NTF-thong-bao/CHANGELOG.md §2` ràng buộc #3) và *"⛔ KHÔNG assert text NTF-06"* (ràng buộc #4) **HẾT HIỆU LỰC kể từ v1.1** — đừng trích lại 2 ràng buộc đó cho v1.1; hiện hành là **assert đủ 15 loại + đúng text NTF-06** theo `DOC-v1.1-01 §8.13.1`.

## Vibe-check bổ sung 2026-09-15 (không resolve CL nào — ghi nhận để không lặp lại hướng đã thử)

**`C-NTF-03(a)` — cơ chế "Đánh dấu đã đọc" (home canonical `v1.0/NTF-thong-bao/risk_assessment.md`):** đã thử trực tiếp trên demo `foxeco_demo/FoxEcoQC`, đúng khuyến nghị cũ *"vibe-test thử cả 2 cách (tap item / bấm nút)"*:
> Ảnh `00_input/v1.1/design/NTF_02_thongbao_sau_danhdaudadoc_CNTF03.png` — sau khi bấm nút "Đánh dấu đã đọc" (mark-all), 3 chấm đỏ unread **VẪN CÒN NGUYÊN**, không đổi.
> Ảnh `00_input/v1.1/design/NTF_03_thongbao_sau_tap_item_CNTF03.png` — sau khi tap vào 1 item ("Tìm thấy đơn hàng phù hợp tuyến của bạn") và quay lại, chấm đỏ của item đó **VẪN CÒN**, không đổi.

↳ **Kết luận: KHÔNG resolve được `C-NTF-03(a)` qua demo này** — cả 2 cách thử đều không có hiệu ứng, tức cơ chế đọc trong demo là **dữ liệu tĩnh/mock, không nối logic thật**. Đây là giới hạn của công cụ tham chiếu (demo), không phải câu trả lời cho câu hỏi nghiệp vụ. **KHÔNG dùng 2 ảnh trên làm bằng chứng "app không có tính năng đánh dấu đã đọc"** — chỉ ghi nhận để tránh người sau lặp lại đúng 2 phép thử này trên cùng demo rồi tưởng đã có kết luận. Câu hỏi `C-NTF-03(a)` **vẫn Open**, cần hỏi BA hoặc verify trên STG thật.

## Khuyến nghị tổng thể (delta v1.1)
1. **Không còn blocker** — `C-NTF-01` đã Resolved, không cần hỏi BA trước khi generate-tc phần NTF.
2. **Ưu tiên test P1:** `SC-NTF-008` mở rộng — phải test đủ 15/15 sự kiện, không chỉ 9 sự kiện cũ.
3. **Cần môi trường/tiền đề:** 6 SC mới (`SC-NTF-017..022`) phụ thuộc trực tiếp tiến độ vibe-test nhánh FR08/FR09 bên `DLV` — lên lịch chạy chung, không tách riêng.
4. **`C-NTF-03` (cơ chế đánh dấu đã đọc), `RISK-NTF-03`, `RISK-NTF-05`, `RISK-NTF-06`** — PRD v1.1 không đề cập, giữ nguyên Open/Pending như v1.0. Đã thử vibe-check qua demo 2026-09-15 (xem mục trên) nhưng **không kết luận được** — vẫn cần hỏi BA hoặc verify STG thật, KHÔNG coi là đã xử lý.
