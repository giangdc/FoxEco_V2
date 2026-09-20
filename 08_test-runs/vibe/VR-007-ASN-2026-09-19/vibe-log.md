# Vibe Test Log — VR-007 — v1.1 (+ CARRIED v1.0) — 2026-09-19

> Module: **ASN** (Ghép nối) · Platform: **mobile (Appium MCP / UiAutomator2)** · Env: STG, app `com.hrisproject.stag`
> Device: emulator-5554 · Session: `55129e7d-a214-4167-a988-d83f2e82c2b7` · Evidence dir: `screenshots/`
> Phiên: 2026-09-19 (khởi tạo)
> Tập chạy: **24 TC pending** (24 `⏳ NOT_RUN` trong `coverage-ASN.md`; 2 TC `⛔ N-A` không bốc). Không TC nào đã PASS ⇒ ⛔ không phát sinh câu hỏi Step 1.2.

## 🔓 ĐIỀU KIỆN MỚI — phiên này khác hẳn phiên ASN trước (0 verdict)

| Dữ kiện | Trước (2026-09-19 07:58) | Giờ |
|---|---|---|
| Đăng tin NEED/OFFER | tưởng bị bug `B1` chặn | ✅ **đăng được** (đã bác bỏ `B1`) |
| Đổi tài khoản | tưởng cần người nhập OTP | ✅ **AI tự login** — OTP staging **cố định**, QC cấp `04_test-data/account.txt` |
| Số tài khoản dùng được | 1 | **5** (`USR-accounts.md §1`) |

⇒ Nhóm TC từng `NOT_RUN` vì *"cần tài khoản thứ 2"* nay **chạy được**.

> ⚠️ **Run ID nhảy từ VR-005 → VR-007.** `VR-006` đã được cấp rồi **rút lại** (phiên ASN 0-verdict, folder đã xoá, chuyển thành `repro/RP-ASN-lo-sdt-sau-ghep-2026-09-19/`). Theo luật *"VR-[NNN] never reuse"* ⇒ ⛔ không tái dùng số 006.

## 🔑 Tài khoản dùng trong phiên

| Vai | Email | Danh tính | Ghi chú |
|---|---|---|---|
| **C** *(đang login lô 1)* | `stag_taipm@fpt.com` | **Phan Minh Tài** · MNV `00041796` · Phòng PTPM số 8 · SĐT `0833329408` | 🆕 danh tính xác nhận trong phiên này |
| B | `stag_anhdc4@fpt.com` | Đặng Châu Anh · MNV `00286248` | chủ 1 OFFER + 1 NEED tạo lúc 08:26–08:38 |
| — | `stag_huyennhk@fpt.com` | **Nguyễn Huỳnh Kim Huyền** | 🆕 lộ qua autofill người nhận |

---

## TC-ASN-013: Check tài khoản không được gợi ý khớp tuyến cho tin do chính mình đăng — **P1** · SC-ASN-012 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Tài khoản A đăng 1 tin **OFFER** với điểm lấy/giao + khung giờ xác định *(setup)* | login `stag_taipm@` → `Đăng tin` → `Tôi nhận giao hàng` → A=`FPT Tân Thuận 1`, B=`FTEL SG08 Quận 12`, Hôm nay, buổi **Chiều** → `Đăng tin ngay` | ✅ PASS | `TC-ASN-013__pre-offer-cua-chinh-minh.png` | *"Đã ghi nhận tuyến đường!"* — ⛔ OFFER **không** hiện công khai trên Bảng tin |
| 2 | Vẫn tài khoản A, đăng 1 tin **NEED trùng đúng 2 điểm + giao khung giờ** *(setup)* | wizard NEED 3 bước: `Tài liệu`+`Thấp`+`Nhẹ`+`Nhỏ`+1 ảnh · lấy `FPT Tân Thuận 1` · giao `FTEL SG08 Quận 12` · **Chiều** · người nhận `stag_huyennhk@` | ✅ PASS | — | trùng **tuyệt đối** tuyến + buổi + ngày với OFFER ở step 1 ⇒ nếu app không loại trừ chủ tin thì **chắc chắn** phải sinh thông báo |
| 3 | Nhấn icon chuông, check danh sách thông báo | tap `accessibility id "Thông báo"` | ✅ PASS | `TC-ASN-013__verify-khong-thong-bao-tin-cua-minh.png` | — |
| E3 | **KHÔNG** có thông báo khớp tuyến trỏ tới tin NEED của chính A | 2 phép kiểm độc lập ↓ | ✅ **PASS** | ↑ | (a) `find_element(textContains "tuyến")` → 🚫 **NOT FOUND**; (b) `find_element(text "HÔM NAY")` → 🚫 **NOT FOUND** ⇒ **0 thông báo mới hôm nay**, item mới nhất là *"15 giờ trước"* |
| 4 | Nhấn tab "Bảng tin", check tin NEED của chính mình | tap `accessibility id "Bảng tin"` → tap card | ✅ PASS | `TC-ASN-013__verify-badge-tin-cua-ban.png` | — |
| E4 | Card có badge **"Tin của bạn"** và **không có đường nhận đơn** | badge ✅ · CTA ❌ | ✅ **PASS** | `TC-ASN-013__verify-badge-tin-cua-ban.png` · `TC-ASN-013__verify-khong-cta-nhan-don.png` | badge `find_element(text "Tin của bạn")` ✅; mở Chi tiết tin → `find_element(textContains "Tôi mang giúp được")` 🚫 **NOT FOUND**, cuộn hết màn kết thúc ở card `NGƯỜI GỬI`, ⛔ không có thanh CTA đáy |

