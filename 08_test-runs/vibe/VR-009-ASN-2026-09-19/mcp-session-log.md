# MCP Session Log — VR-009 — 2026-09-19

## Session info
- Platform: mobile (**Appium MCP**, UiAutomator2)
- Device: `emulator-5554` (AVD `qa_a33`, 720×1280) — ⚠️ **emulator chưa chạy lúc bắt đầu phiên**, phải boot thủ công (`emulator -avd qa_a33`, boot xong sau ~10s)
- Session ID: `91f7628d-dc29-4440-af70-5263197828f3` (sống suốt 14:47 → 15:46, ⛔ không fail lần nào)
- App: `com.hrisproject.stag` (host FoxPro_Stag · FoxEco là SDK nhúng)
- Pre-flight: ✅ `select_device` → `session_management(create)` → `app_lifecycle(activate)` → evidence-path check đều OK
- Tài khoản dùng trong phiên: `stag_anhdc4@` (B) → `stag_giangdc2@` (D) → `stag_anhdc4@` (B) → `stag_giangdc2@` (D) — **3 lượt đổi**

> ⚠️ **Lệch template (giữ nguyên lý do của VR-008):** evidence chụp bằng `adb exec-out screencap -p`, ⛔ không dùng `appium_screenshot`
> vì mỗi lần gọi trả **~216k ký tự** HTML viewer vào context. `SKILL.md` cho phép `adb screencap` cho vai trò **evidence**.
> 🔑 **Locator + action vẫn 100% qua MCP** — ⛔ không có locator nào suy từ ảnh, ⛔ không dùng `adb input tap` để thao tác element
> (ngoại lệ duy nhất: `adb shell input text "$OTP"` vào ô OTP **tự focus**, đúng cách VR-008 đã xác lập, và 2 lần tap toạ độ nêu ở bảng dưới).

## Pre-flight + Pha A (ghi từng call)

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| 1 | 14:47 | `select_device` | platform=android | OK `emulator-5554` | Pre-flight |
| 2 | 14:47 | `appium_session_management` | action=create | OK sid=`91f7628d` | Pre-flight |
| 3 | 14:48 | `appium_app_lifecycle` | activate `com.hrisproject.stag` | OK | Pre-flight |
| 4 | 14:48 | *(adb)* `screencap` | `_setup__preflight-launch.png` | OK, file tồn tại trong `screenshots/` | **Evidence-path pre-flight PASS** |
| A1 | 14:48 | `find_element` + `gesture tap` | `text("Chức năng")` | OK | điều hướng host → danh tính = **Đặng Châu Anh** (B) |
| A2 | 14:48 | `gesture scroll_to_element` + tap | `text("FoxEco")` (3 nhịp, preset small) | OK | vào FoxEco |
| A3 | 14:49 | `find_element` + tap | `accessibility id "Thông báo"` | OK | màn Thông báo — recon 3 thông báo khớp tuyến |
| A4 | 14:50 | `find_element` + tap | `textContains("Tìm thấy…").instance(0)` | OK | mở Chi tiết tin |
| A5 | 14:51 | `gesture scroll/swipe` ×4 | duyệt Chi tiết tin | OK | xác lập: màn này **KHÔNG có mục GHI CHÚ** |
| A6 | 14:52 | **`appium_get_page_source`** | Chi tiết tin | OK — **170.483 ký tự, MCP tự ghi ra FILE** | ⚠️ **snapshot DUY NHẤT của phiên**; trả về file nên ⛔ không đẩy cây vào context |
| A7 | 14:53–14:57 | `gesture back/scroll` + *(adb)* `force-stop`+`activate` | khôi phục màn Thông báo | OK | xác nhận nhóm `HÔM NAY` **rỗng thật**, ⛔ không phải lỗi refresh |
| A8 | 14:54 | `find_element` + tap | `text("Bảng tin")` | OK | kiểm kê 6 tin NEED (bảng trong `vibe-log.md`) |

## Pha B — 1 DÒNG / TC

