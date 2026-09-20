# Vibe Test Log — VR-010 — v1.1 — 2026-09-19

> Module: ASN · Platform: mobile (Appium MCP · emulator-5554) · Env: STG — host app FoxPro `com.hrisproject.stag` · Evidence dir: `screenshots/`
> Phiên: 2026-09-19 (khởi tạo 16:27)
> Tập chạy: **pending 7 TC** — `014` `015` `016` `017` `018` `025` `019` (theo lựa chọn QC ở Step 1.2).
> 🔴 `TC-ASN-006`/`008` QC **để lại** (cần 2–3 thiết bị) — xem `scope-ledger.md`.
> ⚠️ Evidence chụp bằng `adb exec-out screencap -p` (giữ nguyên lý do VR-008/009: `appium_screenshot` trả ~150k ký tự HTML viewer vào context). `SKILL.md` cho phép `adb screencap` cho vai trò **evidence**.

## 🌱 Kế hoạch seed của phiên (đọc trước khi đọc kết quả TC)

Nhóm trần & thứ tự gợi ý bắt buộc phải **đếm thông báo trên tài khoản chủ tin OFFER**, nên thiết kế:

| Vai | Tài khoản | Việc |
|---|---|---|
| **B** — chủ tin OFFER, người ĐẾM thông báo | `stag_giangdc2@` *(Đặng Châu Giang — đang đăng nhập sẵn)* | đăng OFFER `R1`,`R2`; đếm chuông 3 mốc |
| **A** — người đăng NEED | `stag_anhdc4@` *(Đặng Châu Anh)* | đăng 6 tin NEED khớp `R1` + 1 tin khớp `R2` |
| **người nhận** của các tin NEED | `stag_taipm@` *(Phan Minh Tài, SĐT HRIS `0833329408`)* | chỉ là dữ liệu form |

**Tuyến chọn** *(⛔ tránh trùng `OFFER-C1` V-City→Cầu Giấy Chiều của chính B — đã nhiễm 1 thông báo cũ)*:
- `R1` = **`FPT Cầu Giấy` → `Tòa V-City, Lê Thái Tổ`** (chiều ngược `OFFER-C1`) — dùng cho `015/016/017/014`
- `R2` = **`FPT Tân Thuận 1` → `FTEL SG08 Quận 12`** — dùng cho `025`
- `R3` = **`FTEL SG08 Quận 12` → `FPT Tân Thuận 1`**, chủ tin là `stag_huyennhk@` *(chuông sạch)* — dùng cho `018`

🔴 **Buổi = `Giờ nào cũng được` cho CẢ OFFER lẫn NEED** — cố ý, để né bẫy **`T-ASN-09`**
(VR-009 ghi: thông báo khớp tuyến **biến mất hàng loạt** khi khung giờ trôi qua). Lúc bắt đầu phiên là **16:29**,
khung `Chiều (13–17h)` chỉ còn ~30 phút ⇒ mọi phép ĐẾM sẽ vô nghĩa nếu seed vào khung sắp đóng.

## 🌱 SEED lượt 1 — tài khoản B `stag_giangdc2@` đăng 2 tin OFFER (16:29–16:37)

| Seed | Tuyến | Ngày | Buổi | Kết quả | Dùng cho |
|---|---|---|---|---|---|
| **`OFFER-R1`** | `FPT Cầu Giấy` → `Tòa V-City, Lê Thái Tổ` | Hôm nay–Hôm nay | **Giờ nào cũng được** | ✅ *"Đã ghi nhận tuyến đường!"* (16:34) | `TC-ASN-015/016/017/014` |
| **`OFFER-R2`** | `FPT Tân Thuận 1` → **`FTEL SG08 Gò Vấp`** | Hôm nay–Hôm nay | **Giờ nào cũng được** | ✅ *"Đã ghi nhận tuyến đường!"* (16:37) | `TC-ASN-025` |

**Evidence seed:** `screenshots/_setup__offer-r1-truoc-dang.png` · `screenshots/_setup__offer-r2-truoc-dang.png`

⚠️ **Ghi chú tuyến `R2`:** gõ `FTEL SG08` thì gợi ý-0 trả về **`FTEL SG08 Gò Vấp`**, ⛔ KHÔNG phải `FTEL SG08 Quận 12`
như các phiên trước. ⇒ tin NEED của `R2` phải gõ **đủ chuỗi `FTEL SG08 Gò Vấp`**, nếu không sẽ lệch điểm giao và không khớp.

### 📏 Mốc đo BASELINE của chuông B (đo TRƯỚC khi seed NEED — 16:28)

| Phép đo MCP | Kết quả |
|---|---|
| `…textContains("Tìm thấy đơn hàng phù hợp tuyến của bạn — xem chi tiết").instance(0)` | ✅ tìm thấy |
| `scroll_to_element` cùng chuỗi `.instance(1)`, 8 nhịp cuộn | 🚫 **NOT FOUND** |

⇒ **BASELINE = đúng 1 thông báo khớp tuyến** (của `OFFER-C1` tồn dư từ VR-009).
🔑 Mọi phép đếm bên dưới đều là **`instance(k)` tuyệt đối trên cả danh sách**, nên số kỳ vọng = **BASELINE + số tin NEED khớp**.

## 🌱 SEED lượt 2 — tài khoản A `stag_anhdc4@` đăng 3 tin NEED khớp `R1` (16:39–16:53)

