# Vibe Test Log — VR-017 — module ACT — v1.1 — 2026-09-21

> Module: **ACT — Hoạt động (Đơn của tôi)** · Platform: **mobile** (Appium MCP / UiAutomator2) · Device `emulator-5554` · Env: STG · host app `com.hrisproject.stag` (FoxPro) → FoxEco
> Evidence dir: `screenshots/`
> Phiên: 2026-09-21 (khởi tạo) · 2026-09-21 (chấm lại `TC-ACT-015` + `TC-ACT-017` theo Expected mới — QC chốt không phải bug)
> Tập chạy: **chỉ 10 TC v1.1** (`001 005 008 012 013 014 015 016 017 018`) theo yêu cầu QC — ⛔ không gồm 8 TC CARRIED v1.0 (`002 003 004 006 007 009 010 011`).
> Nguồn kết quả: tất cả TC chạy mới trong run này (ACT chưa có run nào trước).
> 🔒 **Chế độ chỉ đọc:** QC chưa cấp quyền đổi trạng thái đơn trên STG ⇒ không nhận đơn / lấy hàng / hoàn hàng / huỷ đơn. Mọi TC chỉ quan sát dữ liệu có sẵn.
> Cách chụp ảnh: `adb exec-out screencap -p` ghi thẳng vào `screenshots/` (cùng cách VR-015); `appium_screenshot` chỉ dùng 1 lần cho ảnh element (`TC-ACT-008__verify-*`).

---

## Lô 1 — tài khoản A = `stag_anhdc4@fpt.com` (Đặng Châu Anh)

> Lý do dùng `anhdc4` làm tài khoản A thay `giangdc2`: máy ảo đang đăng nhập sẵn `anhdc4`, và tab `Đã hoàn thành` của tài khoản này có đủ đơn `Hoàn thành` + `Hết hạn` + 1 đơn `Đã huỷ` ⇒ khớp phần lớn `SEED-ACT-03`. Không có đơn đã trả lại người gửi (`RETURNED`).
> Toàn bộ tab `Đã hoàn thành` đã được rà **từ đầu tới cuối** qua `appium_get_page_source` (14 khung cuộn, chồng lấn) — kết quả rà dùng chung cho `005` · `008` · `013` · `015`.

## TC-ACT-001: Check màn Hoạt động dùng đúng bộ nhãn của app cho tên màn và hai tab

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco từ FoxPro (setup) | FoxPro `Chức năng` → `scroll_to_element textContains("FoxEco")` → tap | ✅ | — | tài khoản đang đăng nhập sẵn: Đặng Châu Anh |
| 2 | Nhấn tab "Hoạt động" (setup) | find `text("Hoạt động")` → tap | ✅ | — | — |
| 3 | Check nhãn bottom nav, tiêu đề màn, hàng tab con | `appium_get_page_source` | ✅ PASS | `TC-ACT-001__verify-nhan-hoat-dong-don-cua-toi-2-tab.png` | page source: `Đơn của tôi` · `Đang diễn ra` · `Đã hoàn thành` · nav `Hoạt động` — đúng 2 tab con, không có tab thứ 3 |

**Result: ✅ PASS**
**Evidence:** `screenshots/TC-ACT-001__verify-nhan-hoat-dong-don-cua-toi-2-tab.png` — verified tồn tại

---

## TC-ACT-005: Check tab Đã hoàn thành chứa đủ cả ba loại đơn kết thúc

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco, nhấn tab "Hoạt động" (setup) | như TC-ACT-001 | ✅ | — | — |
| 2 | Nhấn tab con "Đã hoàn thành" (setup) | find `text("Đã hoàn thành")` → tap | ✅ | — | — |
| 3 | Check badge trạng thái của từng card | rà toàn bộ danh sách qua page source | 🚫 BLOCKED | `TC-ACT-005__step3-BLOCKED-chi-co-hoan-thanh-va-het-han-khong-co-don-tra-lai.png` | Badge thấy được: chỉ `Hoàn thành` và `Hết hạn`. **Không có card nào của đơn đã trả lại người gửi** ⇒ thiếu tiền đề `SEED-ACT-03` (đơn `RETURNED` phải dựng qua `TC-DLV-063`, cần đổi trạng thái đơn — chưa được phép). |

