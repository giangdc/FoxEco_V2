# Vibe Locators — v1.1 (+ CARRIED v1.0) — VR-002 — 2026-09-18

> Captured via **Appium MCP** (UiAutomator2) trong phiên này. Platform: **mobile** · app `com.hrisproject.stag` (FoxPro) → FoxEco.
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred (thấy trong page source, chưa find/act trực tiếp) · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md` (audit trail) · locator tích luỹ: `../locators/vibe-locators-latest.md`

## 🔴 5 BẪY KỸ THUẬT MỚI phát hiện ở VR-002 (bổ sung T1–T5 của VR-001)

| # | Bẫy | Bằng chứng trong run này | Cách làm đúng |
|---|---|---|---|
| **T6** | `resource-id` của React Native **không resolve** qua strategy `id` nhưng **resolve** qua `-android uiautomator resourceId(...)` | `id "multi-photo-remove-0"` → NOT FOUND · `new UiSelector().resourceId("multi-photo-remove-0")` → OK | Với mọi rid dạng RN (không có prefix package) **luôn** dùng `-android uiautomator` + `resourceId()` |
| **T7** | **Nút thêm ảnh có `content-desc` = CHÍNH BỘ ĐẾM** (`0/5` → `1/5` → …) ⇒ locator theo desc **đổi theo state** | `accessibility id "0/5"` OK khi chưa có ảnh, NOT FOUND sau khi thêm 1 ảnh | Dùng `resourceId("multi-photo-add-button")` (bền), chỉ dùng `"N/5"` khi **cố ý assert bộ đếm** |
| **T8** | Element **ngoài viewport thì KHÔNG resolve** (kể cả accessibility id đúng) | `accessibility id "0/5"` NOT FOUND khi khối ảnh đang cuộn khỏi màn; `scroll_to_element` xong thì OK | Trước khi find element ở cuối form ⇒ `appium_gesture(action=scroll_to_element)` |
| **T9** | `appium_mobile_keyboard(action=hide)` **gửi BACK** ⇒ ở bước 1 wizard = **thoát wizard + mất dữ liệu** | mất draft giữa lô 3 (xem `vibe-log.md §F6`) | ⛔ Không dùng `hide` để "rời ô" trong wizard — tap vùng trống, hoặc get_text trực tiếp |
| **T10** ♻️ **SAI — ĐÃ ĐÍNH CHÍNH 2026-09-18 chiều** | ~~Dải ảnh khối `ẢNH HÀNG` không cuộn ngang và không render phần tử thứ ≥4~~ → thực tế là **lazy horizontal list**: dải **CÓ cuộn**, phần tử ngoài viewport chỉ **chưa được compose**. Bản sai này đã đẻ ra ứng viên bug ma **B3** (đã huỷ) | recheck: `adb shell input swipe 950 1836 150 1836 500` cuộn tới cuối ngay; app nhận đủ **5 ảnh**; `multi-photo-remove-3`/`-4` có thật | **Cuộn dải rồi mới assert.** Bản đầy đủ + lý do: `locators/vibe-locators-latest.md` **T10** |

## Screen: Đăng tin mới *(chọn loại tin — bottom nav ẩn)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Subtitle "Bạn muốn làm gì?" | verify_visible | -android uiautomator | `new UiSelector().text("Bạn muốn làm gì?")` | ✅ | mcp-log TC-ORD-001 | TC-ORD-001 |
| Card NEED "Tôi cần gửi hàng" | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Tôi cần gửi hàng")` | ✅ | mcp-log TC-ORD-001 | TC-ORD-001/002 + mọi TC wizard |
| Card OFFER "Tôi nhận giao hàng" | verify_visible | -android uiautomator | `new UiSelector().descriptionStartsWith("Tôi nhận giao hàng")` | ✅ | mcp-log TC-ORD-001 | TC-ORD-001 *(chưa tap — step 5 còn nợ)* |
| Banner cam kết | get_text | -android uiautomator | `new UiSelector().textContains("không thu phí")` | ✅ | mcp-log TC-ORD-001 | TC-ORD-001 |
| ↳ chuỗi thật | — | — | `App không thu phí, không chat, không thanh toán. Sau khi ghép, SĐT hai bên sẽ được lộ để liên hệ ngoài app.` | ✅ | — | — |
| Nút "←" của màn này | — | *(không phải `Quay lại`)* | `accessibility id "Quay lại"` 🚫 NOT FOUND ở màn này ⇒ dùng `appium_gesture(action=back)` | 🚫 | mcp-log TC-ORD-062 | — |

