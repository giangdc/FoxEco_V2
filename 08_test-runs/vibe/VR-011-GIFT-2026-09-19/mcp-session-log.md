# MCP Session Log — VR-011 — 2026-09-19

## Session info
- Platform: mobile (Appium MCP, UiAutomator2)
- Device: emulator-5554 (720×1280)
- Session ID: `b69a6f75-56db-4181-a8d0-40c3d597b20c`
- Created: 20:15
- Pre-flight: ✅ select_device + create + get_window_size + get_page_source — 4/4 OK
- ⚠️ **Lệch template (giữ nguyên lý do VR-008/009/010):** evidence chụp bằng `adb exec-out screencap -p`,
  ⛔ không dùng `appium_screenshot` vì mỗi lần gọi trả ~150k ký tự HTML viewer vào context.
- ℹ️ `appium_get_page_source` ở môi trường này **tự tràn ra file** (không vào context) ⇒ dùng được ở Pha A, đọc bằng `grep`/`python` trên đĩa.

## Pre-flight + Pha A (ghi từng call)

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| 1 | 20:14 | select_device | platform=android | OK emulator-5554 | Pre-flight |
| 2 | 20:15 | appium_session_management | action=create, noReset=true | OK sid=b69a6f75 | Pre-flight |
| 3 | 20:15 | appium_get_window_size | — | 720×1280 | Pre-flight |
| 4 | 20:15 | *(adb)* `screencap` | `_setup__preflight-launch.png` | OK, file tồn tại trong `screenshots/` | **Evidence-path pre-flight PASS** |
| 5 | 20:15 | appium_find_element + gesture tap | `text("Đồng ý")` | OK | Đóng dialog lỗi mạng giả (**bẫy `T-ASN-07`**, ping 8.8.8.8 0% loss) |
| A1 | 20:18 | appium_get_page_source | màn **Đơn của tôi → Đã hoàn thành** (acc `stag_taipm@`) | OK 214k ký tự → tràn ra file | **Pha A** — chốt khuôn card đơn hoàn thành + 3 biến thể hint quà |
| A2 | 20:18–20:20 | *(adb)* `screencap` ×5 | 5 vị trí cuộn của danh sách "Đã hoàn thành" | OK | **Pha A** — kiểm kê đơn: **2 đơn có hint `Chạm để tặng quà`** (chưa tặng, mình là người gửi) · nhiều đơn `Đã tặng quà` · nhiều đơn không hint |

## Pha B — 1 DÒNG / TC (gộp)

