# Vibe Test Log — VR-009 — v1.1 — 2026-09-19

> Module: ASN · Platform: mobile (Appium MCP, UiAutomator2) · App: `com.hrisproject.stag` (host FoxPro_Stag, FoxEco = SDK nhúng)
> Env: STG · Evidence dir: `screenshots/` · Device: emulator-5554 (720×1280)
> Phiên: 2026-09-19 (khởi tạo)
> Tập chạy: **pending 16 TC** (Step 1.2 — QC chọn "chỉ TC còn nợ" 2026-09-19).
> QC chốt thêm: **006/008/019 giữ ⏳ NOT_RUN** (chặn hạ tầng: 2–3 thiết bị · cần dev lùi ngày) ⇒ mục tiêu phiên = **13 TC**.

## 🔴 PHÁT HIỆN CHẶN LÔ 1 — thông báo khớp tuyến ĐÃ BIẾN MẤT khi khung giờ trôi qua

> Ghi ở đây vì nó **thay đổi kế hoạch lô**, không phải verdict của TC nào.

| Mốc | Quan sát |
|---|---|
| 14:49 mở chuông lần đầu | `HÔM NAY` có **3** thông báo `Tìm thấy đơn hàng phù hợp tuyến của bạn` — `2 giờ trước` ×2 · `5 giờ trước` ×1 |
| 14:50 tap thông báo `.instance(0)` | mở **Chi tiết tin** `Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy · Hôm nay · Sáng · Phan Minh Tài` |
| 14:53 quay lại chuông | nhóm `HÔM NAY` **rỗng** — cả 3 thông báo biến mất |
| 14:56 `force-stop` + relaunch app, mở chuông lại | nhóm `HÔM NAY` **vẫn rỗng** ⇒ ⛔ không phải lỗi refresh client (T-ASN-04), mà là **trạng thái thật** |

**Giả thuyết (⛔ CHƯA kiểm chứng, không dùng làm verdict):** thông báo gợi ý khớp tuyến **hết hiệu lực khi khung giờ khớp trôi qua**.
Mọi seed S1–S4 + tin VR-007 đều là buổi `Sáng (8–12h)`; lúc quan sát là **14:49** ⇒ đã ngoài khung.

**Hệ quả lên scope:** `TC-ASN-010/011/012/022` đều verify **trên màn Thông báo**. Khẳng định "không có thông báo"
lúc này là **vô nghĩa** vì *mọi* thông báo khớp tuyến đều đã mất, kể cả của `SEED S1` là ca khớp ĐỦ điều kiện
(chứng cứ dương đối chứng). ⇒ ⛔ **KHÔNG khai PASS cho 011/012/022** dù bề mặt "đúng như expected" —
đó sẽ là PASS giả do mất đối chứng, đúng kiểu suy diễn mà `SKILL.md §SCOPE` cấm.

⇒ 4 TC này cần **seed lại trên khung giờ CÒN MỞ** (`Chiều 13–17h`) mới chạy được. Xem mục Handoff ở `vibe-report.md`.

**Evidence (recon, không thuộc TC nào):** `screenshots/_recon__bell-inventory.png` · `_recon__notif0-detail.png` · `_recon__notif0-top.png` · `_recon__notif0-mid.png` · `_recon__notif0-between.png` · `_recon__notif0-ghichu.png` · `_recon__after-back.png` · `_recon__bell-top2.png` · `_recon__bell-fresh.png` · `_recon__after-restart.png` · `_recon__foxeco-home.png` · `_recon__bell-restored.png`

## 📋 Kiểm kê Bảng tin của tài khoản B (`stag_anhdc4@`) lúc 14:54 — dùng để định danh seed

> Chi tiết tin **KHÔNG có mục GHI CHÚ** ⇒ ⛔ mẹo "đọc mã `SEED Sx` trong Ghi chú" của VR-008 **không dùng được ở màn này**.
> Thay bằng **chữ ký tuyến + khung giờ** trên card Bảng tin — phân biệt được S2/S3/S4 vì mỗi seed lệch đúng 1 chiều.

