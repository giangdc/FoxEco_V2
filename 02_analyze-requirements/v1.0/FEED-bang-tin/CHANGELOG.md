---
id: v1.0/FEED-bang-tin/changelog
title: Changelog — Module FEED
type: changelog
version: v1.0
sprint: 1
module:
  code: FEED
  dir: FEED-bang-tin
  name: Bảng tin & Chi tiết tin
doc_source:
  - id: DOC-v1.0-02
    section: "§2 · §3.3 · §3.4 · §4.2 · §7 (dòng 1, 9, 10)"
  - id: DOC-v1.0-01
    section: "§A5 (BR-CON-02) · §D1b (US-D07, US-D11) · §D7 (OPR-05, OPR-07) · §D8.1"
  - id: DOC-v1.0-06
    section: "KP-01 §4 (KB-ASN-01/02) · §10.2 (KB-VIBE-01) · KP-02 §2/§5 · KP-05 §2/§3"
id_range:
  req: REQ-FEED-001..009
  sc: "SC-FEED-001..014 (NEW)"
  cl: "C-FEED-01 (mới) + C-ASN-01/02, C-ORD-06 (tham chiếu — home ở ASN/ACT)"
  risk: RISK-FEED-01..05
status: ANALYZED
updated: 2026-09-07
---

