# MCP Session Log — VR-019 — 2026-09-22

## Session info

- Platform: mobile (Appium MCP), 2 thiết bị chạy song song
- Device A (sender/observer, vai A): `emulator-5554` — account `stag_giangdc2@fpt.com` (đã login sẵn từ đầu phiên)
- Device C→B→C (vai C rồi tạm B rồi về C): `R58T20PLP8K` — bắt đầu account `stag_taipm@fpt.com`
- Session ID (emulator-5554): `818e9b8a-c384-4272-990f-5c8a30044543`
- Session ID (R58T20PLP8K): `7efb5efb-7b9f-45ca-ad83-a32665d565dd`
- Created: 09:29–09:30
- Pre-flight: ✅ select_device ×2 + session create ×2 + get_page_source ×2 + get_window_size ×2 all OK

## Pre-flight (ghi từng call)

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| 1 | 09:28 | select_device | platform=android (discover) | OK — 2 devices | R58T20PLP8K, emulator-5554 |
| 2 | 09:28 | select_device | deviceUdid=emulator-5554 | OK | |
| 3 | 09:28 | appium_session_management | action=create, emulator-5554 | OK sid=818e9b8a… | |
| 4 | 09:29 | select_device | deviceUdid=R58T20PLP8K | OK | |
| 5 | 09:29 | appium_session_management | action=create, R58T20PLP8K | OK sid=7efb5efb… | |
| 6 | 09:29 | appium_get_window_size | sid=818e9b8a… | OK 1080x2400 | |
| 7 | 09:29 | appium_get_window_size | sid=7efb5efb… | OK 720x1600 | |
| 8 | 09:29 | appium_get_page_source | sid=818e9b8a… | OK (huge, not read) | pre-flight liveness only |
| 9 | 09:29 | appium_get_page_source | sid=7efb5efb… | OK (huge, not read) | pre-flight liveness only |

⚠️ **Đổi cách chụp ảnh evidence (giống VR-015/017/018):** `appium_screenshot` MCP trả base64 quá lớn,
vượt token limit context (~150k ký tự/ảnh full, vẫn ~66k ở `maxWidth=360`) → dùng
`adb exec-out screencap -p > <path>` thẳng vào `screenshots/` cho MỌI ảnh evidence của run này.
✅ Verify ảnh preflight tồn tại: `_setup__preflight-emulator-giangdc2.png` (108795 bytes) ·
`_setup__preflight-real-taipm.png` (72262 bytes). Locator vẫn lấy qua MCP `appium_find_element`/
`appium_get_page_source` — chỉ đổi kênh chụp ảnh, không đổi kênh capture locator.

## Pha A + Pha B — 1 dòng / TC (gộp)

> Không có Pha A snapshot riêng: locator dùng lại 100% từ `vibe-locators-latest.md` (wizard NEED,
> Bảng tin, Theo dõi đơn, `track-report-incident`, FoxPro login) — đã ✅ Verified từ các run trước
> (VR-002/003/004/012/015/017/018), tái verify bằng action thành công trong run này (tự động giữ ✅).

| TC / Hoạt động | Time | Calls | Chi tiết gộp | Snapshot? | Kết quả |
|----|------|------:|--------------|-----------|---------|
| Setup — post SEED-TS-01 (wizard NEED, device A) | 09:32–09:41 | ~28 | find×15, tap×13, set_value×3 (email/địa chỉ/ghi chú), scroll_to_element×5 | 0 | ✅ Đăng tin thành công |
| TC-TS-022 (3 checkpoint, xen kẽ B advance state) | 09:42–10:01 | ~10 | find×6, tap×2, adb screencap×3 | 0 | ✅ PASS |
| Setup B — logout C→login B (`stag_anhptm17@`) | 09:49–09:54 | ~16 | find×10, tap×6, adb input text×1 (OTP) | 0 | ✅ Login OK |
| B nhận đơn + Tôi đã lấy hàng (MATCHED→IN_TRANSIT) | 09:54–09:58 | ~9 | find×6, tap×5 | 0 | ✅ 2 chuyển trạng thái |
| TC-TS-023 (2 checkpoint) | 09:55–10:00 | ~4 | find×2, tap×2 | 0 | ✅ PASS |
| TC-TS-018 (đóng WebView) | 10:00 | ~2 | find×1, tap×1 | 0 | ✅ PASS |
| TC-TS-016 (mất mạng) | 10:02 | ~3 | adb svc wifi disable×1, tap×1, find (miss)×1 | 0 | ❌ FAIL (BUG-038) |
| TC-TS-017 (thử lại) | 10:02 | ~2 | adb svc wifi enable×1, find (miss)×1 | 0 | 🚫 BLOCKED |
| TC-TS-008/009/010/011/012/013/014/015/019/020/021 (form) | 09:42 (mở lần đầu) | 1 mở WebView dùng chung | tap×1 (đã mở từ TC-TS-008), quan sát | 0 | 🚫 BLOCKED ×11 (BUG-037, 1 lần mở WebView đủ chứng minh cho cả 11 TC) |
| Setup C — logout B→login C (`stag_taipm@`) | 10:03–10:11 | ~18 | find×11, tap×7, adb input text×1 (OTP); 1 lần timeout mạng thoáng qua (retry) | 0 | ✅ Login OK |
| TC-TS-024 | 10:11–10:12 | ~4 | find×3, tap×1 | 0 | 🚫 BLOCKED (partial PASS — nút hiện) |