| # | Tuyến | Khung giờ | Đăng | Là seed nào |
|--:|---|---|---|---|
| 1 | V-City → FPT Cầu Giấy | **22/09/2026 · Giờ nào cũng được** | 2 giờ trước | **S3** (lệch ngày) |
| 2 | V-City → FPT Cầu Giấy | **Hôm nay · Sau giờ làm** | 2 giờ trước | **S4** (lệch buổi) |
| 3 | V-City → **FPT Tân Thuận 1** | Hôm nay · Sáng | 2 giờ trước | **S2** (lệch điểm giao) |
| 4 | V-City → FPT Cầu Giấy | Hôm nay · Sáng | 2 giờ trước | **S1** (khớp đủ) |
| 5 | V-City → FPT Cầu Giấy | Hôm nay · Sáng | 5 giờ trước | tin VR-007 (Phan Minh Tài) |
| 6 | V-City → FPT Cầu Giấy | Hôm nay · Sáng | 6 giờ trước | **`Tin của bạn`** — NEED của chính B |

**Evidence:** `screenshots/_recon__bangtin-inventory.png` · `_recon__bangtin-inventory2.png`

---

## TC-ASN-005: Check người ngoài cặp ghép không thấy SĐT của hai bên trong cặp

> Tài khoản D = `stag_giangdc2@fpt.com` (**Đặng Châu Giang**) — ⛔ không thuộc cặp ghép.
> Cặp ghép đang xét = **Tin 2**: chủ tin A `stag_taipm@` · vận chuyển B `stag_anhdc4@` · người nhận C `stag_huyennhk@`,
> tuyến `FPT Tân Thuận 1 → FTEL SG08 Quận 12` · Chiều · trạng thái `Đã ghép` (tiền đề do VR-008 tạo).
> 🔑 **Oracle định danh tin**: chuỗi `FTEL SG08` — ⛔ không tin nào khác trên STG dùng điểm giao này.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) A đăng tin NEED khai C là người nhận | — | ✅ PASS | — | có sẵn từ VR-008, ⛔ không seed lại |
| 2 | (setup) B nhận đơn + xác nhận | — | ✅ PASS | — | có sẵn từ VR-008 (`TC-ASN-001`) |
| 3 | (setup) Đăng nhập tài khoản D | logout B → email `stag_giangdc2@` → `NHẬN MÃ OTP` → OTP → `ĐĂNG NHẬP` | ✅ PASS | `_setup__login-d-landing.png` | ⚠️ lần bấm `NHẬN MÃ OTP` **đầu** trả *"Không thể kết nối mạng!"*; bấm lại lần 2 OK (xem T-ASN-07) |
| 4 | Nhấn tab "Bảng tin" và tìm tin đó | `scroll_to_element textContains("FTEL SG08")` trên toàn danh sách | ✅ PASS | `TC-ASN-005__verify-bangtin-khong-co-tin-da-ghep.png` | 🚫 **NOT FOUND** — cuộn hết danh sách vẫn không có. Feed **có tải dữ liệu** (thấy S3/S4/S2) ⇒ ⛔ không phải empty state giả |
| 5 | Nhấn tab "Hoạt động", tìm đơn ở **cả hai** tab con | `Đang diễn ra`: scroll_to `textContains("FTEL SG08")` → 🚫 NOT FOUND (10 nhịp cuộn)<br>`Đã hoàn thành`: 🚫 NOT FOUND (10 nhịp cuộn) | ✅ PASS | `TC-ASN-005__verify-hoatdong-khong-co-don-cap-ghep.png` | D **có** đơn riêng trong tab này (`Gửi:`/`Nhận:`/`Nhận giao hàng`) ⇒ tab hoạt động bình thường, ⛔ không phải rỗng |
| E5 | Không có bề mặt nào cho D thấy SĐT của A hoặc B | find `textContains("0833329408")` *(SĐT của A)* → 🚫 NOT FOUND<br>find `textContains("0343439724")` *(SĐT của B)* → 🚫 NOT FOUND | ✅ PASS | `TC-ASN-005__verify-hoatdong-khong-co-don-cap-ghep.png` | 🔑 2 phép find **phủ định trên toàn cây** — đây là chứng cứ trực tiếp cho mệnh đề "không lộ SĐT", ⛔ không suy từ việc đơn vắng mặt |

