# Scope Ledger — VR-029 — module TS — SCOPE_TOTAL = 17 TC

> Mode **RETEST** theo yêu cầu QC 2026-09-24: chỉ **v1.1** (`TC-TS-008..024`), tập chạy = 5 TC cần chạy lại sau khi sửa Expected theo quyết định BA (`C-TS-04`) + `FE-325` Fixed: `TC-TS-009` · `012` · `013` · `016` · `021`.
> Seed từ: `coverage/coverage-TS.md` (17 dòng) — 12 TC không chạm giữ nguyên verdict cũ.
> Thiết bị: `emulator-5554` (QC đã đăng nhập sẵn FoxEco + tài khoản Microsoft "Giang"). Lô 1/1.
> ⚠️ Lệch setup so với script: dùng đơn sẵn có trên máy ở trạng thái **Đã ghép** (vai người gửi) thay vì dựng `SEED-TS-01` CP2 `IN_TRANSIT` với vai B — nút "Báo cáo sự cố" + form giống nhau ở mọi trạng thái/vai (`C-TS-02(a)`), 5 TC này chỉ kiểm nội dung form nên không ảnh hưởng kết luận.

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-TS-008 | ✅ PASS | — | giữ nguyên từ `coverage-TS.md` (run VR-019 follow-up) | không nằm trong tập retest |
| TC-TS-009 | ✅ PASS | 1 | run này (retest) | `TC-TS-009__pre-form-filled-2-anh.png` + `__verify-man-xac-nhan-mac-dinh-ms-forms.png` |
| TC-TS-010 | ✅ PASS | — | giữ nguyên từ `coverage-TS.md` (run VR-019 follow-up) | không nằm trong tập retest |
| TC-TS-011 | ✅ PASS | — | giữ nguyên từ `coverage-TS.md` (run VR-019 follow-up) | không nằm trong tập retest |
| TC-TS-012 | ✅ PASS | 1 | run này (retest) | `TC-TS-012__pre-sdt-0912abc-form-filled.png` + `__verify-sdt-0912abc-gui-thanh-cong.png` |
| TC-TS-013 | ✅ PASS | 1 | run này (retest) | `TC-TS-013__pre-form-filled-0-anh.png` + `__verify-0-anh-gui-thanh-cong.png` |
| TC-TS-014 | ✅ PASS | — | giữ nguyên từ `coverage-TS.md` (run VR-019 follow-up) | không nằm trong tập retest |
| TC-TS-015 | ✅ PASS | — | giữ nguyên từ `coverage-TS.md` (run VR-019 follow-up) | không nằm trong tập retest |
| TC-TS-016 | ❌ FAIL | 1 | run này (retest) | `TC-TS-016__step6-FAIL-app-ve-man-loi-co-nut-thu-lai.png` + `__verify-mat-mang-man-loi-app.png` — app nay tự vẽ màn lỗi + nút "Thử lại", khác Expected sửa 2026-09-24 |
| TC-TS-017 | ⛔ N-A | — | TC-MASTER `DESCOPED` + `Skipped` 2026-09-24 | BA bỏ vế mất mạng của `BR16-04` (`FE-322`, `C-TS-04(a)`) — không tính vào mẫu số |
| TC-TS-018 | ✅ PASS | — | giữ nguyên từ `coverage-TS.md` (run VR-019) | không nằm trong tập retest |
| TC-TS-019 | ✅ PASS | — | giữ nguyên từ `coverage-TS.md` (run VR-019 follow-up) | không nằm trong tập retest |
| TC-TS-020 | ✅ PASS | — | giữ nguyên từ `coverage-TS.md` (run VR-019 follow-up) | không nằm trong tập retest |
| TC-TS-021 | ✅ PASS | 1 | run này (retest) | `TC-TS-021__verify-madon-sua-duoc-chen-x.png` |
| TC-TS-022 | ✅ PASS | — | giữ nguyên từ `coverage-TS.md` (run VR-019) | không nằm trong tập retest |
| TC-TS-023 | ✅ PASS | — | giữ nguyên từ `coverage-TS.md` (run VR-019) | không nằm trong tập retest |
| TC-TS-024 | ✅ PASS | — | giữ nguyên từ `coverage-TS.md` (run VR-019 follow-up) | không nằm trong tập retest |
