---
id: v1.1/ACT-hoat-dong/scenario-map
title: Test Scenario Map — v1.1 · Module ACT
type: scenario-map
version: v1.1
sprint: 1
module: ACT
counts:
  req: 10
  sc: 17
  new: 3
  modified: 6
  carried: 8
  deprecated: 0
  p1: 0
  p2: 11
  p3: 6
status: ANALYZED
updated: 2026-09-15
---

# Test Scenario Map — v1.1 · Module ACT

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module ACT **tính tới v1.1** (bao gồm CARRIED từ v1.0).
> Parent: `v1.0/ACT-hoat-dong/` — 8 SC không đổi (CARRIED), 6 SC MODIFIED (giữ ID v1.0), 3 SC NEW.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Delta lần này fan-out theo: 2 empty state có **bất đối xứng CTA** (mỗi tab 1 SC — đã có sẵn, chỉ siết) · kết cục đơn mới (`RETURNED`) · 3 rule hình thức chung của `FR17` gom thành 2 SC cross-cutting đặt home tại đây.
> Trần: **text** của `EMP-01..04`, `EMP-07`, `EMP-08` có home ở module tương ứng — ⛔ không nhân bản; ở đây chỉ giữ `EMP-05`/`EMP-06` + **rule chung**.
> 📌 `Project_rule §Custom Rules §10.2`: **màn có tab ⇒ mỗi tab 1 TC riêng verify data** — đã tuân thủ từ v1.0 (`SC-ACT-004`/`SC-ACT-005`, `SC-ACT-012`/`SC-ACT-014`).