**Result: ✅ PASS (5 steps, 1 expected)**
**Evidence:** `screenshots/TC-ASN-005__verify-bangtin-khong-co-tin-da-ghep.png` + `screenshots/TC-ASN-005__verify-hoatdong-khong-co-don-cap-ghep.png` — verified tồn tại
**Locators captured:** 0 mới (dùng lại map VR-007/008) · 4 phép find phủ định

---

## TC-ASN-007: Check tin đã ghép biến mất khỏi Bảng tin và khỏi luồng gợi ý của Carrier khác

> Vai "tài khoản C" (người thứ 3, ⛔ ngoài cặp ghép) do **`stag_giangdc2@`** đảm nhiệm — cùng phiên đăng nhập với `TC-ASN-005`.
> Tin đang xét = **Tin 2** (`FPT Tân Thuận 1 → FTEL SG08 Quận 12`, trạng thái `Đã ghép`). Oracle định danh: chuỗi `FTEL SG08`.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1–3 | (setup) A đăng tin · B nhận đơn · đăng nhập C | — | ✅ PASS | `_setup__login-d-landing.png` | tiền đề VR-008, ⛔ không seed lại |
| 4 | Nhấn tab "Bảng tin" và tìm tin đó trong danh sách | `scroll_to_element textContains("FTEL SG08")` → cuộn hết danh sách | ✅ PASS | `TC-ASN-007__verify-bangtin-vang-tin-da-ghep.png` | 🚫 **NOT FOUND** — tin `Đã ghép` ⛔ không còn trên Bảng tin của người thứ 3 |
| 5 | (setup) Nhấn icon chuông | `accessibility id "Thông báo"` trên Trang chủ → tap | ✅ PASS | — | ⚠️ chuông **chỉ có ở Trang chủ** ⇒ phải về `Trang chủ` trước |
| E6 | Danh sách thông báo KHÔNG có gợi ý nào trỏ tới tin đó | find `textContains("Tìm thấy đơn hàng phù hợp tuyến")` trên toàn cây | ✅ PASS | `TC-ASN-007__verify-chuong-khong-co-goi-y.png` | 🚫 **NOT FOUND** — ⛔ không có thông báo khớp tuyến nào. Danh sách **có** dữ liệu khác (`Tin của bạn đã quá hạn` · `Đã có người nhận mang giúp đơn của bạn` · `Đơn đã bị huỷ` · `Đơn gửi tới bạn đã có người vận chuyển`) ⇒ màn tải bình thường, ⛔ không phải empty state giả |

**Result: ✅ PASS (5 steps, 1 expected)**
**Evidence:** `screenshots/TC-ASN-007__verify-bangtin-vang-tin-da-ghep.png` + `screenshots/TC-ASN-007__verify-chuong-khong-co-goi-y.png` — verified tồn tại

> ⚖️ **Giới hạn của phép thử, khai để người đọc tự cân nhắc:** tài khoản `stag_giangdc2@` **không sở hữu tin OFFER nào trên tuyến đó**,
> nên về nguyên tắc nó sẽ không nhận gợi ý khớp tuyến **dù tin có còn sống hay không**. Phép thử vì vậy chứng minh đúng **mệnh đề của TC**
> (*danh sách thông báo không có gợi ý trỏ tới tin đã ghép*) nhưng **chưa cô lập được** nguyên nhân là "tin đã ghép nên bị loại khỏi luồng gợi ý".
> 🔁 Muốn chặt hơn: dùng Carrier **có OFFER trùng tuyến** với tin đó rồi mới kiểm — ghi vào khuyến nghị `vibe-report.md`.

---

## TC-ASN-020: Check Carrier huỷ nhận đơn trước khi lấy hàng thì tin trở lại Bảng tin và Carrier khác ghép được

