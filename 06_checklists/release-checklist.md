# Release Checklist — foxeco-v2 [Version]

> Gate cụ thể: `02_analyze-requirements/Project_rule.md §Report Rules & Quality Gates` (G1–G6 + G7+ riêng project).

## Trước Release (Pre-Release)
- [ ] G4 — Bug P1 còn Open = 0 (`§Report Rules & Quality Gates`)
- [ ] G3 — Pass rate (effective) ≥ 90%, G2 — 100% TC P1 đã execute
- [ ] Bộ test Regression đã pass (211/211 SC scope — `MASTER-MEMORY.md §4 Regression Scope`)
- [ ] UAT đã được sign-off
- [ ] Release notes đã soạn xong
- [ ] Kế hoạch rollback đã được ghi nhận
- [ ] SRC-TC review score ≥ 70 — **N/A, project chưa có automation** (`Project_rule.md §Automation Rules`)
- [ ] G1 — TC Review score ≥ 70 (hiện `11_tc-review/review-report-v1.0.md` = **0/100 REJECTED**, phải pass lại trước khi release)

## Ngày Release (Release Day)
- [ ] Smoke test trên production sau khi deploy
- [ ] Theo dõi error logs trong 30 phút
- [ ] Thông báo cho các stakeholders

## Sau Release (Post-Release)
- [ ] Đóng các bug đã resolved trong tracker
- [ ] Lưu trữ kết quả test run
- [ ] Ghi nhận retrospective notes
- [ ] Update MASTER-MEMORY.md version status → "✅ Released"
