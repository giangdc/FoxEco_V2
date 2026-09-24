# Vibe Log — VR-029 — module TS — RETEST 5 TC v1.1

> Phiên: 2026-09-24 (khởi tạo) · 2026-09-24 (follow-up — QC chốt lại Expected `TC-TS-016`)
> Mode: RETEST (`/vibe-test --module TS --retest TC-TS-009,012,013,016,021`, chỉ v1.1)
> Thiết bị: `emulator-5554` · Appium session `70280ba9-848b-4733-af46-64737dfa2a70` · QC đã đăng nhập sẵn FoxEco + tài khoản Microsoft (form chào "Hi, Giang")
> Build: STG FoxPro_Stag (host app `com.hrisproject.stag`) — không đổi build so với VR-019 theo khai báo, **nhưng hành vi mất mạng đã khác** (xem `TC-TS-016`)
> Đơn dùng: đơn sẵn có trong "Đơn của tôi" — **Giao: Tài liệu | Giá trị thấp**, Tòa V-City → FPT Cầu Giấy, trạng thái **Đã ghép**, mã đơn `01a0b8ce-11a9-7d61-af4d-388ab682f669`
> ⚠️ Lệch setup: script dựng `SEED-TS-01` CP2 `IN_TRANSIT` với vai B; phiên này dùng đơn Đã ghép sẵn có (vai người gửi). Form giống nhau ở mọi trạng thái/vai (`C-TS-02(a)` Resolved), 5 TC chỉ kiểm nội dung form ⇒ không ảnh hưởng kết luận.
> 🔎 Quan sát chung: form Microsoft Forms hiển thị giao diện **tiếng Anh** trên máy này (nút "Submit", màn xác nhận "Your response was submitted.") — theo ngôn ngữ tài khoản Microsoft; ở VR-019 (máy thật) hiện tiếng Việt ("Gửi", "Đã gửi phản hồi của bạn."). Ô "Hình ảnh đính kèm" **không còn dấu `*`** (khớp `FE-325` Fixed). Ô SĐT có placeholder mới "Please enter at most 10 characters".
> 🛠️ Nhập liệu tiếng Việt: `set_value` W3C không gõ được ký tự có dấu (UiAutomator2 `KeyCharacterMap`) ⇒ dùng `appium_mobile_clipboard(set)` + keyevent PASTE.

## TC-TS-021 — Check ô mã đơn hàng là nhãn tĩnh chỉ đọc không sửa được *(Expected sửa 2026-09-24: ô sửa được)*

| Step | Hành động | Cách làm | Kết quả | Evidence | Ghi chú |
|---|---|---|---|---|---|
| 1-3 | (setup) Mở đơn → "Báo cáo sự cố" | tap card · `find resourceId("track-report-incident")` + tap | ✅ | — | Form tải được, ô "Mã đơn hàng" prefill `01a0b8ce-…f669` kèm ghi chú "Tự động điền từ ứng dụng, vui lòng không chỉnh sửa" |
| 4 | Nhấn vào ô "Mã đơn hàng", nhập "X" | tap toạ độ (800,1263) · `adb input text X` | ✅ | — | Bàn phím (thanh công cụ nhập liệu nổi) bật lên |
| 5 | Check kiểu ô, bàn phím, giá trị | quan sát | ✅ | `TC-TS-021__verify-madon-sua-duoc-chen-x.png` | Giá trị thành `…682f6X69` — ký tự "X" chèn vào được |

**Result: ✅ PASS** — khớp Expected mới (ô sửa được, `C-TS-04(d)`). Before: ❌ FAIL ở VR-019 — ảnh cũ xem `VR-019-TS-2026-09-22/vibe-log.md` §TC tương ứng.
**Evidence:** `screenshots/TC-TS-021__verify-madon-sua-duoc-chen-x.png`

## TC-TS-012 — Check nút Gửi vô hiệu hoá khi số điện thoại sai định dạng *(Expected sửa 2026-09-24: không validate định dạng)*