> 🔗 **TC chạy 2 chặng / 2 phiên.** Chặng **step 1–5** đã PASS ở **VR-008** (B nhận đơn → huỷ + lý do → tin trở lại Bảng tin,
> xác nhận cả 2 phía). Phiên này chạy nốt **step 6–9** bằng **Carrier thứ 3** ⇒ **chốt verdict cuối cho TC**.
> Tin dùng: **Tin 1** `Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy · Hôm nay · Sáng`, chủ tin `stag_taipm@`, đăng ~09:43.
> 🔑 **Cách định danh đúng tin giữa 3 card trùng tuyến + trùng buổi:** nhãn tuổi tin trên card = **`5 giờ trước`**
> (S1 = `2 giờ trước` · tin của B = `6 giờ trước`). Chi tiết tin cũng in `5 giờ trước` ở header ⇒ đối chiếu được 2 lần.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1–5 | (đã chạy ở VR-008) A đăng tin · B nhận · B huỷ + lý do · đơn về `Chờ ghép` | — | ✅ PASS | ⛔ **không thuộc run này** — evidence nằm trong run folder `VR-008-ASN-2026-09-19/screenshots/` (2 ảnh `…__verify-tin-tro-lai-bang-tin` và `…__verify-chu-tin-thay-cho-ghep`) | ⛔ không chạy lại. ⚠️ Cố ý **không trích tên file kèm đuôi** ở đây: ảnh của phiên khác, trích như evidence của VR-009 sẽ thành link chết khi audit run này |
| 6 | (setup) Đăng nhập bằng tài khoản C | `stag_giangdc2@` (**Đặng Châu Giang**) — ⛔ khác `taipm` (chủ tin) và khác `anhdc4` (carrier đã huỷ) | ✅ PASS | `_setup__login-d-landing.png` | đúng yêu cầu "Carrier **khác**" |
| 7 | Nhấn tab "Bảng tin" và tìm tin đó | `scroll_to_element text("5 giờ trước")` → thấy card `V-City → FPT Cầu Giấy · Hôm nay · Sáng` | ✅ PASS | `TC-ASN-020__pre-tin-cho-ghep-tren-bang-tin.png` | **E7 ✓** tin hiển thị **lại** trên Bảng tin của tài khoản C sau khi bị huỷ nhận |
| 8 | Nhấn tin đó | tap `text("5 giờ trước")` → mở `Chi tiết tin`, header `5 giờ trước · Gửi tài liệu` | ✅ PASS | — | CTA `Tôi mang giúp được` **có mặt** ⇒ tin đang ở `Chờ ghép`, ⛔ chưa ai ghép |
| 9 | Nhấn "Tôi mang giúp được" rồi "Xác nhận" | find+tap `textContains("Tôi mang giúp được")` → find+tap `text("Xác nhận")` | ✅ PASS | — | — |
| E9a | Tài khoản C ghép được đơn | mở thẳng màn **`Theo dõi đơn`**; stepper sáng tới mốc `Lấy hàng`; CTA = `Tôi đã lấy hàng` + `Huỷ nhận đơn` (bộ CTA của **vai carrier**) | ✅ PASS | `TC-ASN-020__verify-carrier-thu-3-ghep-duoc.png` | tuyến trên màn khớp `Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy` |
| E9b | Đơn chuyển sang "Đã ghép" với **C là người vận chuyển** | màn `Hoạt động` của C: card đầu `Giao: Tài liệu \| Giá trị thấp` + badge **`Đã ghép`**; `get_text` trả đúng chuỗi `Giao: Tài liệu \| Giá trị thấp` | ✅ PASS | `TC-ASN-020__verify-vai-carrier-tren-hoat-dong.png` | 🔑 dùng **oracle phân vai của VR-008**: tiền tố `Giao:` = mình vận chuyển. Card `Gửi:` ngay dưới là đơn **riêng** của C, ⛔ không phải đơn đang xét |

**Result: ✅ PASS (9 steps, 3 expected) — verdict cuối, TC đã đủ 2 chặng**
**Evidence:** `screenshots/TC-ASN-020__verify-carrier-thu-3-ghep-duoc.png` + `screenshots/TC-ASN-020__verify-vai-carrier-tren-hoat-dong.png` (+ `TC-ASN-020__pre-tin-cho-ghep-tren-bang-tin.png`) — verified tồn tại
**Locators captured:** 0 mới (dùng lại map VR-007/008)

> 🗂️ **Dữ liệu STG thay đổi bởi step 9:** Tin 1 nay `Đã ghép`, người vận chuyển = **`stag_giangdc2@`**.
> ⚠️ Phiên sau đừng coi Tin 1 là tin `Chờ ghép` nữa.

