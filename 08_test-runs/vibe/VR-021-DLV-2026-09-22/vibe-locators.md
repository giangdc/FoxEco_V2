# Vibe Locators — v1.1 — VR-021 — 2026-09-22

> Captured via Appium MCP during this run.
> Mark legend: ✅ Verified (MCP find+action OK) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: see mcp-session-log.md
> Platform: mobile

## Screen: Theo dõi đơn — kiểm "Không thể liên lạc cho người nhận?" (KHÔNG tồn tại)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Link/nút "Không thể liên lạc cho người nhận?" (trên màn Theo dõi đơn chính) | find | -android uiautomator | `new UiSelector().textContains("liên lạc")` | 🚫 NOT FOUND | mcp-log TC-DLV-050 | TC-DLV-050 |
| Cùng link, trong popup xác nhận giao hàng (nút chính "Đã giao cho người nhận") | find | -android uiautomator | `new UiSelector().textContains("liên lạc")` | 🚫 NOT FOUND | mcp-log TC-DLV-050 | TC-DLV-050 |
| Popup xác nhận giao hàng (nút chính) | verify | — | "Xác nhận" / "Bạn xác nhận đã giao hàng tận tay người nhận?" / Huỷ / Xác nhận | ✅ | mcp-log TC-DLV-050 | tái xác nhận, giống hệt VR-020 |

## Screen: Xác nhận đã lấy hàng 🆕 HARVEST ĐẦY ĐỦ (bổ sung so với VR-018/VR-019, trước đây chỉ có 2 element)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tiêu đề màn | verify | -android uiautomator | `new UiSelector().text("Xác nhận đã lấy hàng")` | ✅ | mcp-log TC-DLV-041 | TC-DLV-041/042 |
| Khối "ĐIỂM LẤY HÀNG" | verify | -android uiautomator | `new UiSelector().text("ĐIỂM LẤY HÀNG")` | ✅ | mcp-log TC-DLV-041 | — |
| Khối "ẢNH BẰNG CHỨNG (TÙY CHỌN)" 🆕 | verify | -android uiautomator | `new UiSelector().textContains("ẢNH BẰNG CHỨNG")` | ✅ | mcp-log TC-DLV-041 | 🔑 đính chính `RISK-DLV-11` — field CÓ tồn tại |
| Ô thêm ảnh (đếm N/5) | tap | accessibility id | `0/5` → `1/5` sau khi đính | ✅ | mcp-log TC-DLV-041 | TC-DLV-041 |
| ↳ ⚠️ Bẫy: KHÔNG có bottom sheet "Chụp ảnh / Chọn từ thư viện" như Wizard NEED — mở THẲNG camera in-app | — | — | — | ✅ | mcp-log TC-DLV-041 | khác hành vi Wizard Bước 1 |
| Camera in-app — nút chụp | tap (coordinate) | — | `(360, 1405)` — nút tròn trắng viền cam giữa màn | ✅ | mcp-log TC-DLV-041 | ⚠️ không có accessibility id ổn định, dùng toạ độ |
| Camera in-app — nút xác nhận ảnh vừa chụp | tap (coordinate) | — | `(360, 1405)` — nút cam tròn có dấu ✓ (cùng vị trí, khác icon) | ✅ | mcp-log TC-DLV-041 | — |
| Popup quyền camera "Trong khi dùng ứng dụng" | tap | -android uiautomator | `new UiSelector().textContains("Trong khi dùng ứng dụng")` | ✅ | mcp-log TC-DLV-041 | chỉ hiện lần đầu/phiên |
| Nút "Đã lấy hàng — Bắt đầu giao" | tap | -android uiautomator | `new UiSelector().textContains("Bắt đầu giao")` | ✅ | mcp-log TC-DLV-041/042 | TC-DLV-041/042 |
| Popup 2 (sau khi bấm nút trên) — "Xác nhận" | tap | -android uiautomator | `new UiSelector().text("Xác nhận")` | ✅ ⚠️ | mcp-log TC-DLV-041/042 | 🪤 xem bẫy dưới — tap theo `elementUUID` từ `find_element` **không đáng tin** ở popup này, phải tap theo toạ độ nếu lần đầu không ăn |
| Popup kết quả "Đã lấy hàng" → nút "Đồng ý" | tap | -android uiautomator | `new UiSelector().text("Đồng ý")` | ✅ | mcp-log TC-DLV-041/042 | — |

