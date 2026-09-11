---
id: v1.0/TS-trust-safety/scenario-map
title: Test Scenario Map — v1.0 · Module TS
type: scenario-map
version: v1.0
sprint: 1
module: TS
counts:
  req: 5
  sc: 7
  new: 7
  modified: 0
  carried: 0
  deprecated: 0
  p1: 1
  p2: 2
  p3: 4
status: ANALYZED
updated: 2026-09-07
---

# Test Scenario Map — v1.0 · Module TS

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module TS.
> ⚠️ Module **phần lớn backend/Admin** ⇒ 4/7 SC là dạng `[GAP]`/assert-absent; phạm vi test = **hệ quả quan sát được từ phía end-user**.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Fan-out mỗi role · state-transition · lớp EP · boundary · nhánh lỗi = 1 SC.
> Trần: display-only/Phase-2/duplicate → `coverage-gap-report.md`. Chấm sao đã có SC ở `GIFT` ⇒ ⛔ không nhân bản.

## Tổng quan
- Tổng số scenarios: **7** (NEW: 7, MODIFIED: 0, CARRIED: 0, DEPRECATED: 0)
- Phân bổ priority: P1: 1 | P2: 2 | P3: 4
- **SC P1 duy nhất (`SC-TS-003`) là rule bị app vi phạm rõ nhất của cả dự án:** log audit phải **bất biến** nhưng huỷ nhận đơn **XOÁ** dòng log đã ghi.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### TS — Trust & Safety

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-TS-001 | Log đủ mốc + timestamp | REQ-TS-001 | DOC-v1.0-01 §A8 TS-01 L121 · §D3 ORD-04 L243 | 1 đơn đã đi trọn vòng đời tới "Hoàn thành" (đi thẳng, không qua huỷ) | Mở block LỊCH SỬ ở màn Theo dõi đơn | Có đủ mốc từ "Đăng tin" tới "Hoàn thành", **mỗi mốc kèm timestamp** | P2 | Functional | NEW |
| SC-TS-002 | Log ghi rõ actor | REQ-TS-001 | DOC-v1.0-01 §A8 TS-01 L121 | 1 đơn đã qua nhiều lần đổi trạng thái bởi các vai khác nhau | Đối chiếu từng mốc trong LỊCH SỬ với vai đã thực hiện | Mỗi mốc ghi rõ **ai thực hiện** (ai đăng · ai nhận · ai đổi trạng thái) | P2 | Functional | NEW |
| SC-TS-003 | [GAP·bug] Log bất biến (audit trail) | REQ-TS-002 | DOC-v1.0-01 §A8 TS-02 L122 · §A5 BR-INT-04 L80 · KP-01 §7 KB-CNL-01 | 1 đơn có LỊCH SỬ đã ghi ≥2 mốc (gồm "Ghép thành công") | Thực hiện các hành động có thể làm thay đổi lịch sử: **huỷ nhận đơn** (Carrier), huỷ đơn, sửa tin (nếu còn ở Chờ ghép) | Mọi dòng log đã ghi **VẪN CÒN NGUYÊN**, không dòng nào bị xoá/sửa. ⚠ Dự kiến FAIL — huỷ nhận đơn hiện **XOÁ** dòng "Ghép thành công" → log bug (vi phạm `TS-02`+`BR-INT-04`) | P1 | Business Rule | NEW |
| SC-TS-004 | Consent điều khoản trước khi đăng | REQ-TS-004 | DOC-v1.0-01 §A8 L115 · §D3 ORD-09 L245 | Rule `§A8` yêu cầu consent **trước khi đăng VÀ trước khi ghép** | Rà cả 2 luồng: đăng tin (NEED wizard B3 + form OFFER) và ghép ("Tôi mang giúp được") | Luồng **đăng tin**: có checkbox điều khoản bắt buộc (cả NEED và OFFER). Luồng **ghép**: GHI NHẬN chỉ có modal xác nhận lộ SĐT, ⛔ KHÔNG assert có checkbox điều khoản | P3 | Business Rule | NEW |
| SC-TS-005 | [GAP] Không có cơ chế chặn user | REQ-TS-005 | DOC-v1.0-01 §A8 L125 | `§A8` khai rõ phạm vi v1.0: *"KHÔNG có chặn (block) người dùng"* | Rà toàn app tìm chức năng báo cáo/chặn/ẩn người dùng (Chi tiết tin · Theo dõi đơn · Cá nhân) | GHI NHẬN GAP: không tồn tại cơ chế chặn/báo cáo người dùng ở v1.0 (đúng phạm vi). ⛔ KHÔNG viết TC chặn user | P3 | Business Rule | NEW |
| SC-TS-006 | [GAP] Hệ quả "admin hỗ trợ" | REQ-TS-003 | DOC-v1.0-01 §A8 TS-03 L123 · §D4 BR-CNF-04 L266 | Đơn ở "Đã giao"; Receiver không xác nhận quá 4 giờ (2 giờ nhắc + 2 giờ) | Quan sát trạng thái/thông báo phía end-user sau 4 giờ | GHI NHẬN hệ quả quan sát được từ phía user (chuyển "admin hỗ trợ" / thông báo tương ứng). ⚠ Cùng tiền đề `SC-DLV-024` — chạy 1 lần lấy dữ liệu cho cả 2; chưa chạy đủ mốc thì GHI RÕ | P3 | Business Rule | NEW |
| SC-TS-007 | [GAP] Admin Web Portal không có bề mặt test | REQ-TS-003 | DOC-v1.0-06 KP-01 §9 KB-TS-01 · C-TS-01 | `§A3` nhắc tên *"Admin Web Portal"* nhưng không mô tả màn hình/field nào | Rà tài liệu + app tìm bề mặt Admin thuộc phạm vi test v1.0 | GHI NHẬN GAP: không có đặc tả UI Admin ⇒ out of scope v1.0 (C-TS-01 Resolved); cột `Admin` trong permission matrix `§D4` **không test được** | P3 | Business Rule | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-TS-001 / SC-TS-002 — Log đủ mốc + timestamp · ghi rõ actor

