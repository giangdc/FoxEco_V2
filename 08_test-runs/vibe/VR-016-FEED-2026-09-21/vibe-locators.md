# Vibe Locators — v1.1 (module FEED) — VR-016 — 2026-09-21

> Captured via Appium MCP (UiAutomator2) during this run.
> Mark legend: ✅ Verified (MCP find+action OK) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: see `mcp-session-log.md`
> Platform: mobile (Android, package `com.hrisproject.stag`)

## Screen: Bảng tin (Feed list)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Card tin #0 (topmost) | tap | -android uiautomator | `new UiSelector().resourceId("feed-post-card-0")` | ✅ | mcp-session-log Pha B TC-FEED-007 | TC-FEED-002, TC-FEED-007 |
| Card tin #1 | tap | -android uiautomator | `new UiSelector().resourceId("feed-post-card-1")` | ✅ | mcp-session-log Pha B TC-FEED-009 | TC-FEED-009 |
| Card tin #4 | tap | -android uiautomator | `new UiSelector().resourceId("feed-post-card-4")` | ✅ | mcp-session-log Pha B TC-FEED-015 | TC-FEED-015 |
| Badge "Tin của bạn" | verify_visible | (native resource-id, từ page source) | `resource-id="feed-post-own-badge"` | ✅ | mcp-session-log A1 | TC-FEED-002 (đối chứng phủ định) |
| Bottom nav — Bảng tin / Đăng tin / Hoạt động / Cá nhân | (không thao tác trong phiên này) | text | `text("Bảng tin")` / `text("Đăng tin")` / `text("Hoạt động")` / `text("Cá nhân")` | ⚠️ Inferred (chỉ thấy trong page source, chưa tap) | mcp-session-log A1 | — |

> Card `feed-post-card-N` là index theo **thứ tự hiển thị hiện tại** trong RecyclerView (0 = trên cùng), KHÔNG phải ID cố định của tin — thứ tự đổi khi có tin mới đăng. implement-automation cần tra lại thứ tự tại thời điểm chạy, không hardcode N↔nội dung tin.

