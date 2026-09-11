---
id: v1.0/USR-tai-khoan/changelog
title: Changelog — Module USR
type: changelog
version: v1.0
sprint: 1
module:
  code: USR
  dir: USR-tai-khoan
  name: Tài khoản & Hồ sơ
doc_source:
  - id: DOC-v1.0-01
    section: "§A6 · §A7 · §D1b (US-D20)"
  - id: DOC-v1.0-02
    section: "§1.1 · §3.9"
  - id: DOC-v1.0-04
    section: "2 ảnh màn Cá nhân (570ad9d3… · e5764b10…)"
  - id: DOC-v1.0-06
    section: "KP-01 §2 (KB-USR-01..04) · KP-02 §2/§3"
id_range:
  req: REQ-USR-001..007
  sc: "SC-USR-001..012 (NEW)"
  cl: C-USR-01..04
  risk: RISK-USR-01..05
status: ANALYZED
updated: 2026-09-07
---

# Changelog — Module USR (`USR`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt `--init`/`--sweep`/`--update`/`--delta` chạm module này ghi **1 dòng ở §1**.
> ⛔ KHÔNG nối banner *"Cập nhật lần cuối"* vào đầu các deliverable khác.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-07 | INIT | Phân tích lần đầu §A6/§A7/§3.9 — 7 REQ (`001..007`), 12 SC, 4 CL, 5 RISK. Điểm nghiệp vụ đáng chú ý nhất: màn Cá nhân **view-only hoàn toàn** dù `USR-02` ghi *"Xem/cập nhật"*, và BRD↔PRD lệch **2 vs 3 chỉ số** (BRD thắng — tier/điểm/CO₂ deferred) | `DOC-v1.0-01` §A6/§A7 · `DOC-v1.0-02` §3.9 · `DOC-v1.0-04` · `DOC-v1.0-06` KP-01/KP-02 | Dựng đủ 5 deliverable + `CHANGELOG.md` |
| 2026-09-07 | INIT | Mở CL mới `C-USR-04` — gộp 2 điểm chưa xác nhận của bề mặt màn Cá nhân (nhãn menu thứ hai · 3 trường hồ sơ không có bằng chứng UI) | Phát hiện khi đối chiếu 3 nguồn ở lượt INIT này | `SC-USR-002` chỉ assert 4 trường; `SC-USR-012` ghi nhận nhãn menu |
| 2026-09-07 | REFACTOR | Đổi tên thư mục module `USR/` → `USR-tai-khoan/` — tên gợi nghĩa để người mới đọc thư mục là biết chức năng. Cập nhật kèm: frontmatter `id:` của 5 deliverable + `module.dir` ở file này + mọi cross-ref `USR/<file>.md` | Yêu cầu QC GiangDC2 2026-09-07 (mã 2–4 chữ không nói lên chức năng) · `Project_rule §Module Codes` nay có cột `Dir` riêng | ⛔ **Mã module `USR` và toàn bộ ID (`REQ-USR-*` · `SC-USR-*`) KHÔNG đổi** — chỉ đường dẫn thư mục đổi. TC chưa sinh nên không TC nào bị ảnh hưởng |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **KHÔNG viết TC luồng sửa/cập nhật hồ sơ** — màn Cá nhân view-only | `C-USR-03` Resolved 2026-07-24 (QA kiểm app STG) | TC sẽ FAIL 100% ở bước tìm nút Sửa và bị đọc là bug của app, trong khi thực tế là TC sai nguồn |
| 2 | ⛔ **KHÔNG assert Điểm ECO / Điểm uy tín / CO₂** ở bất kỳ màn nào | `C-USR-01` Resolved — deferred phase sau | TC assert 3 chỉ số theo PRD demo sẽ FAIL; đợt v1.0 cũ đã mắc đúng lỗi này |
| 3 | ⛔ **KHÔNG assert logic đổi hạng thành viên** — badge chỉ là text tĩnh | Figma có badge nhưng BA xác nhận không có cơ chế tier ở v1.0 | TC "đủ N đơn thì lên hạng" không có cách nào PASS, và không có ai fix vì đó không phải bug |
| 4 | ⚠️ **`SC-USR-002` chỉ assert 4 trường** (avatar · tên · phòng ban · MNV) — ⛔ không mở rộng thành "đủ 6 trường" theo `USR-02` | 3 trường còn lại (SĐT · khu vực/văn phòng · kênh liên hệ) chưa có bằng chứng UI; `C-USR-04(b)` Open | TC completeness FAIL ở 3 trường không tồn tại ⇒ log bug oan, mất uy tín bộ TC |
| 5 | ⚠️ **Chỉ số đóng góp verify bằng DELTA +1**, ⛔ không assert số tuyệt đối | `Runtime` data, không seed được (`RISK-USR-03`) | TC hardcode "12 đơn" FAIL ngay lượt chạy thứ hai vì số đã tăng |
| 6 | ⚠️ **`SC-USR-011` completeness đối chiếu CẤU TRÚC, không đối chiếu GIÁ TRỊ** ảnh Figma | Số `12`/`8` trong ảnh là dữ liệu mẫu mockup (status bar "9:41" — mẫu Apple, không phải máy thật) | Assert giá trị mockup = TC FAIL vĩnh viễn trên mọi tài khoản thật |

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🟡 `C-USR-04(a)` — nhãn mục menu thứ hai (*"Quà đã nhận"* vs *"Đánh giá đã nhận"*) | Chưa hỏi BA ở lượt này (mới phát hiện 2026-09-07) | Hỏi BA; hoặc vibe-test màn Cá nhân đọc nhãn thật rồi `/analyze --update` |
| 2 | 🟡 `C-USR-04(b)` — 3 trường hồ sơ chưa có bằng chứng UI | Chưa hỏi BA | Vibe-test màn Cá nhân trước generate-tc; kết quả về `SC-USR-002` qua `/analyze --update` |
| 3 | 🟡 Empty state / hồ sơ thiếu field (avatar · phòng ban · chỉ số = 0) chưa có oracle | Residual của `C-ORD-06` (Open, thuộc `ACT`) | Ghi nhận khi execute; TC viết dạng ghi nhận, không assert text |
