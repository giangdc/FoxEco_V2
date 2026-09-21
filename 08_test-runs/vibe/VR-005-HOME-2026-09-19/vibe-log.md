# Vibe Test Log — VR-005 — v1.1 (+ CARRIED v1.0) — 2026-09-19

> Module: **HOME** (Trang chủ) · Platform: **mobile (Appium MCP / UiAutomator2)** · Env: STG, app `com.hrisproject.stag` (host FoxPro → FoxEco)
> Device: emulator-5554 · Session: `55129e7d-a214-4167-a988-d83f2e82c2b7` · Evidence dir: `screenshots/`
> Phiên: 2026-09-19 (khởi tạo)
> Tài khoản: **A** = `Đặng Châu Giang` (đã đăng nhập sẵn từ host FoxPro)
> Tập chạy: **toàn bộ pending** — `coverage-HOME.md` chưa tồn tại ⇒ cả 30 TC đều pending, không cần hỏi Step 1.2.

## 🔴 Trạng thái dữ liệu STG lúc bắt đầu phiên (quyết định TC nào chạy được)

| Dữ kiện | Giá trị đo được ở Pha A | Ảnh hưởng |
|---|---|---|
| Section "Tin mới" | **EMPTY STATE** (`home-news-empty`) — 0 tin NEED hợp lệ toàn hệ thống | ✅ mở cửa sổ chạy `TC-HOME-026` (`EMP-01`) · ⛔ chặn mọi TC cần ≥1 tin cộng đồng |
| Section "Đơn của tôi" | **6 card**, đủ 3 nhãn vai `Gửi:` / `Giao:` / `Nhận:` | ✅ chạy được nhóm nhãn vai + điều hướng |
| Hero | `13` đơn đã giúp · cộng đồng `317 đơn · 23743 người` | ✅ đọc được, ⛔ không dựng được phép đo tăng (+1) |
| Chuông thông báo | **có chấm đỏ** (≥1 chưa đọc) | ✅ chạy được `TC-HOME-005` |

---

## TC-HOME-001: Check bottom nav đủ 5 tab đúng thứ tự và tab "Trang chủ" đang active

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco từ host FoxPro *(setup)* | app đã ở Trang chủ, tài khoản A | ✅ PASS | — | `noReset=true`, phiên đăng nhập sẵn |
| 2 | Check thanh tab dưới cùng | `find_element` ×5 qua `accessibility id` | ✅ PASS | `TC-HOME-001__verify-bottom-nav-5-tabs.png` | 5/5 tìm thấy |
| E1 | 5 tab đúng thứ tự trái→phải | đọc `bounds` từ page source A1 | ✅ PASS | ↑ | `Trang chủ`[0,1118] → `Bảng tin`[140] → `Đăng tin`[280, FAB giữa] → `Hoạt động`[440] → `Cá nhân`[580] |
| E2 | Tab "Trang chủ" active | đo bằng ảnh *(bẫy **T1**: `selected` luôn `false`)* | ✅ PASS | ↑ | chữ + icon `Trang chủ` màu cam, có chấm chỉ báo dưới icon; 4 tab còn lại xám |

**Result: ✅ PASS (2 steps, 2 expected)**
**Evidence:** `screenshots/TC-HOME-001__verify-bottom-nav-5-tabs.png`
**Locators captured:** 5 elements (bottom nav) — tái xác nhận map VR-001

---

