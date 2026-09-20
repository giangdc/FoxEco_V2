# Vibe Test Report — VR-010 — v1.1 — 2026-09-19

> Platform: **mobile** (Appium MCP · UiAutomator2 · emulator-5554)
> Environment: STG — host app FoxPro `com.hrisproject.stag`, SDK nhúng FoxEco
> Module: **ASN (Ghép nối)** · Tập chạy phiên này: **7 TC pending**

## Scope Coverage ★★ *(trạng thái CẢ MODULE sau khi merge run này)*

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module ASN)** | **26** | 100% |
| Chạy **trong run này** | 7 | 27% |
| ✅ PASS từ **run trước** (không chạy lại theo lựa chọn QC) | 15 | 58% |
| ⛔ N-A (cố ý không test qua UI, có lý do) | 2 | 8% |
| ⏳ **NOT_RUN (còn nợ)** | **2** | **8%** |
| ⚠️ NOT_EVIDENCED (còn nợ) | 0 | 0% |

**Còn nợ = 2 TC → §8 = PARTIAL.**

- Chi tiết từng TC **của module (xuyên run)**: `08_test-runs/vibe/coverage/coverage-ASN.md` ← **xem cái này**
- Chi tiết **run này làm gì**: `scope-ledger.md`

> 🔴 **2 TC còn nợ là quyết định của QC, ⛔ không phải hết sức phiên.** QC chốt 2026-09-19 16:30:
> *"2 emulator thôi nhé, case nào cần 2 emulator thì để lại giúp t"* ⇒ `TC-ASN-006` (2 thiết bị) và
> `TC-ASN-008` (3 thiết bị) để QC tự chạy. Máy chạy phiên này chỉ có **1 emulator** (RAM 7GB / trống ~2GB).

## Kết quả các TC chạy trong run này

| Result | Count | % trên 7 |
|--------|-------|---|
| ✅ PASS | 5 | 71% |
| ❌ FAIL | 2 | 29% |
| 🚫 BLOCKED | 0 | 0% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | **7/7 (100%)** |
| File ảnh trong `screenshots/` | 18 |
| TC thiếu evidence (⚠️ NOT_EVIDENCED) | — *(không có)* |
| Gate `verify_evidence.py` | xem §Gate cuối báo cáo |

## 🔴 Failed TCs — 1 LỖI GỐC, cần `/log-bug`

| TC ID | Failed at | Expected | Actual |
|-------|----------|----------|--------|
| **TC-ASN-016** | E1 (đếm thông báo) | đúng **5** thông báo khớp tuyến cho tin OFFER có 5 tin NEED khớp | **4** — dù Bảng tin xác nhận **đủ 5** tin NEED khớp |
| **TC-ASN-025** | E1 (trần độc lập theo tuyến) | tuyến OFFER **thứ hai** nhận thông báo mới; tổng **> 5** | tuyến 2 nhận **0** thông báo; tổng **vẫn đúng 5** |

### Nguyên nhân gốc (đã chứng minh, ⛔ không suy diễn)

> **Trần 5 thông báo khớp tuyến được áp cho TOÀN TÀI KHOẢN, không phải cho từng tuyến OFFER** —
> đúng rủi ro BA lường trước ở `C-ASN-04(e)`: *"rủi ro thật nếu backend dùng chung 1 bộ đếm cho cả tài khoản"*.

| # | Thời điểm | Việc đã làm | Thông báo khớp tuyến |
|---|---|---|---|
| 0 | 16:28 | *(chưa seed)* | **1** (tồn dư VR-009) |
| 1 | 17:18 | `OFFER-R1` + **5** tin NEED khớp | **5** ⇒ chỉ **+4** ❌ |
| 2 | 17:38 & 17:43 | + tin NEED **thứ 6** của `R1` | **5** ⇒ +0 |
| 3 | 17:38 & 17:43 | + **`OFFER-R2` tuyến khác (0/5 slot)** + 1 tin NEED trùng khít | **5** ⇒ **+0** ❌ ← **mắt xích quyết định** |

Giả thuyết *"thông báo đến chậm"* **bị bác bỏ**: đo **2 lần cách nhau 5 phút**, tin đã 2–13 phút tuổi ≫ `NFR-04` (≤60s).

**Tác động:** CBNV đăng nhiều tuyến sẽ **mất hoàn toàn** thông báo khớp tuyến ở mọi tuyến sau khi **tổng** chạm 5 — kể cả tuyến mới tinh.

## ⚠️ Passed TCs — 2 ca PASS cần đọc kèm cảnh báo

| TC ID | Verdict | Vì sao PASS này **chưa** đủ để yên tâm |
|---|---|---|
| **TC-ASN-014** | ✅ PASS | Assertion *"gợi ý nhiều nhất là 5"* thoả (actual **4**), nhưng app dừng ở 4 vì **trần tài khoản**, ⛔ không phải trần gợi ý per-tuyến ⇒ TC **không phân biệt được** app đúng/sai ở mốc 5. **Chạy lại sau khi fix.** |
| **TC-ASN-017** | ✅ PASS | Quan sát đúng expected (tin thứ 6 không sinh thông báo), nhưng **tiền đề *"tuyến đã đủ 5"* chưa bao giờ đạt** (tuyến `R1` chỉ có 4) ⇒ ⛔ **không chứng minh** `C-ASN-04(d)`. **Chạy lại sau khi fix.** |

