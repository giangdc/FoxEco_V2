# Scope Ledger — VR-014 — module HOME — SCOPE_TOTAL = 32 TC

> Seed từ: `coverage/coverage-HOME.md` (trước phiên: có verdict cuối 17/32 · nợ 15)
> Tập chạy phiên này: **`--pending` CHỈ TC v1.1** (QC chỉ định) = 9 TC nợ: `008 019 021 025 027 028 029 030 031`. Chạy được **5** (`019 021 025 027 028`); **4** giữ nợ vì QC không cho phép ghép đơn / vòng giao–nhận (`008 029 030 031`). TC v1.0 CARRIED không đụng.

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-HOME-001 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-001__verify-bottom-nav-5-tabs.png` |
| TC-HOME-002 | 🚫 BLOCKED | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-002__step2-BLOCKED-bang-tin-0-tin.png` |
| TC-HOME-003 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-003__verify-greeting-name.png` |
| TC-HOME-004 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (TC v1.0 CARRIED — QC chỉ yêu cầu v1.1) · **Lý do:** cần **3 tài khoản** giữ 3 vai trên cùng 1 đơn + đăng xuất/đăng nhập ×3 (**OTP nhập tay**). 🔍 Quan s |
| TC-HOME-005 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-005__verify-chuong-cham-do.png` |
| TC-HOME-006 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-006__verify-chuong-khong-cham-do.png` |
| TC-HOME-007 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-007__verify-tagline-giup-dong-nghiep.png` |
| TC-HOME-008 | ⏳ NOT_RUN | — | — | ⏳ **Chưa chạy — QC không cho phép chạy vòng giao–nhận đến Hoàn thành ở VR-014** (cần A nhận đơn → giao → C xác nhận, đổi trạng thái đơn thật). Lý do cũ (bug `B1`, OTP nhập tay) **đã lỗi thời**: đăng NEED được (VR-013), OTP cố định |
| TC-HOME-009 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-009__verify-6-thanh-phan-don-cua-toi.png` |
| TC-HOME-010 | ⛔ N-A | — | run trước — | **DESCOPED** — `SC-HOME-010` DEPRECATED ở v1.1 — `C-HOME-05` Resolved 2026-09-17: BA chốt **HIỆN** empty state `EMP-02`, |
| TC-HOME-011 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-011__verify-nhan-vai-gui.png` |
| TC-HOME-012 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-012__verify-nhan-vai-giao.png` |
| TC-HOME-013 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-013__verify-nhan-vai-nhan.png` |
| TC-HOME-014 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (TC v1.0 CARRIED — QC chỉ yêu cầu v1.1) · **Lý do:** cần đẩy **1 đơn** qua 4 trạng thái liên tiếp với tài khoản Carrier + Receiver (OTP nhập tay) và đăn |
| TC-HOME-015 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-015__verify-lo-trinh-khop.png` |
| TC-HOME-016 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-016__verify-mo-man-hoat-dong.png` |
| TC-HOME-017 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (TC v1.0 CARRIED — QC chỉ yêu cầu v1.1) · **Lý do:** cần ≥1 tin NEED hợp lệ do **tài khoản khác** đăng; STG hiện **0 tin** (xác nhận 2 bề mặt, `_recon__ |
| TC-HOME-018 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (TC v1.0 CARRIED — QC chỉ yêu cầu v1.1) · **Lý do:** cần ≥1 tin NEED hợp lệ do **tài khoản khác** đăng; STG hiện **0 tin** (xác nhận 2 bề mặt, `_recon__ |
| TC-HOME-019 | ✅ PASS | 1 | run này | `TC-HOME-019__verify-tin-moi-hien-5-tin-khi-he-thong-co-6-tin.png` |
| TC-HOME-020 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (TC v1.0 CARRIED — QC chỉ yêu cầu v1.1) · **Lý do:** cần ≥1 tin NEED hợp lệ do **tài khoản khác** đăng; STG hiện **0 tin** (xác nhận 2 bề mặt, `_recon__ |
| TC-HOME-021 | ✅ PASS | 1 | run này | `TC-HOME-021__verify-nhan-xem-them-mo-man-bang-tin.png` |
| TC-HOME-022 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-022__verify-chuyen-tab-bang-tin.png` |
| TC-HOME-023 | ⏳ NOT_RUN | — | — | ngoài phạm vi phiên này (TC v1.0 CARRIED — QC chỉ yêu cầu v1.1) · **Lý do:** cần ≥1 tin NEED hợp lệ do **tài khoản khác** đăng; STG hiện **0 tin** (xác nhận 2 bề mặt, `_recon__ |
| TC-HOME-024 | ⛔ N-A | — | run trước — | **DESCOPED** — `SC-HOME-024` DEPRECATED ở v1.1 — tách thành 3 SC atomic `EMP-01/02/03`; thay bằng `TC-HOME-026/027/028`. |
| TC-HOME-025 | ❌ FAIL | 1 | run này | `TC-HOME-025__step4-FAIL-van-co-nut-xem-them-khi-dung-5-tin.png` |
| TC-HOME-026 | ✅ PASS | — | run trước VR-005 (seed, không chạy lại) | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-026__verify-empty-state-tin-moi.png` |
| TC-HOME-027 | ❌ FAIL | 1 | run này | `TC-HOME-027__step3-FAIL-empty-state-chua-co-don-nao-thieu-cta-tao-don-gui-hang.png` |
| TC-HOME-028 | 🚫 BLOCKED | 1 | run này | `TC-HOME-028__step3-BLOCKED-cong-dong-325-don-khong-phai-0-he-thong-da-co-don-hoan-thanh.png` |
| TC-HOME-029 | ⏳ NOT_RUN | — | — | ⏳ **Chưa chạy — cần vòng giao–nhận đến Hoàn thành (QC không cho phép ở VR-014).** Tài khoản "sạch" nay có: `stag_thuyntt22@` (0 đơn, 0 đóng góp). Cần Thủy đăng NEED khai C nhận, B giao tới `Đã giao`, C xác nhận rồi xem hero của Th |
| TC-HOME-030 | ⏳ NOT_RUN | — | — | ⏳ **Chưa chạy — thiếu 1 tin `Đã ghép` còn hạn:** cần ghép 1 tin bằng tài khoản thứ 3 (QC không cho phép ghép đơn P3 ở VR-014) + tin hết hạn (có sẵn `Gửi tài liệu 19/9`) + tin của chính người xem (có). Chạy tiếp: `/vibe-test --modu |
| TC-HOME-031 | ⏳ NOT_RUN | — | — | ⏳ **Chưa chạy — cần vòng giao–nhận đến Hoàn thành (QC không cho phép ở VR-014).** Mốc nền hôm nay: cộng đồng `325 đơn · 23743 người` (Thủy, 15:00). Chạy tiếp: `/vibe-test --module HOME --tc TC-HOME-031` |
| TC-HOME-032 | ⛔ N-A | — | run trước — | **Lý do:** NFR hiệu năng — cần môi trường load-test mô phỏng **1.000 user đồng thời** trên 4G + công cụ đo p95; ⛔ **khôn |