## Tổng quan
- Tổng số scenarios (tính tới v1.1): **17** (NEW: 3, MODIFIED: 6, CARRIED: 8)
- Phân bổ priority: P1: 0 | P2: 11 | P3: 6
- Delta lớn nhất: **`C-ORD-06` đóng** — CL lan rộng nhất dự án (5 màn / 6 SC) có home canonical ở module này; `SC-ACT-012`/`SC-ACT-014` hết `[GAP]`, nâng P3 → P2.
- ⚠️ Delta gây tranh cãi nhất: **nhãn 2 tab PRD ≠ app** ⇒ `C-ACT-02` mở 2026-09-15 → ✅ **Resolved 2026-09-16 theo app** (PRD chưa cập nhật); `SC-ACT-001` assert cứng nhãn app.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### ACT — Hoạt động / "Đơn của tôi" (delta v1.1)

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-ACT-015 | Đơn RETURNED hiện ở tab kết thúc kèm lý do hoàn hàng | REQ-ACT-004 | DOC-v1.1-01 §6.2 AC-24.2.01 | Có 1 đơn kết thúc ở `RETURNED` (đã đi hết nhánh `FR09`) và 1 đơn `CANCELLED` để đối chứng | Mở "Đơn của tôi" → tab kết thúc, rà cả 2 đơn | Đơn `RETURNED` **CÓ** trong danh sách và **hiện lý do hoàn hàng**; đơn `CANCELLED` **vẫn bị ẩn** (rule v1.0 `SC-ACT-007`) — hai kết cục bất thường, hai cách xử lý khác nhau | P2 | Business Rule | NEW |
| SC-ACT-016 | Empty state không che thanh tab dưới và vẫn cuộn được | REQ-ACT-010 | DOC-v1.1-01 §8.17.2 BR17-03 · §6.2 AC-29.1.01 | Tài khoản trắng, đang ở 1 trong 2 tab rỗng của "Đơn của tôi" | Quan sát thanh tab dưới, rồi thử vuốt cuộn màn | Empty state **KHÔNG che** thanh tab dưới (cả 5 tab bấm được) **và** màn **vẫn cuộn được** | P3 | UI | NEW |
| SC-ACT-017 | [GAP] Điều kiện hiện empty state dựa cờ rỗng, không dựa null field | REQ-ACT-010 | DOC-v1.1-01 §8.17 Pre-Conditions · §8.17.2 BR17-02 | Tài khoản trắng; có thể throttle mạng về 3G chậm | Mở tab rỗng và quan sát chuỗi trạng thái hiển thị từ lúc vào màn | Phân biệt rõ **đang tải** ⟷ **không có dữ liệu**; ⛔ không skeleton vô hạn. GHI NHẬN GAP: điều kiện *"cờ dữ liệu rỗng"* là rule **backend**, không verify trực tiếp qua UI được | P3 | UI | NEW |
| SC-ACT-012 | Empty state tab "Đang chạy" — text + CTA chính thức *(hết gap)* | REQ-ACT-008 | DOC-v1.1-01 §8.17.1 EMP-05 | Tài khoản **chưa có đơn nào đang chạy** | Mở "Đơn của tôi" → tab đang-chạy | Hiện **đúng chuỗi** "Không có đơn đang thực hiện" **và có đúng 1 CTA** nhãn "Đăng tin gửi hàng"; kèm icon nét mảnh màu neutral + 1 dòng giải thích (`BR17-01`) | P2 | UI | MODIFIED |
| SC-ACT-014 | Empty state tab "Hoàn tất" — text + **ẩn khối lịch sử** *(hết gap)* | REQ-ACT-008 | DOC-v1.1-01 §8.17.1 EMP-06 | Tài khoản **chưa có đơn hoàn tất nào** | Mở "Đơn của tôi" → tab hoàn-tất | Hiện **đúng chuỗi** "Chưa có đơn hoàn tất"; **KHÔNG có CTA** (khác hẳn tab kia); **khối lịch sử bị ẩn hẳn**, không hiện khung rỗng | P2 | UI | MODIFIED |
| SC-ACT-001 | Hai tab + tên màn — nhãn theo app *(hết ghi nhận 2026-09-16)* | REQ-ACT-001 | DOC-v1.1-01 §8.17.1 EMP-05/EMP-06 · §6.2 AC-09.1.01 · BA trả lời `C-ACT-02` 2026-09-16 | Đã đăng nhập, bấm tab **"Hoạt động"** ở bottom nav | Đọc tiêu đề màn, số lượng tab và nhãn từng tab | Tiêu đề màn **"Đơn của tôi"**; có đúng **2 tab** nhãn **"Đang diễn ra"** và **"Đã hoàn thành"**; nhãn bottom nav là **"Hoạt động"** (PRD ghi "Đang chạy"/"Hoàn tất" là **PRD chưa cập nhật** — ⛔ không assert theo PRD) | P2 | UI | MODIFIED |
| SC-ACT-005 | Data tab kết thúc — gồm cả EXPIRED và RETURNED | REQ-ACT-004 | DOC-v1.1-01 §6.2 AC-09.1.01 · AC-24.2.01 | Tài khoản có đủ 3 loại đơn kết thúc: `COMPLETED` · `EXPIRED` · `RETURNED` | Mở tab kết thúc, đối chiếu từng đơn | Cả **3 loại** đều hiện trong tab này; đơn `EXPIRED` có badge "Hết hạn" (`AC-09.1.01` chốt vị trí là tab kết thúc), đơn `RETURNED` có lý do hoàn hàng | P2 | Functional | MODIFIED |
| SC-ACT-008 | Card "Hết hạn" — lý do đúng chuỗi chính thức | REQ-ACT-005 | DOC-v1.1-01 §8.5.1 BR05-03 · §6.2 AC-09.1.01 | Có 1 tin NEED quá "Đến ngày" mà **vẫn ở POSTED** (chưa ai ghép) | Mở tab kết thúc, mở card của tin đó | Badge "Hết hạn" kèm **đúng chuỗi** lý do "Không có ai nhận mang giúp trong thời gian đăng" | P3 | UI | MODIFIED |
| SC-ACT-013 | ★★★★★ leftover trên card — nay là defect | REQ-ACT-009 | DOC-v1.1-01 §8.14.1 BR14-03 · §4 SCOPES Out of Scope | Tab kết thúc có ≥ 1 đơn `COMPLETED` | Rà toàn bộ card đơn ở tab kết thúc | **KHÔNG** có ★/điểm/tier/chỉ số môi trường trên card. ⚠ Nếu còn ★ → **log bug** (`BR14-03` + §4 loại trừ vĩnh viễn), ⛔ KHÔNG diễn giải là "dấu vết phase sau" | P2 | Business Rule | MODIFIED |

#### Source Detail per Scenario (verbatim quotes)

