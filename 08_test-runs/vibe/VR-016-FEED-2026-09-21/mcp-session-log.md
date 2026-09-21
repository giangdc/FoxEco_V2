# MCP Session Log — VR-016 — 2026-09-21

## Session info
- Platform: mobile (Appium MCP, UiAutomator2)
- Device: `emulator-5554`, 1080×2400
- Session ID: `abb80234-dae5-435a-9d54-208d0b1b14f8`
- Capabilities: `appium:noReset=true` · `appium:appPackage=com.hrisproject.stag` · `appium:appActivity=com.hrisproject.MainActivity` · `appium:autoLaunch=false`
- Created: 17:34 (giờ máy chủ, xem timestamp header ảnh chụp)
- Pre-flight: ✅ select_device → session create → get_page_source → get_window_size — tất cả OK
- App state khi bắt đầu: app đã mở sẵn, đăng nhập sẵn tài khoản **Đặng Châu Giang** (`stag_giangdc2@fpt.com`, vai A), đứng ở màn Chi tiết tin còn sót từ phiên trước (leftover) → KHÔNG dùng làm evidence TC, chỉ dùng để xác nhận identity rồi back về Bảng tin.

## Pre-flight + Pha A (ghi từng call)

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| 1 | 17:34 | select_device | platform=android | OK — 2 devices (`R58T20PLP8K`, `emulator-5554`) | Pre-flight |
| 2 | 17:34 | select_device | deviceUdid=emulator-5554 | OK | Pre-flight |
| 3 | 17:34 | appium_session_management | action=create, appPackage=com.hrisproject.stag | OK sid=abb80234-… | Pre-flight (lần 1 fail thiếu vendor-prefix `appium:`, lần 2 OK) |
| 4 | 17:34 | appium_get_page_source | — | OK (~106KB XML) | Pre-flight — màn Chi tiết tin leftover |
| 5 | 17:34 | appium_get_window_size | — | 1080×2400 | Pre-flight |
| 6 | 17:35 | appium_screenshot | — | OK → `_setup__preflight-launch.png` | Evidence path pre-flight — verified tồn tại trong `screenshots/` |
| 7 | 17:36 | appium_gesture(back) | — | OK | Rời màn leftover, về Bảng tin |
| A1 | 17:37 | appium_get_page_source | màn Bảng tin | OK — 5 card `feed-post-card-0..4`, resource-id sạch | **Pha A** — harvest màn Bảng tin, 6 locator vào map |
| A2 | 17:37 | appium_screenshot | — | OK → `_recon__bang-tin-list.png` | Pha A recon, không tính verdict |

## Pha B — 1 dòng / TC (gộp)

| TC | Time | Calls | Chi tiết gộp | Snapshot? | Kết quả |
|----|------|------:|--------------|-----------|---------|
| TC-FEED-002 | 17:38 | 1 | screenshot×1 (dùng lại màn Bảng tin đã harvest ở Pha A, không cần find/tap) | 0 | ✅ PASS |
| TC-FEED-007 | 17:39–17:40 | 5 | find(`feed-post-card-0`)×1, tap×1, get_page_source×1 (màn Chi tiết tin mới), scroll×1, screenshot×1 | **1** (L2a: màn mới) | ❌ FAIL |
| TC-FEED-009 | 17:41–17:44 | 6 | back×1, find(`feed-post-card-1`)×2 (mở 2 lần để chụp evidence đúng lúc), tap×2, get_page_source×1, scroll×1, screenshot×1 | **1** (L2b: office pair khác) | 🚫 BLOCKED |
| TC-FEED-015 | 17:43–17:44 | 6 | back×1, find(`feed-post-card-4`)×1, tap×1, get_page_source×1, scroll×1, screenshot×2 | **1** (L2a: office pair khác) | ❌ FAIL |
| TC-FEED-013 | 17:44 | 2 | back×1, screenshot×1 (dùng lại màn Bảng tin, không snapshot mới) | 0 | 🚫 BLOCKED |

## Retest — TC-FEED-009 (session mới, cùng ngày, sau khi QC cấp 2 địa chỉ)

