# Vibe Test Log — VR-008 — v1.1 — 2026-09-19

> Module: ASN (Ghép nối) · Platform: mobile (Appium MCP / UiAutomator2) · App: `com.hrisproject.stag` (host FoxPro_Stag, STG)
> Evidence dir: `screenshots/` · Device: emulator-5554 · Appium session `482f2d33-da4a-4db6-ba7c-575b694b21b2`
> Phiên: 2026-09-19 (khởi tạo)
> Tập chạy: **pending 21 TC** (theo lựa chọn QC ở Step 1.2 — bỏ qua 3 TC đã PASS ở VR-007, giữ 2 TC ⛔ N-A)
> QC chốt thêm: TC cần thiết bị thứ 2/3 (`006`/`008`) và TC cần dev lùi ngày (`019`) → **cố chạy thật rồi mới kết luận**, không đánh NOT_RUN sẵn.
>
> 📸 **Ghi chú công cụ evidence:** ảnh chụp bằng `adb exec-out screencap -p > <EVID_DIR>/<tên>.png`.
> Lý do: `appium_screenshot` của MCP trả kèm ~216k ký tự HTML viewer vào context mỗi lần gọi (đã đo ở pre-flight),
> không đủ ngân sách cho ~21 TC. `SKILL.md §Step 2` cho phép `adb screencap` đúng cho vai trò evidence
> (*"adb screencap → snapshot file (evidence, NOT locator source)"*). ⛔ Locator + action vẫn 100% qua MCP.

## Tài khoản & dữ liệu STG lúc mở phiên

| Vai | Account | Ghi chú |
|---|---|---|
| **B — carrier / chủ OFFER** | `stag_anhdc4@` — Đặng Châu Anh | ✅ đang đăng nhập lúc mở phiên · hero `3 đơn đã giúp` |
| A — chủ tin | `stag_taipm@` — Phan Minh Tài | chủ 2 tin NEED đang sống trên Bảng tin |
| C — người nhận | `stag_taipm@` / `stag_huyennhk@` | — |
| D — người ngoài cặp | `stag_huyennhk@` — Nguyễn Huỳnh Kim Huyền | — |

**Bảng tin lúc mở phiên (3 tin NEED)** — `_recon__bang-tin-inventory.png`:

| # | Tuyến | Buổi | Chủ tin | Dùng cho |
|---|---|---|---|---|
| Tin 1 | Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy | Hôm nay · Sáng | A (không có badge) | khớp tuyến với OFFER của B ⇒ TC-009/010 |
| Tin 2 | FPT Tân Thuận 1 → FTEL SG08 Quận 12 | Hôm nay · Chiều | A (không có badge) | TC-002 (huỷ modal) → TC-001 (ghép) |
| Tin 3 | Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy | Hôm nay · Sáng | **B** (badge `Tin của bạn`) | ⛔ không dùng để ghép (tin của chính mình) |

---

## TC-ASN-002: Check nhấn "Huỷ" trên modal xác nhận giữ đơn ở "Chờ ghép" và không lộ SĐT

> Tin dùng: **Tin 2** (FPT Tân Thuận 1 → FTEL SG08 Quận 12 · Hôm nay · Chiều) — chủ tin **Phan Minh Tài** (A).
> Vai đang đăng nhập: **B** (`stag_anhdc4@` — Đặng Châu Anh). Step 1–2 là setup, dữ liệu đã có sẵn trên STG.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) A đăng 1 tin NEED | — | ✅ PASS | `_recon__bang-tin-inventory.png` | Tin 2 đã có sẵn, đăng 2 giờ trước |
| 2 | (setup) B mở tab Bảng tin → nhấn tin của A | find+tap `text("FPT Tân Thuận 1")` | ✅ PASS | — | mở màn Chi tiết tin |
| 3 | Nhấn "Tôi mang giúp được" | find+tap `textContains("Tôi mang giúp được")` | ✅ PASS | `TC-ASN-002__pre-modal-xac-nhan.png` | modal **"Xác nhận mang giúp"** hiện ra, 2 nút `Huỷ` / `Xác nhận` |
| 4 | Nhấn "Huỷ" trên modal | find+tap `text("Huỷ")` | ✅ PASS | — | — |
| E4 | Modal đóng, vẫn ở màn Chi tiết tin | `text("Xác nhận mang giúp")` → 🚫 NOT FOUND · tiêu đề `Chi tiết tin` còn nguyên | ✅ PASS | `TC-ASN-002__verify-huy-giu-cho-ghep.png` | — |
| 5 | Check cụm "Người gửi" + nút CTA | scroll_to_element `textContains("NGƯỜI GỬI")` | ✅ PASS | — | — |
| E5a | Cụm "Người gửi" KHÔNG hiển thị SĐT | `text("0833329408")` → 🚫 NOT FOUND; cụm chỉ có tên `Phan Minh Tài` + nút `Gọi` **mờ/disabled** | ✅ PASS | `TC-ASN-002__verify-huy-giu-cho-ghep.png` | SĐT thật của A trong hồ sơ = `0833329408` (USR-accounts §1) ⇒ phép thử âm có đối chứng, ⛔ không phải "không thấy chữ số nào" |
| E5b | Nút "Tôi mang giúp được" vẫn hiển thị | `textContains("Tôi mang giúp được")` → ✅ tìm thấy | ✅ PASS | `TC-ASN-002__verify-huy-giu-cho-ghep.png` | — |
| E5c | Đơn vẫn ở trạng thái "Chờ ghép" | *(suy từ CTA còn hiển thị — xem Notes)* | ✅ PASS | `TC-ASN-002__verify-huy-giu-cho-ghep.png` | ⚠️ Màn Chi tiết tin **không in chuỗi "Chờ ghép"**; oracle dùng được là **CTA `Tôi mang giúp được` còn hiển thị** — tin đã ghép thì mất CTA này (đối chứng: `TC-ASN-013` VR-007 xác nhận CTA biến mất khi không đủ điều kiện nhận). Tin cũng còn nguyên trên Bảng tin ở TC-ASN-001 ngay sau đó |

