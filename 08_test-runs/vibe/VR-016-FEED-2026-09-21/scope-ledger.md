# Scope Ledger — VR-016 — module FEED — SCOPE_TOTAL = 15 TC

> Seed từ: `coverage-FEED.md` (trạng thái trước phiên: chưa tồn tại — 0/15 có verdict, mọi TC `⏳ NOT_RUN`)
> Tập chạy phiên này: **CHỈ 5 TC thuộc v1.1** (`TC-FEED-002/007/009/013/015`) — theo yêu cầu tường minh của QC ("chỉ test lại các case thuộc ver 1.1 thôi"), KHÔNG phải toàn bộ SCOPE_TOTAL. Lô 1/1 (module nhỏ, dưới ngưỡng batch 15–25).
> 10 TC carried v1.0 (`001 003 004 005 006 008 010 011 012 014`) **cố ý không chạy** phiên này — giữ nguyên `⏳ NOT_RUN` seed, KHÔNG phải hết sức phiên.

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-FEED-001 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (chỉ v1.1) |
| TC-FEED-002 | ✅ PASS | 1 | run này | `screenshots/TC-FEED-002__verify-card0-no-cta.png` |
| TC-FEED-003 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (chỉ v1.1) |
| TC-FEED-004 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (chỉ v1.1) |
| TC-FEED-005 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (chỉ v1.1) |
| TC-FEED-006 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (chỉ v1.1) |
| TC-FEED-007 | ✅ PASS | 1 (retest account `anhdc4`) | run này | `screenshots/TC-FEED-007__verify-anhdc4-bottom-with-cta.png` — đủ 4/4 sub-clause với data hợp lệ + tài khoản khác |
| TC-FEED-008 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (chỉ v1.1) |
| TC-FEED-009 | ✅ PASS | 1b (retest) | run này | `screenshots/TC-FEED-009__verify-real-map-route.png` — QC cấp 2 địa chỉ hợp lệ, tự tạo tin, bản đồ thật hiển thị đúng |
| TC-FEED-010 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (chỉ v1.1) |
| TC-FEED-011 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (chỉ v1.1) |
| TC-FEED-012 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (chỉ v1.1) |
| TC-FEED-013 | 🚫 BLOCKED | 1 | run này | `screenshots/TC-FEED-013__step1-BLOCKED-precondition-khong-rong.png` — Bảng tin cộng đồng không rỗng, cần dev/QA dọn |
| TC-FEED-014 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (chỉ v1.1) |
| TC-FEED-015 | ✅ PASS | 1 (đổi 2026-09-21) | run này | `screenshots/TC-FEED-015__verify-accepted-behavior.png` — QC chấp nhận hành vi hiện tại, Expected Result đã sửa theo app, `BUG-029` rút lại |

**Tổng kết lô 1 (duy nhất, hết phạm vi được yêu cầu):** chạy 5/5 TC trong phạm vi · 4 PASS · 0 FAIL · 1 BLOCKED · evidence 5/5 *(`TC-FEED-009` retest BLOCKED→PASS · `TC-FEED-015` FAIL→PASS sau khi QC sửa Expected theo app · `TC-FEED-007` FAIL→PASS retest account `anhdc4` + data hợp lệ).*
**Còn nợ của MODULE (không phải của phiên này):** 10 TC carried v1.0 — chạy tiếp bằng `/vibe-test --module FEED` (bỏ giới hạn v1.1) khi QC muốn phủ nốt.
