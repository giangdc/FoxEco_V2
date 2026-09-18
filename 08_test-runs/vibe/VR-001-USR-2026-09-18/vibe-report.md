# Vibe Test Report — VR-001 — v1.1 (+ CARRIED v1.0) — 2026-09-18

> Platform: **mobile** (Appium MCP / UiAutomator2) · Device: **emulator-5554** (Pixel 7 AVD, 1080×2400)
> Environment: **STG** — host app `com.hrisproject.stag` (FoxPro) → Chức năng → FoxEco
> Tài khoản: **A** — "Đặng Châu Giang" · MNV `00131946` · Ban Giám đốc
> Module: **USR** (Tài khoản & Hồ sơ) · Session 10:25 → 12:10

## Scope Coverage ★★

> Mẫu số là **SCOPE_TOTAL của module = 46 TC**, không phải số TC chạy phiên này.
> 🔴 **46 = 38 (v1.1) + 8 (CARRIED v1.0)** — `v1.1` **không gộp CARRIED** (`CLAUDE.md §TC-MASTER`) ⇒ phủ đủ module phải mở **cả 2 fragment**.

| | Count | % scope |
|---|--:|--:|
| **SCOPE_TOTAL (module USR)** | **46** | 100% |
| Chạy **trong run này** | **40** | 87% |
| ✅ PASS từ run trước (không chạy lại) | 0 | 0% |
| ⛔ N-A (cố ý không test qua UI, có lý do) | 2 | 4% |
| ⏳ **NOT_RUN (còn nợ)** | **4** | **9%** |
| ⚠️ NOT_EVIDENCED (còn nợ) | 0 | 0% |

**Còn nợ = 4 TC → §8 = PARTIAL.**

- Chi tiết từng TC **của module (xuyên run)**: `08_test-runs/vibe/coverage/coverage-USR.md` ← **xem cái này**
- Chi tiết **run này làm gì**: `scope-ledger.md`

## Kết quả các TC chạy trong run này

| Result | Count | % trên 40 |
|---|--:|--:|
| ✅ PASS | **19** | 48% |
| ❌ FAIL | **15** | 38% |
| 🚫 BLOCKED | **6** | 15% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|---|---|
| TC có evidence / tổng TC đã chạy | **40/40 (100%)** |
| File ảnh trong `screenshots/` | **66** (40 TC + 2 `_setup`/`_recon` + ảnh `__pre`/`__step` phụ) |
| Ảnh trùng md5 mang 2 mã TC khác nhau | **0** |
| TC thiếu evidence (⚠️ NOT_EVIDENCED) | **không có** |
| Gate `.claude/hooks/verify_evidence.py` | phần **evidence + trích dẫn: ✅ 40/40**; **coverage: còn nợ 4** ⇒ §8 PARTIAL |

→ QC lead verify lại từng case bằng `screenshots/TC-USR-<NNN>__verify*.png` (1 file riêng/TC).

## 🐞 ỨNG VIÊN BUG — đã nhóm theo nguyên nhân, KHÔNG phải 15 bug rời

> 🔄 **ĐÍNH CHÍNH 2026-09-18 — còn 7 ứng viên bug, KHÔNG phải 8: `B1` ĐÃ RÚT LẠI.**
> QC GiangDC2 chốt hành vi app của `TC-USR-015` là **ĐÚNG** (lưu xong **không có banner** + **điều hướng về màn "Cá nhân"**)
> ⇒ đã sửa `Expected Result` của TC (fragment + TC-MASTER v1.1 + LATEST), verdict `TC-USR-015`: **❌ FAIL → ✅ PASS**.
> ⇒ Bảng dưới **giữ nguyên nội dung gốc của phiên** để truy vết; dòng `B1` đọc kèm đính chính này.
> Kết quả phiên sau đính chính: **20 PASS / 14 FAIL / 6 BLOCKED / 2 N-A / 4 NOT_RUN** (tổng verdict cuối 42/46 **không đổi**).
> ⚠️ `TC-USR-027` (BLOCKED) và `TC-USR-029` (FAIL) **neo vào banner nay đã bỏ** ⇒ chờ QC quyết; `029` vẫn còn lý do FAIL thứ hai (**B4**).
> 📄 Verdict của record: `coverage/coverage-USR.md`.

