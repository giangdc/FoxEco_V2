# Vibe Log — VR-003 — module USR — 2026-09-18

- **Platform:** mobile (Appium MCP · UiAutomator2 · emulator-5554, 1080x2400)
- **Host app:** `com.hrisproject.stag` / `com.hrisproject.MainActivity` (FoxPro = HRIS; FoxEco mở qua **Chức năng → FoxEco**)
- **Version TC:** v1.1 (`TC-USR-027/040/043`) + v1.0 CARRIED (`TC-USR-006`)
- **Tập chạy:** pending — 4/5 TC còn nợ. `TC-USR-005` bỏ qua theo chỉ đạo QC.
- **Tài khoản:** `stag_thuyntt22@fpt.com` · MNV `00002352` · "Nguyễn Thị Thanh Thủy" · Phòng Hành chính phía Bắc
  - ⚠️ **Không có trong `04_test-data/valid/USR-accounts.md §1`** lúc bắt đầu phiên (không thuộc A/B/C/BLANK1/SPARE/RESIGNED).
  - ✅ QC GiangDC2 xác nhận 2026-09-18: tài khoản này **chưa từng lưu hồ sơ** ⇒ dùng thay vai **C** cho `TC-USR-040/043`.
  - ✅ Quan sát tại chỗ: 2 chỉ số card = **0/0** ⇒ thoả luôn precondition "tài khoản trắng" của `TC-USR-006`.
- ⛔ **Không chép SĐT thật vào log/evidence** (`Project_rule §Execution Rules`) — giá trị HRIS chỉ mô tả định tính.

---

## TC-USR-006 — Check card chỉ số hiển thị 0 với tài khoản chưa có lịch sử
**Scenario:** SC-USR-005 · **Priority:** P2 · **Nguồn:** fragment v1.0 (CARRIED)

| # | Step | Actual | Kết quả | Evidence |
|---|------|--------|---------|----------|
| 1 | Đăng nhập FoxEco bằng tài khoản "trắng" *(setup)* | Người chạy đã đăng nhập sẵn `00002352`; FoxEco mở từ FoxPro → Chức năng → FoxEco | ✅ | `screenshots/_setup__preflight-launch.png` |
| 2 | Nhấn tab "Cá nhân" ở bottom nav *(setup)* | `find_element(accessibility id "Trang chủ")` → tap → `find_element(accessibility id "Cá nhân")` → tap; mở màn "Cá nhân" | ✅ | — |
| 3 | Check card chỉ số | MCP `get_page_source`: card hiện **đủ 2 chỉ số** — TextView `0` + nhãn `đơn đã giúp`, TextView `0` + nhãn `quà đã nhận` (`profile-stat-gifts`). Card **không bị ẩn**. | ✅ | `screenshots/TC-USR-006__verify-hai-chi-so-bang-0.png` |

**Expected (step 3):** Card chỉ số vẫn hiển thị đủ 2 chỉ số, cả hai mang giá trị 0.
**Result:** ✅ PASS
**Evidence:** `screenshots/TC-USR-006__verify-hai-chi-so-bang-0.png`
**Ghi chú:** Đóng luôn **gap #2** của `USR-accounts.md §4` — trước phiên này chưa tài khoản nào được verify có 2 chỉ số = 0 (`BLANK1` mới chỉ là *ứng viên*). Tài khoản `00002352` là bằng chứng đầu tiên.

---

## TC-USR-043 — Check lần đầu mở màn cập nhật số điện thoại mặc định điền sẵn từ HRIS
**Scenario:** SC-USR-023 · **Priority:** P2 · **Nguồn:** fragment v1.1

