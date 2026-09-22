# Vibe Test Log — VR-018 — module CNL — v1.1 — 2026-09-21

> Module: **CNL — Huỷ đơn / Huỷ nhận đơn** · Platform: **mobile** (Appium MCP / UiAutomator2) · Device `emulator-5554` · Env: STG · host app `com.hrisproject.stag` (FoxPro) → FoxEco
> Evidence dir: `screenshots/`
> Phiên: 2026-09-21 (khởi tạo) · 2026-09-22 (follow-up — chụp bù evidence đúng slot cho `TC-CNL-010/017/018/019`)
> Tập chạy: **chỉ 13 TC v1.1** (`004 006 009 010 012 015 016 017 018 019 020 021 022`) theo yêu cầu QC — ⛔ không gồm 9 TC CARRIED v1.0 (`001 002 003 005 007 008 011 013 014`) — header fragment v1.1 chỉ liệt kê 8, thiếu `014` (đối chiếu 2 file TC-MASTER).
> 🔓 **QC cho phép đầy đủ** (2026-09-21): đăng tin NEED, ghép, bấm "Tôi đã lấy hàng", huỷ đơn / huỷ nhận đơn trên STG.
> Cách chụp ảnh: `adb exec-out screencap -p` ghi thẳng vào `screenshots/` (cùng cách VR-015/017).

## Dữ liệu dựng trong phiên

| Mã | Chủ tin (A) | Tuyến | Người nhận (C) | Buổi | Dùng cho |
|---|---|---|---|---|---|
| **O1** | `stag_anhdc4@` (Đặng Châu Anh) | Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy · Hôm nay | `stag_huyennhk@` (Nguyễn Huỳnh Kim Huyền) | Giờ nào cũng được | `004` · `012` (Chờ ghép) → `009` (Đã ghép) |

Ảnh: `screenshots/_setup__o1-dang-tin-thanh-cong.png` · `screenshots/_setup__preflight-anhdc4-hoat-dong.png`

---

## TC-CNL-004: Check lý do huỷ 4 ký tự bị chặn ngay từ nút xác nhận

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập A, đăng 1 tin NEED qua wizard "+ Đăng tin" (setup) | wizard 3 bước → `Đăng tin thành công!` | ✅ | `_setup__o1-dang-tin-thanh-cong.png` | tin O1 |
| 2 | Nhấn tab "Hoạt động", mở đơn vừa đăng, nhấn "Huỷ đơn" (setup) | find+tap `text("Chờ ghép").instance(0)` → `resourceId("track-cancel-post")` | ✅ | — | popup `Huỷ đơn hàng`, ô lý do trống thì `cancel-order-confirm` `enabled=false` |
| 3 | Nhập "abcd" vào ô lý do | set_value `resourceId("cancel-order-reason")` = `abcd` | ✅ | — | — |
| 4 | Check nút "Xác nhận" và vùng dưới ô lý do | `get_element_attribute enabled` + page source | ❌ FAIL | `TC-CNL-004__step4-FAIL-nut-xac-nhan-khoa-nhung-khong-co-loi-duoi-o-ly-do.png` | Nút `Xác nhận` **`enabled=false`** ✅ (khoá sẵn, không phải bấm rồi báo lỗi) · trạng thái đơn vẫn `Chờ ghép` ✅ · **❌ KHÔNG có dòng lỗi** dưới ô lý do: page source giữa ô lý do `[92,636][628,812]` và hàng nút `[..,848]` không có text nào |

**Result: ❌ FAIL at Step 4**
**Expected:** nút "Xác nhận" vô hiệu hoá ngay; **hiện lỗi ngay dưới ô lý do**; trạng thái đơn không đổi.
**Actual:** 2/3 vế đúng (nút khoá · đơn không đổi); **thiếu thông báo lỗi dưới ô lý do** — người dùng không biết vì sao không bấm được.
**Evidence:** `screenshots/TC-CNL-004__step4-FAIL-nut-xac-nhan-khoa-nhung-khong-co-loi-duoi-o-ly-do.png` — verified tồn tại
**Ghi chú:** TC ghi *"Dự kiến FAIL — app hiện cho qua"*; thực tế app **đã** chặn bằng nút khoá (khác dự kiến), chỉ còn thiếu vế lỗi hiển thị (`VAL-04` + `AC-25.1.03`).

---

## TC-CNL-012: Check lý do huỷ gồm năm dấu cách bị chặn sau khi cắt khoảng trắng

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập A, đăng 1 tin NEED (setup) | dùng lại O1 (cùng phiên, vừa đăng) | ✅ | — | — |
| 2 | Nhấn "Hoạt động", mở đơn, nhấn "Huỷ đơn" (setup) | đóng popup của `004` bằng `cancel-order-dismiss` → tap lại `track-cancel-post` | ✅ | — | ô lý do mở lại **trống** (text = placeholder) |
| 3 | Nhập đúng 5 dấu cách | set_value = `"     "` → `get_element_attribute text` trả **5 dấu cách** | ✅ | — | xác nhận giá trị thật trong ô, không phải placeholder |
| 4 | Check trạng thái nút "Xác nhận" | `get_element_attribute enabled` | ✅ PASS | `TC-CNL-012__verify-5-dau-cach-nut-xac-nhan-vo-hieu-hoa.png` | `cancel-order-confirm` **`enabled=false`** |

