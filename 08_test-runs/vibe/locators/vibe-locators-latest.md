# Vibe Locators — LATEST (tích lũy xuyên run)

> ★ **`implement-automation` đọc FILE NÀY.** Pointer không mang ngày; snapshot khi đóng version → `vibe-locators-v[X].md`.
> Cập nhật lần cuối: **VR-002** (2026-09-18) · module **ORD** · platform **mobile (Appium MCP / UiAutomator2)**
> App: `com.hrisproject.stag` (host FoxPro → FoxEco)
>
> **Lịch sử merge**
> | Run | Ngày | Module | Elements | ✅ | ⚠️ | 🚫 |
> |---|---|---|--:|--:|--:|--:|
> | VR-001 | 2026-09-18 | USR | 77 | 45 | 26 | 6 |
> | VR-002 | 2026-09-18 | ORD | 62 | 47 | 10 | 5 |
>
> ⚠️ **VR-001 là run vibe ĐẦU TIÊN của dự án** ⇒ phần dưới = hợp nhất nguyên vẹn `VR-001-USR-2026-09-18/vibe-locators.md`
> (tỷ lệ hấp thụ **77/77 = 100%**, không có run trước để gộp).
>
> 🔴 **VR-002 (module ORD) gộp NGUYÊN VẸN ở phần cuối file** (§"MERGE VR-002") — hấp thụ **62/62 = 100%**.
> Bẫy kỹ thuật **T6–T10** là **mới**, đọc cùng T1–T5. **5 đính chính** với phần VR-001, áp dụng khi implement:
> | # | Mục VR-001 | Đính chính từ VR-002 |
> |---|---|---|
> | 1 | `value-tier-chip-option-*` ghi 🚫 NOT FOUND | **resolve được** qua `-android uiautomator resourceId(...)`; chỉ strategy `id` là fail (**T6**) |
> | 2 | Nút thêm ảnh = `accessibility id "0/5"` | ⛔ desc **đổi theo bộ đếm** (`1/5`, `2/5`…) ⇒ dùng `resourceId("multi-photo-add-button")` (**T7**) |
> | 3 | *(chưa ghi)* nút xoá ảnh | `resourceId("multi-photo-remove-<N>")`; `N=3` **không render** (bug trần ảnh, **T10**) |
> | 4 | Wizard B1 "Tiếp theo" enable khi đủ 4 chip | **đo lại**: cần **giá trị + trọng lượng + kích thước + ≥1 ẢNH** (ảnh là bắt buộc từ v1.1) |
> | 5 | *(chưa ghi)* cách rời ô trong wizard | ⛔ **KHÔNG** dùng `appium_mobile_keyboard(hide)` — nó gửi BACK, ở bước 1 = thoát wizard + mất draft (**T9**) |

---


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

---

# MERGE VR-002 — module ORD (2026-09-18)

> Nguồn: `VR-002-ORD-2026-09-18/vibe-locators.md` — gộp nguyên vẹn, giữ nguyên mark ✅/⚠️/🚫.
> Màn **Wizard Bước 1/3** và **Bước 2/3** ở đây **chi tiết hơn** bản VR-002 phía trên của VR-001 ⇒ khi 2 phần lệch nhau, **lấy bản VR-002 này**.

## 🔴 5 BẪY KỸ THUẬT MỚI phát hiện ở VR-002 (bổ sung T1–T5 của VR-001)

