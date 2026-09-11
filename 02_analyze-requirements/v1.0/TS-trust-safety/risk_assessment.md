---
id: v1.0/TS-trust-safety/risk
title: Risk Assessment — v1.0 · Module TS
type: risk-assessment
version: v1.0
sprint: 1
module: TS
counts:
  cl: 1
  risk: 5
  cl_open: 0
  cl_resolved: 1
status: ANALYZED
updated: 2026-09-07
---

# Risk Assessment — v1.0 · Module TS

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module TS.
> 🔑 Frontmatter `counts:` = nguồn canonical CL/RISK — **chỉ đếm CL có home ở module này**; CL tham chiếu (home ở module khác) KHÔNG tính vào `counts`. **Layout v2 ⇒ đây là home của Clarification.**
> 📌 **Home canonical của `C-TS-01`** (Admin Web Portal).

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| TS | **Medium** | Module nhỏ nhưng chứa **rule bị app vi phạm rõ nhất của cả dự án**: log audit phải bất biến (`TS-02`+`BR-INT-04`) nhưng huỷ nhận đơn **XOÁ** dòng log đã ghi. Ngoài ra **phần lớn phạm vi module không test được** từ phía end-user |

## Chi tiết rủi ro (bảng hợp nhất)
| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-TS-01 | TS / Audit trail | **Log KHÔNG bất biến** — huỷ nhận đơn xoá dòng "Ghép thành công" ⇒ vi phạm `TS-02`+`BR-INT-04`; mất bằng chứng khi tranh chấp, và `TS-03` (*"Admin can thiệp **dựa trên log**"*) mất nền tảng | **High** | `TS-02` L122 · `BR-INT-04` L80 vs `KP-01` §7 KB-CNL-01 (live-verify) | `SC-TS-003` (P1) — thử **nhiều hành động**, không chỉ huỷ nhận | Log bug; kiểm chéo `SC-CNL-010` | Open | REQ-TS-002, SC-TS-003 |
| RISK-TS-02 | TS / Log actor khi huỷ | `TS-01` yêu cầu log **huỷ (kèm lý do + ai huỷ)** nhưng app **không ghi log nào** khi huỷ đơn ⇒ nhóm thông tin thứ 5 của `TS-01` hoàn toàn thiếu | **High** | `TS-01` L121 vs `KP-01` §7 KB-CNL-01 | `SC-TS-002` (actor) + `SC-CNL-009` (log huỷ) | Log bug ở `CNL`; SC ở đây kiểm từ góc audit | Open | REQ-TS-001, SC-TS-002 |
| RISK-TS-03 | TS / Phạm vi không test được | **Phần lớn module nằm ngoài bề mặt test:** Admin Web Portal không có đặc tả (`C-TS-01`), cột `Admin` trong permission matrix `§D4` (nhiều dòng *"✓ override"*) **không test được** ⇒ dễ báo cáo coverage cao hơn thực tế | Medium | `§A3` L29 · `§D4` L279-286 · `KP-01` §9 KB-TS-01 | `SC-TS-007` ghi nhận rõ phạm vi không phủ được | **Nêu rõ trong test report:** nhánh Admin không nằm trong phạm vi v1.0 | Pending | REQ-TS-003, SC-TS-007 |
| RISK-TS-04 | TS / Consent khi ghép | `§A8` yêu cầu consent **trước khi đăng VÀ ghép**, nhưng luồng ghép chỉ có **modal xác nhận lộ SĐT** — không phải consent điều khoản ⇒ có thể là **gap tuân thủ pháp lý**, không chỉ là gap UI | Medium | `§A8` L115 vs `ORD-09` L245 + `DOC-v1.0-02` §4.2 | `SC-TS-004` ghi nhận trạng thái 2 luồng | Nêu với BA/PO: rule `§A8` có áp cho luồng ghép hay chỉ luồng đăng? | Open | REQ-TS-004, SC-TS-004 |
| RISK-TS-05 | TS / Tiền đề thời gian | `SC-TS-006` cần **4 giờ thực tế** (2h nhắc + 2h admin) — cùng tiền đề `SC-DLV-024` ⇒ dễ bị bỏ qua ở cả 2 module | Medium | `BR-CNF-04` L266 · `DLV` `RISK-DLV-04` | Chạy 1 lần, lấy dữ liệu cho cả `SC-TS-006` và `SC-DLV-024` | Kế hoạch riêng hoặc dev seed timestamp; chưa chạy đủ mốc thì GHI RÕ | Open | REQ-TS-003, SC-TS-006 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-TS-01 | Admin Web Portal có đặc tả UI để test không? (**home canonical ở đây**) | ✅ Resolved — **Out of scope v1.0** | 2026-07-27 | REQ-TS-003 |
| C-CNL-02 | Huỷ đơn / huỷ nhận đơn có ghi log LỊCH SỬ (tham chiếu — home ở `CNL`) | ✅ Resolved — **PHẢI ghi log**; hành vi hiện tại là gap | 2026-07-30 | REQ-TS-002 |