##### SC-ACT-015 — Kết cục `RETURNED` hiện kèm lý do, đối chứng với `CANCELLED` bị ẩn
📍 `DOC-v1.1-01 §6.2 AC-24.2.01 "Đơn hoàn hàng không mở bước tặng quà" · trang 25`

> "Then: Không có nút tặng quà (không có giao dịch giúp đỡ hoàn tất). Đơn hiển thị lý do hoàn hàng và nằm trong lịch sử đơn, nhưng không cộng vào "Đơn đã giúp" của người vận chuyển."

**Analyst Note:** ⭐ **SC này tồn tại vì có cặp đối chứng, không phải vì có kết cục mới.** v1.0 đã có rule *"đơn 'Đã huỷ' bị ẩn khỏi màn Hoạt động"* (`SC-ACT-007`, nguồn `KB-ORD-07 #7`). v1.1 thêm `RETURNED` — cũng là **kết cục bất thường** — nhưng `AC-24.2.01` nói nó **nằm trong lịch sử đơn** và **hiện lý do**. Hai hành vi ngược nhau cho hai trạng thái gần giống nhau ⇒ đây đúng là chỗ dev dễ gộp thành một nhánh *"đơn kết thúc bất thường thì ẩn"*, và khi đó đơn hoàn hàng biến mất khỏi lịch sử mà **người dùng không có cách nào biết hàng đã về đâu**. ⇒ Given bắt buộc có **cả 2 đơn** để so trong 1 lượt, ⛔ không tách thành 2 SC rời. ⚠️ Phần *"không cộng vào Đơn đã giúp"* có home ở `GIFT` (`SC-GIFT-014`), ⛔ không nhân bản.

---

##### SC-ACT-016 / SC-ACT-017 — Rule hình thức chung của `FR17` (home cross-cutting đặt tại đây)
📍 `DOC-v1.1-01 §8.17.2 BR17-01..03 · trang 51` · `§8.17 dòng Pre-Conditions · trang 50` · `§6.2 AC-29.1.01 · trang 28`

> `BR17-02`: "Không dùng ảnh minh hoạ nặng; không hiện skeleton vô hạn — phân biệt rõ đang tải và không có dữ liệu."

> `BR17-03`: "Empty state không được che thanh tab dưới và vẫn cuộn được."

> `FR17` Pre-Conditions: "Cờ dữ liệu rỗng của khu vực đó bằng true (không dựa vào null của từng field)"

**Analyst Note:** `FR17` có **2 tầng**: *danh mục text* (8 dòng `EMP-01..08`, chia về từng module) và *rule hình thức* (`BR17-01..03` + điều kiện hiển thị, **chung cho cả 8**). Nếu mỗi module tự assert tầng 2 thì sinh **8 bản sao của cùng 1 rule** — vi phạm nguyên tắc 1-quote-1-home và tạo 8 chỗ để drift. ⇒ Gom về `ACT` vì đây là màn **duy nhất có 2 empty state cạnh nhau** (mỗi tab một cái), kiểm được `BR17-03` + bất đối xứng CTA trong 1 lượt. ⚠️ `SC-ACT-017` gắn nhãn `[GAP]` có chủ đích: *"cờ dữ liệu rỗng, không dựa vào null của từng field"* là **rule cài đặt phía backend** — qua UI chỉ quan sát được **triệu chứng** (skeleton vô hạn / nhảy giữa loading và empty), ⛔ không verify được rule gốc. Theo `Project_rule §Custom Rules §10.1` bước 3: ghi nhận, không viết TC khẳng định. Cần **throttle mạng** để quan sát — ghi ở `test_data_catalog.md`.

---

##### SC-ACT-012 / SC-ACT-014 — `EMP-05` / `EMP-06`: text chính thức và **bất đối xứng CTA**
📍 `DOC-v1.1-01 §8.17.1 bảng Danh mục empty state · trang 51`

> ↪ *Quote `EMP-05` — home ở `requirement_traceability.md` · `REQ-ACT-008` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

> ↪ *Quote `EMP-06` — home ở `requirement_traceability.md` · `REQ-ACT-008` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

