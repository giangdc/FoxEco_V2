# Scope Ledger — VR-027 — module DLV — retest bug In review

> Tập chạy: retest 5 bug Jira DLV đang In review (FE-327, FE-331, FE-334, FE-337, FE-338) theo yêu cầu QC, map về 4 TC. TC DLV còn lại giữ nguyên verdict trong `coverage/coverage-DLV.md` (ngoài phạm vi phiên này — chỉ bug In review).
> ⛔ Chưa merge vào coverage / TC-MASTER / §8.

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|-------------------|
| TC-DLV-043 | ✅ PASS | 1 | run này (retest FE-327) | `TC-DLV-043__verify-bam-nut-vao-thang-man-xac-nhan-da-giao.png` |
| TC-DLV-044 | ✅ PASS | 1 | run này (retest FE-334) | `TC-DLV-044__verify-uy-quyen-sdt-1-so-bam-gui-bi-chan.png` |
| TC-DLV-032 | ❌ FAIL | 1 | run này (retest FE-331 + FE-338) | `TC-DLV-032__verify-hen-giao-lai-moi-lich-su-va-nut.png` |
| TC-DLV-035 | ❌ FAIL | 1 | run này (retest FE-337) | `TC-DLV-035__verify-dang-hoan-hang-lich-su-va-nut.png` |
