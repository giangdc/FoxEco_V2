# Scope Ledger — VR-023 — module ORD — SCOPE_TOTAL = 88 TC

> Seed từ: `coverage/coverage-ORD.md` (trạng thái trước phiên: có verdict 85/88).
> Tập chạy phiên này: **retest 3 TC** gắn bug Jira đang In review (FE-302/303/304) theo yêu cầu QC. 85 TC còn lại không chạm — giữ nguyên verdict trong `coverage-ORD.md`.
> ⛔ Chưa merge kết quả vào `coverage-ORD.md` / TC-MASTER / §8 — QC chỉ yêu cầu recheck + comment Jira.

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|-------------------|
| TC-ORD-053 | ❌ FAIL | 1 | run này (retest FE-302) | `TC-ORD-053__step4-FAIL-khong-co-popup-thoat.png` |
| TC-ORD-059 | ✅ PASS | 1 | run này (retest FE-303) | `TC-ORD-059__verify-buoi-sang-da-qua-bi-chan.png` |
| TC-ORD-058 | ✅ PASS | 1 | run này (retest FE-304) | `TC-ORD-058__verify-buoi-mac-dinh-need.png` |
| TC-ORD-080 | ⚠️ NOT_EVIDENCED | — | coverage-ORD.md (run trước) | ngoài phạm vi retest phiên này (chỉ 3 TC gắn bug In review) |
| TC-ORD-067 | ⏳ NOT_RUN | — | coverage-ORD.md | ngoài phạm vi retest phiên này |
| TC-ORD-082 | ⏳ NOT_RUN | — | coverage-ORD.md | ngoài phạm vi retest phiên này |
| 82 TC còn lại | (giữ nguyên verdict) | — | coverage-ORD.md | không nằm trong phạm vi retest |
