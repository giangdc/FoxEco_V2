# MCP Session Log — VR-018 — 2026-09-21

## Session info
- Platform: mobile (Appium MCP, UiAutomator2) · Device `emulator-5554`
- Session ID: `7d44341c-8a3e-45c5-ac5e-7d4e134d157e` (tái dùng từ VR-017, `session_management list` xác nhận còn sống lúc bắt đầu)
- Capabilities: `noReset=true` · `appPackage=com.hrisproject.stag` · `appActivity=com.hrisproject.MainActivity` · `autoLaunch=false`
- ⚠️ Lệch template (giống VR-015/017): ảnh evidence chụp bằng `adb exec-out screencap -p` thẳng vào `screenshots/`. Chọn ảnh trong Android Photo Picker bằng `adb input tap` (OS picker, không phải app). Fling về đầu màn bằng `adb input swipe`. ⛔ Không ghi locator nào từ các thao tác adb.

## Pre-flight + Pha A

| # | MCP method | Args (summary) | Result | Note |
|--:|-----------|----------------|--------|------|
| 1 | appium_session_management | list | OK — 1 session active | Pre-flight |
| A1 | find+tap / set_value | wizard Đăng tin NEED 3 bước (O1, O2) | OK | locator lấy từ `vibe-locators-latest.md`, action chạy được ⇒ ✅ |
| A2 | appium_get_page_source | popup `Huỷ đơn hàng` | OK 268k → file | **Pha A** — `cancel-order-*` |
| A3 | appium_get_page_source | Theo dõi đơn A · Chờ ghép (3 khung) | OK | **Pha A** |
| A4 | appium_get_page_source | Cá nhân FoxEco | OK | **Pha A** |
| A5 | find+tap / set_value | luồng đổi tài khoản FoxPro ×3 (`anhdc4`→`anhptm17`→`anhdc4`→`giangdc2`) | OK | — |

## Pha B — 1 dòng / TC

| TC | Calls (xấp xỉ) | Chi tiết gộp | Snapshot? | Kết quả |
|----|------:|--------------|-----------|---------|
| TC-CNL-004 | 6 | find×3, tap×2, set_value×1, get_attribute×1, page_source×1 | 1 (A2) | ❌ FAIL |
| TC-CNL-012 | 6 | find×3, tap×2, set_value×1, get_attribute×2 | 0 | ✅ PASS |
| TC-CNL-022 | 8 | scroll×3, page_source×4, back, find+tap `Cá nhân` | 4 (A3+A4) | ✅ PASS |
| TC-CNL-010 | 14 | find+tap card/CTA/Xác nhận, scroll_to LỊCH SỬ, page_source×3, set_value, tap confirm, scroll_to (NOT FOUND ở Chi tiết tin) | 3 | ❌ FAIL |
| TC-CNL-021 | 2 | find+tap `track-carrier-pickup` | 0 | 🚫 BLOCKED |
| TC-CNL-018 | 6 | find+tap `Xác nhận`(instance 1) · `Bắt đầu giao` · `Đồng ý`, page_source×2 | 2 | ❌ FAIL |
| TC-CNL-015 | 2 | find+tap `track-report-incident`, back | 0 | ✅ PASS |
| TC-CNL-017 | 5 | find+tap card, page_source×2, scroll_to `hoàn hàng` (NOT FOUND) | 2 | ❌ FAIL |
| TC-CNL-006 | 3 | find+tap `track-report-incident`, back×2 | 0 | ✅ PASS |
| TC-CNL-009 | 12 | find+tap card, scroll_to LỊCH SỬ ×2, page_source×2, set_value, tap confirm, `Đồng ý` | 2 | ❌ FAIL |
| TC-CNL-019 | 5 | find+tap card, page_source×2, scroll_to `hoàn hàng` (NOT FOUND) | 2 | ❌ FAIL |
| TC-CNL-016 | 2 | find+tap `track-report-incident` | 0 | ✅ PASS |
| TC-CNL-020 | 1 | back | 0 | 🚫 BLOCKED |

## Statistics
- Tổng snapshot (page source): ~19 · Số màn đã harvest: 6 — lệch do phải đọc LỊCH SỬ nhiều lần (trước/sau huỷ) và rà đủ 3 vai ở `Đang giao`.
- find_element NOT FOUND: 3 lần có chủ đích (`hoàn hàng` ×2 vai qua scroll_to, `LỊCH SỬ` ở Chi tiết tin) + 3 lần thao tác lỗi (element cache hết hạn / chọn nhầm id — đã tìm lại).
- 1 lần bấm trượt: `text("Xác nhận")` khớp **tiêu đề** popup lấy hàng ⇒ dùng `instance(1)`.
