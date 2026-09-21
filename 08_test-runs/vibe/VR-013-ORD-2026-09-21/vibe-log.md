# Vibe Test Log — VR-013 — v1.1 (+ CARRIED v1.0) — 2026-09-21

> Module: **ORD — Đăng tin & Quản lý tin** · Platform: **mobile** (Appium MCP / UiAutomator2) · Env: **STG** — host app `com.hrisproject.stag` (FoxPro) → FoxEco · Evidence dir: `screenshots/`
> **2 thiết bị chạy song song bằng 2 session Appium:**
> · **EMU** `emulator-5554` (1080×2400, Android 13) — session `b944ccd4-ceb7-4812-bdc2-864228ca23e8` — **tài khoản A = `Đặng Châu Giang`** (`stag_giangdc2@`) — QC duyệt đổi từ `Nguyễn Thị Thanh Thủy` sang Giang lúc 10:05.
> · **REAL** `R58T20PLP8K` (Samsung SM-A127F, 720×1600) — session `9ffdf4be-b083-4068-b84e-8a19b6d29a9a` — **tài khoản B = `Đặng Châu Anh`** (`stag_anhdc4@`, đăng nhập sẵn, không đổi).
> Phiên: 2026-09-21 (khởi tạo)
> Tập chạy: **theo yêu cầu QC** — (a) 22 TC còn nợ trong `coverage-ORD.md` + (b) TC gắn với bug **chưa push Jira**: `TC-ORD-004` (`BUG-020`) và `TC-ORD-068` (`BUG-019`). Không chạy lại TC đã có verdict cuối. *(⚠️ không dùng `--all`; QC chỉ định tường minh tập chạy.)*
> Evidence chụp bằng `adb exec-out screencap` (tiền lệ VR-004: `appium_screenshot` không có tham số `filename`, trả ~147k ký tự HTML/call). **Locator + mọi thao tác 100% qua MCP.** Ngoại lệ có chủ ý: `TC-ORD-085` dùng **burst screencap** (không có ffmpeg/cv2 để tách khung video).
> 🔑 OTP dùng chung nằm ở biến `FOXECO_STG_PASS` của `~/.foxeco-v2/credentials.env` (⚠️ file **không có** biến `FOXECO_STG_OTP` như CLAUDE.md khai) — không in ra.

---

## TC-ORD-004: Check đăng tin NEED thành công với dữ liệu hợp lệ đầy đủ ba bước — P1 · SC-ORD-004 *(v1.0 CARRIED · 🐞 retest `BUG-020`)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco tài khoản A, `+ Đăng tin`, card `Tôi cần gửi hàng` *(setup)* | find `accessibility id "Đăng tin"` → tap; `descriptionStartsWith("Tôi cần gửi hàng")` → tap | ✅ PASS | — | login Giang trên EMU (xem header) |
| 2 | Chọn loại hàng | tap `accessibility id "Tài liệu"` | ✅ PASS | — | chip nay tên `Tài liệu` (TC ghi `Giấy tờ, hồ sơ` — đã lỗi thời, `C-ORD-09`) |
| 3 | Chọn giá trị `Thấp` + `Dưới 5 kg` + `Nhỏ` + 1 ảnh (`instance(0)` Photo Picker) + ghi chú `Giao gio hanh chinh` | tap ×3 · `scroll_to_element` → tap `multi-photo-add-button` → `Chọn từ thư viện` → thumbnail → `Add (1)` · `set_value` | ✅ PASS | — | bộ đếm `1/5`; **giống hệt payload VR-004** (cả ghi chú) |
| 4 | Nhấn `Tiếp theo` | tap | ✅ PASS | — | sang `Bước 2 / 3` |
| 5 | Nhập email `stag_anhdc4@fpt.com`, rời ô | `set_value` → tap tiêu đề `Bước 2 / 3` (rời ô) | ✅ PASS | — | `Đã tìm thấy trong hệ thống nội bộ` · autofill `Đặng Châu Anh` · `0343439724` · địa chỉ giao **`Tòa V-City, Lê Thái Tổ`** |
| 6 | Địa chỉ lấy hàng: gõ + **chạm gợi ý** | `set_value "Cẩm Lệ"` → tap `address-suggestion-0` | ✅ PASS | — | → `FTEL Đà Nẵng Cẩm Lệ` |
| 7 | Địa chỉ giao: gõ + **chạm gợi ý** | `set_value "Lê Thái Tổ"` → tap `address-suggestion-0` | ✅ PASS | — | → `Tòa V-City, Lê Thái Tổ` |
| 8 | Chọn khung giờ muộn hơn hiện tại | tap `descriptionStartsWith("Chiều")` (giờ máy 10:13 < 13:00) · `Đến ngày` = 22/09 (khoảng 2 ngày, **giống VR-004**) | ✅ PASS | — | `Từ ngày` = `Hôm nay` (21/09) |
| 9 | Nhấn `Tiếp theo` | tap | ✅ PASS | — | sang `Bước 3 / 3` |
| 10 | Tick điều khoản | tap `descriptionStartsWith("Tôi đã đọc và đồng ý")` | ✅ PASS | `TC-ORD-004__pre-buoc-3-tom-tat-truoc-khi-dang.png` | nút `Đăng tin ngay` `enabled=true`; đã `logcat -c` trước khi bấm |
| 11 | Nhấn `Đăng tin ngay` (10:14:43) | tap → `textContains("Đăng tin thành công")` tìm thấy | ✅ PASS | `TC-ORD-004__verify-man-dang-tin-thanh-cong.png` | **không lỗi**; `logcat` 0 dòng `REQ_400`/`Failed to create post` |
| E1 | Tin ở trạng thái `Chờ ghép` khi mở lại từ tab `Hoạt động` | tab `Hoạt động` → card đầu tiên | ✅ PASS | `TC-ORD-004__verify-hoat-dong-tin-vua-dang-cho-ghep.png` | card: `Gửi: Tài liệu \| Giá trị thấp, Chờ ghép, Từ: FTEL Đà Nẵng Cẩm Lệ, Đến: Tòa V-City, Lê Thái Tổ` |

