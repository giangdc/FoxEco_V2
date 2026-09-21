# Scope Ledger — VR-015 — module ASN — SCOPE_TOTAL = 26 TC

> Seed từ: `coverage/coverage-ASN.md` (trạng thái trước phiên: có verdict cuối **25/26** — 20 PASS · 2 FAIL · 3 BLOCKED — còn nợ **1**)
> Tập chạy phiên này: **pending 1 TC** — `006` *(QC đã cắm 1 real device + 1 emulator, 2026-09-21)*
> Kết quả phiên: **1/1 TC trong tập chạy có verdict cuối — 1 PASS · 0 FAIL · 0 NOT_EVIDENCED**
> Sau phiên: **26/26 có verdict cuối** (21 PASS · 2 FAIL · 3 BLOCKED) — ⛔ không còn NOT_RUN
> 🟢 **Sau phiên (2026-09-21, QC recheck):** `016` + `025` đổi FAIL → PASS (không phải bug) ⇒ **23 PASS · 0 FAIL · 3 BLOCKED**; chỉ v1.1: **10P · 3 BLOCKED / 13**.

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-ASN-001 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-002 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-003 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-004 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-005 | ✅ PASS | — | run trước VR-009 | (seed, không chạy lại) |
| TC-ASN-006 | ✅ PASS | 1 | run này | `TC-ASN-006__verify-nguoi-thang-vao-theo-doi-don.png` + `TC-ASN-006__verify-nguoi-thua-toast-tin-da-co-nguoi-nhan.png` + `TC-ASN-006__verify-chu-tin-thay-1-nguoi-van-chuyen-la-nguoi-thang.png` — đủ mọi vế (đã đăng nhập lại chủ tin) |
| TC-ASN-007 | ✅ PASS | — | run trước VR-009 | (seed, không chạy lại) |
| TC-ASN-008 | 🚫 BLOCKED | — | (QC chốt 2026-09-21) | Cần 3 thiết bị đo ≤5s; môi trường chỉ có 2 |
| TC-ASN-009 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-010 | ✅ PASS | — | run trước VR-009 | (seed, không chạy lại) |
| TC-ASN-011 | ✅ PASS | — | run trước VR-009 | (seed, không chạy lại) |
| TC-ASN-012 | ✅ PASS | — | run trước VR-009 | (seed, không chạy lại) |
| TC-ASN-013 | ✅ PASS | — | run trước VR-007 | (seed, không chạy lại) |
| TC-ASN-014 | ✅ PASS | — | run trước VR-010 | (seed, không chạy lại) |
| TC-ASN-015 | ✅ PASS | — | run trước VR-010 | (seed, không chạy lại) |
| TC-ASN-016 | ✅ PASS | — | VR-010 → đổi PASS 2026-09-21 | QC recheck: không phải bug, sửa Expected (trần 5 theo tài khoản) |
| TC-ASN-017 | ✅ PASS | — | run trước VR-010 | (seed, không chạy lại) |
| TC-ASN-018 | ✅ PASS | — | run trước VR-010 | (seed, không chạy lại) |
| TC-ASN-019 | ✅ PASS | — | run trước VR-010 | (seed, không chạy lại) |
| TC-ASN-020 | ✅ PASS | — | run trước VR-008+VR-009 | (seed, không chạy lại) |
| TC-ASN-021 | ✅ PASS | — | run trước VR-007 | (seed, không chạy lại) |
| TC-ASN-022 | ✅ PASS | — | run trước VR-009 | (seed, không chạy lại) |
| TC-ASN-023 | ✅ PASS | — | run trước VR-007 | (seed, không chạy lại) — QC chấp nhận độ trễ đo được (2026-09-21) |
| TC-ASN-024 | 🚫 BLOCKED | — | (QC chốt 2026-09-21) | Cần công cụ concurrency/load gọi thẳng API — ngoài phạm vi vibe-test UI |
| TC-ASN-025 | ✅ PASS | — | VR-010 → đổi PASS 2026-09-21 | QC recheck: không phải bug, sửa Expected (trần 5 theo tài khoản) |
| TC-ASN-026 | 🚫 BLOCKED | — | (QC chốt 2026-09-21) | Cần API client + kiểm audit log server — ngoài phạm vi vibe-test UI |