---

## 🌱 SEED LÔ 2 — dựng lại bề mặt thông báo trên khung giờ CÒN MỞ

> Vì sao phải seed lại: xem callout 🔴 đầu file — mọi thông báo khớp tuyến của khung `Sáng` đã biến mất lúc 14:49.
> Thiết kế: **1 OFFER + 4 NEED**, mỗi NEED lệch **đúng 1 chiều** so với OFFER ⇒ mỗi TC âm có biến độc lập, và **N1 là chứng cứ DƯƠNG đối chứng**.

| Seed | Tài khoản | Tuyến | Ngày | Buổi | Vai trò | Giờ đăng |
|---|---|---|---|---|---|---|
| **OFFER-C1** | **D** `stag_giangdc2@` | `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` | Hôm nay | **Chiều (13–17h)** | tuyến nhận thông báo | 15:14 |
| **N1** | B `stag_anhdc4@` | V-City → FPT Cầu Giấy | Hôm nay | **Chiều** | ✅ khớp ĐỦ → chứng cứ **dương** | 15:22 |
| **N2** | B | V-City → FPT Cầu Giấy | Hôm nay | **Sau giờ làm** | lệch **buổi** → `TC-ASN-022` | 15:26 |
| **N3** | B | V-City → **FPT Tân Thuận 1** | Hôm nay | Chiều | lệch **điểm giao** → `TC-ASN-011` | 15:31 |
| **N4** | B | V-City → FPT Cầu Giấy | **22/09/2026** | Chiều | lệch **ngày** → `TC-ASN-012` | 15:35 |

**Kết quả đọc chuông của D lúc 15:37** *(sau khi cả 4 NEED đã đăng xong)*:
`HÔM NAY` có **ĐÚNG 1** thông báo `Tìm thấy đơn hàng phù hợp tuyến của bạn` — nhãn **`14 phút trước`** (≈15:23 ⇒ **N1**).
Phép đếm bằng MCP: `...instance(0)` ✅ tìm thấy · `...instance(1)` 🚫 **NOT FOUND** ⇒ **đúng 1 thông báo**, ⛔ không phải "nhìn ảnh đoán".

🔑 **Chính vì N1 SINH thông báo trong cùng bài test**, việc N2/N3/N4 **không** sinh thông báo mới là chứng cứ có giá trị —
⛔ không rơi vào bẫy "không có thông báo nào cả nên TC nào cũng "đạt"" như tình huống 14:49.

**Evidence chung:** `screenshots/_setup__offer-c1-posted.png` · `_recon__bell-d-after-seeds.png` · `_recon__need-n1-step2-filled.png` · `_recon__need-n2-step2-filled.png` · `_recon__need-n3-step2-filled.png` · `_recon__need-n4-datepicker.png` · `_recon__offer-form-d.png` · `_recon__offer-form-filled.png` · `_recon__photo-picker.png` · `_recon__need-step2-recipient.png` · `_setup__login-b-landing.png` · `_recon__canhan-check.png`

---

## TC-ASN-010: Check nhấn "Nhận giao" ở tin khớp tuyến ghép đơn và mở màn Theo dõi đơn

