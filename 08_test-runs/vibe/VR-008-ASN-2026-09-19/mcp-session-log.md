# MCP Session Log — VR-008 — 2026-09-19

## Session info
- Platform: mobile (Appium MCP, UiAutomator2)
- Device: emulator-5554 (720×1280)
- Session ID: `482f2d33-da4a-4db6-ba7c-575b694b21b2`
- Created: 11:32
- App: `com.hrisproject.stag` (host FoxPro_Stag — FoxEco là SDK nhúng)
- Pre-flight: ✅ select_device + session create + activate + get_window_size đều OK

> ⚠️ **Lệch so với template:** bước pre-flight thứ 3 dùng `appium_app_lifecycle(activate)` + `adb screencap`
> thay cho `appium_get_page_source`, và evidence chụp bằng `adb exec-out screencap`.
> Lý do đo được tại chỗ: `appium_screenshot` trả **216.355 ký tự** HTML viewer vào context mỗi lần gọi
> ⇒ ~21 TC sẽ vượt ngân sách context nhiều lần. `SKILL.md` cho phép `adb screencap` cho **evidence**.
> ⛔ Locator + action vẫn 100% qua MCP — không có locator nào suy từ ảnh.

## Pre-flight + Pha A (ghi từng call)

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| 1 | 11:32 | select_device | platform=android | OK emulator-5554 | Pre-flight |
| 2 | 11:32 | appium_session_management | action=create | OK sid=482f2d33 | Pre-flight |
| 3 | 11:33 | appium_app_lifecycle | activate com.hrisproject.stag | OK | Pre-flight |
| 4 | 11:33 | appium_get_window_size | — | 720×1280 | Pre-flight |
| 5 | 11:33 | appium_screenshot | *(không tham số)* | OK nhưng **216k ký tự** | ⇒ quyết định chuyển evidence sang `adb screencap` |
| A1 | 11:34 | appium_find_element + gesture tap | `text("Chức năng")` | OK | điều hướng host |
| A2 | 11:35 | appium_gesture | scroll_to_element `text("FoxEco")` | không thấy | app đã ở sẵn trong FoxEco (state khôi phục) |
| A3 | 11:35 | appium_gesture | action=back | OK | rời Chi tiết tin |
| A4 | 11:35 | appium_find_element + tap | `text("Trang chủ")` | OK | → xác định danh tính = **Đặng Châu Anh** |
| A5 | 11:36 | appium_find_element + tap | `text("Bảng tin")` | OK | → recon 3 tin NEED (`_recon__bang-tin-inventory.png`) |

## Pha B — 1 DÒNG / TC

| TC | Time | Calls | Chi tiết gộp | Snapshot? | Kết quả |
|----|------|------:|--------------|-----------|---------|
| TC-ASN-002 | 11:36 | 9 | find×4 (1 chủ ý NOT FOUND), gesture tap×3, scroll_to×1, screencap×2 | 0 | ✅ PASS |
| TC-ASN-001 | 11:39 | 8 | find×4, tap×3, get_text×1, screencap×2 | 0 | ✅ PASS |
| TC-ASN-004 *(chặng B)* | 11:41 | 5 | scroll/swipe×3, find×2 (2 SĐT), screencap×1 | 0 | ✅ PASS (chặng) |
| *(recon chuông B lần 1)* | 11:44 | 5 | find×3 (2 chủ ý NOT FOUND), tap×2, screencap×1 | 0 | ⛔ không sinh verdict — xem T-ASN-04 |
| *(recon OFFER của B)* | 11:46 | 5 | find×2, tap×2, swipe×1, screencap×2 | 0 | ⛔ recon |
| TC-ASN-020 *(chặng B)* | 11:47 | 13 | find×6, tap×5, set_value×1, get_attribute×1, screencap×3 | 0 | ✅ PASS (chặng) |
| *(đổi tài khoản B→A)* | 11:50 | 12 | scroll_to×2, find×6, tap×5, set_value×1, adb input OTP | 0 | ✅ login `stag_taipm@` |
| TC-ASN-003 | 11:54 | 9 | find×5 (3 chủ ý NOT FOUND), tap×2, screencap×2 | 0 | ✅ PASS |
| TC-ASN-004 *(chặng A)* | 11:55 | 3 | swipe×1, find×1, screencap×1 | 0 | ✅ PASS (chốt TC) |
| *(SEED S1)* | 11:57–12:09 | ~40 | wizard 3 bước; 3 lần thử ảnh (2 lần hỏng — T-ASN-01), grant permission qua adb | 0 | ✅ đăng tin thành công |
| *(SEED S2)* | 12:10–12:14 | ~26 | wizard 3 bước, 1 lần chạy suôn | 0 | ✅ |
| *(SEED S4)* | 12:15–12:20 | ~30 | wizard 3 bước; 1 lần vướng T-ASN-02 (địa chỉ giao chưa commit) | 0 | ✅ |
| *(SEED S3)* | 12:21–12:28 | ~34 | wizard 3 bước + **date picker** (22/09); 1 lần vướng T-ASN-02/03 | 0 | ✅ |
| *(đổi tài khoản A→B)* | 12:29 | 12 | scroll_to×2, find×6, tap×5, adb input OTP | 0 | ✅ login `stag_anhdc4@` |
| TC-ASN-009 | 12:31 | 7 | find×3, tap×2, scroll_to×1, screencap×2 | 0 | ✅ PASS |

## Statistics
- Total MCP calls: **~230** · **Tổng snapshot (`appium_get_page_source`): 0** · Số màn đã harvest: **7**
- 🔑 **0 snapshot / 7 màn** — toàn bộ locator lấy từ `locators/vibe-locators-latest.md` (cache VR-007) + `appium_find_element` trực tiếp, đúng luật **B1/B2** (`SKILL.md §CONTEXT BUDGET`). ⛔ Không lần nào phải dump full XML.
- `find_element`: ~95 (success ~88 · NOT FOUND 7 — trong đó **6 là chủ ý** làm chứng cứ âm, 1 là T-ASN-03)
- Action (tap/set_value/swipe/scroll_to): ~120
- `appium_screenshot` của MCP: **1 lần duy nhất** (pre-flight) — sau đó chuyển sang `adb screencap` vì tốn ~216k ký tự/lần (T-ASN-06)
- ⚠️ MCP **không** fail lần nào giữa phiên; session `482f2d33` sống suốt từ 11:32 đến 12:33.
