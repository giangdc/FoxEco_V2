# Vibe Locators — v1.1 — VR-009 — 2026-09-19

> Captured via **Appium MCP** (UiAutomator2) · app `com.hrisproject.stag` · Module **ASN**
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md` · Tài khoản: `stag_anhdc4@` (B) ↔ `stag_giangdc2@` (D), 3 lượt đổi
> 🔑 **Phiên này gần như không harvest locator mới** — 9 màn đều đã có trong `locators/vibe-locators-latest.md`, nên giá trị đóng góp nằm ở
> **(a) tái xác nhận locator cũ vẫn đúng**, **(b) 4 chứng cứ âm mới**, **(c) 2 bẫy mới `T-ASN-07`/`T-ASN-08`**, **(d) đính chính oracle `SEED Sx`**.

## Màn: Thông báo — đếm & định danh thông báo khớp tuyến ★

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Thông báo khớp tuyến thứ **N** | find + tap | -android uiautomator | `new UiSelector().textContains("Tìm thấy đơn hàng phù hợp tuyến của bạn — xem chi tiết").instance(N)` | ✅ | mcp-log TC-ASN-010/011/012/022 | **010 · 011 · 012 · 022** |
| ↳ ★🆕 **Đếm số thông báo bằng `.instance(N)`** | verify_absent | -android uiautomator | `…instance(1)` 🚫 NOT FOUND ⇒ danh sách có **đúng 1** | 🚫 NOT FOUND *(chủ ý ×4)* | mcp-log TC-ASN-010/011/012/022 | 🔑 **Kỹ thuật đếm rẻ nhất** cho nhóm trần `014/015/016/017/025`: dò `instance(k)` tăng dần tới khi NOT_FOUND, ⛔ không cần dump page source |
| ↳ ⚠️ khớp trên **phụ đề**, ⛔ không khớp tiêu đề | — | — | tiêu đề bị xuống dòng nên `textContains` trên tiêu đề dễ trượt; phụ đề `…— xem chi tiết để nhận giao` là chuỗi **1 dòng, ổn định** | ✅ | mcp-log TC-ASN-010 | — |
| Thông báo **đã đọc** vs **chưa đọc** | verify | *(dấu hiệu thị giác)* | chưa đọc = chấm đỏ + vạch cam trái · đã đọc = mất cả hai, **nhưng dòng vẫn còn** | ⚠️ Inferred | mcp-log 15:46 | ⇒ tin đã ghép **vẫn chiếm slot** trong danh sách |
| Icon chuông | find + tap | accessibility id | `Thông báo` | ✅ | mcp-log TC-ASN-007/010/011/012/022 | ⚠️ **chỉ có ở Trang chủ** — tái xác nhận VR-008 |

## Màn: Chi tiết tin — ★ ĐÍNH CHÍNH oracle định danh tin

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| ★🆕 **Tuổi tin (header)** | verify | -android uiautomator | `new UiSelector().text("5 giờ trước")` · `("19 phút trước")` | ✅ | mcp-log TC-ASN-020, 010 | 🔑 **Oracle định danh tin THAY THẾ** — xem đính chính dưới |
| 🔴 **Mục `GHI CHÚ`** | verify_absent | — | **KHÔNG TỒN TẠI** trên màn Chi tiết tin | 🚫 NOT FOUND | mcp-log **A6** *(page source đầy đủ)* | 🔴 **ĐÍNH CHÍNH VR-008** — xem dưới |
| CTA "Tôi mang giúp được" | find + tap | -android uiautomator | `new UiSelector().textContains("Tôi mang giúp được")` | ✅ | mcp-log TC-ASN-020, 010 | tái xác nhận |
| Nhãn `"Nhận giao"` *(theo Steps TC-ASN-010)* | verify_absent | -android uiautomator | `new UiSelector().textContains("Nhận giao")` | 🚫 **NOT FOUND** *(chủ ý)* | mcp-log TC-ASN-010 | 🔴 **chứng cứ sai lệch tài liệu** |
| Thứ tự khối trên màn | — | — | `ẢNH SẢN PHẨM` → `THÔNG TIN HÀNG` → `LỘ TRÌNH` → `KHUNG GIỜ` → `NGƯỜI GỬI` → CTA | ✅ | mcp-log A6 | ⛔ **không có** khối Ghi chú ở giữa |

> 🔴 **ĐÍNH CHÍNH QUAN TRỌNG cho `implement-automation` và cho phiên sau.**
> `vibe-locators-latest.md` (merge VR-008) ghi mẹo: *"ghi mã seed vào ô GHI CHÚ lúc đăng ⇒ sau này assert thông báo trỏ đúng tin nào bằng chuỗi"*
> với dòng `scroll_to + verify textContains("SEED S1")` đánh ✅.
> **Phiên này kiểm lại bằng `appium_get_page_source` đầy đủ: màn `Chi tiết tin` KHÔNG render mục `GHI CHÚ`** ⇒ mẹo đó **không dùng được ở màn này**.
> ✅ **Oracle thay thế đã kiểm chứng (2 dấu hiệu độc lập):**
> 1. **Tuổi tin ở header** Chi tiết tin (`19 phút trước`) đối chiếu **giờ đăng** đã ghi lại — cũng chính là nhãn trên card Bảng tin;
> 2. **Ảnh sản phẩm** — chọn ảnh seed **khác màu** cho mỗi lô thì nhận diện được bằng mắt trên ảnh evidence (lô này dùng **ảnh xanh lá**).
> 🔑 Và để phân biệt các tin **trùng tuyến + trùng buổi**, dùng **chữ ký `tuyến + khung giờ` trên card Bảng tin** (`TC-ASN-011/012/022` khai thác đúng điểm này).

## Màn: Bảng tin — card tin

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| ★🆕 Card theo **tuổi tin** | find + tap | -android uiautomator | `new UiSelector().text("5 giờ trước")` | ✅ | mcp-log TC-ASN-020 | 🔑 cách chọn **đúng 1 tin** giữa 3 card trùng tuyến/buổi; tap vào nhãn giờ **mở được** card |
| Chữ ký điểm giao | scroll_to + verify | -android uiautomator | `new UiSelector().textContains("FPT Tân Thuận 1")` · `("FTEL SG08")` | ✅ | mcp-log TC-ASN-005/007/011 | dùng cả **khẳng định** (011) lẫn **phủ định** (005/007) |
| Chữ ký khung giờ | scroll_to + verify | -android uiautomator | `textContains("22/09/2026")` · `textContains("Sau giờ làm")` | ✅ | mcp-log TC-ASN-012/022 | phân biệt seed lệch ngày / lệch buổi |

## Màn: Theo dõi đơn + Hoạt động — tái xác nhận oracle phân vai

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| §NGƯỜI GỬI — SĐT sau ghép | scroll_to + verify | -android uiautomator | `new UiSelector().text("0343439724")` | ✅ | mcp-log TC-ASN-010 | SĐT của `stag_anhdc4@`; cụm hiện **tên + SĐT + email**, nút `Gọi` bật |
| Tiền tố card = vai | find + get_text | -android uiautomator | `new UiSelector().textStartsWith("Giao:")` → `Giao: Tài liệu \| Giá trị thấp` | ✅ | mcp-log TC-ASN-020 | tái xác nhận oracle VR-008 trên **tài khoản thứ 3** |
| SĐT **người ngoài cặp** không thấy | verify_absent | -android uiautomator | `textContains("0833329408")` · `textContains("0343439724")` | 🚫 NOT FOUND *(chủ ý ×2)* | mcp-log TC-ASN-005 | **TC-ASN-005 E5** |

## Màn: Form OFFER + Wizard NEED — tái xác nhận (⛔ không có element mới)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Chip buổi — 4 giá trị | find + tap | -android uiautomator | `textStartsWith("Chiều (13")` · `("Sau giờ làm")` · `("Sáng (8")` · `("Giờ nào cũng được")` | ✅ | mcp-log SEED OFFER-C1/N1–N4 | ⚠️ nhãn thật `Sáng (8–12h)` — **lần thứ 3** xác nhận fragment ghi *"(6–12h)"* là **sai tài liệu** |
| Gợi ý địa chỉ | find + tap | -android uiautomator | `new UiSelector().resourceId("address-suggestion-0")` | ✅ | mcp-log SEED ×10 | 🔴 bẫy T11/T-ASN-02 tái xác nhận: **bắt buộc** tap gợi ý |
| Bộ đếm ảnh | verify | -android uiautomator | `new UiSelector().text("1/5")` | ✅ | mcp-log SEED N1–N4 | 🔑 assert sau mỗi lần Add (bẫy T-ASN-01) — 4/4 lần đều `1/5` ngay lần đầu khi dùng ảnh nhỏ |
| Nút `Tiếp theo` bước 1 | get_attribute + tap | -android uiautomator | `new UiSelector().text("Tiếp theo")` | ✅ | mcp-log SEED N1 | `enabled=true` sau khi đủ 4 điều kiện (giá trị + trọng lượng + kích thước + ≥1 ảnh) |
| Checkbox điều khoản NEED | tap | -android uiautomator | `new UiSelector().resourceId("post-n3-consent-checkbox")` | ✅ | mcp-log SEED N1–N4 | ⚠️ cần `scroll_to_element` trước |
| Checkbox điều khoản **OFFER** | tap *(toạ độ)* | *(không có locator riêng)* | tap `(52, y_text)` | ⚠️ Inferred | mcp-log SEED OFFER-C1 | ⛔ OFFER **không có** resourceId như NEED — tái xác nhận |
| `Từ ngày` → date picker | find + tap | -android uiautomator | `text("Từ ngày")` → `text("22")` | ✅ | mcp-log SEED N4 | ⚠️ chọn `Từ ngày` thì **`Đến ngày` tự nhảy theo** — tái xác nhận |
| Ô email người nhận | set_value | -android uiautomator | `new UiSelector().text("Email công ty người nhận")` | ✅ | mcp-log SEED N1–N4 | ⭐ **`stag_huyennhk@` autofill ĐÚNG** tên + SĐT `0989014863` — xem T-ASN-08 |
| Màn đăng nhập FoxPro | set_value/tap | -android uiautomator | `text("Nhập email đăng nhập")` · `text("NHẬN MÃ OTP")` · `text("ĐĂNG NHẬP")` · `text("Đăng xuất")` · `text("Đồng ý")` | ✅ | mcp-log ×3 lượt đổi | 3/3 lượt đổi tài khoản thành công |

## 🪤 Bẫy mới của phiên này

| # | Bẫy | Hiện tượng | Cách xử lý |
|---|---|---|---|
| **T-ASN-07** | **`NHẬN MÃ OTP` có thể trả lỗi mạng giả** | Bấm lần 1 → dialog *"Không thể kết nối mạng! Vui lòng kiểm tra lại."* dù `adb shell ping 8.8.8.8` **0% packet loss** (~294ms). Bấm lại lần 2 → OK ngay | ⛔ Đừng kết luận mất mạng/hỏng tài khoản. **Retry 1 lần** trước khi báo lỗi. Dialog là **in-app**, đóng bằng `find text("Đồng ý") + tap` (⛔ không phải alert hệ thống nên MCP vẫn thao tác được) |
| **T-ASN-08** | **Autofill SĐT người nhận đúng/sai TUỲ TÀI KHOẢN** | `stag_huyennhk@` → autofill **đúng** `0989014863`. Nhưng VR-008 ghi `stag_thuyntt22@` → autofill ra **MNV** `0000002352` rồi app báo *"Số điện thoại không hợp lệ"* | ⇒ `BUG-008` **không phải lỗi toàn cục**, mà phụ thuộc **HRIS có SĐT hay không**. Khi seed, **ưu tiên `stag_huyennhk@`** để ⛔ không vướng bug. Cần bổ sung thông tin này vào `BUG-008` |
| **T-ASN-09** | **Thông báo khớp tuyến có thể BIẾN MẤT hàng loạt** | 14:49 có 3 thông báo; sau đó `HÔM NAY` rỗng, **force-stop + relaunch vẫn rỗng**. Mọi tin liên quan đều buổi `Sáng`, quan sát lúc 14:49 (ngoài khung 8–12h) | ⚠️ **Giả thuyết chưa chốt:** hết hiệu lực khi khung giờ trôi qua. ⇒ **Chạy nhóm TC thông báo khi khung giờ CÒN MỞ**, và luôn seed 1 tin **khớp đủ** làm **chứng cứ dương đối chứng** — nếu không, mọi TC âm đều "đạt" một cách vô nghĩa |

## Navigation Flow (chỉ flow đã đi qua bằng MCP trong run này)

| From | Trigger | To | MCP-verified |
|------|---------|-----|--------------|
| FoxPro `Cá nhân` | scroll → `Đăng xuất` → `Đồng ý` | màn login FoxPro | ×3 lượt |
| màn login | email → `NHẬN MÃ OTP` → `adb input` OTP → `ĐĂNG NHẬP` | FoxPro Trang chủ | ×3 lượt |
| FoxPro `Chức năng` | scroll → `FoxEco` | FoxEco Trang chủ | ×3 lượt |
| FoxEco Trang chủ | `Đăng tin` → `Tôi nhận giao hàng` → điền → `Đăng tin ngay` | *"Đã ghi nhận tuyến đường!"* | SEED OFFER-C1 |
| FoxEco Trang chủ | `Đăng tin` → `Tôi cần gửi hàng` → wizard 3 bước | *"Đăng tin thành công!"* → CTA `Theo dõi đơn`/`Về trang chủ` | SEED N1–N4 |
| màn Thông báo | tap thông báo khớp tuyến | **Chi tiết tin** của đúng tin NEED | TC-ASN-010 |
| Chi tiết tin | `Tôi mang giúp được` → `Xác nhận` | **Theo dõi đơn** vai carrier | TC-ASN-010/020 |
| Bảng tin | tap nhãn tuổi tin (`5 giờ trước`) | Chi tiết tin của **đúng** card đó | TC-ASN-020 |

## Thống kê VR-009

| Màn đã harvest | Elements ghi nhận | ✅ Verified | ⚠️ Inferred | 🚫 NOT FOUND |
|---|--:|--:|--:|--:|
| **9** (Thông báo · Chi tiết tin · Bảng tin · Theo dõi đơn · Hoạt động · form OFFER · wizard NEED ×3 bước · login FoxPro · FoxPro Cá nhân) | **28** | **22** | **3** | **3\*** |

> \* 3 dòng `🚫 NOT FOUND` đều **chủ ý** làm chứng cứ âm (mục `GHI CHÚ` · nhãn `"Nhận giao"` · SĐT với người ngoài cặp) — ⛔ không phải locator hỏng.
> 🔑 **Đóng góp lớn nhất của phiên: (1) kỹ thuật ĐẾM thông báo bằng `.instance(N)`** — chìa khoá cho cả nhóm trần `014/015/016/017/025` chưa chạy;
> **(2) đính chính oracle `SEED Sx`** vốn đang sai trong `latest` và sẽ khiến phiên sau/automation đi vào ngõ cụt.
