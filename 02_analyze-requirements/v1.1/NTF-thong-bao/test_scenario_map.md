---
id: v1.1/NTF-thong-bao/scenario-map
title: Test Scenario Map — v1.1 · Module NTF (Delta)
type: scenario-map
version: v1.1
sprint: 1
module: NTF
counts:
  req: 12
  sc: 22
  new: 6
  modified: 3
  carried: 13
  deprecated: 0
  p1: 1
  p2: 15
  p3: 6
status: ANALYZED
updated: 2026-09-15
---

# Test Scenario Map — v1.1 · Module NTF (Delta)

> **Home của SC quote** (1 quote = 1 nơi): Source Quote per SC ở §"Source Detail per Scenario" file này.
> REQ quote → `requirement_traceability.md §2` · Clarification quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/lifecycle/priority module NTF **tính tới v1.1** (bao gồm CARRIED từ v1.0) — cùng nghĩa với 4 module delta còn lại. **22 SC** = CARRIED 13 + MODIFIED 3 (giữ ID v1.0) + NEW 6. Router `v1.1/MEMORY.md §2` là bản **dẫn xuất**, cộng lại từ đây.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)
> **1 SC = 1 hành vi nguyên tử.** Fan-out mỗi sự kiện thông báo (state-transition sinh thông báo) = 1 SC riêng.
> Trần: display-only/duplicate → không tạo SC rác (vd `NTF-07` đã có SC ở `GIFT`, không lặp).

