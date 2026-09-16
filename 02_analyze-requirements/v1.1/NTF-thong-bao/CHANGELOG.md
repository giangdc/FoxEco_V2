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
  cl: "C-NTF-01 (Resolved, giữ ID sprint 1 — không mở CL mới)"
  risk: "RISK-NTF-07 (NEW) + RISK-NTF-01, RISK-NTF-02, RISK-NTF-04 (Status cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-16
---

# Changelog — Module NTF (`NTF`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-15 | UPDATE | **DELTA v1.1** — PRD chính thức (`DOC-v1.1-01`) chốt danh mục **15 sự kiện thông báo chính thức** (`NTF-01..15`, §8.13.1), resolve `C-NTF-01` (Open từ 2026-07, CL lớn nhất module) và text `NTF-06`. 6 sự kiện mới (`NTF-10..15`) gắn với nhánh xử lý giao hàng không thành công của `DLV` (FR08/FR09). +1 REQ mới, +6 SC mới, 3 SC MODIFIED (`SC-NTF-005`, `SC-NTF-008`, `SC-NTF-014`), 3 REQ MODIFIED | `DOC-v1.1-01` §8.13/§8.13.1 | `C-NTF-01` đóng; `SC-NTF-005`/`SC-NTF-014` chuyển từ ghi-nhận sang assert; `SC-NTF-008` mở rộng phạm vi |
| 2026-09-15 | UPDATE | Bổ sung UI reference (`00_input/v1.1/design/NTF_01..03`) + thử vibe-check `C-NTF-03(a)` (mark-all + tap-item) — **không resolve được**, demo không nối logic đọc/chưa đọc thật (mock tĩnh). Ghi nhận để không lặp lại hướng thử này | Vibe-check thủ công qua Playwright, theo yêu cầu QC GiangDC2 2026-09-15 | Không ảnh hưởng generate-tc; `C-NTF-03(a)` vẫn Open, cần hỏi BA/STG thật |
| 2026-09-16 | UPDATE | Tái xác nhận độc lập `C-NTF-03(a)` bằng cách thử thứ 3 (tap item với dữ liệu đơn thật, không phải item mẫu) — điều hướng route hoạt động thật nhưng **trạng thái đã đọc vẫn không đổi**, kể cả sau khi bấm mark-all. Củng cố kết luận: đây là giới hạn cài đặt của demo (không lưu trạng thái đọc), không phải câu trả lời nghiệp vụ | Vibe-check thủ công qua Playwright, theo yêu cầu QC GiangDC2 2026-09-16 | `C-NTF-03(a)` giữ nguyên Open — không còn hướng thử nào khác qua demo này, cần hỏi BA hoặc verify STG thật |
| 2026-09-15 | ĐÍNH CHÍNH | Frontmatter `counts:` module này đang dùng nghĩa **delta-only** (`req: 4` · `sc: 9` · `P 0/8/1`) trong khi 4 module delta còn lại dùng **cumulative** ⇒ sửa về cumulative: `req: 12` · `sc: 22` (CARRIED 13 + MODIFIED 3 + NEW 6) · `P1/P2/P3 = 1/15/6`. Ghi chú dưới tiêu đề cũng sai (*"= 19"* — bỏ quên 3 SC MODIFIED) ⇒ sửa thành 22 | `health-check` 2026-09-15 G-02 (cộng ngang 5 module ra 134, không phải số có nghĩa); chốt nghĩa `counts:` = cumulative ở `v1.1/MEMORY.md §Luật counts canonical` | Số SC/REQ **thực tế không đổi** — chỉ cách ghi. Router §2 đọc được; ⛔ ai đã trích `19`/`9` từ file này trước 2026-09-15 phải lấy lại |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — thư mục dùng lại qua nhiều version, phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | ⚠️ **`SC-NTF-017..022` phụ thuộc tiến độ vibe-test nhánh FR08/FR09 bên `DLV`** — không seed riêng được | Tiền đề nghiệp vụ nằm ở module khác (`RISK-NTF-07`) | Chạy riêng lẻ mà không có đơn ở đúng nhánh phụ ⇒ không quan sát được, báo BLOCKED oan |
| 3 | ⚠️ **`C-NTF-03` (cơ chế đánh dấu đã đọc) vẫn Open** — PRD v1.1 không đề cập | Ngoài phạm vi PRD "Gửi Hàng" | Đừng hiểu nhầm là đã resolve theo lượt delta này |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"KHÔNG assert danh mục / danh sách loại thông báo"** và **"KHÔNG assert text NTF-06"** (bản v1.0, `v1.0/NTF-thong-bao/CHANGELOG.md §2` ràng buộc #3 và #4, dựa trên `C-NTF-01` Open) **HẾT HIỆU LỰC kể từ v1.1 — đừng trích lại**; hiện hành là **assert đủ 15 loại thông báo + đúng text NTF-06** theo `DOC-v1.1-01 §8.13.1` (xem `risk_assessment.md` mục C-NTF-01).

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🟡 `C-NTF-03(a)` — cơ chế "Đánh dấu đã đọc" vẫn Open, PRD v1.1 không đề cập | Đã vibe-test cả 2 cách qua demo 2026-09-15 — **không kết luận được** (demo mock tĩnh, không đổi trạng thái đọc) | Hỏi BA trực tiếp, hoặc verify lại trên STG thật (demo không dùng được cho câu hỏi này) |
| 2 | 🟡 `SC-NTF-017..022` cần chạy chung lô với vibe-test `DLV` (nhánh FR08/FR09) | Chưa có lịch chạy cụ thể | Lên kế hoạch vibe-test `DLV` + `NTF` cùng lô trước generate-tc |
