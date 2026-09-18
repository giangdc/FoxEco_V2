# MCP Session Log — VR-001 — 2026-09-18

## Session info
- Platform: mobile (Appium MCP, UiAutomator2)
- Device: emulator-5554 (Pixel 7 AVD, `sdk_gphone64_x86_64`, 1080x2400)
- Session ID: `438ded8f-5192-436f-b3c5-03755ef57743`
- Created: 10:25
- Host app: `com.hrisproject.stag` / `com.hrisproject.MainActivity` (FoxPro/HRIS — FoxEco chạy trong app này)
  ⚠️ **Đính chính:** `04_test-data/valid/USR-accounts.md §0` ghi package `vn.fpt.ftel.sop.stg`; package THẬT trên STG emulator là **`com.hrisproject.stag`**.
- Tài khoản đang đăng nhập: **A** — "Đặng Châu Giang", MNV `00131946`, Ban Giám đốc (khớp `FOXECO_STG_USER_A`)
- Pre-flight: ✅ select_device + session create + get_page_source + get_window_size — 4/4 OK

> 🧾 **Evidence chụp bằng `adb exec-out screencap`, KHÔNG bằng `appium_screenshot`.**
> Lý do cơ học: `appium_screenshot` của MCP này trả **inline HTML viewer ~428.000 ký tự/call**
> (không có tham số `filename`), tức ~1 lần chụp = vượt ngân sách cả lô TC. `adb screencap`
> ghi thẳng vào `screenshots/` với đường dẫn tuyệt đối, đúng §"Contract đường dẫn ảnh".
> Skill cho phép tường minh: *"adb screencap → snapshot file (evidence, NOT locator source)"*.
> ⛔ Locator thì **tuyệt đối không** qua ADB — 100% qua `appium_find_element` / `appium_get_page_source`.

> 📄 **Page source cũng vượt ngưỡng inline** ⇒ MCP tự lưu ra file tool-result; đây chính là
> pattern L3 *"tree ra FILE, response chỉ còn 1 link"*. Locator vẫn là chuỗi MCP trả về nguyên văn.

## Pre-flight + Pha A (ghi từng call)

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| 1 | 10:24 | select_device | platform=android | OK emulator-5554 | Pre-flight |
| 2 | 10:25 | appium_session_management | action=create, noReset=true, autoLaunch=false | OK sid=438ded8f | Pre-flight — `autoLaunch=false` để **giữ nguyên phiên đăng nhập OTP** của người chạy |
| 3 | 10:25 | appium_get_window_size | — | 1080x2400 | Pre-flight |
| A1 | 10:25 | appium_get_page_source | màn **Trang chủ** | OK 105.278 bytes | **Pha A** — 9 element vào map (bottom nav ×5 + hero) |
| A2 | 10:26 | appium_find_element | accessibility id `Cá nhân` | OK | Pha A — điều hướng |
| A3 | 10:26 | appium_gesture | tap `Cá nhân` | OK | Pha A |
| A4 | 10:26 | appium_get_page_source | màn **Cá nhân** | OK 203.531 bytes | **Pha A** — 8 element vào map |
| A5 | 10:26 | appium_find_element | accessibility id `profile-menu-editProfile` | OK | Pha A |
| A6 | 10:26 | appium_gesture | tap `profile-menu-editProfile` | OK | Pha A |
| A7 | 10:26 | appium_get_page_source | màn **Cập nhật thông tin** | OK 136.995 bytes | **Pha A** — 7 element vào map; 2 EditText `showing-hint="true"` ⇒ **rỗng** |

**Số màn đã harvest ở Pha A: 3** (Trang chủ · Cá nhân · Cập nhật thông tin)

## Pha B — 1 DÒNG / TC