## Screen: Wizard Bước 1/3 "Thông tin hàng" ★

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Step indicator | get_text | -android uiautomator | `new UiSelector().text("Bước 1 / 3")` *(CÓ space quanh `/`)* | ✅ | mcp-log TC-ORD-002 | TC-ORD-002/007/008/014/063 |
| Tiêu đề bước | get_text | -android uiautomator | `new UiSelector().text("Thông tin hàng")` | ✅ | mcp-log TC-ORD-002 | TC-ORD-002 |
| Nút "←" (lùi bước / thoát ở bước 1) | tap | accessibility id | `Quay lại` | ✅ | mcp-log TC-ORD-053 | TC-ORD-053/062/064/066 |
| 8 chip LOẠI HÀNG | tap | accessibility id | `Tài liệu` · `Đồ điện tử` · `Thực phẩm` · `Hàng nhỏ` · `Đồ dễ vỡ` · `Quần áo` · `Thuốc/Y tế` · `Khác` | ✅ *(`Tài liệu` đã tap)* | mcp-log TC-ORD-005/006/007 | TC-ORD-005/006/007/014 |
| Field GHI CHÚ | type · get_text | class name | `android.widget.EditText` *(EditText DUY NHẤT ở bước 1)* | ✅ | mcp-log TC-ORD-011 | TC-ORD-011/054 |
| ↳ thuộc tính | — | — | `max-text-length=300` · `input-type=147457` · rỗng ⇒ `showing-hint="true"` | ✅ | — | TC-ORD-011/062 |
| Chip GIÁ TRỊ HÀNG | tap | -android uiautomator | `descriptionStartsWith("Thấp")` · `("Vừa, 1")` · `("Cao, Trên 5")` | ✅ | mcp-log TC-ORD-008/009/010 | TC-ORD-008/009/010/054/063/064/066 |
| ↳ resource-id *(nay resolve được qua T6)* | tap | -android uiautomator | `resourceId("value-tier-chip-option-low")` / `-medium` / `-high` | ⚠️ Inferred | mcp-log A2 | — *(VR-001 ghi 🚫 với strategy `id`; đổi sang uiautomator thì thấy trong tree)* |
| Banner "hàng giá trị cao" | get_text | -android uiautomator | `new UiSelector().textContains("giá trị cao")` | ✅ | mcp-log TC-ORD-009 | TC-ORD-009/010 |
| ↳ chuỗi thật | — | — | `Hàng giá trị cao: hai bên tự thoả thuận và chịu trách nhiệm với nhau. FoxEco không bảo hiểm, không đứng ra vận chuyển hay bồi thường.` | ✅ | — | — |
| Chip TRỌNG LƯỢNG | tap | -android uiautomator | `descriptionStartsWith("Dưới 5 kg")` · `("5 – 10 kg")` · `("Trên 10 kg")` | ✅ *(`Dưới 5 kg` đã tap)* | mcp-log TC-ORD-064 | TC-ORD-063/064/065 |
| ↳ desc đầy đủ | — | — | `Dưới 5 kg, Nhẹ` · `5 – 10 kg, Trung bình` · `Trên 10 kg, Nặng` | ✅ | — | TC-ORD-064 |
| ↳ resource-id | — | -android uiautomator | `resourceId("weight-tier-chip-option-light")` / `-medium` / `-heavy` | ⚠️ Inferred | mcp-log A2 | — |
| Chip KÍCH THƯỚC | tap | -android uiautomator | `descriptionStartsWith("Nhỏ")` · `("Vừa, ~20")` · `("Lớn")` | ✅ *(`Nhỏ` đã tap)* | mcp-log TC-ORD-066 | TC-ORD-063/066/067 |
| ↳ desc đầy đủ | — | — | `Nhỏ, Cầm tay` · `Vừa, ~20×20 cm` · `Lớn, > 20×20 cm` | ✅ | — | TC-ORD-066 |
| ↳ resource-id | — | -android uiautomator | `resourceId("size-tier-chip-option-small")` / `-medium` / `-large` | ⚠️ Inferred | mcp-log A2 | — |
| Nhãn khối ảnh | get_text | -android uiautomator | `new UiSelector().textStartsWith("ẢNH HÀNG")` → **`ẢNH HÀNG *`** | ✅ | mcp-log TC-ORD-013 | TC-ORD-013 |
| **Nút thêm ảnh** | tap | -android uiautomator | `new UiSelector().resourceId("multi-photo-add-button")` ⭐ **bền** | ✅ | mcp-log TC-ORD-064 | TC-ORD-012/068/069/070/087 |
| ↳ bộ đếm ảnh *(= content-desc của nút, **T7**)* | verify | accessibility id | `0/5` → `1/5` → `2/5` → `3/5` | ✅ | mcp-log TC-ORD-012/087 | TC-ORD-012/013/068/087 |
| Nút xoá ảnh thứ N | tap | -android uiautomator | `new UiSelector().resourceId("multi-photo-remove-<N>")` *(N từ 0)* | ✅ *(N=0)* | mcp-log TC-ORD-087 | TC-ORD-087/071 |
| ↳ `multi-photo-remove-3` | — | -android uiautomator | *(chỉ NOT FOUND khi **chưa cuộn** dải — xem **T10** đã đính chính; cuộn xong thì có thật)* | ⚠️ cần cuộn | mcp-log TC-ORD-070 | TC-ORD-070/071 |
| Dòng helper khối ảnh | get_text | -android uiautomator | `new UiSelector().textStartsWith("Bắt buộc ít nhất 1 ảnh")` | ✅ | mcp-log TC-ORD-013 | TC-ORD-013/063 |
| ↳ chuỗi thật | — | — | `Bắt buộc ít nhất 1 ảnh · tối đa 5 ảnh · giúp người vận chuyển nhận diện hàng` | ✅ | — | — |
| Lỗi "ảnh quá 5MB" | get_text | -android uiautomator | `new UiSelector().textContains("5MB")` → `Ảnh vượt quá 5MB, vui lòng chọn ảnh nhỏ hơn.` | ✅ | mcp-log TC-ORD-068 | TC-ORD-068 |
| Nút "Tiếp theo" | tap · get_element_attribute | accessibility id | `Tiếp theo` | ✅ | mcp-log TC-ORD-008 | gần như mọi TC |
| ↳ ⚠️ đọc enable/disable | — | — | **dùng `enabled`** (`false`/`true`); ⛔ `clickable` luôn `false` (bẫy **T4** của VR-001) | ✅ | mcp-log TC-ORD-008/063 | — |
| ↳ điều kiện enable (đo được) | — | — | **cần ĐỦ 4**: giá trị hàng + trọng lượng + kích thước + **≥1 ảnh** | ✅ | mcp-log TC-ORD-027 | F1 |
| Thông báo lỗi ở khối thiếu dữ liệu | verify_absent | -android uiautomator | *(không có node nào)* | 🚫 **NOT FOUND** *(SAI kỳ vọng ⇒ bug F3)* | mcp-log TC-ORD-063/064/066 | TC-ORD-063/064/066 |