**Result: ✅ PASS (4 steps, 3 expected)**
**Evidence:** `screenshots/TC-ASN-002__verify-huy-giu-cho-ghep.png` (+ `TC-ASN-002__pre-modal-xac-nhan.png`) — verified tồn tại
**Locators captured:** 3 element mới (modal `Xác nhận mang giúp`, nút `Huỷ`, nút `Xác nhận`)

---

## TC-ASN-001: Check Carrier xác nhận "Tôi mang giúp được" đưa đơn sang trạng thái "Đã ghép"

> Tin dùng: **Tin 2** (FPT Tân Thuận 1 → FTEL SG08 Quận 12 · Chiều) — chủ tin **Phan Minh Tài** (A). Vai đang đăng nhập: **B** (`stag_anhdc4@`).
> ℹ️ Chạy nối ngay sau `TC-ASN-002` trên cùng tin: `002` đã bấm `Huỷ` nên tin vẫn `Chờ ghép` ⇒ tiền đề của `001` còn nguyên.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) A đăng 1 tin NEED rồi đăng xuất | — | ✅ PASS | `_recon__bang-tin-inventory.png` | Tin 2 có sẵn trên STG |
| 2 | (setup) B nhấn tab "Bảng tin" và nhấn tin của A | find+tap `text("FPT Tân Thuận 1")` | ✅ PASS | — | — |
| 3 | Nhấn "Tôi mang giúp được" | find+tap `textContains("Tôi mang giúp được")` | ✅ PASS | — | modal `Xác nhận mang giúp` hiện ra |
| 4 | Nhấn "Xác nhận" trên modal | find+tap `text("Xác nhận")` | ✅ PASS | — | — |
| E4 | Mở màn Theo dõi đơn của đơn vừa nhận | tiêu đề `Theo dõi đơn` ✓ · stepper sáng tới mốc `Lấy hàng` · CTA `Tôi đã lấy hàng` + `Huỷ nhận đơn` | ✅ PASS | `TC-ASN-001__verify-theo-doi-don-mo.png` | ⛔ không còn CTA `Tôi mang giúp được` |
| 5 | (setup) Nhấn tab "Hoạt động" | find+tap `text("Hoạt động")` | ✅ PASS | — | mở màn `Đơn của tôi`, tab con `Đang diễn ra` |
| 6 | Check card của đơn vừa nhận | — | ✅ PASS | `TC-ASN-001__verify-card-da-ghep.png` | — |
| E6a | Card hiển thị badge "Đã ghép" | `text("Đã ghép")` → ✅ tìm thấy | ✅ PASS | `TC-ASN-001__verify-card-da-ghep.png` | badge nằm trên card `FPT Tân Thuận 1 → FTEL SG08 Quận 12` |
| E6b | Tài khoản B ở vai **người vận chuyển** | `textStartsWith("Giao:")` → get_text = `Giao: Tài liệu \| Giá trị thấp` | ✅ PASS | `TC-ASN-001__verify-card-da-ghep.png` | 🔑 **Oracle vai:** app phân vai bằng **tiền tố card** — `Giao:` = mình vận chuyển · `Gửi:` = mình là chủ tin. Cùng màn còn card `Gửi:` (tin của chính B) ⇒ đối chứng 2 vai trên 1 ảnh |