## TC-HOME-003: Check header hiển thị lời chào kèm đúng tên hồ sơ của tài khoản đăng nhập

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco *(setup)* | tài khoản A | ✅ PASS | — | — |
| 2 | Check dòng lời chào ở header | `find_element` + `get_text` | ✅ PASS | `TC-HOME-003__verify-greeting-name.png` | — |
| E1 | Header hiện "Xin chào, [tên]" khớp hồ sơ | 2 TextView: `Xin chào,` + `Đặng Châu Giang` | ✅ PASS | ↑ | tên khớp hồ sơ HRIS của tài khoản A (đã đối chiếu ở VR-001 §`TC-USR-002`) |

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-HOME-003__verify-greeting-name.png`
**Locators captured:** 2 elements
ℹ️ Lời chào tách **2 TextView** (`Xin chào,` và tên), ⛔ không phải 1 chuỗi ghép — assert automation phải ghép 2 node.

---

## TC-HOME-007: Check banner quảng bá hiển thị tagline kèm logo và không phát sinh điều hướng khi nhấn

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco *(setup)* | tài khoản A | ✅ PASS | — | — |
| 2 | Check vùng banner quảng bá | `find_element(textContains "Tiện đường")` + `get_text` | ✅ PASS | `TC-HOME-007__verify-tagline-giup-dong-nghiep.png` (+ `__pre-banner-before-tap.png`) | tagline khớp Expected đã sửa — xem E1 |
| 3 | Nhấn vào banner | `gesture(tap)` trên chính element tagline | ✅ PASS | ↑ | — |
| E1 | Banner hiện logo "FOX ECO" + tagline "Tiện đường — Giúp đồng nghiệp" | logo ✅ có (`FOX ECO`) · tagline ✅ | ✅ **PASS** | ↑ | **Expected (đã sửa 2026-09-21):** `Tiện đường — Giúp đồng nghiệp` · **Actual (MCP `get_text`, nguyên văn):** `Tiện đường —\nGiúp đồng nghiệp` |
| E2 | Nhấn banner không mở màn nào, không popup, Trang chủ giữ nguyên | so ảnh trước/sau tap | ✅ PASS | ↑ | không điều hướng, không popup, scroll giữ nguyên |

**Result: ✅ PASS** — vế chuỗi tagline (E1) và vế "nhấn banner không điều hướng" (E2) đều đúng.
**Evidence:** `screenshots/TC-HOME-007__verify-tagline-giup-dong-nghiep.png` (+ `TC-HOME-007__pre-banner-before-tap.png`)
**Reason:** app hiển thị `Tiện đường — Giúp đồng nghiệp` = Expected sau khi sửa (chuỗi PRD, khớp design `HOME_01/02/04`).
📌 Lịch sử: run 2026-09-19 ghi FAIL so với Expected cũ (chuỗi BRD). 2026-09-21 QC GiangDC2 chốt chuỗi PRD là oracle (`C-HOME-01(b)`), sửa Expected của TC, đổi verdict FAIL → PASS theo dữ liệu đo ngày 2026-09-19, **không chạy lại**. ⛔ Không log bug.
Dòng phụ dưới tagline (`Gửi hàng nội bộ · Không phí · Không chat`) **không nằm trong Expected** của TC — ghi nhận để BA rà.

---

## TC-HOME-005: Check icon chuông hiển thị chấm đỏ khi còn thông báo chưa đọc

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập bằng tài khoản có thông báo chưa đọc *(setup)* | tài khoản A — có 4+ thông báo chưa đọc | ✅ PASS | — | xác nhận ở `_recon__man-thong-bao.png`: 4 item đều có chấm đỏ |
| 2 | Check icon chuông ở header Trang chủ | `find_element(accessibility id "Thông báo")` + đo pixel | ✅ PASS | `TC-HOME-005__verify-chuong-cham-do.png` | — |
| E1 | Icon chuông hiển thị chấm đỏ | **đo pixel** vùng badge `[664..686, 99..115]` | ✅ PASS | ↑ | chấm đỏ `RGB(244,64,74)`, tương phản rõ với nền cam `(255,133,0)`/`(255,171,46)` |

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-HOME-005__verify-chuong-cham-do.png`
**Locators captured:** 1 element (`accessibility id "Thông báo"`)
🔧 **Bẫy T15 (mới):** chấm đỏ của chuông **KHÔNG có node riêng** trong accessibility tree (không desc, không rid) ⇒ ⛔ không assert được bằng `find_element`; phải **đo pixel** hoặc so ảnh. Cùng họ bẫy **T1** (`selected` không expose).

---

