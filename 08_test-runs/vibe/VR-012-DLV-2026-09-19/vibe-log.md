# Vibe Test Log — VR-012 — module DLV — 2026-09-19

> Module: **DLV — Giao nhận & Theo dõi đơn** · Platform: **mobile (Appium MCP / UiAutomator2)** · Env: STG, app `com.hrisproject.stag` (FoxPro host → FoxEco)
> Evidence dir: `screenshots/` · SCOPE_TOTAL = **81 TC** (30 CARRIED v1.0 + 51 v1.1)
> Phiên: **2026-09-19** (khởi tạo)
> Tập chạy: **pending 81/81** — sổ cái `coverage/coverage-DLV.md` mở lần đầu ở phiên này ⇒ 0 TC đã PASS ⇒ Step 1.2 không phải hỏi user.
> Tài khoản mở phiên: **Đặng Châu Anh** `stag_anhdc4@fpt.com` (MNV `00286248`)

---
## TC-DLV-001: Check người gửi ở trạng thái "Chờ ghép" thấy nhãn chờ vận chuyển bị khoá kèm nút Chỉnh sửa và Huỷ đơn

> Đơn dùng làm tiền đề: `Gửi: Tài liệu | Giá trị thấp` · `FPT Tân Thuận 1 → Tòa V-City, Lê Thái Tổ` · badge **Chờ ghép** — tin NEED do chính `stag_anhdc4@` (tài khoản A của TC) đăng ở VR-010 (`SEED R…`).
> ⇒ **Step 1 (setup "đăng 1 tin NEED") KHÔNG chạy lại** vì pre-condition *"A là người gửi của 1 đơn Chờ ghép"* đã thoả bằng dữ liệu seed sẵn có. Điều này ⛔ không làm giảm giá trị của step 2–4, là phần thực sự được TC kiểm.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) A có 1 đơn NEED ở `Chờ ghép` | dùng đơn seed VR-010 của chính `stag_anhdc4@` | ✅ PASS | — | không đăng tin mới |
| 2 | Tab "Hoạt động" → tap card đơn | `find(descriptionStartsWith("Gửi: Tài liệu \| Giá trị thấp, Chờ ghép, Từ: FPT Tân Thuận 1"))` → `tap` → màn **Theo dõi đơn** | ✅ PASS | — | — |
| 3 | Check nhãn hành động chính + trạng thái | page source: nhãn `Đang chờ người vận chuyển nhận đơn` — băng chứa nhãn `[32,1008][688,1094]` có **`clickable=false`, KHÔNG resource-id, KHÔNG content-desc** | ✅ PASS | `TC-DLV-001__verify-nhan-cho-van-chuyen-khoa.png` | nhãn xám, ⛔ không phải nút |
| 4 | Check các nút phụ | 2 `ViewGroup` **`clickable=true`**: `track-edit-post` (desc `Chỉnh sửa`) và `track-cancel-post` (desc `Huỷ đơn`) | ✅ PASS | *(cùng ảnh)* | — |
| E3 | Nhãn "Đang chờ người vận chuyển nhận đơn" **disable** | ✅ đúng nguyên văn · ⛔ không nhấn được | ✅ PASS | — | 🔑 **Oracle "khoá" dùng được cho cả nhóm 001–015:** nhãn khoá = `clickable=false` + không rid; nút thật = `ViewGroup clickable=true` + có rid. ⛔ KHÔNG dùng attribute `enabled` (bẫy **T4** — luôn `true`) |
| E4 | Có nút "Chỉnh sửa" và "Huỷ đơn" | ✅ có đủ 2 | ✅ PASS | — | ⛔ không tap `Huỷ đơn` (sẽ huỷ đơn thật) |

**Result: ✅ PASS (4 steps, 2 expected)**
**Evidence:** `screenshots/TC-DLV-001__verify-nhan-cho-van-chuyen-khoa.png` — verified tồn tại (85 KB)
**Locators captured:** 4 elements (nhãn khoá · `track-edit-post` · `track-cancel-post` · stepper 5 mốc)

---
## TC-DLV-010: Check người gửi ở trạng thái "Đã giao" thấy nhãn chờ người nhận xác nhận bị khoá

