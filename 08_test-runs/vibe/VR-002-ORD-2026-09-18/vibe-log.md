# Vibe Test Log — VR-002 — v1.1 + CARRIED v1.0 — 2026-09-18

> Module: **ORD** (Đăng tin & Quản lý tin) · Platform: **mobile** (Appium MCP, UiAutomator2) ·
> Env: STG · host app `com.hrisproject.stag` (FoxPro) → icon FoxEco · Evidence dir: `screenshots/`
> Tài khoản: **A** — "Đặng Châu Giang", MNV `00131946` (`FOXECO_STG_USER_A`) · emulator-5554
> Phiên: 2026-09-18 (khởi tạo)
> SCOPE_TOTAL = **88 TC** = 48 (v1.1) + 40 (CARRIED v1.0) — xem `scope-ledger.md`
> Tập chạy: **pending = toàn bộ 88** (chưa có `coverage-ORD.md` trước phiên ⇒ Step 1.2 không hỏi)

> 🧾 **Evidence chụp bằng `adb exec-out screencap`** (không dùng `appium_screenshot`: MCP này trả
> inline HTML viewer ~428k ký tự/call và không có tham số `filename`) — theo tiền lệ VR-001.
> ⛔ Locator **100% qua MCP** (`appium_find_element` / `appium_get_page_source`), không qua ADB.

---

## 🗺️ Pha A — recon (KHÔNG sinh verdict)

| # | Màn | Cách vào | Page source | Element vào map |
|---|---|---|---|---|
| A1 | **Đăng tin mới** (chọn loại tin) | tab `Đăng tin` (bottom nav FoxEco) | — *(đọc qua find_element từng phần tử)* | 4 |
| A2 | **Wizard Bước 1/3 — Thông tin hàng** | card `Tôi cần gửi hàng` | 204.867 ký tự → file tool-result (L3) | 30 |
| A3 | **Android Photo Picker** (OS, `com.google.android.providers.media.module`) | `0/5` → `Chọn từ thư viện` | 166.093 ký tự → file tool-result (L3) | 4 |

**Số màn harvest ở Pha A: 3.** Locator map nạp thêm từ `locators/vibe-locators-latest.md` (VR-001, 9 màn — trong đó wizard 3 bước + Theo dõi đơn đã có sẵn) ⇒ Pha B chạy gần như 0 snapshot.

---

## 🔴 Phát hiện chung của lô 1 (đọc trước khi đọc verdict từng TC)

**F1 — 3 trường bắt buộc MỚI của v1.1 làm hỏng bước "Tiếp theo" trong Steps của nhiều TC CARRIED v1.0.**
App bản STG hiện tại chỉ enable nút `Tiếp theo` ở Bước 1 khi có **đủ 4 thứ**: `GIÁ TRỊ HÀNG` + `TRỌNG LƯỢNG` + `KÍCH THƯỚC` + **≥1 ảnh**. Các TC v1.0 viết thời `SC-ORD-052/053/054` chưa tồn tại nên chỉ chọn `giá trị hàng` rồi bấm `Tiếp theo` ⇒ **bị chặn**.
⇒ Đây **KHÔNG phải lỗi app** (đúng `BR01-01`/`BR01-02` của v1.1) mà là **TC v1.0 hết hiệu lực phần navigation**.
⛔ Không log bug. 📨 Route `/analyze-requirements --module ORD` + QC chốt `DESCOPED`/cập nhật Steps theo `Project_rule §10.5`.
TC bị ảnh hưởng đã chạy ở lô này: `TC-ORD-007` (step 5) · `TC-ORD-008` (step 6) · `TC-ORD-014`.

**F2 — Host app FoxPro nhảy về tab "Chang"/THÔNG BÁO sau khi đóng photo picker — chỉ tái hiện ở nhánh ảnh > 5MB.**
Ở `TC-ORD-068` (ảnh 6MB bị từ chối), ngay sau khi picker đóng thì người chạy bị đẩy ra màn THÔNG BÁO của FoxPro; phải bấm lại menu `Chức năng` mới trở lại FoxEco. **State wizard giữ nguyên** (chip đã chọn + thông báo lỗi ảnh vẫn còn) ⇒ không mất dữ liệu.
Ở `TC-ORD-012` (ảnh JPG nhỏ, **cùng đường đi**) thì **KHÔNG** tái hiện — app quay lại wizard ngay.
⇒ Nghi liên quan thời gian xử lý ảnh quá cỡ, **chưa đủ căn cứ kết luận**; là bề mặt chưa có trong `scenario_map`.
📨 Route `/analyze-requirements --update "host app FoxPro đổi tab sau khi FoxEco đóng photo picker (ảnh quá cỡ)"` + theo dõi thêm ở lô sau.
⚠️ **2 lần đính chính trong phiên, ghi lại để không ai đọc lệch:**
 (1) thoạt đầu ghi nhận nhầm là *"app thoát/crash, mất draft"* — kiểm `logcat -b events` **không** có `am_proc_died` cho `com.hrisproject.stag`, và quay lại tab `Chức năng` thì wizard còn nguyên ⇒ sửa kết luận **TRƯỚC** khi chốt verdict `TC-ORD-068`;
 (2) sau đó ghi nhầm là *"xảy ra sau mọi lần chọn ảnh"* — `TC-ORD-012` không tái hiện ⇒ thu hẹp lại đúng nhánh > 5MB.
🧾 **Không có ảnh riêng cho F2:** ảnh chụp đúng lúc đó mang tên `TC-ORD-068__step3-FAIL-*` theo verdict SAI ban đầu, đã **xoá** khi sửa verdict (⛔ không đổi tên ảnh cũ thành bằng chứng của kết luận mới). Sẽ chụp lại khi tái hiện được ở lô sau.

---

## TC-ORD-001: Check màn "Đăng tin mới" đủ bốn thành phần và cả hai card bấm được — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Mở FoxEco → tab "Đăng tin" | tap `Đăng tin` (accessibility id) | ✅ PASS | — | phiên OTP do người chạy mở sẵn |
| 3 | Check các thành phần | find `text("Bạn muốn làm gì?")` ✓ · `descriptionStartsWith("Tôi cần gửi hàng")` ✓ · `("Tôi nhận giao hàng")` ✓ · `textContains("không thu phí")` ✓ | ✅ PASS | `TC-ORD-001__verify-bon-thanh-phan.png` | banner nguyên văn: *"App không thu phí, không chat, không thanh toán. Sau khi ghép, SĐT hai bên sẽ được lộ để liên hệ ngoài app."* — khớp đủ 4 vế Expected |
| 4 | Nhấn card "Tôi cần gửi hàng" | tap → wizard Bước 1/3 | ✅ PASS | — | xác nhận bằng `text("Bước 1 / 3")` |
| 5 | Nhấn card "Tôi nhận giao hàng" | ⏳ chưa chạy trong lô 1 | ⏳ | — | gộp cùng `TC-ORD-003` ở lô sau (cùng màn OFFER) |

**Result: ⏳ NOT_RUN (chưa chốt — còn step 5)**
**Evidence:** `screenshots/TC-ORD-001__verify-bon-thanh-phan.png` — verified tồn tại (chỉ phủ step 3–4)
**Lý do chưa chốt:** step 5 cần mở form OFFER; gom chung lô OFFER với `TC-ORD-003`/`042`/`043` để không phải vào/ra wizard 2 lượt.

---

## TC-ORD-002: Check nhấn card "Tôi cần gửi hàng" mở wizard bước 1/3 kèm step indicator — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Mở wizard NEED | tap card `Tôi cần gửi hàng` | ✅ PASS | — | — |
| 4 | Check tiêu đề bước + step indicator | get_text `Bước 1 / 3` · `Thông tin hàng` | ✅ PASS | `TC-ORD-002__verify-buoc-1-3.png` | App ghi **"Bước 1 / 3"** (có space quanh `/`), TC ghi "Bước 1/3" — cùng ngữ nghĩa, ⛔ không tính FAIL. Có thêm progress bar 3 đoạn, đoạn 1 active |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-002__verify-buoc-1-3.png` — verified tồn tại
**Locators captured:** 2 (step indicator, tiêu đề bước)

---

## TC-ORD-005: Check field Loại hàng có đúng tám giá trị và mặc định là Tài liệu — *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Mở wizard NEED | tap card `Tôi cần gửi hàng` | ✅ PASS | — | — |
| 3 | Liệt kê giá trị + giá trị đang chọn | page source: **đúng 8** ViewGroup trong khối `LOẠI HÀNG` | ✅ PASS | `TC-ORD-005__verify-8-chip-mac-dinh-tai-lieu.png` | Thứ tự app = **Tài liệu · Đồ điện tử · Thực phẩm · Hàng nhỏ · Đồ dễ vỡ · Quần áo · Thuốc/Y tế · Khác** — khớp **y hệt** thứ tự Expected. Mặc định chọn sẵn = **Tài liệu** (viền + chữ cam), đọc bằng **ảnh** vì React Native không expose `selected` (bẫy **T1**) |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-005__verify-8-chip-mac-dinh-tai-lieu.png` — verified tồn tại
**Notes:** 🎯 Đây là TC mà `C-ORD-09` cố tình đảo chiều so với v1.0: app **đã** hiện nhãn "Tài liệu" ⇒ PASS đúng oracle v1.1 (đối chứng: `TC-ORD-006` bản v1.0 FAIL trên **cùng** hiện trạng).
**Locators captured:** 8 chip loại hàng (accessibility id = nhãn chip)

---

## TC-ORD-006: Check danh mục loại hàng có tám chip, không có chip "Tài liệu" — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở wizard NEED | tap card `Tôi cần gửi hàng` | ✅ PASS | — | — |
| 2 | Đếm số chip loại hàng | page source: đúng 8 chip | ✅ PASS | — | vế "8 chip" đúng |
| 3 | Tìm chip nhãn "Tài liệu" | find `accessibility id "Tài liệu"` → **FOUND** (còn là chip đang chọn) | ❌ FAIL | `TC-ORD-006__step3-FAIL-co-chip-tai-lieu.png` | Expected đòi **KHÔNG** có chip "Tài liệu" |