> Session cũ đã `delete` cuối phần trên; tạo session **mới** để retest — session ID khác.

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| R1 | 18:02 | appium_session_management | action=create | OK sid=549c5521-ec0b-4c19-8479-48e25e1153fd | Session mới |
| R2 | 18:02 | appium_get_page_source | — | OK, vẫn ở Bảng tin (noReset) | Xác nhận state |
| R3 | 18:02 | find+tap `text("Đăng tin")` | — | OK | Mở wizard |
| R4–R6 | 18:03 | find+tap `Tôi cần gửi hàng`, `Thấp`, `Dưới 5 kg`, `Nhỏ` | — | OK ×4 | Bước 1/3 |
| R7 | 18:03 | tap ô ảnh (`textContains("0/5")`) → bottom sheet → `Chọn từ thư viện` → chọn ảnh trong picker hệ thống → `Add` | 2 lần thử (ảnh đầu >5MB bị chặn, ảnh 2 OK) | OK 1/5 | Native Android photo picker, không phải MCP app — chỉ dùng tap/find trên UI hệ thống |
| R8 | 18:04 | tap `Tiếp theo` | — | OK → Bước 2/3 | |
| R9 | 18:04 | tap ô địa chỉ Người gửi (`text("363 Nguyễn Hữu Thọ...")`) → `set_value("Trần Hưng Đạo")` → tap gợi ý `FTEL An Giang Trần Hưng Đạo - Long Xuyên` | | OK | Autocomplete field, editable dù nhìn như prefill tĩnh |
| R10 | 18:05 | `set_value` ô Email người nhận = `stag_taipm@fpt.com` | | OK — auto-fill tên "Phan Minh Tài" + SĐT | Hệ thống nhận diện nội bộ |
| R11 | 18:06 | `set_value` ô Địa chỉ giao hàng = `"Phú An"` → tap gợi ý `FTEL An Giang VPGD Bình Hòa` | | OK | |
| R12 | 18:07 | tap `Sáng (8–12h)` (buổi mong muốn — field ẩn dưới scroll, ban đầu bỏ sót gây lỗi "Tiếp theo" không phản hồi) | | OK | Bẫy: nút "Tiếp theo" luôn hiện màu cam dù thiếu field bắt buộc, không có thông báo lỗi rõ — phải cuộn xuống mới thấy "Chọn ít nhất 1 buổi" |
| R13 | 18:08 | tap `Tiếp theo` → Bước 3/3 | | OK | |
| R14 | 18:09 | tap checkbox đồng ý điều khoản → tap `Đăng tin ngay` | | OK — "Đăng tin thành công!" | |
| R15 | 18:10 | tap `Về trang chủ` → tab `Bảng tin` → `get_page_source` | | OK, tin mới ở `feed-post-card-0` | |
| R16 | 18:10 | find+tap `feed-post-card-0` → screenshot ×2 (cuộn giữa 2 lần) | | OK | `TC-FEED-009__verify-real-map-route.png` — bản đồ Google Maps thật + "17.2 km · 15 phút" |

## Statistics
- Total MCP calls: ~50 (phần đầu ~34 + retest ~16)
- Tổng `get_page_source`/snapshot: **6** (5 ở phần đầu + 1 ở retest, sau khi đăng tin) — vẫn ≈ số màn/state đã harvest, không vi phạm B1/B2/B3
- `find_element` calls: ~8 (tất cả `-android uiautomator`, 100% thành công trừ 1 lần element stale do re-render sau tap — retry re-find thành công)
- Action calls (tap/scroll/back/set_value): ~28
- ⚠️ Failures: 1 lần `appium_session_management create` fail do thiếu vendor-prefix `appium:` (đã sửa) · 1 lần `appium_set_value` fail vì element stale (đã re-find và retry thành công) · 1 lần ảnh >5MB bị chặn khi đăng tin (đổi ảnh khác)

## Retest — TC-FEED-007 (session mới, account `stag_anhdc4@fpt.com`, theo yêu cầu QC)

| # | Time | MCP method | Args (summary) | Result | Note |
|--:|------|-----------|----------------|--------|------|
| S1 | 18:35 | appium_session_management | action=create | OK sid=73f68bad-9b76-48d5-8c26-c38b235c906c | Session mới |
| S2 | 18:35 | appium_get_page_source | — | OK, còn ở Chi tiết tin leftover phiên trước | Xác nhận state |
| S3 | 18:36 | gesture(back) | — | OK → Bảng tin (vẫn account Giang) | |
| S4–S9 | 18:36–18:39 | Luồng đăng xuất: tap `Cá nhân` (FoxEco) → back ×2 (thoát ra FoxPro `Chức năng`) → tap `Cá nhân` (FoxPro) → `scroll_to_element` "Đăng xuất" → tap → tap "Đồng ý" | | OK, về màn login | Xác nhận: FoxEco **không có** nút đăng xuất (đúng `CLAUDE.md`); phải thoát ra FoxPro trước |
| S10 | 18:39 | `set_value` ô email = `stag_anhdc4@fpt.com` → tap `NHẬN MÃ OTP` | | OK → màn OTP | |
| S11 | 18:40 | `adb shell input text "$FOXECO_STG_PASS"` (OTP cố định, ô tự focus) → tap `ĐĂNG NHẬP` | | OK — "Chào bạn, Đặng Châu Anh" | Xác nhận đúng danh tính |
| S12 | 18:40 | tap `Chức năng` → `scroll_to_element` "FoxEco" → tap | | OK vào FoxEco | |
| S13 | 18:41 | tap `Bảng tin` | | OK, `get_page_source` xác nhận 5 card | Pha A mini — harvest lại màn Bảng tin cho account mới |
| S14–S15 | 18:41 | find+tap `feed-post-card-0` → screenshot ×2 (trước/sau scroll) | | OK — CTA có | `TC-FEED-007__verify-anhdc4-bottom-with-cta.png` |
| S16 | 18:45 | back → find+tap `feed-post-card-1` → get_page_source → scroll → get_page_source | | OK — CTA KHÔNG có | Tin `FTEL SG09→SG07`, người gửi Nguyễn Thị Thanh Thủy |
| S17 | 18:46 | screenshot | | OK | `TC-FEED-007__verify-anhdc4-sg09sg07-no-cta.png` |
| S18 | 18:47 | back → find+tap `feed-post-card-2` → tap → scroll → get_page_source | | OK — CTA có | Tin `FTEL SG07→SG03`, người gửi Nguyễn Tấn Vũ (chỉ kiểm bằng page source, không chụp — không phải evidence chính) |

## Statistics (cộng dồn cả phiên)
- Total MCP calls: ~68 (phần đầu ~50 + retest TC-007 ~18)
- `get_page_source`/snapshot trong retest: 6 (≈ 3 màn: Bảng tin theo account mới + 3 Chi tiết tin)
- Action calls (tap/scroll/back/set_value) trong retest: ~14
- ⚠️ Failures: không có lần nào trong retest — luồng đăng xuất/đăng nhập theo đúng `USR-accounts.md §0b`