Mọi tin giống hệt nhau trừ mã seed ở ô **GHI CHÚ**: `Tài liệu · Thấp · Dưới 5 kg · Nhỏ` · 1 ảnh (xanh lá) ·
lấy `FPT Cầu Giấy` → giao `Tòa V-City, Lê Thái Tổ` · **Hôm nay–Hôm nay** · **Giờ nào cũng được** ·
người nhận `stag_huyennhk@` *(autofill SĐT `0989014863` ĐÚNG — tái xác nhận `T-ASN-08`)*.

| Mã seed (ô Ghi chú) | Giờ đăng | Kết quả |
|---|---|---|
| `SEED R1-1` | 16:46 | ✅ *"Đăng tin thành công!"* |
| `SEED R1-2` | 16:50 | ✅ *"Đăng tin thành công!"* |
| `SEED R1-3` | 16:53 | ✅ *"Đăng tin thành công!"* |

**Evidence seed:** `screenshots/_setup__need-r1-1-truoc-dang.png` *(màn Bước 3/3 xác nhận — chứng minh đủ 4 chiều khớp `OFFER-R1`)*

---

## TC-ASN-015: Check tin OFFER có 3 tin NEED khớp nhận đủ 3 thông báo

> Scenario `SC-ASN-014` · P2 · Lô 1 · Tài khoản đếm: **B `stag_giangdc2@`** (chủ `OFFER-R1`)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | B đăng 1 tin OFFER tuyến/ngày/buổi xác định *(setup)* | form `Tôi nhận giao hàng` → `Đăng tin ngay` | ✅ PASS | `_setup__offer-r1-truoc-dang.png` | `OFFER-R1` = `FPT Cầu Giấy → Tòa V-City, Lê Thái Tổ` · Hôm nay · **Giờ nào cũng được** (16:34) |
| 2 | A đăng **đúng 3** tin NEED, mỗi tin trùng 2 điểm + giao ngày/buổi *(setup)* | wizard 3 bước ×3 | ✅ PASS | `_setup__need-r1-1-truoc-dang.png` | `SEED R1-1` 16:46 · `R1-2` 16:50 · `R1-3` 16:53 — mã seed cắm ở ô **GHI CHÚ** |
| 3 | B đăng nhập, nhấn icon chuông, **đếm** thông báo khớp tuyến | `find accessibility id "Thông báo"` → tap | ✅ PASS | — | vào màn Thông báo lúc 16:58 |
| E1 | **Có đúng 3 thông báo khớp tuyến cho tin OFFER đó** | `…instance(3)` ✅ tìm thấy · `scroll_to_element …instance(4)` 🚫 **NOT FOUND** sau 8 nhịp | ✅ PASS | `TC-ASN-015__verify-dung-3-thong-bao.png` | **4 = BASELINE 1 + 3 mới** ⇒ đúng 3 |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-ASN-015__verify-dung-3-thong-bao.png`
**Oracle định danh 3 thông báo mới** — ⛔ không suy từ con số tổng, mà đọc **nhãn tuổi** khớp đúng 3 mốc đăng:
`2 phút trước` ↔ `R1-3` (16:53) · `7 phút trước` ↔ `R1-2` (16:50) · `12 phút trước` ↔ `R1-1` (16:46);
thông báo thứ 4 là `1 giờ trước` = **BASELINE** (`OFFER-C1`, tồn dư VR-009) và **đã đọc** (mất vạch cam + chấm đỏ),
trong khi 3 cái mới đều **chưa đọc** (còn vạch cam + chấm đỏ) ⇒ 2 dấu hiệu độc lập cùng chỉ ra 3 là số mới.
**Locators captured:** 2 (`instance(N)` đếm · icon chuông — tái xác nhận VR-009)

---

## TC-ASN-016: Check tin OFFER có 5 tin NEED khớp nhận đủ 5 thông báo

> Scenario `SC-ASN-014` · P2 · Lô 1 · Tài khoản đếm: **B `stag_giangdc2@`** (chủ `OFFER-R1`)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | B đăng 1 tin OFFER *(setup)* | — | ✅ PASS | `_setup__offer-r1-truoc-dang.png` | tái dùng `OFFER-R1` của `TC-ASN-015` (`§10.3` gộp seed) |
| 2 | A đăng **đúng 5** tin NEED khớp *(setup)* | wizard ×5 (3 tin ở `TC-ASN-015` + `R1-4`,`R1-5`) | ✅ PASS | `TC-ASN-016__pre-du-5-tin-need-tren-bang-tin.png` | ✅ **Đã kiểm ĐỘC LẬP**: Bảng tin có **đúng 5** card tuyến `FPT Cầu Giấy → Tòa V-City`, `Hôm nay · Giờ nào cũng được`, tuổi **6′ · 11′ · 23′ · 28′ · 32′**; card kế tiếp là tuyến khác ⇒ seed KHÔNG thiếu |
| 3 | B nhấn chuông, **đếm** thông báo khớp tuyến | cuộn-và-ghép page source ×2 vị trí (xem *Phương pháp đếm*) | ❌ **FAIL** | `TC-ASN-016__step3-FAIL-chi-4-thong-bao-moi.png` | — |
| E1 | **Có đúng 5 thông báo khớp tuyến cho tin OFFER đó** | **Expected: 5 · Actual: 4** | ❌ **FAIL** | `TC-ASN-016__step3-FAIL-chi-4-thong-bao-moi.png` | xem bảng chứng cứ dưới |

**Result: ❌ FAIL tại E1 — Expected `5` thông báo · Actual `4`**
**Evidence:** `screenshots/TC-ASN-016__step3-FAIL-chi-4-thong-bao-moi.png` (+ `TC-ASN-016__pre-du-5-tin-need-tren-bang-tin.png`)

### 🔍 Chứng cứ — 3 phép đo độc lập, ⛔ không suy diễn

| Phép đo | Cách lấy | Kết quả |
|---|---|---|
| **(1) BASELINE trước seed** | 16:28, `instance(0)` ✅ · `scroll_to …instance(1)` 🚫 NOT FOUND | **đúng 1** thông báo khớp tuyến, và nó **đã đọc** |
| **(2) Số tin NEED khớp thực có** | page source Bảng tin ở **2 vị trí cuộn**, ghép theo nhãn tuổi | **đúng 5** (`6′·11′·23′·28′·32′`), cùng tuyến + cùng khung giờ |
| **(3) Số thông báo khớp tuyến sau seed** | page source màn Thông báo ở **2 vị trí cuộn**, ghép theo nhãn tuổi | **5 tổng** = `7′·18′·23′·28′` (**chưa đọc**) + `1 giờ` (**đã đọc** = baseline) |

⇒ **(3) − (1) = 4 thông báo MỚI cho 5 tin NEED khớp.** Dấu hiệu đọc/chưa-đọc là oracle thứ 2 độc lập với nhãn tuổi:
4 cái mới đều còn **vạch cam trái + chấm đỏ**, baseline thì mất cả hai.

### 🪤 Phương pháp đếm — ĐÍNH CHÍNH cách làm của VR-009 (bẫy mới `T-ASN-10`)

🔴 `appium_find_element` / `scroll_to_element` với `.instance(N)` **chỉ thấy node ĐANG RENDER**.
Màn Thông báo chỉ render **~4 mục** một lúc ⇒ `instance(5)` báo `NOT FOUND` **ngay cả khi danh sách có 6 mục**,
và sau khi `scroll_to_element` cuộn xuống đáy thì `instance(4)` cũng biến mất.
⇒ ⛔ **KHÔNG được dùng `instance(N)` làm phép đếm tuyệt đối cho danh sách dài.**
✅ Cách đúng đã dùng ở đây: **dump page source ở nhiều vị trí cuộn rồi ghép theo nhãn tuổi** (nhãn tuổi là khoá duy nhất).
*(`TC-ASN-015` không dính bẫy này vì tổng chỉ có 4 mục — vẫn nằm trong cửa sổ render; kết luận của nó vẫn đúng.)*

### ❓ Hai giả thuyết cho việc thiếu 1 thông báo — **CHƯA chốt, sẽ tách ở `TC-ASN-025`**

| GT | Nội dung | Phép thử tách |
|---|---|---|
| **H1** ⚠️ | **Trần 5 tính theo TÀI KHOẢN chứ không theo TUYẾN** — tài khoản B đã có 5 thông báo (4 mới + 1 baseline của `OFFER-C1`) nên tin thứ 5 bị chặn. Đây đúng là rủi ro `C-ASN-04(e)` mà `TC-ASN-025` sinh ra để bắt | đăng 1 tin NEED khớp **`OFFER-R2`** (tuyến KHÁC): H1 ⇒ **không** có thông báo mới |
| **H2** | 1 thông báo bị **rớt/chậm** (lỗi giao thông báo), không liên quan trần | H2 ⇒ tin `R2` **vẫn** sinh thông báo |

⛔ Dù H1 hay H2 thì `TC-ASN-016` **vẫn FAIL** (expected 5, actual 4) — nguyên nhân gốc chỉ đổi **nội dung bug**, không đổi verdict.

---

## 🌱 SEED lượt 3 — tài khoản A đăng `R1-6` + `R2-1` (17:25–17:36)

| Mã seed | Tuyến | Khớp OFFER nào | Giờ đăng | Kết quả |
|---|---|---|---|---|
| `SEED R1-6` | `FPT Cầu Giấy → Tòa V-City` · Hôm nay · Giờ nào cũng được | `OFFER-R1` *(tin khớp thứ **6**)* | ~17:30 | ✅ *"Đăng tin thành công!"* |
| `SEED R2-1` | `FPT Tân Thuận 1 → FTEL SG08 Gò Vấp` · Hôm nay · Giờ nào cũng được | **`OFFER-R2`** *(tuyến THỨ HAI, tin khớp đầu tiên của tuyến này)* | ~17:36 | ✅ *"Đăng tin thành công!"* |

**Evidence seed:** ảnh màn Bước 3/3 của `SEED R2-1` (`FPT Tân Thuận 1` → `FTEL SG08 Gò Vấp` · Hôm nay · Giờ nào cũng được — trùng khít `OFFER-R2`) được trích trong section `TC-ASN-025` bên dưới.

### 📏 Phép đo chốt (17:38–17:40, tài khoản B) — dùng cho **3 TC** cùng lúc

Ghép page source **2 vị trí cuộn**: danh sách khớp tuyến = `30′ · 41′ · 46′ · 51′` + `2 giờ` ⇒ **vẫn đúng 5, y hệt lần đo 17:18**
(4 mốc đầu chính là `7′·18′·23′·28′` của lần trước cộng thêm 23 phút — ⛔ không mục nào mới).
⇒ **cả `R1-6` LẪN `R2-1` đều KHÔNG sinh thông báo.**

---

## TC-ASN-017: Check tin NEED khớp thứ 6 không sinh thêm thông báo khi tuyến đã đủ trần 5

> Scenario `SC-ASN-014` · P2 · Lô 1 · Tài khoản đếm: **B `stag_giangdc2@`**

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | B đăng 1 tin OFFER *(setup)* | — | ✅ PASS | `_setup__offer-r1-truoc-dang.png` | tái dùng `OFFER-R1` |
| 2 | A đăng đúng 5 tin NEED khớp *(setup)* | wizard ×5 | ✅ PASS | *(dùng chung seed — ảnh seed trích ở section `TC-ASN-016`)* | Bảng tin xác nhận đủ 5 |
| 3 | B nhấn chuông, **ghi lại** số thông báo khớp tuyến *(setup)* | ghép page source 2 vị trí, 17:18 | ✅ PASS | *(phép đo dùng chung — ảnh trích ở section `TC-ASN-016`)* | **số ghi được = 4** *(đáng lẽ 5 — đó là FAIL của `TC-ASN-016`)* |
| 4 | A đăng thêm tin NEED **thứ 6** khớp *(setup)* | wizard | ✅ PASS | *(dùng chung seed — ảnh seed trích ở section `TC-ASN-025`)* | `SEED R1-6` lúc ~17:30 *(ảnh trích là màn xác nhận của lượt seed cùng phiên)* |
| 5 | B nhấn chuông, **đếm lại** | ghép page source 2 vị trí, 17:38 | ✅ PASS | `TC-ASN-017__verify-so-thong-bao-khong-doi.png` | mục mới nhất là `30 phút trước`; `R1-6` đăng ~8 phút trước ⇒ ⛔ không có mục nào của nó |
| E1 | **Số thông báo vẫn bằng bước 3; KHÔNG có thông báo mới cho tin thứ 6** | bước 3 = 4 · bước 5 = 4 · không mục mới | ✅ PASS | `TC-ASN-017__verify-so-thong-bao-khong-doi.png` | — |

**Result: ✅ PASS (5 steps, 1 expected)**
**Evidence:** `screenshots/TC-ASN-017__verify-so-thong-bao-khong-doi.png`
⚠️ **CẢNH BÁO ĐỌC KẾT QUẢ — PASS này KHÔNG chứng minh `C-ASN-04(d)`.**
Mệnh đề TC muốn xác nhận là *"**TUYẾN** đã đủ 5 thì không gửi thêm"*, nhưng trong lần chạy này **tuyến `R1` mới chỉ có 4**
thông báo — thứ chặn tin thứ 6 là **trần theo TÀI KHOẢN** (chứng minh ở `TC-ASN-025`). Kết quả quan sát đúng y như expected,
nhưng **tiền đề của TC chưa bao giờ đạt** ⇒ ⛔ **không được kết luận "trần per-tuyến đã verify"**. Phải chạy lại TC này
sau khi sửa lỗi ở `TC-ASN-025`.

---

## TC-ASN-014: Check chỉ gợi ý tối đa 5 tin khi có 6 tin NEED khớp

> Scenario `SC-ASN-013` · P2 · Lô 1 · Tài khoản đếm: **B `stag_giangdc2@`**

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | B đăng 1 tin OFFER *(setup)* | — | ✅ PASS | `_setup__offer-r1-truoc-dang.png` | `OFFER-R1` |
| 2 | A đăng **6** tin NEED khớp *(setup)* | wizard ×6 (`R1-1`…`R1-6`) | ✅ PASS | *(dùng chung seed — ảnh seed trích ở section `TC-ASN-016`)* | Bảng tin xác nhận 5 tin đầu; `R1-6` đăng ~17:30 |
| 3 | B nhấn chuông *(setup)* | tap `accessibility id "Thông báo"` | ✅ PASS | — | — |
| 4 | **Đếm số tin NEED khác nhau được gợi ý** | ghép page source 2 vị trí cuộn | ✅ PASS | `TC-ASN-014__verify-toi-da-5-goi-y.png` | khối khớp tuyến kết thúc sau mục `2 giờ trước`, kế tiếp là loại thông báo khác ⇒ **tổng 5**, trong đó **4** trỏ tới tin NEED của `R1` |
| E1 | **Số tin NEED được gợi ý nhiều nhất là 5** | Actual = **4** ≤ 5 | ✅ PASS | `TC-ASN-014__verify-toi-da-5-goi-y.png` | ⛔ app **không** gợi ý quá trần |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ASN-014__verify-toi-da-5-goi-y.png`
⚠️ **CẢNH BÁO ĐỌC KẾT QUẢ — đây là PASS trên một CẬN TRÊN chưa bị chạm.** Assertion `≤5` thoả, nhưng app dừng ở **4**
vì trần TÀI KHOẢN (xem `TC-ASN-025`), ⛔ **không phải** vì trần gợi ý per-tuyến. Nói cách khác TC này **không có khả năng
phân biệt** app đúng hay sai ở mốc 5 chừng nào lỗi trần-theo-tài-khoản còn tồn tại ⇒ **chạy lại sau khi fix**.

