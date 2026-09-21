# Vibe Locators — v1.1 — VR-018 — 2026-09-21

> Captured via Appium MCP (UiAutomator2) · Platform: mobile (Android, FoxPro host → FoxEco)
> Mark legend: ✅ Verified (MCP find+action OK trong run này) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md`

## Screen: Theo dõi đơn — nút theo vai / trạng thái

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Nút "Báo cáo sự cố" (mọi vai, mọi trạng thái đã thấy) | tap | -android uiautomator | `new UiSelector().resourceId("track-report-incident")` | ✅ | TC-CNL-006/015/016 | TC-CNL-006, 015, 016, 022 |
| Nút "Chỉnh sửa" (A · Chờ ghép) | verify_visible | page source | `resource-id="track-edit-post"` | ✅ | TC-CNL-022 | TC-CNL-022 |
| Nút "Huỷ đơn" (A · **Chờ ghép**) | tap | -android uiautomator | `new UiSelector().resourceId("track-cancel-post")` | ✅ | TC-CNL-004 | TC-CNL-004, 012 |
| Nút "Huỷ đơn" (A · **Đã ghép**) | tap | -android uiautomator | `new UiSelector().resourceId("track-sender-matched-cancel")` | ✅ | TC-CNL-009 | TC-CNL-009 ⚠️ **id khác** với Chờ ghép |
| Nhãn trạng thái (A · Đã ghép) | verify_visible | page source | `resource-id="track-sender-matched-status"` text `Đã ghép · chờ shipper lấy hàng` | ✅ | TC-CNL-009 | TC-CNL-009 |
| Nút "Tôi đã lấy hàng" (B · Đã ghép) | tap | -android uiautomator | `new UiSelector().resourceId("track-carrier-pickup")` | ✅ | TC-CNL-021 | TC-CNL-021 |
| Nút "Huỷ nhận đơn" (B · Đã ghép) | tap | -android uiautomator | `new UiSelector().resourceId("track-carrier-cancel-accept")` | ✅ | TC-CNL-010 | TC-CNL-010 |
| Nút "Đã giao cho người nhận" (B · Đang giao) | verify_visible | page source | content-desc `Đã giao cho người nhận` (không có resource-id) | ✅ | TC-CNL-018 | TC-CNL-018 |
| Nhãn tắt chân màn (A · Đang giao) | verify_visible | page source | text `Đang giao đến người nhận` `clickable=false` | ✅ | TC-CNL-017 | TC-CNL-017 |
| Nhãn tắt chân màn (C · Đang giao) | verify_visible | page source | text `Đơn đang trên đường đến bạn` `clickable=false` | ✅ | TC-CNL-019 | TC-CNL-019 |
| "Yêu cầu hoàn hàng" (mọi vai · Đang giao) | verify_absent | -android uiautomator | `scroll_to_element new UiSelector().textContains("hoàn hàng")` | 🚫 NOT FOUND | TC-CNL-017/018/019 | **kết quả kiểm** — không phải locator hỏng |
| Block LỊCH SỬ | scroll_to_element | -android uiautomator | `new UiSelector().text("LỊCH SỬ")` (preset small, ≤15 nhịp) | ✅ | TC-CNL-009/010 | TC-CNL-009, 010 |

## Popup huỷ đơn / huỷ nhận đơn (dùng chung 1 component)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Ô lý do huỷ | set_value · get_element_attribute text | -android uiautomator | `new UiSelector().resourceId("cancel-order-reason")` | ✅ | TC-CNL-004 | TC-CNL-004, 009, 010, 012 |
| Nút "Xác nhận" | get_element_attribute enabled · tap | -android uiautomator | `new UiSelector().resourceId("cancel-order-confirm")` | ✅ | TC-CNL-004 | TC-CNL-004, 009, 010, 012 |
| Nút "Huỷ" (đóng popup) | tap | -android uiautomator | `new UiSelector().resourceId("cancel-order-dismiss")` | ✅ | TC-CNL-004 | TC-CNL-004, 012 |
| Popup kết quả "Đồng ý" | tap | -android uiautomator | `new UiSelector().text("Đồng ý")` | ✅ | TC-CNL-009/010 | TC-CNL-009, 010 |

## Luồng lấy hàng (B)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Popup "Xác nhận" — nút | tap | -android uiautomator | `new UiSelector().text("Xác nhận").instance(1)` | ✅ | TC-CNL-018 setup | ⚠️ `instance(0)` là **tiêu đề popup** (cùng chữ) — bấm vào không có tác dụng |
| Màn trung gian "Xác nhận đã lấy hàng" — nút | tap | -android uiautomator | `new UiSelector().textContains("Bắt đầu giao")` | ✅ | TC-CNL-018 setup | text `Đã lấy hàng — Bắt đầu giao` |

## Navigation Flow (MCP-traversed)

| From | Trigger | To | MCP-verified |
|------|---------|-----|--------------|
| Theo dõi đơn (B · Đã ghép) | `Huỷ nhận đơn` → `Xác nhận` → `Đồng ý` | **Chi tiết tin** (không có LỊCH SỬ) | TC-CNL-010 |
| Theo dõi đơn (A · Đã ghép) | `Huỷ đơn` → `Xác nhận` → `Đồng ý` | **Đơn của tôi** (danh sách) | TC-CNL-009 |
| Theo dõi đơn (B · Đã ghép) | `Tôi đã lấy hàng` → `Xác nhận` | màn `Xác nhận đã lấy hàng` → `Bắt đầu giao` → popup `Đã lấy hàng` → Theo dõi đơn `Đang giao` | TC-CNL-018 setup |
| Theo dõi đơn (mọi vai) | `Báo cáo sự cố` | màn `Báo sự cố đơn hàng` = **webview Microsoft Sign in** | TC-CNL-006/015/016 |