# Changelog — Module FEED (`FEED`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-07 | INIT | Phân tích lần đầu §3.3/§3.4 — 9 REQ (`001..009`), 14 SC, 4 CL (1 mới), 5 RISK. Điểm nghiệp vụ đáng chú ý nhất: bề mặt công khai này chứa **2 vi phạm rule đã được BA xác nhận là bug** — lộ SĐT trước ghép (`BR-CON-02`) và chủ tin tự nhận đơn (`OPR-05`) | `DOC-v1.0-02` §3.3/§3.4/§7 · `DOC-v1.0-01` §A5/§D7/§D1b · `DOC-v1.0-06` KP-01/KP-02 | Dựng đủ 5 deliverable + `CHANGELOG.md` |
| 2026-09-07 | REFACTOR | **Tách module mới khỏi `ASN`.** Đợt v1.0 cũ để Bảng tin + Chi tiết tin trong `ASN` với **2 scenario** (`SC-ASN-005`, `SC-ASN-014`) trong khi bộ TC có **31 TC** (sheet `TC_06`). Lượt này fan-out **14 SC** và tách rõ ranh giới: FEED = bề mặt hiển thị, ASN = rule ghép nối | Quyết định QC GiangDC2 2026-09-07 | ID cũ `SC-ASN-014` **không carry sang**; nội dung tương ứng nay là `SC-FEED-001/002/005` |
| 2026-09-07 | INIT | Mở `C-FEED-01` — gộp 2 điểm chưa xác nhận: vị trí nút CTA (card vs chi tiết, `US-D07` vs `§3.3`) và bản đồ thật vs placeholder (`§7 dòng 10`) | Đối chiếu chéo BRD ↔ PRD ở lượt INIT | `SC-FEED-002` không assert CTA trên card; `SC-FEED-009` assert placeholder |
| 2026-09-07 | SCOPE↓ | Mở rộng phạm vi `C-ORD-06` (empty state) sang **màn Bảng tin** — màn thứ tư của cùng vấn đề | `OPR-03` ẩn tin đã ghép ⇒ bảng tin có thể rỗng dù hệ thống đang nhiều đơn | `SC-FEED-013` ghi nhận, không assert text |
| 2026-09-07 | REFACTOR | Đổi tên thư mục module `FEED/` → `FEED-bang-tin/` — tên gợi nghĩa để người mới đọc thư mục là biết chức năng. Cập nhật kèm: frontmatter `id:` của 5 deliverable + `module.dir` ở file này + mọi cross-ref `FEED/<file>.md` | Yêu cầu QC GiangDC2 2026-09-07 (mã 2–4 chữ không nói lên chức năng) · `Project_rule §Module Codes` nay có cột `Dir` riêng | ⛔ **Mã module `FEED` và toàn bộ ID (`REQ-FEED-*` · `SC-FEED-*`) KHÔNG đổi** — chỉ đường dẫn thư mục đổi. TC chưa sinh nên không TC nào bị ảnh hưởng |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **`SC-FEED-010` / `SC-FEED-011` / `SC-FEED-012` viết theo RULE, KHÔNG theo hành vi app** — dự kiến FAIL và FAIL là kết quả đúng | `C-ASN-01`/`C-ASN-02` Resolved: hành vi prototype là **bug** | "Sửa expected cho PASS" = hợp thức hoá lỗi lộ SĐT công khai và lỗi cho phép người gửi = người vận chuyển; bug sẽ không bao giờ được log |
| 2 | ⛔ **KHÔNG dùng nhãn "Tài liệu"** cho chip Loại hàng — app STG dùng **"Giấy tờ, hồ sơ"**, và trong 8 chip **không có** chip nào tên "Tài liệu" | `DOC-v1.0-06` KP-01 §10.2 `KB-VIBE-01` (VR-002 `TC_04.5` FAIL, có screenshot) | Đúng lỗi lan rộng nhất của đợt v1.0 cũ — mọi TC nhắc "Tài liệu" đều sai chữ và FAIL hàng loạt vì lý do không liên quan tới nghiệp vụ |
| 3 | ⛔ **`SC-FEED-011/012` chỉ áp cho màn Chi tiết tin (public)** — ⛔ không nhân bản sang màn Theo dõi đơn | `DOC-v1.0-06` KP-01 §4 KB-ASN-02: màn Theo dõi đơn **đã role-aware đúng** | Log bug oan cho màn đã làm đúng; và làm loãng bug thật ở màn Chi tiết tin |
| 4 | ⛔ **`SC-FEED-002` KHÔNG assert nút CTA trên card** Bảng tin | `US-D07` và `§3.3` lệch nhau về vị trí nút (`C-FEED-01(a)` Open) | TC completeness FAIL vì assert thành phần chưa xác nhận, vi phạm `§Custom Rules §10.1` |
| 5 | ⛔ **KHÔNG assert giá trị `~X km`, thời gian đăng, nội dung ảnh mặc định** | Đều là `Runtime`/không có đặc tả | TC FAIL ở mọi lượt chạy vì dữ liệu thay đổi hoặc không có oracle |
| 6 | ⚠️ **Bảng tin chỉ chứa tin NEED** — tin OFFER (tuyến Carrier) không lên bảng tin | `US-D11` §D1b L185: *"tuyến đường… không hiển thị công khai lên bảng tin"* | TC đếm/duyệt tin sẽ sai kỳ vọng; tệ hơn: bỏ sót việc verify quyền riêng tư tuyến của Carrier |
| 7 | ⚠️ **Bảng tin có thể rỗng dù hệ thống đang có nhiều đơn** — tin `MATCHED`/`IN_TRANSIT` bị ẩn theo `OPR-03`/`OPR-08` | `DOC-v1.0-01` §D7 L339/L344 | TC kết luận "app mất dữ liệu" trong khi đó là hành vi đúng |

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 **2 bug đã biết chưa log**: lộ SĐT trước ghép · chủ tin tự nhận đơn | Đợt v1.0 cũ xác nhận là bug nhưng **chưa log Jira** (`KP-05 §5`) | Chạy `SC-FEED-010`/`SC-FEED-011` rồi `/log-bug` — có nguồn rule + phán quyết BA sẵn |
| 2 | 🔴 Nhãn danh mục "Loại hàng" (`C-ORD-09`, home ở `ORD`) | Chờ BA/Dev trả lời: UI đổi tên hay tài liệu sai | Hỏi BA; tới khi đó dùng nhãn app STG |
| 3 | 🟡 `C-FEED-01(a)` — vị trí nút CTA | Chưa hỏi BA (mới mở 2026-09-07) | Vibe-test Bảng tin: xem card có nút hay không → `/analyze --update` |
| 4 | 🟡 `C-FEED-01(b)` — bản đồ thật vs placeholder | Doc tự đặt câu hỏi, chưa ai trả lời | Hỏi BA về scope v1.0; `RISK-FEED-05` giữ `Pending` |
| 5 | 🟡 Empty state Bảng tin chưa có oracle | Residual `C-ORD-06` (Open, home ở `ACT`) | Ghi nhận khi execute cùng lô với `SC-HOME-024`/`SC-ACT-014`/`SC-NTF-015`/`SC-GIFT-008` |