| Step | Hành động | Cách làm | Kết quả | Evidence | Ghi chú |
|---|---|---|---|---|---|
| 1-3 | (setup) Đóng form cũ (`accessibility id "Quay lại"`), mở lại "Báo cáo sự cố" | find + tap | ✅ | — | Phiên form mới |
| 4 | Chọn "Góp ý / đề xuất" | tap toạ độ | ✅ | — | |
| 5 | Nhập "App hay bị chậm ở màn bảng tin" | clipboard + PASTE | ✅ | — | Lần gõ W3C đầu bị cắt "App hay b" → xoá, dán lại |
| 6 | Nhập "0912abc" vào ô SĐT | `set_value` W3C | ✅ | `TC-TS-012__pre-sdt-0912abc-form-filled.png` | Không có lỗi định dạng nào hiện ra |
| 7 | Nhấn "Submit" | tap toạ độ (540,1572) | ✅ | — | Không có ảnh đính kèm |
| 8 | Check phản hồi form + màn sau khi gửi | quan sát | ✅ | `TC-TS-012__verify-sdt-0912abc-gui-thanh-cong.png` | "Your response was submitted." — gửi thành công với SĐT "0912abc" |

**Result: ✅ PASS** — khớp Expected mới (`C-TS-04(c)`, BA chấp nhận rủi ro data). Before: ❌ FAIL ở VR-019 — ảnh cũ xem `VR-019-TS-2026-09-22/vibe-log.md` §TC tương ứng.
**Evidence:** `screenshots/TC-TS-012__pre-sdt-0912abc-form-filled.png` · `screenshots/TC-TS-012__verify-sdt-0912abc-gui-thanh-cong.png`

## TC-TS-013 — Check gửi báo cáo sự cố thành công khi không đính ảnh nào *(retest `FE-325` Fixed)*

| Step | Hành động | Cách làm | Kết quả | Evidence | Ghi chú |
|---|---|---|---|---|---|
| 1-3 | (setup) Đóng màn xác nhận, mở lại form | find + tap | ✅ | — | |
| 4 | Chọn "Sự cố đơn hàng" | tap toạ độ | ✅ | — | |
| 5 | Nhập "Không liên lạc được người nhận" | clipboard + PASTE | ✅ | — | |
| 6 | Nhập "0912345678" | `adb input text` | ✅ | `TC-TS-013__pre-form-filled-0-anh.png` | Ô "Hình ảnh đính kèm" không có `*`, 0 tệp |
| 7 | Nhấn "Submit", không đính ảnh | tap toạ độ | ✅ | — | |
| 8 | Check màn sau khi gửi | quan sát | ✅ | `TC-TS-013__verify-0-anh-gui-thanh-cong.png` | "Your response was submitted.", không có lỗi đòi ảnh |

**Result: ✅ PASS** — `FE-325` đã fix đúng. Before: ❌ FAIL ở VR-019 — ảnh cũ xem `VR-019-TS-2026-09-22/vibe-log.md` §TC tương ứng.
⚠️ Expected của TC còn ghi chữ "Đã ghi nhận phản hồi" (màn app-branded cũ, đã hết hiệu lực theo `C-TS-04(b)`) — đã sửa Expected theo màn mặc định Microsoft Forms cùng lượt này.
**Evidence:** `screenshots/TC-TS-013__pre-form-filled-0-anh.png` · `screenshots/TC-TS-013__verify-0-anh-gui-thanh-cong.png`

## TC-TS-009 — Check gửi báo cáo sự cố hợp lệ hiện màn ghi nhận kèm cam kết liên hệ lại *(Expected sửa 2026-09-24: màn mặc định MS Forms)*

| Step | Hành động | Cách làm | Kết quả | Evidence | Ghi chú |
|---|---|---|---|---|---|
| 1-3 | (setup) Đóng màn xác nhận, mở lại form | find + tap | ✅ | — | |
| 4 | Chọn "Sự cố đơn hàng" | tap toạ độ | ✅ | — | |
| 5 | Nhập "Hàng bị móp góc khi giao" | clipboard + PASTE | ✅ | — | Lần dán đầu ra "FE" (clipboard bị ghi đè) → xoá, dán lại đúng |
| 6 | Nhập "0912345678" | `adb input text` | ✅ | — | |
| 7 | Đính 2 ảnh JPG | "Upload file" → Media picker → chọn tệp vr013_f4_5_6mb (JPG 5.6MB), lặp lại chọn tệp vr013_f1_4_8mb (JPG 4.8MB) trong /sdcard/Pictures | ✅ | `TC-TS-009__pre-form-filled-2-anh.png` | 2 tệp hiện trong danh sách, mỗi tệp có nút xoá |
| 8 | Nhấn "Submit" | tap toạ độ | ✅ | — | |
| 9 | Check màn sau khi gửi | quan sát | ✅ | `TC-TS-009__verify-man-xac-nhan-mac-dinh-ms-forms.png` | Màn mặc định Microsoft Forms: "Your response was submitted." + "Save my response" + "Submit another response" + thẻ quảng cáo Microsoft Forms |

