# Vibe Locators — v1.1 — VR-019 — 2026-09-22

> Captured via Appium MCP during this run (2 thiết bị song song).
> Mark legend: ✅ Verified (MCP find+action OK) · ⚠️ Inferred · 🚫 NOT FOUND · ⏳ Pending
> MCP session log: see mcp-session-log.md (audit trail)
> Platform: mobile (Android, UiAutomator2)

> 🔁 **Phần lớn locator của run này TÁI DÙNG nguyên văn từ `locators/vibe-locators-latest.md`**
> (wizard NEED 3 bước, Bảng tin, Chi tiết tin, Theo dõi đơn, FoxPro login/logout) — re-verify bằng
> action thành công trong run này. Bảng dưới chỉ liệt **locator MỚI** hoặc **đính chính** của module TS.

## Screen: Theo dõi đơn — nút Báo cáo sự cố (re-verify mở rộng, cả 3 vai + 4 trạng thái)

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---------|------------|----------|-------|----------|--------------|---------|
| Nút "Báo cáo sự cố" | tap | -android uiautomator | `new UiSelector().resourceId("track-report-incident")` | ✅ | mcp-log TC-TS-022 | TC-TS-008..024 (mọi TC chạm màn này) |
| ↳ hiện ở **cả 5 trạng thái đã thử trong run này** | verify | — | `POSTED` · `MATCHED` · **màn trung gian "Xác nhận đã lấy hàng"** (🆕 chưa từng ghi nhận trước đây) · `IN_TRANSIT` | ✅ | mcp-log TC-TS-022/023 | 🔑 xác nhận `C-TS-02(a)`: hiện ở MỌI trạng thái, không giới hạn |
| ↳ hiện ở **cả 3 vai** (A/B/C) trên cùng 1 đơn | verify | — | A=`stag_giangdc2@` · B=`stag_anhptm17@` · C=`stag_taipm@` | ✅ | mcp-log TC-TS-022/023/024 | TC-TS-022/023/024 |

## Screen: Xác nhận đã lấy hàng (màn trung gian, giữa MATCHED và IN_TRANSIT) 🆕

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Nút "Báo cáo sự cố" (cũng có ở màn NÀY, không chỉ Theo dõi đơn) | verify | -android uiautomator | `resourceId("track-report-incident")` | ✅ | mcp-log setup B | 🆕 màn mới chưa từng harvest ở các run trước |
| Nút "Đã lấy hàng — Bắt đầu giao" | tap | -android uiautomator | `new UiSelector().textContains("Bắt đầu giao")` | ✅ | mcp-log setup B | khớp `vibe-locators-latest.md` (đã có, re-verify) |

## Màn: "Báo sự cố đơn hàng" (WebView) — 🔴 CHỈ TỚI ĐƯỢC MÀN ĐĂNG NHẬP MICROSOFT (run gốc, TÀI KHOẢN TEST STG)

> ⚠️ Vẫn đúng cho tài khoản **test STG** (`stag_*@fpt.com`, không có Microsoft 365). Với tài khoản
> Microsoft **thật** (follow-up 2026-09-22), màn login được bypass — xem section
> "🆕 Màn: 'Báo sự cố đơn hàng' (WebView) — sau khi bypass được màn login Microsoft" bên dưới.

| Element | Action Used | Strategy | Value | Verified | MCP call ref | TC refs |
|---|---|---|---|---|---|---|
| Nút đóng WebView "←" | tap | accessibility id | `Quay lại` | ✅ | mcp-log TC-TS-018 | TC-TS-018 |
| Tiêu đề màn (native header, KHÔNG phải WebView) | verify | -android uiautomator | `new UiSelector().text("Báo sự cố đơn hàng")` | ✅ | mcp-log TC-TS-008 | mọi TC chạm màn |
| ↳ 🔴 Nội dung WebView **luôn là** màn Microsoft "Đăng nhập" | verify | — | logo Microsoft + text "Đăng nhập" + hint "Email hoặc điện thoại" + nút "Tiếp theo" | ✅ *(tái hiện 100%, 2 thiết bị, 3 tài khoản)* | mcp-log TC-TS-008/024 | **`BUG-037`** — form thật (Mã đơn hàng/Loại yêu cầu/Mô tả/SĐT/Ảnh) KHÔNG BAO GIỜ hiện ra |
| Trang lỗi khi mất mạng (WebView tự vẽ, không phải app) | verify | — | text tiếng Anh: `Error loading page` / `Domain: undefined` / `Error Code: -2` / `Description: net::ERR_INTERNET_DISCONNECTED` | ✅ | mcp-log TC-TS-016 | **`BUG-038`** — không phải UI app, là trang lỗi mặc định Chromium |
| ↳ Nút "Thử lại" (kỳ vọng theo spec) | find | -android uiautomator | `textContains("Thử lại")` | 🚫 **NOT FOUND** *(đúng kỳ vọng của phép kiểm — kết quả FAIL của TC, không phải locator sai)* | mcp-log TC-TS-016/017 | TC-TS-016/017 |