---

## TC-ASN-025: Check mỗi tuyến OFFER có trần 5 thông báo độc lập, không cộng dồn

> Scenario `SC-ASN-014` · P2 · Lô 2 · Tài khoản đếm: **B `stag_giangdc2@`** (chủ **cả hai** tuyến OFFER)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 0 | *(pre-cond)* B đã có tuyến OFFER thứ nhất + các tin NEED khớp, chuông **đã chạm mốc 5** | tái dùng seed `TC-ASN-016` | ✅ PASS | *(dùng chung seed — ảnh seed trích ở section `TC-ASN-016`)* | ⚠️ mốc 5 đạt được là **4 (`R1`) + 1 (baseline `OFFER-C1`)**, ⛔ không phải 5 của riêng `R1` — chính đây là dấu hiệu đầu tiên của lỗi |
| 1 | B đăng thêm tin OFFER **thứ hai**, tuyến khác *(setup)* | form `Tôi nhận giao hàng` | ✅ PASS | `_setup__offer-r2-truoc-dang.png` | `OFFER-R2` = `FPT Tân Thuận 1 → FTEL SG08 Gò Vấp` · Hôm nay · Giờ nào cũng được (16:37) |
| 2 | A đăng 1 tin NEED trùng tuyến thứ hai, ngày/buổi giao nhau *(setup)* | wizard 3 bước | ✅ PASS | `TC-ASN-025__pre-seed-r2-khop-tuyen-2.png` | `SEED R2-1` — màn xác nhận cho thấy trùng **khít** cả 2 điểm + ngày + buổi |
| 3 | B nhấn chuông, check thông báo **của riêng tuyến 2** và **tổng** số thông báo | ghép page source 2 vị trí cuộn, **đo 2 lần** (17:38 và 17:43) | ❌ **FAIL** | `TC-ASN-025__step3-FAIL-tuyen-2-khong-co-thong-bao.png` | — |
| E1 | **Tuyến 2 nhận thông báo mới dù tuyến 1 đã đạt trần; tổng > 5** | Actual: tuyến 2 **KHÔNG có** thông báo nào · tổng **vẫn đúng 5** | ❌ **FAIL** | `TC-ASN-025__step3-FAIL-tuyen-2-khong-co-thong-bao.png` | — |

