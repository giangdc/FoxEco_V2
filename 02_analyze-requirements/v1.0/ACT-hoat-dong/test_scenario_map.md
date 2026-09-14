---
id: v1.0/ACT-hoat-dong/scenario-map
title: Test Scenario Map — v1.0 · Module ACT
type: scenario-map
version: v1.0
sprint: 1
module: ACT
counts:
  req: 9
  sc: 14
  new: 14
  modified: 0
  carried: 0
  deprecated: 0
  p1: 0
  p2: 7
  p3: 7
status: ANALYZED
updated: 2026-09-07
---

# Test Scenario Map — v1.0 · Module ACT

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module ACT.
> ⚠️ **P1 = 0 là có chủ đích:** module là bề mặt **hiển thị lịch sử đơn**, không chứa hành động nghiệp vụ nào có thể chặn luồng. Rủi ro cao nhất chỉ ở mức lọc data sai tab (P2).

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Fan-out mỗi role · state · lớp EP · boundary · nhánh lỗi = 1 SC.
> 📌 **Áp thêm `Project_rule §Custom Rules §10.2`:** màn có tab ⇒ **mỗi tab ≥1 SC riêng verify data**, và **SC verify cơ chế switch tab giữ độc lập**. Vì vậy: `SC-ACT-003` (switch) tách khỏi `SC-ACT-004`/`SC-ACT-005` (data từng tab), và empty state cũng tách 2 SC theo tab.