> 15 TC FAIL **không** tương ứng 15 defect: nhiều TC FAIL vì **cùng một lỗi**, và 3 TC FAIL do **dây chuyền**.

| # | Defect | Sev đề xuất | TC FAIL | Kỳ vọng ⟷ Thực tế |
|---|---|---|---|---|
| ~~**B1**~~ 🔄 **RÚT LẠI 2026-09-18** | ~~Lưu thành công KHÔNG có banner + app thoát màn~~ — **hành vi ĐÚNG theo QC chốt**, Expected của TC đã sửa | ⛔ **không phải bug** | `TC-USR-015` | KV: banner xanh `Đã lưu thông tin của bạn` ngay trên nút Lưu, **màn ở lại** ⟷ TT: **0 banner** (soi **60 frame**), app **về màn Cá nhân**. Dữ liệu **vẫn lưu đúng** (`TC-USR-016` PASS) ⇒ lỗi **UI feedback**, không mất dữ liệu |
| **B2** | **Chặn lưu IM LẶNG — không thông báo lỗi nào** | 🔴 **Cao** | `TC-USR-021` `TC-USR-022` | KV: thông báo lỗi đỏ dưới field ⟷ TT: **0 thông báo**, giá trị **không được lưu**. Input `0912 345 678` (khoảng trắng) và `+84912345678`. Xác minh **2 lượt + kiểm persist** |
| **B3** | **Chuỗi thông báo lỗi lệch chuỗi BA đã chốt** | 🟠 TB | `TC-USR-017` `TC-USR-018` `TC-USR-020` `TC-USR-023` | `017` KV `Vui lòng nhập số điện thoại` ⟷ TT `Số điện thoại không được để trống`; `018/020/023` KV `Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)` ⟷ TT `Số điện thoại không hợp lệ` (thiếu phần trong ngoặc). Màu đỏ + vị trí + chặn lưu **đều đúng** |
| **B4** | **Text gõ tay KHÔNG bị xoá rỗng khi rời field, và BỊ LƯU làm địa chỉ mặc định** | 🔴 **Cao** | `TC-USR-028` *(+ dây chuyền `029` `030`)* | KV: rời field ⇒ ô về rỗng ⟷ TT: giữ `asdfghjkl1`, bấm Lưu thì **persist chuỗi rác**. Đã loại trừ "chưa blur" bằng **3 tín hiệu** (`focused=false`, bàn phím ẩn, 2 vùng trống). ⚠️ Chuỗi rác này sẽ **prefill sang địa chỉ lấy hàng của đơn** ⇒ ảnh hưởng ngoài USR |
| **B5** | **Gợi ý địa chỉ tìm theo MÃ TỈNH, không chỉ theo tên VP** | 🟠 TB | `TC-USR-039` | KV: `hcm` → 0 gợi ý (không tên VP nào chứa "hcm") ⟷ TT: **12 gợi ý** toàn VP thuộc HCM (`FTEL SG07`, `FPT Tân Thuận 1`…). Đúng y cảnh báo `USR-office-catalog.md §2 K6`: app đang dùng `search_alias_text` thay vì `name` ⇒ vi phạm `C-USR-05`. **Độc lập với lệch data** ⇒ kết luận được chắc chắn |
| **B6** | **Avatar chữ viết tắt sai quy tắc dẫn xuất** | 🟡 Thấp | `TC-USR-002` | KV `Đặng Châu Giang` → **`CG`** (2 từ **CUỐI**, **không dấu**) ⟷ TT **`ĐC`** (2 từ **ĐẦU**, **còn dấu**). Sai **2 điểm**. Các vế khác của TC đều ✅ |
| **B7** | **Nhãn menu thứ 3 lệch PRD** | 🟡 Thấp | `TC-USR-013` | KV `Cập nhật thông tin` ⟷ TT `Cập nhật thông tin cá nhân`. Vị trí ✅. ⚠️ App **không nhất quán với chính nó**: tiêu đề màn đích lại đúng là `Cập nhật thông tin` |
| **B8** | **Thiếu icon khiên cạnh field "Email công ty"** | 🟡 Thấp | `TC-USR-024` | KV: icon khiên **bên phải** field ⟷ TT: **không có icon nào bên phải**, chỉ có icon phong bì bên trái. 4 vế "chỉ đọc" của TC **đều ✅** |

