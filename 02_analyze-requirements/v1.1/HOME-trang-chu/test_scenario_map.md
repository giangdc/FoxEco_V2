---
id: v1.1/HOME-trang-chu/scenario-map
title: Test Scenario Map — v1.1 · Module HOME
type: scenario-map
version: v1.1
sprint: 1
module: HOME
counts:
  req: 13
  sc: 27
  new: 4
  modified: 2
  carried: 21
  deprecated: 1
  p1: 1
  p2: 13
  p3: 13
status: ANALYZED
updated: 2026-09-15
---

# Test Scenario Map — v1.1 · Module HOME

> **Home của SC quote** (1 quote = 1 nơi): Source Quote per SC ở §"Source Detail per Scenario" file này.
> REQ quote → `requirement_traceability.md §2` · Clarification quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/lifecycle/priority module HOME **tính tới v1.1** (bao gồm cả CARRIED tham chiếu từ v1.0).
> Parent version: v1.0 — `02_analyze-requirements/v1.0/HOME-trang-chu/test_scenario_map.md`.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Sàn tối thiểu/REQ: ≥1 positive + ≥1 negative (nếu có rule) + boundary (nếu có input range).
> Fan-out mỗi role/quyền · mỗi state-transition · mỗi lớp EP · mỗi boundary · mỗi nhánh lỗi = 1 SC riêng.

## Tổng quan
- Tổng số scenarios (tính tới v1.1): **27** (NEW: 4, MODIFIED: 2, CARRIED: 21, DEPRECATED: 1)
- Phân bổ priority: P1: 1 | P2: 13 | P3: 13
- Delta lần này: **resolve `C-HOME-03`** (số tin mới nhất chốt = 5) + **đặc tả hoá empty state Trang chủ** (thay SC gộp `SC-HOME-024` bằng 3 SC atomic) + 1 SC hiệu năng mới (NFR01).

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### HOME — Trang chủ (delta v1.1)

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-HOME-019 | "Tin mới" — đúng 5 tin, loại trừ MATCHED/EXPIRED/của chính mình | REQ-HOME-011 | DOC-v1.1-01 §6.2 AC-11.1.01 | Trong khu vực của người dùng có 12 tin NEED ở POSTED, trong đó có ít nhất 1 tin đã MATCHED, 1 tin đã EXPIRED và 1 tin do chính người dùng đăng | Mở Trang chủ | Section "Tin mới" hiển thị **đúng 5 tin** mới nhất; tin MATCHED, EXPIRED và tin của chính người dùng **KHÔNG** nằm trong danh sách; có nút "Xem thêm trên Bảng tin" | P3 | Business Rule | MODIFIED |
| SC-HOME-021 | Nút "Xem thêm trên Bảng tin" — điều kiện hiện | REQ-HOME-011 | DOC-v1.1-01 §6.2 AC-11.1.01 · DOC-v1.0-01 §D1b US-D06 L175 | Cộng đồng có **hơn 5** tin NEED hợp lệ (đã loại MATCHED/EXPIRED/của chính mình) | Quan sát cuối section "Tin mới" | Nút "Xem thêm trên Bảng tin" hiển thị và dẫn sang màn Bảng tin; nếu tổng tin hợp lệ ≤5 thì nút KHÔNG hiện | P3 | Functional | MODIFIED |
| SC-HOME-025 | [Empty state] "Tin mới" — không có tin nào trong khu vực | REQ-HOME-011, REQ-HOME-012 | DOC-v1.1-01 §6.2 AC-11.2.01 · §8.17.1 EMP-01 | Không có tin NEED nào ở POSTED trong khu vực của người dùng | Mở Trang chủ | Section "Tin mới" hiện empty state: icon nét mảnh + "Chưa có tin nào trong khu vực của bạn" + dòng giải thích "Đăng tin để đồng nghiệp nhìn thấy nhu cầu của bạn" + CTA "Đăng tin ngay"; không hiện skeleton kéo dài | P3 | UI | NEW |
| SC-HOME-026 | [Empty state] "Đơn của tôi" — chưa có đơn đang chạy | REQ-HOME-012 | DOC-v1.1-01 §8.17.1 EMP-02 | Tài khoản không có đơn đang hoạt động | Mở Trang chủ | Section "Đơn của tôi" hiện empty state: icon nét mảnh + "Bạn chưa có đơn nào đang chạy" + CTA "Tạo đơn gửi hàng" | P3 | UI | NEW |
| SC-HOME-027 | [Empty state] Hero & cộng đồng — tài khoản/cộng đồng chưa có dữ liệu | REQ-HOME-012 | DOC-v1.1-01 §8.17.1 EMP-03 | Tài khoản mới (0 đơn đã giúp) và cộng đồng chưa có đóng góp nào | Mở Trang chủ | Hero hiện "0 · Chưa có đóng góp nào"; cụm cộng đồng hiện "0 đơn · 0 người"; **không** CTA | P3 | UI | NEW |
| SC-HOME-028 | [Performance] Thời gian hiển thị nội dung đầu Trang chủ | REQ-HOME-013 | DOC-v1.1-01 §9 NFR01 | Môi trường load-test: 1.000 người dùng đồng thời, mạng 4G | Mở Trang chủ | Nội dung đầu tiên hiển thị trong < 2 giây (p95) | P2 | Performance | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-HOME-019 — "Tin mới" đúng 5 tin, loại trừ MATCHED/EXPIRED/của chính mình

