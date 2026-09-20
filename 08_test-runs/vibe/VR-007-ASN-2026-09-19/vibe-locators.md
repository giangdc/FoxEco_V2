# Vibe Locators — v1.1 — VR-007 — 2026-09-19

> Captured via **Appium MCP** (UiAutomator2) · app `com.hrisproject.stag` · Module **ASN**
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md` · Tài khoản: `stag_taipm@` (Phan Minh Tài) → `stag_anhdc4@` (Đặng Châu Anh)

## 🔑 MÀN ĐĂNG NHẬP FoxPro — lần đầu được harvest (mở khoá đổi tài khoản tự động)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Ô email đăng nhập | set_value | -android uiautomator | `new UiSelector().text("Nhập email đăng nhập")` | ✅ | mcp-log S1, S2 | *(hạ tầng đổi tài khoản)* |
| Nút "NHẬN MÃ OTP" | tap | -android uiautomator | `new UiSelector().text("NHẬN MÃ OTP")` | ✅ | mcp-log S1, S2 | — |
| Ô nhập OTP | *(tự focus)* | *(không cần locator)* | `adb shell input text "$FOXECO_STG_OTP"` | ✅ | mcp-log S1, S2 | ℹ️ ô **tự focus** khi vào màn ⇒ ⛔ không cần find |
| Nút "ĐĂNG NHẬP" | tap | -android uiautomator | `new UiSelector().text("ĐĂNG NHẬP")` | ✅ | mcp-log S1, S2 | — |
| Nút "Đăng xuất" *(FoxPro → Cá nhân)* | tap | -android uiautomator | `new UiSelector().text("Đăng xuất")` | ✅ | mcp-log S1, S2 | ⚠️ cuối danh sách ⇒ cần `scroll_to_element` |
| Popup xác nhận đăng xuất | tap | -android uiautomator | `new UiSelector().text("Đồng ý")` | ✅ | mcp-log S1, S2 | text popup: *"Bạn muốn đăng xuất?"* |
| Icon "FoxEco" *(FoxPro → Chức năng)* | tap | -android uiautomator | `new UiSelector().text("FoxEco")` | ✅ | mcp-log S1, S2 | ⚠️ cần `scroll_to_element` 3–4 nhịp |
| Tab "Chức năng" *(FoxPro)* | tap | -android uiautomator | `new UiSelector().text("Chức năng")` | ✅ | mcp-log S1, S2 | — |

> 🔑 **Luồng 5 bước đầy đủ + bẫy:** `04_test-data/valid/USR-accounts.md §0b`. ⏱️ ~14 MCP call / ~2 phút mỗi lượt đổi tài khoản.

## Màn: Đăng tin — OFFER (*"Tôi nhận giao hàng"*)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Card chọn loại tin OFFER | tap | -android uiautomator | `new UiSelector().text("Tôi nhận giao hàng")` | ✅ | mcp-log A1 | TC-ASN-013 |
| ĐIỂM XUẤT PHÁT (A) | set_value | -android uiautomator | `new UiSelector().text("Bạn đang ở đâu / xuất phát từ đâu")` | ✅ | mcp-log A1 | TC-ASN-013 |
| ĐIỂM ĐẾN (B) | set_value | -android uiautomator | `new UiSelector().text("Bạn sẽ đến đâu")` | ✅ | mcp-log A1 | TC-ASN-013 |
| ↳ ⚠️ ô rỗng trả về **chuỗi hint** | — | — | bẫy **T2** (VR-003): `text` của ô rỗng = placeholder, ⛔ đừng assert `text != ""` | ⚠️ Inferred | — | — |
| Gợi ý địa chỉ | tap | -android uiautomator | `new UiSelector().resourceId("address-suggestion-0")` | ✅ | mcp-log A1 | 🔴 bẫy **T11** — **BẮT BUỘC chạm gợi ý**, gõ tay không đủ |
| Chip buổi | tap | -android uiautomator | `new UiSelector().textStartsWith("Sáng (8")` · `("Chiều (13")` | ✅ | mcp-log A1 | ⚠️ nhãn thật **`Sáng (8–12h)`**, fragment ghi *"(6–12h)"* ⇒ **sai tài liệu** |
| Checkbox điều khoản | tap *(toạ độ)* | *(không có locator riêng)* | text `Tôi đã đọc và đồng ý…` tìm được, nhưng **ô tick** nằm lệch trái ⇒ tap `(52, y_text)` | ⚠️ Inferred | mcp-log A1 | ⛔ OFFER **không có** `post-n3-consent-checkbox` như NEED |
| Nút "Đăng tin ngay" | tap | -android uiautomator | `new UiSelector().text("Đăng tin ngay")` | ✅ | mcp-log A1 | — |
| Màn thành công OFFER | verify | -android uiautomator | `new UiSelector().text("Đã ghi nhận tuyến đường!")` | ⚠️ Inferred | mcp-log A1 | ⚠️ **khác** NEED (*"Đăng tin thành công!"*) |
| ↳ ℹ️ OFFER **không lên Bảng tin** | — | — | *"Tuyến đường của bạn được lưu vào hệ thống (không hiển thị công khai)"* | ✅ | mcp-log A1 | giải thích vì sao Bảng tin chỉ đếm NEED |

## Màn: Đăng tin — NEED (wizard 3 bước)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Card chọn loại tin NEED | tap | -android uiautomator | `new UiSelector().text("Tôi cần gửi hàng")` | ✅ | mcp-log A2 | TC-ASN-013, 021, 023 |
| Chip loại hàng | tap | -android uiautomator | `new UiSelector().text("Tài liệu")` | ✅ | mcp-log A2 | 🔴 nhãn `"Giấy tờ, hồ sơ"` trong `TC-ASN-021` Steps **KHÔNG tồn tại** (`C-ORD-09`) |
| Chip giá trị / trọng lượng / kích thước | tap | -android uiautomator | `resourceId("value-tier-chip-option-low")` · `("weight-tier-chip-option-light")` · `("size-tier-chip-option-small")` | ✅ | mcp-log A2 | ⚠️ mỗi chip cần `scroll_to_element` riêng |
| Nút thêm ảnh | tap | -android uiautomator | `new UiSelector().resourceId("multi-photo-add-button")` | ✅ | mcp-log A2 | bẫy **T7** — ⛔ đừng dùng `accessibility id "0/5"` |
| Bottom sheet chọn ảnh | tap | -android uiautomator | `new UiSelector().text("Chọn từ thư viện")` | ✅ | mcp-log A2 | — |
| Nút xác nhận ảnh *(Photo Picker hệ thống)* | tap | -android uiautomator | `new UiSelector().textStartsWith("Add (")` | ✅ | mcp-log A2 | ⚠️ **tiếng Anh** — thuộc Android Photo Picker, ⛔ không phải app |
| Ô địa chỉ lấy / giao hàng | set_value | -android uiautomator | `new UiSelector().text("Địa chỉ lấy hàng")` · `("Địa chỉ giao hàng")` | ✅ | mcp-log A2 | ⚠️ ô lấy hàng **rỗng** (hồ sơ không có địa chỉ mặc định) |
| Ô email người nhận | set_value | -android uiautomator | `new UiSelector().text("Email công ty người nhận")` | ✅ | mcp-log A2 | tra danh bạ tự động |
| Ô SĐT người nhận | set_value | -android uiautomator | `new UiSelector().text("Số điện thoại")` | ✅ | mcp-log A2 | ⚠️ autofill có thể trả **MNV** thay SĐT (xem repro B1) |
| Checkbox điều khoản (NEED) | tap | -android uiautomator | `new UiSelector().resourceId("post-n3-consent-checkbox")` | ✅ | mcp-log A2 | ✅ NEED **CÓ** resource-id, khác OFFER |
| Nút "Tiếp theo" | tap + get_attribute | -android uiautomator | `new UiSelector().text("Tiếp theo")` | ✅ | mcp-log A2 | assert `enabled` `false→true` |
| Màn thành công NEED | verify | -android uiautomator | `new UiSelector().text("Đăng tin thành công!")` | ⚠️ Inferred | mcp-log A2 | 2 CTA: `Theo dõi đơn` · `Về trang chủ` |

## Màn: Bảng tin

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| **Badge "Tin của bạn"** | find + tap | -android uiautomator | `new UiSelector().text("Tin của bạn")` | ✅ | mcp-log A4 | **TC-ASN-013 E4** · TC-ASN-021 |
| ↳ ℹ️ badge bám **phiên đăng nhập** | — | — | cùng 1 tin: chủ tin thấy badge, người khác **không** | ✅ | mcp-log A4 + TC-ASN-021 | đối chứng 2 tài khoản |
| Dòng tuyến trên card | verify | -android uiautomator | `new UiSelector().text("<địa chỉ>")` | ⚠️ Inferred | mcp-log A4 | giá trị động |

## Màn: Chi tiết tin

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| **CTA "Tôi mang giúp được"** | verify | -android uiautomator | `new UiSelector().textContains("Tôi mang giúp được")` | ✅ | mcp-log A4, TC-ASN-023 | 🟢 **CÓ** khi không phải chủ tin · 🚫 **NOT FOUND** khi là chủ tin ⇒ chứng cứ **TC-ASN-013 E4** |
| §LỘ TRÌNH — địa chỉ | verify | -android uiautomator | `new UiSelector().text("Tòa V-City, Lê Thái Tổ")` | ✅ | mcp-log TC-ASN-023 | dùng đối chiếu thông báo ↔ tin |
| §NGƯỜI GỬI — nút "Gọi" | — | -android uiautomator | `new UiSelector().text("Gọi")` | ⚠️ Inferred | mcp-log A4 | ℹ️ **mờ/disabled** khi xem tin của chính mình |

## Màn: Thông báo

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| **Thông báo khớp tuyến** | find + tap | -android uiautomator | `new UiSelector().textContains("Tìm thấy đơn hàng phù hợp tuyến")` | ✅ | mcp-log TC-ASN-023 | **TC-ASN-023** — tap mở thẳng `Chi tiết tin` |
| ↳ nguyên văn phụ đề | — | — | `Tìm thấy đơn hàng phù hợp tuyến của bạn — xem chi tiết để nhận giao` | ✅ | mcp-log TC-ASN-023 | — |
| Nhóm ngày | verify_absent | -android uiautomator | `new UiSelector().text("HÔM NAY")` | ✅ | mcp-log A3 | 🔑 **mẹo đo rẻ**: `HÔM NAY` **NOT FOUND** ⇒ chứng minh **0 thông báo mới hôm nay** (dùng cho `TC-ASN-013 E3`) |
| Từ khoá khớp tuyến | verify_absent | -android uiautomator | `new UiSelector().textContains("tuyến")` | ✅ | mcp-log A3 | 🚫 NOT FOUND ở tài khoản chủ tin = chứng cứ âm |
| ↳ ⚠️ nhãn thời gian **độ phân giải 1 phút** | — | — | `"3 phút trước"` ⇒ elapsed ∈ [180s, 240s) | ✅ | mcp-log TC-ASN-023 | 🔴 **không đo được mốc giây** ⇒ NFR ≤60s cần 2 thiết bị |

## Navigation Flow

| From | Trigger | To | MCP-verified |
|------|---------|-----|--------------|
| FoxPro `Cá nhân` | tap `Đăng xuất` → `Đồng ý` | Màn login FoxPro | mcp-log S1, S2 |
| Màn login | email → `NHẬN MÃ OTP` → OTP → `ĐĂNG NHẬP` | FoxPro Trang chủ *(đã đăng nhập)* | mcp-log S1, S2 |
| FoxPro `Chức năng` | tap `FoxEco` | FoxEco Trang chủ | mcp-log S1, S2 |
| FoxEco Trang chủ | tap `Đăng tin` → `Tôi nhận giao hàng` | Form OFFER 1 trang | mcp-log A1 |
| FoxEco Trang chủ | tap `Đăng tin` → `Tôi cần gửi hàng` | Wizard NEED Bước 1/3 | mcp-log A2 |
| Màn Thông báo | tap thông báo khớp tuyến | **Chi tiết tin** của tin NEED tương ứng | mcp-log TC-ASN-023 |

## Thống kê

| Màn đã harvest | Elements | ✅ Verified | ⚠️ Inferred | 🚫 NOT FOUND |
|---|--:|--:|--:|--:|
| **7** (login FoxPro · OFFER · wizard NEED ×3 · Bảng tin · Chi tiết tin · Thông báo) | **34** | **26** | **8** | **0*** |

> \* 2 phép `find_element` trả NOT FOUND trong phiên là **chủ ý** (chứng cứ âm cho `TC-ASN-013 E3/E4`), ⛔ không phải locator hỏng.
> 🔑 **Đóng góp lớn nhất của phiên: màn đăng nhập FoxPro** — đây là thứ mở khoá toàn bộ nhóm TC đa-tài-khoản của **mọi module**, không riêng ASN.