**Result: ✅ PASS**
**Evidence:** `screenshots/TC-CNL-012__verify-5-dau-cach-nut-xac-nhan-vo-hieu-hoa.png` — verified tồn tại
**Ghi chú:** TC ghi *"Dự kiến FAIL — `KB-CNL-02` đã live-verify app cho qua"* ⇒ **app đã sửa**, nay chặn đúng. Popup đóng lại bằng `Huỷ`, O1 vẫn `Chờ ghép`.

---

## TC-CNL-022: Check không tồn tại bề mặt Admin vận hành trong app end-user

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập A (CBNV thường) (setup) | `stag_anhdc4@` | ✅ | — | — |
| 2 | Rà toàn bộ màn Theo dõi đơn và trang Cá nhân tìm chức năng huỷ/can thiệp của "Admin vận hành" | page source màn Theo dõi đơn O1 (đầu → cuối, 3 khung) + màn `Cá nhân`; grep `admin|quản trị|vận hành` | ✅ PASS | `TC-CNL-022__verify-trang-ca-nhan-khong-co-be-mat-admin.png` | Theo dõi đơn: `Báo cáo sự cố` · timeline 5 mốc · LỘ TRÌNH · ẢNH · THÔNG TIN HÀNG · LỊCH SỬ · `Chỉnh sửa` · `Huỷ đơn`. Cá nhân: 3 mục `Đơn của tôi` · `Quà đã nhận` · `Cập nhật thông tin cá nhân`. **0** kết quả grep ở cả 2 màn |

**Result: ✅ PASS**
**Evidence:** `screenshots/TC-CNL-022__verify-trang-ca-nhan-khong-co-be-mat-admin.png` — verified tồn tại

---

## TC-CNL-010: Check huỷ nhận đơn giữ nguyên log ghép cũ và đơn về lại bảng tin

> Dữ liệu: **O2** — chủ tin `stag_anhdc4@` · `FPT Tân Thuận 1 → Tòa V-City, Lê Thái Tổ` · Hôm nay · Giờ nào cũng được · người nhận `stag_giangdc2@` (Đặng Châu Giang, `0964633310`). Ảnh: `screenshots/_setup__o2-dang-tin-thanh-cong.png`. B = `stag_anhptm17@` (Phan Thị Mỹ Anh). Cùng lượt B cũng ghép **O1** (`screenshots/_setup__o1-anhptm17-ghep-thanh-cong.png`) để dùng cho `009`.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | A đăng 1 tin NEED rồi đăng xuất (setup) | O2 | ✅ | `_setup__o2-dang-tin-thanh-cong.png` | — |
| 2 | B nhận đơn và xác nhận (setup) | Bảng tin → card O2 → `Tôi mang giúp được` → `Xác nhận` | ✅ | `_setup__o2-anhptm17-ghep-thanh-cong.png` | màn Theo dõi đơn vai người vận chuyển |
| 3-4 | Mở LỊCH SỬ, check dòng "Ghép thành công" (setup) | scroll `text("LỊCH SỬ")` + page source | ✅ | `TC-CNL-010__pre-lich-su-truoc-khi-huy-nhan-co-ghep-thanh-cong.png` | `Ghép thành công · Hôm nay · 23:21 · Phan Thị Mỹ Anh` + `Đăng tin lên bảng tin · 23:16 · Đặng Châu Anh` |
| 5-7 | Nhấn "✕ Huỷ nhận đơn", nhập "Doi ca lam viec", nhấn "Xác nhận" | `resourceId("track-carrier-cancel-accept")` → set_value `cancel-order-reason` → `cancel-order-confirm` | ✅ | `TC-CNL-010__pre-popup-huy-nhan-ly-do-doi-ca-lam-viec.png` | popup `Đã huỷ` — *"Đã huỷ nhận đơn. Đơn đã trả lại bảng tin."* |
| 8 | Không rời màn Theo dõi đơn, mở lại LỊCH SỬ | ⚠️ sau `Đồng ý` **app tự chuyển B sang `Chi tiết tin`** (B không còn là bên của đơn) — màn này **không có** block LỊCH SỬ | ⚠️ | `TC-CNL-010__pre-sau-huy-nhan-app-chuyen-sang-chi-tiet-tin-khong-co-lich-su.png` | đọc LỊCH SỬ bằng cách B ghép lại O2 (cần cho seed Đang giao) → Theo dõi đơn: xem hàng dưới |
| 9 | Vào "Bảng tin" tìm đơn đó | back → Bảng tin | ✅ | `TC-CNL-010__pre-o2-hien-lai-tren-bang-tin-sau-huy-nhan.png` | O2 **hiện lại** đầu Bảng tin (Tân Thuận 1 → V-City), mở ra có `Tôi mang giúp được` ⇒ đơn về `Chờ ghép` ✅ |
| E | Check LỊCH SỬ (đọc sau khi B ghép lại O2) | page source block LỊCH SỬ | ⚠️ **NOT_EVIDENCED** *(nội dung ĐẠT sau đính chính 2026-09-22, ảnh sai slot — lúc chạy chấm ❌ FAIL)* | `TC-CNL-010__step8-FAIL-log-huy-nhan-ghi-ten-khong-ghi-vai-nguoi-van-chuyen.png` | Thứ tự mới → cũ: `Ghép thành công · 23:24 · Phan Thị Mỹ Anh` · **`Đã huỷ nhận đơn · 23:22 · Phan Thị Mỹ Anh` + `Lý do: Doi ca lam viec`** · `Ghép thành công · 23:21 · Phan Thị Mỹ Anh` (✅ **không bị xoá**) · `Đăng tin lên bảng tin · 23:16` |