| # | Bẫy | Bằng chứng trong run này | Cách làm đúng |
|---|---|---|---|
| **T6** | `resource-id` của React Native **không resolve** qua strategy `id` nhưng **resolve** qua `-android uiautomator resourceId(...)` | `id "multi-photo-remove-0"` → NOT FOUND · `new UiSelector().resourceId("multi-photo-remove-0")` → OK | Với mọi rid dạng RN (không có prefix package) **luôn** dùng `-android uiautomator` + `resourceId()` |
| **T7** | **Nút thêm ảnh có `content-desc` = CHÍNH BỘ ĐẾM** (`0/5` → `1/5` → …) ⇒ locator theo desc **đổi theo state** | `accessibility id "0/5"` OK khi chưa có ảnh, NOT FOUND sau khi thêm 1 ảnh | Dùng `resourceId("multi-photo-add-button")` (bền), chỉ dùng `"N/5"` khi **cố ý assert bộ đếm** |
| **T8** | Element **ngoài viewport thì KHÔNG resolve** (kể cả accessibility id đúng) | `accessibility id "0/5"` NOT FOUND khi khối ảnh đang cuộn khỏi màn; `scroll_to_element` xong thì OK | Trước khi find element ở cuối form ⇒ `appium_gesture(action=scroll_to_element)` |
| **T9** | `appium_mobile_keyboard(action=hide)` **gửi BACK** ⇒ ở bước 1 wizard = **thoát wizard + mất dữ liệu** | mất draft giữa lô 3 (xem `vibe-log.md §F6`) | ⛔ Không dùng `hide` để "rời ô" trong wizard — tap vùng trống, hoặc get_text trực tiếp |
| **T10** ♻️ **ĐÃ ĐÍNH CHÍNH 2026-09-18 chiều** | Dải ảnh khối `ẢNH HÀNG` là **lazy horizontal list**: phần tử ngoài viewport **không được compose** ⇒ **không tồn tại trong cây**. ⛔ **Bản T10 cũ ghi SAI** (*"dải không cuộn ngang, không render phần tử thứ ≥4"*) và đã làm dựng lên một ứng viên bug ma (**B3 — trần ảnh 4/5**) | Recheck: `adb shell input swipe 950 1836 150 1836 500` **cuộn tới cuối dải ngay lần đầu**; app nhận **đủ 5 ảnh**; `multi-photo-remove-3`/`-4` có thật và xoá được sau khi cuộn. Gesture của lượt 1 không ăn là do **tham số/vùng swipe**, ⛔ không phải dải không cuộn | **Luôn cuộn dải rồi mới assert.** ⛔ Tuyệt đối không suy *"không tìm thấy node" = "chức năng không có"*. Lưu ý kèm **T7**: bộ đếm `n/5` là `content-desc` của **tile thêm ảnh ở CUỐI dải** ⇒ ở mức 5/5 tile bị ẩn đúng `BR18-02` nên **không còn bộ đếm nào** — QC chốt 2026-09-18 đây là **hành vi đúng**, Expected `TC-ORD-070` đã sửa theo, ⛔ không phải bug |

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
| ↳ `multi-photo-remove-3` | — | -android uiautomator | *(không render — xem **T10**)* | 🚫 NOT FOUND | mcp-log TC-ORD-070 | TC-ORD-070/071 |
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

---

# MERGE VR-003 — module USR, phần còn nợ (2026-09-18)

> Nguồn: `VR-003-USR-2026-09-18/vibe-locators.md`. Tài khoản `00002352` (tài khoản trắng, chưa từng lưu hồ sơ).
> **Hấp thụ 19/19 = 100%.** Phiên này chạm 5 màn: 2 của FoxEco (đã có ở VR-001, **xác nhận lại locator còn đúng**) + **3 màn HRIS/FoxPro mới**.

## 🔴 4 BẪY KỸ THUẬT MỚI ở VR-003 (bổ sung T1–T5 của VR-001 và T6–T10 của VR-002)

| # | Bẫy | Hệ quả nếu bỏ qua |
|---|---|---|
| **T11** | 🔴 **Field rỗng vẫn trả `text` = chuỗi HINT.** `(//android.widget.EditText)[1]` của màn "Cập nhật thông tin" trả `09xx xxx xxx` khi rỗng; chỉ `showing-hint="true"` trong page source mới phân biệt được. | Assert `text != ""` hoặc `text is not None` sẽ **PASS OAN** trên field rỗng. Đây đúng là chỗ `TC-USR-040/043` dễ bị đọc sai thành PASS. **Luôn assert bằng `showing-hint`, không bằng `text`.** |
| **T12** | 2 field của màn "Cập nhật thông tin" **không có `resource-id`, không có `content-desc`** ⇒ chỉ định vị được bằng **thứ tự EditText** (`[1]` = SĐT, `[2]` = Địa chỉ). | Thêm 1 field ở giữa là gãy toàn bộ. Nên xin dev gắn `testID` trước khi automate màn này. |
| **T13** | Đường quay lại FoxEco sau khi thoát sang FoxPro: **back → back → tap `Chức năng` → tap `FoxEco`**. Không có deeplink. | TC nào cần thoát/mở lại app (vd `TC-USR-042`) phải đi đủ chuỗi này, không rút gọn được. |
| **T14** | Hồ sơ HRIS mobile **không phơi trường "địa chỉ làm việc / văn phòng"** của chính người dùng (đã kiểm cả *Thông tin* lẫn *Quá trình làm việc*). | Không lấy được oracle địa chỉ VP từ app ⇒ phải lấy từ `00_input/v1.1/datatest` hoặc hỏi QC/BA. Đừng phí phiên đi tìm trong app. |

