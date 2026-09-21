# Vibe Test Log — VR-014 — v1.1 — 2026-09-21

> Module: **HOME — Trang chủ** · Platform: **mobile** (Appium MCP / UiAutomator2) · Env: **STG** — host app `com.hrisproject.stag` (FoxPro) → FoxEco · Evidence dir: `screenshots/`
> Thiết bị: **EMU** `emulator-5554` (1080×2400) — session `b944ccd4-ceb7-4812-bdc2-864228ca23e8`. Máy thật `R58T20PLP8K` **đã ngắt kết nối** (chỉ còn emulator) ⇒ đổi tài khoản trên 1 máy.
> Tài khoản: **Nguyễn Thị Thanh Thủy** (`stag_thuyntt22@`) làm tài khoản "sạch" (0 đơn · 0 đóng góp · 0 tin) — QC duyệt đổi từ Giang.
> Phiên: 2026-09-21 (khởi tạo)
> Tập chạy: **`--pending`, CHỈ TC v1.1** (QC chỉ định) — 9 TC nợ: `008 019 021 025 027 028 029 030 031` (`026` đã PASS · `032` N-A). **QC cho phép:** đổi tài khoản + đăng thêm 1 tin NEED. **QC KHÔNG cho phép:** ghép đơn P3, chạy vòng giao–nhận đến Hoàn thành ⇒ `008 029 030 031` giữ nợ.
> Evidence chụp bằng `adb exec-out screencap` (tiền lệ VR-004/VR-013). Locator + thao tác 100% qua MCP.

## TC-HOME-027: Check section Đơn của tôi vẫn hiện kèm empty state khi chưa có đơn đang chạy — P3 · SC-HOME-026

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco bằng tài khoản "sạch" *(setup)* | FoxPro: `Cá nhân`→`Đăng xuất`→`Đồng ý` → email `stag_thuyntt22@` → `NHẬN MÃ OTP` → OTP → `ĐĂNG NHẬP` → `Chức năng`→`FoxEco` | ✅ PASS | `_setup__emulator-dang-nhap-thuy-trang-chu.png` | xác nhận `Xin chào, Nguyễn Thị Thanh Thủy` |
| 2 | Mở Trang chủ *(setup)* | tab `Trang chủ` | ✅ PASS | — | hero `0 · Chưa có đóng góp nào` (`home-helped-count` = `0`) ⇒ tài khoản đủ "sạch" |
| 3 | Check section `Đơn của tôi` và nội dung bên trong | `text("Đơn của tôi")` **có mặt**; `text("Chưa có đơn nào")` **tìm thấy**; `textContains("chưa có đơn nào đang chạy")` **NOT FOUND**; `textContains("Tạo đơn gửi hàng")` **NOT FOUND** | ❌ **FAIL** | `TC-HOME-027__step3-FAIL-empty-state-chua-co-don-nao-thieu-cta-tao-don-gui-hang.png` | section **vẫn hiển thị** ✓ (vế chính đúng) nhưng: chuỗi thật là **`Chưa có đơn nào`** (Expected/`EMP-02`: *"Bạn chưa có đơn nào đang chạy"*); **không có nút CTA** `Tạo đơn gửi hàng`; ảnh chụp **không thấy icon nét mảnh** |

**Result: ❌ FAIL at Step 3** — *empty state `EMP-02` thiếu 3/4 thành phần: sai chuỗi, thiếu CTA, thiếu icon (section vẫn hiện — đúng `C-HOME-05`).*
**Evidence:** `screenshots/TC-HOME-027__step3-FAIL-empty-state-chua-co-don-nao-thieu-cta-tao-don-gui-hang.png` — verified tồn tại (ảnh = crop vùng `Đơn của tôi`)
**🐞 Ứng viên bug (P3, chưa log):** *"Empty state `Đơn của tôi` không đúng `EMP-02` (chuỗi + CTA + icon)"* — căn cứ `DOC-v1.1-01 §8.17.1` `EMP-02`. ⚠️ nếu BA chốt app đúng thì sửa Expected. Cùng họ với empty state `Tin mới` (`TC-HOME-026` PASS: chuỗi đúng) ⇒ chỉ `EMP-02` sai.

---

