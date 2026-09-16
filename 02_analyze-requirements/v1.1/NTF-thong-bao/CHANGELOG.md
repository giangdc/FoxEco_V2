---
id: v1.1/NTF-thong-bao/changelog
title: Changelog — Module NTF
type: changelog
version: v1.1
sprint: 1
module:
  code: NTF
  dir: NTF-thong-bao
  name: Thông báo
doc_source:
  - id: DOC-v1.1-01
    section: "§8.13 FR13 (Thông báo) · §8.13.1 Danh mục thông báo (bảng 15 dòng, page 47-48)"
id_range:
  req: "REQ-NTF-012 (NEW) + REQ-NTF-003, REQ-NTF-005, REQ-NTF-010 (MODIFIED, giữ ID sprint 1)"
  sc: "SC-NTF-017..022 (NEW) + SC-NTF-005, SC-NTF-008, SC-NTF-014 (MODIFIED, giữ ID sprint 1)"
  cl: "C-NTF-01 (Resolved, giữ ID sprint 1 — không mở CL mới) + C-NTF-04, C-NTF-05 (NEW 2026-09-16) · C-NTF-03 → Resolved (2026-09-16)"
  risk: "RISK-NTF-07 (NEW) + RISK-NTF-01, RISK-NTF-02, RISK-NTF-04 (Status cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-16
---