**Source Quote:**
> "TS-01 | Ghi log toàn bộ tương tác: ai đăng, ai nhận, mốc thời gian, đổi trạng thái, huỷ (kèm lý do + ai huỷ)"

**Source Location:** `DOC-v1.0-01 §A8 "Trust & Safety (chung)" · bảng ID/Yêu cầu · L121`

**Analyst Note:** `TS-01` liệt kê **5 nhóm thông tin phải log** ⇒ tách 2 SC theo 2 trục kiểm được từ phía user: **mốc + timestamp** (`SC-TS-001`) và **actor** (`SC-TS-002`). ⚠️ Bề mặt quan sát duy nhất = block **LỊCH SỬ** ở màn Theo dõi đơn ⇒ trùng bề mặt với `SC-DLV-029`, nhưng **khác góc nhìn**: `SC-DLV-029` assert *"timeline có đủ mốc đúng danh sách"* (yêu cầu hiển thị), 2 SC ở đây assert *"log có đủ thông tin audit"* (yêu cầu ghi nhận) — đặc biệt `SC-TS-002` kiểm **actor**, thứ `SC-DLV-029` không kiểm. Given yêu cầu đơn **đi thẳng tới Hoàn thành** (không qua huỷ) vì bug `SC-CNL-010` sẽ làm thiếu mốc.

##### SC-TS-003 — [GAP·bug] Log bất biến (audit trail)

**Source Quote:**
> Rule (`TS-02` §A8 L122): "Log không sửa được sau khi ghi (audit trail)"
> Rule (`BR-INT-04` §A5 L80): "Timeline tương tác không sửa được sau khi ghi (audit)"
> Hành vi (`DOC-v1.0-06` KP-01 §7 `KB-CNL-01`, live-verify 2026-07-29): "- **Huỷ nhận đơn** (Carrier) → tệ hơn: **XOÁ LUÔN dòng "Ghép thành công"** khỏi LỊCH SỬ"

**Source Location:** `DOC-v1.0-01 §A8 · TS-02 · L122` và `§A5 · BR-INT-04 · L80` ⟷ `DOC-v1.0-06 KP-01 §7 "KB-CNL-01"`

**Analyst Note:** ⭐ **SC P1 duy nhất của module, và là rule bị app vi phạm rõ nhất của cả dự án:** 2 nguồn BRD yêu cầu log **bất biến**, live-verify cho thấy log **bị xoá**. ⚠️ **Phân biệt với `SC-CNL-010`:** SC ở `CNL` nhìn từ **luồng huỷ nhận** (một hành động cụ thể); SC này nhìn từ **thuộc tính audit** — When của nó **thử nhiều hành động** (huỷ nhận · huỷ đơn · sửa tin) để xem còn hành động nào khác cũng làm thay đổi log. ⇒ Nếu `SC-CNL-010` FAIL thì SC này cũng FAIL, nhưng SC này có thể phát hiện **thêm** đường vi phạm khác. Viết theo rule ⇒ dự kiến FAIL, ⛔ không sửa expected.