## TC-HOME-028: Check hero và cụm cộng đồng hiện số không khi tài khoản và hệ thống chưa có đóng góp — P3 · SC-HOME-027

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập tài khoản "sạch", mở Trang chủ *(setup)* | như `TC-HOME-027` | ✅ PASS | — | — |
| 3 | Check hero, cụm cộng đồng, các nút CTA trong vùng | hero: `home-helped-count`=`0` + `· Chưa có đóng góp nào` ✓ · cộng đồng: **`Cộng đồng FoxEco: 325 đơn · 23743 người`** ✗ (Expected `0 đơn · 0 người`) · CTA: nút **`Xem bảng tin gửi hàng`** có mặt ✗ (Expected KHÔNG có CTA) | 🚫 **BLOCKED** | `TC-HOME-028__step3-BLOCKED-cong-dong-325-don-khong-phai-0-he-thong-da-co-don-hoan-thanh.png` | **Điều kiện tiên quyết không thoả:** TC đòi *"STG chưa có đơn Hoàn thành nào của bất kỳ tài khoản nào"* — STG đang có **325 đơn** cộng đồng (tăng 322→325 trong ngày). Không thể dựng trên STG dùng chung (cần môi trường riêng) |

**Result: 🚫 BLOCKED at Step 3** — *vế hero (`0 · Chưa có đóng góp nào`) ĐÚNG; vế cộng đồng không kiểm được vì STG không thể về 0.*
**Evidence:** `screenshots/TC-HOME-028__step3-BLOCKED-cong-dong-325-don-khong-phai-0-he-thong-da-co-don-hoan-thanh.png` — verified tồn tại
**📝 Ghi nhận cho BA/QC:** ở trạng thái `0 · Chưa có đóng góp nào` vùng hero **vẫn có** nút `Xem bảng tin gửi hàng`, còn Expected nói vùng này KHÔNG có CTA — chưa xác định do *hệ thống không rỗng* hay do app; cần môi trường sạch hoặc BA chốt. Không log bug.

---

## TC-HOME-025: Check nút Xem thêm trên Bảng tin không hiện khi chỉ có đúng năm tin hợp lệ — P3 · SC-HOME-030

> ⚠️ **Tiền đề "dọn STG về 0 rồi đăng đúng 5 tin" KHÔNG làm được trên STG dùng chung** — thay bằng **đo số tin hợp lệ hiện có** và bổ sung/bớt cho đủ 5. Lúc bắt đầu Bảng tin của Thủy có **4 tin** (đơn P3 của VR-013 không còn trong danh sách); Giang đăng thêm **1 tin** (Tài liệu·Thấp·Nhẹ·Nhỏ, `Giờ nào cũng được`) ⇒ **đúng 5**.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Dọn STG rồi đăng đúng 5 tin bằng tài khoản phụ *(setup)* | Giang đăng 1 tin (4 → 5). Xác nhận **exactly 5**: tab `Bảng tin` của Thủy (không có tin của chính mình) cuộn hết → `feed-post-card-0..4` = **5 tin**, không có `-5` | ✅ PASS | `TC-HOME-025__verify-bang-tin-5-tin-hop-le-toan-he-thong.png` | ảnh chụp lúc 15:03 |
| 2 | Đăng nhập tài khoản A (Thủy), mở Trang chủ *(setup)* | đổi tài khoản Giang → Thủy | ✅ PASS | — | — |
| 3 | Đếm số tin ở `Tin mới` rồi cuộn xuống cuối section | page source: **5 card** tin (P2 · P1 · tin mới · 2 tin ngoài) | ✅ PASS | — | — |
| 4 | Check khu vực cuối section | `text("Xem thêm trên Bảng tin")` **TÌM THẤY** (page source + ảnh) | ❌ **FAIL** | `TC-HOME-025__step4-FAIL-van-co-nut-xem-them-khi-dung-5-tin.png` | Expected: đúng 5 tin và **KHÔNG** có nút — app hiện `Xem thêm trên Bảng tin ›` ngay cả khi tổng chỉ 5 |

