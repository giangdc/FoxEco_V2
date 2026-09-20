# Vibe Locators — LATEST (tích lũy xuyên run)

> ★ **`implement-automation` đọc FILE NÀY.** Pointer không mang ngày; snapshot khi đóng version → `vibe-locators-v[X].md`.
> Cập nhật lần cuối: **VR-012** (2026-09-19) · module **DLV** · platform **mobile (Appium MCP / UiAutomator2)**
> App: `com.hrisproject.stag` (host FoxPro → FoxEco)
>
> **Lịch sử merge**
> | Run | Ngày | Module | Elements | ✅ | ⚠️ | 🚫 |
> |---|---|---|--:|--:|--:|--:|
> | VR-001 | 2026-09-18 | USR | 77 | 45 | 26 | 6 |
> | VR-002 | 2026-09-18 | ORD | 62 | 47 | 10 | 5 |
> | VR-004 | 2026-09-18 | ORD | 35 | 35 | 0 | 0 |
> | **VR-005** | **2026-09-19** | **HOME** | **51** | **24** | **23** | **4** |
> | `repro/RP-ASN-lo-sdt-sau-ghep-2026-09-19` | **2026-09-19** | **ASN** *(repro)* | **20** | **7** | **12** | **1** |
> | **VR-007** | **2026-09-19** | **ASN** | **34** | **26** | **8** | **0** |
> | **VR-009** | **2026-09-19** | **ASN** | **28** | **22** | **3** | **3** |
> | **VR-010** | **2026-09-19** | **ASN** | **38** | **33** | **3** | **2** |
> | **VR-011** | **2026-09-19** | **GIFT** | **43** | **38** | **1** | **4** |
| **VR-012** | **2026-09-19** | **DLV** | **33** | **33** | **0** | **0** |
>
> 🔴🔴 **VR-010 ĐÍNH CHÍNH HAI ĐIỀU ĐANG SAI TRONG FILE NÀY — đọc trước khi dùng phần VR-008/VR-009 bên dưới:**
> | Điều đang ghi trong file | Sự thật đo được ở VR-010 |
> |---|---|
> | *"Kỹ thuật ĐẾM thông báo bằng `.instance(N)` … ⛔ Không cần dump page source. Đây là chìa khoá cho nhóm trần"* | ❌ **SAI.** `.instance(N)` **chỉ thấy node ĐANG RENDER** (~4 mục) ⇒ `instance(5)` báo NOT FOUND dù danh sách có 6 mục; sau `scroll_to_element` xuống đáy thì `instance(4)` cũng biến mất. ✅ Cách đúng: **dump page source ở nhiều vị trí cuộn rồi ghép theo nhãn tuổi** *(bẫy `T-ASN-10`)* |
> | *"màn `Chi tiết tin` **không render** mục GHI CHÚ ⇒ mẹo mã `SEED Sx` KHÔNG dùng được"* | ❌ **SAI.** Mục `Ghi chú` **CÓ**, nằm trong khối `THÔNG TIN HÀNG`, chỉ render khi ô Ghi chú **khác rỗng**. ✅ **Mã seed ở ô Ghi chú = oracle định danh MẠNH NHẤT**, hơn nhãn tuổi tin (bị làm tròn) *(`T-ASN-13`)* |
>
> ⚠️ **VR-001 là run vibe ĐẦU TIÊN của dự án** ⇒ phần dưới = hợp nhất nguyên vẹn `VR-001-USR-2026-09-18/vibe-locators.md`
> (tỷ lệ hấp thụ **77/77 = 100%**, không có run trước để gộp).
>
> 🔴 **VR-002 (module ORD) gộp NGUYÊN VẸN ở phần cuối file** (§"MERGE VR-002") — hấp thụ **62/62 = 100%**.
> Bẫy kỹ thuật **T6–T10** là **mới**, đọc cùng T1–T5. **5 đính chính** với phần VR-001, áp dụng khi implement:
> | # | Mục VR-001 | Đính chính từ VR-002 |
> |---|---|---|
> | 1 | `value-tier-chip-option-*` ghi 🚫 NOT FOUND | **resolve được** qua `-android uiautomator resourceId(...)`; chỉ strategy `id` là fail (**T6**) |
> | 2 | Nút thêm ảnh = `accessibility id "0/5"` | ⛔ desc **đổi theo bộ đếm** (`1/5`, `2/5`…) ⇒ dùng `resourceId("multi-photo-add-button")` (**T7**) |
> | 3 | *(chưa ghi)* nút xoá ảnh | `resourceId("multi-photo-remove-<N>")`; `N=3` **không render** (bug trần ảnh, **T10**) |
> | 4 | Wizard B1 "Tiếp theo" enable khi đủ 4 chip | **đo lại**: cần **giá trị + trọng lượng + kích thước + ≥1 ẢNH** (ảnh là bắt buộc từ v1.1) |
> | 5 | *(chưa ghi)* cách rời ô trong wizard | ⛔ **KHÔNG** dùng `appium_mobile_keyboard(hide)` — nó gửi BACK, ở bước 1 = thoát wizard + mất draft (**T9**) |

---


> Captured via **Appium MCP** (UiAutomator2) during this run · app `com.hrisproject.stag` (FoxPro host → FoxEco)
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md` (audit trail) · Platform: **mobile**
> Ưu tiên strategy: `accessibility id` > `id` > `-android uiautomator` > `xpath`

## 🔴 5 BẪY KỸ THUẬT — đọc trước khi implement automation

| # | Bẫy | Bằng chứng trong run này | Cách làm đúng |
|---|---|---|---|
| **T1** | **`selected` KHÔNG BAO GIỜ được expose** trên tab/chip (React Native) | tab `Đang diễn ra` **đang active** nhưng `selected="false"`; cả 4 chip đã chọn (viền cam) vẫn `selected="false"` | ⛔ Không assert trạng thái active/selected bằng attribute. Dùng ảnh, hoặc assert **hệ quả** (nội dung list đổi, nút `Tiếp theo` enable) |
| **T2** | `resource-id` **có trong page source nhưng KHÔNG resolve** qua `id`/`accessibility id` với một số element | `value-tier-chip-option-low` → cả 2 strategy đều NOT FOUND; `activity-order-card-0` cũng có lúc NOT FOUND | Dùng `-android uiautomator` `descriptionStartsWith(...)`. Các id **có** resolve: `profile-menu-*`, `address-suggestion-N`, `track-edit-post`, `post-n3-consent-checkbox` |
| **T3** | `appium_get_element_attribute` **không nhận** `showing-hint` dù bảng attribute hợp lệ có liệt kê | `showing-hint` + `showingHintText` đều báo *"attribute is unknown"* | Kiểm ô rỗng bằng `appium_get_page_source` rồi đọc `showing-hint="true"` |
| **T4** | Nút `Tiếp theo` / `Lưu thay đổi` luôn `clickable="false"` **kể cả khi enable** | `Tiếp theo` `clickable=false` ở cả trạng thái disable **và** enable | ⛔ Không dùng `clickable` để suy enable/disable. `tap` qua element vẫn chạy khi enable |
| **T5** | Ô "Địa chỉ mặc định"/"Địa chỉ lấy hàng" **phải CHỌN từ gợi ý**, gõ xong bấm nút là bị chặn | Bước 2/3 wizard: gõ `FPT Cầu Giấy` rồi bấm `Tiếp theo` → không sang bước; phải `tap address-suggestion-0` trước | Luôn `set_value` → `find(address-suggestion-N)` → `tap` |

## Host app: FoxPro — màn "Chức năng"

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Icon FoxEco (entry point) | tap | -android uiautomator | `new UiSelector().text("FoxEco")` | ✅ | mcp-log TC-USR-001 | TC-USR-001, TC-USR-042 |

## Screen: FoxEco — Trang chủ

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tab "Trang chủ" | tap | accessibility id | `Trang chủ` | ✅ | mcp-log A1 | TC-USR-002/004/007/008/012/013 |
| Tab "Bảng tin" | verify_absent | accessibility id | `Bảng tin` | ✅ | mcp-log TC-USR-014 | TC-USR-014 (chứng cứ ẩn bottom nav) |
| Tab "Đăng tin" | tap | accessibility id | `Đăng tin` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Tab "Hoạt động" | tap | accessibility id | `Hoạt động` | ✅ | mcp-log TC-USR-009 | TC-USR-009, TC-USR-025 |
| Tab "Cá nhân" | tap | accessibility id | `Cá nhân` | ✅ | mcp-log A2 | hầu hết TC USR |
| Nút thoát FoxEco → FoxPro | tap | accessibility id | `Quay lại` | ✅ | mcp-log TC-USR-001 | TC-USR-001, TC-USR-042 |
| Icon thông báo | — | accessibility id | `Thông báo` | ⚠️ Inferred | mcp-log A1 | — *(thấy trong tree, chưa tap)* |
| Số "đơn đã giúp" (hero) | verify | id | `home-helped-count` | ⚠️ Inferred | mcp-log A1 | — *(chưa dùng trong TC nào của lô này)* |
| CTA "Xem bảng tin gửi hàng" | — | accessibility id | `Xem bảng tin gửi hàng` | ⚠️ Inferred | mcp-log A1 | — |
| Link "Xem tất cả" (Đơn của tôi) | — | accessibility id | `Xem tất cả` | ⚠️ Inferred | mcp-log A1 | — |

## Screen: Cá nhân

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Avatar chữ viết tắt | get_text | -android uiautomator | `new UiSelector().text("ĐC")` | ✅ | mcp-log TC-USR-002 | TC-USR-002, TC-USR-003 |
| ↳ ⚠️ **giá trị động theo tên** | — | — | bền hơn: `xpath //android.widget.TextView[string-length(@text)=2]` trong khối header | ⚠️ Inferred | — | — |
| Dòng "phòng ban · MNV" | get_text | -android uiautomator | `new UiSelector().textContains("MNV:")` | ✅ | mcp-log TC-USR-001 | TC-USR-001/002/003/004 |
| Card chỉ số "quà đã nhận" | — | accessibility id | `profile-stat-gifts` | ⚠️ Inferred | mcp-log A4 | TC-USR-012 *(chỉ đọc bounds, chưa tap)* |
| Menu "Đơn của tôi" | tap | accessibility id | `profile-menu-activity` | ✅ | mcp-log TC-USR-009 | TC-USR-009, TC-USR-012 |
| Menu "Quà đã nhận" | tap | accessibility id | `profile-menu-gifts` | ✅ | mcp-log TC-USR-010 | TC-USR-010, TC-USR-012/013 |
| Menu "Cập nhật thông tin cá nhân" | tap | accessibility id | `profile-menu-editProfile` | ✅ | mcp-log TC-USR-014 | TC-USR-011/013/014/024 + toàn bộ lô 2–4 |
| ↳ nhãn của menu đó | get_text | -android uiautomator | `new UiSelector().textStartsWith("Cập nhật thông tin")` → `Cập nhật thông tin cá nhân` | ✅ | mcp-log TC-USR-013 | TC-USR-013 |
| Badge "Hạng Đồng hành" | verify_absent | -android uiautomator | `new UiSelector().textContains("Hạng")` · `...textContains("Đồng hành")` | 🚫 **NOT FOUND** *(đúng kỳ vọng)* | mcp-log TC-USR-008 | TC-USR-008, TC-USR-012 |
| "Điểm ECO"/"Điểm uy tín"/CO₂ | verify_absent | -android uiautomator | `textContains("Điểm")` · `("ECO")` · `("uy tín")` · `("CO")` | 🚫 **NOT FOUND** *(đúng kỳ vọng)* | mcp-log TC-USR-007 | TC-USR-007 |
| Email công ty (trên màn Cá nhân) | verify_absent | -android uiautomator | `new UiSelector().textContains("@fpt.com")` | 🚫 **NOT FOUND** *(đúng kỳ vọng)* | mcp-log TC-USR-002 | TC-USR-002 |

## Screen: Đơn của tôi *(= "màn Hoạt động"; mở từ `profile-menu-activity` HOẶC tab `Hoạt động`)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tab "Đang diễn ra" | verify_visible | accessibility id | `Đang diễn ra` | ✅ | mcp-log TC-USR-009 | TC-USR-009 |
| Tab "Đã hoàn thành" | verify_visible | accessibility id | `Đã hoàn thành` | ✅ | mcp-log TC-USR-009 | TC-USR-009 |
| ↳ ⚠️ **T1**: trạng thái active **không** đọc được qua `selected` | — | — | cả 2 tab đều `selected="false"` | — | — | — |
| Card đơn thứ N | tap | accessibility id | `activity-order-card-<N>` *(N từ 0)* | ✅ | mcp-log TC-USR-009 | TC-USR-025 |
| ↳ fallback khi id không resolve (**T2**) | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Gửi: Tài liệu")` | ✅ | mcp-log TC-USR-025 | TC-USR-025 |

## Screen: Quà đã nhận

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tiêu đề màn | verify_visible | -android uiautomator | `new UiSelector().text("Quà đã nhận")` | ✅ | mcp-log TC-USR-010 | TC-USR-010 |

## Screen: Cập nhật thông tin ★ *(màn trọng tâm của USR v1.1)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Nút "←" (quay lại) | tap | accessibility id | `Quay lại` | ✅ | mcp-log TC-USR-014 | TC-USR-014/019/030/045/046 |
| Tiêu đề màn | verify_visible | -android uiautomator | `new UiSelector().text("Cập nhật thông tin")` | ✅ | mcp-log TC-USR-014 | TC-USR-014 |
| **Field "Số điện thoại mặc định"** | type · get_text | xpath | `//android.widget.EditText[@hint="09xx xxx xxx"]` | ✅ | mcp-log TC-USR-017 | TC-USR-015..023, 027, 043 |
| ↳ ⚠️ `input-type=16387` (phone) **vẫn nhận chữ** · `max-text-length=5000` | — | — | — | — | — | TC-USR-019, TC-USR-023 |
| **Field "Địa chỉ mặc định"** | type · get_text | xpath | `//android.widget.EditText[@hint="Toà nhà, đường, quận"]` | ✅ | mcp-log TC-USR-031 | TC-USR-028..042, 045, 046 |
| ↳ `max-text-length=200` · `input-type=16385` | — | — | — | — | — | — |
| Gợi ý văn phòng thứ N | tap | accessibility id | `address-suggestion-<N>` *(N từ 0)* | ✅ | mcp-log TC-USR-033 | TC-USR-032..039, 045, 046, 025, 026 |
| Email công ty *(chỉ đọc)* | verify_visible | -android uiautomator | `new UiSelector().textContains("@fpt.com")` | ✅ | mcp-log TC-USR-024 | TC-USR-024 |
| ↳ ⚠️ là `TextView`, **không** `EditText` ⇒ đúng "chỉ đọc" | — | — | — | — | — | TC-USR-024 |
| Nút "Lưu thay đổi" | tap | accessibility id | `Lưu thay đổi` | ✅ | mcp-log TC-USR-017 | toàn bộ lô 2–4 |
| Thông báo lỗi dưới field SĐT | get_text | -android uiautomator | `new UiSelector().textContains("Số điện thoại")` | ✅ | mcp-log TC-USR-017 | TC-USR-017/018/020/023 |
| ↳ chuỗi thật: `Số điện thoại không được để trống` · `Số điện thoại không hợp lệ` | — | — | — | — | — | — |
| Banner "Đã lưu thông tin của bạn" | verify_absent | -android uiautomator | `new UiSelector().textContains("Đã lưu")` | 🚫 **NOT FOUND** *(SAI kỳ vọng — bug)* | mcp-log TC-USR-015 | TC-USR-015, 027, 029 |
| Icon khiên bên phải field Email | verify_absent | *(không có node)* | — | 🚫 **NOT FOUND** *(SAI kỳ vọng — bug)* | mcp-log TC-USR-024 | TC-USR-024 |

