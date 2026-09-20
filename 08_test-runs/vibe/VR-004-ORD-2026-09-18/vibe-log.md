# Vibe Test Log — VR-004 — v1.1 (+ CARRIED v1.0) — 2026-09-18

> Module: **ORD — Đăng tin & Quản lý tin** · Platform: **mobile** (Appium MCP / UiAutomator2) · Env: **STG** — host app `com.hrisproject.stag` (FoxPro) → FoxEco · emulator-5554 (720x1280)
> Tài khoản: **A** — `Đặng Châu Giang`, MNV 00131946 (phiên đăng nhập sẵn, giữ bằng `autoLaunch=false`)
> Evidence dir: `screenshots/`
> Phiên: 2026-09-18 (khởi tạo) · 2026-09-19 (cùng một phiên liên tục, chạy qua nửa đêm theo giờ máy chủ — ⚠️ giờ trong ảnh là giờ **emulator**, lệch ~11h so với host)
> Tập chạy: `--all` → toàn bộ **88 TC** của module (gồm 27 TC đã PASS ở VR-002)
> Seed data: **SEED-ORD-02** — dựng lại lúc 23:43 (`/sdcard` emulator đã trống, `SEED-ORD-01` của VR-002 không còn)
> ♻️ **Lượt CHỤP LẠI EVIDENCE cuối phiên (khai minh bạch):** kiểm md5 toàn bộ ảnh phát hiện **5 cặp ảnh trùng byte mà mang 2 mã TC khác nhau** — vi phạm luật *"1 ảnh không chứng minh được 2 case"*. Nguyên nhân: chụp 2 ảnh liên tiếp cho 2 TC trên **cùng một màn tĩnh**. Đã **chụp lại riêng cho từng TC tại đúng vùng verify của nó** (`003`·`042`·`043` màn OFFER · `017` ô địa chỉ lấy hàng khi đã focus · `035`·`037`·`050` màn Bước 3) ⇒ nay **0 cặp trùng khác-TC**. ⛔ Không đổi tên/copy ảnh để lách — đã tái tạo state thật và chụp mới.
> ⚠️ Evidence chụp bằng `adb exec-out screencap` (lý do cơ học: `appium_screenshot` trả ~147k ký tự HTML viewer/call và không có tham số `filename`). **Locator 100% qua MCP.**

## TC-ORD-001: Check màn "Đăng tin mới" đủ bốn thành phần và cả hai card bấm được — P2 · SC-ORD-001 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco từ FoxPro *(setup)* | phiên sẵn có, tài khoản A `Đặng Châu Giang` | ✅ PASS | — | `_setup__preflight-launch.png` |
| 2 | Nhấn "+ Đăng tin" ở bottom nav *(setup)* | find `accessibility id "Đăng tin"` → tap | ✅ PASS | — | — |
| 3 | Check lần lượt các thành phần trên màn | find ×3 + get_text ×1 | ✅ PASS | `TC-ORD-001__verify-dang-tin-moi-4-thanh-phan.png` | đủ **4/4**: subtitle `Bạn muốn làm gì?` · card `Tôi cần gửi hàng` · card `Tôi nhận giao hàng` · banner cam kết |
| 4 | Nhấn card "Tôi cần gửi hàng", sau đó nhấn quay lại *(setup)* | tap card NEED → find `Bước 1 / 3` OK → tap `Quay lại` → về `Đăng tin mới` | ✅ PASS | — | card NEED mở được màn tiếp theo |
| 5 | Nhấn card "Tôi nhận giao hàng" | tap card OFFER → mở form `Tôi nhận giao hàng` | ✅ PASS | `TC-ORD-001__verify-card-offer-mo-duoc-man.png` | card OFFER mở được màn tiếp theo ⇒ **cả hai card đều mở được** |

Banner cam kết — chuỗi thật khớp đủ 4 mệnh đề của Expected (không phí · không chat · không thanh toán · SĐT lộ sau ghép):
> `App không thu phí, không chat, không thanh toán. Sau khi ghép, SĐT hai bên sẽ được lộ để liên hệ ngoài app.`

**Result: ✅ PASS (5 steps, 2 expected)** — ⭐ TC này VR-002 **để dở ở step 5**, phiên này chạy trọn.
**Evidence:** `screenshots/TC-ORD-001__verify-dang-tin-moi-4-thanh-phan.png` (+ `TC-ORD-001__verify-card-offer-mo-duoc-man.png`) — verified tồn tại
**Locators captured:** 4 element *(dùng lại map VR-002, action OK ⇒ giữ ✅ Verified)*

---

## TC-ORD-002: Check nhấn card "Tôi cần gửi hàng" mở wizard bước 1/3 kèm step indicator — P2 · SC-ORD-002 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Đăng nhập → "+ Đăng tin" → card "Tôi cần gửi hàng" *(setup)* | tap `Đăng tin` → tap card NEED | ✅ PASS | — | — |
| 4 | Check tiêu đề bước và step indicator | find `text("Thông tin hàng")` OK · find `text("Bước 1 / 3")` OK | ✅ PASS | `TC-ORD-002__verify-buoc-1-3-thong-tin-hang.png` | ⚠️ chuỗi thật là **`Bước 1 / 3`** (CÓ space quanh `/`), Expected ghi `Bước 1/3` — chênh lệch trình bày, cùng nội dung ⇒ vẫn PASS |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-002__verify-buoc-1-3-thong-tin-hang.png` — verified tồn tại
**Locators captured:** 2 element *(map VR-002)*

---

## TC-ORD-003: Check nhấn card "Tôi nhận giao hàng" mở form một trang không có step indicator — P2 · SC-ORD-003 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Đăng nhập → "+ Đăng tin" → card "Tôi nhận giao hàng" *(setup)* | tap card OFFER | ✅ PASS | — | — |
| 4 | Check bố cục form và vùng step indicator | `appium_get_page_source` *(màn MỚI — harvest L2a)* + find `textContains("Bước")` → **NOT FOUND** | ✅ PASS | `TC-ORD-003__verify-form-1-trang-khong-step-indicator.png` | form **1 trang** trong 1 `ScrollView`: `THÔNG TIN CỦA TÔI` (Họ tên + SĐT) → `ĐIỂM XUẤT PHÁT (A)` → `ĐIỂM ĐẾN (B)` → nút `Đăng tin ngay`. **KHÔNG** có node nào chứa chữ "Bước" ⇒ không có step indicator dạng "Bước x/y". Cũng **không** có nút `Tiếp theo` |

**Result: ✅ PASS (4 steps, 1 expected)** — đối chứng đúng với luồng NEED 3 bước ở TC-ORD-002.
**Evidence:** `screenshots/TC-ORD-003__verify-form-1-trang-khong-step-indicator.png` — verified tồn tại
**Locators captured:** **7 element MỚI** (màn form OFFER — xem `vibe-locators.md`)

> 🔎 **Ghi nhận kỹ thuật (không thuộc TC nào):** SĐT prefill ở form OFFER = `0964633310`, trong khi SĐT prefill ở **Bước 2/3 của luồng NEED** (VR-002) = `0912345670`. Hai luồng lấy SĐT từ nguồn khác nhau → cần đối chiếu khi chạy `TC-ORD-042/043` và nhóm SĐT người gửi (`TC-ORD-015/018`).

---

## TC-ORD-005: Check field Loại hàng có đúng tám giá trị và mặc định là Tài liệu — P2 · SC-ORD-005 *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập → "+ Đăng tin" → card NEED *(setup)* | tap `Đăng tin` → tap card NEED | ✅ PASS | — | — |
| 3 | Check giá trị đang chọn + liệt kê toàn bộ lựa chọn theo thứ tự | `appium_get_page_source` *(cần chứng minh "đúng 8 và đúng thứ tự" — find_element không chứng minh được số lượng)* | ✅ PASS | `TC-ORD-005__verify-8-chip-mac-dinh-tai-lieu.png` | đúng **8** chip, thứ tự khớp Expected **từng nhãn**; `Tài liệu` đang được chọn (viền + chữ cam, 7 chip còn lại xám) |

Thứ tự thật trong cây (khớp Expected 100%): `Tài liệu` → `Đồ điện tử` → `Thực phẩm` → `Hàng nhỏ` → `Đồ dễ vỡ` → `Quần áo` → `Thuốc/Y tế` → `Khác`

**Result: ✅ PASS (3 steps, 1 expected)** — app hiện nhãn **"Tài liệu"** đúng PRD ⇒ `C-ORD-09` đã được app thực hiện.
**Evidence:** `screenshots/TC-ORD-005__verify-8-chip-mac-dinh-tai-lieu.png` — verified tồn tại
**Locators captured:** 8 chip *(map VR-002, re-verify OK)*
> ⚠️ Trạng thái "đang chọn" **phải đọc bằng ảnh** — bẫy **T1**: `selected` luôn `false` trên chip React Native.

---

## TC-ORD-006: Check danh mục loại hàng có tám chip, không có chip "Tài liệu" — P3 · SC-ORD-006 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập → "+ Đăng tin" → card NEED *(setup)* | — | ✅ PASS | — | — |
| 2 | Đếm số chip loại hàng hiển thị ở bước 1 | đếm từ page source | ✅ PASS | — | đúng **8** chip ⇒ vế số lượng ĐÚNG |
| 3 | Đối chiếu nhãn từng chip, tìm chip nhãn "Tài liệu" | find `accessibility id "Tài liệu"` → **FOUND** | ❌ **FAIL** | `TC-ORD-006__step3-FAIL-co-chip-tai-lieu.png` | Expected: KHÔNG có chip "Tài liệu". Actual: **CÓ** chip "Tài liệu", lại còn là chip **mặc định đang chọn** |

**Result: ❌ FAIL at Step 3**
**Expected vs Actual:** *không có chip "Tài liệu"* ↔ **có** chip "Tài liệu" (mặc định)
**Evidence:** `screenshots/TC-ORD-006__step3-FAIL-co-chip-tai-lieu.png` — verified tồn tại
**Impact:** 🔴 **TC hết hiệu lực, KHÔNG phải lỗi app** — `C-ORD-09` (BA chốt 2026-09-16) quy định **CÓ** nhãn "Tài liệu"; `TC-ORD-005` (v1.1) PASS là bản thay thế. ⛔ **Không log bug.** Chờ QC chốt `DESCOPED` theo `Project_rule §10.5` (giữ nguyên dòng). **Tái xác nhận kết luận VR-002.**

---

## TC-ORD-008: Check chưa chọn giá trị hàng thì nút "Tiếp theo" bị khoá — P2 · SC-ORD-008 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập → "+ Đăng tin" → card NEED *(setup)* | — | ✅ PASS | — | — |
| 2 | Không chọn giá trị hàng | giữ nguyên state mới mở | ✅ PASS | — | — |
| 3 | Check trạng thái nút "Tiếp theo" | find `Tiếp theo` → `get_element_attribute(enabled)` = **`false`**; đo màu nền nút bằng lấy mẫu pixel | ✅ PASS | — *(state này trùng state của TC-ORD-005; ⛔ KHÔNG trích ảnh TC khác làm evidence cho TC này)* | **đúng CẢ 2 vế**: `enabled=false` **và** nút **bị làm mờ thật** — nền disable `(253,175,62)` cam nhạt (blend trắng) vs enable `(255,160,0)` cam bão hoà |
| 4 | Nhấn nút "Tiếp theo" | tap → find `text("Bước 1 / 3")` vẫn OK | ✅ PASS | — | màn ở lại bước 1, đúng Expected |
| 5 | Chọn giá trị hàng "Thấp" | find/tap `descriptionStartsWith("Thấp")` | ✅ PASS | — | — |
| 6 | Check lại trạng thái nút "Tiếp theo" | `get_element_attribute(enabled)` = **`false`** | ❌ **FAIL** | `TC-ORD-008__step6-FAIL-tiep-theo-van-disable-sau-khi-chon-thap.png` | Expected: enable. Actual: **vẫn disable** |

**Result: ❌ FAIL at Step 6** *(step 3 đúng cả 2 vế — xem đính chính dưới)*
**Expected vs Actual:** *chọn giá trị hàng ⇒ "Tiếp theo" enable* ↔ **vẫn disable**, vì v1.1 yêu cầu **đủ 4 điều kiện**: giá trị hàng **+ TRỌNG LƯỢNG + KÍCH THƯỚC + ≥1 ảnh**
**Evidence:** `screenshots/TC-ORD-008__step6-FAIL-tiep-theo-van-disable-sau-khi-chon-thap.png` — verified tồn tại
**Impact:** 🔴 **TC hết hiệu lực (họ F1)** — v1.0 viết khi bước 1 chỉ có 1 trường bắt buộc. ⛔ không log bug; chờ QC chốt `DESCOPED`. **Tái xác nhận VR-002.**
> ♻️ **TỰ ĐÍNH CHÍNH TRONG PHIÊN (ghi lại để không ai lặp lại lỗi này):** lúc đầu t kết luận *"nút disable không hề làm mờ"* — **SAI**, do **nhìn bằng mắt trên ảnh** thay vì đo. Khi **lấy mẫu pixel** thì nền nút disable là `(253,175,62)` (cam **nhạt**, đã blend trắng ⇒ giảm opacity) còn enable là `(255,160,0)` (cam **bão hoà**) ⇒ **app CÓ làm mờ**, đúng như VR-002 đã kiểm (`CHANGELOG ORD §Nợ #3`). Verdict step 3 đã sửa **⚠️ → ✅ PASS**, và **ứng viên bug "nút disable không làm mờ" bị RÚT LẠI**.
> ⚠️ Bài học: khác biệt màu do opacity **rất khó thấy bằng mắt trên ảnh chụp** — phải đo pixel, y như cách đã dùng cho `TC-ORD-085`.

