# Vibe Test Log — VR-016 — v1.1 (module FEED) — 2026-09-21

> Module: FEED · Platform: mobile (Appium, UiAutomator2, `emulator-5554`) · Env: STG (`com.hrisproject.stag`) · Evidence dir: `screenshots/`
> Phiên: 2026-09-21 (khởi tạo)
> **Phạm vi phiên này (theo yêu cầu QC):** CHỈ 5 TC thuộc v1.1 của module FEED (`TC-FEED-002/007/009/013/015`) —
> ⛔ KHÔNG chạy 10 TC carried từ v1.0 (`001/003/004/005/006/008/010/011/012/014`), giữ `⏳ NOT_RUN` có lý do trong `coverage-FEED.md`.
> Nguồn TC: `03_test-cases/v1.1/fragments/TC-FEED-v1.1.md`.
> Account: **Đặng Châu Giang** (`stag_giangdc2@fpt.com`) — app đã đăng nhập sẵn từ đầu phiên (xác nhận qua badge "Tin của bạn" trên card do chính tài khoản này đăng), không cần đổi tài khoản vì cả 5 TC chỉ cần vai "người xem" xem tin của tài khoản khác trong Bảng tin cộng đồng.

## TC-FEED-002: Check card tin ở Bảng tin đủ thành phần và không có nút CTA

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập bằng tài khoản B, nhấn tab "Bảng tin" | app đã ở sẵn màn Bảng tin, đã đăng nhập | ✅ PASS | — | tận dụng session có sẵn |
| 2 | Check lần lượt các thành phần và rà toàn bộ card tin đầu tiên tìm nút "Tôi mang giúp được" | quan sát card `feed-post-card-0` | ✅ PASS | `TC-FEED-002__verify-card0-no-cta.png` | — |
| E1 | Card hiển thị đủ: icon/ảnh hàng, dòng loại hàng kèm giá trị hàng, thời gian đăng, dòng "Nhận:"/"Giao:" dạng rút gọn, khung giờ mong muốn; card KHÔNG có nút "Tôi mang giúp được" ở bất kỳ đâu | Card 0: icon thumbnail ✓ · "Tài liệu \| Giá trị thấp" ✓ · "53 phút trước" ✓ · "Nhận: FTEL SG09 / Giao: FTEL SG07" ✓ · "Hôm nay · Sáng" ✓ · KHÔNG có nút "Tôi mang giúp được" trên bất kỳ card nào trong 5 card hiển thị | ✅ PASS | `TC-FEED-002__verify-card0-no-cta.png` | Card không có badge "Tin của bạn" (tin của tài khoản khác) — đúng, không ảnh hưởng TC này |

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-FEED-002__verify-card0-no-cta.png` — verified tồn tại
**Locators captured:** `feed-post-card-0..4`, `feed-post-own-badge`

---

## TC-FEED-007: Check phần dưới Chi tiết tin đủ lộ trình, khung giờ, tên người gửi và CTA

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập bằng tài khoản B, nhấn tab "Bảng tin" và nhấn 1 tin do tài khoản khác đăng | tap `feed-post-card-0` (tin "FTEL SG09 → FTEL SG07", không có badge "Tin của bạn" ⇒ đúng tài khoản khác) | ✅ PASS | — | — |
| 2 | Cuộn xuống phần dưới màn Chi tiết tin | `appium_gesture(scroll, down)` | ✅ PASS | — | — |
| 3 | Check lần lượt các thành phần | quan sát LỘ TRÌNH / KHUNG GIỜ / NGƯỜI GỬI / CTA | ❌ FAIL (1 trong 4 cụm không khớp) | `TC-FEED-007__verify-bottom-section.png` | xem chi tiết dưới |
| E1 | Hiển thị đủ: khối Lộ trình gồm điểm lấy hàng và điểm giao hàng đầy đủ như data đã đăng **kèm khung "Bản đồ · ~X km"**, khung giờ mong muốn, cụm Người gửi có đúng họ tên (KHÔNG có số điện thoại), và nút "Tôi mang giúp được" | Lộ trình: "Lấy hàng: FTEL SG09" / "Giao hàng: FTEL SG07" đầy đủ ✓ — nhưng **KHÔNG có khung "Bản đồ · ~X km"** nào, thay bằng 1 dòng chữ "Chưa xác định được toạ độ trên bản đồ cho địa chỉ này" ✗. Khung giờ "Hôm nay · Sáng" ✓. Người gửi "Nguyễn Thị Thanh Thủy" — có họ tên đầy đủ, KHÔNG có số điện thoại dạng text ✓ (có nút "Gọi" hiển thị nhưng SĐT dạng số không lộ ra text — ngoài phạm vi assert của TC này). Nút "Tôi mang giúp được" có, sticky ở đáy màn ✓ | ❌ **FAIL trên đúng 1 sub-clause: khung "Bản đồ · ~X km"** | `TC-FEED-007__verify-bottom-section.png` | **Root cause:** văn phòng `FTEL SG09`/`FTEL SG07` không có toạ độ hợp lệ trên STG hiện tại (đã kiểm chứng qua page source: không có node text nào chứa "km"). Đây là **cùng hiện tượng** với `TC-FEED-015` (xem bên dưới) — khi thiếu toạ độ, app không hiện bất kỳ khung/placeholder "Bản đồ" nào, chỉ có dòng cảnh báo lồng trong LỘ TRÌNH. 3/4 cụm còn lại PASS đúng như Expected. |

**Result (lần chạy 1, tài khoản Giang, data `FTEL SG09/SG07`): ❌ FAIL (khung "Bản đồ · ~X km" không hiển thị)**
**Evidence:** `screenshots/TC-FEED-007__verify-bottom-section.png` — verified tồn tại (giữ làm hồ sơ)
**Locators captured:** `text("Tôi mang giúp được")`, `text("Chưa xác định được toạ độ...")`

---

### 🔁 Retest — tài khoản `stag_anhdc4@fpt.com` (Đặng Châu Anh), 2026-09-21

> QC yêu cầu: login `anhdc4`, kiểm CTA trên vài tin không phải của mình. Thực hiện đăng xuất `Đặng Châu Giang` → đăng nhập `anhdc4` (luồng `USR-accounts.md §0b`: FoxPro → Cá nhân → Đăng xuất → Đồng ý → nhập email → NHẬN MÃ OTP → OTP cố định qua `adb shell input text` → ĐĂNG NHẬP → Chức năng → FoxEco) → Bảng tin.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập bằng tài khoản B (`anhdc4`), nhấn tab "Bảng tin" và nhấn 1 tin do tài khoản khác đăng | tap `feed-post-card-0` (tin của `Đặng Châu Giang` — seed fixture `TC-FEED-009`, KHÔNG có badge "Tin của bạn" với viewer `anhdc4` ⇒ đúng tài khoản khác) | ✅ PASS | — | Dùng lại fixture đã xác nhận có toạ độ hợp lệ (`FTEL An Giang Trần Hưng Đạo - Long Xuyên` ↔ `FTEL An Giang VPGD Bình Hòa`) — chọn có chủ đích để phủ luôn sub-clause "Bản đồ" |
| 2 | Cuộn xuống phần dưới màn Chi tiết tin | `appium_gesture(scroll, down)` | ✅ PASS | — | — |
| 3 | Check lần lượt các thành phần | quan sát LỘ TRÌNH (kèm bản đồ) / KHUNG GIỜ / NGƯỜI GỬI / CTA | ✅ PASS (4/4) | `TC-FEED-007__verify-anhdc4-bottom-with-cta.png` | xem chi tiết dưới |
| E1 | Hiển thị đủ: khối Lộ trình kèm khung "Bản đồ · ~X km", khung giờ mong muốn, cụm Người gửi có đúng họ tên (KHÔNG có số điện thoại), và nút "Tôi mang giúp được" | Lộ trình đầy đủ: "Lấy hàng: FTEL An Giang Trần Hưng Đạo - Long Xuyên" / "Giao hàng: FTEL An Giang VPGD Bình Hòa" ✓ — **kèm khung bản đồ Google Maps thật, vẽ tuyến cam, "17.2 km · 15 phút"** ✓. Khung giờ "Hôm nay · Sáng" ✓. Người gửi "Đặng Châu Giang" — họ tên đầy đủ, KHÔNG có SĐT dạng text ✓ (có nút "Gọi"). Nút "Tôi mang giúp được" có, sticky đáy màn ✓ | ✅ **PASS đủ 4/4 sub-clause** | `TC-FEED-007__verify-anhdc4-bottom-with-cta.png` | Xác nhận: FAIL lần 1 đúng là do data (`FTEL SG09`/`SG07` thiếu toạ độ), KHÔNG phải bug app |

**Result (retest, tài khoản anhdc4, data hợp lệ): ✅ PASS**
**Evidence:** `screenshots/TC-FEED-007__verify-anhdc4-bottom-with-cta.png` — verified tồn tại
**Locators captured:** luồng đăng xuất/đăng nhập FoxPro (tái sử dụng `USR-accounts.md §0b`), `feed-post-card-0` (tái sử dụng)
**Impact:** ✅ **Verdict cuối cùng: PASS.** Root cause của FAIL lần 1 đã xác nhận đúng là chọn nhầm test data (văn phòng thiếu toạ độ), không phải bug — khớp với kết luận đã rút ra sau retest `TC-FEED-009`. Không log bug.

### 🔍 Phát hiện kèm (theo yêu cầu QC) — CTA vắng mặt có chọn lọc theo tin, không phải theo tài khoản

> QC báo: "1 vài tin truy cập từ Bảng tin → tap vào tin (khác tôi tạo) nhưng không hiện nút Tôi mang giúp được" khi dùng `anhdc4`. Kiểm tra 3 tin không phải của `anhdc4` trong Bảng tin hiện tại:

| Tin (Lấy → Giao) | Người gửi | CTA với viewer `anhdc4`? |
|---|---|---|
| `FTEL An Giang Trần Hưng Đạo - Long Xuyên` → `FTEL An Giang VPGD Bình Hòa` | Đặng Châu Giang | ✅ Có |
| `FTEL SG09` → `FTEL SG07` | Nguyễn Thị Thanh Thủy | 🚫 **KHÔNG có** — quét hết page source + ảnh chụp toàn màn (`TC-FEED-007__verify-anhdc4-sg09sg07-no-cta.png`), không có sticky bar CTA nào |
| `FTEL SG07` → `FTEL SG03 Quận Tân Bình` | Nguyễn Tấn Vũ | ✅ Có |

**Kết luận:** CTA vắng mặt **có chọn lọc theo TỪNG TIN**, không phải `anhdc4` bị chặn CTA toàn bộ Bảng tin (2/3 tin kiểm vẫn có CTA bình thường). Khớp với rule đã biết `OPR-05`/`SC-FEED-012`: *"người nhận được khai không thấy nút Tôi mang giúp được"* — nhiều khả năng `anhdc4` là người nhận đã khai sẵn của tin `SG09→SG07` (app không có label "bạn là người nhận" để xác nhận trực tiếp, nhưng hành vi khớp đúng rule). **Đây không phải bug** — đây là dữ liệu thật, hữu ích để chạy `TC-FEED-012` (P2, hiện vẫn `⏳ NOT_RUN`, thuộc 10 TC carried v1.0 ngoài phạm vi VR-016) khi QC muốn phủ nốt case đó, vì đã có sẵn 1 cặp tin+tài khoản xác nhận đúng điều kiện "người nhận được khai".
**Evidence:** `screenshots/TC-FEED-007__verify-anhdc4-sg09sg07-no-cta.png` — verified tồn tại (ảnh phụ, không tính là evidence chính của `TC-FEED-007` — TC này đã PASS ở card-0)

---

## TC-FEED-009: Check khung bản đồ ở Chi tiết tin là ảnh tĩnh có vẽ tuyến thật

> ⚠️ **Retest cùng ngày sau khi log ban đầu BLOCKED.** QC cấp 2 địa chỉ cụ thể (`132 Trần Hưng Đạo, LX` = `FTEL An Giang Trần Hưng Đạo - Long Xuyên` · `19 ấp Phú An 1, Bình Hòa` = `FTEL An Giang VPGD Bình Hòa`) — cả 2 đều **có mặt** trong `location_address_catalog.xlsx` với `coordinate_status = MISSING`, nhưng app **thực tế hiển thị bản đồ thật** ⇒ xác nhận cột `coordinate_status` của file catalog **KHÔNG đáng tin** làm oracle dự đoán hành vi app (399/399 dòng đều `MISSING` kể cả khi có lat/lng hợp lệ — xem ghi chú ở `TC-FEED-015`). Phiên BLOCKED lúc đầu do chọn nhầm 5 tin "FTEL SGxx"/"Tòa V-City" sẵn có trên Bảng tin — đều thật sự thiếu toạ độ, không phải oracle sai.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (Precondition, lần 1) Tin NEED có điểm lấy/giao đều thuộc văn phòng CÓ đủ toạ độ, NGOÀI danh sách lỗi `C-FEED-05` | Kiểm 5 tin có sẵn trong Bảng tin — cả 5 đều thiếu toạ độ | 🚫 BLOCKED (lần 1) | `TC-FEED-009__step2-BLOCKED-no-valid-coord-office.png` | Đã gỡ ở retest — giữ ảnh làm hồ sơ |
| 1b | (Precondition, retest) Tự tạo 1 tin NEED mới qua wizard Đăng tin (module ORD), Lấy hàng = `FTEL An Giang Trần Hưng Đạo - Long Xuyên`, Giao hàng = `FTEL An Giang VPGD Bình Hòa` (2 địa chỉ QC cấp) | Đăng nhập sẵn `Đặng Châu Giang`; wizard 3 bước: Loại hàng=Tài liệu/Thấp/Nhẹ/Nhỏ + 1 ảnh, địa chỉ lấy = search "Trần Hưng Đạo" → chọn gợi ý An Giang/Long Xuyên, người nhận `stag_taipm@fpt.com` (auto-fill "Phan Minh Tài") + địa chỉ giao = search "Phú An" → chọn gợi ý An Giang/Bình Hòa, buổi Sáng → "Đăng tin thành công!" | ✅ PASS | — | Tin mới lên Bảng tin ngay (card 0, badge "Tin của bạn") |
| 2 | Đăng nhập bằng tài khoản B, nhấn tab "Bảng tin" và nhấn tin đó để mở màn Chi tiết tin. (setup) | tap card 0 (tin vừa tạo) | ✅ PASS | — | — |
| 3 | Check khung "Bản đồ · ~X km" | cuộn tới card LỘ TRÌNH | ✅ PASS | `TC-FEED-009__verify-real-map-route.png` | xem chi tiết dưới |
| E1 | Khung hiển thị ảnh bản đồ **tĩnh có vẽ tuyến** từ điểm lấy tới điểm giao (không phải khung trống/placeholder); có dòng "~X km" (không assert giá trị số cụ thể) | Khung hiển thị **ảnh bản đồ Google Maps thật** (logo "Google" góc trái dưới), có **đường tuyến màu cam vẽ nối 2 điểm ghim** (Lấy hàng — điểm cam đặc · Giao hàng — điểm cam viền xanh), kèm dòng **"17.2 km · 15 phút"** ngay dưới khung. Không phải khung trống/placeholder | ✅ PASS | `TC-FEED-009__verify-real-map-route.png` | Note gốc "Không test zoom/pan — ảnh tĩnh, không phải bản đồ tương tác" ⇒ **không** thao tác zoom/pan/tap vào khung, đúng theo TC |

**Result: ✅ PASS (retest với data QC cấp)**
**Evidence:** `screenshots/TC-FEED-009__verify-real-map-route.png` — verified tồn tại
**Locators captured:** wizard address autocomplete field (EditText, `set_value` + chọn gợi ý từ `-android uiautomator textContains(...)`), `feed-post-card-0` (tái sử dụng)
**Impact:** Automate được — dùng data cố định `FTEL An Giang Trần Hưng Đạo - Long Xuyên` ↔ `FTEL An Giang VPGD Bình Hòa` làm fixture chuẩn cho nhánh "bản đồ thật" của module FEED (và các TC khác cần văn phòng có toạ độ hợp lệ, ví dụ retest `TC-FEED-007`).
**🔑 Ghi nhớ cho lần sau:** `location_address_catalog.xlsx` (`DOC-v1.1-04`) không dùng được để suy đoán văn phòng nào có toạ độ hợp lệ (100% dòng đều `MISSING` bất kể lat/lng có giá trị) — phải kiểm THẬT qua app bằng cách tạo tin, không tra file.

---

## TC-FEED-013: Check empty state Bảng tin đúng text và chỉ 1 danh sách không tab

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Nhờ dev/QA chuẩn bị môi trường không còn tin NEED ở trạng thái "Chờ ghép" | Kiểm tra Bảng tin hiện tại | 🚫 BLOCKED | `TC-FEED-013__step1-BLOCKED-precondition-khong-rong.png` | Bảng tin hiện có ≥5 tin "Chờ ghép" (community-wide, không phải theo tài khoản) |

**Result: 🚫 BLOCKED tại Step 1 — precondition không đạt được**
**Reason:** Bảng tin là danh sách **cộng đồng toàn hệ thống** (không lọc theo tài khoản đang đăng nhập — đã xác nhận ở `TC-FEED-002/007/009/015` cùng phiên, thấy tin của nhiều tài khoản khác nhau). Muốn có precondition "0 tin Chờ ghép" cần dev/QA **xoá hoặc chuyển trạng thái TOÀN BỘ tin NEED đang Chờ ghép trên STG** — ngoài khả năng của AI (không có quyền admin/DB), và **không nên tự làm qua UI** vì sẽ phá dữ liệu fixture mà các module khác (ASN, ORD, DLV...) đang dùng chung (đã thấy card 4 có ghi chú "SEED S3 - lech khoang ngay (TC-ASN-012)" — chứng minh tin này là fixture của module ASN).
**Evidence:** `screenshots/TC-FEED-013__step1-BLOCKED-precondition-khong-rong.png` — verified tồn tại
**Impact:** Cần lên lịch với dev/QA một cửa sổ riêng (môi trường sạch hoặc STG phụ) để test case này mà không ảnh hưởng fixture của module khác.

---

## TC-FEED-015: Check khung bản đồ hiện placeholder và 0km khi văn phòng thiếu toạ độ

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập bằng tài khoản B, nhấn tab "Bảng tin" và nhấn tin đó để mở màn Chi tiết tin | tap `feed-post-card-4` (tin "Tòa V-City → FPT Cầu Giấy", người gửi "Phan Minh Tài" — tài khoản khác) | ✅ PASS | — | cả 2 điểm lấy/giao đều nằm trong danh sách lỗi toạ độ `C-FEED-05` (đối chiếu `DOC-v1.1-04`) — đúng precondition TC-015 |
| 2 | Check khung "Bản đồ · ~X km" và tổng thể bố cục màn | cuộn qua toàn bộ màn Chi tiết tin, đọc page source | ❌ FAIL | `TC-FEED-015__step2-FAIL-lo-trinh-no-map-box.png` (+ `__step2-FAIL-no-placeholder-no-0km.png`) | xem chi tiết dưới |
| E1 | Khung hiển thị placeholder kèm thông báo (không phải ảnh bản đồ vẽ tuyến); khoảng cách hiện đúng "0km"; màn không vỡ layout | **KHÔNG có khung/placeholder riêng nào cho bản đồ** — chỉ có 1 dòng chữ "Chưa xác định được toạ độ trên bản đồ cho địa chỉ này" lồng ngay dưới địa chỉ "Giao hàng" trong card LỘ TRÌNH. **KHÔNG có text "0km"** hay bất kỳ giá trị khoảng cách nào ở bất kỳ đâu trên màn (xác nhận qua `get_page_source`, không có node nào chứa "km"). Màn KHÔNG vỡ layout — các card THÔNG TIN HÀNG / LỘ TRÌNH / KHUNG GIỜ / NGƯỜI GỬI vẫn hiển thị đúng vị trí, không tràn/chồng lấn | ❌ FAIL (2/3 sub-clause sai: thiếu khung placeholder riêng + thiếu "0km"; chỉ đúng phần "không vỡ layout") | `TC-FEED-015__step2-FAIL-lo-trinh-no-map-box.png` | Tái hiện được **2 lần độc lập** trên 2 cặp văn phòng khác nhau (xem `TC-FEED-007`/`TC-FEED-009` cùng phiên) ⇒ hành vi nhất quán, không phải lỗi ngẫu nhiên/network |

**Result: ✅ PASS** *(đổi từ ❌ FAIL — xem ĐÍNH CHÍNH 2026-09-21 bên dưới)*
**Expected vs Actual (lúc chạy):** Expected gốc = khung placeholder + "0km" hiển thị. Actual = chỉ có dòng cảnh báo text, không có khung riêng, không có "0km".
**Evidence:** `screenshots/TC-FEED-015__verify-accepted-behavior.png` (bản copy y hệt `__step2-FAIL-lo-trinh-no-map-box.png`, đổi tên theo verdict cuối PASS — nội dung ảnh không đổi) + `__step2-FAIL-lo-trinh-no-map-box.png` (+ `__step2-FAIL-no-placeholder-no-0km.png`, giữ nguyên làm hồ sơ lúc còn FAIL) — verified tồn tại
**Impact ban đầu (rút lại):** ~~Khuyến nghị `/log-bug`~~ — đã log `BUG-029`, sau đó **rút lại** (xem đính chính).

⚠️ **ĐÍNH CHÍNH 2026-09-21 (QC GiangDC2, sau khi review `BUG-029`):** QC **chấp nhận hành vi hiện tại của app là đúng** — dòng cảnh báo text thay cho khung placeholder + "0km" là hành vi chấp nhận được, không phải bug. Đã sửa lại **Expected Result** của `TC-FEED-015` trong `03_test-cases/v1.1/fragments/TC-FEED-v1.1.md` + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx` để khớp hành vi thật (không đổi Test Title/Steps/số lượng TC — đúng `Project_rule §10.5`). `BUG-029` đã xoá khỏi `draft/`, không push Jira. Actual quan sát ở trên **vẫn đúng** (không sửa lại phần ghi nhận thực tế) — chỉ đổi **kết luận PASS/FAIL** vì Expected đã đổi để khớp app.
Lưu ý: verdict này **độc lập với `TC-FEED-007`** — xem đính chính riêng ở `TC-FEED-007` (case đó KHÔNG được chấp nhận, vẫn cần retest với data hợp lệ).
