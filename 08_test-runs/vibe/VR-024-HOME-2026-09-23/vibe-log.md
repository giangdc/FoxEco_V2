# Vibe Test Log — VR-024 — v1.1 — 2026-09-23

> Module: HOME (Trang chủ) · Platform: mobile (Appium MCP + adb, UiAutomator2) · Env: STG · app `com.hrisproject.stag` (FoxPro) · Evidence dir: `screenshots/`
> Mode: **RETEST** 2 bug HOME đang **In review** sau `/sync-jira-bugs` 2026-09-23 — `TC-HOME-025` (FE-309 / BUG-025) · `TC-HOME-027` (FE-310 / BUG-026).
> Phiên: 2026-09-23 (khởi tạo, 14:25–14:49)
> Thiết bị: emulator-5554 (Android, 1080×2400).
> Tài khoản: người xem **`stag_MinhNDN2@`** (Nguyễn Đình Nhật Minh — tài khoản trắng, 0 đơn, 0 tin, 0 đóng góp; chỉ đọc) · người đăng tin setup **`stag_giangdc2@`**.
> ⛔ Theo yêu cầu QC: chỉ comment + đính kèm ảnh lên Jira, **KHÔNG đổi trạng thái bug**; không cập nhật TC-MASTER / §8 / coverage trong run này.

## Dữ liệu tạo trên STG (setup TC-HOME-025)

`stag_giangdc2@` đăng **4 tin NEED** 14:35–14:41 — `Tài liệu · Thấp · Dưới 5 kg · Nhỏ`, 1 ảnh, người nhận `stag_anhdc4@`,
lấy `363 Nguyễn Hữu Thọ, Cẩm Lệ` → giao `FPT Cầu Giấy`, `Hôm nay · Sau giờ làm`. **Để lại trên STG** (chưa huỷ).
⚠️ STG dùng chung đang có người khác đăng/huỷ tin liên tục (tin "0–1 phút trước" xuất hiện rồi mất trong vài phút) ⇒ số tin được **đếm lại trên Bảng tin ngay trước mỗi lần quan sát Trang chủ**.
14:42 có người khác đăng thêm 1 tin (tổng 6) ⇒ quan sát nhánh > 5 (`TC-HOME-021`) trước; sau đó **QC tự huỷ 1 tin** (tổng về 5) rồi quan sát nhánh = 5.

## TC-HOME-027: Check section Đơn của tôi vẫn hiện kèm empty state khi chưa có đơn đang chạy (FE-310)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco bằng tài khoản sạch | logout giangdc2 → login `stag_MinhNDN2@` + OTP → Chức năng → FoxEco | ✅ PASS | — | hero `0 · Chưa có đóng góp nào` |
| 2 | Mở Trang chủ | — | ✅ PASS | — | — |
| 3 | Check section "Đơn của tôi" | screencap | ✅ PASS | `TC-HOME-027__verify-don-cua-toi-empty-state.png` | section hiện · icon hộp nét mảnh · "Bạn chưa có đơn nào đang chạy" · nút "Tạo đơn gửi hàng" (`home-orders-empty-cta`) |
| 3b | (mở rộng) nhấn CTA | tap `Tạo đơn gửi hàng` | ✅ PASS | `TC-HOME-027__verify-cta-mo-form-gui-hang.png` | mở wizard "Tôi cần gửi hàng" Bước 1/3; thoát ra không lưu gì |

**Result: ✅ PASS — bug FE-310 ĐÃ fix**
**Before (run cũ):** `VR-014-HOME-2026-09-21` — chỉ có dòng "Chưa có đơn nào", không CTA, không icon.

## TC-HOME-021 (hồi quy, chiều > 5): nút Xem thêm hiện khi có hơn 5 tin

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đếm tin hợp lệ trên Bảng tin (viewer Minh) | page source `feed-post-card-0..5`, scroll tới cuối không có card-6 | ✅ PASS | `TC-HOME-021__pre-bang-tin-6-tin.png` | **6 tin** (4 giangdc2 + 1 tin 5 giờ trước + 1 tin người khác 14:42) |
| 2 | Mở Trang chủ, check section "Tin mới" | screencap đầu + cuối section | ✅ PASS | `TC-HOME-021__verify-6-tin-cuoi-section.png` (+ `__verify-6-tin-link-o-header.png`, `__verify-6-tin-co-link-xem-them.png`) | 5 tin + nút `Xem thêm trên Bảng tin ›` cuối section; header section cũng có link "Xem thêm trên Bảng tin" |

**Result: ✅ PASS**

## TC-HOME-025: Check nút Xem thêm trên Bảng tin không hiện khi chỉ có đúng năm tin hợp lệ (FE-309)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Hệ thống có đúng 5 tin NEED hợp lệ | QC huỷ 1 tin ⇒ viewer Minh: Bảng tin pull-to-refresh, `feed-post-card-0..4`, scroll tới cuối không có card-5 | ✅ PASS | `TC-HOME-025__pre-bang-tin-5-tin-dau-danh-sach.png` · `TC-HOME-025__pre-bang-tin-5-tin-cuoi-danh-sach.png` | 4 tin giangdc2 + 1 tin "5 giờ trước" |
| 2 | Đăng nhập tài khoản xem, mở Trang chủ | tab Trang chủ | ✅ PASS | `TC-HOME-025__verify-header-tin-moi-khong-co-link.png` | header "Tin mới" **không** còn link "Xem thêm" (khác lúc 6 tin) |
| 3 | Đếm số tin trong "Tin mới", cuộn cuối section | swipe ×3, page source | ✅ PASS | — | 5 card (5/7/9/10 phút + 5 giờ trước) |
| 4 | Check khu vực cuối section | screencap | ✅ PASS | `TC-HOME-025__verify-5-tin-khong-co-nut-xem-them.png` | **không có** nút "Xem thêm trên Bảng tin" |

**Result: ✅ PASS — bug FE-309 ĐÃ fix** (ngưỡng nay là `> 5`: 5 tin → không nút, 6 tin → có nút)
**Before (run cũ):** `VR-014-HOME-2026-09-21` — 5 tin vẫn hiện nút.
⚠️ Ghi chú TC: Pre-condition `TC-HOME-025` yêu cầu *"dọn dữ liệu toàn hệ thống"* — lần này đạt được đúng 5 tin trên STG dùng chung nhờ đếm Bảng tin ngay trước khi quan sát, không dọn toàn hệ thống.

## Setup / môi trường
- Ảnh `TC-HOME-025__verify-header-tin-moi-khong-co-link.png` đã được upload lên FE-309 **trước** khi đổi tên cho đúng quy ước evidence ⇒ trên Jira nó mang tên cũ `TC-HOME-025__step4-home-minh-header-tin-moi-5-tin.png` (cùng nội dung).
- Emulator lúc bắt đầu còn popup "Thoát và bỏ nội dung đã nhập?" do VR-023 (kết thúc 12:09) để lại ⇒ bấm "Thoát".
- Bảng tin hiển thị cả tin của chính người xem (badge "Tin của bạn").
- Hero "Cộng đồng FoxEco" đổi 350 → 354 → 353 đơn trong phiên — khớp việc tạo/huỷ tin.