**Result: ✅ PASS (6 steps, 3 expected)**
**Evidence:** `screenshots/TC-ASN-001__verify-card-da-ghep.png` (+ `TC-ASN-001__verify-theo-doi-don-mo.png`) — verified tồn tại
**Locators captured:** 4 element mới (`Xác nhận`, màn `Theo dõi đơn`, badge `Đã ghép`, tiền tố card `Giao:`)

---

## TC-ASN-004: Check sau khi ghép cả người gửi và người vận chuyển đều thấy SĐT của bên còn lại

> ⚠️ **TC này chạy 2 chặng trên 2 tài khoản.** Chặng này (E3) chạy bằng **B**; chặng E5 cần đăng nhập **A** — xem section `TC-ASN-004 (tiếp)` bên dưới.
> Tin dùng: **Tin 2**, vừa được B ghép ở `TC-ASN-001`. Tin có khai người nhận ⇒ tiền đề *"A khai C là người nhận"* thoả.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) A đăng tin NEED khai C là người nhận | — | ✅ PASS | `TC-ASN-004__verify-b-thay-sdt-a-va-c.png` | người nhận khai sẵn = **Nguyễn Huỳnh Kim Huyền** (`stag_huyennhk@` = vai C) |
| 2 | (setup) B nhận đơn bằng "Tôi mang giúp được" và xác nhận | *(đã thực hiện ở TC-ASN-001 step 3–4)* | ✅ PASS | — | — |
| 3 | Check cụm liên hệ trên màn Theo dõi đơn của B | swipe xuống cụm `NGƯỜI GỬI` / `NGƯỜI NHẬN` | ✅ PASS | `TC-ASN-004__verify-b-thay-sdt-a-va-c.png` | — |
| E3a | B thấy SĐT của tài khoản A | `text("0833329408")` → ✅ tìm thấy | ✅ PASS | `TC-ASN-004__verify-b-thay-sdt-a-va-c.png` | cụm `NGƯỜI GỬI`: `Phan Minh Tài` · `0833329408` · `stag_taipm@fpt.com` · nút `Gọi` **bật** |
| E3b | B thấy SĐT của người nhận C | `text("0989014863")` → ✅ tìm thấy | ✅ PASS | `TC-ASN-004__verify-b-thay-sdt-a-va-c.png` | cụm `NGƯỜI NHẬN`: `Nguyễn Huỳnh Kim Huyền` · `0989014863` · nút `Gọi` **bật** |

**Result chặng B: ✅ PASS** — chờ chặng E5 (vai A) để chốt verdict cuối.
**Evidence:** `screenshots/TC-ASN-004__verify-b-thay-sdt-a-va-c.png` — verified tồn tại

> 🔑 **Đối chứng mạnh cho `BR-CON-02`:** cùng 1 tin, cùng 1 tài khoản B —
> **trước ghép** (`TC-ASN-002`) cụm `NGƯỜI GỬI` **không có** SĐT, nút `Gọi` mờ;
> **sau ghép** (`TC-ASN-004`) có đủ SĐT + email, nút `Gọi` bật. ⇒ SĐT lộ **đúng lúc ghép**, không sớm hơn.
> 🆕 **Dữ liệu mới thu được:** SĐT của `stag_huyennhk@` (Nguyễn Huỳnh Kim Huyền) = **`0989014863`** — trước phiên này `USR-accounts.md §1` còn để trống.

---

## TC-ASN-020: Check Carrier huỷ nhận đơn trước khi lấy hàng thì tin trở lại Bảng tin và Carrier khác ghép được

> ⚠️ **TC chạy 2 chặng trên 2 tài khoản.** Chặng này (step 1–5) chạy bằng **B**; chặng step 6–9 cần **Carrier khác** — xem `TC-ASN-020 (tiếp)`.
> Tin dùng: **Tin 1** (Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy · Hôm nay · Sáng) — chủ tin A (`stag_taipm@`).

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) A đăng 1 tin NEED rồi đăng xuất | — | ✅ PASS | — | Tin 1 có sẵn trên STG (đăng ~09:43) |
| 2 | (setup) B nhận đơn + xác nhận, **KHÔNG** nhấn "Tôi đã lấy hàng" | find+tap `textContains("Tôi mang giúp được")` → `text("Xác nhận")` | ✅ PASS | `TC-ASN-020__pre-da-ghep-truoc-khi-huy.png` | stepper dừng ở `Lấy hàng`, ⛔ chưa bấm `Tôi đã lấy hàng` ⇒ đúng tiền đề "trước khi lấy hàng" |
| 3 | B huỷ nhận đơn | find+tap `text("Huỷ nhận đơn")` | ✅ PASS | — | modal `Huỷ nhận đơn` mở, nút `Xác nhận` **disabled** khi chưa nhập lý do |
| 4 | Nhập lý do huỷ | set_value `textStartsWith("Nhập lý do bạn muốn huỷ đơn")` = `Doi lich, khong di tuyen nay nua` | ✅ PASS | `TC-ASN-020__pre-ly-do-huy.png` | sau khi nhập: `get_element_attribute(enabled)` của `Xác nhận` = **`true`** ⇒ `Lý do huỷ` là field **bắt buộc** |
| 5 | Xác nhận huỷ | find+tap `text("Xác nhận")` → `text("Đồng ý")` | ✅ PASS | — | — |
| E5 | Đơn chuyển về trạng thái "Chờ ghép" | modal kết quả: **"Đã huỷ — Đã huỷ nhận đơn. Đơn đã trả lại bảng tin."** · sau đó tin xuất hiện lại trên Bảng tin | ✅ PASS | `TC-ASN-020__verify-tin-tro-lai-bang-tin.png` | Bảng tin của B sau huỷ có lại đúng card `Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy · Hôm nay · Sáng`, ⛔ không có badge `Tin của bạn` (tin của A) |