**Result: ✅ PASS** *(đính chính nội dung 2026-09-22; evidence đúng slot bổ sung ở Follow-up 2026-09-22 — xem cuối file)*
**Expected (mới):** "Ghép thành công" vẫn còn; có thêm 1 dòng log huỷ nhận đúng nhãn **"Đã huỷ nhận đơn"** kèm **tên người thực hiện** (không ghi vai trò — chấp nhận) và lý do "Doi ca lam viec"; đơn về "Chờ ghép" và hiện lại trên bảng tin.
**Actual:** đúng như Expected mới — dòng ghép cũ **giữ nguyên** ✅ · nhãn `Đã huỷ nhận đơn` đúng ✅ · có **lý do** + **thời điểm** ✅ · ghi **tên người** (`Phan Thị Mỹ Anh`) — chấp nhận ✅ · đơn **về bảng tin** ✅.
> 🔁 **Đính chính nội dung 2026-09-22:** app ghi **tên người thực hiện** thay vì vai trò ở dòng log huỷ nhận, nhất quán với **mọi dòng LỊCH SỬ khác** trong toàn app (không riêng dòng huỷ) — chấp nhận, không phải bug. Expected step E đã sửa cho khớp (fragment `TC-CNL-v1.1.md` + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`); draft `BUG-035` đã xoá.
> ⚠️ **Evidence:** ảnh gốc của phiên 2026-09-21 mang tên slot `__step8-FAIL` (chụp lúc đang chấm FAIL theo Expected cũ) — không đủ cho verdict PASS theo gate. Đã chụp bù ảnh đúng slot `__verify` ở phiên follow-up 2026-09-22 (đọc lại LỊCH SỬ hiện tại của O2, không cần lặp lại thao tác huỷ nhận vì log bất biến) — xem `TC-CNL-010__verify-lich-su-huy-nhan-giu-nguyen-sau-dinh-chinh.png`.
**Ghi nhận ngoài TC:** sau khi huỷ nhận, app tự rời `Theo dõi đơn` sang `Chi tiết tin` ⇒ step 7 *"không rời màn Theo dõi đơn"* không làm được đúng nguyên văn trên vai B.
**Evidence:** `screenshots/TC-CNL-010__verify-lich-su-huy-nhan-giu-nguyen-sau-dinh-chinh.png` (follow-up 2026-09-22) + `screenshots/TC-CNL-010__step8-FAIL-log-huy-nhan-ghi-ten-khong-ghi-vai-nguoi-van-chuyen.png` (+ `screenshots/TC-CNL-010__pre-lich-su-truoc-khi-huy-nhan-co-ghep-thanh-cong.png` · `screenshots/TC-CNL-010__pre-popup-huy-nhan-ly-do-doi-ca-lam-viec.png` · `screenshots/TC-CNL-010__pre-sau-huy-nhan-app-chuyen-sang-chi-tiet-tin-khong-co-lich-su.png` · `screenshots/TC-CNL-010__pre-o2-hien-lai-tren-bang-tin-sau-huy-nhan.png`, evidence gốc) — verified tồn tại

---

## TC-CNL-021: Check huỷ đơn bị chặn khi đơn còn hiện Đã ghép nhưng người vận chuyển đã bấm lấy hàng

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 0 | Tiền đề: O2 `Đã ghép` (B ghép lại lần 2) | — | ✅ | `_setup__o2-anhptm17-ghep-lai-lan-2.png` | — |
| 1 | Phiên B: nhấn "Tôi đã lấy hàng", CHƯA xác nhận popup | `resourceId("track-carrier-pickup")` → popup `Xác nhận` — *"Bạn xác nhận đã lấy hàng từ người gửi và bắt đầu giao?"* | ✅ | — | popup giữ mở |
| 2 | Phiên A: mở Theo dõi đơn, nhấn "Huỷ đơn" | ⛔ **không thực hiện được** — chỉ có **1 thiết bị** (`emulator-5554`); máy thật `R58T20PLP8K` không kết nối. Đổi tài khoản trên cùng máy sẽ đóng popup của B ⇒ phá tiền đề | 🚫 BLOCKED | `TC-CNL-021__step2-BLOCKED-popup-lay-hang-dang-mo-o-phien-b-khong-co-phien-a-song-song.png` | — |

**Result: 🚫 BLOCKED at Step 2**
**Reason:** TC cần **2 phiên đăng nhập song song** (A + B cùng lúc). Cắm lại máy thật (hoặc bật emulator thứ 2) rồi chạy lại.
**Ghi nhận kèm (quan trọng cho lượt chạy lại):** sau popup `Xác nhận`, app còn **1 màn trung gian** `Xác nhận đã lấy hàng` (thông tin người gửi · điểm lấy hàng · ảnh bằng chứng tuỳ chọn 0/5) với nút `Đã lấy hàng — Bắt đầu giao` ⇒ có **2 thời điểm** để thử cuộc đua (popup đang mở · màn trung gian đang mở).
**Evidence:** `screenshots/TC-CNL-021__step2-BLOCKED-popup-lay-hang-dang-mo-o-phien-b-khong-co-phien-a-song-song.png` — verified tồn tại

---

## TC-CNL-018: Check chỉ còn đúng 2 đường thoát cho vai Người vận chuyển sau khi đơn đang giao

> Tiền đề: B xác nhận popup → màn `Xác nhận đã lấy hàng` → `Đã lấy hàng — Bắt đầu giao` → `Đồng ý` ⇒ O2 **Đang giao** (LỊCH SỬ thêm `Người mang đã lấy hàng · 23:26 · FPT Tân Thuận 1`).

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | B mở Theo dõi đơn của đơn Đang giao (setup) | — | ✅ | — | timeline active `Đang giao` |
| 2 | Rà toàn bộ nút hành động | page source đầu → cuối, lọc `clickable=true` + grep `hoàn hàng|huỷ` | ⚠️ **NOT_EVIDENCED** *(nội dung ĐẠT sau đính chính 2026-09-22, ảnh sai slot — lúc chạy chấm ❌ FAIL)* | `TC-CNL-018__step2-FAIL-vai-nguoi-van-chuyen-dang-giao-khong-co-yeu-cau-hoan-hang.png` | Nút bấm được: `Quay lại` · **`Báo cáo sự cố`** (`track-report-incident`) · `Copy`×3 · `Gọi người gửi` · **`Đã giao cho người nhận`**. **Không** có nút huỷ ✅ |

**Result: ✅ PASS** *(đính chính nội dung 2026-09-22; evidence đúng slot bổ sung ở Follow-up 2026-09-22 — xem cuối file)*
**Expected (mới):** KHÔNG còn nút huỷ đơn thường; có `Báo cáo sự cố` VÀ đường vào hoàn hàng qua màn giao hàng (`Đã giao cho người nhận` → `Xử lý đơn hàng` → `Cầm hàng về`) — KHÔNG có nút riêng tên "Yêu cầu hoàn hàng".
**Actual:** không có nút huỷ ✅; có `Báo cáo sự cố` ✅; đường hoàn hàng đi gián tiếp: `Đã giao cho người nhận` → *Không thể liên lạc cho người nhận?* → *Xử lý đơn hàng* → *Cầm hàng về* (theo `TC-DLV-034/063`) ✅ — đúng như Expected mới.
> 🔁 **Đính chính nội dung 2026-09-22:** đã đối chiếu PRD gốc (`AC-25.2.01` + `BR11-04` + `FR09` §8.9) — không có nút "Yêu cầu hoàn hàng" nào được đặc tả; luồng hoàn hàng thật do Người vận chuyển khởi tạo qua "Xử lý đơn hàng" → "Cầm hàng về", đúng như app đang có. Expected TC đã sửa; draft `BUG-033` đã xoá.
> ⚠️ **Evidence:** ảnh gốc mang tên slot `__step2-FAIL` — không đủ cho verdict PASS theo gate. Đã chụp bù ảnh đúng slot `__verify` ở phiên follow-up 2026-09-22 (đọc lại màn Theo dõi đơn hiện tại của O2 vai Carrier, không cần lặp lại hành động nào) — xem `TC-CNL-018__verify-vai-nguoi-van-chuyen-bao-cao-su-co-va-duong-giao-hang.png`.
> *(Câu "Nên hỏi BA" bên dưới là ghi chép lúc chạy — QC đã tự chốt bằng cách đọc PRD, không cần hỏi BA.)*
**Evidence:** `screenshots/TC-CNL-018__verify-vai-nguoi-van-chuyen-bao-cao-su-co-va-duong-giao-hang.png` (follow-up 2026-09-22) + `screenshots/TC-CNL-018__step2-FAIL-vai-nguoi-van-chuyen-dang-giao-khong-co-yeu-cau-hoan-hang.png` (evidence gốc) — verified tồn tại

---

## TC-CNL-015: Check nút "Báo cáo sự cố" tồn tại cho vai Người vận chuyển khi đơn đang giao

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | B mở Theo dõi đơn của đơn Đang giao (setup) | — | ✅ | — | — |
| 2 | Check góc trên bên phải | find `resourceId("track-report-incident")` → tap | ✅ PASS | `TC-CNL-015__verify-nguoi-van-chuyen-bam-bao-cao-su-co-mo-luong-bao-su-co.png` | nút `Báo cáo sự cố` ở góc trên phải ✅ · nhấn mở màn **`Báo sự cố đơn hàng`** ✅ |

**Result: ✅ PASS**
**Evidence:** `screenshots/TC-CNL-015__verify-nguoi-van-chuyen-bam-bao-cao-su-co-mo-luong-bao-su-co.png` — verified tồn tại
**Ghi nhận:** màn `Báo sự cố đơn hàng` là **webview đòi đăng nhập Microsoft** (`Sign in` · *Email or phone*) — tức form báo sự cố nằm **ngoài app** (MS Forms). Nội dung form thuộc `TS` (`SC-TS-008..015`), ⛔ không kiểm ở đây. Hệ quả: báo sự cố **không** đổi trạng thái đơn trong app ⇒ không dựng được đơn `INCIDENT` (xem `TC-CNL-020`). Đã `back` ra, **không gửi** gì. Nút `Báo cáo sự cố` hiện ở **mọi** trạng thái đã thấy (cả `Chờ ghép`).

---

## TC-CNL-017: Check chỉ còn đúng 2 đường thoát cho vai Người gửi sau khi đơn đang giao

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | A (`anhdc4`) mở Theo dõi đơn của O2 Đang giao (setup) | đăng nhập lại A → Hoạt động → card `Đang giao` | ✅ | — | timeline active `Đang giao`; khối `NGƯỜI GIAO HÀNG` = Phan Thị Mỹ Anh `0947153040` |
| 2 | Rà toàn bộ nút hành động | page source đầu + `scroll_to_element textContains("hoàn hàng")` tới cuối (không thấy) + page source cuối | ⚠️ **NOT_EVIDENCED** *(nội dung ĐẠT sau đính chính 2026-09-22, ảnh sai slot — lúc chạy chấm ❌ FAIL)* | `TC-CNL-017__step2-FAIL-vai-nguoi-gui-dang-giao-khong-co-yeu-cau-hoan-hang.png` | Nút bấm được: `Quay lại` · **`Báo cáo sự cố`** · `Copy`×2 · `Gọi người giao hàng`. Chân màn: nhãn **tắt** `Đang giao đến người nhận` (`clickable=false`). **Không** nút huỷ ✅ |

**Result: ✅ PASS** *(đính chính nội dung 2026-09-22; evidence đúng slot bổ sung ở Follow-up 2026-09-22 — xem cuối file)*
**Expected (mới):** không còn nút huỷ thường; chỉ còn đúng 1 nút liên quan: "Báo cáo sự cố". Người gửi KHÔNG có nút/route hoàn hàng nào (hoàn hàng là hành động của Người vận chuyển, `FR09`).
**Actual:** chỉ có `Báo cáo sự cố`, không có gì khác liên quan huỷ/hoàn hàng — đúng như Expected mới (cùng hiện tượng `TC-CNL-018`/`019`).
> 🔁 **Đính chính nội dung 2026-09-22** — xem đầy đủ ở `TC-CNL-018`. Draft `BUG-033` đã xoá.
> ⚠️ **Evidence:** ảnh gốc mang tên slot `__step2-FAIL` — không đủ cho verdict PASS theo gate. Đã chụp bù ảnh đúng slot `__verify` ở phiên follow-up 2026-09-22 (đọc lại màn Theo dõi đơn hiện tại của O2 vai Sender) — xem `TC-CNL-017__verify-vai-nguoi-gui-chi-co-bao-cao-su-co.png`.
**Evidence:** `screenshots/TC-CNL-017__verify-vai-nguoi-gui-chi-co-bao-cao-su-co.png` (follow-up 2026-09-22) + `screenshots/TC-CNL-017__step2-FAIL-vai-nguoi-gui-dang-giao-khong-co-yeu-cau-hoan-hang.png` (evidence gốc) — verified tồn tại

---

## TC-CNL-006: Check nút "Báo cáo sự cố" tồn tại cho vai Người gửi khi đơn đang giao

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | A mở Theo dõi đơn của O2 Đang giao (setup) | như `017` | ✅ | — | — |
| 2 | Check góc trên bên phải | find+tap `resourceId("track-report-incident")` | ✅ PASS | `TC-CNL-006__verify-nguoi-gui-bam-bao-cao-su-co-mo-luong-bao-su-co.png` | nút có ✅ · nhấn mở màn `Báo sự cố đơn hàng` ✅ (webview Microsoft `Sign in`, giống `015`) |

**Result: ✅ PASS**
**Evidence:** `screenshots/TC-CNL-006__verify-nguoi-gui-bam-bao-cao-su-co-mo-luong-bao-su-co.png` — verified tồn tại
**Ghi chú:** kỳ vọng **ngược bản v1.0** cùng ID (v1.0: không có nút) — bản v1.1 PASS. Đã `back`, không gửi gì.

---

## TC-CNL-009: Check huỷ đơn ghi log đủ vai trò, lý do và thời điểm

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | A đăng NEED, B nhận ⇒ "Đã ghép" (setup) | **O1** (đăng 23:09 bởi A, ghép 23:20 bởi `anhptm17`) | ✅ | `_setup__o1-anhptm17-ghep-thanh-cong.png` | — |
| 2-3 | Mở Theo dõi đơn, mở LỊCH SỬ, ghi số dòng | A → Hoạt động → card O1 (`textContains("FPT Cầu Giấy")`) → scroll `LỊCH SỬ` + page source | ✅ | `TC-CNL-009__pre-lich-su-truoc-khi-huy-2-dong.png` | **2 dòng**: `Ghép thành công · 23:20 · Phan Thị Mỹ Anh` · `Đăng tin lên bảng tin · 23:09 · Đặng Châu Anh`. Chân màn: `Đã ghép · chờ shipper lấy hàng` + nút `Huỷ đơn` (`track-sender-matched-cancel`) |
| 4-6 | Nhấn "Huỷ đơn", nhập "Huy vi trung lich", "Xác nhận" | `track-sender-matched-cancel` → set_value `cancel-order-reason` → `cancel-order-confirm` | ✅ | `TC-CNL-009__pre-popup-huy-don-ly-do-huy-vi-trung-lich.png` | popup `Đã huỷ` — *"Đã huỷ đơn hàng."* → `Đồng ý` |
| 7 | Không rời màn Theo dõi đơn, mở lại LỊCH SỬ | ⚠️ sau `Đồng ý` app **tự về danh sách `Đơn của tôi`** (O1 mang badge `Đã huỷ`, vẫn ở tab `Đang diễn ra`) ⇒ mở lại card O1 | ⚠️ | — | không giữ được nguyên văn "không rời màn" |
| 8 | Check số dòng log mới và nội dung | page source LỊCH SỬ | ❌ FAIL | `TC-CNL-009__step8-FAIL-log-nguoi-gui-huy-ghi-nhan-da-huy-nhan-don-khong-co-vai.png` | **3 dòng** (+1 ✅). Dòng mới: **`Đã huỷ nhận đơn`** · `Hôm nay · 23:34 · Đặng Châu Anh` · `Lý do: Huy vi trung lich`. Chân màn: nhãn tắt `Đơn đã huỷ` |

**Result: ❌ FAIL at Step 8** *(vẫn FAIL sau đính chính 2026-09-22 — xem dưới)*
**Expected (mới, sau đính chính):** đúng +1 dòng; dòng mới ghi đúng nhãn hành động huỷ đơn của Người gửi (KHÔNG phải "Đã huỷ nhận đơn"), kèm **tên người thực hiện** (không ghi vai trò — chấp nhận), lý do "Huy vi trung lich", thời điểm huỷ.
**Actual:** +1 dòng ✅ · lý do ✅ · thời điểm `23:34` ✅ · ghi **tên người** (`Đặng Châu Anh`) — chấp nhận ✅ · ❌ **vẫn sai nhãn hành động:** ghi **"Đã huỷ nhận đơn"** thay vì nhãn của luồng huỷ đơn — đúng nhãn của người vận chuyển huỷ nhận (xem `TC-CNL-010`), người đọc log sẽ hiểu nhầm người vận chuyển là bên huỷ.
> 🔁 **Đính chính 2026-09-22 (QC):** vế "tên thay vai" được **chấp nhận** (app nhất quán ghi tên ở mọi dòng LỊCH SỬ, không phải bug) — `BUG-035` đã xoá, Expected đã sửa. Vế **nhãn hành động sai** vẫn là lỗi **độc lập, chưa được chấp nhận** ⇒ TC này **vẫn FAIL**, giữ `BUG-034` (chờ QC push Jira).
**Evidence:** `screenshots/TC-CNL-009__step8-FAIL-log-nguoi-gui-huy-ghi-nhan-da-huy-nhan-don-khong-co-vai.png` (+ `screenshots/TC-CNL-009__pre-lich-su-truoc-khi-huy-2-dong.png` · `screenshots/TC-CNL-009__pre-popup-huy-don-ly-do-huy-vi-trung-lich.png`) — verified tồn tại
**Ghi chú:** TC ghi *"Dự kiến FAIL — app chỉ hiện banner, không ghi log"* ⇒ app **đã** ghi log (khác dự kiến).

---

## TC-CNL-019: Check chỉ còn đúng 2 đường thoát cho vai Người nhận sau khi đơn đang giao

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | C (`stag_giangdc2@`, người nhận O2) mở Theo dõi đơn (setup) | đăng nhập C → Hoạt động → card `Nhận: … Đang giao` | ✅ | — | khối `NGƯỜI GIAO HÀNG` = Phan Thị Mỹ Anh; chân màn nhãn tắt `Đơn đang trên đường đến bạn` |
| 2 | Rà toàn bộ nút hành động | page source đầu + `scroll_to_element textContains("hoàn hàng")` (không thấy) + page source cuối | ⚠️ **NOT_EVIDENCED** *(nội dung ĐẠT sau đính chính 2026-09-22, ảnh sai slot — lúc chạy chấm ❌ FAIL)* | `TC-CNL-019__step2-FAIL-vai-nguoi-nhan-dang-giao-khong-co-yeu-cau-hoan-hang.png` | Nút bấm được: `Quay lại` · **`Báo cáo sự cố`** · `Copy`×2 · `Gọi người giao hàng`. **Không** nút huỷ ✅ |

**Result: ✅ PASS** *(đính chính nội dung 2026-09-22; evidence đúng slot bổ sung ở Follow-up 2026-09-22 — xem cuối file)*
**Expected (mới):** không còn nút huỷ thường; chỉ còn đúng 1 nút liên quan: "Báo cáo sự cố". Người nhận KHÔNG có nút/route hoàn hàng nào.
**Actual:** chỉ có `Báo cáo sự cố` — đúng như Expected mới, cùng hiện tượng ở cả 3 vai (`017` · `018` · `019`).
> 🔁 **Đính chính nội dung 2026-09-22** — xem đầy đủ ở `TC-CNL-018`. Draft `BUG-033` đã xoá.
> ⚠️ **Evidence:** ảnh gốc mang tên slot `__step2-FAIL` — không đủ cho verdict PASS theo gate. Đã chụp bù ảnh đúng slot `__verify` ở phiên follow-up 2026-09-22 (đọc lại màn Theo dõi đơn hiện tại của O2 vai Receiver) — xem `TC-CNL-019__verify-vai-nguoi-nhan-chi-co-bao-cao-su-co.png`.
**Evidence:** `screenshots/TC-CNL-019__verify-vai-nguoi-nhan-chi-co-bao-cao-su-co.png` (follow-up 2026-09-22) + `screenshots/TC-CNL-019__step2-FAIL-vai-nguoi-nhan-dang-giao-khong-co-yeu-cau-hoan-hang.png` (evidence gốc) — verified tồn tại

---

## TC-CNL-016: Check nút "Báo cáo sự cố" tồn tại cho vai Người nhận khi đơn đang giao

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | C mở Theo dõi đơn của O2 Đang giao (setup) | như `019` | ✅ | — | — |
| 2 | Check góc trên bên phải | find+tap `resourceId("track-report-incident")` | ✅ PASS | `TC-CNL-016__verify-nguoi-nhan-bam-bao-cao-su-co-mo-luong-bao-su-co.png` | nút có ✅ · mở màn `Báo sự cố đơn hàng` ✅ (webview Microsoft `Sign in`) |

**Result: ✅ PASS**
**Evidence:** `screenshots/TC-CNL-016__verify-nguoi-nhan-bam-bao-cao-su-co-mo-luong-bao-su-co.png` — verified tồn tại
**Ghi chú:** đủ 3 vai (`006` · `015` · `016`) đều có nút và mở được. Đã `back`, không gửi gì.

---

## TC-CNL-020: Check đơn ở trạng thái sự cố không tự chuyển hoàn thành

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 0 | Tiền đề: đơn đã ở `INCIDENT` qua luồng báo sự cố (`FR16`) | ⛔ **không dựng được**: `Báo cáo sự cố` mở **webview Microsoft đăng nhập** (form ngoài app, xem `015`/`006`/`016`) — không có luồng trong app đổi trạng thái đơn sang sự cố | 🚫 | — | — |
| 1 | C mở Theo dõi đơn của đơn `INCIDENT` | chỉ mở được O2 ở trạng thái **`Đang giao`** | 🚫 BLOCKED | `TC-CNL-020__step1-BLOCKED-khong-dung-duoc-don-su-co-van-dang-giao.png` | timeline active `Đang giao`, không có nhãn/trạng thái sự cố nào |

**Result: 🚫 BLOCKED at Step 1**
**Reason:** STG không có đường tạo đơn `INCIDENT` từ app — đúng kịch bản TC đã dự báo (*"Verdict đúng khi STG chưa build `INCIDENT`/`FR16` là BLOCKED, ⛔ không đánh PASS"*). Gỡ khi: dev seed 1 đơn `INCIDENT`, hoặc QC gửi thử form báo sự cố (đăng nhập Microsoft) và dev xác nhận form đó có đổi trạng thái đơn.
**Evidence:** `screenshots/TC-CNL-020__step1-BLOCKED-khong-dung-duoc-don-su-co-van-dang-giao.png` — verified tồn tại

---

## Trạng thái dữ liệu cuối phiên

| Đơn | Trạng thái | Ghi chú |
|---|---|---|
| **O1** `anhdc4` · V-City → FPT Cầu Giấy | **Đã huỷ** (bởi người gửi, 23:34) | vẫn hiện ở tab `Đang diễn ra` của A (đúng Expected mới `TC-ACT-015`) |
| **O2** `anhdc4` · FPT Tân Thuận 1 → V-City · người nhận `giangdc2` | **Đang giao** — carrier `anhptm17` | ⚠️ đơn còn mở trên STG. Dùng tiếp được cho `DLV` (giao / hoàn hàng / `TC-DLV-063` để có đơn `RETURNED` cho `TC-ACT-005/015`) |

---

## 🆕 Follow-up 2026-09-22 — chụp bù evidence đúng slot `__verify` cho `TC-CNL-010`/`017`/`018`/`019`

> Bối cảnh: đính chính 2026-09-22 đã xác nhận nội dung 4 TC này ĐẠT theo Expected mới, nhưng ảnh sẵn có của phiên gốc (2026-09-21) mang tên slot `__step*-FAIL` (chụp lúc đang chấm FAIL theo Expected cũ) ⇒ gate `verify_evidence.py` không chấp nhận cho verdict PASS (đòi slot `__verify`). Phiên follow-up này **chỉ đọc lại state hiện tại của O2 (không đổi trạng thái đơn)** để chụp ảnh đúng slot — không cần re-run hành động huỷ/ghép nào, vì log LỊCH SỬ là bất biến (`BR11-03`) và ma trận nút của `Đang giao` không đổi theo thời gian.

> Session mới: `select_device(emulator-5554)` → `appium_session_management(action=create)` — app đang đứng sẵn ở màn "Chi tiết tin" của A (Đặng Châu Anh, giữa chừng phiên trước đó); xác nhận danh tính qua `Cá nhân` trước khi thao tác theo đúng luật `USR-accounts.md §0`.

| # | TC | Vai / Account | Thao tác | Result | Evidence | Notes |
|---|----|----|----|--------|----------|-------|
| 1 | `TC-CNL-017` | A (Người gửi) `stag_anhdc4@` — đã sẵn login | Mở "Đơn của tôi" → `Đang diễn ra` → card O2 (`Đang giao`) → "Chạm để theo dõi đơn của bạn" → cuộn hết trang | ✅ **PASS** | `TC-CNL-017__verify-vai-nguoi-gui-chi-co-bao-cao-su-co.png` | Xác nhận lại: chỉ có `Báo cáo sự cố`, không nút huỷ, không route hoàn hàng nào cho Sender. Cuộn tới cuối trang (LỊCH SỬ + footer) không phát sinh thêm nút nào khác |
| 2 | `TC-CNL-010` | A (cùng phiên, cùng màn) | Cuộn xuống block LỊCH SỬ của O2 | ✅ **PASS** | `TC-CNL-010__verify-lich-su-huy-nhan-giu-nguyen-sau-dinh-chinh.png` | LỊCH SỬ vẫn giữ nguyên 5 dòng như phiên gốc (bất biến, đúng `BR11-03`): `Người mang đã lấy hàng` → `Ghép thành công 23:24` → **`Đã huỷ nhận đơn · 23:22 · Phan Thị Mỹ Anh · Lý do: Doi ca lam viec`** → `Ghép thành công 23:21` → `Đăng tin lên bảng tin 23:16`. Đúng Expected mới: nhãn `Đã huỷ nhận đơn` đúng, tên người (chấp nhận), lý do, đơn không mất dòng cũ |
| 3 | `TC-CNL-018` | B (Người vận chuyển) `stag_anhptm17@` — đăng xuất A → đăng nhập B (OTP cố định, 5 bước theo `USR-accounts.md §0b`) → vào thẳng FoxEco → card O2 vai `Giao` (`Đang giao`) → mở Theo dõi đơn | ✅ **PASS** | `TC-CNL-018__verify-vai-nguoi-van-chuyen-bao-cao-su-co-va-duong-giao-hang.png` | Có `Báo cáo sự cố` + nút `Đã giao cho người nhận` (điểm vào luồng hoàn hàng gián tiếp `FR09`), không nút huỷ. Không có nút riêng "Yêu cầu hoàn hàng" — đúng Expected mới |
| 4 | `TC-CNL-019` | C (Người nhận) `stag_giangdc2@` — đăng xuất B → đăng nhập C → vào FoxEco → card O2 vai `Nhận` (`Đang giao`) → mở Theo dõi đơn | ✅ **PASS** | `TC-CNL-019__verify-vai-nguoi-nhan-chi-co-bao-cao-su-co.png` | Chỉ có `Báo cáo sự cố`, footer nhãn tắt `Đơn đang trên đường đến bạn`. Không route hoàn hàng nào cho Receiver — đúng Expected mới |

**Kết quả follow-up: 4/4 PASS** (đúng như đính chính nội dung 2026-09-22 đã kết luận). Gate `verify_evidence.py` chạy lại sau follow-up: **GATE PASS**, không còn `no_verify`.

**Evidence:** `screenshots/TC-CNL-017__verify-vai-nguoi-gui-chi-co-bao-cao-su-co.png` · `screenshots/TC-CNL-010__verify-lich-su-huy-nhan-giu-nguyen-sau-dinh-chinh.png` · `screenshots/TC-CNL-018__verify-vai-nguoi-van-chuyen-bao-cao-su-co-va-duong-giao-hang.png` · `screenshots/TC-CNL-019__verify-vai-nguoi-nhan-chi-co-bao-cao-su-co.png` — cả 4 verified tồn tại trên đĩa.

Ảnh cũ (`__step*-FAIL` slot, phiên 2026-09-21) **giữ nguyên, không xoá** — vẫn được trích dẫn trong section gốc của từng TC ở trên làm hồ sơ lúc chạy ban đầu.
