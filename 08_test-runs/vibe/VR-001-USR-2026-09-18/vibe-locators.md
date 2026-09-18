# Vibe Locators — v1.1 — VR-001 — 2026-09-18

> Captured via **Appium MCP** (UiAutomator2) during this run · app `com.hrisproject.stag` (FoxPro host → FoxEco)
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md` (audit trail) · Platform: **mobile**
> Ưu tiên strategy: `accessibility id` > `id` > `-android uiautomator` > `xpath`

## 🔴 5 BẪY KỸ THUẬT — đọc trước khi implement automation

| # | Bẫy | Bằng chứng trong run này | Cách làm đúng |
|---|---|---|---|
| **T1** | **`selected` KHÔNG BAO GIỜ được expose** trên tab/chip (React Native) | tab `Đang diễn ra` **đang active** nhưng `selected="false"`; cả 4 chip đã chọn (viền cam) vẫn `selected="false"` | ⛔ Không assert trạng thái active/selected bằng attribute. Dùng ảnh, hoặc assert **hệ quả** (nội dung list đổi, nút `Tiếp theo` enable) |
| **T2** | `resource-id` **có trong page source nhưng KHÔNG resolve** qua `id`/`accessibility id` với một số element | `value-tier-chip-option-low` → cả 2 strategy đều NOT FOUND; `activity-order-card-0` cũng có lúc NOT FOUND | Dùng `-android uiautomator` `descriptionStartsWith(...)`. Các id **có** resolve: `profile-menu-*`, `address-suggestion-N`, `track-edit-post`, `post-n3-consent-checkbox` |
| **T3** | `appium_get_element_attribute` **không nhận** `showing-hint` dù bảng attribute hợp lệ có liệt kê | `showing-hint` + `showingHintText` đều báo *"attribute is unknown"* | Kiểm ô rỗng bằng `appium_get_page_source` rồi đọc `showing-hint="true"` |
| **T4** | Nút `Tiếp theo` / `Lưu thay đổi` luôn `clickable="false"` **kể cả khi enable** | `Tiếp theo` `clickable=false` ở cả trạng thái disable **và** enable | ⛔ Không dùng `clickable` để suy enable/disable. `tap` qua element vẫn chạy khi enable |
| **T5** | Ô "Địa chỉ mặc định"/"Địa chỉ lấy hàng" **phải CHỌN từ gợi ý**, gõ xong bấm nút là bị chặn | Bước 2/3 wizard: gõ `FPT Cầu Giấy` rồi bấm `Tiếp theo` → không sang bước; phải `tap address-suggestion-0` trước | Luôn `set_value` → `find(address-suggestion-N)` → `tap` |

## Host app: FoxPro — màn "Chức năng"

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Icon FoxEco (entry point) | tap | -android uiautomator | `new UiSelector().text("FoxEco")` | ✅ | mcp-log TC-USR-001 | TC-USR-001, TC-USR-042 |

## Screen: FoxEco — Trang chủ

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tab "Trang chủ" | tap | accessibility id | `Trang chủ` | ✅ | mcp-log A1 | TC-USR-002/004/007/008/012/013 |
| Tab "Bảng tin" | verify_absent | accessibility id | `Bảng tin` | ✅ | mcp-log TC-USR-014 | TC-USR-014 (chứng cứ ẩn bottom nav) |
| Tab "Đăng tin" | tap | accessibility id | `Đăng tin` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Tab "Hoạt động" | tap | accessibility id | `Hoạt động` | ✅ | mcp-log TC-USR-009 | TC-USR-009, TC-USR-025 |
| Tab "Cá nhân" | tap | accessibility id | `Cá nhân` | ✅ | mcp-log A2 | hầu hết TC USR |
| Nút thoát FoxEco → FoxPro | tap | accessibility id | `Quay lại` | ✅ | mcp-log TC-USR-001 | TC-USR-001, TC-USR-042 |
| Icon thông báo | — | accessibility id | `Thông báo` | ⚠️ Inferred | mcp-log A1 | — *(thấy trong tree, chưa tap)* |
| Số "đơn đã giúp" (hero) | verify | id | `home-helped-count` | ⚠️ Inferred | mcp-log A1 | — *(chưa dùng trong TC nào của lô này)* |
| CTA "Xem bảng tin gửi hàng" | — | accessibility id | `Xem bảng tin gửi hàng` | ⚠️ Inferred | mcp-log A1 | — |
| Link "Xem tất cả" (Đơn của tôi) | — | accessibility id | `Xem tất cả` | ⚠️ Inferred | mcp-log A1 | — |

## Screen: Cá nhân

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Avatar chữ viết tắt | get_text | -android uiautomator | `new UiSelector().text("ĐC")` | ✅ | mcp-log TC-USR-002 | TC-USR-002, TC-USR-003 |
| ↳ ⚠️ **giá trị động theo tên** | — | — | bền hơn: `xpath //android.widget.TextView[string-length(@text)=2]` trong khối header | ⚠️ Inferred | — | — |
| Dòng "phòng ban · MNV" | get_text | -android uiautomator | `new UiSelector().textContains("MNV:")` | ✅ | mcp-log TC-USR-001 | TC-USR-001/002/003/004 |
| Card chỉ số "quà đã nhận" | — | accessibility id | `profile-stat-gifts` | ⚠️ Inferred | mcp-log A4 | TC-USR-012 *(chỉ đọc bounds, chưa tap)* |
| Menu "Đơn của tôi" | tap | accessibility id | `profile-menu-activity` | ✅ | mcp-log TC-USR-009 | TC-USR-009, TC-USR-012 |
| Menu "Quà đã nhận" | tap | accessibility id | `profile-menu-gifts` | ✅ | mcp-log TC-USR-010 | TC-USR-010, TC-USR-012/013 |
| Menu "Cập nhật thông tin cá nhân" | tap | accessibility id | `profile-menu-editProfile` | ✅ | mcp-log TC-USR-014 | TC-USR-011/013/014/024 + toàn bộ lô 2–4 |
| ↳ nhãn của menu đó | get_text | -android uiautomator | `new UiSelector().textStartsWith("Cập nhật thông tin")` → `Cập nhật thông tin cá nhân` | ✅ | mcp-log TC-USR-013 | TC-USR-013 |
| Badge "Hạng Đồng hành" | verify_absent | -android uiautomator | `new UiSelector().textContains("Hạng")` · `...textContains("Đồng hành")` | 🚫 **NOT FOUND** *(đúng kỳ vọng)* | mcp-log TC-USR-008 | TC-USR-008, TC-USR-012 |
| "Điểm ECO"/"Điểm uy tín"/CO₂ | verify_absent | -android uiautomator | `textContains("Điểm")` · `("ECO")` · `("uy tín")` · `("CO")` | 🚫 **NOT FOUND** *(đúng kỳ vọng)* | mcp-log TC-USR-007 | TC-USR-007 |
| Email công ty (trên màn Cá nhân) | verify_absent | -android uiautomator | `new UiSelector().textContains("@fpt.com")` | 🚫 **NOT FOUND** *(đúng kỳ vọng)* | mcp-log TC-USR-002 | TC-USR-002 |

