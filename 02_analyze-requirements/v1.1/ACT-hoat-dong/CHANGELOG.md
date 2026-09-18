---
id: v1.1/ACT-hoat-dong/changelog
title: Changelog — Module ACT
type: changelog
version: v1.1
sprint: 1
module:
  code: ACT
  dir: ACT-hoat-dong
  name: Hoạt động (Đơn của tôi)
doc_source:
  - id: DOC-v1.1-01
    section: "§8.17 FR17 (Empty state) · §8.17.1 EMP-05/EMP-06 (+ bảng 8 dòng) · §8.17.2 BR17-01..03 · §6.2 AC-29.1.01 / AC-09.1.01 / AC-24.2.01 · §8.5.1 BR05-03 · §8.14.1 BR14-03 · §4 SCOPES"
id_range:
  req: "REQ-ACT-010 (NEW) + REQ-ACT-001, REQ-ACT-004, REQ-ACT-005, REQ-ACT-008, REQ-ACT-009 (MODIFIED, giữ ID sprint 1)"
  sc: "SC-ACT-015, SC-ACT-016, SC-ACT-017 (NEW) + SC-ACT-001, SC-ACT-005, SC-ACT-008, SC-ACT-012, SC-ACT-013, SC-ACT-014 (MODIFIED, giữ ID sprint 1)"
  cl: "C-ACT-02 (NEW) + C-ORD-06 (home canonical ở module này — chuyển Resolved, giữ ID) · C-ACT-01 (Resolved 2026-09-16 qua demo) + C-ACT-03, C-ACT-04 (NEW 2026-09-16) · C-ACT-02 → Resolved (2026-09-16)"
  risk: "RISK-ACT-06, RISK-ACT-07, RISK-ACT-08 (NEW) + RISK-ACT-03, RISK-ACT-04 (Status/Severity cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-17
---