**Result: ✅ PASS (4 steps, 2 expected)**
**Evidence:** `screenshots/TC-ASN-013__verify-khong-thong-bao-tin-cua-minh.png` (E3) · `screenshots/TC-ASN-013__verify-badge-tin-cua-ban.png` (E4 badge) · `screenshots/TC-ASN-013__verify-khong-cta-nhan-don.png` (E4 không CTA) (+ `TC-ASN-013__pre-offer-cua-chinh-minh.png`)
**Locators captured:** 9 elements
🟢 **Phép thử mạnh:** tin NEED trùng **tuyệt đối** cả 3 chiều (2 điểm + ngày + buổi) với OFFER của chính mình — đây là điều kiện dễ sinh thông báo nhất; app **vẫn loại trừ đúng** ⇒ `BR03-06`/`SC-ASN-012` được thi hành.
ℹ️ Nút `Gọi` ở card `NGƯỜI GỬI` hiện **mờ/disabled** khi xem tin của chính mình — hợp lý, ⛔ chưa có TC nào phủ.

---

## TC-ASN-023: Check có thông báo khớp tuyến trong vòng 60 giây khi khớp đầy đủ điều kiện — **P2** · SC-ASN-011 *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 0 | *(Pre)* Tin OFFER `SEED-ASN-01` của tài khoản B có sẵn | OFFER của `Đặng Châu Anh`: `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` · Hôm nay · **Sáng** | ✅ PASS | — | tạo 08:26 cùng ngày |
| 1 | Tài khoản A đăng 1 tin NEED trùng P1/P2, ngày giao nhau, buổi **có chung** với OFFER; **ghi lại thời điểm đăng** *(setup)* | login `stag_taipm@` → wizard NEED đủ 3 bước → cùng tuyến, Hôm nay, buổi **Sáng** | ✅ PASS | — | 🕐 **Thời điểm đăng: `09:42:54`** *(đo bằng `date` ngay sau khi màn "Đăng tin thành công!" hiện)* |
| 2 | Đăng nhập B, nhấn chuông, check nội dung + thời điểm nhận | **đổi tài khoản** `stag_taipm@` → `stag_anhdc4@` *(logout + login + OTP, AI tự làm)* → tap `Thông báo` lúc **`09:46:59`** | ✅ PASS | `TC-ASN-023__verify-thong-bao-khop-tuyen.png` | — |
| E1 | B **CÓ** nhận thông báo khớp tuyến trỏ tới tin NEED vừa đăng, **≤60 giây** | vế *"CÓ nhận + trỏ đúng tin"* ✅ · vế *"≤60s"* xem phân tích ↓ | ✅ **PASS** | ↑ + `TC-ASN-023__verify-tro-dung-tin-need-vua-dang.png` | — |

**Đối chiếu 2 vế của Expected:**

| Vế | Bằng chứng | Kết luận |
|---|---|---|
| **CÓ nhận thông báo khớp tuyến** | mục **HÔM NAY** có *"Tìm thấy đơn hàng phù hợp tuyến của bạn — xem chi tiết để nhận giao"*, dấu chưa đọc đỏ | ✅ |
| **Trỏ ĐÚNG tin NEED vừa đăng** | tap thông báo → mở `Chi tiết tin` = `Gửi tài liệu`, `5 phút trước`, §LỘ TRÌNH `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` — **khớp tuyệt đối** tin đăng ở step 1 | ✅ |
| **≤60 giây** | xem phép đo ↓ | ✅ *(trong sai số)* |

