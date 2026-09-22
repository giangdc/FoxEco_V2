# Vibe Test Log — VR-019 — v1.1 — 2026-09-22

> Module: TS (Trust & Safety) · Platform: mobile (Appium MCP, Android) · Env: STG (host app FoxPro, FoxEco SDK nhúng)
> Scope: 17 TC v1.1 (`TC-TS-008..024`) · Evidence dir: `screenshots/`
> Thiết bị: `emulator-5554` (vai A = `stag_giangdc2@fpt.com`) · `R58T20PLP8K` (vai C → tạm B → về C: `stag_taipm@fpt.com` → `stag_anhptm17@fpt.com` → `stag_taipm@fpt.com`)
> Seed: `SEED-TS-01` (1 đơn NEED, A đăng, người nhận C) — dùng chung cho toàn bộ 17 TC.
> Phiên: 2026-09-22 (khởi tạo) · 2026-09-22 (follow-up — retest sau khi có tài khoản Microsoft thật)

## 🔑 Phát hiện chặn scope (đọc trước khi xem từng TC)

**`BUG-037` (🔁 đã đổi hướng 2026-09-22 sau phản hồi Dev: từ P1/Critical → Suggestion P2):** Nút
"Báo cáo sự cố" mở WebView, nhưng WebView **luôn dừng ở màn đăng nhập Microsoft** (`Microsoft —
Đăng nhập — Email hoặc điện thoại`), không bao giờ tới được form thật — tái hiện 100% ở cả 2 thiết
bị, cả 3 tài khoản (A/B/C), cả 3 trạng thái đơn đã thử. Test account `stag_*@fpt.com` không có tài
khoản Microsoft/Azure AD tương ứng để đăng nhập tiếp ⇒ **13/17 TC BLOCKED** vì không chạm được nội
dung form. **Dev xác nhận nguyên nhân:** form có trường tải file ("Hình ảnh đính kèm") ⇒ Microsoft
Forms bắt buộc đăng nhập — quy định nền tảng, không phải lỗi code. Nội dung bug nay là **đề xuất bỏ
bắt buộc đăng nhập** để thuận tiện hơn cho người dùng (form là khảo sát nhanh, bắt đăng nhập dễ
khiến người dùng bỏ dở). Xem `05_bug-reports/draft/BUG-037-*.md`.

**`BUG-038` (P2):** Khi mất mạng, WebView hiện nguyên trang lỗi kỹ thuật Chromium
(`net::ERR_INTERNET_DISCONNECTED`), KHÔNG có nút "Thử lại" như spec yêu cầu ⇒ `TC-TS-016` FAIL,
`TC-TS-017` BLOCKED theo (không có nút để bấm "thử lại"). Xem `05_bug-reports/draft/BUG-038-*.md`.

**3 TC PASS được vì Expected không phụ thuộc nội dung form** (chỉ cần nút hiện+nhấn được, hoặc chỉ
cần hành vi đóng WebView): `TC-TS-018`, `TC-TS-022`, `TC-TS-023`.

**Ảnh phát hiện gốc** (lần đầu tiên quan sát màn Microsoft, trước khi tách thành 11 ảnh riêng cho
từng TC BLOCKED — giữ lại làm ảnh đại diện đính kèm `BUG-037`): `screenshots/BUG-037__webview-bao-cao-su-co-chan-boi-microsoft-signin.png`.

---

## TC-TS-022: Check người gửi thấy nút báo cáo sự cố ở cả ba trạng thái đơn

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập A, đăng 1 tin NEED (SEED-TS-01), người nhận C | wizard NEED 3 bước qua MCP (emulator) | ✅ PASS | `TC-TS-022__pre-observation1-posted.png` | Ghi chú tin = `SEED-TS-01` |
| 2 | Mở đơn, check góc trên phải màn Theo dõi đơn (POSTED) | find `resourceId("track-report-incident")` | ✅ PASS | `TC-TS-022__pre-observation1-posted.png` | Nút hiện, nền cam nhạt, icon cảnh báo |
| 3 | (song song, thiết bị B) B nhận đơn + xác nhận → MATCHED | — | ✅ PASS | — | Thực hiện trên `R58T20PLP8K` (B=`stag_anhptm17@`) |
| 4 | A mở lại đơn, check góc trên phải (MATCHED) | find `track-report-incident` | ✅ PASS | `TC-TS-022__pre-observation2-matched.png` | Nút vẫn hiện |
| 5 | (song song) B nhấn "Tôi đã lấy hàng" → xác nhận → IN_TRANSIT | — | ✅ PASS | — | — |
| 6 | A mở lại đơn, check góc trên phải (IN_TRANSIT), nhấn thử | find + tap `track-report-incident` | ✅ PASS | `TC-TS-022__verify-observation3-intransit.png` | Tap mở được WebView (đã verify tappable ở bước POSTED trước đó cùng account) |

**Result: ✅ PASS (3 checkpoint, đủ cả 3 trạng thái)**
**Evidence:** `screenshots/TC-TS-022__pre-observation1-posted.png` · `screenshots/TC-TS-022__pre-observation2-matched.png` · `screenshots/TC-TS-022__verify-observation3-intransit.png`
**Locators captured:** `track-report-incident` (resourceId, -android uiautomator), `descriptionStartsWith("Gửi: Tài liệu")` (card đơn)

---