# Changelog — Module ACT (`ACT`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-17 | UPDATE | **Áp câu trả lời BA vòng 3 + tái vibe-check demo theo đúng chỉ dẫn BA.** BA phản bác lượt vibe-check trước ("ngoài màn hình trang chủ → click vào Hoạt động sẽ xem được mà sao lại giới hạn??") — lượt trước chỉ kiểm màn "Theo dõi đơn" sau submit OFFER (bị ghi đè, đúng là không quan sát được), CHƯA thử điều hướng đúng vào tab "Hoạt động" → "Đang diễn ra". Tái vibe-check theo đúng đường dẫn BA chỉ → **quan sát được card OFFER**: title "Nhận giao hàng &lt;tuyến&gt;", badge "Chờ ghép", 2 dòng "Từ:"/"Đến:", CTA "Chạm để xem tuyến đường của bạn". **`C-ACT-04` ĐÓNG HẲN** | BA trả lời `CL-hoi-BA-v1.1.xlsx` sheet `ACT` dòng "(vòng 3)" 2026-09-17 (bỏ sót ở lượt trước) · vibe-check demo QA GiangDC2 (Chrome MCP) | `counts` cl_resolved 4→5, module ACT **HẾT điểm hỏi BA**; `SC-ACT-004/005/015` viết được Then chính xác |
| 2026-09-17 | UPDATE | **Đồng bộ câu trả lời BA từ `CL-hoi-BA-v1.1.xlsx` (chưa được ghi vào file này ở lượt trước) + vibe-check demo.** `C-ACT-03` → **Resolved** (đích tap card mọi ô còn lại = "Theo dõi đơn", trừ Hoàn thành-chưa-tặng-quà → "Tặng quà"). `C-ACT-04` → **Partially Resolved** — (a)(b) chốt (Hẹn giao lại/Đang hoàn hàng/Có sự cố → "Đang diễn ra"; "Đã huỷ" vẫn ẨN khỏi cả 2 tab, rule v1.0 còn hiệu lực); (c) tin OFFER hiển thị ở "Đơn của tôi" **KHÔNG verify được qua demo** — cùng giới hạn demo đã ghi ở `C-ORD-16`/`C-ASN-03` (đăng OFFER ghi đè lên đơn NEED, không tạo card riêng) | BA trả lời 2026-09-16/17 (`CL-hoi-BA-v1.1.xlsx`) · vibe-check demo QA GiangDC2 2026-09-17 (Playwright MCP) | `counts` cl_open 2→0, cl_resolved 3→4; `C-ACT-04` câu (c) đặt lại câu hỏi cho BA (không dựa demo) |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa WARNING health-check G-03:** thay 5 trích dẫn bị chép lặp sang file khác bằng dòng trỏ `↪` về đúng home (REQ → `requirement_traceability.md` · CL → `risk_assessment.md`) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Nội dung quote không mất — chỉ còn 1 home |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa theo health-check VERSION v1.1 (G-06b CRITICAL):** các đoạn register sống còn kể lại kết luận cũ của CL vừa Resolved (`C-ACT-02` — heading CL, Khuyến nghị #1, ghi chú `REQ-ACT-001`, Source Detail `SC-ACT-001`, dòng tổng quan scenario map) — đổi mục Khuyến nghị / heading / data catalog sang kết luận hiện hành và thêm dòng *"⛔ Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC"* sau các ghi chú gốc (giữ nguyên nội dung cũ làm hồ sơ, không xoá lặng lẽ) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Không đổi `counts`, không đổi Then SC — chỉ đồng bộ chữ với CL section |
| 2026-09-16 | UPDATE | **Áp câu trả lời BA** + rà sâu `§8.12.2/§8.12.3` đối chiếu rule màn Hoạt động. (a) `C-ACT-02` → **Resolved** theo **app**: màn "Đơn của tôi", tab "Đang diễn ra"/"Đã hoàn thành", nav "Hoạt động" (PRD chưa cập nhật); `SC-ACT-001` assert cứng; `RISK-ACT-06` Resolved. (b) `C-ACT-01` bổ sung nhánh BA: Hoàn thành **chưa tặng quà** → màn "Tặng quà"; `SC-ACT-011` cập nhật. (c) **Mở 2 CL mới:** `C-ACT-03` (đích tap card các ô còn thiếu: đã tặng quà · Carrier/Receiver · RETURNED/EXPIRED · INCIDENT) · `C-ACT-04` (12 trạng thái chia 2 tab; CANCELLED ẩn hay hiện; tin OFFER) — vì PRD §8.12.3 cho *"Xem lý do"* đơn đã huỷ/hết hạn, **ngược** rule v1.0 `SC-ACT-007`/`SC-ACT-009` | BA trả lời 2026-09-16 · rà kỹ theo yêu cầu QC GiangDC2 | `counts` cl 3→5; ràng buộc #2 hết hiệu lực; `SC-ACT-001`/`SC-ACT-011` regenerate TC; `SC-ACT-007`/`SC-ACT-009`/`SC-ACT-015` treo chờ `C-ACT-03/04` |
| 2026-09-15 | UPDATE | **DELTA v1.1 (lượt bù — module này bị bỏ sót ở lượt delta đầu).** Kết quả: **+1 REQ, +3 SC, +3 RISK, +1 CL**; **5 REQ / 6 SC MODIFIED**. Ba việc lớn: (a) **`C-ORD-06` ĐÓNG** — CL lan rộng nhất dự án (5 màn / 6 SC), home canonical ở module này, lần này Resolved bằng **tài liệu đã phê duyệt** chứ không phải lời chốt miệng như lần bị REVERT 2026-07-29; (b) `RETURNED` — kết cục đơn hoàn toàn mới — tạo cặp **đối chứng với `CANCELLED`** (`SC-ACT-015`); (c) `SC-ACT-013` (★ leftover) chuyển từ `[GAP]` sang **defect đủ căn cứ log bug** | `DOC-v1.1-01` §8.17/§8.17.1/§8.17.2 · §6.2 AC-29/AC-09/AC-24 · §8.5.1 BR05-03 · §8.14.1 BR14-03 · §4 | 2 SC empty state hết gap ⇒ **regenerate TC**, ⛔ không patch; `C-ACT-02` (nhãn tab) phải chốt **trước** `generate-tc` |
| 2026-09-16 | UPDATE | Vibe-check qua demo (Playwright, vai Carrier) — **đóng `C-ACT-01`**: tap card ở màn Hoạt động mở đúng "Theo dõi đơn" (role-aware), không phải "Chi tiết tin"; card còn tự in dòng "Chạm để theo dõi đơn của bạn". Bác bỏ quan sát cũ `KP-01 §3 KB-ORD-07` (nghi ghi nhầm tên màn). Đồng thời củng cố thêm bằng chứng cho `C-ACT-02` (nhãn tab) — demo cho kết quả giống hệt quan sát STG cũ ("Đang diễn ra"/"Đã hoàn thành"), không resolve được câu hỏi PRD-vs-app nhưng loại trừ khả năng quan sát cũ lỗi thời | Vibe-check thủ công qua Playwright, theo yêu cầu QC GiangDC2 2026-09-16 | `SC-ACT-011` hết `[GAP]`, assert cứng đích "Theo dõi đơn"; `counts.cl_resolved` 1→2, `cl_open` 2→1 |
| 2026-09-15 | ĐÍNH CHÍNH | Phát hiện **xung đột nhãn PRD ⟷ app**: PRD gọi 2 tab "Đang chạy"/"Hoàn tất" và màn là "Đơn của tôi"; app STG hiển thị "Đang diễn ra"/"Đã hoàn thành", bottom nav "Hoạt động". `SC-ACT-001` **tạm hạ phần nhãn xuống ghi nhận**, ⛔ không assert cứng bên nào | `DOC-v1.1-01` §8.17.1 EMP-05/EMP-06 · §6.2 AC-09.1.01 vs `KP-01` §3 KB-ORD-07 · áp `Project_rule §Custom Rules §10.1` | Mở `C-ACT-02`; nhãn tab nằm trong Steps của nhiều TC ở nhiều module ⇒ chốt muộn sẽ phải sửa rải rác |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | ~~⛔ KHÔNG assert cứng nhãn 2 tab~~ — **HẾT HIỆU LỰC 2026-09-16** | `C-ACT-02` Resolved: BA chốt nhãn theo app. Hiện hành: assert "Đơn của tôi" · "Đang diễn ra" · "Đã hoàn thành" · nav "Hoạt động" | Tiếp tục chỉ ghi nhận ⇒ bỏ lọt đổi nhãn sai |
| 3 | ⭐ **Bất đối xứng CTA giữa `EMP-05` và `EMP-06` là nội dung PHẢI assert** — tab đang-chạy **có** CTA, tab hoàn-tất **không** | `BR17-01` viết *"tối đa một CTA"* ⇒ "không có" là lựa chọn thiết kế hợp lệ, không phải thiếu sót | Bỏ qua ⇒ app hiện thừa/thiếu nút mà TC vẫn PASS |
| 4 | ⭐ **`EMP-06` phải assert thêm *"ẩn luôn khối lịch sử"*** — hành vi NGOÀI cấu trúc chuẩn `BR17-01`, chỉ tab này có | Khung lịch sử rỗng vẫn hiện thì trông "gần đúng" nên rất dễ lọt | Lỗi hiển thị lọt qua vì TC chỉ kiểm chuỗi text |
| 5 | ⛔ **KHÔNG tách `SC-ACT-015` thành 2 SC rời** — Given phải có **cả** đơn `CANCELLED` lẫn đơn `RETURNED` | Giá trị của SC nằm ở phép **đối chứng**: 2 kết cục bất thường, 2 cách xử lý ngược nhau (`RISK-ACT-07`) | Tách ra ⇒ mất đúng cái SC sinh ra để bắt (dev gộp 2 nhánh thành 1) |
| 6 | ⛔ **KHÔNG nhân bản text `EMP-01..04`, `EMP-07`, `EMP-08`** sang module này — chỉ giữ `EMP-05`/`EMP-06` + rule hình thức chung | `C-ORD-06` chạm 5 màn; mỗi text có home ở module sở hữu màn đó | 8 bản sao của cùng 1 bảng ⇒ 8 chỗ để drift |
| 7 | ⚠️ **`SC-ACT-017` giữ nhãn `[GAP]`** — *"cờ dữ liệu rỗng, không dựa null từng field"* là rule **backend**, UI chỉ thấy triệu chứng | `§Custom Rules §10.1` bước 3: ghi nhận, không viết TC khẳng định cho rule không có bề mặt | TC khẳng định cho rule không verify được ⇒ FAIL vĩnh viễn hoặc PASS giả |

### 🔁 Kết luận bị đảo

⛔ `DOC-v1.0-06 KP-01 §3 KB-ORD-07` dòng 5 **"Tap card ≠ Hết hạn → mở màn Chi tiết tin"** **HẾT HIỆU LỰC** (demo 2026-09-16 + BA 2026-09-16). Hiện hành: Đang diễn ra → **"Theo dõi đơn"**; Đã hoàn thành chưa tặng quà → **"Tặng quà"**. KP-01 là file v1.0, **không sửa**.


⛔ Kết luận **"text empty state chưa chốt — chỉ ghi nhận, không assert"** (`C-ORD-06`, REVERT 2026-07-29) **HẾT HIỆU LỰC** — đừng trích lại. Hiện hành: **8 empty state có text chính thức** ở `DOC-v1.1-01 §8.17.1`, phân chia về từng module; `SC-ACT-012`/`SC-ACT-014` assert **verbatim**.

⛔ Kết luận **"★ leftover là dấu vết của phase sau, không log bug"** (suy từ `C-GIFT-01` *"out of scope v1.0"*) **HẾT HIỆU LỰC**. Hiện hành: đánh giá sao bị loại trừ **vĩnh viễn** (`§4 SCOPES`, `BR14-03`) ⇒ ★ còn sót **là defect**. Home phán quyết ở `GIFT`.

## 3. Nợ đang mở

| # | Nợ | Vì sao còn treo | Hướng xử lý |
|---|---|---|---|
| 1 | 🔴 **`C-ACT-03` + `C-ACT-04`** (mới 2026-09-16) — đích tap card còn thiếu + phân bổ 12 trạng thái vào 2 tab + CANCELLED/OFFER | PRD mở rộng 5 → 12 trạng thái nhưng không nói trạng thái nào ở tab nào; rule v1.0 (Đã huỷ ẩn, Hết hạn không tap) đụng PRD §8.12.3 | Hỏi BA (sheet `ACT`) **trước `generate-tc`** — nằm trong Steps của `SC-ACT-004/005/007/009/010/015` |
| 2 | ✅ **`C-ACT-01` Resolved 2026-09-16** — tap card mở "Theo dõi đơn" (role-aware), xác nhận qua demo | Card tự in "Chạm để theo dõi đơn của bạn"; khớp hành vi đã biết ở HOME | `SC-ACT-011` hết `[GAP]`, assert cứng |
| 3 | 🟡 **`SC-ACT-015` / phần `RETURNED` của `SC-ACT-005` chờ nhánh `FR09`** | Trạng thái `RETURNED` mới ở v1.1, `RISK-DLV-08` cảnh báo app có thể chưa build | Gộp lô với `SC-DLV-053..056`; nếu chưa có thì verdict `BLOCKED`, ⛔ không PASS |
| 4 | 🟡 **Tài khoản trắng dùng chung** cho `SC-ACT-012/014/016/017` | Cùng nhu cầu với `SC-HOME-025..027` và `SC-GIFT-008`; môi trường đã có dữ liệu thì không tái tạo được | Xin **1 tài khoản mới tinh**, chạy hết cụm empty state trong 1 lượt rồi mới để nó "bẩn" |
| 5 | 🟡 **`SC-ACT-017` cần throttle mạng** | Mạng nhanh thì pha loading trôi quá nhanh, không phân biệt được *đang tải* ⟷ *không có dữ liệu* | Ghi rõ bước throttle 3G trong Steps của TC |