## TC-HOME-006: Check icon chuông không có chấm đỏ khi đã đọc hết thông báo

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập bằng tài khoản có thông báo *(setup)* | tài khoản A | ✅ PASS | — | — |
| 2 | Mở chuông, đọc hết thông báo còn chấm đỏ *(setup)* | tap `Thông báo` → tap `Đánh dấu đã đọc` | ✅ PASS | `_recon__man-thong-bao.png` | ⚠️ **lệch câu chữ step** — xem ghi chú dưới |
| 3 | Nhấn nút quay lại về Trang chủ | `gesture(back)` | ✅ PASS | — | về đúng Trang chủ |
| 4 | Check icon chuông ở header | đo pixel cùng vùng như `TC-HOME-005` | ✅ PASS | `TC-HOME-006__verify-chuong-khong-cham-do.png` | — |
| E1 | Icon chuông KHÔNG hiển thị chấm đỏ | đo pixel `[664..686, 99..115]` | ✅ PASS | ↑ | **0 pixel đỏ** (trước đó có `(244,64,74)`); vùng badge nay đồng màu nền cam |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-HOME-006__verify-chuong-khong-cham-do.png`
**Locators captured:** 2 elements (`Thông báo`, `Đánh dấu đã đọc`)
⚠️ **Khai báo lệch step (không giấu):** step 2 viết *"mở lần lượt toàn bộ thông báo còn chấm đỏ"*; phiên này dùng nút **`Đánh dấu đã đọc`** (bulk) — app **có sẵn** control này ở màn Thông báo. Đạt đúng **trạng thái đích** của step (*"không còn item nào chưa đọc"*) và Expected chỉ assert trạng thái chuông, nên verdict vẫn tin được. 📌 Đề nghị QC: bổ sung nhánh bulk vào Steps, hoặc tách 1 TC riêng cho `Đánh dấu đã đọc` — **⛔ nhưng `§10.5` FREEZE cấm thêm TC**, nên nghiêng về **sửa Steps**.
🗂️ **Dữ liệu phát sinh trên STG:** toàn bộ thông báo của tài khoản A nay **đã đọc** ⇒ ⚠️ muốn chạy lại `TC-HOME-005` phải có sự kiện sinh thông báo mới.

---

## TC-HOME-022: Check nhấn "Xem bảng tin gửi hàng" chuyển sang tab Bảng tin

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco từ host FoxPro *(setup)* | tài khoản A | ✅ PASS | — | — |
| 2 | Nhấn "Xem bảng tin gửi hàng" ở Trang chủ | `find_element(accessibility id)` + `gesture(tap)` | ✅ PASS | `TC-HOME-022__verify-chuyen-tab-bang-tin.png` | — |
| E1 | Chuyển sang tab "Bảng tin", tab đó active trên bottom nav | đọc tiêu đề màn + đo màu tab | ✅ PASS | ↑ | tiêu đề `Bảng tin`; tab `Bảng tin` cam + chấm chỉ báo, `Trang chủ` trở lại xám; bottom nav vẫn hiện (đúng, đây là tab gốc) |

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-HOME-022__verify-chuyen-tab-bang-tin.png`
**Locators captured:** 1 element (`accessibility id "Xem bảng tin gửi hàng"` — nâng từ ⚠️ Inferred của VR-001 lên ✅ Verified)
🔴 **Dữ kiện quyết định phần còn lại của phiên:** màn Bảng tin **RỖNG** — *"Chưa có tin nào / Thử mở rộng khu vực tìm kiếm hoặc đăng tin của riêng bạn"* (`_recon__bang-tin-empty-0-tin.png`). ⇒ xác nhận **0 tin NEED hợp lệ toàn hệ thống** từ **2 bề mặt độc lập** (Trang chủ §Tin mới + Bảng tin), không phải lỗi lọc của riêng Trang chủ.

---

## TC-HOME-026: Check empty state section Tin mới hiện đúng chuỗi và nút đăng tin ngay

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Dọn STG về 0 tin NEED hợp lệ *(setup)* | **không phải dọn** — STG **vốn đã** 0 tin hợp lệ | ✅ PASS | `_recon__bang-tin-empty-0-tin.png` | điều kiện thoả **tự nhiên**, xác nhận 2 bề mặt (xem `TC-HOME-022`) |
| 2 | Đăng nhập tài khoản A, mở Trang chủ *(setup)* | tap tab `Trang chủ` + scroll xuống cuối | ✅ PASS | — | — |
| 3 | Check icon, dòng tiêu đề, dòng giải thích, nút CTA | `find_element` ×4 | ✅ PASS | `TC-HOME-026__verify-empty-state-tin-moi.png` | 4/4 khớp |
| E1 | icon nét mảnh + tiêu đề + giải thích + CTA "Đăng tin ngay", không skeleton kéo dài | đối chiếu **nguyên văn** | ✅ PASS | ↑ | chi tiết ↓ |

**Đối chiếu nguyên văn 4 vế của Expected:**