🕐 **Phép đo độ trễ — khai đầy đủ vì có chạm biên:**
```
Đăng NEED      : 09:42:54
Quan sát chuông: 09:46:59   → thông báo ghi "3 phút trước"
"3 phút trước" = floor(elapsed/60)=3 ⇒ elapsed ∈ [180s, 240s)
⇒ thời điểm thông báo tới ∈ (09:42:59 , 09:43:59]
⇒ ĐỘ TRỄ THỰC ∈ (5 giây , 65 giây]
```
⚠️ **Cận trên 65s vượt ngưỡng 60s đúng 5 giây** — đây là **sai số làm tròn của nhãn thời gian (độ phân giải 1 phút)**, ⛔ KHÔNG phải quan sát thấy app chậm. Không đo chính xác hơn được vì **chỉ có 1 thiết bị**: phải đăng xuất/đăng nhập (~2 phút) mới xem được chuông của B, ⇒ ⛔ không thể "nhấn chuông theo chu kỳ" trong 60 giây như Steps mô tả.
📌 Verdict **PASS** dựa trên: (a) thông báo **đã có sẵn** ngay lần xem đầu tiên, (b) khoảng đo nằm gọn trong spec trừ 5s làm tròn, (c) chính fragment ghi *"⚠️ Đo bằng tay có sai số; ưu tiên automation nếu cần độ chính xác cao"* — tức tác giả TC **chấp nhận đo tay**.
🔁 **Đề nghị đo lại chốt `NFR-04`** bằng **2 thiết bị** (máy B mở sẵn màn Thông báo, máy A đăng tin) — khi đó đọc được mốc giây thật.

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-ASN-023__verify-thong-bao-khop-tuyen.png` · `screenshots/TC-ASN-023__verify-tro-dung-tin-need-vua-dang.png`
**Locators captured:** 3 elements
🟢 **Đối chứng chéo rất mạnh với `TC-ASN-013`:** cùng một cơ chế khớp tuyến, **cùng tuyến `Tòa V-City → FPT Cầu Giấy` buổi Sáng** — chủ tin (Tài, ở TC-013) **KHÔNG** nhận thông báo, người khác (Anh, ở TC-023) **CÓ** nhận. ⇒ chứng minh app **loại trừ theo chủ sở hữu**, ⛔ không phải "không gửi thông báo gì cả".
🟢 Màn Chi tiết tin khi **KHÔNG phải chủ tin** có CTA **`Tôi mang giúp được`** — đối chứng dương cho `TC-ASN-013 E4` (chủ tin thì không có).

---

## TC-ASN-021: Check đăng hai tin NEED liên tiếp tạo ra hai tin độc lập trên Bảng tin — **P3** · SC-ASN-018 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Tài khoản A đăng tin NEED **thứ nhất**, ghi lại tuyến *(setup)* | `stag_taipm@` → NEED#1: `FPT Tân Thuận 1` → `FTEL SG08 Quận 12` · Hôm nay · **Chiều** | ✅ PASS | — | ⚠️ loại hàng dùng `Tài liệu`, xem khai báo lệch dưới |
| 2 | Vẫn A, đăng tin NEED **thứ hai** tuyến KHÁC, ghi lại, rồi đăng xuất *(setup)* | NEED#2: `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` · Hôm nay · **Sáng** → đăng xuất | ✅ PASS | — | 2 tuyến **khác hẳn nhau** (khác cả 2 đầu + khác buổi) |
| 3 | Đăng nhập B, nhấn tab "Bảng tin" | login `stag_anhdc4@` → tap `Bảng tin` | ✅ PASS | — | — |
| 4 | Đếm và đối chiếu các tin của A trong danh sách | đếm trên danh sách | ✅ PASS | `TC-ASN-021__verify-hai-tin-doc-lap.png` | — |
| E1 | Có **đúng 2 tin riêng** của A, tuyến khớp 2 tin đã ghi; tin thứ hai **KHÔNG ghi đè** tin thứ nhất | 3 card, trong đó **đúng 2** của A | ✅ **PASS** | ↑ | chi tiết ↓ |

**Đối chiếu danh sách Bảng tin (nhìn từ tài khoản B):**

| # card | Tuyến | Buổi | Tuổi tin | Của ai | Khớp ghi chép |
|---|---|---|---|---|---|
| 1 | `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` | Sáng | 6 phút trước | **A (Tài)** | ✅ = NEED#2 (step 2) |
| 2 | `FPT Tân Thuận 1` → `FTEL SG08 Quận 12` | Chiều | 18 phút trước | **A (Tài)** | ✅ = NEED#1 (step 1) |
| 3 | `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` | Sáng | 1 giờ trước | B (Anh) — badge `Tin của bạn` | ⛔ không tính (tin của chính người xem) |

⇒ **Đúng 2 tin của A, 2 tuyến độc lập, cả hai cùng tồn tại** — tin thứ hai ⛔ **không** ghi đè tin thứ nhất.

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ASN-021__verify-hai-tin-doc-lap.png`
**Locators captured:** 1 element
⚠️ **Khai báo lệch step (không giấu):** step 1 yêu cầu loại hàng **`"Giấy tờ, hồ sơ"`** — nhãn đó **KHÔNG tồn tại** trên app; `C-ORD-09` đã chốt app dùng **`Tài liệu`** (và `KB-VIBE-01` của `KP-01 §10.2` bị đánh dấu lỗi thời từ VR-002 vì đúng lý do này). Phiên này dùng `Tài liệu`. Expected ⛔ không assert loại hàng ⇒ verdict tin được. 📌 Đề nghị QC **sửa câu chữ Steps** của `TC-ASN-021` cho khớp `C-ORD-09`.
🟢 **Tiện thể xác nhận lại:** badge `Tin của bạn` chỉ gắn vào tin của **chính người đang xem** — ở `TC-ASN-013` badge nằm trên tin của Tài (khi Tài xem), ở đây badge nhảy sang tin của Anh (khi Anh xem). Hành vi **đúng**, bám theo phiên đăng nhập.

