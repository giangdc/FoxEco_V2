# Vibe Locators — v1.1 — VR-010 — 2026-09-19

> Captured via **Appium MCP** (UiAutomator2) during this run.
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md` · Platform: **mobile** · Device: emulator-5554 (720×1280)

## Màn: Thông báo — ★ ĐÍNH CHÍNH phương pháp ĐẾM của VR-009

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Icon chuông | find + tap | accessibility id | `Thông báo` | ✅ | mcp-log TC-015/016/017/025/018/019 | tái xác nhận VR-009 — ⚠️ chỉ có ở **Trang chủ** FoxEco |
| Thông báo khớp tuyến (phụ đề) | find + tap | -android uiautomator | `new UiSelector().textContains("Tìm thấy đơn hàng phù hợp tuyến của bạn — xem chi tiết").instance(N)` | ✅ | mcp-log TC-015/019/018 | khớp trên **phụ đề** (tiêu đề bị xuống dòng nên dễ trượt) |
| 🔴 **`.instance(N)` KHÔNG phải phép đếm tuyệt đối** | — | — | chỉ thấy node **đang render** (~4 mục) ⇒ `instance(5)` NOT FOUND dù có 6 mục; sau `scroll_to_element` xuống đáy thì `instance(4)` cũng biến mất | 🚫 **bẫy `T-ASN-10`** | mcp-log TC-016 | **đính chính VR-009** |
| ✅ **Phép đếm ĐÚNG** | get_page_source ×N vị trí | — | dump page source ở **nhiều vị trí cuộn** → ghép theo **nhãn tuổi** (khoá duy nhất) | ✅ | mcp-log TC-016/017/025 | dùng cho mọi TC nhóm trần |
| Nhóm ngày | verify | -android uiautomator | `text("HÔM NAY")` · `("HÔM QUA")` · `("40 NGÀY TRƯỚC")` | ✅ | mcp-log A1 | mốc neo khi cuộn lên đầu |
| Dấu chưa đọc | verify *(thị giác)* | — | vạch cam trái + chấm đỏ; đã đọc thì mất cả hai | ⚠️ Inferred | mcp-log TC-015 | oracle phụ để tách "mới" khỏi "tồn dư" |
| 🆕 **Thông báo biến mất sau khi MỞ** | — | — | `stag_taipm@`: 2 → 1 → 0 sau 2 lần mở. ⚠️ `stag_giangdc2@` thì **không** | ⚠️ Inferred | mcp-log TC-019 | **bẫy `T-ASN-11`** — đếm TRƯỚC khi mở |
| 4 loại thông báo quan sát được | verify | -android uiautomator | `textContains("Tìm thấy đơn hàng phù hợp tuyến")` · `("Tin của bạn đã quá hạn")` · `("Đã có người nhận mang giúp")` · `("Đơn đã bị huỷ")` | ✅ | mcp-log A1 | dùng để **tách** loại khi đếm |

## Màn: Chi tiết tin — 🔴 ĐÍNH CHÍNH VR-009: mục `Ghi chú` CÓ TỒN TẠI

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| 🔑 **Mục `Ghi chú`** | verify | -android uiautomator | `new UiSelector().text("SEED R3b dang sau")` — nằm trong khối `THÔNG TIN HÀNG` | ✅ **Verified** | mcp-log TC-018 | 🔴 **VR-009 ghi "KHÔNG TỒN TẠI" — SAI.** Khối chỉ render khi ô Ghi chú khác rỗng ⇒ **mã seed = oracle định danh MẠNH NHẤT** |
| Tuổi tin (header) | verify | -android uiautomator | `text("9 giờ trước")` · `("2 giờ trước")` | ✅ | mcp-log TC-019 | oracle phụ — ⚠️ bị làm tròn |
| Khối `LỘ TRÌNH` | verify | -android uiautomator | `text("LỘ TRÌNH")` → `Lấy hàng` / `Giao hàng` | ✅ | mcp-log TC-019/018 | đọc trực tiếp 2 điểm để đối chiếu tuyến OFFER |
| CTA `Tôi mang giúp được` | verify | -android uiautomator | `new UiSelector().textContains("Tôi mang giúp được")` | ✅ | mcp-log TC-019 | 🔑 **CÒN CTA ⇒ tin CÒN SỐNG** — oracle phân biệt tin sống/hết hạn |

## Màn: Form OFFER (`Tôi nhận giao hàng`)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Điểm xuất phát (A) | set_value | -android uiautomator | `new UiSelector().text("Bạn đang ở đâu / xuất phát từ đâu")` | ✅ | mcp-log SEED OFFER R1–R4 | — |
| Điểm đến (B) | set_value | -android uiautomator | `new UiSelector().text("Bạn sẽ đến đâu")` | ✅ | mcp-log SEED OFFER R1–R4 | ⚠️ phải **scroll down 1 nhịp** mới thấy |
| Gợi ý địa chỉ | find + tap | -android uiautomator | `new UiSelector().resourceId("address-suggestion-0")` | ✅ | mcp-log SEED ×18 | 🔴 **bắt buộc** tap gợi ý; ⚠️ gõ `FTEL SG08` → gợi ý-0 trả **`FTEL SG08 Gò Vấp`** (⛔ không phải `Quận 12`) ⇒ **gõ đủ chuỗi** khi cần đúng chi nhánh |
| Chip buổi `Giờ nào cũng được` | find + tap | -android uiautomator | `new UiSelector().text("Giờ nào cũng được")` | ✅ | mcp-log SEED ×13 | 🔑 chọn buổi này để tin **không bị đóng** khi khung giờ trôi qua |
| Checkbox điều khoản OFFER | tap *(toạ độ)* | *(không có resourceId)* | tap `(52, 1051)` **sau khi scroll down đến đáy ×2 nhịp** | ✅ *(4/4 lần)* | mcp-log SEED OFFER R1–R4 | tái xác nhận VR-009; cuộn đến đáy làm toạ độ **tất định** |
| Nút `Đăng tin ngay` | find + tap | -android uiautomator | `new UiSelector().text("Đăng tin ngay")` | ✅ | mcp-log SEED OFFER R1–R4 | — |
| Toast thành công | verify | -android uiautomator | `new UiSelector().textContains("Đã ghi nhận tuyến đường")` | ✅ | mcp-log SEED OFFER R1–R4 | oracle đăng OFFER thành công |

## Màn: Wizard NEED 3 bước (`Tôi cần gửi hàng`)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Ô `GHI CHÚ` *(bước 1)* | set_value | -android uiautomator | `new UiSelector().textContains("Lưu ý khi giao nhận")` | ✅ | mcp-log SEED NEED ×9 | 🔑 **nơi cắm mã seed** |
| Chip giá trị/trọng lượng/kích thước | find + tap | -android uiautomator | `text("Thấp")` · `text("Dưới 5 kg")` · `text("Nhỏ")` | ✅ | mcp-log SEED NEED ×9 | `Tài liệu` là loại hàng **mặc định sẵn** |
| Bộ đếm ảnh | find + tap / verify | -android uiautomator | `new UiSelector().text("0/5")` → sau khi thêm: `text("1/5")` | ✅ | mcp-log SEED NEED ×9 | tap chính bộ đếm để mở sheet chọn ảnh |
| Sheet chọn ảnh | find + tap | -android uiautomator | `new UiSelector().text("Chọn từ thư viện")` | ✅ | mcp-log SEED NEED ×9 | — |
| Ảnh trong picker hệ thống | tap *(toạ độ)* | *(picker Android, không có id ổn định)* | tap `(277, 715)` = ô ảnh **xanh lá** hàng 2 cột 2 | ✅ *(9/9 lần)* | mcp-log SEED NEED ×9 | ⚠️ toạ độ, ⛔ không phải locator — chỉ dùng cho picker hệ thống |
| Nút xác nhận picker | find + tap | -android uiautomator | `new UiSelector().text("Add (1)")` | ✅ | mcp-log SEED NEED ×9 | — |
| Địa chỉ lấy / giao *(bước 2)* | set_value | -android uiautomator | `text("Địa chỉ lấy hàng")` · `text("Địa chỉ giao hàng")` | ✅ | mcp-log SEED NEED ×9 | ⚠️ ô giao hàng phải **scroll down 1 nhịp** |
| Ô email người nhận | set_value | -android uiautomator | `new UiSelector().text("Email công ty người nhận")` | ✅ | mcp-log SEED NEED ×9 | ⭐ `stag_huyennhk@` autofill **ĐÚNG** SĐT `0989014863` — **9/9 lần** (tái xác nhận `T-ASN-08`) |
| Checkbox điều khoản NEED | find + tap | -android uiautomator | `new UiSelector().resourceId("post-n3-consent-checkbox")` | ✅ | mcp-log SEED NEED ×9 | cần `scroll_to_element` trước |
| Toast thành công | verify | -android uiautomator | `new UiSelector().textContains("Đăng tin thành công")` | ✅ | mcp-log SEED NEED ×9 | — |
| CTA sau khi đăng | find + tap | -android uiautomator | `new UiSelector().text("Về trang chủ")` | ✅ | mcp-log SEED ×13 | dùng cho **cả** OFFER lẫn NEED |

## Màn: Bảng tin

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tab Bảng tin | find + tap | -android uiautomator | `new UiSelector().text("Bảng tin")` | ✅ | mcp-log TC-016/019 | — |
| Cấu trúc 1 card *(để parse)* | get_page_source | — | `Tài liệu` → `Giá trị thấp` → `<tuổi tin>` → `Nhận:` → `<A>` → `Giao:` → `<B>` → `<ngày · buổi>` → `Nhẹ (< 5 kg)` → `Nhỏ, cầm tay` | ✅ | mcp-log TC-016/019 | 🔑 **khuôn parse** để đếm chính xác số tin theo tuyến |
| Badge tin của mình | verify | -android uiautomator | `new UiSelector().text("Tin của bạn")` | ✅ | mcp-log TC-019 | nằm **trước** nhãn tuổi trong thứ tự node |
| Tin **Hết hạn** vắng mặt | verify_absent | -android uiautomator | `scroll_to_element textContains("KCX Tân Thuận")` — cuộn hết danh sách | 🚫 **NOT FOUND** *(chủ ý)* | mcp-log TC-019 | **TC-ASN-019 E2** |

## Màn: Đơn của tôi (`Hoạt động`) — ★ nguồn xác định tin HẾT HẠN

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tab `Đã hoàn thành` | find + tap | -android uiautomator | `new UiSelector().text("Đã hoàn thành")` | ✅ | mcp-log TC-019 | 🔑 **nơi DUY NHẤT thấy tin `Hết hạn`** |
| Badge `Hết hạn` | verify | -android uiautomator | `new UiSelector().textContains("Hết hạn")` | ✅ | mcp-log TC-019 | kèm chú thích *"Không có ai nhận mang giúp trong thời gian đăng — tin đã tự động đóng."* |
| Dòng tuyến + ngày của tin hết hạn | get_page_source | — | `Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy · 19/9/2026` | ✅ | mcp-log TC-019 | ⇒ dựng được tiền đề `TC-ASN-019` **không cần dev** |

## Màn: FoxPro host — đăng xuất / đổi tài khoản

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tab `Cá nhân` (FoxPro) | find + tap | -android uiautomator | `new UiSelector().text("Cá nhân")` | ✅ | mcp-log ×7 lượt đổi | ⚠️ **phải thoát FoxEco trước** (FoxEco cũng có tab tên `Cá nhân`) |
| `Đăng xuất` | scroll_to + tap | -android uiautomator | `new UiSelector().text("Đăng xuất")` *(3 nhịp cuộn)* | ✅ | mcp-log ×7 lượt | 🚫 **NOT FOUND với `stag_huyennhk@`** — màn Cá nhân tài khoản đó không render mục này |
| Popup xác nhận | find + tap | -android uiautomator | `new UiSelector().text("Đồng ý")` | ✅ | mcp-log ×7 lượt | — |
| Ô email đăng nhập | set_value | -android uiautomator | `new UiSelector().text("Nhập email đăng nhập")` | ✅ | mcp-log ×7 lượt | — |
| `NHẬN MÃ OTP` / `ĐĂNG NHẬP` | find + tap | -android uiautomator | `text("NHẬN MÃ OTP")` · `text("ĐĂNG NHẬP")` | ✅ | mcp-log ×7 lượt | ⛔ **0/7 lần** gặp bẫy `T-ASN-07` (lỗi mạng giả) trong phiên này |
| Ô OTP | *(adb input text)* | *(ô tự focus)* | `adb shell input text "$FOXECO_STG_OTP"` | ✅ | mcp-log ×7 lượt | ⛔ không cần find element |
| Icon `FoxEco` ở `Chức năng` | scroll_to + tap | -android uiautomator | `new UiSelector().text("FoxEco")` *(preset `small`, 3–4 nhịp)* | ✅ | mcp-log ×7 lượt | 🚫 **NOT FOUND với `stag_huyennhk@`** — tài khoản không được bật FoxEco |
| Dialog quyền sau `pm clear` | find + tap | -android uiautomator | `text("Allow")` *(thông báo)* · `text("While using the app")` *(vị trí)* | ✅ | mcp-log 17:55–17:57 | chỉ xuất hiện sau khi xoá dữ liệu app |

## Navigation Flow (chỉ flow đã đi qua bằng MCP trong run này)

| From | Trigger | To | MCP-verified |
|------|---------|-----|--------------|
| FoxEco Trang chủ | `Đăng tin` → `Tôi nhận giao hàng` → điền → `Đăng tin ngay` | *"Đã ghi nhận tuyến đường!"* → `Về trang chủ` | ×4 (OFFER R1–R4) |
| FoxEco Trang chủ | `Đăng tin` → `Tôi cần gửi hàng` → wizard 3 bước | *"Đăng tin thành công!"* → `Về trang chủ` | ×9 (NEED) |
| FoxEco Trang chủ | tap `accessibility id "Thông báo"` | màn **Thông báo** | ×6 |
| màn Thông báo | tap 1 thông báo khớp tuyến | **Chi tiết tin** của đúng tin NEED | ×4 |
| FoxEco Trang chủ | `Hoạt động` → tab `Đã hoàn thành` | danh sách tin **Hết hạn** / **Hoàn thành** | ×2 |
| FoxEco *(bất kỳ)* | `back` | FoxPro host | ×7 |
| FoxPro `Cá nhân` | scroll → `Đăng xuất` → `Đồng ý` | màn login FoxPro | ×6 *(thất bại 1 lần với `stag_huyennhk@`)* |
| màn login | email → `NHẬN MÃ OTP` → adb OTP → `ĐĂNG NHẬP` | FoxPro Trang chủ | ×7 |
| FoxPro `Chức năng` | scroll → `FoxEco` | FoxEco Trang chủ | ×6 *(NOT FOUND 1 lần với `stag_huyennhk@`)* |

## Thống kê VR-010

| Màn đã harvest | Elements ghi nhận | ✅ Verified | ⚠️ Inferred | 🚫 NOT FOUND |
|---|---|---|---|---|
| **7** (Thông báo · Chi tiết tin · form OFFER · wizard NEED · Bảng tin · Đơn của tôi · FoxPro login/Cá nhân/Chức năng) | **38** | **33** | **3** | **2\*** |

\* 2 mục `🚫 NOT FOUND` là **chủ ý** (tin Hết hạn vắng khỏi Bảng tin = oracle của `TC-ASN-019`; `FoxEco`/`Đăng xuất` vắng ở `stag_huyennhk@` = phát hiện phân quyền) — ⛔ không phải locator hỏng.