| TC | Time | Calls | Chi tiết gộp | Snapshot? | Kết quả |
|----|------|------:|--------------|-----------|---------|
| *(pre-flight)* | 20:15–20:16 | find_element + gesture tap | `text("Đồng ý")` · `text("Cá nhân")` · `text("Chức năng")` | OK | Thoát dialog lỗi mạng giả, định vị màn |
| **TC-GIFT-001** | 20:26–20:28 | 6 | find×3, tap×2, get_text×1, screencap×2 | 0 *(dùng locator_map)* | ❌ **FAIL** step 3–4 |
| **TC-GIFT-002** | 20:28–20:29 | 3 | find×2 (`instance(3)` ✅ · `instance(4)` 🚫 **chủ ý**), screencap×1 | 0 | ✅ PASS |
| **TC-GIFT-004** | 20:29–20:31 | 3 | find×2 (regex tiền tệ 🚫 + regex đối chứng ✅), screencap×1 | 0 | ✅ PASS |
| **TC-GIFT-010** | 20:31–20:33 | 8 | find×3, tap×3, swipe×1, screencap×2 | 0 | ❌ **FAIL** step 4–5 |
| **TC-GIFT-003** | 20:33–20:35 | 9 | find×4, tap×3, get_text×1, screencap×3 | 0 | ❌ **FAIL** step 5 *(chuỗi popup)* |
| **TC-GIFT-005** | 20:36–20:40 | 18 | find×8, tap×6, back×2, get_element_attribute×2, screencap×4 | 0 | ✅ PASS |
| **TC-GIFT-007** | 20:42–20:43 | 4 | find×2, tap×2, screencap×1 | 0 | ✅ PASS |
| **TC-GIFT-009** | 20:43–20:44 | 3 | find×1, tap×1, screencap×1 | 0 | ✅ PASS |
| **TC-GIFT-013** | 20:45 | 4 | find×2 (regex trạng thái hoàn hàng 🚫 **chủ ý**), tap×1, screencap×1 | 0 | 🚫 **BLOCKED** step 1 |
| **TC-GIFT-014** | 20:45–20:46 | 4 | find×1, tap×1, screencap×1 | 0 | 🚫 **BLOCKED** step 3 |
| *(đổi acc `taipm` → `giangdc2`)* | 20:47–20:51 | 20 | find×11, tap×9, set_value×1, scroll_to×2, *(adb input text OTP)*×1 | 0 | login OK · ⚠️ dính bẫy `T-ASN-07`, retry 1 lần |
| **TC-GIFT-012** | 20:51–20:52 | 6 | tap×2 (1 tap **toạ độ** cho icon chuông — ⚠️ chưa có locator), find×1, get_text×1, screencap×2 | 0 | ❌ **FAIL** step 4 |
| *(đổi acc `giangdc2` → `anhptm17`)* | 20:53–20:56 | 20 | find×11, tap×9, set_value×1, scroll_to×2, *(adb input text OTP)*×1 | 0 | login OK · 🆕 danh tính mới: **Phan Thị Mỹ Anh** `00287493` |
| **TC-GIFT-006** | 20:57 | 6 | find×4 (2× 🚫 **chủ ý** cho loại count = 0), tap×2, screencap×1 | 0 | ✅ PASS *(có hoán tên loại quà, đã khai)* |
| *(thăm dò `TC-GIFT-011`)* | 20:58–21:00 | 5 | find×2, tap×2, scroll_to×1 (🚫 `Chạm để tặng quà`) | 0 | ⏳ NOT_RUN — acc không có đơn đủ điều kiện |

## Statistics

- **Total MCP calls: ~125** · **Tổng snapshot (`get_page_source`): 2** · **Số màn đã harvest: 7** ← S (2) ≤ M_screen (7) ✅ **không vi phạm B1/B2**
  *(2 snapshot đều ở Pha A; toàn bộ 12 TC của Pha B chạy **0 snapshot**, thuần `find_element` từ `locator_map`)*
- `find_element` calls: **~58** (success **~50** · NOT FOUND **8** — trong đó **7 là 🚫 CHỦ Ý** để chứng minh vắng mặt: `instance(4)` ở TC-002, regex tiền tệ ở TC-004, regex hoàn hàng ở TC-013, `Bông hoa`/`Gấu bông` ở TC-006, `ancestor clickable` ở TC-005, `Bông hoa` ở TC-005 step 6; **1 là miss thật**: strategy `id` `gift-cell-flower`)
- Action calls (tap / set_value / swipe / back / scroll_to): **~62**
- `get_text` / `get_element_attribute`: **5**
- Evidence: **`adb exec-out screencap -p`** ×21 *(⛔ không dùng `appium_screenshot` — trả ~150k ký tự HTML viewer vào context)*
- ⚠️ **Sự cố trong run:**
  - 20:15 — dialog **"Không thể kết nối mạng!"** giả lúc mở app *(bẫy `T-ASN-07`)*; `ping 8.8.8.8` 0% loss. Đóng bằng `Đồng ý`, chạy tiếp bình thường.
  - 20:48 — bẫy `T-ASN-07` lặp lại ở `NHẬN MÃ OTP` khi đăng nhập `stag_giangdc2@`; **bấm lại lần 2 thì qua** (đúng cách xử lý đã ghi ở `USR-accounts.md §5`).
  - 20:22 — `appium_gesture(scroll, direction=up)` và `swipe(direction=down)` **báo success nhưng danh sách không cuộn**. Phải dùng **swipe toạ độ tường minh**. → đã ghi vào `vibe-locators.md`.
- MCP **không** mất kết nối lần nào trong suốt phiên.
