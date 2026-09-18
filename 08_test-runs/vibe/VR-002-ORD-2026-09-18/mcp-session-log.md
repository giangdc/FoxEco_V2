# MCP Session Log — VR-002 — 2026-09-18

## Session info
- Platform: mobile (Appium MCP, UiAutomator2)
- Device: emulator-5554 (`sdk_gphone64_x86_64`, 1080x2400)
- Session ID: `9eccccc1-c791-4f0b-a0b0-739aae23eac7`
- Created: 12:28
- Host app: `com.hrisproject.stag` / `com.hrisproject.MainActivity` (FoxPro/HRIS — FoxEco chạy trong app này)
- Tài khoản đang đăng nhập: **A** — "Đặng Châu Giang", MNV `00131946` (phiên OTP do người chạy mở, giữ nguyên bằng `autoLaunch=false`)
- Pre-flight: ✅ select_device + session create + get_window_size + get_page_source (Pha A) — OK

> 🧾 Evidence bằng `adb exec-out screencap` (lý do cơ học: `appium_screenshot` trả inline HTML
> ~428k ký tự/call, không có tham số `filename`). Locator thì 100% qua MCP.
> 📄 Page source > ngưỡng inline ⇒ MCP tự ghi ra file tool-result (đúng pattern L3).

## Pre-flight + Pha A (ghi từng call)

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| 1 | 12:28 | select_device | platform=android, udid=emulator-5554 | OK emulator-5554 | Pre-flight |
| 2 | 12:28 | appium_session_management | action=create, noReset=true, autoLaunch=false | OK sid=9eccccc1 | Pre-flight — giữ phiên đăng nhập OTP |
| 3 | 12:28 | appium_get_window_size | — | 1080x2400 | Pre-flight |
| A1 | 12:31 | appium_find_element ×4 + get_text ×1 | màn **Đăng tin mới**: `text("Bạn muốn làm gì?")`, `descriptionStartsWith("Tôi cần gửi hàng")`, `("Tôi nhận giao hàng")`, `textContains("không thu phí")` | OK 4/4 | **Pha A** — 4 element vào map (không cần page source) |
| A2 | 12:33 | appium_get_page_source | màn **Wizard Bước 1/3** (sau khi tap card NEED) | OK **204.867 ký tự** → file tool-result (L3) | **Pha A** — 30 element vào map: 8 chip loại hàng + ghi chú + 9 chip tier + nút Tiếp theo + khối ảnh |
| A3 | 12:45 | appium_get_page_source | **Android Photo Picker** (OS) | OK **166.093 ký tự** → file tool-result (L3) | **Pha A** — 4 element: `icon_thumbnail` ×10 (dùng `.instance(N)`), `Add`, tab Photos/Albums, Cancel |
| A4 | 12:56 | appium_get_page_source | Wizard B1 — **khối ảnh khi có 2 ảnh** | OK 223.727 ký tự | L2(b) — tìm locator nút xoá ảnh: `multi-photo-remove-0/1` + `multi-photo-add-button` |
| A5 | 13:02 | appium_get_page_source | Wizard B1 — **khối ảnh khi có 4 ảnh** | OK 232.993 ký tự | L2(b) — xác nhận `multi-photo-remove-3` + add-button **KHÔNG render** (bug T10) |

**Số màn đã harvest ở Pha A + L2(b): 5** (Đăng tin mới · Wizard B1 · Bottom sheet ảnh · Photo Picker · Wizard B2 — B2 dùng lại map VR-001, chỉ bổ sung bằng `find_element`)

## Pha B — 1 DÒNG / TC (gộp)