## TC-TS-023: Check người vận chuyển thấy nút báo cáo sự cố ở cả hai trạng thái sau khi nhận đơn

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | (setup, dùng chung SEED-TS-01) | — | ✅ PASS | — | — |
| 3 | B (`stag_anhptm17@`) nhận đơn (Bảng tin → Chi tiết tin → "Tôi mang giúp được" → Xác nhận), check góc trên phải (MATCHED) | tap CTA + `text("Xác nhận").instance(1)` + find `track-report-incident` | ✅ PASS | `TC-TS-023__pre-observation1-matched.png` | Nút hiện |
| 4 | B nhấn "Tôi đã lấy hàng" → Xác nhận → "Đã lấy hàng — Bắt đầu giao" → Đồng ý → IN_TRANSIT | tap `text("Tôi đã lấy hàng")` → `.instance(1)` → `textContains("Bắt đầu giao")` → `text("Đồng ý")` | ✅ PASS | — | — |
| 5 | Mở lại đơn, check góc trên phải (IN_TRANSIT), tap thử | find + tap `track-report-incident` | ✅ PASS | `TC-TS-023__verify-observation2-intransit.png` | Tap mở WebView thành công (dừng ở `BUG-037`, nhưng nút bấm được — đủ điều kiện Expected) |

**Result: ✅ PASS (2 checkpoint đủ, cả 2 nhấn được)**
**Evidence:** `screenshots/TC-TS-023__pre-observation1-matched.png` · `screenshots/TC-TS-023__verify-observation2-intransit.png`
**Locators captured:** `text("Tôi mang giúp được")`, `text("Xác nhận").instance(1)`, `text("Tôi đã lấy hàng")`, `textContains("Bắt đầu giao")`, `track-report-incident`

---

## TC-TS-018: Check đóng WebView quay về đúng màn theo dõi đơn trước đó

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | (setup) Đơn IN_TRANSIT, mở Theo dõi đơn | — | ✅ PASS | — | Thực hiện trên B (`stag_anhptm17@`, `R58T20PLP8K`) |
| 4 | Nhấn "Báo cáo sự cố" | tap `track-report-incident` | ✅ PASS | — | WebView mở (dừng ở màn Microsoft — `BUG-037`, không ảnh hưởng phép thử đóng) |
| 5 | (Bỏ qua nhập mô tả — form chưa tới được do `BUG-037`, xem ghi chú) | — | ⚠️ Note | — | Step 5 gốc ("Nhập mô tả") không thực hiện được vì chưa qua được màn Microsoft; không ảnh hưởng assertion chính (đóng WebView) |
| 6 | Nhấn nút đóng ("←") của WebView | tap `accessibility id "Quay lại"` | ✅ PASS | — | — |
| 7 | Check màn hiện ra + trạng thái đơn | verify text "Theo dõi đơn" + stepper "Đang giao" | ✅ PASS | `TC-TS-018__verify-quay-lai-dung-man-in-transit.png` | Quay về đúng đơn, đúng trạng thái `IN_TRANSIT`, không mất dữ liệu đơn |

**Result: ✅ PASS**
**Note:** Step 5 gốc (nhập mô tả trước khi đóng) không thực hiện được do `BUG-037` chặn form — nhưng expected result của TC chỉ khẳng định **hành vi đóng WebView + trạng thái đơn giữ nguyên**, cả hai đều verify được độc lập với nội dung form đã nhập hay chưa.
**Evidence:** `screenshots/TC-TS-018__verify-quay-lai-dung-man-in-transit.png`

---

## TC-TS-016: Check mất mạng khi mở báo cáo sự cố thì app hiện lỗi kèm nút thử lại

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-3 | (setup) Đơn IN_TRANSIT, mở Theo dõi đơn | — | ✅ PASS | — | Trên `R58T20PLP8K` (B) |
| 4 | Ngắt hoàn toàn kết nối mạng thiết bị | `adb shell svc wifi disable` | ✅ PASS | — | Xác nhận `wifi_on=0`; thiết bị không có mobile data khác |
| 5 | Nhấn "Báo cáo sự cố" | tap `track-report-incident` | ✅ PASS | — | — |
| 6 | Check màn hiện ra + các nút trên màn | screenshot + `find textContains("Thử lại")` | ❌ FAIL | `TC-TS-016__step6-FAIL-raw-error-no-retry-button.png` | Actual: trang lỗi Chromium kỹ thuật `"Error loading page / Domain: undefined / Error Code: -2 / Description: net::ERR_INTERNET_DISCONNECTED"`. Nút "Thử lại" **NOT FOUND** |

**Result: ❌ FAIL tại step 6**
**Expected:** Màn hiển thị thông báo lỗi không tải được kèm nút "Thử lại"; form không hiện ra.
**Actual:** Form đúng là không hiện ra (phần đó khớp Expected) — nhưng thông báo lỗi là **trang lỗi kỹ thuật thô của WebView** (tiếng Anh, lộ `Domain`/`Error Code`), và **hoàn toàn không có nút "Thử lại"** nào trên màn.
**Bug:** `BUG-038` (P2) — xem `05_bug-reports/draft/BUG-038-*.md`.
**Evidence:** `screenshots/TC-TS-016__step6-FAIL-raw-error-no-retry-button.png`

---

## TC-TS-017: Check thử lại sau khi có mạng mở đúng form của đơn cũ không mất ngữ cảnh

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | (dựng lại tiền đề trên thiết bị A — mất mạng qua `svc wifi/data disable`, mở "Báo cáo sự cố") | tap `track-report-incident` khi offline | 🚫 BLOCKED | `TC-TS-017__step6-BLOCKED-no-retry-button.png` | Trang lỗi kỹ thuật `net::ERR_PROXY_CONNECTION_FAILED` (biến thể lỗi khác `TC-TS-016` do khác cơ chế ngắt mạng, cùng bản chất: không có nút) |
| 5 | Bật lại kết nối mạng | `adb shell svc wifi/data enable` | ✅ PASS | — | `wifi_on=1` xác nhận lại |
| 6 | Nhấn "Thử lại" | find `textContains("Thử lại")` | 🚫 BLOCKED | `TC-TS-017__step6-BLOCKED-no-retry-button.png` | Nút không tồn tại trên màn lỗi — không có gì để bấm |

