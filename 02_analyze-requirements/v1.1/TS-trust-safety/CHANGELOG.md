---
id: v1.1/TS-trust-safety/changelog
title: Changelog — Module TS
type: changelog
version: v1.1
sprint: 1
module:
  code: TS
  dir: TS-trust-safety
  name: Trust & Safety
doc_source:
  - id: DOC-v1.1-01
    section: "§8.16 FR16 (Báo cáo sự cố & hỗ trợ) · §8.16.1 BR16-01..06 · §8.16.2 UI/Field Spec · §6.1 US31 · §6.2 AC-31.1.01/.02/AC-31.2.01"
id_range:
  req: "REQ-TS-006 (NEW)"
  sc: "SC-TS-008..015 (NEW)"
  cl: "(không mở CL mới) + C-TS-02, C-TS-03 (NEW 2026-09-16) + C-TS-04 (NEW 2026-09-24)"
  risk: "RISK-TS-06, RISK-TS-07 (NEW)"
status: ANALYZED
updated: 2026-09-24
---

# Changelog — Module TS (`TS`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-24 | UPDATE | **QC chốt lại lần 2 hành vi mất mạng theo app hiện tại (VR-029).** App nay tự vẽ màn lỗi "Không tải được trang" + nút "Thử lại" (đúng `AC-31.2.01` gốc), khác trang lỗi Chromium lúc VR-019 ⇒ sửa Then `SC-TS-012`, Expected `TC-TS-016` (→ Pass theo evidence VR-029). Kết luận "mất mạng hiện trang lỗi mặc định WebView" (bản sáng cùng ngày) HẾT HIỆU LỰC | QC GiangDC2 trong chat sau VR-029 | `TC-TS-017` vẫn DESCOPED — đề xuất khôi phục (recon: Thử lại giữ đúng mã đơn) |
| 2026-09-24 | UPDATE | **QC chốt 2 câu con của `C-TS-04` → Resolved.** (1) Chỉ bỏ vế mất mạng của `BR16-04`: mất mạng hiện trang lỗi mặc định WebView (như hiện tại) ⇒ `SC-TS-012` **HUỶ DEPRECATED**, quay lại NEW với Then mới; `TC-TS-016` bỏ DESCOPED, Expected = trang lỗi mặc định; `TC-TS-017` giữ DESCOPED. Vế đóng WebView giữ ⇒ `TC-TS-018` không đổi. (2) Popup đăng nhập Microsoft (`FE-321`) hiện mỗi lần phải đăng nhập | QC GiangDC2 trả lời trong chat 2026-09-24 | `counts` new 7→8 · deprecated 1→0 · p2 4→5 · cl_resolved 3→4 |
| 2026-09-24 | UPDATE | **Áp quyết định BA trên Jira cho 6 bug TS (`FE-321..326`)** sau khi sync Jira (4 bug `FE-322/323/324/326` → Done / Won't Fix). Mở `C-TS-04` (Partially). `SC-TS-012` → **DEPRECATED** (BA bỏ `BR16-04` vế mất mạng + `AC-31.2.01`). Sửa Then: `SC-TS-008` (màn xác nhận mặc định Microsoft Forms) · `SC-TS-009` (bỏ nhánh SĐT sai định dạng; nút Gửi không disable mà báo lỗi inline) · `SC-TS-014` (kể cả ô mã đơn cũng sửa được). Đảo `C-TS-03(b)(c)(d)` | Comment BA LinhDCC trên `FE-321..326` 2026-09-24 (đọc qua Atlassian MCP) | `counts` new 8→7 · deprecated 0→1 · p2 5→4 · cl 3→4. TC (freeze §10.5, không đổi số lượng): sửa Expected `TC-TS-009/012/021` · Steps `TC-TS-012/020` · `TC-TS-016/017` → DESCOPED + Skipped |
| 2026-09-17 | UPDATE | **Áp câu trả lời Dev vòng 3 (rà lại `CL-hoi-BA-v1.1.xlsx` theo yêu cầu QC — phát hiện câu trả lời mới chưa đóng sổ).** `C-TS-03` câu (c) duy nhất còn treo: Dev trả lời "App hiển thị nhé" — nút "Thử lại" khi mất mạng do CHÍNH APP vẽ/điều khiển, không phải nội dung WebView/Custom Tabs tự sinh. Không cần xác nhận thêm công nghệ nhúng cụ thể. `C-TS-03` ĐÓNG HẲN | Dev trả lời `CL-hoi-BA-v1.1.xlsx` sheet `TS` dòng "(vòng 3)" 2026-09-17 (bỏ sót ở lượt trước — chỉ đọc cột Ghi chú, chưa đọc cột Câu trả lời BA thô) | `counts` cl_resolved 2→3; module TS **HẾT điểm hỏi BA/Dev**; `SC-TS-012` assert được ai hiển thị nút "Thử lại" |
| 2026-09-17 | UPDATE | **Áp câu trả lời BA + vibe-check demo (Playwright MCP, đi lần lượt các mục BA yêu cầu "vào demo xem").** `C-TS-02` → **Resolved**: nút "Báo cáo sự cố" xác nhận hiện ở MỌI trạng thái/vai (Chờ ghép/Đã ghép/Đang giao × Sender/Carrier); gửi form KHÔNG đổi trạng thái đơn (verify bằng thao tác thật, không chỉ theo lời BA) ⇒ INCIDENT chỉ vào được qua xử lý tay Dev, khớp `C-CNL-03`. `C-TS-03` → **Partially Resolved**: (a) chỉ mã đơn (b) mã đơn chỉ đọc (d) nút "Quay lại đơn hàng" do APP hiển thị — cả 3 xác nhận qua demo; còn (c) công nghệ nhúng thật (WebView vs Custom Tabs) — ảnh `TS_02` cho thấy chrome kiểu Custom Tabs (✕ + thanh địa chỉ) nhưng chưa chắc chắn, cần Dev xác nhận | BA trả lời `CL-hoi-BA-v1.1.xlsx` sheet `TS` 2026-09-17 · vibe-check demo QA GiangDC2 2026-09-17 (Playwright MCP, tái xác nhận + mở rộng vibe-check 2026-09-15 đã có ở `00_input/v1.1/design/TS_01..05`) | `counts` cl_open 2→0, cl_resolved 1→2; `SC-CNL-015`/`SC-DLV-034` xác nhận out of scope qua UI; `C-TS-03` câu (c) đặt câu hỏi thẳng cho Dev |
| 2026-09-16 | ĐÍNH CHÍNH | **Rà sâu lại `FR16` theo yêu cầu QC** — nhận định lượt delta *"FR16 đặc tả đầy đủ, không có vùng mơ hồ cần hỏi BA"* **chưa đúng**. **Mở 2 CL:** `C-TS-02` (nút Báo cáo sự cố hiện ở trạng thái nào — `AC-31.1.01` ⟷ `§8.12.3`; gửi form có tự chuyển INCIDENT không — BA `C-CNL-03` nói dev xử lý tay) · `C-TS-03` (prefill 1 trường `BR16-02` ⟷ 9 trường `AC-31.1.01`; mã đơn chỉ đọc `§8.16.2` ⟷ sửa được `BR16-03`; Custom Tabs không vẽ được nút "Thử lại"/"Quay lại đơn hàng") | Rà chéo `§8.16` với `§8.12.2/§8.12.3` + câu trả lời BA `C-CNL-03` | `counts` cl 1→3; `SC-TS-012`/`014`/`015` hạ phần treo xuống ghi nhận; nếu INCIDENT không bao giờ xuất hiện ⇒ `SC-CNL-015`/`SC-DLV-034` out of scope |
| 2026-09-15 | UPDATE | **DELTA v1.1** — PRD chính thức (`DOC-v1.1-01`) đưa tính năng "Báo cáo sự cố & hỗ trợ" (`FR16`) hoàn toàn mới vào scope, đảo ngược kết luận `C-CNL-01` (v1.0: màn này out of scope) **chỉ trong phạm vi `TS` sở hữu**. +1 REQ mới (`REQ-TS-006`), +8 SC mới (`SC-TS-008..015`) phủ happy path/validation/boundary ảnh/mất mạng/vòng đời phiên/field prefill/đa vai trò. Module có test_data_catalog lần đầu (trước đây module log-only, không có form) | `DOC-v1.1-01` §8.16 | Module TS từ "chỉ log + gap ghi nhận" (7 SC v1.0) sang có tính năng UI đầy đủ test được (8 SC mới) |
| 2026-09-15 | UPDATE | Bổ sung UI reference (`00_input/v1.1/design/TS_01..05`) — verify **toàn bộ end-to-end** luồng "Báo cáo sự cố" trên demo: trigger button (3 vai), form + trần 5 ảnh (`SC-TS-011`), validation nút Gửi disable/enable (`SC-TS-009`), success state đúng verbatim (`SC-TS-008`). Không có CL để resolve (module không mở CL mới ở v1.1) — mục đích là nâng độ tin cậy trước `generate-tc` | Vibe-check thủ công qua Playwright, theo yêu cầu QC GiangDC2 2026-09-15 | `SC-TS-008/009/010/011` sẵn sàng cho `generate-tc` với độ tin cậy cao nhất trong đợt rà này |
| 2026-09-15 | ĐÍNH CHÍNH | Frontmatter `counts` P2/P3 = 6/7 ⇒ **5/8** (v1.0 CARRIED 1/2/4 + v1.1 NEW 1/3/4). Bổ sung frontmatter `counts:` (cl/risk) và `## Tổng quan` cho `risk_assessment.md` — 2 phần bắt buộc theo template mà lượt DELTA bỏ sót | `health-check` 2026-09-15 G-02 + structure-lock (`risk-assessment-template.md`) | Tổng SC 15 không đổi. `risk_assessment.md` giờ có nguồn canonical CL/RISK đọc được bằng máy (`cl: 1` · `risk: 7`) |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — thư mục dùng lại qua nhiều sprint, phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | ⚠️ **KHÔNG mở rộng SC sang xử lý phía Admin** ("liên hệ lại 24h", "đối chiếu MNV") — quy trình ngoài app, không có bề mặt UI end-user để test | `RISK-TS-07`; Admin Portal out of scope (`C-TS-01`, kế thừa v1.0) | Viết SC không thể execute được (không có màn hình để verify) |
| 3 | ⚠️ **`C-CNL-01` (home canonical ở module `CNL`) CHƯA được sửa/đóng ở lượt này** — chỉ có cảnh báo chéo ở đây (`RISK-TS-06`) | `CNL`/`DLV` chưa rà lại delta v1.1 tại thời điểm này | Người đọc `CNL`/`DLV` trước khi 2 module đó được rà lại delta có thể tưởng "Báo sự cố" vẫn out of scope toàn bộ |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"màn 'Báo cáo sự cố' chưa có đặc tả — out of scope v1.0"** (`C-CNL-01`, Resolved 2026-07-27, home canonical ở `v1.0/CNL-huy-don/risk_assessment.md`) **HẾT HIỆU LỰC kể từ v1.1 trong phạm vi module `TS`** — đừng trích lại cho bề mặt "Báo sự cố"; hiện hành là **có đặc tả đầy đủ, vào scope** (`DOC-v1.1-01 §8.16`, xem `REQ-TS-006`). ⚠️ File `CNL-huy-don/` và `DLV-giao-nhan/` (nơi `C-CNL-01` được tham chiếu) **chưa được cập nhật** — chỉ ghi nhận đảo kết luận ở đây, chờ delta chính thức của 2 module đó.

⛔ Kết luận **`C-TS-03(b)` "ô Mã đơn hàng là nhãn tĩnh, không sửa được"** (bản 2026-09-17) **HẾT HIỆU LỰC** — đừng trích lại; hiện hành: ô **sửa được**, `§8.16.2` sai tài liệu (`C-TS-04(d)`).
⛔ Kết luận **"mất mạng hiện trang lỗi mặc định của WebView, không có nút Thử lại"** (bản sáng 2026-09-24) **HẾT HIỆU LỰC** — hiện hành (QC chốt lần 2 sau VR-029): **APP vẽ màn lỗi + nút "Thử lại"**, tức `C-TS-03(c)` (2026-09-17) thực tế lại đúng.
⛔ Kết luận **`C-TS-03(d)` "màn Đã ghi nhận phản hồi + nút Quay lại đơn hàng do APP vẽ"** (bản 2026-09-17) **HẾT HIỆU LỰC** — hiện hành: màn mặc định Microsoft Forms "Đã gửi phản hồi của bạn." (`C-TS-04(b)`).
⛔ Mọi chỗ ghi form là **"Google Form"** — form thật là **Microsoft Forms**.

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🟢 ~~`C-TS-04` còn 2 câu con~~ — **đã chốt 2026-09-24** (QC). Còn duy nhất: hành vi nút "Huỷ" của popup đăng nhập — chốt khi Dev làm xong `FE-321` | Chờ Dev | Retest `FE-321` |
| 3 | 🟡 **Popup đăng nhập Microsoft (`FE-321`, hiện mỗi lần phải đăng nhập) chưa có TC phủ** — yêu cầu mới BA thêm 2026-09-24 | Số lượng TC freeze (`Project_rule §10.5`) ⇒ AI không tự thêm TC | QC quyết định: thêm TC qua lượt `generate-tc` có duyệt, hoặc gắn vào Steps TC hiện có khi Dev làm xong |
| 2 | 🟡 `RISK-TS-07` — quy trình đối chiếu MNV/liên hệ lại phía Admin không test được qua UI | Ngoài phạm vi app end-user | Ghi rõ trong test report nếu execute; không mở SC mới |
