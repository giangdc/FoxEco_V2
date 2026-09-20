# MCP Session Log — VR-004 — 2026-09-18

## Session info
- Platform: mobile (Appium MCP, UiAutomator2)
- Device: emulator-5554 (`sdk_gphone64_x86_64`, Android 13 / API 33, 720x1280)
- Session ID: `a0de9221-7d08-4c2a-a491-29a0c59b3a3b`
- Created: 23:32
- Host app: `com.hrisproject.stag` / `com.hrisproject.MainActivity`
- Tài khoản đang đăng nhập: **A** — "Đặng Châu Giang", MNV `00131946`
- Pre-flight: ✅ select_device + session create + get_window_size + evidence-path check — OK

> 🧾 Evidence bằng `adb exec-out screencap` (`appium_screenshot` trả ~147k ký tự HTML viewer mỗi call, không có tham số `filename`). Locator thì 100% qua MCP.

## Pre-flight + Pha A (ghi từng call)

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| 1 | 23:32 | select_device | platform=android | OK emulator-5554 | Pre-flight |
| 2 | 23:32 | appium_session_management | action=create, udid=emulator-5554 | OK sid=a0de9221 | Pre-flight |
| 3 | 23:41 | appium_mobile_device_info | action=info | OK Android 13, 720x1280 | Pre-flight |
| 4 | 23:42 | appium_get_window_size | — | 720x1280 | Pre-flight |
| 5 | 23:42 | appium_screenshot | maxWidth=720 | OK → `/tmp/screenshot_*.png` (+147k ký tự HTML) | Evidence-path pre-flight → `_setup__preflight-launch.png`; từ đây dùng adb screencap |
| 6 | 23:46 | appium_find_element ×4 + get_text ×1 | màn **Đăng tin mới**: `text("Bạn muốn làm gì?")`, 2 card, banner `textContains("không thu phí")` | OK 4/4 | **Pha A** — 4 element (dùng lại map VR-002, re-verify) |
| A1 | 00:07 | appium_get_page_source | **Form OFFER** *(màn MỚI)* | OK **151.633** ký tự → file tool-result (L3) | **Pha A** — 7 element vào map |
| A2 | 00:10 | appium_get_page_source | **Wizard Bước 1/3** — nửa trên | OK **159.767** ký tự | **Pha A** — chip LOẠI HÀNG ×8 + GHI CHÚ + 3 chip GIÁ TRỊ |
| A3 | 00:14 | appium_get_page_source | **Wizard Bước 1/3** — nửa dưới *(sau scroll)* | OK **186.315** ký tự | **Pha A** — 3 chip TRỌNG LƯỢNG + 3 KÍCH THƯỚC + khối ẢNH HÀNG |
| A4 | 00:27 | appium_get_page_source | **Wizard Bước 2/3** — nửa dưới | OK **162.829** ký tự | **Pha A** — ngày/buổi + nút uỷ quyền |
| A5 | 00:30 | appium_get_page_source | **Wizard Bước 2/3** — vùng người gửi/người nhận | OK **183.249** ký tự | L2(b) — soi thuộc tính từng ô khi khoanh vùng bug T11 |
| A6 | 00:35 | appium_get_page_source | **Wizard Bước 3/3** *(màn MỚI — VR-002 chưa từng tới)* | OK **205.223** ký tự | **Pha A** — 8 element vào map |
| A7 | 00:44 | appium_get_page_source | **Form OFFER** — nửa dưới | OK **153.105** ký tự | **Pha A** — điểm đến + 4 chip `offer-day-part-*` + checkbox |
| A8 | 01:13 | appium_get_page_source | **Khối NGƯỜI NHẬN UỶ QUYỀN** *(mới mở)* | OK **186.819** ký tự | **Pha A** — 5 element `alt-receiver-*` |
| A9 | 01:20 | appium_get_page_source | **Màn Theo dõi đơn** *(chi tiết đơn)* | OK **229.409** ký tự | **Pha A** — 6 element `track-*` + 2 icon Copy |