## ✅ Passed TCs — sẵn sàng implement automation

| TC ID | Steps | Evidence file |
|-------|-------|---------------|
| TC-ASN-014 | 4 | `screenshots/TC-ASN-014__verify-toi-da-5-goi-y.png` |
| TC-ASN-015 | 3 | `screenshots/TC-ASN-015__verify-dung-3-thong-bao.png` |
| TC-ASN-017 | 5 | `screenshots/TC-ASN-017__verify-so-thong-bao-khong-doi.png` |
| TC-ASN-018 | 4 | `screenshots/TC-ASN-018__verify-thu-tu-goi-y.png` · `TC-ASN-018__verify-dinh-danh-r3b-tren-cung.png` |
| TC-ASN-019 | 6 | `screenshots/TC-ASN-019__verify-thong-bao-chi-tro-tin-con-song.png` · `TC-ASN-019__verify-bangtin-vang-tin-het-han.png` |

## Locator Coverage

| Màn đã harvest | Elements captured | ✅ Verified | 🚫 NOT FOUND |
|--------------|------------------|------------|-------------|
| 7 | 38 | 33 | 2\* |

\* cả 2 `NOT FOUND` là **chủ ý / phát hiện**, ⛔ không phải locator hỏng.
→ implement-automation có thể bắt đầu với **33 locators đã verified** (`08_test-runs/vibe/locators/vibe-locators-latest.md`).

## 🧭 Phát hiện phụ cần QC/BA/DEV xử lý

| # | Phát hiện | Đề nghị |
|---|---|---|
| 1 | 🔴 **Trần 5 theo tài khoản** *(xem trên)* | **`/log-bug`** — P1/P2, kèm chuỗi số đo 4 mốc |
| 2 | `stag_huyennhk@` **không được bật FoxEco**; màn `Cá nhân` cũng **không render** mục `Đăng xuất` ⇒ phải `pm clear` để thoát | Cập nhật `USR-accounts.md §1`: tài khoản này **chỉ làm người nhận**. Mục `Đăng xuất` biến mất có thể là **bug riêng** — đề nghị DEV xem |
| 3 | `TC-ASN-019` Steps ghi *"Nhờ dev/QA seed"* + Test Data ghi *"⛔ không seed được qua UI"* — **đã lỗi thời** | Sửa fragment: STG **tự sinh** tin `Hết hạn`, xem ở `Đơn của tôi → Đã hoàn thành` |
| 4 | Gõ `FTEL SG08` ở ô địa chỉ ⇒ gợi ý-0 trả **`FTEL SG08 Gò Vấp`**, ⛔ không phải `Quận 12` như phiên trước | Test data phải ghi **đủ chuỗi** chi nhánh |
| 5 | Đăng OFFER mới ⇒ hệ thống **bắn thông báo HỒI TỐ** cho tin NEED **đã có sẵn** khớp tuyến | Hành vi này **chưa có trong scenario_map** ⇒ `/analyze-requirements --update` |
| 6 | **Thông báo khớp tuyến biến mất sau khi MỞ** (`stag_taipm@`), nhưng **không** biến mất ở `stag_giangdc2@` | Hành vi không nhất quán — ⇒ `/analyze-requirements --update` + DEV xác nhận |

## 🪤 Bẫy đo lường mới (bắt buộc đọc trước phiên ASN sau)

| # | Bẫy | Cách xử lý |
|---|---|---|
| `T-ASN-10` | `.instance(N)` **chỉ thấy node đang render** (~4 mục) ⇒ ⛔ không dùng làm phép đếm tuyệt đối | dump page source **nhiều vị trí cuộn** → ghép theo nhãn tuổi |
| `T-ASN-11` | Thông báo **biến mất sau khi mở** | **đếm TRƯỚC khi mở** |
| `T-ASN-12` | Không phải tài khoản nào cũng có FoxEco | chọn actor trong 4 tài khoản còn lại |
| `T-ASN-13` | VR-009 ghi *"Chi tiết tin không có mục Ghi chú"* — **SAI** | ✅ mã seed ở ô `Ghi chú` = **oracle định danh mạnh nhất** |

## Recommendation

- **Log bug ngay:** 1 bug — trần 5 theo tài khoản (`TC-ASN-016` + `TC-ASN-025`) → `/log-bug`
- **Chạy lại sau khi fix:** `TC-ASN-014`, `TC-ASN-017` — 2 PASS hiện **không có khả năng phân biệt**
- **QC tự chạy (đa thiết bị):** `TC-ASN-006` (2 máy) · `TC-ASN-008` (3 máy)
- **Về analyze:** 2 hành vi chưa có trong scenario_map (thông báo hồi tố · thông báo biến mất sau khi mở) → `/analyze-requirements --update`
- **Automate:** 5 TC PASS có locator sẵn → `/implement-automation --module ASN` *(⚠️ hoãn `014`/`017` tới sau fix)*
