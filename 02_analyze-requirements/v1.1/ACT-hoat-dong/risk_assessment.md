---
id: v1.1/ACT-hoat-dong/risk
title: Risk Assessment — v1.1 · Module ACT
type: risk-assessment
version: v1.1
sprint: 1
module: ACT
counts:
  cl: 5
  risk: 8
  cl_open: 2
  cl_resolved: 3
status: ANALYZED
updated: 2026-09-16
---

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (5 dòng, `RISK-ACT-01..05`) xem `v1.0/ACT-hoat-dong/risk_assessment.md` — KHÔNG lặp lại ở đây. **ID mới bắt đầu từ `RISK-ACT-06`.**

## Tổng quan
| Module | Risk Level | Rủi ro chính (delta v1.1) |
|--------|-----------|--------------|
| ACT | **Medium** (không đổi) | `C-ORD-06` — CL lan rộng nhất dự án, **home canonical ở module này** — đã đóng bằng tài liệu phê duyệt, gỡ được rủi ro lớn nhất của v1.0. Đổi lại mở rủi ro mới cùng loại nhưng ngược chiều: **PRD gọi 2 tab khác app** (`RISK-ACT-06`), và nếu chọn sai bên thì TC FAIL hàng loạt vì lý do không phải bug |

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-ACT-06 | ACT / Nhãn tab & tên màn | **(risk mới 2026-09-15)** PRD gọi 2 tab "Đang chạy" / "Hoàn tất" và màn "Đơn của tôi"; app hiển thị "Đang diễn ra" / "Đã hoàn thành", bottom nav "Hoạt động". **BA chốt 2026-09-16: app đúng, PRD chưa cập nhật** | Medium → **Resolved** | `DOC-v1.1-01` §8.17.1 EMP-05/EMP-06 · §6.2 AC-09.1.01 vs `KP-01` §3 KB-ORD-07 · BA trả lời 2026-09-16 | `SC-ACT-001` — assert cứng: tiêu đề màn **"Đơn của tôi"**, 2 tab **"Đang diễn ra"** / **"Đã hoàn thành"**, nhãn bottom nav **"Hoạt động"** | Ràng buộc #2 `CHANGELOG §2` hết hiệu lực. Mọi chỗ PRD viết "tab Đang chạy"/"tab Hoàn tất" (AC-01.1.01, AC-09.1.01, EMP-05/06…) đọc thành nhãn app | **Resolved** | REQ-ACT-001, SC-ACT-001 |
| RISK-ACT-07 | ACT / Kết cục đơn bất thường | **(risk mới)** Hai kết cục bất thường được xử lý **ngược nhau**: `CANCELLED` **ẩn** khỏi màn (rule v1.0, `SC-ACT-007`) nhưng `RETURNED` **hiện kèm lý do** (`AC-24.2.01`). Dev rất dễ gộp thành một nhánh *"đơn kết thúc bất thường thì ẩn"* ⇒ đơn hoàn hàng biến mất, người dùng **không có cách nào biết hàng đã về đâu** | **Medium** | `DOC-v1.1-01` §6.2 AC-24.2.01 vs `KP-01` §3 KB-ORD-07 (#7) | `SC-ACT-015` — Given phải có **cả 2 đơn** để so trong 1 lượt | ⛔ Không tách `SC-ACT-015` thành 2 SC rời — giá trị của nó nằm ở phép **đối chứng** | Open | REQ-ACT-004, SC-ACT-007, SC-ACT-015 |
| RISK-ACT-03 | ACT / Empty state | *(cập nhật Status)* v1.0: text empty state chưa chốt, từng Resolved rồi REVERT sau 1 ngày ⇒ 2 SC treo ở dạng `[GAP]`, không assert được gì | Medium → **Resolved** | `DOC-v1.1-01` §8.17.1 EMP-05/EMP-06 · §8.17.2 BR17-01..03 · §6.2 AC-29.1.01 | `SC-ACT-012`, `SC-ACT-014` (P3→P2) + `SC-ACT-016`, `SC-ACT-017` | 2 SC hết gap phải **regenerate TC** (Then đổi từ *ghi nhận* sang *assert verbatim*), ⛔ không patch TC cũ | **Resolved** | REQ-ACT-008, REQ-ACT-010 |
| RISK-ACT-04 | ACT / ★ leftover | *(cập nhật Severity + Status)* ★★★★★ còn sót trên card tab kết thúc — v1.0 xếp là *"dấu vết phase sau"* nên **không log bug**; PRD v1.1 loại trừ đánh giá sao **vĩnh viễn** ⇒ nay là **defect** | Low → **Medium** | `DOC-v1.1-01` §8.14.1 BR14-03 · §4 SCOPES Out of Scope (*"thay bằng quà ảo"*) | `SC-ACT-013` — nâng P3 → P2 | Log bug; home phán quyết là `C-GIFT-01` ở module `GIFT`, ⛔ không tạo CL trùng ở đây | Open | REQ-ACT-009, SC-ACT-013 |
| RISK-ACT-08 | ACT / Rule backend không verify được | **(risk mới)** `FR17` Pre-Conditions đặt điều kiện hiển thị empty state là *"cờ dữ liệu rỗng… không dựa vào null của từng field"* — đây là **rule cài đặt phía backend**, qua UI chỉ thấy triệu chứng (skeleton vô hạn / nhảy giữa loading và empty) | Low | `DOC-v1.1-01` §8.17 Pre-Conditions · §8.17.2 BR17-02 | `SC-ACT-017` — gắn `[GAP]` có chủ đích, cần **throttle mạng** mới quan sát được | Ghi nhận theo `§Custom Rules §10.1` bước 3; ⛔ không viết TC khẳng định cho rule không có bề mặt | Open (ghi nhận, non-blocking) | REQ-ACT-010, SC-ACT-017 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-ORD-06 | Text empty state của các màn khi không có data (**home canonical ở đây**) | ✅ **Resolved 2026-09-15 — bằng tài liệu đã phê duyệt, không phải lời chốt miệng** | mở lại 2026-07-29 (từng Resolved 2026-07-28 → REVERT) | REQ-ACT-008, REQ-GIFT-007, REQ-HOME-012, và các SC empty state của FEED/NTF |
| C-ACT-02 | Nhãn 2 tab + tên màn: theo PRD hay theo app? | ✅ **Resolved 2026-09-16 — BA: theo app** (màn "Đơn của tôi", tab "Đang diễn ra"/"Đã hoàn thành", nav "Hoạt động"; PRD chưa cập nhật) | 2026-09-15 | REQ-ACT-001, SC-ACT-001 |
| C-ACT-01 | Tap card ở màn Hoạt động mở "Chi tiết tin" hay "Theo dõi đơn"? | ✅ **Resolved 2026-09-16 — demo + BA xác nhận**: Đang diễn ra → "Theo dõi đơn"; Hoàn thành **chưa tặng quà** → màn "Tặng quà" | mở 2026-09-07 | REQ-ACT-006, SC-ACT-011 |
| C-ACT-03 | Đích tap card cho các ô BA chưa nói: đã tặng quà · vai Carrier/Receiver ở tab Đã hoàn thành · RETURNED/EXPIRED · INCIDENT | 🔴 **Open (mới 2026-09-16)** | 2026-09-16 | REQ-ACT-006, SC-ACT-009, SC-ACT-010, SC-ACT-011 |
| C-ACT-04 | 12 trạng thái chia vào 2 tab thế nào; đơn "Đã huỷ" ẩn (rule v1.0) hay hiện "Xem lý do" (PRD §8.12.3); tin OFFER hiển thị ở đâu | 🔴 **Open (mới 2026-09-16)** | 2026-09-16 | REQ-ACT-004, SC-ACT-004, SC-ACT-005, SC-ACT-007, SC-ACT-015 |

### C-ORD-06 · Text empty state *(RESOLVED 2026-09-15 — lần thứ hai, lần này có bằng chứng)*

📍 `DOC-v1.1-01 §8.17.1 bảng Danh mục empty state · trang 51` · `§8.17.2 BR17-01..03 · trang 51` · `§6.2 AC-29.1.01 · trang 28`

> ↪ *Quote `EMP-05` — home ở `requirement_traceability.md` · `REQ-ACT-008` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

> ↪ *Quote `EMP-06` — home ở `requirement_traceability.md` · `REQ-ACT-008` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

> `BR17-01`: "Mỗi empty state gồm: icon nét mảnh màu neutral + một dòng tiêu đề + một dòng giải thích + tối đa một CTA."

↳ **Ghi chú:** ⭐ **CL lan rộng nhất của dự án — 5 màn / 6 SC — và home canonical của nó là module này.** Lần chốt trước (2026-07-28) bị **REVERT sau đúng 1 ngày** vì chốt không kèm bằng chứng; đó là lý do lần này phải ghi rõ nguồn: **tài liệu đã phê duyệt**, liệt kê đủ **8 dòng `EMP-01..08`** kèm text và CTA cho từng màn. ⇒ Resolved bền, không phải lời chốt miệng.
**Phân chia text về từng module** (⛔ không tập trung ở đây): `EMP-01/02/03` → `HOME` (`SC-HOME-025..027`) · `EMP-04` → `FEED` · `EMP-05/06` → `ACT` (`SC-ACT-012`/`SC-ACT-014`) · `EMP-07` → `NTF` · `EMP-08` → `GIFT` (`SC-GIFT-008`). **Rule hình thức chung** (`BR17-01..03` + điều kiện cờ rỗng) giữ home tại `ACT` (`SC-ACT-016`/`SC-ACT-017`) vì đây là màn duy nhất có 2 empty state cạnh nhau.
⚠️ **Bất đối xứng CTA là nội dung phải assert, không phải chi tiết trình bày:** `EMP-01` `EMP-02` `EMP-04` `EMP-05` **có** CTA; `EMP-03` `EMP-06` `EMP-07` `EMP-08` **không**. `BR17-01` viết *"tối đa một CTA"* nên "không có" là lựa chọn thiết kế hợp lệ — nếu app hiện nút ở màn đáng lẽ không có thì **sai spec**.

### C-ACT-02 · Nhãn 2 tab và tên màn — PRD hay app? *(mở 2026-09-15 → RESOLVED 2026-09-16, xem khối trả lời BA bên dưới)*

📍 `DOC-v1.1-01 §8.17.1 EMP-05 / EMP-06 · trang 51` · `§6.2 AC-09.1.01 · trang 19`

> `EMP-05`: "Đơn của tôi — tab **Đang chạy**"

> `EMP-06`: "Đơn của tôi — tab **Hoàn tất**"

> `AC-09.1.01`: "Hiện badge "Hết hạn" ở tab **Hoàn tất** kèm lý do…"

↳ **Ghi chú:** PRD dùng **"Đang chạy" / "Hoàn tất"** nhất quán ở **3 chỗ độc lập** ⇒ ⛔ không thể coi là lỗi đánh máy. App STG (`KP-01 §3 KB-ORD-07`, quan sát 2026-07-27) hiển thị **"Đang diễn ra" / "Đã hoàn thành"**; và bottom nav gọi màn là **"Hoạt động"** trong khi PRD gọi **"Đơn của tôi"** (v1.0 ghi nhận "Đơn của tôi" là tiêu đề *bên trong* màn).
**Câu hỏi cho BA/PM:** (a) nhãn nào là chuẩn để assert — PRD hay app? (b) nếu PRD chuẩn thì đây là **defect UI** cần dev sửa hay PRD viết theo bản thiết kế cũ? (c) tên màn trên bottom nav có đổi theo không?
**Vì sao non-blocking:** `SC-ACT-001` vẫn chạy được ở phần *"có đúng 2 tab"*; chỉ phần nhãn treo. **Vì sao vẫn phải chốt trước generate-tc:** nhãn tab xuất hiện trong **Steps của rất nhiều TC** ở `ACT` và các module khác (*"mở tab Đã hoàn thành"*) — chốt muộn thì phải sửa rải rác, đúng kiểu lỗi #1 của đợt cũ (`C-ORD-09` với nhãn "Tài liệu").

⛔ **Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC, đừng trích lại:** BA chốt nhãn **theo app** — màn "Đơn của tôi", tab "Đang diễn ra"/"Đã hoàn thành", nav "Hoạt động"; PRD chưa cập nhật. `SC-ACT-001` assert cứng.

↳ **Cập nhật 2026-09-16 — bằng chứng phụ từ demo (không resolve, chỉ củng cố):** Vibe-check qua demo (vai Carrier, Playwright) xác nhận màn Hoạt động có H1 **"Đơn của tôi"** và 2 tab **"Đang diễn ra" / "Đã hoàn thành"** — khớp chính xác quan sát STG cũ (`KP-01 §3 KB-ORD-07`, 2026-07-27), không khớp PRD. Đây là **nguồn độc lập thứ hai** (khác STG thật) cùng cho kết quả app-side giống nhau ⇒ củng cố khả năng nếu BA chọn "PRD chuẩn" thì đây **thực sự là defect**, không phải do quan sát cũ lỗi thời. Câu hỏi "bên nào đúng" vẫn là quyết định của BA/PM, demo không tự trả lời được.

### C-ACT-01 · Đích tap card ở màn Hoạt động *(RESOLVED 2026-09-16 — qua demo)*

📍 Vibe-check demo 2026-09-16 (home canonical gốc: `v1.0/ACT-hoat-dong/risk_assessment.md`, giữ nguyên làm hồ sơ lịch sử)

**Bằng chứng:** Tap vào card "Đơn của tôi" ở màn Hoạt động (vai Carrier, đơn đang `Chờ ghép`) mở đúng màn **"Theo dõi đơn"** — role-aware, có khối "Người gửi"/"Người nhận" kèm nút Gọi, thanh trạng thái 5 mốc, nút hành động theo vai ("Nhận mang giúp đơn này" / "Tôi đã lấy hàng" / …). Chính bản thân card còn in sẵn dòng chữ **"Chạm để theo dõi đơn của bạn"** — tự mô tả đích đến.

**Analyst Note:** Kết quả khớp **Nguồn B** (`DOC-v1.0-02 §3.7`: "bấm vào mở Theo dõi đơn") và khớp hành vi đã biết ở `HOME` (`SC-HOME-015`). Bác bỏ **Nguồn A** (`KP-01 §3 KB-ORD-07` dòng 5: "→ mở Chi tiết tin") — đúng như nghi vấn đã nêu trước đó rằng quan sát cũ **ghi nhầm tên màn** (Chi tiết tin là màn public khác hẳn, không role-aware). `SC-ACT-011` hết `[GAP]`, có thể viết TC assert cứng đích "Theo dõi đơn" thay vì chỉ ghi nhận theo dữ liệu.
⚠️ Khuyến nghị double-check nhanh trên STG thật trước khi hardening automation locator (đúng caveat chung dùng demo làm nguồn), nhưng bằng chứng (nhãn tự mô tả trên card + cấu trúc màn đích) đủ rõ để không coi là blocker cho `generate-tc`.

### C-ACT-02 · ↳ BA trả lời 2026-09-16 *(→ RESOLVED)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `ACT` · cột "Câu trả lời BA" · 2026-09-16

> "a. Đơn của tôi. Tab Đang diễn ra|Đã hoàn thành
> b. PRD Ba chưa cập nhật nhé,
> c. Vẫn là Hoạt động"

↳ **Ghi chú:** Chốt cả 3 vế theo **app**: tiêu đề màn **"Đơn của tôi"** · 2 tab **"Đang diễn ra"** / **"Đã hoàn thành"** · nhãn bottom nav **"Hoạt động"**. Lệch là do **PRD chưa cập nhật**, không phải defect app. ⇒ `SC-ACT-001` assert cứng; ràng buộc #2 `CHANGELOG §2` hết hiệu lực. ⚠️ Text empty state `EMP-05` / `EMP-06` (*"Không có đơn đang thực hiện"*, *"Chưa có đơn hoàn tất"*) **không bị ảnh hưởng** — BA chỉ chốt nhãn tab, không chốt text empty state. Chữ "tab Đang chạy"/"tab Hoàn tất" ở mọi AC khác (`AC-01.1.01`, `AC-09.1.01`) đọc là "Đang diễn ra"/"Đã hoàn thành".

### C-ACT-01 · ↳ BA trả lời 2026-09-16 *(RESOLVED — mở rộng thêm 1 nhánh)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `ACT` · cột "Câu trả lời BA" · 2026-09-16

> "Đọc lại ver cũ xem có hong , chỗ này không đổi nhé ,(đang diễn ra thì ra màn hình theo dõi đơn, hoàn thành chưa tặng quà thì ra màn hình tặng qùa"

↳ **Ghi chú:** Khớp kết luận demo 2026-09-16 (**Đang diễn ra → "Theo dõi đơn"**) và bổ sung nhánh mới: **Đã hoàn thành + chưa tặng quà → màn "Tặng quà"**. ⚠️ BA bảo *"đọc lại ver cũ, không đổi"* — nhưng bản v1.0 `KP-01 §3 KB-ORD-07` dòng 5 ghi *"→ mở màn Chi tiết tin"*, **ngược** với câu trả lời này. Theo nguyên tắc *kết luận bị đảo không xoá lặng lẽ*: dòng đó của KP-01 **hết hiệu lực** (ghi ở `CHANGELOG §2`), không sửa file v1.0. Các ô BA chưa nói → mở `C-ACT-03`.

### C-ACT-03 · Đích tap card cho các trường hợp còn lại *(OPEN — mới 2026-09-16)*

📍 BA trả lời `C-ACT-01` 2026-09-16 ⟷ `DOC-v1.1-01 §8.12.3 Hành động khả dụng theo trạng thái · trang 46` · `DOC-v1.0-06 KP-01 §3 KB-ORD-07` dòng 5–6

> `§8.12.3`: "COMPLETED | Tặng quà cảm ơn | Xem quà đã nhận | Xem lịch sử" · "RETURNED · CANCELLED · EXPIRED | Xem lý do · đăng lại | Xem lý do | Xem lý do"

> `KB-ORD-07` #6: "Tap card "Hết hạn" | → không cho thao tác (non-clickable)"

↳ **Ghi chú:** BA mới trả lời 2 ô (Đang diễn ra · Hoàn thành *chưa tặng quà*). Ma trận thật là **trạng thái × vai × đã/chưa tặng quà**, còn thiếu: (a) Hoàn thành **đã tặng quà** (vai Sender) → "Theo dõi đơn" chỉ xem? (b) Vai **Carrier / Receiver** ở tab Đã hoàn thành (không bao giờ tặng quà) → màn nào? (c) Đơn **RETURNED** và **EXPIRED** — mở được để *"Xem lý do · đăng lại"* như PRD, hay **không cho tap** như rule v1.0 (`SC-ACT-009`)? (d) Đơn **INCIDENT / RESCHEDULED / RETURNING** mở "Theo dõi đơn" như đơn đang chạy? ⛔ Chưa chốt thì `SC-ACT-010/011` chỉ assert 2 ô BA đã trả lời.

### C-ACT-04 · Phân bổ trạng thái vào 2 tab + đơn "Đã huỷ" + tin OFFER *(OPEN — mới 2026-09-16)*

📍 `DOC-v1.1-01 §8.12.2 · trang 45` · `§8.12.3 · trang 46` · `§6.2 AC-19.1.01 / AC-20.1.01 · trang 23` ⟷ `DOC-v1.0-06 KP-01 §3 KB-ORD-07` dòng 7

> `KB-ORD-07` #7: "Đơn trạng thái "Đã huỷ" | **KHÔNG** hiển thị ở cả 2 tab"

> `§8.12.3`: "RETURNED · CANCELLED · EXPIRED | Xem lý do · đăng lại | Xem lý do | Xem lý do"

> `AC-19.1.01`: "…Sau khi đăng, hiện màn "Đã ghi nhận tuyến đường"; tuyến xem lại được ở "Đơn của tôi"."

↳ **Ghi chú:** PRD v1.1 có **12 trạng thái** (v1.0 chỉ 5) nhưng **không nói trạng thái nào nằm tab nào**. (a) `RESCHEDULED` · `RETURNING` · `INCIDENT` → tab **Đang diễn ra**? `RETURNED` · `EXPIRED` → **Đã hoàn thành** (`SC-ACT-005` đang giả định vậy)? (b) Đơn **CANCELLED**: rule v1.0 (BA-chat 2026-07-27) là **ẩn khỏi cả 2 tab** (`SC-ACT-007`) — nhưng PRD cho mọi vai *"Xem lý do"* đơn đã huỷ ⇒ nếu ẩn thì xem lý do ở đâu? Rule v1.0 **còn hiệu lực** không? (c) Tin **OFFER** (tuyến đường) hiện ở tab nào, card trông ra sao, nhãn trạng thái gì, tap vào mở màn nào? `SC-ACT-015` (đối chứng CANCELLED ẩn ⟷ RETURNED hiện) phụ thuộc trực tiếp câu (b).

## Khuyến nghị tổng thể
0. ✅ **`C-ACT-01` đã Resolved 2026-09-16** — đích tap card = "Theo dõi đơn" (role-aware), không phải "Chi tiết tin". `SC-ACT-011` hết GAP.
1. ✅ **`C-ACT-02` Resolved 2026-09-16** — nhãn theo app ("Đơn của tôi" · "Đang diễn ra"/"Đã hoàn thành" · nav "Hoạt động"). Việc cần chốt **trước `generate-tc`** nay là **`C-ACT-03`** (đích tap card các ô còn thiếu) và **`C-ACT-04`** (12 trạng thái chia 2 tab, đơn Đã huỷ ẩn/hiện, tin OFFER).
2. **2 SC hết gap phải regenerate TC, không patch** (`SC-ACT-012`/`SC-ACT-014`) — Then đổi từ *ghi nhận text là gì* sang *assert verbatim + assert bất đối xứng CTA + assert ẩn khối lịch sử*.
3. **`SC-ACT-015` phải giữ nguyên dạng đối chứng 2 đơn** — tách rời sẽ mất đúng cái nó sinh ra để bắt (`RISK-ACT-07`).
4. **`SC-ACT-013` nay đủ căn cứ log bug** — phối hợp với `SC-GIFT-011` (cùng phán quyết `C-GIFT-01`), chạy cùng lô để log 1 bug 2 bề mặt.
5. **`SC-ACT-016`/`SC-ACT-017` cần tài khoản trắng + throttle mạng** — gộp lô với cụm empty state của `HOME` (`SC-HOME-025..027`) và `GIFT` (`SC-GIFT-008`) để dùng chung 1 tài khoản mới tinh.