**Source Quote (old) — v1.0, `RISK-HOME-01`/`C-HOME-03`:**
> Nguồn A (`DOC-v1.0-02` §3.1): "Tin mới | Rút gọn 1 tin mới nhất của CẢ CỘNG ĐỒNG…"
> Nguồn B (`DOC-v1.0-01` §D1b US-D06 L175): "Trang chủ hiển thị đúng 5 tin mới nhất…"

**Source Quote (new) — `DOC-v1.1-01` §6.2 AC-11.1.01 · trang 19:**
> "Given: Trong khu vực của người dùng có 12 tin NEED đang ở POSTED. When: Mở trang chủ. Then: Khối 'Tin mới' hiển thị đúng 5 tin mới nhất. Có nút 'Xem thêm trên Bảng tin'. Tin đã MATCHED, EXPIRED hoặc tin của chính người dùng không nằm trong danh sách gợi ý."

**Analyst Note (diff):** v1.0 để SC này ở dạng GAP (ghi nhận số thật, không assert 1 hay 5) vì 2 nguồn mâu thuẫn không ai chốt. PRD chính thức `DOC-v1.1-01` — độc lập với cả BRD lẫn PRD-demo cũ — xác nhận **5**, RESOLVE `C-HOME-03`. Bổ sung thật sự mới (không có ở v1.0): điều kiện lọc 3 lớp (MATCHED / EXPIRED / tin của chính người dùng) — Given viết lại để có đủ 3 lớp cần loại trừ trong dữ liệu test. `test_data_catalog.md` cập nhật boundary tương ứng.

##### SC-HOME-021 — Nút "Xem thêm trên Bảng tin"

**Source Quote (old):**
> "nếu còn tin khác hiện nút 'Xem thêm trên Bảng tin' dẫn sang màn Bảng tin" (`DOC-v1.0-01` §D1b US-D06 L175) — Given viết theo quan hệ ("nhiều hơn số section hiển thị") vì số chưa chốt.

**Source Quote (new):**
> AC-11.1.01: "...Có nút 'Xem thêm trên Bảng tin'..." — ngầm định điều kiện hiện nút gắn với ngưỡng 5 tin đã chốt.

**Analyst Note (diff):** Số tin đã chốt = 5 (`SC-HOME-019`) nên Given ở đây chuyển từ quan hệ mơ hồ sang ngưỡng cụ thể "> 5 tin hợp lệ". Giữ nguyên ID vì bản chất hành vi (tap nút → sang Bảng tin) không đổi, chỉ điều kiện kích hoạt được làm rõ.

##### SC-HOME-025 — [Empty state] "Tin mới"

**Source Quote:**
> AC-11.2.01 (trang 19): "...Khối 'Tin mới' hiển thị empty state: icon nét mảnh + 'Chưa có tin nào trong khu vực của bạn' + một dòng giải thích + đúng một CTA 'Đăng tin ngay'..."
> EMP-01 (§8.17.1, trang 51): "Trang chủ — Tin mới | 'Chưa có tin nào trong khu vực của bạn' + 'Đăng tin để đồng nghiệp nhìn thấy nhu cầu của bạn' | CTA 'Đăng tin ngay'"

**Source Location:** `DOC-v1.1-01 §6.2 AC-11.2.01 · trang 19` và `§8.17.1 · trang 51`

**Analyst Note:** 2 nguồn PRD (AC + bảng danh mục empty state) trùng khớp nội dung — dùng làm oracle mạnh (2 nguồn cùng tài liệu, không mâu thuẫn). Đây là 1 trong 3 SC atomic thay cho `SC-HOME-024` gộp cũ (xem `CHANGELOG.md §2` — kết luận bị đảo). Thêm điều kiện chung BR17-02/03 (không skeleton vô hạn, không che tab, vẫn cuộn được) — assert-absent, không cần SC riêng vì áp dụng chung cho cả 3 empty state của module này.

##### SC-HOME-026 — [Empty state] "Đơn của tôi"

**Source Quote:**
> EMP-02 (§8.17.1, trang 51): "Trang chủ — Đơn của tôi | 'Bạn chưa có đơn nào đang chạy' | CTA 'Tạo đơn gửi hàng'"

**Source Location:** `DOC-v1.1-01 §8.17.1 · trang 51`

