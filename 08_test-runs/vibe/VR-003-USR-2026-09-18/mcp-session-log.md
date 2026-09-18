# MCP Session Log — VR-003 — 2026-09-18

## Session info
- Platform: mobile (Appium MCP, UiAutomator2)
- Device: emulator-5554 (`sdk_gphone64_x86_64`, 1080x2400)
- Session ID: `086251e5-bb53-428a-8667-731d11f7f68e`
- Created: 17:13
- Host app: `com.hrisproject.stag` / `com.hrisproject.MainActivity`
- Tài khoản đang đăng nhập: `stag_thuyntt22@fpt.com` · MNV `00002352` · "Nguyễn Thị Thanh Thủy" (người chạy đăng nhập tay + OTP trước khi bàn giao)
- Pre-flight: ✅ select_device · session create (`noReset=true`, `autoLaunch=false` để giữ phiên đăng nhập OTP) · get_page_source · evidence-path check — OK

> 🧾 **Evidence chụp bằng `adb exec-out screencap`, KHÔNG bằng `appium_screenshot`** — giữ nguyên lý do cơ học đã ghi ở VR-001: `appium_screenshot` của MCP này không có tham số `filename` và trả viewer HTML rất lớn vào context. `adb screencap` ghi thẳng đường dẫn tuyệt đối trong `screenshots/`. ⛔ Locator thì 100% qua MCP.
> 📄 `appium_get_page_source` vượt ngưỡng inline ⇒ MCP tự lưu ra file tool-result; locator vẫn là chuỗi MCP trả về nguyên văn.

## Pre-flight + Pha A (ghi từng call)

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| 1 | 17:12 | select_device | platform=android | OK emulator-5554 | Pre-flight |
| 2 | 17:13 | appium_session_management | action=create, noReset=true, autoLaunch=false | OK sid=086251e5 | Pre-flight |
| 3 | 17:13 | *(adb screencap)* | `_setup__preflight-launch.png` | OK, file trong run folder | Evidence-path pre-flight ✅ |
| A1 | 17:14 | appium_find_element | accessibility id `Trang chủ` | OK | Pha A — điều hướng |
| A2 | 17:14 | appium_gesture | tap `Trang chủ` | OK | Pha A |
| A3 | 17:14 | appium_find_element | accessibility id `Cá nhân` | OK | Pha A |
| A4 | 17:14 | appium_gesture | tap `Cá nhân` | OK | Pha A |
| A5 | 17:15 | appium_get_page_source | màn **Cá nhân** | OK 203.565 ký tự | **Pha A** — 9 element vào map |
| A6 | 17:16 | appium_find_element + gesture | accessibility id `profile-menu-editProfile` | OK | Pha A |
| A7 | 17:17 | appium_get_page_source | màn **Cập nhật thông tin** | OK 137.035 ký tự | **Pha A** — 6 element; 2 EditText `showing-hint="true"` ⇒ **rỗng** |
| A8 | 17:21 | appium_get_page_source | màn **HRIS · Thông tin cá nhân → Thông tin** | OK 166.025 ký tự | **Pha A (ngoài FoxEco)** — đọc **oracle HRIS** cho `TC-USR-043` |
| A9 | 17:23 | appium_get_page_source | màn **HRIS · Quá trình làm việc** | OK 142.603 ký tự | **Pha A (ngoài FoxEco)** — tìm địa chỉ làm việc cho `TC-USR-040`: **không có trường này** |

**Số màn đã harvest ở Pha A: 5** (FoxEco: Cá nhân · Cập nhật thông tin — HRIS: Thông tin cá nhân · Thông tin · Quá trình làm việc)
**Tổng `get_page_source` cả run: 5** ≈ số màn ⇒ đúng luật B1/B2 (act bằng selector, không snapshot lại màn đã biết).

## Pha B — 1 DÒNG / TC

| TC | Time | Calls | Chi tiết gộp | Snapshot? | Kết quả |
|----|------|------:|--------------|-----------|---------|
| TC-USR-006 | 17:15 | 5 | find×2 + tap×2 (nav `Trang chủ`→`Cá nhân`), đọc card từ page source A5 | 0 (dùng A5) | ✅ PASS |
| TC-USR-043 | 17:17 | 5 | find `(//android.widget.EditText)[1]` + tap, `mobile: isKeyboardShown`, `get_element_attribute(text)` | 0 (dùng A7) | ❌ FAIL step 5 |
| TC-USR-040 | 17:18 | 4 | find `(//android.widget.EditText)[2]` + tap, `isKeyboardShown`, `get_element_attribute(text)` | 0 (dùng A7) | ❌ FAIL step 5 |
| TC-USR-027 | 17:24 | 16 | nav vào lại FoxEco (back×4, find/tap `Chức năng`, `FoxEco`, `Cá nhân`, `profile-menu-editProfile`), set_value×2, get_attribute×3, find/tap `Lưu thay đổi`×2, find `textContains("Đã lưu")`🚫, find `profile-menu-editProfile` | 0 | ✅ PASS |

**MCP calls Pha B: 30** · **MCP fail giữa run: không có.**
