---
id: v1.0/TS-trust-safety/changelog
title: Changelog — Module TS
type: changelog
version: v1.0
sprint: 1
module:
  code: TS
  dir: TS-trust-safety
  name: Trust & Safety
doc_source:
  - id: DOC-v1.0-01
    section: "§A3 (L29) · §A5 (BR-INT-04) · §A8 (L115, TS-01..03, L125) · §D3 (ORD-04, ORD-09) · §D4 (BR-CNF-04, permission matrix L279-286) · §D5 (L296) · §D1b (US-D09)"
  - id: DOC-v1.0-06
    section: "KP-01 §9 (KB-TS-01) · §7 (KB-CNL-01) · KP-02 §3"
id_range:
  req: REQ-TS-001..005
  sc: "SC-TS-001..007 (NEW)"
  cl: "C-TS-01 (home canonical) · C-CNL-02 (tham chiếu — home ở CNL)"
  risk: RISK-TS-01..05
status: ANALYZED
updated: 2026-09-07
---

# Changelog — Module TS (`TS`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-07 | INIT | Phân tích lần đầu §A8 — 5 REQ (`001..005`), 7 SC, 2 CL, 5 RISK. Điểm nghiệp vụ đáng chú ý nhất: **rule log bất biến (`TS-02`+`BR-INT-04`) đang bị app vi phạm** — huỷ nhận đơn XOÁ dòng "Ghép thành công", làm `TS-03` (*"Admin can thiệp dựa trên log"*) mất nền tảng | `DOC-v1.0-01` §A3/§A5/§A8/§D3/§D4/§D5/§D1b · `DOC-v1.0-06` KP-01 §7/§9 | Dựng đủ 5 deliverable + `CHANGELOG.md` |
| 2026-09-07 | INIT | **Nhận home canonical của `C-TS-01`** (Admin Web Portal — out of scope v1.0) | CL thuộc phạm vi Trust & Safety | `SC-TS-007` chốt bằng SC có ID rằng nhánh Admin không phủ được |
| 2026-09-07 | INIT | Mở góc nhìn **audit** cho 2 gap đã biết ở `CNL`: `SC-TS-002` (log thiếu actor khi huỷ) và `SC-TS-003` (log bị xoá) — **không nhân bản** SC của `CNL` mà kiểm từ thuộc tính audit, thử **nhiều hành động** | `TS-01`/`TS-02` yêu cầu ở tầng audit, rộng hơn luồng huỷ | `SC-TS-003` có thể phát hiện **thêm** đường vi phạm khác ngoài huỷ nhận đơn |
| 2026-09-07 | INIT | Ghi nhận **gap tuân thủ tiềm ẩn**: `§A8` yêu cầu consent *"trước khi đăng/**ghép**"* nhưng luồng ghép chỉ có modal xác nhận lộ SĐT, không có consent điều khoản | Đối chiếu `§A8` L115 ↔ `ORD-09` + `DOC-v1.0-02` §4.2 | `SC-TS-004` ghi nhận 2 luồng; câu hỏi mới cho BA/PO (`RISK-TS-04`) |
| 2026-09-07 | SCOPE↓ | Vế *"KHÔNG có chấm sao/đánh giá"* của `§A8` L125 **không tạo SC** ở module này — đã có `SC-GIFT-011` | Trần Scenario Sufficiency Rule: duplicate | `SC-TS-005` chỉ phủ vế **"không có chặn (block) người dùng"** |
| 2026-09-07 | REFACTOR | Đổi tên thư mục module `TS/` → `TS-trust-safety/` — tên gợi nghĩa để người mới đọc thư mục là biết chức năng. Cập nhật kèm: frontmatter `id:` của 5 deliverable + `module.dir` ở file này + mọi cross-ref `TS/<file>.md` | Yêu cầu QC GiangDC2 2026-09-07 (mã 2–4 chữ không nói lên chức năng) · `Project_rule §Module Codes` nay có cột `Dir` riêng | ⛔ **Mã module `TS` và toàn bộ ID (`REQ-TS-*` · `SC-TS-*`) KHÔNG đổi** — chỉ đường dẫn thư mục đổi. TC chưa sinh nên không TC nào bị ảnh hưởng |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **`SC-TS-003` viết theo RULE (log bất biến)** — dự kiến FAIL và FAIL là kết quả đúng | `TS-02` L122 + `BR-INT-04` L80 vs live-verify: huỷ nhận đơn **XOÁ** dòng log | "Sửa expected cho PASS" = hợp thức hoá audit trail không đáng tin, và làm `TS-03` (Admin can thiệp dựa trên log) mất nền tảng |
| 2 | ⚠️ **`SC-TS-003` phải thử NHIỀU hành động** (huỷ nhận đơn · huỷ đơn · sửa tin), ⛔ không chỉ huỷ nhận đơn | Đây là điểm khác biệt so với `SC-CNL-010` (chỉ kiểm 1 hành động) — mục đích là tìm đường vi phạm khác | Bỏ sót đường làm thay đổi log khác ⇒ bug được đóng nửa vời rồi tái xuất ở luồng khác |
| 3 | ⚠️ **`SC-TS-001`/`SC-TS-002` chỉ chạy trên đơn ĐI THẲNG tới Hoàn thành** | Đơn từng bị huỷ nhận **thiếu mốc "Ghép thành công"** do bug ở `CNL` | Chẩn đoán sai: kết luận `TS` thiếu ghi mốc trong khi lỗi thuộc `CNL` |
| 4 | ⛔ **KHÔNG viết TC cho UI Admin Web Portal** | `C-TS-01` Resolved: không có đặc tả UI, out of scope v1.0 | TC cho màn không có đặc tả ⇒ không thể thiết kế bước lẫn expected |
| 5 | ⚠️ **BÁO CÁO RÕ: cột `Admin` trong permission matrix `§D4` KHÔNG được phủ** | Nhiều dòng chức năng có `Admin` = *"✓ override"*, toàn bộ ngoài phạm vi v1.0 | Stakeholder hiểu là bộ TC đã phủ hết permission matrix ⇒ đánh giá rủi ro release sai |
| 6 | ⛔ **KHÔNG nhân bản SC chấm sao** — đã có `SC-GIFT-011` | Trần Scenario Sufficiency Rule (duplicate) | 2 SC cùng nội dung ở 2 module ⇒ số liệu coverage bị đếm trùng |
| 7 | ⚠️ **`SC-TS-006` dùng chung tiền đề 4 giờ với `SC-DLV-024`** — chạy 1 lần lấy dữ liệu cho cả 2 | Cả 2 cùng phụ thuộc `BR-CNF-04` (2h nhắc + 2h admin) | Chạy 2 lần = tốn 8 giờ chờ; hoặc tệ hơn: cả 2 module đều bỏ qua vì "tốn thời gian" |
| 8 | ⚠️ **Banner cam kết ở màn "Đăng tin mới" KHÔNG tính là consent** — chỉ là thông tin tĩnh | `KB-ORD-10` mô tả banner là thành phần thông tin; consent là **checkbox bắt buộc** (`D8.1` L373) | Đánh PASS cho `SC-TS-004` vì thấy banner ⇒ bỏ qua việc luồng ghép thiếu consent |

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 **Bug log audit chưa log Jira** (log bị xoá + log huỷ thiếu actor) | Đợt cũ live-verify 2026-07-29, **chưa log bug** (`KP-05 §5`) | Chạy `SC-TS-003` **cùng lô** với `SC-CNL-010` → `/log-bug` 1 report đầy đủ 2 góc nhìn |
| 2 | 🟡 **Câu hỏi mới cho BA/PO:** rule `§A8` (*"buộc consent trước khi đăng/ghép"*) có áp cho **luồng ghép** hay chỉ luồng đăng? | `RISK-TS-04` Open — mới phát hiện 2026-09-07 | Hỏi BA/PO; nếu áp cho luồng ghép thì đây là **gap tuân thủ pháp lý**, cần escalate |
| 3 | 🟡 Tiền đề **4 giờ** cho `SC-TS-006` (dùng chung `SC-DLV-024`) | `RISK-TS-05` Open | Kế hoạch chạy riêng hoặc dev seed timestamp; ⛔ chưa chạy đủ mốc thì GHI RÕ |
| 4 | 🟡 Nhánh **Admin (permission matrix `§D4`)** không phủ được ở v1.0 | `RISK-TS-03` Pending (`C-TS-01` Resolved out-of-scope) | Nêu rõ trong `test-report`; version sau nếu Admin Portal có đặc tả → mở REQ/SC mới |