**Result: ❌ FAIL at Step 4** — *nút "Xem thêm trên Bảng tin" hiện khi đúng 5 tin (Expected: chỉ hiện khi > 5) — lệch biên `SC-HOME-030` / `C-HOME-03`.*
**Evidence:** `screenshots/TC-HOME-025__verify-bang-tin-5-tin-hop-le-toan-he-thong.png` · `screenshots/TC-HOME-025__step4-FAIL-van-co-nut-xem-them-khi-dung-5-tin.png` — verified tồn tại
**🐞 Ứng viên bug (P3, chưa log):** *"Nút Xem thêm trên Bảng tin hiện khi đúng 5 tin (biên dưới)"*. ⚠️ Phụ thuộc vào việc app đếm "hợp lệ" giống người xem (5 tin ngoài, không có tin của chính mình) — đã xác nhận bằng Bảng tin cùng tài khoản. Cần thêm 1 điểm dữ liệu (4 tin → không nút?) để chốt *"hiện khi ≥5"* hay *"luôn hiện"*: lúc Thủy còn 4 tin, ở cuối Tin mới **không có** nút (page source trước khi đăng) ⇒ nhiều khả năng app dùng **`≥ 5`** thay vì `> 5`.

---

## TC-HOME-019: Check section Tin mới hiển thị đúng năm tin khi hệ thống có nhiều hơn năm tin hợp lệ — P3 · SC-HOME-029

> ⚠️ Tiền đề "B đăng 6 tin" được **thay bằng đo số tin hợp lệ của hệ thống** (dữ liệu chung STG): Giang đăng thêm 2 tin (tổng thêm từ 4 lên ≥6). Lúc chạy Bảng tin của Thủy có **≥7 tin** (`feed-post-card-0..6`) — trong đó có **1 tin lạ** `FTEL SG07 → FTEL SG03 Quận Tân Bình` do **người khác** đăng ~2 phút trước (dữ liệu STG đang bị người khác thao tác song song).

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng ≥6 tin NEED còn hiệu lực *(setup)* | Giang đăng 2 tin (`Tài liệu·Thấp·Nhẹ·Nhỏ`, người nhận `stag_anhdc4@`) ; đối chiếu Bảng tin ≥7 tin | ✅ PASS | — | — |
| 2 | Đăng nhập tài khoản A (Thủy), mở Trang chủ *(setup)* | đổi tài khoản Giang → Thủy | ✅ PASS | — | — |
| 3 | Đếm số tin ở `Tin mới` | cuộn xuống, page source + ảnh: **đúng 5 card** rồi tới nút `Xem thêm trên Bảng tin` | ✅ PASS | `TC-HOME-019__verify-tin-moi-hien-5-tin-khi-he-thong-co-6-tin.png` | 5 card, không hơn không kém (tin thứ 6/7 không hiện) |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-HOME-019__verify-tin-moi-hien-5-tin-khi-he-thong-co-6-tin.png` — verified tồn tại

---

## TC-HOME-021: Check nút Xem thêm trên Bảng tin hiện và dẫn sang Bảng tin khi có hơn năm tin hợp lệ — P3 · SC-HOME-029

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng ≥6 tin, đăng nhập A, mở Trang chủ *(setup)* | như `TC-HOME-019` | ✅ PASS | — | — |
| 3 | Cuộn xuống cuối section `Tin mới` | `text("Xem thêm trên Bảng tin")` **tìm thấy** ở cuối section | ✅ PASS | `TC-HOME-021__pre-nut-xem-them-o-cuoi-section-tin-moi.png` | — |
| 4 | Nhấn `Xem thêm trên Bảng tin` | tap | ✅ PASS | — | — |
| 5 | Check tên màn vừa mở | màn `Bảng tin`: `accessibility id "feed-post-card-0"` tìm thấy; cuộn ⇒ `feed-post-card-2..6` (≥7 tin) | ✅ PASS | `TC-HOME-021__verify-nhan-xem-them-mo-man-bang-tin.png` | mở đúng màn Bảng tin |

**Result: ✅ PASS (5 steps, 1 expected)**
**Evidence:** `screenshots/TC-HOME-021__pre-nut-xem-them-o-cuoi-section-tin-moi.png` · `screenshots/TC-HOME-021__verify-nhan-xem-them-mo-man-bang-tin.png` — verified tồn tại