**Result: 🚫 BLOCKED at Step 3**
**Reason:** thiếu đơn `RETURNED`. Hai vế còn lại quan sát được đều đúng: có card `Hoàn thành` + `Hết hạn`; **không** có card nào mang badge `Chờ ghép` / `Đã ghép` / `Đang giao` / `Đã giao`. Theo Notes của TC: *"Lô DLV chưa đẩy được đơn tới RETURNED ⇒ ghi Blocked phần đó, ⛔ không PASS cả TC"*.
**Evidence:** `screenshots/TC-ACT-005__step3-BLOCKED-chi-co-hoan-thanh-va-het-han-khong-co-don-tra-lai.png` — verified tồn tại

---

## TC-ACT-008: Check card đơn Hết hạn hiện badge và đúng chuỗi lý do chính thức

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập, tab "Hoạt động" → "Đã hoàn thành" (setup) | như trên | ✅ | — | — |
| 2 | Check badge và dòng lý do trên card "Hết hạn" | find `textStartsWith("Không có ai nhận mang giúp")` → `appium_get_text` | ❌ FAIL | `TC-ACT-008__step2-FAIL-ly-do-het-han-ban-dai-tin-da-tu-dong-dong.png` | badge `Hết hạn` ✅. Chuỗi lý do MCP trả về: **`Không có ai nhận mang giúp trong thời gian đăng — tin đã tự động đóng.`** |

**Result: ❌ FAIL at Step 2**
**Expected:** `Không có ai nhận mang giúp trong thời gian đăng` (bản ngắn — `DOC-v1.1-01 §8.5.1 BR05-03` + `AC-09.1.01`)
**Actual:** `Không có ai nhận mang giúp trong thời gian đăng — tin đã tự động đóng.` (bản dài của `KB-ORD-07`, đúng bản v1.0 đang assert). Mọi card `Hết hạn` trong danh sách (≈30 card) đều dùng bản dài.
**Theo Notes TC:** *"App hiện bản dài ⇒ FAIL và log bug, ⛔ không hạ Expected về bản v1.0"*.
**Bug:** 🐞 `BUG-030` (draft, chờ QC review — chưa push Jira) ⚠️ Nên hỏi lại BA trước khi log: có thể PRD v1.1 chỉ rút gọn cách viết chứ không định đổi chuỗi.
**Evidence:** `screenshots/TC-ACT-008__step2-FAIL-ly-do-het-han-ban-dai-tin-da-tu-dong-dong.png` (+ `screenshots/TC-ACT-008__verify-chuoi-ly-do-het-han-mcp-element.png` — ảnh element do `appium_screenshot` chụp) — verified tồn tại

---

## TC-ACT-013: Check card đơn Hoàn thành không còn dấu vết sao điểm tier hay chỉ số môi trường

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập, tab "Hoạt động" → "Đã hoàn thành" (setup) | như trên | ✅ | — | — |
| 2 | Check toàn bộ nội dung trên từng card | page source 14 khung cuộn, đầu → cuối danh sách | ✅ PASS | `TC-ACT-013__verify-card-hoan-thanh-cuoi-danh-sach-khong-sao-diem-tier.png` | ~17 card `Hoàn thành` (21/9, 9/8, 8/8, 4/8/2026). Text trên card chỉ gồm: loại hàng · tuyến · ngày · badge · `Đã tặng quà` / `Chạm để tặng quà`. **Không** có chuỗi ★, điểm số, nhãn tier hay chỉ số môi trường (CO₂/kg…) |

**Result: ✅ PASS**
**Evidence:** `screenshots/TC-ACT-013__verify-card-hoan-thanh-cuoi-danh-sach-khong-sao-diem-tier.png` — verified tồn tại
**Ghi chú:** ⚠️ Rà bằng **text** trong page source + ảnh chụp. Nếu ★ được vẽ bằng icon không có text thì chỉ bắt được qua ảnh — trên các khung đã chụp không thấy ★.

---

## TC-ACT-015: Check đơn đã trả người gửi hiện kèm lý do còn đơn đã huỷ vẫn bị ẩn