# Changelog — Module NTF (`NTF`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa WARNING health-check G-03:** thay 1 trích dẫn bị chép lặp sang file khác bằng dòng trỏ `↪` về đúng home (REQ → `requirement_traceability.md` · CL → `risk_assessment.md`) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Nội dung quote không mất — chỉ còn 1 home |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa theo health-check VERSION v1.1 (G-06b CRITICAL):** các đoạn register sống còn kể lại kết luận cũ của CL vừa Resolved (`C-NTF-03` — Khuyến nghị #4) — đổi mục Khuyến nghị / heading / data catalog sang kết luận hiện hành và thêm dòng *"⛔ Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC"* sau các ghi chú gốc (giữ nguyên nội dung cũ làm hồ sơ, không xoá lặng lẽ) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Không đổi `counts`, không đổi Then SC — chỉ đồng bộ chữ với CL section |
| 2026-09-16 | UPDATE | **Áp câu trả lời BA** + rà sâu `FR13` (15 dòng danh mục ⟷ AC các module). (a) `C-NTF-03(a)` → **Resolved**: "Đánh dấu đã đọc" = **mark-all**; `SC-NTF-011` hết GAP, `SC-NTF-013` rõ bước đọc hết. (b) **Mở 2 CL mới:** `C-NTF-04` (đích điều hướng khi chạm 14/15 loại thông báo PRD không nêu — trong khi DoD #7 bắt test; chạm 1 item có đánh dấu riêng không) · `C-NTF-05` (người nhận thông báo khi Carrier huỷ nhận / giao uỷ quyền-quầy / huỷ ở POSTED) | BA trả lời 2026-09-16 · rà kỹ theo yêu cầu QC GiangDC2 | `counts` cl 2→4; `SC-NTF-011`/`013` regenerate TC |
| 2026-09-15 | UPDATE | **DELTA v1.1** — PRD chính thức (`DOC-v1.1-01`) chốt danh mục **15 sự kiện thông báo chính thức** (`NTF-01..15`, §8.13.1), resolve `C-NTF-01` (Open từ 2026-07, CL lớn nhất module) và text `NTF-06`. 6 sự kiện mới (`NTF-10..15`) gắn với nhánh xử lý giao hàng không thành công của `DLV` (FR08/FR09). +1 REQ mới, +6 SC mới, 3 SC MODIFIED (`SC-NTF-005`, `SC-NTF-008`, `SC-NTF-014`), 3 REQ MODIFIED | `DOC-v1.1-01` §8.13/§8.13.1 | `C-NTF-01` đóng; `SC-NTF-005`/`SC-NTF-014` chuyển từ ghi-nhận sang assert; `SC-NTF-008` mở rộng phạm vi |
| 2026-09-15 | UPDATE | Bổ sung UI reference (`00_input/v1.1/design/NTF_01..03`) + thử vibe-check `C-NTF-03(a)` (mark-all + tap-item) — **không resolve được**, demo không nối logic đọc/chưa đọc thật (mock tĩnh). Ghi nhận để không lặp lại hướng thử này | Vibe-check thủ công qua Playwright, theo yêu cầu QC GiangDC2 2026-09-15 | Không ảnh hưởng generate-tc; `C-NTF-03(a)` vẫn Open, cần hỏi BA/STG thật |
| 2026-09-16 | UPDATE | Tái xác nhận độc lập `C-NTF-03(a)` bằng cách thử thứ 3 (tap item với dữ liệu đơn thật, không phải item mẫu) — điều hướng route hoạt động thật nhưng **trạng thái đã đọc vẫn không đổi**, kể cả sau khi bấm mark-all. Củng cố kết luận: đây là giới hạn cài đặt của demo (không lưu trạng thái đọc), không phải câu trả lời nghiệp vụ | Vibe-check thủ công qua Playwright, theo yêu cầu QC GiangDC2 2026-09-16 | `C-NTF-03(a)` giữ nguyên Open — không còn hướng thử nào khác qua demo này, cần hỏi BA hoặc verify STG thật |
| 2026-09-15 | ĐÍNH CHÍNH | Frontmatter `counts:` module này đang dùng nghĩa **delta-only** (`req: 4` · `sc: 9` · `P 0/8/1`) trong khi 4 module delta còn lại dùng **cumulative** ⇒ sửa về cumulative: `req: 12` · `sc: 22` (CARRIED 13 + MODIFIED 3 + NEW 6) · `P1/P2/P3 = 1/15/6`. Ghi chú dưới tiêu đề cũng sai (*"= 19"* — bỏ quên 3 SC MODIFIED) ⇒ sửa thành 22 | `health-check` 2026-09-15 G-02 (cộng ngang 5 module ra 134, không phải số có nghĩa); chốt nghĩa `counts:` = cumulative ở `v1.1/MEMORY.md §Luật counts canonical` | Số SC/REQ **thực tế không đổi** — chỉ cách ghi. Router §2 đọc được; ⛔ ai đã trích `19`/`9` từ file này trước 2026-09-15 phải lấy lại |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — thư mục dùng lại qua nhiều version, phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | ⚠️ **`SC-NTF-017..022` phụ thuộc tiến độ vibe-test nhánh FR08/FR09 bên `DLV`** — không seed riêng được | Tiền đề nghiệp vụ nằm ở module khác (`RISK-NTF-07`) | Chạy riêng lẻ mà không có đơn ở đúng nhánh phụ ⇒ không quan sát được, báo BLOCKED oan |
| 3 | ✅ **`C-NTF-03` Resolved 2026-09-16 — "Đánh dấu đã đọc" là mark-all** | BA xác nhận | TC viết theo từng item ⇒ FAIL oan |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"KHÔNG assert danh mục / danh sách loại thông báo"** và **"KHÔNG assert text NTF-06"** (bản v1.0, `v1.0/NTF-thong-bao/CHANGELOG.md §2` ràng buộc #3 và #4, dựa trên `C-NTF-01` Open) **HẾT HIỆU LỰC kể từ v1.1 — đừng trích lại**; hiện hành là **assert đủ 15 loại thông báo + đúng text NTF-06** theo `DOC-v1.1-01 §8.13.1` (xem `risk_assessment.md` mục C-NTF-01).

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 `C-NTF-04` + `C-NTF-05` (mới 2026-09-16) — đích chạm thông báo + người nhận ở sự kiện mơ hồ | PRD chỉ nêu đích của `NTF-07`; `AC-25.1.02` không nói dùng thông báo nào | Hỏi BA (sheet `NTF`) trước `generate-tc` — DoD #7 bắt buộc test đích |
| 2 | 🟡 `SC-NTF-017..022` cần chạy chung lô với vibe-test `DLV` (nhánh FR08/FR09) | Chưa có lịch chạy cụ thể | Lên kế hoạch vibe-test `DLV` + `NTF` cùng lô trước generate-tc |
