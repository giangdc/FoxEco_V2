# Vibe Locators — v1.1 — VR-015 — 2026-09-21

> Captured via **Appium MCP** (UiAutomator2) + `adb` during this run.
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> Platform: **mobile** · Devices: emulator-5554 (1080×2400) + real R58T20PLP8K (720×1600)

## Màn: Chi tiết tin (nút nhận đơn)

| Element | Action Used | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| Nút nhận đơn | find (phủ định) | -android uiautomator | `new UiSelector().textContains("mang giúp")` | ✅ *(🚫 NOT FOUND với `anhdc4` — nút không hiện; ✅ với `taipm`/`anhptm17`/`Thủy`)* | TC-ASN-006 |
| Modal xác nhận — `Xác nhận` | tap | toạ độ (adb) | real `(509,928)` · emu `(767,1442)` | ⚠️ chưa harvest locator text (dùng toạ độ để chạm song song) | TC-ASN-006 |

## Màn: Đăng xuất / đăng nhập FoxPro

| Element | Action Used | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| `Đăng xuất` | scroll_to_element + tap | -android uiautomator | `new UiSelector().text("Đăng xuất")` | ✅ | (setup) |
| Popup xác nhận | tap | -android uiautomator | `new UiSelector().text("Đồng ý")` | ✅ | (setup) |
| Ô email | tap | -android uiautomator | `new UiSelector().text("Nhập email đăng nhập")` | ✅ | (setup) |
| `NHẬN MÃ OTP` | tap | -android uiautomator | `new UiSelector().text("NHẬN MÃ OTP")` | ✅ | (setup) |
| `ĐĂNG NHẬP` | tap | -android uiautomator | `new UiSelector().text("ĐĂNG NHẬP")` | ✅ | (setup) |
| Icon FoxEco ở `Chức năng` | scroll_to_element + tap | -android uiautomator | `new UiSelector().textContains("FoxEco")` | ✅ *(selector `text("FoxEco")` **trượt** trên real device — dùng `textContains`)* | (setup) |