| TC | Time | Calls | Chi tiết gộp | Snapshot? | Kết quả |
|----|------|------:|--------------|-----------|---------|
| TC-ORD-001 | 12:31 | 7 | find×4 (4 thành phần) + get_text×1 + tap card NEED + find `Bước 1 / 3` | 0 | ⏳ chạy dở (step 5 còn nợ) |
| TC-ORD-002 | 12:34 | 2 | find `Bước 1 / 3` + `Thông tin hàng` | 0 *(dùng A2)* | ✅ PASS |
| TC-ORD-005 | 12:34 | 1 | đọc 8 chip từ page source A2 + ảnh xác nhận chip đang chọn | 0 | ✅ PASS |
| TC-ORD-006 | 12:35 | 2 | find `accessibility id "Tài liệu"` (FOUND) + scroll | 0 | ❌ FAIL step 3 |
| TC-ORD-007 | 12:42 | 6 | find/tap `Tài liệu`, find/tap `Thấp`, find/tap `Tiếp theo`, find `Bước 1 / 3` | 0 | ❌ FAIL step 5 |
| TC-ORD-008 | 12:39 | 7 | find `Tiếp theo` + get_attr `enabled`×2, tap×2, find/tap `Thấp`, find `Bước 1 / 3` | 0 | ❌ FAIL step 6 |
| TC-ORD-009 | 12:40 | 4 | find/tap `Cao, Trên 5`, find `textContains("giá trị cao")` + get_text | 0 | ✅ PASS |
| TC-ORD-010 | 12:40 | 4 | find `textContains("giá trị cao")`🚫, find/tap `Vừa, 1`, find `textContains("thoả thuận")`🚫 | 0 | ✅ PASS |
| TC-ORD-013 | 12:36 | 5 | find `textStartsWith("Bắt buộc ít nhất 1 ảnh")`+get_text, find `text("0/5")`, find `textStartsWith("ẢNH HÀNG")`+get_text | 0 | ✅ PASS |
| TC-ORD-054 | 12:43 | 4 | find `EditText instance(1)`🚫 ×2 (trước/sau khi chọn "Cao"), find/tap `Cao` | 0 | ✅ PASS |
| TC-ORD-069 | 12:45 | 5 | scroll_to_element, find/tap `descriptionContains("0/5")`, get_attr content-desc, find/tap `Chọn từ thư viện` | **1** (A3) | 🚫 BLOCKED step 2 |
| TC-ORD-068 | 12:50 | 8 | find/tap thumbnail `.instance(7)`, find/tap `Add`, *(F2: qua tab Chức năng)*, scroll_to_element `textContains("5MB")`, find+get_text, find `accessibility id "0/5"` | 0 | ✅ PASS |
| TC-ORD-012 | 12:54 | 7 | find/tap add-button, find/tap `Chọn từ thư viện`, find/tap thumbnail `.instance(0)`, find/tap `Add`, find `accessibility id "1/5"` | 0 | ✅ PASS |
| TC-ORD-087 | 12:58 | 9 | thêm ảnh 2 (5 call), **get_page_source×1** tìm nút xoá, find/tap `resourceId("multi-photo-remove-0")`, find `"1/5"` | **1** (A4) | ✅ PASS |
| TC-ORD-070 | 13:02 | 18 | thêm ảnh ×3 (15 call), find add-button🚫, swipe/scroll ngang ×3, **get_page_source×1** | **1** (A5) | 🚫 BLOCKED step 2–3 |
| TC-ORD-071 | 13:04 | 1 | find `resourceId("multi-photo-remove-3")`🚫 | 0 | 🚫 BLOCKED step 2 |
| TC-ORD-027 | 13:06 | 8 | find/tap `Dưới 5 kg`, scroll+find/tap `Nhỏ`, get_attr `enabled`=true, tap `Tiếp theo`, find `(//EditText)[3]`+get_text, set_value, get_text | 0 | ✅ PASS |
| TC-ORD-074 | 13:12 | 9 | find/set_value email, hideKeyboard, find `receiver-name-input`+set_value+get_text, đọc 3 ô qua ảnh | 0 | ❌ FAIL step 5 |
| TC-ORD-075 | 13:18 | 9 | set_value email (không tồn tại), hideKeyboard, find `Tiếp theo`+get_attr×3 (loại nhiễu: điền địa chỉ giao + chọn buổi rồi đọc lại), find/set_value địa chỉ giao, find/tap `Giờ nào cũng được` | 0 | ✅ PASS |
| TC-ORD-076 | 13:20 | 4 | set_value email nghỉ việc, hideKeyboard, get_attr `enabled`=false | 0 | ✅ PASS |
| TC-ORD-028 | 13:22 | 4 | set_value `Số 7 ngõ 12 Trần Duy Hưng`, find `address-suggestion-0`🚫, get_text | 0 | ✅ PASS |
| TC-ORD-055 | 13:24 | 4 | set_value 200 ký tự + get_text, set_value `w3cActions` 1 ký tự + get_text | 0 | ✅ PASS |
| TC-ORD-083 | 13:28 | 9 | set_value email hợp lệ + 2 ô địa chỉ trùng nhau, hideKeyboard, get_attr `enabled`, tap `Tiếp theo`, find `textContains("trùng")`🚫, find `Bước 2 / 3` | 0 | ❌ FAIL step 5 |
| TC-ORD-084 | 13:30 | 4 | set_value chuỗi có khoảng trắng đầu/cuối, hideKeyboard, get_attr `enabled`, get_text | 0 | ❌ FAIL step 5 |
| TC-ORD-053 | 13:33 | 6 | set_value `Số 9 Duy Tân`, hideKeyboard, find/tap `Quay lại` ×2 (bước 2 → bước 1 → thoát), find `textContains("Thoát")`🚫 | 0 | ❌ FAIL step 4 |
| TC-ORD-062 | 13:36 | 9 | gesture back, find/tap `Hoạt động`, find `textContains("háp")`🚫, find/tap `Đã hoàn thành`, find `textContains("háp")`🚫, find/tap `Đăng tin`, find/tap card NEED | 0 | ✅ PASS |
| TC-ORD-063 | 13:40 | 9 | find/tap 3 chip (`Thấp`/`Dưới 5 kg`/`Nhỏ`), find `Tiếp theo`+get_attr, tap, scroll_to_element khối ảnh, đọc khối ảnh (không có lỗi) | 0 | ❌ FAIL step 6 (P1) |
| TC-ORD-014 | 13:42 | 1 | dùng lại state của TC-ORD-063 + 1 ảnh chụp | 0 | ❌ FAIL step 4 |
| TC-ORD-064 | 13:47 | 13 | thoát+vào lại wizard (3), tap `Thấp`+`Nhỏ` (4), thêm 1 ảnh (5), get_attr `enabled`, tap `Tiếp theo` | 0 | ❌ FAIL step 6 |
| TC-ORD-066 | 13:50 | 13 | thoát+vào lại wizard, tap `Thấp`+`Dưới 5 kg`, thêm 1 ảnh, get_attr, tap `Tiếp theo` | 0 | ❌ FAIL step 5 |
| TC-ORD-011 | 13:53 | 8 | find `EditText`+set_value 300 ký tự+get_text, tap `Nhỏ`, tap `Tiếp theo`, tap `Quay lại`, get_text, set_value `w3cActions`+get_text | 0 | ✅ PASS |
| TC-ORD-058 | 13:52 | 2 | scroll_to_element `BUỔI MONG MUỐN` + đọc trạng thái 4 chip (ảnh) | 0 | ❌ FAIL step 2 |
| TC-ORD-059 | 13:44 | 3 | find `descriptionStartsWith("Sáng")` + get_attr `enabled`=true + tap | 0 | ❌ FAIL step 4 |
| TC-ORD-030 | 13:46 | 3 | find/tap `Từ ngày`, find/tap `text("17")` | 0 | ✅ PASS |
| TC-ORD-056 | 13:48 | 4 | find/tap `Đóng`, find/tap `Đến ngày`, find/tap `text("25")` | 0 | ✅ PASS |
| TC-ORD-057 | 13:49 | 5 | find/tap `Đến ngày`, find/tap `text("26")`, find `textContains("5MB")`… → get_text lỗi khoảng ngày | 0 | ✅ PASS |
| TC-ORD-031 | 13:50 | 6 | tap `Từ ngày`, tap `text("21")`, tap `Đến ngày`, tap `text("19")`, tap `Đóng` | 0 | ✅ PASS |
| TC-ORD-077 | 13:52 | 5 | find/set_value email sai định dạng, hideKeyboard, find `textContains("mail")`🚫, scroll_to_element | 0 | ❌ FAIL step 4 |
| TC-ORD-078 | 13:54 | 3 | set_value `nguyenvana@gmail.com`, hideKeyboard, đọc dòng lỗi + 3 ô (ảnh) | 0 | ✅ PASS |
| TC-ORD-015 | 13:58 | 14 | dựng lại wizard đầy đủ (12 call: vào wizard + 3 chip + 1 ảnh + Tiếp theo), find `(//EditText)[1]`+get_text, find `(//EditText)[2]`+get_text | 0 | ✅ PASS |
| TC-ORD-016 | 13:59 | 3 | tap `(//EditText)[1]`, `isKeyboardShown`=false, get_text | 0 | ✅ PASS |
| TC-ORD-017 | 14:00 | 1 | đọc `(//EditText)[3]` (đã get_text ở TC-ORD-027) + ảnh | 0 | ✅ PASS |
| TC-ORD-018 | 14:02 | 8 | set_value email, set_value địa chỉ giao, scroll_to_element+tap `Chiều`, scroll_to_element `NGƯỜI GỬI`, find+get_text SĐT | 0 | ✅ PASS |