## Tổng quan
- Delta v1.1: **9 SC** (NEW: 6, MODIFIED: 3, CARRIED: 13 — không liệt kê chi tiết, xem bảng CARRIED)
- Phân bổ priority (delta): P2: 8 | P3: 1

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### NTF — Thông báo (Delta v1.1)

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-NTF-005 | NTF-06 — đơn hoàn tất (text đã chốt) | REQ-NTF-003 | DOC-v1.1-01 §8.13.1 | Đơn ở DELIVERED | Người nhận bấm "Xác nhận đã nhận hàng" → xác nhận | **Cả Sender và Carrier** nhận đúng text "Đơn đã hoàn tất — cảm ơn bạn!" | P2 | Functional | MODIFIED |
| SC-NTF-008 | SĐT không có trong nội dung thông báo (mở rộng phạm vi) | REQ-NTF-005 | DOC-v1.1-01 §8.13.1 | Đơn đã ghép (SĐT lộ trong app cho cặp) VÀ đơn đã đi qua ít nhất 1 trong 6 nhánh mới (uỷ quyền/quầy/không liên lạc được/hẹn giao lại/hoàn hàng) | Đọc toàn bộ nội dung thông báo in-app và push của **đủ 15 sự kiện** (9 cũ + 6 mới) | KHÔNG thông báo nào (kể cả 6 sự kiện mới) chứa số điện thoại; chỉ được nhắc "có ảnh bằng chứng"/"cần xác nhận uỷ quyền" | P1 | Business Rule | MODIFIED |
| SC-NTF-014 | Danh sách loại thông báo chính thức — đủ 15 loại | REQ-NTF-010 | DOC-v1.1-01 §8.13.1 | Đơn đi trọn 1 vòng đời qua đủ nhánh chính (POSTED→MATCHED→IN_TRANSIT→DELIVERED→COMPLETED) VÀ 1 lượt qua nhánh phụ FR08/FR09 (không liên lạc được→gửi quầy→cầm hàng về→hẹn giao lại→giao lại thành công; và 1 lượt hoàn hàng) | Liệt kê toàn bộ loại thông báo thực tế app bắn ra trong các vòng đời trên | Đủ **15/15 loại** theo danh mục chính thức `§8.13.1`, đúng người nhận mỗi loại. Thiếu 1 loại bất kỳ → log finding, KHÔNG lặng lẽ coi là OK | P2 | Business Rule | MODIFIED |
| SC-NTF-017 | NTF-10 — giao cho người được uỷ quyền | REQ-NTF-012 | DOC-v1.1-01 §8.13.1 | Người vận chuyển vừa xác nhận giao hàng (FR07) chọn đối tượng nhận = "Người được uỷ quyền" | Đơn chuyển DELIVERED | Người nhận và người gửi nhận thông báo NTF-10, có nêu tên người nhận thay + ai uỷ quyền + có ảnh bằng chứng; KHÔNG chứa SĐT | P2 | Functional | NEW |
| SC-NTF-018 | NTF-11 — gửi tại quầy lễ tân/bảo vệ | REQ-NTF-012 | DOC-v1.1-01 §8.13.1 | Người vận chuyển chọn phương án gửi quầy (lễ tân hoặc bảo vệ) ở nhánh FR08 | Đơn chuyển DELIVERED kèm cờ không liên lạc được người nhận | Người nhận và người gửi nhận thông báo NTF-11, nêu đúng loại quầy + tên người trực; KHÔNG chứa SĐT | P2 | Functional | NEW |
| SC-NTF-019 | NTF-12 — không liên lạc được người nhận | REQ-NTF-012 | DOC-v1.1-01 §8.13.1 | Người vận chuyển bấm "Không liên lạc được người nhận?" và chọn hướng liên hệ người gửi xin uỷ quyền khác | Modal mở, đơn gắn cờ không liên lạc được người nhận | Người gửi nhận thông báo NTF-12 với nội dung "cần bạn xác nhận uỷ quyền cho người khác nhận hàng"; KHÔNG chứa SĐT người nhận | P2 | Functional | NEW |
| SC-NTF-020 | NTF-13 — hẹn giao lại (RESCHEDULED) | REQ-NTF-012 | DOC-v1.1-01 §8.13.1 | Người vận chuyển chọn "Cầm hàng về" → chế độ `retry` (hẹn giao lại), nhập lịch hẹn hợp lệ | Đơn chuyển RESCHEDULED | Người nhận và người gửi nhận thông báo NTF-13 có đúng {ngày · giờ} và {nơi hẹn} vừa nhập; KHÔNG chứa SĐT | P2 | Functional | NEW |
| SC-NTF-021 | NTF-14 — trả hàng về người gửi (RETURNING) | REQ-NTF-012 | DOC-v1.1-01 §8.13.1 | Người vận chuyển chọn "Cầm hàng về" → chế độ `return` (trả người gửi), nhập lịch hẹn hợp lệ | Đơn chuyển RETURNING | Người gửi và người nhận nhận thông báo NTF-14 có đúng {ngày · giờ} và {nơi hẹn}; KHÔNG chứa SĐT | P2 | Functional | NEW |
| SC-NTF-022 | NTF-15 — đã nhận lại hàng (RETURNED) | REQ-NTF-012 | DOC-v1.1-01 §8.13.1 | Đơn ở RETURNING, người gửi bấm "Xác nhận đã nhận lại hàng" | Đơn chuyển RETURNED (đóng) | Người vận chuyển và người nhận nhận thông báo NTF-15 "Đơn đã đóng — hàng đã được trả lại người gửi" | P3 | Functional | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-NTF-005 — NTF-06 text đã chốt

**Source Quote (old):**
> "NTF-06 | ... | "Đơn đã hoàn tất — cảm ơn bạn!"" (BRD `DOC-v1.0-01` §D6 L324) — mâu thuẫn với `DOC-v1.0-06 KP-07` hàng #6 (Figma/PRD-demo: "Đơn đã hoàn thành — đánh giá ngay")

**Source Quote (new):**
> ↪ *Quote `NTF-06` — home ở `requirement_traceability.md` · `REQ-NTF-003` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

**Source Location:** `DOC-v1.1-01 §8.13.1 · bảng "Danh mục thông báo" · dòng NTF-06 · page 48`

**Analyst Note:** PRD chính thức xác nhận bản BRD cũ, loại bỏ nghi vấn dùng từ "đánh giá" (vốn xung đột với `C-GIFT-01` — rating đã defer khỏi v1.0). Từ v1.1 assert được text chính xác, không còn ghi nhận-không-assert như v1.0.

##### SC-NTF-008 — Mở rộng phạm vi kiểm SĐT sang 6 sự kiện mới

**Source Quote:**
> Đối chiếu toàn bộ 15 dòng "Nội dung (mẫu)" ở bảng `§8.13.1`, không dòng nào chứa placeholder hay giá trị số điện thoại — kể cả `NTF-10`/`NTF-11`/`NTF-12` (các tình huống nhạy cảm nhất về liên hệ).