## Screen: Wizard "Đăng tin" — Bước 1/3 "Thông tin hàng"

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Lựa chọn "Tôi cần gửi hàng" (NEED) | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Tôi cần gửi hàng")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Lựa chọn "Tôi nhận giao hàng" (OFFER) | — | -android uiautomator | `new UiSelector().descriptionStartsWith("Tôi nhận giao hàng")` | ⚠️ Inferred | mcp-log TC-USR-025 | — |
| Chip loại hàng "Tài liệu" | tap | accessibility id | `Tài liệu` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ các chip khác | — | accessibility id | `Đồ điện tử` · `Thực phẩm` · `Hàng nhỏ` · `Đồ dễ vỡ` · `Quần áo` · `Thuốc/Y tế` · `Khác` | ⚠️ Inferred | mcp-log TC-USR-025 | — |
| Field "GHI CHÚ" | type | class name | `android.widget.EditText` *(EditText duy nhất ở bước này)* | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Chip giá trị "Thấp" | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Thấp")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ resource-id *(⚠️ **T2** không resolve)* | — | id | `value-tier-chip-option-low` / `-medium` / `-high` | 🚫 NOT FOUND | mcp-log TC-USR-025 | — |
| Chip trọng lượng "Dưới 5 kg" | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Dưới 5 kg")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ resource-id | — | *(page source only)* | `weight-tier-chip-option-light` / `-medium` / `-heavy` | ⚠️ Inferred | — | — |
| Chip kích thước "Nhỏ" | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Nhỏ, Cầm tay")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ resource-id | — | *(page source only)* | `size-tier-chip-option-small` / `-medium` / `-large` | ⚠️ Inferred | — | — |
| **Nút thêm ảnh hàng (BẮT BUỘC)** | tap | accessibility id | `0/5` *(đổi theo số ảnh: `1/5`…)* | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ resource-id bền hơn | tap | *(page source only)* | `multi-photo-add-button` | ⚠️ Inferred | — | — |
| Bottom sheet "Chụp ảnh" | — | -android uiautomator | `new UiSelector().text("Chụp ảnh")` | ⚠️ Inferred | mcp-log TC-USR-025 | — |
| Bottom sheet "Chọn từ thư viện" | tap | -android uiautomator | `new UiSelector().text("Chọn từ thư viện")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Nút "Add (N)" của photo picker Android | tap | -android uiautomator | `new UiSelector().textStartsWith("Add")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Nút "Tiếp theo" | tap | accessibility id | `Tiếp theo` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Nút "Huỷ chỉnh sửa" *(chỉ có ở mode edit)* | tap | -android uiautomator | `new UiSelector().text("Huỷ chỉnh sửa")` | ✅ | mcp-log TC-USR-025 | TC-USR-025 |

## Screen: Wizard "Đăng tin" — Bước 2/3 "Địa điểm & Thời gian" ★

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tên người gửi *(chỉ đọc)* | verify_visible | xpath | `(//android.widget.EditText)[1]` | ✅ | mcp-log TC-USR-025 | TC-USR-025 |
| **SĐT người gửi** *(prefill từ hồ sơ)* | type · get_text | xpath | `(//android.widget.EditText)[2]` | ✅ | mcp-log TC-USR-026 | TC-USR-025, TC-USR-026 |
| **Địa chỉ lấy hàng** *(prefill từ hồ sơ)* | type · get_text | xpath | `(//android.widget.EditText)[3]` | ✅ | mcp-log TC-USR-026 | TC-USR-025, TC-USR-026 |
| Email công ty người nhận | type | xpath | `//android.widget.EditText[@hint="Email công ty người nhận"]` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Tên người nhận *(autofill từ HRIS)* | verify_visible | accessibility id | `receiver-name-input` | ⚠️ Inferred | mcp-log TC-USR-025 | TC-USR-025 *(đọc qua page source, chưa find trực tiếp)* |
| SĐT người nhận *(autofill từ HRIS)* | verify_visible | accessibility id | `receiver-phone-input` | ⚠️ Inferred | mcp-log TC-USR-025 | TC-USR-025 |
| Địa chỉ giao hàng | type | xpath | `//android.widget.EditText[@hint="Địa chỉ giao hàng"]` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Nút "Thêm người nhận uỷ quyền" | — | accessibility id | `alt-receiver-expand-button` | ⚠️ Inferred | mcp-log TC-USR-025 | — |
| Chọn "Từ ngày" / "Đến ngày" | — | -android uiautomator | `descriptionStartsWith("Từ ngày")` · `("Đến ngày")` | ⚠️ Inferred | mcp-log TC-USR-025 | — *(mặc định "Hôm nay", không cần tap)* |
| **Buổi "Giờ nào cũng được" (BẮT BUỘC ≥1)** | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Giờ nào cũng được")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ resource-id các buổi | — | *(page source only)* | `day-part-morning` · `day-part-afternoon` · `day-part-after_work` · `day-part-anytime` | ⚠️ Inferred | — | — |

## Screen: Wizard "Đăng tin" — Bước 3/3 "Xác nhận & Đăng tin"

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Checkbox đồng ý điều khoản | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Tôi đã đọc và đồng ý")` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| ↳ resource-id | tap | accessibility id | `post-n3-consent-checkbox` | ⚠️ Inferred | mcp-log TC-USR-025 | — |
| Nút "Đăng tin ngay" | tap | accessibility id | `Đăng tin ngay` | ✅ | mcp-log TC-USR-025 | TC-USR-025, TC-USR-026 |
| Popup "Đăng tin thành công!" → "Theo dõi đơn" | tap | -android uiautomator | `new UiSelector().text("Theo dõi đơn")` | ✅ | mcp-log TC-USR-025 | TC-USR-025 |
| Popup → "Về trang chủ" | tap | -android uiautomator | `new UiSelector().text("Về trang chủ")` | ✅ | mcp-log TC-USR-026 | TC-USR-026 |

## Screen: Theo dõi đơn

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tiêu đề màn | verify_visible | -android uiautomator | `new UiSelector().text("Theo dõi đơn")` | ✅ | mcp-log TC-USR-025 | TC-USR-025 |
| Giá trị "Lấy hàng" *(địa chỉ lấy hàng của ĐƠN)* | get_text | *(TextView ngay dưới label `Lấy hàng`)* | `xpath //android.widget.TextView[@text="Lấy hàng"]/following-sibling::*[1]` | ⚠️ Inferred | mcp-log TC-USR-025 | TC-USR-025 *(đọc qua page source)* |
| Nút "Chỉnh sửa" | tap | accessibility id | `Chỉnh sửa` | ✅ | mcp-log TC-USR-025 | TC-USR-025 |
| ↳ resource-id | tap | *(page source only)* | `track-edit-post` | ⚠️ Inferred | — | — |
| Nút "Huỷ đơn" | — | accessibility id | `Huỷ đơn` *(rid `track-cancel-post`)* | ⚠️ Inferred | mcp-log TC-USR-025 | — ⛔ **không tap** (có popup xác nhận, sẽ huỷ đơn thật) |
| Khối ảnh sản phẩm | — | accessibility id | `Xem ảnh 1/1` | ⚠️ Inferred | mcp-log TC-USR-025 | — |

## Navigation Flow (chỉ flow đã đi qua bằng MCP)

| From | Trigger | To | MCP-verified |
|---|---|---|---|
| FoxPro "Chức năng" | tap `text("FoxEco")` | FoxEco Trang chủ | TC-USR-001 step 2 · TC-USR-042 step 8 |
| FoxEco Trang chủ | tap `Quay lại` | FoxPro "Chức năng" | TC-USR-001 · TC-USR-042 step 7 |
| bất kỳ tab | tap `Cá nhân` | Cá nhân | TC-USR-002 step 2 |
| Cá nhân | tap `profile-menu-activity` | Đơn của tôi (tab "Đang diễn ra" active) | TC-USR-009 step 3 |
| Cá nhân | tap `profile-menu-gifts` | Quà đã nhận | TC-USR-010 step 3 |
| Cá nhân | tap `profile-menu-editProfile` | Cập nhật thông tin *(bottom nav ẩn)* | TC-USR-014 step 3 |
| Cập nhật thông tin | tap `Lưu thay đổi` *(hợp lệ)* | **→ Cá nhân** *(⚠️ KHÔNG ở lại — bug TC-USR-015)* | TC-USR-015 step 8 |
| Cập nhật thông tin | tap `Lưu thay đổi` *(SĐT không hợp lệ)* | ở lại + thông báo lỗi dưới field | TC-USR-017/018/020/023 |
| Cập nhật thông tin | tap `Quay lại` *(có thay đổi chưa lưu)* | → Cá nhân **ngay, không hộp thoại** | TC-USR-045 step 8 |
| tab `Đăng tin` | tap `descriptionStartsWith("Tôi cần gửi hàng")` | Wizard Bước 1/3 | TC-USR-025 step 2 |
| Wizard Bước 1/3 | tap `Tiếp theo` *(đủ ảnh + 4 chip)* | Bước 2/3 | TC-USR-025 |
| Wizard Bước 2/3 | tap `Tiếp theo` *(đủ người nhận + ≥1 buổi)* | Bước 3/3 | TC-USR-025 |
| Wizard Bước 3/3 | tick điều khoản → tap `Đăng tin ngay` | Popup "Đăng tin thành công!" | TC-USR-025, TC-USR-026 |
| Popup thành công | tap `Theo dõi đơn` | Theo dõi đơn | TC-USR-025 step 3 |
| Theo dõi đơn | tap `Chỉnh sửa` | Wizard Bước 1/3 *(mode edit, giá trị của ĐƠN)* | TC-USR-025 step 13 |

## Thống kê

| Pages visited | Elements captured | Verified ✅ | Inferred ⚠️ | NOT FOUND 🚫 |
|---|---|---|---|---|
| **9** (FoxPro Chức năng · Trang chủ · Cá nhân · Đơn của tôi · Quà đã nhận · Cập nhật thông tin · Wizard ×3 · Theo dõi đơn) | **77** | **45** | **26** | **6** |

> 🚫 NOT FOUND gồm **4 ca đúng kỳ vọng** (badge hạng · Điểm ECO/uy tín/CO₂ · email trên màn Cá nhân · bottom nav trên màn Cập nhật) và **2 ca SAI kỳ vọng ⇒ bug** (banner "Đã lưu thông tin của bạn" · icon khiên cạnh field Email).

---

# MERGE VR-002 — module ORD (2026-09-18)

> Nguồn: `VR-002-ORD-2026-09-18/vibe-locators.md` — gộp nguyên vẹn, giữ nguyên mark ✅/⚠️/🚫.
> Màn **Wizard Bước 1/3** và **Bước 2/3** ở đây **chi tiết hơn** bản VR-002 phía trên của VR-001 ⇒ khi 2 phần lệch nhau, **lấy bản VR-002 này**.

## 🔴 5 BẪY KỸ THUẬT MỚI phát hiện ở VR-002 (bổ sung T1–T5 của VR-001)

| # | Bẫy | Bằng chứng trong run này | Cách làm đúng |
|---|---|---|---|
| **T6** | `resource-id` của React Native **không resolve** qua strategy `id` nhưng **resolve** qua `-android uiautomator resourceId(...)` | `id "multi-photo-remove-0"` → NOT FOUND · `new UiSelector().resourceId("multi-photo-remove-0")` → OK | Với mọi rid dạng RN (không có prefix package) **luôn** dùng `-android uiautomator` + `resourceId()` |
| **T7** | **Nút thêm ảnh có `content-desc` = CHÍNH BỘ ĐẾM** (`0/5` → `1/5` → …) ⇒ locator theo desc **đổi theo state** | `accessibility id "0/5"` OK khi chưa có ảnh, NOT FOUND sau khi thêm 1 ảnh | Dùng `resourceId("multi-photo-add-button")` (bền), chỉ dùng `"N/5"` khi **cố ý assert bộ đếm** |
| **T8** | Element **ngoài viewport thì KHÔNG resolve** (kể cả accessibility id đúng) | `accessibility id "0/5"` NOT FOUND khi khối ảnh đang cuộn khỏi màn; `scroll_to_element` xong thì OK | Trước khi find element ở cuối form ⇒ `appium_gesture(action=scroll_to_element)` |
| **T9** | `appium_mobile_keyboard(action=hide)` **gửi BACK** ⇒ ở bước 1 wizard = **thoát wizard + mất dữ liệu** | mất draft giữa lô 3 (xem `vibe-log.md §F6`) | ⛔ Không dùng `hide` để "rời ô" trong wizard — tap vùng trống, hoặc get_text trực tiếp |
| **T10** ♻️ **ĐÃ ĐÍNH CHÍNH 2026-09-18 chiều** | Dải ảnh khối `ẢNH HÀNG` là **lazy horizontal list**: phần tử ngoài viewport **không được compose** ⇒ **không tồn tại trong cây**. ⛔ **Bản T10 cũ ghi SAI** (*"dải không cuộn ngang, không render phần tử thứ ≥4"*) và đã làm dựng lên một ứng viên bug ma (**B3 — trần ảnh 4/5**) | Recheck: `adb shell input swipe 950 1836 150 1836 500` **cuộn tới cuối dải ngay lần đầu**; app nhận **đủ 5 ảnh**; `multi-photo-remove-3`/`-4` có thật và xoá được sau khi cuộn. Gesture của lượt 1 không ăn là do **tham số/vùng swipe**, ⛔ không phải dải không cuộn | **Luôn cuộn dải rồi mới assert.** ⛔ Tuyệt đối không suy *"không tìm thấy node" = "chức năng không có"*. Lưu ý kèm **T7**: bộ đếm `n/5` là `content-desc` của **tile thêm ảnh ở CUỐI dải** ⇒ ở mức 5/5 tile bị ẩn đúng `BR18-02` nên **không còn bộ đếm nào** — QC chốt 2026-09-18 đây là **hành vi đúng**, Expected `TC-ORD-070` đã sửa theo, ⛔ không phải bug |

