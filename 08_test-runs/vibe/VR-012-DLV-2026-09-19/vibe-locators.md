# Vibe Locators — v1.0+v1.1 — VR-012 — 2026-09-19 — module **DLV**

> Captured via **Appium MCP** (UiAutomator2) · app `com.hrisproject.stag` (FoxPro host → FoxEco)
> Mark legend: ✅ Verified (MCP find + action OK **trong run này**) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: `mcp-session-log.md` · Platform: **mobile** · Tài khoản: `stag_anhdc4@fpt.com` (Đặng Châu Anh)
> Ưu tiên strategy: `accessibility id` > `id` > `-android uiautomator` > `xpath`

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
