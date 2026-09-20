# Vibe Locators — v1.1 — VR-008 — 2026-09-19

> Captured via **Appium MCP** (UiAutomator2) · app `com.hrisproject.stag` · Module **ASN**
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md` · Tài khoản: `stag_anhdc4@` (B) → `stag_taipm@` (A) → `stag_anhdc4@` (B)
> 🔑 Đóng góp chính của phiên: **luồng ghép đơn đầy đủ** (modal xác nhận · huỷ nhận đơn + lý do · Theo dõi đơn 2 vai) và **wizard NEED chạy trọn vẹn 3 bước**.

## Màn: Chi tiết tin — cụm ghép đơn

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| CTA "Tôi mang giúp được" | find + tap | -android uiautomator | `new UiSelector().textContains("Tôi mang giúp được")` | ✅ | mcp-log TC-ASN-002, 001, 020 | TC-ASN-001/002/020 |
| **Modal "Xác nhận mang giúp"** 🆕 | verify | -android uiautomator | `new UiSelector().text("Xác nhận mang giúp")` | ✅ | mcp-log TC-ASN-002 | TC-ASN-002 — tiêu đề modal; phụ đề: *"Nhận mang giúp ngay — SĐT sẽ lộ cho cả hai bên để liên hệ."* |
| ↳ Nút "Huỷ" trên modal 🆕 | find + tap | -android uiautomator | `new UiSelector().text("Huỷ")` | ✅ | mcp-log TC-ASN-002 | TC-ASN-002 — đóng modal, ⛔ không tạo tác động |
| ↳ Nút "Xác nhận" trên modal 🆕 | find + tap | -android uiautomator | `new UiSelector().text("Xác nhận")` | ✅ | mcp-log TC-ASN-001, 020 | TC-ASN-001/020 — ghép đơn |
| §NGƯỜI GỬI — tiêu đề cụm | scroll_to + verify | -android uiautomator | `new UiSelector().textContains("NGƯỜI GỬI")` | ✅ | mcp-log TC-ASN-002 | TC-ASN-002/004 |
| ↳ SĐT người gửi **trước** ghép | verify_absent | -android uiautomator | `new UiSelector().text("0833329408")` | 🚫 NOT FOUND *(chủ ý)* | mcp-log TC-ASN-002 | **TC-ASN-002** — chứng cứ âm: chưa ghép thì ⛔ không lộ SĐT |
| ↳ Nút "Gọi" **trước** ghép | verify | -android uiautomator | `new UiSelector().text("Gọi")` | ⚠️ Inferred | mcp-log TC-ASN-002 | hiển thị nhưng **mờ/disabled** |

## Màn: Theo dõi đơn — vai **người vận chuyển** (carrier)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tiêu đề màn | verify | -android uiautomator | `new UiSelector().text("Theo dõi đơn")` | ✅ | mcp-log TC-ASN-001 | TC-ASN-001 |
| Stepper 5 mốc | verify | -android uiautomator | `text("Chờ ghép")` · `("Lấy hàng")` · `("Đang giao")` · `("Đã giao")` · `("Hoàn thành")` | ⚠️ Inferred | mcp-log TC-ASN-001 | sau ghép: sáng tới mốc `Lấy hàng` |
| CTA "Tôi đã lấy hàng" | verify | -android uiautomator | `new UiSelector().text("Tôi đã lấy hàng")` | ⚠️ Inferred | mcp-log TC-ASN-001 | ⛔ phiên này KHÔNG bấm (giữ tiền đề "trước khi lấy hàng") |
| **CTA "Huỷ nhận đơn"** 🆕 | find + tap | -android uiautomator | `new UiSelector().text("Huỷ nhận đơn")` | ✅ | mcp-log TC-ASN-020 | **TC-ASN-020** |
| ↳ Ô "Lý do huỷ" (bắt buộc) 🆕 | set_value | -android uiautomator | `new UiSelector().textStartsWith("Nhập lý do bạn muốn huỷ đơn")` | ✅ | mcp-log TC-ASN-020 | placeholder đầy đủ: *"Nhập lý do bạn muốn huỷ đơn (VD: đổi lịch, không cần gửi nữa...)"* |
| ↳ Nút "Xác nhận" của modal huỷ 🆕 | get_attribute + tap | -android uiautomator | `new UiSelector().text("Xác nhận")` | ✅ | mcp-log TC-ASN-020 | 🔑 `enabled` = **`false` → `true`** sau khi nhập lý do ⇒ oracle "field bắt buộc" |
| ↳ Modal kết quả "Đã huỷ" 🆕 | verify + tap | -android uiautomator | `new UiSelector().text("Đồng ý")` | ✅ | mcp-log TC-ASN-020 | nội dung: *"Đã huỷ nhận đơn. Đơn đã trả lại bảng tin."* |
| §NGƯỜI GỬI **sau** ghép — SĐT ★ | verify | -android uiautomator | `new UiSelector().text("0833329408")` | ✅ | mcp-log TC-ASN-004 | **TC-ASN-004 E3a** — cụm hiện tên + SĐT + **email**, nút `Gọi` **bật** |
| §NGƯỜI NHẬN **sau** ghép — SĐT ★ 🆕 | verify | -android uiautomator | `new UiSelector().text("0989014863")` | ✅ | mcp-log TC-ASN-004 | **TC-ASN-004 E3b** — carrier thấy cả SĐT người nhận |

## Màn: Theo dõi đơn — vai **chủ tin** (người gửi)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| **Nhãn trạng thái tĩnh** 🆕 | verify | -android uiautomator | `new UiSelector().textContains("Đã ghép · chờ shipper lấy hàng")` | ✅ | mcp-log TC-ASN-003 | **TC-ASN-003 E4** — ⛔ không bấm được, chỉ là nhãn |
| **Nút "Huỷ đơn"** (khác `Huỷ nhận đơn` của carrier) 🆕 | verify | -android uiautomator | `new UiSelector().text("Huỷ đơn")` | ⚠️ Inferred | mcp-log TC-ASN-003 | nút hành động **duy nhất** của chủ tin |
| Vắng mặt nút duyệt ★ | verify_absent | -android uiautomator | `textContains("Duyệt")` · `("Chấp nhận")` · `("Phê duyệt")` | 🚫 NOT FOUND *(chủ ý ×3)* | mcp-log TC-ASN-003 | **TC-ASN-003 E5** — chứng cứ âm cho cơ chế "ghép ngay" |
| §NGƯỜI GIAO HÀNG — SĐT carrier ★ | verify | -android uiautomator | `new UiSelector().text("0343439724")` | ✅ | mcp-log TC-ASN-004 | **TC-ASN-004 E5** |

## Màn: Đơn của tôi (tab Hoạt động) — oracle phân vai

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Badge trạng thái | find + tap | -android uiautomator | `new UiSelector().text("Đã ghép")` | ✅ | mcp-log TC-ASN-001, 003 | tap vào badge **mở được** đơn tương ứng |
| **Tiền tố card = vai của mình** ★🆕 | get_text | -android uiautomator | `new UiSelector().textStartsWith("Giao:")` → `Giao: Tài liệu \| Giá trị thấp` | ✅ | mcp-log TC-ASN-001 | 🔑 **`Giao:` = mình vận chuyển · `Gửi:` = mình là chủ tin · `Nhận giao hàng ...` = card OFFER.** Đây là oracle rẻ nhất để assert vai, ⛔ không cần mở chi tiết |
| Card OFFER của chính mình | find + tap | -android uiautomator | `new UiSelector().textStartsWith("Nhận giao hàng")` | ✅ | mcp-log lô 1 | mở ra Theo dõi đơn của OFFER, CTA = `Chỉnh sửa` / `Huỷ đơn`, nhãn *"Đang chờ người gửi ghép"* |
| §LỊCH SỬ trên OFFER 🆕 | verify | -android uiautomator | `new UiSelector().textContains("Đăng tin lên bảng tin")` | ⚠️ Inferred | mcp-log lô 1 | kèm mốc `Hôm nay · 08:29 · <tên>` ⇒ đọc được **giờ đăng chính xác** |

## Màn: Thông báo — khớp tuyến

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Icon chuông (Trang chủ FoxEco) | find + tap | accessibility id | `Thông báo` | ✅ | mcp-log TC-ASN-009 | ⚠️ chỉ tồn tại trên **Trang chủ**, ⛔ không có ở Bảng tin/Hoạt động |
| **Thông báo khớp tuyến (chọn theo thứ tự)** ★🆕 | find + tap | -android uiautomator | `new UiSelector().textContains("Tìm thấy đơn hàng phù hợp tuyến").instance(0)` | ✅ | mcp-log TC-ASN-009 | 🔑 `.instance(0)` = **mới nhất**; cần thiết khi có nhiều thông báo cùng nội dung |
| Nhóm ngày "HÔM NAY" | verify | -android uiautomator | `new UiSelector().text("HÔM NAY")` | ✅ | mcp-log TC-ASN-009 | 🚫 NOT FOUND lúc 11:44 → ✅ tìm thấy lúc 12:31 (xem cảnh báo refresh dưới) |
| Dấu định danh seed trong Chi tiết tin ★🆕 | scroll_to + verify | -android uiautomator | `new UiSelector().textContains("SEED S1")` | ✅ | mcp-log TC-ASN-009 | 🔑 **Kỹ thuật dùng lại được:** ghi mã seed vào ô **GHI CHÚ** lúc đăng ⇒ sau này assert "thông báo trỏ đúng tin nào" bằng chuỗi, ⛔ không phải suy từ timestamp |

## Màn: Wizard đăng tin NEED (3 bước) — bổ sung VR-007

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Ô GHI CHÚ (bước 1) 🆕 | set_value | -android uiautomator | `new UiSelector().textStartsWith("Lưu ý khi giao nhận")` | ✅ | mcp-log SEED S1–S4 | dùng cắm mã seed |
| Bộ đếm ảnh ★🆕 | verify | -android uiautomator | `new UiSelector().text("0/5")` / `("1/5")` | ✅ | mcp-log SEED S1 | 🔑 **oracle "ảnh đã gắn chưa"** — bắt buộc kiểm, xem bẫy T-ASN-01 |
| Chip buổi — 4 giá trị 🆕 | find + tap | -android uiautomator | `textStartsWith("Sáng (8")` · `("Chiều (13")` · `("Sau giờ làm")` · `("Giờ nào cũng được")` | ✅ | mcp-log SEED S1/S3/S4 | ⚠️ nhãn thật **`Sáng (8–12h)`** — fragment ghi *"(6–12h)"* ⇒ **sai tài liệu** (trùng phát hiện VR-007) |
| "Từ ngày" → date picker 🆕 | find + tap | -android uiautomator | `new UiSelector().text("Từ ngày")` | ✅ | mcp-log SEED S3 | mở bottom-sheet lịch `Tháng 9 2026`, ngày quá khứ **disabled**, nút đóng = `Đóng` |
| ↳ Chọn ngày trong lịch 🆕 | find + tap | -android uiautomator | `new UiSelector().text("22")` | ✅ | mcp-log SEED S3 | ⚠️ chọn `Từ ngày` thì **`Đến ngày` tự nhảy theo cùng ngày** |
| Gợi ý địa chỉ | find + tap | -android uiautomator | `new UiSelector().resourceId("address-suggestion-0")` | ✅ | mcp-log SEED S1–S4 | 🔴 bẫy **T11** tái xác nhận — xem T-ASN-02 |

## 🪤 Bẫy mới phát hiện ở phiên này (quan trọng cho implement-automation)

| # | Bẫy | Hiện tượng | Cách xử lý |
|---|---|---|---|
| **T-ASN-01** | **Ảnh quá khổ bị từ chối IM LẶNG** | Chọn `seed-ord-oversize-5mb.jpg` (5 MB) → picker đóng bình thường, ⛔ **không báo lỗi**, bộ đếm vẫn `0/5`, nút `Tiếp theo` không ăn | ⛔ Đừng tin picker đã đóng là đã gắn ảnh. **Luôn assert `text("1/5")`** sau khi Add. Dùng ảnh thường (vài trăm KB) |
| **T-ASN-02** | **Địa chỉ gõ tay không được tính là hợp lệ** | `set_value` đủ chuỗi `"FPT Cầu Giấy"` nhưng **không tap gợi ý** ⇒ `Tiếp theo` **im lặng không chuyển bước**; khi `set_value` lại thì ô **rỗng trắng** (giá trị cũ chưa từng commit) | **Bắt buộc** `resourceId("address-suggestion-N")` rồi tap. Mẹo: gõ chuỗi **ngắn hơn** (`"FPT Cầu"`) để chắc chắn dropdown bung |
| **T-ASN-03** | **Gợi ý địa chỉ có thể nằm ngoài viewport** | `find_element("address-suggestion-0")` trả NOT FOUND dù dropdown có | `scroll_to_element` tới chính `address-suggestion-0` rồi mới tap |
| **T-ASN-04** | **Màn Thông báo không tự refresh** | 11:44 danh sách chỉ có `HÔM QUA`, thiếu cả thông báo 09:43; 12:31 (sau đăng nhập lại) hiện đủ **3** thông báo hôm nay | ⛔ Đừng kết luận "không có thông báo" từ 1 lần mở. Đăng nhập lại / kill app trước khi assert chứng cứ **âm** |
| **T-ASN-05** | **`scroll_to_element` báo "already visible" nhưng phần tử ngoài màn** | Node có trong cây a11y nhưng chưa render trong viewport ⇒ scroll bị bỏ qua | Dùng `appium_gesture(action=swipe)` toạ độ tường minh; ⛔ tránh vùng widget **Bản đồ** (nuốt gesture) |
| **T-ASN-06** | **`appium_screenshot` của MCP rất đắt** | Mỗi lần gọi trả **~216.000 ký tự** HTML viewer vào context | Evidence chụp bằng `adb exec-out screencap -p > <path>` (SKILL.md cho phép cho vai trò evidence) |

## Navigation Flow

| From | Trigger | To | MCP-verified |
|------|---------|-----|--------------|
| Bảng tin | tap card tin của người khác | Chi tiết tin (**có** CTA `Tôi mang giúp được`) | TC-ASN-002 step 2 |
| Chi tiết tin | tap CTA → `Xác nhận` | **Theo dõi đơn** vai carrier | TC-ASN-001 E4 |
| Chi tiết tin | tap CTA → `Huỷ` | ở lại Chi tiết tin, ⛔ không tác động | TC-ASN-002 E4 |
| Theo dõi đơn (carrier) | `Huỷ nhận đơn` → lý do → `Xác nhận` → `Đồng ý` | tin **trở lại Bảng tin**, đơn về `Chờ ghép` | TC-ASN-020 E5 |
| Hoạt động | tap badge `Đã ghép` | Theo dõi đơn (vai tuỳ tài khoản) | TC-ASN-001/003 |
| Trang chủ | tap chuông → tap thông báo khớp tuyến | **Chi tiết tin** của đúng tin NEED khớp | TC-ASN-009 E5 |

## Thống kê

| Màn đã harvest | Elements | ✅ Verified | ⚠️ Inferred | 🚫 NOT FOUND |
|---|--:|--:|--:|--:|
| **7** (Chi tiết tin · Theo dõi đơn ×2 vai · Đơn của tôi · Thông báo · Wizard NEED ×3 bước · login FoxPro) | **34** | **25** | **5** | **4*** |

> \* 4 phép NOT FOUND đều **chủ ý** làm chứng cứ âm: SĐT trước ghép (`TC-ASN-002`) và 3 nhãn duyệt (`TC-ASN-003`). ⛔ Không phải locator hỏng.
