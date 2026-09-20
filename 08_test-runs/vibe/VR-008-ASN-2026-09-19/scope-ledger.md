# Scope Ledger — VR-008 — module ASN — SCOPE_TOTAL = 26 TC

> Seed từ: `coverage/coverage-ASN.md` (trạng thái trước phiên: có verdict **5/26**, còn nợ **21**)
> ⏸️ **PHIÊN DỪNG 2026-09-19 12:33 theo yêu cầu QC ("mai tiếp").** Chạy được **5 TC** (001·002·003·004·009), tất cả ✅ PASS.
> Tập chạy phiên này: **pending 21 TC** (Step 1.2 — QC chọn "chỉ TC còn nợ") · Lô mặc định ~7 TC
> ⚠️ 3 TC đã PASS ở VR-007 giữ nguyên verdict, KHÔNG chạy lại. 2 TC ⛔ N-A giữ nguyên.

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-ASN-001 | ✅ PASS | 1 | run này | `TC-ASN-001__verify-card-da-ghep.png` |
| TC-ASN-002 | ✅ PASS | 1 | run này | `TC-ASN-002__verify-huy-giu-cho-ghep.png` |
| TC-ASN-003 | ✅ PASS | 1 | run này | `TC-ASN-003__verify-khong-co-nut-duyet.png` |
| TC-ASN-004 | ✅ PASS | 1 | run này | `TC-ASN-004__verify-a-thay-sdt-b.png` |
| TC-ASN-005 | ⏳ NOT_RUN | 1 | — | cần tài khoản D ngoài cặp ghép (Tin 2 đã `Đã ghép` sẵn làm tiền đề) — hết phiên |
| TC-ASN-006 | ⏳ NOT_RUN | 4 | — | cần **2 thiết bị** bấm cách <2s — chỉ có 1 emulator; QC chốt cố chạy thật ở lô 4, phiên dừng trước lô 4 |
| TC-ASN-007 | ⏳ NOT_RUN | 1 | — | cần tài khoản C khác cặp để kiểm tin đã ghép biến mất khỏi Bảng tin (Tin 2 sẵn sàng) — hết phiên |
| TC-ASN-008 | ⏳ NOT_RUN | 4 | — | cần **3 thiết bị** đo mốc ≤5s — chỉ có 1 emulator; QC chốt cố chạy thật ở lô 4, phiên dừng trước lô 4 |
| TC-ASN-009 | ✅ PASS | 2 | run này | `TC-ASN-009__verify-tro-dung-tin-seed-s1.png` |
| TC-ASN-010 | ⏳ NOT_RUN | 2 | — | **dừng phiên theo yêu cầu QC 12:33.** Đang đứng đúng màn Chi tiết tin SEED S1 mở từ thông báo; chưa bấm CTA. ⚠️ CTA thật là `Tôi mang giúp được`, không phải `Nhận giao` như Steps ⇒ phải chạy thật rồi mới kết luận |
| TC-ASN-011 | ⏳ NOT_RUN | 2 | — | **dừng phiên theo yêu cầu QC 12:33.** Seed S2 (lệch điểm giao) ĐÃ đăng xong; chuông 12:31 không có mốc trùng giờ đăng seed ⇒ dấu hiệu thuận, nhưng **thiếu ảnh evidence riêng cho TC này** (cấm 1 ảnh cho nhiều TC) ⇒ ⛔ không khai PASS |
| TC-ASN-012 | ⏳ NOT_RUN | 2 | — | **dừng phiên theo yêu cầu QC 12:33.** Seed S3 (lệch khoảng ngày) ĐÃ đăng xong; chuông 12:31 không có mốc trùng giờ đăng seed ⇒ dấu hiệu thuận, nhưng **thiếu ảnh evidence riêng cho TC này** (cấm 1 ảnh cho nhiều TC) ⇒ ⛔ không khai PASS |
| TC-ASN-013 | ✅ PASS | — | run trước VR-007 | (seed, không chạy lại) |
| TC-ASN-014 | ⏳ NOT_RUN | 3 | — | cần seed 6 tin NEED cùng tuyến — hết phiên |
| TC-ASN-015 | ⏳ NOT_RUN | 3 | — | cần seed 3 tin NEED cùng tuyến — hết phiên |
| TC-ASN-016 | ⏳ NOT_RUN | 3 | — | cần seed 5 tin NEED cùng tuyến — hết phiên |
| TC-ASN-017 | ⏳ NOT_RUN | 3 | — | cần seed 6 tin NEED cùng tuyến — hết phiên |
| TC-ASN-018 | ⏳ NOT_RUN | 3 | — | cần seed 3 tin NEED ở 3 mốc thời gian + 1 tin lệch tuyến — hết phiên |
| TC-ASN-019 | ⏳ NOT_RUN | 4 | — | cần dev/QA lùi ngày để có tin **Hết hạn** — ⛔ không tạo được qua UI; phiên dừng trước lô 4 |
| TC-ASN-020 | ⏳ NOT_RUN | 1 | run này (chặng B xong) | **Chặng B ĐÃ PASS** (nhận → huỷ + lý do → tin trở lại Bảng tin, verify cả phía B lẫn phía chủ tin). Còn step 6–9: cần **Carrier thứ 3** (≠ taipm, ≠ anhdc4) ghép lại tin. Ảnh: `TC-ASN-020__verify-tin-tro-lai-bang-tin.png`, `TC-ASN-020__verify-chu-tin-thay-cho-ghep.png` |
| TC-ASN-021 | ✅ PASS | — | run trước VR-007 | (seed, không chạy lại) |
| TC-ASN-022 | ⏳ NOT_RUN | 2 | — | **dừng phiên theo yêu cầu QC 12:33.** Seed S4 (lệch buổi) ĐÃ đăng xong; chuông 12:31 không có mốc trùng giờ đăng seed ⇒ dấu hiệu thuận, nhưng **thiếu ảnh evidence riêng cho TC này** (cấm 1 ảnh cho nhiều TC) ⇒ ⛔ không khai PASS |
| TC-ASN-023 | ✅ PASS | — | run trước VR-007 | (seed, không chạy lại) |
| TC-ASN-024 | ⛔ N-A | — | run trước VR-007 | cần concurrency/load tool bắn 50 request thẳng API — ngoài phạm vi vibe-test UI thuần |
| TC-ASN-025 | ⏳ NOT_RUN | 3 | — | cần 2 tuyến OFFER độc lập + seed — hết phiên |
| TC-ASN-026 | ⛔ N-A | — | run trước VR-007 | cần API client + kiểm audit log server — ngoài phạm vi vibe-test UI thuần |