**Result: ❌ FAIL tại E1**
**Evidence:** `screenshots/TC-ASN-025__step3-FAIL-tuyen-2-khong-co-thong-bao.png` (+ `TC-ASN-025__pre-seed-r2-khop-tuyen-2.png`)

### 🔴 KẾT LUẬN — chốt được `H1`, bác bỏ `H2` (xem `TC-ASN-016`)

| Phép đo | 17:38 | 17:43 *(load lại màn)* | Diễn giải |
|---|---|---|---|
| Danh sách khớp tuyến của B | `30′ · 41′ · 46′ · 51′` + `2 giờ` | `35′ · 46′ · 51′ · 56′` + `2 giờ` | **cùng 5 mục**, chỉ già thêm 5 phút ⇒ ⛔ **0 mục mới** |
| Tuổi `SEED R1-6` khi đo | ~8 phút | ~13 phút | ≫ `NFR-04` (≤60s) |
| Tuổi `SEED R2-1` khi đo | ~2 phút | ~7 phút | ≫ `NFR-04` (≤60s) |

⇒ ⛔ **Không phải "thông báo đến chậm"** (`H2` bị bác bỏ bằng 2 lần đo cách nhau 5 phút, đều vượt NFR).
⇒ ✅ **`H1` ĐÚNG: trần 5 được áp theo TÀI KHOẢN, không theo từng tuyến OFFER.**