## Screen: Đơn của tôi *(= "màn Hoạt động"; mở từ `profile-menu-activity` HOẶC tab `Hoạt động`)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tab "Đang diễn ra" | verify_visible | accessibility id | `Đang diễn ra` | ✅ | mcp-log TC-USR-009 | TC-USR-009 |
| Tab "Đã hoàn thành" | verify_visible | accessibility id | `Đã hoàn thành` | ✅ | mcp-log TC-USR-009 | TC-USR-009 |
| ↳ ⚠️ **T1**: trạng thái active **không** đọc được qua `selected` | — | — | cả 2 tab đều `selected="false"` | — | — | — |
| Card đơn thứ N | tap | accessibility id | `activity-order-card-<N>` *(N từ 0)* | ✅ | mcp-log TC-USR-009 | TC-USR-025 |
| ↳ fallback khi id không resolve (**T2**) | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Gửi: Tài liệu")` | ✅ | mcp-log TC-USR-025 | TC-USR-025 |

## Screen: Quà đã nhận

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tiêu đề màn | verify_visible | -android uiautomator | `new UiSelector().text("Quà đã nhận")` | ✅ | mcp-log TC-USR-010 | TC-USR-010 |

## Screen: Cập nhật thông tin ★ *(màn trọng tâm của USR v1.1)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Nút "←" (quay lại) | tap | accessibility id | `Quay lại` | ✅ | mcp-log TC-USR-014 | TC-USR-014/019/030/045/046 |
| Tiêu đề màn | verify_visible | -android uiautomator | `new UiSelector().text("Cập nhật thông tin")` | ✅ | mcp-log TC-USR-014 | TC-USR-014 |
| **Field "Số điện thoại mặc định"** | type · get_text | xpath | `//android.widget.EditText[@hint="09xx xxx xxx"]` | ✅ | mcp-log TC-USR-017 | TC-USR-015..023, 027, 043 |
| ↳ ⚠️ `input-type=16387` (phone) **vẫn nhận chữ** · `max-text-length=5000` | — | — | — | — | — | TC-USR-019, TC-USR-023 |
| **Field "Địa chỉ mặc định"** | type · get_text | xpath | `//android.widget.EditText[@hint="Toà nhà, đường, quận"]` | ✅ | mcp-log TC-USR-031 | TC-USR-028..042, 045, 046 |
| ↳ `max-text-length=200` · `input-type=16385` | — | — | — | — | — | — |
| Gợi ý văn phòng thứ N | tap | accessibility id | `address-suggestion-<N>` *(N từ 0)* | ✅ | mcp-log TC-USR-033 | TC-USR-032..039, 045, 046, 025, 026 |
| Email công ty *(chỉ đọc)* | verify_visible | -android uiautomator | `new UiSelector().textContains("@fpt.com")` | ✅ | mcp-log TC-USR-024 | TC-USR-024 |
| ↳ ⚠️ là `TextView`, **không** `EditText` ⇒ đúng "chỉ đọc" | — | — | — | — | — | TC-USR-024 |
| Nút "Lưu thay đổi" | tap | accessibility id | `Lưu thay đổi` | ✅ | mcp-log TC-USR-017 | toàn bộ lô 2–4 |
| Thông báo lỗi dưới field SĐT | get_text | -android uiautomator | `new UiSelector().textContains("Số điện thoại")` | ✅ | mcp-log TC-USR-017 | TC-USR-017/018/020/023 |
| ↳ chuỗi thật: `Số điện thoại không được để trống` · `Số điện thoại không hợp lệ` | — | — | — | — | — | — |
| Banner "Đã lưu thông tin của bạn" | verify_absent | -android uiautomator | `new UiSelector().textContains("Đã lưu")` | 🚫 **NOT FOUND** *(SAI kỳ vọng — bug)* | mcp-log TC-USR-015 | TC-USR-015, 027, 029 |
| Icon khiên bên phải field Email | verify_absent | *(không có node)* | — | 🚫 **NOT FOUND** *(SAI kỳ vọng — bug)* | mcp-log TC-USR-024 | TC-USR-024 |