| Vế | Kỳ vọng | Đo được (MCP) | Khớp |
|---|---|---|---|
| Container | — | `resourceId("home-news-empty")` | — |
| Icon | icon nét mảnh | icon kiện hàng **nét mảnh (outline)**, xám | ✅ |
| Tiêu đề | `Chưa có tin nào trong khu vực của bạn` | `find_element(text=…)` khớp **nguyên văn** | ✅ |
| Giải thích | `Đăng tin để đồng nghiệp nhìn thấy nhu cầu của bạn` | khớp **nguyên văn** | ✅ |
| CTA | `Đăng tin ngay` | `accessibility id "Đăng tin ngay"` (`resourceId home-news-empty-cta`) | ✅ |
| Skeleton | không kéo dài | nội dung hiện ngay, không thấy skeleton | ✅ |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-HOME-026__verify-empty-state-tin-moi.png`
**Locators captured:** 4 elements
🟢 **Xác nhận oracle phản trực giác của `C-HOME-04`:** chuỗi *"trong khu vực của bạn"* **vẫn nguyên** dù tin load toàn quốc — đúng như BA chốt *"giữ nguyên nhé"*. ⛔ Không log bug, ⛔ không sửa Expected theo logic.
🔧 **Bẫy T2 tái hiện:** `home-news-empty` **NOT FOUND** với strategy `id`, **resolve được** với `-android uiautomator resourceId(...)`.
🍀 **Ghi chú cơ hội:** TC này được `§0.3` của fragment cảnh báo *"không dựng được trên STG dùng chung ⇒ ghi Blocked"*. Phiên này **chạy được thật** vì STG tình cờ sạch tin. ⚠️ **Cửa sổ này sẽ đóng** ngay khi có ai đăng tin — kết quả PASS neo vào thời điểm 2026-09-19 05:59.

---

## TC-HOME-009: Check section "Đơn của tôi" hiển thị đủ sáu thành phần khi tài khoản có đơn đang hoạt động

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng 1 tin NEED để có đơn "Chờ ghép" *(setup)* | **KHÔNG thực hiện** — dùng đơn có sẵn của tài khoản A | ⚠️ lệch | — | xem "Khai báo lệch" dưới — đăng tin NEED đang bị chặn bởi bug `B1` của VR-004 |
| 2 | Nhấn tab "Trang chủ" | đã ở Trang chủ, scroll tới section | ✅ PASS | — | — |
| 3 | Check lần lượt các thành phần của section | `find_element` ×2 + đối chiếu ảnh | ✅ PASS | `TC-HOME-009__verify-6-thanh-phan-don-cua-toi.png` | — |
| E1 | Section hiển thị đủ **6 thành phần** | đối chiếu từng thành phần trên card đầu | ✅ PASS | ↑ | chi tiết ↓ |

**Đối chiếu 6 thành phần (card đầu — `Gửi: Tài liệu | Giá trị thấp`):**

| # | Thành phần kỳ vọng | Đo được | Khớp |
|---|---|---|---|
| 1 | nhãn vai + loại hàng + giá trị hàng | `Gửi: Tài liệu | Giá trị thấp` (MCP `find_element`) | ✅ |
| 2 | badge trạng thái | `Đã ghép` (pill tím nhạt, góc phải) | ✅ |
| 3 | dòng "Từ:" | `Từ: Tòa V-City, Lê Thái Tổ` | ✅ |
| 4 | dòng "Đến:" | `Đến: FPT Cầu Giấy` | ✅ |
| 5 | thanh progress **5 bước** | **5 đoạn**, 2 đoạn đầu tô cam, 3 đoạn xám | ✅ |
| 6 | dòng "Chạm để theo dõi đơn của bạn" | khớp nguyên văn (MCP `find_element`) | ✅ |

**Result: ✅ PASS (3 steps, 1 expected) — 6/6 thành phần có mặt**
**Evidence:** `screenshots/TC-HOME-009__verify-6-thanh-phan-don-cua-toi.png`
**Locators captured:** 2 elements
⚠️ **Khai báo lệch step (không giấu):** step 1 yêu cầu **tự đăng 1 tin NEED** để có đơn ở trạng thái **`Chờ ghép`**; phiên này dùng **đơn có sẵn** ở trạng thái **`Đã ghép`**. Lý do: `VR-004` đã chứng minh **không đăng được tin NEED** (bug `B1`, API `400 REQ_400`, app im lặng) ⇒ không dựng lại được tiền đề. Expected **không assert giá trị badge**, chỉ assert *"có thành phần badge trạng thái"*, nên 6/6 vẫn kết luận được. 📌 Nếu QC muốn siết đúng trạng thái `Chờ ghép` thì TC này phải **chờ fix `B1`** rồi chạy lại.
🔧 **Bẫy T16 (mới):** **thanh progress 5 bước KHÔNG có node** trong accessibility tree (không text, không desc, không resource-id) ⇒ ⛔ không assert được bằng `find_element`; phải **đo pixel / so ảnh**. Cùng họ **T1** và **T15**.

---

## TC-HOME-011: Check section "Đơn của tôi" dùng nhãn "Gửi:" khi tài khoản là người gửi

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng 1 tin NEED để có đơn đang hoạt động *(setup)* | dùng đơn có sẵn (A là **người gửi**) | ⚠️ lệch | — | cùng lý do `TC-HOME-009` (bug `B1`) |
| 2 | Nhấn tab "Trang chủ" | đã ở Trang chủ | ✅ PASS | — | — |
| 3 | Check nhãn vai ở dòng đầu section | `find_element(text="Gửi: Tài liệu | Giá trị thấp")` | ✅ PASS | `TC-HOME-011__verify-nhan-vai-gui.png` | — |
| E1 | Nhãn vai hiển thị đúng chuỗi **"Gửi:"** | MCP khớp nguyên văn, tiền tố = `Gửi:` | ✅ PASS | ↑ | nhãn tô **màu cam**, tách khỏi phần loại hàng |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-HOME-011__verify-nhan-vai-gui.png` *(ảnh cắt đúng card đang assert)*
**Locators captured:** 1 element