## Screen: Đăng tin mới *(chọn loại tin — bottom nav ẩn)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Subtitle "Bạn muốn làm gì?" | verify_visible | -android uiautomator | `new UiSelector().text("Bạn muốn làm gì?")` | ✅ | mcp-log TC-ORD-001 | TC-ORD-001 |
| Card NEED "Tôi cần gửi hàng" | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Tôi cần gửi hàng")` | ✅ | mcp-log TC-ORD-001 | TC-ORD-001/002 + mọi TC wizard |
| Card OFFER "Tôi nhận giao hàng" | verify_visible | -android uiautomator | `new UiSelector().descriptionStartsWith("Tôi nhận giao hàng")` | ✅ | mcp-log TC-ORD-001 | TC-ORD-001 *(chưa tap — step 5 còn nợ)* |
| Banner cam kết | get_text | -android uiautomator | `new UiSelector().textContains("không thu phí")` | ✅ | mcp-log TC-ORD-001 | TC-ORD-001 |
| ↳ chuỗi thật | — | — | `App không thu phí, không chat, không thanh toán. Sau khi ghép, SĐT hai bên sẽ được lộ để liên hệ ngoài app.` | ✅ | — | — |
| Nút "←" của màn này | — | *(không phải `Quay lại`)* | `accessibility id "Quay lại"` 🚫 NOT FOUND ở màn này ⇒ dùng `appium_gesture(action=back)` | 🚫 | mcp-log TC-ORD-062 | — |

## Screen: Wizard Bước 1/3 "Thông tin hàng" ★

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Step indicator | get_text | -android uiautomator | `new UiSelector().text("Bước 1 / 3")` *(CÓ space quanh `/`)* | ✅ | mcp-log TC-ORD-002 | TC-ORD-002/007/008/014/063 |
| Tiêu đề bước | get_text | -android uiautomator | `new UiSelector().text("Thông tin hàng")` | ✅ | mcp-log TC-ORD-002 | TC-ORD-002 |
| Nút "←" (lùi bước / thoát ở bước 1) | tap | accessibility id | `Quay lại` | ✅ | mcp-log TC-ORD-053 | TC-ORD-053/062/064/066 |
| 8 chip LOẠI HÀNG | tap | accessibility id | `Tài liệu` · `Đồ điện tử` · `Thực phẩm` · `Hàng nhỏ` · `Đồ dễ vỡ` · `Quần áo` · `Thuốc/Y tế` · `Khác` | ✅ *(`Tài liệu` đã tap)* | mcp-log TC-ORD-005/006/007 | TC-ORD-005/006/007/014 |
| Field GHI CHÚ | type · get_text | class name | `android.widget.EditText` *(EditText DUY NHẤT ở bước 1)* | ✅ | mcp-log TC-ORD-011 | TC-ORD-011/054 |
| ↳ thuộc tính | — | — | `max-text-length=300` · `input-type=147457` · rỗng ⇒ `showing-hint="true"` | ✅ | — | TC-ORD-011/062 |
| Chip GIÁ TRỊ HÀNG | tap | -android uiautomator | `descriptionStartsWith("Thấp")` · `("Vừa, 1")` · `("Cao, Trên 5")` | ✅ | mcp-log TC-ORD-008/009/010 | TC-ORD-008/009/010/054/063/064/066 |
| ↳ resource-id *(nay resolve được qua T6)* | tap | -android uiautomator | `resourceId("value-tier-chip-option-low")` / `-medium` / `-high` | ⚠️ Inferred | mcp-log A2 | — *(VR-001 ghi 🚫 với strategy `id`; đổi sang uiautomator thì thấy trong tree)* |
| Banner "hàng giá trị cao" | get_text | -android uiautomator | `new UiSelector().textContains("giá trị cao")` | ✅ | mcp-log TC-ORD-009 | TC-ORD-009/010 |
| ↳ chuỗi thật | — | — | `Hàng giá trị cao: hai bên tự thoả thuận và chịu trách nhiệm với nhau. FoxEco không bảo hiểm, không đứng ra vận chuyển hay bồi thường.` | ✅ | — | — |
| Chip TRỌNG LƯỢNG | tap | -android uiautomator | `descriptionStartsWith("Dưới 5 kg")` · `("5 – 10 kg")` · `("Trên 10 kg")` | ✅ *(`Dưới 5 kg` đã tap)* | mcp-log TC-ORD-064 | TC-ORD-063/064/065 |
| ↳ desc đầy đủ | — | — | `Dưới 5 kg, Nhẹ` · `5 – 10 kg, Trung bình` · `Trên 10 kg, Nặng` | ✅ | — | TC-ORD-064 |
| ↳ resource-id | — | -android uiautomator | `resourceId("weight-tier-chip-option-light")` / `-medium` / `-heavy` | ⚠️ Inferred | mcp-log A2 | — |
| Chip KÍCH THƯỚC | tap | -android uiautomator | `descriptionStartsWith("Nhỏ")` · `("Vừa, ~20")` · `("Lớn")` | ✅ *(`Nhỏ` đã tap)* | mcp-log TC-ORD-066 | TC-ORD-063/066/067 |
| ↳ desc đầy đủ | — | — | `Nhỏ, Cầm tay` · `Vừa, ~20×20 cm` · `Lớn, > 20×20 cm` | ✅ | — | TC-ORD-066 |
| ↳ resource-id | — | -android uiautomator | `resourceId("size-tier-chip-option-small")` / `-medium` / `-large` | ⚠️ Inferred | mcp-log A2 | — |
| Nhãn khối ảnh | get_text | -android uiautomator | `new UiSelector().textStartsWith("ẢNH HÀNG")` → **`ẢNH HÀNG *`** | ✅ | mcp-log TC-ORD-013 | TC-ORD-013 |
| **Nút thêm ảnh** | tap | -android uiautomator | `new UiSelector().resourceId("multi-photo-add-button")` ⭐ **bền** | ✅ | mcp-log TC-ORD-064 | TC-ORD-012/068/069/070/087 |
| ↳ bộ đếm ảnh *(= content-desc của nút, **T7**)* | verify | accessibility id | `0/5` → `1/5` → `2/5` → `3/5` | ✅ | mcp-log TC-ORD-012/087 | TC-ORD-012/013/068/087 |
| Nút xoá ảnh thứ N | tap | -android uiautomator | `new UiSelector().resourceId("multi-photo-remove-<N>")` *(N từ 0)* | ✅ *(N=0)* | mcp-log TC-ORD-087 | TC-ORD-087/071 |
| ↳ `multi-photo-remove-3` | — | -android uiautomator | *(không render — xem **T10**)* | 🚫 NOT FOUND | mcp-log TC-ORD-070 | TC-ORD-070/071 |
| Dòng helper khối ảnh | get_text | -android uiautomator | `new UiSelector().textStartsWith("Bắt buộc ít nhất 1 ảnh")` | ✅ | mcp-log TC-ORD-013 | TC-ORD-013/063 |
| ↳ chuỗi thật | — | — | `Bắt buộc ít nhất 1 ảnh · tối đa 5 ảnh · giúp người vận chuyển nhận diện hàng` | ✅ | — | — |
| Lỗi "ảnh quá 5MB" | get_text | -android uiautomator | `new UiSelector().textContains("5MB")` → `Ảnh vượt quá 5MB, vui lòng chọn ảnh nhỏ hơn.` | ✅ | mcp-log TC-ORD-068 | TC-ORD-068 |
| Nút "Tiếp theo" | tap · get_element_attribute | accessibility id | `Tiếp theo` | ✅ | mcp-log TC-ORD-008 | gần như mọi TC |
| ↳ ⚠️ đọc enable/disable | — | — | **dùng `enabled`** (`false`/`true`); ⛔ `clickable` luôn `false` (bẫy **T4** của VR-001) | ✅ | mcp-log TC-ORD-008/063 | — |
| ↳ điều kiện enable (đo được) | — | — | **cần ĐỦ 4**: giá trị hàng + trọng lượng + kích thước + **≥1 ảnh** | ✅ | mcp-log TC-ORD-027 | F1 |
| Thông báo lỗi ở khối thiếu dữ liệu | verify_absent | -android uiautomator | *(không có node nào)* | 🚫 **NOT FOUND** *(SAI kỳ vọng ⇒ bug F3)* | mcp-log TC-ORD-063/064/066 | TC-ORD-063/064/066 |

## Screen: Bottom sheet chọn nguồn ảnh *(app)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| "Chụp ảnh" | verify_visible | -android uiautomator | `new UiSelector().text("Chụp ảnh")` | ✅ | mcp-log TC-ORD-069 | TC-ORD-069 |
| "Chọn từ thư viện" | tap | -android uiautomator | `new UiSelector().text("Chọn từ thư viện")` | ✅ | mcp-log TC-ORD-012 | mọi TC ảnh |
| ⚠️ **KHÔNG có** lối chọn file khác ảnh | verify_absent | — | *(chỉ 2 mục trên)* | 🚫 NOT FOUND | mcp-log TC-ORD-069 | TC-ORD-069 *(⇒ BLOCKED)* |

## Screen: Android Photo Picker *(OS — `com.google.android.providers.media.module`)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Thumbnail thứ N | tap | -android uiautomator | `new UiSelector().resourceId("com.google.android.providers.media.module:id/icon_thumbnail").instance(<N>)` ⭐ | ✅ | mcp-log A3 | TC-ORD-012/068/070/087 |
| ↳ ⚠️ `content-desc` **không phân biệt được** | — | — | mọi item đều `Photo taken on Sep 18, 2026, 12:29:40 PM` ⇒ **phải dùng `.instance(N)`** | ✅ | mcp-log A3 | — |
| Nút xác nhận "Add (N)" | tap | -android uiautomator | `new UiSelector().textStartsWith("Add")` | ✅ | mcp-log TC-ORD-012 | mọi TC ảnh |
| Tab "Photos" / "Albums" | — | accessibility id | `Photos` · `Albums` | ⚠️ Inferred | mcp-log A3 | — |
| Nút "Cancel" | — | accessibility id | `Cancel` | ⚠️ Inferred | mcp-log A3 | — |

## Screen: Wizard Bước 2/3 "Địa điểm & Thời gian" ★

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Step indicator | get_text | -android uiautomator | `new UiSelector().text("Bước 2 / 3")` | ✅ | mcp-log TC-ORD-083 | TC-ORD-083/084 |
| Tên người gửi *(chỉ đọc)* | tap · get_text | xpath | `(//android.widget.EditText)[1]` → `Đặng Châu Giang` | ✅ | mcp-log TC-ORD-015/016 | TC-ORD-015/016 |
| ↳ ⚠️ chạm **không mở bàn phím** ⇒ đúng "chỉ đọc" | — | — | kiểm bằng `appium_mobile_keyboard(action=is_shown)` → `false` | ✅ | mcp-log TC-ORD-016 | TC-ORD-016 |
| SĐT người gửi *(prefill)* | get_text | xpath | `(//android.widget.EditText)[2]` → `0912345670` | ✅ | mcp-log TC-ORD-015/018 | TC-ORD-015/018 |
| **Địa chỉ lấy hàng** *(prefill = địa chỉ mặc định hồ sơ)* | type · get_text | xpath | `(//android.widget.EditText)[3]` → `363 Nguyễn Hữu Thọ, Cẩm Lệ` | ✅ | mcp-log TC-ORD-027 | TC-ORD-017/027/083/084 |
| Email công ty người nhận | type | xpath | `//android.widget.EditText[@hint="Email công ty người nhận"]` | ✅ | mcp-log TC-ORD-074 | TC-ORD-074..078/083/084/018 |
| Tên người nhận *(autofill)* | type · get_text | -android uiautomator | `new UiSelector().resourceId("receiver-name-input")` | ✅ | mcp-log TC-ORD-074 | TC-ORD-074 |
| SĐT người nhận *(autofill)* | verify | -android uiautomator | `resourceId("receiver-phone-input")` | ⚠️ Inferred | mcp-log TC-ORD-074 | TC-ORD-074 *(đọc qua ảnh, chưa find trực tiếp)* |
| Địa chỉ giao hàng | type · get_text | xpath | `//android.widget.EditText[@hint="Địa chỉ giao hàng"]` | ✅ | mcp-log TC-ORD-028 | TC-ORD-028/055/083/084/053/018 |
| ↳ thuộc tính | — | — | `max-text-length=200` · **không tự trim** giá trị hiển thị | ✅ | mcp-log TC-ORD-055/084 | TC-ORD-055/084 |
| ↳ ⚠️ **KHÔNG có** dropdown gợi ý ở ô này | verify_absent | -android uiautomator | `resourceId("address-suggestion-0")` | 🚫 NOT FOUND *(đúng kỳ vọng — khác màn USR)* | mcp-log TC-ORD-028 | TC-ORD-028 |
| Thông báo tra danh bạ | get_text | -android uiautomator | `textContains("Đã tìm thấy")` / `textContains("Không tìm thấy email")` | ✅ | mcp-log TC-ORD-074/075 | TC-ORD-074..078 |
| ↳ chuỗi thật (tìm thấy) | — | — | `Đã tìm thấy trong hệ thống nội bộ · vui lòng bổ sung SĐT/địa chỉ giao còn thiếu.` | ✅ | — | TC-ORD-074 |
| ↳ chuỗi thật (không thấy) | — | — | `Không tìm thấy email này — vui lòng nhập tay thông tin bên dưới.` *(🚩 câu chữ v1.0, xem F5)* | ✅ | — | TC-ORD-075/076/078 |
| Nút "Thêm người nhận uỷ quyền" | — | accessibility id | `alt-receiver-expand-button` *(nhãn: `+ Thêm người nhận uỷ quyền`)* | ⚠️ Inferred | mcp-log A2 | ⏳ TC-ORD-079..082 |
| Ô "Từ ngày" | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Từ ngày")` | ✅ | mcp-log TC-ORD-030 | TC-ORD-030/031/056/057 |
| Ô "Đến ngày" | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Đến ngày")` | ✅ | mcp-log TC-ORD-031 | TC-ORD-031/056/057 |
| Ngày thứ N trong date picker | tap | -android uiautomator | `new UiSelector().text("<số ngày>")` *(vd `"25"`)* | ✅ | mcp-log TC-ORD-056 | TC-ORD-030/031/056/057 |
| ↳ ⚠️ ngày không hợp lệ **bị làm mờ** và tap **không có tác dụng** | — | — | quá khứ · sớm hơn `Từ ngày` | ✅ | mcp-log TC-ORD-030/031 | TC-ORD-030/031 |
| Nút "Đóng" date picker | tap | -android uiautomator | `new UiSelector().text("Đóng")` | ✅ | mcp-log TC-ORD-031 | TC-ORD-031/056/057 |
| Lỗi khoảng ngày | get_text | -android uiautomator | `textContains("tối đa 7 ngày")` → `Đến ngày tối đa 7 ngày kể từ Từ ngày` | ✅ | mcp-log TC-ORD-057 | TC-ORD-057 |
| 4 chip BUỔI MONG MUỐN | tap | -android uiautomator | `descriptionStartsWith("Sáng")` · `("Chiều")` · `("Sau giờ làm")` · `("Giờ nào cũng được")` | ✅ *(3/4 đã tap)* | mcp-log TC-ORD-059/075/018 | TC-ORD-058/059/075/018 |
| ↳ nhãn thật | — | — | `Sáng (8–12h)` 08:00–12:00 · `Chiều (13–17h)` 13:00–17:00 · `Sau giờ làm (17–19h)` 17:00–19:00 · `Giờ nào cũng được` Linh động cả ngày | ✅ | — | TC-ORD-058 |
| ↳ ⚠️ **không có mặc định** + buổi đã qua **vẫn `enabled=true`** | — | — | ⇒ bug `TC-ORD-058`/`059` | ✅ | mcp-log TC-ORD-058/059 | — |
| Lỗi "chưa chọn buổi" | get_text | -android uiautomator | `new UiSelector().text("Chọn ít nhất 1 buổi")` | ✅ | mcp-log TC-ORD-058 | TC-ORD-058 |
| Nút "Tiếp theo" (bước 2) | tap · get_element_attribute | accessibility id | `Tiếp theo` | ✅ | mcp-log TC-ORD-075 | TC-ORD-075/076/083/084 |
| ↳ điều kiện enable (đo được) | — | — | email **tra thấy trên HRIS** + tên + SĐT + địa chỉ giao (**≠ địa chỉ lấy**) + ≥1 buổi | ✅ | mcp-log TC-ORD-075/083 | F3/F5 |

