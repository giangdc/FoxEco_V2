---
id: v1.0/ACT-hoat-dong/risk
title: Risk Assessment — v1.0 · Module ACT
type: risk-assessment
version: v1.0
sprint: 1
module: ACT
counts:
  cl: 2
  risk: 5
  cl_open: 2
  cl_resolved: 0
status: ANALYZED
updated: 2026-09-07
---

# Risk Assessment — v1.0 · Module ACT

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module ACT.
> 🔑 Frontmatter `counts:` = nguồn canonical CL/RISK. **Layout v2 ⇒ đây là home của Clarification.**
> 📌 **Đây là home canonical của `C-ORD-06`** (empty state) — CL dùng chung cho 5 màn (Hoạt động · Quà đã nhận · Thông báo · Trang chủ · Bảng tin). Các module khác chỉ tham chiếu.

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| ACT | **Medium** | **Đặc tả mỏng nhất dự án** — 6/9 REQ chỉ có nguồn `QA-obs` + 1 ảnh mockup, BRD/PRD gần như không mô tả màn này. Kèm chi phí thiết lập tiền đề cao (cần đồng thời 6 nhóm đơn) |

## Chi tiết rủi ro (bảng hợp nhất)
| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-ACT-01 | ACT / Nguồn đặc tả | **6/9 REQ chỉ có 1 nguồn** (`KP-01 §3 KB-ORD-07` = `QA-obs` + ảnh mockup); BRD/PRD không mô tả card, tab mặc định, rule ẩn đơn "Đã huỷ" ⇒ nếu quan sát cũ sai thì cả nhóm SC sai theo | **High** | `DOC-v1.0-06` KP-01 §3 `KB-ORD-07` (nguồn `QA-obs` 2026-07-27) | Vibe-test xác nhận lại toàn bộ 7 dòng của `KB-ORD-07` trước khi generate-tc | Vibe-test màn Hoạt động **trước** khi viết TC; kết quả về qua `/analyze --update` | Open | REQ-ACT-002, REQ-ACT-005, REQ-ACT-006, REQ-ACT-007 |
| RISK-ACT-02 | ACT / Đích tap card | 2 nguồn nêu 2 đích khác bản chất ("Chi tiết tin" public vs "Theo dõi đơn" role-aware). Nếu app mở **Chi tiết tin** cho đơn của chính mình thì trùng đúng bug `SC-FEED-011` (chủ tin thấy CTA "Tôi mang giúp được") | Medium | `KP-01` §3 KB-ORD-07 (#5) vs `DOC-v1.0-02` §3.7 đoạn 2 | `SC-ACT-011` ghi nhận màn đích; đối chiếu với `RISK-FEED-02` | Hỏi BA (`C-ACT-01`); vibe-test tap card của chính mình | Open | REQ-ACT-006, SC-ACT-010, SC-ACT-011 |
| RISK-ACT-03 | ACT / Tiền đề dữ liệu | Cần **đồng thời 6 nhóm đơn** (đang hoạt động · Hoàn thành · Hết hạn · Đã huỷ · tài khoản không đơn hoạt động · tài khoản chưa có đơn kết thúc). Đơn `Hết hạn` ⛔ không seed được qua UI | Medium | `test_data_catalog.md` §Ghi chú chung · `ORD-dang-tin/risk_assessment.md` `RISK-ORD-06` | Lập kế hoạch seed dữ liệu trước khi execute cả lô | Nhờ dev/QA seed đơn quá hạn + 1 tài khoản trắng trên STG | Open | REQ-ACT-003, REQ-ACT-004, REQ-ACT-005, REQ-ACT-008 |
| RISK-ACT-04 | ACT / Empty state | Text empty state **chưa có đặc tả** và CL từng bị **revert Resolved→Open** vì đánh dấu Resolved không kèm bằng chứng ⇒ dễ tái diễn nếu ai đó "chốt theo mô tả chat" | Medium | `C-ORD-06` (`KP-02` §5, §6) | `SC-ACT-012`/`SC-ACT-014` ghi nhận, không assert text | Chờ BA; ⛔ không ghi Resolved khi chưa có ảnh/câu trả lời có ngày | Open | REQ-ACT-008, SC-ACT-012, SC-ACT-014 |
| RISK-ACT-05 | ACT / UI leftover | Chuỗi `★★★★★ Đã đánh giá` trên card Hoàn thành là leftover của rating đã defer ⇒ reviewer/tester sau dễ hiểu là v1.0 có tính năng đánh giá và viết TC chấm sao | Low | `DOC-v1.0-02` §3.7 vs `C-GIFT-01` Resolved-deferred | `SC-ACT-013` ghi nhận sự tồn tại, không assert giá trị | Ghi ràng buộc ở `CHANGELOG §2` | Resolved | REQ-ACT-009, SC-ACT-013 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-ORD-06 | 🔴 Text empty state của các màn khi không có data (**home canonical ở đây**) | 🔴 **Open** (từng Resolved 2026-07-28 → **REVERT** 2026-07-29) | mở lại 2026-07-29 | REQ-ACT-008 · và `HOME`/`FEED`/`NTF`/`GIFT` |
| C-ACT-01 | 🔴 Tap card ở màn Hoạt động mở "Chi tiết tin" hay "Theo dõi đơn"? | 🔴 **Open** | mở 2026-09-07 | REQ-ACT-006 |

### C-ORD-06 · 🔴 Text empty state (home canonical)

**Source Quote (ambiguous — chính sự thiếu vắng là nội dung của CL):**
> "**C-ORD-06** | Empty state của 3 màn (Hoạt động · Quà đã nhận · Thông báo) khi không có data | ⚠ **Có lịch sử đảo chiều:** từng Resolved 2026-07-28 với text *"Hiện tại chưa có dữ liệu"*, sau đó **REVERT về Open 2026-07-29** vì rà lại toàn bộ 82 ảnh Figma + BRD + demo docx **không tìm thấy bằng chứng nào** — nhãn "Resolved" cũ chỉ dựa trên mô tả qua chat không kèm nguồn. QA xác nhận đang nhờ BA bổ sung text chính thức"

**Source Location:** `DOC-v1.0-06 KP-02 §5 · bảng "Nhóm Open" · dòng "C-ORD-06"`

**Analyst Note:** **Phạm vi mở rộng ở lượt này từ 3 màn lên 5 màn**: Hoạt động (2 tab ⇒ 2 SC) · Quà đã nhận · Thông báo · **Trang chủ** (`SC-HOME-024`) · **Bảng tin** (`SC-FEED-013`). Cùng một câu trả lời của BA đóng được cả 6 SC. ⚠️ **Bài học vận hành** (`KP-02 §6`): CL này là 1 trong 2 ca phải revert `Resolved → Open` vì đánh dấu Resolved dựa trên mô tả chat không kèm bằng chứng ⇒ chỉ ghi `Resolved` khi có **(a)** câu trả lời BA/PO ghi rõ ngày + nội dung nguyên văn, **hoặc (b)** ảnh Figma có hash, **hoặc (c)** screenshot vibe-test. **Non-blocking** — 6 SC đã viết dạng ghi nhận nên generate-tc chạy được.

### C-ACT-01 · 🔴 Đích tap card ở màn Hoạt động

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-06` KP-01 §3 KB-ORD-07 dòng 5): "| 5 | Tap card ≠ "Hết hạn" | → mở màn **"Chi tiết tin"** |"
> Nguồn B (`DOC-v1.0-02` §3.7 đoạn 2): "Tab "Đang diễn ra": card đơn hiện tại (nếu có) → bấm vào mở **Theo dõi đơn**."

**Source Location:** `DOC-v1.0-06 KP-01 §3 "KB-ORD-07" · bảng · dòng 5` ⟷ `DOC-v1.0-02 §3.7 · đoạn 2`

**Analyst Note:** Hai màn **khác bản chất**, không phải khác cách gọi tên: *"Chi tiết tin"* là màn **public** (module `FEED`, có CTA "Tôi mang giúp được", không role-aware) · *"Theo dõi đơn"* là màn **role-aware** (module `DLV`, nút hành động theo vai + 5 mốc trạng thái). Hệ quả nếu app mở **Chi tiết tin**: chủ tin sẽ thấy nút "Tôi mang giúp được" trên đơn của chính mình ⇒ trùng đúng bug đã xác nhận `C-ASN-02`/`SC-FEED-011`. Ngược lại, `HOME` đã rõ là mở **Theo dõi đơn** (`SC-HOME-015`) ⇒ nghi vấn `KB-ORD-07` (#5) ghi nhận nhầm tên màn. **Non-blocking** — `SC-ACT-010` assert theo dữ liệu ("đúng đơn"), không theo tên màn.

## Khuyến nghị tổng thể
1. **Resolve trước generate-tc:** không có blocker, nhưng **`RISK-ACT-01` cần vibe-test trước** — 6/9 REQ dựa vào 1 lượt `QA-obs` từ 2026-07; nếu quan sát đó lệch thì cả nhóm TC sai theo.
2. **Ưu tiên test high-risk:** `SC-ACT-004` và `SC-ACT-005` (lọc data theo tab) — đây là chỗ TC gộp tab của đợt cũ **không bắt được lỗi**, và là case gốc sinh ra `§Custom Rules §10.2`.
3. **Cần môi trường/dữ liệu:** seed đồng thời 6 nhóm đơn; 2 tiền đề khó nhất là **đơn `Hết hạn`** (nhờ dev, không seed được qua UI) và **tài khoản trắng**. Không có bộ này thì 6/14 SC blocked.
4. **ID/text cleanup (non-blocking, cần trước automation):** chốt đích tap card (`C-ACT-01`) vì nó quyết định luồng điều hướng trong script · chốt bản text lý do "Hết hạn" (2 nguồn lệch phần cuối câu) vì sẽ dùng làm assert text.
