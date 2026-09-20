# Repro Report — RP-ASN-lo-sdt-sau-ghep — 2026-09-19

> **Hợp đồng NHẸ** (`repro/`): report + ≤3 ảnh, ⛔ KHÔNG per-TC evidence.
> Platform: mobile (Appium MCP / UiAutomator2) · `emulator-5554` · app `com.hrisproject.stag`
> Session: `55129e7d-a214-4167-a988-d83f2e82c2b7` · Tài khoản: **`Đặng Châu Anh`**
> Mục tiêu: xác minh clarification đã ghi ở `INDEX.md §VR-004`.

## Vì sao phiên này là `repro/` chứ không phải `VR-`

Phiên khởi đầu là `/vibe-test --module asn` (EXECUTE). Sau khi seed scope + recon, kết luận:
**cả 26/26 TC của ASN đều chặn tiền đề ⇒ 0 TC thực thi được.**

`vibe/VR-*` là hợp đồng ĐẦY ĐỦ và **bắt buộc có ≥1 TC chạy kèm evidence per-TC**
(`verify_evidence.py`: `log_format_broken = not tc_results and isfile(log_path)` — không có ngoại lệ cho phiên 0-verdict).
⇒ Mở `VR-006` là **sai hợp đồng**; folder đó đã bị **xoá**. Phần recon có giá trị chuyển về đây.

📋 **Ledger 26 TC của ASN vẫn được ghi đầy đủ** ở `08_test-runs/vibe/coverage/coverage-ASN.md`
(24 `⏳ NOT_RUN` + 2 `⛔ N-A`, mỗi dòng kèm lý do) — ⛔ không TC nào bị khai là đã phủ.

## Kết luận 1 — ĐÍNH CHÍNH: SĐT **CÓ** được lộ sau khi ghép

`INDEX.md §VR-004` ghi 1 clarification BA: *"màn đơn **đã ghép** không lộ SĐT, **trái banner cam kết**"*.
Mở đúng màn đó (đơn `Đã ghép`, tuyến `Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy`, **vai người nhận**):

| Đo được (MCP `find_element`) | Giá trị |
|---|---|
| Tiêu đề cụm | `NGƯỜI GIAO HÀNG` |
| Tên người vận chuyển | `Phan Thị Mỹ Anh` |
| **Số điện thoại** | **`0947153040`** ✅ hiện đầy đủ |
| Nút hành động | `Gọi` |

**Ảnh:** `_recon__lo-sdt-sau-ghep-nguoi-giao-hang.png`

### 🔑 Nguyên nhân kết luận cũ sai — bẫy **T18**

Màn "Theo dõi đơn" **chỉ cuộn khi bước cuộn NHỎ**:

| Cách gọi | Kết quả |
|---|---|
| `appium_gesture(action=scroll, direction=down)` | báo *"Successfully scrolled"* — **màn đứng yên** |
| `scroll` với toạ độ tuỳ chỉnh (800→300) | báo thành công — **màn đứng yên** |
| `swipe(direction=up, speed=slow)` | báo thành công — **màn đứng yên** |
| **`scroll_to_element(..., scrollDistancePreset="small")`** | ✅ **cuộn thật**, 4 nhịp |

⇒ Cụm `NGƯỜI GIAO HÀNG` nằm **dưới nếp gấp, bị bottom bar che**; `appium_get_page_source` lúc chưa cuộn
**KHÔNG chứa** tên/SĐT ⇒ rất dễ kết luận *"app không lộ SĐT"*.
**Ảnh:** `_recon__man-theo-doi-don-chua-cuon.png` (màn sau 4 lần scroll "thành công" mà không đổi).

⛔ **KHÔNG** dùng `adb shell wm density` để lộ vùng bị che — đã thử trong phiên, **app restart về host FoxPro, mất ngữ cảnh** (đã khôi phục `320` và vào lại FoxEco).

### ⚠️ Phạm vi của đính chính — ⛔ đừng suy rộng

Chỉ quan sát được **vai người NHẬN**. `TC-ASN-004` đòi vai **người gửi** (E4) và **người vận chuyển** (E3).
⇒ `TC-ASN-004` **giữ `⏳ NOT_RUN`**, ⛔ không đổi thành PASS.
⇒ Việc cần làm: **MỞ LẠI clarification của VR-004** và kiểm đúng 2 vai còn lại — ⛔ không đóng nó bằng quan sát này.

## Kết luận 2 — Đổi tài khoản giữa 2 phiên, suýt tạo phát hiện sai

| | VR-005 (05:51–06:10) | Phiên này (07:51–07:58) |
|---|---|---|
| Tên hiển thị | `Đặng Châu Giang` | **`Đặng Châu Anh`** |
| Hero "đơn đã giúp" | `13` | **`3`** |
| Cộng đồng | `317 đơn · 23743 người` | không đổi |

Cùng **một đơn** (`Tòa V-City → FPT Cầu Giấy`, `Đã ghép`) hiện **`Gửi:`** ở VR-005 và **`Nhận:`** ở phiên này;
đơn `Đồ dễ vỡ` thì ngược lại. Nhìn rất giống bug *"nhãn vai tính sai / không ổn định"*.

✅ **Kiểm header trước khi kết luận ⇒ là 2 TÀI KHOẢN KHÁC NHAU** — cùng 1 đơn thì bên gửi thấy `Gửi:`,
bên nhận thấy `Nhận:`. **Hành vi ĐÚNG, không có bug.**
Đồng thời là **đối chứng dương** cho `TC-HOME-011/012/013` (VR-005): nhãn vai bám theo vai của người đang đăng nhập.
**Ảnh:** `_recon__trang-chu-du-lieu-doi.png`

📌 **Bài học quy trình:** tài khoản đăng nhập trên emulator có thể đổi giữa 2 phiên **mà không ai báo**
⇒ **luôn đọc tên tài khoản ở header trước khi so kết quả với phiên trước.**

## Locators

20 element của 3 màn (Theo dõi đơn vai người nhận · Trang chủ §Đơn của tôi · FoxPro host) đã merge
**100%** vào `08_test-runs/vibe/locators/vibe-locators-latest.md` §MERGE RP-ASN, kèm **T18** và **T2** (lần 4:
`accessibility id "Gọi"` 🚫 / `text("Gọi")` ✅).
⚠️ **12/20 là ⚠️ Inferred** (recon, chưa có action xác nhận) — `implement-automation` phải re-verify.

## Việc cần làm tiếp

1. **Mở lại** clarification VR-004 về lộ SĐT — kiểm vai **gửi** và **vận chuyển**.
2. **Fix bug `B1`** (đăng tin NEED trả `400 REQ_400`) — chặn 20/26 TC của ASN.
3. Cấp **tài khoản phụ + người nhập OTP**, và **thêm emulator thứ 2/3** cho `TC-ASN-006`/`008`.
4. `TC-ASN-024` · `TC-ASN-026` → giao automation/backend/security (`⛔ N-A`, không chờ gì).