---

## TC-HOME-012: Check section "Đơn của tôi" dùng nhãn "Giao:" khi tài khoản là người vận chuyển

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở Bảng tin, nhấn 1 tin, nhấn "Tôi mang giúp được" *(setup)* | **KHÔNG thực hiện được** — Bảng tin **0 tin** | ⚠️ lệch | `_recon__bang-tin-empty-0-tin.png` | tiền đề đã thoả sẵn bằng đơn cũ (A **đang là người vận chuyển** của 1 đơn) |
| 2 | Nhấn tab "Trang chủ" | đã ở Trang chủ, scroll tới card | ✅ PASS | — | — |
| 3 | Check nhãn vai ở dòng đầu section | `find_element(text="Giao: Quần áo | Giá trị thấp")` | ✅ PASS | `TC-HOME-012__verify-nhan-vai-giao.png` | — |
| E1 | Nhãn vai hiển thị đúng chuỗi **"Giao:"** | MCP khớp nguyên văn, tiền tố = `Giao:` | ✅ PASS | ↑ | nhãn tô **màu tím** |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-HOME-012__verify-nhan-vai-giao.png` *(ảnh cắt đúng card đang assert)*
**Locators captured:** 1 element
📨 **Quan sát spec gap (dẫn chứng nằm trong chính ảnh của TC này):** ngay phía trên card `Giao:` là card **`Nhận giao hàng Thuận đường`** — **không có nhãn vai** dạng `<Vai>:`. Đó là **tin OFFER**, không phải đơn, nhưng vẫn nằm chung section ⇒ route `/analyze-requirements`.
⚠️ **Khai báo lệch step:** không nhận đơn mới được (0 tin trên Bảng tin) ⇒ verify trên đơn **vai vận chuyển có sẵn** (badge `Đã giao`). Expected chỉ assert **chuỗi nhãn vai**, không assert trạng thái đơn ⇒ verdict tin được.

---

## TC-HOME-013: Check section "Đơn của tôi" dùng nhãn "Nhận:" khi tài khoản là người nhận

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Nhờ dev/QA seed 1 đơn đang hoạt động mà tài khoản là người nhận *(setup)* | **KHÔNG cần seed** — A đã có sẵn đơn vai người nhận | ⚠️ lệch | — | đơn có sẵn ở trạng thái `Đã huỷ` (⛔ không phải "đang hoạt động") |
| 2 | Đăng nhập FoxEco bằng tài khoản Receiver | tài khoản A | ✅ PASS | — | — |
| 3 | Check nhãn vai ở dòng đầu section | `find_element(text="Nhận: Đồ dễ vỡ | Giá trị vừa")` | ✅ PASS | `TC-HOME-013__verify-nhan-vai-nhan.png` | — |
| E1 | Nhãn vai hiển thị đúng chuỗi **"Nhận:"** | MCP khớp nguyên văn, tiền tố = `Nhận:` | ✅ PASS | ↑ | nhãn tô **màu xanh lục** |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-HOME-013__verify-nhan-vai-nhan.png` *(ảnh cắt đúng card đang assert)*
**Locators captured:** 1 element
⚠️ **Khai báo lệch step:** đơn dùng để verify đang ở trạng thái **`Đã huỷ`**, không phải *"đang hoạt động"* như Pre-condition. Expected chỉ assert **chuỗi nhãn vai** ⇒ verdict tin được, nhưng 📌 nếu QC muốn siết *"chỉ đơn đang hoạt động mới lên section này"* thì đó là **assert khác** và cần TC khác (⛔ `§10.5` FREEZE cấm thêm TC ⇒ đưa vào Notes của TC hiện có).
🟢 **3 nhãn vai đủ bộ, 3 màu phân biệt:** `Gửi:` cam · `Giao:` tím · `Nhận:` xanh lục.