## Navigation Flow (chỉ flow đã đi qua bằng MCP trong run này)

| From | Trigger | To | MCP-verified |
|---|---|---|---|
| FoxEco Trang chủ | tap `Đăng tin` (bottom nav) | Đăng tin mới *(bottom nav ẩn)* | TC-ORD-001 step 2 |
| Đăng tin mới | tap card `Tôi cần gửi hàng` | Wizard Bước 1/3 | TC-ORD-002 step 3 |
| Wizard Bước 1/3 | tap `Tiếp theo` *(đủ 4 điều kiện)* | Bước 2/3 | TC-ORD-027 step 2 |
| Wizard Bước 1/3 | tap `Tiếp theo` *(thiếu 1 điều kiện)* | **ở lại bước 1, KHÔNG báo lỗi** | TC-ORD-063/064/066 |
| Wizard Bước 2/3 | tap `Quay lại` | **về Bước 1/3** *(⚠️ KHÔNG phải đóng wizard)* | TC-ORD-053 step 3 |
| Wizard Bước 1/3 | tap `Quay lại` *(có dữ liệu chưa lưu)* | **thoát về Đăng tin mới NGAY, xoá dữ liệu, KHÔNG popup** | TC-ORD-053 step 3b |
| Wizard Bước 1/3 | `appium_mobile_keyboard(hide)` | **= BACK ⇒ thoát wizard, mất draft** | lô 3 (F6) |
| Đăng tin mới | `appium_gesture(action=back)` | FoxEco Trang chủ *(bottom nav hiện lại)* | TC-ORD-062 step 4 |
| Trang chủ | tap `Hoạt động` | Đơn của tôi *(2 tab con: `Đang diễn ra` / `Đã hoàn thành`)* | TC-ORD-062 step 4 |
| Khối ảnh | tap `multi-photo-add-button` → `Chọn từ thư viện` | Android Photo Picker | TC-ORD-012 step 2 |
| Photo Picker | tap thumbnail → `Add (N)` | về wizard, bộ đếm +N | TC-ORD-012 step 3 |
| Photo Picker *(ảnh > 5MB)* | tap thumbnail → `Add (1)` | ⚠️ **1 lần** bị đẩy ra tab THÔNG BÁO của FoxPro (F2); state wizard giữ nguyên | TC-ORD-068 step 3 |
| FoxPro THÔNG BÁO | tap menu `Chức năng` | về FoxEco **đúng màn đang dở** | TC-ORD-068 step 3 |

## Thống kê

| Screens visited | Elements captured | Verified ✅ | Inferred ⚠️ | NOT FOUND 🚫 |
|---|---|---|---|---|
| **5** (Đăng tin mới · Wizard B1 · Bottom sheet ảnh · Android Photo Picker · Wizard B2) | **62** | **47** | **10** | **5** |

> 🚫 NOT FOUND gồm **3 ca đúng kỳ vọng** (`address-suggestion-0` ở ô địa chỉ giao · không có lối chọn file ngoài ảnh · `Quay lại` không tồn tại ở màn "Đăng tin mới")
> và **2 ca SAI kỳ vọng ⇒ bug** (thông báo lỗi ở khối thiếu dữ liệu — F3 · `multi-photo-remove-3`/add-button sau ảnh thứ 4 — T10).
>
> ⏳ **Chưa harvest** (thuộc phần còn nợ 46 TC): Wizard **Bước 3/3**, màn **Đăng tin thành công**, **Theo dõi đơn** (VR-001 đã có), form **OFFER**, khối **uỷ quyền**, **lightbox/carousel ảnh** ở chi tiết tin, **icon copy** địa chỉ/SĐT.

---

# MERGE VR-003 — module USR, phần còn nợ (2026-09-18)

> Nguồn: `VR-003-USR-2026-09-18/vibe-locators.md`. Tài khoản `00002352` (tài khoản trắng, chưa từng lưu hồ sơ).
> **Hấp thụ 19/19 = 100%.** Phiên này chạm 5 màn: 2 của FoxEco (đã có ở VR-001, **xác nhận lại locator còn đúng**) + **3 màn HRIS/FoxPro mới**.

## 🔴 4 BẪY KỸ THUẬT MỚI ở VR-003 (bổ sung T1–T5 của VR-001 và T6–T10 của VR-002)

| # | Bẫy | Hệ quả nếu bỏ qua |
|---|---|---|
| **T11** | 🔴 **Field rỗng vẫn trả `text` = chuỗi HINT.** `(//android.widget.EditText)[1]` của màn "Cập nhật thông tin" trả `09xx xxx xxx` khi rỗng; chỉ `showing-hint="true"` trong page source mới phân biệt được. | Assert `text != ""` hoặc `text is not None` sẽ **PASS OAN** trên field rỗng. Đây đúng là chỗ `TC-USR-040/043` dễ bị đọc sai thành PASS. **Luôn assert bằng `showing-hint`, không bằng `text`.** |
| **T12** | 2 field của màn "Cập nhật thông tin" **không có `resource-id`, không có `content-desc`** ⇒ chỉ định vị được bằng **thứ tự EditText** (`[1]` = SĐT, `[2]` = Địa chỉ). | Thêm 1 field ở giữa là gãy toàn bộ. Nên xin dev gắn `testID` trước khi automate màn này. |
| **T13** | Đường quay lại FoxEco sau khi thoát sang FoxPro: **back → back → tap `Chức năng` → tap `FoxEco`**. Không có deeplink. | TC nào cần thoát/mở lại app (vd `TC-USR-042`) phải đi đủ chuỗi này, không rút gọn được. |
| **T14** | Hồ sơ HRIS mobile **không phơi trường "địa chỉ làm việc / văn phòng"** của chính người dùng (đã kiểm cả *Thông tin* lẫn *Quá trình làm việc*). | Không lấy được oracle địa chỉ VP từ app ⇒ phải lấy từ `00_input/v1.1/datatest` hoặc hỏi QC/BA. Đừng phí phiên đi tìm trong app. |

## Screen: FoxPro — Cá nhân (hồ sơ HRIS) · **MỚI**

| Element | Strategy | Value | Action | ✅ |
|---|---|---|---|:--:|
| Tab "Cá nhân" (bottom nav FoxPro) | -android uiautomator | `new UiSelector().text("Cá nhân")` | tap | ✅ |
| Mục "Thông tin cá nhân" | -android uiautomator | `new UiSelector().text("Thông tin cá nhân")` | tap | ✅ |
| Thẻ "Thông tin" | -android uiautomator | `new UiSelector().text("Thông tin")` | tap | ✅ |
| Thẻ "Quá trình làm việc" | -android uiautomator | `new UiSelector().text("Quá trình làm việc")` | tap | ✅ |
| Thẻ "Người thân" / "Trình độ" / "Hồ sơ" | -android uiautomator | `new UiSelector().text("<nhãn>")` | — | ⚠️ Inferred |

## Screen: FoxPro — Thông tin cá nhân → **Thông tin** · **MỚI** *(nguồn oracle HRIS)*

> Bảng label → value, **không có `resource-id`**; đọc bằng `text` của TextView kế bên nhãn.

| Nhãn có trên màn | Ghi chú dùng làm oracle |
|---|---|
| `Mã nhân viên` · `Điện thoại` · `Ngày sinh` · `Giới tính` · `Ngày vào Cty` · `Level cán bộ` · `Địa chỉ` · `Số CMND/CCCD` | ✅ **`Điện thoại` = oracle SĐT HRIS** cho `TC-USR-043`. ⛔ **Không chép giá trị vào repo/evidence** (`Project_rule §Execution Rules`). |
| `IP Phone` · `Nơi sinh` · `Địa chỉ thường trú` · `Nơi ở hiện nay` · `Số định danh` · `Ngày cấp/Nơi cấp số định danh` | Có nhãn nhưng **giá trị rỗng** trên tài khoản `00002352` |
| ⛔ **KHÔNG có** nhãn "địa chỉ làm việc"/"văn phòng" | → T14 |

## Screen: FoxPro — **Quá trình làm việc** · **MỚI**

| Element | Strategy | Value | ✅ |
|---|---|---|:--:|
| Đơn vị công tác | -android uiautomator | `new UiSelector().textContains("Công ty Cổ phần Viễn thông FPT/")` | ✅ |
| Nhãn `Vị trí công việc:` · `Chức danh:` | -android uiautomator | `new UiSelector().text("<nhãn>")` | ✅ |

## ⚠️ Đính chính cho các phiên sau

| Mục | Đính chính |
|---|---|
| Icon "Hồ sơ nhân viên" ở màn **Chức năng** | **KHÔNG phải hồ sơ của mình** — đó là danh sách nhân viên cấp dưới (tài khoản `00002352` thấy *"Bạn không có danh sách nhân viên"*). Hồ sơ cá nhân nằm ở **bottom nav `Cá nhân` → `Thông tin cá nhân`**. |
| `accessibility id "Lưu thay đổi"` · `profile-menu-editProfile` · `profile-stat-gifts` · nav `Trang chủ`/`Cá nhân` | ✅ **Xác nhận lại ở VR-003 — vẫn đúng** trên build 2026-09-18 |

## Thống kê VR-003

| Screens visited | Elements captured | Verified ✅ | Inferred ⚠️ | NOT FOUND 🚫 |
|---|---|---|---|---|
| **5** (2 FoxEco xác nhận lại + 3 HRIS mới) | **19** | **17** | **1** | **1** |

> 🚫 NOT FOUND duy nhất là **đúng kỳ vọng**: `textContains("Đã lưu")` sau khi lưu — app cố ý không còn banner (`TC-USR-027` PASS).


---

# MERGE VR-004 — module ORD (2026-09-18)

> Nguồn: `VR-004-ORD-2026-09-18/vibe-locators.md` — gộp **nguyên vẹn**, giữ nguyên mark ✅/⚠️/🚫.
> 🔴 **Phần này chứa 4 ĐÍNH CHÍNH cho bản VR-002 phía trên.** Khi 2 phần lệch nhau ⇒ **lấy bản VR-004 này**:
> 1. Ô `Địa chỉ giao hàng` **CÓ** dropdown gợi ý (VR-002 ghi không có) — và **cả 2 ô địa chỉ đều BẮT BUỘC chạm gợi ý** (bẫy **T11**)
> 2. Lỗi `Địa chỉ giao phải khác địa chỉ lấy hàng` **CÓ THẬT** (VR-002 kết luận nhánh này chặn im lặng)
> 3. SĐT người gửi prefill nay là `0964633310` (VR-002: `0912345670`) · ô `Địa chỉ lấy hàng` nay **RỖNG** (VR-002: prefill)
> 4. `accessibility id "alt-receiver-expand-button"` **NOT FOUND** — dùng `descriptionStartsWith("Thêm người nhận uỷ quyền")`


| # | Bẫy | Bằng chứng trong run này | Cách làm đúng |
|---|---|---|---|
| **T11** ⭐ **quan trọng nhất** | **CẢ HAI ô địa chỉ ở Bước 2/3 là autocomplete BẮT BUỘC chạm gợi ý.** Gõ tay đủ chữ, text hiển thị đúng, nhưng không tap `address-suggestion-N` ⇒ `Tiếp theo` **giữ `enabled=false` vĩnh viễn và app KHÔNG báo gì** | Mất ~20 MCP call để khoanh vùng ở `TC-ORD-004`. Ghi chú VR-002 *"KHÔNG có dropdown gợi ý ở ô này"* chỉ đúng khi ô **chưa được gõ** | Luôn `set_value` **một phần** tên (vd `"Cẩm Lệ"`) → `find(accessibility id "address-suggestion-0")` → `tap` → `get_text` xác nhận giá trị đã đổi thành chuỗi gợi ý |
| **T12** | **`(//android.widget.EditText)[N]` KHÔNG ổn định** ở Bước 2/3 — màn render **lazy**, số EditText trong cây đổi theo vị trí cuộn | Khi đang ở cuối form, `[2]` trả về **`alt-receiver-name-input`** chứ không phải SĐT người gửi (`TC-ORD-018`) | Dùng `xpath` theo **`@hint` + `@enabled`**: `//android.widget.EditText[@hint="Số điện thoại" and @enabled="true"]`, hoặc `resourceId` |
| **T13** | **Thông báo lỗi validate KHÔNG tự xoá khi đã sửa input** (lỗi "dính") | `TC-ORD-083`: lỗi `Địa chỉ giao phải khác địa chỉ lấy hàng` **vẫn hiện** sau khi đổi ô địa chỉ giao sang chuỗi hoàn toàn khác | ⛔ **KHÔNG** đọc thông báo lỗi ngay sau TC trước — phải **thoát wizard, vào lại form sạch**, nếu không sẽ kết luận PASS/FAIL sai |
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


