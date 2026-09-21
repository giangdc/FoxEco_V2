# MCP Session Log — VR-015 — 2026-09-21

## Session info
- Platform: mobile (Appium MCP, UiAutomator2) — **2 session cùng lúc**
- Device 1: `emulator-5554` (1080×2400) — session `88812560-3e52-45cd-80db-50418fa6b87a` · `systemPort=8201`
- Device 2: real `R58T20PLP8K` Samsung A12s (720×1600, Android 13) — session `b0b58511-f95f-4cf2-a85b-afbd969c9447` · `systemPort=8202`
- Capabilities chung: `noReset=true` · `appPackage=com.hrisproject.stag` · `appActivity=com.hrisproject.MainActivity` · `autoLaunch=false`
- Đổi thiết bị: `appium_session_management action=select sessionId=…`
- ⚠️ **Lệch template:** phần lớn thao tác chạm/chụp dùng `adb -s <udid> shell input tap|swipe` + `exec-out screencap -p` (lý do: 2 máy khác độ phân giải, cần **chạm song song trong 1 lệnh** cho `TC-ASN-006`; `appium_screenshot` trả HTML viewer rất lớn). Appium dùng để: tạo session, `find_element`/`scroll_to_element`/`tap` ở luồng **đăng xuất/đăng nhập FoxPro**.

## Ghi chú kỹ thuật cần nhớ

| # | Điều | Ghi chú |
|---|---|---|
| 1 | Chạm đồng thời 2 máy | `( adb -s A shell input tap x y & adb -s B shell input tap x y & wait )`; đo `date +%s%N` quanh mỗi lệnh ⇒ độ lệch ≤ ~95 ms |
| 2 | Toast biến mất sau ~2–3s | Sau khi chạm phải **chụp liên tục** (`screencap` ~0.25–0.3s/khung) — ảnh chụp sau 6s **không thấy** toast lần 1 |
| 3 | Toạ độ nút | Real: `CTA (360,1440)` · `Xác nhận (509,928)` · tab dưới `y≈1450`. Emulator: `CTA (540,2238)` · `Xác nhận (767,1442)` · tab dưới `y≈2262`. ⚠️ Màn `Theo dõi đơn` **không có thanh tab** — chạm `y≈2262` trúng nút `Huỷ nhận đơn` |
| 4 | Mã đăng nhập | ⚠️ `credentials.env` không có `FOXECO_STG_OTP`; đã dùng `FOXECO_STG_PASS` ở màn OTP |
| 5 | Sau khi gõ OTP **không** bấm `BACK` trên emulator | `BACK` lúc đó đưa về màn nhập email (mất 1 vòng) |

| 6 | Đổi tài khoản để đọc góc nhìn chủ tin | Emulator: logout `stag_anhptm17@` → login `stag_giangdc2@`. ⚠️ Lần gõ mã đầu bị **mất** (màn OTP chưa nhận focus sau 4s) → popup *"Mã OTP không đúng định dạng"*; cách xử: `Đồng ý` → chạm ô OTP → gõ lại → `ĐĂNG NHẬP` |