📨 **SPEC GAP — route `/analyze-requirements`** *(2 mục, chi tiết + ảnh nằm ở `vibe-report.md §Phản hồi ngược`)*: (1) section "Đơn của tôi" còn card **`Nhận giao hàng Thuận đường`** **không có nhãn vai** dạng `<Vai>:` — đó là **tin OFFER**, `SC-HOME-011/012/013` ⛔ chưa đặc tả; (2) section hiển thị **cả đơn đã kết thúc** (`Đã huỷ`, `Đã giao`, 6 card) — ⚠️ mâu thuẫn cách hiểu *"đơn đang hoạt động"*, cần BA chốt phạm vi.

---

## TC-HOME-015: Check chạm section "Đơn của tôi" mở màn Theo dõi đơn của đúng đơn đang hiển thị

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng 1 tin NEED, ghi lại loại hàng + địa chỉ *(setup)* | dùng đơn có sẵn; **ghi lại từ chính card**: loại hàng `Tài liệu`, `Từ: Tòa V-City, Lê Thái Tổ`, `Đến: FPT Cầu Giấy` | ⚠️ lệch | `TC-HOME-015__pre-card-truoc-khi-cham.png` | không đăng được tin mới (bug `B1`) |
| 2 | Nhấn tab "Trang chủ" | đã ở Trang chủ | ✅ PASS | — | — |
| 3 | Chạm vào section "Đơn của tôi" | `find_element(descriptionStartsWith "Gửi: Tài liệu")` + `gesture(tap)` | ✅ PASS | — | — |
| E1 | Mở màn Theo dõi đơn có **loại hàng và địa chỉ trùng khớp** | đối chiếu 3 giá trị | ✅ PASS | `TC-HOME-015__verify-lo-trinh-khop.png` · `TC-HOME-015__verify-loai-hang-khop.png` | chi tiết ↓ |

**Đối chiếu card (Trang chủ) ↔ màn Theo dõi đơn:**