---

## TC-ORD-009: Check chọn giá trị hàng "Cao" hiện banner cảnh báo đúng nguyên văn — P2 · SC-ORD-009 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập → "+ Đăng tin" → card NEED *(setup)* | — | ✅ PASS | — | — |
| 2 | Chọn giá trị hàng "Cao" | find/tap `descriptionStartsWith("Cao, Trên 5")` | ✅ PASS | — | — |
| 3 | Check nội dung banner cảnh báo hiện ra | find `textContains("giá trị cao")` → lần 1 **NOT FOUND** *(ngoài viewport — bẫy **T8**)* → `scroll_to_element` → FOUND → `get_text` | ✅ PASS | `TC-ORD-009__verify-banner-hang-gia-tri-cao.png` | chuỗi thật **khớp nguyên văn 100%** Expected |

Chuỗi thật:
> `Hàng giá trị cao: hai bên tự thoả thuận và chịu trách nhiệm với nhau. FoxEco không bảo hiểm, không đứng ra vận chuyển hay bồi thường.`

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-009__verify-banner-hang-gia-tri-cao.png` — verified tồn tại
**Locators captured:** 2 element *(map VR-002)*

---

## TC-ORD-010: Check chọn giá trị hàng "Thấp" hoặc "Vừa" không hiện banner cảnh báo — P3 · SC-ORD-010 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập → "+ Đăng tin" → card NEED *(setup)* | — | ✅ PASS | — | — |
| 2 | Chọn giá trị hàng "Thấp" | find/tap `descriptionStartsWith("Thấp")` | ✅ PASS | — | — |
| 3 | Check vùng dưới nhóm giá trị hàng | find `textContains("giá trị cao")` → NOT FOUND, **với vùng đó ĐANG hiển thị trong viewport** | ✅ PASS | `TC-ORD-010__verify-thap-khong-co-banner.png` | ngay dưới nhóm giá trị là `TRỌNG LƯỢNG`, không có banner |
| 4 | Chọn giá trị hàng "Vừa" | find/tap `descriptionStartsWith("Vừa, 1")` | ✅ PASS | — | — |
| 5 | Check lại vùng đó | find `textContains("giá trị cao")` → NOT FOUND *(vẫn trong viewport)* | ✅ PASS | `TC-ORD-010__verify-vua-khong-co-banner.png` | — |

**Result: ✅ PASS (5 steps, 2 expected)** — cặp đối chứng âm khớp với `TC-ORD-009`: banner chỉ gắn mức "Cao".
**Evidence:** `screenshots/TC-ORD-010__verify-thap-khong-co-banner.png` (+ `TC-ORD-010__verify-vua-khong-co-banner.png`) — verified tồn tại
> ♻️ **Đã chạy lại 2 lần trong phiên này, có chủ ý.** Lượt 1 assert vắng banner khi vùng banner **nằm ngoài viewport** ⇒ theo bẫy **T8**, "NOT FOUND" lúc đó **không chứng minh được vắng thật**. Đã cuộn cho vùng đó vào viewport rồi assert lại; 2 ảnh evidence là của lượt 2. *(Đây đúng loại suy diễn sai đã sinh ra "bug ma" B3 ở VR-002 — xem T10.)*

---

## TC-ORD-013: Check khối ảnh hàng mang dấu bắt buộc và dòng helper nêu rõ ràng buộc — P2 · SC-ORD-012 *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập → "+ Đăng tin" → card NEED *(setup)* | — | ✅ PASS | — | — |
| 2 | Check nhãn khối ảnh, bộ đếm và dòng helper khi chưa tải ảnh nào | page source: `ẢNH HÀNG *` + `multi-photo-add-button` desc=`0/5`; find helper → NOT FOUND *(**T8**)* → `scroll_to_element` → `get_text` | ✅ PASS | `TC-ORD-013__verify-anh-hang-bat-buoc-0-5-helper.png` | đủ **3/3** vế: nhãn `ẢNH HÀNG` + **dấu `*` đỏ** · bộ đếm `0/5` · helper khớp nguyên văn |

Helper — chuỗi thật khớp Expected 100%:
> `Bắt buộc ít nhất 1 ảnh · tối đa 5 ảnh · giúp người vận chuyển nhận diện hàng`

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-013__verify-anh-hang-bat-buoc-0-5-helper.png` — verified tồn tại
**Locators captured:** 3 element *(map VR-002)*

---

## TC-ORD-054: Check bước 1 không có field nhập số tiền hay ngưỡng giá trị hàng — P3 · SC-ORD-051 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập → "+ Đăng tin" → card NEED *(setup)* | — | ✅ PASS | — | — |
| 2 | Cuộn toàn bước 1 | `scroll_to_element` ×2 (banner → `ẢNH HÀNG` → helper) + 2 lần `get_page_source` phủ **cả 2 nửa** form | ✅ PASS | — | phủ hết: LOẠI HÀNG · GHI CHÚ · GIÁ TRỊ HÀNG · TRỌNG LƯỢNG · KÍCH THƯỚC · ẢNH HÀNG |
| 3 | Check tìm field nhập số tiền / ngưỡng giá trị hàng | toàn bước 1 có **đúng 1 `EditText` = GHI CHÚ** (`maxlen=300`, input-type text). Giá trị hàng là **3 chip định tính**, khoảng tiền chỉ là **nhãn mô tả** (`Dưới 1 triệu ₫` · `1 – 5 triệu ₫` · `Trên 5 triệu ₫`) | ✅ PASS | `TC-ORD-054__verify-khong-co-field-so-tien.png` | KHÔNG có field số tiền, KHÔNG có field ngưỡng |
| 4 | Chọn giá trị hàng "Cao" | find/tap `resourceId("value-tier-chip-option-high")` | ✅ PASS | — | — |
| 5 | Check lại vùng quanh nhóm giá trị hàng | find `class name android.widget.EditText` → **NOT FOUND** trong viewport; chỉ xuất hiện **banner cảnh báo**, không có ô nhập nào | ✅ PASS | `TC-ORD-054__verify-chon-cao-van-khong-co-field-so-tien.png` | — |

**Result: ✅ PASS (5 steps, 2 expected)** — chốt đúng ranh giới: ngưỡng bằng **số tiền** (`BR-ORD-03`) **out of scope**; cảnh báo theo **mức định tính "Cao"** thì CÓ (`TC-ORD-009`).
**Evidence:** `screenshots/TC-ORD-054__verify-khong-co-field-so-tien.png` (+ `TC-ORD-054__verify-chon-cao-van-khong-co-field-so-tien.png`) — verified tồn tại

---

## TC-ORD-007: Check nhấn lại chip đang chọn không bỏ chọn giá trị — P3 · SC-ORD-007 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập → "+ Đăng tin" → card NEED *(setup)* | — | ✅ PASS | — | — |
| 2 | Nhấn đúng chip loại hàng đang được chọn | find `accessibility id "Tài liệu"` → tap *(chip đang chọn)* | ✅ PASS | — | — |
| 3 | Check trạng thái các chip loại hàng | đọc bằng ảnh *(bẫy **T1**: `selected` luôn `false`)* | ✅ PASS | `TC-ORD-007__verify-nhan-lai-chip-van-duoc-chon.png` | chip `Tài liệu` **VẪN** được chọn (viền + chữ cam); **không** có trạng thái 8 chip cùng không chọn ⇒ đúng Expected |
| 4 | Chọn giá trị hàng "Thấp" | find/tap `resourceId("value-tier-chip-option-low")` | ✅ PASS | — | — |
| 5 | Nhấn "Tiếp theo" | tap → find `text("Bước 1 / 3")` **vẫn còn** | ❌ **FAIL** | `TC-ORD-007__step5-FAIL-khong-sang-buoc-2.png` | Expected: sang bước 2. Actual: **ở lại bước 1** |

**Result: ❌ FAIL at Step 5**
> ✅ Điểm kiểm chứng chính của TC (step 3 — chip giữ trạng thái chọn) thì **đúng**.
**Expected vs Actual:** *chọn loại hàng + giá trị hàng ⇒ sang bước 2* ↔ **ở lại bước 1** (v1.1 cần thêm TRỌNG LƯỢNG + KÍCH THƯỚC + ≥1 ảnh)
**Evidence:** `screenshots/TC-ORD-007__verify-nhan-lai-chip-van-duoc-chon.png` (+ `TC-ORD-007__step5-FAIL-khong-sang-buoc-2.png`) — verified tồn tại
**Impact:** 🔴 **TC hết hiệu lực ở vế điều hướng (họ F1)**, ⛔ không log bug, chờ QC chốt `DESCOPED`. Giá trị còn lại của TC vẫn đúng: nó chứng minh **không viết được TC negative "để trống loại hàng"** — UI không cho tạo tiền đề đó (`KB-VIBE-02`). **Tái xác nhận VR-002.**

---

## TC-ORD-011: Check ghi chú nhận đúng 300 ký tự và chặn ký tự thứ 301 — P3 · SC-ORD-011 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập → "+ Đăng tin" → card NEED *(setup)* | — | ✅ PASS | — | — |
| 2 | Nhập vào ô Ghi chú chuỗi dài **đúng 300 ký tự** | find `class name android.widget.EditText` *(EditText duy nhất ở bước 1)* → `set_value` 300 ký tự → `get_text` | ✅ PASS | `TC-ORD-011__pre-ghi-chu-300-ky-tu.png` | nhận **trọn 300/300**; đọc lại khớp từng ký tự. Thuộc tính ô: `max-text-length=300` |
| 3 | Chọn giá trị hàng "Thấp" | *(đã chọn từ TC-ORD-007, giữ nguyên state)* | ✅ PASS | — | — |
| 4 | Nhấn "Tiếp theo" | tap → find `text("Bước 1 / 3")` **vẫn còn** | ❌ **FAIL** | `TC-ORD-011__step4-FAIL-khong-sang-buoc-2.png` | Expected: sang bước 2. Actual: **ở lại bước 1** (họ F1) |
| 5 | Nhấn quay lại bước 1 | ⏭ **KHÔNG CẦN** — app chưa rời bước 1 do step 4 fail | — | — | ⛔ không tap `Quay lại`: ở bước 1 nút này **thoát wizard + xoá dữ liệu** (nav map VR-002) ⇒ sẽ mất chuỗi 300 ký tự đang cần kiểm |
| 6 | Nhập tiếp 1 ký tự nữa vào ô Ghi chú | `set_value(text="Z", w3cActions=true)` → gõ vào element đang focus, **nối thêm** chứ không ghi đè | ✅ PASS | — | — |
| 7 | Check độ dài nội dung trong ô Ghi chú | `get_text` → chuỗi **y hệt** bản 300 ký tự, không có `Z` | ✅ PASS | `TC-ORD-011__verify-ghi-chu-dung-300-ky-tu.png` | vẫn **đúng 300**; ký tự thứ 301 **bị chặn** ⇒ đúng Expected |

**Result: ❌ FAIL at Step 4**
> ✅ Biên 300/301 — điểm kiểm chứng chính (Expected 7) — **đúng hoàn toàn**.
**Expected vs Actual:** chỉ lệch ở vế điều hướng của step 4 (họ F1).
**Evidence:** `screenshots/TC-ORD-011__verify-ghi-chu-dung-300-ky-tu.png` (+ `TC-ORD-011__pre-ghi-chu-300-ky-tu.png`, `TC-ORD-011__step4-FAIL-khong-sang-buoc-2.png`) — verified tồn tại
**Impact:** 🔴 vế điều hướng hết hiệu lực (F1) ⇒ ⛔ không log bug. **Khuyến nghị QC:** TC này chỉ cần **bỏ step 4-5** là dùng lại được cho v1.1 (khác `TC-ORD-006/014` phải DESCOPED hẳn).
> ⚠️ **Sai lệch quy trình có chủ ý, khai báo rõ:** step 5 (quay lại bước 1) **không thực hiện** vì app chưa hề rời bước 1 — thực hiện đúng chữ sẽ **thoát wizard và xoá chuỗi 300 ký tự**, làm không kiểm được Expected 7. Bản chất phép kiểm biên **không đổi**.

---

