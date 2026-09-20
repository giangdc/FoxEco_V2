# Vibe Locators — v1.1 — VR-011 — 2026-09-19 — module GIFT

> Captured via **Appium MCP (UiAutomator2)** during this run.
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md` (audit trail) · Platform: mobile · Host app `com.hrisproject.stag`
>
> 🔑 **Điểm quan trọng cho `implement-automation`:** màn **"Tặng quà"** có `resource-id` **ổn định, không kèm package** (`gift-cell-*`, `gift-confirm-btn`) — nhưng ⚠️ **strategy `id` KHÔNG tìm được** chúng (Appium `id` ghép package prefix). ⇒ dùng **`accessibility id`** (content-desc trùng tên quà) hoặc `-android uiautomator` + `resourceIdMatches`.

## Screen: Tặng quà *(mở bằng cách tap card đơn `Hoàn thành` có hint `Chạm để tặng quà`)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Nút quay lại (header) | tap | accessibility id | `Quay lại` | ✅ | Pha B `TC-GIFT-010` | TC-GIFT-010 |
| Ô quà "Bông hoa" | tap | accessibility id | `Bông hoa` | ✅ | Pha B `TC-GIFT-003` | TC-GIFT-003, TC-GIFT-005 |
| Ô quà "Ly cà phê" | tap | accessibility id | `Ly cà phê` | ✅ | Pha B `TC-GIFT-005` | TC-GIFT-005 |
| Ô quà "Gấu bông" | verify_visible | accessibility id | `Gấu bông` | ✅ | A2 | TC-GIFT-002 |
| Ô quà "Vương miện" | verify_visible | accessibility id | `Vương miện` | ✅ | A2 | TC-GIFT-002 |
| Ô quà (đếm số lượng) | verify_visible | -android uiautomator | `new UiSelector().resourceIdMatches(".*gift-cell-.*").instance(N)` | ✅ | Pha B `TC-GIFT-002` | TC-GIFT-002 |
| Nút "Xác nhận tặng quà" | tap | accessibility id | `Xác nhận tặng quà` | ✅ | Pha B `TC-GIFT-003` | TC-GIFT-003, TC-GIFT-005 |
| *(rid của 4 ô quà)* | — | *(resource-id đọc từ page source)* | `gift-cell-flower` · `gift-cell-coffee` · `gift-cell-teddy` · `gift-cell-crown` | ✅ | A2 | TC-GIFT-002 |
| *(rid nút xác nhận)* | — | *(resource-id đọc từ page source)* | `gift-confirm-btn` — `enabled=false` khi **chưa chọn quà**, `enabled=true` sau khi chọn | ✅ | A2 | TC-GIFT-002, TC-GIFT-003 |
| Ô quà qua strategy `id` | *(thử)* | id | `gift-cell-flower` | 🚫 **NOT FOUND** | Pha B `TC-GIFT-003` | — |

## Screen: Popup "Đã gửi lời cảm ơn!" *(modal sau khi xác nhận tặng quà)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Thân popup | get_text | -android uiautomator | `new UiSelector().textContains("Cảm ơn của bạn đã được gửi")` → trả về `"Món quà và lời cảm ơn của bạn đã được gửi đến người vận chuyển."` | ✅ | Pha B `TC-GIFT-003` | TC-GIFT-003 |
| Nút "Về trang chủ" | tap | -android uiautomator | `new UiSelector().text("Về trang chủ")` | ✅ | Pha B `TC-GIFT-003` | TC-GIFT-003, TC-GIFT-005 |
| Nút "Về trang chủ" qua a11y id | *(thử)* | accessibility id | `Về trang chủ` | 🚫 **NOT FOUND** | Pha B `TC-GIFT-003` | — |

> ⚠️ **Popup KHÔNG đóng được bằng `back`** — `back` chỉ pop màn nền, popup vẫn nổi. Automation phải tap `Về trang chủ`.

## Screen: Đơn của tôi — tab "Đã hoàn thành"

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Tab "Đang diễn ra" | tap | -android uiautomator | `new UiSelector().text("Đang diễn ra")` | ✅ | A1 | TC-GIFT-013 |
| Tab "Đã hoàn thành" | tap | -android uiautomator | `new UiSelector().text("Đã hoàn thành")` | ✅ | A1 | TC-GIFT-001…005 |
| Card đơn (theo loại hàng) | tap | -android uiautomator | `new UiSelector().text("<loại hàng>").instance(N)` | ✅ | Pha B `TC-GIFT-001` | TC-GIFT-001, 003, 005, 010 |
| Hint "chưa tặng quà" | verify_visible | -android uiautomator | `new UiSelector().text("Chạm để tặng quà")` | ✅ | A1 | TC-GIFT-001, 010 |
| Hint "đã tặng quà" | verify_visible | -android uiautomator | `new UiSelector().text("Đã tặng quà")` | ✅ | A1 | TC-GIFT-005 |
| Badge trạng thái đơn | verify_visible | -android uiautomator | `new UiSelector().text("Hoàn thành")` · `text("Hết hạn")` | ✅ | A1 | TC-GIFT-013 |

> ⚠️ **Bẫy cuộn:** `appium_gesture(action=scroll, direction=up)` và `swipe direction=down` **KHÔNG cuộn ngược** được danh sách này (báo success nhưng page source không đổi). Dùng **swipe toạ độ tường minh** (`x=360,y=400 → endX=360,endY=1050`) mới lên được đầu danh sách.

## Screen: Theo dõi đơn *(chỉ mở được khi đơn KHÔNG còn chờ tặng quà)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Tiêu đề màn | verify_visible | -android uiautomator | `new UiSelector().text("Theo dõi đơn")` | ✅ | Pha B `TC-GIFT-005` | TC-GIFT-005 |
| Nút cuối màn — đã tặng quà | tap | -android uiautomator | `new UiSelector().text("Bạn đã đánh giá")` | ✅ | Pha B `TC-GIFT-005` | TC-GIFT-005 |
| Trạng thái disable của nút trên | verify | xpath | `//android.widget.TextView[@text="Bạn đã đánh giá"]/ancestor::*[@clickable="true"][1]` → 🚫 NOT FOUND ⇒ **không clickable ⇒ disable** | ✅ | Pha B `TC-GIFT-005` | TC-GIFT-005 |
| Nút cuối màn — đơn hoàn thành (không tặng quà) | verify_visible | -android uiautomator | `new UiSelector().textContains("Đơn đã hoàn thành")` | ✅ | A1 | *(recon)* |
| Nút "Huỷ đơn" (đơn Đã ghép) | verify_visible | -android uiautomator | `new UiSelector().text("Huỷ đơn")` | ✅ | Pha B `TC-GIFT-014` | TC-GIFT-014 |
| Nút "✓ Cảm ơn người vận chuyển" *(theo `KB-GIFT-01`)* | *(thử)* | -android uiautomator | `new UiSelector().textContains("Cảm ơn người vận chuyển")` → **chỉ khớp TextView phụ đề** của màn "Tặng quà", ⛔ không có nút nào | 🚫 **NOT FOUND** | Pha B `TC-GIFT-001` | TC-GIFT-001 |

