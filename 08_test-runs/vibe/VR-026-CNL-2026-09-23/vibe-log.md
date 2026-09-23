# Vibe Test Log — VR-026 — v1.1 — 2026-09-23

> Module: CNL (Huỷ đơn / Huỷ nhận đơn) · Platform: mobile (Appium MCP + adb, UiAutomator2) · Env: STG · app `com.hrisproject.stag` (FoxPro) · Evidence dir: `screenshots/`
> Phiên: 2026-09-23 (khởi tạo, 15:29–15:44)
> Mode: **RETEST** bug Jira CNL đang **In review** (tra Jira 15:28): FE-319 (BUG-034, `TC-CNL-009`) · FE-320 (BUG-036, `TC-CNL-004`).
> Thiết bị: emulator-5554 (Android, 1080×2400) · Người gửi `stag_giangdc2@` (Đặng Châu Giang) · carrier setup `stag_anhptm17@` (Phan Thị Mỹ Anh — đã chấp nhận điều khoản).
> ⛔ Theo yêu cầu QC: chỉ comment + đính kèm ảnh lên Jira, **KHÔNG đổi trạng thái bug**; không cập nhật TC-MASTER / §8 / coverage trong run này.

## Dữ liệu thay đổi trên STG
- 1 trong 4 tin NEED do VR-024 tạo (đăng 14:37, `363 Nguyễn Hữu Thọ, Cẩm Lệ → FPT Cầu Giấy`, người nhận `stag_anhdc4@`): `stag_anhptm17@` ghép lúc 15:38 → `stag_giangdc2@` **huỷ** lúc 15:43 (lý do "Huy vi trung lich") ⇒ nay `Đã huỷ`.
- 1 tin khác trong 4 tin đó đã được người khác nhận **trước phiên này** — đang `Đang giao` (không do run này). 2 tin còn `Chờ ghép`.
- FE-320 chỉ mở popup rồi bấm "Huỷ" (đóng popup) ⇒ đơn đó vẫn `Chờ ghép`.

## TC-CNL-004: Check lý do huỷ 4 ký tự bị chặn kèm thông báo lỗi (FE-320)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở đơn `Chờ ghép` của giangdc2 → nhấn "Huỷ đơn" | tap | ✅ PASS | — | popup "Huỷ đơn hàng", "Xác nhận" mờ khi ô trống |
| 2 | Nhập `abcd` (4 ký tự) — quan sát ngay khi đang gõ | adb input text | ✅ PASS | `TC-CNL-004__pre-nhap-4-ky-tu-dang-focus.png` | viền ô đỏ + lỗi xuất hiện ngay (không cần rời ô) |
| 3 | Check nút "Xác nhận" + vùng dưới ô lý do | get_text `textContains("tối thiểu 5")` | ✅ PASS | `TC-CNL-004__verify-loi-ly-do-4-ky-tu-nut-xac-nhan-khoa.png` | lỗi **"Lý do huỷ cần tối thiểu 5 ký tự"** ngay dưới ô · "Xác nhận" vẫn mờ (khoá) |
| 4 | Bấm "Huỷ" đóng popup, check trạng thái đơn | tap | ✅ PASS | `TC-CNL-004__verify-trang-thai-van-cho-ghep.png` | đơn vẫn `Chờ ghép` |

**Result: ✅ PASS — bug FE-320 ĐÃ fix**
⚠️ Thanh công cụ nổi của bàn phím che mép trái popup ở ảnh step 2 — đã kéo sang phải trước khi chụp ảnh verify (step 3), chữ lỗi đọc đủ.

## TC-CNL-009: Check người gửi huỷ đơn đã ghép ghi đúng log (FE-319)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 0 | Setup: `stag_anhptm17@` mở tin của giangdc2 trên Bảng tin → "Tôi mang giúp được" → "Xác nhận" | đổi tài khoản | ✅ PASS | `_setup__anhptm17-ghep-don-cua-giangdc2.png` | đơn sang bước "Lấy hàng" (đã ghép) |
| 1 | Đăng nhập giangdc2, mở đơn `Đã ghép`, xem LỊCH SỬ | scroll_to_element `LỊCH SỬ` | ✅ PASS | `TC-CNL-009__pre-lich-su-2-dong-truoc-khi-huy.png` | 2 dòng: "Ghép thành công 15:38 · Phan Thị Mỹ Anh" · "Đăng tin lên bảng tin 14:37 · Đặng Châu Giang" |
| 2 | "Huỷ đơn" → lý do "Huy vi trung lich" → "Xác nhận" | adb input text | ✅ PASS | — | popup "Đã huỷ — Đã huỷ đơn hàng." → "Đồng ý"; app về "Đơn của tôi", thẻ đơn `Đã huỷ` |
| 3 | Mở lại đơn, check LỊCH SỬ | scroll | ✅ PASS | `TC-CNL-009__verify-log-da-huy-don-dung-nhan.png` | thêm đúng **1** dòng: **"Đã huỷ đơn"** · Hôm nay · 15:43 · Đặng Châu Giang · *Lý do: Huy vi trung lich* |

**Result: ✅ PASS — bug FE-319 ĐÃ fix** (nhãn nay là "Đã huỷ đơn", không còn "Đã huỷ nhận đơn")
Ghi chú: dòng log ghi **tên người** (Đặng Châu Giang) thay vì chữ "Người gửi" — đúng theo quyết định QC 2026-09-22 (xoá `BUG-035`, xem `bug-index.md`).

## Setup / môi trường
- Tìm đơn `Đã ghép` vai người gửi trong "Đơn của tôi" của giangdc2: không có (thẻ `Đã ghép` duy nhất là vai **Nhận**) ⇒ tự dựng bằng anhptm17 như bước 0.
- Đổi tài khoản 2 lần: giangdc2 → anhptm17 → giangdc2.