| # | Step | Actual | Kết quả | Evidence |
|---|------|--------|---------|----------|
| 1 | Đăng nhập FoxEco bằng tài khoản C *(setup)* | Dùng `00002352` thay vai C (QC duyệt — cùng trạng thái "chưa từng lưu hồ sơ") | ✅ | — |
| 2 | Nhấn tab "Cá nhân" *(setup)* | Mở màn "Cá nhân" | ✅ | — |
| 3 | Nhấn mục menu "Cập nhật thông tin" | `find_element(accessibility id "profile-menu-editProfile")` → tap; mở màn "Cập nhật thông tin" | ✅ | `screenshots/_recon__man-cap-nhat-mo-lan-dau-tk-00002352.png` |
| 4 | Nhấn vào field "Số điện thoại mặc định" | tap `(//android.widget.EditText)[1]`; `mobile: isKeyboardShown` → **true** | ✅ | — |
| 5 | Check field "Số điện thoại mặc định" | `get_element_attribute(text)` = `09xx xxx xxx`, page source `showing-hint="true"` ⇒ field **RỖNG**, không prefill. Oracle: HRIS của chính tài khoản này **CÓ** số điện thoại (đọc tại chỗ 18/09 tại FoxPro → Cá nhân → Thông tin cá nhân → Thông tin, mục "Điện thoại", 10 số bắt đầu bằng 0 ⇒ hợp lệ `BR15-02`). | ❌ | `screenshots/TC-USR-043__step5-FAIL-sdt-khong-prefill-hris.png` |

**Expected (step 5):** Field hiển thị đúng số điện thoại của tài khoản trên HRIS và cho phép nhập.
**Actual:** Vế "cho phép nhập" ĐẠT (con trỏ + bàn phím). Vế "hiển thị đúng SĐT HRIS" **KHÔNG ĐẠT** — field rỗng hoàn toàn.
**Result:** ❌ FAIL
**Evidence:** `screenshots/TC-USR-043__step5-FAIL-sdt-khong-prefill-hris.png`
**Ghi chú:** 🕐 Bẫy thời điểm 18/09 (`USR-accounts.md §2`) **không áp dụng** — bẫy đó nói về *giá trị SĐT lệch do chưa đồng bộ*; ở đây app **không prefill gì cả**, nên không phải ca "lệch giá trị ⇒ ghi BLOCKED". ⇒ FAIL là verdict đúng, và được phép log bug.

---

## TC-USR-040 — Check lần đầu mở màn cập nhật địa chỉ mặc định điền sẵn từ HRIS
**Scenario:** SC-USR-022 · **Priority:** P2 · **Nguồn:** fragment v1.1

| # | Step | Actual | Kết quả | Evidence |
|---|------|--------|---------|----------|
| 1 | Đăng nhập FoxEco bằng tài khoản C *(setup)* | Dùng `00002352` thay vai C | ✅ | — |
| 2 | Nhấn tab "Cá nhân" *(setup)* | Mở màn "Cá nhân" | ✅ | — |
| 3 | Nhấn mục menu "Cập nhật thông tin" | Mở màn "Cập nhật thông tin" (cùng lần mở với TC-USR-043, chưa chạm field nào) | ✅ | `screenshots/_recon__man-cap-nhat-mo-lan-dau-tk-00002352.png` |
| 4 | Nhấn vào field "Địa chỉ mặc định" | tap `(//android.widget.EditText)[2]`; `mobile: isKeyboardShown` → **true** | ✅ | — |
| 5 | Check field "Địa chỉ mặc định" | `get_element_attribute(text)` = `Toà nhà, đường, quận`, page source `showing-hint="true"` ⇒ field **RỖNG**, không prefill. | ❌ | `screenshots/TC-USR-040__step5-FAIL-dia-chi-khong-prefill-hris.png` |