| E5b | Chủ tin cũng thấy đơn về "Chờ ghép" *(bổ sung, chụp lúc đã đăng nhập vai A)* | màn `Đơn của tôi` của **A**: card `V-City → FPT Cầu Giấy` mang badge **`Chờ ghép`** | ✅ PASS | `TC-ASN-020__verify-chu-tin-thay-cho-ghep.png` | 🔑 Xác nhận **2 phía**: không chỉ carrier thấy tin trở lại Bảng tin, mà **chủ tin** cũng thấy đơn rơi về `Chờ ghép` ⇒ trạng thái thật sự đổi ở backend, ⛔ không phải chỉ ẩn/hiện phía carrier |

**Result chặng B: ✅ PASS (step 1–5)** — chờ chặng step 6–9 (Carrier khác) để chốt verdict cuối.
**Evidence:** `screenshots/TC-ASN-020__verify-tin-tro-lai-bang-tin.png` + `screenshots/TC-ASN-020__verify-chu-tin-thay-cho-ghep.png` (+ `TC-ASN-020__pre-da-ghep-truoc-khi-huy.png`, `TC-ASN-020__pre-ly-do-huy.png`) — verified tồn tại

---

## 🔎 Ghi nhận giữa lô 1 — quan sát ảnh hưởng tới TC-ASN-009 (chưa chấm verdict)

> ⛔ **Đây KHÔNG phải verdict.** Ghi lại để chặng sau chạy `TC-ASN-009` đúng cách và để QC/BA biết có dấu hiệu cần soi.

Khi mở icon chuông bằng tài khoản **B** lúc 11:44 (B đang có tin OFFER `Chờ ghép` tuyến `Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy`, đăng hôm nay **08:29**):

| Phép thử qua MCP | Kết quả |
|---|---|
| `textContains("Tìm thấy đơn hàng phù hợp tuyến")` trong màn Thông báo FoxEco | 🚫 **NOT FOUND** |
| `text("HÔM NAY")` (nhóm ngày) | 🚫 **NOT FOUND** ⇒ B có **0 thông báo hôm nay** trong FoxEco |
| Danh sách FoxEco mở ra nhóm đầu tiên là | `HÔM QUA` |

Ảnh màn Thông báo của B lúc 11:44: `screenshots/_recon__thong-bao-b-1144.png` *(đặt tên `_recon__` vì `TC-ASN-009` **chưa chạy** — ⛔ ảnh không được mang mã TC khi chưa có verdict)*.

⚠️ **Nhưng** màn Thông báo của **host FoxPro** lúc mở app (11:33, cùng tài khoản B) **CÓ** dòng
`Tìm thấy đơn hàng phù hợp tuyến của bạn — 19/09 - 09:43` (`_setup__preflight-launch.png`).
⇒ Cùng 1 tài khoản, cùng 1 thời điểm: **host FoxPro có, FoxEco in-app không có.**

🔍 Tin 1 (`V-City → Cầu Giấy · Sáng`, chủ A) đăng ~09:43 — đúng mốc thông báo đó, và **trùng tuyến tuyệt đối** với OFFER của B.
`VR-007/TC-ASN-023` đã tìm thấy thông báo này **trong màn FoxEco** lúc 09:43 ⇒ lúc đó nó CÓ, bây giờ KHÔNG.

⛔ **Chưa kết luận** vì chưa loại trừ được: (a) thông báo rụng khỏi danh sách FoxEco sau một khoảng thời gian,
(b) rụng sau khi đã đọc/đã tap, (c) danh sách FoxEco phân trang/lọc khác host.
⇒ `TC-ASN-009` sẽ được chạy **đúng kịch bản của nó** (A đăng tin NEED **mới** rồi mới kiểm chuông của B),
⛔ không chấm verdict dựa trên dữ liệu cũ 2 tiếng.