**Analyst Note:** Thay cho phần "Đơn của tôi" trong `SC-HOME-024` gộp cũ. Điều kiện Given dùng chung với `REQ-HOME-005` (section chỉ hiện khi có đơn hoạt động) — Given ở đây là nhánh "0 đơn" của chính điều kiện đó, không phải điều kiện mới. Không ảnh hưởng tới `C-HOME-02` (vẫn Open, PRD không nói rõ ẩn theo điều kiện hay vai trò — SC này chỉ xác nhận nội dung hiển thị KHI đã ẩn/rỗng, không xác nhận LÝ DO ẩn).

##### SC-HOME-027 — [Empty state] Hero & cộng đồng

**Source Quote:**
> EMP-03 (§8.17.1, trang 51): "Trang chủ — Hero & cộng đồng | Hero hiện '0 · Chưa có đóng góp nào'; cụm cộng đồng hiện '0 đơn · 0 người' | CTA '—'"

**Source Location:** `DOC-v1.1-01 §8.17.1 · trang 51`

**Analyst Note:** Thay phần "Hero/card Đóng góp của bạn" trong `SC-HOME-024` gộp cũ. Đối chiếu `test_data_catalog.md` v1.0 dòng "Số đơn đã giúp (card)" — trước đây chỉ ghi "0 (tài khoản mới)" mà chưa có text hiển thị cụ thể; giờ PRD cho đúng câu chữ. Không có CTA — khác với 2 SC còn lại (025/026), assert **không có** nút hành động nào ở khu vực này khi rỗng.

##### SC-HOME-028 — [Performance] Thời gian hiển thị nội dung đầu

**Source Quote:**
> NFR01 (§9, trang 53): "Bảng tin và trang chủ hiển thị nội dung đầu tiên < 2 giây (p95) trên mạng 4G với 1.000 người dùng đồng thời." Cách đo: "Load test trước go-live."

**Source Location:** `DOC-v1.1-01 §9 · trang 53`

**Analyst Note:** NFR mới, không có tương đương ở v1.0. Cần môi trường load-test chuyên dụng (1.000 người dùng đồng thời) — **KHÔNG chạy được bằng manual/vibe-test thông thường**. Viết SC ở đây để không mất traceability, nhưng ghi rõ trong `risk_assessment.md` là cần defer cho automation/load-test riêng, không tính vào scope `vibe-test`/execute-maintain thủ công.

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| SC-HOME-001 | Bottom nav đủ 5 tab | HOME | v1.0 | P1 | `v1.0/HOME-trang-chu/test_scenario_map.md` |
| SC-HOME-002 | Bottom nav ẩn ở màn con | HOME | v1.0 | P3 | ← |
| SC-HOME-003 | Header — lời chào | HOME | v1.0 | P2 | ← |
| SC-HOME-004 | [GAP] Icon vai trò header | HOME | v1.0 | P3 | ← |
| SC-HOME-005 | Chuông — có tin chưa đọc | HOME | v1.0 | P2 | ← |
| SC-HOME-006 | Chuông — đã đọc hết | HOME | v1.0 | P3 | ← |
| SC-HOME-007 | Banner tĩnh | HOME | v1.0 | P3 | ← |
| SC-HOME-008 | Card "Đóng góp của bạn" | HOME | v1.0 | P2 | ← |
| SC-HOME-009 | Section "Đơn của tôi" — có đơn | HOME | v1.0 | P2 | ← |
| SC-HOME-010 | Section "Đơn của tôi" — không đơn | HOME | v1.0 | P2 | ← |
| SC-HOME-011 | Nhãn vai Sender | HOME | v1.0 | P2 | ← |
| SC-HOME-012 | Nhãn vai Carrier | HOME | v1.0 | P2 | ← |
| SC-HOME-013 | Nhãn vai Receiver | HOME | v1.0 | P2 | ← |
| SC-HOME-014 | Badge + progress theo trạng thái | HOME | v1.0 | P3 | ← |
| SC-HOME-015 | Tap section → Theo dõi đơn | HOME | v1.0 | P2 | ← |
| SC-HOME-016 | "Xem tất cả" → Hoạt động | HOME | v1.0 | P3 | ← |
| SC-HOME-017 | "Tin mới" — vai Sender | HOME | v1.0 | P2 | ← |
| SC-HOME-018 | "Tin mới" — vai Carrier | HOME | v1.0 | P2 | ← |
| SC-HOME-020 | Tap tin → Chi tiết tin | HOME | v1.0 | P3 | ← |
| SC-HOME-022 | "Xem bảng tin gửi hàng" | HOME | v1.0 | P2 | ← |
| SC-HOME-023 | Điều hướng sau khi nhận đơn | HOME | v1.0 | P3 | ← |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| SC-HOME-024 | [GAP] Empty state Trang chủ (gộp) | HOME | v1.1 | PRD v1.1 đặc tả riêng cho 3 khu vực — thay bằng `SC-HOME-025/026/027` theo Scenario Sufficiency Rule. Xem `CHANGELOG.md §2` |
