# Vibe Locators — v1.0 — VR-001 — 2026-07-31

> Captured via Appium MCP during this run.
> Mark legend: ✅ Verified (MCP find+action OK) · ⚠️ Inferred/coordinate-based · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: see mcp-session-log.md (audit trail)
> Platform: mobile (Android, real device, UiAutomator2)
> App: FoxEco SDK (launched from host app FoxPro_Stag → "Chức năng" tab → FoxEco icon; standalone package id not confirmed by user)

## Page: FoxPro host app — Chức năng tab

| Element | Action Used | Locator Strategy | Locator Value | Verified | MCP call ref | TC refs |
|---------|------------|-------------------|----------------|----------|---------------|---------|
| FoxEco icon | tap | -android uiautomator | `new UiSelector().textContains("FoxEco")` | ✅ | mcp-log #20-21 | (navigation only) |

## Page: FoxEco — Trang chủ (Home)

| Element | Action Used | Locator Strategy | Locator Value | Verified | MCP call ref | TC refs |
|---------|------------|-------------------|----------------|----------|---------------|---------|
| "Đăng tin" bottom nav | tap | accessibility id | `Đăng tin` | ✅ | mcp-log #32-33 | TC_04.2, TC_04.73 |

## Page: Đăng tin mới (role selection)

| Element | Action Used | Locator Strategy | Locator Value | Verified | MCP call ref | TC refs |
|---------|------------|-------------------|----------------|----------|---------------|---------|
| "Tôi cần gửi hàng" card | tap | -android uiautomator | `new UiSelector().textContains("Tôi cần gửi hàng")` | ✅ | mcp-log #35-36 | TC_04.2, TC_04.73 |

## Page: Wizard Bước 1/3 (Thông tin hàng)

| Element | Action Used | Locator Strategy | Locator Value | Verified | MCP call ref | TC refs |
|---------|------------|-------------------|----------------|----------|---------------|---------|
| "Giá trị vừa" chip | tap | -android uiautomator | `new UiSelector().textContains("Giá trị vừa")` | ✅ | mcp-log #38-39 | TC_04.73 |
| "Tiếp theo" button (step 1) | tap | -android uiautomator | `new UiSelector().textContains("Tiếp theo")` | ✅ | mcp-log #40-41 | TC_04.73 |

## Page: Wizard Bước 2/3 (Địa điểm & Thời gian)

| Element | Action Used | Locator Strategy | Locator Value | Verified | MCP call ref | TC refs |
|---------|------------|-------------------|----------------|----------|---------------|---------|
| "Địa chỉ lấy hàng" input | tap + type | -android uiautomator | `new UiSelector().textContains("Địa chỉ lấy hàng")` | ✅ | mcp-log #42-44 | TC_04.73 |
| Địa chỉ lấy hàng — autocomplete suggestion row | tap | ⚠️ coordinate (no disambiguating locator found — `find_element` resolves to same node as the input itself) | tap(480, 978) relative to a 1080×2460 screen, ~30px below the input row | ⚠️ Inferred | mcp-log #46-48 | TC_04.73 — **needs re-verification**, do not reuse coordinates as-is (layout-dependent, recompute per run) |
| "Email công ty người nhận" input | tap + type | -android uiautomator | `new UiSelector().textContains("Email công ty người nhận")` | ✅ | mcp-log #49, #57 | TC_04.73 |
| "Tên người nhận" input | tap + type | -android uiautomator | `new UiSelector().textContains("Tên người nhận")` | ✅ | mcp-log #51 | TC_04.73 |
| "Số điện thoại" (recipient) input | tap + type | -android uiautomator | `new UiSelector().textContains("Số điện thoại")` | ✅ | mcp-log #51 | TC_04.73 |
| "Địa chỉ giao hàng" input | tap + type | -android uiautomator | `new UiSelector().textContains("Địa chỉ giao hàng")` | ✅ | mcp-log #51 | TC_04.73 — note: typing alone did not reliably persist the value across retries; combine with explicit suggestion-tap like the pickup address for reliability |
| "Khung giờ mong muốn" — Từ time field | tap | -android uiautomator | `new UiSelector().textContains("11:10")` (value-based, NOT stable — changes every render) | ⚠️ Inferred | mcp-log #54 | TC_04.73 — do not reuse literal time-value locator; needs a stable resource-id from a full `appium_get_page_source` dump (not captured this run, output was too large to inspect in full) |
| Time picker — hour wheel column | swipe | ⚠️ coordinate (custom wheel widget, tap-to-select did not work, only swipe did) | swipe x=430 within hour column, ~108px per row | ⚠️ Inferred | mcp-log #54 | TC_04.73 |
| Time picker — "Xong" confirm | tap | -android uiautomator | `new UiSelector().textContains("Xong")` | ✅ | mcp-log #54 | TC_04.73 |
| "Tiếp theo" button (step 2) | tap | -android uiautomator | `new UiSelector().textContains("Tiếp theo")` | ✅ | mcp-log #60 | TC_04.73 |