**Chuỗi suy luận khép kín** *(mỗi mắt xích đều là số đo, ⛔ không suy diễn)*:
1. Trước seed, B có **1** thông báo khớp tuyến (của `OFFER-C1`) — đo 16:28.
2. `OFFER-R1` + **5** tin NEED khớp ⇒ chỉ thêm **4** ⇒ tổng chạm đúng **5** — đo 17:18.
3. Thêm tin NEED thứ **6** của `R1` ⇒ không thêm — đo 17:38 & 17:43.
4. Thêm **`OFFER-R2` (tuyến hoàn toàn khác) + 1 tin NEED khớp** ⇒ **cũng không thêm** — đo 17:38 & 17:43.
   👉 Mắt xích 4 là mắt xích quyết định: nếu trần tính theo tuyến thì tuyến `R2` **phải** có slot trống (0/5).

**Tác động:** CBNV đăng nhiều tuyến sẽ **mất hoàn toàn** thông báo khớp tuyến ở các tuyến sau khi tổng chạm 5 —
kể cả tuyến mới tinh chưa có thông báo nào. Đây đúng là rủi ro BA đã lường trước ở `C-ASN-04(e)`
(*"rủi ro thật nếu backend dùng chung 1 bộ đếm cho cả tài khoản"*) ⇒ **cần `/log-bug`**.

---

## 🔎 Recon giữa phiên — cơ chế "Hết hạn" (gỡ chặn `TC-ASN-019`)

`TC-ASN-019` ghi *"Nhờ dev/QA seed 1 tin NEED … có `Đến ngày` đã trôi qua"* và `Test Data` ghi
*"⛔ không seed được qua UI"*. **Không còn đúng**: trên STG đã có sẵn tin thoả điều kiện, ⛔ không cần dev.

Vào **`Hoạt động` → `Đơn của tôi` → tab `Đã hoàn thành`** của B thấy:

| Tin | Tuyến | Ngày | Badge | Chú thích app |
|---|---|---|---|---|
| **`Gửi tài liệu`** *(NEED)* | `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` | **19/9/2026 = HÔM NAY** | 🏷️ **`Hết hạn`** | *"Không có ai nhận mang giúp trong thời gian đăng — tin đã tự động đóng."* |

