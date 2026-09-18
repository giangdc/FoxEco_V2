# Vibe Locators — VR-003 — module USR — 2026-09-18

> Mọi locator dưới đây lấy qua **Appium MCP** (`appium_get_page_source` / `appium_find_element`), chuỗi ghi **nguyên văn** MCP trả về.
> ✅ Verified = MCP tìm thấy **và** action chạy được **trong run này**. 🚫 NOT FOUND = MCP tìm không ra (dùng làm assert-absent).

## 1. Màn "Cá nhân" (FoxEco)

| Element | Strategy | Value | Action | Verified | TC | MCP call ref |
|---|---|---|---|:--:|---|---|
| Tab bottom nav "Trang chủ" | accessibility id | `Trang chủ` | tap | ✅ | 006 | A1/A2 |
| Tab bottom nav "Cá nhân" | accessibility id | `Cá nhân` | tap | ✅ | 006, 027 | A3/A4 |
| Chỉ số "đơn đã giúp" — nhãn | -android uiautomator | `new UiSelector().text("đơn đã giúp")` | read | ✅ | 006 | A5 |
| Chỉ số "quà đã nhận" — container | accessibility id | `profile-stat-gifts` | read | ✅ | 006 | A5 |
| Menu "Đơn của tôi" | accessibility id | `profile-menu-activity` | — | ✅ | — | A5 |
| Menu "Quà đã nhận" | accessibility id | `profile-menu-gifts` | — | ✅ | — | A5 |
| Menu "Cập nhật thông tin cá nhân" | accessibility id | `profile-menu-editProfile` | tap | ✅ | 027, 040, 043 | A6 |

## 2. Màn "Cập nhật thông tin" (FoxEco)

| Element | Strategy | Value | Action | Verified | TC | MCP call ref |
|---|---|---|---|:--:|---|---|
| Nút back | accessibility id | `Quay lại` | — | ⚠️ Inferred | — | A7 (thấy trong tree, chưa tap trong run này) |
| Field "Số điện thoại mặc định" | xpath | `(//android.widget.EditText)[1]` | tap · set_value · get_attribute | ✅ | 027, 043 | Pha B |
| Field "Địa chỉ mặc định" | xpath | `(//android.widget.EditText)[2]` | tap · get_attribute | ✅ | 040 | Pha B |
| Nút "Lưu thay đổi" | accessibility id | `Lưu thay đổi` | tap | ✅ | 027 | Pha B |
| Banner "Đã lưu…" | -android uiautomator | `new UiSelector().textContains("Đã lưu")` | find | 🚫 NOT FOUND | 027 | Pha B — assert-absent, đúng kỳ vọng bản sửa 2026-09-18 |

## 3. FoxPro / HRIS (ngoài FoxEco — dùng lấy oracle + điều hướng)

| Element | Strategy | Value | Action | Verified | Dùng cho |
|---|---|---|---|:--:|---|
| Tab "Chức năng" | -android uiautomator | `new UiSelector().text("Chức năng")` | tap | ✅ | quay lại FoxEco |
| Icon "FoxEco" | -android uiautomator | `new UiSelector().text("FoxEco")` | tap | ✅ | mở FoxEco |
| Tab "Cá nhân" (FoxPro) | -android uiautomator | `new UiSelector().text("Cá nhân")` | tap | ✅ | vào hồ sơ HRIS |
| Mục "Thông tin cá nhân" | -android uiautomator | `new UiSelector().text("Thông tin cá nhân")` | tap | ✅ | oracle |
| Thẻ "Thông tin" | -android uiautomator | `new UiSelector().text("Thông tin")` | tap | ✅ | oracle SĐT HRIS |
| Thẻ "Quá trình làm việc" | -android uiautomator | `new UiSelector().text("Quá trình làm việc")` | tap | ✅ | tìm địa chỉ làm việc |
| Mục "Hồ sơ nhân viên" (Chức năng) | -android uiautomator | `new UiSelector().text("Hồ sơ nhân viên")` | tap | ✅ | ⚠️ **không phải hồ sơ của mình** — là danh sách nhân viên cấp dưới ("Bạn không có danh sách nhân viên") |

## 4. 🔴 BẪY KỸ THUẬT (bổ sung cho `§5` của `vibe-locators-latest.md`)

| # | Bẫy | Hệ quả nếu bỏ qua |
|---|---|---|
| T1 | 2 field của màn "Cập nhật thông tin" **không có `resource-id` và không có `content-desc`** ⇒ chỉ định vị được bằng **thứ tự EditText**. | Automation phải dựa vào thứ tự; thêm 1 field mới ở giữa là gãy hết. Nên xin dev gắn `testID`. |
| T2 | Field rỗng vẫn trả `text` = **chuỗi hint** (`09xx xxx xxx`). Phải đọc thêm `showing-hint="true"` trong page source mới biết là rỗng. | Assert `text != ""` sẽ **PASS oan** trên field rỗng — đây đúng là chỗ `TC-USR-040/043` dễ bị đọc sai. |
| T3 | Đường về FoxEco sau khi thoát: **back → back → `Chức năng` → `FoxEco`**, không có deeplink. | Test nào cần thoát/mở lại app phải đi lại đủ chuỗi này. |
| T4 | Hồ sơ HRIS mobile **không phơi trường "địa chỉ làm việc / văn phòng"** cho chính người dùng. | Không lấy được oracle địa chỉ VP từ app — phải lấy từ `datatest` hoặc hỏi QC/BA. |
