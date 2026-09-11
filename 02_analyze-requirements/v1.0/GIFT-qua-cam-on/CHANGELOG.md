---
id: v1.0/GIFT-qua-cam-on/changelog
title: Changelog — Module GIFT
type: changelog
version: v1.0
sprint: 1
module:
  code: GIFT
  dir: GIFT-qua-cam-on
  name: Quà cảm ơn
doc_source:
  - id: DOC-v1.0-01
    section: "§A5 (BR-INT-06) · §A7 · §A8 (L125) · §D3 (GIFT-01, RAT-01/02) · §D4 (BR-GIFT-01) · §D6 (NTF-07) · §D1b (US-D15, US-D20)"
  - id: DOC-v1.0-02
    section: "§3.8 · §3.9 · §5.2"
  - id: DOC-v1.0-04
    section: "popup \"Đã gửi lời cảm ơn!\" · màn Quà đã nhận"
  - id: DOC-v1.0-06
    section: "KP-01 §6 (KB-GIFT-01..04) · §5.1 (ô 5·Sender) · KP-02 §3/§5 · KP-07 (hàng #7)"
id_range:
  req: REQ-GIFT-001..008
  sc: "SC-GIFT-001..012 (NEW)"
  cl: "C-GIFT-01 · C-GIFT-02 · C-GIFT-03 (mới) · C-ORD-06 (tham chiếu — home ở ACT)"
  risk: RISK-GIFT-01..05
status: ANALYZED
updated: 2026-09-07
---