## Screen: Bottom sheet chọn nguồn ảnh *(app)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| "Chụp ảnh" | verify_visible | -android uiautomator | `new UiSelector().text("Chụp ảnh")` | ✅ | mcp-log TC-ORD-069 | TC-ORD-069 |
| "Chọn từ thư viện" | tap | -android uiautomator | `new UiSelector().text("Chọn từ thư viện")` | ✅ | mcp-log TC-ORD-012 | mọi TC ảnh |
| ⚠️ **KHÔNG có** lối chọn file khác ảnh | verify_absent | — | *(chỉ 2 mục trên)* | 🚫 NOT FOUND | mcp-log TC-ORD-069 | TC-ORD-069 *(⇒ BLOCKED)* |

## Screen: Android Photo Picker *(OS — `com.google.android.providers.media.module`)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Thumbnail thứ N | tap | -android uiautomator | `new UiSelector().resourceId("com.google.android.providers.media.module:id/icon_thumbnail").instance(<N>)` ⭐ | ✅ | mcp-log A3 | TC-ORD-012/068/070/087 |
| ↳ ⚠️ `content-desc` **không phân biệt được** | — | — | mọi item đều `Photo taken on Sep 18, 2026, 12:29:40 PM` ⇒ **phải dùng `.instance(N)`** | ✅ | mcp-log A3 | — |
| Nút xác nhận "Add (N)" | tap | -android uiautomator | `new UiSelector().textStartsWith("Add")` | ✅ | mcp-log TC-ORD-012 | mọi TC ảnh |
| Tab "Photos" / "Albums" | — | accessibility id | `Photos` · `Albums` | ⚠️ Inferred | mcp-log A3 | — |
| Nút "Cancel" | — | accessibility id | `Cancel` | ⚠️ Inferred | mcp-log A3 | — |