**Analyst Note (diff):** ⭐ **Đây là chỗ `C-ORD-06` được đóng, và home canonical của CL đó chính là module này.** CL từng `Resolved 2026-07-28` rồi **REVERT 2026-07-29** vì lần chốt không kèm bằng chứng — nay nguồn là tài liệu đã phê duyệt, liệt kê đủ 8 dòng ⇒ bền. Hai SC hết `[GAP]`, nâng **P3 → P2** (từ *ghi nhận text là gì* sang *assert verbatim*). **Hai bất đối xứng bắt buộc phải assert:** (a) `EMP-05` **có** CTA `"Đăng tin gửi hàng"`, `EMP-06` **không** có — hai tab cạnh nhau khác nhau có chủ đích, và `BR17-01` viết *"tối đa một CTA"* nên "không có" là lựa chọn hợp lệ chứ không phải thiếu; (b) `EMP-06` có mệnh đề riêng **"ẩn luôn khối lịch sử"** — hành vi **ngoài** cấu trúc chuẩn `BR17-01`, chỉ tab này có, và là thứ dễ bị bỏ sót nhất (khung rỗng vẫn hiện thì trông "gần đúng"). ⚠️ Nhãn tab trong 2 dòng này là **"Đang chạy"/"Hoàn tất"** — xung đột với app, xem `SC-ACT-001` và `C-ACT-02`; 2 SC này **assert text bên trong empty state**, không assert nhãn tab.

---

##### SC-ACT-001 — Nhãn 2 tab: theo app *(BA chốt 2026-09-16)*
📍 `DOC-v1.1-01 §8.17.1 EMP-05 / EMP-06 · trang 51` · `§6.2 AC-09.1.01 · trang 19`

> `EMP-05`: "Đơn của tôi — tab **Đang chạy**" · `EMP-06`: "Đơn của tôi — tab **Hoàn tất**"

> ↪ *Quote `AC-09.1.01` — home ở `risk_assessment.md` · `C-ACT-02` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

**Analyst Note (diff):** PRD dùng **"Đang chạy" / "Hoàn tất"** nhất quán ở **3 chỗ độc lập** ⇒ không phải lỗi đánh máy. App STG (`KB-ORD-07`, quan sát 2026-07-27) hiển thị **"Đang diễn ra" / "Đã hoàn thành"**. Theo `Project_rule §Custom Rules §10.1` — *UI phải khớp Tài liệu mới được viết TC* — ⛔ **không được tự chọn bên nào**: chọn PRD ⇒ TC FAIL hàng loạt trên app hiện tại vì lý do không phải bug nghiệp vụ; chọn app ⇒ hợp thức hoá việc app lệch đặc tả đã phê duyệt. ⇒ SC giữ phần **chắc chắn** (*có đúng 2 tab*) và **hạ phần nhãn xuống ghi nhận**, mở `C-ACT-02`. Cùng vấn đề với **tên màn**: PRD gọi *"Đơn của tôi"*, v1.0 ghi nhận bottom nav là *"Hoạt động"* còn tiêu đề trong màn là *"Đơn của tôi"*.

⛔ **Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC, đừng trích lại:** BA chốt nhãn **theo app** (`C-ACT-02` Resolved) — Then hiện hành ở bảng SC phía trên: tiêu đề "Đơn của tôi", tab "Đang diễn ra"/"Đã hoàn thành", nav "Hoạt động".

---

##### SC-ACT-005 / SC-ACT-008 — Tab kết thúc chứa 3 loại đơn; lý do "Hết hạn" có chuỗi verbatim
📍 `DOC-v1.1-01 §6.2 AC-09.1.01 · trang 19` · `§8.5.1 BR05-03 · trang 38` · `§6.2 AC-24.2.01 · trang 25`

> `AC-09.1.01`: "Tin chuyển sang EXPIRED, biến khỏi bảng tin và khỏi luồng khớp tuyến. Hiện badge "Hết hạn" ở tab Hoàn tất kèm lý do "Không có ai nhận mang giúp trong thời gian đăng"."

> `BR05-03`: "Hết ngày cuối của khoảng ngày mà đơn vẫn POSTED thì chuyển EXPIRED; hiện badge "Hết hạn" kèm lý do "Không có ai nhận mang giúp trong thời gian đăng"."