**Result: ✅ PASS** — khớp Expected mới (`C-TS-04(b)`); chuỗi hiển thị tiếng Anh do ngôn ngữ tài khoản Microsoft, tương đương "Đã gửi phản hồi của bạn." (VR-019). Before: ❌ FAIL ở VR-019 — ảnh cũ xem `VR-019-TS-2026-09-22/vibe-log.md` §TC tương ứng.
**Evidence:** `screenshots/TC-TS-009__pre-form-filled-2-anh.png` · `screenshots/TC-TS-009__verify-man-xac-nhan-mac-dinh-ms-forms.png`

## TC-TS-016 — Check mất mạng khi mở báo cáo sự cố thì app hiện lỗi kèm nút thử lại *(Expected sửa 2026-09-24: trang lỗi mặc định WebView)*

| Step | Hành động | Cách làm | Kết quả | Evidence | Ghi chú |
|---|---|---|---|---|---|
| 1-3 | (setup) Đóng màn xác nhận, về "Theo dõi đơn" | find `Quay lại` + tap | ✅ | — | |
| 4 | Ngắt hoàn toàn mạng | `adb shell svc wifi disable` + `svc data disable` | ✅ | — | `dumpsys connectivity`: Active default network = none |
| 5 | Nhấn "Báo cáo sự cố" | find `resourceId("track-report-incident")` + tap | ✅ | — | |
| 6 | Check màn hiện ra | quan sát | ❌ | `TC-TS-016__step6-FAIL-app-ve-man-loi-co-nut-thu-lai.png` · `TC-TS-016__verify-mat-mang-man-loi-app.png` | **App tự vẽ** màn lỗi native: icon "!" + "Không tải được trang" + "Vui lòng kiểm tra kết nối mạng và thử lại." + nút cam **"Thử lại"** (`text("Thử lại")` find được). KHÔNG còn trang lỗi Chromium `net::ERR_INTERNET_DISCONNECTED` như VR-019 |

**Result: ❌ FAIL so với Expected hiện hành** (Expected sửa sáng 2026-09-24: "trang lỗi mặc định của WebView, không có nút Thử lại do app vẽ"). 🔴 **Đây KHÔNG phải lỗi app** — app nay làm **đúng spec gốc** `AC-31.2.01`/`BR16-04` (vế mất mạng) mà BA vừa bảo bỏ khi Won't Fix `FE-322`. Hành vi thật đã đổi so với VR-019 ⇒ QC cần chốt lại Expected (và cân nhắc khôi phục `TC-TS-017`).
Before: ❌ FAIL ở VR-019 (trang lỗi Chromium) — ảnh cũ xem `VR-019-TS-2026-09-22/vibe-log.md`.
**Evidence:** `screenshots/TC-TS-016__step6-FAIL-app-ve-man-loi-co-nut-thu-lai.png` · `screenshots/TC-TS-016__verify-mat-mang-man-loi-app.png`

### Recon ngoài scope (không phải verdict) — luồng "Thử lại" của case thử-lại-giữ-ngữ-cảnh (TC 017, đang DESCOPED)

Bật lại mạng (`svc wifi enable` + `svc data enable`) → nhấn "Thử lại" → form tải được, ô "Mã đơn hàng" vẫn là `01a0b8ce-11a9-7d61-af4d-388ab682f669` (**giữ ngữ cảnh đơn**) — đúng Expected gốc của `TC-TS-017`. Ảnh: `screenshots/_recon__thu-lai-sau-khi-co-mang.png`. Chỉ ghi nhận để QC quyết định bỏ DESCOPED; ⛔ không tính vào coverage.

## Setup

Ảnh màn hình lúc bắt đầu (Đơn của tôi, 1 đơn Đã ghép): `screenshots/_setup__emulator-current-screen.png`.

## 🆕 Follow-up 2026-09-24 — QC chốt lại Expected `TC-TS-016` theo hành vi hiện tại

QC yêu cầu sửa Expected `TC-TS-016` theo đúng hành vi app đang có: *"App hiển thị màn lỗi "Không tải được trang" kèm dòng "Vui lòng kiểm tra kết nối mạng và thử lại." và nút "Thử lại"; form Microsoft Forms không hiện ra."* Ảnh verify đã chụp ở trên khớp đúng Expected mới ⇒ **TC-TS-016: ❌ FAIL → ✅ PASS**, không cần chạy lại (cùng cách xử lý `TC-TS-010/011` ở VR-019).
**Evidence:** `screenshots/TC-TS-016__verify-mat-mang-man-loi-app.png`