---

# MERGE VR-005 — module HOME — 2026-09-19

> Hợp nhất **NGUYÊN VẸN** `VR-005-HOME-2026-09-19/vibe-locators.md` — hấp thụ **51/51 = 100%**.
> **Màn Trang chủ lần đầu được harvest đầy đủ** (VR-001 mới có 10 element rời của màn này).
> 🔧 **3 bẫy mới T15–T17** + **T2 tái hiện lần 3** — đọc ở đầu phần dưới.
> 📌 **2 đính chính với phần VR-001:**
> | # | Mục VR-001 | Đính chính từ VR-005 |
> |---|---|---|
> | 1 | `Xem bảng tin gửi hàng` và `Xem tất cả` ghi ⚠️ Inferred | **nâng ✅ Verified** — cả 2 đã `find` + `tap` thành công (TC-HOME-022 / TC-HOME-016) |
> | 2 | `home-helped-count` ghi strategy `id` ⚠️ Inferred | **vẫn ⚠️ Inferred** — phiên này đọc được giá trị `13` từ tree nhưng **chưa thử `find_element`**; ⚠️ nghi dính **T2** (cùng dạng `home-news-empty`) ⇒ implement phải thử `-android uiautomator resourceId(...)` trước |


> Captured via **Appium MCP** (UiAutomator2) during this run · app `com.hrisproject.stag` (FoxPro host → FoxEco)
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md` (audit trail) · Platform: **mobile** · Module: **HOME**
> Ưu tiên strategy: `accessibility id` > `id` > `-android uiautomator` > `xpath`

## 🔴 BẪY KỸ THUẬT MỚI CỦA PHIÊN NÀY (T15–T17) — đọc trước khi implement automation

| # | Bẫy | Bằng chứng trong run này | Cách làm đúng |
|---|---|---|---|
| **T15** | **Chấm đỏ chuông = ViewGroup ẩn danh** — không `text`, không `content-desc`, không `resource-id` | node `[666,97][684,115]` chỉ xuất hiện khi có thông báo chưa đọc; ⛔ `find_element` bằng `accessibility id`/`id` **không tới được** | Assert bằng **đo pixel** vùng badge (đỏ `RGB(244,64,74)` ⟷ nền cam `(255,133,0)`), hoặc `xpath` theo vị trí trong khối header. ⛔ Không assert bằng id |
| **T16** | **Thanh progress 5 bước KHÔNG có node nào** trong accessibility tree | card đơn chỉ expose 5 TextView (vai/loại hàng · badge · Từ · Đến · "Chạm để theo dõi"); 5 đoạn progress **vắng mặt hoàn toàn** | Đếm đoạn tô bằng **đo pixel** theo hàng y của thanh. ⛔ Không assert số bước bằng `find_element` |
| **T17** | `content-desc` của **card đơn** là **chuỗi gộp cả 5 dòng** | `Gửi: Tài liệu \| Giá trị thấp, Đã ghép, Từ: …, Đến: …, Chạm để theo dõi đơn của bạn` | Khớp bằng `-android uiautomator` `descriptionStartsWith("<Vai>: <Loại hàng>")`. ⛔ Đừng khớp full string (đổi theo badge + địa chỉ) |

🔁 **T2 tái hiện lần thứ 3** (đã ghi ở VR-002): `resource-id` có trong page source nhưng **không resolve** qua strategy `id`.
Ca mới của phiên này: **`home-news-empty`** → `id` 🚫 NOT FOUND, `-android uiautomator resourceId("home-news-empty")` ✅ OK.

🧾 **Ghi chú công cụ (lặp lại của VR-004, vẫn đúng):** `appium_screenshot` **không có tham số `filename`** và trả ~148k ký tự HTML viewer ⇒ evidence chụp bằng `adb exec-out screencap`. `appium_get_page_source` trả ~220k ký tự ⇒ MCP tự ghi ra file, parse ngoài context. **Locator vẫn 100% qua MCP.**

## Screen: FoxEco — Trang chủ (header + hero)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Nút thoát FoxEco → FoxPro | — | accessibility id | `Quay lại` | ⚠️ Inferred | mcp-log A1 | — *(thấy trong tree, phiên này không tap)* |
| Dòng "Xin chào," | verify | -android uiautomator | `new UiSelector().text("Xin chào,")` | ⚠️ Inferred | mcp-log A1 | TC-HOME-003 *(đọc từ tree, không find riêng)* |
| Tên tài khoản (header) | get_text | -android uiautomator | `new UiSelector().text("Đặng Châu Giang")` | ✅ | mcp-log TC-HOME-003 | TC-HOME-003 |
| ↳ ⚠️ **giá trị động theo tài khoản** | — | — | bền hơn: TextView thứ 2 trong khối header (`[120,124][428,178]`) | ⚠️ Inferred | — | — |
| Icon chuông thông báo | tap | accessibility id | `Thông báo` | ✅ | mcp-log TC-HOME-005 | TC-HOME-005, TC-HOME-006, TC-HOME-002 |
| ↳ **chấm đỏ (badge chưa đọc)** | verify (pixel) | *(không có locator — bẫy **T15**)* | ViewGroup ẩn danh `[666,97][684,115]` | 🚫 NOT FOUND | mcp-log TC-HOME-005 | TC-HOME-005, TC-HOME-006 |
| Tagline banner | get_text + tap | -android uiautomator | `new UiSelector().textContains("Tiện đường")` | ✅ | mcp-log TC-HOME-007 | TC-HOME-007 |
| ↳ giá trị đo được | — | — | `Tiện đường —\nGiúp đồng nghiệp` *(**2 dòng**, có `\n`)* | ✅ | mcp-log TC-HOME-007 | TC-HOME-007 |
| Logo "FOX ECO" | verify | -android uiautomator | `new UiSelector().text("FOX ECO")` | ⚠️ Inferred | mcp-log A1 | TC-HOME-007 *(đọc từ tree)* |
| Dòng phụ banner | verify | -android uiautomator | `new UiSelector().text("Gửi hàng nội bộ · Không phí · Không chat")` | ⚠️ Inferred | mcp-log A1 | — |
| Hero — số đơn đã giúp | verify | id | `home-helped-count` | ⚠️ Inferred | mcp-log A1 | TC-HOME-008 *(đọc từ tree: `13`; ⚠️ chưa thử `find_element` ⇒ giữ Inferred, xem **T2**)* |
| Dòng số liệu cộng đồng | verify | -android uiautomator | `new UiSelector().textStartsWith("Cộng đồng FoxEco:")` | ⚠️ Inferred | mcp-log A1 | TC-HOME-008, TC-HOME-031 |
| ↳ giá trị đo được 05:51 | — | — | `Cộng đồng FoxEco: 317 đơn · 23743 người` | ⚠️ Inferred | mcp-log A1 | — |
| CTA "Xem bảng tin gửi hàng" | tap | accessibility id | `Xem bảng tin gửi hàng` | ✅ | mcp-log TC-HOME-022 | TC-HOME-022 *(nâng từ ⚠️ Inferred của VR-001)* |

## Screen: FoxEco — Trang chủ (section "Đơn của tôi")

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tiêu đề section | verify | -android uiautomator | `new UiSelector().text("Đơn của tôi")` | ⚠️ Inferred | mcp-log A3 | TC-HOME-009 |
| Link "Xem tất cả" | tap | accessibility id | `Xem tất cả` | ✅ | mcp-log TC-HOME-016 | TC-HOME-016 *(nâng từ ⚠️ Inferred của VR-001)* |
| **Card đơn (chung)** | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("<Vai>: <Loại hàng>")` | ✅ | mcp-log TC-HOME-015 | TC-HOME-015 · bẫy **T17** |
| Card — nhãn vai `Gửi:` | verify | -android uiautomator | `new UiSelector().text("Gửi: Tài liệu \| Giá trị thấp")` | ✅ | mcp-log TC-HOME-009 | TC-HOME-009, TC-HOME-011 |
| Card — nhãn vai `Giao:` | verify | -android uiautomator | `new UiSelector().text("Giao: Quần áo \| Giá trị thấp")` | ✅ | mcp-log TC-HOME-012 | TC-HOME-012 |
| Card — nhãn vai `Nhận:` | verify | -android uiautomator | `new UiSelector().text("Nhận: Đồ dễ vỡ \| Giá trị vừa")` | ✅ | mcp-log TC-HOME-013 | TC-HOME-013 |
| ↳ ⚠️ **3 nhãn là giá trị động** | — | — | bền hơn: `textStartsWith("Gửi:")` / `("Giao:")` / `("Nhận:")` | ⚠️ Inferred | — | — |
| Card — dòng "Chạm để theo dõi đơn của bạn" | verify | -android uiautomator | `new UiSelector().text("Chạm để theo dõi đơn của bạn")` | ✅ | mcp-log TC-HOME-009 | TC-HOME-009 |
| Card — badge trạng thái | verify | -android uiautomator | `new UiSelector().text("Đã ghép")` *(cũng thấy `Đã huỷ`, `Đã giao`)* | ⚠️ Inferred | mcp-log A3 | TC-HOME-009, TC-HOME-014 |
| Card — thanh progress 5 bước | verify (pixel) | *(không có locator — bẫy **T16**)* | — | 🚫 NOT FOUND | mcp-log A3 | TC-HOME-009, TC-HOME-014 |
| Card OFFER *(không có nhãn vai)* | verify | -android uiautomator | `new UiSelector().textStartsWith("Nhận giao hàng")` | ⚠️ Inferred | mcp-log A3 | 📨 spec gap — xem `vibe-log` §TC-HOME-013 |

## Screen: FoxEco — Trang chủ (section "Tin mới" — empty state)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tiêu đề section | verify | -android uiautomator | `new UiSelector().text("Tin mới")` | ⚠️ Inferred | mcp-log A5 | TC-HOME-019 |
| **Container empty state** | verify | -android uiautomator | `new UiSelector().resourceId("home-news-empty")` | ✅ | mcp-log TC-HOME-026 | TC-HOME-026 |
| ↳ 🚫 strategy `id` **KHÔNG** resolve | — | id | `home-news-empty` | 🚫 NOT FOUND | mcp-log TC-HOME-026 | bẫy **T2** |
| Dòng tiêu đề empty | verify | -android uiautomator | `new UiSelector().text("Chưa có tin nào trong khu vực của bạn")` | ✅ | mcp-log TC-HOME-026 | TC-HOME-026 |
| Dòng giải thích empty | verify | -android uiautomator | `new UiSelector().text("Đăng tin để đồng nghiệp nhìn thấy nhu cầu của bạn")` | ✅ | mcp-log TC-HOME-026 | TC-HOME-026 |
| CTA "Đăng tin ngay" | verify | accessibility id | `Đăng tin ngay` | ✅ | mcp-log TC-HOME-026 | TC-HOME-026 |
| ↳ resource-id tương ứng | — | -android uiautomator | `new UiSelector().resourceId("home-news-empty-cta")` | ⚠️ Inferred | mcp-log A5 | — |

## Screen: Bottom navigation (5 tab)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tab "Trang chủ" | find + tap | accessibility id | `Trang chủ` | ✅ | mcp-log TC-HOME-001 | TC-HOME-001, 002, 016, 026 |
| Tab "Bảng tin" | find + tap | accessibility id | `Bảng tin` | ✅ | mcp-log TC-HOME-001 | TC-HOME-001, TC-HOME-002 |
| Tab "Đăng tin" (FAB giữa) | find + tap | accessibility id | `Đăng tin` | ✅ | mcp-log TC-HOME-001 | TC-HOME-001, TC-HOME-002 |
| Tab "Hoạt động" | find | accessibility id | `Hoạt động` | ✅ | mcp-log TC-HOME-001 | TC-HOME-001 |
| Tab "Cá nhân" | find | accessibility id | `Cá nhân` | ✅ | mcp-log TC-HOME-001 | TC-HOME-001 |
| **Thứ tự trái→phải** *(đo bằng `bounds`)* | — | — | `Trang chủ`[x=0] · `Bảng tin`[140] · `Đăng tin`[280] · `Hoạt động`[440] · `Cá nhân`[580] | ✅ | mcp-log A1 | TC-HOME-001 |
| **Trạng thái active** | — | *(không có locator — bẫy **T1**)* | `selected` luôn `false` ⇒ đo bằng màu chữ/icon + chấm chỉ báo | 🚫 NOT FOUND | mcp-log A1 | TC-HOME-001, TC-HOME-022 |

## Screen: Thông báo

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Nút "Đánh dấu đã đọc" | find + tap | accessibility id | `Đánh dấu đã đọc` | ✅ | mcp-log TC-HOME-006 | TC-HOME-006 |
| ↳ ℹ️ **nút biến mất khi 0 chưa đọc** | — | — | sau khi đọc hết, nút **không còn** trong tree | ✅ | mcp-log TC-HOME-002 | TC-HOME-006 |
| Item thông báo | — | -android uiautomator | `new UiSelector().resourceIdMatches("notif-item-.*")` | ⚠️ Inferred | mcp-log A6 | — *(id chứa **UUID của bản ghi**, ⛔ không hardcode)* |
| Bottom nav **vắng mặt** | verify_absent | accessibility id | `Trang chủ` → 🚫 NOT FOUND | ✅ | mcp-log TC-HOME-002 | TC-HOME-002 |