> Đơn dùng làm tiền đề: `Gửi: Quần áo | Giá trị thấp` · `35 La Thành, Sơn Tây → 122 Tây Sơn, Đan Phượng` · badge **Đã giao**, tài khoản đang đăng nhập (`stag_anhdc4@`) là **người gửi**.
> ⇒ Step 1 *(nhờ dev/QA seed đơn "Đã giao")* **không cần** — STG đã sẵn đơn đúng trạng thái + đúng vai.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) có đơn `Đã giao`, A = người gửi | dùng đơn sẵn có trên STG | ✅ PASS | — | ⛔ không nhờ dev seed |
| 2 | Tab "Hoạt động" → mở đơn | `find(descriptionStartsWith("Gửi: Quần áo \| Giá trị thấp, Đã giao"))` → `tap` | ✅ PASS | — | vào **Theo dõi đơn** |
| 3 | Check nhãn hành động chính + trạng thái | nhãn `Đã giao · chờ người nhận xác nhận`; băng chứa nhãn `[32,1114][688,1200]` **`clickable=false`, không rid, không desc** | ✅ PASS | `TC-DLV-010__verify-nhan-cho-nguoi-nhan-xac-nhan.png` | — |
| E3 | Nhãn "✓ Đã giao · chờ người nhận xác nhận" **disable** | ✅ khớp nguyên văn (dấu `✓` của TC render bằng **icon đồng hồ**, không phải ký tự trong `text`) · ⛔ không nhấn được | ✅ PASS | — | Stepper sáng 4/5 mốc, `Hoàn thành` còn xám ⇒ đúng trạng thái. Người gửi ở `Đã giao` **không còn nút hành động nào** |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-DLV-010__verify-nhan-cho-nguoi-nhan-xac-nhan.png` — verified tồn tại (247 KB)
**Locators captured:** 2 elements (nhãn khoá `Đã giao · chờ người nhận xác nhận` · `track-report-incident`)

---
## TC-DLV-008: Check người vận chuyển ở trạng thái "Đang giao" thấy nút "Đã giao cho người nhận" bật

> Đơn dùng làm tiền đề: `Giao: Thuốc/Y tế | Giá trị thấp` · `336-340 Huỳnh Tấn Phát, Q7 → 04, 05 Nguyễn Duy Hiệu` · badge **Đang giao**. Tài khoản đăng nhập (`stag_anhdc4@`) là **người vận chuyển** (tiền tố card `Giao:` — oracle phân vai của VR-008). Người gửi `Tuan VM37`, người nhận `Châu Ngọc Việt` ⇒ đủ 3 vai A/B/C như TC yêu cầu.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) đơn `Đang giao` đủ 3 vai | dùng đơn sẵn có trên STG | ✅ PASS | — | ⛔ không nhờ dev seed |
| 2 | Đăng nhập B, mở Theo dõi đơn | `scroll_to_element(descriptionContains("Giao: Thuốc/Y tế"))` → `find(descriptionStartsWith("… Đang giao"))` → `tap` | ✅ PASS | — | ⚠️ cần `scrollDistancePreset=small` + 27 nhịp (bẫy **T18**) |
| 3 | Check nút hành động chính + trạng thái | `ViewGroup` desc `Đã giao cho người nhận`, **`clickable=true`**, `[32,1114][688,1200]`, nền **cam đặc** | ✅ PASS | `TC-DLV-008__verify-nut-da-giao-cho-nguoi-nhan-bat.png` | ⛔ **KHÔNG tap** — sẽ đẩy đơn thật sang `Đã giao` |
| E3 | Nút "Đã giao cho người nhận" **enable** | ✅ có, enable | ✅ PASS | — | Stepper sáng 3/5 (`Chờ ghép`→`Lấy hàng`→`Đang giao`), `Đã giao`/`Hoàn thành` xám ⇒ đúng trạng thái |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-DLV-008__verify-nut-da-giao-cho-nguoi-nhan-bat.png` — verified tồn tại (88 KB)
**Locators captured:** 1 element mới (`desc="Đã giao cho người nhận"`)

---

## TC-DLV-027: Check người vận chuyển thấy cả cụm liên hệ người gửi và người nhận

> 🔶 **KHAI SAI LỆCH SO VỚI STEPS (đọc trước khi dùng kết quả):** TC dựng tiền đề bằng đơn ở trạng thái **`Đã ghép`**.
> Tài khoản `stag_anhdc4@` hiện **KHÔNG có đơn nào ở `Đã ghép`** (quét toàn bộ tab *Đang diễn ra*, 5 vị trí cuộn),
> nên TC được chạy trên đơn **`Đang giao`** (cùng đơn của `TC-DLV-008`) — vai **người vận chuyển** giữ nguyên.
> ⇒ Kết quả này chứng minh *"carrier thấy đủ 2 cụm liên hệ"*, **chưa** chứng minh riêng cho mốc `Đã ghép`.
> Mốc `Đã ghép` sẽ được phủ khi phiên sau dựng được đơn ở trạng thái đó (xem §Khuyến nghị của `vibe-report.md`).

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1–2 | (setup) A đăng tin khai C là người nhận; B nhận đơn | dùng đơn sẵn có: A=`Tuan VM37`, B=`stag_anhdc4@`, C=`Châu Ngọc Việt` | ✅ PASS | — | ⚠️ đơn đã đi tiếp tới `Đang giao` (xem khai sai lệch ở trên) |
| 3 | Mở Theo dõi đơn, check các cụm liên hệ | `scroll_to_element(textContains("THÔNG TIN HÀNG"))` rồi cuộn ngược về `textContains("NGƯỜI GỬI")` | ✅ PASS | `TC-DLV-027__verify-cum-nguoi-gui-va-nguoi-nhan.png` | 2 cụm nằm liền nhau, lọt cùng 1 khung hình |
| E3 | Có cả cụm "NGƯỜI GỬI" và "NGƯỜI NHẬN", mỗi cụm có tên + SĐT + nút "Gọi" | **NGƯỜI GỬI**: `Tuan VM37` · `0900000037` · `stag_tuanvm37@fpt.com` · nút `Gọi` (desc `Gọi người gửi`, `clickable=true`)<br>**NGƯỜI NHẬN**: `Châu Ngọc Việt` · `0963852741` · nút `Gọi` (desc `Gọi người nhận`, `clickable=true`) | ✅ PASS | — | 🔑 Cụm **NGƯỜI GỬI có thêm email** mà cụm NGƯỜI NHẬN **không có** — TC không nói tới, ⛔ không tính là lệch. 🔑 2 nút `Gọi` phân biệt bằng **`content-desc`** (`Gọi người gửi` / `Gọi người nhận`), ⛔ không phải bằng `text` (cả hai đều `Gọi`) |