## Screen: Cá nhân (FoxEco)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Tab "Cá nhân" (bottom nav) | tap | -android uiautomator | `new UiSelector().text("Cá nhân")` | ✅ | Pha B `TC-GIFT-007` | TC-GIFT-007, 009, 006 |
| Mục menu "Quà đã nhận" | tap | -android uiautomator | `new UiSelector().text("Quà đã nhận")` | ✅ | Pha B `TC-GIFT-007` | TC-GIFT-006, 007, 009 |
| Mục menu "Đơn của tôi" | verify_visible | -android uiautomator | `new UiSelector().text("Đơn của tôi")` | ✅ | Pha B `TC-GIFT-009` | TC-GIFT-009 |
| Mục menu "Cập nhật thông tin cá nhân" | verify_visible | -android uiautomator | `new UiSelector().text("Cập nhật thông tin cá nhân")` | ✅ | Pha B `TC-GIFT-009` | TC-GIFT-009 |

> ⚠️ Menu có **3 mục**, ⛔ không phải 2 như `TC-GIFT-009` Expected đang ghi.

## Screen: Quà đã nhận

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Nút quay lại (header) | tap | accessibility id | `Quay lại` | ✅ | Pha B `TC-GIFT-009` | TC-GIFT-009 |
| Tổng quà đã nhận | get_text | -android uiautomator | `new UiSelector().textContains("<N> món")` | ✅ | Pha B `TC-GIFT-006` | TC-GIFT-006 |
| Ô đếm 1 loại quà | verify_visible | -android uiautomator | `new UiSelector().text("Ly cà phê")` · `text("Vương miện")` · `text("Gấu bông")` | ✅ | Pha B `TC-GIFT-006` | TC-GIFT-006, 007 |
| Ô đếm loại quà có count = 0 | *(thử)* | -android uiautomator | `new UiSelector().text("Bông hoa")` / `text("Gấu bông")` trên acc chỉ có 2 loại | 🚫 **NOT FOUND** *(đúng kỳ vọng — loại count = 0 bị ẩn)* | Pha B `TC-GIFT-006` | TC-GIFT-006 |
| Khối lịch sử | verify_visible | -android uiautomator | `new UiSelector().text("LỊCH SỬ NHẬN QUÀ")` | ✅ | Pha B `TC-GIFT-007` | TC-GIFT-007 |

