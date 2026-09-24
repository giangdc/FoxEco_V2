# Vibe Report — VR-029 — module TS — 2026-09-24 (RETEST, chỉ v1.1)

## Scope Coverage

| Hạng mục | Số |
|---|--:|
| SCOPE_TOTAL module TS (v1.1) | 17 |
| Chạy trong run này | **5** (`TC-TS-009` · `012` · `013` · `016` · `021`) |
| Kết quả run này | **5 PASS** *(4P/1F lúc chạy; `016` → PASS sau khi QC chốt lại Expected)* |
| Evidence | 5/5 có `__verify` |
| Sổ cái TS sau merge | **17/17 có verdict · còn nợ 0** — 16 PASS · 1 N-A (`017` DESCOPED) |

## Before → After

| TC | Before (VR-019) | After (VR-029) | Ghi chú |
|---|---|---|---|
| TC-TS-009 | ❌ FAIL | ✅ PASS | Expected sửa theo BA `FE-323`: màn xác nhận mặc định Microsoft Forms |
| TC-TS-012 | ❌ FAIL | ✅ PASS | Expected sửa theo BA `FE-324`: SĐT "0912abc" gửi được, không validate |
| TC-TS-013 | ❌ FAIL | ✅ PASS | `FE-325` Fixed — ảnh không còn bắt buộc |
| TC-TS-016 | ❌ FAIL (trang lỗi Chromium) | ❌ FAIL (app vẽ màn lỗi + nút "Thử lại") | 🔴 Hành vi app đã đổi (nay đúng spec gốc) ⇒ **QC chốt lại Expected theo app hiện tại → ✅ PASS** (follow-up cùng ngày) |
| TC-TS-021 | ❌ FAIL | ✅ PASS | Expected sửa theo BA `FE-326`: ô mã đơn sửa được |

## Phát hiện cần QC quyết định

1. 🔴 **`TC-TS-016`** — khi mất mạng, app hiện màn lỗi native "Không tải được trang — Vui lòng kiểm tra kết nối mạng và thử lại." + nút **"Thử lại"**. Recon: có mạng lại rồi nhấn "Thử lại" ⇒ form tải lại **đúng mã đơn cũ**. ⇒ Đề xuất: đưa Expected `TC-TS-016` về bản gốc (app hiện lỗi + nút Thử lại), **bỏ DESCOPED `TC-TS-017`** và chạy lại; cập nhật `C-TS-04(a)`. `FE-322` (Won't Fix) có thể thực tế đã được Dev xử lý.
2. Form Microsoft Forms hiện **tiếng Anh** trên emulator (theo ngôn ngữ tài khoản Microsoft): "Submit", "Your response was submitted." — Expected ghi chuỗi tiếng Việt; không coi là lỗi.
3. Ô SĐT có placeholder mới "Please enter at most 10 characters" (giới hạn 10 ký tự) — chưa có trong phân tích.

📁 `vibe-log.md` · `scope-ledger.md` · `vibe-locators.md` · `mcp-session-log.md` · `screenshots/`