## Screen: Bảng tin (empty)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tiêu đề màn | verify | -android uiautomator | `new UiSelector().text("Bảng tin")` | ⚠️ Inferred | mcp-log TC-HOME-022 | TC-HOME-022 |
| Dòng empty state | verify | -android uiautomator | `new UiSelector().text("Chưa có tin nào")` | ⚠️ Inferred | mcp-log TC-HOME-022 | TC-HOME-002, TC-HOME-026 |
| ↳ dòng giải thích | — | — | `Thử mở rộng khu vực tìm kiếm hoặc đăng tin của riêng bạn` | ⚠️ Inferred | mcp-log TC-HOME-022 | — |
| ⚠️ **Chuỗi empty KHÁC Trang chủ** | — | — | Bảng tin: `Chưa có tin nào` ⟷ Trang chủ: `Chưa có tin nào trong khu vực của bạn` | ⚠️ Inferred | — | ⛔ đừng dùng chung assert |

## Screen: Theo dõi đơn

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Địa chỉ lấy hàng | verify | -android uiautomator | `new UiSelector().text("Tòa V-City, Lê Thái Tổ")` | ⚠️ Inferred | mcp-log TC-HOME-015 | TC-HOME-015 *(đọc từ ảnh §LỘ TRÌNH)* |
| Loại hàng | verify | -android uiautomator | `new UiSelector().textContains("Tài liệu")` | ✅ | mcp-log TC-HOME-015 | TC-HOME-015 *(qua `scroll_to_element`)* |
| Bottom nav **vắng mặt** | verify_absent | accessibility id | `Trang chủ` → 🚫 NOT FOUND | ✅ | mcp-log TC-HOME-002 | TC-HOME-002 |

## Screen: Đăng tin mới (wizard — màn chọn loại tin)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Lựa chọn "Tôi cần gửi hàng" | — | -android uiautomator | `new UiSelector().text("Tôi cần gửi hàng")` | ⚠️ Inferred | mcp-log TC-HOME-002 | — |
| Lựa chọn "Tôi nhận giao hàng" | — | -android uiautomator | `new UiSelector().text("Tôi nhận giao hàng")` | ⚠️ Inferred | mcp-log TC-HOME-002 | — |
| Bottom nav **vắng mặt** | verify_absent | *(quan sát ảnh)* | — | ✅ | mcp-log TC-HOME-002 | TC-HOME-002 |

## Screen: Đơn của tôi (màn Hoạt động)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tiêu đề màn | verify | -android uiautomator | `new UiSelector().text("Đơn của tôi")` | ⚠️ Inferred | mcp-log TC-HOME-016 | TC-HOME-016 |
| Tab con "Đang diễn ra" | — | accessibility id | `Đang diễn ra` | ⚠️ Inferred | mcp-log TC-HOME-016 | TC-HOME-016 |
| Tab con "Đã hoàn thành" | — | accessibility id | `Đã hoàn thành` | ⚠️ Inferred | mcp-log TC-HOME-016 | TC-HOME-016 |

## Navigation Flow (chỉ flow đã đi qua bằng MCP trong run này)

| From | Trigger | To | MCP-verified |
|------|---------|-----|--------------|
| Trang chủ | tap `Thông báo` | Thông báo *(bottom nav ẩn)* | TC-HOME-005 · TC-HOME-002 step 5 |
| Thông báo | `gesture(back)` | Trang chủ | TC-HOME-006 step 3 |
| Trang chủ | tap `Xem bảng tin gửi hàng` | **tab Bảng tin** *(bottom nav vẫn hiện)* | TC-HOME-022 |
| Trang chủ | tap card đơn (`descriptionStartsWith`) | Theo dõi đơn *(bottom nav ẩn)* | TC-HOME-015 · TC-HOME-002 step 3 |
| Theo dõi đơn | `gesture(back)` | Trang chủ | TC-HOME-002 |
| Trang chủ | tap `Đăng tin` (FAB) | Đăng tin mới *(bottom nav ẩn)* | TC-HOME-002 step 4 |
| Trang chủ | tap `Xem tất cả` | Đơn của tôi *(= màn Hoạt động, tab `Hoạt động` active)* | TC-HOME-016 |
| Trang chủ | tap tab `Bảng tin` | Bảng tin | TC-HOME-002 |

## Thống kê

| Màn đã harvest | Elements | ✅ Verified | ⚠️ Inferred | 🚫 NOT FOUND |
|---|--:|--:|--:|--:|
| **8** (Trang chủ header/hero · Trang chủ §Đơn của tôi · Trang chủ §Tin mới · Bottom nav · Thông báo · Bảng tin · Theo dõi đơn · Wizard · Đơn của tôi) | **51** | **24** | **23** | **4** |

> 🚫 **4 NOT FOUND đều là "không có locator", KHÔNG phải "locator sai"** — chấm đỏ chuông (**T15**), thanh progress (**T16**), trạng thái tab active (**T1**), `home-news-empty` qua strategy `id` (**T2**, đã có đường thay thế). 3 cái đầu **bắt buộc đo pixel** khi automate.


---

# MERGE `repro/RP-ASN-lo-sdt-sau-ghep-2026-09-19` — module ASN — 2026-09-19

> Hợp nhất **NGUYÊN VẸN** locator thu được ở phiên `repro/RP-ASN-lo-sdt-sau-ghep-2026-09-19/` — hấp thụ **20/20 = 100%**.
> ⚠️ **Phiên này KHÔNG có run folder `VR-`**: nó thu được **0 verdict TC** nên không đủ hợp đồng `VR-*` (`verify_evidence.py` đòi ≥1 TC có evidence). Ledger 26 TC của ASN nằm ở `coverage/coverage-ASN.md`.
> ⚠️ **Phiên recon-only, 0 TC chạy** ⇒ **12/20 element là ⚠️ Inferred** (chỉ đọc từ tree/ảnh, chưa có action xác nhận). `implement-automation` **phải re-verify** trước khi dùng nhóm Inferred.
> 🆕 **Màn "Theo dõi đơn" vai NGƯỜI NHẬN lần đầu được harvest** (VR-005 mới harvest vai người gửi).
> 🔧 **Bẫy mới T18** (rất dễ gây kết luận sai) + **T2 tái hiện lần 4**.
> 🟢 **1 đính chính với kết luận đã ghi của VR-004:**
> | # | Mục VR-004 | Đính chính từ phiên repro ASN |
> |---|---|---|
> | 1 | clarification *"màn đơn **đã ghép** không lộ SĐT, trái banner cam kết"* | **Đo lại: SĐT CÓ lộ.** Cụm `NGƯỜI GIAO HÀNG` hiện tên + **`0947153040`** + nút `Gọi` (MCP verified). Kết luận cũ nhiều khả năng do **T18** — màn không cuộn nên page source thiếu phần dưới nếp gấp. ⚠️ Mới kiểm **vai người nhận** ⇒ **mở lại** clarification để kiểm đúng vai gửi/vận chuyển, ⛔ chưa đóng |