## Page: Wizard Bước 3/3 (Xác nhận & Đăng tin)

| Element | Action Used | Locator Strategy | Locator Value | Verified | MCP call ref | TC refs |
|---------|------------|-------------------|----------------|----------|---------------|---------|
| Terms checkbox / label | tap | -android uiautomator | `new UiSelector().textContains("Tôi đã đọc và đồng ý")` | ✅ | mcp-log #62 | TC_04.73 |
| "Đăng tin ngay" submit button | tap | -android uiautomator | `new UiSelector().textContains("Đăng tin ngay")` | ✅ | mcp-log #63 | TC_04.73 |

## Page: Đăng tin thành công (success modal)

| Element | Action Used | Locator Strategy | Locator Value | Verified | MCP call ref | TC refs |
|---------|------------|-------------------|----------------|----------|---------------|---------|
| "Theo dõi đơn" button | (visible, not yet tapped — session ended before use) | -android uiautomator (untested) | `new UiSelector().textContains("Theo dõi đơn")` | ⏳ Pending | — | TC_04.89 (future run) |
| "Về trang chủ" button | (visible, not tapped) | -android uiautomator (untested) | `new UiSelector().textContains("Về trang chủ")` | ⏳ Pending | — | — |

## Navigation Flow (MCP-traversed this run)

| From | Trigger | To | Verified by |
|------|---------|-----|------------|
| FoxPro host app "Chức năng" | tap FoxEco icon | FoxEco Trang chủ | mcp-log #20-22 |
| FoxEco Trang chủ | tap "Đăng tin" bottom nav | Đăng tin mới (role select) | mcp-log #32-34 |
| Đăng tin mới | tap "Tôi cần gửi hàng" | Wizard Bước 1/3 | mcp-log #35-37 (TC_04.2 evidence) |
| Wizard Bước 1/3 | tap "Tiếp theo" (valid Loại hàng + Giá trị hàng) | Wizard Bước 2/3 | mcp-log #40-41 |
| Wizard Bước 2/3 | tap "Tiếp theo" (all fields valid) | Wizard Bước 3/3 | mcp-log #60 |
| Wizard Bước 3/3 | tap "Đăng tin ngay" (checkbox ticked) | Đăng tin thành công (success modal) | mcp-log #63-64 |

## Known ambiguities / re-verify before automation

- App package name for FoxEco/FoxPro_Stag is **still unconfirmed** — the app was reached via manual host-app navigation, not `appium_app_lifecycle(launch, app_id=...)`. `implement-automation` will need the real package id (or an activity-based launch) before it can script app startup.
- Two elements required coordinate-based taps because `appium_find_element` could not disambiguate them from a sibling node with identical text (address-autocomplete suggestion row) or because the widget is a native Android wheel picker with no stable per-item locator exposed (time picker hour column). Both are marked ⚠️ and must be re-derived per screen resolution — do not hardcode the pixel values found this run.
- No `appium_get_page_source` dump was saved in full for the Bước 2/3 or Bước 3/3 screens (outputs exceeded the tool's inline size limit and were only spot-inspected); a future run should capture and store these via the file-redirect path for a proper resource-id audit.