## Kỹ thuật ADB dùng trong run (không phải locator — lifecycle/network control)

| Việc | Lệnh | Dùng cho |
|---|---|---|
| Mô phỏng mất mạng | `adb -s <udid> shell svc wifi disable` | TC-TS-016 |
| Khôi phục mạng | `adb -s <udid> shell svc wifi enable` | TC-TS-017 |
| Chụp evidence (thay `appium_screenshot` do MCP trả base64 quá lớn) | `adb -s <udid> exec-out screencap -p > <path>` | mọi ảnh evidence của run |

## 🆕 Màn: "Báo sự cố đơn hàng" (WebView) — sau khi bypass được màn login Microsoft (follow-up 2026-09-22)

> 🚫 **KHÔNG có locator chuẩn cho các ô nhập liệu bên trong** — `appium_context(action=list)` chỉ
> trả `NATIVE_APP` (không có `WEBVIEW_*`); `appium_find_element` query được text node của **nút**
> (`Gửi`, `Hủy bỏ`) nhưng **không** query được input field (Mô tả, SĐT). Nội dung chạy trong Custom
> Tab tách biệt tiến trình. Mọi tương tác với ô nhập liệu dùng **toạ độ (x,y) đọc từ screenshot**,
> không phải strategy chuẩn — đây là ngoại lệ hợp lệ (không có gì để capture), KHÔNG dùng cho
> implement-automation.