> Captured via **Appium MCP** (UiAutomator2) · app `com.hrisproject.stag` · Module **ASN** (recon-only)
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md` · Platform: **mobile** · Tài khoản: `Đặng Châu Anh`

## 🔴 BẪY MỚI T18 — màn "Theo dõi đơn" chỉ cuộn khi bước cuộn NHỎ

| | |
|---|---|
| **Triệu chứng** | `appium_gesture(action=scroll, direction=down)`, `scroll` toạ độ tuỳ chỉnh và `swipe(speed=slow)` đều trả **"Successfully scrolled"** nhưng màn **không nhúc nhích** (thử 4 lần) |
| **Hệ quả nguy hiểm** | `appium_get_page_source` lúc đó **KHÔNG chứa** nội dung dưới nếp gấp ⇒ kết luận *"app không có thông tin X"* là **SAI**. Đây gần như chắc chắn là gốc của clarification VR-004 *"đơn đã ghép không lộ SĐT"* |
| **Cách làm đúng** | `appium_gesture(action=scroll_to_element, strategy=…, selector=…, scrollDistancePreset="small")` — cuộn thật sau 4 nhịp |
| **⛔ KHÔNG dùng** | `adb shell wm density` để "thu nhỏ cho vừa màn" — **app restart về host FoxPro, mất ngữ cảnh** (đã dính trong phiên này) |

> 🔗 Cùng họ **T14** (VR-004: bottom bar che vùng lỗi ⇒ cuộn 1 nhịp rồi mới assert) nhưng **nặng hơn**: T14 là *che*, T18 là *cuộn không ăn* nên không có cách nào thấy được nếu không đổi preset.

## Screen: Theo dõi đơn — vai **người nhận**, đơn `Đã ghép`

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tiêu đề màn | verify | -android uiautomator | `new UiSelector().text("Theo dõi đơn")` | ⚠️ Inferred | mcp-log A5 | — |
| Nút "Báo cáo sự cố" | — | -android uiautomator | `new UiSelector().text("Báo cáo sự cố")` | ⚠️ Inferred | mcp-log A5 | — |
| Stepper 5 mốc | verify | -android uiautomator | `text("Chờ ghép")` · `("Lấy hàng")` · `("Đang giao")` · `("Đã giao")` · `("Hoàn thành")` | ⚠️ Inferred | mcp-log A5 | TC-ASN-001 *(chưa chạy)* |
| §LỘ TRÌNH — địa chỉ lấy | verify | -android uiautomator | `new UiSelector().text("Tòa V-City, Lê Thái Tổ")` | ⚠️ Inferred | mcp-log A5 | — *(giá trị động)* |
| §LỘ TRÌNH — địa chỉ giao | verify | -android uiautomator | `new UiSelector().text("FPT Cầu Giấy")` | ⚠️ Inferred | mcp-log A5 | — *(giá trị động)* |
| **§NGƯỜI GIAO HÀNG — tiêu đề cụm** | verify | -android uiautomator | `new UiSelector().textContains("NGƯỜI GIAO HÀNG")` | ✅ | mcp-log A8 | TC-ASN-004 · TC-ASN-002 |
| ↳ **Tên người vận chuyển** | verify | *(đọc từ ảnh — chưa find riêng)* | `Phan Thị Mỹ Anh` | ⚠️ Inferred | mcp-log A9 | TC-ASN-004 |
| ↳ **SỐ ĐIỆN THOẠI** ★ | verify | -android uiautomator | `new UiSelector().text("0947153040")` | ✅ | mcp-log A9 | **TC-ASN-004** — chứng cứ SĐT **CÓ** lộ sau ghép |
| ↳ ⚠️ **giá trị động** | — | — | bền hơn: `new UiSelector().textMatches("0[0-9]{9}")` trong khối `NGƯỜI GIAO HÀNG` | ⚠️ Inferred | — | — |
| ↳ Nút "Gọi" | — | -android uiautomator | `new UiSelector().text("Gọi")` | ✅ | mcp-log A9 | TC-ASN-004 |
| ↳ 🚫 `accessibility id "Gọi"` **KHÔNG** resolve | — | accessibility id | `Gọi` | 🚫 NOT FOUND | mcp-log A9 | bẫy **T2** (lần 4) |
| §ẢNH SẢN PHẨM | verify | -android uiautomator | `new UiSelector().textContains("ẢNH SẢN PHẨM")` | ⚠️ Inferred | mcp-log A8 | — |
| §THÔNG TIN HÀNG | verify | -android uiautomator | `new UiSelector().textContains("THÔNG TIN HÀNG")` | ✅ | mcp-log A8 | — *(dùng làm mốc `scroll_to_element`)* |
| Thanh trạng thái dưới | verify | -android uiautomator | `new UiSelector().textContains("Đã có người vận chuyển")` | ⚠️ Inferred | mcp-log A5 | TC-ASN-001 |
| Nút "Huỷ đơn" | — | -android uiautomator | `new UiSelector().text("Huỷ đơn")` | ⚠️ Inferred | mcp-log A5 | *(module `CNL`)* |

## Screen: Trang chủ §Đơn của tôi — tài khoản `Đặng Châu Anh`

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Card đơn `Đã ghép` (vai nhận) | tap | -android uiautomator | `new UiSelector().descriptionStartsWith("Nhận: Tài liệu \| Giá trị thấp, Đã ghép")` | ✅ | mcp-log A3 | — |
| ↳ ℹ️ **nhãn vai bám theo tài khoản đăng nhập** | — | — | cùng 1 đơn: tài khoản gửi thấy `Gửi:`, tài khoản nhận thấy `Nhận:` | ✅ | mcp-log A1 + A2 | **đối chứng dương** cho TC-HOME-011/012/013 |

## Screen: FoxPro host — đường vào lại FoxEco *(dùng khi app bị restart)*

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tab "Chức năng" | tap | -android uiautomator | `new UiSelector().text("Chức năng")` | ✅ | mcp-log A7 | — |
| Icon "FoxEco" | tap (sau `scroll_to_element`) | -android uiautomator | `new UiSelector().text("FoxEco")` | ✅ | mcp-log A7 | — |
| ↳ ℹ️ cần cuộn | — | — | `scroll_to_element` 2 nhịp mới thấy — ⛔ không nằm màn đầu | ✅ | mcp-log A7 | — |

## Navigation Flow (chỉ flow đã đi qua bằng MCP trong run này)

| From | Trigger | To | MCP-verified |
|------|---------|-----|--------------|
| Trang chủ | tap card đơn `Đã ghép` | Theo dõi đơn *(vai người nhận)* | mcp-log A3 |
| FoxPro "Chức năng" | tap `FoxEco` | FoxEco Trang chủ | mcp-log A7 |
| *(bất kỳ)* | `adb shell wm density <khác>` | ⚠️ **app RESTART → FoxPro host** | mcp-log A6 — ⛔ tránh |

## Thống kê

| Màn đã harvest | Elements | ✅ Verified | ⚠️ Inferred | 🚫 NOT FOUND |
|---|--:|--:|--:|--:|
| **3** (Theo dõi đơn vai nhận · Trang chủ §Đơn của tôi · FoxPro host) | **20** | **7** | **12** | **1** |

> ⚠️ Tỷ lệ ⚠️ Inferred cao (12/20) là **đúng với bản chất phiên recon-only**: không chạy TC nên phần lớn element chỉ được **đọc từ tree/ảnh**, chưa có action xác nhận. ⛔ `implement-automation` phải re-verify trước khi dùng.


---

# MERGE VR-007 — module ASN — 2026-09-19

> Hợp nhất **NGUYÊN VẸN** `VR-007-ASN-2026-09-19/vibe-locators.md` — hấp thụ **34/34 = 100%**.
> 🔑 **ĐÓNG GÓP QUAN TRỌNG NHẤT: MÀN ĐĂNG NHẬP FoxPro lần đầu được harvest.** Nó mở khoá nhóm TC **đa tài khoản** của **MỌI module** (ASN · HOME · ORD · USR · DLV · GIFT), ⛔ không riêng ASN. Luồng 5 bước + bẫy: `04_test-data/valid/USR-accounts.md §0b`.
> 🔴 **Đính chính hạ tầng:** mọi ghi chú cũ *"OTP nhập tay, AI không đổi được tài khoản"* **ĐÃ LỖI THỜI** — OTP staging **cố định**, AI tự login (đã đổi 2 lượt trong phiên).
> ⚠️ **2 lệch tài liệu phát hiện qua locator:** chip buổi thật là **`Sáng (8–12h)`** (fragment ghi *6–12h*) · nhãn loại hàng **`Tài liệu`** (`TC-ASN-021` Steps ghi *"Giấy tờ, hồ sơ"* — không tồn tại).
> ℹ️ **OFFER ≠ NEED ở 2 chỗ dễ sập automation:** checkbox điều khoản của OFFER **không có** `resourceId` (NEED có `post-n3-consent-checkbox`) · màn thành công khác chuỗi (`Đã ghi nhận tuyến đường!` ⟷ `Đăng tin thành công!`).


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

---

# MERGE VR-008 — module ASN — 2026-09-19

> Hợp nhất **NGUYÊN VẸN** `VR-008-ASN-2026-09-19/vibe-locators.md` — hấp thụ **34/34 = 100%**.
> 🔑 **Đóng góp lớn nhất: luồng GHÉP ĐƠN đầy đủ** (modal xác nhận · huỷ nhận đơn + lý do bắt buộc · Theo dõi đơn **2 vai** carrier/chủ tin)
> và **wizard NEED chạy trọn 3 bước** (kể cả date picker). Đây là phần `implement-automation` cần cho toàn bộ nhóm TC ghép nối.
> 🪤 **6 bẫy mới `T-ASN-01..06`** — 2 cái trong đó (ảnh quá khổ im lặng · địa chỉ gõ tay không commit) đã **thực sự chặn phiên này**, đọc trước khi code.

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


---

# MERGE VR-009 — module ASN — 2026-09-19

> Hợp nhất **NGUYÊN VẸN** `VR-009-ASN-2026-09-19/vibe-locators.md` — hấp thụ **28/28 = 100%**.
> 🔴 **CHỨA 1 ĐÍNH CHÍNH NGƯỢC với phần MERGE VR-008 ở trên** (oracle `SEED Sx` trong ô GHI CHÚ) — đọc kỹ mục *"ĐÍNH CHÍNH QUAN TRỌNG"* bên dưới **trước khi** dùng lại mẹo đó.
> 🔑 Đóng góp chính: **kỹ thuật đếm thông báo bằng `.instance(N)`** (chìa khoá cho nhóm trần `TC-ASN-014/015/016/017/025` còn nợ) · **3 bẫy mới `T-ASN-07..09`**.

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


---

# MERGE VR-010 — module ASN — 2026-09-19 (hấp thụ 38/38 = 100%)

> Nguồn: `VR-010-ASN-2026-09-19/vibe-locators.md`. Nội dung đầy đủ ở file per-run; phần dưới là **bản hợp nhất nguyên vẹn** các selector + đính chính.

## ★ Đính chính bắt buộc (ghi đè ghi chép VR-008/VR-009)

| # | Chủ đề | Kết luận VR-010 |
|---|---|---|
| `T-ASN-10` | **Đếm phần tử trong list dài** | ⛔ `.instance(N)` **không** là phép đếm tuyệt đối (chỉ thấy node đang render). ✅ `appium_get_page_source` ở nhiều vị trí cuộn → ghép theo nhãn tuổi. *(Ở môi trường này page source **tự tràn ra file**, không vào context ⇒ chi phí thấp.)* |
| `T-ASN-11` | **Thông báo biến mất sau khi MỞ** | `stag_taipm@`: 2 → 1 → 0 sau 2 lần mở. `stag_giangdc2@` thì **không**. ⇒ **đếm TRƯỚC khi mở** |
| `T-ASN-12` | **Phân quyền FoxEco theo tài khoản** | `stag_huyennhk@` **không có icon FoxEco** ⇒ chỉ làm **người nhận**; màn `Cá nhân` của nó cũng không render `Đăng xuất` ⇒ thoát bằng `adb shell pm clear com.hrisproject.stag` |
| `T-ASN-13` | **Mục `Ghi chú` trên Chi tiết tin** | ✅ **CÓ tồn tại** (render khi khác rỗng) ⇒ mã seed = oracle định danh mạnh nhất |
| — | **Gợi ý địa chỉ** | gõ `FTEL SG08` ⇒ gợi ý-0 trả **`FTEL SG08 Gò Vấp`** (⛔ không phải `Quận 12`) ⇒ **gõ đủ chuỗi** khi cần đúng chi nhánh |

## Selector mới / tái xác nhận (38 element, 7 màn)

| Màn | Element | Strategy | Value | ✅/⚠️/🚫 |
|---|---|---|---|---|
| Thông báo | icon chuông | accessibility id | `Thông báo` | ✅ |
| Thông báo | thông báo khớp tuyến | -android uiautomator | `new UiSelector().textContains("Tìm thấy đơn hàng phù hợp tuyến của bạn — xem chi tiết").instance(N)` | ✅ *(tap được; ⛔ không dùng để ĐẾM)* |
| Thông báo | nhóm ngày | -android uiautomator | `text("HÔM NAY")` · `text("HÔM QUA")` · `text("40 NGÀY TRƯỚC")` | ✅ |
| Thông báo | 4 loại thông báo | -android uiautomator | `textContains("Tìm thấy đơn hàng phù hợp tuyến")` · `("Tin của bạn đã quá hạn")` · `("Đã có người nhận mang giúp")` · `("Đơn đã bị huỷ")` | ✅ |
| Chi tiết tin | **mục `Ghi chú`** | -android uiautomator | `new UiSelector().text("<mã seed>")` trong khối `THÔNG TIN HÀNG` | ✅ ★ |
| Chi tiết tin | khối `LỘ TRÌNH` | -android uiautomator | `text("LỘ TRÌNH")` → `Lấy hàng` / `Giao hàng` | ✅ |
| Chi tiết tin | CTA | -android uiautomator | `textContains("Tôi mang giúp được")` | ✅ ★ **còn CTA ⇒ tin CÒN SỐNG** |
| Chi tiết tin | tuổi tin | -android uiautomator | `text("9 giờ trước")` | ✅ *(⚠️ bị làm tròn)* |
| Form OFFER | điểm A / điểm B | -android uiautomator | `text("Bạn đang ở đâu / xuất phát từ đâu")` · `text("Bạn sẽ đến đâu")` | ✅ |
| Form OFFER | gợi ý địa chỉ | -android uiautomator | `resourceId("address-suggestion-0")` | ✅ *(18 lần)* |
| Form OFFER | chip buổi | -android uiautomator | `text("Giờ nào cũng được")` · `textStartsWith("Sáng (8")` · `("Chiều (13")` · `("Sau giờ làm")` | ✅ |
| Form OFFER | checkbox điều khoản | *(toạ độ)* | tap `(52, 1051)` **sau khi cuộn xuống đáy ×2** | ✅ *(4/4)* |
| Form OFFER | submit / toast | -android uiautomator | `text("Đăng tin ngay")` → `textContains("Đã ghi nhận tuyến đường")` | ✅ |
| Wizard NEED B1 | ô `GHI CHÚ` | -android uiautomator | `textContains("Lưu ý khi giao nhận")` | ✅ ★ nơi cắm mã seed |
| Wizard NEED B1 | chip hàng | -android uiautomator | `text("Thấp")` · `text("Dưới 5 kg")` · `text("Nhỏ")` | ✅ |
| Wizard NEED B1 | bộ đếm ảnh | -android uiautomator | `text("0/5")` → `text("1/5")` | ✅ |
| Wizard NEED B1 | sheet ảnh / picker | -android uiautomator / *(toạ độ)* | `text("Chọn từ thư viện")` → tap `(277,715)` → `text("Add (1)")` | ✅ *(9/9)* |
| Wizard NEED B2 | địa chỉ lấy / giao | -android uiautomator | `text("Địa chỉ lấy hàng")` · `text("Địa chỉ giao hàng")` | ✅ |
| Wizard NEED B2 | email người nhận | -android uiautomator | `text("Email công ty người nhận")` | ✅ *(`stag_huyennhk@` autofill ĐÚNG 9/9)* |
| Wizard NEED B3 | checkbox điều khoản | -android uiautomator | `resourceId("post-n3-consent-checkbox")` | ✅ |
| Wizard NEED B3 | submit / toast | -android uiautomator | `text("Đăng tin ngay")` → `textContains("Đăng tin thành công")` | ✅ |
| Sau khi đăng | CTA | -android uiautomator | `text("Về trang chủ")` | ✅ *(13 lần, dùng cho cả OFFER lẫn NEED)* |
| Bảng tin | tab | -android uiautomator | `text("Bảng tin")` | ✅ |
| Bảng tin | **khuôn parse 1 card** | get_page_source | `Tài liệu` → `Giá trị thấp` → `<tuổi>` → `Nhận:` → `<A>` → `Giao:` → `<B>` → `<ngày · buổi>` → `Nhẹ (< 5 kg)` → `Nhỏ, cầm tay` | ✅ ★ |
| Bảng tin | badge tin của mình | -android uiautomator | `text("Tin của bạn")` *(đứng TRƯỚC nhãn tuổi)* | ✅ |
| Đơn của tôi | tab + badge hết hạn | -android uiautomator | `text("Đã hoàn thành")` → `textContains("Hết hạn")` | ✅ ★ **nơi DUY NHẤT thấy tin hết hạn** |
| FoxPro | đăng xuất / login / FoxEco | -android uiautomator | `text("Cá nhân")` → `text("Đăng xuất")` → `text("Đồng ý")` → `text("Nhập email đăng nhập")` → `text("NHẬN MÃ OTP")` → *(adb OTP)* → `text("ĐĂNG NHẬP")` → `text("Chức năng")` → `text("FoxEco")` | ✅ *(7 lượt)* |
| FoxPro | dialog quyền sau `pm clear` | -android uiautomator | `text("Allow")` · `text("While using the app")` | ✅ |

## Giá trị cho implement-automation

- **33 locator ✅ Verified** trên 7 màn — đủ dựng Screen class cho: Thông báo · Chi tiết tin · form OFFER · wizard NEED (3 bước) · Bảng tin · Đơn của tôi · luồng đổi tài khoản FoxPro.
- 🔑 **Hàm tiện ích nên viết trước:** `dumpAndStitch(screen)` — dump page source ở N vị trí cuộn rồi ghép theo nhãn tuổi. Mọi TC nhóm trần/thứ tự/đếm đều phụ thuộc nó (`T-ASN-10`).
- 🔑 **Oracle định danh tin:** ưu tiên **mã seed ở ô Ghi chú** > tuổi tin > chữ ký tuyến+buổi.

---

# MERGE VR-011 — module **GIFT** — 2026-09-19 — hấp thụ **43/43 = 100%**

> Nguồn: `08_test-runs/vibe/VR-011-GIFT-2026-09-19/vibe-locators.md` — gộp **nguyên vẹn**, không lược.
> **43 element · ✅ 38 · ⚠️ 1 · 🚫 4** (3/4 mã 🚫 là **thử có chủ ý để chứng minh vắng mặt**, không phải miss).
> Module GIFT **lần đầu** được vibe-test ⇒ toàn bộ màn dưới đây là **MÀN MỚI** so với VR-001…VR-010,
> trừ `Cá nhân` / `Quà đã nhận` / `Theo dõi đơn` / `Đơn của tôi` (bổ sung cho phần VR-001/VR-004).

## 🔴 4 BẪY KỸ THUẬT MỚI Ở VR-011 (T18–T21) — đọc trước khi implement automation

| # | Bẫy | Cách xử lý |
|---|---|---|
| **T18** | `resource-id` của màn "Tặng quà" (`gift-cell-*`, `gift-confirm-btn`) **không kèm package** ⇒ strategy `id` **luôn NOT FOUND** | Dùng `accessibility id` (content-desc = tên quà) hoặc `-android uiautomator` + `resourceIdMatches(".*gift-cell-.*")`. ⚠️ Cùng lớp bẫy với **T6** (VR-002) |
| **T19** | Popup "Đã gửi lời cảm ơn!" **không đóng được bằng `back`** — mỗi `back` chỉ pop **màn nền**, popup vẫn nổi trên Trang chủ | ⛔ Không dùng `back` để thoát popup. **Bắt buộc** tap `text("Về trang chủ")`. ⚠️ `accessibility id "Về trang chủ"` **không** khớp — phải dùng `text()` |
| **T20** | Danh sách "Đã hoàn thành" **không cuộn ngược** được bằng `gesture(scroll, up)` hay `swipe(direction=down)` — cả hai **báo success nhưng page source không đổi**; đổi tab rồi quay lại cũng **giữ nguyên** vị trí cuộn | Dùng **swipe toạ độ tường minh**: `x=360,y=400 → endX=360,endY=1050`, `speed=fast` |
| **T21** | Trạng thái **disable** của nút ở màn "Theo dõi đơn" **không đọc được** qua `get_element_attribute(enabled)` — TextView trả `enabled=true` dù nút xám | Kiểm bằng **vắng mặt tổ tiên clickable**: `xpath //android.widget.TextView[@text="…"]/ancestor::*[@clickable="true"][1]` → NOT FOUND ⇒ disable. *(Cùng khuôn với `gift-confirm-btn`: ViewGroup mang `enabled=false`, TextView con vẫn `true`)* |

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

---

# MERGE VR-012 — module **DLV** — 2026-09-19 — hấp thụ **33/33 = 100%**

> Nguồn: `VR-012-DLV-2026-09-19/vibe-locators.md`. Tài khoản `stag_anhdc4@fpt.com`. Phiên **PARTIAL** (13P/2F, 62 TC còn nợ do blocker quyền — xem `vibe-report.md`), nhưng phần locator đã harvest thì **đầy đủ và đã verify**.

## 🔑 PHÁT HIỆN LỚN NHẤT CỦA PHIÊN — oracle "nhãn khoá vs nút thật"

> Cả nhóm `TC-DLV-001..015` (ma trận 3 vai × 5 trạng thái) hỏi đúng một câu: *"cái ở thanh dưới là **nhãn bị khoá** hay **nút bấm được**?"*
> Phiên này đo được **oracle dùng chung, rẻ và chắc**, thay cho việc nhìn ảnh đoán màu:

| | Nhãn **bị khoá** | Nút **thật** |
|---|---|---|
| `clickable` của băng `[32,~1114][688,~1200]` | **`false`** | **`true`** |
| `resource-id` / `content-desc` | **không có** | **có** (`content-desc` = đúng nhãn nút) |
| Node cha | `ViewGroup` trơn bọc `TextView` | `ViewGroup` clickable |

