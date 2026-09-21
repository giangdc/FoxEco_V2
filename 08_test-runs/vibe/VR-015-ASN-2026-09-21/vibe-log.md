# Vibe Test Log — VR-015 — v1.1 — 2026-09-21

> Module: ASN · Platform: mobile (Appium MCP + `adb`) · **2 thiết bị đồng thời**: real device `R58T20PLP8K` (Samsung A12s, 720×1600) + `emulator-5554` (1080×2400) · Env: STG — host app FoxPro `com.hrisproject.stag` · Evidence dir: `screenshots/`
> Phiên: 2026-09-21 (16:00–16:26) · Tập chạy: **1 TC — `TC-ASN-006`** (QC đã cắm 1 real + 1 emulator, yêu cầu chạy lại case đa thiết bị) · QC chốt **dùng tin có sẵn, không tạo tin mới**.
> ⚠️ Evidence chụp bằng `adb exec-out screencap -p` (lý do như VR-008/009/010: `appium_screenshot` trả HTML viewer rất lớn vào context).

## 🧭 Thiết lập phiên — 2 lần chạy, chỉ lần 2 hợp lệ

| Lần | Actor (real / emulator) | Tin | Kết quả | Hợp lệ? |
|---|---|---|---|---|
| **1** *(16:13)* | `stag_taipm@` / `stag_thuyntt22@` (Nguyễn Thị Thanh Thủy) | tin #1 của `stag_giangdc2@` | real ghép thành công; emulator bị từ chối với toast **"Bạn cần chấp nhận điều khoản hiện hành trước khi đăng tin hoặc ghép chuyến"** | ❌ **KHÔNG hợp lệ** — emulator thua vì **chưa chấp nhận điều khoản**, ⛔ không phải vì thua cuộc đua ⇒ không chứng minh được gì về tính duy nhất. Ảnh giữ lại làm ghi chú: `_recon__lan-1-khong-hop-le-chua-chap-nhan-dieu-khoan.png` |
| **2** *(16:22)* | `stag_taipm@` (real) / `stag_anhptm17@` (**Phan Thị Mỹ Anh**, emulator) | tin #2 của `stag_giangdc2@` *(cùng tuyến, còn `Chờ ghép`)* | **1 thắng — 1 thua đúng expected** | ✅ hợp lệ |

**Vì sao đổi tài khoản giữa 2 lần:** `Thủy` chưa chấp nhận điều khoản ⇒ không thể ghép. `stag_anhptm17@` đã có **6 đơn đã giúp** ⇒ điều khoản đã chấp nhận. `stag_anhdc4@` (đang đăng nhập sẵn trên real device) **không thấy nút `Tôi mang giúp được`** ở các tin của `stag_giangdc2@` (đã mở 2 tin, chờ 9–10s để loại trừ lỗi tải) — chưa rõ nguyên nhân, xem `vibe-report.md §Phát hiện`. ⇒ real device được đăng xuất khỏi `anhdc4` và đăng nhập `taipm`.

**Tin dùng:** tin của `Đặng Châu Giang` — `FTEL Đà Nẵng Cẩm Lệ → Tòa V-City, Lê Thái Tổ` · `Hôm nay · Giờ nào cũng được` · `Tài liệu · Thấp · Nhẹ · Nhỏ` · ảnh `VIBE TEST VR-001 · TC-USR-025` · tuổi ~1 giờ. ⛔ Không chọn tin của `Nguyễn Tấn Vũ` (dữ liệu của người khác, có `stag_taipm@` là người nhận) để khỏi ảnh hưởng dữ liệu ngoài phạm vi QC.

---

## TC-ASN-006: Check hai người vận chuyển nhận gần đồng thời chỉ một người ghép được