## TC-ORD-014: Check không tải ảnh vẫn chuyển được sang bước 2 — P3 · SC-ORD-013 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập → "+ Đăng tin" → card NEED *(setup)* | — | ✅ PASS | — | — |
| 2 | Chọn chip loại hàng "Giấy tờ, hồ sơ" | ⚠️ **nhãn không tồn tại** → dùng chip **`Tài liệu`** (chip mặc định, tương đương vai trò) | ✅ PASS | — | nhãn trong Steps là câu chữ v1.0 đã hết hiệu lực (`C-ORD-09`, xem `TC-ORD-005/006`) |
| 3 | Chọn giá trị hàng "Thấp", không tải ảnh nào | `Thấp` đang chọn · bộ đếm ảnh `0/5` | ✅ PASS | — | TRỌNG LƯỢNG + KÍCH THƯỚC cũng **chưa chọn** |
| 4 | Nhấn "Tiếp theo" | tap → vẫn `Bước 1 / 3`; cuộn về đúng vùng khối ảnh để kiểm thông báo lỗi | ❌ **FAIL** | `TC-ORD-014__step4-FAIL-khong-sang-buoc-2-khong-bao-loi-anh.png` | Expected: **sang bước 2**, không báo lỗi ảnh. Actual: **ở lại bước 1**; đồng thời **không có thông báo lỗi nào** ở cả 3 khối thiếu dữ liệu |

**Result: ❌ FAIL at Step 4**
**Expected vs Actual:** *không ảnh vẫn qua bước 2* ↔ **bị chặn** (ảnh là **bắt buộc** ở v1.1 — `BR01-01`)
**Evidence:** `screenshots/TC-ORD-014__step4-FAIL-khong-sang-buoc-2-khong-bao-loi-anh.png` — verified tồn tại
**Impact:** 🔴 **TC hết hiệu lực — mâu thuẫn TRỰC TIẾP với `TC-ORD-063`** (v1.1 **P1**: chưa có ảnh **PHẢI** chặn). Hai TC không thể cùng đúng ⇒ QC **phải** chốt `DESCOPED` cho `TC-ORD-014`. ⛔ không log bug. **Tái xác nhận VR-002.**
> 🐞 **Đồng thời là bằng chứng bổ sung cho bug chặn im lặng (F3/F7):** thiếu **3** trường bắt buộc (trọng lượng · kích thước · ảnh), nút khoá, **không một dòng lỗi nào** trên cả màn — ảnh evidence chụp đúng vùng khối ảnh để chứng minh (⛔ không kết luận từ viewport khác, tránh bẫy **T8**).

---

## TC-ORD-012: Check tải một ảnh JPG hợp lệ hiện đúng bộ đếm một trên năm — P2 · SC-ORD-012 *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập → "+ Đăng tin" → card NEED *(setup)* | — | ✅ PASS | — | — |
| 2 | Nhấn vùng "ẢNH HÀNG" và chọn 1 ảnh JPG nhỏ từ thư viện | find/tap `resourceId("multi-photo-add-button")` → tap `text("Chọn từ thư viện")` → Photo Picker → tap `icon_thumbnail.instance(6)` → tap `textStartsWith("Add")` | ✅ PASS | `TC-ORD-012__pre-chon-1-anh-jpg-nho.png` | ảnh đã chọn = tệp seed số 01 (**38 KB**, JPG 1200×900, nền đỏ) — nhận diện bằng ảnh recon `_recon__photo-picker-seed-ord-02.png` |
| 3 | Check ô ảnh và bộ đếm bên cạnh nhãn "ẢNH HÀNG" | find `accessibility id "1/5"` → FOUND | ✅ PASS | `TC-ORD-012__verify-bo-dem-1-tren-5.png` | ảnh **hiện trong ô** (kèm nút `×` xoá) và bộ đếm chuyển **`0/5` → `1/5`** ⇒ đúng Expected |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-012__verify-bo-dem-1-tren-5.png` (+ `TC-ORD-012__pre-chon-1-anh-jpg-nho.png`) — verified tồn tại
**Locators captured:** 4 element *(map VR-002, re-verify OK)* — bộ đếm là `content-desc` của nút thêm ảnh (bẫy **T7**), nên `0/5` → `1/5` là **đổi locator**, không phải đổi giá trị.
> 🌱 **Seed:** dùng `SEED-ORD-02` (dựng lại phiên này). `SEED-ORD-01` của VR-002 **không còn trên máy ảo** — `/sdcard` đã trống khi bắt đầu phiên.

---

## TC-ORD-034: Check bước 3 tóm tắt đúng dữ liệu nhập ở bước 1 và 2 — P2 · SC-ORD-031 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 2 | Chọn chip loại hàng "Giấy tờ, hồ sơ" | ⚠️ nhãn không tồn tại → dùng **`Tài liệu`** | ✅ PASS | — | câu chữ v1.0 hết hiệu lực (`C-ORD-09`) |
| 3 | Chọn giá trị hàng "Vừa" | ⚠️ **lệch dữ liệu**: dùng **`Thấp`** *(state mang sang từ `TC-ORD-007`)* | ✅ PASS | — | khai báo rõ ở cuối section |
| 4 | Nhập ghi chú "Giao gio hanh chinh" | ⚠️ **lệch dữ liệu**: lần chạy này ô ghi chú mang chuỗi **300 ký tự** của `TC-ORD-011` | ✅ PASS | — | — |
| 5-9 | Tiếp theo → bước 2 (email + 2 địa chỉ khác nhau + buổi) → Tiếp theo | *(xem TC-ORD-004)* | ✅ PASS | — | — |
| 10 | Check phần tóm tắt ở bước 3 | `appium_get_page_source` màn **Bước 3 / 3** *(màn MỚI — harvest L2a, VR-002 chưa từng tới đây)* | ✅ PASS | `TC-ORD-034__verify-tom-tat-buoc-3.png` | **6/6 mục của Expected đều đúng** — xem bảng dưới |

| Expected yêu cầu | Tóm tắt thật ở bước 3 | Khớp? |
|---|---|---|
| loại hàng | `Tài liệu · Giá trị thấp` | ✅ (đúng chip đã chọn) |
| giá trị hàng | *(gộp cùng dòng trên)* `Giá trị thấp` | ✅ |
| ghi chú | `A012345678B012345678…` (300 ký tự, đủ) | ✅ |
| khung giờ | `18/09/2026 – 19/09/2026 · Chiều` | ✅ (đúng ngày + buổi đã chọn) |
| người gửi | `Đặng Châu Giang · 0964633310` + `FTEL Đà Nẵng Cẩm Lệ` | ✅ |
| người nhận | `Đặng Châu Anh · 0343439724` + `Tòa V-City, Lê Thái Tổ` | ✅ |

**Result: ✅ PASS (10 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-034__verify-tom-tat-buoc-3.png` — verified tồn tại
**Locators captured:** **8 element MỚI** (màn Bước 3/3)
> ⚠️ **Lệch dữ liệu đầu vào, khai báo rõ:** chạy với `Tài liệu`/`Thấp`/ghi-chú-300-ký-tự thay cho `Giấy tờ, hồ sơ`/`Vừa`/`"Giao gio hanh chinh"`. Điểm kiểm của TC là **tóm tắt có phản chiếu đúng cái đã nhập hay không** — vẫn kiểm được trọn vẹn với dữ liệu khác. Nhãn `Giấy tờ, hồ sơ` **không tồn tại** trên app nên không thể làm đúng chữ.
> 🔴 **PHÁT HIỆN NGOÀI EXPECTED — spec gap, không đổi verdict:** tóm tắt bước 3 **KHÔNG hiển thị `TRỌNG LƯỢNG`, `KÍCH THƯỚC` và ảnh hàng** — 3 trường **v1.1 mới thêm và đều BẮT BUỘC**. TC-034 là TC v1.0 nên Expected của nó không đòi 3 mục này, và **không TC nào của v1.1 assert việc chúng xuất hiện ở bước 3** ⇒ lỗ hổng phân tích. **Route:** `/analyze-requirements --update "Bước 3/3 tóm tắt đơn thiếu TRỌNG LƯỢNG + KÍCH THƯỚC + ảnh hàng — 3 trường bắt buộc của v1.1"`.

---

## TC-ORD-035: Check bước 3 hiện banner cảnh báo hàng cấm — P3 · SC-ORD-032 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Điền đủ bước 1 + 2, vào bước 3 *(setup)* | *(xem TC-ORD-004)* | ✅ PASS | — | — |
| 2 | Check nội dung banner cảnh báo trên màn | đọc từ page source bước 3 + cuộn tới vùng banner | ✅ PASS | `TC-ORD-035__verify-banner-hang-cam.png` | banner **CÓ**, nêu đủ **4 nhóm** Expected đòi: thuốc · vũ khí · chất nguy hiểm · hàng phi pháp |

