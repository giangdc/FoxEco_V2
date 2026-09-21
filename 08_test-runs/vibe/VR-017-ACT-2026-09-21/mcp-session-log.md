# MCP Session Log — VR-017 — 2026-09-21

## Session info
- Platform: mobile (Appium MCP, UiAutomator2)
- Device: `emulator-5554` (720×1280 theo toạ độ page source)
- Session ID: `7d44341c-8a3e-45c5-ac5e-7d4e134d157e`
- Capabilities: `noReset=true` · `appPackage=com.hrisproject.stag` · `appActivity=com.hrisproject.MainActivity` · `autoLaunch=false` · `systemPort=8201`
- Created: ~22:02 (giờ máy host; máy ảo hiển thị 10:02)
- Pre-flight: ✅ `select_device` + `session create` + `get_page_source` (màn Hoạt động) OK
- ⚠️ **Lệch template (giống VR-015):** ảnh evidence chụp bằng `adb exec-out screencap -p` ghi thẳng vào `screenshots/` (vì `appium_screenshot` trả HTML viewer rất lớn và lưu ra `/tmp`). `appium_screenshot` chỉ dùng 1 lần (ảnh element `TC-ACT-008__verify-*`, đã move vào run folder).
- ⚠️ `adb shell uiautomator dump` **không dùng được** khi Appium UiAutomator2 đang chạy (xung đột) ⇒ đọc trạng thái danh sách bằng `appium_get_page_source` (kết quả >100k ký tự tự ghi ra file, parse bằng script).
- Thao tác điều hướng thuần (`input keyevent 4`, `input swipe` fling về đầu danh sách, `input tap` trong burst chụp của `TC-ACT-018`) dùng adb — ⛔ không ghi locator nào từ các thao tác này.

## Pre-flight + Pha A

| # | MCP method | Args (summary) | Result | Note |
|--:|-----------|----------------|--------|------|
| 1 | select_device | android | OK `emulator-5554` | Pre-flight |
| 2 | appium_session_management | create | OK sid `7d44341c…` | Pre-flight |
| A1 | find_element + tap | `text("Chức năng")` → scroll_to_element `textContains("FoxEco")` → tap | OK | vào FoxEco (FoxPro host) |
| A2 | find_element + tap | `text("Hoạt động")` | OK | nav FoxEco |
| A3 | appium_get_page_source | màn `Đơn của tôi` (có dữ liệu) | OK 180k chars → file | **Pha A** — tiêu đề, 2 tab, 5 mục nav |
| A4 | appium_get_page_source | màn `Đơn của tôi` rỗng (`MinhNDN2`) | OK 155k chars → file | **Pha A** — empty state 2 tab |
| A5 | find_element + tap/set_value | luồng đăng xuất/đăng nhập FoxPro | OK | `Cá nhân` → `Đăng xuất` → `Đồng ý` → `Nhập email đăng nhập` → `NHẬN MÃ OTP` → `ĐĂNG NHẬP` (×2 lượt) |

## Pha B — 1 dòng / TC

| TC | Calls (xấp xỉ) | Chi tiết gộp | Snapshot? | Kết quả |
|----|------:|--------------|-----------|---------|
| TC-ACT-001 | 3 | find×1, tap×1, page_source×1 (A3) | 1 (Pha A) | ✅ PASS |
| TC-ACT-005 | 30 | rà cả tab `Đã hoàn thành`: scroll×14, page_source×14, find/tap tab | 14 (rà danh sách dài — dùng chung 005/008/013/015) | 🚫 BLOCKED |
| TC-ACT-008 | 3 | find `textStartsWith("Không có ai nhận mang giúp")`, get_text, screenshot(element) | 0 | ❌ FAIL |
| TC-ACT-013 | 0 thêm | dùng kết quả rà của lô 1 | 0 | ✅ PASS |
| TC-ACT-015 | 3 | find+tap `text("Đang diễn ra")`, find `text("Đã huỷ")` = tìm thấy | 0 | ❌ FAIL |
| TC-ACT-014 | 3 | find+tap `Hoạt động`, `Đã hoàn thành`, page_source×1 | 1 | ✅ PASS |
| TC-ACT-012 | 3 | find+tap `Hoạt động`, page_source×1 | 1 (A4) | ❌ FAIL |
| TC-ACT-016 | 30 | find+tap 5 mục nav × 2 tab + find phần tử xác nhận màn đích, `back`×2 | 0 | ✅ PASS |
| TC-ACT-017 | 6 | find `scrollable(true)` ×2 (không thấy), page_source×1, find+tap tab | 1 | ❌ FAIL |
| TC-ACT-018 | 5 | find+tap `Trang chủ`, scroll_to_element + tap FoxEco (vào lại) | 0 | ✅ PASS |

## Statistics
- Tổng snapshot (page source): ~19 · Số màn đã harvest: 3 (`Đơn của tôi` có dữ liệu · `Đơn của tôi` rỗng · FoxPro login)
  ⚠️ Lệch lớn là do **rà danh sách dài 14 khung** của `anhdc4` (~30 card `Hết hạn` + ~17 card `Hoàn thành`) — cần thiết để kết luận `005`/`013`/`015` trên TOÀN danh sách, không phải snapshot thừa.
- find_element: ~45 (NOT FOUND: 2 — cả 2 là `scrollable(true)` của `TC-ACT-017`, là kết quả kiểm chứ không phải lỗi locator)
- MCP failures: 1 — `scroll_to_element direction=up` báo *page source did not change* (không cuộn lên được) ⇒ thay bằng adb fling
- Đăng nhập: 2 lượt đổi tài khoản (`anhdc4` → `thuyntt22` → `MinhNDN2`); 1 lần gặp bẫy `T-ASN-07`
- Throttle mạng (`TC-ACT-018`): `adb emu network speed umts` + `delay umts` → đã trả `speed full` + `delay none`