## Screen: Wizard "Đăng tin" — Bước 1/3 "Thông tin hàng"

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Lựa chọn "Tôi cần gửi hàng" (NEED) | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Tôi cần gửi hàng")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Lựa chọn "Tôi nhận giao hàng" (OFFER) | — | -android uiautomator | `new UiSelector().descriptionStartsWith("Tôi nhận giao hàng")` | ⚠️ Inferred | mcp-log TC-USR-025 | — |
| Chip loại hàng "Tài liệu" | tap | accessibility id | `Tài liệu` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ các chip khác | — | accessibility id | `Đồ điện tử` · `Thực phẩm` · `Hàng nhỏ` · `Đồ dễ vỡ` · `Quần áo` · `Thuốc/Y tế` · `Khác` | ⚠️ Inferred | mcp-log TC-USR-025 | — |
| Field "GHI CHÚ" | type | class name | `android.widget.EditText` *(EditText duy nhất ở bước này)* | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Chip giá trị "Thấp" | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Thấp")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ resource-id *(⚠️ **T2** không resolve)* | — | id | `value-tier-chip-option-low` / `-medium` / `-high` | 🚫 NOT FOUND | mcp-log TC-USR-025 | — |
| Chip trọng lượng "Dưới 5 kg" | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Dưới 5 kg")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ resource-id | — | *(page source only)* | `weight-tier-chip-option-light` / `-medium` / `-heavy` | ⚠️ Inferred | — | — |
| Chip kích thước "Nhỏ" | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Nhỏ, Cầm tay")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ resource-id | — | *(page source only)* | `size-tier-chip-option-small` / `-medium` / `-large` | ⚠️ Inferred | — | — |
| **Nút thêm ảnh hàng (BẮT BUỘC)** | tap | accessibility id | `0/5` *(đổi theo số ảnh: `1/5`…)* | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ resource-id bền hơn | tap | *(page source only)* | `multi-photo-add-button` | ⚠️ Inferred | — | — |
| Bottom sheet "Chụp ảnh" | — | -android uiautomator | `new UiSelector().text("Chụp ảnh")` | ⚠️ Inferred | mcp-log TC-USR-025 | — |
| Bottom sheet "Chọn từ thư viện" | tap | -android uiautomator | `new UiSelector().text("Chọn từ thư viện")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Nút "Add (N)" của photo picker Android | tap | -android uiautomator | `new UiSelector().textStartsWith("Add")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Nút "Tiếp theo" | tap | accessibility id | `Tiếp theo` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Nút "Huỷ chỉnh sửa" *(chỉ có ở mode edit)* | tap | -android uiautomator | `new UiSelector().text("Huỷ chỉnh sửa")` | ✅ | mcp-log TC-USR-025 | TC-USR-025 |