| TC | Time | Calls | Chi tiết gộp | Snapshot? | Kết quả |
|----|------|------:|--------------|-----------|---------|
| TC-USR-001 | 10:31 | 6 | find×3 (`FoxEco`, `Cá nhân`, `MNV:`), gesture tap×2, get_text×1 | 0 (dùng locator_map) | ✅ PASS |
| TC-USR-002 | 10:33 | 8 | find×5 (2 nav + `ĐC` + `MNV:` + `@fpt.com`🚫), tap×2, get_text×1 | 0 | ❌ FAIL step 3 |
| TC-USR-003 | 10:35 | 8 | tap×3 (coord: avatar/tên/dòng MNV), keyboard is_shown×1, find×3 (`EditText`🚫, `MNV:`), get_text×1 | 0 | ✅ PASS |
| TC-USR-004 | 10:36 | 4 | find×2 + tap×2 (điều hướng vào màn độc lập) | 0 | ✅ PASS |
| TC-USR-007 | 10:37 | 8 | find×4 nav/tap, find×4 absence (`Điểm`🚫 `ECO`🚫 `uy tín`🚫 `CO`🚫) | 0 | ✅ PASS |
| TC-USR-008 | 10:38 | 6 | find×2+tap×2 nav, find×2 absence (`Hạng`🚫 `Đồng hành`🚫) | 0 | ✅ PASS |
| TC-USR-009 | 10:41 | 7 | find×2+tap×2, find `profile-menu-activity`+tap, **get_page_source×1** (màn mới) | **1** (L2a: màn Đơn của tôi lần đầu) | ✅ PASS |
| TC-USR-010 | 10:42 | 5 | find/tap `Cá nhân`, find/tap `profile-menu-gifts`, find `text("Quà đã nhận")` | 0 | ✅ PASS |
| TC-USR-011 | 10:43 | 4 | find/tap `profile-menu-editProfile`, find `Số điện thoại mặc định` | 0 | ❌ FAIL step 3 |
| TC-USR-012 | 10:39 | 4 | find×2+tap×2 nav (dùng bounds từ page source Pha A) | 0 | ✅ PASS |
| TC-USR-013 | 10:40 | 7 | find×2+tap×2 nav, find `textStartsWith`+get_text, find `text("Cập nhật thông tin")`🚫 | 0 | ❌ FAIL step 3 |
| TC-USR-014 | 10:44 | 4 | find `Bảng tin`🚫, find `text("Cập nhật thông tin")`, find/tap editProfile | 0 | ✅ PASS |
| TC-USR-024 | 10:45 | 7 | tap×4 (coord: avatar/tên/MNV/email), keyboard is_shown, **get_page_source×1** (đối chiếu cây trước/sau) | **1** (L2c: xác nhận không có popup/EditText mới) | ❌ FAIL step 8 |
| TC-USR-017 | 10:49 | 4 | find/tap `Lưu thay đổi`, **get_page_source×1** (đọc chuỗi lỗi) | **1** (L2c: DOM đổi sau submit) | ❌ FAIL step 5 |
| TC-USR-018 | 10:51 | 7 | find/tap nav×2, find SĐT+set_value, find/tap Lưu, **get_page_source×1** | **1** | ❌ FAIL step 5 |
| TC-USR-019 | 10:55 | 9 | find SĐT+set_value+get_text, find/tap Lưu, find/tap Quay lại, find/tap editProfile, **get_page_source×1** | **1** | ✅ PASS |
| TC-USR-020 | 10:52 | 7 | như 018 | **1** | ❌ FAIL step 5 |
| TC-USR-021 | 10:53 | 13 | 2 lượt xác minh: set_value×2, tap Lưu×2, **get_page_source×3** (2 lượt + 1 kiểm persist) | **3** (L2b: kết luận nặng ⇒ xác minh lại) | ❌ FAIL step 5 |
| TC-USR-022 | 10:54 | 10 | set_value, tap Lưu, **get_page_source×2** (sau submit + kiểm persist) | **2** | ❌ FAIL step 5 |
| TC-USR-023 | 10:56 | 6 | find SĐT+set_value+get_text, find/tap Lưu, **get_page_source×1** | **1** | ❌ FAIL step 5 |
| TC-USR-031 | 10:58 | 3 | find địa chỉ+set_value, **get_page_source×1** | **1** | ✅ PASS |
| TC-USR-032 | 10:58 | 3 | set_value `fpt`, **get_page_source×1** (đếm 9 gợi ý) | **1** | 🚫 BLOCKED step 5 |
| TC-USR-033 | 11:02 | 6 | set_value, find/tap `address-suggestion-0`, tap vùng trống, **get_page_source×1** | **1** | ✅ PASS |
| TC-USR-034 | 10:59 | 2 | set_value `Cẩm Lệ`, **get_page_source×1** | **1** | 🚫 BLOCKED step 5 |
| TC-USR-035 | 11:00 | 2 | set_value `cam le`, **get_page_source×1** | **1** | 🚫 BLOCKED step 5 |
| TC-USR-036 | 11:00 | 2 | set_value `CAM LE`, **get_page_source×1** | **1** | 🚫 BLOCKED step 5 |
| TC-USR-037 | 11:01 | 2 | set_value `tan`, **get_page_source×1** (11 gợi ý) | **1** | 🚫 BLOCKED step 5 |
| TC-USR-038 | 11:01 | 2 | set_value `xyz`, **get_page_source×1** | **1** | ✅ PASS |
| TC-USR-039 | 11:01 | 2 | set_value `hcm`, **get_page_source×1** (12 gợi ý) | **1** | ❌ FAIL step 5 |
| TC-USR-015 | 11:15 | 10 | find/tap editProfile, **get_page_source×1** (ghi baseline), set_value×2, tap suggestion, tap Lưu, + **burst 60 frame adb** soi banner | **1** | ❌ FAIL step 8 |
| TC-USR-016 | 11:16 | 3 | find/tap editProfile, **get_page_source×1** (kiểm persist) | **1** | ✅ PASS |
| TC-USR-027 | 11:19 | 6 | find/tap editProfile, find SĐT+set_value, find/tap Lưu, find `textContains("Đã lưu")`🚫 | 0 | 🚫 BLOCKED step 6 |
| TC-USR-028 | 11:21 | 9 | find/tap editProfile, find địa chỉ+set_value, find `address-suggestion-0`🚫, tap vùng trống×2, **get_page_source×1**, keyboard is_shown, get_text | **1** | ❌ FAIL step 6 |
| TC-USR-029 | 11:23 | 7 | find/tap Lưu, find/tap editProfile, **get_page_source×1**, set_value, tap vùng trống, find `textContains("Đã lưu")`🚫 | **1** | ❌ FAIL step 7 |
| TC-USR-030 | 11:23 | 3 | find/tap editProfile, **get_page_source×1** | **1** | ❌ FAIL step 10 |
| TC-USR-042 | 11:30 | 12 | set_value+tap suggestion+tap Lưu, gesture back×2, find/tap `FoxEco`, find/tap `Cá nhân`, find/tap editProfile, **get_page_source×1** | **1** | ✅ PASS |
| TC-USR-045 | 11:26 | 8 | find/tap editProfile, set_value `Cẩm Lệ`, find/tap `address-suggestion-1`, find/tap `Quay lại`, **get_page_source×1** (quét dialog) | **1** | ✅ PASS |
| TC-USR-046 | 11:28 | 3 | find/tap editProfile, **get_page_source×1** | **1** | ✅ PASS |
| TC-USR-025 | 11:41–11:58 | 48 | **wizard 3 bước + đăng tin + đổi hồ sơ + mở lại đơn**: find/tap×28 (chips, ảnh, picker, buổi, điều khoản, Đăng tin ngay, Theo dõi đơn, Chỉnh sửa, Huỷ chỉnh sửa), set_value×4, gesture scroll×3 + back×3, **get_page_source×10** | **10** (6 màn wizard/đơn lần đầu + 4 lần L2c sau khi đổi state) | ✅ PASS |
| TC-USR-026 | 12:00–12:10 | 34 | wizard lần 2 (đã có locator_map): find/tap×22, set_value×5, scroll_to_element×2, **get_page_source×4** | **4** | ✅ PASS |