> Vai: **B** đăng OFFER / **A** đăng NEED theo Steps ⇒ ánh xạ thực tế: **D `stag_giangdc2@` = chủ OFFER (carrier)** · **B `stag_anhdc4@` = chủ tin NEED**.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) Đăng nhập B, đăng 1 tin OFFER, đăng xuất | D đăng `OFFER-C1` (V-City → FPT Cầu Giấy · Hôm nay · Chiều) | ✅ PASS | `_setup__offer-c1-posted.png` | màn thành công OFFER: *"Đã ghi nhận tuyến đường!"* |
| 2 | (setup) Đăng nhập A, đăng 1 tin NEED trùng 2 điểm và giao khung giờ, đăng xuất | B đăng **N1** trùng **cả 2 điểm + ngày + buổi** | ✅ PASS | `_recon__need-n1-step2-filled.png` | ảnh đã gắn (`1/5` assert), 2 địa chỉ đều chọn từ gợi ý |
| 3 | (setup) Đăng nhập B, nhấn chuông và nhấn thông báo khớp tuyến để mở Chi tiết tin | tap `accessibility id "Thông báo"` → tap `textContains("Tìm thấy đơn hàng phù hợp tuyến…").instance(0)` | ✅ PASS | `TC-ASN-010__pre-chi-tiet-tin-mo-tu-thong-bao.png` | mở đúng tin: header `19 phút trước` (≈15:23 = N1) + **ảnh xanh lá** đúng ảnh seed ⇒ 2 dấu hiệu định danh độc lập |
| 4 | Nhấn nút "Nhận giao" | ⚠️ nhãn thật = **`Tôi mang giúp được`**; find `textContains("Nhận giao")` → 🚫 **NOT FOUND** | ✅ PASS *(có sai lệch tài liệu)* | — | 🔴 **Steps sai nhãn** — xem mục Sai lệch bên dưới. Đã bấm đúng CTA thật rồi `Xác nhận` |
| E4 | Mở màn Theo dõi đơn với trạng thái "Đã ghép" | màn **`Theo dõi đơn`** mở ngay; CTA = `Tôi đã lấy hàng` + `Huỷ nhận đơn` (bộ CTA **vai carrier** ⇒ đã ghép) | ✅ PASS | `TC-ASN-010__verify-theo-doi-don-va-sdt-nguoi-gui.png` | tuyến trên màn khớp `Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy` |
| E5 | Cụm liên hệ hiển thị số điện thoại của người gửi | §NGƯỜI GỬI: **Đặng Châu Anh** · **`0343439724`** · `stag_anhdc4@fpt.com`, nút **`Gọi`** bật | ✅ PASS | `TC-ASN-010__verify-theo-doi-don-va-sdt-nguoi-gui.png` | `scroll_to_element text("0343439724")` ✅ tìm thấy ⇒ MCP-verified, ⛔ không đọc từ ảnh |

**Result: ✅ PASS (5 steps, 2 expected)**
**Evidence:** `screenshots/TC-ASN-010__verify-theo-doi-don-va-sdt-nguoi-gui.png` (+ `TC-ASN-010__pre-chi-tiet-tin-mo-tu-thong-bao.png`) — verified tồn tại

> 🔴 **SAI LỆCH TÀI LIỆU ↔ APP (cần QC/BA quyết):** `TC-ASN-010` Steps 4 ghi nút **`"Nhận giao"`**, nhưng trên app nút đó **không tồn tại**
> (`find textContains("Nhận giao")` 🚫 NOT FOUND); CTA thật là **`Tôi mang giúp được`** — *cùng* nút với luồng vào từ Bảng tin.
> Đây là điều `coverage-ASN.md` đã nghi từ VR-008 và nay **đã kiểm chứng thật**. ⇒ Đề nghị sửa Steps của `TC-ASN-010`.
> ⚠️ ⛔ **Không hạ FAIL**: hành vi nghiệp vụ (ghép đơn từ thông báo → Theo dõi đơn → lộ SĐT người gửi) **đúng hoàn toàn**; chỉ sai *câu chữ* trong TC.

---