---

## 🔄 Đổi tài khoản: B (`stag_anhdc4@`) → A (`stag_taipm@` — Phan Minh Tài)

Luồng `USR-accounts.md §0b` chạy đúng 5 bước, ⛔ không cần người nhập tay:
FoxPro `Cá nhân` → scroll `Đăng xuất` → `Đồng ý` → `Nhập email đăng nhập` = `stag_taipm@fpt.com` → `NHẬN MÃ OTP`
→ `adb shell input text "$FOXECO_STG_OTP"` *(đọc từ `~/.foxeco-v2/credentials.env`, ⛔ không in ra log)* → `ĐĂNG NHẬP`
→ FoxPro `Chức năng` → `scroll_to_element text("FoxEco")` (4 nhịp) → tap.
**Evidence:** `screenshots/_setup__login-taipm-foxeco.png` · ⏱️ ~11:50→11:53.

---

## TC-ASN-003: Check đơn ghép ngay mà chủ tin không phải thực hiện bước duyệt nào

> Đơn dùng: **Tin 2** (FPT Tân Thuận 1 → FTEL SG08 Quận 12), do A đăng và đã được B ghép ở `TC-ASN-001`.
> Vai đang đăng nhập: **A** = chủ tin.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) A đăng 1 tin NEED rồi đăng xuất | — | ✅ PASS | — | Tin 2 |
| 2 | (setup) B mở tin của A, "Tôi mang giúp được" → "Xác nhận", rồi đăng xuất | *(đã thực hiện ở TC-ASN-001)* | ✅ PASS | — | — |
| 3 | (setup) Đăng nhập lại bằng tài khoản A | luồng `§0b` | ✅ PASS | `_setup__login-taipm-foxeco.png` | — |
| 4 | Nhấn tab "Hoạt động" và mở đơn vừa được nhận | find+tap `text("Hoạt động")` → tap card `text("Đã ghép")` | ✅ PASS | — | — |
| E4 | Đơn đã ở trạng thái "Đã ghép" | `textContains("Đã ghép · chờ shipper lấy hàng")` → ✅ tìm thấy | ✅ PASS | `TC-ASN-003__verify-khong-co-nut-duyet.png` | stepper: `Chờ ghép` ✓ → `Lấy hàng` (mốc hiện tại) |
| 5 | Check toàn màn Theo dõi đơn tìm nút chấp nhận / duyệt / phê duyệt | 3 phép `find_element` phủ định trên **toàn cây** (kể cả node ngoài viewport) | ✅ PASS | `TC-ASN-003__verify-khong-co-nut-duyet.png` | — |
| E5 | KHÔNG có nút chấp nhận / duyệt / phê duyệt nào | `textContains("Duyệt")` 🚫 · `textContains("Chấp nhận")` 🚫 · `textContains("Phê duyệt")` 🚫 | ✅ PASS | `TC-ASN-003__verify-khong-co-nut-duyet.png` | Nút hành động **duy nhất** của chủ tin = `Huỷ đơn`. Dải trạng thái `Đã ghép · chờ shipper lấy hàng` là **nhãn tĩnh, không bấm được** ⇒ chủ tin ⛔ không có bước duyệt nào ⇒ đúng cơ chế "ghép ngay" (`BR-CON-01`) |

**Result: ✅ PASS (5 steps, 2 expected)**
**Evidence:** `screenshots/TC-ASN-003__verify-khong-co-nut-duyet.png` — verified tồn tại
**Locators captured:** 2 element mới (nhãn `Đã ghép · chờ shipper lấy hàng`, nút `Huỷ đơn` của chủ tin)

---

## TC-ASN-004 (tiếp — chặng A): Check sau khi ghép cả người gửi và người vận chuyển đều thấy SĐT của bên còn lại

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 4 | Đăng nhập lại bằng tài khoản A, mở đơn đó | luồng `§0b` → `Hoạt động` → card `Đã ghép` | ✅ PASS | `_setup__login-taipm-foxeco.png` | — |
| 5 | Check cụm liên hệ của tài khoản A | swipe tới cụm `NGƯỜI GIAO HÀNG` | ✅ PASS | — | — |
| E5 | A thấy SĐT của tài khoản B | `text("0343439724")` → ✅ tìm thấy | ✅ PASS | `TC-ASN-004__verify-a-thay-sdt-b.png` | cụm `NGƯỜI GIAO HÀNG`: `Đặng Châu Anh` · `0343439724` · nút `Gọi` **bật**. Khớp SĐT hồ sơ của B ở `USR-accounts.md §1` |

