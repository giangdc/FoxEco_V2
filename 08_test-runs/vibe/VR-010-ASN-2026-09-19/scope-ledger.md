# Scope Ledger — VR-010 — module ASN — SCOPE_TOTAL = 26 TC

> Seed từ: `coverage/coverage-ASN.md` (trạng thái trước phiên: có verdict cuối **17/26**, còn nợ 9)
> Tập chạy phiên này: **pending 7 TC** — `014` `015` `016` `017` `018` `025` `019`
> 🔴 **`TC-ASN-006` + `TC-ASN-008` CỐ Ý KHÔNG chạy phiên này** — QC chốt 2026-09-19 16:30:
>   *"2 emulator thôi nhé, case nào cần 2 emulator thì để lại giúp t"* ⇒ nhóm đa thiết bị QC tự chạy.
>   Máy hiện tại: **1 emulator**, RAM tổng 7GB / trống ~2GB ⇒ bật máy thứ 2 có rủi ro OOM giết emulator đang chạy.
> Kết quả phiên: **7/7 TC trong tập chạy đều có verdict cuối — 5 PASS · 2 FAIL · 0 NOT_EVIDENCED**
> Lô: 4 TC/lô (TC nhóm trần rất nặng seed — mỗi TC tốn nhiều lượt đổi tài khoản)

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-ASN-001 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-002 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-003 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-004 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-005 | ✅ PASS | — | run trước VR-009 | (seed, không chạy lại) |
| TC-ASN-006 | ⏳ NOT_RUN | — | — | **QC để lại** — cần 2 thiết bị bấm cách <2s; QC chốt 16:30 tự chạy nhóm đa thiết bị |
| TC-ASN-007 | ✅ PASS | — | run trước VR-009 | (seed, không chạy lại) |
| TC-ASN-008 | ⏳ NOT_RUN | — | — | **QC để lại** — cần 3 thiết bị đo ≤5s; QC chốt 16:30 tự chạy nhóm đa thiết bị |
| TC-ASN-009 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-010 | ✅ PASS | — | run trước VR-009 | (seed, không chạy lại) |
| TC-ASN-011 | ✅ PASS | — | run trước VR-009 | (seed, không chạy lại) |
| TC-ASN-012 | ✅ PASS | — | run trước VR-009 | (seed, không chạy lại) |
| TC-ASN-013 | ✅ PASS | — | run trước VR-007 | (seed, không chạy lại) |
| TC-ASN-014 | ✅ PASS | 1 | run này | `TC-ASN-014__verify-toi-da-5-goi-y.png` — ⚠️ cận trên chưa bị chạm, xem log |
| TC-ASN-015 | ✅ PASS | 1 | run này | `TC-ASN-015__verify-dung-3-thong-bao.png` |
| TC-ASN-016 | ❌ FAIL | 1 | run này | `TC-ASN-016__step3-FAIL-chi-4-thong-bao-moi.png` + `TC-ASN-016__pre-du-5-tin-need-tren-bang-tin.png` |
| TC-ASN-017 | ✅ PASS | 1 | run này | `TC-ASN-017__verify-so-thong-bao-khong-doi.png` — ⚠️ tiền đề chưa đạt, xem log |
| TC-ASN-018 | ✅ PASS | 3 | run này | `TC-ASN-018__verify-thu-tu-goi-y.png` + `TC-ASN-018__verify-dinh-danh-r3b-tren-cung.png` + `TC-ASN-018__pre-seed-r3b-dang-sau.png` |
| TC-ASN-019 | ✅ PASS | 4 | run này | `TC-ASN-019__verify-thong-bao-chi-tro-tin-con-song.png` + `TC-ASN-019__verify-bangtin-vang-tin-het-han.png` + `TC-ASN-019__pre-tin-need-het-han-ngay-hom-nay.png` |
| TC-ASN-020 | ✅ PASS | — | run trước VR-008+VR-009 | (seed, không chạy lại) |
| TC-ASN-021 | ✅ PASS | — | run trước VR-007 | (seed, không chạy lại) |
| TC-ASN-022 | ✅ PASS | — | run trước VR-009 | (seed, không chạy lại) |
| TC-ASN-023 | ✅ PASS | — | run trước VR-007 | (seed, không chạy lại) |
| TC-ASN-024 | ⛔ N-A | — | (giữ nguyên) | Cần công cụ concurrency/load gọi thẳng API (JMeter/k6) — ngoài phạm vi vibe-test UI |
| TC-ASN-025 | ❌ FAIL | 2 | run này | `TC-ASN-025__step3-FAIL-tuyen-2-khong-co-thong-bao.png` + `TC-ASN-025__pre-seed-r2-khop-tuyen-2.png` |
| TC-ASN-026 | ⛔ N-A | — | (giữ nguyên) | Cần API client + kiểm audit log server — ngoài phạm vi vibe-test UI |