### 3 TC FAIL là DÂY CHUYỀN — ⛔ KHÔNG mở bug riêng

| TC | FAIL vì | Bug gốc |
|---|---|---|
| `TC-USR-029` | thiếu banner **+** địa chỉ chưa bao giờ rỗng | B1 + B4 |
| `TC-USR-030` | field không rỗng *(vế **"không bị HRIS ghi đè" ĐẠT** ✅)* | B4 |
| `TC-USR-011` | **KHÔNG phải lỗi app** — xem §Phản hồi ngược | — |

## 🚫 BLOCKED TCs — ⚠️ KHÔNG automate, và KHÔNG phải lỗi app

| TC | Blocked at | Reason | Điều kiện gỡ |
|---|---|---|---|
| `TC-USR-032` `TC-USR-034` `TC-USR-035` `TC-USR-036` `TC-USR-037` | step 5 | **Master data văn phòng trên STG ≠ `DOC-v1.1-04`** (bản BA 2026-09-16, 399 VP) ⇒ oracle danh sách tên VP không tồn tại ⇒ **không phán quyết được app đúng/sai** | **Refresh `DOC-v1.1-04`** từ BA (hoặc đồng bộ data STG) → chạy lại 5 TC |
| `TC-USR-027` | step 6 | Tiền đề *"banner tồn tại"* không đạt do **B1** ⇒ không kiểm được vế "banner tự ẩn" | Sau khi dev fix **B1** |

**Bằng chứng P1 (lệch data) — 3 phép đo độc lập:**
| Phép đo | Kết quả |
|---|---|
| `Lê Thái Tổ` | → đúng **1** VP `Tòa V-City, Lê Thái Tổ` ✅ **khớp catalog** |
| `Tầng 20` | → **0 gợi ý** ⇒ VP `Tầng 20, FPT Tower` **không tồn tại trên STG** |
| `fpt` | → **9** VP, chỉ **2/8** tên khớp catalog; xuất hiện tên lạ `FPT Tower - FTEL T8`, `FTEL SG…` |
⇒ STG giữ **một bản khác** của danh mục VP: một phần trùng, một phần đã đổi tên/thay thế.

> ✅ **Quan trọng — 3 RULE cốt lõi của gợi ý VẪN ĐÚNG**, kiểm được độc lập với lệch data:
> · **ngưỡng 3 ký tự**: `fp` → 0 · `fpt` → có *(`TC-USR-031` PASS)*
> · **không phân biệt dấu + hoa/thường**: `Cẩm Lệ` · `cam le` · `CAM LE` → **tập kết quả GIỐNG HỆT**
> · **khớp chứa-chuỗi giữa từ**: `tan` khớp `Tầng 17,18 FPT Tower` (tan ⊂ tang)
> ⇒ 5 TC BLOCKED **không có nghĩa tính năng chưa được kiểm** — logic đã đúng, chỉ oracle dữ liệu sai.

## ✅ Passed TCs — sẵn sàng implement automation (19 TC)