**Result: ✅ PASS (3 steps, 1 expected) — kèm khai sai lệch trạng thái ở trên**
**Evidence:** `screenshots/TC-DLV-027__verify-cum-nguoi-gui-va-nguoi-nhan.png` — verified tồn tại
**Locators captured:** 4 elements (`Gọi người gửi` · `Gọi người nhận` · 2 nhãn cụm)

---
## TC-DLV-009: Check người nhận ở trạng thái "Đang giao" thấy nhãn đơn đang trên đường bị khoá

> Đơn dùng làm tiền đề: `Nhận: Đồ điện tử | Giá trị vừa` · `35 La Thành, Sơn Tây → Tân Tây Đô, Đan Phượng` · badge **Đang giao**. Tài khoản đăng nhập là **người nhận** (tiền tố card `Nhận:`).

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) đơn `Đang giao` đủ 3 vai | dùng đơn sẵn có trên STG | ✅ PASS | — | ⛔ không nhờ dev seed |
| 2 | Đăng nhập C, tab "Hoạt động" → mở đơn | `scroll_to_element(descriptionContains("Nhận: Đồ điện tử"))` (29 nhịp, preset `small`) → `tap` | ✅ PASS | — | — |
| 3 | Check nhãn hành động chính + trạng thái | nhãn `Đơn đang trên đường đến bạn`, **không nằm trong tập node `clickable=true`** của màn ⇒ nhãn khoá | ✅ PASS | `TC-DLV-009__verify-nhan-don-dang-tren-duong.png` | dấu `✓` render thành **icon tick**, đúng như TC mô tả |
| E3 | Nhãn "✓ Đơn đang trên đường đến bạn" **disable** | ✅ khớp | ✅ PASS | — | Stepper sáng 3/5 ⇒ đúng trạng thái `Đang giao` |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-DLV-009__verify-nhan-don-dang-tren-duong.png` — verified tồn tại
**Locators captured:** 1 element mới (nhãn khoá `Đơn đang trên đường đến bạn`)

> 🔎 **Quan sát ngoài phạm vi TC (ghi lại để BA/QC quyết, ⛔ không tự chấm FAIL):** ở màn này người nhận
> **KHÔNG thấy cụm `NGƯỜI GIAO HÀNG`, không thấy `ẢNH SẢN PHẨM`, không thấy `THÔNG TIN HÀNG`** — toàn màn chỉ
> có stepper + `LỘ TRÌNH` + bản đồ + nhãn khoá. Đã loại trừ khả năng "nội dung bị ẩn dưới nếp gấp" bằng **4 phép
> cuộn khác nhau** (`scroll_to_element` preset `small`, `swipe slow`, scroll toạ độ ở mép phải ngoài bản đồ,
> scroll toạ độ trong vùng danh sách) — cả 4 đều không làm màn nhúc nhích, và `ẢNH SẢN PHẨM`/`NGƯỜI GIAO` **không
> tồn tại trong page source**. 🔴 Điều này **ngược** với `repro/RP-ASN-lo-sdt-sau-ghep-2026-09-19`, nơi người nhận ở
> trạng thái **`Đã ghép`** thấy đủ cụm `NGƯỜI GIAO HÀNG` + SĐT + nút `Gọi`. ⇒ Giả thuyết: cụm liên hệ **biến mất
> khỏi màn người nhận khi đơn sang `Đang giao`**. Chưa có SC nào phủ ⇒ route `/analyze-requirements --update`.
> 🪤 **Bẫy mới `T-DLV-01`:** widget **Google Map nuốt gesture** — `swipe` lên trên màn này chỉ pan bản đồ, không cuộn trang.

---
## TC-DLV-012: Check người nhận ở trạng thái "Đã giao" thấy nút "Xác nhận đã nhận hàng" bật  *(P1)*

> Đơn dùng làm tiền đề: `Nhận: Quần áo | Giá trị thấp` · `ITD Bld, Tân Thuận, Q7 → L29B-31B-33B KCX Tân Thuận` · badge **Đã giao**. Tài khoản đăng nhập là **người nhận**; người vận chuyển là `Phan Minh Tài` (`0833329408`).

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) đơn `Đã giao` đủ 3 vai | dùng đơn sẵn có trên STG | ✅ PASS | — | ⛔ không nhờ dev seed |
| 2 | Đăng nhập C, tab "Hoạt động" → mở đơn | `scroll_to_element(descriptionStartsWith("Nhận: Quần áo \| Giá trị thấp, Đã giao"))` (43 nhịp) → `tap` | ✅ PASS | — | — |
| 3 | Check nút hành động chính + trạng thái | `ViewGroup` desc `Xác nhận đã nhận hàng`, **`clickable=true`**, `[32,1114][688,1200]`, nền **cam đặc** | ✅ PASS | `TC-DLV-012__verify-nut-xac-nhan-da-nhan-hang-bat.png` | ⛔ **KHÔNG tap** ở lô này — sẽ đẩy đơn sang `Hoàn thành` và làm mất tiền đề `Đã giao` của `TC-DLV-010/011/028` |
| E3 | Nút "Xác nhận đã nhận hàng" **enable** | ✅ có, enable | ✅ PASS | — | Stepper sáng 4/5 ⇒ đúng trạng thái `Đã giao`. 🔑 Đây là **nút duy nhất** trên màn — khớp `TC-DLV-022` (chỉ người nhận chốt được đơn) |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-DLV-012__verify-nut-xac-nhan-da-nhan-hang-bat.png` — verified tồn tại
**Locators captured:** 1 element mới (`desc="Xác nhận đã nhận hàng"`)