Chuỗi thật:
> `Không được gửi: thuốc, vũ khí, chất nguy hiểm, hàng phi pháp. FoxEco là nền tảng kết nối, không chịu trách nhiệm về nội dung hàng.`

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-035__verify-banner-hang-cam.png` — verified tồn tại
> 🔎 Banner là **thông tin tĩnh**, hiện với **mọi** loại hàng (lần chạy này loại hàng = `Tài liệu`, không phải `Thuốc/Y tế`) ⇒ đúng kết luận `C-ORD-04`: banner **không phải cơ chế chặn**. Đây là tiền đề của `TC-ORD-038`.
> ⚠️ **Lưu ý cho QC:** ghi chú của `TC-ORD-005` (v1.1) viết *"⛔ không assert banner hàng cấm — v1.1 không có"*. Thực tế **app CÓ** banner này ở bước 3. Hai câu này không mâu thuẫn nếu hiểu "v1.1 không có" = *tài liệu v1.1 không còn nhắc*, nhưng **nên chốt lại** để phiên sau không hiểu nhầm thành "app không có".

---

## TC-ORD-036: Check checkbox điều khoản ở bước 3 mặc định chưa được tick — P2 · SC-ORD-033 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Điền đủ bước 1 + 2, vào bước 3 **lần đầu** *(setup)* | — | ✅ PASS | — | lần đầu vào bước 3 của phiên |
| 2 | Check trạng thái checkbox điều khoản | đọc bằng ảnh *(bẫy **T1**)* | ✅ PASS | `TC-ORD-036__verify-checkbox-dieu-khoan-chua-tick.png` | ô checkbox **trống** (không dấu tick, viền xám) ⇒ **CHƯA** được tick, đúng Expected |

**Result: ✅ PASS (2 steps, 1 expected)** — khớp `C-ORD-12` (`D8.1` L373 + app STG); bản `TC_04.71` đợt cũ expected "tick sẵn" là **sai nguồn**, nay có bằng chứng phủ định.
**Evidence:** `screenshots/TC-ORD-036__verify-checkbox-dieu-khoan-chua-tick.png` — verified tồn tại

---

## TC-ORD-037: Check chưa tick điều khoản thì không đăng được tin — **P1** · SC-ORD-034 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Điền đủ bước 1 + 2, vào bước 3 *(setup)* | — | ✅ PASS | — | — |
| 2 | Không tick checkbox điều khoản | giữ nguyên | ✅ PASS | — | — |
| 3 | Check trạng thái nút "Đăng tin ngay" | find `accessibility id "Đăng tin ngay"` → `get_element_attribute(enabled)` = **`false`** | ✅ PASS | `TC-ORD-037__verify-step3-dang-tin-ngay-disable.png` | đúng Expected |
| 4 | Nhấn nút "Đăng tin ngay" | tap → find `text("Bước 3 / 3")` **vẫn còn** | ✅ PASS | `TC-ORD-037__verify-step4-khong-dang-duoc-tin.png` | tin **không** được đăng, màn ở lại bước 3 ⇒ đúng Expected |
| 5 | Tick checkbox điều khoản | find/tap `descriptionStartsWith("Tôi đã đọc và đồng ý")` | ✅ PASS | — | — |
| 6 | Check lại trạng thái nút | `get_element_attribute(enabled)` = **`true`** | ✅ PASS | `TC-ORD-037__verify-step6-dang-tin-ngay-enable.png` | đúng Expected |

**Result: ✅ PASS (6 steps, 3 expected)** — ⭐ điểm chặn consent bắt buộc hoạt động đúng (cùng rule `TC-TS-004`).
**Evidence:** `screenshots/TC-ORD-037__verify-step6-dang-tin-ngay-enable.png` (+ `__verify-step3-...`, `__verify-step4-...`) — verified tồn tại
**Locators captured:** 2 element *(checkbox điều khoản + nút Đăng tin ngay, màn Bước 3/3)*

---

## TC-ORD-050: Check nút gửi của NEED và OFFER chỉ bật khi đủ trường và tick — P2 · SC-ORD-047 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 3 luồng **NEED** *(setup)* | — | ✅ PASS | — | — |
| 2-3 | Không tick điều khoản → check nút | `enabled=false` | ✅ PASS | *(dùng chung state với TC-037)* | đúng Expected 3 |
| 4-5 | Tick điều khoản → check lại nút | `enabled=true` | ✅ PASS | `TC-ORD-050__verify-need-nut-gui-bat-sau-khi-tick.png` | đúng Expected 5 |
| 6 | Quay lại màn "Đăng tin mới" | `appium_gesture(back)` ×3 → về Trang chủ → tap `Đăng tin` | ✅ PASS | — | ⚠️ back ×3 đi **quá** 1 màn (về Trang chủ), đã vào lại `Đăng tin mới` bằng tab `Đăng tin` |
| 7 | Nhấn card OFFER, để trống field điểm đến *(setup)* | tap card OFFER; page source xác nhận `EditText[hint="Bạn sẽ đến đâu"]` có `showing-hint=true` ⇒ **RỖNG** | ✅ PASS | — | đồng thời **chưa** chọn buổi, **chưa** tick điều khoản |
| 8 | Check trạng thái nút đăng tin của form OFFER | `get_element_attribute(enabled)` = **`true`** | ❌ **FAIL** | `TC-ORD-050__step8-FAIL-offer-nut-gui-enabled-khi-thieu-du-lieu.png` | Expected: **disable**. Actual: **enable** dù thiếu điểm đến + buổi + consent |
| 9 | Nhập điểm đến bằng chạm chọn gợi ý | `set_value "Lê Thái Tổ"` → find/tap `accessibility id "address-suggestion-0"` | ✅ PASS | — | ⭐ ô này **CÓ** dropdown gợi ý |
| 10 | Tick checkbox điều khoản | find/tap `descriptionStartsWith("Tôi đã đọc và đồng ý")` | ✅ PASS | — | — |
| 11 | Check lại trạng thái nút đăng tin | `enabled=true` | ✅ PASS | `TC-ORD-050__verify-offer-nut-gui-enable-sau-khi-du-du-lieu.png` | đúng Expected 11 |

**Result: ❌ FAIL at Step 8** *(3/4 expected còn lại đều đúng)*
**Expected vs Actual:** *nút gửi form OFFER disable khi thiếu trường* ↔ **luôn enable**
**Evidence:** `screenshots/TC-ORD-050__step8-FAIL-offer-nut-gui-enabled-khi-thieu-du-lieu.png` (+ 2 ảnh `__verify`) — verified tồn tại
**Impact:** 🐞 **Ứng viên bug MỚI (chưa có ở VR-002) — nhưng mức độ THẤP, và phải đọc kèm ngữ cảnh:** hai luồng đăng tin dùng **2 cơ chế validate khác nhau**:
> | Luồng | Nút gửi khi thiếu dữ liệu | Khi nhấn | Người dùng có biết thiếu gì? |
> |---|---|---|---|
> | **NEED** (wizard) | **disable** | không gì xảy ra | ❌ **KHÔNG** — chặn im lặng (bug F3/F7) |
> | **OFFER** (1 trang) | **enable** | **không đăng**, hiện lỗi đỏ inline `Chọn ít nhất 1 buổi` | ✅ **CÓ** |
>
> ⇒ Trái chữ `VAL-01` (`D8.3` L392: nút chỉ bật khi đủ) nên **TC FAIL đúng**, nhưng **tinh thần "không cho gửi khi thiếu" thì OFFER vẫn giữ**, và trải nghiệm của OFFER **tốt hơn** NEED. **Khuyến nghị:** đừng fix OFFER cho giống NEED — nên **đưa cơ chế lỗi inline của OFFER sang NEED** để dứt bug chặn im lặng. Đây là dữ kiện đắt giá cho BA/Dev khi xử lý F3/F7.

---

## TC-ORD-004: Check đăng tin NEED thành công với dữ liệu hợp lệ đầy đủ ba bước — **P1** · SC-ORD-004 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | "+ Đăng tin" → card "Tôi cần gửi hàng" *(setup)* | tap `Đăng tin` → tap card NEED | ✅ PASS | — | — |
| 2 | Chọn chip loại hàng "Giấy tờ, hồ sơ" | ⚠️ nhãn không tồn tại → dùng **`Tài liệu`** | ✅ PASS | — | `C-ORD-09` |
| 3 | Chọn giá trị hàng "Thấp" | find/tap `resourceId("value-tier-chip-option-low")` | ✅ PASS | — | — |
| 3b | *(v1.1 bổ sung — không có trong Steps v1.0)* TRỌNG LƯỢNG + KÍCH THƯỚC + ≥1 ảnh | tap `weight-tier-chip-option-light` + `size-tier-chip-option-small`; ảnh đã có từ `TC-ORD-012` | ✅ PASS | `TC-ORD-004__pre-buoc-1-da-dien-du.png` | `Tiếp theo` `enabled` **`false`→`true`** ⇒ xác nhận lại luật enable **4 điều kiện** |
| 4 | Nhấn "Tiếp theo" | tap → find `text("Bước 2 / 3")` OK | ✅ PASS | — | — |
| 5 | Nhập email `stag_anhdc4@fpt.com` rồi rời ô | `set_value` → app hiện `Đã tìm thấy trong hệ thống nội bộ…` + **autofill** `Đặng Châu Anh` / `0343439724` | ✅ PASS | — | tra danh bạ OK |
| 6 | Nhập địa chỉ lấy hàng rồi **chạm chọn 1 gợi ý** | ⚠️ ô này **RỖNG** khi vào bước 2 *(VR-002 ghi là prefill)* → `set_value "Cẩm Lệ"` → find/tap `address-suggestion-0` = `FTEL Đà Nẵng Cẩm Lệ` | ✅ PASS | — | xem khối 🔑 dưới |
| 7 | Nhập địa chỉ giao khác địa chỉ lấy rồi **chạm chọn gợi ý** | `set_value "Lê Thái Tổ"` → find/tap `address-suggestion-0` = `Tòa V-City, Lê Thái Tổ` | ✅ PASS | — | khác địa chỉ lấy ✓ |
| 8 | Chọn khung giờ muộn hơn hiện tại | v1.1 = **chip BUỔI** → tap `Chiều (13–17h)` *(giờ máy 12:0x)*; `Đến ngày` đổi sang 19/09 | ✅ PASS | `TC-ORD-004__pre-buoc-2-da-dien-du.png` | — |
| 9 | Nhấn "Tiếp theo" | `enabled` **`false`→`true`** sau khi chọn gợi ý → tap → find `text("Bước 3 / 3")` OK | ✅ PASS | — | — |
| 10 | Tick checkbox điều khoản | find/tap checkbox → `Đăng tin ngay` `enabled=true` | ✅ PASS | `TC-ORD-004__pre-buoc-3-truoc-khi-dang.png` | tóm tắt bước 3 đúng (xem `TC-ORD-034`) |
| 11 | Nhấn "Đăng tin ngay" | tap → **KHÔNG mở màn "Đăng tin thành công"**, màn ở lại `Bước 3 / 3`, **không toast, không lỗi, không loading** | ❌ **FAIL** | `TC-ORD-004__step11-FAIL-khong-dang-duoc-tin-api-400.png` | logcat: **API trả 400** |

**Result: ❌ FAIL at Step 11 — 🔴🔴 KHÔNG ĐĂNG ĐƯỢC TIN NEED (P1, happy path của cả module)**
**Expected vs Actual:** *mở màn "Đăng tin thành công", tin ở trạng thái "Chờ ghép"* ↔ **ở lại bước 3, không đơn nào được tạo**
**Evidence:** `screenshots/TC-ORD-004__step11-FAIL-khong-dang-duoc-tin-api-400.png` · log: `logcat-TC-ORD-004-REQ_400.txt` — verified tồn tại

🐞 **Bug nghiêm trọng nhất phiên này — 2 lỗi xếp lớp:**

```
E ReactNativeJS: 'Failed to create post:', { [FoxEcoApiError: Dữ liệu đầu vào không hợp lệ]
                    name: 'FoxEcoApiError', code: 'REQ_400', retryable: false, details: undefined }
```

| # | Lỗi | Bằng chứng |
|---|---|---|
| **1. API từ chối tạo đơn** | `POST create post` → **400 `REQ_400`** *"Dữ liệu đầu vào không hợp lệ"* dù UI đã pass toàn bộ validate client | logcat, **3 lần bấm / 3 lần lỗi** (00:18:34 · 00:19:11 · 00:21:44) |
| **2. App im lặng tuyệt đối** | người dùng bấm "Đăng tin ngay" và **không thấy bất cứ gì**: không toast, không banner, không spinner, nút vẫn bật. Không có cách nào biết đơn thất bại | ảnh `__step11-FAIL`; `details: undefined` ⇒ app cũng **không** lấy chi tiết lỗi từ API |

**Đã loại trừ giả thuyết ghi chú 300 ký tự:** chạy lại với ghi chú ngắn (`Giao gio hanh chinh`) — **vẫn 400**. ⇒ không phải lỗi độ dài ghi chú.
**Đã xác nhận không có đơn nào được tạo:** về Trang chủ, khối "Đơn của tôi" + số "13 đơn đã giúp" **không đổi**.
**Impact:** ⛔ **chặn cứng** mọi TC cần một đơn NEED vừa đăng: `TC-ORD-038` · `039` · `040` · `041` · `046`–`049` · `060` · `061` · `072` · `073` · `085` · `086` · `088`.
**Route:** `/log-bug` — **P1/Blocker**, gộp 2 lỗi trên thành 1 bug (1 nguyên nhân gốc là API, 1 là thiếu error handling ở client; nên tách 2 bug nếu Dev 2 bên khác nhau).

> 🔑 **PHÁT HIỆN KỸ THUẬT QUAN TRỌNG NHẤT CHO CÁC PHIÊN SAU (đính chính map VR-002):**
> **CẢ HAI ô địa chỉ ở Bước 2/3 (`Địa chỉ lấy hàng` VÀ `Địa chỉ giao hàng`) đều là autocomplete BẮT BUỘC chọn từ `address-suggestion-N`.** Gõ tay đủ chữ, hiển thị đúng text, nhưng **không chạm gợi ý** ⇒ `Tiếp theo` **giữ `enabled=false` vĩnh viễn và app không báo gì**.
> · T đã mất ~20 call để khoanh vùng cái này, vì VR-002 ghi *"KHÔNG có dropdown gợi ý ở ô này"* — ghi chú đó **chỉ đúng cho ô địa chỉ giao khi ô ở trạng thái chưa gõ**, và VR-002 chưa bao giờ phải tự gõ ô địa chỉ lấy (khi đó nó **prefill** từ hồ sơ).
> · Nay hồ sơ tài khoản A **không còn "Địa chỉ mặc định"** (VR-003 `TC-USR-040` đã ghi nhận field rỗng và app vẫn cho lưu) ⇒ ô `Địa chỉ lấy hàng` vào bước 2 là **RỖNG**, nên mọi phiên sau **buộc** phải tự gõ + chạm gợi ý.
> · ⇒ Đây cũng là **nguồn nhiễu cực mạnh** khi chạy nhóm `TC-ORD-074`–`084`: nút khoá vì thiếu gợi ý địa chỉ **rất dễ bị kết luận nhầm** thành "app chặn đúng" ở các TC negative.

---

## TC-ORD-042: Check form OFFER đủ các nhóm trường trên một trang và không có step indicator — P2 · SC-ORD-039 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | "+ Đăng tin" → card "Tôi nhận giao hàng" *(setup)* | tap `Đăng tin` → tap card OFFER | ✅ PASS | — | form mở sạch (chưa nhập gì) |
| 3 | Cuộn toàn form | `appium_get_page_source` ×2 (nửa trên + nửa dưới) + cuộn | ✅ PASS | — | — |
| 4 | Check lần lượt các nhóm trường cùng vùng step indicator | đối chiếu 7 mục Expected | ✅ PASS | `TC-ORD-042__verify-form-offer-nhom-truong-giua.png` (+ `__verify-form-offer-nua-duoi.png`) | **7/7 nhóm có mặt**, 1 nhóm đổi hình thức — xem bảng |

| Expected yêu cầu | Có trên app? | Hình thức thật |
|---|---|---|
| nhóm "thông tin của tôi" gồm tên + SĐT | ✅ | `THÔNG TIN CỦA TÔI`: `Đặng Châu Giang` · `0964633310` |
| field điểm xuất phát | ✅ | `ĐIỂM XUẤT PHÁT (A)`, hint `Bạn đang ở đâu / xuất phát từ đâu` |
| field điểm đến | ✅ | `ĐIỂM ĐẾN (B)`, hint `Bạn sẽ đến đâu` |
| khoảng thời gian theo ngày | ✅ | `KHOẢNG THỜI GIAN (NGÀY)`: `Từ ngày` — `Đến ngày` |
| **thời gian di chuyển** | ✅ *(đổi hình thức)* | `BUỔI MONG MUỐN` — 4 chip `offer-day-part-morning/afternoon/after_work/anytime` thay cho ô giờ của v1.0 |
| checkbox điều khoản | ✅ | `Tôi đã đọc và đồng ý Điều khoản sử dụng FoxEco` |
| nút đăng tin | ✅ | `Đăng tin ngay` |
| **KHÔNG** có step indicator | ✅ | 0 node chứa chữ "Bước" *(đã assert ở `TC-ORD-003`)* |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-042__verify-form-offer-nhom-truong-giua.png` (+ `TC-ORD-042__verify-form-offer-nua-duoi.png`) — verified tồn tại
**Locators captured:** **11 element MỚI** (form OFFER — 4 chip buổi có prefix `offer-` riêng, KHÔNG dùng chung với NEED)
> ⚠️ Vế *"thời gian di chuyển"* nay là **chip BUỔI**, cùng kiểu đổi mà v1.1 đã áp cho luồng NEED (khung giờ → buổi, xem `TC-ORD-058/059`). Nhóm trường **vẫn tồn tại** nên không hạ FAIL, nhưng **câu chữ TC lỗi thời** ⇒ khuyến nghị QC cập nhật chữ, không cần DESCOPED.
> 🔎 Ảnh nửa dưới chụp khi form đã có dữ liệu (chạy liền sau `TC-ORD-043`); cấu trúc nhóm trường không phụ thuộc dữ liệu nên không ảnh hưởng điểm kiểm.

