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
| 2026-09-21 | VIBE-TEST | **VR-016 retest cùng ngày.** QC cấp 2 địa chỉ có toạ độ hợp lệ → `TC-FEED-009` BLOCKED → PASS (bản đồ thật). Phát hiện `location_address_catalog.xlsx` không đáng tin làm oracle (100% dòng `MISSING`) ⇒ đính chính `TC-FEED-007`: KHÔNG cùng root cause với `TC-FEED-015`, nghi do chọn nhầm data, chưa log bug. `TC-FEED-015` vẫn là bug thật độc lập | Vibe-test VR-016 retest, data QC cấp qua chat | `counts` không đổi; §3 Nợ #6 Resolved, #5 sửa lại phạm vi (chỉ còn `015`) |
| 2026-09-21 | VIBE-TEST | **Retest `TC-FEED-007` theo yêu cầu QC — account `stag_anhdc4@fpt.com`, mở tin của Giang (data hợp lệ) thay vì `FTEL SG09/SG07`.** Kết quả: PASS đủ 4/4 sub-clause, xác nhận FAIL lần 1 do chọn nhầm data. Kèm phát hiện: CTA vắng mặt chọn lọc theo tin (khớp `OPR-05`/`SC-FEED-012`), không phải bug — data hữu ích cho `TC-FEED-012` | QC yêu cầu retest qua chat + đăng nhập account `anhdc4` | `counts` không đổi; §4 Vibe Status PASS 3→4, FAIL 1→0 |
| 2026-09-21 | UPDATE | **QC review `BUG-029` (`TC-FEED-015`) — chấp nhận hành vi hiện tại của app, không phải bug.** Sửa Expected Result: bỏ "khung placeholder + 0km", thay bằng "dòng cảnh báo text lồng trong card Lộ trình" (khớp app thật). `BUG-029` rút khỏi `draft/`, không push Jira. Verdict `TC-FEED-015` đổi FAIL → PASS | QC GiangDC2 duyệt trực tiếp trong chat 2026-09-21 | `counts` không đổi (chỉ sửa Expected/Notes/Status theo `§10.5`, không đổi Title/Steps/số lượng TC); §3 Nợ #5 Resolved; §4 Vibe Status PASS 2→3, FAIL 2→1 |
| 2026-09-17 | UPDATE | **Áp câu trả lời BA `C-HOME-04` vòng 3 (home ở `HOME`) — đóng vế (c) của `C-FEED-03`.** BA: *"giữ nguyên nhé"* ⇒ `EMP-04` **giữ nguyên chữ PRD** (*"Chưa có tin nào"* + gợi ý mở rộng khu vực hoặc đăng tin) dù Bảng tin load **toàn quốc**. `SC-FEED-013` bỏ rào *"chỉ ghi nhận"* → **assert cứng** chuỗi `EMP-04` | BA trả lời vòng 3 (QC GiangDC2 chuyển lời) 2026-09-17 · home: `v1.1/HOME-trang-chu/risk_assessment.md` `C-HOME-04` | `counts` không đổi (CL home ở `HOME`); `SC-FEED-013` + `TC-FEED-013` assert đủ chuỗi empty state, hết `[GAP]` |
| 2026-09-17 | UPDATE | **Rà soát toàn bộ workbook (không chỉ mục nhắc demo) theo yêu cầu QC — đóng `C-FEED-05`.** BA: toạ độ lấy từ đúng cột lat/lng của file (đã import DB, cột `coordinate_status` bỏ qua); thiếu 1 trong 2 điểm hoặc toạ độ ngoài Việt Nam đều là **data STG sai**, không phải bug app — ưu tiên viết TC cho case đủ data, case lỗi hạ P3/optional | BA trả lời `CL-hoi-BA-v1.1.xlsx` sheet `FEED` 2026-09-17 (bỏ sót ở lượt trước) | `counts` cl_open 1→0, cl_resolved 6→7 — module FEED **HẾT điểm hỏi BA**; `SC-FEED-009` dựng được Given, `SC-FEED-015` hạ P3 |
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
| 2026-09-21 | VIBE-TEST | **VR-016 — 5 TC thuộc v1.1 (`002/007/009/013/015`), theo yêu cầu QC "chỉ test case v1.1".** Kết quả: 1 PASS (`002`) · 2 FAIL (`007`/`015`, cùng root cause — khung "Bản đồ · ~X km"/placeholder+"0km" không hiển thị khi văn phòng thiếu toạ độ, dù `C-FEED-02` đã Resolved) · 2 BLOCKED (`009` thiếu văn phòng toạ độ hợp lệ · `013` Bảng tin cộng đồng không rỗng). 10 TC carried v1.0 chưa chạy (ngoài phạm vi phiên). Chi tiết: xem §4 dưới + `08_test-runs/vibe/coverage/coverage-FEED.md` | Vibe-test VR-016 qua Appium MCP, tài khoản `stag_giangdc2@fpt.com` | `counts` không đổi; mở 2 nợ mới (#5 bug ứng viên, #6 thiếu data) — xem §3 |

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
| 5 | ~~🔴 `C-FEED-02` Resolved chốt "thiếu toạ độ ⇒ placeholder + thông báo + 0km" nhưng STG chỉ hiện dòng cảnh báo text~~ ✅ **Resolved cùng ngày (VR-016, 2026-09-21) — QC chấp nhận hành vi hiện tại là đúng, không phải bug.** `BUG-029` đã log rồi rút lại; Expected Result của `TC-FEED-015` sửa lại theo app (fragment + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`), verdict FAIL → PASS | QC GiangDC2 duyệt sau khi review `BUG-029` | Không còn nợ — `C-FEED-02` xem như **cập nhật lại theo hành vi app hiện tại**, PRD chưa đồng bộ chữ (nợ tài liệu, không phải nợ code) |
| 6 | ~~🟡 Không tìm được văn phòng có toạ độ hợp lệ~~ ✅ **Resolved cùng ngày (VR-016 retest)** — QC cấp `132 Trần Hưng Đạo, LX` / `19 ấp Phú An 1, Bình Hòa` = `FTEL An Giang Trần Hưng Đạo - Long Xuyên` / `FTEL An Giang VPGD Bình Hòa`, tạo tin xác nhận bản đồ thật render đúng ⇒ `TC-FEED-009` **PASS**. 🔑 Đồng thời phát hiện `location_address_catalog.xlsx` (`DOC-v1.1-04`) không đáng tin làm oracle (100% dòng gắn `MISSING`) | Không còn nợ | — |
| 7 | ~~⚠️ `TC-FEED-007` FAIL nghi do chọn nhầm data, chưa log bug~~ ✅ **Resolved cùng ngày (VR-016 retest account `anhdc4`)** — mở tin của Giang (data hợp lệ) → PASS đủ 4/4 sub-clause, xác nhận đúng là do data, không phải bug | Không còn nợ | — |

## 4. Vibe Status — kết quả thực thi trên STG

> ⚠️ **Vì sao ghi ở đây:** module `FEED` không có thư mục v1.1 (xem banner đầu file `03_test-cases/v1.1/fragments/TC-FEED-v1.1.md`), và router `v1.0/MEMORY.md`/`v1.1/MEMORY.md` layout `module-first v2` **chỉ có** §1 Function Register + §2 Module Summary — không có §4 Vibe Status riêng. Sổ cái verdict per-TC canonical là **`08_test-runs/vibe/coverage/coverage-FEED.md`**; mục này là bản trỏ đường, cùng quy ước với `v1.1/ASN-ghep-noi/CHANGELOG.md §4`.

**Trạng thái module sau VR-016 (2026-09-21):**

| Chỉ số | Giá trị |
|---|---|
| SCOPE_TOTAL | **15 TC** = 5 (v1.1: `002` `007` `009` `013` `015`) + 10 (CARRIED v1.0, ID không đổi) |
| ✅ PASS | **4** (`TC-FEED-002`, `TC-FEED-007` — retest account `anhdc4` + data hợp lệ, `TC-FEED-009` — retest cùng ngày, `TC-FEED-015` — Expected sửa theo app, QC chấp nhận) |
| ❌ FAIL | **0** |
| 🚫 BLOCKED | **1** (`TC-FEED-013` precondition cộng đồng không rỗng) |
| ⏳ NOT_RUN | **10** (carried v1.0, ngoài phạm vi VR-016) |
| **Có verdict cuối** | **5/15** ⇒ §8 = **PARTIAL** |

| Phiên | Ngày | TC thu verdict |
|---|---|---|
| `VR-016` | 2026-09-21 | 5 — `002` (PASS) · `007` (FAIL→PASS, retest account `anhdc4` cùng ngày) · `009` (BLOCKED→PASS retest cùng ngày) · `013` (BLOCKED) · `015` (FAIL→PASS, Expected sửa theo app cùng ngày) |

**10 TC còn nợ + lý do:**

| TC | Lý do |
|---|---|
| `001` `003` `004` `005` `006` `008` `010` `011` `012` `014` | Ngoài phạm vi VR-016 (QC chỉ định "chỉ test case thuộc v1.1") — carried nguyên trạng từ v1.0, **chưa từng vibe-test** ở bất kỳ phiên nào. `010`/`011` dự kiến FAIL theo thiết kế TC (2 bug đã biết chưa log, xem §3 Nợ #1) |

### 🟢 Retest `TC-FEED-009` cùng ngày — BLOCKED → PASS, đính chính `TC-FEED-007`

> **QC cấp 2 địa chỉ cụ thể có toạ độ hợp lệ** (`FTEL An Giang Trần Hưng Đạo - Long Xuyên` ↔ `FTEL An Giang VPGD Bình Hòa`). Tự tạo 1 tin NEED qua wizard Đăng tin bằng 2 địa chỉ này ⇒ Chi tiết tin hiện **bản đồ Google Maps thật, có vẽ tuyến cam, "17.2 km · 15 phút"** ⇒ `TC-FEED-009` **PASS**.
>
> 🔑 **Phát hiện kèm quan trọng:** `location_address_catalog.xlsx` (`DOC-v1.1-04`, nguồn của `C-FEED-05`) **KHÔNG đáng tin** để suy đoán văn phòng nào có toạ độ hợp lệ — **100% (399/399) dòng đều gắn `coordinate_status = MISSING`**, kể cả 2 địa chỉ QC vừa cấp (đều có lat/lng hợp lệ nhưng app render bản đồ thật bình thường). File này thực chất là **danh sách các dòng import lỗi/nghi vấn**, không phải "danh sách địa chỉ xấu đã xác nhận" như suy đoán trước đó — phải kiểm THẬT qua app, không tra file.
>
> ⇒ **Đính chính `TC-FEED-007`:** verdict FAIL **KHÔNG cùng root cause với `TC-FEED-015`** như ghi nhận lúc đầu. Tính năng bản đồ hoạt động đúng khi data hợp lệ, nên FAIL của `007` (dùng data `FTEL SG09`/`SG07`, tình cờ thiếu toạ độ) **nhiều khả năng chỉ là chọn nhầm test data, không phải bug**.
>
> ✅ **Xác nhận cùng ngày:** retest `TC-FEED-007` bằng account `stag_anhdc4@fpt.com` + tin của Giang (data hợp lệ) → **PASS đủ 4/4 sub-clause** (lộ trình + bản đồ thật, khung giờ, người gửi, CTA). Không phải bug — không log.
>
> 🔍 **Phát hiện kèm khi retest (theo yêu cầu QC kiểm thêm):** CTA "Tôi mang giúp được" với account `anhdc4` **vắng mặt có chọn lọc theo TỪNG TIN** — 2/3 tin không phải của `anhdc4` vẫn có CTA bình thường (tin Giang, tin của Nguyễn Tấn Vũ), chỉ 1 tin (`FTEL SG09→SG07`, người gửi Nguyễn Thị Thanh Thủy) không có. Khớp rule đã biết `OPR-05`/`SC-FEED-012`: người nhận được khai không thấy CTA. **Không phải bug** — là data thật hữu ích cho `TC-FEED-012` khi chạy (còn `⏳ NOT_RUN`).
>
> `TC-FEED-015` (precondition = văn phòng THIẾU toạ độ) ban đầu bị đánh FAIL và log `BUG-029` vì lệch `C-FEED-02` Resolved (chỉ có dòng cảnh báo text, không có khung placeholder/"0km"). **QC review `BUG-029` cùng ngày và chấp nhận hành vi hiện tại của app là đúng** ⇒ `BUG-029` rút lại, Expected Result của `TC-FEED-015` sửa lại theo app, verdict đổi **FAIL → PASS**.
>
> Chi tiết đầy đủ + ảnh: `08_test-runs/vibe/VR-016-FEED-2026-09-21/vibe-log.md`.