---

## TC-DLV-028: Check người nhận chỉ thấy cụm liên hệ người giao hàng và không thấy thông tin người gửi

> 🔶 **KHAI SAI LỆCH SO VỚI STEPS:** TC dựng tiền đề ở trạng thái **`Đã ghép`**; tài khoản `stag_anhdc4@` không có đơn
> `Đã ghép` nào nên TC chạy trên đơn **`Đã giao`** (cùng đơn của `TC-DLV-012`), vai **người nhận** giữ nguyên.
> 🔴 Đây là **lựa chọn có chủ ý, không phải tiện tay**: bản chạy ở `Đang giao` (đơn của `TC-DLV-009`) sẽ cho **FAIL oan**
> vì ở trạng thái đó app **không render cụm liên hệ nào**. Xem quan sát ở `TC-DLV-009`.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1–2 | (setup) A đăng tin khai C là người nhận; B nhận đơn | dùng đơn sẵn có: B = `Phan Minh Tài`, C = `stag_anhdc4@` | ✅ PASS | — | — |
| 3 | Đăng nhập C, tab "Hoạt động" → mở đơn | `tap` card | ✅ PASS | — | — |
| 4 | Check các cụm liên hệ trên màn | quét **toàn bộ** màn qua 3 vị trí cuộn: `NGƯỜI GIAO HÀNG` = `Phan Minh Tài` · `0833329408` · nút `Gọi` (desc `Gọi người giao hàng`, `clickable=true`) | ✅ PASS | `TC-DLV-028__verify-chi-cum-nguoi-giao-hang.png` | — |
| E4 | Chỉ có cụm "NGƯỜI GIAO HÀNG" (tên + SĐT + nút "Gọi"); **KHÔNG** có cụm/SĐT người gửi | ✅ đúng cả vế dương lẫn **vế âm**: chuỗi `NGƯỜI GỬI` · `NGƯỜI NHẬN` · `Gọi người gửi` đều **KHÔNG tồn tại** trong page source ở mọi vị trí cuộn; sau cụm `NGƯỜI GIAO HÀNG` là `THÔNG TIN HÀNG` rồi `LỊCH SỬ` — ⛔ không chen cụm nào | ✅ PASS | — | 🔑 Vế âm được chứng minh bằng **quét chuỗi trên page source đã cuộn hết màn**, ⛔ không phải bằng "nhìn ảnh không thấy" |

**Result: ✅ PASS (4 steps, 1 expected) — kèm khai sai lệch trạng thái ở trên**
**Evidence:** `screenshots/TC-DLV-028__verify-chi-cum-nguoi-giao-hang.png` — verified tồn tại
**Locators captured:** 2 elements (`Gọi người giao hàng` · nhãn cụm `NGƯỜI GIAO HÀNG`)

---
## TC-DLV-011: Check người vận chuyển ở trạng thái "Đã giao" thấy nhãn chờ người nhận xác nhận bị khoá

> Đơn dùng làm tiền đề: `Giao: Đồ dễ vỡ | Giá trị vừa` · `Lô 37-39A KCX Tân Thuận → L29B-31B-33B KCX Tân Thuận` · badge **Đã giao**. Đủ 3 vai: A = `Đặng Châu Giang` (`0900131946`), B = `stag_anhdc4@` (đang đăng nhập), C = `Phan Minh Tài` (`0964633320`).

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) đơn `Đã giao` đủ 3 vai | dùng đơn sẵn có trên STG | ✅ PASS | — | ⛔ không nhờ dev seed |
| 2 | Đăng nhập B, mở Theo dõi đơn | `scroll_to_element(descriptionStartsWith("Giao: Đồ dễ vỡ \| Giá trị vừa, Đã giao"))` (31 nhịp) → `tap` | ✅ PASS | — | — |
| 3 | Check nhãn hành động chính + trạng thái | nhãn `Đã giao · chờ người nhận xác nhận` ở thanh dưới, **không có node `clickable=true` nào** ở băng đó | ✅ PASS | `TC-DLV-011__verify-carrier-nhan-cho-nguoi-nhan-xac-nhan.png` | — |
| 4 | Check toàn màn tìm nút chốt hoàn tất đơn | cuộn hết màn (tới `LỊCH SỬ`) rồi quét chuỗi page source: `Xác nhận` · `Hoàn tất` · `Chốt đơn` · `Đã nhận hàng` — **cả 4 đều KHÔNG tồn tại** | ✅ PASS | *(cùng ảnh)* | — |
| E3 | Nhãn "✓ Đã giao · chờ người nhận xác nhận" **disable** | ✅ khớp nguyên văn | ✅ PASS | — | — |
| E4 | **KHÔNG** có nút nào cho người vận chuyển chốt hoàn tất đơn | ✅ đúng — toàn màn chỉ có `Quay lại` · `Báo cáo sự cố` · `Copy` ×2 · `Gọi người gửi` · `Gọi người nhận` | ✅ PASS | — | 🔑 **Đối chứng chéo mạnh với `TC-DLV-012`:** cùng trạng thái `Đã giao`, chỉ **người nhận** có nút `Xác nhận đã nhận hàng`; người gửi (`TC-DLV-010`) và người vận chuyển (TC này) **đều không có nút nào** ⇒ 3 vai đã được đo, là chứng cứ trực tiếp cho `TC-DLV-022` |