---

## TC-ORD-043: Check điểm xuất phát form OFFER sửa được, điểm đến trùng bị chặn — P2 · SC-ORD-040 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | "+ Đăng tin" → card OFFER *(setup)* | — | ✅ PASS | — | form mở sạch |
| 2-3 | Check + ghi lại giá trị field điểm xuất phát | find `xpath //android.widget.EditText[@hint="Bạn đang ở đâu / xuất phát từ đâu"]` → `get_text` = **`Bạn đang ở đâu / xuất phát từ đâu`** (= chính hint) ⇒ field **RỖNG** | ❌ **FAIL** | `TC-ORD-043__verify-diem-xuat-phat-khong-prefill.png` | Expected: điền sẵn **nơi làm việc**. Actual: **không prefill gì** |
| 4 | Xoá nội dung, gõ tên văn phòng khác, chạm chọn 1 gợi ý | `set_value "Cẩm Lệ"` → find/tap `address-suggestion-0` → `get_text` = **`FTEL Đà Nẵng Cẩm Lệ`** | ✅ PASS | — | field **sửa được** và nhận đúng giá trị đã chạm chọn ⇒ đúng Expected 4 |
| 5 | Nhập điểm đến **trùng** giá trị đó (cùng gợi ý) | `set_value "Cẩm Lệ"` → tap `address-suggestion-0` → `get_text` = **`FTEL Đà Nẵng Cẩm Lệ`** | ✅ PASS | — | A và B **trùng hệt** |
| 6 | Tick checkbox điều khoản | find/tap checkbox | ✅ PASS | — | — |
| 7 | Chọn ngày và thời gian di chuyển hợp lệ | ngày mặc định `Hôm nay`; tap `offer-day-part-afternoon` (`Chiều 13–17h`) | ✅ PASS | — | — |
| 8 | Nhấn nút đăng tin | tap `Đăng tin ngay` → **không đăng** ✓ · **KHÔNG có thông báo lỗi nào** ✗ (đã cuộn kiểm **cả 2 nửa** form) | ❌ **FAIL** | `TC-ORD-043__step8-FAIL-khong-co-thong-bao-loi-diem-den-trung.png` (+ `TC-ORD-043__step8-FAIL-diem-den-trung-diem-xuat-phat.png`) | logcat: **không có** request nào ⇒ client chặn, nhưng chặn **im lặng** |

**Result: ❌ FAIL at Step 3 và Step 8** *(riêng Expected 4 — vế sửa được — thì đúng)*
**Expected vs Actual:**
- *điểm xuất phát điền sẵn nơi làm việc* ↔ **rỗng hoàn toàn**
- *không đăng **VÀ** hiện thông báo "điểm đến phải khác điểm xuất phát"* ↔ **không đăng ĐÚNG, nhưng không một chữ thông báo nào**

**Evidence:** `screenshots/TC-ORD-043__step8-FAIL-khong-co-thong-bao-loi-diem-den-trung.png` (+ `screenshots/TC-ORD-043__verify-diem-xuat-phat-khong-prefill.png`, `screenshots/TC-ORD-043__step8-FAIL-diem-den-trung-diem-xuat-phat.png`) — verified tồn tại
**Impact:** 🐞 **2 bug, cả 2 đều thuộc họ đã biết:**
> 1. **Chặn im lặng lan sang luồng OFFER** (họ F3/F7): nhánh *điểm đến trùng điểm xuất phát* bị chặn mà không báo. ⚠️ Đáng chú ý: **cùng form OFFER** vẫn báo lỗi inline đúng ở nhánh *chưa chọn buổi* (`Chọn ít nhất 1 buổi`, xem `TC-ORD-050`) ⇒ **không phải thiếu framework hiển thị lỗi**, mà là **thiếu ở từng nhánh validate** — y hệt kết luận VR-002 cho luồng NEED. Cũng **cùng cặp nghiệp vụ** với `TC-ORD-083`/`084` (địa chỉ giao trùng địa chỉ lấy, FAIL ở VR-002) ⇒ `/log-bug` nên **gộp 3 TC này vào 1 bug**.
> 2. **Prefill địa chỉ từ hồ sơ/HRIS không hoạt động** — cùng gốc với `TC-USR-040` (VR-003 FAIL: *"địa chỉ không prefill HRIS"*) và là nguyên nhân `TC-ORD-017`/`027` mất prefill.

---

## TC-ORD-015: Check bước 2 tự điền tên và SĐT người gửi từ hồ sơ — P2 · SC-ORD-014 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Ghi lại tên hiển thị của hồ sơ *(setup)* | oracle = header Trang chủ `Xin chào, **Đặng Châu Giang**` (ảnh `_setup__preflight-launch.png`) | ✅ PASS | — | ⚠️ đọc từ Trang chủ thay vì tab `Cá nhân` — cùng nguồn hồ sơ, rẻ hơn 2 lần điều hướng |
| 2 | Mở wizard NEED, điền bước 1, "Tiếp theo" *(setup)* | chip `Tài liệu` + `Thấp` + `Dưới 5 kg` + `Nhỏ` + 1 ảnh → `Tiếp theo` | ✅ PASS | — | — |
| 3 | Check giá trị 2 field nhóm "Người gửi" | `get_text (//android.widget.EditText)[1]` = `Đặng Châu Giang` · `[2]` = `0964633310` | ✅ PASS | `TC-ORD-015__verify-prefill-ten-sdt-nguoi-gui.png` | tên **khớp đúng** hồ sơ; SĐT **có điền sẵn** ⇒ đúng cả 2 vế Expected |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-015__verify-prefill-ten-sdt-nguoi-gui.png` — verified tồn tại
> 🔎 SĐT prefill nay là `0964633310`, **khác** `0912345670` mà VR-002 ghi — hồ sơ đã bị đổi ở VR-003 (module USR). Không ảnh hưởng verdict (TC chỉ đòi "được điền sẵn một số điện thoại").

---

## TC-ORD-016: Check field tên người gửi chỉ đọc, không bị xoá khi chạm — P2 · SC-ORD-015 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Vào bước 2, ghi lại giá trị field tên người gửi | `get_text` = `Đặng Châu Giang` | ✅ PASS | — | page source: ô này `enabled="false"` |
| 3 | Chạm vào field tên người gửi | `appium_gesture(tap)` | ✅ PASS | — | — |
| 4 | Check bàn phím và giá trị trong field | `appium_mobile_keyboard(is_shown)` → **`false`** · `get_text` = `Đặng Châu Giang` | ✅ PASS | `TC-ORD-016__verify-ten-nguoi-gui-chi-doc.png` | bàn phím **KHÔNG mở**, giá trị **giữ nguyên**, không xoá trắng ⇒ đúng Expected |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-016__verify-ten-nguoi-gui-chi-doc.png` — verified tồn tại

---

## TC-ORD-017: Check field địa chỉ lấy hàng điền sẵn theo nơi làm việc — P2 · SC-ORD-016 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Vào bước 2 *(setup)* | — | ✅ PASS | — | — |
| 3 | Check giá trị field địa chỉ lấy hàng | `get_text (//android.widget.EditText)[3]` = **`Địa chỉ lấy hàng`** (= chính hint) ⇒ field **RỖNG** | ❌ **FAIL** | `TC-ORD-017__step3-FAIL-dia-chi-lay-hang-khong-prefill.png` | Expected: điền sẵn địa chỉ nơi làm việc, **không phải chỉ có placeholder**. Actual: **chỉ có placeholder** |

**Result: ❌ FAIL at Step 3**
> ⚠️ **ĐỔI VERDICT so với VR-002** — verdict cũ của TC này là ✅, nay là ❌.
**Expected vs Actual:** *prefill địa chỉ nơi làm việc* ↔ **rỗng, chỉ có placeholder**
**Evidence:** `screenshots/TC-ORD-017__step3-FAIL-dia-chi-lay-hang-khong-prefill.png` — verified tồn tại
**Impact:** 🐞 **Không phải TC lỗi thời — là hồi quy/lỗi thật, cùng gốc với `TC-USR-040`** (VR-003 FAIL: *"Địa chỉ mặc định không prefill từ HRIS"*). Chuỗi nhân quả đã đo được:
> `TC-USR-040` (prefill HRIS hỏng) → hồ sơ tài khoản A **không có địa chỉ mặc định** → `TC-ORD-017`/`027` mất prefill → **bước 2 không thể hoàn tất nếu không tự gõ + chạm gợi ý** → là nguồn nhiễu cho toàn nhóm `074`–`084`.
> ⇒ `/log-bug` nên **gộp** `TC-USR-040` + `TC-ORD-017` + `TC-ORD-043` (điểm xuất phát OFFER cũng không prefill) vào **1 bug prefill địa chỉ**.

---

## TC-ORD-029: Check field địa chỉ dùng dropdown autocomplete và không có chip preset văn phòng — P3 · SC-ORD-027 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 *(setup)* | — | ✅ PASS | — | — |
| 2 | Check vùng quanh 2 field địa chỉ, tìm chip preset văn phòng | quét ảnh + page source cả 2 vùng | ✅ PASS | `TC-ORD-029__verify-dropdown-autocomplete-khong-co-chip-preset.png` | **KHÔNG** có chip preset nào quanh cả 2 field ⇒ đúng Expected 2 |
| 3 | Gõ một phần tên văn phòng vào field địa chỉ | `set_value "Cẩm Lệ"` | ✅ PASS | — | — |
| 4 | Check cách gợi ý hiện ra | **dropdown ngay dưới ô**, 2 mục: `FTEL Đà Nẵng Cẩm Lệ` · `363 Nguyễn Hữu Thọ / Cẩm Lệ`; locator `accessibility id "address-suggestion-0/1"` | ✅ PASS | *(cùng ảnh)* | đúng dạng **dropdown autocomplete theo chuỗi đang gõ** ⇒ đúng Expected 4 |

**Result: ✅ PASS (4 steps, 2 expected)**
**Evidence:** `screenshots/TC-ORD-029__verify-dropdown-autocomplete-khong-co-chip-preset.png` — verified tồn tại
> 🔑 TC này chính là **bằng chứng trực tiếp** cho phát hiện lớn của phiên: ô địa chỉ là autocomplete **phải chạm gợi ý** (xem khối 🔑 ở `TC-ORD-004`).

---

## TC-ORD-023: Check để trống nhóm người nhận thì không qua được bước 3 — **P1** · SC-ORD-022 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 *(setup)* | — | ✅ PASS | — | — |
| 2 | Để trống ô email + cả 3 field tên/SĐT/địa chỉ người nhận | giữ nguyên form sạch | ✅ PASS | — | ảnh chứng minh cả 4 ô chỉ có placeholder |
| 3 | Nhập địa chỉ lấy hàng | `set_value "Cẩm Lệ"` → tap `address-suggestion-0` → `FTEL Đà Nẵng Cẩm Lệ` | ✅ PASS | — | — |
| 4 | Chọn ngày và khung giờ hợp lệ | ngày mặc định `Hôm nay`; tap `day-part-afternoon` | ✅ PASS | — | — |
| 5 | Nhấn "Tiếp theo" | `enabled=false` → tap → **KHÔNG** sang bước 3 ✓ · cuộn về nhóm `NGƯỜI NHẬN`: **KHÔNG có thông báo lỗi nào** ✗ | ❌ **FAIL** | `TC-ORD-023__step5-FAIL-khong-co-thong-bao-loi-nhom-nguoi-nhan.png` | Expected đòi **cả 2**: không sang bước 3 **VÀ** hiện thông báo lỗi ở nhóm "Người nhận" |

**Result: ❌ FAIL at Step 5** *(vế chặn ĐÚNG, vế thông báo SAI)*
**Evidence:** `screenshots/TC-ORD-023__step5-FAIL-khong-co-thong-bao-loi-nhom-nguoi-nhan.png` — verified tồn tại
**Impact:** 🐞 **Nhánh thứ 6 của bug chặn im lặng (F3/F7)** — và là nhánh **P1**. Gộp vào bug F3/F7 khi `/log-bug`.

---

## TC-ORD-019: Check email nội bộ tra được tự điền ba trường người nhận — **P1** · SC-ORD-018 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 *(setup)* | — | ✅ PASS | — | — |
| 2-3 | Nhập `stag_anhdc4@fpt.com` rồi rời ô | `set_value` → tap nhãn `NGƯỜI NHẬN` để blur | ✅ PASS | — | — |
| 4 | Check thông báo + giá trị 3 field người nhận | thông báo **CÓ** ✓ · tên ✓ · SĐT ✓ · **địa chỉ giao RỖNG** ✗ | ❌ **FAIL** | `TC-ORD-019__step4-FAIL-autofill-thieu-o-dia-chi-giao.png` | autofill **2/3** field, thiếu đúng ô địa chỉ |