> ⚠️ **Vì sao 9 dump cho 5 màn (không phải 1 dump/màn):** 3 màn dài nhất (Bước 1/3 · Bước 2/3 · Form OFFER) render **lazy** — chỉ node **trong viewport** được compose, nên **1 dump không bao giờ phủ hết màn**. Phải dump 2–3 lần theo vị trí cuộn. Đây là **lý do cơ học**, không phải vi phạm B1/B3.

## Pha B — 1 DÒNG / TC (gộp)

| TC | Time | Calls | Chi tiết gộp | Snapshot? | Kết quả |
|----|------|------:|--------------|-----------|---------|
| TC-ORD-001 | 23:46 | 11 | find×6, get_text×1, tap×4 (Đăng tin → card NEED → Quay lại → card OFFER) | 0 | ✅ PASS |
| TC-ORD-002 | 23:47 | 2 | find `Bước 1 / 3` + `Thông tin hàng` | 0 | ✅ PASS |
| TC-ORD-003 | 00:07 | 2 | find `textContains("Bước")` → NOT FOUND | **1** *(A1 — màn mới)* | ✅ PASS |
| TC-ORD-005 | 00:10 | 1 | đọc 8 chip + thứ tự từ A2 | **1** *(A2)* | ✅ PASS |
| TC-ORD-006 | 00:11 | 1 | find `accessibility id "Tài liệu"` → FOUND | 0 | ❌ FAIL step 3 |
| TC-ORD-008 | 00:11 | 6 | find `Tiếp theo`, get_attr `enabled`×2, tap×2, find/tap `Thấp` | 0 | ❌ FAIL step 6 |
| TC-ORD-010 | 00:12 | 6 | find/tap `Thấp`+`Vừa`, find `textContains("giá trị cao")`×2 → NOT FOUND | 0 | ✅ PASS *(chạy 2 lượt — lượt 1 loại bỏ do T8)* |
| TC-ORD-009 | 00:13 | 5 | find/tap `Cao`, find → NOT FOUND, scroll_to_element, find → FOUND, get_text | 0 | ✅ PASS |
| TC-ORD-054 | 00:14 | 5 | scroll_to_element×2, find/tap `value-tier-chip-option-high`, find `class EditText` → NOT FOUND | **1** *(A3)* | ✅ PASS |
| TC-ORD-013 | 00:15 | 4 | find `textStartsWith("Bắt buộc")` → NOT FOUND → scroll_to_element → FOUND → get_text | 0 *(dùng A3)* | ✅ PASS |
| TC-ORD-007 | 00:17 | 7 | scroll_to_element, find/tap `Tài liệu`, find/tap `low`, find/tap `Tiếp theo`, find `Bước 1 / 3` | 0 | ❌ FAIL step 5 |
| TC-ORD-011 | 00:19 | 8 | find `class EditText`, set_value 300 ký tự, get_text×2, set_value w3cActions, find/tap nhãn, find/tap `Tiếp theo` | 0 | ❌ FAIL step 4 *(biên 300/301 PASS)* |
| TC-ORD-014 | 00:20 | 4 | tap `Tiếp theo`, find `textContains("ảnh")`, scroll_to_element khối ảnh | 0 | ❌ FAIL step 4 |
| TC-ORD-012 | 00:21 | 8 | find/tap `multi-photo-add-button`, tap `Chọn từ thư viện`, tap `icon_thumbnail.instance(6)`, tap `Add`, find `accessibility id "1/5"` | 0 | ✅ PASS |
| TC-ORD-004 | 00:22–00:35 | **~45** | ⭐ TC đắt nhất phiên: 3 chip + ảnh + 2 lần `Tiếp theo`, set_value email/2 địa chỉ, **~20 call khoanh vùng bug T11** (thử blur, thử đổi ngày, thử dropdown), tap `Đăng tin ngay` ×3, `adb logcat` | **2** *(A5, A6)* | ❌ **FAIL step 11 — P1 BLOCKER** |
| TC-ORD-034 | 00:36 | 1 | đọc tóm tắt từ A6 | 0 *(A6)* | ✅ PASS |
| TC-ORD-035 | 00:36 | 1 | đọc banner hàng cấm từ A6 + ảnh | 0 | ✅ PASS |
| TC-ORD-036 | 00:36 | 0 | đọc trạng thái checkbox **bằng ảnh** (T1) | 0 | ✅ PASS |
| TC-ORD-037 | 00:37 | 6 | find/tap `Đăng tin ngay`, find `Bước 3 / 3`, find/tap checkbox, get_attr `enabled`×2 | 0 | ✅ **PASS (P1)** |
| TC-ORD-050 | 00:38–00:46 | 16 | back×3, tap `Đăng tin`, tap card OFFER, get_attr `enabled`×2, tap submit, set_value điểm đến + tap gợi ý, tap checkbox | **1** *(A7)* | ❌ FAIL step 8 |
| TC-ORD-042 | 00:47 | 3 | find tiêu đề + đối chiếu 7 nhóm trường từ A1+A7 | 0 | ✅ PASS |
| TC-ORD-043 | 00:48–00:52 | 14 | find/get_text điểm xuất phát, set_value + tap gợi ý ×2, get_text×3, tap chip buổi, tap checkbox, tap submit, scroll×2 | 0 | ❌ FAIL step 3 + 8 |
| TC-ORD-015 | 00:56 | 6 | find `(//EditText)[1..3]` + get_text×3 | 0 | ✅ PASS |
| TC-ORD-017 | 00:56 | 1 | get_text ô địa chỉ lấy = hint ⇒ rỗng | 0 | ❌ FAIL step 3 |
| TC-ORD-016 | 00:57 | 3 | tap ô tên, `appium_mobile_keyboard(is_shown)`=false, get_text | 0 | ✅ PASS |
| TC-ORD-029 | 00:58 | 2 | set_value `"Cẩm Lệ"` → dropdown 2 gợi ý hiện | 0 | ✅ PASS |
| TC-ORD-023 | 00:59 | 7 | tap gợi ý, scroll_to_element, find/tap chip buổi, get_attr `enabled`, tap `Tiếp theo`, scroll về nhóm NGƯỜI NHẬN | 0 | ❌ FAIL step 5 *(P1)* |
| TC-ORD-055 | 01:00 | 4 | find ô địa chỉ giao, set_value 200 ký tự, set_value w3cActions, get_text | 0 | ✅ PASS |
| TC-ORD-021 | 01:01–01:04 | 10 | set_value email sai ×2, tap nhãn blur ×2, find 3 chuỗi lỗi → NOT FOUND | 0 | ❌ FAIL step 3 |
| TC-ORD-020 | 01:05 | 6 | set_value email không tồn tại, blur, find/get_text `Không tìm thấy email`, dọn ô địa chỉ | 0 | ✅ PASS |
| TC-ORD-019 | 01:06 | 3 | set_value email tra được, blur, đọc 3 field autofill | 0 | ❌ FAIL step 4 *(P1)* |
| TC-ORD-024 | 01:07 | 8 | find `receiver-name-input`, set_value ×4 (1/2/60 ký tự + w3cActions), blur, find `textContains("Tên")` → NOT FOUND, get_text | 0 | ❌ FAIL step 3 |
| TC-ORD-025 | 01:08–01:11 | 16 | find `receiver-phone-input`, set_value ×5 (9/10/11/không-0/chữ), blur ×5, find chuỗi lỗi ×5, get_text | 0 | ✅ **PASS 5/5** |
| TC-ORD-032 | 01:12 | 5 | scroll_to_element, find/tap `day-part-morning`, find/tap `day-part-anytime` | 0 | ✅ PASS |
| TC-ORD-079 | 01:13–01:15 | 12 | find/tap `descriptionStartsWith("Thêm người nhận uỷ quyền")` *(sau khi `alt-receiver-expand-button` NOT FOUND)*, set_value name+phone, tap `Tiếp theo`, find `Bước 2 / 3` + chuỗi lỗi, **loại nhiễu** ô SĐT người nhận | **1** *(A8)* | ✅ PASS |
| TC-ORD-081 | 01:16–01:18 | 18 | dựng form hợp lệ (set_value name + địa chỉ giao + tap gợi ý), set_value tên uỷ quyền ×4, tap `Tiếp theo` ×3, find `Bước 2/3`+`Bước 3/3`, get_text, scroll | 0 | ✅ **PASS 4/4** |
| TC-ORD-018 | 01:19 | 5 | tap `Quay lại`, scroll×2, find `xpath @hint+@enabled`, get_text | 0 | ✅ PASS |
| TC-ORD-026 | 01:20 | 8 | scroll_to_element, set_value + tap gợi ý, get_text, get_attr `enabled`, tap `Tiếp theo`, find chuỗi lỗi → **FOUND** | 0 | ✅ **PASS** *(bác bỏ VR-002)* |
| TC-ORD-083 | 01:21–01:25 | 20 | lượt 1 nhiễu bởi T13 → **thoát wizard, dựng lại bước 1 từ đầu** (13 call) → set_value 2 địa chỉ gõ tay, tap `Tiếp theo`, find chuỗi lỗi → NOT FOUND | 0 | ❌ FAIL step 5 |
| TC-ORD-084 | 01:26 | 3 | set_value địa chỉ giao + khoảng trắng, tap `Tiếp theo`, find `textContains("phải khác")` → NOT FOUND | 0 | ❌ FAIL step 5 |
| TC-ORD-022 | 01:27–01:30 | 12 | set_value email, get_text SĐT autofill, set_value + tap gợi ý ×2, tap chip buổi, tap `Tiếp theo`, find `Bước 3 / 3` | 0 | ✅ PASS |
| TC-ORD-033 | 01:31 | 1 | xác nhận 4 chip buổi **không có mặc định** ⇒ không dựng được tiền đề | 0 | 🚫 BLOCKED step 2 |
| TC-ORD-051 | 01:32–01:34 | 10 | tap `Quay lại`, scroll_to_element, set_value tên 1 ký tự + SĐT rỗng, find `textContains("Tên phải")` → NOT FOUND, scroll×3, tap `Tiếp theo` | 0 | ❌ FAIL step 3 + 7 |
| TC-ORD-047 | 01:35–01:37 | 6 | back×3, find/tap tab `Hoạt động`, find/tap card `Gửi: Tài liệu`, find `accessibility id "Chỉnh sửa"` → NOT FOUND | **1** *(A9)* | ✅ PASS |
| TC-ORD-085 | 01:38–01:40 | 6 | `appium_mobile_clipboard(set)` sentinel, find `description("Copy").instance(1)`, tap ×2, `clipboard(get)`, lấy mẫu pixel 2 ảnh | 0 | ❌ FAIL step 5 *(vế nội dung PASS)* |
| TC-ORD-086 | 01:41 | 1 | quét A9 tìm SĐT → không có node nào | 0 *(A9)* | 🚫 BLOCKED step 3 |