| TC | Time | Calls | Chi tiết gộp | Snapshot? | Kết quả |
|----|------|------:|--------------|-----------|---------|
| *(đổi tài khoản B→D)* | 14:58–15:01 | 14 | scroll_to×1, find×7, tap×5, set_value×1, `adb input` OTP | 0 | ✅ login `stag_giangdc2@` · ⚠️ lần bấm `NHẬN MÃ OTP` đầu lỗi mạng, bấm lại OK |
| **TC-ASN-005** | 15:02–15:05 | 12 | find×3, tap×3, scroll_to×3 (**3 chủ ý NOT FOUND**), find×2 phủ định SĐT, screencap×2 | 0 | ✅ PASS |
| **TC-ASN-007** | 15:06 | 8 | find×4, tap×3, scroll_to×1 (chủ ý NOT FOUND), screencap×2 | 0 | ✅ PASS |
| **TC-ASN-020** *(step 6–9)* | 15:07–15:10 | 13 | scroll_to×1, find×6, tap×5, get_text×1, screencap×3 | 0 | ✅ PASS ⇒ chốt verdict cuối |
| *(SEED `OFFER-C1`)* | 15:12–15:14 | 14 | find×6, tap×4 (**1 tap toạ độ** = checkbox điều khoản OFFER, ⛔ không có resourceId), set_value×2, scroll×2 | 0 | ✅ *"Đã ghi nhận tuyến đường!"* |
| *(đổi tài khoản D→B)* | 15:15–15:16 | 14 | scroll_to×2, find×7, tap×5, set_value×1, `adb input` OTP | 0 | ✅ login `stag_anhdc4@` |
| *(SEED `N1` khớp đủ)* | 15:17–15:22 | 28 | wizard 3 bước: find×13, tap×9, set_value×4, scroll_to×6, get_attribute×1, **1 tap toạ độ** (ô ảnh trong Photo Picker hệ thống) | 0 | ✅ *"Đăng tin thành công!"* |
| *(SEED `N2` lệch buổi)* | 15:23–15:26 | 26 | wizard 3 bước, chạy suôn | 0 | ✅ |
| *(SEED `N3` lệch điểm giao)* | 15:27–15:31 | 27 | wizard 3 bước + `get_text` kiểm gợi ý địa chỉ | 0 | ✅ |
| *(SEED `N4` lệch ngày)* | 15:32–15:35 | 28 | wizard 3 bước + **date picker** (chọn `22`) | 0 | ✅ |
| *(đổi tài khoản B→D)* | 15:36–15:37 | 13 | scroll_to×2, find×6, tap×5, `adb input` OTP | 0 | ✅ login `stag_giangdc2@` |
| **TC-ASN-022** | 15:38–15:40 | 9 | find×5 (**1 chủ ý NOT FOUND** `instance(1)`), tap×3, scroll_to×1, screencap×2 | 0 | ✅ PASS |
| **TC-ASN-011** | 15:40–15:41 | 9 | find×5 (1 chủ ý NOT FOUND), tap×3, scroll_to×1, screencap×2 | 0 | ✅ PASS |
| **TC-ASN-012** | 15:41–15:42 | 9 | find×5 (1 chủ ý NOT FOUND), tap×3, scroll_to×1, screencap×2 | 0 | ✅ PASS |
| **TC-ASN-010** | 15:42–15:43 | 9 | find×5 (**1 chủ ý NOT FOUND** = `"Nhận giao"`), tap×3, scroll_to×1, screencap×2 | 0 | ✅ PASS |
| *(quan sát bổ sung: chuông sau khi ghép N1)* | 15:46 | 5 | back×2, find×2, screencap×2 | 0 | ⛔ không sinh verdict — xem `vibe-log.md §Quan sát bổ sung` |

## Statistics
- **Total MCP calls: ~245** · **Tổng snapshot (`appium_get_page_source`): 1** · **Số màn đã harvest: 9**
- 🔑 **1 snapshot / 9 màn** — đúng luật **B1/B2** (`SKILL.md §CONTEXT BUDGET`): toàn bộ locator lấy từ `locators/vibe-locators-latest.md` (cache VR-001…VR-008) rồi `appium_find_element` gọi thẳng. Lần snapshot duy nhất là để **chứng minh màn Chi tiết tin không có mục GHI CHÚ** (L2b — oracle cũ của VR-008 không dùng được), và MCP **tự ghi ra file** nên ⛔ không tốn context.
- `find_element`: **~105** (success ~96 · NOT FOUND **9**, trong đó **8 là CHỦ Ý** làm chứng cứ âm: `FTEL SG08`×3, SĐT A/B×2, `Tìm thấy…tuyến`×1 cho TC-007, `instance(1)`×4 cho 010/011/012/022, `"Nhận giao"`×1 — và **1 là thật**: `text("Bạn sẽ đến đâu")` chưa render, đã scroll rồi tìm lại OK)
- Action (tap/set_value/scroll_to/swipe/back): **~135** — trong đó **chỉ 2 tap toạ độ**, cả 2 đều là element **không có locator ổn định** (checkbox điều khoản OFFER · ô ảnh trong Android Photo Picker), ⛔ không dùng toạ độ thay cho element có locator
- `adb`: `screencap` (evidence) · `force-stop`+`activate` (lifecycle) · `input text` (ô OTP tự focus) — ⛔ **0 lần** `adb input tap` để thao tác element
- ⚠️ MCP **không fail** lần nào. Sự cố duy nhất là **phía app**: 1 lần `NHẬN MÃ OTP` trả *"Không thể kết nối mạng!"* lúc 15:00 (ping emulator OK, ~294ms) — bấm lại lần 2 thành công ⇒ ghi thành bẫy **T-ASN-07**.
