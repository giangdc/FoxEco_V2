# Scope Ledger — VR-005 — module HOME — SCOPE_TOTAL = 30 TC

> Seed từ: `coverage-HOME.md` — **file chưa tồn tại trước phiên** ⇒ trạng thái trước phiên: có verdict **0/30**.
> Tập chạy phiên này: **toàn bộ pending (30 TC)** — không có TC nào đã PASS ⇒ ⛔ không phát sinh câu hỏi Step 1.2.
> Lô: 1 lô (mặc định 20 TC/lô; phiên dừng khi **hết TC chạy được**, ⛔ không phải hết sức phiên).

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-HOME-001 | ✅ PASS | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-001__verify-bottom-nav-5-tabs.png` |
| TC-HOME-002 | 🚫 BLOCKED | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-002__step2-BLOCKED-bang-tin-0-tin.png` |
| TC-HOME-003 | ✅ PASS | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-003__verify-greeting-name.png` |
| TC-HOME-004 | ⏳ NOT_RUN | — | — | **Lý do:** cần **3 tài khoản** giữ 3 vai trên cùng 1 đơn + đăng xuất/đăng nhập ×3 (**OTP nhập tay**). 🔍 Quan sát rời: header của tài khoản A **KHÔNG có node icon vai trò nào** (tree chỉ có `Quay lại` · lời chào · `Thông báo`) ⇒ nghi vấn bề mặt chưa build, cần BA xác nhận trước khi chạy |
| TC-HOME-005 | ✅ PASS | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-005__verify-chuong-cham-do.png` |
| TC-HOME-006 | ✅ PASS | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-006__verify-chuong-khong-cham-do.png` |
| TC-HOME-007 | ❌ FAIL | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-007__step2-FAIL-tagline-sai-chuoi.png` |
| TC-HOME-008 | ⏳ NOT_RUN | — | — | **Lý do:** cần chạy trọn vòng giao–nhận với **3 tài khoản** (A/B/C) + đăng được tin NEED — đang bị chặn bởi bug `B1` của `VR-004` (`400 REQ_400`). 🔍 2/3 vế của Expected đã đo được sẵn: card **không** có chỉ số CO₂/điểm ECO, dòng cộng đồng đúng dạng `[số] đơn · [số] người` (`317 đơn · 23743 người`); chỉ thiếu vế **hero +1** |
| TC-HOME-009 | ✅ PASS | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-009__verify-6-thanh-phan-don-cua-toi.png` |
| TC-HOME-011 | ✅ PASS | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-011__verify-nhan-vai-gui.png` |
| TC-HOME-012 | ✅ PASS | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-012__verify-nhan-vai-giao.png` |
| TC-HOME-013 | ✅ PASS | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-013__verify-nhan-vai-nhan.png` |
| TC-HOME-014 | ⏳ NOT_RUN | — | — | **Lý do:** cần đẩy **1 đơn** qua 4 trạng thái liên tiếp với tài khoản Carrier + Receiver (OTP nhập tay) và đăng được tin NEED (bug `B1`). 🔍 Quan sát rời khớp 2/4 mốc: `Đã ghép`→**2/5** đoạn tô · `Đã giao`→**4/5** đoạn tô |
| TC-HOME-015 | ✅ PASS | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-015__verify-lo-trinh-khop.png` |
| TC-HOME-016 | ✅ PASS | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-016__verify-mo-man-hoat-dong.png` |
| TC-HOME-017 | ⏳ NOT_RUN | — | — | **Lý do:** cần ≥1 tin NEED hợp lệ do **tài khoản khác** đăng; STG hiện **0 tin** (xác nhận 2 bề mặt, `_recon__bang-tin-empty-0-tin.png`). Tin của chính mình bị loại khỏi "Tin mới" ⇒ ⛔ không tự seed bằng tài khoản A được; cần **tài khoản B + OTP nhập tay** |
| TC-HOME-018 | ⏳ NOT_RUN | — | — | **Lý do:** cần ≥1 tin NEED hợp lệ do **tài khoản khác** đăng; STG hiện **0 tin** (xác nhận 2 bề mặt, `_recon__bang-tin-empty-0-tin.png`). Tin của chính mình bị loại khỏi "Tin mới" ⇒ ⛔ không tự seed bằng tài khoản A được; cần **tài khoản B + OTP nhập tay** |
| TC-HOME-019 | ⏳ NOT_RUN | — | — | **Lý do:** cần **≥6 tin** NEED hợp lệ do tài khoản khác đăng; STG hiện **0 tin**. Cần tài khoản B + OTP nhập tay |
| TC-HOME-020 | ⏳ NOT_RUN | — | — | **Lý do:** cần ≥1 tin NEED hợp lệ do **tài khoản khác** đăng; STG hiện **0 tin** (xác nhận 2 bề mặt, `_recon__bang-tin-empty-0-tin.png`). Tin của chính mình bị loại khỏi "Tin mới" ⇒ ⛔ không tự seed bằng tài khoản A được; cần **tài khoản B + OTP nhập tay** |
| TC-HOME-021 | ⏳ NOT_RUN | — | — | **Lý do:** cần **>5 tin** NEED hợp lệ do tài khoản khác đăng; STG hiện **0 tin**. Cần tài khoản B + OTP nhập tay |
| TC-HOME-022 | ✅ PASS | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-022__verify-chuyen-tab-bang-tin.png` |
| TC-HOME-023 | ⏳ NOT_RUN | — | — | **Lý do:** cần ≥1 tin NEED hợp lệ do **tài khoản khác** đăng; STG hiện **0 tin** (xác nhận 2 bề mặt, `_recon__bang-tin-empty-0-tin.png`). Tin của chính mình bị loại khỏi "Tin mới" ⇒ ⛔ không tự seed bằng tài khoản A được; cần **tài khoản B + OTP nhập tay** |
| TC-HOME-025 | ⏳ NOT_RUN | — | — | **Lý do:** cần khống chế **đúng 5 tin** hợp lệ TOÀN hệ thống ⇒ phải có môi trường riêng / khung giờ dọn dữ liệu (`fragment §0.3`). Hiện 0 tin, không tự dựng được 5 tin (cần tài khoản B + OTP) |
| TC-HOME-026 | ✅ PASS | 1 | run này | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-026__verify-empty-state-tin-moi.png` |
| TC-HOME-027 | ⏳ NOT_RUN | — | — | **Lý do:** cần tài khoản "sạch" `SEED-HOME-01` (0 tin · 0 đơn · 0 đóng góp). Tài khoản A có 6 đơn + 13 đóng góp ⇒ không dùng được; cần tài khoản mới + **OTP nhập tay** |
| TC-HOME-028 | ⏳ NOT_RUN | — | — | **Lý do:** cần tài khoản "sạch" **VÀ** *"hệ thống chưa có đơn Hoàn thành nào"* — STG đang có **317 đơn** cộng đồng ⇒ ⛔ không thoả được trên STG dùng chung, cần môi trường riêng |
| TC-HOME-029 | ⏳ NOT_RUN | — | — | **Lý do:** cần tài khoản "sạch" + trọn vòng giao–nhận với 2 tài khoản phụ (OTP nhập tay) + đăng được tin NEED (bug `B1`) |
| TC-HOME-030 | ⏳ NOT_RUN | — | — | **Lý do:** cần 6 tin của tài khoản B + 1 tin đã ghép + **dev/QA lùi "Đến ngày"** để tạo tin hết hạn (⛔ không tạo được qua UI). STG hiện 0 tin |
| TC-HOME-031 | ⏳ NOT_RUN | — | — | **Lý do:** cần **3 tài khoản** + trọn vòng giao–nhận để đo cộng đồng tăng đúng 1 (OTP nhập tay + bug `B1`). 🔍 Giá trị nền đã ghi: `317 đơn · 23743 người` lúc 05:51 |
| TC-HOME-032 | ⛔ N-A | — | — | **Lý do:** NFR hiệu năng — cần môi trường load-test mô phỏng **1.000 user đồng thời** trên 4G + công cụ đo p95; ⛔ **không dựng được bằng thiết bị tay / không phải bài test UI** (`fragment §0.3` chốt đánh `Deferred`). Thuộc phạm vi skill `k6-load-test`, không phải `vibe-test` |

## Ghi chú phiên

- **Chạy 14/30**, thu **12 PASS · 1 FAIL · 1 BLOCKED**; **15 ⏳ NOT_RUN** + **1 ⛔ N-A**.
- 🛑 **Dừng KHÔNG phải vì hết sức phiên** — đã chạy hết mọi TC mà dữ liệu STG hiện tại cho phép.
  16 TC còn lại chặn ở **tiền đề dữ liệu/môi trường**, ⛔ không gỡ được bằng cách chạy lâu hơn:
  8 TC cần tài khoản B đăng tin · 5 TC cần 3 tài khoản + trọn vòng giao–nhận · 2 TC cần môi trường riêng · 1 TC là NFR load-test (`N-A`).
- 🔑 **Chặn gốc là OTP nhập tay**: mọi hướng seed dữ liệu đều phải đăng nhập tài khoản phụ. Cùng blocker đã ghi ở `VR-001` và `VR-003`.
- Chi tiết verdict + lý do từng TC: `08_test-runs/vibe/coverage/coverage-HOME.md` (sổ cái tích lũy).
