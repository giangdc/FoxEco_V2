# Vibe Test Log — VR-023 — v1.1 — 2026-09-23

> Module: ORD (Đăng tin & Quản lý tin) · Platform: mobile (Appium MCP, UiAutomator2) · Env: STG · app `com.hrisproject.stag` (FoxPro 3.0.8) · Evidence dir: `screenshots/`
> Phiên: 2026-09-23 (khởi tạo)
> Mode: **RETEST** 3 TC có bug Jira đang **In review** — `TC-ORD-053` (FE-302 / BUG-010) · `TC-ORD-059` (FE-303 / BUG-011) · `TC-ORD-058` (FE-304 / BUG-012).
> Thiết bị: emulator-5554 (Android, 1080×2400) · Tài khoản A `stag_giangdc2@` — Đặng Châu Giang (vai người gửi, cùng môi trường lúc log bug).
> ⛔ Theo yêu cầu QC: chỉ comment kết quả lên Jira, **KHÔNG đổi trạng thái bug**; không cập nhật TC-MASTER / §8 / coverage trong run này.
> Ảnh ban đầu đặt tên theo mã Jira (`FE-30x__…`) rồi đổi sang quy ước `TC-<ID>__…` theo gate evidence cùng phiên; nội dung ảnh không đổi.

## TC-ORD-053: Check chọn ở lại ở popup thoát wizard giữ nguyên dữ liệu đã nhập

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | "+ Đăng tin" → "Tôi cần gửi hàng" → bước 1 chọn Thấp · Dưới 5 kg · Nhỏ · 1 ảnh → "Tiếp theo" | tap toạ độ chip + `resourceId("multi-photo-add-button")` → Photo Picker → Add (1) | ✅ PASS | — | — |
| 2 | Bước 2 nhập "Số 9 Duy Tân" vào "Địa chỉ giao hàng" | set_value `//android.widget.EditText[@hint="Địa chỉ giao hàng"]` | ✅ PASS | — | — |
| 3 | Nhấn quay lại ở bước 2 | phím BACK | ✅ PASS | `TC-ORD-053__pre-back-tu-buoc-2-ve-buoc-1.png` | về bước 1, không đóng wizard |
| 4 | Nhấn quay lại ở bước 1, quan sát popup thoát | tap nút ← header (89,218) | ❌ FAIL | `TC-ORD-053__step4-FAIL-khong-co-popup-thoat.png` | về thẳng "Đăng tin mới", không popup |
| 4b | Lặp lại, chụp liên tiếp ~0,5 s/ảnh quanh lúc nhấn nút header | adb screencap ×7 | ❌ FAIL | `TC-ORD-053__step4-FAIL-burst-nut-quay-lai-header.png` (+ `TC-ORD-053__step4-FAIL-screenrecord.mp4`) | không khung nào có popup |
| 4c | Lặp lại với phím BACK hệ thống ở bước 1 | keyevent 4 + screencap ×5 | ❌ FAIL | `TC-ORD-053__step4-FAIL-burst-phim-back-he-thong.png` | cùng hành vi |
| 5 | Mở lại "Tôi cần gửi hàng", kiểm tra dữ liệu | tap card | ❌ FAIL | `TC-ORD-053__step5-FAIL-mo-lai-mat-du-lieu.png` | toàn bộ dữ liệu trống |

**Result: ❌ FAIL (step 4) — bug FE-302 CHƯA fix**
**Evidence:** `screenshots/TC-ORD-053__step4-FAIL-khong-co-popup-thoat.png` (+ `__step4-FAIL-burst-nut-quay-lai-header.png`, `__step4-FAIL-burst-phim-back-he-thong.png`, `__step5-FAIL-mo-lai-mat-du-lieu.png`, `__pre-back-tu-buoc-2-ve-buoc-1.png`) — verified tồn tại
**Before (run cũ):** ảnh FAIL của VR-002-ORD-2026-09-18 (xem `vibe-report.md`)

## TC-ORD-059: Check buổi đã trôi qua trong ngày hôm nay bị chặn chọn

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Chạy sau 12:00 (12:04:52) để buổi Sáng đã qua; nhập đủ bước 1 → "Tiếp theo" | như TC-ORD-053 step 1 | ✅ PASS | — | — |
| 2 | Bước 2: Từ ngày = Đến ngày = Hôm nay (mặc định) | quan sát | ✅ PASS | `TC-ORD-059__pre-hom-nay-truoc-khi-chon.png` | chip Sáng đã xám trước khi nhấn |
| 3 | Nhấn chip "Sáng (8–12h)" và quan sát trạng thái | tap (298,1788) · `descriptionStartsWith("Sáng")` → `enabled=false` | ✅ PASS | `TC-ORD-059__verify-buoi-sang-da-qua-bi-chan.png` | không đổi trạng thái sau khi nhấn |

**Result: ✅ PASS (3 steps, 1 expected) — bug FE-303 ĐÃ fix**
**Evidence:** `screenshots/TC-ORD-059__verify-buoi-sang-da-qua-bi-chan.png` (+ `__pre-hom-nay-truoc-khi-chon.png`) — verified tồn tại
**Before (run cũ):** ảnh FAIL của VR-002-ORD-2026-09-18 (xem `vibe-report.md`)
Ghi nhận thêm: form OFFER cũng xám chip Sáng cùng thời điểm (quan sát ở section TC-ORD-058, step 3).

## TC-ORD-058: Check buổi mong muốn mặc định là Sau giờ làm khi vừa mở bước hai

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Nhập đủ bước 1 → "Tiếp theo" | như TC-ORD-053 step 1 | ✅ PASS | — | — |
| 2 | Bước 2, cuộn tới "Buổi mong muốn" — chưa chạm field nào — quan sát | swipe mép phải (1040,1700→900) | ✅ PASS | `TC-ORD-058__verify-buoi-mac-dinh-need.png` | "Sau giờ làm (17–19h)" chọn sẵn; `textContains("Chọn ít nhất 1 buổi")` NOT FOUND |
| 3 | (mở rộng theo ghi chú bug) form "Tôi nhận giao hàng" — quan sát nhóm buổi | tap card OFFER + swipe | ✅ PASS | `TC-ORD-058__verify-buoi-mac-dinh-offer.png` | OFFER cũng chọn sẵn "Sau giờ làm (17–19h)" |

**Result: ✅ PASS (2 steps, 1 expected) — bug FE-304 ĐÃ fix**
**Evidence:** `screenshots/TC-ORD-058__verify-buoi-mac-dinh-need.png` (+ `__verify-buoi-mac-dinh-offer.png`) — verified tồn tại
**Before (run cũ):** ảnh FAIL của VR-002-ORD-2026-09-18 (xem `vibe-report.md`)
⚠ Thuộc tính `selected` của chip trả `false` (React Native không phản ánh) ⇒ kết luận theo ảnh.
Ghi nhận nhỏ: nhãn chip nay có "h" — `Sáng (8–12h)` · `Chiều (13–17h)` · `Sau giờ làm (17–19h)` (PRD §8.1.4 không có "h").

## Setup / môi trường
- `_setup__start.png`: màn đăng nhập FoxPro lúc bắt đầu phiên (ô email trống).
- Biến OTP trong `~/.foxeco-v2/credentials.env` là `FOXECO_STG_PASS` (không phải `FOXECO_STG_OTP` như CLAUDE.md).
- Bẫy: lần đầu nhấn "NHẬN MÃ OTP" không chuyển màn ⇒ mã gõ bằng adb dính vào ô email. Luôn chờ thấy `Xác nhận OTP` rồi mới gõ.
