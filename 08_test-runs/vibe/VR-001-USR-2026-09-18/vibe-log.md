# Vibe Test Log — VR-001 — v1.1 (+ CARRIED v1.0) — 2026-09-18

> Module: USR (Tài khoản & Hồ sơ) · Platform: mobile (Appium MCP / UiAutomator2) · Env: STG
> Host app: `com.hrisproject.stag` (FoxPro) → Chức năng → FoxEco · Device: emulator-5554 (Pixel 7, 1080x2400)
> Tài khoản: **A** — "Đặng Châu Giang" · MNV `00131946` · Ban Giám đốc
> Evidence dir: `screenshots/` · Chụp bằng `adb exec-out screencap` (xem lý do ở `mcp-session-log.md`)
> SCOPE_TOTAL = **46 TC** (38 v1.1 + 8 CARRIED v1.0) · Tập chạy phiên này: pending (run đầu tiên ⇒ toàn bộ)
> Phiên: 2026-09-18 (khởi tạo)

---

## TC-USR-001 (CARRIED v1.0, P1): Check mở FoxEco từ host app vào đúng danh tính CBNV của tài khoản SSO

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập host app FoxPro bằng SSO CBNV *(setup)* | người chạy đăng nhập + OTP trước phiên | ✅ PASS | `_setup__preflight-launch.png` | OTP nhập tay, AI không lấy được mã |
| 2 | Nhấn entry point FoxEco trong host app | `find(-android uiautomator: text("FoxEco"))` → `gesture tap` | ✅ PASS | `_recon__foxpro-chuc-nang-foxeco-entry.png` | Đường đi: FoxPro → tab "Chức năng" → icon FoxEco |
| 3 | Nhấn tab "Cá nhân" *(setup)* | `find(accessibility id: Cá nhân)` → `tap` | ✅ PASS | — | — |
| E1 | Tên, phòng ban, MNV trùng hồ sơ nhân viên | `get_text` = `Ban Giám đốc · MNV: 00131946`; tên `Đặng Châu Giang` | ✅ PASS | `TC-USR-001__verify-danh-tinh-cbnv.png` | Khớp `FOXECO_STG_USER_A` (MNV `00131946`) ở `USR-accounts.md §1` |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-001__verify-danh-tinh-cbnv.png`
**Locators captured:** 3 (`FoxEco` entry · `Cá nhân` tab · dòng định danh)

---

## TC-USR-002 (v1.1 MODIFIED, P2): Check trang "Cá nhân" hiển thị avatar chữ viết tắt, tên, phòng ban và MNV

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco bằng tài khoản A *(setup)* | phiên A đang mở | ✅ PASS | — | — |
| 2 | Nhấn tab "Cá nhân" *(setup)* | `find(accessibility id: Trang chủ)`→tap→`find(accessibility id: Cá nhân)`→tap | ✅ PASS | — | vào màn độc lập cho TC này |
| 3 | Check khối hồ sơ đầu trang | `find(-android uiautomator: text("ĐC"))` → `get_text` = **`ĐC`**; `get_text` dòng định danh = `Ban Giám đốc · MNV: 00131946`; `find(textContains "@fpt.com")` → 🚫 NOT FOUND | ❌ **FAIL** | `TC-USR-002__step3-FAIL-avatar-chu-viet-tat-sai.png` | xem phân tích dưới |

**Result: ❌ FAIL tại Step 3 (điểm kiểm avatar)**

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Avatar = chữ viết tắt **2 từ CUỐI**, **không dấu**, viết hoa | `Đặng Châu Giang` → **`CG`** | **`ĐC`** | ❌ sai **2 điểm**: lấy 2 từ **ĐẦU** (`Đặng Châu`) · **giữ dấu** (`Đ`, đúng phải là `D`/`C`) |
| Dưới avatar: tên + dòng `phòng ban · MNV` trùng hồ sơ | `Đặng Châu Giang` + `Ban Giám đốc · MNV: 00131946` | y hệt | ✅ |
| KHÔNG hiển thị SĐT / email công ty / địa chỉ mặc định | vắng cả 3 | `find(textContains "@fpt.com")` 🚫 NOT FOUND; page source màn Cá nhân không có SĐT/địa chỉ | ✅ |

**Evidence:** `screenshots/TC-USR-002__step3-FAIL-avatar-chu-viet-tat-sai.png` (+ `TC-USR-002__verify-avatar-ten-phongban-mnv.png`)
**Notes:** Đây **KHÔNG** phải ca *"demo hiện icon người"* mà fragment cảnh báo — STG **đã** render chữ viết tắt, nhưng **quy tắc dẫn xuất sai**. Ứng viên log bug (`BR15-01` / `C-USR-05(a)`). ⛔ Không sửa TC theo app (`Project_rule §10.1`).
**Locators captured:** 2 (avatar initials · dòng định danh)

---

## TC-USR-003 (v1.1 MODIFIED, P2): Check trang "Cá nhân" không cho sửa trực tiếp avatar, tên, phòng ban và MNV

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập A + tab "Cá nhân" *(setup)* | `find/tap` `Trang chủ` → `Cá nhân` | ✅ PASS | — | — |
| 3 | Nhấn vào avatar | `gesture tap (126,355)` | ✅ PASS | — | vùng avatar `[88,316][164,394]` |
| 4 | Nhấn vào tên | `gesture tap (640,328)` | ✅ PASS | — | — |
| 5 | Nhấn vào dòng phòng ban · MNV | `gesture tap (640,389)` | ✅ PASS | — | — |
| 6 | Check trạng thái sau cả 3 lần nhấn | `mobile_keyboard is_shown` = **false**; `find(class name: android.widget.EditText)` → 🚫 **NOT FOUND**; `get_text` dòng định danh = `Ban Giám đốc · MNV: 00131946` (không đổi) | ✅ PASS | `TC-USR-003__verify-khong-sua-truc-tiep.png` | — |

**Result: ✅ PASS (5 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-003__verify-khong-sua-truc-tiep.png`
**Notes:** Đây là bản **v1.1** (kỳ vọng "không sửa **trực tiếp** trên từng trường"), ⛔ KHÔNG dùng bản v1.0 cùng ID (kỳ vọng "không có bất kỳ control sửa nào" — đã bị đảo bởi `C-USR-03`).
**Locators captured:** 1 (dòng định danh) + 1 chứng cứ vắng (`EditText` 🚫)

---

## TC-USR-004 (CARRIED v1.0, P2): Check dòng định danh hiển thị phòng ban và MNV đúng định dạng

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập + tab "Cá nhân" *(setup)* | `find/tap` `Trang chủ` → `Cá nhân` | ✅ PASS | — | vào màn độc lập cho TC này |
| E1 | Dòng định danh đúng định dạng `[Phòng ban] · MNV: [mã]`, trùng hồ sơ | `get_text` = **`Ban Giám đốc · MNV: 00131946`** | ✅ PASS | `TC-USR-004__verify-dong-dinh-danh.png` | khớp định dạng + khớp MNV của A ở `USR-accounts.md §1` |

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-004__verify-dong-dinh-danh.png`
**Notes:** ⚠️ Chuỗi `(vd "Phòng Kỹ thuật · MNV: FTEL2291")` trong Expected chỉ là **ví dụ**, không phải ràng buộc định dạng mã. MNV thật trên STG là **8 chữ số** (`00131946`) — đúng như `USR-accounts.md §2` đã cảnh báo lệch với `FTEL####`. Đã chấm theo **pattern** `[Phòng ban] · MNV: [mã]` ⇒ PASS. 🙋 Nếu QC muốn siết mã về dạng `FTEL####` thì đây là điểm cần chốt lại với BA, không phải lỗi app.
**Locators captured:** 1

---

## TC-USR-007 (CARRIED v1.0, P2): Check màn "Cá nhân" không hiển thị Điểm ECO, Điểm uy tín và CO₂

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập + tab "Cá nhân" *(setup)* | `find/tap` `Trang chủ` → `Cá nhân` | ✅ PASS | — | — |
| E1 | KHÔNG có "Điểm ECO" / "Điểm uy tín" / CO₂ ở bất kỳ vị trí nào | `find(textContains "Điểm")` 🚫 NOT FOUND · `find(textContains "ECO")` 🚫 NOT FOUND · `find(textContains "uy tín")` 🚫 NOT FOUND · `find(textContains "CO")` 🚫 NOT FOUND | ✅ PASS | `TC-USR-007__verify-vang-diem-eco-uytin-co2.png` | 4 phép tìm độc lập, tất cả NOT FOUND trên cây a11y toàn màn |

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-007__verify-vang-diem-eco-uytin-co2.png`
**Notes:** Card chỉ số chỉ có **2** chỉ số (`13 đơn đã giúp` · `11 quà đã nhận`) — không có chỉ số thứ 3 nào.
**Locators captured:** 0 mới · 4 chứng cứ vắng (🚫)

---

## TC-USR-008 (v1.1 MODIFIED, P3): Check trang "Cá nhân" không hiển thị badge "Hạng Đồng hành"

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập A + tab "Cá nhân" *(setup)* | `find/tap` `Trang chủ` → `Cá nhân` | ✅ PASS | — | — |
| E1 | KHÔNG có badge "Hạng Đồng hành" hay nhãn hạng thành viên nào | `find(textContains "Hạng")` 🚫 NOT FOUND · `find(textContains "Đồng hành")` 🚫 NOT FOUND | ✅ PASS | `TC-USR-008__verify-vang-badge-hang-dong-hanh.png` | vùng dưới dòng phòng ban · MNV đi thẳng xuống card 2 chỉ số, không có dải badge |

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-008__verify-vang-badge-hang-dong-hanh.png`
**Notes:** Đây là bản **v1.1** (assert badge **VẮNG**) — ngược bản v1.0 cùng ID (assert badge **TỒN TẠI**). Kết quả xác nhận `C-USR-06` Resolved + `BR14-03`. Demo `DOC-v1.1-02` còn badge nhưng **STG thì không** ⇒ ⛔ không log bug.
**Locators captured:** 0 mới · 2 chứng cứ vắng (🚫)

---