## Screen: Wizard "Đăng tin" — Bước 2/3 "Địa điểm & Thời gian" ★

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tên người gửi *(chỉ đọc)* | verify_visible | xpath | `(//android.widget.EditText)[1]` | ✅ | mcp-log TC-USR-025 | TC-USR-025 |
| **SĐT người gửi** *(prefill từ hồ sơ)* | type · get_text | xpath | `(//android.widget.EditText)[2]` | ✅ | mcp-log TC-USR-026 | TC-USR-025, TC-USR-026 |
| **Địa chỉ lấy hàng** *(prefill từ hồ sơ)* | type · get_text | xpath | `(//android.widget.EditText)[3]` | ✅ | mcp-log TC-USR-026 | TC-USR-025, TC-USR-026 |
| Email công ty người nhận | type | xpath | `//android.widget.EditText[@hint="Email công ty người nhận"]` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Tên người nhận *(autofill từ HRIS)* | verify_visible | accessibility id | `receiver-name-input` | ⚠️ Inferred | mcp-log TC-USR-025 | TC-USR-025 *(đọc qua page source, chưa find trực tiếp)* |
| SĐT người nhận *(autofill từ HRIS)* | verify_visible | accessibility id | `receiver-phone-input` | ⚠️ Inferred | mcp-log TC-USR-025 | TC-USR-025 |
| Địa chỉ giao hàng | type | xpath | `//android.widget.EditText[@hint="Địa chỉ giao hàng"]` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Nút "Thêm người nhận uỷ quyền" | — | accessibility id | `alt-receiver-expand-button` | ⚠️ Inferred | mcp-log TC-USR-025 | — |
| Chọn "Từ ngày" / "Đến ngày" | — | -android uiautomator | `descriptionStartsWith("Từ ngày")` · `("Đến ngày")` | ⚠️ Inferred | mcp-log TC-USR-025 | — *(mặc định "Hôm nay", không cần tap)* |
| **Buổi "Giờ nào cũng được" (BẮT BUỘC ≥1)** | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Giờ nào cũng được")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ resource-id các buổi | — | *(page source only)* | `day-part-morning` · `day-part-afternoon` · `day-part-after_work` · `day-part-anytime` | ⚠️ Inferred | — | — |

## Screen: Wizard "Đăng tin" — Bước 3/3 "Xác nhận & Đăng tin"

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Checkbox đồng ý điều khoản | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Tôi đã đọc và đồng ý")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ resource-id | tap | accessibility id | `post-n3-consent-checkbox` | ⚠️ Inferred | mcp-log TC-USR-025 | — |
| Nút "Đăng tin ngay" | tap | accessibility id | `Đăng tin ngay` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Popup "Đăng tin thành công!" → "Theo dõi đơn" | tap | -android uiautomator | `new UiSelector().text("Theo dõi đơn")` | ✅ | mcp-log TC-USR-025 | TC-USR-025 |
| Popup → "Về trang chủ" | tap | -android uiautomator | `new UiSelector().text("Về trang chủ")` | ✅ | mcp-log TC-USR-026 | TC-USR-026 |