| TC ID | Điểm kiểm | Evidence |
|---|---|---|
| TC-USR-001 | mở FoxEco từ host → đúng danh tính CBNV | `TC-USR-001__verify-danh-tinh-cbnv.png` |
| TC-USR-003 | màn Cá nhân không cho sửa trực tiếp | `TC-USR-003__verify-khong-sua-truc-tiep.png` |
| TC-USR-004 | dòng định danh đúng `[Phòng ban] · MNV: [mã]` | `TC-USR-004__verify-dong-dinh-danh.png` |
| TC-USR-007 | vắng Điểm ECO / Điểm uy tín / CO₂ | `TC-USR-007__verify-vang-diem-eco-uytin-co2.png` |
| TC-USR-008 | vắng badge "Hạng Đồng hành" | `TC-USR-008__verify-vang-badge-hang-dong-hanh.png` |
| TC-USR-009 | "Đơn của tôi" → tab "Đang diễn ra" active | `TC-USR-009__verify-man-don-cua-toi-tab-dang-dien-ra.png` |
| TC-USR-010 | "Quà đã nhận" → đúng màn | `TC-USR-010__verify-man-qua-da-nhan.png` |
| TC-USR-012 | đủ thành phần, đúng thứ tự (7/7) | `TC-USR-012__verify-thu-tu-thanh-phan.png` |
| TC-USR-014 | mở màn Cập nhật + **ẩn bottom nav** | `TC-USR-014__verify-man-cap-nhat-an-bottom-nav.png` |
| TC-USR-016 | **SĐT + địa chỉ persist đúng** sau mở lại màn | `TC-USR-016__verify-gia-tri-persist-sau-mo-lai.png` |
| TC-USR-019 | SĐT 11 số không được lưu | `TC-USR-019__verify-sdt-11-so-khong-luu.png` |
| TC-USR-025 | **P1** — đổi hồ sơ ⇏ đổi đơn đã đăng | `TC-USR-025__verify-don-giu-nguyen-sau-doi-ho-so.png` |
| TC-USR-026 | sửa trong đơn ⇏ ghi đè hồ sơ | `TC-USR-026__verify-ho-so-khong-bi-don-ghi-de.png` |
| TC-USR-031 | 2 ký tự chưa gợi ý | `TC-USR-031__verify-2-ky-tu-khong-goi-y.png` |
| TC-USR-033 | chọn gợi ý điền đúng chuỗi `name` | `TC-USR-033__verify-chon-goi-y-dien-dung-ten-vp.png` |
| TC-USR-038 | từ khoá không khớp → 0 gợi ý, 0 thông báo | `TC-USR-038__verify-tu-khoa-khong-khop.png` |
| TC-USR-042 | địa chỉ đã lưu **giữ qua vòng mở lại app**, HRIS không ghi đè | `TC-USR-042__verify-persist-sau-mo-lai-app.png` |
| TC-USR-045 | quay lại khi chưa lưu → **không hộp thoại** | `TC-USR-045__verify-quay-lai-khong-hop-thoai.png` |
| TC-USR-046 | thoát màn → bỏ thay đổi, không giữ bản nháp | `TC-USR-046__verify-bo-thay-doi-khong-giu-ban-nhap.png` |

> 🟢 **Vùng nghiệp vụ SẠCH NHẤT:** ranh giới **hồ sơ ⟷ đơn** — `TC-USR-025` (P1) + `TC-USR-026` chốt **cả 2 chiều đều đúng**; prefill chỉ là giá trị khởi tạo một chiều hồ sơ → đơn, đúng `BR15`.
> 🟢 **Persist cũng sạch:** `016` (mở lại màn) + `042` (mở lại app) + `030` vế HRIS ⇒ **FoxEco không để HRIS ghi đè hồ sơ đã lưu**.

## ⏳ NOT_RUN — 4 TC còn nợ, TẤT CẢ cùng 1 blocker

> **Blocker duy nhất: phải đăng nhập tài khoản KHÁC, mỗi lượt cần 1 mã OTP nhập tay** — AI không lấy được OTP
> (`USR-accounts.md §0`), và đổi tài khoản phải **đăng xuất khỏi app FoxPro** rồi lặp lại 3 bước vào FoxEco.

| TC | Prio | Tài khoản cần | Ghi chú riêng |
|---|---|---|---|
| `TC-USR-040` | P2 | **vai C** `FOXECO_STG_USER_C` (MNV 00041796) | 🔴 **ưu tiên cao** — xem §Dữ kiện quan trọng dưới |
| `TC-USR-043` | P2 | **vai C** *(gom cùng phiên với 040)* | 🕐 SĐT HRIS đổi 18/09, chỉ sync **sau 18/09** ⇒ chạy **từ 19/09**; lệch đúng 18/09 ⇒ BLOCKED, ⛔ không log bug |
| `TC-USR-006` | P2 | **BLANK** `FOXECO_STG_USER_BLANK1` (MNV 00157112) | chạy **trước** khi dùng tài khoản đó vào đơn nào |
| `TC-USR-005` | P2 | **A + B + C** (3 lượt login) | cần hoàn tất 1 đơn end-to-end (lấy hàng → giao → người nhận xác nhận) |