| Expected | Actual |
|---|---|
| thông báo "Đã tìm thấy trong hệ thống nội bộ" | ✅ `Đã tìm thấy trong hệ thống nội bộ · vui lòng bổ sung SĐT/địa chỉ giao còn thiếu.` |
| tên người nhận điền sẵn | ✅ `Đặng Châu Anh` |
| SĐT người nhận điền sẵn | ✅ `0343439724` |
| **địa chỉ người nhận điền sẵn** | ❌ **rỗng** |

**Result: ❌ FAIL at Step 4**
**Evidence:** `screenshots/TC-ORD-019__step4-FAIL-autofill-thieu-o-dia-chi-giao.png` — verified tồn tại
**Impact:** 🐞 **Xác nhận độc lập `TC-ORD-074`** (v1.1 **P1**, FAIL ở VR-002 cùng lý do) ⇒ 2 TC ở 2 version cùng chỉ vào **1 bug**. ⚠️ Lưu ý nghịch lý cần BA chốt: **chính thông báo của app** nói *"vui lòng bổ sung SĐT/địa chỉ giao còn thiếu"* — tức app **tự nhận** là không điền đủ; nhưng nó **lại điền được SĐT**. Vậy hành vi đúng là gì: autofill 3 hay 2 field? ⇒ `C-ORD-??` cần mở trước khi log bug.

---

## TC-ORD-020: Check email không tra được hiện thông báo nhập thủ công — P2 · SC-ORD-019 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 *(setup)* | — | ✅ PASS | — | — |
| 2-3 | Nhập email nội bộ không tồn tại rồi rời ô | `set_value "stag_khongtontai9999@fpt.com"` → blur | ✅ PASS | — | — |
| 4 | Check thông báo + giá trị 3 field người nhận | thông báo **CÓ**; 3 field tên/SĐT/địa chỉ **đều rỗng** | ✅ PASS | `TC-ORD-020__verify-email-khong-tra-duoc.png` | đúng cả 2 vế Expected |

Chuỗi thật: `Không tìm thấy email này — vui lòng nhập tay thông tin bên dưới.`

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-020__verify-email-khong-tra-duoc.png` — verified tồn tại
> 🚩 Câu chữ khác Expected (*"Không tìm thấy · nhập thủ công"*) nhưng **đúng nghĩa** ⇒ PASS. Đây chính là chuỗi **F5** mà VR-002 đã raise là *câu chữ còn của v1.0* — vẫn chưa sửa.

---

## TC-ORD-021: Check email sai định dạng và ngoài tên miền đều bị chặn — P2 · SC-ORD-020 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 *(setup)* | — | ✅ PASS | — | — |
| 2 | Nhập chuỗi email **thiếu `@`** rồi rời ô | `set_value "stag_anhdc4.fpt.com"` → blur bằng tap nhãn | ✅ PASS | — | — |
| 3 | Check thông báo + 3 field người nhận | **KHÔNG có thông báo nào** (đã quét `textContains` cho `định dạng` · `không hợp lệ` · `Không tìm thấy` — cả 3 NOT FOUND) ✗ · 3 field **không** tự điền ✓ | ❌ **FAIL** | `TC-ORD-021__step3-FAIL-khong-bao-loi-email-sai-dinh-dang.png` (+ `__verify-email-thieu-a-coi.png`) | — |
| 4 | Nhập email đúng định dạng nhưng **ngoài tên miền** rồi rời ô | `set_value "nguoingoai@gmail.com"` → blur | ✅ PASS | — | — |
| 5 | Check thông báo + 3 field người nhận | thông báo **CÓ** ✓ · 3 field **không** tự điền ✓ | ✅ PASS | `TC-ORD-021__verify-email-ngoai-ten-mien.png` | — |

**Result: ❌ FAIL at Step 3** *(riêng Expected 5 — email ngoài tên miền — thì đúng)*
**Evidence:** `screenshots/TC-ORD-021__step3-FAIL-khong-bao-loi-email-sai-dinh-dang.png` (+ 2 ảnh `__verify`) — verified tồn tại
**Impact:** 🐞 **Xác nhận độc lập `TC-ORD-077`** (v1.1, FAIL ở VR-002: email sai định dạng bị chặn im lặng) ⇒ gộp vào bug F3/F7.
> ⚠️ **Chi tiết đáng ngờ cho BA:** email **ngoài tên miền** lại nhận đúng thông báo *"Không tìm thấy email này — vui lòng nhập tay…"* — tức app xử lý nó như *"nội bộ nhưng chưa có trong danh bạ"*, **không** phải *"sai tên miền"*. Thông báo này còn **mời người dùng nhập tay**, trong khi `TC-ORD-078` (v1.1) yêu cầu **chặn**. Verdict TC-021 không đổi (Expected chỉ đòi "có thông báo lỗi"), nhưng **nội dung thông báo sai nghiệp vụ** ⇒ nên raise cùng **F5**.

---

## TC-ORD-024: Check tên người nhận nhận 2 và 60 ký tự, chặn 1 và 61 — P2 · SC-ORD-023 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 2-3 | Nhập **1 ký tự** rồi rời ô → check thông báo | `set_value "A"` → blur → quét `textContains("Tên")` = **NOT FOUND** | ❌ **FAIL** | `TC-ORD-024__step3-FAIL-ten-1-ky-tu-khong-bao-loi.png` | Expected: **hiện** thông báo lỗi. Actual: **không có** |
| 4-5 | Nhập **2 ký tự** rồi rời ô → check | `set_value "Ab"` → không thông báo | ✅ PASS | — | đúng Expected 5 |
| 6-7 | Nhập **60 ký tự** rồi rời ô → check | `set_value` 60 ký tự → không thông báo | ✅ PASS | — | đúng Expected 7 |
| 8-9 | Nhập tiếp 1 ký tự (→61) → check nội dung + thông báo | `set_value("Z", w3cActions)` → `get_text` = **vẫn đúng 60 ký tự**, không có `Z` | ✅ PASS | `TC-ORD-024__verify-ten-nguoi-nhan-bien-60-61.png` | ký tự 61 **không được nhận** ⇒ thoả vế đầu của Expected 9 |

**Result: ❌ FAIL at Step 3** *(3/4 expected còn lại đều đúng)*
**Evidence:** `screenshots/TC-ORD-024__verify-ten-nguoi-nhan-bien-60-61.png` (+ `__step3-FAIL-...`) — verified tồn tại
**Impact:** 🐞 Nhánh nữa của **chặn im lặng** — nhưng là loại *"không báo khi dữ liệu sai"* ở tầng field. Gộp F3/F7.

---

## TC-ORD-025: Check SĐT người nhận chỉ hợp lệ khi đủ 10 số bắt đầu 0 — P2 · SC-ORD-023 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 2-3 | **9 số** rồi rời ô → check | `set_value "098765432"` → find `text("Số điện thoại không hợp lệ")` **FOUND** | ✅ PASS | `TC-ORD-025__step3-FAIL-sdt-9-so-khong-bao-loi.png` *(tên file đặt theo dự đoán ban đầu; kết quả thực tế là **có** báo lỗi ⇒ PASS)* | đúng Expected 3 |
| 4-5 | **10 số bắt đầu 0** rồi rời ô → check | `set_value "0987654321"` → lỗi **NOT FOUND** | ✅ PASS | `TC-ORD-025__verify-sdt-10-so-hop-le.png` | đúng Expected 5 |
| 6-7 | **11 số** rồi rời ô → check | `set_value "09876543210"` → lỗi **FOUND** | ✅ PASS | — | đúng Expected 7 |
| 8-9 | **10 số không bắt đầu 0** rồi rời ô → check | `set_value "9876543210"` → lỗi **FOUND** | ✅ PASS | `TC-ORD-025__verify-sdt-khong-bat-dau-0-bi-chan.png` | đúng Expected 9 |
| 10-11 | Chuỗi **có chữ cái** rồi rời ô → check | `set_value "abc123xyz0"` → ô **nhận** ký tự chữ, nhưng lỗi **FOUND** | ✅ PASS | `TC-ORD-025__verify-sdt-co-chu-cai-bi-bao-loi.png` | Expected là **HOẶC** (không nhận **hoặc** báo lỗi) ⇒ thoả vế sau |

**Result: ✅ PASS (11 steps, 5 expected — 5/5)**
**Evidence:** `screenshots/TC-ORD-025__verify-sdt-10-so-hop-le.png` (+ 3 ảnh khác) — verified tồn tại
> 🔑 **Dữ kiện quan trọng cho bug F3/F7:** ô **SĐT người nhận CÓ** lỗi inline đầy đủ (`Số điện thoại không hợp lệ`) ở **cả 4 nhánh sai**. Cùng màn, cùng form, mà ô **email** và ô **tên** thì **không có lỗi nào**. ⇒ Một lần nữa khẳng định: **không phải thiếu framework hiển thị lỗi, mà là thiếu ở từng nhánh** — đây là lập luận mạnh nhất để Dev không đóng bug F3/F7 bằng lý do *"app chưa có cơ chế báo lỗi"*.

---

## TC-ORD-055: Check ô địa chỉ nhận đúng hai trăm ký tự và chặn ký tự thứ hai trăm lẻ một — P3 · SC-ORD-026 *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 *(setup)* | — | ✅ PASS | — | — |
| 2 | Nhập chuỗi **đúng 200 ký tự** vào ô "Địa chỉ giao hàng" | `set_value` 200 ký tự → `get_text` khớp từng ký tự | ✅ PASS | — | thuộc tính ô: `max-text-length=200` |
| 3 | Nhập thêm 1 ký tự nữa vào cuối ô | `set_value("Z", w3cActions=true)` → gõ vào ô đang focus | ✅ PASS | — | — |
| 4 | Check số ký tự thực tế còn lại trong ô | `get_text` = **vẫn đúng 200 ký tự**, không có `Z` | ✅ PASS | `TC-ORD-055__verify-dia-chi-giao-dung-200-ky-tu.png` | ký tự 201 **không được nhận** ⇒ đúng Expected |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-055__verify-dia-chi-giao-dung-200-ky-tu.png` — verified tồn tại

---

## TC-ORD-032: Check chọn Giờ nào cũng được tự bỏ chọn các buổi đang chọn — P2 · SC-ORD-029 *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 *(setup)* | — | ✅ PASS | — | — |
| 2-3 | Chọn buổi "Sáng" rồi chọn thêm "Chiều" *(setup)* | tap `day-part-morning` (`Chiều` đã chọn sẵn từ TC trước) | ✅ PASS | `TC-ORD-032__pre-sang-va-chieu-dang-chon.png` | ảnh chứng minh **cả 2 chip cùng ở trạng thái chọn** (viền + chữ cam) |
| 4 | Chọn "Giờ nào cũng được" | tap `day-part-anytime` | ✅ PASS | — | — |
| 5 | Check trạng thái chọn của cả bốn buổi | đọc bằng ảnh *(bẫy **T1**)* | ✅ PASS | `TC-ORD-032__verify-gio-nao-cung-duoc-bo-chon-cac-buoi.png` | **chỉ còn** `Giờ nào cũng được` được chọn; `Sáng` + `Chiều` **tự bỏ chọn**; `Sau giờ làm` vẫn không chọn ⇒ đúng Expected |