## Screen: Wizard Bước 2/3 "Địa điểm & Thời gian" ★

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Step indicator | get_text | -android uiautomator | `new UiSelector().text("Bước 2 / 3")` | ✅ | mcp-log TC-ORD-083 | TC-ORD-083/084 |
| Tên người gửi *(chỉ đọc)* | tap · get_text | xpath | `(//android.widget.EditText)[1]` → `Đặng Châu Giang` | ✅ | mcp-log TC-ORD-015/016 | TC-ORD-015/016 |
| ↳ ⚠️ chạm **không mở bàn phím** ⇒ đúng "chỉ đọc" | — | — | kiểm bằng `appium_mobile_keyboard(action=is_shown)` → `false` | ✅ | mcp-log TC-ORD-016 | TC-ORD-016 |
| SĐT người gửi *(prefill)* | get_text | xpath | `(//android.widget.EditText)[2]` → `0912345670` | ✅ | mcp-log TC-ORD-015/018 | TC-ORD-015/018 |
| **Địa chỉ lấy hàng** *(prefill = địa chỉ mặc định hồ sơ)* | type · get_text | xpath | `(//android.widget.EditText)[3]` → `363 Nguyễn Hữu Thọ, Cẩm Lệ` | ✅ | mcp-log TC-ORD-027 | TC-ORD-017/027/083/084 |
| Email công ty người nhận | type | xpath | `//android.widget.EditText[@hint="Email công ty người nhận"]` | ✅ | mcp-log TC-ORD-074 | TC-ORD-074..078/083/084/018 |
| Tên người nhận *(autofill)* | type · get_text | -android uiautomator | `new UiSelector().resourceId("receiver-name-input")` | ✅ | mcp-log TC-ORD-074 | TC-ORD-074 |
| SĐT người nhận *(autofill)* | verify | -android uiautomator | `resourceId("receiver-phone-input")` | ⚠️ Inferred | mcp-log TC-ORD-074 | TC-ORD-074 *(đọc qua ảnh, chưa find trực tiếp)* |
| Địa chỉ giao hàng | type · get_text | xpath | `//android.widget.EditText[@hint="Địa chỉ giao hàng"]` | ✅ | mcp-log TC-ORD-028 | TC-ORD-028/055/083/084/053/018 |
| ↳ thuộc tính | — | — | `max-text-length=200` · **không tự trim** giá trị hiển thị | ✅ | mcp-log TC-ORD-055/084 | TC-ORD-055/084 |
| ↳ ⚠️ **KHÔNG có** dropdown gợi ý ở ô này | verify_absent | -android uiautomator | `resourceId("address-suggestion-0")` | 🚫 NOT FOUND *(đúng kỳ vọng — khác màn USR)* | mcp-log TC-ORD-028 | TC-ORD-028 |
| Thông báo tra danh bạ | get_text | -android uiautomator | `textContains("Đã tìm thấy")` / `textContains("Không tìm thấy email")` | ✅ | mcp-log TC-ORD-074/075 | TC-ORD-074..078 |
| ↳ chuỗi thật (tìm thấy) | — | — | `Đã tìm thấy trong hệ thống nội bộ · vui lòng bổ sung SĐT/địa chỉ giao còn thiếu.` | ✅ | — | TC-ORD-074 |
| ↳ chuỗi thật (không thấy) | — | — | `Không tìm thấy email này — vui lòng nhập tay thông tin bên dưới.` *(🚩 câu chữ v1.0, xem F5)* | ✅ | — | TC-ORD-075/076/078 |
| Nút "Thêm người nhận uỷ quyền" | — | accessibility id | `alt-receiver-expand-button` *(nhãn: `+ Thêm người nhận uỷ quyền`)* | ⚠️ Inferred | mcp-log A2 | ⏳ TC-ORD-079..082 |
| Ô "Từ ngày" | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Từ ngày")` | ✅ | mcp-log TC-ORD-030 | TC-ORD-030/031/056/057 |
| Ô "Đến ngày" | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Đến ngày")` | ✅ | mcp-log TC-ORD-031 | TC-ORD-031/056/057 |
| Ngày thứ N trong date picker | tap | -android uiautomator | `new UiSelector().text("<số ngày>")` *(vd `"25"`)* | ✅ | mcp-log TC-ORD-056 | TC-ORD-030/031/056/057 |
| ↳ ⚠️ ngày không hợp lệ **bị làm mờ** và tap **không có tác dụng** | — | — | quá khứ · sớm hơn `Từ ngày` | ✅ | mcp-log TC-ORD-030/031 | TC-ORD-030/031 |
| Nút "Đóng" date picker | tap | -android uiautomator | `new UiSelector().text("Đóng")` | ✅ | mcp-log TC-ORD-031 | TC-ORD-031/056/057 |
| Lỗi khoảng ngày | get_text | -android uiautomator | `textContains("tối đa 7 ngày")` → `Đến ngày tối đa 7 ngày kể từ Từ ngày` | ✅ | mcp-log TC-ORD-057 | TC-ORD-057 |
| 4 chip BUỔI MONG MUỐN | tap | -android uiautomator | `descriptionStartsWith("Sáng")` · `("Chiều")` · `("Sau giờ làm")` · `("Giờ nào cũng được")` | ✅ *(3/4 đã tap)* | mcp-log TC-ORD-059/075/018 | TC-ORD-058/059/075/018 |
| ↳ nhãn thật | — | — | `Sáng (8–12h)` 08:00–12:00 · `Chiều (13–17h)` 13:00–17:00 · `Sau giờ làm (17–19h)` 17:00–19:00 · `Giờ nào cũng được` Linh động cả ngày | ✅ | — | TC-ORD-058 |
| ↳ ⚠️ **không có mặc định** + buổi đã qua **vẫn `enabled=true`** | — | — | ⇒ bug `TC-ORD-058`/`059` | ✅ | mcp-log TC-ORD-058/059 | — |
| Lỗi "chưa chọn buổi" | get_text | -android uiautomator | `new UiSelector().text("Chọn ít nhất 1 buổi")` | ✅ | mcp-log TC-ORD-058 | TC-ORD-058 |
| Nút "Tiếp theo" (bước 2) | tap · get_element_attribute | accessibility id | `Tiếp theo` | ✅ | mcp-log TC-ORD-075 | TC-ORD-075/076/083/084 |
| ↳ điều kiện enable (đo được) | — | — | email **tra thấy trên HRIS** + tên + SĐT + địa chỉ giao (**≠ địa chỉ lấy**) + ≥1 buổi | ✅ | mcp-log TC-ORD-075/083 | F3/F5 |

