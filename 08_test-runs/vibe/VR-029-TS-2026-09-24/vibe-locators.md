# Vibe Locators — v1.1 — VR-029 — 2026-09-24

> Captured via Appium MCP. Legend: ✅ Verified · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending. Chỉ liệt locator MỚI / re-verify của run này; phần còn lại xem `VR-019-TS-2026-09-22/vibe-locators.md` + `locators/vibe-locators-latest.md`.

## Screen: Theo dõi đơn

| Element | Action Used | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| Nút "Báo cáo sự cố" | tap | -android uiautomator | `new UiSelector().resourceId("track-report-incident")` | ✅ (re-verify) | TC-TS-009/012/013/016/021 |

## Screen: Báo sự cố đơn hàng (native header)

| Element | Action Used | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| Nút "←" đóng WebView | tap | accessibility id | `Quay lại` | ✅ (re-verify) | TC-TS-009/012/013/016 |

## 🆕 Screen: Báo sự cố đơn hàng — màn lỗi mất mạng (APP vẽ, native)

| Element | Action Used | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| Nút "Thử lại" | find + tap | -android uiautomator | `new UiSelector().text("Thử lại")` | ✅ | TC-TS-016 (recon TC-TS-017) |
| Tiêu đề lỗi | verify (ảnh) | — | "Không tải được trang" / "Vui lòng kiểm tra kết nối mạng và thử lại." | ⚠️ Inferred (chỉ đọc từ ảnh) | TC-TS-016 |

> 🔁 Đính chính VR-019: locator `textContains("Thử lại")` từng 🚫 NOT FOUND — nay **tìm thấy** (hành vi app đã đổi).

## Kỹ thuật dùng trong run (không phải locator)

| Việc | Cách |
|---|---|
| Nhập tiếng Việt có dấu vào form | `appium_mobile_clipboard(set)` + `adb shell input keyevent 279` (PASTE) — `set_value` W3C lỗi `KeyCharacterMap` |
| Mất mạng hoàn toàn | `adb shell svc wifi disable` + `svc data disable` (emulator có cả data 3G) |
