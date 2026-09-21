# Vibe Locators — v1.1 — VR-017 — 2026-09-21

> Captured via Appium MCP (UiAutomator2) during this run · Platform: mobile (Android, FoxPro host → FoxEco)
> Mark legend: ✅ Verified (MCP find+action OK trong run này) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md`

## Page: FoxEco — Đơn của tôi (nav `Hoạt động`)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Nav "Hoạt động" | tap | -android uiautomator | `new UiSelector().text("Hoạt động")` | ✅ | A2 | TC-ACT-001, 012, 014, 016 |
| Tiêu đề màn | verify_visible | page source text | `Đơn của tôi` | ✅ | A3 | TC-ACT-001 |
| Tab con "Đang diễn ra" | tap | -android uiautomator | `new UiSelector().text("Đang diễn ra")` | ✅ | TC-ACT-015 | TC-ACT-001, 015, 017 |
| Tab con "Đã hoàn thành" | tap | -android uiautomator | `new UiSelector().text("Đã hoàn thành")` | ✅ | TC-ACT-005 | TC-ACT-005, 008, 013, 014, 015, 016, 017 |
| Badge "Đã huỷ" | verify_visible | -android uiautomator | `new UiSelector().text("Đã huỷ")` | ✅ | TC-ACT-015 | TC-ACT-015 |
| Dòng lý do card Hết hạn | get_text | -android uiautomator | `new UiSelector().textStartsWith("Không có ai nhận mang giúp")` | ✅ | TC-ACT-008 | TC-ACT-008 |
| Danh sách đơn (khi có dữ liệu) | scroll | class | `android.widget.ScrollView` bounds `[0,276][720,1108]` `scrollable="true"` | ✅ | A3 | TC-ACT-005, 013, 017 (đối chứng) |
| Phần tử cuộn được khi tab RỖNG | verify_absent | -android uiautomator | `new UiSelector().scrollable(true)` | 🚫 NOT FOUND | TC-ACT-017 | TC-ACT-017 — **kết quả kiểm**, không phải locator hỏng |
| Empty state tab "Đang diễn ra" — tiêu đề | verify_visible | -android uiautomator | `new UiSelector().text("Không có đơn đang thực hiện")` | ✅ | TC-ACT-016 | TC-ACT-012, 016 |
| Empty state tab "Đang diễn ra" — CTA | verify_visible | page source text | `Đăng tin gửi hàng` (clickable `[225,658][496,726]`) | ✅ | A4 | TC-ACT-012 |
| Empty state tab "Đã hoàn thành" — tiêu đề | verify_visible | page source text | `Chưa có đơn hoàn tất` | ✅ | TC-ACT-014 | TC-ACT-014, 018 |

## Page: FoxEco — thanh tab dưới (dùng chung)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Nav "Trang chủ" | tap | -android uiautomator | `new UiSelector().text("Trang chủ")` | ✅ | TC-ACT-016 | TC-ACT-016, 018 |
| Nav "Bảng tin" | tap | -android uiautomator | `new UiSelector().text("Bảng tin")` | ✅ | TC-ACT-016 | TC-ACT-016 |
| Nav "Đăng tin" (nút giữa) | tap | -android uiautomator | `new UiSelector().text("Đăng tin")` | ✅ | TC-ACT-016 | TC-ACT-016 |
| Nav "Cá nhân" (FoxEco) | tap | -android uiautomator | `new UiSelector().text("Cá nhân")` | ✅ | TC-ACT-016 | TC-ACT-016 |
| Xác nhận màn Trang chủ | verify_visible | -android uiautomator | `new UiSelector().textContains("Đóng góp của bạn")` | ✅ | TC-ACT-016 | TC-ACT-016 |
| Xác nhận màn Cá nhân | verify_visible | -android uiautomator | `new UiSelector().text("Quà đã nhận")` | ✅ | TC-ACT-016 | TC-ACT-016 |
| Xác nhận màn Đăng tin | verify_visible | -android uiautomator | `new UiSelector().text("Đăng tin mới")` | ✅ | TC-ACT-016 | TC-ACT-016 |

## Page: FoxPro host — đăng xuất / đăng nhập

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Tab "Chức năng" | tap | -android uiautomator | `new UiSelector().text("Chức năng")` | ✅ | A1 | setup |
| Icon FoxEco | scroll_to_element + tap | -android uiautomator | `new UiSelector().textContains("FoxEco")` | ✅ | A1 | setup |
| Tab "Cá nhân" (FoxPro) | tap | -android uiautomator | `new UiSelector().text("Cá nhân")` | ✅ | A5 | setup |
| Nút "Đăng xuất" | scroll_to_element + tap | -android uiautomator | `new UiSelector().text("Đăng xuất")` | ✅ | A5 | setup |
| Popup "Đồng ý" | tap | -android uiautomator | `new UiSelector().text("Đồng ý")` | ✅ | A5 | setup (cả popup đăng xuất lẫn popup lỗi mạng `T-ASN-07`) |
| Ô email | set_value | -android uiautomator | `new UiSelector().text("Nhập email đăng nhập")` | ✅ | A5 | setup |
| Nút "NHẬN MÃ OTP" | tap | -android uiautomator | `new UiSelector().text("NHẬN MÃ OTP")` | ✅ | A5 | setup |
| Nút "ĐĂNG NHẬP" | tap | -android uiautomator | `new UiSelector().text("ĐĂNG NHẬP")` | ✅ | A5 | setup |

## Navigation Flow (MCP-traversed)

| From | Trigger | To | MCP-verified |
|------|---------|-----|--------------|
| FoxEco Trang chủ | tap `Hoạt động` | Đơn của tôi, tab `Đang diễn ra` active | TC-ACT-001 |
| Đơn của tôi (tab bất kỳ) | tap `Trang chủ`/`Bảng tin`/`Cá nhân` rồi tap `Hoạt động` | Đơn của tôi, **luôn về tab `Đang diễn ra`** | TC-ACT-016 |
| Đơn của tôi (tab `Đã hoàn thành`) | tap `Đăng tin` → `back` | Đơn của tôi, **giữ tab `Đã hoàn thành`** | TC-ACT-016 |
