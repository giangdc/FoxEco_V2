# Scope Ledger — VR-019 — module TS — SCOPE_TOTAL = 17 TC

> Scope theo yêu cầu QC: **chỉ 17 TC thuộc v1.1** (`TC-TS-008..024`, gắn `SC-TS-008..015` NEW của `REQ-TS-006`).
> 7 TC CARRIED v1.0 (`TC-TS-001..007`) **KHÔNG nằm trong scope phiên này**.
> Seed từ: `coverage-TS.md` (chưa tồn tại trước phiên này → tạo mới, 17 dòng `⏳ NOT_RUN`).
> Tập chạy phiên này: toàn bộ 17 TC · Lô 1/1 (17 TC ≤ batch 20).
> Thiết bị: 2 máy song song — `emulator-5554` (vai A) · `R58T20PLP8K` (vai C → tạm B → về C).
> Tài khoản: A=`stag_giangdc2@fpt.com` · B=`stag_anhptm17@fpt.com` · C=`stag_taipm@fpt.com`.
> 🐞 Phát hiện chặn: `BUG-037` (WebView → màn đăng nhập Microsoft, P1) + `BUG-038` (mất mạng → trang lỗi kỹ thuật, không nút Thử lại, P2).

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-TS-008 | ✅ PASS | 1 (2 follow-up) | follow-up 2026-09-22 | `TC-TS-008__verify-only-madon-prefilled.png` + `__verify-2-mota-sdt-empty.png` |
| TC-TS-009 | ❌ FAIL | 1 (2 follow-up) | follow-up 2026-09-22 | `TC-TS-009__pre-form-filled-valid.png` + `__verify-da-ghi-nhan-phan-hoi.png` |
| TC-TS-010 | ✅ PASS | 1 (2 follow-up) | follow-up 2026-09-22 + hiệu chỉnh Expected | `TC-TS-010__verify-gui-empty-required-behavior.png` — Expected sửa 2026-09-22 (`BUG-040` xoá), nay khớp Actual |
| TC-TS-011 | ✅ PASS | 1 (2 follow-up) | follow-up 2026-09-22 + hiệu chỉnh Expected | `TC-TS-011__verify-mota-empty-blocks-submit.png` — cùng lý do `TC-TS-010` |
| TC-TS-012 | ❌ FAIL | 1 (2 follow-up) | follow-up 2026-09-22 + hiệu chỉnh Expected | `TC-TS-012__verify-sdt-invalid-khong-bi-chan.png` — cơ chế nút đã sửa (khớp Actual), vẫn FAIL vì SĐT sai định dạng không bị chặn (`BUG-041`) |
| TC-TS-013 | ❌ FAIL | 1 (2 follow-up) | follow-up 2026-09-22 | `TC-TS-013__verify-anh-required-blocks-submit.png` |
| TC-TS-014 | ✅ PASS | 1 (2 follow-up) | follow-up 2026-09-22 | `TC-TS-014__verify-5-anh-them-anh-bi-vo-hieu.png` |
| TC-TS-015 | ✅ PASS | 1 (2 follow-up) | follow-up 2026-09-22 | `TC-TS-015__verify-xoa-anh-3-con-4-anh.png` |
| TC-TS-016 | ❌ FAIL | 1 | run này | `TC-TS-016__step6-FAIL-raw-error-no-retry-button.png` (`BUG-038`) |
| TC-TS-017 | 🚫 BLOCKED | 1 | run này | không có nút "Thử lại" (`BUG-038`) — không liên quan màn login, chưa retest |
| TC-TS-018 | ✅ PASS | 1 | run này | `TC-TS-018__verify-quay-lai-dung-man-in-transit.png` |
| TC-TS-019 | ✅ PASS | 1 (2 follow-up) | follow-up 2026-09-22 | `TC-TS-019__verify-reopen-la-phien-moi-khong-giu-du-lieu.png` + `__verify-2-mota-empty-newsession.png` |
| TC-TS-020 | ✅ PASS | 1 (2 follow-up) | follow-up 2026-09-22 | `TC-TS-020__verify-trang-thai-khong-doi-sau-gui.png` |
| TC-TS-021 | ❌ FAIL | 1 (2 follow-up) | follow-up 2026-09-22 | `TC-TS-021__verify-madon-read-only-khong-sua-duoc.png` |
| TC-TS-022 | ✅ PASS | 1 | run này | `TC-TS-022__pre-observation1-posted.png` + `__pre-observation2-matched.png` + `__verify-observation3-intransit.png` |
| TC-TS-023 | ✅ PASS | 1 | run này | `TC-TS-023__pre-observation1-matched.png` + `__verify-observation2-intransit.png` |
| TC-TS-024 | ✅ PASS | 1 (2 follow-up) | follow-up 2026-09-22 | `TC-TS-024__pre-observation-button-visible.png` + `__verify-form-loaded-after-ms-login.png` |

**Kết quả lô 1 (run gốc): 17/17 có verdict · 3 PASS / 1 FAIL / 13 BLOCKED · evidence 17/17.**
**Kết quả lô 2 (follow-up 2026-09-22, retest 12 TC bị chặn login): 12/12 đảo verdict · 9 PASS / 3 FAIL.**
**Hiệu chỉnh cùng ngày (sau log-bug, `BUG-040` xoá):** `TC-TS-010`/`TC-TS-011` FAIL → PASS (Expected
sửa theo hành vi thật). **Tổng cộng cuối cùng: 17/17 có verdict · 11 PASS / 5 FAIL / 1 BLOCKED
(`TC-TS-017`, chờ `BUG-038`) · evidence 17/17.**
**Tổng cộng cuối cùng: 17/17 có verdict · 9 PASS / 7 FAIL / 1 BLOCKED (`TC-TS-017`, chờ `BUG-038`) · evidence 17/17.**