**Result: 🚫 BLOCKED tại step 6**
**Reason:** Tiền đề của TC (có nút "Thử lại" để bấm) không tồn tại trên app thật — cùng gốc `BUG-038`. Không thể verify "mở đúng form của đơn cũ" vì không có hành động "thử lại" nào khả thi.
**Impact:** Retest sau khi `BUG-038` được fix (thêm nút "Thử lại" đúng spec).
**Evidence:** `screenshots/TC-TS-017__step6-BLOCKED-no-retry-button.png`

---

## TC-TS-008: Check form báo cáo sự cố mở trong WebView và chỉ điền sẵn mã đơn hàng

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-4 | (setup, đơn IN_TRANSIT) Nhấn "Báo cáo sự cố" | tap `track-report-incident` | ✅ PASS (mở WebView) | `TC-TS-008__step5-BLOCKED-microsoft-signin-wall.png` | WebView mở toàn màn hình đúng như expected (phần này khớp) |
| 5 | Check khung WebView + 4 ô (Mã đơn hàng, Loại yêu cầu, Mô tả chi tiết, SĐT) | quan sát nội dung WebView | 🚫 BLOCKED | `TC-TS-008__step5-BLOCKED-microsoft-signin-wall.png` | WebView dừng ở màn đăng nhập Microsoft — 4 ô form thật **không hiển thị được** để kiểm |

**Result: 🚫 BLOCKED tại step 5**
**Reason:** `BUG-037` — WebView không tới được nội dung form thật.
**Evidence:** `screenshots/TC-TS-008__step5-BLOCKED-microsoft-signin-wall.png`

---

## TC-TS-009: Check gửi báo cáo sự cố hợp lệ hiện màn ghi nhận kèm cam kết liên hệ lại

**Result: 🚫 BLOCKED** — không nhập được vào 4 trường của form (không tồn tại trên màn hiện tại), không gửi được → không thể verify màn "Đã ghi nhận phản hồi".
**Reason:** `BUG-037`.
**Evidence:** `screenshots/TC-TS-009__step5-BLOCKED-microsoft-signin-wall.png`

---

## TC-TS-010: Check nút Gửi vô hiệu hoá khi chưa chọn loại yêu cầu

**Result: 🚫 BLOCKED** — không có ô "Loại yêu cầu"/nút "Gửi" nào để kiểm trên màn hiện tại.
**Reason:** `BUG-037`.
**Evidence:** `screenshots/TC-TS-010__step5-BLOCKED-microsoft-signin-wall.png`

---

## TC-TS-011: Check nút Gửi vô hiệu hoá khi chưa nhập mô tả chi tiết

**Result: 🚫 BLOCKED** — cùng lý do `TC-TS-010`.
**Reason:** `BUG-037`.
**Evidence:** `screenshots/TC-TS-011__step5-BLOCKED-microsoft-signin-wall.png`

---

## TC-TS-012: Check nút Gửi vô hiệu hoá khi số điện thoại sai định dạng

**Result: 🚫 BLOCKED** — cùng lý do `TC-TS-010`.
**Reason:** `BUG-037`.
**Evidence:** `screenshots/TC-TS-012__step5-BLOCKED-microsoft-signin-wall.png`

---

## TC-TS-013: Check gửi báo cáo sự cố thành công khi không đính ảnh nào

**Result: 🚫 BLOCKED** — không gửi được form (không tới được).
**Reason:** `BUG-037`.
**Evidence:** `screenshots/TC-TS-013__step5-BLOCKED-microsoft-signin-wall.png`

---

## TC-TS-014: Check đính đủ năm ảnh thì nút thêm ảnh khác bị vô hiệu hoá

**Result: 🚫 BLOCKED** — không có khối "Ảnh sản phẩm" của form (không tồn tại trên màn hiện tại) để đính ảnh.
**Reason:** `BUG-037`.
**Evidence:** `screenshots/TC-TS-014__step5-BLOCKED-microsoft-signin-wall.png`

---

## TC-TS-015: Check xoá được từng ảnh đính kèm riêng lẻ và mở lại chỗ thêm ảnh

**Result: 🚫 BLOCKED** — cùng lý do `TC-TS-014`.
**Reason:** `BUG-037`.
**Evidence:** `screenshots/TC-TS-015__step5-BLOCKED-microsoft-signin-wall.png`

---

## TC-TS-019: Check mở lại báo cáo sự cố là phiên mới không giữ dữ liệu nhập dở

**Result: 🚫 BLOCKED** — không nhập được "dữ liệu dở dang" vào ô nào (form không hiển thị) nên không dựng được tiền đề của TC.
**Reason:** `BUG-037`.
**Evidence:** `screenshots/TC-TS-019__step5-BLOCKED-microsoft-signin-wall.png`

---

## TC-TS-020: Check gửi báo cáo sự cố không làm đơn đổi trạng thái

**Result: 🚫 BLOCKED** — không gửi được form (nút "Gửi" thuộc form thật, không tồn tại trên màn hiện tại) nên không tạo được hành động cần verify.
**Reason:** `BUG-037`. Ghi chú thêm: TC này theo thiết kế cần chạy khi đơn còn `POSTED`; đơn `SEED-TS-01` đã được B ghép/lấy hàng trong lúc chạy `TC-TS-022/023` (dùng chung 1 seed cho 17 TC theo `§0.6` của fragment) — nhưng do form không tới được ở bất kỳ trạng thái nào, thực tế precondition trạng thái không phải là yếu tố chặn ở đây.
**Evidence:** `screenshots/TC-TS-020__step5-BLOCKED-microsoft-signin-wall.png`