🔴 **⛔ TUYỆT ĐỐI KHÔNG dùng attribute `enabled`** để suy enable/disable: đo được **`enabled="true"` trên CẢ nhãn khoá lẫn nút thật** (bẫy **T4** của VR-001, tái xác nhận lần thứ 5 ở phiên này).

## 🪤 Bẫy kỹ thuật MỚI của phiên này

| # | Bẫy | Bằng chứng | Cách làm đúng |
|---|---|---|---|
| **T-DLV-01** | **Widget Google Map nuốt gesture** — `swipe`/`scroll` rơi vào vùng bản đồ chỉ **pan bản đồ**, màn hình không cuộn | màn *Theo dõi đơn* vai người nhận (`TC-DLV-009`): 4 phép cuộn khác nhau đều "Successfully scrolled" mà màn **không nhúc nhích** | cuộn bằng `scroll_to_element` với **selector nằm ngoài bản đồ**, hoặc scroll toạ độ bắt đầu **trên** khối bản đồ |
| **T-DLV-02** | **`scroll_to_element` dừng ngay khi element *vừa chạm* mép dưới** ⇒ card chỉ cao ~5–17px và **nằm dưới nút FAB `Đăng tin`** ⇒ `tap` **trúng FAB**, nhảy sang màn *Đăng tin mới* | 2 lần dính liên tiếp (`TC-DLV-003`, `TC-DLV-026`); `get_attribute(bounds)` ra `[32,1103][688,1108]` | **Luôn `get_attribute("bounds")` trước khi tap.** `y2 > ~1090` ⇒ chưa an toàn. ✅ Cách chắc: **cuộn quá xuống rồi `scroll_to_element` ngược `direction=up`** — element rơi về **đầu** viewport (đo được `[32,300][688,540]`) |
| **T-DLV-03** | `appium_get_page_source` của app này **~135–252k ký tự** ⇒ MCP **tự ghi ra file** thay vì trả vào context | mọi lần gọi trong phiên | ⇒ dump page source ở app này **gần như miễn phí context**; `grep` bằng script thay vì đọc cả cây. **Đổi hẳn cách tính chi phí so với VR-008/009** |
| **T-DLV-04** | Card ở tab **"Đã hoàn thành"** **KHÔNG mang tiền tố vai** (`Gửi:`/`Giao:`/`Nhận:`) như tab *Đang diễn ra* — chỉ có `Gửi khác` / `Gửi tài liệu`… | `TC-DLV-014`, `TC-DLV-015` | Xác định vai bằng **cụm liên hệ hiển thị** (bảng dưới) hoặc bằng **block `LỊCH SỬ`** |

## 🔑 Oracle phân vai trên màn "Theo dõi đơn" (đo đủ 3 vai trong phiên này)

| Vai | Cụm liên hệ nhìn thấy | Suy ra |
|---|---|---|
| **Người gửi** | chỉ `NGƯỜI GIAO HÀNG` *(sau khi ghép)* · ⛔ không cụm nào khi `Chờ ghép` | `TC-DLV-026` |
| **Người vận chuyển** | **cả `NGƯỜI GỬI` và `NGƯỜI NHẬN`** | `TC-DLV-027` |
| **Người nhận** | chỉ `NGƯỜI GIAO HÀNG` | `TC-DLV-028` |

⚠️ **Người gửi và người nhận thấy cụm giống hệt nhau** ⇒ ⛔ không phân biệt được 2 vai này chỉ bằng cụm liên hệ. Phân biệt bằng **tiền tố card** ở tab *Đang diễn ra* (`Gửi:` vs `Nhận:`) hoặc bằng **block `LỊCH SỬ`** (ai *"Đăng tin lên bảng tin"*, ai *"Hoàn thành đơn"*).

## Screen: Theo dõi đơn — thanh hành động theo (vai × trạng thái)

| Vai · trạng thái | Element | Action | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|---|
| gửi · Chờ ghép | Nhãn khoá | verify | -android uiautomator | `new UiSelector().text("Đang chờ người vận chuyển nhận đơn")` | ✅ | mcp-log TC-DLV-001 | TC-DLV-001 |
| gửi · Chờ ghép | Nút "Chỉnh sửa" | verify | -android uiautomator | `new UiSelector().description("Chỉnh sửa")` — rid **`track-edit-post`**, `clickable=true` | ✅ | mcp-log TC-DLV-001 | TC-DLV-001 |
| gửi · Chờ ghép | Nút "Huỷ đơn" | verify | -android uiautomator | `new UiSelector().description("Huỷ đơn")` — rid **`track-cancel-post`**, `clickable=true` | ✅ | mcp-log TC-DLV-001 | TC-DLV-001 · ⛔ không tap |
| vận chuyển · Đang giao | **CTA "Đã giao cho người nhận"** | verify | -android uiautomator | `new UiSelector().description("Đã giao cho người nhận")` — `clickable=true` | ✅ | mcp-log TC-DLV-008 | TC-DLV-008 · ⛔ tap bị chặn |
| nhận · Đang giao | Nhãn khoá | verify | -android uiautomator | `new UiSelector().text("Đơn đang trên đường đến bạn")` | ✅ | mcp-log TC-DLV-009 | TC-DLV-009 |
| gửi · Đã giao | Nhãn khoá | verify | -android uiautomator | `new UiSelector().text("Đã giao · chờ người nhận xác nhận")` | ✅ | mcp-log TC-DLV-010 | TC-DLV-010 · TC-DLV-011 |
| nhận · Đã giao | **CTA "Xác nhận đã nhận hàng"** | verify | -android uiautomator | `new UiSelector().description("Xác nhận đã nhận hàng")` — `clickable=true` | ✅ | mcp-log TC-DLV-012 | TC-DLV-012 |
| vận chuyển/nhận · Hoàn thành | Nhãn khoá | verify | -android uiautomator | `new UiSelector().text("Đơn đã hoàn thành ✓")` | ✅ | mcp-log TC-DLV-014/015 | TC-DLV-014 · TC-DLV-015 |
| gửi · Hoàn thành, **đã tặng quà** | Nhãn khoá | verify | -android uiautomator | `new UiSelector().text("Bạn đã đánh giá")` | ✅ | mcp-log lô 2 | 🔑 tiền đề **âm** của `TC-DLV-013` |
| nhận · Đã huỷ | Nhãn khoá | verify | -android uiautomator | `new UiSelector().text("Đơn đã huỷ")` | ✅ | mcp-log lô 2 | — |
| mọi màn | Nút "Báo cáo sự cố" | verify | id | **`track-report-incident`** — `clickable=true` | ✅ | mcp-log TC-DLV-008 | ⛔ không tap |

## Screen: Theo dõi đơn — cụm liên hệ + LỘ TRÌNH

| Element | Action | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Nhãn cụm người gửi | verify | -android uiautomator | `new UiSelector().textContains("NGƯỜI GỬI")` | ✅ | mcp-log TC-DLV-027 | TC-DLV-027 |
| Nhãn cụm người nhận | verify | -android uiautomator | `new UiSelector().textContains("NGƯỜI NHẬN")` | ✅ | mcp-log TC-DLV-027 | TC-DLV-027 |
| Nhãn cụm người giao hàng | verify | -android uiautomator | `new UiSelector().textContains("NGƯỜI GIAO HÀNG")` | ✅ | mcp-log TC-DLV-028 | TC-DLV-026 · 028 |
| **Nút Gọi — người gửi** | verify | -android uiautomator | `new UiSelector().description("Gọi người gửi")` | ✅ | mcp-log TC-DLV-027 | 🔑 phân biệt bằng **`content-desc`**, ⛔ không phải `text` (cả 3 nút đều `text="Gọi"`) |
| **Nút Gọi — người nhận** | verify | -android uiautomator | `new UiSelector().description("Gọi người nhận")` | ✅ | mcp-log TC-DLV-027 | TC-DLV-027 |
| **Nút Gọi — người giao hàng** | verify | -android uiautomator | `new UiSelector().description("Gọi người giao hàng")` | ✅ | mcp-log TC-DLV-028 | TC-DLV-026 · 028 |
| **Icon Copy — địa chỉ LẤY hàng** | tap | -android uiautomator | `new UiSelector().description("Copy").instance(0)` | ✅ | mcp-log TC-DLV-081 | — |
| **Icon Copy — địa chỉ GIAO hàng** | tap | -android uiautomator | `new UiSelector().description("Copy").instance(1)` | ✅ | mcp-log TC-DLV-081 | **TC-DLV-081** |
| **Icon Copy — SĐT trong cụm liên hệ** | tap | -android uiautomator | `new UiSelector().description("Copy").instance(2)` | ✅ | mcp-log TC-DLV-080 | **TC-DLV-080** |
| ↳ đọc kết quả copy | — | — | `appium_mobile_clipboard(get)` — **đặt sentinel bằng `set` TRƯỚC khi tap** | ✅ | mcp-log TC-DLV-080/081 | ⛔ không có sentinel ⇒ PASS oan |
| ↳ 🐞 **icon copy KHÔNG đổi màu** | — | — | mẫu pixel `(160,164,175)` xám ở cả t≈0s và t≈2–3s | ✅ | mcp-log TC-DLV-080/081 | **cùng lỗi gốc với `TC-ORD-085` (VR-004)** |
| Stepper 5 mốc | verify | -android uiautomator | `text("Chờ ghép")` · `("Lấy hàng")` · `("Đang giao")` · `("Đã giao")` · `("Hoàn thành")` | ✅ | mcp-log TC-DLV-001 | quan sát đúng ở **4 trạng thái** |

## Screen: Theo dõi đơn — block LỊCH SỬ (mẫu câu nhật ký đo được)

| Mẫu câu (nguyên văn trong `text`) | Kèm theo | Verified | TC refs |
|---|---|---|---|
| `Đăng tin lên bảng tin` | `9/8/2026 · 08:13 · <tên người gửi>` | ✅ | TC-DLV-029 |
| `Ghép thành công (tuyến đường)` · `Ghép thành công` | timestamp + tên | ✅ | TC-DLV-029 |
| `Người mang đã lấy hàng` | timestamp + **địa chỉ lấy hàng** (⛔ không phải tên người) + **ảnh inline** | ✅ | TC-DLV-029 · tiền đề `TC-DLV-041` |
| **`Đã giao tận tay người nhận`** | timestamp + tên + **ảnh bằng chứng inline** | ✅ | **TC-DLV-068** |
| `Hoàn thành đơn` | timestamp + tên **người nhận** | ✅ | TC-DLV-029 |
| `Đã tặng quà cảm ơn` | `Hôm nay · 20:33 · <tên>` | ✅ | mốc thứ 6 ngoài danh sách TC-029 |
| `Đơn hàng đã bị huỷ` + `Huỷ bởi: Người nhận` + block `LÝ DO HUỶ` | lý do render **inline**, ⛔ không phải nút *"Xem lý do"* | ✅ | ⚠️ ngược kỳ vọng `TC-DLV-037/038/039` — xem `vibe-report.md` |

> 🔴 **Thứ tự hiển thị của LỊCH SỬ là MỚI→CŨ** (mốc mới nhất trên cùng) — ngược với thứ tự TC liệt kê. Cần cho `implement-automation` khi assert theo index.

## Screen: Đơn của tôi (tab Hoạt động) — bổ sung VR-012

| Element | Action | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| Tab con "Đang diễn ra" | tap | accessibility id | `Đang diễn ra` | ✅ | mọi TC |
| Tab con "Đã hoàn thành" | tap | accessibility id | `Đã hoàn thành` | ✅ | TC-DLV-014/015/029/068 |
| Card đơn (tab *Đang diễn ra*) | tap | -android uiautomator | `descriptionStartsWith("<Vai>: <Loại hàng> \| <Giá trị>, <Trạng thái>, Từ: <addr>")` | ✅ | mọi TC |
| ↳ **định dạng đầy đủ của `content-desc`** | — | — | `Gửi:/Giao:/Nhận: <loại> \| <giá trị>, <badge trạng thái>, Từ: <A>, Đến: <B>, Chạm để theo dõi đơn của bạn` | ✅ | 🔑 badge **có mặt trong desc** ⇒ lọc theo trạng thái **không cần mở đơn** |
| Card đơn (tab *Đã hoàn thành*) | tap | -android uiautomator | `descriptionStartsWith("Gửi <loại>, <A> → <B> · <ngày>")` | ✅ | **khác hẳn** định dạng tab kia (bẫy `T-DLV-04`) |

## Navigation Flow (chỉ flow đã đi thật qua MCP)

| From | Trigger | To | MCP-verified |
|---|---|---|---|
| Đơn của tôi | tap card `Đang diễn ra` | Theo dõi đơn *(vai theo card)* | TC-DLV-001/008/009/010/011/012 |
| Đơn của tôi | tap `Đã hoàn thành` → tap card | Theo dõi đơn *(đơn Hoàn thành)* | TC-DLV-014/015/029/068 |
| Theo dõi đơn | `gesture back` | Đơn của tôi *(danh sách reset về đầu)* | mọi lô — ⚠️ **mất vị trí cuộn** ⇒ mỗi lần quay lại phải cuộn lại từ đầu |
| bất kỳ tab | tap `Cá nhân` | Cá nhân *(đọc được tên + MNV tài khoản đang đăng nhập)* | Pha A |
| Đơn của tôi | **tap nhầm FAB** | Đăng tin mới | bẫy `T-DLV-02` — ⛔ lỗi điều hướng, không phải chủ ý |
| Theo dõi đơn *(carrier · Đang giao)* | tap `Đã giao cho người nhận` | *(chưa đi được — bị chặn)* | 🚫 **BLOCKER**, xem `vibe-report.md` |

## Thống kê

| Màn đã harvest | Elements | ✅ Verified | ⚠️ Inferred | 🚫 NOT FOUND |
|---|--:|--:|--:|--:|
| 3 (`Đơn của tôi` 2 tab · `Theo dõi đơn` · `Cá nhân`) | **33** | **33** | 0 | 0 |

> Tổng `appium_get_page_source` = **24**, trên **3 màn** — cao hơn số màn vì **12 lần là phép ĐO** (liệt kê tồn kho đơn ở 5 vị trí cuộn; quét chuỗi chứng minh **vế âm** của `TC-DLV-011/026/028`), ⛔ không phải harvest lặp. Nhờ bẫy `T-DLV-03`, mỗi lần dump **không tốn context**.