## TC-USR-009 (CARRIED v1.0, P3): Check nhấn mục "Đơn của tôi" mở màn Hoạt động tab "Đang diễn ra"

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập + tab "Cá nhân" *(setup)* | `find/tap` `Cá nhân` | ✅ PASS | — | — |
| 3 | Nhấn mục menu "Đơn của tôi" | `find(accessibility id: profile-menu-activity)` → `tap` | ✅ PASS | — | — |
| E1 | Điều hướng sang màn Hoạt động, tab "Đang diễn ra" active | màn mở ra có tabs `Đang diễn ra` / `Đã hoàn thành`; tab **"Đang diễn ra" active** (pill trắng, chữ cam) | ✅ PASS | `TC-USR-009__verify-man-don-cua-toi-tab-dang-dien-ra.png` | xem ghi chú đối chứng dưới |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-009__verify-man-don-cua-toi-tab-dang-dien-ra.png`
**Notes:** ⚠️ Tiêu đề header màn đích là **"Đơn của tôi"**, KHÔNG phải "Hoạt động". Đã **đối chứng độc lập**: nhấn tab `Hoạt động` ở bottom nav mở ra **CÙNG một màn** (cùng tiêu đề "Đơn của tôi", cùng 2 tab, cùng danh sách) ⇒ *"màn Hoạt động"* của TC **chính là** màn này, chỉ khác nhãn tiêu đề ⇒ chấm PASS (`_recon__bottomnav-hoat-dong-tab.png`).
⚠️ Trạng thái active của tab **không đọc được qua a11y** (cả 2 tab đều `selected="false"` — React Native không expose) ⇒ phải kết luận bằng ảnh. 📌 Đây là điểm implement-automation cần biết: **không assert tab active bằng attribute `selected`**.
**Locators captured:** 3 (`profile-menu-activity` · tab `Đang diễn ra` · tab `Đã hoàn thành`)

---

## TC-USR-010 (CARRIED v1.0, P3): Check nhấn mục menu "Quà đã nhận" điều hướng sang màn "Quà đã nhận"

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập + tab "Cá nhân" *(setup)* | `find/tap` `Cá nhân` | ✅ PASS | — | — |
| 3 | Nhấn mục menu "Quà đã nhận" | `find(accessibility id: profile-menu-gifts)` → `tap` | ✅ PASS | — | — |
| E1 | Điều hướng sang màn "Quà đã nhận" | `find(text "Quà đã nhận")` OK — header màn đích = `Quà đã nhận`, có `Tổng quà đã nhận 11 món` + `LỊCH SỬ NHẬN QUÀ` | ✅ PASS | `TC-USR-010__verify-man-qua-da-nhan.png` | `11 món` khớp chỉ số `11 quà đã nhận` ở card Cá nhân |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-010__verify-man-qua-da-nhan.png`
**Locators captured:** 1 (`profile-menu-gifts`)

---

## TC-USR-011 (CARRIED v1.0, P3): Check không có bề mặt cấu hình kênh liên hệ trên app v1.0

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập + tab "Cá nhân" *(setup)* | `find/tap` `Cá nhân` | ✅ PASS | — | — |
| 3 | Check toàn màn + từng mục menu con tìm bề mặt cấu hình kênh liên hệ (SĐT, Workplace, email) | `find(accessibility id: profile-menu-editProfile)` → `tap` → `find(text "Số điện thoại mặc định")` → **TÌM THẤY** (EditText nhập được, có nút "Lưu thay đổi") | ❌ **FAIL** | `TC-USR-011__step3-FAIL-co-be-mat-cau-hinh-sdt.png` | — |

**Result: ❌ FAIL tại Step 3**

| Vế của Expected | Kỳ vọng | Actual |
|---|---|---|
| KHÔNG có mục menu / màn / control cấu hình kênh liên hệ | vắng hoàn toàn | **TỒN TẠI**: menu `Cập nhật thông tin cá nhân` → màn `Cập nhật thông tin` có field **"Số điện thoại mặc định"** (EditText, sửa + lưu được) |

**Evidence:** `screenshots/TC-USR-011__step3-FAIL-co-be-mat-cau-hinh-sdt.png` (+ `TC-USR-011__verify-man-cap-nhat-thong-tin.png`)
**🔴 Notes — FAIL này KHÔNG phải lỗi app, mà là TC CARRIED đã hết hiệu lực:** tiêu đề TC tự ghi *"trên app **v1.0**"*, `REQ-USR-005` v1.0 cấm bề mặt cấu hình kênh liên hệ. Nhưng **v1.1 `FR15` (`REQ-USR-008`, `SC-USR-013..024`) cố ý THÊM** đúng bề mặt đó — chính là cụm TC `TC-USR-014..046` của phiên này. ⇒ Hai kỳ vọng **loại trừ nhau**; TC-USR-011 lẽ ra phải là `DEPRECATED`/`MODIFIED` ở v1.1 chứ không `CARRIED`.
⛔ **KHÔNG log bug.** ⛔ Không tự sửa/xoá TC (`Project_rule §10.5` FREEZE — số lượng TC đã chốt).
▶️ **Route đúng:** `/analyze-requirements --update "SC-USR-010 (REQ-USR-005, v1.0) mâu thuẫn FR15 v1.1 — bề mặt cấu hình SĐT nay tồn tại có chủ đích"` → QC/BA chốt cho `TC-USR-011` sang `DESCOPED` + `Skipped`, **giữ nguyên dòng**.
**Locators captured:** 2 (`profile-menu-editProfile` · label `Số điện thoại mặc định`)

---

## TC-USR-012 (v1.1 MODIFIED, P3): Check trang "Cá nhân" hiển thị đủ thành phần theo đúng thứ tự

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập A + tab "Cá nhân" *(setup)* | `find/tap` `Trang chủ` → `Cá nhân` | ✅ PASS | — | — |
| E1 | Đúng thứ tự: avatar chữ viết tắt → tên → phòng ban·MNV → card 2 chỉ số → 3 mục menu; không badge hạng | thứ tự theo `bounds` từ page source (MCP): avatar `[88,316]` → tên `[242,296]` → `phòng ban·MNV [242,366]` → card 2 chỉ số `[~512,638]` → `profile-menu-activity [45,714]` → `profile-menu-gifts [45,863]` → `profile-menu-editProfile [45,1013]`; badge 🚫 NOT FOUND | ✅ PASS | `TC-USR-012__verify-thu-tu-thanh-phan.png` | 7 thành phần, thứ tự trên→dưới đúng 100% |

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-012__verify-thu-tu-thanh-phan.png`
**🙋 Notes — 1 điểm cần QC chốt:** nhãn mục menu thứ ba trên app là **"Cập nhật thông tin cá nhân"**, còn Expected của TC-USR-012 liệt kê **"Cập nhật thông tin"**. Đã chấm **PASS** vì TC-USR-012 là TC về **thành phần + THỨ TỰ** (tiêu đề + Notes của nó nói vậy), và vế nhãn verbatim do **`TC-USR-013` sở hữu** — TC đó đã ❌ FAIL đúng vào lệch này, nên defect **không bị bỏ sót**. Nếu QC muốn chấm strict-verbatim thì TC-USR-012 cũng thành FAIL **cùng 1 defect duy nhất** (không phải defect mới).
**Locators captured:** 0 mới (dùng lại 7 element từ locator_map Pha A)

---

## TC-USR-013 (v1.1 MODIFIED, P2): Check mục menu "Cập nhật thông tin" nằm ngay dưới mục "Quà đã nhận"

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập A + tab "Cá nhân" *(setup)* | `find/tap` `Trang chủ` → `Cá nhân` | ✅ PASS | — | — |
| 3 | Check nhãn và thứ tự các mục menu | `find(textStartsWith "Cập nhật thông tin")` → `get_text` = **`Cập nhật thông tin cá nhân`**; `find(text "Cập nhật thông tin")` (khớp tuyệt đối) → 🚫 **NOT FOUND** | ❌ **FAIL** | `TC-USR-013__step3-FAIL-nhan-menu-thu-ba.png` | — |

**Result: ❌ FAIL tại Step 3 (điểm kiểm nhãn)**

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Mục menu thứ **hai** có nhãn "Quà đã nhận" | `Quà đã nhận` | `Quà đã nhận` | ✅ |
| Mục menu thứ **ba** có nhãn "Cập nhật thông tin" | `Cập nhật thông tin` | **`Cập nhật thông tin cá nhân`** (thừa " cá nhân") | ❌ |
| Mục thứ ba nằm **ngay dưới** "Quà đã nhận" | liền kề | `gifts [45,863][1035,1012]` → `editProfile [45,1013][1035,1160]` — liền kề, không chen mục nào | ✅ |

**Evidence:** `screenshots/TC-USR-013__step3-FAIL-nhan-menu-thu-ba.png` (+ `TC-USR-013__verify-nhan-menu-thu-ba.png`)
**Notes:** Vị trí đúng, **chỉ lệch chuỗi nhãn**. Nhãn kỳ vọng lấy từ `DOC-v1.1-01 §8.15 Trigger`. ⚠️ Lưu ý: tiêu đề **header của màn đích** lại đúng là `Cập nhật thông tin` (xem `TC-USR-014`) ⇒ app **không nhất quán giữa nhãn menu và tiêu đề màn**. Ứng viên log bug (nhẹ, UI text). ⛔ Không sửa TC theo app (`Project_rule §10.1`).
**Locators captured:** 1 (nhãn menu thứ ba)

---

## TC-USR-014 (v1.1 NEW, P2): Check nhấn mục "Cập nhật thông tin" mở đúng màn và ẩn bottom nav

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập A + tab "Cá nhân" *(setup)* | `find/tap` `Cá nhân` | ✅ PASS | — | — |
| 3 | Nhấn mục menu "Cập nhật thông tin" | `find(accessibility id: profile-menu-editProfile)` → `tap` | ✅ PASS | — | — |
| E1 | Header có "←" + tiêu đề "Cập nhật thông tin"; màn KHÔNG có bottom nav | `find(accessibility id: Quay lại)` OK (nút ←, `[42,168][137,262]`) · `find(text "Cập nhật thông tin")` OK (`[158,185][526,246]`) · `find(accessibility id: Bảng tin)` → 🚫 **NOT FOUND** (bottom nav đã ẩn) | ✅ PASS | `TC-USR-014__verify-man-cap-nhat-an-bottom-nav.png` | — |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-014__verify-man-cap-nhat-an-bottom-nav.png`
**Notes:** Tiêu đề màn đúng verbatim `Cập nhật thông tin` (khác nhãn menu — xem `TC-USR-013`).
**Locators captured:** 3 (`Quay lại` · tiêu đề màn · chứng cứ vắng bottom nav 🚫)

---

## TC-USR-024 (v1.1 NEW, P2): Check avatar, tên, phòng ban, MNV và email trên màn cập nhật chỉ đọc

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Đăng nhập A → "Cá nhân" → "Cập nhật thông tin" *(setup)* | `find/tap` `profile-menu-editProfile` | ✅ PASS | — | — |
| 4 | Nhấn vào avatar | `gesture tap (144,512)` | ✅ PASS | — | — |
| 5 | Nhấn vào tên | `gesture tap (400,488)` | ✅ PASS | — | — |
| 6 | Nhấn vào dòng phòng ban · MNV | `gesture tap (400,546)` | ✅ PASS | — | — |
| 7 | Nhấn vào field "Email công ty" | `gesture tap (500,980)` | ✅ PASS | — | — |
| 8 | Check trạng thái 4 thành phần + icon bên phải field "Email công ty" | `mobile_keyboard is_shown` = **false**; `get_page_source` sau 4 tap **trùng khít** cây trước đó (email vẫn là `TextView` chứ không phải `EditText`, đúng 2 EditText SĐT/địa chỉ như cũ, không popup); **icon bên phải field Email: KHÔNG CÓ** | ❌ **FAIL** | `TC-USR-024__step8-FAIL-thieu-icon-khien-email.png` | — |

**Result: ❌ FAIL tại Step 8 (điểm kiểm icon khiên)**

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Không popup đổi ảnh / không field nhập / không bàn phím ở cả 4 lần nhấn | vắng cả 3 | `is_shown=false`; 0 EditText mới; 0 popup; cây a11y không đổi | ✅ |
| Avatar, tên, phòng ban·MNV, email giữ nguyên | không đổi | `ĐC` · `Đặng Châu Giang` · `Ban Giám đốc · MNV: 00131946` · `stag_GiangDC2@fpt.com` — y hệt | ✅ |
| Icon **bên phải** field "Email công ty" = **icon khiên** | icon khiên bên phải | **KHÔNG có icon nào bên phải.** Field chỉ có **icon phong bì ✉ BÊN TRÁI** | ❌ |

