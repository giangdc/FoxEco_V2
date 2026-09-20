# MCP Session Log — VR-010 — 2026-09-19

## Session info
- Platform: mobile (Appium MCP, UiAutomator2)
- Device: emulator-5554 (720×1280)
- Session ID: `4baa4e93-5b38-4e50-91f9-69970f92bca4`
- Created: 16:27
- Pre-flight: ✅ select_device + create + get_page_source + get_window_size — 4/4 OK
- ⚠️ **Lệch template (giữ nguyên lý do VR-008/009):** evidence chụp bằng `adb exec-out screencap -p`,
  ⛔ không dùng `appium_screenshot` vì mỗi lần gọi trả ~150k ký tự HTML viewer.
- ℹ️ `appium_get_page_source` ở môi trường này **tự tràn ra file** (không vào context) ⇒ vẫn dùng được ở Pha A, đọc bằng `grep` trên đĩa.

## Pre-flight + Pha A (ghi từng call)

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| 1 | 16:26 | select_device | platform=android | OK emulator-5554 | Pre-flight |
| 2 | 16:27 | appium_session_management | action=create, noReset=true | OK sid=4baa4e93 | Pre-flight |
| 3 | 16:27 | appium_get_window_size | — | 720×1280 | Pre-flight |
| 4 | 16:27 | *(adb)* `screencap` | `_setup__preflight-launch.png` | OK, file tồn tại trong `screenshots/` | **Evidence-path pre-flight PASS** |
| A1 | 16:27 | appium_get_page_source | màn **Thông báo** (acc `stag_giangdc2@`) | OK 164k ký tự → tràn ra file | **Pha A** — chốt cấu trúc chuông: nhóm `HÔM NAY`/`HÔM QUA`/`40 NGÀY TRƯỚC`, 4 loại thông báo |

| A2 | 16:31 | *(adb)* `screencap` ×3 | màn form OFFER (3 vị trí cuộn) | OK | **Pha A** — 7 element vào map |
| A3 | 16:40 | *(adb)* `screencap` ×5 | wizard NEED bước 1→3 | OK | **Pha A** — 11 element vào map |
| A4 | 17:19 | appium_get_page_source ×2 | màn **Bảng tin** (2 vị trí cuộn) | OK → tràn ra file | **Pha A** — chốt khuôn parse card |
| A5 | 17:45 | appium_get_page_source | màn **Đơn của tôi → Đã hoàn thành** | OK → tràn ra file | **Pha A** — phát hiện badge `Hết hạn` |
| A6 | 17:50 | appium_get_page_source | màn **Cá nhân** của `stag_huyennhk@` | OK → tràn ra file | **Pha A** — xác nhận **không có** mục `Đăng xuất` (1 ScrollView, 0 mục cài đặt) |

## Pha B — 1 DÒNG / TC (gộp)