**Source Location:** `DOC-v1.1-01 §8.13.1 · page 48` (đối chiếu `DOC-v1.0-01 §D7 OPR-07 · L343`)

**Analyst Note:** Rule bảo mật cũ (`OPR-07`) tiếp tục đúng cho cả 6 sự kiện mới. Given mở rộng để P1 test này phủ đủ 15/15 sự kiện thay vì chỉ 9/9 — nếu bỏ sót 1 trong 6 sự kiện mới thì rủi ro lộ SĐT (P1) không được kiểm.

##### SC-NTF-014 — Đủ 15 loại thông báo chính thức

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-NTF-010`)*

**Source Location:** `DOC-v1.1-01 §8.13.1 · page 48`

**Analyst Note:** SC này giờ là **SC bảo vệ danh mục chính thức** (đảo vai trò từ [GAP] ghi-nhận sang assert đủ-danh-mục) — tương tự mẫu `SC-USR-003`/`SC-TS-003`: nếu app thiếu 1 trong 15 loại thì đây là bằng chứng cụ thể để log finding, không phải "coverage đã đủ vì có SC chạy qua". Cần chạy đơn qua **cả nhánh chính lẫn nhánh phụ FR08/FR09** mới quan sát đủ 15 loại — tiền đề tốn thời gian nhất module, nên gộp chạy chung với vibe-test `DLV` (xem `RISK-NTF-05`).

##### SC-NTF-017..022 — 6 sự kiện thông báo mới (NTF-10..15)

**Source Quote:** *(quote đầy đủ per-dòng ở `requirement_traceability.md §2 REQ-NTF-012`)*

**Source Location:** `DOC-v1.1-01 §8.13.1 · page 48`

**Analyst Note:** Mỗi SC chỉ assert **có bắn đúng thông báo, đúng người nhận, đúng nội dung + biến** — KHÔNG lặp lại nghiệp vụ giao nhận (đã có SC tương ứng bên `DLV-giao-nhan/` delta v1.1). Trigger tiền đề của cả 6 SC phụ thuộc trực tiếp luồng FR08/FR09 — nên chạy **sau khi** đã dựng xong đơn ở đúng nhánh tương ứng bên `DLV`, không seed riêng.

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| SC-NTF-001 | NTF-01/02 — ghép ngay | NTF | v1.0 | P2 | → `v1.0/NTF-thong-bao/test_scenario_map.md` |
| SC-NTF-002 | NTF-03 — khớp tuyến OFFER | NTF | v1.0 | P2 | → như trên |
| SC-NTF-003 | NTF-04 — Carrier đã lấy hàng | NTF | v1.0 | P2 | → như trên |
| SC-NTF-004 | NTF-05 — Carrier đã giao | NTF | v1.0 | P2 | → như trên |
| SC-NTF-006 | NTF-08 — đơn bị huỷ | NTF | v1.0 | P2 | → như trên |
| SC-NTF-007 | NTF-09 — tin quá hạn | NTF | v1.0 | P2 | → như trên |
| SC-NTF-009 | Nhóm theo mốc thời gian | NTF | v1.0 | P2 | → như trên |
| SC-NTF-010 | Chấm đỏ theo từng item | NTF | v1.0 | P3 | → như trên |
| SC-NTF-011 | [GAP] Cơ chế "Đánh dấu đã đọc" | NTF | v1.0 | P3 | → như trên — ✅ **2026-09-16 BA: mark-all** (`C-NTF-03` Resolved) ⇒ hết `[GAP]`, Then assert bấm 1 lần → **mọi** thông báo về đã đọc, không còn chấm đỏ nào |
| SC-NTF-012 | Scroll / lazy-load | NTF | v1.0 | P3 | → như trên |
| SC-NTF-013 | Chuông đồng bộ số chưa đọc | NTF | v1.0 | P2 | → như trên — ⚠️ **2026-09-16:** bước "đọc hết" = bấm "Đánh dấu đã đọc" (mark-all, `C-NTF-03`) ⇒ assert badge chuông về 0/ẩn ngay sau đó |
| SC-NTF-015 | [GAP] Empty state màn Thông báo | NTF | v1.0 | P3 | → như trên |
| SC-NTF-016 | Nút back màn Thông báo | NTF | v1.0 | P3 | → như trên |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