> Scenario `SC-ASN-006` · P1 · Nhánh (a) — 2 thiết bị thật; nhánh (b) 50 request nằm ở `TC-ASN-024` *(BLOCKED)* · Tài khoản: **A** chủ tin `stag_giangdc2@` (không thao tác — dùng tin có sẵn) · **B** `stag_taipm@` (real device) · **C** `stag_anhptm17@` (emulator)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | A đăng 1 tin NEED rồi đăng xuất *(setup)* | ⛔ **không thực hiện** — QC chốt dùng tin có sẵn của `stag_giangdc2@` | ✅ PASS | — | Tin đã có sẵn ở `Chờ ghép` (đọc trên Bảng tin cả 2 máy) |
| 2 | B trên thiết bị 1, C trên thiết bị 2, cùng mở Chi tiết tin *(setup)* | Bảng tin → mở tin → cuộn tới nút | ✅ PASS | — | Cả 2 máy hiện cùng tin: `Đặng Châu Giang` · `FTEL Đà Nẵng Cẩm Lệ → Tòa V-City` · `Hôm nay · Giờ nào cũng được` · nút `Tôi mang giúp được` đều **bật** |
| 3 | Trên cả 2 thiết bị nhấn `Tôi mang giúp được` | `adb -s <máy> shell input tap` | ✅ PASS | `TC-ASN-006__pre-hai-may-cung-o-modal-xac-nhan.png` | Cả 2 máy hiện modal `Xác nhận mang giúp` — *"Nhận mang giúp ngay — SĐT sẽ lộ cho cả hai bên để liên hệ"* |
| 4 | Nhấn `Xác nhận` trên cả 2 máy cách nhau **<2 giây** | **1 lệnh Bash duy nhất** chạy 2 `adb ... input tap` song song (`&` + `wait`) | ✅ PASS | `TC-ASN-006__verify-chuoi-4-khung-hinh-ca-hai-may.png` | Mốc đo ns: cả 2 tiến trình **khởi động cùng lúc** (`…427758100` vs `…427758069`, lệch **31 ns**); tiến trình xong lúc `+94 ms` (real) và `+24 ms` (emulator). ⇒ độ lệch giữa 2 lần chạm **≤ ~95 ms**, ≪ 2s |
| 5 | Check màn hiện ra trên từng thiết bị *(ghi từng khung ~0.25s)* | chụp xen kẽ 2 máy × 4 khung | ✅ PASS | `TC-ASN-006__verify-nguoi-thang-vao-theo-doi-don.png` + `TC-ASN-006__verify-nguoi-thua-toast-tin-da-co-nguoi-nhan.png` | **Emulator (Mỹ Anh)** → màn **`Theo dõi đơn`** vai người vận chuyển: stepper `Chờ ghép → Lấy hàng`, `NGƯỜI GỬI Đặng Châu Giang · 0912345670 · stag_giangdc2@fpt.com`, nút `Gọi` bật, `Tôi đã lấy hàng` + `Huỷ nhận đơn`. **Real device (taipm)** → ở lại `Chi tiết tin`, toast đỏ **"Tin đã có người nhận vận chuyển"** (giữ ≥3 khung liên tiếp, ~0.7s) |
| E1 | **Đúng 1 thiết bị vào `Theo dõi đơn`, thiết bị còn lại KHÔNG ghép được + thông báo "tin đã có người nhận"** | so 2 màn hình | ✅ PASS | `TC-ASN-006__verify-nguoi-thang-vao-theo-doi-don.png` + `TC-ASN-006__verify-nguoi-thua-toast-tin-da-co-nguoi-nhan.png` | Đúng nguyên văn kỳ vọng. Ai thắng là **kết quả cuộc đua** (lần này emulator), ⛔ không phải do thứ tự bấm |
| 6 | Đăng nhập lại tài khoản A, check người vận chuyển của đơn *(2026-09-21 16:56–16:58, bổ sung sau)* | emulator: logout `stag_anhptm17@` → login `stag_giangdc2@` → FoxEco → `Hoạt động` → mở 2 đơn `Đã ghép` cùng tuyến | ✅ PASS | `TC-ASN-006__verify-chu-tin-thay-1-nguoi-van-chuyen-la-nguoi-thang.png` | Đơn của **race** (đăng 15:00): `LỊCH SỬ` = **`Ghép thành công · Hôm nay · 16:22 · Phan Thị Mỹ Anh`** — SĐT carrier `0947153040`. Đơn còn lại (đăng 15:11, tin #1 của lần chạy không hợp lệ): `Ghép thành công · 16:13 · Phan Minh Tài`, SĐT `0833329408`. ⇒ mỗi đơn có **đúng 1** mục *Ghép thành công* và **đúng 1** người vận chuyển; đơn race thuộc **người thắng (Mỹ Anh)**, ⛔ không thuộc người thua (taipm). Giờ 16:22 khớp thời điểm bấm |
| E2 | **Đơn có đúng 1 người vận chuyển = tài khoản thiết bị ghép thành công** | so `LỊCH SỬ` đơn race với người thắng | ✅ PASS | `TC-ASN-006__verify-chu-tin-thay-1-nguoi-van-chuyen-la-nguoi-thang.png` | Người vận chuyển = `Phan Thị Mỹ Anh` = tài khoản trên emulator thắng cuộc đua |

**Result: ✅ PASS** *(6 steps + E1 + E2 — đủ mọi vế của Expected)*
**Evidence:** `screenshots/TC-ASN-006__pre-hai-may-cung-o-modal-xac-nhan.png` + `screenshots/TC-ASN-006__verify-nguoi-thang-vao-theo-doi-don.png` + `screenshots/TC-ASN-006__verify-nguoi-thua-toast-tin-da-co-nguoi-nhan.png` + `screenshots/TC-ASN-006__verify-chuoi-4-khung-hinh-ca-hai-may.png` + `screenshots/TC-ASN-006__verify-chu-tin-thay-1-nguoi-van-chuyen-la-nguoi-thang.png` (+ `screenshots/_recon__lan-1-khong-hop-le-chua-chap-nhan-dieu-khoan.png`)

### ⚖️ Giới hạn của phép thử — đọc trước khi trích dẫn kết quả này

- ✅ *Cập nhật 2026-09-21 16:58:* vế "đăng nhập lại A" đã chạy, xem Step 6/E2 — giới hạn *không có góc nhìn chủ tin* **không còn**.
- **1 mẫu, không phải thống kê.** Chỉ chứng minh ở mức *"2 người bấm cách nhau ≤95 ms trên cùng tin ⇒ hệ thống cho đúng 1 người thắng"* trong **1 lần**. ⛔ Không thay thế `TC-ASN-024` (50 request đồng thời, NFR-06 ≤0% trùng).
- **Độ lệch ≤95 ms là cận trên** suy từ thời điểm tiến trình `adb` kết thúc; thời điểm chạm thật nằm đâu đó trong khoảng đó.
- **Real device có lúc timeout mạng** (toast `Kết nối quá thời gian chờ` xuất hiện ở 16:25 khi mở `Hoạt động`) ⇒ các màn danh sách trên máy này **có lúc trống giả**; kết quả của TC **không** dựa vào màn danh sách mà dựa vào khung hình chụp ngay sau khi bấm.