## TC-ASN-011: Check không có thông báo khớp tuyến khi tin NEED lệch điểm giao hàng

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) B đăng OFFER với điểm lấy/giao xác định | `OFFER-C1` V-City → **FPT Cầu Giấy** · Chiều | ✅ PASS | `_setup__offer-c1-posted.png` | — |
| 2 | (setup) A đăng NEED **trùng điểm lấy** nhưng **điểm giao là văn phòng khác** | **N3**: V-City *(trùng)* → **FPT Tân Thuận 1** *(khác)* · cùng ngày · cùng buổi Chiều | ✅ PASS | `TC-ASN-011__pre-seed-n3-lech-diem-giao-tren-bang-tin.png` | 🔑 chỉ lệch **1 biến** = điểm giao. Card trên Bảng tin xác nhận tin **sống thật** |
| 3–4 | (setup) Đăng nhập B, nhấn icon chuông | login `stag_giangdc2@` → Trang chủ → `accessibility id "Thông báo"` | ✅ PASS | — | — |
| E5 | KHÔNG có thông báo khớp tuyến nào trỏ tới tin NEED ở bước 2 | `...instance(1)` 🚫 **NOT FOUND** ⇒ toàn danh sách chỉ có **1** thông báo khớp tuyến, và nó là **N1** (`14 phút trước`), ⛔ không phải N3 | ✅ PASS | `TC-ASN-011__verify-chuong-khong-co-tb-cho-seed-lech-diem-giao.png` | ✅ **Có đối chứng dương**: N1 cùng lô vẫn sinh thông báo ⇒ cơ chế đang chạy, việc N3 không sinh là **do lệch điểm giao**, ⛔ không phải do hệ thống im lặng |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ASN-011__verify-chuong-khong-co-tb-cho-seed-lech-diem-giao.png` (+ `TC-ASN-011__pre-seed-n3-lech-diem-giao-tren-bang-tin.png`) — verified tồn tại

---

## TC-ASN-012: Check không có thông báo khớp tuyến khi khoảng ngày không giao nhau

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) B đăng OFFER | `OFFER-C1` · khoảng ngày **Hôm nay–Hôm nay** · Chiều | ✅ PASS | `_setup__offer-c1-posted.png` | — |
| 2 | (setup) A đăng NEED trùng 2 điểm nhưng **khoảng ngày tách rời** | **N4**: V-City → FPT Cầu Giấy *(trùng cả 2 điểm)* · **22/09/2026–22/09/2026** · Chiều | ✅ PASS | `TC-ASN-012__pre-seed-n4-lech-ngay-tren-bang-tin.png` | 🔑 chỉ lệch **1 biến** = khoảng ngày (cách hôm nay 3 ngày, ⛔ không giao nhau). ⚠️ chọn `Từ ngày` thì `Đến ngày` **tự nhảy theo** |
| 3–4 | (setup) Đăng nhập B, nhấn icon chuông | như trên | ✅ PASS | — | — |
| E5 | KHÔNG có thông báo khớp tuyến nào trỏ tới tin NEED ở bước 2 | `...instance(1)` 🚫 **NOT FOUND** ⇒ chỉ **1** thông báo khớp tuyến và nó là **N1**, ⛔ không phải N4 | ✅ PASS | `TC-ASN-012__verify-chuong-khong-co-tb-cho-seed-lech-ngay.png` | ✅ có đối chứng dương N1 cùng lô |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ASN-012__verify-chuong-khong-co-tb-cho-seed-lech-ngay.png` (+ `TC-ASN-012__pre-seed-n4-lech-ngay-tren-bang-tin.png`) — verified tồn tại

> ℹ️ **Ghi chú tài liệu:** Steps bản v1.0 mô tả lệch giờ dạng `08:00–09:00` vs `20:00–21:00`. App **không** cho nhập giờ tự do
> mà dùng **khoảng NGÀY + tập BUỔI** ⇒ đã hiện thực hoá đúng *ý định* của TC (hai khoảng thời gian tách rời hoàn toàn) bằng **khoảng ngày**.
> Nhánh "lệch buổi trong cùng ngày" được phủ riêng ở `TC-ASN-022`.

---

