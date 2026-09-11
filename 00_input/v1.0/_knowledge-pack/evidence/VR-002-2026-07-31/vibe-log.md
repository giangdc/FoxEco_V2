# Vibe Test Log — VR-002 — v1.0 — 2026-07-31 (afternoon)

> Platform: mobile (Appium MCP, real Android device ZPB66PZLPRBMEAZT)
> Module: Đăng tin (TC_04) — scope: Priority ∈ {High, Medium}, excluding TC_04.2/TC_04.73 (already PASS in VR-001)
> App: FoxEco SDK — package confirmed this run: `vn.fpt.ftel.sop.stg`
> Account: pre-logged-in, "Chung Hoàng Liêm"

## Group A: Đăng tin mới (chọn vai trò)

### TC_04.1: Check đầy đủ 5 thành phần hiển thị tại màn 'Đăng tin mới'

| # | Step | Result | Notes |
|---|------|--------|-------|
| 1 | Quan sát toàn bộ màn 'Đăng tin mới' | ✅ PASS | (1) subtitle "Bạn muốn làm gì?" ✅ (2) card "Tôi cần gửi hàng" icon hộp cam + đúng mô tả ✅ (3) card "Tôi nhận giao hàng" icon route tím + đúng mô tả ✅ (4) banner cam kết nền vàng nhạt icon ⓘ đúng nguyên văn ✅ (5) 2 card bấm được — xác nhận qua TC_04.2 (card 1) + TC_04.3 (card 2) đều tap thành công |

**Result: ✅ PASS** — **Screenshot:** `screenshots/TC_04.1_final.png`

### TC_04.3: Check chọn 'Tôi nhận giao hàng' chuyển sang Form đăng ký tuyến (OFFER)

| # | Step | Result | Notes |
|---|------|--------|-------|
| 1 | Bấm 'Tôi nhận giao hàng' | ✅ PASS | Chuyển sang Form OFFER 1 trang (không có step indicator Bước x/3) — đúng expected |

**Result: ✅ PASS** — **Screenshot:** `screenshots/TC_04.3_final.png`
**Note:** Form OFFER fields quan sát được (dùng lại cho Group K sau): "Thông tin của tôi" (Tên, SĐT — read-only, auto-filled), "Điểm xuất phát (A)", "Điểm đến (B)", "Khoảng thời gian (ngày)" Từ ngày/Đến ngày, "Thời gian di chuyển" Khởi hành/Đến nơi, nút "Đăng tin ngay".

---

## Group B: Wizard Bước 1/3 (Thông tin hàng)

> ⚠️ Lưu ý xuyên suốt group này: chip Loại hàng mặc định là **"Giấy tờ, hồ sơ"**, KHÔNG PHẢI "Tài liệu" như TC ghi (finding đã log ở VR-001). Mọi step ghi "Tài liệu" bên dưới đều thực hiện bằng chip mặc định "Giấy tờ, hồ sơ" thay thế.

### TC_04.4: Check đầy đủ 4 field hiển thị tại Bước 1/3
✅ PASS — đủ 4 field đúng thứ tự: Loại hàng (chip) → Ghi chú (textarea) → Giá trị hàng (chip) → Ảnh hàng (chụp/thư viện). **Screenshot:** `TC_04.4_final.png`

### TC_04.5: Check Loại hàng mặc định = 'Tài liệu' khi mở Bước 1/3 lần đầu
❌ FAIL — chip mặc định được chọn là **"Giấy tờ, hồ sơ"**, không phải "Tài liệu" (chip "Tài liệu" không tồn tại trong 8 lựa chọn thực tế). **Screenshot:** `TC_04.5_final.png`
**Finding:** xác nhận lại finding VR-001 #1 (Loại hàng chip naming mismatch) — cần BA/dev xác nhận đổi tên TC hay UI có bug.