**Expected (step 5):** Field hiển thị đúng địa chỉ làm việc của tài khoản trên HRIS và cho phép nhập.
**Actual:** Vế "cho phép nhập" ĐẠT. Vế "hiển thị địa chỉ làm việc HRIS" **KHÔNG ĐẠT** — field rỗng hoàn toàn.
**Result:** ❌ FAIL
**Evidence:** `screenshots/TC-USR-040__step5-FAIL-dia-chi-khong-prefill-hris.png`
**Ghi chú — giới hạn oracle, đọc kỹ:** app HRIS mobile **không phơi trường "địa chỉ làm việc / văn phòng"** cho chính tài khoản này (đã kiểm 2 màn: *Thông tin cá nhân → Thông tin* chỉ có `Địa chỉ` = `Tp. Hà Nội`; *Quá trình làm việc* chỉ có đơn vị `…/Phòng Hành chính phía Bắc/`), và `00002352` không nằm trong `00_input/v1.1/datatest` ⇒ **không đọc được chuỗi VP kỳ vọng**. Verdict vẫn là FAIL vì: (a) field rỗng thì không thể bằng bất kỳ địa chỉ nào; (b) QC đã chốt HRIS **bắt buộc** trường địa chỉ làm việc khi tạo nhân viên (`USR-accounts.md §4` gap #1); (c) VR-001 đã quan sát **cùng hiện tượng rỗng** trên tài khoản A — tài khoản CÓ địa chỉ HRIS đã biết (`HCM LôB3,E-Office,KCN TânThuận`). ⇒ Defect độc lập với việc thiếu oracle của riêng tài khoản này.

---

## TC-USR-027 — Check hành vi lưu nhất quán qua 2 lần lưu liên tiếp *(Title cũ: "banner đã lưu tự ẩn…")*
**Scenario:** SC-USR-019 · **Priority:** P3 · **Nguồn:** fragment v1.1 — **bản Steps/Expected sửa 2026-09-18**

| # | Step | Actual | Kết quả | Evidence |
|---|------|--------|---------|----------|
| 1-3 | Đăng nhập → "Cá nhân" → "Cập nhật thông tin" *(setup)* | Mở màn "Cập nhật thông tin" | ✅ | — |
| 4 | Nhập `0987654321` vào field SĐT *(setup)* | `set_value` OK, field hiện `0987654321` | ✅ | `screenshots/TC-USR-027__pre-nhap-sdt-lan-1.png` |
| 5 | Nhấn "Lưu thay đổi" *(setup)* | Lưu thành công — **không banner**, app về màn "Cá nhân" | ✅ | — |
| 6 | Mở lại "Cập nhật thông tin" từ "Cá nhân" *(setup)* | Mở lại OK; `get_element_attribute(text)` field SĐT = `0987654321` ⇒ lần lưu 1 đã persist | ✅ | — |
| 7 | Nhập `0987654322` vào field SĐT | `set_value` OK, đọc lại = `0987654322` | ✅ | `screenshots/TC-USR-027__pre-nhap-sdt-lan-2.png` |
| 8 | Nhấn "Lưu thay đổi" lần 2 | tap `accessibility id "Lưu thay đổi"` | ✅ | — |
| 9 | Check màn hình ngay sau khi lưu lần 2 | `textContains("Đã lưu")` → 🚫 **NOT FOUND** (không banner); `accessibility id "profile-menu-editProfile"` → **FOUND** ⇒ đang ở màn "Cá nhân" | ✅ | `screenshots/TC-USR-027__verify-luu-lan-2-khong-banner-ve-ca-nhan.png` |

**Expected (step 9):** Giống lần lưu đầu (`TC-USR-015`): KHÔNG hiện banner nào, app tiếp tục điều hướng về màn "Cá nhân" — hành vi nhất quán giữa các lần lưu liên tiếp.
**Result:** ✅ PASS
**Evidence:** `screenshots/TC-USR-027__verify-luu-lan-2-khong-banner-ve-ca-nhan.png` (+ `__pre-nhap-sdt-lan-1.png`, `__pre-nhap-sdt-lan-2.png`)
**Ghi chú:** 🙋 Quan sát ngoài lề, **không thuộc điểm kiểm của TC**: cả 2 lần lưu đều đi qua với **field "Địa chỉ mặc định" để RỖNG** ⇒ app **không** bắt buộc địa chỉ. Đây đúng là câu hỏi đang treo cho BA ở `TC-USR-029` ("địa chỉ rỗng có hợp lệ không") — nay có dữ kiện thực nghiệm để BA chốt. ⛔ Không tự đổi verdict `TC-USR-029`.

---

## Tổng kết phiên

| | |
|---|--:|
| TC chạy trong phiên | **4** |
| ✅ PASS | 2 (`006`, `027`) |
| ❌ FAIL | 2 (`040`, `043`) — cùng 1 defect (B9) |
| ⏳ Còn nợ sau phiên | **1** (`TC-USR-005`) |
| Ảnh evidence TC | 6 file (4 TC) + 1 `_setup` + 1 `_recon` |