### C-TS-01 · Admin Web Portal (home canonical)

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-01` §A3 L29): "Tagline: "Tiện đường — Đồng nghiệp giúp nhau" · Nền tảng: Mobile App (iOS/Android) + **Admin Web Portal**."
> Nguồn B (`DOC-v1.0-01` §A8 `TS-03` L123): "Admin có quyền can thiệp hỗ trợ khi có vướng mắc (dựa trên log)"
> Nguồn C (`DOC-v1.0-01` §D4 permission matrix L279-286): nhiều dòng có cột `Admin` = *"✓ override"*
> Nguồn D — PHÁN QUYẾT (`DOC-v1.0-06` KP-01 §9 `KB-TS-01`): "BRD §A3 chỉ nhắc tên nền tảng…, **không mô tả màn hình/field nào**." · "Phạm vi test v1.0 chỉ verify **hệ quả quan sát được từ phía end-user**…, không test UI Admin Portal."

**Source Location:** `DOC-v1.0-01 §A3 · L29` · `§A8 · TS-03 · L123` · `§D4 · permission matrix · L279-286` ⟷ `DOC-v1.0-06 KP-01 §9 "KB-TS-01"`

**Analyst Note:** Resolved 2026-07-27: **out of scope v1.0** — nền tảng được nhắc tên nhưng **không có đặc tả UI**. ⚠️ **Hệ quả cần nêu rõ trong test report:** cột `Admin` của permission matrix `§D4` xuất hiện ở **nhiều dòng chức năng** với quyền *"✓ override"* — toàn bộ nhánh này **không nằm trong phạm vi test v1.0** ⇒ ⛔ đừng để stakeholder hiểu là bộ TC đã phủ hết permission matrix. `SC-TS-007` tồn tại để chốt điều đó bằng một SC có ID, thay vì chỉ là ghi chú.

### C-CNL-02 · Log LỊCH SỬ khi huỷ *(tham chiếu)*

**Source Quote:**
> "User chốt: *"huy don va huy nhan don hien tai cu luu log lich su nha"* → **LỊCH SỬ phải ghi log cho cả 2 hành động; hành vi hiện tại là GAP cần dev bổ sung.**"

**Source Location:** `DOC-v1.0-06 KP-01 §7 "KB-CNL-01"` (home canonical: `CNL-huy-don/risk_assessment.md`)

**Analyst Note:** CL này là **nền của 2 rule ở module TS**: `TS-01` (log phải có nhóm *"huỷ (kèm lý do + ai huỷ)"*) và `TS-02` (log bất biến). Resolved theo hướng **override hành vi hiện tại** ⇒ 2 SC ở module này (`SC-TS-002`, `SC-TS-003`) viết theo rule và **dự kiến FAIL**. ⚠️ Mức độ nghiêm trọng nhìn từ `TS` **cao hơn** nhìn từ `CNL`: ở `CNL` đó là *"thiếu/xoá log của luồng huỷ"*; ở `TS` đó là **audit trail không đáng tin** — làm `TS-03` (*"Admin can thiệp dựa trên log"*) mất nền tảng và mất bằng chứng khi tranh chấp (`§D5` L296: *"Admin cung cấp ảnh + timeline"*).

## Khuyến nghị tổng thể
1. **Resolve blocker trước generate-tc:** cả 2 CL đã Resolved ⇒ **không có blocker**. Cần nêu với BA/PO 1 câu hỏi mới: rule `§A8` (*"buộc consent trước khi đăng/ghép"*) có áp cho **luồng ghép** hay chỉ luồng đăng? (`RISK-TS-04`).
2. **Ưu tiên test P1 high-risk:** `SC-TS-003` (log bất biến) — chạy **cùng lô** với `SC-CNL-010` để có 1 bug report đầy đủ cả 2 góc nhìn (luồng huỷ + thuộc tính audit).
3. **Cần môi trường/dữ liệu:** 1 đơn **đi thẳng tới Hoàn thành** (cho `SC-TS-001/002`) + 1 đơn để phá log (cho `SC-TS-003`) + tiền đề **4 giờ** dùng chung với `SC-DLV-024`.
4. **Báo cáo trung thực về phạm vi:** ghi rõ trong test report rằng **nhánh Admin (permission matrix `§D4` cột Admin) không nằm trong phạm vi v1.0** — đây là phần lớn chức năng của `TS-03` và không có cách nào phủ từ phía end-user.