## Tổng quan
- Tổng số scenarios: **14** (NEW: 14, MODIFIED: 0, CARRIED: 0, DEPRECATED: 0)
- Phân bổ priority: P1: 0 | P2: 7 | P3: 7
- Nguồn đặc tả **mỏng nhất dự án**: 6/9 REQ chỉ có nguồn `DOC-v1.0-06` KP-01 §3 `KB-ORD-07` (`QA-obs` + 1 ảnh mockup) — BRD/PRD gần như không mô tả màn này.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### ACT — Hoạt động ("Đơn của tôi")

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-ACT-001 | Hai tab | REQ-ACT-001 | DOC-v1.0-02 §2 · KP-01 §3 KB-ORD-07 (#1) | Đã vào FoxEco | Mở tab "Hoạt động" | Màn có đúng 2 tab con: "Đang diễn ra" và "Đã hoàn thành" | P2 | UI | NEW |
| SC-ACT-002 | Tab mặc định | REQ-ACT-001 | KP-01 §3 KB-ORD-07 (#2) | Chưa từng mở màn Hoạt động trong phiên | Mở tab "Hoạt động" | Tab "Đang diễn ra" đang active mặc định | P2 | UI | NEW |
| SC-ACT-003 | Cơ chế switch tab | REQ-ACT-001 | KP-01 §3 KB-ORD-07 (#1) · Custom Rule §10.2 | Đang ở màn Hoạt động, tab "Đang diễn ra" active | Bấm sang tab "Đã hoàn thành", rồi bấm quay lại tab "Đang diễn ra" | Tab active đổi đúng theo thao tác; nội dung danh sách đổi theo tab (⛔ SC này KHÔNG verify nội dung data — xem SC-ACT-004/005) | P3 | Functional | NEW |
| SC-ACT-004 | Data tab "Đang diễn ra" | REQ-ACT-003 | DOC-v1.0-02 §3.7 đoạn 2 | Tài khoản có đơn ở các trạng thái Chờ ghép · Đã ghép · Đang giao · Đã giao **và** có đơn Hoàn thành/Hết hạn | Mở tab "Đang diễn ra" | Danh sách CHỈ chứa đơn đang hoạt động (Chờ ghép..Đã giao); KHÔNG lẫn đơn Hoàn thành/Hết hạn | P2 | Functional | NEW |
| SC-ACT-005 | Data tab "Đã hoàn thành" | REQ-ACT-004 | DOC-v1.0-02 §3.7 đoạn 3 · DOC-v1.0-01 §D1b US-D04 | Tài khoản có ≥1 đơn "Hoàn thành", ≥1 đơn "Hết hạn" **và** ≥1 đơn đang hoạt động | Mở tab "Đã hoàn thành" | Danh sách chứa CẢ đơn "Hoàn thành" VÀ đơn "Hết hạn"; KHÔNG lẫn đơn đang hoạt động | P2 | Functional | NEW |
| SC-ACT-006 | Completeness card đơn | REQ-ACT-002 | KP-01 §3 KB-ORD-07 (#3) · DOC-v1.0-05 | Có ≥1 đơn hiển thị ở 1 trong 2 tab | Đối chiếu từng trường của 1 card | Card đủ 5 trường: icon trạng thái · tên tin · tuyến "Từ → Đến" · ngày · badge trạng thái | P2 | UI | NEW |
| SC-ACT-007 | Đơn "Đã huỷ" bị ẩn | REQ-ACT-007 | KP-01 §3 KB-ORD-07 (#7) | Tài khoản có ≥1 đơn đã bị huỷ | Mở lần lượt cả 2 tab, tìm đơn đã huỷ đó | Đơn "Đã huỷ" KHÔNG xuất hiện ở cả 2 tab | P2 | Business Rule | NEW |
| SC-ACT-008 | Card "Hết hạn" có lý do | REQ-ACT-005 | KP-01 §3 KB-ORD-07 (#4) · DOC-v1.0-01 §D1b US-D04 | Có ≥1 đơn ở trạng thái "Hết hạn" | Mở tab "Đã hoàn thành", xem card đơn Hết hạn | Card có badge "Hết hạn" + dòng lý do "Không có ai nhận mang giúp trong thời gian đăng — tin đã tự động đóng." | P3 | UI | NEW |
| SC-ACT-009 | Card "Hết hạn" không thao tác được | REQ-ACT-005 | KP-01 §3 KB-ORD-07 (#6) | Đang ở tab "Đã hoàn thành", có card "Hết hạn" | Tap vào card "Hết hạn" | Không có phản hồi / không mở màn nào (non-clickable) | P3 | Business Rule | NEW |
| SC-ACT-010 | Tap card (≠ Hết hạn) | REQ-ACT-006 | KP-01 §3 KB-ORD-07 (#5) · DOC-v1.0-02 §3.7 | Có ≥1 đơn trạng thái khác "Hết hạn" | Tap vào card đó | Mở màn tiếp của ĐÚNG đơn vừa tap (dữ liệu hiển thị khớp card) | P2 | Functional | NEW |
| SC-ACT-011 | [GAP] Đích tap card | REQ-ACT-006 | KP-01 §3 KB-ORD-07 (#5) vs DOC-v1.0-02 §3.7 | 2 nguồn nêu 2 đích khác nhau ("Chi tiết tin" vs "Theo dõi đơn") | Tap card rồi ghi nhận tên màn đích | GHI NHẬN màn đích thật; ⛔ KHÔNG assert tên màn (C-ACT-01 Open) | P3 | Functional | NEW |
| SC-ACT-012 | [GAP] Empty state tab "Đang diễn ra" | REQ-ACT-008 | DOC-v1.0-06 KP-02 §5 · C-ORD-06 | Tài khoản KHÔNG có đơn đang hoạt động nào | Mở tab "Đang diễn ra" | GHI NHẬN hiển thị thực tế (text/ảnh empty state nếu có); ⛔ KHÔNG assert text (C-ORD-06 Open) | P3 | UI | NEW |
| SC-ACT-013 | [GAP] ★★★★★ leftover trên card Hoàn thành | REQ-ACT-009 | DOC-v1.0-02 §3.7 · KP-01 §3 KB-ORD-07 ghi chú · §6 KB-GIFT-02 | Có ≥1 đơn "Hoàn thành"; rating 1-5 sao đã out-of-scope v1.0 (C-GIFT-01) | Xem card đơn Hoàn thành | GHI NHẬN có/không có chuỗi "★★★★★ Đã đánh giá"; ⛔ KHÔNG assert số sao, KHÔNG assert cơ chế đánh giá | P3 | UI | NEW |
| SC-ACT-014 | [GAP] Empty state tab "Đã hoàn thành" | REQ-ACT-008 | DOC-v1.0-06 KP-02 §5 · C-ORD-06 | Tài khoản chưa có đơn Hoàn thành và chưa có đơn Hết hạn nào | Mở tab "Đã hoàn thành" | GHI NHẬN hiển thị thực tế; ⛔ KHÔNG assert text (C-ORD-06 Open) | P3 | UI | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-ACT-001 / SC-ACT-002 / SC-ACT-003 — Hai tab · tab mặc định · cơ chế switch

**Source Quote:**
> Nguồn A (`DOC-v1.0-02` §2 dòng "Tab Hoạt động"): "Tab Hoạt động | "Đơn của tôi" — 2 tab con: Đang diễn ra / Đã hoàn thành"
> Nguồn B (`DOC-v1.0-06` KP-01 §3 KB-ORD-07): "| 1 | 2 tab | `Đang diễn ra` / `Đã hoàn thành` |" · "| 2 | Tab mặc định | `Đang diễn ra` |"

**Source Location:** `DOC-v1.0-02 §2 · bảng Thành phần/Mô tả · dòng "Tab Hoạt động"` ⟷ `DOC-v1.0-06 KP-01 §3 "KB-ORD-07" · bảng · dòng 1-2`

**Analyst Note:** **Tab mặc định** chỉ có nguồn `KB-ORD-07` (`QA-obs` + ảnh `DOC-v1.0-05`) ⇒ 1 nguồn + ảnh mockup, cần vibe-test xác nhận. `SC-ACT-003` tách riêng theo `§Custom Rules §10.2` — **case gốc của chính rule đó là màn Hoạt động này**: đợt cũ từng gộp verify data 2 tab vào 1 TC "chuyển tab qua lại" rồi phải tách ra. SC switch **cố ý không verify nội dung data**.

##### SC-ACT-004 — Data tab "Đang diễn ra"

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-ACT-003`)*

**Source Location:** `DOC-v1.0-02 §3.7 "Màn hình Hoạt động ("Đơn của tôi")" · đoạn 2`

**Analyst Note:** Doc chỉ nói *"đơn hiện tại"*, **không liệt kê trạng thái** ⇒ tập trạng thái là **suy diễn của analyst**: `Chờ ghép · Đã ghép · Đang giao · Đã giao` (từ 5 mốc `§D2` L232, trừ `Hoàn thành` vì `§3.7` đoạn 3 xếp nó sang tab kia, trừ `Đã huỷ` theo `KB-ORD-07` #7). Given **bắt buộc có cả 2 nhóm dữ liệu** để phát hiện lỗi lọc — đây là điểm mà TC gộp tab của đợt cũ không bắt được.

##### SC-ACT-005 — Data tab "Đã hoàn thành" (gồm cả Hết hạn)

**Source Quote:**
> Nguồn A (`DOC-v1.0-02` §3.7 đoạn 3): "Tab "Đã hoàn thành": đơn trạng thái "Hoàn thành" (5 sao + "Đã đánh giá") hoặc "Hết hạn" (không ai nhận mang giúp trong thời gian đăng — tin tự động đóng)."
> Nguồn B (`DOC-v1.0-01` §D1b `US-D04` L166): "hiển thị badge "Hết hạn" ở tab hoàn tất kèm lý do…"

**Source Location:** `DOC-v1.0-02 §3.7 · đoạn 3` ⟷ `DOC-v1.0-01 §D1b · US-D04 · Acceptance Criteria · L166`

**Analyst Note:** ⚠️ **Điểm dễ sai:** tên tab gợi ý chỉ chứa đơn thành công, nhưng **đơn Hết hạn (thất bại) cũng nằm ở đây** — 2 nguồn đồng thuận. TC viết theo trực giác tên tab sẽ assert thiếu nhóm Hết hạn.

##### SC-ACT-006 — Completeness card đơn (5 trường)

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-ACT-002`)*

**Source Location:** `DOC-v1.0-06 KP-01 §3 "KB-ORD-07" · bảng · dòng 3`

**Analyst Note:** BRD/PRD **không mô tả** card này ⇒ nguồn duy nhất là `QA-obs` + ảnh `DOC-v1.0-05`. ⚠️ Ảnh đó có status bar **"9:41"** — **mockup Apple, không phải máy thật** ⇒ đối chiếu **cấu trúc**, ⛔ không đối chiếu giá trị dữ liệu trong ảnh. Cần vibe-test xác nhận trước khi coi là đã chốt (`§Custom Rules §10.1`).

##### SC-ACT-007 — Đơn "Đã huỷ" không hiển thị ở cả 2 tab

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-ACT-007`)*

**Source Location:** `DOC-v1.0-06 KP-01 §3 "KB-ORD-07" · bảng · dòng 7`

**Analyst Note:** Rule **không có trong BRD/PRD**, chỉ `QA-obs`. Đáng chú ý về nghiệp vụ: đơn đã huỷ **biến mất khỏi lịch sử của user** trong khi `TS-01` (§A8 L121) yêu cầu ghi log đầy đủ cả hành động huỷ ⇒ log tồn tại ở backend nhưng **không có bề mặt cho user xem lại**. Cross-ref `SC-CNL-009` (`C-CNL-02`: huỷ đơn phải ghi log LỊCH SỬ) — 2 SC này cùng chỉ vào một khoảng trống thiết kế.

##### SC-ACT-008 / SC-ACT-009 — Card "Hết hạn": lý do · non-clickable

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-ACT-005`)*

**Source Location:** `DOC-v1.0-06 KP-01 §3 "KB-ORD-07" · bảng · dòng 4 và 6`

**Analyst Note:** ⭐ Text có **nguyên văn từ 2 nguồn** (`KB-ORD-07` và `US-D04`) — hiếm trong dự án này ⇒ assert được. ⚠️ 2 nguồn **lệch phần cuối câu**: `KB-ORD-07` có thêm *"— tin đã tự động đóng."*, `US-D04` dừng sớm hơn ⇒ assert theo `KB-ORD-07` (bản quan sát app). Given cần đơn đã Hết hạn ⇒ phụ thuộc `SC-ORD-045` và cần dev seed (xem `risk_assessment.md` `RISK-ACT-03`).

##### SC-ACT-010 / SC-ACT-011 — Tap card: hành vi · [GAP] đích điều hướng

**Source Quote:**
> Nguồn A (`DOC-v1.0-06` KP-01 §3 KB-ORD-07 dòng 5): "| 5 | Tap card ≠ "Hết hạn" | → mở màn "Chi tiết tin" |"
> Nguồn B (`DOC-v1.0-02` §3.7 đoạn 2): "Tab "Đang diễn ra": card đơn hiện tại (nếu có) → bấm vào mở **Theo dõi đơn**."

**Source Location:** `DOC-v1.0-06 KP-01 §3 "KB-ORD-07" · dòng 5` ⟷ `DOC-v1.0-02 §3.7 · đoạn 2`

**Analyst Note:** ⚠️ 2 đích **khác bản chất**: "Chi tiết tin" là màn **public** (module `FEED`, có CTA "Tôi mang giúp được"), "Theo dõi đơn" là màn **role-aware** (module `DLV`, có nút hành động theo vai). Nếu app mở "Chi tiết tin" cho đơn của chính mình thì lại rơi vào đúng bug `SC-FEED-011` (chủ tin thấy CTA) ⇒ `C-ACT-01` có liên hệ trực tiếp tới `RISK-FEED-02`. `SC-ACT-010` vì thế assert *"mở màn tiếp của đúng đơn"* mà **không assert tên màn**.

##### SC-ACT-012 / SC-ACT-014 — [GAP] Empty state 2 tab

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-ACT-008`)*

**Source Location:** `DOC-v1.0-06 KP-02 §5 · bảng "Nhóm Open" · dòng "C-ORD-06"`

**Analyst Note:** Tách 2 SC theo `§Custom Rules §10.2` (mỗi tab 1 tiền đề dữ liệu riêng: tab 1 rỗng khi không có đơn đang hoạt động; tab 2 rỗng khi chưa có đơn Hoàn thành **và** chưa có đơn Hết hạn). ⚠️ Bài học `KP-02 §6`: lần trước CL này bị đánh `Resolved` dựa trên mô tả chat không kèm bằng chứng rồi phải revert ⇒ lượt này ⛔ không assert text cho tới khi có ảnh/BA trả lời.

##### SC-ACT-013 — [GAP] ★★★★★ "Đã đánh giá" là UI leftover

**Source Quote:**
> Nguồn A (`DOC-v1.0-02` §3.7 đoạn 3): "đơn trạng thái "Hoàn thành" (**5 sao + "Đã đánh giá"**)"
> Nguồn B (`DOC-v1.0-06` KP-01 §3 KB-ORD-07 ghi chú): "⚠ Trên card "Hoàn thành" có chuỗi `★★★★★ Đã đánh giá` nhưng **rating 1-5 sao đã out-of-scope v1.0** → coi là UI leftover, KHÔNG viết TC assert rating"

**Source Location:** `DOC-v1.0-02 §3.7 · đoạn 3` ⟷ `DOC-v1.0-06 KP-01 §3 "KB-ORD-07" · ghi chú cuối`

**Analyst Note:** `C-GIFT-01` Resolved: rating là phase sau. SC ghi nhận **sự tồn tại của chuỗi UI** (để version sau biết nó có từ đầu, không phải mới xuất hiện), ⛔ không assert số sao và không assert cơ chế đánh giá. Cross-ref `SC-USR-006` (không hiện Điểm uy tín) và `SC-GIFT-011` — cùng một nhóm "UI leftover của tính năng đã defer".

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| — | *(không có — v1.0 là version đầu của chuỗi phân tích mới)* | — | — | — | — |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