| Giá trị | Ghi ở card (step 1) | Trên màn Theo dõi đơn | Khớp |
|---|---|---|---|
| Địa chỉ lấy | `Từ: Tòa V-City, Lê Thái Tổ` | §LỘ TRÌNH → `Lấy hàng` = `Tòa V-City, Lê Thái Tổ` | ✅ |
| Địa chỉ giao | `Đến: FPT Cầu Giấy` | §LỘ TRÌNH → `Giao hàng` = `FPT Cầu Giấy` | ✅ |
| Loại hàng | `Tài liệu` | §THÔNG TIN HÀNG → `Loại hàng` = `Tài liệu` | ✅ |
| *(thêm)* Giá trị | `Giá trị thấp` | §THÔNG TIN HÀNG → `Giá trị` = `Giá trị thấp` | ✅ |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-HOME-015__verify-lo-trinh-khop.png` + `screenshots/TC-HOME-015__verify-loai-hang-khop.png` (+ `TC-HOME-015__pre-card-truoc-khi-cham.png`)
**Locators captured:** 1 element (card — `descriptionStartsWith("Gửi: Tài liệu")`)
ℹ️ Đơn dùng để verify là **dữ liệu thừa của `VR-001`** — Ghi chú đơn ghi nguyên văn `Test vibe VR-001 TC-USR-026`.
🔧 **Locator bền cho card đơn:** `-android uiautomator` + `descriptionStartsWith("<Nhãn vai>: <Loại hàng>")` — `content-desc` của card là **chuỗi gộp cả 5 dòng**, ⛔ đừng khớp full string.

---

## TC-HOME-002: Check các màn con không hiển thị bottom nav mà chỉ có nút quay lại

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập FoxEco *(setup)* | tài khoản A | ✅ PASS | — | — |
| 2 | Bảng tin → nhấn 1 tin → **Chi tiết tin**; check vùng dưới | **KHÔNG mở được** — Bảng tin **0 tin** | 🚫 **BLOCKED** | `TC-HOME-002__step2-BLOCKED-bang-tin-0-tin.png` | không có tin nào để nhấn ⇒ **không tồn tại màn Chi tiết tin để kiểm** |
| 3 | Theo dõi đơn; check vùng dưới | `find_element("Trang chủ")` → **NOT FOUND** | ✅ PASS | `TC-HOME-002__verify-theo-doi-don-khong-bottom-nav.png` | không bottom nav; **có** nút quay lại góc trên-trái |
| 4 | Wizard "+ Đăng tin"; check vùng dưới | quan sát màn `Đăng tin mới` | ✅ PASS | `TC-HOME-002__verify-wizard-khong-bottom-nav.png` | không bottom nav; **có** nút quay lại |
| 5 | Màn Thông báo; check vùng dưới | `find_element("Trang chủ")` → **NOT FOUND** | ✅ PASS | `TC-HOME-002__verify-thong-bao-khong-bottom-nav.png` | không bottom nav; **có** nút quay lại |

**Result: 🚫 BLOCKED at Step 2** — 3/4 màn con verify được (step 3·4·5 đều ✅), **màn Chi tiết tin không dựng được**
**Reason:** Bảng tin **0 tin hợp lệ toàn hệ thống** ⇒ không mở được màn Chi tiết tin ⇒ **E của step 2 không đánh giá được**.
**Evidence:** `screenshots/TC-HOME-002__step2-BLOCKED-bang-tin-0-tin.png` (+ 3 ảnh `__verify-*` của step 3/4/5)
**Impact:** verdict **BLOCKED** (không phải FAIL — ⛔ app không sai ở đây). Chạy lại khi STG có ≥1 tin: `/vibe-test --tc TC-HOME-002`.
📌 **Ghi rõ để khỏi hiểu nhầm:** 3 màn con còn lại **ĐÃ kiểm và đều đúng**, nhưng theo luật *"mọi Expected phải đánh giá được"* thì TC chưa đóng được ⇒ **KHÔNG** khai là PASS một phần, ⛔ **KHÔNG** tính vào coverage như đã phủ.

---

## TC-HOME-016: Check nhấn "Xem tất cả" ở section "Đơn của tôi" mở màn Hoạt động

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng 1 tin NEED qua wizard "+ Đăng tin" *(setup)* | dùng đơn có sẵn của tài khoản A | ⚠️ lệch | — | cùng lý do `TC-HOME-009` (bug `B1` chặn đăng tin) |
| 2 | Nhấn tab "Trang chủ" | tap `accessibility id "Trang chủ"` | ✅ PASS | — | — |
| 3 | Nhấn "Xem tất cả" ở section "Đơn của tôi" | `scroll_to_element` + `find_element(accessibility id "Xem tất cả")` + `gesture(tap)` | ✅ PASS | `TC-HOME-016__verify-mo-man-hoat-dong.png` | — |
| E1 | Mở màn **Hoạt động** | đối chiếu màn + trạng thái bottom nav | ✅ PASS | ↑ | màn tiêu đề **`Đơn của tôi`** với 2 tab con `Đang diễn ra` / `Đã hoàn thành`; tab **`Hoạt động`** trên bottom nav chuyển sang **active** (cam + chấm chỉ báo) |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-HOME-016__verify-mo-man-hoat-dong.png`
**Locators captured:** 1 element (`accessibility id "Xem tất cả"` — nâng từ ⚠️ Inferred của VR-001 lên ✅ Verified)
ℹ️ **Tên màn ≠ tên tab:** tab bottom nav ghi **`Hoạt động`** nhưng tiêu đề màn ghi **`Đơn của tôi`** — khớp mô tả module `TC-05 ACT` trong `Project_rule §Module Codes` (*"Hoạt động (Đơn của tôi)"*). ⛔ Đừng coi là sai điều hướng.