| Element | Action Used | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| Ô "Mã đơn hàng" | verify + tap-to-test | — (toạ độ) | prefill GUID nội bộ đơn, VD `01a0c6fd-4730-74d6-8e99-d3e416b5bb56` | ✅ | TC-TS-008/024 |
| ↳ Ô "Mã đơn hàng" **SỬA ĐƯỢC** (🔴 đảo `C-TS-03(b)`) | tap + `input text` | — (toạ độ) | bàn phím bật, ký tự chèn vào được | ✅ | TC-TS-021 (FAIL) |
| 4 radio "Loại yêu cầu" (+ 1 ô "Khác" tự do — 🆕 lựa chọn thứ 4 ngoài dự tính của TC) | tap | — (toạ độ) | Sự cố đơn hàng / Lỗi ứng dụng / Góp ý đề xuất / Khác (free text) | ✅ | TC-TS-009/010/011/012 |
| Ô "Mô tả chi tiết" | tap + `input text` | — (toạ độ) | text field, không giới hạn ký tự quan sát được | ✅ | TC-TS-009/010/011/013 |
| Nút "Tải lên tệp" (Hình ảnh đính kèm) | tap → mở Android file-picker hệ thống | — (toạ độ) | mở picker native, chọn qua long_press + tap | ✅ | TC-TS-009/013/014/015 |
| ↳ Hình ảnh đính kèm **BẮT BUỘC** (🔴 đảo giả định gốc) | verify | — | có dấu `*`, chặn submit khi 0 ảnh | ✅ | TC-TS-013 (FAIL) |
| ↳ Trần 5 ảnh: nút "Tải lên tệp" **BIẾN MẤT** khi đủ 5 (không phải disable) | verify | — | — | ✅ | TC-TS-014 (PASS, cơ chế khác Expected) |
| Link "Hủy bỏ" cạnh mỗi ảnh đã đính | tap (accessibility text, query được) | accessibility text `"Hủy bỏ"` + `.instance(N)` | xoá đúng ảnh thứ N, giữ nguyên thứ tự ảnh còn lại | ✅ | TC-TS-015 |
| Ô "Số điện thoại liên hệ lại" | tap + `input text` | — (toạ độ) | 🔴 **KHÔNG có validate định dạng** — chấp nhận `"0912abc"` | ✅ | TC-TS-012 (FAIL) |
| Nút "Gửi" | find (accessibility text `"Gửi"` — query được) + tap | accessibility text `"Gửi"` | 🔴 **KHÔNG BAO GIỜ disable** — luôn bấm được; validate qua inline error sau khi bấm, không qua trạng thái nút | ✅ | TC-TS-010/011/012 (FAIL — Expected sai giả định) |
| ↳ Cảnh báo tổng hợp dưới nút Gửi khi thiếu ≥1 câu | verify | — | `"Cần hoàn thành N câu hỏi trước khi gửi: Câu hỏi X, Y."` | ✅ | TC-TS-010/011/012/013 |
| ↳ Lỗi inline dưới từng câu hỏi thiếu | verify | — | `"Câu hỏi này là bắt buộc."` | ✅ | TC-TS-010/011 |
| Màn xác nhận sau khi Gửi thành công (🔴 đảo `C-TS-03(d)`) | verify | — | Màn **mặc định Microsoft Forms** ("Đã gửi phản hồi của bạn." + nút "Lưu câu trả lời của tôi" + link "Gửi phản hồi khác" + thẻ quảng cáo MS Forms) — KHÔNG có cam kết "24 giờ làm việc", KHÔNG có nút "Quay lại đơn hàng" | ✅ | TC-TS-009 (FAIL) |
| Nút "←" (Quay lại) trên màn xác nhận | find (accessibility description `"Quay lại"`) + tap | accessibility description `"Quay lại"` | thoát WebView, về Theo dõi đơn (native header, không phải nút app-branded) | ✅ | TC-TS-009 |
| ⚠️ Hành vi "nhớ câu trả lời" sau khi đã submit 1 lần | verify | — | mở lại form sau khi đã Gửi thành công 1 lần trong phiên ⇒ Loại yêu cầu + SĐT **tự điền lại** giá trị lần trước (khác hẳn hành vi "phiên mới sạch" khi phiên trước CHƯA submit — xem `TC-TS-019`) | ⚠️ quan sát phụ, chưa có TC nào kiểm | ngoài phạm vi 17 TC hiện có |

## Navigation Flow (MCP-traversed, bổ sung run này)

| From | Trigger | To | MCP-verified |
|------|---------|-----|--------------|
| Theo dõi đơn (mọi vai, mọi trạng thái) | tap `Báo cáo sự cố` | Màn "Báo sự cố đơn hàng" → WebView → **Microsoft Đăng nhập** (KHÔNG phải form) | TC-TS-008/009/.../024 |
| Màn "Báo sự cố đơn hàng" | tap nút đóng "←" | Quay về đúng Theo dõi đơn, giữ nguyên trạng thái đơn | TC-TS-018 |
| Đã ghép → "Tôi đã lấy hàng" → Xác nhận | tap | Màn "Xác nhận đã lấy hàng" (🆕, có sẵn nút Báo cáo sự cố) → "Bắt đầu giao" → popup "Đã lấy hàng" → Đồng ý → Theo dõi đơn `Đang giao` | setup B (TC-TS-022/023) |

## Thống kê

| Màn đã harvest/re-verify | Elements mới | ✅ Verified | 🚫 NOT FOUND |
|---|--:|--:|--:|
| Theo dõi đơn (nút Báo cáo sự cố, mở rộng 3 vai × 5 trạng thái) · Xác nhận đã lấy hàng (🆕) · WebView Báo sự cố (Microsoft wall + trang lỗi mạng) | 8 | 6 | 2 *(đúng kỳ vọng — kết quả FAIL/spec-gap, không phải sai locator)* |

> Tổng snapshot trần trong run: **0** — toàn bộ dùng lại locator từ `vibe-locators-latest.md` + `find_element` trực tiếp theo `resourceId`/`text` đã biết trước.