**Result: ✅ PASS (5 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-032__verify-gio-nao-cung-duoc-bo-chon-cac-buoi.png` (+ `__pre-sang-va-chieu-dang-chon.png`) — verified tồn tại

---

## TC-ORD-018: Check SĐT người gửi không tự đổi giá trị trong cùng phiên — P3 · SC-ORD-017 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Vào bước 2, ghi lại SĐT người gửi | `get_text` = **`0964633310`** | ✅ PASS | — | — |
| 3 | Nhập email người nhận | `stag_anhdc4@fpt.com` → autofill chạy | ✅ PASS | — | — |
| 4 | Nhập địa chỉ lấy hàng và địa chỉ giao hàng | cả 2 ô, có chạm gợi ý | ✅ PASS | — | — |
| 5 | Chọn ngày và khung giờ | ngày `Hôm nay`; nhiều lượt đổi buổi (TC-032) | ✅ PASS | — | — |
| 6-7 | Cuộn lại nhóm "Người gửi", check giá trị SĐT | `xpath //android.widget.EditText[@hint="Số điện thoại" and @enabled="true"]` → `get_text` = **`0964633310`** | ✅ PASS | `TC-ORD-018__verify-sdt-nguoi-gui-khong-doi.png` | **không đổi** sau toàn bộ thao tác, kể cả sau khi qua/về giữa bước 2 ↔ bước 3 |

**Result: ✅ PASS (7 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-018__verify-sdt-nguoi-gui-khong-doi.png` — verified tồn tại
> ⚠️ **Bẫy locator mới, ghi cho phiên sau:** `(//android.widget.EditText)[N]` **KHÔNG ổn định** ở màn này — màn render **lazy**, số EditText trong cây đổi theo vị trí cuộn. Lúc đang ở cuối form, `[2]` trả về **ô tên người nhận uỷ quyền** chứ không phải SĐT người gửi. ⇒ dùng `xpath` theo **`@hint` + `@enabled`** như trên, hoặc `resourceId`.

---

## TC-ORD-079: Check số điện thoại uỷ quyền sai định dạng bị báo lỗi và chặn — P2 · SC-ORD-061 *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 *(setup)* | — | ✅ PASS | — | — |
| 2 | Nhấn "+ Thêm người nhận uỷ quyền" | find/tap `descriptionStartsWith("Thêm người nhận uỷ quyền")` → khối mở ra | ✅ PASS | — | ⚠️ `accessibility id "alt-receiver-expand-button"` **NOT FOUND** (VR-002 ghi ⚠️ Inferred) — phải dùng `descriptionStartsWith` |
| 3 | Nhập "Nguyễn Văn Bảy" vào ô tên uỷ quyền | `set_value` vào `alt-receiver-name-input` | ✅ PASS | — | — |
| 4 | Nhập "123" vào ô SĐT uỷ quyền | `set_value` vào `alt-receiver-phone-input` | ✅ PASS | — | — |
| 5 | Nhấn "Tiếp theo" | tap | ✅ PASS | — | — |
| 6 | Check màn + thông báo lỗi ở ô SĐT | vẫn `Bước 2 / 3` ✓ · `text("Số điện thoại không hợp lệ")` **FOUND**, nằm **ngay dưới ô SĐT uỷ quyền** ✓ | ✅ PASS | `TC-ORD-079__verify-sdt-uy-quyen-sai-dinh-dang-bao-loi.png` | đúng cả 2 vế Expected |

**Result: ✅ PASS (6 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-079__verify-sdt-uy-quyen-sai-dinh-dang-bao-loi.png` — verified tồn tại
**Locators captured:** **5 element MỚI** (`alt-receiver-box` · `alt-receiver-collapse-button` · `alt-receiver-name-input` maxlen 60 · `alt-receiver-phone-input` maxlen 12 · `alt-receiver-note-input` maxlen 60)
> ⚠️ **Đã loại nhiễu trước khi kết luận:** ô SĐT **người nhận** lúc đó đang giữ `abc123xyz0` (sai) và dùng **cùng chuỗi lỗi**. Đã sửa ô đó về `0343439724` hợp lệ rồi mới chụp — ảnh cho thấy ô người nhận **không** có lỗi, chỉ ô uỷ quyền có.

---

## TC-ORD-081: Check tên người nhận uỷ quyền nhận đúng hai và sáu mươi ký tự — P2 · SC-ORD-061 *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Vào bước 2, mở khối uỷ quyền *(setup)* | — | ✅ PASS | — | ⚠️ trước khi kiểm, đã dựng form **hợp lệ hoàn toàn** (email tra được + 2 địa chỉ chạm gợi ý + buổi) để `Tiếp theo` `enabled=true` — nếu không, mọi lần "không đi tiếp được" đều **vô nghĩa** vì bị chặn bởi lý do khác |
| 3 | Nhập **1 ký tự** vào ô tên rồi nhấn "Tiếp theo" | `set_value "A"` → tap | ✅ PASS | `TC-ORD-081__verify-ten-uy-quyen-1-ky-tu-bi-chan.png` | vẫn `Bước 2 / 3` + lỗi đỏ **`Tên phải từ 2–60 ký tự`** ngay dưới ô |
| 4 | Nhập **2 ký tự** rồi nhấn "Tiếp theo" | `set_value "Ab"` → tap → find `text("Bước 3 / 3")` OK | ✅ PASS | `TC-ORD-081__verify-ten-uy-quyen-2-ky-tu-di-tiep-duoc.png` | **đi tiếp được** ⇒ đúng Expected |
| 5 | Quay lại bước 2, nhập **60 ký tự** rồi "Tiếp theo" | tap `Quay lại` → `set_value` 60 ký tự → tap → `Bước 3 / 3` OK | ✅ PASS | `TC-ORD-081__verify-ten-uy-quyen-60-ky-tu-di-tiep-duoc-61-bi-chan.png` | **đi tiếp được** |
| 6-7 | Nhập chuỗi **61 ký tự**, check trạng thái ô | `set_value("Z", w3cActions)` → `get_text` = **vẫn 60 ký tự** | ✅ PASS | *(cùng ảnh)* | ký tự 61 **không nhập được** ⇒ đúng Expected |

**Result: ✅ PASS (7 steps, 1 expected — 4/4 nhánh)**
**Evidence:** `screenshots/TC-ORD-081__verify-ten-uy-quyen-1-ky-tu-bi-chan.png` (+ 2 ảnh `__verify` khác) — verified tồn tại
> 🔑 **Dữ kiện nữa cho F3/F7:** ô tên **uỷ quyền** CÓ lỗi rõ ràng `Tên phải từ 2–60 ký tự`, trong khi ô tên **người nhận** (`TC-ORD-024`) ở **cùng màn** thì **không có lỗi nào** cho cùng loại vi phạm. ⇒ Củng cố: lỗi hiển thị được cài **rời rạc theo từng ô**, không phải thiếu cơ chế.

---

## TC-ORD-026: Check địa chỉ giao trùng địa chỉ lấy hàng thì bị chặn — P2 · SC-ORD-024 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 2-3 | Nhập địa chỉ lấy hàng, **chạm chọn 1 gợi ý**, ghi lại | `set_value "Cẩm Lệ"` → tap `address-suggestion-0` → **`FTEL Đà Nẵng Cẩm Lệ`** | ✅ PASS | — | — |
| 4 | Nhập địa chỉ giao và **chạm đúng gợi ý trùng** giá trị đó | `set_value "Cẩm Lệ"` → tap `address-suggestion-0` → `get_text` = **`FTEL Đà Nẵng Cẩm Lệ`** | ✅ PASS | — | 2 ô **trùng hệt** |
| 5-6 | Nhập đủ thông tin người nhận + chọn ngày/khung giờ | email tra được + tên + SĐT + buổi | ✅ PASS | — | — |
| 7 | Nhấn "Tiếp theo" | `enabled=true` → tap → vẫn `Bước 2 / 3` ✓ · lỗi đỏ **`Địa chỉ giao phải khác địa chỉ lấy hàng`** hiện **ngay dưới ô địa chỉ giao** ✓ | ✅ PASS | `TC-ORD-026__verify-loi-trung-dia-chi-hien-dung.png` | đúng **cả 2 vế** Expected |

**Result: ✅ PASS (7 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-026__verify-loi-trung-dia-chi-hien-dung.png` — verified tồn tại
> 🔴🔑 **KẾT QUẢ NÀY BÁC BỎ MỘT PHẦN KẾT LUẬN CỦA VR-002.** VR-002 ghi `TC-ORD-083`/`084` FAIL với lý do *"chặn nhưng im lặng, không có lỗi ở ô Địa chỉ giao (F3)"* và gộp chúng vào bug chặn-im-lặng. Thực tế: **quy tắc trùng địa chỉ CÓ thông báo lỗi đầy đủ** — chỉ cần 2 địa chỉ được **chạm chọn từ gợi ý**. Xem `TC-ORD-083` bên dưới để biết vì sao VR-002 không thấy nó.

---

## TC-ORD-083: Check địa chỉ giao trùng hệt địa chỉ lấy bị chặn — P2 · SC-ORD-063 *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 với **form hoàn toàn sạch** *(setup)* | thoát wizard, vào lại, điền lại bước 1 | ✅ PASS | — | ⚠️ **cố ý làm sạch** — xem khối ♻️ dưới |
| 2 | Nhập `Số 7 ngõ 12 Trần Duy Hưng` vào ô "Địa chỉ lấy hàng" *(setup)* | `set_value` — **gõ tay, KHÔNG chạm gợi ý** (đúng chữ của Steps) | ✅ PASS | — | chuỗi này không khớp gợi ý nào của STG |
| 3 | Nhập **đúng chuỗi đó** vào ô "Địa chỉ giao hàng" | `set_value` cùng chuỗi | ✅ PASS | — | — |
| 4 | Nhấn "Tiếp theo" | `enabled=false` → tap | ✅ PASS | — | — |
| 5 | Check màn + thông báo lỗi ở ô địa chỉ giao | vẫn `Bước 2 / 3` ✓ · `text("Địa chỉ giao phải khác địa chỉ lấy hàng")` **NOT FOUND** ✗ | ❌ **FAIL** | `TC-ORD-083__step5-FAIL-khong-co-loi-o-o-dia-chi-giao.png` | — |

**Result: ❌ FAIL at Step 5** *(vế chặn ĐÚNG, vế thông báo SAI)* — **giữ nguyên verdict FAIL của VR-002, nhưng ĐỔI HẲN nguyên nhân.**
**Evidence:** `screenshots/TC-ORD-083__step5-FAIL-khong-co-loi-o-o-dia-chi-giao.png` (+ `TC-ORD-083__verify-loi-cu-khong-tu-xoa-khi-da-sua-dia-chi.png`) — verified tồn tại

🔍 **Cơ chế thật (đo được, khác hẳn quy kết của VR-002):**

| Cách nhập 2 địa chỉ | Nút `Tiếp theo` | Nhấn vào thì sao | Có báo lỗi trùng? |
|---|---|---|---|
| **Gõ tay, không chạm gợi ý** *(đúng Steps của TC-083)* | `enabled=false` | không gì xảy ra | ❌ **không** — validate **chưa bao giờ chạy tới** luật trùng địa chỉ |
| **Chạm chọn từ gợi ý** *(`TC-ORD-026`)* | `enabled=true` | không sang bước 3 | ✅ **có** — `Địa chỉ giao phải khác địa chỉ lấy hàng` |

⇒ Cái mà VR-002 ghi là *"bug chặn im lặng ở nhánh trùng địa chỉ"* thực ra là **bug chặn im lặng ở nhánh "địa chỉ chưa chọn từ gợi ý"**. Luật trùng địa chỉ **không có lỗi**.
**Đề nghị `/log-bug`:** **gỡ `TC-ORD-083`/`084` khỏi danh sách dẫn chứng của bug F3/F7 nhánh-trùng-địa-chỉ**, chuyển chúng sang dẫn chứng cho bug **"ô địa chỉ bắt buộc chọn gợi ý nhưng không báo gì"** (cùng bug đã chặn `TC-ORD-004`).

> ♻️ **Vì sao phải chạy lại từ form sạch — và một bug mới lòi ra:** lượt đầu t chạy TC-083 **ngay sau** `TC-ORD-026`, và thấy lỗi `Địa chỉ giao phải khác địa chỉ lấy hàng` **vẫn hiện** ⇒ suýt kết luận PASS. Kiểm chứng lại: đổi ô địa chỉ giao sang chuỗi **hoàn toàn khác** (`Số 99 Nguyễn Trãi Hà Nội`) mà **lỗi vẫn còn nguyên**.
> 🐞 ⇒ **Ứng viên bug MỚI: thông báo lỗi validate KHÔNG tự xoá khi người dùng đã sửa dữ liệu** (lỗi "dính"). Bằng chứng: `TC-ORD-083__verify-loi-cu-khong-tu-xoa-khi-da-sua-dia-chi.png`. Mức độ trung bình — gây hiểu nhầm cho người dùng **và** làm sai lệch kết quả test (đúng như suýt xảy ra ở đây). ⇒ Đã chạy lại TC từ form sạch để verdict không dính lỗi này.

---

## TC-ORD-084: Check địa chỉ giao chỉ khác khoảng trắng đầu cuối vẫn bị chặn — P2 · SC-ORD-063 *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Form sạch, nhập `Số 7 ngõ 12 Trần Duy Hưng` vào ô địa chỉ lấy *(setup)* | gõ tay | ✅ PASS | — | nối tiếp state của `TC-ORD-083` |
| 3 | Nhập `␣␣Số 7 ngõ 12 Trần Duy Hưng␣␣` (thêm khoảng trắng đầu/cuối) vào ô địa chỉ giao | `set_value` | ✅ PASS | — | — |
| 4 | Nhấn "Tiếp theo" | tap | ✅ PASS | — | — |
| 5 | Check màn + thông báo lỗi ở ô địa chỉ giao | vẫn `Bước 2 / 3` ✓ · `textContains("phải khác")` **NOT FOUND** ✗ | ❌ **FAIL** | `TC-ORD-084__step5-FAIL-khong-co-loi-khi-chi-khac-khoang-trang.png` | — |

**Result: ❌ FAIL at Step 5** — **cùng cơ chế `TC-ORD-083`**, không phải lỗi riêng của biên khoảng trắng.
**Evidence:** `screenshots/TC-ORD-084__step5-FAIL-khong-co-loi-khi-chi-khac-khoang-trang.png` — verified tồn tại
> ⚠️ **Lưu ý quan trọng cho QC:** vì cả 2 địa chỉ đều gõ tay nên validate **chưa chạy tới luật trim**, ⇒ **phiên này KHÔNG kết luận được** app có trim khoảng trắng khi so sánh hay không. Ghi chú của VR-002 (*"So sánh CÓ trim (biên khoảng trắng chặn đúng)"*) là **suy diễn không có căn cứ** — app chặn vì **địa chỉ chưa chọn gợi ý**, không phải vì so sánh sau trim. Muốn kiểm đúng biên trim thì **phải sửa Steps**: chọn gợi ý cho ô lấy hàng, rồi ô giao hàng gõ đúng chuỗi gợi ý đó + khoảng trắng — nhưng khi đó ô giao lại không được chọn từ gợi ý ⇒ **TC-084 hiện KHÔNG thực thi được đúng ý đồ trên app v1.1**. Đề nghị QC xem lại thiết kế TC này.

---

## TC-ORD-022: Check SĐT do app tự điền từ danh bạ được nhận là hợp lệ — P2 · SC-ORD-021 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 *(setup)* | form sạch | ✅ PASS | — | — |
| 2 | Nhập `stag_anhdc4@fpt.com` và rời ô để app tự điền *(setup)* | `set_value` → autofill chạy | ✅ PASS | — | — |
| 3-4 | **Không sửa** field SĐT người nhận, ghi lại giá trị app vừa điền | `get_text resourceId("receiver-phone-input")` = **`0343439724`** | ✅ PASS | — | ⛔ không chạm vào ô này nữa cho tới hết TC |
| 5 | Nhập địa chỉ lấy hàng và địa chỉ giao hàng | cả 2 ô: `set_value` + tap `address-suggestion-0` | ✅ PASS | — | — |
| 6 | Chọn ngày và khung giờ hợp lệ | ngày `Hôm nay`; tap `day-part-afternoon` | ✅ PASS | — | — |
| 7 | Nhấn "Tiếp theo" | tap → find `text("Bước 3 / 3")` **OK** · **không** có lỗi nào ở ô SĐT người nhận | ✅ PASS | `TC-ORD-022__verify-sdt-autofill-duoc-chap-nhan-sang-buoc-3.png` | đúng cả 2 vế Expected |

**Result: ✅ PASS (7 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-022__verify-sdt-autofill-duoc-chap-nhan-sang-buoc-3.png` — verified tồn tại

---

## TC-ORD-033: Check khung giờ mặc định đã trôi qua thì bị chặn khi submit — P3 · SC-ORD-030 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 *(setup)* | — | ✅ PASS | — | — |
| 2 | **Không thao tác gì với field khung giờ**, để form mở >15 phút cho tới khi **khung giờ mặc định** trôi qua | ⛔ **KHÔNG TẠO ĐƯỢC TIỀN ĐỀ** — v1.1 thay "khung giờ" bằng **4 chip BUỔI** và **không chip nào được chọn sẵn** | 🚫 **BLOCKED** | `TC-ORD-033__step5-BLOCKED-v11-khong-co-khung-gio-mac-dinh.png` | ảnh cho thấy cả 4 chip buổi đều **không được chọn** khi vừa mở bước 2 |
| 3-5 | — | ⏭ SKIPPED | — | — | blocked ở step 2 |

**Result: 🚫 BLOCKED at Step 2**
**Reason:** TC giả định tồn tại **"khung giờ mặc định"**. Trên v1.1 **không có mặc định nào** — sự kiện này đã được `TC-ORD-058` (v1.1) đo và ghi FAIL ở VR-002 (*"buổi mong muốn không có mặc định"*). Không có mặc định ⇒ **không thể có "mặc định đã trôi qua"** ⇒ tiền đề của TC không dựng được trên app.
**Evidence:** `screenshots/TC-ORD-033__step5-BLOCKED-v11-khong-co-khung-gio-mac-dinh.png` — verified tồn tại
**Impact:** 🔴 **TC hết hiệu lực** (họ giống `006`/`014`) — ⛔ không log bug. Đề nghị QC chốt `DESCOPED`, và lưu ý nghiệp vụ **vẫn còn giá trị** ở dạng khác: `TC-ORD-059` (v1.1) đã phủ *"buổi đã trôi qua vẫn chọn được"* — đó mới là TC còn hiệu lực cho rule này.

---

## TC-ORD-051: Check lỗi validate hiện ngay dưới ô nhập khi rời ô — P3 · SC-ORD-048 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Vào bước 2 *(setup)* | — | ✅ PASS | — | — |
| 2 | Nhập 1 ký tự vào field tên người nhận rồi rời ô | `set_value "A"` vào `receiver-name-input` | ✅ PASS | — | — |
| 3 | Check vị trí thông báo lỗi | `textContains("Tên phải")` → **NOT FOUND**; không popup, cũng **không** dòng lỗi nào | ❌ **FAIL** | `TC-ORD-051__step3-FAIL-khong-co-loi-duoi-o-ten-nguoi-nhan.png` | Expected: lỗi hiện **ngay dưới ô**. Actual: **không có lỗi nào** |
| 4 | Để trống thêm SĐT người nhận và địa chỉ giao hàng | `set_value " "` | ✅ PASS | — | — |
| 5-6 | Cuộn xuống cuối form, nhấn "Tiếp theo" | scroll ×2 → tap | ✅ PASS | — | — |
| 7 | Check vị trí màn sau khi nhấn | màn **đứng nguyên ở cuối form** (vùng `BUỔI MONG MUỐN`), **không** cuộn lên ô lỗi đầu tiên (ô tên người nhận ở phía trên) | ❌ **FAIL** | `TC-ORD-051__step7-FAIL-man-khong-cuon-toi-o-loi-dau-tien.png` | Expected: màn cuộn tới ô lỗi đầu tiên |

**Result: ❌ FAIL at Step 3 và Step 7** *(0/2 expected)*
**Evidence:** `screenshots/TC-ORD-051__step3-FAIL-khong-co-loi-duoi-o-ten-nguoi-nhan.png` (+ `__step7-FAIL-...`) — verified tồn tại
**Impact:** 🐞 TC này là **bản mô tả đúng nhất của bug F3/F7 ở tầng UX**: app vừa **không báo lỗi tại ô**, vừa **không đưa người dùng tới chỗ sai**. Người dùng bấm nút, không có gì xảy ra, không biết phải sửa đâu. ⇒ nên dùng TC-051 làm **TC đại diện** khi log bug F3/F7.

---

## TC-ORD-047: Check tin đã ghép không còn nút Chỉnh sửa — P2 · SC-ORD-044 *(v1.1 MODIFIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng 1 tin NEED; tài khoản B nhận và xác nhận *(setup)* | ⚠️ **dùng dữ liệu CÓ SẴN trên STG** thay vì tự dựng — xem ghi chú dưới | ✅ PASS | — | đơn `Gửi: Tài liệu \| Giá trị thấp` đang ở trạng thái **Đã ghép** |
| 3 | Đăng nhập lại tài khoản A, tab "Hoạt động", mở tin đó *(setup)* | tap tab `Hoạt động` → tap `descriptionStartsWith("Gửi: Tài liệu")` → màn **Theo dõi đơn** | ✅ PASS | — | `track-sender-matched-status` = `Đã ghép · chờ shipper lấy hàng` ⇒ xác nhận đúng trạng thái |
| 4 | Check các nút hành động trên màn Theo dõi đơn | `appium_get_page_source` + find `accessibility id "Chỉnh sửa"` → **NOT FOUND** | ✅ PASS | `TC-ORD-047__verify-tin-da-ghep-khong-co-nut-chinh-sua.png` | các nút có mặt: `Báo cáo sự cố` (`track-report-incident`) · `Huỷ đơn` (`track-sender-matched-cancel`) · `Bản đồ`. **KHÔNG** có `Chỉnh sửa` ⇒ đúng Expected |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-047__verify-tin-da-ghep-khong-co-nut-chinh-sua.png` — verified tồn tại
**Locators captured:** **6 element MỚI** (màn Theo dõi đơn: `track-report-incident` · `track-sender-matched-status` · `track-sender-matched-cancel` · 2 icon `Copy` · `Bản đồ`)
> ⚠️ **Sai lệch tiền đề, khai rõ:** step 1-2 đòi tài khoản B nhận đơn — **không có phiên OTP của tài khoản B**. Thay vào đó dùng **đơn có sẵn trên STG đã ở trạng thái `Đã ghép`**. Điểm kiểm của TC (*đơn đã ghép thì không có nút Chỉnh sửa*) **không phụ thuộc vào việc ai tạo trạng thái đó** ⇒ verdict vẫn tin được. ⛔ Nhưng nếu QC muốn đúng 100% chữ thì cần cấp tài khoản B.

---

## TC-ORD-085: Check icon copy cạnh địa chỉ giao ở chi tiết tin sao chép đúng nội dung — P3 · SC-ORD-064 *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Mở 1 tin NEED ở màn chi tiết *(setup)* | dùng đơn có sẵn (như `TC-ORD-047`) | ✅ PASS | — | — |
| 3 | Ghi lại địa chỉ giao đang hiển thị | khối `LỘ TRÌNH` → `Giao hàng` = **`FPT Cầu Giấy`** | ✅ PASS | — | — |
| 4 | Nhấn icon copy cạnh địa chỉ giao | đặt **sentinel** `SENTINEL-TRUOC-KHI-COPY` vào clipboard trước → tap `description("Copy").instance(1)` | ✅ PASS | — | — |
| 5a | Check nội dung đã copy | `appium_mobile_clipboard(get)` = **`FPT Cầu Giấy`** — sentinel đã bị thay ⇒ copy **thật sự chạy** và **đúng nguyên văn** | ✅ PASS | `TC-ORD-085__verify-copy-dia-chi-giao.png` | — |
| 5b | Check trạng thái icon copy lúc vừa nhấn | tap lại + chụp **2 ảnh liên tiếp** trong cửa sổ 2 giây → lấy mẫu pixel vùng icon: **`(160,164,175)` xám ở cả 2 ảnh**, không có sắc xanh | ❌ **FAIL** | *(cùng ảnh)* | Expected: icon **đổi sang màu xanh ~2 giây** rồi trở lại |

**Result: ❌ FAIL at Step 5** *(vế nội dung copy thì đúng; vế phản hồi thị giác sai)*
**Evidence:** `screenshots/TC-ORD-085__verify-copy-dia-chi-giao.png` — verified tồn tại
**Impact:** 🐞 Bug **nhỏ, UX**: copy hoạt động nhưng **không có phản hồi nào cho người dùng** — bấm xong không biết đã copy hay chưa. Cùng họ "hành động im lặng" với F3/F7 nhưng **mức thấp hơn nhiều**; nên log **riêng**, mức Minor.
> 🔬 **Cách đo, để retest lặp lại được:** ghi sentinel vào clipboard trước khi tap ⇒ phân biệt được *"copy chạy"* với *"clipboard vốn đã có sẵn nội dung đó"*. Vế màu đo bằng lấy mẫu pixel, không bằng mắt.
> ⚠️ **Sai lệch có chủ ý:** step 5 của TC đòi **dán vào ô tìm kiếm tab "Bảng tin"**; t đọc clipboard trực tiếp bằng MCP — cùng oracle, ít nhiễu hơn (ô tìm kiếm có thể tự trim/chuẩn hoá làm sai lệch phép so nguyên văn).

---

## TC-ORD-086: Check icon copy cạnh số điện thoại ở chi tiết tin sao chép đúng nội dung — P3 · SC-ORD-064 *(v1.1 NEW)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Mở 1 tin NEED ở màn chi tiết *(setup)* | dùng đơn có sẵn (`Đã ghép`) | ✅ PASS | — | — |
| 3 | Ghi lại **số điện thoại** đang hiển thị trên màn | `appium_get_page_source` toàn màn + cuộn: **KHÔNG có số điện thoại nào** trên màn chi tiết. Chỉ có 2 icon `Copy`, **cả hai đều cạnh địa chỉ** (`Lấy hàng` · `Giao hàng`) | 🚫 **BLOCKED** | `TC-ORD-086__step3-BLOCKED-khong-co-sdt-tren-man-chi-tiet.png` | không có đối tượng để kiểm |
| 4-5 | — | ⏭ SKIPPED | — | — | blocked ở step 3 |

**Result: 🚫 BLOCKED at Step 3**
**Reason:** Màn chi tiết của đơn ở trạng thái **`Đã ghép`** không hiển thị số điện thoại nào (của người nhận lẫn của shipper) ⇒ **không có icon copy cạnh SĐT** để kiểm. Không thể thử trên đơn `Chờ ghép` mới vì **bug `TC-ORD-004` chặn tạo đơn**.
**Evidence:** `screenshots/TC-ORD-086__step3-BLOCKED-khong-co-sdt-tren-man-chi-tiet.png` — verified tồn tại
**Impact:** ⏳ **Chưa kết luận được là bug hay không** — cần 1 trong 2 điều kiện: (a) fix bug `TC-ORD-004` để tạo đơn `Chờ ghép` mới rồi mở chi tiết, hoặc (b) BA chốt xem màn chi tiết **có phải** hiển thị SĐT người nhận hay không.
> 🚩 **Quan sát ngoài phạm vi TC, đáng để BA xem:** banner cam kết của app ghi *"Sau khi ghép, SĐT hai bên sẽ được lộ để liên hệ ngoài app"* (`TC-ORD-001`), nhưng đơn này **đã ghép** mà màn chi tiết **không lộ SĐT nào**. Hai điều này **mâu thuẫn**. ⛔ Không đổi verdict TC-086 (ngoài Expected của nó), nhưng đề nghị mở clarification.

---