**Result: ✅ PASS (4 steps, 2 expected)**
**Evidence:** `screenshots/TC-DLV-011__verify-carrier-nhan-cho-nguoi-nhan-xac-nhan.png` — verified tồn tại
**Locators captured:** 0 element mới (toàn bộ lấy từ `locator_map` đã dựng)

---
## TC-DLV-015: Check người nhận ở trạng thái "Hoàn thành" thấy nhãn đơn đã hoàn thành bị khoá

> Đơn dùng làm tiền đề: tab **Đã hoàn thành** → card `Gửi khác, ITD Bld, Tân Thuận, Q7 → L29B-31B-33B KCX Tân Thuận · 9/8/2026, Hoàn thành`.
> Vai đọc từ **block LỊCH SỬ** của chính đơn: A (đăng tin) = `Phan Minh Tài` · B (ghép + giao) = `Đặng Châu Giang` · C (hoàn thành đơn) = `Đặng Châu Anh` = **tài khoản đang đăng nhập** ⇒ đúng vai **người nhận**.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) đơn `Hoàn thành` đủ 3 vai | dùng đơn sẵn có trên STG | ✅ PASS | — | ⛔ không nhờ dev seed |
| 2 | Tab "Hoạt động" → tab con "Đã hoàn thành" → mở đơn | `tap(accessibility id "Đã hoàn thành")` → `tap(descriptionStartsWith("Gửi khác"))` | ✅ PASS | — | ⚠️ card ở tab này **KHÔNG mang tiền tố vai** (`Gửi:`/`Giao:`/`Nhận:`) như tab *Đang diễn ra* ⇒ phải mở đơn mới biết vai |
| 3 | Check nhãn hành động chính + trạng thái | nhãn `Đơn đã hoàn thành ✓` ở thanh dưới, **không có node `clickable=true`** ở băng đó | ✅ PASS | `TC-DLV-015__verify-nhan-don-da-hoan-thanh.png` | — |
| E3 | Nhãn "Đơn đã hoàn thành ✓" **disable** | ✅ khớp nguyên văn, **kể cả dấu `✓` ở cuối là ký tự thật trong `text`** | ✅ PASS | — | Stepper sáng **đủ 5/5** mốc ⇒ đúng trạng thái `Hoàn thành` |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-DLV-015__verify-nhan-don-da-hoan-thanh.png` — verified tồn tại
**Locators captured:** 1 element mới (nhãn khoá `Đơn đã hoàn thành ✓`)

---

## TC-DLV-029: Check block Lịch sử có đủ năm mốc sự kiện kèm timestamp trên đơn đi thẳng tới hoàn thành

> 🔶 **KHAI SAI LỆCH SO VỚI STEPS:** step 2 yêu cầu xem bằng **tài khoản A (người gửi)**; phiên này xem bằng **tài khoản C (người nhận)** trên cùng đơn của `TC-DLV-015`. Block `LỊCH SỬ` là **nội dung của đơn**, không phải nội dung theo vai — nhưng điều đó **chưa được đo cho vai A**, nên vẫn khai ra đây.
> ✅ Điều kiện *"đi thẳng tới Hoàn thành, không qua huỷ nhận"* **đã kiểm**: timeline không có mốc huỷ/huỷ nhận nào.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) đơn đi thẳng tới `Hoàn thành`, đủ 3 vai | dùng đơn sẵn có | ✅ PASS | — | ⛔ không nhờ dev seed |
| 2 | Mở đơn ở tab "Đã hoàn thành" | như `TC-DLV-015` | ✅ PASS | — | — |
| 3 | Mở block "Lịch sử", check các mốc + timestamp | `scroll_to_element(textContains("LỊCH SỬ"))` rồi cuộn thêm 1 nhịp | ✅ PASS | `TC-DLV-029__verify-lich-su-du-5-moc.png` | block **không cần bấm để mở** — luôn bung sẵn |
| E3 | Timeline đủ 5 mốc "Đăng tin" → "Ghép thành công" → "Lấy hàng" → "Đã giao" → "Hoàn thành", mỗi mốc kèm timestamp | ✅ đủ **5/5**, mỗi mốc có timestamp **+ tên người thực hiện**:<br>· `Đăng tin lên bảng tin` — `9/8/2026 · 08:13 · Phan Minh Tài`<br>· `Ghép thành công (tuyến đường)` — `9/8/2026 · 08:19 · Đặng Châu Giang`<br>· `Người mang đã lấy hàng` — `9/8/2026 · 08:20 · ITD Bld, Tân Thuận, Q7`<br>· `Đã giao tận tay người nhận` — `9/8/2026 · 08:42 · Đặng Châu Giang`<br>· `Hoàn thành đơn` — `9/8/2026 · 21:03 · Đặng Châu Anh` | ✅ PASS | — | xem 2 ghi chú bên dưới |

**Result: ✅ PASS (3 steps, 1 expected) — kèm khai sai lệch vai ở trên**
**Evidence:** `screenshots/TC-DLV-029__verify-lich-su-du-5-moc.png` — verified tồn tại
**Locators captured:** 5 elements (5 nhãn mốc lịch sử)

> ⚠️ **2 điểm lệch nhỏ với câu chữ của TC — ⛔ KHÔNG tự sửa Expected, chuyển BA quyết:**
> 1. **Thứ tự hiển thị là MỚI→CŨ** (`Hoàn thành đơn` nằm trên cùng, `Đăng tin` dưới cùng), tức **ngược** với thứ tự
>    TC liệt kê. Chuỗi sự kiện và timestamp thì **đúng tuyệt đối**. Chấm PASS vì yêu cầu thực chất *(đủ 5 mốc + có
>    timestamp + đúng trình tự thời gian)* đã thoả; nhưng nếu BA muốn **cũ→mới** thì đây là lệch cần sửa app.
> 2. **Có mốc thứ 6 ngoài danh sách của TC:** `Đã tặng quà cảm ơn — Hôm nay · 20:33 · Phan Minh Tài` (do `VR-011`
>    tạo). TC chỉ nói *"có đủ 5 mốc"*, ⛔ không nói *"chỉ có 5 mốc"* ⇒ không tính là lệch.
>
> 🎁 **Thu hoạch kèm cho các TC sau (chưa chấm, chỉ ghi lại):** 2 mốc `Người mang đã lấy hàng` và `Đã giao tận tay
> người nhận` **có ảnh đính kèm hiển thị ngay trong timeline** ⇒ tiền đề dương sẵn có cho `TC-DLV-041` (ảnh lúc lấy
> hàng lưu kèm mốc) và mẫu câu `Đã giao tận tay người nhận` cho `TC-DLV-068`.

---
## TC-DLV-014: Check người vận chuyển ở trạng thái "Hoàn thành" thấy nhãn đơn đã hoàn thành bị khoá

> Đơn dùng làm tiền đề: tab **Đã hoàn thành** → `Gửi tài liệu, ITD Bld, Tân Thuận, Q7 → L29B-31B-33B KCX Tân Thuận · 9/8/2026`.
> **Cách xác định vai (dùng lại được):** màn hiện cụm **`NGƯỜI GỬI`** (`Đặng Châu Giang`) ⇒ tài khoản đang đăng nhập **không thể** là người gửi; người nhận thì chỉ thấy `NGƯỜI GIAO HÀNG` (đo ở `TC-DLV-028`) ⇒ vai còn lại là **người vận chuyển**.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) đơn `Hoàn thành` đủ 3 vai | dùng đơn sẵn có trên STG | ✅ PASS | — | ⛔ không nhờ dev seed |
| 2 | Đăng nhập B, tab "Hoạt động" → "Đã hoàn thành" → mở đơn | `scroll_to_element(descriptionStartsWith("Gửi tài liệu, ITD Bld"))` → `tap` | ✅ PASS | — | — |
| 3 | Check nhãn hành động chính + trạng thái | nhãn `Đơn đã hoàn thành ✓`; băng nhãn **không có node `clickable=true`** | ✅ PASS | `TC-DLV-014__verify-carrier-nhan-don-da-hoan-thanh.png` | — |
| E3 | Nhãn "✓ Đơn đã hoàn thành ✓" **disable** | ✅ khớp | ✅ PASS | — | Stepper sáng đủ **5/5**. Người vận chuyển ở `Hoàn thành` **không còn nút hành động nào** |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-DLV-014__verify-carrier-nhan-don-da-hoan-thanh.png` — verified tồn tại
**Locators captured:** 0 element mới