**Result: ❌ FAIL at Step 3**
**Reason:** App có chip "Tài liệu" (mặc định chọn) — trái Expected của bản v1.0.
**Evidence:** `screenshots/TC-ORD-006__step3-FAIL-co-chip-tai-lieu.png` — verified tồn tại
**Impact:** 🔴 **TC hết hiệu lực, KHÔNG phải lỗi app.** `C-ORD-09` Resolved 2026-09-16 chốt nhãn **"Tài liệu"**; ràng buộc cũ *"không dùng nhãn Tài liệu"* đã **HẾT HIỆU LỰC** (ghi ngay trong Notes của `TC-ORD-005`). ⛔ Không log bug. 📨 QC chốt `DESCOPED` + `Skipped` cho TC này (giữ dòng theo `§10.5`).

---

## TC-ORD-007: Check nhấn lại chip đang chọn không bỏ chọn giá trị — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở wizard NEED | tap card `Tôi cần gửi hàng` | ✅ PASS | — | — |
| 2 | Nhấn đúng chip đang được chọn | tap `accessibility id "Tài liệu"` | ✅ PASS | — | — |
| 3 | Check trạng thái 8 chip | ảnh: "Tài liệu" **vẫn** viền/chữ cam; không có trạng thái 8 chip đều bỏ chọn | ✅ PASS | `TC-ORD-007__verify-nhan-lai-chip-van-chon.png` | đúng `KB-VIBE-02` — không tái hiện được trạng thái "chưa chọn loại hàng" |
| 4 | Chọn giá trị hàng "Thấp" | tap `descriptionStartsWith("Thấp")` | ✅ PASS | — | — |
| 5 | Nhấn "Tiếp theo" | tap `Tiếp theo` → vẫn `Bước 1 / 3` | ❌ FAIL | `TC-ORD-007__step5-FAIL-khong-sang-buoc-2.png` | nút vẫn `enabled=false`; thiếu TRỌNG LƯỢNG + KÍCH THƯỚC + ảnh |

**Result: ❌ FAIL at Step 5**
**Reason:** Không sang được bước 2 khi chỉ chọn loại hàng + giá trị hàng.
**Evidence:** `screenshots/TC-ORD-007__verify-nhan-lai-chip-van-chon.png` (step 3 PASS) · `screenshots/TC-ORD-007__step5-FAIL-khong-sang-buoc-2.png` — cả 2 verified tồn tại
**Impact:** Điểm kiểm chứng **chính** (step 3 — hành vi chip) **PASS**. Chỉ step 5 fail và đúng **F1** ⇒ ⛔ không log bug; QC cập nhật Steps hoặc `DESCOPED` vế navigation.

---

## TC-ORD-008: Check chưa chọn giá trị hàng thì nút "Tiếp theo" bị khoá — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Mở wizard NEED, không chọn giá trị hàng | — | ✅ PASS | — | — |
| 3 | Check trạng thái nút "Tiếp theo" | get_element_attribute `enabled` → **false**; ảnh: nút bị làm mờ | ✅ PASS | — | ⚠️ `clickable` **không** dùng được để suy enable (bẫy **T4**) — dùng `enabled` |
| 4 | Nhấn "Tiếp theo" | tap → vẫn `Bước 1 / 3` | ✅ PASS | — | — |
| 5 | Chọn giá trị hàng "Thấp" | tap `descriptionStartsWith("Thấp")` | ✅ PASS | — | — |
| 6 | Check lại trạng thái nút | `enabled` → **vẫn false** | ❌ FAIL | `TC-ORD-008__step6-FAIL-tiep-theo-van-disable.png` | Expected: enable |

**Result: ❌ FAIL at Step 6**
**Reason:** Chọn xong giá trị hàng nút "Tiếp theo" **vẫn disable** — vì v1.1 còn bắt buộc TRỌNG LƯỢNG, KÍCH THƯỚC và ≥1 ảnh.
**Evidence:** `screenshots/TC-ORD-008__step6-FAIL-tiep-theo-van-disable.png` — verified tồn tại (thấy rõ "Thấp" đã chọn · 2 khối tier chưa chọn · `0/5` ảnh · nút mờ)
**Impact:** Đúng **F1** ⇒ ⛔ không log bug. Vế *"chưa chọn giá trị hàng thì khoá"* (step 3–4) **đúng**; chỉ điều kiện đủ để enable đã đổi theo v1.1.

---

## TC-ORD-009: Check chọn giá trị hàng "Cao" hiện banner cảnh báo đúng nguyên văn — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở wizard NEED | — | ✅ PASS | — | — |
| 2 | Chọn giá trị hàng "Cao" | tap `descriptionStartsWith("Cao, Trên 5")` | ✅ PASS | — | — |
| 3 | Check nội dung banner | get_text → *"Hàng giá trị cao: hai bên tự thoả thuận và chịu trách nhiệm với nhau. FoxEco không bảo hiểm, không đứng ra vận chuyển hay bồi thường."* | ✅ PASS | `TC-ORD-009__verify-banner-gia-tri-cao.png` | khớp **nguyên văn 100%** Expected; banner chữ đỏ ngay dưới nhóm chip |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-009__verify-banner-gia-tri-cao.png` — verified tồn tại
**Notes:** ⚠️ Banner này là cảnh báo theo **mức định tính "Cao"** — khác hoàn toàn banner **hàng cấm** mà `C-ORD-04` nói *"không có ở v1.1"* (banner hàng cấm thuộc `TC-ORD-035`, chưa chạy).
**Locators captured:** 1 (banner giá trị cao)

---

## TC-ORD-010: Check chọn giá trị hàng "Thấp" hoặc "Vừa" không hiện banner cảnh báo — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Mở wizard, chọn "Thấp" | tap `descriptionStartsWith("Thấp")` | ✅ PASS | — | — |
| 3 | Check vùng dưới nhóm giá trị hàng | find `textContains("giá trị cao")` → 🚫 NOT FOUND | ✅ PASS | — | ảnh của state này **không** tách được khỏi ảnh `TC-ORD-008` (cùng pixel) ⇒ ⛔ không chụp trùng md5, kết luận dựa trên phép tìm MCP |
| 4 | Chọn giá trị hàng "Vừa" | tap `descriptionStartsWith("Vừa, 1")` | ✅ PASS | — | — |
| 5 | Check lại vùng đó | find `textContains("thoả thuận")` → 🚫 NOT FOUND | ✅ PASS | `TC-ORD-010__verify-vua-khong-banner.png` | — |

**Result: ✅ PASS (5 steps, 2 expected)**
**Evidence:** `screenshots/TC-ORD-010__verify-vua-khong-banner.png` — verified tồn tại
**Notes:** Cặp đối chứng âm của `TC-ORD-009` khép kín: banner **chỉ** gắn mức "Cao".

---

## TC-ORD-013: Check khối ảnh hàng mang dấu bắt buộc và dòng helper nêu rõ ràng buộc — *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở wizard NEED | — | ✅ PASS | — | — |
| 2 | Check nhãn khối, bộ đếm, dòng helper khi chưa tải ảnh | get_text nhãn → **"ẢNH HÀNG *"** · find `text("0/5")` ✓ · get_text helper → *"Bắt buộc ít nhất 1 ảnh · tối đa 5 ảnh · giúp người vận chuyển nhận diện hàng"* | ✅ PASS | `TC-ORD-013__verify-anh-hang-bat-buoc-0-5.png` | cả 3 vế khớp **nguyên văn**; dấu `*` màu đỏ |

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-013__verify-anh-hang-bat-buoc-0-5.png` — verified tồn tại
**Notes:** Tầng UI của `BR01-01` đã build đúng. Tầng **hành vi chặn** là `TC-ORD-063` (chạy riêng, xem dưới).
**Locators captured:** 3 (nhãn khối, nút thêm ảnh `0/5`, dòng helper)

---

## TC-ORD-054: Check bước 1 không có field nhập số tiền hay ngưỡng giá trị hàng — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Mở wizard, cuộn toàn bước 1 | scroll hết form (2 page source + 4 ảnh) | ✅ PASS | — | thứ tự khối: LOẠI HÀNG → GHI CHÚ → THÔNG TIN HÀNG (3 nhóm chip) → ẢNH HÀNG |
| 3 | Tìm field nhập số tiền / ngưỡng | find `EditText instance(1)` → 🚫 NOT FOUND (chỉ có **1** EditText = Ghi chú) | ✅ PASS | — | mốc tiền chỉ là **nhãn phụ** của chip (`Dưới 1 triệu đ`…), không phải ô nhập |
| 4 | Chọn giá trị hàng "Cao" | tap `descriptionStartsWith("Cao, Trên 5")` | ✅ PASS | — | — |
| 5 | Check lại quanh nhóm giá trị hàng | find `EditText instance(1)` → 🚫 NOT FOUND | ✅ PASS | `TC-ORD-054__verify-khong-co-field-so-tien.png` | chỉ hiện **banner chữ**, không sinh ô nhập nào |

**Result: ✅ PASS (5 steps, 2 expected)**
**Evidence:** `screenshots/TC-ORD-054__verify-khong-co-field-so-tien.png` — verified tồn tại
**Notes:** Chốt đúng ranh giới `C-ORD-02`: ngưỡng bằng **số tiền** out of scope, cảnh báo theo **mức định tính** thì có (`TC-ORD-009`).

---