> 🔄 **Chấm lại 2026-09-21 (cùng phiên) theo Expected mới.** Lượt đầu ghi ❌ FAIL (đơn "Đã huỷ" hiện ở tab "Đang diễn ra" — trái `C-ACT-04(b)`). QC GiangDC2 chốt: **đây KHÔNG phải bug** ⇒ Expected đã sửa theo app (fragment + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`, xem `03_test-cases/v1.1/CHANGELOG.md` REVISE 2026-09-21). Ảnh lượt đầu đổi tên `__step3-FAIL-…` → `__pre-don-da-huy-o-tab-dang-dien-ra.png` (vẫn đúng TC, đúng nội dung). Chạy lại step 1–4 trên `anhdc4` lúc 10:35–10:36 (giờ máy ảo).
> **Expected mới:** đơn đã trả lại người gửi CÓ ở tab "Đã hoàn thành" và hiện lý do hoàn hàng; đơn "Đã huỷ" nằm ở tab "Đang diễn ra" với badge "Đã huỷ" và KHÔNG ở tab "Đã hoàn thành".

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco, nhấn "Hoạt động" (setup) | logout `MinhNDN2` → login `anhdc4` → FoxEco → find+tap `text("Hoạt động")` | ✅ | — | — |
| 2 | Nhấn tab con "Đã hoàn thành" (setup) | find+tap | ✅ | — | — |
| 3 | Nhấn tab con "Đang diễn ra", rà danh sách (setup) | find+tap `text("Đang diễn ra")`; find `text("Đã huỷ")` → **tìm thấy** | ✅ | `TC-ACT-015__pre-don-da-huy-o-tab-dang-dien-ra.png` | card `Gửi: Tài liệu \| Giá trị cao` · FTEL SG09 → FTEL Cao Bằng · badge `Đã huỷ` ⇒ **đúng Expected mới** |
| 4 | Nhấn lại "Đã hoàn thành", check vị trí cả 2 đơn của cặp đối chứng | find+tap; find `text("Đã huỷ")` → **không tìm thấy** (khớp kết quả rà toàn danh sách ở lô 1) | 🚫 BLOCKED | `TC-ACT-015__step4-BLOCKED-tab-da-hoan-thanh-khong-co-don-tra-lai-nguoi-gui.png` | vế "Đã huỷ" ✅ đúng. Vế **đơn đã trả lại người gửi**: tài khoản **không có đơn nào** như vậy ⇒ không kiểm được |

**Result: 🚫 BLOCKED at Step 4**
**Reason:** thiếu đơn `RETURNED` trên cùng tài khoản (tiền đề `SEED-ACT-03`, dựng qua `TC-DLV-063` — cần quyền đổi trạng thái đơn). Vế đơn "Đã huỷ" đã đúng theo Expected mới.
**Evidence:** `screenshots/TC-ACT-015__step4-BLOCKED-tab-da-hoan-thanh-khong-co-don-tra-lai-nguoi-gui.png` (+ `screenshots/TC-ACT-015__pre-don-da-huy-o-tab-dang-dien-ra.png`) — verified tồn tại
**Ghi chú:** ⚠️ Title của TC (*"…còn đơn đã huỷ vẫn bị ẩn"*) còn lệch Expected mới — `§10.5` khoá Title, nợ #27 CHANGELOG v1.1. Ứng viên bug lượt đầu **đã huỷ, không log**.

---

## Lô 2 — tài khoản `stag_thuyntt22@fpt.com` (Nguyễn Thị Thanh Thủy)

> ⚠️ **Tài khoản này KHÔNG còn "trắng"** (khác ghi nhận VR-014): tab `Đang diễn ra` có **2 đơn** — `Giao: Tài liệu | Giá trị thấp` (Tòa V-City → FPT Cầu Giấy, `Đã ghép`) và `Gửi: Tài liệu | Giá trị thấp` (FTEL SG09 → FTEL SG07, `Chờ ghép`). Ảnh recon: `screenshots/_recon__thuy-hoat-dong-dang-dien-ra-co-don.png` · màn chào: `screenshots/_setup__thuy-foxeco-trang-chu.png` (hero vẫn `0 · Chưa có đóng góp nào`).
> Tab `Đã hoàn thành` vẫn rỗng ⇒ chạy được **`TC-ACT-014`** (chỉ cần tab này rỗng). `012/016/017/018` cần **cả 2 tab** rỗng ⇒ chuyển sang tài khoản khác.

## TC-ACT-014: Check empty state tab Đã hoàn thành hiện đúng chuỗi không có CTA và ẩn hẳn khối lịch sử

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco (setup) | FoxPro logout → email `stag_thuyntt22@` → `NHẬN MÃ OTP` → OTP cố định → `ĐĂNG NHẬP` → `Chức năng` → FoxEco | ✅ | — | — |
| 2 | Nhấn tab "Hoạt động" (setup) | find `text("Hoạt động")` → tap | ✅ | — | — |
| 3 | Nhấn tab con "Đã hoàn thành" (setup) | find `text("Đã hoàn thành")` → tap | ✅ | — | — |
| 4 | Check dòng tiêu đề, số nút CTA, khối lịch sử | `appium_get_page_source` | ✅ PASS | `TC-ACT-014__verify-chua-co-don-hoan-tat-khong-cta-khong-khoi-lich-su.png` | text: **`Chưa có đơn hoàn tất`** (khớp nguyên văn). Phần tử `clickable` trên màn chỉ có: nút back · 2 tab con · 5 mục nav ⇒ **0 CTA**. Không có khối/tiêu đề lịch sử, không khung rỗng |

**Result: ✅ PASS**
**Evidence:** `screenshots/TC-ACT-014__verify-chua-co-don-hoan-tat-khong-cta-khong-khoi-lich-su.png` — verified tồn tại
**Ghi chú:** empty state có icon ◠ (activity) nét mảnh trong thẻ trắng — TC không assert icon ở tab này.

---

## Lô 3 — tài khoản trắng `stag_MinhNDN2@fpt.com` (Nguyễn Đình Nhật Minh)

> 🆕 **Lần đăng nhập đầu tiên của tài khoản này** — xác nhận: tên hiển thị **Nguyễn Đình Nhật Minh**, **có icon FoxEco**, hero `0 · Chưa có đóng góp nào`, section `Đơn của tôi` = `Chưa có đơn nào`, **cả 2 tab `Hoạt động` rỗng** ⇒ đúng `SEED-ACT-02`. Ảnh: `screenshots/_setup__minh-foxeco-trang-chu.png`.
> Đăng nhập gặp bẫy `T-ASN-07` 1 lần (popup *"Không thể kết nối mạng!"* ở màn OTP, mạng vẫn OK) → `Đồng ý` → bấm `ĐĂNG NHẬP` lại → vào được.
> 🔒 Chỉ đọc + điều hướng — ⛔ không tạo đơn, không bấm `Đăng tin gửi hàng` tới bước lưu ⇒ tài khoản **vẫn trắng** cho `TC-HOME-027/028/029` và `TC-GIFT-008`.

## TC-ACT-012: Check empty state tab Đang diễn ra hiện đúng chuỗi và đúng một nút đăng tin

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco bằng tài khoản trắng (setup) | logout Thủy → login `stag_MinhNDN2@` → `Chức năng` → FoxEco | ✅ | — | — |
| 2 | Nhấn tab "Hoạt động" (setup) | find `text("Hoạt động")` → tap | ✅ | — | mặc định mở tab `Đang diễn ra` |
| 3 | Check icon, dòng tiêu đề, dòng giải thích, số nút CTA | `appium_get_page_source` (text + `clickable`) | ❌ FAIL | `TC-ACT-012__step3-FAIL-thieu-dong-giai-thich-duoi-tieu-de.png` | Page source chỉ có 2 text trong vùng danh sách: **`Không có đơn đang thực hiện`** và **`Đăng tin gửi hàng`**. Icon ◠ nét mảnh xám ✅ · tiêu đề ✅ khớp nguyên văn · **đúng 1** CTA `Đăng tin gửi hàng` ✅ (`clickable` [225,658][496,726]) · **❌ KHÔNG có dòng giải thích** |

**Result: ❌ FAIL at Step 3**
**Expected:** icon nét mảnh neutral + tiêu đề `Không có đơn đang thực hiện` + **1 dòng giải thích** + đúng 1 CTA `Đăng tin gửi hàng`.
**Actual:** đủ icon, tiêu đề, CTA — **thiếu dòng giải thích** giữa tiêu đề và nút.
⚠️ TC không nêu nguyên văn dòng giải thích (chỉ nói "1 dòng giải thích") ⇒ nên đối chiếu `EMP-05` trong `DOC-v1.1-01` trước khi log bug. Cùng họ với `FE-310` (empty state `Đơn của tôi` ở Trang chủ sai chuỗi, thiếu CTA).
**Bug:** 🐞 `BUG-031` (draft, chờ QC review — chưa push Jira)
**Evidence:** `screenshots/TC-ACT-012__step3-FAIL-thieu-dong-giai-thich-duoi-tieu-de.png` — verified tồn tại

---

## TC-ACT-016: Check empty state không che thanh tab dưới ở cả hai tab rỗng

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập tài khoản trắng, nhấn "Hoạt động" (setup) | — | ✅ | — | — |
| 3 | Tab `Đang diễn ra`: nhấn lần lượt từng mục thanh tab dưới rồi quay lại "Hoạt động" | find+tap `Trang chủ` → thấy `Đóng góp của bạn` · `Bảng tin` → màn `Bảng tin` có card tin · `Cá nhân` → thấy `Quà đã nhận` · `Đăng tin` → màn `Đăng tin mới` → `back` · `Hoạt động` → thấy `Không có đơn đang thực hiện` | ✅ | — | 5/5 mục phản hồi; mỗi lần đều quay lại `Hoạt động` được |
| 4 | Nhấn tab con "Đã hoàn thành" | find+tap | ✅ | — | — |
| 5 | Lặp lại với 5 mục, check thanh tab dưới ở cả 2 tab con | `Trang chủ` · `Bảng tin` (thấy `Giá trị`) · `Đăng tin` (thấy `Đăng tin mới`) → `back` · `Cá nhân` (thấy `Quà đã nhận`) · `Hoạt động` | ✅ PASS | `TC-ACT-016__verify-tab-da-hoan-thanh-rong-thanh-tab-duoi-du-5-muc.png` | thanh tab dưới hiện đủ 5 mục ở cả 2 tab con; empty state nằm gọn ở giữa vùng danh sách, không đè lên thanh tab |

**Result: ✅ PASS**
**Evidence:** `screenshots/TC-ACT-016__verify-tab-da-hoan-thanh-rong-thanh-tab-duoi-du-5-muc.png` — verified tồn tại
**Ghi nhận ngoài Expected:** từ mục khác quay lại `Hoạt động` thì app **luôn mở lại tab `Đang diễn ra`**, không nhớ tab `Đã hoàn thành` vừa chọn (riêng `back` từ `Đăng tin mới` thì giữ tab). Không thuộc Expected của TC nào v1.1 — ghi lại để BA xem có cần rule không.

---

## TC-ACT-017: Check màn vẫn cuộn được khi đang hiện empty state ở cả hai tab rỗng

> 🔄 **Chấm lại 2026-09-21 theo Expected mới.** Lượt đầu ghi ❌ FAIL (không phản hồi cuộn, không có phần tử `scrollable`) + log `BUG-032`. QC GiangDC2 chốt: **app đúng** ⇒ Expected + step 5 sửa theo app (fragment + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`, `CHANGELOG` REVISE 2026-09-21), `BUG-032` xoá. Không chạy lại: hành vi quan sát lượt đầu **chính là** Expected mới. Ảnh `__step5-FAIL-…` đổi tên → `TC-ACT-017__verify-tab-da-hoan-thanh-vuot-man-dung-yen-khong-treo.png` (cùng TC, cùng nội dung).
> **Expected mới:** ở cả 2 tab, empty state đứng cố định khi vuốt (nội dung vừa khít màn, không có gì để cuộn); màn không treo, không lỗi, thanh tab dưới vẫn hiển thị đủ.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng nhập tài khoản trắng, nhấn "Hoạt động" (setup) | — | ✅ | — | — |
| 3 | Vuốt lên/xuống trên tab `Đang diễn ra` | `adb input swipe` chậm 3s, chụp giữa lúc vuốt | ✅ | `TC-ACT-017__pre-tab-dang-dien-ra-giua-thao-tac-vuot-len.png` | thẻ empty state đứng yên, thanh tab dưới đủ 5 mục |
| 4 | Nhấn tab con "Đã hoàn thành" | find+tap | ✅ | — | — |
| 5 | Vuốt lên/xuống, check trạng thái màn ở cả 2 tab | như step 3 + MCP `scrollable(true)` ×2 (không có phần tử cuộn) + tiếp tục tap tab/nav bình thường | ✅ PASS | `TC-ACT-017__verify-tab-da-hoan-thanh-vuot-man-dung-yen-khong-treo.png` | empty state đứng cố định, màn không treo (tap tab con + nav vẫn phản hồi ngay sau đó), thanh tab dưới hiển thị đủ |

