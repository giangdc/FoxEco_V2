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
  sc: "SC-FEED-001..015 (NEW — 015 thêm 2026-09-17)"
  cl: "C-FEED-01 (mới, → Partially 2026-09-16 → Resolved 2026-09-16 theo BA) + C-FEED-02..04 (NEW 2026-09-16 → Resolved 2026-09-17) + C-FEED-05 (NEW 2026-09-17) + C-ASN-01/02, C-ORD-06 (tham chiếu — home ở ASN/ACT)"
  risk: RISK-FEED-01..05
status: ANALYZED
updated: 2026-09-17
---

# Changelog — Module FEED (`FEED`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-17 | UPDATE | **Áp câu trả lời BA sheet `FEED`.** (a) `C-FEED-02` → **Resolved**: thiếu toạ độ ⇒ placeholder + thông báo, "0km"; km tính điểm nhận → điểm giao; bản đồ = **ảnh tĩnh có vẽ tuyến** ⇒ `SC-FEED-009` sửa Then + **NEW `SC-FEED-015`** (P3, BA cho bỏ TC). (b) `C-FEED-03` → **Resolved**: 1 danh sách, không tab, không lọc/tìm kiếm ⇒ `SC-FEED-013` bỏ *"cả hai tab"*; §10.2 không áp. (c) `C-FEED-04` → **Resolved**: trước ghép **chỉ ẩn SĐT**, tên + địa chỉ đầy đủ hiện ⇒ `SC-FEED-007` thêm assert tên. (d) **Mở `C-FEED-05`**: file toạ độ 399/399 `MISSING`, 61 thiếu lat/lng, 34 ngoài VN. (e) Đề nghị BA cập nhật PRD (`EMP-04` · `§7.1` · `AC-12.1.01` · `AC-20.1.01` · `BR03-03` · `NFR-10`) | BA trả lời `CL-hoi-BA-v1.1.xlsx` 2026-09-17 · rà `DOC-v1.1-04` | `counts` sc 14→15 · new 14→15 · p3 6→7; cl 6→7 · open 3→1 · resolved 3→6. Sửa tại chỗ (giữ lifecycle `NEW`) — cần regenerate TC `SC-FEED-007/009/013/015` |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa WARNING health-check G-06b:** router `v1.1/MEMORY.md` + `MASTER-MEMORY §3/§4` bỏ nhận định *"FEED không có delta, PRD không đụng bề mặt Bảng tin"* — thay bằng *"không có thư mục v1.1, thay đổi sửa tại chỗ ở v1.0"*; `SC-FEED-009`/`013` đưa vào phạm vi test lại. Ảnh `FEED_01/02` nay có DOC-ID `DOC-v1.1-03` | `/health-check` 2026-09-16 | Regression scope FEED: 12 carried + 2 phải test lại |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa theo health-check VERSION v1.1 (G-06b CRITICAL):** các đoạn register sống còn kể lại kết luận cũ của CL vừa Resolved (`C-ORD-09` · `C-FEED-01(b)` — `test_data_catalog` dòng Loại hàng + ~X km + ghi chú chung, `RISK-FEED-03` → Resolved, Khuyến nghị #1/#5, heading + ghi chú `REQ-FEED-005`) — đổi mục Khuyến nghị / heading / data catalog sang kết luận hiện hành và thêm dòng *"⛔ Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC"* sau các ghi chú gốc (giữ nguyên nội dung cũ làm hồ sơ, không xoá lặng lẽ) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Không đổi `counts`, không đổi Then SC — chỉ đồng bộ chữ với CL section |
| 2026-09-16 | UPDATE | **Áp câu trả lời BA** + rà `DOC-v1.1-01` phần chạm bề mặt Bảng tin. (a) `C-FEED-01` → **Resolved cả 2 vế**: CTA chỉ ở Chi tiết tin; **có bản đồ thật** (văn phòng thiếu location thì không hiện) ⇒ `SC-FEED-009` **đảo** từ *placeholder tĩnh* sang *bản đồ thật*; `RISK-FEED-05` Resolved. (b) `SC-FEED-013` hết GAP theo `EMP-04` (`C-ORD-06` đã Resolved ở `ACT` 2026-09-15 — dòng CL tham chiếu cập nhật). (c) **Mở 3 CL mới:** `C-FEED-02` (UI khi thiếu location + "~X km") · `C-FEED-03` (2 tab + lọc/tìm kiếm của Bảng tin) · `C-FEED-04` (tên/địa chỉ hiển thị trước ghép — `AC-13.1.02` ⟷ `NFR-10`) | BA trả lời 2026-09-16 · rà kỹ theo yêu cầu QC GiangDC2 | `counts` cl 3→6; `SC-FEED-009`/`013` sửa Then tại chỗ, **giữ lifecycle `NEW`** của v1.0 để `counts` không lệch — cần **regenerate TC** |
| 2026-09-07 | INIT | Phân tích lần đầu §3.3/§3.4 — 9 REQ (`001..009`), 14 SC, 4 CL (1 mới), 5 RISK. Điểm nghiệp vụ đáng chú ý nhất: bề mặt công khai này chứa **2 vi phạm rule đã được BA xác nhận là bug** — lộ SĐT trước ghép (`BR-CON-02`) và chủ tin tự nhận đơn (`OPR-05`) | `DOC-v1.0-02` §3.3/§3.4/§7 · `DOC-v1.0-01` §A5/§D7/§D1b · `DOC-v1.0-06` KP-01/KP-02 | Dựng đủ 5 deliverable + `CHANGELOG.md` |
| 2026-09-07 | REFACTOR | **Tách module mới khỏi `ASN`.** Đợt v1.0 cũ để Bảng tin + Chi tiết tin trong `ASN` với **2 scenario** (`SC-ASN-005`, `SC-ASN-014`) trong khi bộ TC có **31 TC** (sheet `TC_06`). Lượt này fan-out **14 SC** và tách rõ ranh giới: FEED = bề mặt hiển thị, ASN = rule ghép nối | Quyết định QC GiangDC2 2026-09-07 | ID cũ `SC-ASN-014` **không carry sang**; nội dung tương ứng nay là `SC-FEED-001/002/005` |
| 2026-09-07 | INIT | Mở `C-FEED-01` — gộp 2 điểm chưa xác nhận: vị trí nút CTA (card vs chi tiết, `US-D07` vs `§3.3`) và bản đồ thật vs placeholder (`§7 dòng 10`) | Đối chiếu chéo BRD ↔ PRD ở lượt INIT | `SC-FEED-002` không assert CTA trên card; `SC-FEED-009` assert placeholder |
| 2026-09-07 | SCOPE↓ | Mở rộng phạm vi `C-ORD-06` (empty state) sang **màn Bảng tin** — màn thứ tư của cùng vấn đề | `OPR-03` ẩn tin đã ghép ⇒ bảng tin có thể rỗng dù hệ thống đang nhiều đơn | `SC-FEED-013` ghi nhận, không assert text |
| 2026-09-07 | REFACTOR | Đổi tên thư mục module `FEED/` → `FEED-bang-tin/` — tên gợi nghĩa để người mới đọc thư mục là biết chức năng. Cập nhật kèm: frontmatter `id:` của 5 deliverable + `module.dir` ở file này + mọi cross-ref `FEED/<file>.md` | Yêu cầu QC GiangDC2 2026-09-07 (mã 2–4 chữ không nói lên chức năng) · `Project_rule §Module Codes` nay có cột `Dir` riêng | ⛔ **Mã module `FEED` và toàn bộ ID (`REQ-FEED-*` · `SC-FEED-*`) KHÔNG đổi** — chỉ đường dẫn thư mục đổi. TC chưa sinh nên không TC nào bị ảnh hưởng |
| 2026-09-16 | UPDATE | Vibe-check qua demo (`https://giangdc.github.io/foxeco_demo/FoxEcoQC`, vai Carrier, Playwright) — **đóng vế (a) của `C-FEED-01`**: card ở Bảng tin xác nhận **không có** nút CTA "Tôi mang giúp được", nút chỉ có ở màn Chi tiết tin (2 ảnh đối chứng `00_input/v1.1/design/FEED_01/02...png`). `RISK-FEED-04` đóng theo. **Vế (b)** (bản đồ thật hay placeholder) vẫn ghi nhận hiện trạng demo là placeholder tĩnh, nhưng đây là câu hỏi scope sản phẩm — demo không trả lời được, giữ nguyên `Pending`, chưa hỏi BA | Vibe-check thủ công qua Playwright, theo yêu cầu QC GiangDC2 2026-09-16 | `SC-FEED-002` hết gap, đổi từ "cố ý không assert CTA" sang assert cứng "card KHÔNG có CTA"; `C-FEED-01` chuyển Open → Partially Resolved |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **`SC-FEED-010` / `SC-FEED-011` / `SC-FEED-012` viết theo RULE, KHÔNG theo hành vi app** — dự kiến FAIL và FAIL là kết quả đúng | `C-ASN-01`/`C-ASN-02` Resolved: hành vi prototype là **bug** | "Sửa expected cho PASS" = hợp thức hoá lỗi lộ SĐT công khai và lỗi cho phép người gửi = người vận chuyển; bug sẽ không bao giờ được log |
| 2 | ~~⛔ KHÔNG dùng nhãn "Tài liệu" cho chip Loại hàng~~ — **HẾT HIỆU LỰC 2026-09-16** | `C-ORD-09` Resolved (home `ORD`): nhãn chuẩn là **"Tài liệu"** | Né nhãn đúng ⇒ TC sai |
| 3 | ⛔ **`SC-FEED-011/012` chỉ áp cho màn Chi tiết tin (public)** — ⛔ không nhân bản sang màn Theo dõi đơn | `DOC-v1.0-06` KP-01 §4 KB-ASN-02: màn Theo dõi đơn **đã role-aware đúng** | Log bug oan cho màn đã làm đúng; và làm loãng bug thật ở màn Chi tiết tin |
| 4 | ✅ **`SC-FEED-002` giờ assert cứng "card KHÔNG có CTA"** — không còn né tránh như trước | `C-FEED-01(a)` Resolved 2026-09-16 qua demo (vị trí nút = màn Chi tiết tin) | Nếu app STG có CTA trên card thì đây là lệch UI cần log, không phải TC sai |
| 5 | ⛔ **KHÔNG assert giá trị `~X km`, thời gian đăng, nội dung ảnh mặc định** — *ngoại lệ 2026-09-17:* nhánh thiếu toạ độ assert **"0km"** (`SC-FEED-015`) | Đều là `Runtime`/không có đặc tả | TC FAIL ở mọi lượt chạy vì dữ liệu thay đổi hoặc không có oracle |
| 6 | ⚠️ **Bảng tin chỉ chứa tin NEED** — tin OFFER (tuyến Carrier) không lên bảng tin | `US-D11` §D1b L185: *"tuyến đường… không hiển thị công khai lên bảng tin"* | TC đếm/duyệt tin sẽ sai kỳ vọng; tệ hơn: bỏ sót việc verify quyền riêng tư tuyến của Carrier |
| 7 | ⚠️ **Bảng tin có thể rỗng dù hệ thống đang có nhiều đơn** — tin `MATCHED`/`IN_TRANSIT` bị ẩn theo `OPR-03`/`OPR-08` | `DOC-v1.0-01` §D7 L339/L344 | TC kết luận "app mất dữ liệu" trong khi đó là hành vi đúng |
| 8 | ⛔ **KHÔNG log bug vì tên người gửi / địa chỉ đầy đủ hiện trước ghép** — chỉ SĐT + nút Gọi bị cấm | `C-FEED-04` Resolved 2026-09-17 (BA); PRD `BR03-03`/`NFR-10` chưa cập nhật | Bug giả theo PRD cũ |

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 **2 bug đã biết chưa log**: lộ SĐT trước ghép · chủ tin tự nhận đơn | Đợt v1.0 cũ xác nhận là bug nhưng **chưa log Jira** (`KP-05 §5`) | Chạy `SC-FEED-010`/`SC-FEED-011` rồi `/log-bug` — có nguồn rule + phán quyết BA sẵn |
| 2 | ✅ Nhãn danh mục "Loại hàng" (`C-ORD-09`, home ở `ORD`) — **Resolved 2026-09-16: "Tài liệu"** | BA chốt | Không còn nợ |
| 3 | ~~`C-FEED-02..04`~~ ✅ Resolved 2026-09-17 · 🔴 **còn `C-FEED-05`** (toạ độ văn phòng lỗi — chặn Given `SC-FEED-009`) + đề nghị BA cập nhật PRD | BA cấp data khi test; PRD không đặc tả 2 tab/lọc và phạm vi thông tin trước ghép | Hỏi BA (sheet `FEED`). ⚠️ **Module được khai "không delta v1.1" nhưng PRD có chạm** (`AC-12.1.01`, `AC-13.1.02`, `EMP-04`, `BR18-04`, `BR01-01`) — cân nhắc dựng `v1.1/FEED-bang-tin/` ở lượt delta sau; lượt này sửa tại chỗ theo tiền lệ 2026-09-16 (giữ lifecycle `NEW`) |
| 4 | 🟡 Empty state Bảng tin — text đã chốt ở v1.1 (`C-ORD-06` Resolved, home nay ở `ACT-hoat-dong`) | Bản v1.0 này chưa cập nhật theo; `EMP-04` (Bảng tin) chưa gán TC cụ thể | Xem `v1.1/ACT-hoat-dong/risk_assessment.md` §Clarifications khi cập nhật `SC-FEED-013` |
