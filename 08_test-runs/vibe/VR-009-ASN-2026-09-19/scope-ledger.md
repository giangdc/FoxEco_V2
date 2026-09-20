# Scope Ledger — VR-009 — module ASN — SCOPE_TOTAL = 26 TC

> Seed từ: `coverage/coverage-ASN.md` (trạng thái trước phiên: có verdict cuối **10/26**, còn nợ **16**)
> Tập chạy phiên này: **pending 16 TC** (Step 1.2 — QC chọn *"Chỉ 16 TC còn nợ"* 2026-09-19)
> QC chốt thêm cùng lúc: **`006` · `008` · `019` giữ `⏳ NOT_RUN`** (chặn hạ tầng) ⇒ **mục tiêu thực tế = 13 TC**
> Kết quả: **chạy 7 · PASS 7 · còn nợ 9** · Lô: 2 lô · ⏹️ dừng 15:46 (hết sức phiên — xem `vibe-log.md §DỪNG PHIÊN`)
> 8 TC ✅ PASS và 2 TC ⛔ N-A của VR-007/VR-008 giữ nguyên verdict, ⛔ không chạy lại.

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-ASN-001 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-002 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-003 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-004 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-005 | ✅ PASS | 1 | **run này** | `TC-ASN-005__verify-bangtin-khong-co-tin-da-ghep.png` + `TC-ASN-005__verify-hoatdong-khong-co-don-cap-ghep.png` |
| TC-ASN-006 | ⏳ NOT_RUN | — | — | cần **2 thiết bị** bấm `Xác nhận` cách <2s; máy chỉ có 1 AVD `qa_a33`. **QC chốt trong phiên này: giữ NOT_RUN, không nhân bản AVD** |
| TC-ASN-007 | ✅ PASS | 1 | **run này** | `TC-ASN-007__verify-bangtin-vang-tin-da-ghep.png` + `TC-ASN-007__verify-chuong-khong-co-goi-y.png` |
| TC-ASN-008 | ⏳ NOT_RUN | — | — | cần **3 thiết bị** đo mốc ≤5s; chỉ có 1 AVD. **QC chốt trong phiên này: giữ NOT_RUN** |
| TC-ASN-009 | ✅ PASS | — | run trước VR-008 | (seed, không chạy lại) |
| TC-ASN-010 | ✅ PASS | 2 | **run này** | `TC-ASN-010__verify-theo-doi-don-va-sdt-nguoi-gui.png` — kèm phát hiện Steps sai nhãn `"Nhận giao"` |
| TC-ASN-011 | ✅ PASS | 2 | **run này** | `TC-ASN-011__verify-chuong-khong-co-tb-cho-seed-lech-diem-giao.png` |
| TC-ASN-012 | ✅ PASS | 2 | **run này** | `TC-ASN-012__verify-chuong-khong-co-tb-cho-seed-lech-ngay.png` |
| TC-ASN-013 | ✅ PASS | — | run trước VR-007 | (seed, không chạy lại) |
| TC-ASN-014 | ⏳ NOT_RUN | — | — | hết sức phiên — nhóm đếm cần **tuyến OFFER mới sạch + 6 tin NEED + 3 lượt đổi tài khoản**; khung `Chiều` đóng 17:00, dừng lúc 15:46 |
| TC-ASN-015 | ⏳ NOT_RUN | — | — | hết sức phiên — cần OFFER mới sạch + 3 tin NEED (đếm mốc 3) |
| TC-ASN-016 | ⏳ NOT_RUN | — | — | hết sức phiên — cần OFFER mới sạch + 5 tin NEED (đếm mốc 5) |
| TC-ASN-017 | ⏳ NOT_RUN | — | — | hết sức phiên — cần đếm trước/sau khi thêm tin NEED thứ 6 |
| TC-ASN-018 | ⏳ NOT_RUN | — | — | hết sức phiên — cần 3 tin NEED ở 3 mốc thời gian + 1 tin lệch tuyến để kiểm thứ tự |
| TC-ASN-019 | ⏳ NOT_RUN | — | — | cần dev/QA lùi `Đến ngày` để có tin **Hết hạn** — ⛔ không tạo được qua UI |
| TC-ASN-020 | ✅ PASS | 1 | **run này** (chặng step 6–9) + VR-008 (step 1–5) | `TC-ASN-020__verify-carrier-thu-3-ghep-duoc.png` + `TC-ASN-020__verify-vai-carrier-tren-hoat-dong.png` ⇒ **verdict cuối** |
| TC-ASN-021 | ✅ PASS | — | run trước VR-007 | (seed, không chạy lại) |
| TC-ASN-022 | ✅ PASS | 2 | **run này** | `TC-ASN-022__verify-chuong-khong-co-tb-cho-seed-lech-buoi.png` |
| TC-ASN-023 | ✅ PASS | — | run trước VR-007 | (seed, không chạy lại) |
| TC-ASN-024 | ⛔ N-A | — | run trước VR-007 | cần công cụ concurrency/load bắn 50 request thẳng API — ⛔ ngoài phạm vi vibe-test UI thuần |
| TC-ASN-025 | ⏳ NOT_RUN | — | — | hết sức phiên — cần 2 tuyến OFFER độc lập + seed cho tuyến 2 |
| TC-ASN-026 | ⛔ N-A | — | run trước VR-007 | cần API client + kiểm audit log phía server — ⛔ ngoài phạm vi vibe-test UI thuần |

## Tổng kết phiên

| | Số |
|---|--:|
| SCOPE_TOTAL | 26 |
| Chạy **trong run này** | **7** (005 · 007 · 010 · 011 · 012 · 020 · 022) |
| ✅ PASS run này | **7** · ❌ FAIL 0 · 🚫 BLOCKED 0 · ⚠️ NOT_EVIDENCED 0 |
| PASS từ run trước (giữ nguyên) | 8 |
| ⛔ N-A | 2 |
| ⏳ **CÒN NỢ** | **9** |
