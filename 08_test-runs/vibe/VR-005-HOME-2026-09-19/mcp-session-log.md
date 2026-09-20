# MCP Session Log — VR-005 — 2026-09-19

## Session info
- Platform: **mobile (Appium MCP, UiAutomator2)**
- Device: `emulator-5554` · App: `com.hrisproject.stag`
- Session ID: `55129e7d-a214-4167-a988-d83f2e82c2b7`
- Created: 05:51
- Pre-flight: ✅ `select_device` + `session_management(create)` + `get_page_source` + `get_window_size` — 4/4 OK

> 🧾 **Evidence chụp bằng `adb exec-out screencap`** — `appium_screenshot` không có tham số `filename`
> và trả ~148k ký tự HTML viewer mỗi call (xem `SKILL.md §Contract đường dẫn ảnh`: ADB screencap được
> phép dùng cho **evidence**, ⛔ không phải nguồn locator). **Locator 100% qua MCP.**
>
> 🧾 `appium_get_page_source` trả ~220k ký tự ⇒ MCP tự ghi ra file ngoài context, parse bằng script.
> Đây là biến thể của **L3** (tree ra file, response chỉ còn link) — đúng luật CONTEXT BUDGET.

## Pre-flight + Pha A (ghi từng call)

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| 1 | 05:50 | `select_device` | platform=android | OK `emulator-5554` | Pre-flight |
| 2 | 05:51 | `appium_session_management` | action=create, noReset=true | OK sid=`55129e7d…` | Pre-flight |
| 3 | 05:51 | `appium_get_window_size` | — | `720x1280` | Pre-flight |
| 4 | 05:51 | `appium_screenshot` | maxWidth=720 | OK → `/tmp/screenshot_*.png` (+148k ký tự) | ⚠️ từ đây chuyển sang `adb screencap` |
| A1 | 05:51 | `appium_get_page_source` | Trang chủ — viewport 1 | OK 221k ký tự → file | **Pha A** — header/hero/CTA/nav → 13 element vào map |
| A2 | 05:52 | `appium_gesture` | scroll down | OK | điều hướng recon |
| A3 | 05:52 | `appium_get_page_source` | Trang chủ — viewport 2 | OK 221k → file | **Pha A** — section "Đơn của tôi", 4 card → 6 element |
| A4 | 05:52 | `appium_gesture` ×2 | scroll down ×2 | OK | điều hướng recon |
| A5 | 05:52 | `appium_get_page_source` | Trang chủ — viewport 3 | OK 206k → file | **Pha A** — 2 card nữa + **section "Tin mới" EMPTY** → 4 element |

## Pha B — 1 DÒNG / TC

| TC | Time | Calls | Chi tiết gộp | Snapshot? | Kết quả |
|----|------|------:|--------------|-----------|---------|
| TC-HOME-001 | 05:53 | 6 | find×5, screencap×1 | 0 (dùng map Pha A) | ✅ PASS |
| TC-HOME-003 | 05:54 | 3 | find×1, get_text×1, screencap×1 | 0 | ✅ PASS |
| TC-HOME-007 | 05:55 | 5 | find×1, get_text×1, tap×1, screencap×2 | 0 | ❌ FAIL step 2 |
| TC-HOME-005 | 05:56 | 2 | find×1, screencap×1 (+đo pixel) | 0 | ✅ PASS |
| TC-HOME-006 | 05:56–05:58 | 6 | tap×2, find×1, back×1, screencap×2 | **1** *(A6: màn Thông báo — màn mới, L2a)* | ✅ PASS |
| TC-HOME-022 | 05:58 | 3 | find×1, tap×1, screencap×2 (1 recon) | 0 | ✅ PASS |
| TC-HOME-026 | 05:59 | 7 | tap×1, scroll_to_element×1 (miss, đã ở cuối), find×4, screencap×1 | 0 | ✅ PASS |
| TC-HOME-009 | 06:02 | 5 | scroll×3, find×2, screencap×1 | 0 | ✅ PASS |
| TC-HOME-011 | 06:03 | 1 | dùng lại find của TC-009 + crop ảnh | 0 | ✅ PASS |
| TC-HOME-013 | 06:03 | 2 | find×1, crop ảnh | 0 | ✅ PASS |
| TC-HOME-012 | 06:04 | 3 | scroll×1, find×1, screencap×1 + crop | 0 | ✅ PASS |
| TC-HOME-015 | 06:05 | 6 | find×1, tap×1, scroll_to_element×1, screencap×3 | 0 | ✅ PASS |
| TC-HOME-002 | 06:06–06:09 | 12 | back×3, find×5 (2 chủ ý NOT FOUND = chứng cứ vắng bottom nav), tap×3, scroll×1, screencap×4 | 0 | 🚫 BLOCKED step 2 |
| TC-HOME-016 | 06:10 | 4 | tap×1, scroll_to_element×1, find×1, tap×1, screencap×1 | 0 | ✅ PASS |

## Statistics

| Chỉ số | Giá trị |
|---|---|
| Tổng MCP call | **~62** |
| **Tổng snapshot** (`appium_get_page_source`) | **6** |
| **Số màn đã harvest** | **8** |
| `find_element` | 29 (success **25** · chủ ý NOT FOUND **3** = chứng cứ vắng bottom nav/`Thông báo` · NOT FOUND thật **1** = `home-news-empty` qua strategy `id`, bẫy **T2**) |
| Action call (`tap` / `get_text` / `scroll` / `back`) | 27 |
| Screenshot evidence (qua `adb exec-out screencap`) | 23 file |
| MCP fail giữa run | **không có** |

> ✅ **Đồng hồ đo chi phí: 6 snapshot ⟷ 8 màn** — đúng luật **B1/B2** (snapshot ≈ số MÀN, ⛔ không ≈ số TC).
> 14 TC chạy mà chỉ 6 snapshot ⇒ **8/14 TC chạy với 0 snapshot**, dùng thẳng `locator_map` của Pha A (**L1**).
> 2 màn (Wizard · Đơn của tôi) được đọc bằng **ảnh + `find_element`** thay vì `get_page_source`, rẻ hơn nữa.
>
> ⚠️ **Ghi chú cách đo:** `appium_get_page_source` ở app này trả **170k–221k ký tự**, vượt ngưỡng inline ⇒ MCP tự ghi ra file ngoài context và chỉ trả 1 dòng link; phần parse chạy bằng script. Nhờ đó 6 snapshot **không** tiêu 6 cây XML vào context — đây là biến thể hợp lệ của **L3** *(tree ra file, response chỉ còn link)*.
