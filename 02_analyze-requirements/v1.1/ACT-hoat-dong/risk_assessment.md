---
id: v1.1/ACT-hoat-dong/risk
title: Risk Assessment — v1.1 · Module ACT
type: risk-assessment
version: v1.1
sprint: 1
module: ACT
counts:
  cl: 3
  risk: 8
  cl_open: 1
  cl_resolved: 2
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
| RISK-ACT-06 | ACT / Nhãn tab & tên màn | **(risk mới)** PRD gọi 2 tab **"Đang chạy" / "Hoàn tất"** (nhất quán 3 chỗ: `EMP-05`, `EMP-06`, `AC-09.1.01`) và gọi màn là **"Đơn của tôi"**; app STG hiển thị **"Đang diễn ra" / "Đã hoàn thành"**, bottom nav ghi **"Hoạt động"**. Chọn sai bên ⇒ hoặc TC FAIL hàng loạt vì lý do không phải bug, hoặc hợp thức hoá việc app lệch đặc tả | **Medium** | `DOC-v1.1-01` §8.17.1 EMP-05/EMP-06 · §6.2 AC-09.1.01 vs `KP-01` §3 KB-ORD-07 (quan sát app 2026-07-27) | `SC-ACT-001` — giữ assert *"có đúng 2 tab"*, **hạ phần nhãn xuống ghi nhận** | ⛔ KHÔNG tự chọn bên nào (`Project_rule §Custom Rules §10.1`). Chốt `C-ACT-02` với BA trước khi assert cứng nhãn | Open (non-blocking) | REQ-ACT-001, SC-ACT-001 |
| RISK-ACT-07 | ACT / Kết cục đơn bất thường | **(risk mới)** Hai kết cục bất thường được xử lý **ngược nhau**: `CANCELLED` **ẩn** khỏi màn (rule v1.0, `SC-ACT-007`) nhưng `RETURNED` **hiện kèm lý do** (`AC-24.2.01`). Dev rất dễ gộp thành một nhánh *"đơn kết thúc bất thường thì ẩn"* ⇒ đơn hoàn hàng biến mất, người dùng **không có cách nào biết hàng đã về đâu** | **Medium** | `DOC-v1.1-01` §6.2 AC-24.2.01 vs `KP-01` §3 KB-ORD-07 (#7) | `SC-ACT-015` — Given phải có **cả 2 đơn** để so trong 1 lượt | ⛔ Không tách `SC-ACT-015` thành 2 SC rời — giá trị của nó nằm ở phép **đối chứng** | Open | REQ-ACT-004, SC-ACT-007, SC-ACT-015 |
| RISK-ACT-03 | ACT / Empty state | *(cập nhật Status)* v1.0: text empty state chưa chốt, từng Resolved rồi REVERT sau 1 ngày ⇒ 2 SC treo ở dạng `[GAP]`, không assert được gì | Medium → **Resolved** | `DOC-v1.1-01` §8.17.1 EMP-05/EMP-06 · §8.17.2 BR17-01..03 · §6.2 AC-29.1.01 | `SC-ACT-012`, `SC-ACT-014` (P3→P2) + `SC-ACT-016`, `SC-ACT-017` | 2 SC hết gap phải **regenerate TC** (Then đổi từ *ghi nhận* sang *assert verbatim*), ⛔ không patch TC cũ | **Resolved** | REQ-ACT-008, REQ-ACT-010 |
| RISK-ACT-04 | ACT / ★ leftover | *(cập nhật Severity + Status)* ★★★★★ còn sót trên card tab kết thúc — v1.0 xếp là *"dấu vết phase sau"* nên **không log bug**; PRD v1.1 loại trừ đánh giá sao **vĩnh viễn** ⇒ nay là **defect** | Low → **Medium** | `DOC-v1.1-01` §8.14.1 BR14-03 · §4 SCOPES Out of Scope (*"thay bằng quà ảo"*) | `SC-ACT-013` — nâng P3 → P2 | Log bug; home phán quyết là `C-GIFT-01` ở module `GIFT`, ⛔ không tạo CL trùng ở đây | Open | REQ-ACT-009, SC-ACT-013 |
| RISK-ACT-08 | ACT / Rule backend không verify được | **(risk mới)** `FR17` Pre-Conditions đặt điều kiện hiển thị empty state là *"cờ dữ liệu rỗng… không dựa vào null của từng field"* — đây là **rule cài đặt phía backend**, qua UI chỉ thấy triệu chứng (skeleton vô hạn / nhảy giữa loading và empty) | Low | `DOC-v1.1-01` §8.17 Pre-Conditions · §8.17.2 BR17-02 | `SC-ACT-017` — gắn `[GAP]` có chủ đích, cần **throttle mạng** mới quan sát được | Ghi nhận theo `§Custom Rules §10.1` bước 3; ⛔ không viết TC khẳng định cho rule không có bề mặt | Open (ghi nhận, non-blocking) | REQ-ACT-010, SC-ACT-017 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-ORD-06 | Text empty state của các màn khi không có data (**home canonical ở đây**) | ✅ **Resolved 2026-09-15 — bằng tài liệu đã phê duyệt, không phải lời chốt miệng** | mở lại 2026-07-29 (từng Resolved 2026-07-28 → REVERT) | REQ-ACT-008, REQ-GIFT-007, REQ-HOME-012, và các SC empty state của FEED/NTF |
| C-ACT-02 | Nhãn 2 tab + tên màn: theo PRD ("Đang chạy"/"Hoàn tất", màn "Đơn của tôi") hay theo app ("Đang diễn ra"/"Đã hoàn thành", nav "Hoạt động")? | 🔴 **Open (non-blocking)** — có thêm bằng chứng demo 2026-09-16, xem ghi chú | 2026-09-15 | REQ-ACT-001, SC-ACT-001 |
| C-ACT-01 | Tap card ở màn Hoạt động mở "Chi tiết tin" hay "Theo dõi đơn"? | ✅ **Resolved 2026-09-16 — qua demo, xem ghi chú** | mở 2026-09-07 | REQ-ACT-006, SC-ACT-011 |

### C-ORD-06 · Text empty state *(RESOLVED 2026-09-15 — lần thứ hai, lần này có bằng chứng)*

📍 `DOC-v1.1-01 §8.17.1 bảng Danh mục empty state · trang 51` · `§8.17.2 BR17-01..03 · trang 51` · `§6.2 AC-29.1.01 · trang 28`

> "EMP-05 | Đơn của tôi — tab Đang chạy | "Không có đơn đang thực hiện" | "Đăng tin gửi hàng""

> "EMP-06 | Đơn của tôi — tab Hoàn tất | "Chưa có đơn hoàn tất" — ẩn luôn khối lịch sử | —"

> `BR17-01`: "Mỗi empty state gồm: icon nét mảnh màu neutral + một dòng tiêu đề + một dòng giải thích + tối đa một CTA."

↳ **Ghi chú:** ⭐ **CL lan rộng nhất của dự án — 5 màn / 6 SC — và home canonical của nó là module này.** Lần chốt trước (2026-07-28) bị **REVERT sau đúng 1 ngày** vì chốt không kèm bằng chứng; đó là lý do lần này phải ghi rõ nguồn: **tài liệu đã phê duyệt**, liệt kê đủ **8 dòng `EMP-01..08`** kèm text và CTA cho từng màn. ⇒ Resolved bền, không phải lời chốt miệng.
**Phân chia text về từng module** (⛔ không tập trung ở đây): `EMP-01/02/03` → `HOME` (`SC-HOME-025..027`) · `EMP-04` → `FEED` · `EMP-05/06` → `ACT` (`SC-ACT-012`/`SC-ACT-014`) · `EMP-07` → `NTF` · `EMP-08` → `GIFT` (`SC-GIFT-008`). **Rule hình thức chung** (`BR17-01..03` + điều kiện cờ rỗng) giữ home tại `ACT` (`SC-ACT-016`/`SC-ACT-017`) vì đây là màn duy nhất có 2 empty state cạnh nhau.
⚠️ **Bất đối xứng CTA là nội dung phải assert, không phải chi tiết trình bày:** `EMP-01` `EMP-02` `EMP-04` `EMP-05` **có** CTA; `EMP-03` `EMP-06` `EMP-07` `EMP-08` **không**. `BR17-01` viết *"tối đa một CTA"* nên "không có" là lựa chọn thiết kế hợp lệ — nếu app hiện nút ở màn đáng lẽ không có thì **sai spec**.

### C-ACT-02 · Nhãn 2 tab và tên màn — PRD hay app? *(OPEN)*

📍 `DOC-v1.1-01 §8.17.1 EMP-05 / EMP-06 · trang 51` · `§6.2 AC-09.1.01 · trang 19`

> `EMP-05`: "Đơn của tôi — tab **Đang chạy**"

> `EMP-06`: "Đơn của tôi — tab **Hoàn tất**"

> `AC-09.1.01`: "Hiện badge "Hết hạn" ở tab **Hoàn tất** kèm lý do…"

↳ **Ghi chú:** PRD dùng **"Đang chạy" / "Hoàn tất"** nhất quán ở **3 chỗ độc lập** ⇒ ⛔ không thể coi là lỗi đánh máy. App STG (`KP-01 §3 KB-ORD-07`, quan sát 2026-07-27) hiển thị **"Đang diễn ra" / "Đã hoàn thành"**; và bottom nav gọi màn là **"Hoạt động"** trong khi PRD gọi **"Đơn của tôi"** (v1.0 ghi nhận "Đơn của tôi" là tiêu đề *bên trong* màn).
**Câu hỏi cho BA/PM:** (a) nhãn nào là chuẩn để assert — PRD hay app? (b) nếu PRD chuẩn thì đây là **defect UI** cần dev sửa hay PRD viết theo bản thiết kế cũ? (c) tên màn trên bottom nav có đổi theo không?
**Vì sao non-blocking:** `SC-ACT-001` vẫn chạy được ở phần *"có đúng 2 tab"*; chỉ phần nhãn treo. **Vì sao vẫn phải chốt trước generate-tc:** nhãn tab xuất hiện trong **Steps của rất nhiều TC** ở `ACT` và các module khác (*"mở tab Đã hoàn thành"*) — chốt muộn thì phải sửa rải rác, đúng kiểu lỗi #1 của đợt cũ (`C-ORD-09` với nhãn "Tài liệu").

↳ **Cập nhật 2026-09-16 — bằng chứng phụ từ demo (không resolve, chỉ củng cố):** Vibe-check qua demo (vai Carrier, Playwright) xác nhận màn Hoạt động có H1 **"Đơn của tôi"** và 2 tab **"Đang diễn ra" / "Đã hoàn thành"** — khớp chính xác quan sát STG cũ (`KP-01 §3 KB-ORD-07`, 2026-07-27), không khớp PRD. Đây là **nguồn độc lập thứ hai** (khác STG thật) cùng cho kết quả app-side giống nhau ⇒ củng cố khả năng nếu BA chọn "PRD chuẩn" thì đây **thực sự là defect**, không phải do quan sát cũ lỗi thời. Câu hỏi "bên nào đúng" vẫn là quyết định của BA/PM, demo không tự trả lời được.

### C-ACT-01 · Đích tap card ở màn Hoạt động *(RESOLVED 2026-09-16 — qua demo)*

📍 Vibe-check demo 2026-09-16 (home canonical gốc: `v1.0/ACT-hoat-dong/risk_assessment.md`, giữ nguyên làm hồ sơ lịch sử)

**Bằng chứng:** Tap vào card "Đơn của tôi" ở màn Hoạt động (vai Carrier, đơn đang `Chờ ghép`) mở đúng màn **"Theo dõi đơn"** — role-aware, có khối "Người gửi"/"Người nhận" kèm nút Gọi, thanh trạng thái 5 mốc, nút hành động theo vai ("Nhận mang giúp đơn này" / "Tôi đã lấy hàng" / …). Chính bản thân card còn in sẵn dòng chữ **"Chạm để theo dõi đơn của bạn"** — tự mô tả đích đến.

**Analyst Note:** Kết quả khớp **Nguồn B** (`DOC-v1.0-02 §3.7`: "bấm vào mở Theo dõi đơn") và khớp hành vi đã biết ở `HOME` (`SC-HOME-015`). Bác bỏ **Nguồn A** (`KP-01 §3 KB-ORD-07` dòng 5: "→ mở Chi tiết tin") — đúng như nghi vấn đã nêu trước đó rằng quan sát cũ **ghi nhầm tên màn** (Chi tiết tin là màn public khác hẳn, không role-aware). `SC-ACT-011` hết `[GAP]`, có thể viết TC assert cứng đích "Theo dõi đơn" thay vì chỉ ghi nhận theo dữ liệu.
⚠️ Khuyến nghị double-check nhanh trên STG thật trước khi hardening automation locator (đúng caveat chung dùng demo làm nguồn), nhưng bằng chứng (nhãn tự mô tả trên card + cấu trúc màn đích) đủ rõ để không coi là blocker cho `generate-tc`.

## Khuyến nghị tổng thể
0. ✅ **`C-ACT-01` đã Resolved 2026-09-16** — đích tap card = "Theo dõi đơn" (role-aware), không phải "Chi tiết tin". `SC-ACT-011` hết GAP.
1. **Chốt `C-ACT-02` trước `generate-tc`** — nhãn tab nằm trong Steps của nhiều TC ở nhiều module; chốt muộn phải sửa rải rác (đúng vết xe đổ của `C-ORD-09`).
2. **2 SC hết gap phải regenerate TC, không patch** (`SC-ACT-012`/`SC-ACT-014`) — Then đổi từ *ghi nhận text là gì* sang *assert verbatim + assert bất đối xứng CTA + assert ẩn khối lịch sử*.
3. **`SC-ACT-015` phải giữ nguyên dạng đối chứng 2 đơn** — tách rời sẽ mất đúng cái nó sinh ra để bắt (`RISK-ACT-07`).
4. **`SC-ACT-013` nay đủ căn cứ log bug** — phối hợp với `SC-GIFT-011` (cùng phán quyết `C-GIFT-01`), chạy cùng lô để log 1 bug 2 bề mặt.
5. **`SC-ACT-016`/`SC-ACT-017` cần tài khoản trắng + throttle mạng** — gộp lô với cụm empty state của `HOME` (`SC-HOME-025..027`) và `GIFT` (`SC-GIFT-008`) để dùng chung 1 tài khoản mới tinh.
