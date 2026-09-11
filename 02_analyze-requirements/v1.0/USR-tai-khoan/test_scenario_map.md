---
id: v1.0/USR-tai-khoan/scenario-map
title: Test Scenario Map — v1.0 · Module USR
type: scenario-map
version: v1.0
sprint: 1
module: USR
counts:
  req: 7
  sc: 12
  new: 12
  modified: 0
  carried: 0
  deprecated: 0
  p1: 1
  p2: 5
  p3: 6
status: ANALYZED
updated: 2026-09-07
---

# Test Scenario Map — v1.0 · Module USR

> **Home của SC quote** (1 quote = 1 nơi): Source Quote per SC ở §"Source Detail per Scenario" file này.
> REQ quote → `requirement_traceability.md §2` · Clarification quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` của file này là **nguồn canonical** của số REQ/SC/lifecycle/priority module USR.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Sàn tối thiểu/REQ: ≥1 positive + ≥1 negative (nếu có rule) + boundary (nếu có input range).
> Fan-out mỗi role/quyền · mỗi state-transition · mỗi lớp EP · mỗi boundary · mỗi nhánh lỗi = 1 SC riêng.
> Trần: display-only/Phase-2/duplicate → ghi `coverage-gap-report.md`, KHÔNG tạo SC rác.

## Tổng quan
- Tổng số scenarios: **12** (NEW: 12, MODIFIED: 0, CARRIED: 0, DEPRECATED: 0)
- Phân bổ priority: P1: 1 | P2: 5 | P3: 6
- Module là **bề mặt view-only** ⇒ không có state-transition; fan-out chủ yếu theo **lớp hiển thị** và **nhánh negative** (trường doc có mà UI không có).

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### USR — Tài khoản & Hồ sơ

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-USR-001 | Đăng nhập SSO | REQ-USR-001 | DOC-v1.0-01 §A6 | CBNV có tài khoản SSO nội bộ FPT hợp lệ, đã đăng nhập host app FoxPro | Mở SDK FoxEco từ host app | Vào được FoxEco với đúng danh tính CBNV (tên/phòng ban/MNV khớp hồ sơ nhân viên) | P1 | Functional | NEW |
| SC-USR-002 | Hồ sơ cá nhân | REQ-USR-002 | DOC-v1.0-01 §A6 · DOC-v1.0-04 | Đã vào FoxEco bằng tài khoản có hồ sơ đầy đủ | Mở tab "Cá nhân" | Hiển thị đủ các trường hồ sơ đọc được: avatar, tên, phòng ban, MNV | P2 | UI | NEW |
| SC-USR-003 | Hồ sơ view-only | REQ-USR-002 | DOC-v1.0-06 KP-01 §2 KB-USR-01 | Đang ở màn Cá nhân | Rà toàn bộ màn tìm control sửa hồ sơ (nút Sửa/icon bút/tap vào field) | KHÔNG có bất kỳ control sửa nào; mọi trường chỉ đọc | P2 | Business Rule | NEW |
| SC-USR-004 | Định danh & tin cậy | REQ-USR-003 | DOC-v1.0-01 §A6 · DOC-v1.0-02 §1.1 | Tài khoản thuộc 1 phòng ban + có MNV trong hồ sơ nhân viên | Mở màn Cá nhân | Phòng ban + MNV hiển thị đúng giá trị hồ sơ, theo định dạng "<Phòng ban> · MNV: <mã>" | P2 | UI | NEW |
| SC-USR-005 | Chỉ số đóng góp | REQ-USR-004 | DOC-v1.0-01 §A6 L102 · §A7 | Tài khoản đã giúp N đơn và đã nhận M quà | Mở màn Cá nhân | Card chỉ số hiển thị đúng 2 số: "đơn đã giúp" = N, "quà đã nhận" = M | P2 | Business Rule | NEW |
| SC-USR-006 | Loại trừ điểm/tier/CO₂ | REQ-USR-004 | DOC-v1.0-01 §A7 L111 | Đang ở màn Cá nhân | Rà toàn bộ màn tìm "Điểm ECO" / "Điểm uy tín" / chỉ số CO₂ | KHÔNG hiển thị bất kỳ chỉ số nào trong 3 loại đó (out of scope v1.0 — C-USR-01) | P2 | Business Rule | NEW |
| SC-USR-007 | Badge hạng thành viên | REQ-USR-007 | DOC-v1.0-04 ảnh 570ad9d3… · DOC-v1.0-02 §3.9 | Đang ở màn Cá nhân | Quan sát badge hạng thành viên | Hiển thị badge pill dạng text "Hạng Đồng hành"; KHÔNG kèm điểm số, KHÔNG có hành vi đổi hạng | P3 | UI | NEW |
| SC-USR-008 | Điều hướng "Đơn của tôi" | REQ-USR-006 | DOC-v1.0-02 §3.9 · DOC-v1.0-06 KP-01 §2 KB-USR-04 | Đang ở màn Cá nhân | Bấm menu "Đơn của tôi" | Điều hướng sang màn Hoạt động (tab mặc định "Đang diễn ra") | P3 | Functional | NEW |
| SC-USR-009 | Điều hướng "Quà đã nhận" | REQ-USR-006 | DOC-v1.0-01 §D1b US-D20 · DOC-v1.0-04 | Đang ở màn Cá nhân | Bấm menu "Quà đã nhận" | Điều hướng sang màn "Quà đã nhận" (nội dung màn thuộc module GIFT — xem SC-GIFT-006..009) | P3 | Functional | NEW |
| SC-USR-010 | [GAP] Cấu hình kênh liên hệ | REQ-USR-005 | DOC-v1.0-01 §A6 L103 | BRD USR-07 yêu cầu có màn cấu hình kênh liên hệ sẽ lộ | Rà màn Cá nhân + toàn bộ menu con | GHI NHẬN GAP: không tồn tại bề mặt cấu hình kênh liên hệ trên app v1.0 (C-USR-02 — Out of scope). KHÔNG assert hành vi giả định | P3 | Business Rule | NEW |
| SC-USR-011 | Completeness header | REQ-USR-007 | DOC-v1.0-04 ảnh 570ad9d3…, e5764b10… | Đang ở màn Cá nhân | Đối chiếu từng thành phần header với ảnh Figma | Đủ và đúng vị trí: avatar · tên · phòng ban+MNV · badge hạng · card 2 chỉ số · 2 mục menu | P3 | UI | NEW |
| SC-USR-012 | [GAP] Nhãn menu thứ hai | REQ-USR-006 | DOC-v1.0-02 §3.9 vs DOC-v1.0-01 US-D20 | 3 nguồn ghi 3 nhãn khác nhau cho mục menu thứ hai | Quan sát nhãn thật của mục menu thứ hai trên app | GHI NHẬN: nhãn hiện hành theo BRD+Figma là "Quà đã nhận"; nếu app hiện "Đánh giá đã nhận" → báo về C-USR-04, KHÔNG tự chọn nhãn | P3 | UI | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-USR-001 — Đăng nhập SSO thành công vào SDK FoxEco

**Source Quote:**
> "USR-01 | Đăng nhập SSO nội bộ FPT → JWT, role, profile"

**Source Location:** `DOC-v1.0-01 §A6 "Tài khoản & Hồ sơ (USR)" · bảng ID/Yêu cầu · L99`

**Analyst Note:** Given/When/Then thiết kế theo **hệ quả quan sát được**, không theo bước SSO — vì bề mặt đăng nhập thuộc host app FoxPro (`DOC-v1.0-06` KP-03 §1), tester không tác động trực tiếp được. Oracle = danh tính hiển thị đúng ở màn Cá nhân. Cross-ref `REQ-USR-003` (phòng ban/MNV), `RISK-USR-01`.

##### SC-USR-002 — Màn Cá nhân hiển thị các trường hồ sơ

**Source Quote:**
> "USR-02 | Xem/cập nhật hồ sơ: tên, SĐT, avatar, phòng ban, khu vực/văn phòng, kênh liên hệ"

**Source Location:** `DOC-v1.0-01 §A6 · bảng ID/Yêu cầu · L100`

**Analyst Note:** Doc liệt kê 6 trường nhưng **SĐT · khu vực/văn phòng · kênh liên hệ chưa có bằng chứng UI** (Figma chỉ xác nhận avatar/tên/phòng ban/MNV — `DOC-v1.0-06` KP-01 §2 KB-USR-02). Theo `§Custom Rules §10.1`, Then **chỉ assert 4 trường có bằng chứng 2 nguồn**; 2 trường còn lại đưa về `coverage-gap-report` + `C-USR-04`. ⛔ KHÔNG assert "hiển thị đủ 6 trường".

##### SC-USR-003 — Không có control sửa hồ sơ (negative)

**Source Quote:**
> "**Thực tế app STG KHÔNG có bất kỳ chức năng cập nhật/sửa nào** — cả 6 trường đều chỉ để xem."

**Source Location:** `DOC-v1.0-06 KP-01 §2 "KB-USR-01" · dòng 2`

**Analyst Note:** SC negative sinh từ mâu thuẫn doc↔UI đã được `C-USR-03` Resolved theo hướng UI. Đây là SC **bảo vệ kết luận**: nếu lượt sau app xuất hiện nút Sửa thì SC này FAIL và buộc mở lại clarification, thay vì im lặng viết TC edit profile.

##### SC-USR-004 — Phòng ban + MNV đúng hồ sơ nhân viên

**Source Quote:**
> "mỗi tài khoản gắn với Phòng ban và Mã nhân viên (MNV) — ví dụ "Phòng Kỹ thuật · MNV: FTEL2291""

**Source Location:** `DOC-v1.0-02 §1.1 "Bối cảnh & vấn đề" · đoạn 1`

**Analyst Note:** Định dạng `"<Phòng ban> · MNV: <mã>"` lấy từ ví dụ trong PRD — **là ví dụ minh hoạ, không phải đặc tả format**, nên Then assert *nội dung đúng* + *có cả 2 thành phần*, không assert dấu phân cách cứng. Giá trị thật của tài khoản test xác nhận lại ở vibe-test.

##### SC-USR-005 — Đúng 2 chỉ số đóng góp

**Source Quote:**
> "USR-05 | Hiển thị tổng số đơn đã giúp + tổng số quà ảo đã nhận (không tính điểm/CO₂)"

**Source Location:** `DOC-v1.0-01 §A6 · bảng ID/Yêu cầu · L102`

**Analyst Note:** Given cần tài khoản có N đơn đã giúp / M quà — là **Fixture phụ thuộc lịch sử đơn**, không seed nhanh được (xem `RISK-USR-03`). Cách khả thi: đọc giá trị hiện tại rồi verify **tăng đúng 1** sau khi hoàn tất 1 đơn / nhận 1 quà, thay vì assert số tuyệt đối.

##### SC-USR-006 — Không hiển thị Điểm ECO / Điểm uy tín / CO₂ (negative)

**Source Quote:**
> "Không tính điểm, không tier/xếp hạng, không CO₂, không quy đổi tiền / thanh toán in-app"

**Source Location:** `DOC-v1.0-01 §A7 "Phần thưởng — Quà ảo" · bullet 5 · L111`

**Analyst Note:** SC negative chốt mâu thuẫn BRD↔PRD demo (`C-USR-01` Resolved — deferred). Nếu app STG **có** hiện Điểm ECO/uy tín thì đó là UI leftover của bản demo ⇒ báo finding, KHÔNG tự sửa kết luận. Cross-ref `SC-USR-007` (badge được giữ), `SC-ACT-013` (★★★★★ leftover ở card Hoàn thành).

##### SC-USR-007 — Badge hạng thành viên là text tĩnh

**Source Quote:**
> "**CÓ** badge pill `🏆 Hạng Đồng hành` (dạng text)"

**Source Location:** `DOC-v1.0-06 KP-01 §2 "KB-USR-02" · bullet 1`

**Analyst Note:** Badge là **ngoại lệ có chủ đích** của `C-USR-01`: cơ chế tier bị defer nhưng badge text vẫn hiển thị. Then vì thế assert *sự tồn tại + nội dung text*, ⛔ không assert logic đổi hạng theo số đơn.

##### SC-USR-008 — Menu "Đơn của tôi" → màn Hoạt động

**Source Quote:**
> "Menu | "Đơn của tôi" (→ Hoạt động) · "Đánh giá đã nhận" (không có phản hồi khi bấm trong bản demo)"

**Source Location:** `DOC-v1.0-02 §3.9 "Màn hình Cá nhân" · bảng Trường/Thành phần · dòng "Menu"`

**Analyst Note:** Đích điều hướng là màn Hoạt động (module `ACT`) ⇒ Then chỉ assert **đến đúng màn + tab mặc định**, nội dung màn verify ở `SC-ACT-001..003`. Tránh 2 SC cùng assert 1 nội dung.

##### SC-USR-009 — Menu "Quà đã nhận" → màn Quà đã nhận

**Source Quote:**
> "Trang cá nhân có mục "Đơn đã giúp" & "Quà đã nhận"; màn Quà đã nhận hiển thị 1 card đếm số bông hoa/ly cà phê/gấu bông/vương miện + danh sách lịch sử nhận quà"

**Source Location:** `DOC-v1.0-01 §D1b "Nhóm 4 — Hoàn tất, đánh giá & ngoài luồng chính" · US-D20 · L196`

**Analyst Note:** SC này chỉ phủ **hành vi điều hướng**; nội dung màn "Quà đã nhận" (card đếm có điều kiện, lịch sử, icon back) thuộc `GIFT` — `SC-GIFT-006..009`. `US-D20` gọi mục thứ nhất là *"Đơn đã giúp"* trong khi PRD gọi *"Đơn của tôi"* ⇒ ghi vào `C-USR-04`.

##### SC-USR-010 — [GAP] Không tồn tại màn cấu hình kênh liên hệ

**Source Quote:**
> "USR-07 | Cấu hình kênh liên hệ sẽ lộ: SĐT (bắt buộc), Workplace/email (tùy chọn)"

**Source Location:** `DOC-v1.0-01 §A6 · bảng ID/Yêu cầu · L103`

**Analyst Note:** SC dạng **GAP finding** theo `§Custom Rules §10.1` bước 3 — ghi nhận sự thiếu vắng thay vì test hành vi giả định. `C-USR-02` Resolved (Out of scope v1.0) ⇒ SC này **không phải bug**, chỉ là chốt trạng thái để version sau (nếu `USR-07` vào scope) biết đây là điểm khởi đầu.

##### SC-USR-011 — Completeness header màn Cá nhân

**Source Quote:**
> "Card trắng chỉ có 2 số liệu: `12 — đơn đã giúp`, `8 — quà đã nhận`; menu: `Đơn của tôi`, `Quà đã nhận`"

**Source Location:** `DOC-v1.0-06 KP-01 §2 "KB-USR-02" · bullet 3`

**Analyst Note:** SC completeness đối chiếu **cấu trúc** màn với 2 ảnh Figma; **⛔ không assert giá trị số** (12/8 là dữ liệu mẫu của ảnh, không phải đặc tả). Đây là ranh giới hay bị vi phạm nhất khi viết TC completeness từ ảnh mockup.

##### SC-USR-012 — [GAP] 3 nguồn 3 nhãn cho mục menu thứ hai

**Source Quote:**
> "Menu | "Đơn của tôi" (→ Hoạt động) · "Đánh giá đã nhận" (không có phản hồi khi bấm trong bản demo)"

**Source Location:** `DOC-v1.0-02 §3.9 · bảng Trường/Thành phần · dòng "Menu"` (đối chiếu `DOC-v1.0-01 §D1b US-D20 · L196`)

**Analyst Note:** PRD ghi *"Đánh giá đã nhận"*, BRD `US-D20` + Figma ghi *"Quà đã nhận"*. Nhãn *"Đánh giá"* thuộc nhánh rating đã bị `C-GIFT-01` loại khỏi v1.0 ⇒ chọn **"Quà đã nhận"**, nhưng vẫn giữ SC ghi nhận để nếu app hiện nhãn khác thì có chỗ báo về (`C-USR-04`).

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| — | *(không có — v1.0 là version đầu của chuỗi phân tích mới)* | — | — | — | — |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