### 🔴 Dữ kiện quan trọng cho TC-USR-040/043 — phát hiện được trong phiên này

**Tài khoản A mở màn "Cập nhật thông tin" lần đầu: CẢ 2 field SĐT và Địa chỉ đều RỖNG** (`showing-hint="true"`),
**dù `USR-accounts.md §1` ghi A có đủ SĐT + địa chỉ trên HRIS** ⇒ **FoxEco KHÔNG prefill từ HRIS**.
`TC-USR-040`/`TC-USR-043` kỳ vọng vai C **được prefill từ HRIS**. Nếu C hành xử như A ⇒ **cả 2 TC sẽ FAIL và đó là bug thật**.
⇒ Khi chạy 2 TC này, **chụp ảnh ngay khi mở màn lần đầu** trước khi chạm vào field.
📎 Evidence gián tiếp: `_recon__luu-bi-chan-khi-sdt-rong-tk-a.png`

> 🙋 **Kèm theo — điểm cần QC xem lại quyết định DESCOPE:** `TC-USR-044` bị descope vì *"không tồn tại CBNV có
> HRIS trống SĐT"*. Nhưng vì app **không prefill từ HRIS**, **mọi** người dùng lần đầu đều thấy **ô SĐT rỗng** ⇒ đúng
> tình huống `TC-USR-044` mô tả (*"ô SĐT rỗng khi mở lần đầu ⇒ Lưu bị chặn"*) **có xảy ra thật**, và phiên này đã
> quan sát được trên A (Lưu bị chặn đúng). ⛔ Không tự đổi verdict (`Project_rule §10.5` FREEZE) — **báo QC quyết**.

## 📨 Phản hồi ngược → `/analyze-requirements` (2 việc, KHÔNG phải bug)

| # | Bề mặt / vấn đề | Vì sao không phải bug | Lệnh đề xuất |
|---|---|---|---|
| **R1** | **`TC-USR-011` (CARRIED v1.0) mâu thuẫn trực tiếp với `FR15` v1.1** — tiêu đề TC tự ghi *"trên app v1.0"*, `REQ-USR-005` cấm bề mặt cấu hình kênh liên hệ; nhưng v1.1 **cố ý THÊM** field "Số điện thoại mặc định" (`SC-USR-013..024`) | App làm **đúng v1.1**. TC lẽ ra phải là `DEPRECATED`/`MODIFIED` ở v1.1 chứ không `CARRIED` | `/analyze-requirements --update "SC-USR-010 (REQ-USR-005, v1.0) mâu thuẫn FR15 v1.1 — bề mặt cấu hình SĐT nay tồn tại có chủ đích"` → QC chốt `TC-USR-011` sang `DESCOPED` + `Skipped`, **giữ nguyên dòng** |
| **R2** | **2 field BẮT BUỘC của wizard "Đăng tin" chưa có trong scenario_map**: `ẢNH HÀNG *` (≥1 ảnh, Bước 1/3) và `BUỔI MONG MUỐN` (≥1 buổi, Bước 2/3) | Hành vi chặn là **đúng** (field có dấu `*`), chỉ là **chưa được phân tích** ⇒ spec-gap sẽ tồn tại mãi nếu chỉ ghi vào MEMORY | `/analyze-requirements --update "wizard Đăng tin Bước 1/3 có ẢNH HÀNG bắt buộc ≥1 ảnh; Bước 2/3 có BUỔI MONG MUỐN bắt buộc ≥1 buổi — nút Tiếp theo disable âm thầm, không thông báo"` |

