---
id: v1.0/CNL-huy-don/changelog
title: Changelog — Module CNL
type: changelog
version: v1.0
sprint: 1
module:
  code: CNL
  dir: CNL-huy-don
  name: Huỷ đơn / Huỷ nhận đơn
doc_source:
  - id: DOC-v1.0-01
    section: "§A5 (BR-INT-04/05) · §A8 (TS-01/02) · §D2 (L233) · §D3 (CNL-01) · §D4 (BR-CNL-01, BR-ASN-03, permission matrix L285-286) · §D5 (L294) · §D7 (OPR-09, OPR-11) · §D8.3 (VAL-03, VAL-04) · §D1b (US-D16)"
  - id: DOC-v1.0-06
    section: "KP-01 §7 (KB-CNL-01/02) · §5 (KB-DLV-05) · §3 (KB-ORD-07 #7) · KP-02 §2/§3 · KP-05 §4"
id_range:
  req: REQ-CNL-001..007
  sc: "SC-CNL-001..013 (NEW)"
  cl: "C-CNL-01 · C-CNL-02 (cả 2 home canonical ở đây)"
  risk: RISK-CNL-01..06
status: ANALYZED
updated: 2026-09-07
---

# Changelog — Module CNL (`CNL`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-07 | INIT | Phân tích lần đầu §D3/§D4/§D7/§D8.3 — 7 REQ (`001..007`), 13 SC, 2 CL, 6 RISK. Điểm nghiệp vụ đáng chú ý nhất: **4 gap đã live-verify**, trong đó **huỷ nhận đơn XOÁ dòng "Ghép thành công"** khỏi LỊCH SỬ — vi phạm trực tiếp `BR-INT-04`/`TS-02` (audit trail bất biến) | `DOC-v1.0-01` §A5/§A8/§D2/§D3/§D4/§D7/§D8.3/§D1b · `DOC-v1.0-06` KP-01 §7 | Dựng đủ 5 deliverable + `CHANGELOG.md` |
| 2026-09-07 | INIT | **Nhận home canonical của `C-CNL-01`** (màn Báo sự cố) và **`C-CNL-02`** (log LỊCH SỬ khi huỷ) | 2 CL đều thuộc nghiệp vụ huỷ đơn; `DLV` chỉ tham chiếu `C-CNL-01` | `DLV-giao-nhan/risk_assessment.md` tham chiếu; `SC-CNL-006` ghi nhận thiếu bề mặt tạo sự cố |
| 2026-09-07 | SCOPE↓ | `REQ-CNL-007` (màn Báo sự cố) để **gap SC có chủ đích** — `[INCIDENT]` có trong sơ đồ vòng đời và `BR-ASN-03` yêu cầu, nhưng **không tài liệu nào mô tả field/màn** | `C-CNL-01` Resolved: out of scope v1.0 | Ghi ở §3; `SC-CNL-006` đã ghi nhận sự thiếu vắng ⇒ ⛔ không tạo SC riêng |
| 2026-09-07 | INIT | Giữ nguyên **4 SC dự kiến FAIL** của đợt cũ (`KP-05 §4` — *"4 test case CỐ Ý viết để FAIL"*): 2 SC về `VAL-04` + 2 SC về log LỊCH SỬ | Gap đã live-verify Chrome MCP 2026-07-29 + user chốt hướng override | `SC-CNL-004`, `SC-CNL-009`, `SC-CNL-010`, `SC-CNL-012` — chạy để **log 4 bug đợt cũ chưa log** |
| 2026-09-07 | REFACTOR | Đổi tên thư mục module `CNL/` → `CNL-huy-don/` — tên gợi nghĩa để người mới đọc thư mục là biết chức năng. Cập nhật kèm: frontmatter `id:` của 5 deliverable + `module.dir` ở file này + mọi cross-ref `CNL/<file>.md` | Yêu cầu QC GiangDC2 2026-09-07 (mã 2–4 chữ không nói lên chức năng) · `Project_rule §Module Codes` nay có cột `Dir` riêng | ⛔ **Mã module `CNL` và toàn bộ ID (`REQ-CNL-*` · `SC-CNL-*`) KHÔNG đổi** — chỉ đường dẫn thư mục đổi. TC chưa sinh nên không TC nào bị ảnh hưởng |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Phân biệt nghiêm ngặt "Huỷ đơn" ⟷ "✕ Huỷ nhận đơn"** — 2 hành động, 2 kết quả trái ngược (`CANCELLED` vs về `POSTED`) | `OPR-09` L345 · `US-D16` L195 · nhãn nút khác nhau ở `KB-DLV-01` ô 2 | TC assert sai trạng thái cuối: tưởng đơn đã kết thúc trong khi đơn đang chờ người khác nhận (hoặc ngược lại) |
| 2 | ⛔ **`SC-CNL-004`/`SC-CNL-009`/`SC-CNL-010`/`SC-CNL-012` viết theo SPEC** — dự kiến FAIL và FAIL là kết quả đúng | 4 gap đã live-verify (`KB-CNL-01`, `KB-CNL-02`) + `C-CNL-02` Resolved theo hướng **override** | "Sửa expected cho PASS" = hợp thức hoá việc **xoá log audit** và việc lý do huỷ có thể vô nghĩa; 4 bug sẽ không bao giờ được log |
| 3 | ⚠️ **Verify log LỊCH SỬ NGAY tại màn Theo dõi đơn, trước khi rời màn** | Đơn "Đã huỷ" **biến mất khỏi cả 2 tab** màn Hoạt động (`KB-ORD-07` #7) ⇒ không tìm lại được từ phía user | Rời màn rồi mới nhớ verify ⇒ phải tạo đơn mới và chạy lại toàn bộ tiền đề |
| 4 | ⚠️ **`SC-CNL-005` phải kiểm CẢ 3 VAI** ở trạng thái "Đang giao" | `OPR-11` viết *"KHÔNG **ai** được huỷ"* — rule áp cho mọi vai | Chỉ kiểm 1 vai ⇒ bỏ sót vai còn quyền huỷ sai, lỗi lọt ra production |
| 5 | ⛔ **KHÔNG viết TC luồng "Báo sự cố"** | `C-CNL-01` Resolved: màn Báo sự cố **chưa có đặc tả**, out of scope v1.0 | TC cho màn không tồn tại ⇒ FAIL vĩnh viễn; cần nêu với PM như **gap nghiệp vụ**, không phải bug |
| 6 | ⚠️ **Banner đỏ *"Đơn hàng đã bị huỷ"* KHÔNG thay thế được log LỊCH SỬ** | `TS-01` yêu cầu log; banner là hiển thị tạm thời, không phải audit record | Đánh PASS cho `SC-CNL-009` vì thấy banner ⇒ bỏ qua bug thiếu log audit |
| 7 | ⚠️ **Chuỗi boundary lý do huỷ phải test đủ 4 mốc:** `rỗng` → `4 ký tự` → `5 ký tự` → `5 dấu cách` | 2 mốc giữa là 2 bug khác nhau đã live-verify (`KB-CNL-02`) | Test thiếu mốc ⇒ bỏ sót 1 trong 2 bug (đặc biệt mốc "5 dấu cách" vi phạm cả `VAL-03`) |
| 8 | ⚠️ **Hệ quả chéo sang `DLV`:** `SC-DLV-029` (timeline đủ mốc) phải chạy trên đơn **đi thẳng tới Hoàn thành** | Đơn từng bị huỷ nhận sẽ **thiếu mốc "Ghép thành công"** do bug `SC-CNL-010` | Chẩn đoán sai: kết luận `DLV` thiếu ghi mốc trong khi lỗi thuộc `CNL` |

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 **4 bug đã biết chưa log Jira** (2 về `VAL-04` · 2 về log LỊCH SỬ) | Đợt cũ live-verify 2026-07-29, có TC cố ý viết để FAIL nhưng **chưa log bug** (`KP-05 §5`) | Chạy 4 SC tương ứng rồi `/log-bug` — có nguồn spec + live-verify sẵn |
| 2 | 🟡 `REQ-CNL-007` — màn "Báo sự cố" gap SC chủ đích | `C-CNL-01` Resolved out-of-scope | ⚠️ **Nêu với PM như gap nghiệp vụ:** `BR-ASN-03` chặn huỷ sau `IN_TRANSIT` **và** yêu cầu tạo sự cố — nếu bề mặt không có ở v1.0 thì user gặp sự cố **không có đường xử lý nào trong app** |
| 3 | 🟡 Xác nhận lại **scope module với PM** — PM xếp `CNL` out of scope Phase 1 nhưng đã phân tích đầy đủ 13 SC | `RISK-CNL-06` Pending | Hỏi PM trước khi lên kế hoạch execute; nếu giữ out-of-scope thì 13 SC chuyển sang version sau |
| 4 | 🟡 Seed đơn ở đủ 3 trạng thái (`POSTED`/`MATCHED`/`IN_TRANSIT`) + 3 tài khoản + 3 phiên đồng thời | `RISK-CNL-05` Open | Nhờ dev/QA seed; chạy `CNL` **cùng lô** với `DLV` để tái dùng đơn ở các trạng thái |