🔑 **Tin đề ngày HÔM NAY mà ĐÃ hết hạn** ⇒ app đóng tin theo **khung giờ trong ngày**, ⛔ không chỉ theo `Đến ngày`.
⇒ Vẫn dựng được tiền đề của `TC-ASN-019`: một tin NEED **vừa hết hạn vừa giao ngày** với tin OFFER đăng hôm nay.
*(Đây cũng là lời giải cho bẫy `T-ASN-09` của VR-009: thông báo khớp tuyến "biến mất hàng loạt" khi khung giờ trôi qua
là do **tin bị đóng**, không phải thông báo bị xoá.)*

**Evidence:** ảnh tin `Hết hạn` ở `Đơn của tôi → Đã hoàn thành` được trích trong section `TC-ASN-019` bên dưới.

---

## 🔎 Recon giữa phiên — `stag_huyennhk@` **KHÔNG truy cập được FoxEco**

Định dùng `stag_huyennhk@` làm chủ tin OFFER cho `TC-ASN-018`/`019` vì đây là tài khoản **chưa từng đăng nhập**
⇒ chuông sạch ⇒ ⛔ không dính trần-theo-tài-khoản vừa phát hiện. Nhưng:

| Bước | Kết quả |
|---|---|
| Đăng nhập `stag_huyennhk@` | ✅ **THÀNH CÔNG** — FoxPro chào *"Nguyễn Huỳnh Kim Huyền"* (🆕 lần đầu tiên đăng nhập tài khoản này) |
| FoxPro → `Chức năng` → tìm icon `FoxEco` | 🚫 **NOT FOUND** — `scroll_to_element` báo *"page source did not change (end of scrollable content)"*; danh sách chỉ có **9 app**: Phê duyệt cam kết · Hồ sơ nhân viên · Sinh nhật · Báo cáo · Quy định và Chính sách · Quyết toán thuế · F-Office · Cáo sáng tạo · Kiểm soát nội bộ |

🔑 **Kết luận:** FoxEco **không bật cho mọi CBNV** — `stag_huyennhk@` chỉ đóng được vai **người nhận** (dữ liệu trong form),
⛔ **không** đóng được vai actor (đăng tin / nhận đơn / xem chuông). Cần cập nhật `04_test-data/valid/USR-accounts.md §1`.
⇒ Đổi chủ tin OFFER của `TC-ASN-018`/`019` sang **`stag_taipm@`**.

**Evidence:** `screenshots/_recon__huyennhk-khong-co-icon-foxeco.png`

---

## 🌱 SEED lượt 4 — tài khoản **C `stag_taipm@`** đăng 2 tin OFFER (18:01–18:04)

> 🔁 **Đổi vai giữa phiên:** `TC-ASN-018`/`019` cần chủ tin OFFER có chuông **chưa chạm trần 5**
> (vì lỗi ở `TC-ASN-025`). B `stag_giangdc2@` đã đầy 5 ⇒ ⛔ dùng B thì mọi phép "không có thông báo" đều vô nghĩa.
> Đã đo chuông C **trước khi seed**: **0** thông báo khớp tuyến *(chỉ có loại `Đã có người nhận` / `Đơn đã bị huỷ`)* ⇒ còn đủ 5 slot.

| Seed | Tuyến | Ngày · Buổi | Dùng cho |
|---|---|---|---|
| **`OFFER-R3`** | `FTEL SG08 Gò Vấp` → `FPT Tân Thuận 1` | Hôm nay · Giờ nào cũng được | `TC-ASN-018` *(tuyến sạch, chưa tin NEED nào)* |
| **`OFFER-R4`** | `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` | Hôm nay · Giờ nào cũng được | `TC-ASN-019` *(trùng tuyến tin NEED **đã hết hạn** của B)* |

**Evidence seed:** `screenshots/_setup__offer-r3-truoc-dang.png` · `screenshots/_setup__offer-r4-truoc-dang.png`

🆕 **Phát hiện cơ chế:** đăng OFFER mới ⇒ hệ thống **bắn thông báo HỒI TỐ** cho các tin NEED **đã có sẵn** khớp tuyến
(⛔ không chỉ cho tin đăng sau). Đo được: chuông C từ **0** → **2** trong ~2 phút sau khi đăng `OFFER-R4`.
Nhờ đó `TC-ASN-019` có sẵn **đối chứng dương** mà ⛔ không phải seed thêm.

---

## TC-ASN-019: Check tin NEED quá hạn không vào gợi ý và không sinh thông báo