**Result: ✅ PASS**
**Evidence:** `screenshots/TC-ACT-017__verify-tab-da-hoan-thanh-vuot-man-dung-yen-khong-treo.png` (+ `screenshots/TC-ACT-017__pre-tab-dang-dien-ra-giua-thao-tac-vuot-len.png`) — verified tồn tại
**Ghi chú:** ⚠️ Title (*"…vẫn cuộn được…"*) còn lệch Expected mới — `§10.5` khoá Title, nợ #28 CHANGELOG v1.1. `BUG-032` đã xoá, số không tái sử dụng.

---

## TC-ACT-018: Check tab rỗng phân biệt rõ trạng thái đang tải với trạng thái không có dữ liệu

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Throttle mạng về 3G chậm (setup) | `adb emu network speed umts` + `adb emu network delay umts` → status: **384 kbit/s**, latency 35–200 ms | ✅ | — | ⚠️ tài khoản đã đăng nhập từ trước khi throttle (step 2 làm trước step 1) — không ảnh hưởng vì cái cần đo là lúc vào màn |
| 2 | Đăng nhập FoxEco bằng tài khoản trắng (setup) | đã đăng nhập (lô 3) | ✅ | — | — |
| 3 | Nhấn "Hoạt động", theo dõi liên tục tab `Đang diễn ra` | chụp liên tiếp 30 khung (`screencap`) ngay khi tap | ✅ | `TC-ACT-018__pre-tab-dang-dien-ra-pha-skeleton-dang-tai.png` · `TC-ACT-018__pre-tab-dang-dien-ra-da-chuyen-empty-state.png` | khung 3–6: **skeleton 3 card xám** · khung 7: `Không có đơn đang thực hiện` · khung 7–30 **giống hệt nhau** (không quay lại skeleton) |
| 4 | Nhấn tab "Đã hoàn thành", theo dõi liên tục | lần 1 (sau khi đã xem tab này trước đó): empty state hiện ngay, không thấy pha tải. **Lần 2 — thoát FoxEco, vào lại từ đầu dưới 3G**, `Hoạt động` → `Đã hoàn thành` liền tay, chụp 40 khung | ✅ | `TC-ACT-018__pre-tab-da-hoan-thanh-pha-skeleton-dang-tai.png` | khung 4: tab `Đã hoàn thành` đang chuyển, vùng danh sách = **skeleton** · khung 5: `Chưa có đơn hoàn tất` |
| 5 | Check chuỗi trạng thái đã quan sát ở cả 2 tab | so md5 vùng danh sách giữa các khung | ✅ PASS | `TC-ACT-018__verify-tab-da-hoan-thanh-chuyen-han-empty-state-sau-tai.png` | cả 2 tab: **đang tải (skeleton) → empty state**, pha tải kết thúc < 2s ở 3G; khung 5–40 của tab `Đã hoàn thành` giống hệt nhau ⇒ **không skeleton vô hạn** |

**Result: ✅ PASS**
**Evidence:** `screenshots/TC-ACT-018__verify-tab-da-hoan-thanh-chuyen-han-empty-state-sau-tai.png` (+ `__pre-tab-dang-dien-ra-pha-skeleton-dang-tai.png` · `__pre-tab-dang-dien-ra-da-chuyen-empty-state.png` · `__pre-tab-da-hoan-thanh-pha-skeleton-dang-tai.png`) — verified tồn tại
**Giới hạn:** vế backend của `SC-ACT-017` `[GAP]` (*empty state dựa cờ dữ liệu rỗng, không dựa null field*) ⛔ không verify được qua UI — giữ là nợ theo §0.3 của fragment. Mạng đã trả về `full`/`none` sau TC.

---