## Screen: Đăng nhập / Đăng xuất FoxPro (re-verify, tái sử dụng đúng luồng USR-accounts.md §0b)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Tab "Cá nhân" (FoxPro, khác Cá nhân của FoxEco) | tap | -android uiautomator | `new UiSelector().text("Cá nhân")` | ✅ | mcp-log setup | ⚠️ **2 màn "Cá nhân" trùng tên** — FoxEco (3 mục, không có Đăng xuất) vs FoxPro (có Đăng xuất) — phải `scroll_to_element("Đăng xuất")` để xác nhận đúng màn trước khi thao tác |
| Nút "Đăng xuất" | tap | -android uiautomator | `new UiSelector().text("Đăng xuất")` | ✅ | mcp-log setup | — |
| Popup xác nhận đăng xuất — "Đồng ý" | tap | -android uiautomator | `new UiSelector().text("Đồng ý")` | ✅ | mcp-log setup | — |
| Field email đăng nhập | set_value | -android uiautomator | `new UiSelector().text("Nhập email đăng nhập")` | ✅ | mcp-log setup | — |
| Nút "NHẬN MÃ OTP" | tap | -android uiautomator | `new UiSelector().text("NHẬN MÃ OTP")` | ✅ | mcp-log setup | — |
| Ô OTP (tự focus) | adb shell input text | ADB (không phải MCP) | `$FOXECO_STG_PASS` | ✅ | mcp-log setup | ⚠️ Biến đúng tên trong `~/.foxeco-v2/credentials.env` là **`FOXECO_STG_PASS`**, không phải `FOXECO_STG_OTP` như CLAUDE.md ghi — nội dung comment file xác nhận đây là OTP dùng chung |
| Nút "ĐĂNG NHẬP" | tap | -android uiautomator | `new UiSelector().text("ĐĂNG NHẬP")` | ✅ | mcp-log setup | — |
| Tab "Chức năng" | tap | -android uiautomator | `new UiSelector().text("Chức năng")` | ✅ | mcp-log setup | — |
| Icon "FoxEco" trong Chức năng | scroll_to_element + tap | -android uiautomator | `new UiSelector().textContains("FoxEco")` | ✅ | mcp-log setup | preset small |

## Navigation Flow (MCP-traversed, bổ sung VR-021)

| From | Trigger | To | MCP-verified |
|------|---------|-----|--------------|
| Theo dõi đơn (B, IN_TRANSIT) | tap CTA chính "Đã giao cho người nhận" | popup xác nhận đơn giản (v1.0-style) | TC-DLV-050 — **KHÔNG** có nhánh "không liên lạc" |
| Theo dõi đơn (B, MATCHED) | tap "Tôi đã lấy hàng" → popup quick-confirm → Xác nhận | màn **"Xác nhận đã lấy hàng"** (khối ảnh optional) | TC-DLV-041/042 |
| Màn "Xác nhận đã lấy hàng" | tap ô ảnh | camera in-app (KHÔNG có lựa chọn thư viện) | TC-DLV-041 |
| Màn "Xác nhận đã lấy hàng" | tap "Đã lấy hàng — Bắt đầu giao" → popup 2 → Đồng ý | Theo dõi đơn (B, IN_TRANSIT) | TC-DLV-041/042 |
| Chi tiết tin (chủ khác) | tap "Tôi mang giúp được" → popup "Xác nhận mang giúp" → Xác nhận | Theo dõi đơn (B, MATCHED) | TC-DLV-041/042 setup |

## 🪤 Bẫy mới (VR-021)

- **`RISK-DLV-11` bị đảo ngược:** ô đính ảnh lúc lấy hàng **CÓ tồn tại**, chỉ là ở LỚP THỨ 2 (màn "Xác nhận đã lấy hàng"), không phải ở popup quick-confirm đầu tiên. Bug trước đó tưởng thiếu field là do dừng lại ở lớp 1.
- **Popup pickup 2 lớp gây nhầm "loop":** popup lớp 1 ("Bạn xác nhận đã lấy hàng...") và popup lớp 2 (cũng tên "Xác nhận") dùng chung 1 component nên nhìn giống hệt nhau — dễ tưởng app đứng yên/loop nếu tap không ăn ở animation timing. **Fix:** sau `find_element` trên popup này, đợi ≥1.5s rồi tap; nếu vẫn không chuyển màn, tap theo toạ độ `(509, 928)` (nút "Xác nhận" bên phải) thay vì retry theo `elementUUID`.
- **elementUUID có thể trùng giữa 2 lần hiển thị cùng 1 loại popup** (không phải luôn luôn là cùng 1 node thật) — đừng dùng việc "ID giống lần trước" làm bằng chứng đứng yên; phải xác nhận bằng nội dung màn (`find_element` một text đặc trưng của màn kế tiếp) hoặc screenshot.
- **Camera in-app không có nút "chọn từ thư viện"** ở màn lấy hàng — khác hẳn Wizard NEED Bước 1 (có bottom sheet 2 lựa chọn). Chụp trực tiếp bằng camera, không dùng `Chọn từ thư viện`.
- **2 màn "Cá nhân" trùng tên** (FoxEco vs FoxPro) — xác nhận bằng cách `scroll_to_element("Đăng xuất")`, không giả định tap 1 phát là tới đúng màn.
- **Biến OTP trong `credentials.env` tên là `FOXECO_STG_PASS`**, không phải `FOXECO_STG_OTP` (khác CLAUDE.md) — dùng đúng tên biến thật khi cần OTP.