# Changelog — Module GIFT (`GIFT`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-07 | INIT | Phân tích lần đầu §A7/§D3/§3.8 — 8 REQ (`001..008`), 12 SC, 4 CL (1 mới), 5 RISK. Điểm nghiệp vụ đáng chú ý nhất: **BRD mâu thuẫn 3-1 về rating** (`RAT-01/02` có chấm sao ⟷ `BR-INT-06`+`§A7`+`§A8` không) ⇒ `C-GIFT-01` chốt **quà ảo THAY CHO chấm sao** — đây là hệ quả scope lớn nhất dự án | `DOC-v1.0-01` §A5/§A7/§A8/§D3/§D4/§D6/§D1b · `DOC-v1.0-02` §3.8 · `DOC-v1.0-06` KP-01 §6 | Dựng đủ 5 deliverable + `CHANGELOG.md` |
| 2026-09-07 | INIT | Giữ lại **phát hiện ngoài tài liệu** của đợt cũ: nút `✓ Cảm ơn người vận chuyển` → `Bạn đã đánh giá` (disable) sau khi gửi quà — nguồn `QA-obs` + Figma, chưa từng có ở BRD/PRD | `DOC-v1.0-06` KP-01 §6 KB-GIFT-01 (đợt cũ đã sinh REQ riêng) | `REQ-GIFT-003` + `SC-GIFT-005`; kéo theo rule **chỉ tặng quà 1 lần/đơn** |
| 2026-09-07 | INIT | Mở `C-GIFT-03` — gộp 2 điểm chưa chốt: **text popup** sau khi gửi quà (2 nguồn 2 text) và **danh sách lịch sử nhận quà** (1 nguồn văn bản, chưa có ảnh) | Đối chiếu `US-D15`/`US-D20` ↔ PRD §3.8 ↔ `KB-GIFT-03` | `SC-GIFT-003` dùng text PRD+Figma; `SC-GIFT-007` ghi nhận lịch sử |
| 2026-09-07 | INIT | Ghi nhận rule **card đếm chỉ hiện loại `count > 0`** (không hiện dạng "0") — đây là **điều chỉnh so với hiểu ban đầu** của đợt cũ (*"luôn hiện đủ 4 loại"*) | `DOC-v1.0-06` KP-01 §6 KB-GIFT-03 (`QA-obs` 2026-07-27) | `SC-GIFT-006` assert rule count>0; `SC-GIFT-008` (empty state) là hệ quả trực tiếp |
| 2026-09-07 | REFACTOR | Đổi tên thư mục module `GIFT/` → `GIFT-qua-cam-on/` — tên gợi nghĩa để người mới đọc thư mục là biết chức năng. Cập nhật kèm: frontmatter `id:` của 5 deliverable + `module.dir` ở file này + mọi cross-ref `GIFT/<file>.md` | Yêu cầu QC GiangDC2 2026-09-07 (mã 2–4 chữ không nói lên chức năng) · `Project_rule §Module Codes` nay có cột `Dir` riêng | ⛔ **Mã module `GIFT` và toàn bộ ID (`REQ-GIFT-*` · `SC-GIFT-*`) KHÔNG đổi** — chỉ đường dẫn thư mục đổi. TC chưa sinh nên không TC nào bị ảnh hưởng |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **KHÔNG viết TC chấm sao 1–5 / nhận xét** ở bất kỳ bề mặt nào | `C-GIFT-01` Resolved: rating out of scope v1.0 (`BR-INT-06` + `§A7` + `§A8` thắng `RAT-01/02`) | TC cho tính năng không tồn tại ⇒ FAIL và không ai fix; đồng thời hiểu sai luồng #5 của Phase 1 (vốn là **quà ảo**) |
| 2 | ⚠️ **Nhãn "Bạn đã đánh giá" là nhãn của hành động TẶNG QUÀ**, ⛔ không phải bằng chứng có rating | `KB-GIFT-01` + `KB-GIFT-02` | Người đọc sau viết TC chấm sao dựa vào nhãn này ⇒ tái tạo đúng lỗi mà `C-GIFT-01` sinh ra để chặn |
| 3 | ⚠️ **Nút tặng quà chỉ dùng được 1 LẦN / đơn** (sau khi gửi thì disable) | `KB-GIFT-01`: *"disable, không gửi lại được"* | Mỗi lần test tiêu 1 đơn Hoàn thành; TC thiết kế theo kiểu "gửi lại để kiểm tra" sẽ BLOCKED |
| 4 | ⚠️ **Card đếm chỉ hiện loại `count > 0`** — loại chưa nhận **không load**, ⛔ không hiện dạng "0" | `KB-GIFT-03` (điều chỉnh so với hiểu ban đầu là luôn hiện đủ 4 loại) | TC completeness assert "đủ 4 card" ⇒ FAIL với tài khoản chỉ nhận 1–2 loại (đa số trường hợp thật) |
| 5 | ⛔ **KHÔNG assert text popup theo `US-D15`** — dùng bản PRD+Figma *"Đã gửi lời cảm ơn!"* | 2 nguồn 2 text; PRD+Figma là nguồn bề mặt (`C-GIFT-03(a)` Open) | Assert sai text ⇒ FAIL vì lý do câu chữ chưa chốt, không phải lỗi app |
| 6 | ⚠️ **"Gửi ngay không cần xác nhận" = không cần CARRIER xác nhận** — Sender vẫn phải bấm xác nhận | `US-D15` nói *"không cần bước xác nhận"* nhưng PRD §3.8 có bước *"Xác nhận →"* | Hiểu là bấm chọn quà xong gửi luôn ⇒ TC thiếu bước, FAIL ở bước không tồn tại trong kịch bản |
| 7 | ⚠️ **`SC-GIFT-010` phải dùng ĐƠN THẬT**, ⛔ không dùng item mẫu tab "Đã hoàn thành" của demo | `KB-GIFT-04` phát hiện trên item mẫu tĩnh — chính nguồn nghiêng về "giới hạn demo" | Log bug cho giới hạn của bản demo ⇒ bug bị dev đóng "not reproducible", mất uy tín báo cáo |
| 8 | ⚠️ **`SC-GIFT-007` (danh sách lịch sử) chỉ GHI NHẬN, ⛔ không assert** | Chỉ 1 nguồn văn bản `US-D20`, chưa có ảnh Figma/app (`§Custom Rules §10.1`) | Vi phạm rule quan trọng nhất của dự án; nhưng ⛔ cũng **không được im lặng bỏ qua** — nguồn yêu cầu mở CL nếu app không có |

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 Seed **nhiều đơn "Hoàn thành"** (mỗi lần test tặng quà tiêu 1 đơn) + 3 trạng thái tài khoản Carrier (0 / 2 / 4 loại quà) | `RISK-GIFT-01` Open | Chạy `GIFT` **ngay sau** `DLV` trong cùng lô để tái dùng đơn vừa hoàn tất |
| 2 | 🟡 `C-GIFT-03(a)` — text popup sau khi gửi quà (2 nguồn 2 text) | Chưa hỏi BA (mới mở 2026-09-07) | Hỏi BA; hoặc vibe-test đọc text thật → `/analyze --update` |
| 3 | 🟡 `C-GIFT-03(b)` — màn "Quà đã nhận" có danh sách lịch sử hay không | Chưa hỏi BA; nguồn yêu cầu **không im lặng bỏ qua** | **Vibe-test nhanh hơn chờ BA** — mở màn "Quà đã nhận" của tài khoản đã nhận quà |
| 4 | 🟡 `C-GIFT-02` — nút back màn "Tặng quà" nhảy sang đơn khác | Open từ 2026-07-29; nghi giới hạn demo | Chạy `SC-GIFT-010` với đơn thật; tái hiện → `/log-bug` |
| 5 | 🟡 Empty state màn "Quà đã nhận" chưa có oracle | Residual `C-ORD-06` (Open, home ở `ACT`) | Ghi nhận khi execute cùng lô 6 SC empty state |