**Result: ✅ PASS (đủ 2 chặng — E3 trên vai B, E5 trên vai A)**
**Evidence:** `screenshots/TC-ASN-004__verify-a-thay-sdt-b.png` + `screenshots/TC-ASN-004__verify-b-thay-sdt-a-va-c.png` — verified tồn tại

> ✅ **`BR-CON-02` được kiểm chứng đối xứng đủ 3 vai trên cùng 1 đơn:**
> B thấy `A 0833329408` + `C 0989014863` · A thấy `B 0343439724`.
> ⛔ Không vai nào thấy SĐT trước thời điểm ghép (đối chứng `TC-ASN-002`).

---

## 🌱 SEED lô 2 — 4 tin NEED do A đăng (setup cho TC-ASN-009/010/011/012/022)

> Thiết kế: **mỗi seed lệch OFFER của B đúng MỘT chiều** ⇒ 1 lần kiểm chuông của B phân giải được cả 4 TC.
> Mốc đối chiếu — **OFFER của B**: `Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy` · `Hôm nay` · buổi **Sáng** · `Chờ ghép` (đăng hôm nay 08:29).
> Mọi seed đều ghi dấu ở ô **GHI CHÚ** để phân biệt khi mở Chi tiết tin.

| Seed | Ghi chú trong tin | Điểm lấy | Điểm giao | Khoảng ngày | Buổi | Lệch chiều nào | Phục vụ |
|---|---|---|---|---|---|---|---|
| **S1** | `SEED S1 - khop tuyen day du` | Tòa V-City, Lê Thái Tổ | **FPT Cầu Giấy** | Hôm nay | **Sáng** | ⭐ **KHỚP ĐỦ 3 điều kiện** | TC-ASN-009 · 010 |
| **S2** | `SEED S2 - lech diem giao` | Tòa V-City, Lê Thái Tổ | **FPT Tân Thuận 1** | Hôm nay | Sáng | ❶ **điểm giao** | TC-ASN-011 |
| **S3** | `SEED S3 - lech khoang ngay` | Tòa V-City, Lê Thái Tổ | FPT Cầu Giấy | **22/09/2026 – 22/09/2026** | Giờ nào cũng được | ❷ **khoảng ngày** (⛔ không overlap 19/09) | TC-ASN-012 |
| **S4** | `SEED S4 - lech buoi sau gio lam` | Tòa V-City, Lê Thái Tổ | FPT Cầu Giấy | Hôm nay *(overlap)* | **Sau giờ làm (17–19h)** | ❸ **buổi** | TC-ASN-022 |

⏱️ S1 đăng lúc **12:09:50**; S2 ~12:14; S4 ~12:20; S3 ~12:28. Cả 4 đều hiện `Đăng tin thành công!` (MCP-verified).
**Evidence setup:** `_setup__seed-s1-buoc2.png` · `_setup__seed-s1-truoc-dang.png`

> 🔎 **S3 dùng đúng nhánh (b) của `SC-ASN-011`:** chọn buổi `Giờ nào cũng được` **cố ý**, để chứng minh
> biến *buổi* ⛔ **không cứu được** khi *ngày* đã lệch — đúng chủ đích ghi trong `TC-ASN-012` Notes.

### 🐞 Phát hiện phụ khi seed — ảnh quá khổ bị từ chối **im lặng** (ngoài scope ASN)

| Việc | Kết quả |
|---|---|
| Chọn ảnh `seed-ord-oversize-5mb.jpg` (5 MB, còn lại từ bộ seed ORD) qua `Chọn từ thư viện` → `Add (1)` | Picker đóng bình thường, ⛔ **không có thông báo lỗi nào** |
| Đếm ảnh trên form sau đó | vẫn **`0/5`** (MCP `text("0/5")` ✅ tìm thấy, `text("1/5")` 🚫 NOT FOUND) |
| Chọn ảnh thường (~vài trăm KB) cùng thao tác | **`1/5`** ✅ — nút `Tiếp theo` qua được ngay |
| Logcat lúc thất bại | `MediaProvider: Open with lower FS for /storage/emulated/0/Pictures/seed-ord-oversize-5mb.jpg` — ⛔ không có exception phía app |

⇒ App **chặn đúng** ảnh quá khổ nhưng **không nói cho người dùng biết**: người dùng thấy `ẢNH HÀNG *` vẫn `0/5`
và nút `Tiếp theo` không ăn, mà không hiểu vì sao. 📌 **Thuộc module ORD (wizard đăng tin), ⛔ không thuộc TC ASN nào**
⇒ đề xuất QC mở bug riêng cho ORD; phiên này chỉ ghi nhận, ⛔ không tự tạo verdict ngoài scope.
⚠️ Đây cũng là **bẫy cho automation**: `Chụp ảnh` bằng camera emulator cũng **không** gắn được ảnh (viewfinder đen, shutter không sinh file)
⇒ script tự động phải chọn ảnh thường từ thư viện, ⛔ đừng dùng camera và ⛔ đừng dùng ảnh trong bộ seed oversize.