Cột `Snapshot?` là **đồng hồ đo chi phí**: tổng **4 snapshot** / **5 màn harvest** ⇒ **S ≈ M_screen** ✅ đúng luật B1/B2 (⛔ không snapshot lại màn đã biết; Wizard B2 dùng lại map VR-001 với **0 snapshot**).

## ⚠️ Sự cố MCP giữa run

| Time | Sự cố | Xử lý | Ảnh hưởng |
|---|---|---|---|
| ~13:45 | `appium_find_element` trả lỗi *"instrumentation process is not running (probably crashed)"* (UiAutomator2 server chết) | tạo lại session: `appium_session_management(action=create, noReset=true, autoLaunch=false, forceAppLaunch=false)` → sid `f9edaf66-4137-44ee-ad4f-5a623f2a1a1a` | **0 TC bị mất**: app giữ nguyên state (vẫn ở Bước 2/3), chạy tiếp ngay từ `TC-ORD-059`. Element UUID cũ hết hiệu lực ⇒ phải `find_element` lại (đã làm) |

## Statistics
- Total MCP calls (ước lượng gộp): **~265** · Tổng snapshot (`get_page_source`): **4** · Số màn đã harvest: **5** ← **S ≈ M_screen** ✅
- `appium_find_element`: ~150 (success ~137 · **NOT FOUND 13** — trong đó 8 ca *assert-absent đúng kỳ vọng*, 5 ca *phát hiện bug/bẫy*)
- Action calls (`gesture tap` / `set_value` / `scroll*` / `keyboard`): ~95
- `get_element_attribute`: 14 (chủ yếu `enabled` của nút `Tiếp theo` — bẫy T4)
- Session: 2 (1 tạo đầu phiên + 1 tạo lại sau khi UiAutomator2 crash)
- Evidence: **52 ảnh** chụp bằng `adb exec-out screencap` (⛔ không dùng `appium_screenshot` — xem ghi chú đầu file)