> Scenario `SC-ASN-016` · P2 · Lô 4 · Tài khoản đếm: **C `stag_taipm@`** (chủ `OFFER-R4`)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | B đăng 1 tin OFFER tuyến/khung giờ xác định *(setup)* | form `Tôi nhận giao hàng` | ✅ PASS | `_setup__offer-r4-truoc-dang.png` | `OFFER-R4` = `Tòa V-City → FPT Cầu Giấy` · Hôm nay · Giờ nào cũng được (18:04). *(vai "B" của TC do `stag_taipm@` đảm nhiệm — xem lý do đổi vai ở trên)* |
| 2 | *(Steps ghi: nhờ dev/QA seed 1 tin NEED trùng tuyến nhưng đã "Hết hạn")* | ⛔ **KHÔNG cần dev** — STG đã có sẵn | ✅ PASS | `TC-ASN-019__pre-tin-need-het-han-ngay-hom-nay.png` | Tin của **`stag_giangdc2@`**: `Gửi tài liệu` · **`Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy`** · **19/9/2026 (= hôm nay, giao ngày với `OFFER-R4`)** · badge 🏷️ **`Hết hạn`** · *"tin đã tự động đóng"* |
| 3 | Đăng nhập tài khoản chủ OFFER | login `stag_taipm@` | ✅ PASS | — | — |
| 4 | Nhấn icon chuông | `find accessibility id "Thông báo"` → tap | ✅ PASS | — | — |
| 5 | **Check danh sách thông báo** | ghép page source; mở **từng** thông báo để định danh tin đích | ✅ PASS | `TC-ASN-019__verify-thong-bao-chi-tro-tin-con-song.png` | xem bảng dưới |
| 6 | Nhấn tab `Bảng tin`, **tìm tin hết hạn** | `scroll_to_element textContains("KCX Tân Thuận")` — cuộn **hết** danh sách | ✅ PASS | `TC-ASN-019__verify-bangtin-vang-tin-het-han.png` | 🚫 **NOT FOUND**. Enumerate toàn Bảng tin (5 lượt dump page source): tuyến `Tòa V-City → FPT Cầu Giấy` chỉ có **3 card, đều CÒN HẠN** (`Hôm nay·Sau giờ làm` 2 giờ · `Hôm nay·Sáng` *Tin của bạn* 5 giờ · `Hôm nay·Sáng` 9 giờ) — ⛔ không có card nào là tin hết hạn |
| E1 | **KHÔNG có thông báo khớp tuyến nào trỏ tới tin đã hết hạn** | đúng **2** thông báo, **cả 2 trỏ tin CÒN SỐNG** | ✅ PASS | `TC-ASN-019__verify-thong-bao-chi-tro-tin-con-song.png` | — |
| E2 | **Tin đã hết hạn KHÔNG xuất hiện trong Bảng tin** | 🚫 NOT FOUND trên toàn danh sách | ✅ PASS | `TC-ASN-019__verify-bangtin-vang-tin-het-han.png` | — |

**Result: ✅ PASS (6 steps, 2 expected)**
**Evidence:** `screenshots/TC-ASN-019__verify-thong-bao-chi-tro-tin-con-song.png` + `screenshots/TC-ASN-019__verify-bangtin-vang-tin-het-han.png` (+ `TC-ASN-019__pre-tin-need-het-han-ngay-hom-nay.png`)

### 🔍 Định danh từng thông báo — ⛔ không suy từ con số

| Thông báo | Mở ra tin | Tuổi tin | CTA `Tôi mang giúp được` | Lộ trình | Kết luận |
|---|---|---|---|---|---|
| #0 | `Gửi tài liệu` | **9 giờ trước** | ✅ **có** | *(khớp card Bảng tin `Hôm nay · Sáng`, 9 giờ)* | tin **CÒN SỐNG** |
| #1 | `Gửi tài liệu` | **2 giờ trước** | ✅ **có** | **`Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy`** *(đọc trực tiếp ở khối LỘ TRÌNH)* | tin **CÒN SỐNG** |

🔑 **Đối chứng dương nằm ngay trong phép thử** *(đúng bài học `T-ASN-09`)*: matcher **đang chạy** trên đúng tuyến
`Tòa V-City → FPT Cầu Giấy` — nó bắn **2** thông báo cho **2** tin còn sống của người khác trên tuyến đó
*(tin `Hôm nay·Sáng` của chính C bị loại đúng theo `TC-ASN-013`)*.
Vậy mà tin **hết hạn** cùng tuyến, cùng ngày ⇒ **0** thông báo. Sự vắng mặt này là **kết luận được**, ⛔ không phải "matcher im lặng".

🆕 **Bẫy `T-ASN-11` — thông báo khớp tuyến BIẾN MẤT khỏi danh sách sau khi MỞ.** Chuông C có 2 mục lúc 18:13;
mở mục #0 rồi quay lại → còn **1**; mở nốt #1 → còn **0**. ⚠️ Khác hẳn tài khoản B (mục đã đọc **vẫn nằm lại**).
⇒ **Đếm TRƯỚC khi mở**, nếu không sẽ tự phá mẫu số. *(Đây nhiều khả năng là lời giải thật cho `T-ASN-09` của VR-009.)*

📌 **Đề nghị sửa TC:** `Test Data` của `TC-ASN-019` ghi *"⛔ không seed được qua UI"* và Steps ghi *"Nhờ dev/QA seed"* —
**không còn đúng**: STG tự sinh tin `Hết hạn` và `Đơn của tôi → Đã hoàn thành` cho biết chính xác tin nào đã hết hạn.

---

## 🌱 SEED lượt 5 — tài khoản A đăng 3 tin NEED theo **thứ tự thời gian có kiểm soát** (18:25–18:39)

| Thứ tự | Mã seed (ô Ghi chú) | Tuyến | Khớp `OFFER-R3`? | Giờ đăng |
|---|---|---|---|---|
| **1 (sớm nhất)** | `SEED X lech tuyen` | `FPT Tân Thuận 1` → `Tòa V-City, Lê Thái Tổ` | ❌ **KHÔNG** *(cũng không khớp `R4`)* | **18:25** |
| **2** | `SEED R3a dang truoc` | `FTEL SG08 Gò Vấp` → `FPT Tân Thuận 1` | ✅ có | **18:31** |
| **3 (muộn nhất)** | `SEED R3b dang sau` | `FTEL SG08 Gò Vấp` → `FPT Tân Thuận 1` | ✅ có | **18:39** *(cách tin 2 **8 phút** ≥ yêu cầu 1 phút của TC)* |