---

## 🔄 Đổi tài khoản: A (`stag_taipm@`) → B (`stag_anhdc4@`) — để kiểm chuông

Luồng `§0b`, ~12:29→12:31. Không có ảnh `_setup__` riêng (đã có ảnh cho lượt đổi trước; lượt này chỉ lặp lại luồng đã chứng minh).

---

## TC-ASN-009: Check Carrier nhận thông báo khớp tuyến khi có tin NEED trùng cả hai điểm và giao khung giờ

> OFFER của B: `Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy` · Hôm nay · **Sáng** (đăng 08:29, `Chờ ghép`).
> Tin NEED của A: **SEED S1** — trùng đủ 2 điểm + ngày + buổi, đăng **12:09:50**.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) B đăng 1 tin OFFER với điểm lấy/giao + khung giờ xác định, rồi đăng xuất | — | ✅ PASS | — | OFFER có sẵn từ 08:29, xác minh `Chờ ghép` ở lô 1 |
| 2 | (setup) A đăng 1 tin NEED trùng 2 điểm + giao khung giờ, rồi đăng xuất | wizard 3 bước (xem §SEED lô 2) | ✅ PASS | `_setup__seed-s1-buoc2.png`, `_setup__seed-s1-truoc-dang.png` | SEED S1 · `Đăng tin thành công!` lúc 12:09:50 |
| 3 | (setup) Đăng nhập bằng tài khoản B | luồng `§0b` | ✅ PASS | — | 12:29→12:31 |
| 4 | Nhấn icon chuông | find+tap `accessibility id "Thông báo"` | ✅ PASS | `TC-ASN-009__verify-thong-bao-khop-tuyen.png` | — |
| E4 | Danh sách có thông báo *"Tìm thấy đơn hàng phù hợp tuyến của bạn"* | `textContains("Tìm thấy đơn hàng phù hợp tuyến")` → ✅ tìm thấy · nhóm **`HÔM NAY`** xuất hiện, mục mới nhất **`20 phút trước`** (≈12:11, khớp mốc đăng S1 12:09:50) | ✅ PASS | `TC-ASN-009__verify-thong-bao-khop-tuyen.png` | Phụ đề đúng nguyên văn: *"Tìm thấy đơn hàng phù hợp tuyến của bạn — xem chi tiết để nhận giao"* |
| 5 | Nhấn vào thông báo khớp tuyến | tap `textContains("Tìm thấy đơn hàng phù hợp tuyến").instance(0)` | ✅ PASS | — | — |
| E5 | Mở màn Chi tiết tin của **đúng** tin NEED đã đăng ở bước 2 | mở `Chi tiết tin`, tin `22 phút trước`; `textContains("SEED S1")` → ✅ **tìm thấy** trong ô Ghi chú | ✅ PASS | `TC-ASN-009__verify-tro-dung-tin-seed-s1.png` | 🔑 Dấu `SEED S1` cắm sẵn ở ô **GHI CHÚ** lúc đăng là oracle định danh — ⛔ không phải suy từ thời gian |

**Result: ✅ PASS (5 steps, 2 expected)**
**Evidence:** `screenshots/TC-ASN-009__verify-tro-dung-tin-seed-s1.png` (+ `TC-ASN-009__verify-thong-bao-khop-tuyen.png`) — verified tồn tại
**Locators captured:** 2 element (thông báo khớp tuyến `.instance(0)`, nhóm ngày `HÔM NAY`)

> 🟢 **Đính chính ghi nhận giữa lô 1 (11:44):** lúc đó `HÔM NAY` và `textContains("Tìm thấy...")` đều 🚫 NOT FOUND,
> nhưng 12:31 thì **cả 3 thông báo khớp tuyến hôm nay đều hiện**, gồm cả cái cũ nay hiển thị `2 giờ trước` (≈10:31 → gốc ~09:43).
> ⇒ Thông báo **không hề mất**; danh sách FoxEco lúc 11:44 **hiển thị dữ liệu cũ** (app bị nền lâu, chưa refresh).
> 📌 Vẫn nên báo QC/BA: **màn Thông báo không tự làm mới** khi mở lại sau thời gian dài ⇒ người dùng tưởng không có thông báo.
> ⛔ Chưa mở bug trong phiên này vì chưa có TC nào phủ hành vi refresh, và chưa thử lại có kiểm soát (kéo-làm-mới / kill app).