## Screen: Chi tiết tin (Feed detail)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Nút back (header) | (điều hướng, dùng `appium_gesture back` thay vì tap) | — | — | ✅ | mcp-session-log #7 | TC-FEED-007, 009, 015 |
| Nút CTA "Tôi mang giúp được" (sticky bottom) | verify_visible | text | `text("Tôi mang giúp được")` | ✅ | mcp-session-log Pha B TC-FEED-007 | TC-FEED-007 |
| Cảnh báo thiếu toạ độ | verify_visible | text | `text("Chưa xác định được toạ độ trên bản đồ cho địa chỉ này")` | ✅ | mcp-session-log Pha B TC-FEED-007/009/015 | TC-FEED-007, TC-FEED-009 (đối chứng), TC-FEED-015 |
| Cụm "NGƯỜI GỬI" — tên | verify_visible | (label tĩnh, không resource-id riêng — đọc qua get_text vùng "NGƯỜI GỬI") | — | ✅ | mcp-session-log Pha B TC-FEED-007 | TC-FEED-007 |
| Nút "Gọi" cạnh Người gửi | verify_visible (chỉ quan sát, KHÔNG tap) | text | `text("Gọi")` | ⚠️ Inferred (thấy hiển thị nhưng chưa verify enabled/disabled qua MCP — ngoài phạm vi TC hôm nay) | mcp-session-log Pha B TC-FEED-007 | — (quan sát phụ, liên quan nợ #1 CHANGELOG FEED, không thuộc TC nào hôm nay) |

## Screen: Đăng tin — Bước 1/3 "Thông tin hàng"

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Chip loại hàng "Tài liệu" (mặc định chọn sẵn) | verify | text | `text("Tài liệu")` | ✅ | mcp-session-log R4 | TC-FEED-009 (seed) |
| Chip giá trị "Thấp" | tap | text | `text("Thấp")` | ✅ | mcp-session-log R5 | TC-FEED-009 (seed) |
| Chip trọng lượng "Dưới 5 kg" | tap | text | `text("Dưới 5 kg")` | ✅ | mcp-session-log R6 | TC-FEED-009 (seed) |
| Chip kích thước "Nhỏ" | tap | text | `text("Nhỏ")` | ✅ | mcp-session-log R6 | TC-FEED-009 (seed) |
| Ô ảnh hàng (bắt buộc ≥1, tối đa 5) | tap | -android uiautomator | `new UiSelector().textContains("0/5")` | ✅ | mcp-session-log R7 | TC-FEED-009 (seed) |
| ⚠️ Ràng buộc ảnh | — | — | ảnh >5MB bị chặn với toast "Ảnh vượt quá 5MB" — KHÔNG có thông báo trước, phải thử rồi mới biết | ✅ | mcp-session-log R7 | — |

## Screen: Đăng tin — Bước 2/3 "Địa điểm & Thời gian"

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Ô địa chỉ NGƯỜI GỬI (Lấy hàng) — prefill từ hồ sơ NHƯNG editable | tap → `set_value` → chọn gợi ý | -android uiautomator | `new UiSelector().className("android.widget.EditText").focused(true)` (sau khi tap để lấy focus) | ✅ | mcp-session-log R9 | TC-FEED-009 |
| Gợi ý autocomplete địa chỉ (theo searchtext) | tap | -android uiautomator | `new UiSelector().textContains("<office name>")` — vd `"An Giang Trần Hưng Đạo - Long Xuyên"` | ✅ | mcp-session-log R9 | TC-FEED-009 |
| Ô Email công ty người nhận | `set_value` | -android uiautomator | `new UiSelector().text("Email công ty người nhận")` | ✅ | mcp-session-log R10 | TC-FEED-009 |
| ↳ auto-fill tên + SĐT khi email khớp hệ thống nội bộ | verify | — | text "Đã tìm thấy trong hệ thống nội bộ..." | ✅ | mcp-session-log R10 | — |
| Ô Địa chỉ giao hàng (NGƯỜI NHẬN) | `set_value` → chọn gợi ý | -android uiautomator | `new UiSelector().text("Địa chỉ giao hàng")` | ✅ | mcp-session-log R11 | TC-FEED-009 |
| Chip buổi mong muốn "Sáng (8–12h)" | tap | -android uiautomator | `new UiSelector().textContains("Sáng (8")` | ✅ | mcp-session-log R12 | TC-FEED-009 |
| ⚠️ Bẫy validate | — | — | Nút "Tiếp theo" **luôn hiển thị màu cam** (nhìn như enabled) dù thiếu field bắt buộc (buổi mong muốn) — tap không phản hồi, không toast lỗi; phải cuộn xuống mới thấy dòng "Chọn ít nhất 1 buổi" | ✅ | mcp-session-log R12 | — |

## Screen: Đăng tin — Bước 3/3 "Xác nhận & Đăng tin"

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Checkbox đồng ý điều khoản | tap | -android uiautomator | `new UiSelector().textContains("Tôi đã đọc và đồng ý")` | ✅ | mcp-session-log R14 | TC-FEED-009 |
| Nút "Đăng tin ngay" | tap | -android uiautomator | `new UiSelector().description("Đăng tin ngay")` | ✅ | mcp-session-log R14 | TC-FEED-009 |

## 🔑 Fixture cố định — văn phòng CÓ toạ độ hợp lệ (dùng lại được)

| Field | Giá trị | Nguồn |
|---|---|---|
| Lấy hàng | `FTEL An Giang Trần Hưng Đạo - Long Xuyên` | QC cấp — địa chỉ gốc `132 Trần Hưng Đạo, LX` |
| Giao hàng | `FTEL An Giang VPGD Bình Hòa` | QC cấp — địa chỉ gốc `19 ấp Phú An 1, Bình Hòa` |
| Xác nhận | Chi tiết tin hiện bản đồ Google Maps thật, vẽ tuyến cam, "17.2 km · 15 phút" | `TC-FEED-009__verify-real-map-route.png` |
| ⚠️ Lưu ý | `location_address_catalog.xlsx` (`DOC-v1.1-04`) gắn CẢ HAI địa chỉ này `coordinate_status = MISSING` dù lat/lng hợp lệ — **không dùng file này để tra**, phải kiểm qua app thật |

## Navigation Flow (only MCP-traversed flows)

| From | Trigger | To | MCP-verified |
|------|---------|-----|--------------|
| Bảng tin | tap `feed-post-card-0` | Chi tiết tin (tin FTEL SG09→SG07) | TC-FEED-007 |
| Chi tiết tin | `appium_gesture(back)` | Bảng tin | TC-FEED-007→009 |
| Bảng tin | tap `feed-post-card-1` | Chi tiết tin (tin FTEL SG07→SG03) | TC-FEED-009 |
| Bảng tin | tap `feed-post-card-4` | Chi tiết tin (tin Tòa V-City→FPT Cầu Giấy) | TC-FEED-015 |

## Screen: FoxEco — Cá nhân (retest account switch)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tab "Cá nhân" (FoxEco, KHÔNG có Đăng xuất) | tap | text | `text("Cá nhân")` | ✅ | mcp-session-log S4 | — |
| Nút back thoát FoxEco → FoxPro `Chức năng` | gesture back ×2 | — | — | ✅ | mcp-session-log S4-S9 | TC-FEED-007 (retest) |
| Tab "Cá nhân" (FoxPro, CÓ Đăng xuất) | tap | text | `text("Cá nhân")` | ✅ | mcp-session-log S4-S9 | TC-FEED-007 (retest) |
| Nút "Đăng xuất" | scroll_to_element + tap | -android uiautomator | `new UiSelector().textContains("Đăng xuất")` | ✅ | mcp-session-log S4-S9 | — (tái sử dụng `USR-accounts.md §0b`) |
| Popup xác nhận "Đồng ý" | tap | text | `text("Đồng ý")` | ✅ | mcp-session-log S4-S9 | — |

## Ghi nhớ — CTA "Tôi mang giúp được" vắng mặt chọn lọc theo tin

> Không phải locator mới (đã có `text("Tôi mang giúp được")` từ trước) — ghi lại **hành vi** để tránh hiểu nhầm là bug khi implement-automation viết assertion cho TC-FEED-007/012:
> `find_element(text("Tôi mang giúp được"))` **hợp lệ KHÔNG TÌM THẤY** trên 1 số tin cụ thể (viewer = người nhận đã khai của tin đó, theo `OPR-05`) — automation PHẢI tham số hoá theo (viewer, tin), KHÔNG hardcode "mọi tin của người khác đều có CTA".