**Analyst Note (diff):** Hai bổ sung so với v1.0. **(1) Vị trí:** `AC-09.1.01` chốt đơn `EXPIRED` nằm ở **tab kết thúc** — v1.0 biết có badge "Hết hạn" (`KB-ORD-07 #4,#6`) nhưng **không chắc nó ở tab nào**, nên `SC-ACT-005` chỉ assert chung chung. **(2) Chuỗi lý do:** nay là text chính thức, lặp giống hệt ở 2 chỗ (`BR05-03` + `AC-09.1.01`) ⇒ `SC-ACT-008` assert verbatim thay vì *"có kèm lý do"*. ⚠️ `BR05-03` thêm vế **"mà đơn **vẫn POSTED**"** — đơn đã `MATCHED` thì **không** chuyển `EXPIRED` dù quá ngày; v1.0 chưa nêu, và đây là ô dễ sai (dev hay kiểm mỗi ngày hết hạn). Ngưỡng `EXPIRED` = *"Đến ngày"* đã Resolved từ `C-ORD-03` (v1.0) — PRD **xác nhận lại**, không đảo.

---

##### SC-ACT-013 — ★ leftover: từ `[GAP]` thành defect
📍 `DOC-v1.1-01 §8.14.1 BR14-03 · trang 49` · `§4 SCOPES dòng Out of Scope · trang 9`

> `BR14-03`: "Không có chấm sao 1–5, không điểm, không tier/xếp hạng, không chỉ số môi trường."

> §4 Out of Scope: "Đánh giá sao 1–5 và mọi hình thức xếp hạng/tier/điểm thưởng — thay bằng quà ảo"

**Analyst Note (diff):** 🔴 **Hành vi không đổi, phân loại đổi.** `C-GIFT-01` (v1.0) chốt *"out of scope **v1.0**"* — hai chữ "v1.0" khiến ★ leftover đọc được thành *"tính năng phase sau lộ sớm"* ⇒ SC gắn `[GAP]`, **không log bug**. v1.1 loại trừ **vĩnh viễn** (§4, *"thay bằng quà ảo"*) ⇒ ★ còn sót **là defect**, đủ căn cứ log. Nâng **P3 → P2**. Home phán quyết ở `GIFT` (`C-GIFT-01`), ở đây chỉ **áp dụng** — ⛔ không tạo CL trùng.

---

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| SC-ACT-002 | Tab mặc định | ACT | v1.0 | P2 | → `v1.0/ACT-hoat-dong/test_scenario_map.md` — PRD không nêu tab nào mặc định |
| SC-ACT-003 | Cơ chế switch tab | ACT | v1.0 | P3 | → như trên |
| SC-ACT-004 | Data tab đang-chạy | ACT | v1.0 | P2 | → như trên |
| SC-ACT-006 | Completeness card đơn | ACT | v1.0 | P2 | → như trên |
| SC-ACT-007 | Đơn "Đã huỷ" bị ẩn | ACT | v1.0 | P2 | → như trên — ⭐ dùng làm **đối chứng** cho `SC-ACT-015`. ⚠️ **2026-09-16:** PRD §8.12.3 cho mọi vai *"Xem lý do"* đơn CANCELLED ⇒ rule *"ẩn"* có thể hết hiệu lực — chờ `C-ACT-04` |
| SC-ACT-009 | Card "Hết hạn" không thao tác được | ACT | v1.0 | P3 | → như trên — ⚠️ **2026-09-16:** PRD §8.12.3 + `NTF-09` nói *"xem lý do · đăng lại"* ⇒ card có thể phải mở được — chờ `C-ACT-03` / `C-ORD-17` |
| SC-ACT-010 | Tap card (≠ Hết hạn) | ACT | v1.0 | P2 | → như trên |
| SC-ACT-011 | Đích tap card = "Theo dõi đơn" *(hết gap 2026-09-16)* | ACT | v1.0 | P3 | `C-ACT-01` Resolved qua demo + **BA xác nhận 2026-09-16**: tab Đang diễn ra → **"Theo dõi đơn"**; tab Đã hoàn thành, đơn **chưa tặng quà** (vai Sender) → màn **"Tặng quà"**. Các ô còn lại chờ `C-ACT-03` |

> ℹ️ **8 SC CARRIED** — `SC-ACT-001` `005` `008` `012` `013` `014` KHÔNG ở bảng này vì đã MODIFIED (xem §NEW & MODIFIED ở trên).

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