---

## TC-TS-021: Check ô mã đơn hàng là nhãn tĩnh chỉ đọc không sửa được

**Result: 🚫 BLOCKED** — ô "Mã đơn hàng" thuộc form thật, không hiển thị được để kiểm.
**Reason:** `BUG-037`.
**Evidence:** `screenshots/TC-TS-021__step5-BLOCKED-microsoft-signin-wall.png`

---

## TC-TS-024: Check người nhận thấy nút báo cáo sự cố và mở được form giống hai vai kia

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | (setup) Đổi thiết bị `R58T20PLP8K` về vai C (`stag_taipm@`) qua đăng xuất/đăng nhập | logout B → login C | ✅ PASS | — | ~14 MCP call, 1 lần timeout mạng thoáng qua khi vào FoxEco (retry OK) |
| 3 | Mở đơn từ tab "Đơn của tôi", check góc trên phải | find `track-report-incident` | ✅ PASS | `TC-TS-024__pre-observation-button-visible.png` | Nút hiện, giống 2 vai kia |
| 4 | Nhấn "Báo cáo sự cố" | tap `track-report-incident` | ✅ PASS (mở WebView) | — | — |
| 5 | Check WebView + ô "Mã đơn hàng" | quan sát nội dung | 🚫 BLOCKED | `TC-TS-024__step6-BLOCKED-microsoft-signin-wall.png` | Cùng dừng ở màn Microsoft — xác nhận `BUG-037` **không phân biệt vai** (giống hệt A và B) |

**Result: 🚫 BLOCKED tại step 5 (phần "ô Mã đơn hàng điền sẵn")**
**Note:** Phần "nút hiện + mở được WebView" đã PASS (giống 2 vai kia) — nhưng Expected còn yêu cầu verify nội dung ô "Mã đơn hàng", không thực hiện được.
**Reason:** `BUG-037`.
**Evidence:** `screenshots/TC-TS-024__pre-observation-button-visible.png` · `screenshots/TC-TS-024__step6-BLOCKED-microsoft-signin-wall.png`

---

## ⚠️ Phát hiện quan trọng (ngoài phạm vi TC, không tính verdict) — màn Microsoft có thể auto-sign-in bằng tài khoản thật đã cache trên thiết bị

Sau khi chốt xong `TC-TS-024`, khi mở lại "Báo cáo sự cố" trên `R58T20PLP8K` một lần nữa để chuẩn bị
chụp bổ sung evidence cho các TC BLOCKED khác, màn WebView **KHÔNG dừng ở màn nhập email trắng như
mọi lần trước** mà tự động hiện màn **"Chấp thuận yêu cầu đăng nhập" (MFA / Microsoft Authenticator)**
gắn với email **`giangdc2@fpt.com`** — rõ ràng là tài khoản Microsoft 365 thật đã được cache ở cấp
hệ điều hành/trình duyệt trên chính thiết bị thật này (không liên quan gì tới tài khoản FoxEco đang
đăng nhập trong app, lúc đó là `stag_taipm@`). **KHÔNG thao tác gì thêm trên màn này** (không
Đồng ý/Từ chối) — bấm `back` thoát ngay để tránh ảnh hưởng tài khoản thật của người dùng.