## TC-ORD-068: Check ảnh vượt năm MB bị từ chối và bộ đếm không tăng — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở wizard NEED | — | ✅ PASS | — | — |
| 2 | Nhấn vùng "ẢNH HÀNG" → chọn ảnh > 5MB | tap `accessibility id "0/5"` → `text("Chọn từ thư viện")` → picker: tap thumbnail instance 7 (**seed_jpg_over5mb** (6.291.456 B)) → `textStartsWith("Add")` | ✅ PASS | `TC-ORD-068__pre-chon-anh-6mb.png` | ảnh pre chứng minh đã chọn đúng 1 ảnh (nút "Add (1)") |
| 3 | Check thông báo + bộ đếm | get_text → *"Ảnh vượt quá 5MB, vui lòng chọn ảnh nhỏ hơn."* · find `accessibility id "0/5"` ✓ | ✅ PASS | `TC-ORD-068__verify-tu-choi-anh-6mb-0-5.png` | ⚠️ phải bấm lại menu `Chức năng` mới thấy được kết quả — xem **F2** |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-068__verify-tu-choi-anh-6mb-0-5.png` (+ `TC-ORD-068__pre-chon-anh-6mb.png`) — verified tồn tại
**Notes:** Cả 2 vế đúng: **từ chối kèm thông báo** + **bộ đếm vẫn 0/5**. Test data tự dựng (`/sdcard/Pictures/seed_*`), xem §Dữ liệu test dựng trong phiên ở `vibe-report.md`.
**Locators captured:** 1 (thông báo lỗi dung lượng ảnh)

---

## TC-ORD-069: Check file sai định dạng bị từ chối và bộ đếm không tăng — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở wizard NEED | — | ✅ PASS | — | — |
| 2 | Nhấn vùng "ẢNH HÀNG" → chọn file `.pdf` | tap `0/5` → bottom sheet chỉ có **`Chụp ảnh`** + **`Chọn từ thư viện`** → picker là **Android Photo Picker** (`com.google.android.providers.media.module`), **chỉ liệt kê ảnh** — `seed_doc.pdf` tồn tại thật trong `/sdcard/Pictures` nhưng **không xuất hiện** | 🚫 BLOCKED | `TC-ORD-069__step2-BLOCKED-picker-chi-co-anh.png` | picker hiện đúng 10 mục, **0** mục pdf (page source: 10 `icon_thumbnail`, không có node nào là pdf) |
| 3 | — | ⏭ SKIPPED | 🚫 | — | không tạo được tiền đề |

**Result: 🚫 BLOCKED at Step 2**
**Reason:** App **không có đường UI nào** để đưa file sai định dạng vào khối ảnh: cả 2 lối vào đều là ảnh (camera / photo picker của OS). Lọc định dạng nằm ở **tầng OS picker**, nên **không quan sát được** vế *"thông báo lỗi của app"*.
**Evidence:** `screenshots/TC-ORD-069__step2-BLOCKED-picker-chi-co-anh.png` — verified tồn tại
**Impact:** ⛔ **Không được PASS chỉ vì "không có đường thử"** (đúng tinh thần §0.4 #4 của fragment). Vế *"bộ đếm không tăng"* thì hiển nhiên đúng nhưng không kết luận được cả TC. 📨 Đề xuất QC: chuyển `⛔ N-A (không test được qua UI)` hoặc đổi Expected sang *"picker không cho chọn file không phải ảnh"*; cần BA/dev xác nhận tầng lọc định dạng có ở app hay chỉ dựa OS.

---

## 🔴 Phát hiện chung thứ 3 của phiên (bổ sung sau lô 2)

**F3 — CHẶN IM LẶNG: app khoá nút "Tiếp theo" nhưng KHÔNG hiện thông báo lỗi ở đúng trường thiếu/sai.**
Tái hiện ở **4 TC độc lập**, cùng một cơ chế:
| TC | Điều kiện | App chặn? | Có thông báo lỗi? |
|---|---|---|---|
| `TC-ORD-063` **(P1)** | thiếu ảnh | ✅ có (nút disable) | ❌ **không** ở khối `ẢNH HÀNG` |
| `TC-ORD-083` | địa chỉ giao trùng hệt địa chỉ lấy | ✅ có | ❌ **không** ở ô `Địa chỉ giao hàng` |
| `TC-ORD-084` | trùng, chỉ khác khoảng trắng đầu/cuối | ✅ có | ❌ **không** |
| `TC-ORD-064`/`066` | thiếu TRỌNG LƯỢNG / KÍCH THƯỚC | *(chạy ở lô 3)* | *(xem verdict từng TC)* |
⚠️ **Ngoại lệ chứng minh app CÓ cơ chế báo lỗi tại trường:** khối ảnh báo đúng khi **ảnh quá cỡ**
(`Ảnh vượt quá 5MB…` — `TC-ORD-068`) và khối buổi báo đúng khi chưa chọn (`Chọn ít nhất 1 buổi`).
⇒ Không phải "app không có cơ chế", mà là **thiếu ở đúng các nhánh trên** ⇒ 🐞 nhóm bug thật, không phải TC sai.
⇒ Người dùng cuối không biết vì sao không bấm được `Tiếp theo`. Cùng họ với `B2` (chặn lưu im lặng) của VR-001.

**F4 — KHÔNG có popup "Thoát và bỏ nội dung đã nhập?" ⇒ mất dữ liệu soạn dở không cảnh báo.**
Ở bước 1, nhấn `Quay lại` ⇒ **thoát wizard NGAY**, xoá sạch dữ liệu đã nhập, **không hỏi gì**.
Ở bước 2, nhấn `Quay lại` ⇒ **về bước 1** (không phải đóng wizard như Steps của `TC-ORD-053`/`062` giả định).
Trái `AC-01.2.01` + `C-ORD-08` (BA chốt assert **verbatim** chuỗi popup) ⇒ 🐞 bug thật (`TC-ORD-053` FAIL).
Cùng họ với `TC-USR-045` của VR-001 (*"Quay lại khi có thay đổi chưa lưu → về Cá nhân ngay, không hộp thoại"*) ⇒ nghi **một lỗi hệ thống chung**, không riêng ORD.

**F5 — Ràng buộc "email người nhận phải có trên HRIS" đã chặn đúng, nhưng CHUỖI HƯỚNG DẪN còn của v1.0.**
Email `@fpt.com` không có trên HRIS / đã nghỉ việc ⇒ nút `Tiếp theo` **disable kể cả khi đã điền tay đủ
tên + SĐT + địa chỉ giao** (đúng `C-ORD-14`). Nhưng app hiện chuỗi *"Không tìm thấy email này — **vui lòng
nhập tay thông tin bên dưới**."* — đúng câu chữ của `BR01-09` bản v1.0 mà `C-ORD-14` đã **đảo**.
⇒ Không đổi verdict (chặn = hành vi đúng, ⛔ không có ô nào *mở thêm*), nhưng là **text-defect gây hiểu sai**:
người dùng làm theo hướng dẫn rồi vẫn không đi tiếp được. 📨 Đề xuất raise clarification/text-defect cho BA.

---

## TC-ORD-012: Check tải một ảnh JPG hợp lệ hiện đúng bộ đếm một trên năm — *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở wizard NEED | — | ✅ PASS | — | — |
| 2 | Nhấn vùng "ẢNH HÀNG" → chọn 1 ảnh JPG nhỏ | tap `accessibility id "0/5"` → `text("Chọn từ thư viện")` → picker thumbnail instance 0 (**seed_jpg_1** — 27.762 B) → `textStartsWith("Add")` | ✅ PASS | `TC-ORD-012__pre-chon-1-anh-jpg.png` | — |
| 3 | Check ô ảnh + bộ đếm | find `accessibility id "1/5"` ✓ · ảnh thumbnail đỏ hiện trong ô kèm nút `×` | ✅ PASS | `TC-ORD-012__verify-bo-dem-1-5.png` | bộ đếm nằm **trên nút thêm ảnh**, đổi desc theo số ảnh (`0/5`→`1/5`…) |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-012__verify-bo-dem-1-5.png` (+ `TC-ORD-012__pre-chon-1-anh-jpg.png`) — verified tồn tại
**Locators captured:** 3 (`multi-photo-add-button`, `multi-photo-remove-<N>`, picker `icon_thumbnail` instance N)

---

## TC-ORD-014: Check không tải ảnh vẫn chuyển được sang bước 2 — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở wizard NEED | — | ✅ PASS | — | — |
| 2 | Chọn chip loại hàng "Giấy tờ, hồ sơ" | 🚫 chip này **không tồn tại** — app hiện `Tài liệu` (xem `TC-ORD-005`/`006`) | ❌ FAIL | — | thực hiện bằng chip mặc định `Tài liệu` để đi tiếp được |
| 3 | Chọn giá trị hàng "Thấp", không tải ảnh | tap `descriptionStartsWith("Thấp")` (+ `Dưới 5 kg`, `Nhỏ` để loại trừ nguyên nhân khác) | ✅ PASS | — | — |
| 4 | Nhấn "Tiếp theo" | `enabled=false`; tap → vẫn `Bước 1 / 3` | ❌ FAIL | `TC-ORD-014__step4-FAIL-khong-sang-buoc-2-khi-khong-co-anh.png` | Expected: sang bước 2, không lỗi về ảnh |

**Result: ❌ FAIL at Step 4 (step 2 cũng không thực hiện được như viết)**
**Reason:** Ảnh là **BẮT BUỘC** ở v1.1 (`BR01-01`), nên "không tải ảnh vẫn sang bước 2" không còn đúng.
**Evidence:** `screenshots/TC-ORD-014__step4-FAIL-khong-sang-buoc-2-khi-khong-co-anh.png` — verified tồn tại
**Impact:** 🔴 **TC hết hiệu lực (F1), KHÔNG phải lỗi app** — chính `TC-ORD-063` (v1.1, P1) khẳng định hành vi chặn này là **ĐÚNG**. Hai TC **mâu thuẫn trực tiếp** nhau ⇒ ⛔ không log bug; QC chốt `DESCOPED` cho `TC-ORD-014`. Nhãn chip trong Steps cũng đã lỗi thời.

---