**Evidence:** `screenshots/TC-USR-024__step8-FAIL-thieu-icon-khien-email.png` (+ `TC-USR-024__verify-4-thanh-phan-chi-doc.png`)
**Notes:** Đúng vùng assert mà fragment đã cảnh báo *"theo rule BA chốt 2026-09-16 (ngoài PRD), demo `DOC-v1.1-02` đang lệch"* — STG **không có** icon khiên. Ứng viên log bug / hoặc điểm chốt lại với BA. ⛔ Không sửa TC theo app.
**Locators captured:** 4 (avatar · tên · dòng định danh · email value — tất cả `TextView` chỉ đọc)

---

# 🔎 Lô 2 — Validation "Số điện thoại mặc định" (TC-USR-017..023)

> **Trạng thái nền của tài khoản A khi vào lô này:** field "Số điện thoại mặc định" và "Địa chỉ mặc định"
> đều **RỖNG** (`showing-hint="true"` trên cả 2 EditText, xác nhận qua `get_page_source`) — A **chưa từng
> lưu hồ sơ FoxEco** và app **KHÔNG prefill từ HRIS**, dù `USR-accounts.md §1` ghi A có đủ SĐT + địa chỉ HRIS.
> 📌 Dữ kiện này liên quan trực tiếp tới `TC-USR-040`/`TC-USR-043` (kỳ vọng prefill HRIS trên vai C) — xem §Nợ.

> 🔴 **Phát hiện xuyên lô — app có HAI đường xử lý SĐT không hợp lệ:**
>
> | Input | Hành vi app | TC |
> |---|---|---|
> | rỗng | ✅ có thông báo lỗi đỏ (chuỗi lệch) | `017` |
> | `091234567` (9 số) · `1912345678` (không đầu 0) · `09123a5678` (có chữ) | ✅ có thông báo lỗi đỏ (chuỗi lệch) | `018` `020` `023` |
> | `0912 345 678` (khoảng trắng) · `+84912345678` (tiền tố +84) | ⛔ **CHẶN LƯU IM LẶNG — 0 thông báo** | `021` `022` |
>
> Cả 7 TC đều FAIL/PASS **không vì lý do "app cho lưu sai"** — app chặn đúng ở mọi ca. Lệch nằm ở **chuỗi thông báo** (5 TC) và **thiếu hẳn thông báo** (2 TC).

## TC-USR-017 (v1.1 NEW, P2): Check để trống số điện thoại mặc định bị chặn lưu và báo lỗi dưới field

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Đăng nhập A → "Cá nhân" → "Cập nhật thông tin" *(setup)* | `find/tap` `profile-menu-editProfile` | ✅ PASS | — | — |
| 4 | Xoá toàn bộ nội dung field "Số điện thoại mặc định" | field **đã rỗng sẵn** (`showing-hint="true"`) ⇒ điều kiện của step thoả mà không cần xoá | ✅ PASS | `TC-USR-017__pre-sdt-de-trong.png` | A chưa từng lưu hồ sơ — xem khối 🔴 trên |
| 5 | Nhấn nút "Lưu thay đổi" | `find(accessibility id: Lưu thay đổi)` → `tap` → `get_page_source` | ❌ **FAIL** | `TC-USR-017__step5-FAIL-chuoi-thong-bao-lech.png` | — |

**Result: ❌ FAIL tại Step 5 (chuỗi thông báo)**

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Chuỗi thông báo lỗi | **"Vui lòng nhập số điện thoại"** | **"Số điện thoại không được để trống"** | ❌ |
| Màu đỏ | đỏ | đỏ (`#FF4D4F`, viền field cũng đỏ) | ✅ |
| Vị trí ngay dưới field SĐT | dưới field | `[84,824][996,866]`, ngay dưới field `[193,704][950,777]` | ✅ |
| KHÔNG có banner "Đã lưu thông tin của bạn" | vắng | vắng khỏi cây a11y | ✅ |

**Evidence:** `screenshots/TC-USR-017__step5-FAIL-chuoi-thong-bao-lech.png` (+ `TC-USR-017__pre-sdt-de-trong.png`)
**Notes:** Đúng ca mà fragment dự phòng: *"Chuỗi thông báo theo demo `DOC-v1.1-02` — BA xác nhận 2026-09-17 là chuỗi chính thức; STG hiện chuỗi khác ⇒ **log bug**, ⛔ không sửa TC."* ⇒ ứng viên log bug. Hành vi chặn lưu **đúng** (`BR15-02` + `AC-30.1.02`).
**Locators captured:** 3 (`Lưu thay đổi` · EditText SĐT · TextView thông báo lỗi)

---

## TC-USR-018 (v1.1 NEW, P2): Check số điện thoại mặc định 9 chữ số bị chặn lưu

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Vào màn "Cập nhật thông tin" *(setup)* | `find/tap` `Quay lại` → `profile-menu-editProfile` | ✅ PASS | — | vào màn mới, sạch lỗi của TC trước |
| 4 | Nhập "091234567" vào field SĐT | `find(xpath //EditText[@hint="09xx xxx xxx"])` → `set_value "091234567"` | ✅ PASS | `TC-USR-018__pre-sdt-9-so.png` | — |
| 5 | Nhấn nút "Lưu thay đổi" | `tap` → `get_page_source` | ❌ **FAIL** | `TC-USR-018__step5-FAIL-chuoi-thong-bao-lech.png` | — |

**Result: ❌ FAIL tại Step 5 (chuỗi thông báo)**

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Chuỗi thông báo lỗi | **"Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)"** | **"Số điện thoại không hợp lệ"** — thiếu hẳn phần `(10 số, bắt đầu bằng 0)` | ❌ |
| Màu đỏ · ngay dưới field | đỏ, dưới field | đỏ, `[84,824][996,866]` | ✅ |
| KHÔNG có banner "Đã lưu…" | vắng | vắng | ✅ |

**Evidence:** `screenshots/TC-USR-018__step5-FAIL-chuoi-thong-bao-lech.png` (+ `TC-USR-018__pre-sdt-9-so.png`)
**Notes:** Chặn lưu **đúng** — chỉ lệch chuỗi. Cùng 1 defect với `TC-USR-020`/`TC-USR-023` (app dùng chuỗi ngắn, thiếu phần hướng dẫn định dạng trong ngoặc).
**Locators captured:** 0 mới

---

## TC-USR-019 (v1.1 NEW, P2): Check số điện thoại mặc định 11 chữ số bị chặn lưu

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Vào màn "Cập nhật thông tin" *(setup)* | `find/tap` | ✅ PASS | — | — |
| 4 | Nhập "09123456789" vào field SĐT | `set_value` → `get_text` = **`09123456789`** | ✅ PASS | `TC-USR-019__pre-sdt-11-so.png` | 📌 app **KHÔNG chặn nhập** ở ký tự thứ 11 (`max-text-length=5000`) |
| 5 | Nhấn nút "Lưu thay đổi" | `tap` | ✅ PASS | — | — |
| 6 | Nhấn nút "←" | `find/tap` `Quay lại` | ✅ PASS | — | — |
| 7 | Nhấn mục menu "Cập nhật thông tin" | `find/tap` `profile-menu-editProfile` | ✅ PASS | — | — |
| E1 | Field SĐT **không** hiển thị "09123456789" | `get_page_source`: EditText SĐT `text="09xx xxx xxx"` + `showing-hint="true"` ⇒ **RỖNG** | ✅ PASS | `TC-USR-019__verify-sdt-11-so-khong-luu.png` | chuỗi 11 số không được persist |