## Screen: Thông báo (FoxEco)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Icon chuông (header Trang chủ) | tap | *(toạ độ `651,128` — ⚠️ chưa có locator)* | — | ⚠️ **Inferred** | Pha B `TC-GIFT-012` | TC-GIFT-012 |
| Dòng thông báo quà cảm ơn | tap · get_text | -android uiautomator | `new UiSelector().textContains("mở Trang cá nhân để xem").instance(0)` | ✅ | Pha B `TC-GIFT-012` | TC-GIFT-012 |
| Nội dung `NTF-07` (nguyên văn app) | get_text | *(giá trị trả về)* | `Bạn nhận được một món quà cảm ơn — mở Trang cá nhân để xem` *(⛔ **không có** emoji 🎁)* | ✅ | Pha B `TC-GIFT-012` | TC-GIFT-012 |

## Screen: FoxPro — đăng xuất / đăng nhập *(dùng lại của `USR-accounts.md §0b`, re-verify trong run này)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Mục "Đăng xuất" (FoxPro → Cá nhân) | scroll_to_element + tap | -android uiautomator | `new UiSelector().text("Đăng xuất")` | ✅ | Pha B `(đổi acc ×2)` | TC-GIFT-012, 006 |
| Nút xác nhận dialog | tap | -android uiautomator | `new UiSelector().text("Đồng ý")` | ✅ | Pha B `(đổi acc ×2)` | TC-GIFT-012, 006 |
| Ô email đăng nhập | set_value | -android uiautomator | `new UiSelector().text("Nhập email đăng nhập")` | ✅ | Pha B `(đổi acc ×2)` | TC-GIFT-012, 006 |
| Nút "NHẬN MÃ OTP" | tap | -android uiautomator | `new UiSelector().text("NHẬN MÃ OTP")` | ✅ | Pha B `(đổi acc ×2)` | TC-GIFT-012, 006 |
| Nút "ĐĂNG NHẬP" (màn Xác nhận OTP) | tap | -android uiautomator | `new UiSelector().text("ĐĂNG NHẬP")` | ✅ | Pha B `(đổi acc ×2)` | TC-GIFT-012, 006 |
| Icon FoxEco (FoxPro → Chức năng) | scroll_to_element + tap | -android uiautomator | `new UiSelector().text("FoxEco")` | ✅ | Pha B `(đổi acc ×2)` | TC-GIFT-012, 006 |

## Navigation Flow (chỉ ghi luồng đã đi thật qua MCP)

| From | Trigger | To | MCP-verified |
|------|---------|-----|--------------|
| Đơn của tôi → Đã hoàn thành | tap card có hint `Chạm để tặng quà` | **Tặng quà** *(⛔ KHÔNG qua "Theo dõi đơn")* | TC-GIFT-001 step 3 |
| Đơn của tôi → Đã hoàn thành | tap card **không** có hint / có hint `Đã tặng quà` | **Theo dõi đơn** | TC-GIFT-005 step 5 · recon |
| Tặng quà | tap `Quay lại` | **Đơn của tôi → Đã hoàn thành** *(reset vị trí cuộn về đầu)* | TC-GIFT-010 step 4 |
| Tặng quà | chọn quà → tap `Xác nhận tặng quà` | **popup "Đã gửi lời cảm ơn!"** *(gửi ngay, không có bước chờ)* | TC-GIFT-003 step 5 |
| popup "Đã gửi lời cảm ơn!" | tap `Về trang chủ` | **FoxEco Trang chủ** | TC-GIFT-003 |
| popup "Đã gửi lời cảm ơn!" | `back` | **popup GIỮ NGUYÊN**, chỉ màn nền bị pop | TC-GIFT-005 step 4 |
| Quà đã nhận | tap `Quay lại` | **Cá nhân** | TC-GIFT-009 step 3 |
| Thông báo | tap thông báo quà cảm ơn | **Quà đã nhận** *(⛔ KHÔNG phải "Cá nhân" như `NTF-07` nói)* | TC-GIFT-012 step 4 |