## Screen: Theo dõi đơn

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tiêu đề màn | verify_visible | -android uiautomator | `new UiSelector().text("Theo dõi đơn")` | ✅ | mcp-log TC-USR-025 | TC-USR-025 |
| Giá trị "Lấy hàng" *(địa chỉ lấy hàng của ĐƠN)* | get_text | *(TextView ngay dưới label `Lấy hàng`)* | `xpath //android.widget.TextView[@text="Lấy hàng"]/following-sibling::*[1]` | ⚠️ Inferred | mcp-log TC-USR-025 | TC-USR-025 *(đọc qua page source)* |
| Nút "Chỉnh sửa" | tap | accessibility id | `Chỉnh sửa` | ✅ | mcp-log TC-USR-025 | TC-USR-025 |
| ↳ resource-id | tap | *(page source only)* | `track-edit-post` | ⚠️ Inferred | — | — |
| Nút "Huỷ đơn" | — | accessibility id | `Huỷ đơn` *(rid `track-cancel-post`)* | ⚠️ Inferred | mcp-log TC-USR-025 | — ⛔ **không tap** (có popup xác nhận, sẽ huỷ đơn thật) |
| Khối ảnh sản phẩm | — | accessibility id | `Xem ảnh 1/1` | ⚠️ Inferred | mcp-log TC-USR-025 | — |

## Navigation Flow (chỉ flow đã đi qua bằng MCP)

| From | Trigger | To | MCP-verified |
|---|---|---|---|
| FoxPro "Chức năng" | tap `text("FoxEco")` | FoxEco Trang chủ | TC-USR-001 step 2 · TC-USR-042 step 8 |
| FoxEco Trang chủ | tap `Quay lại` | FoxPro "Chức năng" | TC-USR-001 · TC-USR-042 step 7 |
| bất kỳ tab | tap `Cá nhân` | Cá nhân | TC-USR-002 step 2 |
| Cá nhân | tap `profile-menu-activity` | Đơn của tôi (tab "Đang diễn ra" active) | TC-USR-009 step 3 |
| Cá nhân | tap `profile-menu-gifts` | Quà đã nhận | TC-USR-010 step 3 |
| Cá nhân | tap `profile-menu-editProfile` | Cập nhật thông tin *(bottom nav ẩn)* | TC-USR-014 step 3 |
| Cập nhật thông tin | tap `Lưu thay đổi` *(hợp lệ)* | **→ Cá nhân** *(⚠️ KHÔNG ở lại — bug TC-USR-015)* | TC-USR-015 step 8 |
| Cập nhật thông tin | tap `Lưu thay đổi` *(SĐT không hợp lệ)* | ở lại + thông báo lỗi dưới field | TC-USR-017/018/020/023 |
| Cập nhật thông tin | tap `Quay lại` *(có thay đổi chưa lưu)* | → Cá nhân **ngay, không hộp thoại** | TC-USR-045 step 8 |
| tab `Đăng tin` | tap `descriptionStartsWith("Tôi cần gửi hàng")` | Wizard Bước 1/3 | TC-USR-025 step 2 |
| Wizard Bước 1/3 | tap `Tiếp theo` *(đủ ảnh + 4 chip)* | Bước 2/3 | TC-USR-025 |
| Wizard Bước 2/3 | tap `Tiếp theo` *(đủ người nhận + ≥1 buổi)* | Bước 3/3 | TC-USR-025 |
| Wizard Bước 3/3 | tick điều khoản → tap `Đăng tin ngay` | Popup "Đăng tin thành công!" | TC-USR-025, TC-USR-026 |
| Popup thành công | tap `Theo dõi đơn` | Theo dõi đơn | TC-USR-025 step 3 |
| Theo dõi đơn | tap `Chỉnh sửa` | Wizard Bước 1/3 *(mode edit, giá trị của ĐƠN)* | TC-USR-025 step 13 |

## Thống kê

| Pages visited | Elements captured | Verified ✅ | Inferred ⚠️ | NOT FOUND 🚫 |
|---|---|---|---|---|
| **9** (FoxPro Chức năng · Trang chủ · Cá nhân · Đơn của tôi · Quà đã nhận · Cập nhật thông tin · Wizard ×3 · Theo dõi đơn) | **77** | **45** | **26** | **6** |

> 🚫 NOT FOUND gồm **4 ca đúng kỳ vọng** (badge hạng · Điểm ECO/uy tín/CO₂ · email trên màn Cá nhân · bottom nav trên màn Cập nhật) và **2 ca SAI kỳ vọng ⇒ bug** (banner "Đã lưu thông tin của bạn" · icon khiên cạnh field Email).