---
## TC-DLV-081: Check icon copy cạnh địa chỉ giao sao chép đúng nội dung và đổi màu xanh  ❌

> Màn: **Theo dõi đơn** của đơn `Giao: Thuốc/Y tế | Giá trị thấp` (`Đang giao`), vai người vận chuyển.
> Địa chỉ giao ghi nhận ở step 4: **`04, 05 Nguyễn Duy Hiệu`**.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1–3 | Mở màn Theo dõi đơn có khối `LỘ TRÌNH` | `tap` card → `scroll_to_element(textContains("LỘ TRÌNH"))` | ✅ PASS | — | — |
| 4 | Ghi lại địa chỉ giao | đọc `text` sau nhãn `Giao hàng` → `04, 05 Nguyễn Duy Hiệu` | ✅ PASS | — | — |
| 4b | **Đặt sentinel vào clipboard trước khi tap** | `appium_mobile_clipboard(set, "SENTINEL-VR012-DLV-081")` | ✅ PASS | — | 🔑 bắt buộc — nếu không, clipboard cũ có thể trùng và cho PASS oan |
| 5 | Nhấn icon copy cạnh địa chỉ giao | `find(description("Copy").instance(1))` → `tap` | ✅ PASS | `TC-DLV-081__verify-copy-dia-chi-giao.png` | `instance(0)` = cạnh `Lấy hàng` · `instance(1)` = cạnh `Giao hàng` |
| 6a | Dán ra kiểm nội dung | `appium_mobile_clipboard(get)` → **`04, 05 Nguyễn Duy Hiệu`** | ✅ PASS | — | sentinel đã bị ghi đè ⇒ copy thật sự xảy ra |
| 6b | Check icon đổi màu xanh ~2s rồi trở lại | lấy mẫu pixel vùng icon `[620..656]×[418..450]` ở **t≈0s** và **t≈3s**: cả hai đều `(160,164,175)` **xám**, pixel bão hoà nhất không đổi | ❌ **FAIL** | `TC-DLV-081__step6-FAIL-icon-khong-doi-mau.png` | ⛔ **không có** phản hồi thị giác nào |
| E6 | Nội dung dán đúng nguyên văn **VÀ** icon đổi màu xanh ~2s | **nửa đầu ĐÚNG, nửa sau SAI** ⇒ expected không thoả trọn vẹn | ❌ **FAIL** | — | — |