## TC-ORD-027: Check ô địa chỉ lấy hàng điền sẵn địa chỉ mặc định của hồ sơ và sửa được — *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Ghi lại địa chỉ mặc định đang lưu | màn "Cập nhật thông tin" đầu phiên: **`363 Nguyễn Hữu Thọ, Cẩm Lệ`** | ✅ PASS | `_setup__preflight-launch.png` | ảnh preflight chụp đúng màn đó (`SEED-ORD-03` thoả) |
| 2 | Nhập đủ bước 1 → "Tiếp theo" | Tài liệu + Cao + Dưới 5 kg + Nhỏ + 1 ảnh → `Tiếp theo` (`enabled=true`) | ✅ PASS | — | — |
| 3 | Nhập thêm " toà B" vào cuối ô "Địa chỉ lấy hàng" | set_value `(//EditText)[3]` | ✅ PASS | — | — |
| 4 | Check giá trị ban đầu + sau khi sửa | get_text trước: `363 Nguyễn Hữu Thọ, Cẩm Lệ` (khớp step 1) · sau: `363 Nguyễn Hữu Thọ, Cẩm Lệ toà B` | ✅ PASS | `TC-ORD-027__verify-prefill-va-sua-duoc.png` | prefill là **hành vi đặc tả** (`C-ORD-10`), ô trống mới là bug — ở đây KHÔNG trống |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-027__verify-prefill-va-sua-duoc.png` — verified tồn tại
**Notes:** Bước 2 còn prefill đúng **tên** (`Đặng Châu Giang`) và **SĐT** (`0912345670`) của hồ sơ ⇒ đối chứng sẵn cho `TC-ORD-015`/`017` (carried, chưa chạy).
**Locators captured:** 3 (tên người gửi, SĐT người gửi, địa chỉ lấy hàng — đều `(//EditText)[n]`)

---

## TC-ORD-028: Check ô địa chỉ là ô văn bản tự do không phải preset văn phòng — *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 | — | ✅ PASS | — | — |
| 2-3 | Nhấn ô "Địa chỉ giao hàng" và nhập chuỗi tự do | set_value `//EditText[@hint="Địa chỉ giao hàng"]` = `Số 7 ngõ 12 Trần Duy Hưng` | ✅ PASS | — | — |
| 4 | Check kiểu control + giá trị | get_text = **đúng chuỗi vừa nhập** · find `address-suggestion-0` → 🚫 NOT FOUND (không có preset/chip gợi ý) | ✅ PASS | `TC-ORD-028__verify-o-van-ban-tu-do.png` | ⚠️ Khác hẳn ô "Địa chỉ mặc định" của module USR (ô đó **có** `address-suggestion-N`, xem bẫy **T5**) |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-028__verify-o-van-ban-tu-do.png` — verified tồn tại
**Notes:** Chốt `C-ORD-11`: ô tự do, ⛔ không phải preset 6 văn phòng.

---

## TC-ORD-055: Check ô địa chỉ nhận đúng hai trăm ký tự và chặn ký tự thứ hai trăm lẻ một — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 | — | ✅ PASS | — | — |
| 2 | Nhập đúng 200 ký tự vào ô "Địa chỉ giao hàng" | set_value chuỗi `So7ngo12TranDuyHung-` ×10 (=200 ký tự) → get_text: **nhận đủ 200** | ✅ PASS | — | page source: `max-text-length=200` |
| 3 | Nhập thêm 1 ký tự (`Z`) vào cuối | set_value `w3cActions=true` (gửi key vào ô đang focus ⇒ **append thật**, không replace) | ✅ PASS | — | — |
| 4 | Check số ký tự còn lại trong ô | get_text = **vẫn đúng 200 ký tự**, không có `Z` | ✅ PASS | `TC-ORD-055__verify-giu-dung-200-ky-tu.png` | — |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-055__verify-giu-dung-200-ky-tu.png` — verified tồn tại
**Notes:** Ảnh `__pre` bị **xoá có chủ ý**: màn hình không đổi pixel giữa "nhập 200" và "chặn ký tự 201" ⇒ 2 ảnh trùng md5, giữ cả 2 là evidence rỗng nghĩa. Kết luận dựa trên **get_text trước/sau**.

---

## TC-ORD-053: Check chọn ở lại ở popup thoát wizard giữ nguyên dữ liệu đã nhập — *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Vào bước 2, nhập "Số 9 Duy Tân" vào địa chỉ giao | set_value ✓ | ✅ PASS | — | — |
| 3 | Nhấn nút quay lại để **đóng wizard** | tap `Quay lại` ở **bước 2** → **KHÔNG đóng wizard**, chỉ **về bước 1** | ❌ FAIL | — | Steps giả định back = đóng wizard; app dùng back = lùi bước |
| 3b | (đi tiếp để tìm popup) nhấn `Quay lại` ở **bước 1** | → **thoát wizard NGAY** về màn "Đăng tin mới", dữ liệu mất sạch | ❌ FAIL | — | — |
| 4 | Check nội dung popup | find `textContains("Thoát")` → 🚫 **NOT FOUND** — **không có popup nào** | ❌ FAIL | `TC-ORD-053__step4-FAIL-khong-co-popup-thoat.png` | Expected: đúng chuỗi *"Thoát và bỏ nội dung đã nhập?"* |
| 5-6 | Nhấn "ở lại" → check ô địa chỉ giao | ⏭ SKIPPED | ❌ | — | không có popup ⇒ không có lựa chọn "ở lại" |

**Result: ❌ FAIL at Step 4**
**Reason:** Popup xác nhận thoát **không tồn tại**; app thoát thẳng và **xoá dữ liệu soạn dở không cảnh báo**.
**Evidence:** `screenshots/TC-ORD-053__step4-FAIL-khong-co-popup-thoat.png` — verified tồn tại
**Impact:** 🐞🔴 **Bug thật** (mất dữ liệu, không hỏi) — trái `AC-01.2.01` + `C-ORD-08`. Xem **F4**; cùng họ với `TC-USR-045` (VR-001) ⇒ đề nghị mở bug ở phạm vi **hệ thống**, không riêng wizard ORD.

---

## TC-ORD-062: Check chọn thoát ở popup mở lại wizard là form trắng không có bản nháp — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Vào bước 2, nhập "Số 9 Duy Tân" | ✓ | ✅ PASS | — | — |
| 3 | Đóng wizard rồi **chọn thoát trên popup** | không có popup ⇒ tap `Quay lại` ở bước 1 **thoát thẳng** (hệ quả tương đương "chọn thoát") | ⚠️ thực hiện lệch | — | defect popup do `TC-ORD-053` sở hữu, ⛔ không tính lỗi 2 lần |
| 4 | Tab "Hoạt động" + rà **cả 2 tab con** | tab `Đang diễn ra`: 3 đơn cũ (2 NEED `Chờ ghép`, 1 OFFER `Đã huỷ`) · tab `Đã hoàn thành` ✓ · find `textContains("háp")` → 🚫 NOT FOUND ở **cả 2 tab** | ✅ PASS | `TC-ORD-062__pre-hai-tab-khong-co-tin-nhap.png` | **không có tin nháp nào** |
| 5-6 | Mở lại wizard, check các ô | `Đăng tin` → card NEED → bước 1: ghi chú **rỗng** (`showing-hint=true`), 3 khối tier **chưa chọn**, ảnh `0/5`, `Tiếp theo` `enabled=false` | ✅ PASS | `TC-ORD-062__verify-form-trang-khong-nhap.png` | KHÔNG giữ `Số 9 Duy Tân`, không phục hồi nháp |

**Result: ✅ PASS (6 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-062__verify-form-trang-khong-nhap.png` (+ `TC-ORD-062__pre-hai-tab-khong-co-tin-nhap.png`) — verified tồn tại
**Notes:** Điểm kiểm chứng của TC (**không lưu nháp**) đạt. Ô bước 2 được kiểm lại ở lô 3 khi vào bước 2 từ wizard trắng — kết quả trùng khớp (mọi ô người nhận rỗng).

---

## TC-ORD-063: Check chưa tải ảnh nào thì bị chặn sang bước hai — *(v1.1 NEW · P1)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở wizard NEED (form trắng) | — | ✅ PASS | — | — |
| 2-4 | Chọn `Thấp` + `Dưới 5 kg` + `Nhỏ · Cầm tay` | tap 3 chip qua `descriptionStartsWith` | ✅ PASS | — | — |
| 5 | Nhấn "Tiếp theo" khi chưa tải ảnh | `enabled=false`; tap → vẫn `Bước 1 / 3` | ✅ PASS | — | **vế chặn ĐÚNG** |
| 6 | Check màn + thông báo lỗi ở khối "ẢNH HÀNG" | vẫn ở bước 1 ✓ · khối ảnh **chỉ có dòng helper tĩnh**, **KHÔNG có thông báo lỗi** nào | ❌ FAIL | `TC-ORD-063__step6-FAIL-chan-nhung-khong-co-thong-bao-loi.png` | Expected đòi **cả 2**: vẫn ở bước 1 **VÀ** có lỗi ở khối ảnh |

**Result: ❌ FAIL at Step 6 (P1)**
**Reason:** Chặn đúng nhưng **chặn im lặng** — không có thông báo lỗi ở khối `ẢNH HÀNG`.
**Evidence:** `screenshots/TC-ORD-063__step6-FAIL-chan-nhung-khong-co-thong-bao-loi.png` — verified tồn tại
**Impact:** 🐞🔴 **Ứng viên bug P1** (xem **F3**). Đây là oracle của cả cụm ảnh: `BR01-01` yêu cầu *"thiếu ảnh thì chặn sang bước 2"* — chặn có, **báo cho người dùng biết thì không**. Bằng chứng app *có* cơ chế báo lỗi tại khối này: nhánh ảnh quá 5MB báo đúng (`TC-ORD-068`).

---

## TC-ORD-068 / 069 — đã ghi ở lô 1 (xem trên)

## TC-ORD-070: Check tải đủ năm ảnh thì bộ đếm đạt trần và không thêm được ảnh thứ sáu — *(v1.1 NEW)*

> ♻️ **ĐÃ RECHECK 2026-09-18 chiều** — verdict lượt 1 (`🚫 BLOCKED`, "trần 4 ảnh") **bị bác bỏ**, xem khối *Recheck* dưới.
> Recheck chạy trên **emulator-5554**, tài khoản **MNV 00002352** (`Nguyễn Thị Thanh Thủy`) — ⚠️ khác tài khoản A của lượt 1;
> hành vi khối ảnh không phụ thuộc tài khoản nên vẫn dùng làm oracle, nhưng ghi lại để không khai nhầm.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở wizard NEED | — | ✅ PASS | — | — |
| 2 | Tải 5 ảnh hợp lệ vào khối "ẢNH HÀNG" | chọn **5 ảnh trong 1 lượt** ở Android Photo Picker (`Add (5)`) → app nhận **đủ 5** | ✅ PASS | — | ⚠️ sau khi picker đóng, host app FoxPro **nhảy sang tab THÔNG BÁO** (tái hiện lại spec-gap #1) — vào lại `Chức năng` → FoxEco thì wizard **giữ nguyên** 5 ảnh |
| 3 | Thử tải ảnh thứ 6 | ⛔ **không có đường UI** — ở mức 5 ảnh, tile "thêm ảnh" đã bị ẩn khỏi cuối dải | ✅ PASS | — | đúng `BR18-02` *"ẩn nút thêm khi đủ 5"* |
| 4 | Cuộn dải tới cuối rồi check bộ đếm + trạng thái ô thêm ảnh | ở mức 4 ảnh bộ đếm hiện **`4/5`** ✓ · ở mức 5 ảnh **ô thêm ảnh bị ẩn khỏi cuối dải** ✓ và **không còn bộ đếm trên màn** ✓ · không chọn được ảnh thứ 6 ✓ | ✅ PASS | `TC-ORD-070__verify-du-5-anh-an-o-them-anh.png` | khớp Expected **đã sửa 2026-09-18** |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-070__verify-du-5-anh-an-o-them-anh.png` — verified tồn tại
**Notes:** 🔑 **Verdict chốt sau 2 lần đổi** — `🚫 BLOCKED` (lượt 1, kết luận nhầm "trần 4 ảnh") → `❌ FAIL` (recheck, vì Expected cũ đòi bộ đếm `5/5`) → **`✅ PASS`** sau khi **QC GiangDC2 chốt 2026-09-18: hành vi hiện tại là ĐÚNG, đủ 5 ảnh thì bỏ bộ đếm luôn** ⇒ Expected đã sửa ở `TC-MASTER-v1.1` + fragment, bỏ vế `5/5`, chuyển mốc assert bộ đếm về `4/5`.
**Vì sao Expected cũ không thể đạt:** bộ đếm `n/5` được vẽ **bên trong ô "thêm ảnh"** ở cuối dải (xem bẫy `T7`); `BR18-02` vừa bắt *"ẩn nút thêm khi đủ 5"* vừa bắt *"hiện bộ đếm n/5"* ⇒ ở mức 5/5 hai vế **loại trừ nhau**. App chọn vế ẩn nút — QC xác nhận đó là hành vi mong muốn. ⛔ **Không log bug** (ứng viên **B3′** đã huỷ).

**🔴 Bác bỏ verdict lượt 1 (BLOCKED "trần 4 ảnh") — sai do công cụ, không phải do app:**

| Điều lượt 1 kết luận | Thực tế khi recheck |
|---|---|
| "app chỉ cho tải **4** ảnh" | ❌ Sai — app nhận **đủ 5 ảnh** |
| "`multi-photo-add-button` **biến mất khỏi cây**" | ❌ Sai ở mức 4 ảnh — tile thêm ảnh **nằm ở CUỐI dải cuộn ngang**, ở mức 4 ảnh nó **ngoài viewport** nên không được compose ⇒ không có trong accessibility tree. Ở mức 5 ảnh nó ẩn **đúng spec**. |
| "dải ảnh **không cuộn** (thử 3 kiểu swipe)" | ❌ Sai — dải **cuộn ngang bình thường**: `input swipe 950→150 @y=1836, 500ms` cuộn tới cuối dải ngay lần đầu |
| "ảnh thứ 4 **không xoá được** (`multi-photo-remove-3` NOT FOUND)" | ❌ Sai — cùng nguyên nhân off-screen; cuộn tới nơi thì ảnh thứ 4 và thứ 5 **đều có nút `×` và xoá được** |

⇒ Ứng viên bug **B3 (trần ảnh 4/5) BỊ HUỶ** — ⛔ không log bug. Ứng viên thay thế **B3′** (thiếu bộ đếm ở mức 5/5) cũng **BỊ HUỶ** ngày 2026-09-18 sau khi QC chốt hành vi hiện tại là đúng ⇒ **khối ảnh của ORD không còn bug nào**.
📌 Bài học locator cho `implement-automation`: dải ảnh là **danh sách cuộn ngang lazy** — phần tử ngoài viewport **không tồn tại trong cây**. ⛔ Không được suy *"không tìm thấy node"* = *"chức năng không có"*; phải cuộn dải rồi mới assert.

**Nhật ký lượt 1 (2026-09-18 sáng — giữ để truy vết, verdict đã thay):**
Tải **lần lượt** từng ảnh: `1/5` ✓ · `2/5` ✓ · `3/5` ✓ · tới ảnh thứ 4 thì không đọc được bộ đếm, `multi-photo-add-button` NOT FOUND, 3 kiểu cuộn ngang đều không ăn ⇒ kết luận nhầm là "trần 4 ảnh".
Ảnh lượt 1: `TC-ORD-070__step3-BLOCKED-khong-co-nut-them-sau-4-anh.png` *(giữ nguyên — là bằng chứng của chính cái bẫy công cụ này)*.

---

## TC-ORD-071: Check xoá một ảnh làm bộ đếm giảm đúng một đơn vị — *(v1.1 NEW)*

> ♻️ **ĐÃ RECHECK 2026-09-18 chiều** — verdict lượt 1 (`🚫 BLOCKED`) **bị bác bỏ**: tiền đề "5 ảnh" **dựng được bình thường**.
> Cùng phiên/thiết bị/tài khoản với recheck của `TC-ORD-070`.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Tải **5 ảnh** hợp lệ *(setup)* | chọn 5 ảnh 1 lượt ở picker → dải có đủ 5: đỏ · xanh dương · xanh lá · vàng · tím | ✅ PASS | — | thứ tự dải = thứ tự chọn |
| 3 | Nhấn nút xoá trên **ảnh thứ ba** | tap `×` trên ảnh **xanh lá** (vị trí 3) | ✅ PASS | `TC-ORD-071__pre-vua-xoa-anh-thu-ba.png` | còn lại đúng đỏ · xanh dương · vàng · tím — **mất đúng ảnh thứ ba**, ⛔ không phải ảnh cuối |
| 4 | Check bộ đếm, số ảnh còn lại, trạng thái nút thêm | cuộn dải tới cuối: **`4/5`** ✓ · còn **4 ảnh** ✓ · tile **"thêm ảnh" hiện lại** ✓ | ✅ PASS | `TC-ORD-071__verify-bo-dem-4-tren-5-nut-them-hien-lai.png` | — |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-071__verify-bo-dem-4-tren-5-nut-them-hien-lai.png` (+ `TC-ORD-071__pre-vua-xoa-anh-thu-ba.png`) — verified tồn tại
**Notes:** Bắt đúng lỗi mà TC nhắm tới (*"xoá nhầm ảnh cuối thay vì ảnh được chọn"*) — app xoá **đúng ảnh được chọn**. Cùng kết luận với `TC-ORD-087` (mức 2 ảnh), nay có thêm bằng chứng ở **mức 5 ảnh**.
**Nhật ký lượt 1 (2026-09-18 sáng — verdict đã thay):** BLOCKED vì tin rằng không dựng nổi 5 ảnh (hệ quả của kết luận nhầm ở `TC-ORD-070`). Ảnh lượt 1: `TC-ORD-071__step2-BLOCKED-toi-da-4-anh.png` *(giữ nguyên)*.

---

## TC-ORD-074: Check nhập email có trên danh bạ tự điền ba trường và cả ba vẫn sửa được — *(v1.1 NEW · P1)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 | — | ✅ PASS | — | — |
| 2-3 | Nhập `stag_anhdc4@fpt.com` rồi rời ô | set_value + `hideKeyboard` | ✅ PASS | `TC-ORD-074__pre-nhap-email-danh-ba.png` | app tra danh bạ ngay, hiện dòng xanh *"Đã tìm thấy trong hệ thống nội bộ · vui lòng bổ sung SĐT/địa chỉ giao còn thiếu."* |
| 4 | Nhập thêm ký tự "X" vào cuối ô tên | set_value `receiver-name-input` = `Đặng Châu AnhX` → get_text khớp | ✅ PASS | — | ⇒ ô tên **sửa được** |
| 5 | Check 3 ô tên / SĐT / địa chỉ giao | **Tên** = `Đặng Châu Anh` ✓ tự điền · **SĐT** = `0343439724` ✓ tự điền · **Địa chỉ giao** = **RỖNG** ✗ | ❌ FAIL | `TC-ORD-074__step5-FAIL-dia-chi-giao-khong-tu-dien.png` | Expected: **cả ba** ô tự điền khác rỗng |

**Result: ❌ FAIL at Step 5 (P1)**
**Reason:** Chỉ **2/3** ô được tự điền; ô "Địa chỉ giao hàng" vẫn rỗng và app yêu cầu người dùng tự bổ sung.
**Evidence:** `screenshots/TC-ORD-074__step5-FAIL-dia-chi-giao-khong-tu-dien.png` (+ `TC-ORD-074__pre-nhap-email-danh-ba.png`) — verified tồn tại
**Impact:** 🐞 **Ứng viên bug — nhưng cần BA chốt trước khi log.** Hai khả năng loại trừ nhau: (a) HRIS **có** địa chỉ làm việc cho mọi CBNV đang làm việc (`USR-accounts.md §2`: `HCM LôB3,E-Office,KCN TânThuận`) ⇒ app **phải** prefill ⇒ bug app; (b) spec chỉ autofill **tên + SĐT**, còn "địa chỉ giao" cố ý để người gửi nhập ⇒ **TC/spec lệch**, sửa Expected. Chính app đang tự khai (b) bằng dòng *"vui lòng bổ sung SĐT/địa chỉ giao còn thiếu"*. 📨 Route `/analyze-requirements --module ORD` + hỏi BA (`AC-04.x`).

---

## TC-ORD-075: Check email đúng tên miền công ty nhưng không có trên danh bạ thì chặn tạo đơn — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 | — | ✅ PASS | — | — |
| 2-3 | Nhập `stag_khongtontai9999@fpt.com` rồi rời ô | set_value + hideKeyboard | ✅ PASS | — | app hiện dòng đỏ *"Không tìm thấy email này — vui lòng nhập tay thông tin bên dưới."* |
| 4 | Check nút "Tiếp theo" + 3 ô | `enabled=false` **kể cả sau khi đã điền tay đủ** tên + SĐT + địa chỉ giao + chọn buổi ⇒ **chặn tạo đơn** ✓ · **KHÔNG có ô nào mở thêm** (3 ô vốn đã có sẵn từ đầu bước 2, xem `TC-ORD-062`) ✓ | ✅ PASS | `TC-ORD-075__verify-email-la-chan-tao-don.png` | ⚠️ phải **loại trừ nhiễu** trước khi kết luận: nút còn bị khoá bởi *địa chỉ giao rỗng* và *chưa chọn buổi* — đã điền/chọn đủ 2 thứ đó rồi mới đọc lại `enabled` |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-075__verify-email-la-chan-tao-don.png` — verified tồn tại
**Notes:** Đúng `C-ORD-14` (đảo `BR01-09`). 🚩 Nhưng **chuỗi hướng dẫn còn của v1.0** (*"vui lòng nhập tay…"*) — xem **F5**: không đổi verdict, cần raise text-defect.

---

## TC-ORD-076: Check email của người đã nghỉ việc cũng chặn tạo đơn — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 | — | ✅ PASS | — | — |
| 2-3 | Nhập `stag_binhnt23@fpt.com` (MNV 00026682, đã nghỉ việc) rồi rời ô | set_value + hideKeyboard | ✅ PASS | — | `SEED-ORD-02` ② — data QC cấp trong `DOC-v1.1-05` |
| 4 | Check nút "Tiếp theo" + 3 ô | `enabled=false` ⇒ chặn ✓ · không ô nào mở thêm ✓ · dòng đỏ *"Không tìm thấy email này…"* | ✅ PASS | `TC-ORD-076__verify-email-nghi-viec-chan.png` | app **không phân biệt** "nghỉ việc" với "không tồn tại" — cùng 1 chuỗi; đúng kỳ vọng (cùng chặn) nhưng đáng ghi nhận |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-076__verify-email-nghi-viec-chan.png` — verified tồn tại
**Notes:** Gỡ xong nợ data #2 của fragment §0.4 (email người nghỉ việc) ⇒ TC này **không còn Blocked** như dự kiến ban đầu.

---

## TC-ORD-083: Check địa chỉ giao trùng hệt địa chỉ lấy bị chặn — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 (email hợp lệ `stag_anhdc4@fpt.com`, đã chọn buổi) | — | ✅ PASS | — | phải dùng email **tra được** để loại nhiễu của `C-ORD-14` |
| 2-3 | Địa chỉ lấy = địa chỉ giao = `Số 7 ngõ 12 Trần Duy Hưng` | set_value 2 ô | ✅ PASS | `TC-ORD-083__pre-hai-dia-chi-trung-het.png` | — |
| 4 | Nhấn "Tiếp theo" | `enabled=false`; tap → vẫn `Bước 2 / 3` | ✅ PASS | — | **vế chặn ĐÚNG** |
| 5 | Check màn + thông báo lỗi ở ô địa chỉ giao | vẫn bước 2 ✓ · find `textContains("trùng")` → 🚫 NOT FOUND · **không có lỗi nào** dưới ô | ❌ FAIL | `TC-ORD-083__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png` | — |

**Result: ❌ FAIL at Step 5**
**Reason:** Chặn im lặng — không có thông báo lỗi ở ô "Địa chỉ giao hàng".
**Evidence:** `screenshots/TC-ORD-083__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png` (+ `TC-ORD-083__pre-hai-dia-chi-trung-het.png`) — verified tồn tại
**Impact:** 🐞 Ứng viên bug — cùng nhóm **F3** với `TC-ORD-063`/`084`. Rule `BR` *"địa chỉ giao ≠ địa chỉ lấy"* **được thi hành đúng**, chỉ thiếu phản hồi cho người dùng.

---

## TC-ORD-084: Check địa chỉ giao chỉ khác khoảng trắng đầu cuối vẫn bị chặn — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Như `TC-ORD-083`, địa chỉ lấy = `Số 7 ngõ 12 Trần Duy Hưng` | — | ✅ PASS | — | — |
| 3 | Địa chỉ giao = `"  Số 7 ngõ 12 Trần Duy Hưng  "` (thêm 2 space đầu + 2 space cuối) | set_value → get_text giữ **nguyên cả khoảng trắng** | ✅ PASS | — | ô **không tự trim** giá trị hiển thị |
| 4 | Nhấn "Tiếp theo" | `enabled=false` ⇒ vẫn bước 2 | ✅ PASS | — | ⇒ **so sánh có trim** ở tầng validate |
| 5 | Check màn + thông báo lỗi | vẫn bước 2 ✓ · **không có thông báo lỗi** | ❌ FAIL | `TC-ORD-084__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png` | — |

**Result: ❌ FAIL at Step 5**
**Reason:** Giống `TC-ORD-083`: chặn đúng (kể cả biên khoảng trắng) nhưng **không báo lỗi**.
**Evidence:** `screenshots/TC-ORD-084__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png` — verified tồn tại
**Impact:** 🐞 Cùng bug với `TC-ORD-083` ⇒ ⛔ **không mở bug riêng**, gộp 1 bug với 3 TC dẫn chứng (`063`/`083`/`084`).

---

## TC-ORD-087: Check xoá được ảnh khi đang soạn tin chưa đăng — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở wizard NEED | — | ✅ PASS | — | — |
| 2 | Tải 2 ảnh hợp lệ | picker instance 0 (đỏ) + instance 1 (xanh) → bộ đếm `2/5`, mỗi ảnh có nút `×` | ✅ PASS | `TC-ORD-087__pre-chon-anh-thu-2.png` | — |
| 3 | Nhấn nút xoá trên ảnh **thứ nhất** | tap `-android uiautomator resourceId("multi-photo-remove-0")` ⚠️ strategy `id` **NOT FOUND** (bẫy **T2**) | ✅ PASS | — | — |
| 4 | Check số ảnh còn lại + bộ đếm | còn **đúng 1 ảnh** và là **ảnh xanh** (ảnh thứ 2) ⇒ xoá đúng ảnh được chọn · find `accessibility id "1/5"` ✓ | ✅ PASS | `TC-ORD-087__verify-xoa-anh-1-con-1-5.png` | — |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-087__verify-xoa-anh-1-con-1-5.png` (+ `TC-ORD-087__pre-chon-anh-thu-2.png`) — verified tồn tại
**Notes:** Đối chứng với `TC-ORD-088` (chưa chạy). Ở mức 2 ảnh cơ chế xoá **đúng ảnh + giảm đúng 1** hoạt động; ⛔ không suy ra mức 5 ảnh (xem `TC-ORD-070`/`071` BLOCKED).
**Locators captured:** 1 (`multi-photo-remove-<N>`)

---

## 🔴 Phát hiện chung thứ 6 của phiên (lô 3)

**F6 — `appium_mobile_keyboard(action=hide)` gửi BACK ⇒ ở bước 1 wizard = THOÁT + mất dữ liệu.**
Giữa lô 3, một lệnh `hide` khi đang ở **bước 1** làm app thoát thẳng ra màn "Đăng tin mới" và **xoá draft**
(đúng hành vi **F4**). ⇒ 2 hệ quả: (a) thêm 1 bằng chứng độc lập cho bug F4; (b) **ghi chú kỹ thuật cho
`implement-automation`**: ⛔ **đừng dùng `hide` để rời ô trong wizard** — dùng `tap` vào vùng trống hoặc
đọc giá trị trực tiếp. Dữ liệu của `TC-ORD-011` đã verify **xong trước** khi mất, verdict không bị ảnh hưởng.

**F7 — App CÓ báo lỗi inline ở 3 chỗ, KHÔNG báo ở 4 chỗ** (bảng đối chứng của F3, hoàn chỉnh sau lô 3):
| Có báo lỗi ✅ | Không báo lỗi ❌ |
|---|---|
| ảnh > 5MB → *"Ảnh vượt quá 5MB, vui lòng chọn ảnh nhỏ hơn."* (`TC-ORD-068`) | thiếu ảnh (`TC-ORD-063` **P1**) |
| chưa chọn buổi → *"Chọn ít nhất 1 buổi"* (`TC-ORD-058`) | thiếu TRỌNG LƯỢNG (`TC-ORD-064`) |
| khoảng ngày > 7 → *"Đến ngày tối đa 7 ngày kể từ Từ ngày"* (`TC-ORD-057`) | thiếu KÍCH THƯỚC (`TC-ORD-066`) |
| | địa chỉ giao trùng địa chỉ lấy (`TC-ORD-083`/`084`) · email sai định dạng (`TC-ORD-077`) |
⇒ Kết luận cho bug report: **không phải thiếu framework báo lỗi**, mà **bỏ sót đúng 5 nhánh validate**.

---

## TC-ORD-011: Check ghi chú nhận đúng 300 ký tự và chặn ký tự thứ 301 — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở wizard NEED | — | ✅ PASS | — | — |
| 2 | Nhập chuỗi đúng 300 ký tự vào ô Ghi chú | set_value → get_text: nhận **đủ 300** | ✅ PASS | — | `max-text-length=300` |
| 3 | Chọn giá trị hàng "Thấp" | ✓ | ✅ PASS | — | — |
| 4 | Nhấn "Tiếp theo" | sang **Bước 2 / 3** ✓ | ✅ PASS | — | ⚠️ **setup mở rộng theo v1.1**: thêm `Dưới 5 kg` + `Nhỏ` + 1 ảnh mới enable được nút (F1). ⛔ Không đổi điểm kiểm chứng của TC |
| 5 | Nhấn quay lại bước 1 | tap `Quay lại` → về bước 1, ghi chú **còn nguyên 300 ký tự** | ✅ PASS | — | — |
| 6 | Nhập tiếp 1 ký tự (`Z`) | set_value `w3cActions=true` (append thật) | ✅ PASS | — | — |
| 7 | Check độ dài nội dung ô Ghi chú | get_text = **vẫn đúng 300 ký tự**, không có `Z` | ✅ PASS | `TC-ORD-011__verify-ghi-chu-dung-300-ky-tu.png` | — |

**Result: ✅ PASS (7 steps, 2 expected)**
**Evidence:** `screenshots/TC-ORD-011__verify-ghi-chu-dung-300-ky-tu.png` — verified tồn tại
**Notes:** Ghi chú **sống sót** qua vòng bước 1 → bước 2 → bước 1 (điểm mà TC muốn kiểm).

---

## TC-ORD-015: Check bước 2 tự điền tên và SĐT người gửi từ hồ sơ — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Ghi lại tên hiển thị của hồ sơ | **`Đặng Châu Giang`** (màn Cá nhân/Cập nhật thông tin đầu phiên) | ✅ PASS | — | — |
| 2 | Vào bước 2 | (setup v1.1: + trọng lượng + kích thước + 1 ảnh) | ✅ PASS | — | F1 |
| 3 | Check 2 field nhóm "Người gửi" | tên = `Đặng Châu Giang` ✓ khớp step 1 · SĐT = `0912345670` ✓ điền sẵn | ✅ PASS | `TC-ORD-015__verify-tu-dien-ten-va-sdt-nguoi-gui.png` | — |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-015__verify-tu-dien-ten-va-sdt-nguoi-gui.png` — verified tồn tại
**Locators captured:** 2 (`(//EditText)[1]` tên người gửi · `(//EditText)[2]` SĐT người gửi)

---

## TC-ORD-016: Check field tên người gửi chỉ đọc, không bị xoá khi chạm — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Vào bước 2, ghi lại giá trị field tên | `Đặng Châu Giang` | ✅ PASS | — | — |
| 3 | Chạm vào field tên người gửi | tap `(//EditText)[1]` | ✅ PASS | — | — |
| 4 | Check bàn phím + giá trị | `isKeyboardShown` = **false** ⇒ bàn phím KHÔNG mở ✓ · get_text vẫn `Đặng Châu Giang`, không bị xoá trắng ✓ | ✅ PASS | `TC-ORD-016__verify-ten-chi-doc-khong-mo-ban-phim.png` | — |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-016__verify-ten-chi-doc-khong-mo-ban-phim.png` — verified tồn tại
**Notes:** Ảnh chụp ở **offset cuộn khác** ảnh của `TC-ORD-015` — chạm field chỉ-đọc không đổi pixel nào, nếu chụp cùng offset thì 2 ảnh trùng md5 (⛔ cấm dùng 1 bằng chứng cho 2 TC).

---

## TC-ORD-017: Check field địa chỉ lấy hàng điền sẵn theo nơi làm việc — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Check hồ sơ có thông tin nơi làm việc | hồ sơ A có **địa chỉ mặc định** `363 Nguyễn Hữu Thọ, Cẩm Lệ` | ✅ PASS | — | — |
| 2 | Vào bước 2 | (setup v1.1) | ✅ PASS | — | — |
| 3 | Check giá trị field địa chỉ lấy hàng | = `363 Nguyễn Hữu Thọ, Cẩm Lệ` — **giá trị thật, không phải placeholder** ✓ | ✅ PASS | `TC-ORD-017__verify-prefill-dia-chi-lay-hang.png` | — |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-017__verify-prefill-dia-chi-lay-hang.png` — verified tồn tại
**Notes:** 🚩 **Câu chữ v1.0 đã lỗi thời, nhưng hành vi ĐÚNG theo oracle mới.** TC ghi *"địa chỉ **nơi làm việc**"*; nguồn prefill thực tế là **địa chỉ mặc định của hồ sơ** (`C-ORD-10` + `TC-ORD-027` v1.1). Địa chỉ HRIS của A là `HCM LôB3,E-Office,KCN TânThuận` (`USR-accounts.md §2`) — **khác** giá trị prefill. ⇒ PASS theo vế *"được điền sẵn, không phải placeholder"*; 📨 đề nghị QC sửa câu chữ Steps/Expected của `TC-ORD-017` cho khớp `C-ORD-10`.

---

## TC-ORD-018: Check SĐT người gửi không tự đổi giá trị trong cùng phiên — *(CARRIED v1.0)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Vào bước 2, ghi lại SĐT người gửi | `0912345670` | ✅ PASS | — | — |
| 3 | Nhập email người nhận | `stag_anhdc4@fpt.com` (tra được, autofill tên + SĐT người nhận) | ✅ PASS | — | — |
| 4 | Nhập địa chỉ lấy + địa chỉ giao | lấy: giữ prefill · giao: `Số 9 Duy Tân` | ✅ PASS | — | — |
| 5 | Chọn ngày và khung giờ | ngày mặc định `Hôm nay – Hôm nay` · buổi `Chiều (13–17h)` | ✅ PASS | — | — |
| 6-7 | Cuộn lại nhóm "Người gửi", check SĐT | get_text = **`0912345670`** — **không đổi** | ✅ PASS | `TC-ORD-018__verify-sdt-nguoi-gui-khong-doi.png` | ⚠️ SĐT **người nhận** bị autofill ghi đè khi đổi email — nhưng đó là field khác, không thuộc TC này |

**Result: ✅ PASS (7 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-018__verify-sdt-nguoi-gui-khong-doi.png` — verified tồn tại

---

## TC-ORD-030: Check chọn ngày quá khứ cho Từ ngày bị chặn — *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 | — | ✅ PASS | — | — |
| 2 | Nhấn ô "Từ ngày" mở bộ chọn ngày | tap `descriptionStartsWith("Từ ngày")` → calendar `Tháng 9 2026`, hôm nay **18** đang chọn | ✅ PASS | — | — |
| 3 | Chọn ngày liền trước ngày hiện tại | tap `text("17")` | ✅ PASS | — | ngày 1–17 hiển thị **mờ (disabled)** |
| 4 | Check giá trị ô "Từ ngày" + lỗi | tap **không có tác dụng**: ngày chọn vẫn là **18**, ô giữ `Hôm nay` | ✅ PASS | `TC-ORD-030__verify-chan-ngay-qua-khu.png` | đúng Expected nhánh *"ô giữ nguyên trạng thái"* |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-030__verify-chan-ngay-qua-khu.png` — verified tồn tại
**Locators captured:** 3 (ô `Từ ngày`, ô `Đến ngày`, nút `Đóng` của date picker + ô ngày theo `text("<số>")`)

---

## TC-ORD-031: Check chọn Đến ngày sớm hơn Từ ngày bị chặn — *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Vào bước 2, chọn "Từ ngày" = hiện tại + 3 (**21/09/2026**) | tap `Từ ngày` → `text("21")` | ✅ PASS | — | — |
| 3 | Nhấn "Đến ngày", chọn hiện tại + 1 (**19/09**) | tap `Đến ngày` → `text("19")` | ✅ PASS | — | trong picker `Đến ngày`, ngày **19 và 20 đã chuyển mờ (disabled)** ngay sau khi Từ ngày = 21 |
| 4 | Check giá trị ô "Đến ngày" + lỗi | tap **không có tác dụng** — giá trị vẫn là ngày đã chọn trước đó (26/09), ⛔ không nhận 19/09 | ✅ PASS | `TC-ORD-031__verify-chan-den-ngay-som-hon.png` | — |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-031__verify-chan-den-ngay-som-hon.png` — verified tồn tại
**Notes:** App chặn **ở tầng picker** (làm mờ ngày không hợp lệ) ⇒ `BR01-04` *"Đến ≥ Từ"* được thi hành.

---

## TC-ORD-056: Check khoảng đúng bảy ngày được chấp nhận — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Vào bước 2, "Từ ngày" = hôm nay | mặc định `Hôm nay` (18/09) | ✅ PASS | — | — |
| 3 | Chọn "Đến ngày" = hôm nay + 7 | tap `Đến ngày` → `text("25")` | ✅ PASS | — | — |
| 4 | Check 2 ô ngày + lỗi | `Từ ngày` = `Hôm nay` · `Đến ngày` = **`25/09/2026`** ✓ · **KHÔNG có** thông báo lỗi nào về khoảng ngày | ✅ PASS | `TC-ORD-056__verify-khoang-7-ngay-duoc-nhan.png` | — |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-056__verify-khoang-7-ngay-duoc-nhan.png` — verified tồn tại
**Notes:** Biên trên **hợp lệ** đúng `C-ORD-15(a)` (*"Từ X → Đến tối đa X+7"*). Cặp với `TC-ORD-057`.

---

## TC-ORD-057: Check khoảng tám ngày bị chặn — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Vào bước 2, "Từ ngày" = hôm nay | ✓ | ✅ PASS | — | — |
| 3 | Chọn "Đến ngày" = hôm nay + 8 | tap `Đến ngày` → `text("26")` | ✅ PASS | — | ngày 26 **không bị làm mờ** trong picker ⇒ chọn được |
| 4 | Check giá trị ô "Đến ngày" + lỗi | ô **nhận** `26/09/2026` **nhưng** hiện lỗi đỏ ngay dưới khối: *"Đến ngày tối đa 7 ngày kể từ Từ ngày"* | ✅ PASS | `TC-ORD-057__verify-loi-toi-da-7-ngay.png` | Expected có **hoặc**: *"không được nhận **HOẶC** hiện lỗi ngay dưới ô"* ⇒ nhánh 2 thoả |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-057__verify-loi-toi-da-7-ngay.png` — verified tồn tại
**Notes:** 🔑 Đây là **ca đối chứng quan trọng cho F3/F7**: cùng 1 app, khối ngày **có** báo lỗi inline đúng chuẩn ⇒ 5 nhánh im lặng kia là **bỏ sót**, không phải giới hạn thiết kế.

---

## TC-ORD-058: Check buổi mong muốn mặc định là Sau giờ làm khi vừa mở bước hai — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 từ wizard **trắng** | — | ✅ PASS | — | bắt buộc state sạch: TC assert *"khi chưa chạm vào field"* |
| 2 | Check buổi đang được chọn sẵn | **KHÔNG buổi nào** được chọn; app hiện luôn lỗi đỏ *"Chọn ít nhất 1 buổi"* | ❌ FAIL | `TC-ORD-058__verify-buoi-mac-dinh.png` | Expected: `Sau giờ làm (17–19)` **chọn sẵn** |

**Result: ❌ FAIL at Step 2**
**Reason:** Field buổi mong muốn **không có giá trị mặc định**; 4 lựa chọn đều trống.
**Evidence:** `screenshots/TC-ORD-058__verify-buoi-mac-dinh.png` — verified tồn tại
**Impact:** 🐞 Ứng viên bug (mức thấp) — `§8.1.4` PRD v1.1 gọi tên rõ giá trị mặc định, và Notes của TC chốt trước *"app hiện buổi khác ⇒ FAIL và log bug"*. Ở đây còn nặng hơn: **không có** mặc định nào. ⚠️ Nhãn app là `Sau giờ làm (17–19h)` (có `h`), TC ghi `(17–19)` — ⛔ không phải nguyên nhân FAIL.

---

## TC-ORD-059: Check buổi đã trôi qua trong ngày hôm nay bị chặn chọn — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 | — | ✅ PASS | — | ⏰ giờ chạy **13:44** ⇒ buổi `Sáng (8–12h)` **đã trôi qua** (thoả pre-condition *"sau 12 giờ trưa"*) |
| 2 | "Từ ngày" = "Đến ngày" = ngày hiện tại | mặc định `Hôm nay – Hôm nay` ✓ | ✅ PASS | — | — |
| 3 | Nhấn chọn buổi "Sáng (8–12h)" | `enabled=true`; tap | ✅ PASS | — | — |
| 4 | Check trạng thái chọn của buổi "Sáng" | **CHỌN ĐƯỢC** — chip chuyển sang trạng thái đã chọn (viền + chữ cam) | ❌ FAIL | `TC-ORD-059__step4-FAIL-chon-duoc-buoi-da-qua.png` | Expected: không chọn được / bị vô hiệu hoá |

**Result: ❌ FAIL at Step 4**
**Reason:** App **cho chọn buổi đã trôi qua** trong ngày hôm nay (13:44 vẫn chọn được `Sáng 8–12h`).
**Evidence:** `screenshots/TC-ORD-059__step4-FAIL-chon-duoc-buoi-da-qua.png` — verified tồn tại
**Impact:** 🐞 Ứng viên bug — trái `C-ORD-15(b)` (BA chốt 2026-09-17: *"app CHẶN chọn buổi đã qua trong ngày"*). Rule này **không có trong PRD**, câu trả lời BA là nguồn duy nhất ⇒ khi log bug **phải dẫn `C-ORD-15(b)`**, nếu không dev sẽ bác vì không có trong tài liệu.

---

## TC-ORD-064: Check chưa chọn Trọng lượng thì bị chặn và ba chip hiện đúng nhãn chính thức — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Wizard trắng: chọn `Thấp` + `Nhỏ · Cầm tay` + tải 1 ảnh JPG, **không chạm** khối TRỌNG LƯỢNG | (wizard mới để chip trọng lượng chắc chắn chưa chọn — chip **không bỏ chọn được** sau khi đã chọn) | ✅ PASS | — | — |
| 5 | Nhấn "Tiếp theo" | `enabled=false`; tap → vẫn `Bước 1 / 3` | ✅ PASS | — | vế **chặn ĐÚNG** |
| 6 | Check nhãn khối + 3 chip + thông báo lỗi | nhãn = **"TRỌNG LƯỢNG"** ✓ · 3 chip = **`Dưới 5 kg (Nhẹ)`** · **`5 – 10 kg (Trung bình)`** · **`Trên 10 kg (Nặng)`** ✓ (khớp `C-ORD-18`, ⛔ app KHÔNG dùng "Khối lượng" như PRD) · **KHÔNG có thông báo lỗi** ở khối | ❌ FAIL | `TC-ORD-064__step6-FAIL-chan-nhung-khong-co-thong-bao-loi.png` | — |

**Result: ❌ FAIL at Step 6**
**Reason:** 2/3 vế đúng (chặn + nhãn), **thiếu vế thông báo lỗi** ở khối TRỌNG LƯỢNG.
**Evidence:** `screenshots/TC-ORD-064__step6-FAIL-chan-nhung-khong-co-thong-bao-loi.png` — verified tồn tại
**Impact:** 🐞 Cùng bug **F3** với `TC-ORD-063`/`066`/`083`/`084`. 🎉 Tin tốt: **nhãn "Trọng lượng" + phụ đề Nhẹ/Trung bình/Nặng đúng y hệt oracle UI** ⇒ ⛔ không có defect nhãn như §0.2 fragment dự phòng.

---

## TC-ORD-066: Check chưa chọn Kích thước thì bị chặn và ba chip hiện đúng nhãn — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Wizard trắng: chọn `Thấp` + `Dưới 5 kg` + tải 1 ảnh, **không chạm** khối Kích thước | ✓ | ✅ PASS | — | — |
| 4 | Nhấn "Tiếp theo" | `enabled=false`; tap → vẫn bước 1 | ✅ PASS | — | vế **chặn ĐÚNG** |
| 5 | Check 3 chip Kích thước + thông báo lỗi | 3 chip = **`Nhỏ · Cầm tay`** · **`Vừa · ~20×20 cm`** · **`Lớn · > 20×20 cm`** ✓ khớp Expected · **KHÔNG có thông báo lỗi** | ❌ FAIL | `TC-ORD-066__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png` | kiểu control là **chip**, ⛔ không phải Dropdown (đúng `C-ORD-18`) |

**Result: ❌ FAIL at Step 5**
**Reason:** Chặn + nhãn đúng, **thiếu thông báo lỗi** ở khối KÍCH THƯỚC.
**Evidence:** `screenshots/TC-ORD-066__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png` — verified tồn tại
**Impact:** 🐞 Cùng bug **F3**.

---

## TC-ORD-077: Check email sai định dạng bị chặn và không kích hoạt tra danh bạ — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 từ wizard **trắng** | — | ✅ PASS | — | cần state sạch để kiểm *"3 ô vẫn TRỐNG"* |
| 2-3 | Nhập `stag_anhdc4@` rồi rời ô | set_value + hideKeyboard | ✅ PASS | — | — |
| 4 | Check lỗi ở ô email + 3 ô kia | 3 ô tên/SĐT/địa chỉ giao **vẫn TRỐNG** ✓ (không tra danh bạ) · nhưng ô email **KHÔNG hiện lỗi định dạng** nào (find `textContains("mail")` → 🚫 NOT FOUND) | ❌ FAIL | `TC-ORD-077__step4-FAIL-khong-co-loi-dinh-dang.png` | so sánh: email **đủ định dạng nhưng không tra thấy** thì app **CÓ** hiện dòng đỏ (`TC-ORD-075`/`078`) |

**Result: ❌ FAIL at Step 4**
**Reason:** Vế *"không kích hoạt tra danh bạ"* **đúng**; vế *"ô email hiện lỗi định dạng"* **sai** — không có thông báo nào.
**Evidence:** `screenshots/TC-ORD-077__step4-FAIL-khong-co-loi-dinh-dang.png` — verified tồn tại
**Impact:** 🐞 Cùng nhóm **F3/F7** (bỏ sót nhánh validate) — người dùng gõ sai định dạng sẽ không hiểu vì sao không đi tiếp được.

---

## TC-ORD-078: Check email ngoài tên miền công ty bị chặn — *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 (3 ô người nhận đang trống) | — | ✅ PASS | — | — |
| 2-3 | Nhập `nguyenvana@gmail.com` rồi rời ô | set_value + hideKeyboard | ✅ PASS | — | — |
| 4 | Check lỗi ở ô email + 3 ô kia | **CÓ** dòng lỗi đỏ dưới ô email ✓ · 3 ô tên/SĐT/địa chỉ giao **vẫn TRỐNG** ✓ · nút `Tiếp theo` vẫn `enabled=false` | ✅ PASS | `TC-ORD-078__verify-email-ngoai-ten-mien.png` | ⚠️ Chuỗi lỗi là **thông báo chung** *"Không tìm thấy email này — vui lòng nhập tay thông tin bên dưới."*, **không** nói rõ *"ngoài tên miền công ty"* |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-078__verify-email-ngoai-ten-mien.png` — verified tồn tại
**Notes:** Expected chỉ đòi *"ô email hiện lỗi"* (không đòi nguyên văn) ⇒ PASS. 🚩 2 điểm ghi nhận cho BA: (a) app **không phân biệt** *ngoài tên miền* với *không có trên HRIS*; (b) chuỗi vẫn mời **nhập tay** (F5). `@gmail.com` là **data INVALID** theo QC chốt 2026-09-17 (chỉ `@fpt.com` hợp lệ).