**Result: ✅ PASS (11 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-004__pre-buoc-3-tom-tat-truoc-khi-dang.png` · `screenshots/TC-ORD-004__verify-man-dang-tin-thanh-cong.png` · `screenshots/TC-ORD-004__verify-hoat-dong-tin-vua-dang-cho-ghep.png` — verified tồn tại
**🐞 Ý nghĩa cho `BUG-020`:** **KHÔNG tái hiện** lỗi `REQ_400` ở lần retest này — cùng tài khoản Giang, cùng payload (kể cả ghi chú, khoảng ngày 2 ngày, `FTEL Đà Nẵng Cẩm Lệ`→`Tòa V-City`), khác duy nhất **giờ chạy** (10:14 giờ VN thay vì ~00:20 ngày hôm sau). ⇒ **củng cố giả thuyết "lệch ngày quanh nửa đêm"** của draft `BUG-020` *(chưa xác nhận — cần chạy lại trong khung 00:00–07:00)*; giả thuyết "khác tài khoản" bị **loại** (cùng Giang). 🔒 **Draft `BUG-020` KHÔNG đủ cơ sở để push** — xem `vibe-report.md §Kết luận BUG-020`.
**📝 Ghi nhận phụ:** SĐT người gửi trong tóm tắt = **`0912345670`**, khác `0964633310` ghi ở VR-004/`USR-accounts.md` ⇒ HRIS của Giang đã đổi (không ảnh hưởng verdict).

---

## TC-ORD-039: Check màn Đăng tin thành công không hiển thị mã đơn và có đủ hai nút điều hướng — P2 · SC-ORD-036

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | Đăng nhập, `+ Đăng tin`, nhập đủ dữ liệu 3 bước + ảnh, nhấn `Đăng tin ngay` *(setup)* | **dùng lại đơn đã đăng ở `TC-ORD-004`** (seed dùng chung — `Project_rule §10.3`) | ✅ PASS | — | ⚠️ khai minh bạch: bước đăng của TC này được thực hiện bằng **cùng một lần đăng** với `TC-ORD-004`, không đăng thêm đơn thứ 2 |
| 4 | Check toàn bộ nội dung + các nút trên màn thành công | `get_page_source` (ghi ra file, quét toàn bộ node `text`/`content-desc`) | ✅ PASS | `TC-ORD-039__verify-man-thanh-cong-khong-ma-don-du-2-nut.png` | toàn màn chỉ có 4 nút/chuỗi: `Đăng tin thành công!` · `Tin của bạn đã được đăng lên bảng tin. Chúng tôi sẽ thông báo ngay khi có người nhận mang giúp.` · nút `Theo dõi đơn` · nút `Về trang chủ` ⇒ **0 mã đơn**, đủ **2 nút** |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-039__verify-man-thanh-cong-khong-ma-don-du-2-nut.png` — verified tồn tại

---

## TC-ORD-041: Check màn "Đăng tin thành công" không hiển thị mã tin — P3 · SC-ORD-038 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng 1 tin NEED tới màn thành công *(setup)* | dùng lại đơn của `TC-ORD-004` (seed dùng chung) | ✅ PASS | — | — |
| 2 | Check toàn màn tìm mã tin/mã đơn dạng chuỗi ký tự kèm số | quét mọi node của page source: 0 chuỗi dạng `[A-Z]+-?\d+` | ✅ PASS | `TC-ORD-041__verify-khong-co-ma-tin-trong-noi-dung.png` | ảnh = **crop vùng tiêu đề + câu thông báo** của 1 lần chụp (khác ảnh của `004`/`039`/`040` về byte và về vùng chứng minh) |

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-041__verify-khong-co-ma-tin-trong-noi-dung.png` — verified tồn tại

---

## TC-ORD-049: Check block Lịch sử của tin vừa đăng có mốc đăng tin kèm timestamp — P2 · SC-ORD-046 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng 1 tin NEED, ghi lại thời điểm bấm `Đăng tin ngay` *(setup)* | đơn của `TC-ORD-004`, bấm lúc **10:14:43** (đồng hồ host = đồng hồ máy) | ✅ PASS | — | — |
| 2 | Nhấn `Theo dõi đơn` trên màn thành công | tap `accessibility id "Theo dõi đơn"` | ✅ PASS | — | — |
| 3 | Mở block `Lịch sử` | `scroll_to_element` `textContains("LỊCH SỬ")` — block **hiện sẵn**, không cần bấm mở | ✅ PASS | — | — |
| 4 | Check các mốc + timestamp | đọc node | ✅ PASS | `TC-ORD-049__verify-lich-su-moc-dang-tin-10-14.png` | mốc `Đăng tin lên bảng tin` · `Hôm nay · 10:14 · Đặng Châu Giang` ⇒ khớp **10:14** |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-049__verify-lich-su-moc-dang-tin-10-14.png` — verified tồn tại

---

## TC-ORD-085: Check icon copy cạnh địa chỉ giao ở chi tiết tin sao chép đúng nội dung — P3 · SC-ORD-064 *(♻️ QC reset 2026-09-21)*

> ⚠️ **Phương pháp đo (đúng chỉ dẫn QC — "đừng suy từ ảnh rời")**: đặt sentinel clipboard → khởi động **burst `adb exec-out screencap` (~4 khung/s) TRƯỚC khi tap** → tap icon bằng MCP → đọc clipboard → dò pixel chip xanh từng khung. Ffmpeg/cv2 không có nên không tách khung từ `screenrecord`.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng NEED có địa chỉ giao; mở chi tiết tin *(setup)* | đơn của `TC-ORD-004` → `Hoạt động` → card `Chờ ghép` → màn `Theo dõi đơn` | ✅ PASS | — | — |
| 3 | Ghi lại địa chỉ giao đang hiển thị | `get_text` | ✅ PASS | — | `Tòa V-City, Lê Thái Tổ` |
| 4 | Nhấn icon copy cạnh địa chỉ giao | `clipboard set "SENTINEL-TC085-CHUA-COPY"` → find `description("Copy").instance(1)` → tap *(đang burst)* | ✅ PASS | — | — |
| 5a | Nội dung sao chép đúng nguyên văn | `appium_mobile_clipboard(get)` → **`Tòa V-City, Lê Thái Tổ`** (sentinel đã bị ghi đè) | ✅ PASS | — | ⚠️ đọc bằng API clipboard thay vì "dán vào ô tìm kiếm Bảng tin" — điểm kiểm tương đương, không có ô dán thì cũng đọc được |
| 5b | Icon đổi sang **xanh khoảng 2 giây** rồi trở lại | burst 26 khung, dò pixel xanh `(11,215,140)`: **chip `✓ Đã copy` xanh có mặt ở f14–f20 (t=3.28→4.86 s), khung f13 (3.01 s) và f21 (5.13 s) là icon xám** ⇒ thời lượng **1.58–2.12 s** | ✅ PASS | `TC-ORD-085__verify-chip-da-copy-xanh-khi-vua-bam.png` · `TC-ORD-085__verify-icon-tro-lai-xam-sau-2s.png` | dạng phản hồi = **chip xanh `✓ Đã copy` thay thế icon** (không phải đổi màu icon) — `BR18-04` |

**Result: ✅ PASS (5 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-085__verify-chip-da-copy-xanh-khi-vua-bam.png` · `screenshots/TC-ORD-085__verify-icon-tro-lai-xam-sau-2s.png` — verified tồn tại
**🔎 Đối chiếu ứng viên bug B8 (đã rút 2026-09-21):** xác nhận **không phải bug** — 2 khung cách nhau ~1,8 s bằng `adb screencap` rời đúng là dễ hụt cửa sổ ~2 s. ⇒ `DLV-080/081` (*"icon copy không đổi màu"*, VR-012) nhiều khả năng cùng nguyên nhân **âm tính giả** — nên chạy lại bằng burst.

---

## TC-ORD-060: Check huỷ chỉnh sửa trả tin về dữ liệu cũ và không lưu thay đổi — P2 · SC-ORD-043

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng 1 tin NEED để ở `Chờ ghép` *(setup)* | đơn của `TC-ORD-004` | ✅ PASS | — | — |
| 2 | Mở tin từ `Hoạt động`, ghi lại địa chỉ giao | `get_text` ô `Địa chỉ giao hàng` khi vào form sửa | ✅ PASS | — | ghi lại: **`Tòa V-City, Lê Thái Tổ`** |
| 3 | Nhấn `Chỉnh sửa` | tap `resourceId("track-edit-post")` | ✅ PASS | — | form nạp sẵn dữ liệu, `Bước 1 / 3`, nút `Huỷ chỉnh sửa` (`post-nN-cancel-edit`, N = bước) |
| 4 | Nhập địa chỉ giao khác `Số 99 Cầu Giấy` | `Tiếp theo` → `set_value` ô `Địa chỉ giao hàng` | ✅ PASS | `TC-ORD-060__pre-nhap-so-99-cau-giay-truoc-khi-huy.png` | — |
| 5 | Nhấn `Huỷ chỉnh sửa` | tap `accessibility id "Huỷ chỉnh sửa"` → **popup xác nhận** *"Thay đổi chưa lưu sẽ bị mất. Bạn muốn huỷ chỉnh sửa?"* [`Tiếp tục sửa` / `Huỷ chỉnh sửa`] → tap `dialog-confirm-button` | ✅ PASS | `TC-ORD-060__pre-popup-xac-nhan-huy-chinh-sua.png` | 🔎 TC không mô tả popup này — chức năng **có** popup xác nhận (khác hẳn thoát wizard tạo mới `FE-302`) |
| 6 | Check địa chỉ giao của tin | về `Hoạt động` → mở card → `text("Tòa V-City, Lê Thái Tổ")` | ✅ PASS | `TC-ORD-060__verify-dia-chi-giao-giu-nguyen-sau-huy-sua.png` | giữ nguyên `Tòa V-City, Lê Thái Tổ`, **không** nhận `Số 99 Cầu Giấy` |

**Result: ✅ PASS (6 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-060__pre-nhap-so-99-cau-giay-truoc-khi-huy.png` · `screenshots/TC-ORD-060__pre-popup-xac-nhan-huy-chinh-sua.png` · `screenshots/TC-ORD-060__verify-dia-chi-giao-giu-nguyen-sau-huy-sua.png` — verified tồn tại

---

## TC-ORD-046: Check sửa tin đang chờ ghép lưu được dữ liệu mới và giữ nguyên trạng thái — P2 · SC-ORD-043

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng NEED `Chờ ghép`, mở từ `Hoạt động` *(setup)* | đơn của `TC-ORD-004` | ✅ PASS | — | — |
| 3 | Nhấn `Chỉnh sửa` | tap `track-edit-post` | ✅ PASS | — | — |
| 4 | Check dữ liệu đang nạp trong form | page source | ✅ PASS | — | nạp đủ: loại hàng, ghi chú `Giao gio hanh chinh`, chip giá trị/trọng lượng, email + tên + SĐT + địa chỉ giao `Tòa V-City, Lê Thái Tổ` |
| 5 | Nhập địa chỉ giao mới **`Số 9 Duy Tân`** | `set_value` → **`Tiếp theo` `enabled=false`** (không có gợi ý nào cho `Số 9 Duy Tân` **và** `Duy Tân`) → 🔁 **đổi dữ liệu test:** gõ `Cầu Giấy` → tap `address-suggestion-0` → ô = **`FPT Cầu Giấy`** | ✅ PASS | `TC-ORD-046__pre-dia-chi-giao-moi-fpt-cau-giay.png` | ⚠️ **Test Data của TC KHÔNG dùng được**: địa chỉ tự do không thể lưu (bẫy **T11** — bắt buộc chọn gợi ý). QC nên sửa cột Test Data thành 1 địa chỉ có trong danh mục gợi ý (cho phép sửa theo `Project_rule §10.5`) |
| 6 | Nhấn `Cập nhật` | `Tiếp theo` → `Bước 3/3` → tap `accessibility id "Cập nhật đơn"` → popup **`Đã lưu — Đã cập nhật tin đăng.`** → tap `Đồng ý` | ✅ PASS | `TC-ORD-046__pre-popup-da-luu-da-cap-nhat-tin-dang.png` | — |
| 7 | Check địa chỉ giao + trạng thái | màn `Theo dõi đơn`: `Giao hàng` = **`FPT Cầu Giấy`**; còn dòng `Đang chờ người vận chuyển nhận đơn` + nút `Chỉnh sửa` | ✅ PASS | `TC-ORD-046__verify-dia-chi-moi-fpt-cau-giay-van-cho-ghep.png` | địa chỉ mới đã lưu, vẫn `Chờ ghép` |

**Result: ✅ PASS (7 steps, 1 expected)** — *(với Test Data đã điều chỉnh — xem step 5)*
**Evidence:** `screenshots/TC-ORD-046__pre-dia-chi-giao-moi-fpt-cau-giay.png` · `screenshots/TC-ORD-046__pre-popup-da-luu-da-cap-nhat-tin-dang.png` · `screenshots/TC-ORD-046__verify-dia-chi-moi-fpt-cau-giay-van-cho-ghep.png` — verified tồn tại

---

## TC-ORD-038: Check đăng tin với loại hàng "Thuốc/Y tế" vẫn thành công ở phiên bản v1.0 — P3 · SC-ORD-035 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập tài khoản A, `+ Đăng tin`, card `Tôi cần gửi hàng` *(setup)* | tap `Đăng tin` → tap card | ✅ PASS | — | — |
| 2-4 | Chip `Thuốc/Y tế` · giá trị `Thấp` · (bổ sung 3 trường v1.1: `Dưới 5 kg` + `Nhỏ` + 1 ảnh) → `Tiếp theo` | tap `accessibility id "Thuốc/Y tế"`; `resourceId("value-tier-chip-option-low")` · `("weight-tier-chip-option-light")` · `("size-tier-chip-option-small")` ⇒ **3 resource-id nay resolve được** (VR-002 ghi ⚠️ Inferred) | ✅ PASS | `TC-ORD-038__pre-buoc-1-loai-hang-thuoc-y-te.png` | TC v1.0 chưa biết 3 trường bắt buộc mới — step 2–4 bổ sung, không ảnh hưởng điểm kiểm |
| 5-6 | Nhập email người nhận `stag_anhdc4@fpt.com` + 2 địa chỉ (chạm gợi ý) + buổi `Giờ nào cũng được` → `Tiếp theo` | `set_value` → tap `Bước 2 / 3` (rời ô) → `address-suggestion-0` ×2 → chip buổi | ✅ PASS | — | — |
| 7 | Tick điều khoản | tap `descriptionStartsWith("Tôi đã đọc và đồng ý")` | ✅ PASS | `TC-ORD-038__pre-buoc-3-tom-tat-thuoc-y-te-truoc-khi-dang.png` | tóm tắt hiện `Thuốc/Y tế · Giá trị thấp` + banner hàng cấm |
| 8 | Nhấn `Đăng tin ngay` | tap → `textContains("Đăng tin thành công")` | ✅ PASS | `TC-ORD-038__verify-thuoc-y-te-dang-thanh-cong-khong-bi-chan.png` | đăng được, **không bị chặn vì loại hàng** (banner hàng cấm chỉ là thông tin tĩnh — `C-ORD-04`); logcat 0 lỗi |

**Result: ✅ PASS (8 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-038__pre-buoc-1-loai-hang-thuoc-y-te.png` · `screenshots/TC-ORD-038__pre-buoc-3-tom-tat-thuoc-y-te-truoc-khi-dang.png` · `screenshots/TC-ORD-038__verify-thuoc-y-te-dang-thanh-cong-khong-bi-chan.png` — verified tồn tại

---

## TC-ORD-040: Check màn "Đăng tin thành công" có hai lựa chọn điều hướng đúng đích — P2 · SC-ORD-037 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng 1 tin NEED tới màn `Đăng tin thành công` *(setup)* | đơn của `TC-ORD-004` (seed dùng chung) | ✅ PASS | — | — |
| 2 | Check các lựa chọn trên màn | page source: đúng **2** ViewGroup `clickable` — `Theo dõi đơn` · `Về trang chủ` | ✅ PASS | `TC-ORD-040__verify-dung-2-lua-chon-theo-doi-don-va-ve-trang-chu.png` | ảnh = crop vùng 2 nút |
| 3 | Nhấn `Theo dõi đơn` | tap → màn `Theo dõi đơn` của **đúng tin vừa đăng** (`Từ FTEL Đà Nẵng Cẩm Lệ → Tòa V-City`, ghi chú `Giao gio hanh chinh`, `Chờ ghép`) | ✅ PASS | `TC-ORD-040__verify-buoc-3-mo-man-theo-doi-don-tin-vua-dang.png` | — |
| 4 | Quay lại, đăng thêm 1 tin NEED tới màn thành công | đơn thứ 2 = đơn của `TC-ORD-038` (Thuốc/Y tế, seed dùng chung) | ✅ PASS | — | ⚠️ khai minh bạch: tin thứ 2 chính là tin của `TC-ORD-038` |
| 5 | Nhấn `Về trang chủ` | tap `accessibility id "Về trang chủ"` → Trang chủ | ✅ PASS | `TC-ORD-040__verify-buoc-5-ve-trang-chu-tab-trang-chu-active.png` | tab `Trang chủ` active: quét pixel cam vùng bottom nav = **482 px ở `Trang chủ`, 0 ở 3 tab còn lại** (T1: `selected` không expose) |

**Result: ✅ PASS (5 steps, 3 expected)**
**Evidence:** `screenshots/TC-ORD-040__verify-dung-2-lua-chon-theo-doi-don-va-ve-trang-chu.png` · `screenshots/TC-ORD-040__verify-buoc-3-mo-man-theo-doi-don-tin-vua-dang.png` · `screenshots/TC-ORD-040__verify-buoc-5-ve-trang-chu-tab-trang-chu-active.png` — verified tồn tại

---

## TC-ORD-065: Check chọn Trọng lượng trên mười kg vẫn đăng tin được bình thường — P2 · SC-ORD-052

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập, `+ Đăng tin`, card `Tôi cần gửi hàng` *(setup)* | tap | ✅ PASS | — | — |
| 2 | Chọn `Thấp` + `Nhỏ · Cầm tay` + tải ảnh JPG *(setup)* | `resourceId("value-tier-chip-option-low")` · `("size-tier-chip-option-small")` · photo picker | ✅ PASS | — | ⚠️ tải **5 ảnh** (thay vì 1) để đơn này dùng làm tiền đề cho `TC-ORD-072/073/088` (seed dùng chung) — số ảnh không phải điểm kiểm của TC này |
| 3 | Chọn chip `Trên 10 kg (Nặng)` | tap `resourceId("weight-tier-chip-option-heavy")` | ✅ PASS | `TC-ORD-065__pre-chon-tren-10-kg-nang-du-du-lieu-buoc-1.png` | chip cam đang chọn; **không có banner cảnh báo nào** xuất hiện ở bước 1 |
| 4 | `Tiếp theo`, nhập đủ dữ liệu bước 2, 3, `Đăng tin ngay` | email + 2 địa chỉ chạm gợi ý + buổi `Giờ nào cũng được` + khối uỷ quyền (của `TC-ORD-080`) + tick → tap `Đăng tin ngay` (10:41) | ✅ PASS | — | ⚠️ đơn này **đồng thời** mang dữ liệu uỷ quyền của `TC-ORD-080` (gộp seed) — logcat 0 lỗi |
| 5 | Check màn hiện ra sau khi đăng | `textContains("Đăng tin thành công")` | ✅ PASS | `TC-ORD-065__verify-tren-10-kg-dang-thanh-cong-khong-canh-bao.png` | đăng thành công, không cảnh báo/chặn vì trọng lượng. Màn Theo dõi đơn + chi tiết tin hiển thị `Nặng (> 10 kg)` đúng |

**Result: ✅ PASS (5 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-065__pre-chon-tren-10-kg-nang-du-du-lieu-buoc-1.png` · `screenshots/TC-ORD-065__verify-tren-10-kg-dang-thanh-cong-khong-canh-bao.png` — verified tồn tại

---

## TC-ORD-072: Check dải ảnh ở chi tiết tin lướt ngang được và có badge đếm ảnh — P3 · SC-ORD-057

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng 1 tin NEED kèm 5 ảnh *(setup)* | đơn `P3` của `TC-ORD-065` (đủ **5 ảnh**, badge `5 ảnh`) | ✅ PASS | — | — |
| 2 | `Hoạt động` → mở tin vào màn chi tiết *(setup)* | tap `Theo dõi đơn` từ màn thành công | ✅ PASS | — | — |
| 3 | Lướt ngang dải ảnh sang ảnh thứ hai | `descriptionStartsWith("Xem ảnh")` → `appium_gesture(swipe, left, elementUUID)` | ✅ PASS | — | — |
| 4 | Check ảnh đang hiển thị + badge | `find text("2/5")` OK | ✅ PASS | `TC-ORD-072__verify-dai-anh-luot-sang-anh-2-badge-2-tren-5.png` | badge **`2/5`**, ảnh chuyển từ đỏ (1/5) sang xanh lam (2/5) |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-072__verify-dai-anh-luot-sang-anh-2-badge-2-tren-5.png` — verified tồn tại

---

## TC-ORD-073: Check lightbox ảnh đóng được bằng cả nút đóng lẫn chạm nền — P3 · SC-ORD-057

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng NEED 5 ảnh, mở chi tiết *(setup)* | đơn `P3` | ✅ PASS | — | — |
| 3 | Nhấn 1 ảnh để mở lightbox | tap `descriptionStartsWith("Xem ảnh")` | ✅ PASS | `TC-ORD-073__pre-lightbox-mo-lan-1.png` | lightbox **nền đen**, ảnh giữ tỉ lệ, badge `2/5`, 5 chấm, nút × góc trái trên |
| 4 | Nhấn nút đóng | tap `(//android.view.ViewGroup[@clickable="true"])[1]` (nút ×) → về màn `Theo dõi đơn` | ✅ PASS | `TC-ORD-073__pre-da-dong-bang-nut-dong-ve-chi-tiet-tin.png` | đóng được bằng nút ✓ |
| 5 | Nhấn lại ảnh để mở lightbox lần hai | tap | ✅ PASS | `TC-ORD-073__pre-lightbox-mo-lan-2.png` | — |
| 6 | Nhấn vùng nền tối ngoài ảnh | `appium_gesture(tap)` toạ độ tại **5 điểm khác nhau**: `(540,225)` thanh trên · `(540,380)` dải đen phía trên ảnh · `(540,2050)` · `(540,2190)` · `(540,2350)` dải đen phía dưới ảnh; + `(540,1200)` giữa ảnh | ✅ **PASS** *(QC xác nhận)* | `TC-ORD-073__verify-cham-nen-toi-khong-dong-lightbox.png` | **lightbox KHÔNG đóng** sau cả 6 lần tap (sau mỗi lần `find text("Theo dõi đơn")` → NOT FOUND) — nay là hành vi **đúng** (chỉ đóng bằng ×) |
| 7 | Check màn đang hiển thị sau lần đóng bằng nút và sau khi chạm nền tối | — | ✅ PASS | `TC-ORD-073__verify-cham-nen-toi-khong-dong-lightbox.png` | nút × đóng được; chạm nền không đóng — khớp Expected mới |

**Result: ✅ PASS** *(QC override 2026-09-21)* — quan sát gốc: chạm nền không đóng lightbox. QC GiangDC2 kiểm lại 2026-09-21: **app đúng, không phải bug** (chỉ đóng bằng nút ×); Expected của `TC-ORD-073` đã sửa theo app.
**Đối chứng loại trừ lỗi phương pháp:** (a) tap **toạ độ** `(90,215)` đúng nút × ⇒ **đóng được** ⇒ tap toạ độ có hiệu lực; (b) **máy thật** `R58T20PLP8K` (phía người xem `Chi tiết tin`, `Chạm (360,1400)` vào dải đen dưới ảnh) ⇒ **lightbox vẫn mở** (ảnh ở `_recon`-không chụp riêng; xác nhận bằng `find text("Chi tiết tin")` NOT FOUND + screenshot xem trực tiếp) ⇒ **tái hiện trên 2 thiết bị, 2 màn**.
**Evidence:** `screenshots/TC-ORD-073__pre-lightbox-mo-lan-1.png` · `screenshots/TC-ORD-073__pre-da-dong-bang-nut-dong-ve-chi-tiet-tin.png` · `screenshots/TC-ORD-073__pre-lightbox-mo-lan-2.png` · `screenshots/TC-ORD-073__verify-cham-nen-toi-khong-dong-lightbox.png` — verified tồn tại
**🗑️ `BUG-024` đã huỷ** — QC GiangDC2 kiểm lại 2026-09-21: **app đúng, không phải bug**. Không log Jira.

---

## TC-ORD-088: Check không xoá được ảnh của tin đã đăng — P3 · SC-ORD-065

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Đăng NEED kèm ≥2 ảnh, mở tin *(setup)* | đơn `P3` (**5 ảnh**, `Chờ ghép`) — ⚠️ TC ghi 2 ảnh; dùng 5 ảnh vì cùng seed với `072`/`073` | ✅ PASS | — | điểm kiểm (xoá ảnh sau khi đăng) không phụ thuộc số ảnh |
| 3 | Nhấn `Chỉnh sửa` để mở form sửa | tap `resourceId("track-edit-post")` → `scroll_to_element textStartsWith("ẢNH HÀNG")` | ✅ PASS | — | form sửa nạp đủ 5 ảnh |
| 4 | Nhấn giữ ảnh thứ nhất, tìm thao tác xoá | `long_press` 1.5 s vào ảnh 1 → **mở lightbox** (không có menu xoá; `textContains("Xoá")` NOT FOUND). Sau đó thử nút **`×` trên ảnh** (`resourceId("multi-photo-remove-0")` **tìm thấy + tap được**) | ✅ **PASS** *(QC xác nhận)* | `TC-ORD-088__pre-nhan-giu-anh-1-cua-tin-da-dang-khong-co-menu-xoa.png` | ảnh = lightbox mở ra sau khi nhấn giữ. **Nút `×` xoá ảnh HIỆN và HOẠT ĐỘNG** trên ảnh của tin đã đăng — nay là hành vi **đúng** |
| 5 | Check số ảnh của tin sau khi thử xoá | (a) trong form: ảnh đỏ biến mất, nút thêm ảnh hiện `accessibility id "4/5"` · (b) **lưu** (`Tiếp theo` ×2 → `Cập nhật đơn` → `Đồng ý`) → mở lại đơn: badge **`4 ảnh`** *(`text("4 ảnh")` tìm thấy)* | ✅ **PASS** *(QC xác nhận)* | `TC-ORD-088__verify-xoa-duoc-anh-cua-tin-da-dang-con-4-tren-5.png` · `TC-ORD-088__verify-sau-khi-luu-don-chi-con-4-anh.png` | Expected cũ `KHÔNG có thao tác xoá…` đã sửa theo app: xoá **được ghi vào đơn** (5 → 4) là hành vi đúng |

**Result: ✅ PASS** *(QC override 2026-09-21)* — quan sát gốc: ảnh của tin đã đăng xoá được và việc xoá được lưu (5 → 4). QC GiangDC2 kiểm lại 2026-09-21: **app đúng, không phải bug**; Expected + Steps của `TC-ORD-088` đã sửa theo app.
**Evidence:** `screenshots/TC-ORD-088__pre-nhan-giu-anh-1-cua-tin-da-dang-khong-co-menu-xoa.png` · `screenshots/TC-ORD-088__verify-xoa-duoc-anh-cua-tin-da-dang-con-4-tren-5.png` · `screenshots/TC-ORD-088__verify-sau-khi-luu-don-chi-con-4-anh.png` — verified tồn tại
**🗑️ `BUG-023` đã huỷ** — QC GiangDC2 kiểm lại 2026-09-21: **app đúng, không phải bug**. Không log Jira. ⚠️ Tác dụng phụ trên STG: đơn `P3` còn **4 ảnh** (do test). Nhóm `SC-CNL-010`/`SC-DLV-062` (ảnh bất biến truy vết) chưa chạy — nên hỏi BA cách hiểu `BR18-05`/`BR11-03`/`NFR-07` trước khi chạy.

---

## TC-ORD-083: Check địa chỉ giao trùng hệt địa chỉ lấy bị chặn — P2 · SC-ORD-063 *(♻️ QC reset 2026-09-21)*

> ⚠️ **Phương pháp (đúng chỉ dẫn QC — validate on-blur `VAL-02`):** mọi lần nhập/sửa đều có **bước rời ô riêng**; ô SĐT/địa chỉ được rời bằng cách **chuyển focus sang ô nhập khác** (⛔ không tin `hideKeyboard`). Kiểm **cả 2 đường nhập địa chỉ** như QC yêu cầu.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập, `+ Đăng tin`, card `Tôi cần gửi hàng`, nhập đủ trường bước 1 rồi `Tiếp theo` *(setup)* | `Tài liệu`·`Thấp`·`Dưới 5 kg`·`Nhỏ`·1 ảnh | ✅ PASS | — | — |
| 2-3a | **Đường A — gõ tay:** nhập `Số 7 ngõ 12 Trần Duy Hưng` vào cả 2 ô địa chỉ | `set_value` ×2 · **rời ô** sau mỗi lần (tap tiêu đề `Bước 2 / 3`) · chọn buổi `Giờ nào cũng được` để cô lập điều kiện | ✅ PASS | — | — |
| 4-5a | `Tiếp theo` → đọc màn/lỗi | `Tiếp theo` **`enabled=false`**; `textContains("phải khác")` → **NOT FOUND**; ảnh chụp: không dòng lỗi nào dưới ô giao | ⚠️ *(quan sát, không chốt verdict)* | `TC-ORD-083__pre-go-tay-2-dia-chi-trung-da-roi-o-tiep-theo-khoa-khong-loi.png` | **gõ tay ⇒ nút khoá + KHÔNG lỗi** (T11: địa chỉ phải chạm gợi ý). Cùng họ chặn-im-lặng của `FE-301` |
| 2-3b | **Đường B — chạm gợi ý:** lấy = `FTEL Đà Nẵng Cẩm Lệ` (gõ `Cẩm Lệ` → tap `address-suggestion-0`); giao = **cùng gợi ý** đó | `set_value "Cẩm Lệ"` → `address-suggestion-0` → tap (×2 ô) → rời ô | ✅ PASS | `TC-ORD-083__pre-chon-goi-y-2-o-cung-ftel-cam-le-chua-bam-tiep-theo.png` | trước khi bấm: **chưa có lỗi**, `Tiếp theo` `enabled=true` |
| 4b | Nhấn `Tiếp theo` | tap | ✅ PASS | — | không sang `Bước 3 / 3` (find NOT FOUND) |
| 5b | Check màn + lỗi ở ô giao | `text("Địa chỉ giao phải khác địa chỉ lấy hàng")` **tìm thấy** | ✅ PASS | `TC-ORD-083__verify-chon-goi-y-trung-o-lai-buoc-2-hien-loi-dia-chi-giao-phai-khac.png` | wizard ở **Bước 2**, lỗi đỏ ngay **dưới ô giao** |

**Result: ✅ PASS (đường B — chạm gợi ý)** · ⚠️ **đường A (gõ tay đúng chữ trong Steps) không cho ra lỗi** — Test Data `Số 7 ngõ 12 Trần Duy Hưng` **không phải giá trị hợp lệ để chạm gợi ý** ⇒ QC nên đổi cột Test Data sang địa chỉ có trong danh mục gợi ý (được phép sửa theo `Project_rule §10.5`). *Verdict PASS dựa trên đường B; nếu QC coi gõ tay là đường bắt buộc ⇒ đổi thành ❌ FAIL (cùng gốc chặn-im-lặng).*
**Evidence:** `screenshots/TC-ORD-083__pre-go-tay-2-dia-chi-trung-da-roi-o-tiep-theo-khoa-khong-loi.png` · `screenshots/TC-ORD-083__pre-chon-goi-y-2-o-cung-ftel-cam-le-chua-bam-tiep-theo.png` · `screenshots/TC-ORD-083__verify-chon-goi-y-trung-o-lai-buoc-2-hien-loi-dia-chi-giao-phai-khac.png` — verified tồn tại
**🔎 Đối chiếu ứng viên bug cũ *"lỗi validate không tự xoá khi đã sửa input"*:** sau khi lỗi trùng hiện, đổi ô giao sang gợi ý khác (`Tòa V-City, Lê Thái Tổ`) + chuyển focus sang ô khác (blur thật, `keyboardShown=false`) ⇒ **lỗi đỏ VẪN hiện** và `Tiếp theo` **`enabled=true`**; bấm `Tiếp theo` vẫn sang Bước 3 rồi **quay lại thì lỗi đã mất**. ⇒ với blur thật, hiện tượng **vẫn còn** (lỗi chỉ được xoá khi submit thành công, không phải khi blur). *Không kết luận bug ở đây — chờ QC đối chiếu `VAL-02` có bắt buộc xoá lỗi lúc blur không.*

---

## TC-ORD-084: Check địa chỉ giao chỉ khác khoảng trắng đầu cuối vẫn bị chặn — P2 · SC-ORD-063 *(♻️ QC reset 2026-09-21)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Vào Bước 2, nhập địa chỉ lấy `FTEL Đà Nẵng Cẩm Lệ` (chạm gợi ý) *(setup)* | như `TC-ORD-083` (đợt sạch: đã thoát lỗi cũ bằng `Quay lại` từ Bước 3) | ✅ PASS | — | — |
| 3 | Nhập chuỗi có **khoảng trắng đầu/cuối** vào ô giao | 2 đường: **(A)** gõ tay `  Số 7 ngõ 12 Trần Duy Hưng  ` → cùng hành vi `083` đường A (nút khoá, không lỗi). **(B)** chạm gợi ý `FTEL Đà Nẵng Cẩm Lệ` **rồi** `set_value "  FTEL Đà Nẵng Cẩm Lệ  "` (đọc lại `get_text` = chuỗi có 2 space đầu + 2 space cuối ✓) → chuyển focus sang ô tên | ✅ PASS | `TC-ORD-084__pre-da-chon-goi-y-roi-them-khoang-trang-loi-cu-con-sot.png` | ⚠️ ảnh này chụp ở lượt thử đầu (lỗi cũ từ lần bấm trước còn sót) — **không** dùng để kết luận; kết luận lấy từ đợt sạch bên dưới |
| 4 | Nhấn `Tiếp theo` | `Tiếp theo` **`enabled=false`** ⇒ **không bấm được** | 🚫 **BLOCKED** | — | thêm khoảng trắng ⇒ **mất trạng thái "đã chọn gợi ý"** ⇒ nút khoá (luật chọn-gợi ý, không phải luật trùng) |
| 5 | Check màn + lỗi ở ô giao | `textContains("phải khác")` **NOT FOUND**; ảnh: không dòng lỗi | 🚫 **BLOCKED** | `TC-ORD-084__step5-BLOCKED-them-khoang-trang-mat-goi-y-nut-khoa-khong-co-loi.png` | **không dựng được điều kiện** để luật *"trùng sau khi trim"* được đánh giá |

**Result: 🚫 BLOCKED at Step 4–5** — *không thể vừa giữ trạng thái đã-chọn-gợi ý vừa thêm khoảng trắng đầu/cuối; luật so sánh có-trim không có đường UI để chạy.* Đổi từ ❌ FAIL (VR-004) sang 🚫 BLOCKED vì nguyên nhân là **thiết kế TC không thực thi được**, không phải app sai luật trùng. ⛔ **không log bug.** 📨 QC quyết: `DESCOPED` hoặc viết lại TC (vd đổi sang so sánh hoa/thường hoặc khoảng trắng **giữa** chuỗi). Điểm ghi nhận cho `/analyze-requirements`: `SC-ORD-063` chưa quy định UI có trim/so sánh trước khi chọn gợi ý hay không.
**Evidence:** `screenshots/TC-ORD-084__pre-da-chon-goi-y-roi-them-khoang-trang-loi-cu-con-sot.png` · `screenshots/TC-ORD-084__step5-BLOCKED-them-khoang-trang-mat-goi-y-nut-khoa-khong-co-loi.png` — verified tồn tại

---

## TC-ORD-052: Check hệ thống cắt khoảng trắng tên và chuẩn hoá SĐT khi lưu — P3 · SC-ORD-049 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập, `+ Đăng tin`, card NEED, chọn loại/giá trị, `Tiếp theo` *(setup)* | như trên | ✅ PASS | — | — |
| 2 | Nhập tên người nhận có khoảng trắng đầu/cuối, rời ô | `set_value "   Nguyễn Văn An   "` vào `resourceId("receiver-name-input")` | ✅ PASS | — | — |
| 3 | Nhập SĐT `090 123.4567`, rời ô | `set_value` vào `resourceId("receiver-phone-input")` → tap ô tên (rời ô) | ✅ PASS | `TC-ORD-052__pre-ten-co-khoang-trang-va-sdt-090-123-4567.png` | ô SĐT **vẫn giữ nguyên** `090 123.4567` sau khi rời ô (chuẩn hoá không diễn ra tại ô — chỉ ở tóm tắt) |
| 4-5 | Nhập đủ 2 địa chỉ + khung giờ hợp lệ, `Tiếp theo` | `Tòa V-City, Lê Thái Tổ` (chạm gợi ý) + `FTEL Đà Nẵng Cẩm Lệ` + buổi `Giờ nào cũng được` | ✅ PASS | — | `Bước 3 / 3` hiện ra |
| 6 | Check phần tóm tắt bước 3 | `textContains("Nguyễn Văn An")` → `get_text` = **`Nguyễn Văn An · 0901234567`** | ✅ PASS | `TC-ORD-052__verify-tom-tat-ten-da-trim-sdt-chi-con-chu-so.png` | tên **không còn** khoảng trắng đầu/cuối (chỉ 1 space quanh dấu `·`); SĐT **chỉ còn 10 chữ số**, không space/dấu chấm |

**Result: ✅ PASS (6 steps, 1 expected)** — *(⚠️ không đăng tin; "khi lưu" được đo ở tóm tắt bước 3 đúng như Expected)*
**Evidence:** `screenshots/TC-ORD-052__pre-ten-co-khoang-trang-va-sdt-090-123-4567.png` · `screenshots/TC-ORD-052__verify-tom-tat-ten-da-trim-sdt-chi-con-chu-so.png` — verified tồn tại

---

## TC-ORD-068: Check ảnh vượt năm MB bị từ chối và bộ đếm không tăng — P2 · SC-ORD-055 *(🐞 gắn với draft `BUG-019`)*

> 🧪 **Test data dựng riêng (đo được dung lượng byte chính xác, đúng đề xuất "thử 3 dung lượng" của draft BUG-019):** ảnh JPG hợp lệ đệm `\x00` tới kích thước đích rồi `adb push` + quét media + `touch -t` để **nhận diện trong Photo Picker bằng timestamp trong `content-desc`** (không phải đoán `instance(N)`):
> `F1` 4.800.000 B (chưa dùng) · **`F2` 5.242.880 B = đúng 5 MiB** (`11:10:02`) · **`F3` 6.291.456 B = 6 MiB** (`11:10:01`) · **`F4` 5.600.000 B ≈ 5,6 MB** (`11:10:04`).

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập, `+ Đăng tin`, card `Tôi cần gửi hàng` *(setup)* | ở Bước 1, xoá ảnh cũ → bộ đếm `accessibility id "0/5"` | ✅ PASS | — | — |
| 2 | Nhấn vùng `ẢNH HÀNG`, chọn ảnh > 5MB | tap `multi-photo-add-button` → `Chọn từ thư viện` → tap thumbnail `descriptionContains("11:10:01")` (**F3 6 MiB**) → `Add (1)` | ✅ PASS | — | — |
| 3 | Check thông báo + bộ đếm | ngay sau `Add`: `textContains("5MB")` **NOT FOUND**, ảnh chụp không thấy lỗi (ảnh dưới). **Cuộn xuống 1 nhịp** ⇒ `text("Ảnh vượt quá 5MB, vui lòng chọn ảnh nhỏ hơn.")` **tìm thấy**; bộ đếm `0/5` | ✅ PASS | `TC-ORD-068__pre-chua-cuon-thong-bao-loi-bi-khuat-duoi-viewport.png` · `TC-ORD-068__verify-6mib-bi-tu-choi-thong-bao-5mb-bo-dem-0-5.png` | ⚠️ **thông báo nằm DƯỚI khối ảnh, bị thanh nút cố định che ở viewport mặc định** (bẫy T8/T14) — phải cuộn mới thấy |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-068__pre-chua-cuon-thong-bao-loi-bi-khuat-duoi-viewport.png` · `screenshots/TC-ORD-068__verify-6mib-bi-tu-choi-thong-bao-5mb-bo-dem-0-5.png` — verified tồn tại

### 🐞 Kết luận cho draft `BUG-019` *("ảnh ~5MB bị từ chối im lặng")* — **KHÔNG tái hiện**
| File | Dung lượng | Kết quả app | Thông báo |
|---|---|---|---|
| `F2` | **5.242.880 B (đúng 5 MiB)** | ✅ **được nhận**, bộ đếm `0/5 → 1/5` | không cần | *(`TC-ORD-068__pre-file-dung-5mib-duoc-nhan-bo-dem-1-5-khong-loi.png`)* |
| `F4` | 5.600.000 B (≈5,6 MB) | ❌ từ chối, bộ đếm **giữ** `1/5` | ✅ **CÓ** `Ảnh vượt quá 5MB, vui lòng chọn ảnh nhỏ hơn.` *(nằm dưới viewport)* | *(`TC-ORD-068__pre-file-5-6mb-bi-tu-choi-co-thong-bao-nam-duoi-man-hinh.png`)* |
| `F3` | 6.291.456 B (6 MiB) | ❌ từ chối, bộ đếm `0/5` | ✅ **CÓ**, cùng chuỗi | *(step 3)* |

⇒ Ngưỡng là **`> 5 MiB`** (5.242.880 B được nhận). **Mọi ảnh vượt ngưỡng đều có thông báo** — quan sát *"không có thông báo"* ở draft **rất có thể do thông báo nằm dưới viewport** (bộ đếm `0/5` vẫn đọc được từ nút thêm ảnh còn hiện ở mép dưới; dòng lỗi thì bị che), đúng bẫy đã ghi ở `T8`/`T14`. ⛔ **Khuyến nghị: KHÔNG push `BUG-019`** — chuyển sang xoá draft; nếu QC vẫn muốn giữ, cần bằng chứng có cuộn xuống.
**Evidence phụ:** `screenshots/TC-ORD-068__pre-file-dung-5mib-duoc-nhan-bo-dem-1-5-khong-loi.png` · `screenshots/TC-ORD-068__pre-file-5-6mb-bi-tu-choi-co-thong-bao-nam-duoi-man-hinh.png` — verified tồn tại
🔎 **Điểm UX đáng ghi nhận (không phải bug do 1 quan sát):** thông báo lỗi ảnh đặt ở cuối khối và bị che ở viewport mặc định ⇒ người dùng thật cũng dễ **không thấy** lỗi; nếu app tự cuộn tới lỗi (theo `VAL-02` *"cuộn tới ô lỗi đầu tiên"*) thì đây là chỗ không thực thi — nên QC cân nhắc.

---

## TC-ORD-061: Check tin đã ghép quá Đến ngày không chuyển sang hết hạn — P2 · SC-ORD-045

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập tài khoản A, tab `Hoạt động`, tab con `Đang diễn ra` *(setup)* | tab `Hoạt động` | ✅ PASS | `TC-ORD-061__pre-tab-dang-dien-ra-tin-da-ghep-khong-badge-het-han.png` | list có 3 tin `Chờ ghép` mới + các tin `Đã ghép` |
| 2 | Tìm tin đã ghép có `Đến ngày` đã qua *(setup)* | dùng dữ liệu có sẵn: card `Giao: Tài liệu \| Giá trị thấp, Đã ghép, Từ: Tòa V-City → Đến: FPT Cầu Giấy` = tin `N1` của `Đặng Châu Anh`, khung **19/09/2026 · Chiều** (1 ngày), đã ghép bởi Giang ở `TC-ASN-010` *(nguồn: `USR-accounts.md §3`)* | ✅ PASS | — | ⚠️ **`Đến ngày` lấy từ ghi chép seed (19/09 < hôm nay 21/09), KHÔNG đọc được trên màn** — màn Theo dõi đơn của tin đã ghép không hiện khung ngày |
| 3 | Nhấn vào tin để mở chi tiết | `descriptionStartsWith("Giao: Tài liệu \| Giá trị thấp, Đã ghép")` → tap | ✅ PASS | — | màn `Theo dõi đơn` vai người vận chuyển: thanh bước ở `Lấy hàng`, nút `Tôi đã lấy hàng` / `Huỷ nhận đơn` |
| 4 | Check trạng thái + tab chứa tin | `textContains("Hết hạn")` **NOT FOUND** trên chi tiết; tin nằm ở tab `Đang diễn ra` (card không có badge) | ✅ PASS | `TC-ORD-061__verify-chi-tiet-tin-da-ghep-khong-badge-het-han.png` | không badge `Hết hạn`, vẫn ở `Đang diễn ra` |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-061__pre-tab-dang-dien-ra-tin-da-ghep-khong-badge-het-han.png` · `screenshots/TC-ORD-061__verify-chi-tiet-tin-da-ghep-khong-badge-het-han.png` — verified tồn tại
⚠️ **Hạn chế:** ngày quá hạn dựa trên seed ghi chép, không phải on-screen. Nếu QC cần bằng chứng on-screen ⇒ seed 1 tin đã ghép với `Đến ngày` = hôm qua.

---

## TC-ORD-048: Check tin chưa ai ghép quá Đến ngày chuyển sang hết hạn và biến khỏi Bảng tin — P2 · SC-ORD-045

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Tab `Hoạt động`, tìm tin quá `Đến ngày` chưa ai ghép, ghi tiêu đề + `Đến ngày` *(setup)* | tab `Đã hoàn thành` của **Giang (EMU)**: tin `Gửi tài liệu · Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy · 19/9/2026`, badge `Hết hạn`, dòng *"Không có ai nhận mang giúp trong thời gian đăng — tin đã tự động đóng."* | ✅ PASS | `TC-ORD-048__pre-tab-da-hoan-thanh-tin-gui-tai-lieu-19-9-badge-het-han.png` | dữ liệu có sẵn (`USR-accounts.md §3b`); ngày `19/9/2026` **đọc được trên màn** |
| 3 | Đăng nhập tài khoản B *(setup)* | **không cần đổi tài khoản** — dùng **máy thật `R58T20PLP8K` đang đăng nhập sẵn `Đặng Châu Anh`** song song | ✅ PASS | — | lợi thế 2 thiết bị |
| 4 | Tab `Bảng tin` của B, tìm tin đó | `Bảng tin` → cuộn hết danh sách (5 tin) | ✅ PASS | `TC-ORD-048__verify-bang-tin-tai-khoan-b-khong-con-tin-het-han-19-9.png` | 5 tin, ngày ≥ 21/09; **không tin nào ngày 19/09**, không tuyến `V-City → Cầu Giấy` dạng `Gửi tài liệu` |
| 5-6 | Đăng nhập lại A, tab `Đã hoàn thành`, check badge + kết quả step 4 | badge `Hết hạn` ở tab `Đã hoàn thành` (step 1-2) ✓ · không có trên Bảng tin B (step 4) ✓ | ✅ PASS | — | — |

**Result: ✅ PASS (6 steps, 1 expected)**
**Evidence:** `screenshots/TC-ORD-048__pre-tab-da-hoan-thanh-tin-gui-tai-lieu-19-9-badge-het-han.png` · `screenshots/TC-ORD-048__verify-bang-tin-tai-khoan-b-khong-con-tin-het-han-19-9.png` — verified tồn tại
📝 Ghi nhận: tab `Đã hoàn thành` còn chứa **3 tin OFFER `Hết hạn`** (`Tôi đi thuận đường …`, 20/9 & 10/8) — OFFER cũng tự hết hạn.

---

## TC-ORD-045: Check tin OFFER không xuất hiện trên Bảng tin của người khác — P1 · SC-ORD-042 *(v1.0 CARRIED)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập A, đăng 1 tin OFFER qua card `Tôi nhận giao hàng`, ghi lại tuyến *(setup)* | EMU/Giang: `Cẩm Lệ`→`address-suggestion-1` = **`363 Nguyễn Hữu Thọ, Cẩm Lệ`** → `Lê Thái Tổ`→`address-suggestion-0` = `Tòa V-City, Lê Thái Tổ`; buổi `resourceId("offer-day-part-anytime")`; tick; `Đăng tin ngay` (11:28) | ✅ PASS | `TC-ORD-045__pre-form-offer-tuyen-363-nguyen-huu-tho-den-v-city-truoc-khi-dang.png` | tuyến **riêng biệt** (không NEED nào cùng điểm lấy) → không kích hoạt thông báo khớp tuyến của người khác |
| 2 | Đăng nhập B, tab `Bảng tin` *(setup)* | máy thật, `Đặng Châu Anh` (đăng nhập sẵn) | ✅ PASS | — | — |
| 3 | Cuộn toàn danh sách, tìm tin có tuyến đã ghi | `Bảng tin` → cuộn hết (5 tin) → quét text: 0 chuỗi `Hữu Thọ` | ✅ PASS | `TC-ORD-045__verify-bang-tin-tai-khoan-b-cuon-het-khong-co-tin-offer-cua-a.png` | Bảng tin B **KHÔNG có** tin OFFER |
| 4-5 | Đăng nhập lại A, `Bảng tin`, tìm tin OFFER của chính mình | EMU/Giang: `Bảng tin` → cuộn hết (5 tin: 3 tin NEED `Tin của bạn` + 2 tin khác) → quét text: 0 chuỗi `Hữu Thọ` | ✅ PASS | `TC-ORD-045__verify-bang-tin-tai-khoan-a-khong-co-tin-offer-cua-chinh-minh.png` | Bảng tin A cũng **KHÔNG có** |

**Result: ✅ PASS (5 steps, 2 expected)** — *(P1)*
**Evidence:** `screenshots/TC-ORD-045__pre-form-offer-tuyen-363-nguyen-huu-tho-den-v-city-truoc-khi-dang.png` · `screenshots/TC-ORD-045__verify-bang-tin-tai-khoan-b-cuon-het-khong-co-tin-offer-cua-a.png` · `screenshots/TC-ORD-045__verify-bang-tin-tai-khoan-a-khong-co-tin-offer-cua-chinh-minh.png` — verified tồn tại
📝 Màn xác nhận OFFER nêu rõ *"Tuyến đường của bạn được lưu vào hệ thống (**không hiển thị công khai**)"* (ảnh của `TC-ORD-044`). ⚠️ Ghi chú test: lần quét đầu trên A báo 5 khớp giả (`363` là **toạ độ bounds**, không phải text) — đã lọc lại bằng text-only ⇒ 0.

---

## TC-ORD-044: Check vai người gửi không tìm thấy và không mở được tin OFFER của người khác — P2 · SC-ORD-041

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | A đăng 1 tin OFFER với tuyến riêng biệt rồi đăng xuất *(setup)* | dùng OFFER của `TC-ORD-045` (seed dùng chung); **không cần đăng xuất** (máy thật giữ B) | ✅ PASS | `TC-ORD-044__pre-offer-da-ghi-nhan-tuyen-duong-khong-hien-thi-cong-khai.png` | màn xác nhận: *"Đã ghi nhận tuyến đường! … (không hiển thị công khai)"* |
| 2 | Đăng nhập B, tab `Bảng tin` *(setup)* | máy thật | ✅ PASS | — | — |
| 3 | Rà lần lượt **cả hai tab con** của Bảng tin | ⚠️ **Bảng tin v1.1 KHÔNG có tab con** — chỉ là **1 danh sách** duy nhất (5 tin, không tab, không thanh lọc) | ⚠️ *(lệch UI, quan sát)* | — | TC lỗi thời so với UI v1.1 |
| 4 | Nhập tên tuyến vào **ô tìm kiếm** | ⚠️ **Bảng tin không có ô tìm kiếm** (không `EditText` nào; đã kiểm page source) ⇒ thay bằng **quét toàn bộ text danh sách** (cuộn hết 5 tin) tìm `Hữu Thọ` | ✅ PASS | `TC-ORD-044__verify-bang-tin-b-mot-danh-sach-khong-tab-khong-o-tim-kiem-khong-co-offer-cua-a.png` | 0 kết quả; OFFER của A **không** xuất hiện. Ảnh chụp riêng (máy thật) — thấy Bảng tin là **1 danh sách, không tab, không ô tìm kiếm** |

**Result: ✅ PASS (đã điều chỉnh — ý chính "OFFER của người khác không thấy được")** · ⚠️ **step 3–4 của TC nhắc UI không có ở v1.1** (*"hai tab con"*, *"ô tìm kiếm"*) ⇒ QC sửa Steps (cho phép theo `Project_rule §10.5`). Vế *"không mở được"* được suy ra (không có card để mở) — không thử mở bằng deep-link.
**Evidence:** `screenshots/TC-ORD-044__pre-offer-da-ghi-nhan-tuyen-duong-khong-hien-thi-cong-khai.png` · `screenshots/TC-ORD-044__verify-bang-tin-b-mot-danh-sach-khong-tab-khong-o-tim-kiem-khong-co-offer-cua-a.png` — verified tồn tại

---

## TC-ORD-080: Check khai người nhận uỷ quyền hợp lệ gắn nhãn Người gửi chỉ định vào đơn — P2 · SC-ORD-061 *(⏳ CHẠY DỞ — chưa có verdict)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập, `+ Đăng tin`, card NEED, nhập đủ bước 1 gồm ảnh, `Tiếp theo` *(setup)* | đơn `P3` (cùng đơn của `TC-ORD-065`, có 5 ảnh) | ✅ PASS | — | — |
| 2 | Nhấn `+ Thêm người nhận uỷ quyền` | tap `descriptionStartsWith("Thêm người nhận uỷ quyền")` | ✅ PASS | — | khối mở, hiện `resourceId("alt-receiver-name-input")` · `("alt-receiver-phone-input")` |
| 3 | Nhập tên `Nguyễn Văn Bảy` + SĐT `0912345678` | `set_value` ×2 → rời ô (tap nhãn `NGƯỜI NHẬN`) | ✅ PASS | `TC-ORD-080__pre-khoi-uy-quyen-nguyen-van-bay-0912345678.png` | không có lỗi ở 2 ô |
| 4 | `Tiếp theo`, nhập đủ bước 3, `Đăng tin ngay` | tick + `Đăng tin ngay` (10:41) → `Đăng tin thành công` | ✅ PASS | — | đơn tạo được |
| 5 | Tab `Hoạt động`, mở đơn, check khối người nhận uỷ quyền | mở `Theo dõi đơn` của chủ tin: **không có** khối người nhận nào (đã grep toàn page source: 0 `Bảy` / `0912345678` / `chỉ định` / `uỷ quyền`). Kiểm tiếp phía người xem `Chi tiết tin` (máy thật, chưa ghép): cũng **không có** — chỉ có khối `NGƯỜI GỬI` + `Chưa thể gọi — chờ ghép đơn` | ⏳ **CHƯA KẾT LUẬN** | — | 🔴 **Màn của chủ tin không có chỗ hiển thị dữ liệu uỷ quyền.** Spec `AC-05.1.01`: *"Ở màn giao hàng, **người vận chuyển** thấy khối này kèm nhãn `Người gửi chỉ định`"* ⇒ điểm kiểm đúng phải nằm ở **màn giao hàng sau khi ghép** (cần tài khoản B nhận đơn). Chưa làm được vì hết sức phiên |

**Result: ⚠️ NOT_EVIDENCED (chạy 4/5 step; step 5 chưa có màn chứng minh Expected)** — *không hạ thành FAIL: app **không sai** khi chủ tin không thấy khối uỷ quyền (theo spec nó dành cho người vận chuyển); TC-Steps step 5 nhắm sai màn.*
**Evidence:** `screenshots/TC-ORD-080__pre-khoi-uy-quyen-nguyen-van-bay-0912345678.png` — verified tồn tại
**🔎 Thử ghép bằng tài khoản B (máy thật) — KHÔNG được:** B (`Đặng Châu Anh`) chính là **người nhận** của đơn `P3` nên màn `Chi tiết tin` chỉ có `NGƯỜI GỬI` + nút `Gọi` bị khoá, **không có nút `Tôi mang giúp được`**. (Quan sát phụ: `Chi tiết tin` của B hiện ảnh **`1/4`** — xác nhận từ thiết bị thứ 2 rằng ảnh của tin đã đăng bị xoá thật, xem `TC-ORD-088`.)
**▶️ Chạy tiếp:** cần **tài khoản thứ 3 làm người vận chuyển** (vd `stag_taipm@` / `stag_anhptm17@`, ⚠️ đổi tài khoản trên 1 máy = ~14 call) → `Bảng tin` → card `Nặng` → `Tôi mang giúp được` → mở màn giao hàng tìm nhãn `Người gửi chỉ định` · `Nguyễn Văn Bảy` · `0912345678`. ⚠️ hành động ghép là **không đảo ngược** trên STG. Lệnh: `/vibe-test --tc TC-ORD-080`.