## TC-ASN-022: Check không có thông báo khớp tuyến khi ngày giao nhau nhưng buổi không chung

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) A đăng NEED trùng P1/P2, **ngày CÓ giao nhau**, nhưng chỉ chọn buổi `Sau giờ làm` | **N2**: V-City → FPT Cầu Giấy *(trùng 2 điểm)* · **Hôm nay** *(trùng ngày)* · **`Sau giờ làm (17–19h)`** | ✅ PASS | `TC-ASN-022__pre-seed-n2-lech-buoi-tren-bang-tin.png` | 🔑 chỉ lệch **1 biến** = buổi. OFFER-C1 chỉ chọn `Chiều` ⇒ **không có buổi chung**, và ⛔ không chọn `Giờ nào cũng được` đúng như TC dặn |
| 2 | Đăng nhập B, nhấn icon chuông, check danh sách thông báo | login `stag_giangdc2@` → chuông → đếm bằng MCP | ✅ PASS | — | — |
| E2 | KHÔNG có thông báo khớp tuyến nào trỏ tới tin NEED vừa đăng | `...instance(1)` 🚫 **NOT FOUND** ⇒ chỉ **1** thông báo khớp tuyến và nó là **N1** (buổi `Chiều`), ⛔ không phải N2 | ✅ PASS | `TC-ASN-022__verify-chuong-khong-co-tb-cho-seed-lech-buoi.png` | ✅ có đối chứng dương N1 cùng lô ⇒ chứng minh **BR lọc theo buổi** hoạt động đúng |

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-ASN-022__verify-chuong-khong-co-tb-cho-seed-lech-buoi.png` (+ `TC-ASN-022__pre-seed-n2-lech-buoi-tren-bang-tin.png`) — verified tồn tại

> 🧪 **3 ảnh `__verify` của `011`/`012`/`022` là 3 lần quan sát ĐỘC LẬP** (mỗi lần rời màn → mở lại chuông), md5 khác nhau —
> ⛔ không phải 1 ảnh nhân bản 3 tên (điều `SKILL.md §Retention` cấm).

---

## 🔎 Quan sát bổ sung (⛔ KHÔNG phải verdict TC) — thông báo SỐNG SÓT sau khi tin được ghép

Sau khi `TC-ASN-010` ghép **N1**, mở lại chuông của D lúc 15:46: thông báo khớp tuyến của N1 **VẪN CÒN**
(`19 phút trước`), chỉ **đổi sang trạng thái đã đọc** (mất chấm đỏ + mất vạch cam bên trái).

**Vì sao đáng ghi:**
1. ⇒ **Bác bỏ** giả thuyết *"thông báo biến mất vì bị tap"* — lúc 14:49 tôi chỉ tap **1** thông báo mà **cả 3** biến mất.
   ⇒ Củng cố giả thuyết còn lại: **thông báo hết hiệu lực khi khung giờ khớp trôi qua** (3 tin kia đều buổi `Sáng`, quan sát lúc 14:49).
   ⚠️ Vẫn là **giả thuyết** — muốn chốt phải quan sát mốc 17:00 (khi `Chiều` đóng) xem 1 thông báo của N1 có tự mất không.
2. ⇒ **Ràng buộc thiết kế cho nhóm đếm `014/015/016/017/025`:** tin đã ghép **vẫn chiếm 1 slot** trong danh sách thông báo.
   Do đó ⛔ **không được tái dùng `OFFER-C1`** để đếm (nó đã dính 1 thông báo của tin đã ghép) — phiên sau phải seed **tuyến OFFER MỚI, sạch**.

**Evidence:** `screenshots/_recon__bell-after-ghep-n1.png` · `_recon__state-check.png`

---

## ⏹️ DỪNG PHIÊN — còn nợ 9 TC (khai đầy đủ, ⛔ không làm tròn)

| Nhóm còn nợ | TC | Lý do |
|---|---|---|
| **Trần & thứ tự gợi ý** | `014` `015` `016` `017` `018` `025` | **Hết sức phiên.** Cần **tuyến OFFER MỚI sạch + 3–6 tin NEED** và **3 lượt đổi tài khoản** để đếm mốc 3 → 5 → 6 (~50–60 phút). Khung `Chiều` đóng lúc **17:00**, thời điểm dừng là **15:46** ⇒ ⛔ không đủ để chạy TRỌN VẸN; chạy dở sẽ đẻ seed hỏng và số đếm nhiễm bẩn (xem ràng buộc thiết kế ở mục trên) |
| **Cần 2–3 thiết bị** | `006` (2 máy, bấm cách <2s) · `008` (3 máy, đo ≤5s) | Máy chỉ có **1 AVD `qa_a33`**. **QC chốt 2026-09-19** trong phiên này: giữ `⏳ NOT_RUN`, ⛔ không đầu tư nhân bản AVD |
| **Cần dev lùi ngày** | `019` | Cần tin NEED trạng thái **Hết hạn** — ⛔ không tạo được qua UI |

⛔ **KHÔNG** hạ 6 TC nhóm đếm thành `BLOCKED`/`N-A`: chúng **không bị chặn kỹ thuật**, chỉ là chưa đủ thời gian ⇒ đúng nghĩa `⏳ NOT_RUN`.