## Screen: FoxPro — Cá nhân (hồ sơ HRIS) · **MỚI**

| Element | Strategy | Value | Action | ✅ |
|---|---|---|---|:--:|
| Tab "Cá nhân" (bottom nav FoxPro) | -android uiautomator | `new UiSelector().text("Cá nhân")` | tap | ✅ |
| Mục "Thông tin cá nhân" | -android uiautomator | `new UiSelector().text("Thông tin cá nhân")` | tap | ✅ |
| Thẻ "Thông tin" | -android uiautomator | `new UiSelector().text("Thông tin")` | tap | ✅ |
| Thẻ "Quá trình làm việc" | -android uiautomator | `new UiSelector().text("Quá trình làm việc")` | tap | ✅ |
| Thẻ "Người thân" / "Trình độ" / "Hồ sơ" | -android uiautomator | `new UiSelector().text("<nhãn>")` | — | ⚠️ Inferred |

## Screen: FoxPro — Thông tin cá nhân → **Thông tin** · **MỚI** *(nguồn oracle HRIS)*

> Bảng label → value, **không có `resource-id`**; đọc bằng `text` của TextView kế bên nhãn.

| Nhãn có trên màn | Ghi chú dùng làm oracle |
|---|---|
| `Mã nhân viên` · `Điện thoại` · `Ngày sinh` · `Giới tính` · `Ngày vào Cty` · `Level cán bộ` · `Địa chỉ` · `Số CMND/CCCD` | ✅ **`Điện thoại` = oracle SĐT HRIS** cho `TC-USR-043`. ⛔ **Không chép giá trị vào repo/evidence** (`Project_rule §Execution Rules`). |
| `IP Phone` · `Nơi sinh` · `Địa chỉ thường trú` · `Nơi ở hiện nay` · `Số định danh` · `Ngày cấp/Nơi cấp số định danh` | Có nhãn nhưng **giá trị rỗng** trên tài khoản `00002352` |
| ⛔ **KHÔNG có** nhãn "địa chỉ làm việc"/"văn phòng" | → T14 |

## Screen: FoxPro — **Quá trình làm việc** · **MỚI**

| Element | Strategy | Value | ✅ |
|---|---|---|:--:|
| Đơn vị công tác | -android uiautomator | `new UiSelector().textContains("Công ty Cổ phần Viễn thông FPT/")` | ✅ |
| Nhãn `Vị trí công việc:` · `Chức danh:` | -android uiautomator | `new UiSelector().text("<nhãn>")` | ✅ |

## ⚠️ Đính chính cho các phiên sau

| Mục | Đính chính |
|---|---|
| Icon "Hồ sơ nhân viên" ở màn **Chức năng** | **KHÔNG phải hồ sơ của mình** — đó là danh sách nhân viên cấp dưới (tài khoản `00002352` thấy *"Bạn không có danh sách nhân viên"*). Hồ sơ cá nhân nằm ở **bottom nav `Cá nhân` → `Thông tin cá nhân`**. |
| `accessibility id "Lưu thay đổi"` · `profile-menu-editProfile` · `profile-stat-gifts` · nav `Trang chủ`/`Cá nhân` | ✅ **Xác nhận lại ở VR-003 — vẫn đúng** trên build 2026-09-18 |

## Thống kê VR-003

| Screens visited | Elements captured | Verified ✅ | Inferred ⚠️ | NOT FOUND 🚫 |
|---|---|---|---|---|
| **5** (2 FoxEco xác nhận lại + 3 HRIS mới) | **19** | **17** | **1** | **1** |

> 🚫 NOT FOUND duy nhất là **đúng kỳ vọng**: `textContains("Đã lưu")` sau khi lưu — app cố ý không còn banner (`TC-USR-027` PASS).