## Statistics

- Total MCP calls: ~105 · Tổng snapshot trần: **0** · Số màn đã harvest (tái dùng từ locators-latest): 6 (Đăng tin mới, Wizard B1/B2/B3, Bảng tin, Chi tiết tin, Theo dõi đơn, FoxPro login/logout)
- find_element calls: ~65 (success: 63, NOT FOUND: 2 — cả 2 là `textContains("Thử lại")`, kết quả kiểm của `TC-TS-016/017`, không phải locator hỏng)
- Action calls (tap/set_value): ~38
- adb-only (lifecycle, không tính locator): `screencap` ×24 (evidence), `svc wifi disable/enable` ×2, `input text` ×2 (OTP)
- ⚠️ 1 lần timeout mạng thoáng qua khi vào FoxEco với tài khoản C lần 2 (~10:09) — tự khỏi sau ~6s, không phải lỗi locator

## 🆕 Follow-up 2026-09-22 — Retest 12 TC sau khi bypass màn login Microsoft

- Session mới: `select_device(android, R58T20PLP8K)` → `appium_session_management(create)` sid
  `abcd6937-0d8a-488e-b20b-242dd73fa746`, 10:57. Không tạo session thứ 2 (chỉ dùng 1 thiết bị thật,
  đã login sẵn `stag_taipm@` + tài khoản Microsoft thật của QC).
- **Giới hạn kỹ thuật phát hiện trong follow-up:** `appium_context(action=list)` chỉ trả
  `["NATIVE_APP"]` — không có context `WEBVIEW_*` nào cho nội dung Microsoft Forms (chạy trong
  Custom Tab tách biệt tiến trình, không phải WebView nhúng trong app). `appium_find_element` với
  `-android uiautomator` **query được một số text node** (nút "Gửi", "Hủy bỏ") nhưng **KHÔNG query
  được input field** (mô tả, SĐT) — chỉ tap qua toạ độ (x,y) đọc từ `adb exec-out screencap` mới
  tương tác được với các ô nhập liệu. Đây là **ngoại lệ hợp lệ** của MCP-MANDATORY (không có locator
  nào tồn tại để capture cho các ô này — không phải bỏ qua MCP một cách tuỳ tiện).
- Nhập text vào các ô: `adb shell input text` (không hỗ trợ dấu tiếng Việt — mọi chuỗi mô tả gõ
  không dấu, không ảnh hưởng hành vi validate/submit đang kiểm) sau khi `appium_gesture(tap, x, y)`
  focus đúng ô. Xoá text: `adb shell input keyevent 67` (backspace) lặp lại hoặc `keyevent 123`
  (MOVE_END) trước khi backspace.
- Ảnh test: 6 file JPG placeholder tự sinh (PIL, màu đơn sắc) → `adb push` vào `/sdcard/Pictures/`
  + `adb shell am broadcast -a android.intent.action.MEDIA_SCANNER_SCAN_FILE` để native file-picker
  nhận diện — chọn qua picker hệ thống Android (long_press + tap để multi-select), không qua MCP.
- 1 sự cố: `appium_mobile_press_key(BACK)` dùng để ẩn bàn phím lúc bàn phím đã tự ẩn từ trước ⇒ BACK
  lan xuống Custom Tab, đóng luôn WebView ngoài ý muốn (mất dữ liệu `TC-TS-009` đang điền dở — dùng
  làm tiền đề bất ngờ cho `TC-TS-019`). Từ đó dùng `appium_gesture(tap, x=560, y=1558)` (nút mũi tên
  ▽ của bàn phím) để dismiss keyboard an toàn hơn.
- Đổi tài khoản trong follow-up: đăng xuất C → đăng nhập B (`stag_anhptm17@`, OTP qua
  `adb shell input text "$FOXECO_STG_PASS"`) — full flow §0b của `USR-accounts.md`, ~14 call, 1 lần
  gặp toast "Kết nối quá thời gian chờ" + 1 overlay Wi-Fi hệ thống bật nhầm (dismiss bằng `BACK`),
  cả 2 tự khỏi khi thử lại, không phải lỗi locator.
- Tổng MCP calls follow-up: ~55 (find_element ~15, gesture tap/scroll ~30, session/context ~3,
  screenshot MCP: **0 lần dùng** — toàn bộ evidence qua `adb exec-out screencap`, đã xác nhận lại
  vấn đề base64 vượt token limit từ đầu phiên follow-up).
- Tổng snapshot trần: **0** (không gọi `appium_get_page_source` lần nào trong follow-up — dùng
  screenshot + tap toạ độ trực tiếp vì nội dung ngoài accessibility tree).