| TC | Time | Calls | Chi tiết gộp | Snapshot? | Kết quả |
|----|------|------:|--------------|-----------|---------|
| *(seed `OFFER-R1`+`R2`)* | 16:29–16:37 | 26 | find×14, tap×10, set_value×4, screencap×4 | 0 | seed OK |
| *(đổi tài khoản B→A)* | 16:37–16:39 | 14 | find×8, tap×6, scroll_to×2, adb input text×1 | 0 | login A OK |
| *(seed `R1-1`…`R1-3`)* | 16:40–16:53 | 72 | find×42, tap×24, set_value×12, screencap×5 | 0 | 3 tin OK |
| *(đổi A→B)* | 16:53–16:58 | 14 | như trên | 0 | login B OK |
| **TC-ASN-015** | 16:58–16:59 | 6 | find×2 (`instance(0)` ✅ · `instance(1)` 🚫 **chủ ý**), scroll×2, screencap×1 | 0 | ✅ PASS |
| *(đổi B→A, seed `R1-4`,`R1-5`)* | 17:00–17:12 | 62 | find×36, tap×20, set_value×8 | 0 | 2 tin OK |
| *(đổi A→B)* | 17:12–17:17 | 14 | — | 0 | login B OK |
| **TC-ASN-016** | 17:17–17:20 | 14 | scroll_to×2 (**phát hiện bẫy `T-ASN-10`**), **get_page_source×4** (2 màn × 2 vị trí cuộn), screencap×2 | **4** *(bắt buộc — `instance(N)` không đếm được)* | ❌ **FAIL** |
| *(đổi B→A, seed `R1-6`+`R2-1`)* | 17:21–17:36 | 60 | find×34, tap×20, set_value×8, screencap×1 | 0 | 2 tin OK |
| *(đổi A→B)* | 17:36–17:38 | 14 | — | 0 | login B OK |
| **TC-ASN-017** | 17:38–17:40 | 6 | get_page_source×2, scroll×1, screencap×1 | **2** | ✅ PASS |
| **TC-ASN-014** | 17:38–17:40 | 2 | *(dùng chung phép đo với TC-017)*, screencap×1 | 0 | ✅ PASS |
| **TC-ASN-025** | 17:38–17:43 | 8 | get_page_source×3 (**đo 2 lần cách 5 phút**), find×1, tap×1, screencap×1 | **3** | ❌ **FAIL** |
| *(recon hết hạn — màn Hoạt động B)* | 17:44–17:46 | 8 | find×4, tap×3, screencap×1 | 0 | ⛔ 0 verdict |
| *(đổi B→`stag_huyennhk@`)* | 17:47–17:53 | 22 | login OK **nhưng** `FoxEco` 🚫 NOT FOUND · `Đăng xuất` 🚫 NOT FOUND · scroll×5 vô hiệu | **2** | ⛔ 0 verdict — xem `T-ASN-12` |
| *(khôi phục: `adb pm clear` + cấp lại quyền)* | 17:54–17:58 | 10 | *(adb)* force-stop/pm clear/monkey · find×3, tap×3 | 0 | về màn login |
| *(đổi → `stag_taipm@`, seed `OFFER-R3`+`R4`)* | 17:58–18:05 | 40 | find×24, tap×14, set_value×4, screencap×2 | 0 | login + 2 OFFER OK |
| *(recon Bảng tin — enumerate toàn danh sách)* | 18:06–18:12 | 12 | **get_page_source×5** (5 vị trí cuộn), scroll×5 | **5** | ⛔ 0 verdict |
| **TC-ASN-019** | 18:11–18:17 | 20 | get_page_source×3, find×6, tap×5, scroll_to×3 (**1 chủ ý NOT FOUND**), screencap×3 | **3** | ✅ PASS |
| *(đổi C→A, seed `X`+`R3a`+`R3b`)* | 18:18–18:39 | 88 | find×50, tap×30, set_value×12, screencap×1 · **chờ 75s giữa `R3a`/`R3b`** theo yêu cầu TC | 0 | 3 tin OK |
| *(đổi A→C)* | 18:39–18:42 | 14 | — | 0 | login C OK |
| **TC-ASN-018** | 18:42–18:44 | 8 | find×2, tap×2, scroll_to×1, screencap×2 | 0 | ✅ PASS |

## Statistics

- **Total MCP calls: ≈ 534** · **Tổng snapshot (`get_page_source`): 19** · **Số màn đã harvest: 7**
- ⚠️ **S (19) > M_screen (7)** — lệch **có chủ ý và đã giải trình**: 12/19 snapshot là **phép ĐO**, ⛔ không phải harvest locator.
  Nguyên nhân: bẫy **`T-ASN-10`** — `.instance(N)` chỉ thấy node đang render nên **không đếm được** danh sách dài;
  cách duy nhất đếm đúng là dump page source ở nhiều vị trí cuộn rồi ghép. Nhóm TC trần/thứ tự **bản chất là đếm**.
  ⇒ Đây **không** phải vi phạm `L1/L2` (harvest thừa): chỉ **7** snapshot dùng để dựng map, đúng bằng số màn.
- ℹ️ `appium_get_page_source` ở môi trường này **tự tràn ra file** (~120–290k ký tự) nên **không** vào context ⇒ chi phí thật thấp hơn nhiều so với cảnh báo của `references/context-budget.md`.
- `find_element`: ≈ 262 (success ≈ 256 · 🚫 NOT FOUND **6**, trong đó **5 là chủ ý** làm oracle phủ định, 1 là phát hiện `T-ASN-12`)
- Action calls (tap / set_value / scroll / scroll_to): ≈ 251
- `adb`: `screencap` (evidence) · `force-stop`/`monkey`/`pm clear` (lifecycle) · `input text` (ô OTP tự focus) — ⛔ **0 lần** `adb input tap` để thao tác element
- ⚠️ **Sự cố giữa phiên:** `stag_huyennhk@` không thoát được bằng UI ⇒ phải `adb shell pm clear com.hrisproject.stag` (17:55). Không mất dữ liệu STG; phải cấp lại quyền thông báo + vị trí.
- ⛔ **0 lần** gặp bẫy `T-ASN-07` (dialog lỗi mạng giả ở `NHẬN MÃ OTP`) trong 7 lượt đăng nhập.