## Navigation Flow (chỉ flow đã đi qua bằng MCP trong run này)

| From | Trigger | To | MCP-verified |
|---|---|---|---|
| FoxEco Trang chủ | tap `Đăng tin` (bottom nav) | Đăng tin mới *(bottom nav ẩn)* | TC-ORD-001 step 2 |
| Đăng tin mới | tap card `Tôi cần gửi hàng` | Wizard Bước 1/3 | TC-ORD-002 step 3 |
| Wizard Bước 1/3 | tap `Tiếp theo` *(đủ 4 điều kiện)* | Bước 2/3 | TC-ORD-027 step 2 |
| Wizard Bước 1/3 | tap `Tiếp theo` *(thiếu 1 điều kiện)* | **ở lại bước 1, KHÔNG báo lỗi** | TC-ORD-063/064/066 |
| Wizard Bước 2/3 | tap `Quay lại` | **về Bước 1/3** *(⚠️ KHÔNG phải đóng wizard)* | TC-ORD-053 step 3 |
| Wizard Bước 1/3 | tap `Quay lại` *(có dữ liệu chưa lưu)* | **thoát về Đăng tin mới NGAY, xoá dữ liệu, KHÔNG popup** | TC-ORD-053 step 3b |
| Wizard Bước 1/3 | `appium_mobile_keyboard(hide)` | **= BACK ⇒ thoát wizard, mất draft** | lô 3 (F6) |
| Đăng tin mới | `appium_gesture(action=back)` | FoxEco Trang chủ *(bottom nav hiện lại)* | TC-ORD-062 step 4 |
| Trang chủ | tap `Hoạt động` | Đơn của tôi *(2 tab con: `Đang diễn ra` / `Đã hoàn thành`)* | TC-ORD-062 step 4 |
| Khối ảnh | tap `multi-photo-add-button` → `Chọn từ thư viện` | Android Photo Picker | TC-ORD-012 step 2 |
| Photo Picker | tap thumbnail → `Add (N)` | về wizard, bộ đếm +N | TC-ORD-012 step 3 |
| Photo Picker *(ảnh > 5MB)* | tap thumbnail → `Add (1)` | ⚠️ **1 lần** bị đẩy ra tab THÔNG BÁO của FoxPro (F2); state wizard giữ nguyên | TC-ORD-068 step 3 |
| FoxPro THÔNG BÁO | tap menu `Chức năng` | về FoxEco **đúng màn đang dở** | TC-ORD-068 step 3 |

## Thống kê

| Screens visited | Elements captured | Verified ✅ | Inferred ⚠️ | NOT FOUND 🚫 |
|---|---|---|---|---|
| **5** (Đăng tin mới · Wizard B1 · Bottom sheet ảnh · Android Photo Picker · Wizard B2) | **62** | **47** | **10** | **5** |

> 🚫 NOT FOUND gồm **3 ca đúng kỳ vọng** (`address-suggestion-0` ở ô địa chỉ giao · không có lối chọn file ngoài ảnh · `Quay lại` không tồn tại ở màn "Đăng tin mới")
> và **2 ca SAI kỳ vọng ⇒ bug** (thông báo lỗi ở khối thiếu dữ liệu — F3 · `multi-photo-remove-3`/add-button sau ảnh thứ 4 — T10).
>
> ⏳ **Chưa harvest** (thuộc phần còn nợ 46 TC): Wizard **Bước 3/3**, màn **Đăng tin thành công**, **Theo dõi đơn** (VR-001 đã có), form **OFFER**, khối **uỷ quyền**, **lightbox/carousel ảnh** ở chi tiết tin, **icon copy** địa chỉ/SĐT.