### TC_04.6: Check bỏ trống Loại hàng vẫn bấm 'Tiếp theo' bị chặn
❌ FAIL — tap lại chip Loại hàng đang chọn KHÔNG deselect được (single-select, luôn có 1 chip mặc định được giữ). Do đó không thể tái hiện trạng thái "không chọn Loại hàng nào" qua UI thật. Đã thử: chọn Giá trị hàng=Vừa, bấm Tiếp theo → **chuyển sang Bước 2/3 thành công, KHÔNG bị chặn** — trái với expected "bị chặn tại field Loại hàng". **Screenshot:** `TC_04.6_final.png`
**Finding:** Precondition TC không thể thiết lập được trên UI hiện tại (Loại hàng luôn có default, không rỗng được).

### TC_04.7: Check bỏ trống Giá trị hàng vẫn bấm 'Tiếp theo' bị chặn
✅ PASS (hành vi cốt lõi đúng) — Loại hàng giữ mặc định "Giấy tờ, hồ sơ" (thay cho "Tài liệu"), Giá trị hàng để trống, bấm 'Tiếp theo' → nút chuyển màu nhạt/disabled, KHÔNG chuyển Bước 2/3 — đúng expected (bị chặn tại Giá trị hàng). **Screenshot:** `TC_04.7_final.png`

### TC_04.8: Check chọn Giá trị hàng = 'Thấp' KHÔNG hiện cảnh báo
✅ PASS — không có banner cảnh báo. **Screenshot:** `TC_04.8_final.png`

### TC_04.9: Check chọn Giá trị hàng = 'Vừa' KHÔNG hiện cảnh báo
✅ PASS — không có banner cảnh báo. **Screenshot:** `TC_04.9_final.png`

### TC_04.10: Check chọn Giá trị hàng = 'Cao' hiện cảnh báo trách nhiệm tự thoả thuận
✅ PASS — banner hiện đúng, nguyên văn verbatim: *"Hàng giá trị cao: hai bên tự thoả thuận và chịu trách nhiệm với nhau. FoxEco không bảo hiểm, không đứng ra vận chuyển hay bồi thường."* **Screenshot:** `TC_04.10_final.png`

**Group B summary: 5 PASS / 2 FAIL (TC_04.5, TC_04.6) — cả 2 FAIL đều liên quan finding "Loại hàng" đã biết.**

---

## Group C: Bước 2/3 — Người gửi (TC_04.21-25)

### TC_04.21: Check đầy đủ 3 field Người gửi tự động điền từ tài khoản
❌ FAIL — Tên ✅ pre-filled, SĐT ✅ pre-filled, nhưng **Địa chỉ lấy hàng KHÔNG pre-fill** (trống, placeholder) — expected phải mặc định "Tòa nhà Lô B3, KCX Tân Thuận, Q.7". **Screenshot:** `TC_04.21_final.png`
**Finding:** Địa chỉ lấy hàng mặc định không load như spec — cần xác nhận với dev đây là bug hay spec đã đổi (tài khoản test có thể chưa cấu hình địa chỉ mặc định).

### TC_04.22: Check field Tên (Người gửi) không cho chỉnh sửa (read-only)
❌ FAIL — Chạm vào field Tên **MỞ ĐƯỢC bàn phím** (không phải disabled/readonly như expected), và giá trị "Chung Hoàng Liêm" bị **XOÁ TRẮNG** ngay sau khi chạm (không tự phục hồi trong cùng phiên wizard — phải thoát ra vào lại từ đầu Bước 1/3 mới load lại đúng tên). **Screenshot:** `TC_04.22_final.png`
**🐞 Finding nghiêm trọng:** Tên (Người gửi) thực chất là field có thể focus/edit được, trái hẳn với "read-only" trong spec — rủi ro user vô tình xoá tên khi chạm nhầm, tên không tự khôi phục ngay, phải rời khỏi wizard mới reset. Đề xuất log bug riêng.

### TC_04.23: Check bỏ trống SĐT (Người gửi) bị chặn
✅ PASS — Xoá trống SĐT gửi, bấm 'Tiếp theo' → không chuyển bước (nút disabled), đúng expected. **Screenshot:** `TC_04.23_final.png`

