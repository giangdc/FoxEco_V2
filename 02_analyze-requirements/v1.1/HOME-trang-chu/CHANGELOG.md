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
  sc: "SC-HOME-025..030 (NEW — 029/030 thêm 2026-09-17) + SC-HOME-008 (MODIFIED 2026-09-17), SC-HOME-019, SC-HOME-021 (MODIFIED, giữ ID sprint 1) · SC-HOME-024, SC-HOME-010 (DEPRECATED — 010 từ 2026-09-17)"
  cl: "C-HOME-03 (Resolved qua PRD) · C-HOME-02 (Resolved qua vibe-check demo) · C-HOME-01 (Resolved — (b) qua vibe-check demo, (a) qua xác nhận trực tiếp QC) — cả 3 CL giữ ID sprint 1 (kế thừa v1.0), không mở CL mới + C-HOME-04..06 (NEW 2026-09-16)"
  risk: "RISK-HOME-06, RISK-HOME-07 (NEW) + RISK-HOME-01, RISK-HOME-04 (Status cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-17
---

# Changelog — Module HOME (`HOME`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-17 | UPDATE | **Áp câu trả lời BA sheet `HOME`.** (a) `C-HOME-05` → **Resolved**: hiện empty state `EMP-02`, không ẩn ⇒ `SC-HOME-010` **DEPRECATED** (thay bằng `SC-HOME-026`), `SC-HOME-026` bỏ rào ghi nhận; vế *"ẩn"* của `C-HOME-02` hết hiệu lực. (b) `C-HOME-06` → **Partially**: hero vai không giúp = 0 · N toàn hệ thống · realtime ⇒ `SC-HOME-008` MODIFIED + **NEW `SC-HOME-029`** (hero = 0) · **`SC-HOME-030`** (realtime); còn hỏi *"người tham gia"* + đơn Đã trả người gửi. (c) `C-HOME-04` → **Partially**: BA trả lời (a) suy từ địa chỉ mặc định (b) cả 2 điểm nhưng (d) *"tin load toàn quốc"* ⇒ mâu thuẫn với PRD `AC-11.x`/`EMP-01`/`§5.1` ⇒ hỏi vòng 2; `SC-HOME-019/025` tạm Given toàn quốc | BA trả lời `CL-hoi-BA-v1.1.xlsx` sheet `HOME` 2026-09-17 | `counts` sc 28→30 · new 4→6 · modified 2→3 · carried 21→19 · deprecated 1→2 · p3 13→14 (p2 giữ 13: −010 +030); cl_open 3→0, cl_resolved 3→4 (2 Partially) |
| 2026-09-16 | UPDATE | **Rà sâu lại theo yêu cầu QC** (module không có CL nào được hỏi BA lượt này). **Mở 3 CL mới:** `C-HOME-04` ("khu vực của người dùng" — điều kiện lọc Tin mới không được định nghĩa; BA vừa nói khu vực = địa chỉ mặc định văn bản tự do) · `C-HOME-05` (**`SC-HOME-010` ⟷ `SC-HOME-026` mâu thuẫn**: section ẩn theo `C-HOME-02` vs empty state `EMP-02`) · `C-HOME-06` (công thức số liệu hero + cộng đồng) | Rà chéo `AC-11.x`/`EMP-01..03`/`AC-26.2.01` với SC CARRIED 2026-09-16 | `counts` cl 3→6; `SC-HOME-010`/`026` hạ xuống ghi nhận; `SC-HOME-019`/`025` chưa dựng được Given |
| 2026-09-15 | UPDATE | **DELTA v1.1** — PRD chính thức (`DOC-v1.1-01`) resolve `C-HOME-03` (số tin "Tin mới" = 5, chốt sau nhiều tháng Open), đặc tả 3 empty state riêng cho Trang chủ (thay `SC-HOME-024` gộp), thêm NFR01 hiệu năng. +3 REQ mới, +4 SC mới, 2 SC MODIFIED, 1 SC DEPRECATED (`SC-HOME-024`) | `DOC-v1.1-01` §6/§8.17/§9 | `C-HOME-03` đóng; `RISK-HOME-01` Resolved; `SC-HOME-019`/`SC-HOME-021` có thể assert số cứng |
| 2026-09-15 | UPDATE | Bổ sung UI reference (`00_input/v1.1/design/`, ảnh chụp từ demo `foxeco_demo/FoxEcoQC` thay Figma đã xoá) + resolve 2 CL kế thừa từ v1.0 bằng bằng chứng app thật: `C-HOME-02` (Resolved — "Đơn của tôi" ẩn theo điều kiện có đơn, không theo vai trò, đúng phép thử `SC-HOME-012` mà v1.0 đã chỉ ra) và `C-HOME-01` (Partially Resolved — (b) tagline chốt dùng bản PRD, (a) icon mapping theo vai trò vẫn chưa chốt, cần verify STG) | Vibe-check thủ công qua Playwright trên demo, theo yêu cầu QC GiangDC2 2026-09-15 | `SC-HOME-009/010/012` có thể assert cứng; `SC-HOME-004` vẫn ghi nhận (chưa assert icon) |
| 2026-09-15 | UPDATE | **Sửa lỗi lượt trên** — QC GiangDC2 chỉ ra bằng chứng icon vai trò (3 ảnh so sánh header) lấy nhầm từ khu vực "Vai trò đang xem" (panel điều khiển demo để chọn vai trò mô phỏng), **không phải UI thật của app**. Rút lại toàn bộ nhận định về icon; `C-HOME-01(a)` quay về **Open** đúng như v1.0, không có input mới. `C-HOME-01(b)` (tagline) và `C-HOME-02` KHÔNG bị ảnh hưởng — 2 bằng chứng đó lấy từ nội dung màn hình thật bên trong khung điện thoại, vẫn giữ nguyên Resolved | QC GiangDC2 phản hồi trực tiếp 2026-09-15 | `risk_assessment.md` §C-HOME-01 sửa lại; không phát sinh thay đổi cho `scenario_map`/`traceability` vì `SC-HOME-004` vốn đã ở dạng ghi nhận, không đổi |
| 2026-09-15 | UPDATE | QC GiangDC2 xác nhận trực tiếp (không qua demo): **chỉ có 1 icon dùng chung cho cả 3 vai trò**, không phân biệt Sender/Carrier/Receiver. `C-HOME-01(a)` **Resolved** — `KP-05 §3 dòng 5` (quan sát cũ "icon khác theo vai") bị bác bỏ. `RISK-HOME-04` (v1.0) cũng đóng theo | Xác nhận trực tiếp của QC GiangDC2, không qua tài liệu/demo | `SC-HOME-004` chuyển từ dạng GAP/ghi nhận sang assert cứng "1 icon chung, không mapping theo vai" |
| 2026-09-15 | ĐÍNH CHÍNH | Frontmatter `counts.sc` = 27, bỏ sót `SC-HOME-024` (DEPRECATED) ⇒ sửa thành **28**. `Project_rule §Quy ước đếm scenario`: *"Tổng SC đếm TOÀN BỘ, GỒM CẢ DEPRECATED"*; P1/P2/P3 = 1/13/13 = 27 giữ nguyên (đúng — P chỉ đếm SC còn hiệu lực) | `health-check` 2026-09-15 G-02 | Số SC thực tế không đổi (28 dòng trên bảng). Lệch `28 ≠ 27` giữa `sc` và tổng P là **có chủ ý**, đã ghi ở router §2 |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — thư mục dùng lại qua nhiều sprint, phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | ⛔ **`SC-HOME-024` đã DEPRECATED — KHÔNG tái sử dụng ID** — thay bằng 3 SC atomic `SC-HOME-025/026/027` | Empty state Trang chủ giờ đặc tả riêng cho 3 khu vực, không còn 1 trạng thái rỗng gộp | Trace sai giữa nội dung gộp cũ (không có quote) và 3 SC atomic mới (có quote PRD) |
| 3 | ⚠️ **`RISK-HOME-06` (NFR01) chỉ giao automation/load-test** — không viết TC manual assert số đo | PRD chỉ định phương pháp đo là "Load test trước go-live" | Test tay không đo được ngưỡng p95/1.000 user → PASS giả |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"chưa chốt 1 hay 5 tin — chỉ ghi nhận, không assert số lượng"** (bản v1.0, `RISK-HOME-01`/`C-HOME-03` Open) **HẾT HIỆU LỰC kể từ v1.1 — đừng trích lại**; hiện hành là **đúng 5 tin, loại trừ MATCHED/EXPIRED/của chính mình** (`DOC-v1.1-01 §6.2 AC-11.1.01`).