Cột `Snapshot?` là **đồng hồ đo chi phí**: tổng = **9**, số màn harvest = **5–6** ⇒ xấp xỉ nhau (chênh do 3 màn dài phải dump 2–3 lần vì render lazy) ⇒ **không vi phạm B1/B2**.

## Statistics

| Chỉ số | Giá trị |
|---|---|
| Tổng MCP call *(ước, gộp theo TC)* | **≈ 390** |
| **Tổng snapshot (`get_page_source`)** | **9** |
| **Số màn đã harvest** | **5–6** *(Đăng tin mới · Wizard B1 · Wizard B2 + khối uỷ quyền · **Wizard B3 (mới)** · Form OFFER · Theo dõi đơn)* |
| `find_element` call | ≈ 210 — trong đó **NOT FOUND có chủ đích (verify_absent)**: 24 · **NOT FOUND do bẫy T8/T12** rồi khắc phục bằng `scroll_to_element`: 11 |
| Action call (`gesture` tap/scroll · `set_value`) | ≈ 150 |
| `get_element_attribute(enabled)` | 14 — **đây là cách duy nhất đọc trạng thái nút** (bẫy T4: `clickable` luôn `false`) |
| `appium_mobile_keyboard` · `appium_mobile_clipboard` | 1 · 3 |
| Evidence screenshot *(qua `adb exec-out screencap`)* | 62 file |
| ⚠️ MCP fail giữa phiên | **không có** — session `a0de9221` sống xuyên suốt 23:32 → 01:41 |
| ⚠️ Lỗi element stale | 1 lần (`alt-receiver-name-input` sau khi cuộn) — khắc phục bằng `scroll_to_element` + `find` lại |
