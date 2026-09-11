---
id: v1.0/CNL-huy-don/risk
title: Risk Assessment — v1.0 · Module CNL
type: risk-assessment
version: v1.0
sprint: 1
module: CNL
counts:
  cl: 2
  risk: 6
  cl_open: 0
  cl_resolved: 2
status: ANALYZED
updated: 2026-09-07
---

# Risk Assessment — v1.0 · Module CNL

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module CNL.
> 🔑 Frontmatter `counts:` = nguồn canonical CL/RISK. **Layout v2 ⇒ đây là home của Clarification.**
> 📌 **Home canonical của `C-CNL-01`** (màn Báo sự cố) và **`C-CNL-02`** (log LỊCH SỬ khi huỷ).

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| CNL | **Medium-High** | Chứa **4 gap đã live-verify** (2 về `VAL-04`, 2 về log LỊCH SỬ), trong đó **huỷ nhận đơn XOÁ log đã ghi** vi phạm trực tiếp `BR-INT-04`/`TS-02` (audit trail bất biến) — đây là lỗi nặng nhất về tính toàn vẹn dữ liệu của cả dự án |

## Chi tiết rủi ro (bảng hợp nhất)
| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-CNL-01 | CNL / Audit trail | **Huỷ nhận đơn XOÁ dòng "Ghép thành công"** khỏi LỊCH SỬ ⇒ vi phạm `BR-INT-04` (*"không sửa được sau khi ghi"*) và `TS-02` (audit trail) — mất bằng chứng khi tranh chấp | **High** | `KP-01` §7 KB-CNL-01 (live-verify 2026-07-29) vs `BR-INT-04` L80 · `TS-02` L122 | `SC-CNL-010` — assert dòng log vẫn còn | Log bug (chưa log ở đợt cũ); ⛔ không sửa expected cho PASS | Open | REQ-CNL-006, SC-CNL-010 |
| RISK-CNL-02 | CNL / Log huỷ | **Huỷ đơn không ghi log nào**, chỉ hiện banner đỏ ⇒ vi phạm `TS-01` (*"ghi log… huỷ (kèm lý do + ai huỷ)"*); banner **không thay thế** được log | **High** | `KP-01` §7 KB-CNL-01 vs `TS-01` L121 · `C-CNL-02` Resolved-override | `SC-CNL-009` — assert có dòng log mới | Log bug; user đã chốt hướng override 2026-07-30 | Open | REQ-CNL-006, SC-CNL-009 |
| RISK-CNL-03 | CNL / VAL-04 | Ngưỡng **5 ký tự không được enforce** (4 ký tự vẫn qua) và **không trim khoảng trắng** (5 dấu cách vẫn qua) ⇒ lý do huỷ có thể vô nghĩa, làm mất giá trị của chính rule *"bắt buộc lý do"* | Medium | `VAL-04` L395 · `VAL-03` L394 vs `KP-01` §7 KB-CNL-02 | `SC-CNL-004` + `SC-CNL-012` | Log 2 bug riêng (2 lỗi khác nhau) | Open | REQ-CNL-002, SC-CNL-004, SC-CNL-012 |
| RISK-CNL-04 | CNL / Hai hành động huỷ | **"Huỷ đơn" ⟷ "Huỷ nhận đơn" cho 2 kết quả trái ngược** (`CANCELLED` vs về `POSTED`) ⇒ TC trộn 2 hành động sẽ assert sai trạng thái cuối | Medium | `OPR-09` L345 · `US-D16` L195 · `KB-DLV-01` ô 2·Carrier | `SC-CNL-007` có mệnh đề phủ định *"đơn KHÔNG chuyển Đã huỷ"* | Ghi ràng buộc `CHANGELOG §2`; nhãn nút khác nhau là dấu hiệu phân biệt | Resolved | REQ-CNL-004, SC-CNL-007 |
| RISK-CNL-05 | CNL / Verify sau huỷ | Đơn "Đã huỷ" **biến mất khỏi màn Hoạt động** (`KB-ORD-07` #7) ⇒ sau khi huỷ **không xem lại được đơn từ phía user** để verify log/lý do | Medium | `KP-01` §3 KB-ORD-07 (#7) | Mở block LỊCH SỬ **trước khi** rời màn Theo dõi đơn | Ghi vào bước TC: verify log ngay tại màn, ⛔ không rời màn rồi tìm lại | Open | REQ-CNL-005, SC-CNL-008, SC-CNL-009 |
| RISK-CNL-06 | CNL / Scope | PM xếp `CNL` **out of scope Phase 1** (`KP-03 §3.1`) nhưng đợt cũ **vẫn viết 27 TC**; lượt này phân tích đầy đủ theo quyết định 2026-09-07 ⇒ nếu PM giữ nguyên out-of-scope thì 13 SC này không được execute | Low | `KP-03` §3.1 · quyết định scope 2026-09-07 (`Project_rule §Active Memory Rules`) | — | Xác nhận lại với PM trước khi lên kế hoạch execute | Pending | toàn module |

## Clarifications (home của CL quote — layout v2)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-CNL-01 | Màn "Báo sự cố" (Incident) — có đặc tả không? (**home canonical ở đây**) | ✅ Resolved — **Out of scope v1.0** (chưa có đặc tả field) | 2026-07-27 | REQ-CNL-003, REQ-CNL-007 |
| C-CNL-02 | Huỷ đơn / Huỷ nhận đơn có ghi log LỊCH SỬ không? (**home canonical ở đây**) | ✅ Resolved — **PHẢI ghi log** cho cả 2; hành vi hiện tại là gap cần dev bổ sung | 2026-07-30 | REQ-CNL-006 |

### C-CNL-01 · Màn "Báo sự cố" (Incident)

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-01` §D4 `BR-ASN-03` L264): "Sau khi nhận hàng (IN_TRANSIT) không hủy thường → **phải tạo sự cố**"
> Nguồn B (`DOC-v1.0-01` §D2 L233): "Ngoài luồng: [CANCELLED "Đã huỷ"]… · [EXPIRED] · **[INCIDENT]**"
> Nguồn C (`DOC-v1.0-01` §D5 L294): "Sau khi nhận, hàng hỏng/mất | **Tạo sự cố**, không cho COMPLETED thường; dùng timeline + ảnh làm bằng chứng"
> Nguồn D (`DOC-v1.0-06` KP-01 §5 `KB-DLV-05`): "Màn "Báo sự cố" chưa có đặc tả — out of scope v1.0"

**Source Location:** `DOC-v1.0-01 §D4 · BR-ASN-03 · L264` · `§D2 · L233` · `§D5 · L294` ⟷ `DOC-v1.0-06 KP-01 §5 "KB-DLV-05"`

**Analyst Note:** **3 nguồn BRD yêu cầu tính năng** (`BR-ASN-03` + trạng thái `[INCIDENT]` trong sơ đồ + edge case `§D5`) nhưng **không nguồn nào mô tả field/màn**; `§D4` permission matrix (L286) còn ghi *"Báo sự cố | ✓ | ✓ | ✓ | ✓"* — tức cả 4 vai đều có quyền. BA/PO chốt 2026-07-27: **out of scope v1.0** (chưa có đặc tả). ⇒ Theo `§Custom Rules §10.1`, ⛔ không viết SC khẳng định; `SC-CNL-006` ghi nhận sự thiếu vắng bề mặt. ⚠️ **Hệ quả nghiệp vụ cần nêu với PM:** rule `BR-ASN-03` chặn huỷ sau `IN_TRANSIT` **và** yêu cầu tạo sự cố — nếu bề mặt tạo sự cố không có ở v1.0 thì user gặp sự cố sau khi lấy hàng **không có đường xử lý nào trong app**.

### C-CNL-02 · Huỷ đơn / Huỷ nhận đơn có ghi log LỊCH SỬ không?

**Source Quote (ambiguous):**
> Rule (`DOC-v1.0-01` §A8 `TS-01` L121): "Ghi log toàn bộ tương tác: ai đăng, ai nhận, mốc thời gian, đổi trạng thái, **huỷ (kèm lý do + ai huỷ)**"
> Rule (`§A5` `BR-INT-04` L80): "Timeline tương tác **không sửa được sau khi ghi** (audit)"
> Hành vi (`DOC-v1.0-06` KP-01 §7 `KB-CNL-01`, live-verify 2026-07-29): "**Huỷ đơn** (Sender/Receiver) → **không ghi log nào** vào block LỊCH SỬ, chỉ hiện banner đỏ *"Đơn hàng đã bị huỷ"*" · "**Huỷ nhận đơn** (Carrier) → tệ hơn: **XOÁ LUÔN dòng "Ghép thành công"** khỏi LỊCH SỬ"
> Phán quyết (user chốt 2026-07-30): "*"huy don va huy nhan don hien tai cu luu log lich su nha"* → **LỊCH SỬ phải ghi log cho cả 2 hành động; hành vi hiện tại là GAP cần dev bổ sung.**"

**Source Location:** `DOC-v1.0-01 §A8 · TS-01 · L121` · `§A5 · BR-INT-04 · L80` ⟷ `DOC-v1.0-06 KP-01 §7 "KB-CNL-01"` (live-verify Chrome MCP) · `KP-02 §2 · dòng "C-CNL-02"`

**Analyst Note:** **Resolved theo hướng OVERRIDE hành vi hiện tại** (user chốt 2026-07-30, có nguyên văn) — tức spec thắng, app phải sửa. Đủ chuẩn `Resolved` theo `KP-02 §6` (câu trả lời có ngày + nguyên văn + live-verify kèm bằng chứng). **Hai gap khác mức độ:** *thiếu* log (vi phạm `TS-01`) ⟷ **XOÁ** log đã ghi (vi phạm `BR-INT-04` + `TS-02` — **nặng hơn**, vì phá tính bất biến của audit trail). ⚠️ **Ảnh hưởng chéo:** `SC-DLV-029` (timeline đủ mốc) phải chạy trên đơn **đi thẳng tới Hoàn thành**, vì đơn từng bị huỷ nhận sẽ thiếu mốc "Ghép thành công" do chính bug này.

## Khuyến nghị tổng thể
1. **Resolve trước generate-tc:** cả 2 CL đã Resolved ⇒ **không có blocker**. Cần **xác nhận lại scope với PM** (`RISK-CNL-06`): module này PM xếp out-of-scope Phase 1 nhưng đã phân tích đầy đủ.
2. **Ưu tiên test P1 high-risk:** `SC-CNL-005` (chặn huỷ từ "Đang giao" — kiểm cả 3 vai) · `SC-CNL-007` (Carrier huỷ nhận → về Chờ ghép) · `SC-CNL-001`/`SC-CNL-002`. Ngay sau đó chạy **4 SC dự kiến FAIL** (`SC-CNL-004`, `SC-CNL-009`, `SC-CNL-010`, `SC-CNL-012`) để **log 4 bug đã biết mà đợt cũ chưa log**.
3. **Cần môi trường/dữ liệu:** đơn ở `POSTED` · `MATCHED` · `IN_TRANSIT` + **3 tài khoản 3 vai** + **3 phiên đồng thời** (`SC-CNL-011`). ⚠️ Verify log **ngay tại màn Theo dõi đơn trước khi rời màn** — đơn "Đã huỷ" biến mất khỏi màn Hoạt động.
4. **ID/text cleanup (non-blocking, cần trước automation):** phân biệt nghiêm ngặt nhãn **"Huỷ đơn"** ⟷ **"✕ Huỷ nhận đơn"** — 2 nhãn, 2 kết quả trái ngược; dùng lẫn trong locator sẽ làm script huỷ sai kiểu và assert sai trạng thái cuối.