---

## ⏸️ DỪNG PHIÊN THEO YÊU CẦU QC — 2026-09-19 12:33

> QC yêu cầu dừng ("mai tiếp"). Ghi lại **chính xác** trạng thái đang dở để phiên sau nối tiếp, ⛔ không suy đoán kết quả.

### Việc đang dở giữa chừng (KHÔNG chấm verdict)

| TC | Đã có gì | Còn thiếu gì để chốt |
|---|---|---|
| **TC-ASN-010** | Đang đứng **đúng màn Chi tiết tin của SEED S1**, mở từ thông báo khớp tuyến | Chưa bấm CTA. ⚠️ **Quan sát cần soi:** CTA trên màn này là **`Tôi mang giúp được`**, ⛔ **không phải `Nhận giao`** như `TC-ASN-010` Steps mô tả. Fragment v1.0 dặn *"giữ đúng nhãn từng luồng, ⛔ không đồng nhất hoá"* ⇒ **nghi lệch tài liệu hoặc lệch app**, phải chạy thật rồi mới kết luận |
| **TC-ASN-011 / 012 / 022** | 3 seed âm (S2/S3/S4) **đã đăng xong**; ảnh danh sách chuông 12:31 cho thấy **chỉ 3 thông báo khớp tuyến hôm nay** (`20 phút` = S1 · `41 phút` ≈11:50 · `2 giờ` ≈10:31) — ⛔ **không có** mốc nào rơi vào 12:14 (S2) / 12:20 (S4) / 12:28 (S3) | Thiếu **ảnh evidence RIÊNG cho từng TC** tại điểm verify (⛔ cấm 1 ảnh cho 3 TC) và thiếu bước tap xác minh 2 thông báo còn lại **không** trỏ tới S2/S3/S4. ⇒ giữ `⏳ NOT_RUN`, **⛔ không khai PASS dù dấu hiệu rất thuận** |
| **TC-ASN-020** | Chặng B xong (nhận → huỷ → tin trở lại Bảng tin, đã verify 2 phía) | Còn step 6–9: **Carrier khác** (≠ taipm, ≠ anhdc4) đăng nhập, mở tin, ghép được |

### 🔎 Manh mối cho thông báo `41 phút trước` (≈11:50)
Đúng mốc B **huỷ nhận đơn** Tin 1 ở `TC-ASN-020` (11:49) ⇒ nghi ngờ **tin trở lại Bảng tin thì bắn lại thông báo khớp tuyến** cho chủ OFFER.
⛔ Chưa kiểm chứng — phiên sau tap vào nó để xem trỏ tới tin nào.

### 🗂️ Dữ liệu sống trên STG lúc dừng (⛔ đừng seed lại)

| Tin | Chủ | Tuyến | Ngày | Buổi | Trạng thái | Ghi chú nhận dạng |
|---|---|---|---|---|---|---|
| Tin 1 | A (taipm) | V-City → FPT Cầu Giấy | Hôm nay | Sáng | **Chờ ghép** *(đã trả lại sau huỷ)* | dùng cho `TC-ASN-020` step 6–9 |
| Tin 2 | A (taipm) | FPT Tân Thuận 1 → FTEL SG08 Q12 | Hôm nay | Chiều | **Đã ghép** *(B là carrier)* | dùng cho `TC-ASN-005`/`007` |
| Tin 3 | B (anhdc4) | V-City → FPT Cầu Giấy | Hôm nay | Sáng | Chờ ghép | tin của chính B |
| **SEED S1** | A | V-City → FPT Cầu Giấy | Hôm nay | Sáng | Chờ ghép | ghi chú `SEED S1` · dùng cho `TC-ASN-010` |
| **SEED S2** | A | V-City → **FPT Tân Thuận 1** | Hôm nay | Sáng | Chờ ghép | ghi chú `SEED S2` · `TC-ASN-011` |
| **SEED S3** | A | V-City → FPT Cầu Giấy | **22/09** | Giờ nào cũng được | Chờ ghép | ghi chú `SEED S3` · `TC-ASN-012` |
| **SEED S4** | A | V-City → FPT Cầu Giấy | Hôm nay | **Sau giờ làm** | Chờ ghép | ghi chú `SEED S4` · `TC-ASN-022` |
| OFFER B | B (anhdc4) | V-City → FPT Cầu Giấy | Hôm nay | Sáng | Chờ ghép | mốc đối chiếu khớp tuyến |
| OFFER A | A (taipm) | FPT Tân Thuận 1 → FTEL SG08 Q12 | — | Chiều | Chờ ghép | — |

**Tài khoản đang đăng nhập lúc dừng: `stag_anhdc4@` (Đặng Châu Anh — vai B).**

---