**Result: ❌ FAIL tại step 6b (vế "đổi màu xanh")**
**Expected:** icon copy đổi sang **màu xanh khoảng 2 giây** rồi trở lại bình thường
**Actual:** icon giữ nguyên màu xám `(160,164,175)` ở cả t≈0s và t≈3s — ⛔ không có bất kỳ phản hồi thị giác nào
**Evidence:** `screenshots/TC-DLV-081__verify-copy-dia-chi-giao.png` · `screenshots/TC-DLV-081__step6-FAIL-icon-khong-doi-mau.png` — verified tồn tại
**Impact:** người dùng không biết đã copy thành công hay chưa ⇒ dễ bấm nhiều lần.
⚠️ **Hạn chế của phép đo (khai để người sau không tin quá mức):** `adb screencap` mất ~0.5–1s nên **về lý thuyết** một ánh xanh cực ngắn (<0.5s) có thể lọt khe. Nhưng expected nói **~2 giây** — thừa sức bắt được ở cả 2 mốc đo — và `VR-004 / TC-ORD-085` đo độc lập cũng ra **đúng cùng giá trị xám `(160,164,175)`**. ⇒ 2 lần đo độc lập, 2 run khác nhau, cùng kết luận.

---

## TC-DLV-080: Check icon copy cạnh số điện thoại sao chép đúng nội dung và đổi màu xanh  ❌

> Cùng màn với `TC-DLV-081`. SĐT ghi nhận ở step 4: **`0900000037`** (người gửi `Tuan VM37`).

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1–3 | Mở màn Theo dõi đơn có cụm `NGƯỜI GỬI` | đã ở sẵn màn | ✅ PASS | — | — |
| 4 | Ghi lại số điện thoại | đọc `text` trong cụm `NGƯỜI GỬI` → `0900000037` | ✅ PASS | — | — |
| 4b | Đặt sentinel vào clipboard | `appium_mobile_clipboard(set, "SENTINEL-VR012-DLV-080")` | ✅ PASS | — | — |
| 5 | Nhấn icon copy cạnh SĐT | `find(description("Copy").instance(2))` → `tap` | ✅ PASS | `TC-DLV-080__verify-copy-so-dien-thoai.png` | `instance(2)` = icon copy **trong cụm liên hệ**, khác 2 icon của `LỘ TRÌNH` |
| 6a | Dán ra kiểm nội dung | `appium_mobile_clipboard(get)` → **`0900000037`** | ✅ PASS | — | đúng nguyên văn, sentinel đã bị ghi đè |
| 6b | Check icon đổi màu xanh ~2s | lấy mẫu pixel vùng icon `[470..504]×[833..869]` ở **t≈0s** và **t≈2s**: cả hai `(160,164,175)` **xám** | ❌ **FAIL** | `TC-DLV-080__step6-FAIL-icon-khong-doi-mau.png` | — |
| E6 | Nội dung đúng **VÀ** icon đổi màu xanh ~2s | nửa đầu ĐÚNG, nửa sau SAI | ❌ **FAIL** | — | — |

**Result: ❌ FAIL tại step 6b (vế "đổi màu xanh")**
**Expected:** icon copy đổi sang màu xanh khoảng 2 giây rồi trở lại bình thường
**Actual:** giữ nguyên xám `(160,164,175)` ở cả 2 mốc đo
**Evidence:** `screenshots/TC-DLV-080__verify-copy-so-dien-thoai.png` · `screenshots/TC-DLV-080__step6-FAIL-icon-khong-doi-mau.png` — verified tồn tại
**Impact:** 🐛 **`TC-DLV-080` + `TC-DLV-081` + `TC-ORD-085` (VR-004) là CÙNG MỘT LỖI GỐC** — component icon copy dùng chung **không** có state phản hồi. ⇒ nên mở **1 bug** cho component, ⛔ không mở 3 bug riêng. Chức năng copy **vẫn đúng**, chỉ thiếu phản hồi thị giác ⇒ severity thấp.

---
## TC-DLV-068: Check nhật ký ghi đúng nguyên văn mẫu câu giao tận tay người nhận

> 🔶 **KHAI SAI LỆCH SO VỚI STEPS:** các step setup (B mở màn "Xác nhận đã giao" → chọn `Người nhận` → đính ảnh → xác nhận) **KHÔNG chạy lại** ở phiên này vì mọi thao tác đẩy trạng thái đơn đều **bị chặn** (xem §BLOCKER cuối log). Thay vào đó TC được kiểm trên **đơn đã có sẵn mốc đó trên STG** — đơn `Gửi khác, ITD Bld, Tân Thuận, Q7 → L29B-31B-33B KCX Tân Thuận · 9/8/2026`, `Hoàn thành`.
> ⇒ Vế được kiểm là **nội dung dòng nhật ký** — đúng phần mà expected của TC nói tới. Vế **"thao tác nào sinh ra dòng đó"** thì ⛔ **chưa kiểm ở phiên này**.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1–3 | (setup) đơn đã được giao **tận tay người nhận** | dùng đơn sẵn có trên STG | ✅ PASS | — | mốc `Đã giao tận tay người nhận` do `Đặng Châu Giang` (vai B) tạo |
| 4 | Mở block LỊCH SỬ, đọc dòng mốc giao hàng | `scroll_to_element(text("Đã giao tận tay người nhận"))` | ✅ PASS | `TC-DLV-068__verify-mau-cau-giao-tan-tay.png` | — |
| E4 | Dòng mốc ghi **đúng nguyên văn** "Đã giao tận tay người nhận", kèm **thời điểm** và **dấu hiệu có ảnh bằng chứng** | ✅ đủ **cả 3 vế**:<br>· nguyên văn: `Đã giao tận tay người nhận` — khớp **từng ký tự**<br>· thời điểm: `9/8/2026 · 08:42 · Đặng Châu Giang`<br>· dấu hiệu ảnh: **thumbnail ảnh bằng chứng render ngay dưới dòng mốc** | ✅ PASS | — | 🔑 "dấu hiệu có ảnh" ở app này là **ảnh thật hiển thị inline**, ⛔ không phải icon kẹp giấy |