### TC_04.24: Check SĐT (Người gửi) đúng định dạng chuẩn VN hợp lệ
✅ PASS — Điền đủ toàn bộ field hợp lệ (SĐT gửi 0912345678, địa chỉ lấy hàng qua suggestion, email nhận hợp lệ auto-fill, SĐT/địa chỉ nhận sửa hợp lệ, khung giờ điều chỉnh tương lai) → bấm 'Tiếp theo' chuyển sang Bước 3/3 không lỗi. **Screenshot:** `TC_04.24_final.png`
**Note:** Auto-fill từ email `stag_anhdc4@fpt.com` lần này trả về SĐT người nhận mặc định "0000286248" — chính app tự báo "Số điện thoại không hợp lệ" cho giá trị auto-fill của chính nó (finding phụ, xem Group F).

### TC_04.25: Check SĐT (Người gửi) sai định dạng bị chặn
⏳ **KHÔNG HOÀN THÀNH — device mất kết nối màn hình giữa chừng.** Đã nhập SĐT gửi sai định dạng "912345678" (thiếu số 0 đầu) thành công (set_value OK), nhưng **chưa kịp bấm 'Tiếp theo' và chụp màn hình xác nhận** thì màn hình thiết bị tối đen liên tục dù `dumpsys power` báo `mWakefulness=Awake` — nghi ngờ màn khoá bảo mật (PIN/vân tay) mà lệnh `mobile: unlock` chỉ dismiss được ở tầng input, không hiển thị nội dung thật; xác nhận qua cả `adb screencap` trực tiếp (không qua Appium) vẫn ra file đen thui identical byte-size nhiều lần liên tiếp → khả năng cao là vấn đề vật lý (khoá bảo mật cần user mở tay, hoặc máy úp mặt xuống bàn kích hoạt cảm biến).
**→ Cần user kiểm tra lại thiết bị vật lý rồi chạy tiếp `/vibe-test --retest TC_04.25` hoặc `/vibe-test --tc TC_04.25` sau.**

**Group C summary: 2 PASS / 2 FAIL / 1 KHÔNG HOÀN THÀNH (device blocker).**

---

## Group D: Bước 2/3 — Địa chỉ lấy hàng (TC_04.29, 31) — PARTIAL (dừng do device blocker)

### TC_04.29: Check nhập text vào Địa chỉ lấy hàng hiển thị danh sách gợi ý để CHỌN
✅ PASS — gõ "Lô 37-39A KCX Tân Thuận" → dropdown gợi ý xuất hiện đúng bên dưới field, chọn được. **Screenshot:** `TC_04.29_final.png`

### TC_04.31: Check gõ text nhưng KHÔNG chọn gợi ý → không được lưu
⏳ **CHƯA THỰC HIỆN** — dừng do device blocker (xem TC_04.25). Cần chạy lại.

---

## ⚠️ RUN TẠM DỪNG — Device blocker (màn hình đen dai dẳng)

Từ đây trở đi (TC_04.32 trở về sau — Group E/F/G/H/I/J/K/L, tổng ~58 TC còn lại trong scope High+Medium) **CHƯA THỰC HIỆN** do thiết bị không phản hồi hiển thị dù OS báo `Awake`. Đã thử: `input keyevent 224` (wakeup) ×3, `input keyevent 82` (menu/wake), `mobile: unlock` ×2, `adb screencap` trực tiếp (bypass Appium hoàn toàn) — tất cả đều ra kết quả đen giống hệt nhau. Đây nhiều khả năng là vấn đề vật lý (khoá bảo mật thật cần thao tác tay, hoặc máy bị che/úp) chứ không phải lỗi phần mềm phía MCP/test script.

**Cần user:** kiểm tra + mở khoá thiết bị vật lý, sau đó chạy `/vibe-test` lại (mặc định sẽ tự bỏ qua các TC đã ✅ PASS/❌ FAIL đã ghi, tiếp tục từ TC_04.25 trở đi).

