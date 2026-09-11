---
id: v1.0/ACT-hoat-dong/changelog
title: Changelog — Module ACT
type: changelog
version: v1.0
sprint: 1
module:
  code: ACT
  dir: ACT-hoat-dong
  name: Hoạt động (Đơn của tôi)
doc_source:
  - id: DOC-v1.0-02
    section: "§2 (dòng Tab Hoạt động) · §3.7 · §4.5"
  - id: DOC-v1.0-01
    section: "§D1b (US-D04) · §D2 (L232) · §A8 (TS-01)"
  - id: DOC-v1.0-05
    section: "Screenshot màn Hoạt động (⚠ mockup Apple status bar 9:41)"
  - id: DOC-v1.0-06
    section: "KP-01 §3 (KB-ORD-07) · §6 (KB-GIFT-02) · KP-02 §5/§6"
id_range:
  req: REQ-ACT-001..009
  sc: "SC-ACT-001..014 (NEW)"
  cl: "C-ACT-01 (mới) + C-ORD-06 (home canonical ở module này)"
  risk: RISK-ACT-01..05
status: ANALYZED
updated: 2026-09-07
---

# Changelog — Module ACT (`ACT`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-07 | INIT | Phân tích lần đầu §3.7 — 9 REQ (`001..009`), 14 SC, 2 CL (1 mới), 5 RISK. Điểm nghiệp vụ đáng chú ý nhất: tab "Đã hoàn thành" chứa **cả đơn `Hết hạn`** (thất bại), và đơn **`Đã huỷ` bị ẩn khỏi cả 2 tab** dù `TS-01` yêu cầu ghi log đầy đủ | `DOC-v1.0-02` §3.7 · `DOC-v1.0-01` §D1b/§D2 · `DOC-v1.0-06` KP-01 §3 KB-ORD-07 | Dựng đủ 5 deliverable + `CHANGELOG.md` |
| 2026-09-07 | REFACTOR | **Tách module mới khỏi `ORD`.** Đợt v1.0 cũ để màn Hoạt động trong `ORD` (`SC-ORD-015..026`, 12 SC / 20 TC sheet `TC_01`). Lượt này thành module riêng với 14 SC | Quyết định QC GiangDC2 2026-09-07 | ID cũ `SC-ORD-015..026` **không carry sang**; nội dung tương ứng nay là `SC-ACT-001..014` |
| 2026-09-07 | INIT | **Nhận home canonical của `C-ORD-06`** (empty state) và **mở rộng phạm vi từ 3 màn lên 5 màn** (thêm Trang chủ + Bảng tin) | Màn Hoạt động là màn đầu trong danh sách của CL; cùng 1 câu trả lời BA đóng được 6 SC | `SC-ACT-012`/`SC-ACT-014` + `SC-HOME-024` + `SC-FEED-013` + `SC-NTF-015` + `SC-GIFT-008` |
| 2026-09-07 | INIT | Mở `C-ACT-01` — 2 nguồn nêu 2 đích khác bản chất khi tap card ("Chi tiết tin" public vs "Theo dõi đơn" role-aware) | Đối chiếu `KB-ORD-07` (#5) ↔ `DOC-v1.0-02` §3.7 | `SC-ACT-011` ghi nhận; `SC-ACT-010` assert theo dữ liệu, không theo tên màn |
| 2026-09-07 | REFACTOR | Đổi tên thư mục module `ACT/` → `ACT-hoat-dong/` — tên gợi nghĩa để người mới đọc thư mục là biết chức năng. Cập nhật kèm: frontmatter `id:` của 5 deliverable + `module.dir` ở file này + mọi cross-ref `ACT/<file>.md` | Yêu cầu QC GiangDC2 2026-09-07 (mã 2–4 chữ không nói lên chức năng) · `Project_rule §Module Codes` nay có cột `Dir` riêng | ⛔ **Mã module `ACT` và toàn bộ ID (`REQ-ACT-*` · `SC-ACT-*`) KHÔNG đổi** — chỉ đường dẫn thư mục đổi. TC chưa sinh nên không TC nào bị ảnh hưởng |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **KHÔNG gộp verify data 2 tab vào 1 TC "chuyển tab qua lại"** — mỗi tab ≥1 SC/TC riêng, SC switch tab giữ độc lập | `Project_rule §Custom Rules §10.2` — **case gốc của rule này chính là màn Hoạt động** | FAIL không chỉ ra được tab nào lọc sai data; đợt cũ đã phải tách lại từ 1 TC gộp |
| 2 | ⚠️ **Tab "Đã hoàn thành" chứa CẢ đơn `Hết hạn`**, không chỉ đơn thành công | 2 nguồn đồng thuận (`DOC-v1.0-02` §3.7 + `US-D04` L166) | TC viết theo trực giác tên tab sẽ assert thiếu nhóm `Hết hạn` ⇒ bỏ sót nhánh đơn thất bại |
| 3 | ⚠️ **`SC-ACT-004`/`SC-ACT-005` phải có tiền đề CÓ CẢ 2 NHÓM dữ liệu** (đang hoạt động + đã kết thúc) | Chỉ có 1 nhóm thì TC PASS cả khi app không lọc gì | Lỗi lọc tab lọt qua hoàn toàn — đúng loại lỗi mà tách SC theo tab sinh ra để bắt |
| 4 | ⛔ **KHÔNG assert giá trị dữ liệu trong ảnh `DOC-v1.0-05`** — chỉ đối chiếu cấu trúc | Ảnh có status bar **"9:41"** = mockup chuẩn Apple, **không phải screenshot máy thật** (`KP-01` §3 ghi rõ) | TC assert dữ liệu mockup ⇒ FAIL vĩnh viễn trên mọi tài khoản thật |
| 5 | ⛔ **KHÔNG assert số sao / cơ chế đánh giá** từ chuỗi `★★★★★ Đã đánh giá` trên card Hoàn thành | `C-GIFT-01` Resolved: rating 1–5 sao là phase sau; chuỗi này là **UI leftover** | Viết TC chấm sao cho tính năng không tồn tại ⇒ FAIL và không ai fix |
| 6 | ⛔ **KHÔNG assert text empty state** cho tới khi `C-ORD-06` có bằng chứng | CL từng bị **revert `Resolved → Open`** vì chốt theo mô tả chat không kèm nguồn (`KP-02 §6`) | Tái diễn đúng sai sót đã xảy ra: TC assert text bịa, FAIL rồi phải sửa lại toàn bộ |
| 7 | ⚠️ **`SC-ACT-010` assert "mở đúng đơn", ⛔ KHÔNG assert tên màn đích** | `C-ACT-01` Open — 2 nguồn 2 màn khác bản chất | Chọn sai tên màn ⇒ TC FAIL vì lý do chưa được chốt, không phải vì app sai |
| 8 | ⚠️ **6/9 REQ chỉ có 1 nguồn `QA-obs` (2026-07) + ảnh mockup** ⇒ vibe-test xác nhận lại `KB-ORD-07` trước khi coi là đã chốt | `§Custom Rules §10.1` yêu cầu 2 nguồn khớp mới viết TC khẳng định | Nếu quan sát cũ lệch thì cả nhóm TC completeness của module sai theo mà không ai phát hiện |

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 `C-ORD-06` — text empty state (5 màn, 6 SC) | Kế thừa; từng Resolved rồi **revert** 2026-07-29; BA chưa bổ sung text | Hỏi BA 1 lượt cho cả 5 màn; hoặc vibe-test chụp ảnh empty state thật → `/analyze --update` |
| 2 | 🔴 **Vibe-test xác nhận lại `KB-ORD-07`** (7 dòng rule của màn Hoạt động) | `RISK-ACT-01` Open — 6/9 REQ dựa vào 1 lượt quan sát 2026-07-27 | `/vibe-test` màn Hoạt động **trước** generate-tc; kết quả về qua `/analyze --update` |
| 3 | 🟡 `C-ACT-01` — đích tap card ("Chi tiết tin" vs "Theo dõi đơn") | Chưa hỏi BA (mới mở 2026-09-07) | Vibe-test tap card đơn của chính mình — đồng thời kiểm chéo bug `SC-FEED-011` |
| 4 | 🟡 Seed **đơn `Hết hạn`** + **tài khoản trắng** cho 6 SC | `RISK-ACT-03` Open; đơn Hết hạn ⛔ không seed được qua UI | Nhờ dev/QA seed trên STG cùng lô với `SC-ORD-045` |
| 5 | 🟡 Đơn `Đã huỷ` bị ẩn khỏi cả 2 tab trong khi `TS-01` yêu cầu log đầy đủ ⇒ **không có bề mặt cho user xem lại đơn đã huỷ** | Ghi nhận, chưa phải CL (chưa rõ có phải thiếu sót thiết kế) | Nêu với BA cùng lượt `C-CNL-02`; nếu là thiếu sót → mở CL mới ở `CNL` |