⛔ Kết luận **"section 'Đơn của tôi' ẨN khi không có đơn"** (`C-HOME-02` Resolved 2026-09-15 theo demo `HOME_03`, `SC-HOME-010`) **HẾT HIỆU LỰC từ 2026-09-17** — đừng trích lại; hiện hành: **hiện empty state `EMP-02`** (`C-HOME-05`, BA). `SC-HOME-010` DEPRECATED.

⛔ **`SC-HOME-024`** ("[GAP] Empty state Trang chủ — gộp") **HẾT HIỆU LỰC kể từ v1.1**; thay bằng 3 SC atomic `SC-HOME-025` (Tin mới) / `SC-HOME-026` (Đơn của tôi) / `SC-HOME-027` (Hero & cộng đồng), mỗi SC có Source Quote riêng từ `DOC-v1.1-01 §8.17.1`.

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🟡 `RISK-HOME-06` (NFR01) cần môi trường load-test riêng, chưa có lịch | Ngoài khả năng manual/vibe-test | Lên kế hoạch cùng team automation trước go-live |
| 2 | 🟡 **`C-HOME-04` vòng 2** (khu vực: BA nói toàn quốc ⟷ PRD lọc theo khu vực) · **`C-HOME-06` vòng 2** (định nghĩa "người tham gia", đơn Đã trả người gửi) — `C-HOME-05` ✅ Resolved 2026-09-17 | BA trả lời 2026-09-17 còn mâu thuẫn/thiếu | Hỏi BA (sheet `HOME`); `C-HOME-05` ưu tiên cao. *(Nợ cũ `C-ORD-06` đã Resolved 2026-09-15 ở `ACT`, đóng dòng này)* |
| 3 | 🟡 **Demo `HOME_03` ẩn section "Đơn của tôi"** — lệch rule `C-HOME-05` | Nếu STG cũng ẩn ⇒ defect | Chạy `SC-HOME-026` trên STG; ẩn ⇒ `/log-bug` |