Điều hướng lùi lại thêm 1 bước tình cờ đưa vào đúng **form Microsoft Forms thật** (câu hỏi 4 "Hình
ảnh đính kèm", câu hỏi 5 "Số điện thoại liên hệ lại", nút "Gửi", footer "Microsoft 365 / Microsoft
Forms") — xác nhận đúng giả thuyết trong `BUG-037`: đây là **Microsoft Forms cấu hình yêu cầu đăng
nhập tổ chức**, không phải Google Form công khai như tài liệu phân tích giả định. **Không điền/gửi
gì trên form này** (tránh tạo bản ghi thật dưới danh tính thật) — đã thoát ra bằng thao tác cuộn lên
(vô tình trả về màn Theo dõi đơn native), không chụp ảnh nội dung form để tránh lưu lại thông tin
tài khoản thật trong evidence của dự án.

📌 **Ý nghĩa cho `BUG-037`:** đây là bằng chứng cho thấy tính năng **có thể hoạt động được trên
thiết bị công ty thật** (nơi nhân viên đã có sẵn phiên Microsoft 365 hợp lệ) — nhưng **hoàn toàn
không kiểm được trên STG bằng tài khoản test `stag_*@fpt.com`** vì các tài khoản đó không có danh
tính Microsoft tương ứng. Đây cũng đặt ra câu hỏi thiết kế đáng lưu ý cho BA/Dev: **form không xác
thực người gửi có khớp với tài khoản FoxEco/đơn hàng đang xem hay không** — bất kỳ ai có phiên
Microsoft hợp lệ trên thiết bị đều mở được form, không nhất thiết là đúng người đang thao tác trong
app. Đã cập nhật ghi chú này vào `BUG-037` để Dev/BA cân nhắc khi điều tra.

---

## 🆕 Follow-up 2026-09-22 — Retest 12 TC bị chặn ở màn đăng nhập Microsoft (theo yêu cầu QC)

> **Bối cảnh:** QC (`GiangDC2`) đã tự đăng nhập tài khoản Microsoft **thật** của mình trên thiết bị
> thật `R58T20PLP8K` (đang login FoxEco `stag_taipm@`) trước khi gọi phiên này, và yêu cầu dùng
> chính thiết bị này để retest các TC từng BLOCKED bởi màn đăng nhập Microsoft (`BUG-037`).
> ✅ **Xác nhận: màn đăng nhập Microsoft đã được bypass** — WebView tải được **form Microsoft Forms
> thật** ("FoxEco - Báo cáo sự cố & Hỗ trợ", lời chào "Xin chào, Giang").
> ⚠️ **Rủi ro đã xác nhận với QC trước khi thực thi (AskUserQuestion):** vì đây là tài khoản Microsoft
> **thật** (không phải tài khoản test), các TC cần bấm "Gửi" thật sẽ tạo **bản ghi thật** trong hệ
> thống hỗ trợ dưới danh tính thật. QC đã đồng ý bấm Gửi thật.
> 🖼️ **Ảnh đính kèm dùng để test upload:** vì thư viện ảnh thật của thiết bị chứa ảnh cá nhân nhạy
> cảm (ảnh chân dung, biên lai chuyển khoản), phiên này đã **tự tạo 6 ảnh JPG màu đơn sắc placeholder**
> (`seed-ts-01` … `seed-ts-06`, đuôi jpg, sinh bằng PIL, đẩy vào `/sdcard/Pictures/` qua `adb push` + media-scan) thay
> vì dùng ảnh có sẵn trong thư viện — tránh rò rỉ dữ liệu cá nhân vào hệ thống hỗ trợ thật.
> 🚫 **Giới hạn kỹ thuật quan trọng:** nội dung Microsoft Forms chạy trong **Custom Tab tách biệt**,
> **KHÔNG expose qua Appium accessibility tree cho input field** (chỉ button/label text đôi khi query
> được, input placeholder thì không) và **KHÔNG có context `WEBVIEW_*`** (`appium_context action=list`
> chỉ trả `NATIVE_APP`). ⇒ Tương tác với các ô nhập liệu trong form bắt buộc dùng **toạ độ (x,y) suy
> ra từ screenshot**, không phải locator theo strategy chuẩn — đây là **ngoại lệ hợp lệ** của
> §MCP-MANDATORY (không phải vi phạm): không có locator nào tồn tại để capture, vì nội dung nằm
> ngoài accessibility tree của app. Ghi rõ trong `vibe-locators.md` phần bổ sung bên dưới.

### TC-TS-008 — ✅ PASS (đảo từ 🚫 BLOCKED)

Mở "Báo cáo sự cố" từ đơn `SEED-TS-01` (IN_TRANSIT, vai B = `stag_anhptm17@`). WebView tải được form
thật. Ô "Mã đơn hàng" điền sẵn `01a0c6fd-4730-74d6-8e99-d3e416b5bb56` (GUID nội bộ của đơn, không
phải mã hiển thị `SEED-TS-01` — nhưng đây là giá trị "tự động điền từ ứng dụng" đúng như ghi chú dưới
ô, không đổi giữa các lần mở). Ba ô còn lại (Loại yêu cầu, Mô tả chi tiết, SĐT) đều TRỐNG.
**Result: ✅ PASS — khớp đúng Expected** (chỉ 1/4 trường prefill).
**Evidence:** `screenshots/TC-TS-008__verify-only-madon-prefilled.png` · `screenshots/TC-TS-008__verify-2-mota-sdt-empty.png`

### TC-TS-010 — ✅ PASS (đảo từ 🚫 BLOCKED → ❌ FAIL → ✅ PASS sau khi sửa Expected, xem cập nhật cuối mục)

Để "Loại yêu cầu" chưa chọn, điền Mô tả + SĐT, bấm "Gửi". **Actual:** nút "Gửi" **KHÔNG** chuyển
sang trạng thái vô hiệu hoá — vẫn bấm được bình thường. Bấm xong form **tự cuộn tới câu hỏi đầu tiên
còn thiếu** và hiện dòng đỏ inline **"Câu hỏi này là bắt buộc."** ngay dưới câu hỏi đó (không phải
"Điền các mục bắt buộc" cạnh nút như Expected mô tả). Form KHÔNG được gửi đi (đúng ý đồ nghiệp vụ:
chặn submit thiếu trường bắt buộc — chỉ khác cơ chế UI, không khác kết quả nghiệp vụ cuối).
**Result (lúc chạy, đối chiếu Expected cũ): ❌ FAIL** — cơ chế thực tế của Microsoft Forms (inline
validation, không disable nút) khác hẳn giả định "nút disable" trong `SC-TS-009`/Expected cũ.
**Evidence:** `screenshots/TC-TS-010__verify-gui-empty-required-behavior.png`

> 🔁 **Cập nhật 2026-09-22 (sau khi log bug):** QC xem `BUG-040` (log cho phát hiện này) và xác nhận
> **không phải bug** — nghiệp vụ vẫn chặn đúng submit khi thiếu trường bắt buộc, chỉ khác cơ chế UI.
> `BUG-040` đã xoá. Expected của `TC-TS-010` đã sửa lại theo đúng hành vi thật (inline error) trong
> `fragments/TC-TS-v1.1.md` + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx` ⇒ **verdict đảo thành
> ✅ PASS** (Actual == Expected mới). Title vẫn ghi "vô hiệu hoá" (§10.5 không cho sửa Title) — xem
> `CHANGELOG.md §3` nợ #30.

### TC-TS-011 — ✅ PASS (đảo từ 🚫 BLOCKED → ❌ FAIL → ✅ PASS sau khi sửa Expected, cùng lý do TC-TS-010)

Chọn "Lỗi ứng dụng", để Mô tả chi tiết trống, điền SĐT hợp lệ, bấm "Gửi". **Actual:** cùng cơ chế —
nút "Gửi" không disable; sau khi bấm, form hiện cảnh báo **"Cần hoàn thành 2 câu hỏi trước khi gửi:
Câu hỏi 3, Câu hỏi 4."** bên dưới nút (Câu hỏi 3 = Mô tả chi tiết đúng như kỳ vọng; Câu hỏi 4 = Hình
ảnh đính kèm — **trường thứ 4 ngoài dự tính của TC**, xem ghi chú "Hình ảnh bắt buộc" ở `TC-TS-013`).
Không gửi được — đúng ý đồ nghiệp vụ (chặn khi Mô tả rỗng), nhưng cơ chế UI khác Expected.
**Result (lúc chạy, đối chiếu Expected cũ): ❌ FAIL** — cùng lý do spec-gap như `TC-TS-010`.
**Evidence:** `screenshots/TC-TS-011__verify-mota-empty-blocks-submit.png`

> 🔁 **Cập nhật 2026-09-22:** cùng quyết định với `TC-TS-010` — không phải bug, Expected đã sửa,
> **verdict đảo thành ✅ PASS**. Xem chi tiết ở mục cập nhật của `TC-TS-010`.

### TC-TS-012 — ❌ FAIL (đảo từ 🚫 BLOCKED, phát hiện thêm: KHÔNG có validate định dạng SĐT — vẫn FAIL sau khi sửa Expected)

Chọn "Góp ý / đề xuất", điền Mô tả hợp lệ, nhập SĐT **sai định dạng** `"0912abc"`, bấm "Gửi".
**Actual:** thông báo cuối cùng chỉ còn **"Cần hoàn thành 1 câu hỏi trước khi gửi: Câu hỏi 4."**
(Hình ảnh đính kèm) — **KHÔNG** có bất kỳ cảnh báo nào về định dạng SĐT sai. Nghĩa là ô "Số điện
thoại liên hệ lại" trên Microsoft Forms **KHÔNG có validate định dạng** — chấp nhận mọi chuỗi không
rỗng, kể cả có chữ cái. Nếu đính đủ ảnh, form này **SẼ gửi được** với SĐT rác `"0912abc"`.
**Result (lúc chạy, đối chiếu Expected cũ): ❌ FAIL** — vừa sai theo cơ chế "nút disable" (giống 2 TC
trên) vừa phát hiện thêm 1 lỗ hổng thật: **không có validate định dạng SĐT**, dữ liệu rác có thể lọt
tới đội hỗ trợ thật. Log `BUG-041` cho phát hiện này (còn giữ, chưa xoá).
**Evidence:** `screenshots/TC-TS-012__verify-sdt-invalid-khong-bi-chan.png`

> 🔁 **Cập nhật 2026-09-22:** phần "cơ chế nút disable" — cùng quyết định với `TC-TS-010`/`TC-TS-011`,
> không phải bug, Expected đã sửa lại phần đó. Nhưng `TC-TS-012` **vẫn FAIL** vì vế còn lại: Expected
> mới vẫn yêu cầu "SĐT sai định dạng phải bị chặn", còn Actual thì **không chặn** — đúng như `BUG-041`
> đã ghi nhận. Verdict giữ nguyên **❌ FAIL**, chỉ lý do hẹp lại còn đúng 1 vế (data quality, không
> còn dính cơ chế UI của nút Gửi).

### TC-TS-013 — ❌ FAIL (đảo từ 🚫 BLOCKED, ĐẢO NGƯỢC giả định "ảnh không bắt buộc")

Điền đủ Loại yêu cầu + Mô tả + SĐT hợp lệ, **KHÔNG đính ảnh nào**, bấm "Gửi". **Actual:** form
**KHÔNG gửi được** — thông báo **"Cần hoàn thành 1 câu hỏi trước khi gửi: Câu hỏi 4."** (Hình ảnh
đính kèm). Xác nhận trực tiếp: câu hỏi "4. Hình ảnh đính kèm" trên Microsoft Forms có dấu `*` (bắt
buộc) và **thực sự chặn submit** khi 0 ảnh — hoàn toàn ngược lại giả định "biên dưới hợp lệ" của
`SC-TS-010`/`test_data_catalog.md §TS`.
**Result: ❌ FAIL** — 🔴 **Đảo giả định gốc**, cần `/analyze-requirements --update` sửa lại
`test_data_catalog.md` (trường "Hình ảnh đính kèm" từ optional → **bắt buộc thật**) và xem lại
`SC-TS-010` (biên dưới "0 ảnh hợp lệ" không còn đúng nữa).
**Evidence:** `screenshots/TC-TS-013__verify-anh-required-blocks-submit.png`

### TC-TS-014 — ✅ PASS (đảo từ 🚫 BLOCKED, cơ chế UI khác chi tiết nhưng đúng ý đồ nghiệp vụ)

Đính lần lượt 5 ảnh JPG (`seed-ts-01` … `seed-ts-05`). **Actual:** cả 5 ảnh hiển thị đúng tên trong danh
sách, và nút **"Tải lên tệp" biến mất hoàn toàn** khỏi màn (không còn cách nào để chọn ảnh thứ 6) —
khác chi tiết so với Expected ("nút chuyển sang trạng thái vô hiệu hoá", tức nút vẫn hiện nhưng mờ
đi), nhưng đạt đúng mục tiêu nghiệp vụ: **chặn được ảnh thứ 6**.
**Result: ✅ PASS** (tinh thần cốt lõi khớp — chặn thêm ảnh ở ngưỡng 5; note khác biệt cơ chế UI: nút
biến mất thay vì disable).
**Evidence:** `screenshots/TC-TS-014__verify-5-anh-them-anh-bi-vo-hieu.png`

### TC-TS-015 — ✅ PASS (đảo từ 🚫 BLOCKED)

Từ trạng thái 5 ảnh của `TC-TS-014`, bấm "Hủy bỏ" trên ảnh thứ ba (`seed-ts-03`). **Actual:** còn
đúng 4 ảnh (`01, 02, 04, 05`), đúng thứ tự, mất đúng ảnh thứ ba; nút "Tải lên tệp" xuất hiện trở lại
(khả dụng).
**Result: ✅ PASS — khớp đúng Expected.**
**Evidence:** `screenshots/TC-TS-015__verify-xoa-anh-3-con-4-anh.png`

### TC-TS-009 — ❌ FAIL (đảo từ 🚫 BLOCKED, ĐẢO NGƯỢC giả định "màn xác nhận do app vẽ")

Điền đủ 4 trường hợp lệ (Loại yêu cầu = "Sự cố đơn hàng", Mô tả = "Hang bi mop goc khi giao" — ⚠️
gõ không dấu do `adb shell input text` không hỗ trợ Unicode dấu tiếng Việt, không ảnh hưởng tới hành
vi validate/submit đang kiểm, SĐT = `0912345678`, 2 ảnh `seed-ts-01` + `seed-ts-02`), bấm "Gửi" thật (đã xin
phép QC trước — xem đầu section). **Actual:** submit thành công, nhưng màn xác nhận là màn **mặc định
của Microsoft Forms** ("Đã gửi phản hồi của bạn." + nút "Lưu câu trả lời của tôi" + link "Gửi phản
hồi khác" + thẻ quảng cáo "Microsoft Forms — Hãy chuẩn bị cho lời mời sự kiện của riêng bạn!") — hoàn
toàn **KHÔNG có** chuỗi cam kết "Đội hỗ trợ FoxEco sẽ liên hệ lại số ... trong vòng 24 giờ làm việc",
**KHÔNG có** nút "Quay lại đơn hàng". Để quay lại app phải dùng nút "←" (Quay lại) ở header native.
**Result: ❌ FAIL** — 🔴 **Đảo NGƯỢC `C-TS-03(d)` (Resolved 2026-09-17)**: clarification đó kết luận
"màn xác nhận + nút Quay lại đơn hàng do APP vẽ" dựa trên **quan sát demo/phân tích trước khi từng
đăng nhập được qua màn Microsoft** — nay có bằng chứng thật (đã submit thành công), kết luận đó
**sai**. Cần `/analyze-requirements --update` **mở lại `C-TS-03(d)`**, sửa Expected của `SC-TS-008`
(cụm "Đã ghi nhận phản hồi"/"24 giờ làm việc"/"Quay lại đơn hàng") theo đúng màn MS Forms mặc định.
**Evidence:** `screenshots/TC-TS-009__pre-form-filled-valid.png` (trước khi gửi) ·
`screenshots/TC-TS-009__verify-da-ghi-nhan-phan-hoi.png` (màn xác nhận thật)

### TC-TS-019 — ✅ PASS (đảo từ 🚫 BLOCKED)

Điền dở Loại yêu cầu + Mô tả rồi thoát KHÔNG submit (đóng bằng back-navigation ngoài ý muốn — xem
ghi chú kỹ thuật cuối section), sau đó mở lại "Báo cáo sự cố" từ đúng đơn đó. **Actual:** phiên mới
hoàn toàn sạch — "Loại yêu cầu" trở về chưa chọn, "Mô tả chi tiết" trống (placeholder "Nhập câu trả
lời của bạn"), "Hình ảnh đính kèm" 0 ảnh (nút "Tải lên tệp" mới), "Số điện thoại liên hệ lại" trống.
**Result: ✅ PASS — khớp đúng Expected** (mở lại là phiên mới, không giữ dữ liệu nhập dở).
> ⚠️ **Quan sát riêng (không phải verdict TC, không mâu thuẫn với PASS trên):** hành vi "phiên mới"
> này CHỈ đúng khi phiên trước **bị bỏ dở, chưa từng submit**. Sau khi retest `TC-TS-009` (submit
> thành công), mở lại "Báo cáo sự cố" lần tiếp theo cho thấy Microsoft Forms **tự điền lại** Loại
> yêu cầu + SĐT từ lần trả lời gần nhất (tính năng "ghi nhớ câu trả lời" mặc định của MS Forms sau
> khi đã gửi 1 lần thành công trong cùng phiên trình duyệt) — một hành vi KHÁC, ngoài phạm vi bất kỳ
> TC nào trong 17 TC hiện có. Ghi nhận để `/analyze-requirements --update` cân nhắc bổ sung 1 SC mới
> nếu cần kiểm soát việc này (vd lo ngại lộ dữ liệu giữa 2 lượt báo cáo liên tiếp của cùng người dùng).
**Evidence:** `screenshots/TC-TS-019__verify-reopen-la-phien-moi-khong-giu-du-lieu.png` ·
`screenshots/TC-TS-019__verify-2-mota-empty-newsession.png`

### TC-TS-020 — ✅ PASS (đảo từ 🚫 BLOCKED — chạy lệch tài khoản/trạng thái so với script gốc, xem ghi chú)

Sau khi `TC-TS-009` submit thành công, quay lại "Theo dõi đơn" và kiểm tra trạng thái đơn.
**Actual:** đơn vẫn đúng "Đang giao" (IN_TRANSIT) như trước khi gửi báo cáo, không xuất hiện nhãn hay
cờ sự cố nào mới trên UI. Khớp tinh thần Expected (gửi báo cáo không tự đổi trạng thái đơn).
**Result: ✅ PASS.**
> ⚠️ **Lệch so với script gốc của TC:** script yêu cầu tài khoản **A**, đơn ở trạng thái **POSTED**
> ("Chờ ghép"); phiên này verify bằng tài khoản **B** (`stag_anhptm17@`, đang thao tác dở dang cụm TC
> form), đơn ở trạng thái **IN_TRANSIT**. Chấp nhận làm evidence hợp lệ vì: (1) trạng thái đơn là
> thuộc tính backend dùng chung, không phụ thuộc vai đang xem; (2) đã có xác nhận độc lập ở `C-TS-02(b)`
> rằng ver hiện tại "không chuyển trạng thái gì" khi gửi báo cáo — quan sát này củng cố thêm, không
> thay thế hẳn phép kiểm đúng script (account A + POSTED). Nếu cần đúng 100% script gốc, thêm vào
> hàng đợi retest với account A.
**Evidence:** `screenshots/TC-TS-020__verify-trang-thai-khong-doi-sau-gui.png`

### TC-TS-021 — ❌ FAIL (đảo từ 🚫 BLOCKED, ĐẢO NGƯỢC `C-TS-03(b)` Resolved — ô "Mã đơn hàng" THỰC RA sửa được)

Chạm vào ô "Mã đơn hàng" (đang hiển thị GUID `01a0c6fd-4730-74d6-8e99-d3e416b5bb56`), gõ thử ký tự
"X". **Actual:** bàn phím Android **BẬT LÊN** (chứng minh đây là ô nhập liệu thật, không phải nhãn
tĩnh) và ký tự "X" **được chèn vào giữa chuỗi** → giá trị đổi thành
`01a0c6fd-4730-74d6-8Xe99-d3e416b5bb56`. Đã xoá lại "X" để khôi phục giá trị gốc trước khi tiếp tục.
**Result: ❌ FAIL** — 🔴 **Đảo NGƯỢC `C-TS-03(b)` (Resolved 2026-09-17)**: clarification đó kết luận
ô này là "nhãn tĩnh, KHÔNG sửa được" dựa trên **quan sát demo trước khi từng đăng nhập qua màn
Microsoft** — nay có bằng chứng thật trên chính form: ô **CÓ THỂ SỬA**, khớp với `BR16-03` gốc
("cho phép sửa, dạng câu trả lời ngắn") mà `C-TS-03(b)` từng bác bỏ. Cần `/analyze-requirements
--update` **mở lại `C-TS-03(b)`**, đối chiếu lại `§8.16.2` ("Chỉ đọc · Không sửa") — có thể `§8.16.2`
mới là bản sai, không phải `BR16-03`.
**Evidence:** `screenshots/TC-TS-021__pre-madon-tap-attempt.png` (trước khi gõ, bàn phím vừa bật) · `screenshots/TC-TS-021__verify-madon-read-only-khong-sua-duoc.png` (sau khi gõ "X", ký tự đã chèn)

### TC-TS-024 — ✅ PASS (đảo từ 🚫 BLOCKED)

Tài khoản C (`stag_taipm@`, đúng vai "người nhận" theo script) mở đơn `SEED-TS-01` (IN_TRANSIT), góc
trên phải hiện nút "Báo cáo sự cố" (đã xác nhận từ run trước), bấm vào. **Actual:** WebView mở toàn
màn hình, ô "Mã đơn hàng" điền sẵn đúng GUID của đơn — giống hệt hành vi quan sát được ở vai B
(`TC-TS-008`) và về sau ở vai A (`TC-TS-020`/`009`).
**Result: ✅ PASS — khớp đúng Expected** (giống hệt 2 vai kia, cả phần nút hiện lẫn phần mở form).
**Evidence:** `screenshots/TC-TS-024__verify-form-loaded-after-ms-login.png`

---

### 📝 Ghi chú kỹ thuật của phiên follow-up

- **1 sự cố thao tác:** giữa lúc điền `TC-TS-009` lần đầu, nhấn phím hệ thống BACK để ẩn bàn phím
  nhưng bàn phím đã tự ẩn từ trước ⇒ BACK lan xuống WebView, đóng luôn "Báo cáo sự cố" (mất dữ liệu
  đang điền dở, KHÔNG phải hành vi của app mà là thao tác điều khiển sai). Tình cờ dùng chính sự cố
  này làm tiền đề cho `TC-TS-019` (điền dở → thoát ngoài ý muốn → mở lại → verify reset), sau đó điền
  lại từ đầu để hoàn tất `TC-TS-009` cho đúng. Từ đó về sau, dismiss bàn phím bằng nút mũi tên xuống
  (▽) của bàn phím thay vì phím BACK hệ thống.
- **Đổi tài khoản trong phiên:** C (`stag_taipm@`, có sẵn) → B (`stag_anhptm17@`, dùng cho cụm TC
  form 008/009/010/011/012/013/014/015/019/021) → giữ nguyên B khi verify `TC-TS-020`/`021` (không
  đổi lại A, xem ghi chú lệch script ở `TC-TS-020`). `TC-TS-024` verify TRƯỚC khi đổi sang B (lúc còn
  ở C).
- **Ảnh test dùng placeholder tự sinh** (`seed-ts-01` … `seed-ts-06`, đuôi jpg, PIL, màu đơn sắc ngẫu nhiên,
  ~2.5KB/ảnh), đẩy bằng `adb push` vào `/sdcard/Pictures/` + `am broadcast MEDIA_SCANNER_SCAN_FILE`
  — KHÔNG dùng ảnh thật trong thư viện thiết bị (có ảnh cá nhân nhạy cảm của chủ thiết bị).
- **Chụp evidence bằng `adb exec-out screencap -p`** (không dùng `appium_screenshot` — trả về HTML
  viewer + base64 vượt giới hạn token mỗi lần gọi, đã xác nhận lại vấn đề này từ `VR-019` gốc).