**Evidence seed:** ảnh màn Bước 3/3 của `SEED R3b` được trích trong section `TC-ASN-018` bên dưới.

---

## TC-ASN-018: Check danh sách gợi ý ưu tiên tin trùng tuyến trước, thời gian đăng sau

> Scenario `SC-ASN-015` · P3 · Lô 3 · Tài khoản đếm: **C `stag_taipm@`** (chủ `OFFER-R3`)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 0 | *(pre-cond)* B đã đăng 1 tin OFFER `P1→P2` | form `Tôi nhận giao hàng` | ✅ PASS | `_setup__offer-r3-truoc-dang.png` | `OFFER-R3` = `FTEL SG08 Gò Vấp → FPT Tân Thuận 1` · Hôm nay · Giờ nào cũng được. 🔑 Chọn tuyến **hoàn toàn sạch** (chưa tin NEED nào) để mẫu số chỉ gồm 3 tin của TC |
| 1 | A đăng 1 tin NEED **KHÔNG trùng tuyến**, đăng **SỚM NHẤT** *(setup)* | wizard | ✅ PASS | `TC-ASN-018__pre-seed-r3b-dang-sau.png` | `SEED X` 18:25 |
| 2 | A đăng tin NEED thứ hai **trùng tuyến** *(setup)* | wizard | ✅ PASS | `TC-ASN-018__pre-seed-r3b-dang-sau.png` | `SEED R3a` 18:31 |
| 3 | A đăng tin NEED thứ ba **trùng tuyến**, sau tin 2 ≥1 phút *(setup)* | wizard | ✅ PASS | `TC-ASN-018__pre-seed-r3b-dang-sau.png` | `SEED R3b` 18:39 — cách 8 phút |
| 4 | B nhấn chuông, **ghi lại thứ tự** 3 thông báo từ trên xuống, đối chiếu 3 mốc thời gian | đọc danh sách + **mở** mục trên cùng để đọc mã seed | ✅ PASS | `TC-ASN-018__verify-thu-tu-goi-y.png` | xem bảng dưới |
| E1 | **Tin 2 & 3 (trùng tuyến) xếp TRƯỚC tin 1 (không trùng tuyến); tin 3 xếp trước tin 2** | ✅ đúng cả hai vế | ✅ PASS | `TC-ASN-018__verify-thu-tu-goi-y.png` + `TC-ASN-018__verify-dinh-danh-r3b-tren-cung.png` | — |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ASN-018__verify-thu-tu-goi-y.png` + `screenshots/TC-ASN-018__verify-dinh-danh-r3b-tren-cung.png` (+ `TC-ASN-018__pre-seed-r3b-dang-sau.png`)

### 🔍 Thứ tự đọc được trên chuông C (18:42)

| Vị trí | Nhãn tuổi | Là tin nào | Căn cứ định danh |
|---|---|---|---|
| **1 (trên cùng)** | `2 phút trước` | **`SEED R3b`** *(đăng 18:39, MUỘN NHẤT)* | 🔑 **mở ra đọc được `Ghi chú: SEED R3b dang sau`** — oracle tuyệt đối, ⛔ không dựa nhãn thời gian |
| **2** | `9 phút trước` | `SEED R3a` *(đăng 18:31)* | nhãn tuổi khớp; và chỉ còn đúng 1 tin R3 khác |
| — | *(vắng mặt)* | `SEED X` *(đăng 18:25, SỚM NHẤT, lệch tuyến)* | ⛔ **không có thông báo nào** — dù là tin đăng sớm nhất |

**Tầng 1 (độ gần tuyến):** app loại tin không trùng tuyến **hoàn toàn** khỏi gợi ý ⇒ mệnh đề *"trùng tuyến xếp TRƯỚC không trùng tuyến"* thoả ở dạng **mạnh hơn** expected (không phải xếp sau, mà là **không xuất hiện**).
**Tầng 2 (thời gian đăng):** giữa 2 tin cùng trùng tuyến, tin **đăng sau** (`R3b`) nằm **trên** tin đăng trước (`R3a`) ⇒ đúng expected.
⚖️ **Giới hạn đã khai:** vì tin lệch tuyến không xuất hiện, phép thử **không đo được vị trí tương đối** của nó —
chỉ kết luận được "bị loại", ⛔ không kết luận được "xếp dưới".

### 🔴 ĐÍNH CHÍNH ghi chép VR-009 — màn **Chi tiết tin CÓ mục `Ghi chú`**

`VR-009/vibe-locators.md` ghi *"🔴 Mục `GHI CHÚ` **KHÔNG TỒN TẠI** trên màn Chi tiết tin — 🚫 NOT FOUND (page source đầy đủ)"*
và dùng nó để **đính chính VR-008**. Phiên này quan sát ngược lại: màn Chi tiết tin hiển thị khối
`THÔNG TIN HÀNG` → dòng **`Ghi chú` → `SEED R3b dang sau`** (xem `TC-ASN-018__verify-dinh-danh-r3b-tren-cung.png`).
⇒ ✅ **Mẹo "cắm mã seed vào ô Ghi chú để định danh tin" DÙNG ĐƯỢC** — đây là oracle định danh **mạnh nhất** hiện có,
mạnh hơn nhãn tuổi tin (vốn bị làm tròn). Nhiều khả năng VR-009 mở nhầm một tin **không có** ghi chú
(khối chỉ render khi ô Ghi chú khác rỗng). ⚠️ Các phiên sau **đừng** tin dòng "không tồn tại" của VR-009.