**Result: ✅ PASS (4 steps, 1 expected) — kèm khai sai lệch setup ở trên**
**Evidence:** `screenshots/TC-DLV-068__verify-mau-cau-giao-tan-tay.png` — verified tồn tại
**Locators captured:** 1 element (`text("Đã giao tận tay người nhận")`)

---
## TC-DLV-026: Check người gửi thấy cụm liên hệ người vận chuyển sau khi ghép và không thấy trước khi ghép

> 🔶 **KHAI SAI LỆCH SO VỚI STEPS:** TC dùng **một đơn** rồi so trước/sau khi ghép. Phiên này **không đẩy được trạng thái đơn** (thao tác ghép/đổi trạng thái bị chặn — xem §BLOCKER), nên 2 vế được đo trên **2 đơn khác nhau, cùng vai người gửi, cùng tài khoản `stag_anhdc4@`**:
> · **vế "trước ghép"** → đơn `Gửi: Tài liệu | Giá trị thấp` (`FPT Tân Thuận 1 → Tòa V-City`, ghi chú `SEED X lech tuyen`), trạng thái **`Chờ ghép`**
> · **vế "sau ghép"** → đơn `Gửi: Đồ dễ vỡ | Giá trị vừa` (`LôB3, E-Office → 156 Lê Văn Khương, Q12`), trạng thái **`Đã giao`** (đã qua ghép)
> ⇒ Kết luận về **tương quan trạng thái ↔ cụm liên hệ** vẫn đứng vững, nhưng ⛔ **không phải** phép đo before/after trên cùng một đơn.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) A có đơn NEED, mở Theo dõi đơn | mở đơn `Chờ ghép` của chính `stag_anhdc4@` | ✅ PASS | — | — |
| 2 | Check toàn màn tìm cụm liên hệ "Người vận chuyển" | cuộn **hết màn** (tới `LỊCH SỬ`) rồi quét chuỗi page source: `NGƯỜI VẬN CHUYỂN` · `NGƯỜI GIAO HÀNG` · `Gọi người giao hàng` · `NGƯỜI GỬI` · `NGƯỜI NHẬN` · cả chuỗi `Gọi` — **TẤT CẢ đều KHÔNG tồn tại** | ✅ PASS | `TC-DLV-026__pre-truoc-ghep-khong-co-cum-lien-he.png` | màn đi thẳng `LỘ TRÌNH` → `ẢNH SẢN PHẨM` → `THÔNG TIN HÀNG` → `LỊCH SỬ`, ⛔ không có khối liên hệ nào |
| 3 | (setup) B nhận đơn và xác nhận | ⚠️ **thay bằng** đơn khác đã qua ghép *(xem khai sai lệch)* | ✅ PASS | — | — |
| 4 | Quay lại Theo dõi đơn bằng A, check cụm liên hệ | cụm **`NGƯỜI GIAO HÀNG`**: `Phan Thị Mỹ Anh` · `0947153040` · nút `Gọi` (desc `Gọi người giao hàng`, `clickable=true`) | ✅ PASS | `TC-DLV-026__verify-sau-ghep-co-cum-nguoi-giao-hang.png` | — |
| E2 | **KHÔNG** có cụm liên hệ "Người vận chuyển" khi đơn ở `Chờ ghép` | ✅ đúng — chứng minh bằng **quét chuỗi trên page source đã cuộn hết màn**, ⛔ không phải "nhìn ảnh không thấy" | ✅ PASS | — | — |
| E4 | Hiện cụm "Người vận chuyển" gồm tên + SĐT + nút "Gọi" | ✅ đủ 3 thành phần | ✅ PASS | — | ⚠️ **Lệch tên gọi:** TC gọi cụm là **"Người vận chuyển"**, app hiển thị **"NGƯỜI GIAO HÀNG"**. Cùng một cụm (tên + SĐT + `Gọi` của người mang hàng) ⇒ chấm PASS, nhưng **đề nghị BA chốt 1 thuật ngữ** rồi đồng bộ TC ↔ app |

**Result: ✅ PASS (4 steps, 2 expected) — kèm khai sai lệch "2 đơn thay vì 1 đơn" ở trên**
**Evidence:** `screenshots/TC-DLV-026__verify-sau-ghep-co-cum-nguoi-giao-hang.png` (+ `TC-DLV-026__pre-truoc-ghep-khong-co-cum-lien-he.png`) — verified tồn tại
**Locators captured:** 0 element mới

---
