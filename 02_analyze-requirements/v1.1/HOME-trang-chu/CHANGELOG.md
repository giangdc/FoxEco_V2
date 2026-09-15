---
id: v1.1/HOME-trang-chu/changelog
title: Changelog — Module HOME
type: changelog
version: v1.1
sprint: 1
module:
  code: HOME
  dir: HOME-trang-chu
  name: Trang chủ
doc_source:
  - id: DOC-v1.1-01
    section: "§6.1/§6.2 US11+AC-11.x · §8.17/§8.17.1 FR17 EMP-01..03 · §9 NFR01"
id_range:
  req: "REQ-HOME-011, REQ-HOME-012, REQ-HOME-013 (NEW)"
  sc: "SC-HOME-025..028 (NEW) + SC-HOME-019, SC-HOME-021 (MODIFIED, giữ ID sprint 1) · SC-HOME-024 (DEPRECATED)"
  cl: "C-HOME-03 (Resolved qua PRD) · C-HOME-02 (Resolved qua vibe-check demo) · C-HOME-01 (Partially Resolved qua vibe-check demo) — cả 3 giữ ID sprint 1 (kế thừa v1.0), không mở CL mới"
  risk: "RISK-HOME-06, RISK-HOME-07 (NEW) + RISK-HOME-01 (Status cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-15
---

# Changelog — Module HOME (`HOME`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-15 | UPDATE | **DELTA v1.1** — PRD chính thức (`DOC-v1.1-01`) resolve `C-HOME-03` (số tin "Tin mới" = 5, chốt sau nhiều tháng Open), đặc tả 3 empty state riêng cho Trang chủ (thay `SC-HOME-024` gộp), thêm NFR01 hiệu năng. +3 REQ mới, +4 SC mới, 2 SC MODIFIED, 1 SC DEPRECATED (`SC-HOME-024`) | `DOC-v1.1-01` §6/§8.17/§9 | `C-HOME-03` đóng; `RISK-HOME-01` Resolved; `SC-HOME-019`/`SC-HOME-021` có thể assert số cứng |
| 2026-09-15 | UPDATE | Bổ sung UI reference (`00_input/v1.1/design/`, ảnh chụp từ demo `foxeco_demo/FoxEcoQC` thay Figma đã xoá) + resolve 2 CL kế thừa từ v1.0 bằng bằng chứng app thật: `C-HOME-02` (Resolved — "Đơn của tôi" ẩn theo điều kiện có đơn, không theo vai trò, đúng phép thử `SC-HOME-012` mà v1.0 đã chỉ ra) và `C-HOME-01` (Partially Resolved — (b) tagline chốt dùng bản PRD, (a) icon mapping theo vai trò vẫn chưa chốt, cần verify STG) | Vibe-check thủ công qua Playwright trên demo, theo yêu cầu QC GiangDC2 2026-09-15 | `SC-HOME-009/010/012` có thể assert cứng; `SC-HOME-004` vẫn ghi nhận (chưa assert icon) |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — thư mục dùng lại qua nhiều sprint, phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | ⛔ **`SC-HOME-024` đã DEPRECATED — KHÔNG tái sử dụng ID** — thay bằng 3 SC atomic `SC-HOME-025/026/027` | Empty state Trang chủ giờ đặc tả riêng cho 3 khu vực, không còn 1 trạng thái rỗng gộp | Trace sai giữa nội dung gộp cũ (không có quote) và 3 SC atomic mới (có quote PRD) |
| 3 | ⚠️ **`RISK-HOME-06` (NFR01) chỉ giao automation/load-test** — không viết TC manual assert số đo | PRD chỉ định phương pháp đo là "Load test trước go-live" | Test tay không đo được ngưỡng p95/1.000 user → PASS giả |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"chưa chốt 1 hay 5 tin — chỉ ghi nhận, không assert số lượng"** (bản v1.0, `RISK-HOME-01`/`C-HOME-03` Open) **HẾT HIỆU LỰC kể từ v1.1 — đừng trích lại**; hiện hành là **đúng 5 tin, loại trừ MATCHED/EXPIRED/của chính mình** (`DOC-v1.1-01 §6.2 AC-11.1.01`).

⛔ **`SC-HOME-024`** ("[GAP] Empty state Trang chủ — gộp") **HẾT HIỆU LỰC kể từ v1.1**; thay bằng 3 SC atomic `SC-HOME-025` (Tin mới) / `SC-HOME-026` (Đơn của tôi) / `SC-HOME-027` (Hero & cộng đồng), mỗi SC có Source Quote riêng từ `DOC-v1.1-01 §8.17.1`.

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🟡 `C-HOME-01(a)` — icon vai trò header vẫn chưa chốt (chỉ có thêm ảnh làm đầu vào, chưa đủ khẳng định thiết kế đúng/sai) | Đã vibe-check qua demo 2026-09-15 (xem `risk_assessment.md`), nhưng demo lịch sử bị đánh dấu reference-only | Verify lại trên STG thật khi có dịp; nếu STG khớp demo (icon chung, không phân vai) → có thể Resolve dứt điểm, không cần hỏi BA |
| 2 | 🟡 `RISK-HOME-06` (NFR01) cần môi trường load-test riêng, chưa có lịch | Ngoài khả năng manual/vibe-test | Lên kế hoạch cùng team automation trước go-live |
| 3 | 🟡 `C-ORD-06` (empty state ngoài phạm vi Trang chủ — ACT/FEED/GIFT/NTF) vẫn Open | Các module đó chưa được rà lại ở lượt delta này | Rà lại khi delta các module đó chạm tới `FR17` |