> 📌 **Vì sao R2 đáng ghi:** nút `Tiếp theo` **disable mà không nói thiếu gì**, và dòng nhắc `Chọn ít nhất 1 buổi`
> chỉ hiện khi **cuộn xuống**. Đây là chi phí thật: phiên này mất ~15 phút dò 2 rào này. Mọi lượt
> `vibe-test`/`implement-automation` chạm wizard ORD sẽ trả lại đúng chi phí đó nếu không được đặc tả.

## 🗂️ Dữ liệu phát sinh trên STG — cần biết khi test module khác

| Hạng mục | Chi tiết |
|---|---|
| **2 tin NEED mới** (tài khoản A) | ghi chú `Test vibe VR-001 TC-USR-025` và `...TC-USR-026`, loại `Tài liệu`/`Thấp`/`Dưới 5 kg`/`Nhỏ`, trạng thái **`Chờ ghép`**, người nhận `stag_anhdc4@fpt.com`. ⚠️ Sẽ hiện ở **Bảng tin** + **Hoạt động** ⇒ ảnh hưởng TC đếm số đơn của `ORD`/`FEED`/`HOME` |
| **Hồ sơ tài khoản A bị đổi** | SĐT `0912345670` · Địa chỉ mặc định `363 Nguyễn Hữu Thọ, Cẩm Lệ` *(trước phiên: cả 2 **rỗng**)* |
| **Ảnh test trên emulator** | `/sdcard/Pictures/vibe_test_photo.jpg` (tự sinh, không phải ảnh thật) |
| ⚠️ **Tài khoản A KHÔNG còn trạng thái "chưa từng lưu hồ sơ"** | ⇒ ⛔ không dùng A để test prefill-HRIS lần đầu nữa; dùng **vai C** đúng như `USR-accounts.md §3` |

## Locator Coverage

| Pages visited | Elements captured | Verified ✅ | Inferred ⚠️ | Not found 🚫 |
|---|--:|--:|--:|--:|
| **9** | **77** | **45** | **26** | **6** |

→ `implement-automation` bắt đầu được với **45 locator đã MCP-verified**, đọc từ
`08_test-runs/vibe/locators/vibe-locators-latest.md` (hấp thụ **132/132 = 100%**).
🔴 **Đọc trước `§5 BẪY KỸ THUẬT`** trong file locator — có 5 bẫy sẽ làm automation sai âm thầm
(nổi bật: `selected` **không bao giờ** được expose trên tab/chip RN; `clickable` **không** phản ánh enable/disable).

## Recommendation

| Hành động | Số TC | Lệnh / việc cụ thể |
|---|--:|---|
| **Automate now** — locator ready | **19** | `/implement-automation --module USR` *(đọc `vibe-locators-latest.md`, KHÔNG cần mở Appium lại)* |
| **Log bug** — 8 defect đã nhóm | 12 TC FAIL | `/log-bug` — đề xuất **8 bug** (B1..B8), ⛔ không mở bug cho 3 TC dây chuyền (`029` `030` `011`) |
| **Chờ BA refresh data** | **5** | refresh `DOC-v1.1-04` → `/vibe-test --tc TC-USR-032,TC-USR-034,TC-USR-035,TC-USR-036,TC-USR-037` |
| **Chờ dev fix B1** | **1** | `/vibe-test --tc TC-USR-027` |
| **Route về analyze** | 1 TC + 1 spec-gap | R1 (`TC-USR-011`) · R2 (wizard 2 field bắt buộc) |
| **CHẠY TIẾP phần còn nợ** | **4** | `/vibe-test --module USR` ← bộ lọc pending tự bốc đúng 4 TC. **Cần người chạy đăng nhập + OTP** cho vai **C**, **BLANK**, **B** |

### ▶️ Thứ tự đề xuất cho phiên vibe kế tiếp (VR-002)

1. **Đăng nhập vai C** → chạy **`TC-USR-040` + `TC-USR-043`** *(043 từ 19/09)* — ⛔ **trước mọi lần bấm "Lưu thay đổi"** trên C, vì lưu 1 lần là mất trạng thái "chưa từng lưu", **không khôi phục được**.
2. **Đăng nhập BLANK** → `TC-USR-006`.
3. **`TC-USR-005`** cuối cùng (cần 3 lượt login + hoàn tất 1 đơn end-to-end).
