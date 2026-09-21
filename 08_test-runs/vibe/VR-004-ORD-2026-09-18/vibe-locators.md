# Vibe Locators — v1.1 (+ CARRIED v1.0) — VR-004 — 2026-09-18

> Captured via **Appium MCP** (UiAutomator2) trong phiên này. Platform: **mobile** · emulator-5554 · 720x1280
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md` · Ưu tiên strategy: `accessibility id` > `-android uiautomator resourceId` > `xpath`
> 🔁 Màn **Đăng tin mới** · **Wizard Bước 1/3** · **Bottom sheet ảnh** · **Photo Picker** đã có đầy đủ ở `locators/vibe-locators-latest.md` (VR-002) và được **re-verify OK** trong phiên này ⇒ **không chép lại**; dưới đây chỉ ghi **màn mới** + **đính chính**.

## 🔴 4 BẪY KỸ THUẬT MỚI ở VR-004 (bổ sung T1–T5 của VR-001, T6–T10 của VR-002)

| # | Bẫy | Bằng chứng trong run này | Cách làm đúng |
|---|---|---|---|
| **T11** ⭐ **quan trọng nhất** | **CẢ HAI ô địa chỉ ở Bước 2/3 là autocomplete BẮT BUỘC chạm gợi ý.** Gõ tay đủ chữ, text hiển thị đúng, nhưng không tap `address-suggestion-N` ⇒ `Tiếp theo` **giữ `enabled=false` vĩnh viễn và app KHÔNG báo gì** | Mất ~20 MCP call để khoanh vùng ở `TC-ORD-004`. Ghi chú VR-002 *"KHÔNG có dropdown gợi ý ở ô này"* chỉ đúng khi ô **chưa được gõ** | Luôn `set_value` **một phần** tên (vd `"Cẩm Lệ"`) → `find(accessibility id "address-suggestion-0")` → `tap` → `get_text` xác nhận giá trị đã đổi thành chuỗi gợi ý |
| **T12** | **`(//android.widget.EditText)[N]` KHÔNG ổn định** ở Bước 2/3 — màn render **lazy**, số EditText trong cây đổi theo vị trí cuộn | Khi đang ở cuối form, `[2]` trả về **`alt-receiver-name-input`** chứ không phải SĐT người gửi (`TC-ORD-018`) | Dùng `xpath` theo **`@hint` + `@enabled`**: `//android.widget.EditText[@hint="Số điện thoại" and @enabled="true"]`, hoặc `resourceId` |
| **T13** | **Lỗi validate chỉ cập nhật khi RỜI Ô (on blur — `VAL-02`)** — ⛔ *không phải bug "lỗi dính"* | `TC-ORD-083` (VR-004): lỗi `Địa chỉ giao phải khác địa chỉ lấy hàng` **vẫn hiện** khi ô đang được sửa mà **chưa rời ô** | ⛔ Sau mỗi lần nhập/sửa PHẢI **rời ô** (tap nhãn/vùng trống; `hideKeyboard` không đảm bảo mất focus) rồi mới đọc lỗi, và ghi bước rời ô thành dòng riêng trong log. Đồng thời **không** đọc lỗi ngay sau TC trước — vào lại form sạch. Không blur ⇒ kết luận sai cả PASS lẫn FAIL |
| **T14** | Element ở **cuối form** bị **bottom bar cố định che** ⇒ `find` được nhưng thao tác/đọc lỗi bên dưới nó thì không thấy | `TC-ORD-081`: lỗi `Tên phải từ 2–60 ký tự` chỉ hiện sau khi cuộn thêm 1 nhịp | Sau khi tap nút submit, **cuộn 1 nhịp** rồi mới assert vùng lỗi |

## 🔑 Bảng vàng: điều kiện enable của 2 nút `Tiếp theo` (đo được trong phiên này)

| Nút | Điều kiện ĐỦ để `enabled=true` |
|---|---|
| **Bước 1/3** | giá trị hàng **+** TRỌNG LƯỢNG **+** KÍCH THƯỚC **+** ≥1 ảnh *(4 điều kiện — xác nhận lại VR-002)* |
| **Bước 2/3** | email **tra thấy HRIS** + tên người nhận + SĐT người nhận hợp lệ + **địa chỉ lấy hàng CHỌN TỪ GỢI Ý** + **địa chỉ giao CHỌN TỪ GỢI Ý** + ≥1 buổi *(⭐ 2 điều kiện địa chỉ là phát hiện MỚI của VR-004)* |
| **Bước 3/3** (`Đăng tin ngay`) | tick checkbox điều khoản *(1 điều kiện)* |

## Screen: Wizard Bước 3/3 "Xác nhận & Đăng tin" ★ **MÀN MỚI** *(VR-002 chưa từng tới được)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Step indicator | get_text | -android uiautomator | `new UiSelector().text("Bước 3 / 3")` | ✅ | mcp-log TC-ORD-004 | TC-ORD-004/034/037/081 |
| Tiêu đề bước | get_text | -android uiautomator | `new UiSelector().text("Xác nhận & Đăng tin")` | ✅ | mcp-log TC-ORD-034 | TC-ORD-034 |
| Nút "←" lùi về bước 2 | tap | accessibility id | `Quay lại` | ✅ | mcp-log TC-ORD-004 | TC-ORD-004/081 |
| Tiêu đề khối tóm tắt | get_text | -android uiautomator | `new UiSelector().text("Tóm tắt đơn gửi hàng")` | ✅ | mcp-log TC-ORD-034 | TC-ORD-034 |
| Dòng "Loại hàng" | get_text | *(TextView sau nhãn)* | nhãn `Loại hàng` → giá trị `Tài liệu · Giá trị thấp` | ✅ | mcp-log TC-ORD-034 | TC-ORD-034 |
| Dòng "Khung giờ" | get_text | — | nhãn `Khung giờ` → `18/09/2026 – 19/09/2026 · Chiều` | ✅ | mcp-log TC-ORD-034 | TC-ORD-034 |
| Dòng "Người gửi" | get_text | — | `Đặng Châu Giang · 0964633310` + dòng 2 = địa chỉ lấy | ✅ | mcp-log TC-ORD-034 | TC-ORD-034 |
| Dòng "Người nhận" | get_text | — | `Đặng Châu Anh · 0343439724` + dòng 2 = địa chỉ giao | ✅ | mcp-log TC-ORD-034 | TC-ORD-034 |
| Dòng "Ghi chú" | get_text | — | nhãn `Ghi chú` → nội dung ô GHI CHÚ bước 1 | ✅ | mcp-log TC-ORD-034 | TC-ORD-034 |
| ↳ ⚠️ **tóm tắt KHÔNG có** TRỌNG LƯỢNG · KÍCH THƯỚC · ảnh | verify_absent | — | *(không có node nào)* | 🚫 **NOT FOUND** *(spec gap — xem TC-ORD-034)* | mcp-log TC-ORD-034 | TC-ORD-034 |
| **Banner hàng cấm** | get_text | -android uiautomator | `new UiSelector().textStartsWith("Không được gửi")` | ✅ | mcp-log TC-ORD-035 | TC-ORD-035 |
| ↳ chuỗi thật | — | — | `Không được gửi: thuốc, vũ khí, chất nguy hiểm, hàng phi pháp. FoxEco là nền tảng kết nối, không chịu trách nhiệm về nội dung hàng.` | ✅ | — | — |
| **Checkbox điều khoản** | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Tôi đã đọc và đồng ý")` | ✅ | mcp-log TC-ORD-037 | TC-ORD-004/036/037/050 |
| ↳ ⚠️ đọc trạng thái tick | — | — | **phải đọc bằng ảnh** (bẫy **T1**) — mặc định **CHƯA** tick | ✅ | mcp-log TC-ORD-036 | TC-ORD-036 |
| **Nút "Đăng tin ngay"** | tap · get_element_attribute | accessibility id | `Đăng tin ngay` | ✅ | mcp-log TC-ORD-037 | TC-ORD-004/037/050 |
| ↳ đọc enable/disable | — | — | dùng `enabled` (`false` khi chưa tick → `true` sau khi tick) | ✅ | mcp-log TC-ORD-037 | TC-ORD-037/050 |
| ↳ 🐞 **nhấn khi đã đủ điều kiện ⇒ KHÔNG có gì xảy ra** | — | — | API trả **400 `REQ_400`**, app im lặng — xem `logcat-TC-ORD-004-REQ_400.txt` | ✅ | mcp-log TC-ORD-004 | TC-ORD-004 |

## Screen: Bước 2/3 — khối NGƯỜI NHẬN UỶ QUYỀN ★ **MỚI**

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Nút mở khối uỷ quyền | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Thêm người nhận uỷ quyền")` | ✅ | mcp-log TC-ORD-079 | TC-ORD-079/081 |
| ↳ ⚠️ `accessibility id "alt-receiver-expand-button"` | — | accessibility id | *(VR-002 ghi ⚠️ Inferred)* | 🚫 **NOT FOUND** | mcp-log TC-ORD-079 | — *(dùng descriptionStartsWith thay thế)* |
| Container khối uỷ quyền | — | -android uiautomator | `new UiSelector().resourceId("alt-receiver-box")` | ✅ | mcp-log TC-ORD-079 | TC-ORD-079 |
| Nút "×" đóng/xoá khối | — | -android uiautomator | `new UiSelector().resourceId("alt-receiver-collapse-button")` | ⚠️ Inferred | mcp-log TC-ORD-079 | ⏳ TC-ORD-082 *(thấy trong cây + trong ảnh, chưa tap)* |
| **Tên người được uỷ quyền** | type · get_text | -android uiautomator | `new UiSelector().resourceId("alt-receiver-name-input")` | ✅ | mcp-log TC-ORD-081 | TC-ORD-079/081 |
| ↳ thuộc tính | — | — | `max-text-length=60` · hint `Tên người được uỷ quyền` | ✅ | — | TC-ORD-081 |
| ↳ lỗi độ dài | get_text | -android uiautomator | `new UiSelector().text("Tên phải từ 2–60 ký tự")` | ✅ | mcp-log TC-ORD-081 | TC-ORD-081 |
| **SĐT người được uỷ quyền** | type | -android uiautomator | `new UiSelector().resourceId("alt-receiver-phone-input")` | ✅ | mcp-log TC-ORD-079 | TC-ORD-079 |
| ↳ thuộc tính | — | — | `max-text-length=12` · hint `Số điện thoại` | ✅ | — | — |
| ↳ lỗi định dạng | get_text | -android uiautomator | `new UiSelector().text("Số điện thoại không hợp lệ")` | ✅ | mcp-log TC-ORD-079 | TC-ORD-079 |
| Ô "Quan hệ / vị trí" | — | -android uiautomator | `new UiSelector().resourceId("alt-receiver-note-input")` | ⚠️ Inferred | mcp-log TC-ORD-079 | — *(maxlen=60; chưa nhập)* |
| Helper khối | get_text | -android uiautomator | `textStartsWith("Không bắt buộc")` → `Không bắt buộc · người vận chuyển có thể giao cho người này nếu không gặp được người nhận` | ✅ | mcp-log TC-ORD-079 | — |

## Screen: Bước 2/3 — bổ sung/đính chính so với VR-002

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| **Gợi ý địa chỉ (DÙNG CHO CẢ 2 Ô)** ⭐ | tap | accessibility id | `address-suggestion-0` · `address-suggestion-1` | ✅ | mcp-log TC-ORD-029 | TC-ORD-004/022/023/026/029/050 |
| ↳ ⚠️ **ĐÍNH CHÍNH VR-002** | — | — | VR-002 ghi *"KHÔNG có dropdown gợi ý ở ô địa chỉ giao"* — **SAI**: có, chỉ xuất hiện **khi đang gõ** (bẫy **T11**) | ✅ | mcp-log TC-ORD-029 | TC-ORD-028 *(cần review lại verdict)* |
| ↳ giá trị gợi ý thật trên STG | get_text | — | gõ `Cẩm Lệ` → `FTEL Đà Nẵng Cẩm Lệ` · `363 Nguyễn Hữu Thọ, Cẩm Lệ` · gõ `Lê Thái Tổ` → `Tòa V-City, Lê Thái Tổ` | ✅ | mcp-log TC-ORD-029 | — |
| SĐT người gửi *(bền hơn xpath thứ tự)* | get_text | xpath | `//android.widget.EditText[@hint="Số điện thoại" and @enabled="true"]` | ✅ | mcp-log TC-ORD-018 | TC-ORD-015/018 |
| ↳ giá trị hiện tại trên STG | — | — | **`0964633310`** *(VR-002 ghi `0912345670` — hồ sơ đã đổi ở VR-003)* | ✅ | mcp-log TC-ORD-015 | — |
| Tên người gửi *(chỉ đọc)* | tap · get_text | xpath | `//android.widget.EditText[@hint="Tên người gửi"]` | ✅ | mcp-log TC-ORD-016 | TC-ORD-015/016 |
| ↳ chứng minh chỉ-đọc | — | — | page source `enabled="false"` **+** `appium_mobile_keyboard(is_shown)` = `false` khi chạm | ✅ | mcp-log TC-ORD-016 | TC-ORD-016 |
| Địa chỉ lấy hàng | type | xpath | `//android.widget.EditText[@hint="Địa chỉ lấy hàng"]` | ✅ | mcp-log TC-ORD-017 | TC-ORD-004/017/023/026/083 |
| ↳ ⚠️ **nay RỖNG khi mở bước 2** | — | — | prefill hồ sơ **đã mất** (`TC-ORD-017` FAIL; gốc = `TC-USR-040`) — VR-002 còn thấy prefill | ✅ | mcp-log TC-ORD-017 | TC-ORD-017 |
| Lỗi trùng địa chỉ | get_text | -android uiautomator | `new UiSelector().text("Địa chỉ giao phải khác địa chỉ lấy hàng")` | ✅ | mcp-log TC-ORD-026 | TC-ORD-026 |
| ↳ 🔴 **ĐÍNH CHÍNH VR-002** | — | — | lỗi này **CÓ THẬT** — chỉ hiện khi 2 địa chỉ **đã chọn từ gợi ý**. VR-002 kết luận *"chặn im lặng"* vì gõ tay ⇒ validate chưa chạy tới luật này | ✅ | mcp-log TC-ORD-026/083 | TC-ORD-026/083/084 |
| Lỗi SĐT người nhận | get_text | -android uiautomator | `new UiSelector().text("Số điện thoại không hợp lệ")` | ✅ | mcp-log TC-ORD-025 | TC-ORD-025/079 |
| ↳ ⚠️ **dùng chung chuỗi** với ô SĐT uỷ quyền | — | — | phải **loại nhiễu** (đưa ô kia về giá trị hợp lệ) trước khi quy lỗi cho 1 ô | ✅ | mcp-log TC-ORD-079 | TC-ORD-079 |
| ⚠️ **KHÔNG có** lỗi cho ô **email** và ô **tên người nhận** | verify_absent | -android uiautomator | đã quét `textContains` cho `định dạng` · `không hợp lệ` · `Không tìm thấy` · `Tên` | 🚫 **NOT FOUND** *(bug F3/F7)* | mcp-log TC-ORD-021/024/051 | TC-ORD-021/023/024/051 |

## Screen: Form OFFER "Tôi nhận giao hàng" ★ **MÀN MỚI**

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tiêu đề màn | get_text | -android uiautomator | `new UiSelector().text("Tôi nhận giao hàng")` | ✅ | mcp-log TC-ORD-003 | TC-ORD-003/042 |
| ↳ ⚠️ **KHÔNG có** step indicator | verify_absent | -android uiautomator | `new UiSelector().textContains("Bước")` | 🚫 **NOT FOUND** *(đúng kỳ vọng)* | mcp-log TC-ORD-003 | TC-ORD-003/042 |
| Banner intro | get_text | -android uiautomator | `textStartsWith("Hệ thống sẽ tự tìm kiếm")` | ✅ | mcp-log TC-ORD-042 | TC-ORD-042 |
| Họ tên *(prefill)* | get_text | xpath | `//android.widget.EditText[@hint="Họ tên"]` → `Đặng Châu Giang` | ✅ | mcp-log TC-ORD-042 | TC-ORD-042 |
| SĐT *(prefill)* | get_text | xpath | `//android.widget.EditText[@hint="Số điện thoại"]` → `0964633310` | ✅ | mcp-log TC-ORD-042 | TC-ORD-042 |
| **ĐIỂM XUẤT PHÁT (A)** | type · get_text | xpath | `//android.widget.EditText[@hint="Bạn đang ở đâu / xuất phát từ đâu"]` | ✅ | mcp-log TC-ORD-043 | TC-ORD-043/050 |
| ↳ ⚠️ **KHÔNG prefill** nơi làm việc | — | — | `get_text` trả về **chính hint** ⇒ rỗng (`TC-ORD-043` FAIL) | ✅ | mcp-log TC-ORD-043 | TC-ORD-043 |
| **ĐIỂM ĐẾN (B)** | type · get_text | xpath | `//android.widget.EditText[@hint="Bạn sẽ đến đâu"]` | ✅ | mcp-log TC-ORD-050 | TC-ORD-043/050 |
| ↳ gợi ý địa chỉ | tap | accessibility id | `address-suggestion-0` *(giống Bước 2/3)* | ✅ | mcp-log TC-ORD-050 | TC-ORD-043/050 |
| 4 chip BUỔI của OFFER | tap | -android uiautomator | `resourceId("offer-day-part-morning")` · `-afternoon` · `-after_work` · `-anytime` | ✅ *(`-afternoon` đã tap)* | mcp-log TC-ORD-043 | TC-ORD-042/043/050 |
| ↳ ⚠️ **prefix `offer-` RIÊNG**, KHÔNG dùng chung `day-part-*` của NEED | — | — | — | ✅ | mcp-log TC-ORD-050 | — |
| Lỗi "chưa chọn buổi" | get_text | -android uiautomator | `new UiSelector().text("Chọn ít nhất 1 buổi")` | ✅ | mcp-log TC-ORD-050 | TC-ORD-050 |
| Checkbox điều khoản | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Tôi đã đọc và đồng ý")` | ✅ | mcp-log TC-ORD-050 | TC-ORD-043/050 |
| **Nút "Đăng tin ngay"** | tap · get_element_attribute | accessibility id | `Đăng tin ngay` | ✅ | mcp-log TC-ORD-050 | TC-ORD-043/050 |
| ↳ 🐞 **LUÔN `enabled=true`** dù thiếu trường | — | — | khác hẳn NEED (disable). Nhấn ⇒ **không đăng** + hiện lỗi inline ⇒ xem `TC-ORD-050` | ✅ | mcp-log TC-ORD-050 | TC-ORD-050 |
| ⚠️ **KHÔNG có** lỗi cho nhánh *điểm đến trùng điểm xuất phát* | verify_absent | -android uiautomator | `textContains("phải khác")` | 🚫 **NOT FOUND** *(bug — xem TC-ORD-043)* | mcp-log TC-ORD-043 | TC-ORD-043 |

## Screen: Theo dõi đơn *(chi tiết đơn)* — bổ sung VR-001

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Nút "Báo cáo sự cố" | — | -android uiautomator | `new UiSelector().resourceId("track-report-incident")` | ⚠️ Inferred | mcp-log TC-ORD-047 | — ⛔ không tap |
| Trạng thái ghép *(đơn đã ghép)* | get_text | -android uiautomator | `resourceId("track-sender-matched-status")` → `Đã ghép · chờ shipper lấy hàng` | ✅ | mcp-log TC-ORD-047 | TC-ORD-047 |
| Nút "Huỷ đơn" *(đơn đã ghép)* | — | -android uiautomator | `resourceId("track-sender-matched-cancel")` | ⚠️ Inferred | mcp-log TC-ORD-047 | — ⛔ **không tap** (sẽ huỷ đơn thật) |
| ⚠️ **KHÔNG có** nút "Chỉnh sửa" khi đơn `Đã ghép` | verify_absent | accessibility id | `Chỉnh sửa` | 🚫 **NOT FOUND** *(đúng kỳ vọng)* | mcp-log TC-ORD-047 | TC-ORD-047 |
| **Icon copy (2 cái)** | tap | -android uiautomator | `new UiSelector().description("Copy").instance(0)` = cạnh **Lấy hàng** · `.instance(1)` = cạnh **Giao hàng** | ✅ *(instance 1)* | mcp-log TC-ORD-085 | TC-ORD-085 |
| ↳ đọc kết quả copy | — | — | `appium_mobile_clipboard(action=get)` — **đặt sentinel trước khi tap** để phân biệt copy thật | ✅ | mcp-log TC-ORD-085 | TC-ORD-085 |
| ↳ 🐞 **không có phản hồi thị giác** | — | — | lấy mẫu pixel vùng icon 2 ảnh liên tiếp trong 2s: `(160,164,175)` xám, **không xanh** | ✅ | mcp-log TC-ORD-085 | TC-ORD-085 |
| Giá trị "Lấy hàng" / "Giao hàng" | get_text | -android uiautomator | TextView sau nhãn `Lấy hàng` / `Giao hàng` → `Tòa V-City, Lê Thái Tổ` / `FPT Cầu Giấy` | ✅ | mcp-log TC-ORD-085 | TC-ORD-085 |
| Timeline trạng thái | get_text | -android uiautomator | `text("Chờ ghép")` · `("Lấy hàng")` · `("Đang giao")` · `("Đã giao")` · `("Hoàn thành")` | ✅ | mcp-log TC-ORD-047 | TC-ORD-047 |
| ⚠️ **KHÔNG có** số điện thoại nào trên màn | verify_absent | — | quét toàn page source: 0 node chứa SĐT | 🚫 **NOT FOUND** *(⇒ `TC-ORD-086` BLOCKED)* | mcp-log TC-ORD-086 | TC-ORD-086 |

## Screen: Đơn của tôi *(tab Hoạt động)* — bổ sung

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Card đơn *(fallback theo nội dung)* | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Gửi: Tài liệu")` | ✅ | mcp-log TC-ORD-047 | TC-ORD-047/085/086 |
| Dữ liệu đơn có sẵn trên STG *(hữu ích cho phiên sau)* | — | — | `Gửi: Tài liệu \| Giá trị thấp` **Đã ghép** · `Nhận: Đồ dễ vỡ \| Giá trị vừa` **Đã huỷ** · `Nhận giao hàng Thuận đường` **Đã giao** | ✅ | mcp-log TC-ORD-047 | — |

## Navigation Flow (chỉ flow đã đi qua bằng MCP trong run này)

| From | Trigger | To | MCP-verified |
|---|---|---|---|
| Đăng tin mới | tap card `Tôi nhận giao hàng` | **Form OFFER 1 trang** | TC-ORD-001 step 5 · TC-ORD-003 |
| Form OFFER | `appium_gesture(back)` | Đăng tin mới | TC-ORD-050 step 6 |
| Wizard Bước 2/3 | tap `Tiếp theo` *(đủ 6 điều kiện, gồm 2 địa chỉ chọn từ gợi ý)* | **Bước 3/3** | TC-ORD-004 step 9 |
| Wizard Bước 3/3 | tap `Quay lại` | Bước 2/3 | TC-ORD-004 · TC-ORD-081 |
| Wizard Bước 3/3 | tap `Đăng tin ngay` *(đã tick, đủ dữ liệu)* | 🐞 **KHÔNG đi đâu** — API 400, app im lặng | TC-ORD-004 step 11 |
| Bước 1/3 | `appium_gesture(back)` ×1 | Đăng tin mới *(mất draft, không popup)* | TC-ORD-050 |
| Đăng tin mới | `appium_gesture(back)` | FoxEco Trang chủ | TC-ORD-050 step 6 |
| Trang chủ | tap `Hoạt động` | **Đơn của tôi** (2 tab `Đang diễn ra` / `Đã hoàn thành`) | TC-ORD-047 step 3 |
| Đơn của tôi | tap card đơn | **Theo dõi đơn** | TC-ORD-047 step 3 |

## Thống kê VR-004

| Chỉ số | Giá trị |
|---|---|
| Màn đã harvest trong phiên | **6** (Form OFFER · Wizard B1 *(lại)* · Wizard B2 · **Wizard B3 — mới** · khối uỷ quyền · Theo dõi đơn) |
| Tổng `appium_get_page_source` | **8** |
| Element MỚI ghi vào map | **≈ 41** (B3: 8 · OFFER: 11 · uỷ quyền: 5 · Theo dõi đơn: 6 · bổ sung B2: 11) |
| Đính chính map của phiên trước | **4** (dropdown gợi ý 2 ô địa chỉ · lỗi trùng địa chỉ CÓ THẬT · SĐT người gửi đổi giá trị · `alt-receiver-expand-button` NOT FOUND) |
| Bẫy kỹ thuật mới | **4** (T11–T14) |
