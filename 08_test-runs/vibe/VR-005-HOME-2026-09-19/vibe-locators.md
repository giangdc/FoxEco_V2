# Vibe Locators — v1.1 — VR-005 — 2026-09-19

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
