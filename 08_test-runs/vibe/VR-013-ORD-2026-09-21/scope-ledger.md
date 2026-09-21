# Scope Ledger — VR-013 — module ORD — SCOPE_TOTAL = 88 TC

> Seed từ: `coverage/coverage-ORD.md` (trạng thái trước phiên: có verdict cuối 66/88 · nợ 22)
> Tập chạy phiên này: **theo chỉ định của QC (không dùng `--all`)** — 22 TC còn nợ + `TC-ORD-004` (gắn `BUG-020`) + `TC-ORD-068` (gắn `BUG-019`) = **24 TC**. Lô: 1 = đăng tin/xem đơn trên EMU · 2 = đối chiếu 2 thiết bị (EMU + máy thật).
> **Chạy trong run này: 22 TC** · TC khác giữ nguyên verdict cũ (không reset).

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-ORD-001 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-001__verify-dang-tin-moi-4-thanh-phan.png` |
| TC-ORD-002 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-002__verify-buoc-1-3-thong-tin-hang.png` |
| TC-ORD-003 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-003__verify-form-1-trang-khong-step-indicator.png` |
| TC-ORD-004 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-004__verify-man-dang-tin-thanh-cong.png` |
| TC-ORD-005 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-005__verify-8-chip-mac-dinh-tai-lieu.png` |
| TC-ORD-006 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-006__step3-FAIL-co-chip-tai-lieu.png` |
| TC-ORD-007 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-007__verify-nhan-lai-chip-van-duoc-chon.png` |
| TC-ORD-008 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-008__step6-FAIL-tiep-theo-van-disable-sau-khi-chon-thap.png` |
| TC-ORD-009 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-009__verify-banner-hang-gia-tri-cao.png` |
| TC-ORD-010 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-010__verify-thap-khong-co-banner.png` |
| TC-ORD-011 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-011__verify-ghi-chu-dung-300-ky-tu.png` |
| TC-ORD-012 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-012__verify-bo-dem-1-tren-5.png` |
| TC-ORD-013 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-013__verify-anh-hang-bat-buoc-0-5-helper.png` |
| TC-ORD-014 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-014__step4-FAIL-khong-sang-buoc-2-khong-bao-loi-anh.png` |
| TC-ORD-015 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-015__verify-prefill-ten-sdt-nguoi-gui.png` |
| TC-ORD-016 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-016__verify-ten-nguoi-gui-chi-doc.png` |
| TC-ORD-017 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-017__step3-FAIL-dia-chi-lay-hang-khong-prefill.png` |
| TC-ORD-018 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-018__verify-sdt-nguoi-gui-khong-doi.png` |
| TC-ORD-019 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-019__step4-FAIL-autofill-thieu-o-dia-chi-giao.png` |
| TC-ORD-020 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-020__verify-email-khong-tra-duoc.png` |
| TC-ORD-021 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-021__step3-FAIL-khong-bao-loi-email-sai-dinh-dang.png` |
| TC-ORD-022 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-022__verify-sdt-autofill-duoc-chap-nhan-sang-buoc-3.png` |
| TC-ORD-023 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-023__step5-FAIL-khong-co-thong-bao-loi-nhom-nguoi-nhan.png` |
| TC-ORD-024 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-024__verify-ten-nguoi-nhan-bien-60-61.png` |
| TC-ORD-025 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-025__verify-sdt-10-so-hop-le.png` |
| TC-ORD-026 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-026__verify-loi-trung-dia-chi-hien-dung.png` |
| TC-ORD-027 | ✅ PASS | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-027__verify-prefill-va-sua-duoc.png` |
| TC-ORD-028 | ✅ PASS | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-028__verify-o-van-ban-tu-do.png` |
| TC-ORD-029 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-029__verify-dropdown-autocomplete-khong-co-chip-preset.png` |
| TC-ORD-030 | ✅ PASS | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-030__verify-chan-ngay-qua-khu.png` |
| TC-ORD-031 | ✅ PASS | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-031__verify-chan-den-ngay-som-hon.png` |
| TC-ORD-032 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-032__verify-gio-nao-cung-duoc-bo-chon-cac-buoi.png` |
| TC-ORD-033 | 🚫 BLOCKED | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-033__step5-BLOCKED-v11-khong-co-khung-gio-mac-dinh.png` |
| TC-ORD-034 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-034__verify-tom-tat-buoc-3.png` |
| TC-ORD-035 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-035__verify-banner-hang-cam.png` |
| TC-ORD-036 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-036__verify-checkbox-dieu-khoan-chua-tick.png` |
| TC-ORD-037 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-037__verify-step6-dang-tin-ngay-enable.png` |
| TC-ORD-038 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-038__verify-thuoc-y-te-dang-thanh-cong-khong-bi-chan.png` |
| TC-ORD-039 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-039__verify-man-thanh-cong-khong-ma-don-du-2-nut.png` |
| TC-ORD-040 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-040__verify-buoc-5-ve-trang-chu-tab-trang-chu-active.png` |
| TC-ORD-041 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-041__verify-khong-co-ma-tin-trong-noi-dung.png` |
| TC-ORD-042 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-042__verify-form-offer-nhom-truong-giua.png` |
| TC-ORD-043 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-043__step8-FAIL-khong-co-thong-bao-loi-diem-den-trung.png` |
| TC-ORD-044 | ✅ PASS | 2 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-044__verify-bang-tin-b-mot-danh-sach-khong-tab-khong-o-tim-kiem-khong-co-offer-cua-a.png` |
| TC-ORD-045 | ✅ PASS | 2 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-045__verify-bang-tin-tai-khoan-b-cuon-het-khong-co-tin-offer-cua-a.png` |
| TC-ORD-046 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-046__verify-dia-chi-moi-fpt-cau-giay-van-cho-ghep.png` |
| TC-ORD-047 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-047__verify-tin-da-ghep-khong-co-nut-chinh-sua.png` |
| TC-ORD-048 | ✅ PASS | 2 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-048__verify-bang-tin-tai-khoan-b-khong-con-tin-het-han-19-9.png` |
| TC-ORD-049 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-049__verify-lich-su-moc-dang-tin-10-14.png` |
| TC-ORD-050 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-050__step8-FAIL-offer-nut-gui-enabled-khi-thieu-du-lieu.png` |
| TC-ORD-051 | ❌ FAIL | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-051__step3-FAIL-khong-co-loi-duoi-o-ten-nguoi-nhan.png` |
| TC-ORD-052 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-052__verify-tom-tat-ten-da-trim-sdt-chi-con-chu-so.png` |
| TC-ORD-053 | ❌ FAIL | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-053__step4-FAIL-khong-co-popup-thoat.png` |
| TC-ORD-054 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-054__verify-khong-co-field-so-tien.png` |
| TC-ORD-055 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-055__verify-dia-chi-giao-dung-200-ky-tu.png` |
| TC-ORD-056 | ✅ PASS | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-056__verify-khoang-7-ngay-duoc-nhan.png` |
| TC-ORD-057 | ✅ PASS | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-057__verify-loi-toi-da-7-ngay.png` |
| TC-ORD-058 | ❌ FAIL | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-058__verify-buoi-mac-dinh.png` |
| TC-ORD-059 | ❌ FAIL | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-059__step4-FAIL-chon-duoc-buoi-da-qua.png` |
| TC-ORD-060 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-060__verify-dia-chi-giao-giu-nguyen-sau-huy-sua.png` |
| TC-ORD-061 | ✅ PASS | 2 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-061__verify-chi-tiet-tin-da-ghep-khong-badge-het-han.png` |
| TC-ORD-062 | ✅ PASS | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-062__verify-form-trang-khong-nhap.png` |
| TC-ORD-063 | ❌ FAIL | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-063__step6-FAIL-chan-nhung-khong-co-thong-bao-loi.png` |
| TC-ORD-064 | ❌ FAIL | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-064__step6-FAIL-chan-nhung-khong-co-thong-bao-loi.png` |
| TC-ORD-065 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-065__verify-tren-10-kg-dang-thanh-cong-khong-canh-bao.png` |
| TC-ORD-066 | ❌ FAIL | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-066__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png` |
| TC-ORD-067 | ⏳ NOT_RUN | — | — | ⏳ chưa chạy trong phiên này — xem `vibe-report.md §Còn nợ` |
| TC-ORD-068 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-068__verify-6mib-bi-tu-choi-thong-bao-5mb-bo-dem-0-5.png` |
| TC-ORD-069 | 🚫 BLOCKED | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-069__step2-BLOCKED-picker-chi-co-anh.png` |
| TC-ORD-070 | ✅ PASS | — | run trước VR-002 *(recheck)* (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-070__verify-du-5-anh-an-o-them-anh.png` |
| TC-ORD-071 | ✅ PASS | — | run trước VR-002 *(recheck)* (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-071__verify-bo-dem-4-tren-5-nut-them-hien-lai.png` |
| TC-ORD-072 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-072__verify-dai-anh-luot-sang-anh-2-badge-2-tren-5.png` |
| TC-ORD-073 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-073__verify-cham-nen-toi-khong-dong-lightbox.png` |
| TC-ORD-074 | ❌ FAIL | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-074__step5-FAIL-dia-chi-giao-khong-tu-dien.png` |
| TC-ORD-075 | ✅ PASS | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-075__verify-email-la-chan-tao-don.png` |
| TC-ORD-076 | ✅ PASS | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-076__verify-email-nghi-viec-chan.png` |
| TC-ORD-077 | ❌ FAIL | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-077__step4-FAIL-khong-co-loi-dinh-dang.png` |
| TC-ORD-078 | ✅ PASS | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-078__verify-email-ngoai-ten-mien.png` |
| TC-ORD-079 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-079__verify-sdt-uy-quyen-sai-dinh-dang-bao-loi.png` |
| TC-ORD-080 | ⚠️ NOT_EVIDENCED | 3 | run này | `TC-ORD-080__pre-khoi-uy-quyen-nguyen-van-bay-0912345678.png` — chạy 4/5 step; thiếu màn chứng minh Expected, xem vibe-log |
| TC-ORD-081 | ✅ PASS | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-081__verify-ten-uy-quyen-1-ky-tu-bi-chan.png` |
| TC-ORD-082 | ⏳ NOT_RUN | — | — | ⏳ chưa chạy trong phiên này — xem `vibe-report.md §Còn nợ` |
| TC-ORD-083 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-083__verify-chon-goi-y-trung-o-lai-buoc-2-hien-loi-dia-chi-giao-phai-khac.png` |
| TC-ORD-084 | 🚫 BLOCKED | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-084__step5-BLOCKED-them-khoang-trang-mat-goi-y-nut-khoa-khong-co-loi.png` |
| TC-ORD-085 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-085__verify-chip-da-copy-xanh-khi-vua-bam.png` |
| TC-ORD-086 | 🚫 BLOCKED | — | run trước VR-004 (seed, không chạy lại) | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-086__step3-BLOCKED-khong-co-sdt-tren-man-chi-tiet.png` |
| TC-ORD-087 | ✅ PASS | — | run trước VR-002 (seed, không chạy lại) | `VR-002-ORD-2026-09-18/screenshots/TC-ORD-087__verify-xoa-anh-1-con-1-5.png` |
| TC-ORD-088 | ✅ PASS | 1 | run này | `VR-013-ORD-2026-09-21/screenshots/TC-ORD-088__verify-sau-khi-luu-don-chi-con-4-anh.png` |