## Statistics

- **Total MCP calls: ~330** · **Tổng snapshot (`get_page_source`): 58** · **Số màn đã harvest: 9**
  ⚠️ **S(58) > M_screen(9)** — lệch có chủ đích, KHÔNG phải vi phạm B1/B2. Lý do cụ thể:
  · **34 snapshot là ĐỌC KẾT QUẢ, không phải harvest locator** — toàn bộ lô 2 + lô 3 assert **nội dung động**
    (chuỗi thông báo lỗi · số lượng + tên gợi ý văn phòng · giá trị field sau persist). Appium **không có**
    `target=`/`depth=`/`filename=` như Playwright ⇒ không thu hẹp được, buộc phải lấy cả cây (L3 mobile).
  · **14 snapshot ở lô 4** do wizard 3 bước × 2 lần + màn Theo dõi đơn + mode edit = **6 màn mới**.
  · MCP tự ghi mỗi page source **ra file tool-result** (vượt ngưỡng inline) ⇒ chi phí context thực tế
    chỉ là 1 dòng link/call, đúng tinh thần L3 *"tree ra FILE"*.
- find_element calls: ~150 (success ~136 · **NOT FOUND 14** — 10 ca assert-absent đúng kỳ vọng + 4 ca T2/bug)
- Action calls (tap/set_value/scroll/back/keyboard): ~120
- ⚠️ **Failures/quirks gặp giữa run** (không làm mất session):
  · 11:39 `adb exec-out screencap` trả 0 byte — **thiết bị thứ 2 (`5e740e65`) cắm vào giữa phiên** ⇒ `adb` báo *"more than one device"*. Đã cố định `adb -s emulator-5554` cho mọi lệnh sau đó.
  · `appium_get_element_attribute` không nhận `showing-hint`/`showingHintText` (xem `vibe-locators.md` §T3).
  · 12:03 Google Photos backup promo che photo picker ⇒ `gesture back` để bỏ qua.
- Session giữ nguyên từ 10:25 → 12:10, **không mất kết nối lần nào**.