**Result: ✅ PASS (7 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-019__verify-sdt-11-so-khong-luu.png` (+ `TC-USR-019__pre-sdt-11-so.png`)
**Notes:** TC này cố ý **chỉ assert điểm cuối** (không persist) vì doc chưa chốt app chặn-nhập hay báo-lỗi-khi-lưu (§10.4). Quan sát thêm cho `implement-automation` + cho BA: app **cho nhập** quá 10 ký tự rồi mới chặn ở bước lưu, và ở ca 11 số này **cũng không hiện thông báo lỗi** (cùng nhóm hành vi im lặng với `021`/`022`).
**Locators captured:** 0 mới

---

## TC-USR-020 (v1.1 NEW, P2): Check số điện thoại mặc định không bắt đầu bằng 0 bị chặn lưu

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Vào màn "Cập nhật thông tin" *(setup)* | `find/tap` | ✅ PASS | — | — |
| 4 | Nhập "1912345678" vào field SĐT | `set_value` | ✅ PASS | `TC-USR-020__pre-sdt-khong-dau-0.png` | 10 số, đầu `1` | 
| 5 | Nhấn nút "Lưu thay đổi" | `tap` → `get_page_source` | ❌ **FAIL** | `TC-USR-020__step5-FAIL-chuoi-thong-bao-lech.png` | — |

**Result: ❌ FAIL tại Step 5 (chuỗi thông báo)**

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Chuỗi thông báo lỗi | **"Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)"** | **"Số điện thoại không hợp lệ"** | ❌ |
| Màu đỏ · ngay dưới field · không banner | — | đỏ, `[84,824][996,866]`, không banner | ✅ |

**Evidence:** `screenshots/TC-USR-020__step5-FAIL-chuoi-thong-bao-lech.png` (+ `TC-USR-020__pre-sdt-khong-dau-0.png`)
**Notes:** Luật `AC-30.1.02` *"10 số, đầu 0"* được **thực thi đúng** (chặn lưu). Chỉ lệch chuỗi — cùng defect với `018`/`023`.
**Locators captured:** 0 mới

---

## TC-USR-021 (v1.1 NEW, P2): Check số điện thoại mặc định chứa khoảng trắng bị chặn lưu

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Vào màn "Cập nhật thông tin" *(setup)* | `find/tap` | ✅ PASS | — | — |
| 4 | Nhập "0912 345 678" vào field SĐT | `set_value` → `get_page_source`: `text="0912 345 678"` | ✅ PASS | `TC-USR-021__pre-sdt-co-khoang-trang.png` | field **nhận** khoảng trắng |
| 5 | Nhấn nút "Lưu thay đổi" | `tap` → `get_page_source` → **0 TextView thông báo lỗi**, **0 banner**; hàng lỗi không được chèn (EditText địa chỉ vẫn ở `[182,1224]` = offset không-lỗi) | ❌ **FAIL** | `TC-USR-021__step5-FAIL-khong-hien-thong-bao-loi.png` | — |

**Result: ❌ FAIL tại Step 5 (KHÔNG hiển thị thông báo lỗi nào)**

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Hiển thị thông báo lỗi đỏ "Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)" dưới field | có thông báo | **KHÔNG có thông báo nào** — không chuỗi kỳ vọng, cũng không chuỗi thay thế | ❌ |
| KHÔNG có banner "Đã lưu thông tin của bạn" | vắng | vắng | ✅ |

**🔬 Đã xác minh 2 lượt độc lập + kiểm persist** (vì đây là kết luận nặng, không chấm bằng 1 lần bấm):
1. Lượt 1: bấm Lưu → `get_page_source` ngay lập tức → 0 thông báo, 0 banner.
2. Đóng màn, mở lại → EditText SĐT `showing-hint="true"` ⇒ **"0912 345 678" KHÔNG được lưu**.
3. Lượt 2: nhập lại + bấm Lưu → vẫn 0 thông báo (ảnh evidence chụp ở lượt này).
⇒ Kết luận: app **chặn lưu ĐÚNG**, nhưng **im lặng hoàn toàn** — người dùng bấm Lưu và không nhận được phản hồi nào.

**Evidence:** `screenshots/TC-USR-021__step5-FAIL-khong-hien-thong-bao-loi.png` (+ `TC-USR-021__pre-sdt-co-khoang-trang.png`)
**🐞 Notes — defect này NẶNG HƠN nhóm lệch-chuỗi:** `017/018/020/023` chỉ sai chữ; `021`/`022` là **mất phản hồi** (silent failure) — vi phạm `BR15-02` ở vế *"báo lỗi"* chứ không chỉ vế chuỗi. Nên tách **bug riêng, severity cao hơn**. Giả thuyết cho dev (⛔ chưa xác nhận): validator regex chỉ chạy sau một bước sanitize, input có ` ` / `+` rơi ra khỏi cả 2 nhánh.
**Locators captured:** 0 mới

---

## TC-USR-022 (v1.1 NEW, P2): Check số điện thoại mặc định có tiền tố +84 bị chặn lưu

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Vào màn "Cập nhật thông tin" *(setup)* | `find/tap` | ✅ PASS | — | — |
| 4 | Nhập "+84912345678" vào field SĐT | `set_value` → `get_page_source`: `text="+84912345678"` | ✅ PASS | `TC-USR-022__pre-sdt-tien-to-84.png` | field **nhận** dấu `+` |
| 5 | Nhấn nút "Lưu thay đổi" | `tap` → `get_page_source` → **0 thông báo lỗi**, **0 banner**; mở lại màn → field **RỖNG** ⇒ không lưu | ❌ **FAIL** | `TC-USR-022__step5-FAIL-khong-hien-thong-bao-loi.png` | — |

**Result: ❌ FAIL tại Step 5 (KHÔNG hiển thị thông báo lỗi nào)**

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Thông báo lỗi đỏ "…(10 số, bắt đầu bằng 0)" dưới field | có | **KHÔNG có thông báo nào** | ❌ |
| KHÔNG có banner "Đã lưu…" | vắng | vắng | ✅ |

**Evidence:** `screenshots/TC-USR-022__step5-FAIL-khong-hien-thong-bao-loi.png` (+ `TC-USR-022__pre-sdt-tien-to-84.png`)
**Notes:** Đã kiểm persist sau khi mở lại màn: `showing-hint="true"` ⇒ giá trị `+84…` **không được lưu** ⇒ cùng defect *silent failure* với `TC-USR-021`. Gộp chung 1 bug với `021` (2 input cùng một nhánh code).
**Locators captured:** 0 mới

---

## TC-USR-023 (v1.1 NEW, P2): Check số điện thoại mặc định chứa chữ bị chặn lưu

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Vào màn "Cập nhật thông tin" *(setup)* | `find/tap` | ✅ PASS | — | — |
| 4 | Nhập "09123a5678" vào field SĐT | `set_value` → `get_text` = **`09123a5678`** | ✅ PASS | `TC-USR-023__pre-sdt-chua-chu.png` | 📌 field `input-type=16387` (phone) nhưng **vẫn nhận chữ** qua bàn phím mềm/`set_value` |
| 5 | Nhấn nút "Lưu thay đổi" | `tap` → `get_page_source` | ❌ **FAIL** | `TC-USR-023__step5-FAIL-chuoi-thong-bao-lech.png` | — |

**Result: ❌ FAIL tại Step 5 (chuỗi thông báo)**

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Chuỗi thông báo lỗi | **"Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)"** | **"Số điện thoại không hợp lệ"** | ❌ |
| Màu đỏ · ngay dưới field · không banner | — | đỏ, `[84,824][996,866]`, không banner | ✅ |

**Evidence:** `screenshots/TC-USR-023__step5-FAIL-chuoi-thong-bao-lech.png` (+ `TC-USR-023__pre-sdt-chua-chu.png`)
**Notes:** Chặn lưu đúng. Cùng defect lệch-chuỗi với `018`/`020`.
**Locators captured:** 0 mới

---

# 🔎 Lô 3 — Gợi ý "Địa chỉ mặc định" (TC-USR-028..039) + Lưu/persist (TC-USR-015/016/042/045/046)

> 🔴 **HAI phát hiện nền, quyết định verdict của cả lô — tách rạch ròi vì hướng xử lý KHÁC nhau:**
>
> | # | Phát hiện | Bằng chứng | Bản chất | Hướng xử lý |
> |---|---|---|---|---|
> | **P1** | **Master data văn phòng trên STG ≠ `DOC-v1.1-04`** (bản BA 2026-09-16, 399 VP) | `Lê Thái Tổ` → ra đúng `Tòa V-City, Lê Thái Tổ` ✅ **nhưng** `Tầng 20` → **0 gợi ý** ⇒ VP `Tầng 20, FPT Tower` **không tồn tại**; `Cẩm Lệ` ra `FTEL Đà Nẵng Cẩm Lệ` (không có trong catalog) và **thiếu** `36 Nhơn Hòa 4, Cẩm Lệ`; `fpt` ra tên kiểu `FPT Tower - FTEL T8` thay vì `Tầng 8, FPT Tower` | **Lệch DỮ LIỆU / môi trường** — oracle không có trên STG ⇒ **không phán quyết được app đúng/sai** | 🚫 **BLOCKED** cho TC assert danh sách tên VP. Cần **refresh `DOC-v1.1-04`** (hoặc trỏ STG về đúng bộ data) rồi chạy lại 5 TC |
> | **P2** | **App tìm theo mã tỉnh, KHÔNG chỉ theo tên VP** — lệch rule `C-USR-05` | `hcm` → **12 gợi ý** toàn VP thuộc HCM (`FTEL SG07`, `FTEL SG09`, `FPT Tân Thuận 1`…) mà **không tên nào chứa chuỗi "hcm"** | **Lệch HÀNH VI app** so với rule BA đã chốt | ❌ **FAIL** `TC-USR-039` ⇒ **log bug**. Chính là ca mà `USR-office-catalog.md §2 K6` đã dự phòng: *"app hiện dòng HCM ⇒ đang tìm theo `search_alias_text` — lệch rule"* |
>
> ✅ **Tin tốt — 3 rule cốt lõi của gợi ý VẪN ĐÚNG, đã kiểm độc lập với P1:**
> · **ngưỡng 3 ký tự**: `fp` (2) → 0 gợi ý · `fpt` (3) → có gợi ý
> · **không phân biệt dấu + hoa/thường**: `Cẩm Lệ` · `cam le` · `CAM LE` → **tập kết quả GIỐNG HỆT NHAU** (2 dòng y nhau)
> · **khớp chứa-chuỗi giữa từ**: `tan` khớp cả `Tầng 17,18 FPT Tower` (tan ⊂ tang)
> ⇒ Phần logic BA đặc tả chạy đúng; chỉ **bộ dữ liệu** (P1) và **phạm vi field tìm kiếm** (P2) là lệch.

> 🔴 **Phát hiện P3 — luồng "Lưu thay đổi" KHÔNG có banner và THOÁT MÀN:** kỳ vọng
> *"banner xanh 'Đã lưu thông tin của bạn' ngay trên nút Lưu; màn **vẫn ở** Cập nhật thông tin"*.
> Thực tế: nút hiện **spinner** → app **điều hướng về màn "Cá nhân"**, **0 banner ở mọi frame**.
> Đã soi **60 frame liên tiếp** (`adb screencap` burst) qua toàn bộ chuyển cảnh ⇒ không phải
> "banner hiện rồi tắt nhanh mà chụp hụt". Dữ liệu **vẫn lưu đúng** (`TC-USR-016` PASS).
> ⇒ FAIL `TC-USR-015` · FAIL `TC-USR-029` (vế banner) · **BLOCKED `TC-USR-027`** (không có banner để kiểm "banner tự ẩn").

> 🔴 **Phát hiện P4 — text gõ tay KHÔNG bị xoá rỗng và BỊ LƯU làm địa chỉ mặc định:**
> gõ `asdfghjkl1` (không chọn gợi ý) → rời field (`focused=false`, bàn phím ẩn, thử **2 vùng trống
> khác nhau**) → field **vẫn giữ** `asdfghjkl1`; bấm Lưu → mở lại màn → **vẫn là `asdfghjkl1`**.
> ⇒ App **persist chuỗi tự do** làm "Địa chỉ mặc định", trong khi rule đòi địa chỉ phải **chọn từ
> danh sách**. FAIL `TC-USR-028` · FAIL `TC-USR-029`/`TC-USR-030` (dây chuyền: tiền đề "field về rỗng" không xảy ra).

## TC-USR-031 (v1.1 NEW, P2): Check nhập 2 ký tự chưa hiển thị gợi ý văn phòng

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Vào màn "Cập nhật thông tin", xoá field địa chỉ *(setup)* | field địa chỉ rỗng sẵn (`showing-hint="true"`) | ✅ PASS | — | — |
| 5 | Nhập "fp" vào field "Địa chỉ mặc định" | `find(xpath //EditText[@hint="Toà nhà, đường, quận"])` → `set_value "fp"` → `get_page_source` | ✅ PASS | `TC-USR-031__verify-2-ky-tu-khong-goi-y.png` | 0 node `address-suggestion-*` trong cây |

**Result: ✅ PASS (5 steps, 1 expected)** — ngưỡng 3 ký tự thực thi đúng ở biên dưới.
**Evidence:** `screenshots/TC-USR-031__verify-2-ky-tu-khong-goi-y.png`
**Locators captured:** 1 (EditText địa chỉ)

---

## TC-USR-032 (v1.1 NEW, P2): Check nhập đủ 3 ký tự hiển thị đúng danh sách gợi ý văn phòng

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Vào màn, xoá field địa chỉ *(setup)* | — | ✅ PASS | — | — |
| 5 | Nhập "fpt" vào field "Địa chỉ mặc định" | `set_value "fpt"` → `get_page_source` → **9** node `address-suggestion-0..8` | 🚫 **BLOCKED** | `TC-USR-032__step5-FAIL-danh-sach-goi-y-lech.png` | oracle không có trên STG — xem P1 |

**Result: 🚫 BLOCKED tại Step 5** — *không phán quyết được* vì oracle (8 tên VP của `DOC-v1.1-04`) không tồn tại trên STG.

| | Kỳ vọng (`DOC-v1.1-04`, 8 VP) | Actual trên STG (9 VP) |
|--:|---|---|
| 1 | Tầng 20, FPT Tower | FPT Cầu Giấy ✅ *(trùng kỳ vọng)* |
| 2 | Tầng 19, FPT Tower | FPT Tân Thuận 1 |
| 3 | Tầng 8, FPT Tower | FPT Tân Thuận 3 |
| 4 | Tầng 9, FPT Tower | FPT Tower - FTEL T8 |
| 5 | FPT Cầu Giấy | FPT Tower - FTEL T19 |
| 6 | Tầng 17,18 FPT Tower | FTEL SGDA Tân Thuận |
| 7 | Lô A4-1, KĐT Công nghệ FPT | Tầng 17,18 FPT Tower ✅ *(trùng kỳ vọng)* |
| 8 | ĐH FPT, KĐT An Phú Thịnh | FTEL Bình Định An Phú Thịnh |
| 9 | — | FTEL Đà Nẵng KĐT Công nghệ FPT |

⇒ **2/8 tên khớp**, số lượng 9 ≠ 8. Đã kiểm chứng nguyên nhân là **data**, không phải app: `Tầng 20` → **0 gợi ý** ⇒ VP đó **không có trên STG** (`_recon__probe-tang-20-khong-ton-tai.png`).
⚠️ **Quan sát chưa giải thích được, cần dev xem:** `FTEL SGDA Tân Thuận` và `FTEL Bình Định An Phú Thịnh` **không chứa chuỗi "fpt"** trong tên mà vẫn được trả về ⇒ củng cố P2 (app tìm trên field khác/rộng hơn `name`).
**Evidence:** `screenshots/TC-USR-032__step5-FAIL-danh-sach-goi-y-lech.png`
**▶️ Gỡ BLOCKED:** refresh `DOC-v1.1-04` từ BA (hoặc đồng bộ data STG) → chạy lại `/vibe-test --tc TC-USR-032,TC-USR-034,TC-USR-035,TC-USR-036,TC-USR-037`
**Locators captured:** 9 (`address-suggestion-0..8`)

---

## TC-USR-033 (v1.1 NEW, P2): Check chọn 1 văn phòng trong gợi ý điền đúng tên văn phòng vào field

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Vào màn, xoá field địa chỉ *(setup)* | — | ✅ PASS | — | — |
| 5 | Nhập "Lê Thái Tổ" | `set_value "Lê Thái Tổ"` | ✅ PASS | — | — |
| 6 | Check danh sách gợi ý | `get_page_source` → **đúng 1** gợi ý: `Tòa V-City` + `Lê Thái Tổ` (render 2 dòng, cắt ở dấu phẩy) | ✅ PASS | `TC-USR-033__pre-goi-y-toa-v-city.png` | ✅ khớp **đúng** oracle K3 của catalog |
| 7 | Chọn "Tòa V-City, Lê Thái Tổ" | `find(accessibility id: address-suggestion-0)` → `tap` | ✅ PASS | — | — |
| 8 | Nhấn vùng trống ngoài field | `gesture tap (540,300)` → `get_page_source` | ✅ PASS | `TC-USR-033__verify-chon-goi-y-dien-dung-ten-vp.png` | — |
| E1 | Field hiển thị đúng "Tòa V-City, Lê Thái Tổ", không bị xoá rỗng | EditText `text="Tòa V-City, Lê Thái Tổ"` — khớp **verbatim**; danh sách gợi ý đã đóng | ✅ PASS | *(cùng ảnh trên)* | — |

**Result: ✅ PASS (8 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-033__verify-chon-goi-y-dien-dung-ten-vp.png` (+ `TC-USR-033__pre-goi-y-toa-v-city.png`)
**Notes:** TC này **chạy được** vì VP `Tòa V-City, Lê Thái Tổ` **có thật** trên STG (khác 032/034..037). Xác nhận cơ chế: chọn gợi ý ⇒ ô được điền **chính chuỗi `name`** — đúng như BA chốt 2026-09-16.
**Locators captured:** 1 (`address-suggestion-0`)

---

## TC-USR-034 (v1.1 NEW, P2): Check gợi ý văn phòng khớp đúng khi nhập có dấu

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Vào màn, xoá field địa chỉ *(setup)* | — | ✅ PASS | — | — |
| 5 | Nhập "Cẩm Lệ" | `set_value "Cẩm Lệ"` → `get_page_source` → **2** gợi ý: `FTEL Đà Nẵng Cẩm Lệ` · `363 Nguyễn Hữu Thọ, Cẩm Lệ` | 🚫 **BLOCKED** | `TC-USR-034__step5-BLOCKED-oracle-ten-vp-lech-stg.png` | — |

**Result: 🚫 BLOCKED tại Step 5** — oracle tên VP không khớp STG (P1)

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Số lượng gợi ý | 2 | **2** | ✅ |
| `363 Nguyễn Hữu Thọ,Cẩm Lệ` | có | **có** | ✅ |
| `36 Nhơn Hòa 4, Cẩm Lệ` | có | **KHÔNG có** — thay bằng `FTEL Đà Nẵng Cẩm Lệ` (không nằm trong `DOC-v1.1-04`) | 🚫 |

**Evidence:** `screenshots/TC-USR-034__step5-BLOCKED-oracle-ten-vp-lech-stg.png`
**Notes:** Rule *"có dấu vẫn khớp"* **thoả** (gõ có dấu vẫn ra kết quả). Chỉ danh sách tên là không đối chiếu được ⇒ BLOCKED chứ không FAIL.
**Locators captured:** 2 (`address-suggestion-0`, `address-suggestion-1`)

---

## TC-USR-035 (v1.1 NEW, P2): Check gợi ý văn phòng khớp đúng khi nhập chữ thường không dấu

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Vào màn, xoá field địa chỉ *(setup)* | — | ✅ PASS | — | — |
| 5 | Nhập "cam le" | `set_value "cam le"` → `get_page_source` → **2** gợi ý, **GIỐNG HỆT** tập của `Cẩm Lệ` | 🚫 **BLOCKED** | `TC-USR-035__step5-BLOCKED-oracle-ten-vp-lech-stg.png` | — |

**Result: 🚫 BLOCKED tại Step 5** — cùng lý do P1
**✅ Điểm kiểm THỰC CHẤT của TC này vẫn kết luận được:** `cam le` (thường, không dấu) trả về **đúng cùng 2 dòng** như `Cẩm Lệ` ⇒ **rule "không phân biệt dấu + hoa/thường" ĐÚNG**. Chỉ vế *"đúng 2 văn phòng `363…` và `36 Nhơn Hòa 4…`"* là không đối chiếu được (VP thứ 2 không tồn tại trên STG).
**Evidence:** `screenshots/TC-USR-035__step5-BLOCKED-oracle-ten-vp-lech-stg.png`
**Locators captured:** 0 mới

---

## TC-USR-036 (v1.1 NEW, P2): Check gợi ý văn phòng khớp đúng khi nhập chữ hoa không dấu

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Vào màn, xoá field địa chỉ *(setup)* | — | ✅ PASS | — | — |
| 5 | Nhập "CAM LE" | `set_value "CAM LE"` → `get_page_source` → **2** gợi ý, **GIỐNG HỆT** `Cẩm Lệ` và `cam le` | 🚫 **BLOCKED** | `TC-USR-036__step5-BLOCKED-oracle-ten-vp-lech-stg.png` | — |

**Result: 🚫 BLOCKED tại Step 5** — cùng lý do P1
**✅ Điểm kiểm thực chất:** 3/3 biến thể (`Cẩm Lệ` · `cam le` · `CAM LE`) cho **tập kết quả y hệt nhau** ⇒ rule case/diacritic-insensitive **ĐÚNG**, kiểm chứng đủ trên cả 3 TC 034/035/036.
**Evidence:** `screenshots/TC-USR-036__step5-BLOCKED-oracle-ten-vp-lech-stg.png`
**Locators captured:** 0 mới

---

## TC-USR-037 (v1.1 NEW, P2): Check gợi ý văn phòng khớp theo kiểu chứa chuỗi kể cả giữa từ

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Vào màn, xoá field địa chỉ *(setup)* | — | ✅ PASS | — | — |
| 5 | Nhập "tan" | `set_value "tan"` → `get_page_source` → **11** gợi ý | 🚫 **BLOCKED** | `TC-USR-037__step5-BLOCKED-oracle-2-vp-khong-ton-tai.png` | — |

**Result: 🚫 BLOCKED tại Step 5** — **CẢ HAI** VP trong Expected đều không tồn tại trên STG

| Vế của Expected | Kỳ vọng | Actual |
|---|---|---|
| Có VP `Tầng 20, FPT Tower` | có | **VP không tồn tại trên STG** (`grep "Tầng 20"` = 0; probe riêng → 0 gợi ý) |
| Có VP `14 NVY,Phú Thọ Hòa,Tân Phú` | có | **VP không tồn tại** (`grep "NVY"` = 0) |

**✅ Điểm kiểm thực chất (rule "chứa chuỗi giữa từ") VẪN kết luận được:** gợi ý trả về có `Tầng 17,18 FPT Tower` — khớp `tan` **nằm giữa từ** (`tan` ⊂ `tang`) ⇒ **rule chứa-chuỗi ĐÚNG**, đúng như BA chốt 2026-09-16. Danh sách còn lại: `Tân Tây Đô, Đan Phượng` · `FPT Tân Thuận 1/3` · `FTEL Ninh Thuận` · `FPT Tower - FTEL T8/T19` · `FTEL Long An Tân An` · `FTEL SGDA Tân Thuận` · `FTEL Hòa Bình Tân Lạc` · `FTEL Bắc Giang Tân Yên`.
**Evidence:** `screenshots/TC-USR-037__step5-BLOCKED-oracle-2-vp-khong-ton-tai.png`
**Locators captured:** 0 mới

---

## TC-USR-038 (v1.1 NEW, P2): Check từ khoá không khớp văn phòng nào không hiển thị gợi ý

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Vào màn, xoá field địa chỉ *(setup)* | — | ✅ PASS | — | — |
| 5 | Nhập "xyz" | `set_value "xyz"` → `get_page_source` → **0** node `address-suggestion-*`, **0** dòng thông báo | ✅ PASS | `TC-USR-038__verify-tu-khoa-khong-khop.png` | — |

**Result: ✅ PASS (5 steps, 1 expected)** — không gợi ý **và** không hiện dòng thông báo nào (đúng cả 2 vế).
**Evidence:** `screenshots/TC-USR-038__verify-tu-khoa-khong-khop.png`
**Notes:** TC này **không phụ thuộc P1** (assert về sự VẮNG mặt) ⇒ kết luận được chắc chắn.
**Locators captured:** 0 mới

---

## TC-USR-039 (v1.1 NEW, P2): Check gợi ý chỉ tìm theo tên văn phòng, không theo mã tỉnh

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Vào màn, xoá field địa chỉ *(setup)* | — | ✅ PASS | — | — |
| 5 | Nhập "hcm" | `set_value "hcm"` → `get_page_source` → **12** node `address-suggestion-0..11` | ❌ **FAIL** | `TC-USR-039__step5-FAIL-tim-theo-ma-tinh.png` | — |

**Result: ❌ FAIL tại Step 5**

| Vế của Expected | Kỳ vọng | Actual |
|---|---|---|
| Không hiển thị danh sách gợi ý (vì **không tên VP nào chứa "hcm"**) | 0 gợi ý | **12 gợi ý**, tất cả là VP thuộc tỉnh **HCM**: `FTEL SG07` · `FTEL SG09` · `FTEL SG11` · `FPT Tân Thuận 1` · `FPT Tân Thuận 3` · `FTEL SG10 QL 50` · `FTEL SG01 Quận 9` · `FTEL SG02 Quận 6` · `FTEL SG02 Quận 8` · `FTEL SG04 Quận 1` · `FTEL SG08 Gò Vấp` · `FTEL SG16 Quận 7` — **không tên nào chứa chuỗi `hcm`** |

**Evidence:** `screenshots/TC-USR-039__step5-FAIL-tim-theo-ma-tinh.png`
**🐞 Notes — FAIL này ĐỘC LẬP với P1, là lệch HÀNH VI app ⇒ log bug:** không phụ thuộc VP nào tồn tại, chỉ cần *"tên không chứa `hcm` mà vẫn trả về"* là đủ kết luận. App đang tìm trên field có **mã tỉnh ở đầu** (kiểu `search_alias_text` = `hcm ftel sg07 …`) thay vì cột `name` ⇒ **vi phạm rule BA chốt 2026-09-16** (`C-USR-05`: *"gợi ý theo tên văn phòng, không theo mã tỉnh"*).
📌 Đây **đúng y** cảnh báo dự phòng ở `USR-office-catalog.md §2 K6`: *"Nếu app hiện 34 dòng HCM ⇒ app đang tìm theo `search_alias_text` — lệch rule"*. (App hiện 12, không 34 — do master data STG khác, xem P1.)
**Locators captured:** 12 (`address-suggestion-0..11`)

---

## TC-USR-015 (v1.1 NEW, **P1**): Check lưu số điện thoại và địa chỉ mặc định mới hiển thị đúng banner xanh

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Vào màn "Cập nhật thông tin" *(setup)* | `find/tap` `profile-menu-editProfile` | ✅ PASS | — | — |
| 4 | Ghi lại giá trị đang hiển thị ở 2 field | `get_page_source` → SĐT `showing-hint="true"` · địa chỉ `showing-hint="true"` ⇒ **cả 2 RỖNG** | ✅ PASS | — | không trùng test data ⇒ không cần đổi giá trị |
| 5 | Nhập "0987654321" vào field SĐT | `set_value` | ✅ PASS | `TC-USR-015__pre-sdt-va-dia-chi-da-dien.png` | — |
| 6 | Nhập "Lê Thái Tổ" vào field địa chỉ | `set_value` | ✅ PASS | *(cùng ảnh)* | — |
| 7 | Chọn "Tòa V-City, Lê Thái Tổ" trong gợi ý | `find(accessibility id: address-suggestion-0)` → `tap` | ✅ PASS | *(cùng ảnh)* | — |
| 8 | Nhấn nút "Lưu thay đổi" | `tap` → burst **60 frame** qua toàn bộ chuyển cảnh | ❌ **FAIL** | `TC-USR-015__step8-FAIL-khong-co-banner-va-thoat-man.png` | — |

**Result: ❌ FAIL tại Step 8 — sai CẢ HAI vế của Expected** *(⚠️ **verdict này ĐÃ ĐỔI → ✅ PASS ngày 2026-09-18** — xem khối đính chính ngay dưới section này)*

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Banner xanh "Đã lưu thông tin của bạn" ngay trên nút "Lưu thay đổi" | có banner | **KHÔNG có banner** ở bất kỳ frame nào trong 60 frame; `find(textContains "Đã lưu")` → 🚫 NOT FOUND | ❌ |
| Màn **vẫn ở** "Cập nhật thông tin" | ở lại | **Thoát về màn "Cá nhân"** (nút hiện spinner → điều hướng) | ❌ |
| *(ngoài Expected)* dữ liệu có được lưu? | — | ✅ **có** — xem `TC-USR-016` | — |

**Evidence:** `screenshots/TC-USR-015__step8-FAIL-khong-co-banner-va-thoat-man.png` (+ `TC-USR-015__pre-sdt-va-dia-chi-da-dien.png`, + `TC-USR-015__verify-banner-xanh-da-luu.png` — ảnh chụp ngay sau khi bấm Lưu, cho thấy màn đã là "Cá nhân" và **không có banner** ở vị trí kỳ vọng)
**🐞 Notes — TC P1, ứng viên log bug:** hành vi lưu **đúng về dữ liệu** nhưng **sai về phản hồi UI** (`AC-30.1.01` + `BR15-05`). Đã loại trừ khả năng "chụp hụt banner" bằng burst 60 frame (ảnh evidence là strip 3 frame: spinner → spinner → đã ở màn Cá nhân). Kéo theo: FAIL `TC-USR-029`, BLOCKED `TC-USR-027`.
**Locators captured:** 2 (EditText SĐT · `Lưu thay đổi`)

> 🔄 **ĐÍNH CHÍNH 2026-09-18 — `TC-USR-015`: ❌ FAIL → ✅ PASS. ⛔ KHÔNG phải bug.**
> QC GiangDC2 chốt: **hành vi app quan sát được ở phiên này là ĐÚNG** — bấm "Lưu thay đổi" với dữ liệu hợp lệ thì
> **không có banner** `Đã lưu thông tin của bạn` và app **điều hướng về màn "Cá nhân"**.
> ⇒ `Expected Result` của TC đã được sửa (fragment `TC-USR-v1.1.md` + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`;
> `Project_rule §10.5` cho phép sửa Expected/Notes — **Σ TC không đổi: 223, USR 38**).
> ⇒ **Ứng viên bug `B1` RÚT LẠI**; module USR còn **7** ứng viên bug.
>
> 📌 **Quan sát trong bảng trên KHÔNG thay đổi** (không có banner · app về màn Cá nhân · dữ liệu lưu đúng) — chỉ **kỳ vọng** thay đổi.
> Giữ nguyên cả 3 ảnh của TC (kể cả `__step8-FAIL-…` và slug `__verify-banner-xanh-da-luu` theo tên cũ) để **không tạo link chết**
> và để truy vết được lý do đổi verdict. Verdict của record nay ở `coverage/coverage-USR.md`.
>
> ⚠️ **Kéo theo, CHƯA xử lý — chờ QC quyết:** `TC-USR-027` (BLOCKED vì *"banner tự ẩn"* — tiền đề nay không còn tồn tại theo thiết kế)
> và `TC-USR-029` (FAIL vì 2 lý do, 1 trong đó là thiếu banner; lý do còn lại là bug **B4** vẫn còn hiệu lực).

---

## TC-USR-016 (v1.1 NEW, **P1**): Check giá trị số điện thoại và địa chỉ mặc định vẫn đúng sau khi mở lại màn

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-8 | Nhập SĐT + địa chỉ, chọn gợi ý, nhấn Lưu *(setup)* | như `TC-USR-015` | ✅ PASS | — | — |
| 9 | Nhấn nút "←" *(setup)* | **app tự điều hướng về "Cá nhân"** sau khi lưu ⇒ bước này đã xảy ra sẵn | ✅ PASS | — | ⚠️ lệch so với TC (xem Notes) |
| 10 | Nhấn mục menu "Cập nhật thông tin" | `find/tap` `profile-menu-editProfile` | ✅ PASS | — | — |
| E1 | SĐT = "0987654321" · địa chỉ = "Tòa V-City, Lê Thái Tổ" | `get_page_source`: EditText SĐT `text="0987654321"` · EditText địa chỉ `text="Tòa V-City, Lê Thái Tổ"` — khớp **verbatim cả 2** | ✅ PASS | `TC-USR-016__verify-gia-tri-persist-sau-mo-lai.png` | — |

**Result: ✅ PASS (10 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-016__verify-gia-tri-persist-sau-mo-lai.png`
**Notes:** ⚠️ Step 9 (*"Nhấn nút ←"*) **không thực hiện được như mô tả** vì app đã tự thoát màn sau khi lưu (defect của `TC-USR-015`) — kết quả tương đương nên **không ảnh hưởng verdict**. 📌 Đây là TC chứng minh **dữ liệu lưu ĐÚNG** dù UI không báo — tách bạch: bug của `015` là **UI feedback**, không phải mất dữ liệu.
**Locators captured:** 0 mới

---

## TC-USR-027 (v1.1 NEW, P3): Check banner đã lưu tự ẩn khi sửa tiếp nội dung field

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Vào màn "Cập nhật thông tin" *(setup)* | `find/tap` | ✅ PASS | — | — |
| 4 | Nhập "0987654321" vào field SĐT *(setup)* | `set_value` | ✅ PASS | — | — |
| 5 | Nhấn nút "Lưu thay đổi" *(setup)* | `tap` | ✅ PASS | — | — |
| 6 | Check banner phía trên nút "Lưu thay đổi" *(setup)* | `find(textContains "Đã lưu")` → 🚫 **NOT FOUND**; app đã về màn "Cá nhân" ⇒ **nút "Lưu thay đổi" không còn trên màn** | 🚫 **BLOCKED** | `TC-USR-027__step6-BLOCKED-khong-co-banner-de-kiem.png` | — |
| 7-8 | Nhập "0987654322" rồi check banner | ⏭ SKIPPED | — | — | không còn ở màn có banner để kiểm |

**Result: 🚫 BLOCKED tại Step 6**
**Reason:** Điểm kiểm của TC (*"banner **tự ẩn** khi sửa tiếp"*) **giả định banner tồn tại**. Do defect ở `TC-USR-015` (không có banner + app thoát màn), tiền đề không bao giờ đạt ⇒ **không thể phán quyết** vế "tự ẩn".
**Evidence:** `screenshots/TC-USR-027__step6-BLOCKED-khong-co-banner-de-kiem.png`
**Notes:** ⛔ **KHÔNG log bug riêng cho TC này** — nó là *hệ quả* của bug `TC-USR-015`, không phải defect độc lập. ▶️ Chạy lại `/vibe-test --tc TC-USR-027` **sau khi** dev fix banner.
**Locators captured:** 0 mới

---

## TC-USR-028 (v1.1 NEW, P2): Check địa chỉ gõ tay không chọn gợi ý bị xoá rỗng khi rời field

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Nhập "Lê Thái Tổ", chọn "Tòa V-City, Lê Thái Tổ", nhấn Lưu *(setup)* | đã thực hiện ở `TC-USR-015` ⇒ địa chỉ đã lưu | ✅ PASS | — | — |
| 5 | Nhập "asdfghjkl1" vào field "Địa chỉ mặc định" | `set_value "asdfghjkl1"` → `find(accessibility id: address-suggestion-0)` → 🚫 **NOT FOUND** | ✅ PASS | `TC-USR-028__pre-go-tay-khong-goi-y.png` | vế *"không hiện gợi ý"* ✅ |
| 6 | Nhấn vào vùng trống bên ngoài field | `gesture tap (540,300)` → kiểm `focused="false"` + `mobile_keyboard is_shown=false` ⇒ **đã rời field**; rồi `gesture tap (540,1850)` (vùng trống thứ 2) → `get_text` = **`asdfghjkl1`** | ❌ **FAIL** | `TC-USR-028__step6-FAIL-khong-xoa-rong-khi-roi-field.png` | — |

**Result: ❌ FAIL tại Step 6**

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Field "Địa chỉ mặc định" trở về **rỗng** | rỗng | **vẫn giữ `asdfghjkl1`** (`showing-hint="false"`) | ❌ |
| Trong lúc gõ ở bước 5 **không** hiện danh sách gợi ý | không gợi ý | 0 node `address-suggestion-*` | ✅ |

**🔬 Đã loại trừ khả năng "chưa thật sự rời field"** (nếu không thì đây là FAIL oan): kiểm **3 tín hiệu độc lập** — `focused="false"` trên chính EditText đó · bàn phím `is_shown=false` · thử **2 vùng trống khác nhau** (header `y=300` và vùng dưới nút Lưu `y=1850`). Cả 3 đều xác nhận đã blur mà text vẫn còn.
**Evidence:** `screenshots/TC-USR-028__step6-FAIL-khong-xoa-rong-khi-roi-field.png` (+ `TC-USR-028__pre-go-tay-khong-goi-y.png`)
**🐞 Notes — ứng viên log bug, và là gốc của P4:** rule đòi địa chỉ mặc định **phải chọn từ danh sách**; app không dọn chuỗi tự do khi rời field, **và còn lưu được nó** (xem `TC-USR-029`/`TC-USR-030`) ⇒ dữ liệu "Địa chỉ mặc định" có thể là chuỗi rác, sẽ prefill sang **địa chỉ lấy hàng** của đơn (`ORD`). Ảnh hưởng rộng hơn module USR.
**Locators captured:** 0 mới

---

## TC-USR-029 (v1.1 NEW, P2): Check để trống địa chỉ mặc định sau khi xoá vẫn lưu được

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Nhập+chọn "Tòa V-City, Lê Thái Tổ", nhấn Lưu *(setup)* | đã có từ `TC-USR-015` | ✅ PASS | — | — |
| 5 | Nhập "asdfghjkl1" vào field địa chỉ *(setup)* | `set_value` | ✅ PASS | — | — |
| 6 | Nhấn vùng trống ngoài field *(setup)* | `gesture tap (540,1850)` → field **KHÔNG về rỗng** (defect `TC-USR-028`) | ⚠️ | — | tiền đề của TC bị phá ngay ở đây |
| 7 | Nhấn nút "Lưu thay đổi" | `tap` → `find(textContains "Đã lưu")` → 🚫 **NOT FOUND**; mở lại màn → địa chỉ = **`asdfghjkl1`** | ❌ **FAIL** | `TC-USR-029__step7-FAIL-khong-co-banner-xanh.png` | — |

**Result: ❌ FAIL tại Step 7**

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Hiển thị banner xanh "Đã lưu thông tin của bạn" | có banner | **KHÔNG có** (P3) | ❌ |
| "Để trống địa chỉ mặc định vẫn lưu được" | lưu với địa chỉ **rỗng** | lưu với địa chỉ = **`asdfghjkl1`** — chuỗi rác được persist; **chưa bao giờ rỗng** (P4) | ❌ |

**Evidence:** `screenshots/TC-USR-029__step7-FAIL-khong-co-banner-xanh.png`
**Notes:** FAIL **kép, do 2 defect đã báo ở nơi khác** (`TC-USR-015` banner · `TC-USR-028` không xoá rỗng) ⇒ ⛔ **không mở bug thứ 3**. 🙋 **Điểm cần QC/BA chốt:** *"địa chỉ mặc định rỗng"* có phải trạng thái hợp lệ không, và làm sao người dùng **xoá** địa chỉ đã lưu — hiện app **không có đường** đưa field về rỗng (xoá tay rồi rời field thì giữ nguyên chuỗi; chuỗi rỗng chưa kiểm được). ▶️ Chạy lại sau khi fix `028`.
**Locators captured:** 0 mới

---

## TC-USR-030 (v1.1 NEW, P2): Check địa chỉ mặc định đã lưu rỗng vẫn rỗng sau khi mở lại, không tự load lại HRIS

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-7 | Setup như `TC-USR-029` (gõ "asdfghjkl1", rời field, nhấn Lưu) *(setup)* | — | ✅ PASS | — | — |
| 8 | Nhấn nút "←" *(setup)* | app tự về màn "Cá nhân" sau khi lưu | ✅ PASS | — | — |
| 9 | Nhấn mục menu "Cập nhật thông tin" | `find/tap` `profile-menu-editProfile` | ✅ PASS | — | — |
| 10 | Check field "Địa chỉ mặc định" | `get_page_source` → EditText `text="asdfghjkl1"`, `showing-hint="false"` | ❌ **FAIL** | `TC-USR-030__step10-FAIL-khong-rong-giu-text-go-tay.png` | — |

**Result: ❌ FAIL tại Step 10**

| Vế của Expected | Kỳ vọng | Actual | Kết quả |
|---|---|---|---|
| Field "Địa chỉ mặc định" **rỗng** | rỗng | **`asdfghjkl1`** — chuỗi gõ tay đã được lưu và load lại | ❌ |
| **Không** tự điền lại địa chỉ làm việc từ HRIS | không có HRIS | ✅ **đúng** — `grep "LôB3"`/`"TânThuận"` trong cây a11y = **0** ⇒ HRIS **không** ghi đè | ✅ |

**Evidence:** `screenshots/TC-USR-030__step10-FAIL-khong-rong-giu-text-go-tay.png`
**Notes:** Vế **quan trọng nhất về nghiệp vụ** của TC này — *"không bị HRIS ghi đè"* — **ĐẠT**. FAIL chỉ ở vế "rỗng", và là **hệ quả trực tiếp** của defect `TC-USR-028` ⇒ ⛔ không mở bug riêng. Sau khi fix `028` thì TC này cần chạy lại.
**Locators captured:** 0 mới

---

## TC-USR-042 (v1.1 NEW, P2): Check địa chỉ mặc định đã lưu được giữ sau khi mở lại FoxEco, không bị HRIS ghi đè

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-6 | Nhập "Lê Thái Tổ", chọn "Tòa V-City, Lê Thái Tổ", nhấn Lưu *(setup)* | `set_value` → `tap address-suggestion-0` → `tap Lưu thay đổi` | ✅ PASS | — | HRIS của A là `LôB3,E-Office,KCN TânThuận` ⇒ điều kiện "HRIS ≠ giá trị đã lưu" **thoả** |
| 7 | Nhấn back thiết bị tới khi về màn chính host app FoxPro | `gesture back` ×2 → `find(text "FoxEco")` OK ⇒ đã ở màn "Chức năng" của FoxPro | ✅ PASS | — | — |
| 8 | Mở lại FoxEco từ host app | `find(-android uiautomator: text("FoxEco"))` → `tap` | ✅ PASS | — | — |
| 9 | Nhấn tab "Cá nhân" | `find/tap` `Cá nhân` | ✅ PASS | — | — |
| 10 | Nhấn mục menu "Cập nhật thông tin" | `find/tap` `profile-menu-editProfile` | ✅ PASS | — | — |
| E1 | Field địa chỉ = "Tòa V-City, Lê Thái Tổ", không hiển thị địa chỉ HRIS | EditText `text="Tòa V-City, Lê Thái Tổ"` ✅ · `grep "LôB3"`/`"TânThuận"` = **0** ✅ | ✅ PASS | `TC-USR-042__verify-persist-sau-mo-lai-app.png` | — |

**Result: ✅ PASS (10 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-042__verify-persist-sau-mo-lai-app.png`
**Notes:** Đây là TC mạnh nhất chứng minh **FoxEco không để HRIS ghi đè hồ sơ đã lưu** — qua hẳn 1 vòng thoát app + mở lại từ host. SĐT `0987654321` cũng được giữ (HRIS của A là số khác).
**Locators captured:** 0 mới (dùng lại toàn bộ từ locator_map)

---

## TC-USR-045 (v1.1 NEW, P3): Check nhấn quay lại khi chưa lưu không hiển thị hộp thoại xác nhận

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Vào màn "Cập nhật thông tin" *(setup)* | `find/tap` | ✅ PASS | — | — |
| 4 | Ghi lại giá trị đang hiển thị ở 2 field | SĐT = `0987654321` · địa chỉ = `asdfghjkl1` | ✅ PASS | `TC-USR-045__pre-gia-tri-goc-truoc-khi-sua.png` | — |
| 5 | Nhập "0987654321" vào field SĐT | giá trị hiện tại đã là `0987654321` ⇒ giữ nguyên | ✅ PASS | — | — |
| 6 | Nhập "Cẩm Lệ" vào field địa chỉ | `set_value "Cẩm Lệ"` → 2 gợi ý | ✅ PASS | — | — |
| 7 | Chọn "36 Nhơn Hòa 4, Cẩm Lệ" trong gợi ý | ⚠️ **VP này không tồn tại trên STG** (P1) ⇒ **thay bằng** `363 Nguyễn Hữu Thọ, Cẩm Lệ` (`address-suggestion-1`, cùng từ khoá K4) | ✅ PASS | — | xem Notes — thay data, **không** đổi điểm kiểm |
| 8 | Nhấn nút "←" | `find/tap` `Quay lại` → `get_page_source` | ✅ PASS | `TC-USR-045__verify-quay-lai-khong-hop-thoai.png` | — |
| E1 | Quay về trang "Cá nhân" ngay, không hộp thoại xác nhận nào | màn hiện tại = **"Cá nhân"** (có `ĐC`, tên, `MNV: 00131946`, card 2 chỉ số); quét cây a11y tìm `alert\|dialog\|Xác nhận\|Huỷ\|Hủy\|Bỏ` = **0 khớp** | ✅ PASS | *(cùng ảnh)* | — |

**Result: ✅ PASS (8 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-045__verify-quay-lai-khong-hop-thoai.png` (+ `TC-USR-045__pre-gia-tri-goc-truoc-khi-sua.png`)
**🙋 Notes — đã THAY test data ở step 7, khai rõ để QC duyệt:** VP `36 Nhơn Hòa 4, Cẩm Lệ` trong Test Data **không có trên STG** (P1). Đã chọn VP còn lại của **cùng từ khoá K4** (`363 Nguyễn Hữu Thọ, Cẩm Lệ`). Điểm kiểm của TC là *"không có hộp thoại xác nhận khi quay lại"* — **không phụ thuộc chọn VP nào** ⇒ verdict vẫn giá trị. Tiền lệ cho phép thay data: `USR-office-catalog.md` / fragment `TC-USR-015` Notes (*"đổi sang SĐT/văn phòng khác trong catalog"*).
**Locators captured:** 0 mới

---

## TC-USR-046 (v1.1 NEW, P3): Check thoát màn khi chưa lưu bỏ thay đổi không giữ bản nháp

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | Vào màn, ghi lại giá trị gốc *(setup)* | SĐT = `0987654321` · địa chỉ = `asdfghjkl1` | ✅ PASS | — | — |
| 5-7 | Nhập SĐT + "Cẩm Lệ", chọn gợi ý *(setup)* | chọn `363 Nguyễn Hữu Thọ, Cẩm Lệ` (thay VP không tồn tại — như `TC-USR-045`) | ✅ PASS | — | — |
| 8 | Nhấn nút "←" *(setup)* | `find/tap` `Quay lại` → về màn "Cá nhân" | ✅ PASS | — | — |
| 9 | Nhấn mục menu "Cập nhật thông tin" | `find/tap` `profile-menu-editProfile` | ✅ PASS | — | — |
| 10 | Check 2 field | `get_page_source`: SĐT `text="0987654321"` · địa chỉ `text="asdfghjkl1"` ⇒ **trùng đúng giá trị ghi ở bước 4** | ✅ PASS | `TC-USR-046__verify-bo-thay-doi-khong-giu-ban-nhap.png` | — |

**Result: ✅ PASS (10 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-046__verify-bo-thay-doi-khong-giu-ban-nhap.png`
**Notes:** Lựa chọn `363 Nguyễn Hữu Thọ, Cẩm Lệ` **chưa lưu** đã bị **bỏ hoàn toàn** — không giữ bản nháp. ⚠️ Nghịch lý đáng chú ý cho BA: app **bỏ đúng** thay đổi chưa lưu (TC này PASS) nhưng lại **lưu được chuỗi rác** khi bấm Lưu (`TC-USR-028`/`029`) ⇒ vấn đề nằm ở **validate lúc lưu**, không ở quản lý bản nháp. Thay data như `TC-USR-045`, không ảnh hưởng điểm kiểm.
**Locators captured:** 0 mới

---

# 🔎 Lô 4 — Ranh giới HỒ SƠ ⟷ ĐƠN (TC-USR-025/026) · chạy qua wizard "Đăng tin"

> 🟢 **Hai TC này cần dựng đơn thật qua wizard ORD.** Đã dựng **2 đơn NEED** trên STG bằng tài khoản A
> (người nhận `stag_anhdc4@fpt.com` = vai B theo `USR-accounts.md §3b`), loại hàng `Tài liệu` ·
> giá trị `Thấp` · `Dưới 5 kg` · `Nhỏ` · ghi chú `Test vibe VR-001 TC-USR-025` / `...-026`.
> ⚠️ **Dữ liệu phát sinh trên STG:** 2 tin NEED trạng thái `Chờ ghép` — khai ở §Dữ liệu phát sinh của report.
>
> 📌 **2 rào bắt buộc của wizard mà `analyze`/`generate-tc` CHƯA mô tả** (phát hiện khi chạy, đã làm mất
> ~15 phút dò): nút `Tiếp theo` **disable âm thầm**, không có thông báo chỉ ra thiếu gì.
> | Bước | Field bắt buộc chưa khai trong scenario_map | Dấu hiệu |
> |---|---|---|
> | Bước 1/3 | **`ẢNH HÀNG *` — bắt buộc ≥1 ảnh** (`multi-photo-add-button`, "Bắt buộc ít nhất 1 ảnh · tối đa 5 ảnh") | `Tiếp theo` `clickable=false`, **0 thông báo** |
> | Bước 2/3 | **`BUỔI MONG MUỐN` — chọn ít nhất 1 buổi** (`day-part-morning/afternoon/after_work/anytime`) | dòng nhắc `Chọn ít nhất 1 buổi` chỉ hiện khi **cuộn xuống** |
> ⇒ ⚠️ **Đây là bề mặt CHƯA có trong scenario_map** ⇒ route `/analyze-requirements --update` (xem §Phản hồi ngược của report). ⛔ KHÔNG log bug — hành vi chặn là **đúng** (field có dấu `*`), chỉ là chưa được phân tích/đặc tả.
> 🖼️ Ảnh test đẩy vào emulator bằng `adb push /sdcard/Pictures/vibe_test_photo.jpg` (ảnh tự sinh, không phải ảnh thật).

## TC-USR-025 (v1.1 NEW, **P1**): Check đổi số điện thoại và địa chỉ mặc định không làm đổi đơn đã đăng trước đó

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập A *(setup)* | phiên A đang mở | ✅ PASS | — | — |
| 2 | Đăng 1 tin NEED, khai B là người nhận, **giữ nguyên** SĐT người gửi + địa chỉ lấy hàng điền sẵn *(setup)* | wizard 3 bước; Bước 2/3 **prefill sẵn** `0987654321` + `Tòa V-City, Lê Thái Tổ` từ hồ sơ ⇒ **không sửa**; email người nhận `stag_anhdc4@fpt.com` → app **autofill** tên + SĐT người nhận từ HRIS | ✅ PASS | `TC-USR-025__pre-wizard-prefill-nguoi-gui.png` · `TC-USR-025__pre-tom-tat-don-truoc-khi-dang.png` | `Đăng tin thành công!` |
| 3 | Mở màn Theo dõi đơn của tin vừa đăng *(setup)* | nhấn `Theo dõi đơn` trên popup thành công | ✅ PASS | — | — |
| 4 | Ghi lại SĐT người gửi + địa chỉ lấy hàng trên màn Theo dõi đơn | `Lấy hàng` = **`Tòa V-City, Lê Thái Tổ`**. ⚠️ **SĐT người gửi KHÔNG hiển thị** trên màn Theo dõi đơn (view của chủ đơn) ⇒ đọc qua `Chỉnh sửa` → Bước 2/3: **`0987654321`** | ✅ PASS | `TC-USR-025__pre-theo-doi-don-dia-chi-lay-hang.png` | xem Notes |
| 5-6 | Nhấn tab "Cá nhân" → "Cập nhật thông tin" *(setup)* | `find/tap` | ✅ PASS | — | — |
| 7 | Nhập "0987654321" vào field SĐT mặc định | ⚠️ **đổi sang `0912345670`** — xem Notes (giá trị TC trùng giá trị đang có ⇒ phép thử vô nghĩa) | ✅ PASS | — | — |
| 8 | Nhập "Cẩm Lệ" vào field Địa chỉ mặc định | `set_value "Cẩm Lệ"` → 2 gợi ý | ✅ PASS | — | — |
| 9 | Chọn "363 Nguyễn Hữu Thọ,Cẩm Lệ" trong gợi ý | `find(accessibility id: address-suggestion-1)` → `tap` | ✅ PASS | — | VP này **có thật** trên STG ✅ |
| 10 | Nhấn nút "Lưu thay đổi" | `tap` → hồ sơ mới = `0912345670` + `363 Nguyễn Hữu Thọ, Cẩm Lệ` | ✅ PASS | — | — |
| 11-12 | Tab "Hoạt động" → nhấn card đơn đã đăng ở bước 2 *(setup)* | `find(descriptionStartsWith "Gửi: Tài liệu")` → `tap` | ✅ PASS | — | card desc vẫn `Từ: Tòa V-…` |
| E1 | SĐT người gửi + địa chỉ lấy hàng **trùng đúng** giá trị ghi ở bước 4 | `Lấy hàng` = **`Tòa V-City, Lê Thái Tổ`** ✅ · `Chỉnh sửa` Bước 2/3 = **`0987654321`** + **`Tòa V-City, Lê Thái Tổ`** ✅ · quét cây a11y tìm `Nguyễn Hữu Thọ`/`Cẩm Lệ` = **0 khớp** ⇒ giá trị hồ sơ mới **không rò** vào đơn | ✅ PASS | `TC-USR-025__verify-don-giu-nguyen-sau-doi-ho-so.png` | — |

**Result: ✅ PASS (13 steps, 1 expected)** — TC **P1**, ranh giới hồ sơ ⟷ đơn **ĐÚNG**.
**Evidence:** `screenshots/TC-USR-025__verify-don-giu-nguyen-sau-doi-ho-so.png` (+ `TC-USR-025__pre-wizard-prefill-nguoi-gui.png`, `TC-USR-025__pre-tom-tat-don-truoc-khi-dang.png`, `TC-USR-025__pre-theo-doi-don-dia-chi-lay-hang.png`)

**🙋 Notes — 2 điều chỉnh đã khai rõ để QC duyệt:**
1. **Step 7 đổi giá trị:** TC ghi nhập `0987654321`, nhưng hồ sơ A **đang chính là** `0987654321` (do `TC-USR-015` lưu) ⇒ nhập lại số cũ thì *"đổi SĐT"* không xảy ra và TC **không chứng minh được gì**. Đã dùng **`0912345670`** để tạo thay đổi thật. Điểm kiểm (*đơn giữ nguyên giá trị cũ*) **không đổi**.
2. **Step 4 — SĐT người gửi không có trên màn Theo dõi đơn:** view chủ đơn chỉ hiện `Lấy hàng`, ảnh, thông tin hàng, `LỊCH SỬ`, nút `Chỉnh sửa`/`Huỷ đơn`. Đã đọc SĐT qua `Chỉnh sửa` → Bước 2/3 (dùng **cùng một đường đọc** ở bước 4 và bước 13 ⇒ so sánh vẫn công bằng). 📌 Đáng chú ý: `Chỉnh sửa` hiện **giá trị của ĐƠN** (`0987654321`), **không** re-prefill từ hồ sơ hiện tại (`0912345670`) — đây chính là hành vi đúng mà TC cần, và là bằng chứng mạnh nhất của TC này.
3. ⛔ Đã **`Huỷ chỉnh sửa`** để thoát, **không lưu** ⇒ đơn giữ nguyên trạng cho ai muốn đối chiếu lại.
**Locators captured:** 18 (wizard 3 bước + màn Theo dõi đơn — xem `vibe-locators.md`)

---

## TC-USR-026 (v1.1 NEW, P2): Check sửa số điện thoại người gửi và địa chỉ lấy hàng trong đơn không ghi đè hồ sơ

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Đăng nhập A → "Cá nhân" → "Cập nhật thông tin" *(setup)* | `find/tap` | ✅ PASS | — | — |
| 4 | Ghi lại giá trị 2 field hồ sơ | SĐT = **`0912345670`** · địa chỉ = **`363 Nguyễn Hữu Thọ, Cẩm Lệ`** | ✅ PASS | `TC-USR-026__pre-ho-so-truoc-khi-dang-don.png` | giá trị do `TC-USR-025` để lại |
| 5 | Mở wizard "Đăng tin" NEED, khai B là người nhận, tới bước có SĐT người gửi + địa chỉ lấy hàng *(setup)* | Bước 2/3 **prefill** đúng `0912345670` + `363 Nguyễn Hữu Thọ, Cẩm Lệ` ⇒ xác nhận prefill **bám hồ sơ hiện tại** | ✅ PASS | — | — |
| 6 | Nhập "0987654321" vào field SĐT người gửi | `set_value` (khác hồ sơ ✅) | ✅ PASS | `TC-USR-026__pre-don-2-nguoi-gui-khac-ho-so.png` | — |
| 7 | Nhập "Tòa V-City, Lê Thái Tổ" vào field địa chỉ lấy hàng | `set_value "Lê Thái Tổ"` → `tap address-suggestion-0` (khác hồ sơ ✅) | ✅ PASS | *(cùng ảnh)* | — |
| 8 | Hoàn tất wizard và nhấn đăng tin *(setup)* | ảnh hàng + buổi `Giờ nào cũng được` + tick điều khoản → `Đăng tin ngay` → `Đăng tin thành công!` | ✅ PASS | — | Bước 3/3 tóm tắt ghi `Đặng Châu Giang · 0987654321` + `Tòa V-City, Lê Thái Tổ` |
| 9-10 | Tab "Cá nhân" → "Cập nhật thông tin" | `find/tap` | ✅ PASS | — | — |
| E1 | 2 field hồ sơ **trùng đúng** giá trị bước 4; **không** hiển thị "0987654321" hay "Tòa V-City, Lê Thái Tổ" | SĐT = **`0912345670`** ✅ · địa chỉ = **`363 Nguyễn Hữu Thọ, Cẩm Lệ`** ✅ · quét cây a11y tìm `0987654321`/`V-City` = **0 khớp** ✅ | ✅ PASS | `TC-USR-026__verify-ho-so-khong-bi-don-ghi-de.png` | — |

**Result: ✅ PASS (10 steps, 1 expected)**
**Evidence:** `screenshots/TC-USR-026__verify-ho-so-khong-bi-don-ghi-de.png` (+ `TC-USR-026__pre-ho-so-truoc-khi-dang-don.png`, `TC-USR-026__pre-don-2-nguoi-gui-khac-ho-so.png`)
**Notes:** Cùng với `TC-USR-025`, hai TC này chốt **ranh giới 2 chiều** và **cả 2 chiều đều ĐÚNG**:
· hồ sơ đổi ⇏ đơn cũ đổi (`TC-USR-025`)
· đơn nhập khác ⇏ hồ sơ bị ghi đè (`TC-USR-026`)
Prefill chỉ là **giá trị khởi tạo một chiều** hồ sơ → đơn, đúng `BR15`. 📌 Đây là vùng nghiệp vụ **sạch nhất** của module USR trong phiên này.
**Locators captured:** 0 mới (dùng lại locator wizard từ `TC-USR-025`)

---