##### SC-TS-004 — Consent điều khoản trước khi đăng / ghép

**Source Quote:**
> "App hiển thị điều khoản miễn trừ + **buộc consent trước khi đăng/ghép**."

**Source Location:** `DOC-v1.0-01 §A8 "Pháp lý, Trách nhiệm & Trust/Safety" · blockquote · L115`

**Analyst Note:** ⚠️ **Rule `§A8` rộng hơn thực tế triển khai:** yêu cầu consent trước khi **đăng VÀ ghép**, nhưng `ORD-09`+`D8.1`/`D8.2` chỉ có checkbox ở **luồng đăng tin**; ở luồng ghép chỉ có **modal xác nhận lộ SĐT** (`DOC-v1.0-02` §4.2) — **không phải consent điều khoản**. ⇒ Then chia 2 nhánh: **assert** consent ở luồng đăng (đã có `SC-ORD-034` cho NEED — SC này bổ sung góc nhìn cả 2 luồng NEED+OFFER), **ghi nhận** ở luồng ghép. Banner cam kết ở màn "Đăng tin mới" (`KB-ORD-10`) là **thông tin tĩnh**, ⛔ không tính là consent.

##### SC-TS-005 — [GAP] Không có cơ chế chặn user

**Source Quote:**
> "Phạm vi hiện tại: chỉ ghi log + admin can thiệp hỗ trợ. KHÔNG có chấm sao/đánh giá, **KHÔNG có chặn (block) người dùng**."

**Source Location:** `DOC-v1.0-01 §A8 · blockquote phạm vi · L125`

**Analyst Note:** Câu này **định nghĩa phạm vi module**. Vế *"chấm sao/đánh giá"* đã có SC ở `GIFT` (`SC-GIFT-011`) ⇒ ⛔ không nhân bản; vế **"chặn (block) người dùng"** chưa có SC ở module nào ⇒ SC này assert-absent. Ranh giới đáng chốt vì `TS` (Trust & Safety) thường được kỳ vọng có báo cáo/chặn user — v1.0 **chỉ có log + admin can thiệp**.

##### SC-TS-006 / SC-TS-007 — [GAP] Hệ quả "admin hỗ trợ" · Admin Portal ngoài phạm vi

**Source Quote:**
> "TS-03 | Admin có quyền can thiệp hỗ trợ khi có vướng mắc (dựa trên log)"
> (`BR-CNF-04` §D4 L266): "RECEIVER không xác nhận 2 giờ → nhắc; thêm 2 giờ → **admin hỗ trợ**"
> Phán quyết (`DOC-v1.0-06` KP-01 §9 `KB-TS-01`): "Phạm vi test v1.0 chỉ verify **hệ quả quan sát được từ phía end-user** (vd đơn quá hạn xác nhận → chuyển "admin hỗ trợ"), không test UI Admin Portal."

**Source Location:** `DOC-v1.0-01 §A8 · TS-03 · L123` · `§D4 · BR-CNF-04 · L266` ⟷ `DOC-v1.0-06 KP-01 §9 "KB-TS-01"`

**Analyst Note:** `C-TS-01` Resolved 2026-07-27: **Admin Web Portal out of scope v1.0** (`§A3` chỉ nhắc tên nền tảng, không mô tả màn/field). ⇒ `SC-TS-006` chỉ verify **hệ quả phía end-user** — **cùng tiền đề với `SC-DLV-024`** (chờ 2h + 2h) ⇒ chạy 1 lần lấy dữ liệu cho cả 2 SC, và **chưa chạy đủ mốc thì GHI RÕ**. `SC-TS-007` ghi nhận: cột `Admin` trong permission matrix `§D4` (L279-286, nhiều dòng *"✓ override"*) **hoàn toàn không test được** ở v1.0 — cần nêu rõ trong report để stakeholder không hiểu là đã phủ.

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| — | *(không có — v1.0 là version đầu của chuỗi phân tích mới)* | — | — | — | — |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
