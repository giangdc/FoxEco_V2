# Vibe Test Log — VR-011 — module GIFT — 2026-09-19

> Module: GIFT (Quà cảm ơn) · Platform: mobile (Appium MCP, UiAutomator2) · Env: STG — SDK FoxEco trong host app FoxPro (`com.hrisproject.stag`)
> Evidence dir: `screenshots/`
> Phiên: 2026-09-19 (khởi tạo)
> Tài khoản: `stag_taipm@fpt.com` — **Phan Minh Tài**, MNV `00041796`
> Nguồn TC: hợp 2 file TC-MASTER (v1.1 sheet `Quà cảm ơn` 8 TC ∪ v1.0 6 TC riêng) = **SCOPE_TOTAL 14**
> Tập chạy: **pending 14/14** (GIFT chưa từng vibe-test ⇒ không có TC đã PASS ⇒ không phải hỏi Step 1.2)

## TC-GIFT-001: Check người gửi nhấn "✓ Cảm ơn người vận chuyển" mở màn "Tặng quà"

> Nguồn: TC-MASTER **v1.0** (TC này không có trong v1.1) · SC-GIFT-001 · REQ-GIFT-001 · P2
> Đơn dùng: **G1** = `Gửi khác` · `ITD Bld, Tân Thuận, Q7 → L29B-31B-33B KCX Tân Thuận` · 9/8/2026 · card có hint `Chạm để tặng quà` (⇒ đã thoả pre-condition "Hoàn thành, chưa gửi quà", ⛔ không cần dev seed)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Seed đơn "Hoàn thành" chưa gửi quà | — (dùng đơn có sẵn trên STG) | ✅ PASS | `_recon__danh-sach-da-hoan-thanh-2-don-tang-qua.png` | 2 đơn đủ điều kiện: `Gửi khác` (G1) · `Gửi thuốc/y tế` (G2) |
| 2 | Đăng nhập A → tab "Hoạt động" → tab con "Đã hoàn thành" | tap `text("Hoạt động")` → tap `text("Đã hoàn thành")` | ✅ PASS | — | acc `stag_taipm@` (Phan Minh Tài) đóng vai **người gửi** |
| 3 | Nhấn card đơn đã hoàn thành để **mở màn Theo dõi đơn** | tap `text("Gửi khác")` | ❌ **FAIL** | `TC-GIFT-001__step3-FAIL-tap-card-mo-thang-man-tang-qua.png` | App mở **thẳng màn "Tặng quà"**, ⛔ KHÔNG qua màn "Theo dõi đơn" |
| 4 | Nhấn nút "✓ Cảm ơn người vận chuyển" | `textContains("Cảm ơn người vận chuyển")` → chỉ khớp **TextView phụ đề** `"Hành trình hoàn thành!\nGửi một món quà cảm ơn người vận chuyển"` (`get_text` xác nhận), ⛔ không có nút nào mang nhãn đó | 🚫 **không thực hiện được** | *(cùng ảnh step 3 — nút không tồn tại)* | Màn đang mở chỉ có: `Quay lại` · 4 ô quà (`gift-cell-*`) · `gift-confirm-btn` |
| E1 | Mở màn "Tặng quà" với danh mục các lựa chọn quà | màn "Tặng quà" CÓ hiển thị, đủ 4 lựa chọn | ⚠️ đạt **nhưng sai đường đi** | `TC-GIFT-001__verify-man-tang-qua-mo-tu-card.png` | Trạng thái đích đúng, nhưng đạt ở **step 3** chứ không phải qua nút ở step 4 |

**Result: ✅ PASS — Expected của TC ĐẠT; 2 step điều hướng đã lỗi thời (⛔ không phải lỗi app)**

> 🔁 **ĐÍNH CHÍNH TRONG PHIÊN (đọc kỹ — verdict đã đổi từ FAIL sang PASS).** Lúc chạy, tôi chấm FAIL vì step 3–4 không thực hiện được như TC mô tả. Sau đó đối chiếu **tài liệu phân tích của chính dự án** thì thấy cách chấm đó **sai quy kết**:
>
> | Nguồn | Nội dung |
> |---|---|
> | `v1.0/GIFT-qua-cam-on/test_scenario_map.md` L44 — **`SC-GIFT-001` Then** | *"Mở màn "Tặng quà" với 4 lựa chọn quà"* — ⇒ **đây mới là mệnh đề phải kiểm**, và app **đạt** |
> | `v1.1/GIFT-qua-cam-on/CHANGELOG.md` — **`C-GIFT-04` Resolved 2026-09-17 (BA vòng 2)** | *"(3) tap card **đã tặng** → "Theo dõi đơn"; (4) `NTF-06` **chưa tặng** → "Tặng quà", **đã tặng** → "Theo dõi đơn""* |
>
> ⇒ Việc app **route theo trạng thái tặng quà của đơn** (chưa tặng → "Tặng quà" · đã tặng → "Theo dõi đơn") **khớp với câu trả lời BA** đã được chốt `Resolved`. Đơn `Hoàn thành` **đã tặng quà** tap card **đúng là** mở "Theo dõi đơn" — quan sát được ở `_recon__theo-doi-don-hoan-thanh-da-tang-qua.png`. ⇒ **Không có defect điều hướng ở TC này.**

**Expected (step 4) — "Mở màn "Tặng quà" với danh mục các lựa chọn quà": ✅ ĐẠT** (4 ô quà đầy đủ).
**Evidence:** `screenshots/TC-GIFT-001__verify-man-tang-qua-mo-tu-card.png` (+ `TC-GIFT-001__step3-FAIL-tap-card-mo-thang-man-tang-qua.png` — giữ lại vì đây là bằng chứng **step 3 đi đường khác TC mô tả**)

**📝 Đề nghị sửa TC (⛔ KHÔNG log bug):** Steps 3–4 của TC viết theo luồng **trước khi `C-GIFT-04` được BA trả lời**. Sửa thành: *"3. Nhấn card đơn Hoàn thành chưa tặng quà (card có hint `Chạm để tặng quà`) → app mở màn "Tặng quà"."* — bỏ step 4.

**🔴 Vẫn còn 1 SPEC-GAP THẬT, tách riêng khỏi verdict của TC:** nút **`"✓ Cảm ơn người vận chuyển"`** mà `KB-GIFT-01` (`KP-01 §5.1`, ô 5·Sender) và **`SC-GIFT-001` When** đều mô tả là **KHÔNG tồn tại ở bất kỳ đâu trên app** (`textContains("Cảm ơn người vận chuyển")` chỉ khớp **TextView phụ đề** của màn "Tặng quà" — `get_text` xác nhận). ⇒ **ma trận nhãn nút `KB-GIFT-01` cần cập nhật** → `/analyze-requirements --update`. Đây là **nợ tài liệu**, ⛔ không phải nợ kiểm thử và ⛔ không làm TC này FAIL.

---

## TC-GIFT-002: Check màn "Tặng quà" hiển thị đúng tên bốn loại quà theo danh mục chính thức

> Nguồn: TC-MASTER **v1.1** (Lifecycle MODIFIED — siết Expected từ "đếm 4 loại" sang assert **đúng TÊN** theo `BR14-01`) · SC-GIFT-002 · REQ-GIFT-001 · P2
> Đơn dùng: **G1** `Gửi khác` (= vai trò `SEED-GIFT-01`, ⛔ TC này KHÔNG tiêu đơn)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1–3 | (setup) Vào "Hoạt động" → "Đã hoàn thành" → mở đơn Hoàn thành | tap `text("Gửi khác")` → màn "Tặng quà" | ✅ PASS | — | ⚠️ Không qua "Theo dõi đơn" — lệch luồng đã ghi ở `TC-GIFT-001` |
| 4 | Đọc danh sách quà hiển thị trên màn "Tặng quà" | `resourceIdMatches(".*gift-cell-.*").instance(3)` ✅ tồn tại · `.instance(4)` 🚫 NOT FOUND ⇒ **đúng 4 ô quà** | ✅ PASS | — | Đếm bằng MCP, ⛔ không đếm bằng mắt trên ảnh |
| E1 | Đúng 4 loại, đúng tên "Bông hoa" · "Ly cà phê" · "Gấu bông" · "Vương miện"; không có loại thứ năm, không đổi tên/icon | `gift-cell-flower`="Bông hoa" 🌻 · `gift-cell-coffee`="Ly cà phê" ☕ · `gift-cell-teddy`="Gấu bông" 🧸 · `gift-cell-crown`="Vương miện" 👑 — khớp **nguyên văn** `BR14-01` | ✅ PASS | `TC-GIFT-002__verify-4-loai-qua-dung-ten.png` | 4 tên lấy từ `content-desc` + `TextView` của page source MCP, ⛔ không suy từ ảnh |

**Result: ✅ PASS (4 steps, 1 expected)**
**Evidence:** `screenshots/TC-GIFT-002__verify-4-loai-qua-dung-ten.png`
**Locators captured:** 5 elements (`gift-cell-flower` · `gift-cell-coffee` · `gift-cell-teddy` · `gift-cell-crown` · `gift-confirm-btn`)

---

## TC-GIFT-004: Check màn "Tặng quà" không có thành phần thanh toán hay quy đổi tiền

> Nguồn: TC-MASTER **v1.0** · SC-GIFT-004 · REQ-GIFT-002 · P3 · assert-absent
> Đơn dùng: **G1** `Gửi khác` (⛔ không tiêu đơn)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1–2 | (setup) Mở đơn "Hoàn thành" → vào màn "Tặng quà" | tap `text("Gửi khác")` | ✅ PASS | — | — |
| 3 | Check toàn màn "Tặng quà", **gồm cả vùng cuối màn**, tìm giá tiền / ví / cổng thanh toán / quy đổi điểm | `textMatches("(?s).*(đ\|VNĐ\|VND\|₫\|điểm\|Điểm\|ví\|Ví\|thanh toán\|Thanh toán\|quy đổi\|Quy đổi\|xu\|Xu).*")` → 🚫 **NOT FOUND** | ✅ PASS | — | Đối chứng: cùng cú pháp với `"(?s).*(quà\|đ).*"` ✅ khớp ⇒ cơ chế regex hoạt động, kết quả 🚫 là **vắng mặt thật**, không phải selector hỏng |
| E1 | KHÔNG có giá tiền / ví / cổng thanh toán / quy đổi điểm | Toàn bộ cây màn (page source MCP) chỉ gồm: `Quay lại` · tiêu đề `Tặng quà` · phụ đề · nhãn "Chọn một món quà…" · **4 ô quà** · `gift-confirm-btn` — **0 thành phần tiền tệ** | ✅ PASS | `TC-GIFT-004__verify-khong-co-thanh-toan.png` | Màn cao 1232px = vừa 1 khung, ⛔ không có vùng cuộn ẩn bên dưới |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-GIFT-004__verify-khong-co-thanh-toan.png`
**Kết luận `BR-GIFT-01`:** quà là biểu tượng phi vật chất — app khớp, ⛔ không phát sinh CL scope.

---

## TC-GIFT-010: Check nhấn quay lại ở màn "Tặng quà" trở về màn Theo dõi đơn của đúng đơn vừa mở

> Nguồn: TC-MASTER **v1.0** · SC-GIFT-010 · REQ-GIFT-006 · P3 · neo vào `C-GIFT-02` (Open)
> ⚠️ **Lệch Test Data có chủ ý, đã khai:** TC yêu cầu 2 đơn "khác nhau về tuyến đường". Trên STG, **cả 2 đơn Hoàn thành chưa tặng quà đều cùng tuyến** `ITD Bld, Tân Thuận, Q7 → L29B-31B-33B KCX Tân Thuận`. ⇒ dùng **loại hàng** làm dấu phân biệt (`Gửi khác` = đơn 1 · `Gửi thuốc/y tế` = đơn 2). Dấu phân biệt yếu hơn tuyến, nhưng **đủ để chấm** vì kết quả thực tế không về màn Theo dõi đơn của **bất kỳ** đơn nào.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Seed 2 đơn "Hoàn thành" chưa gửi quà | — (dùng 2 đơn có sẵn) | ⚠️ PASS *(lệch: cùng tuyến)* | `TC-GIFT-010__pre-danh-sach-truoc-khi-mo-don-thu-hai.png` | G1 `Gửi khác` · G2 `Gửi thuốc/y tế`, đều 9/8/2026, cùng tuyến |
| 2 | Đăng nhập A → "Hoạt động" → "Đã hoàn thành" | tap `text("Hoạt động")` → `text("Đã hoàn thành")` | ✅ PASS | — | — |
| 3 | Mở **đơn thứ hai**, ghi lại dấu nhận dạng, rồi nhấn "✓ Cảm ơn người vận chuyển" | tap `text("Gửi thuốc/y tế").instance(0)` → app mở **thẳng** màn "Tặng quà" | ⚠️ PASS *(sai đường đi)* | — | Nút `"✓ Cảm ơn người vận chuyển"` **không tồn tại** (đã chốt ở `TC-GIFT-001`); ⚠️ có **2 card** cùng tên `Gửi thuốc/y tế` ⇒ bắt buộc `.instance(0)` (card thứ 2 là `67 Tăng Bạt Hổ`, không có hint tặng quà) |
| 4 | Nhấn nút quay lại trên màn "Tặng quà" | tap `accessibility id "Quay lại"` | ❌ **FAIL** | `TC-GIFT-010__step4-FAIL-back-ve-danh-sach-khong-ve-theo-doi-don.png` | — |
| 5 | Check màn hiện ra và dấu nhận dạng đơn đang mở | Màn hiện ra = **`Đơn của tôi` → tab `Đã hoàn thành`** (danh sách), ⛔ KHÔNG phải `Theo dõi đơn`. Vị trí cuộn bị **reset về đầu danh sách** (card đầu là `Gửi thực phẩm · Hết hạn`) | ❌ **FAIL** | *(cùng ảnh step 4)* | — |
| E1 | Về màn Theo dõi đơn trùng đơn ở bước 3; không mở màn xác nhận nhận hàng, không mở đơn khác | **Vế 1 SAI** (về danh sách, không về Theo dõi đơn). **Vế 2 ĐÚNG** (không mở màn "Xác nhận đã nhận hàng", không mở đơn khác) | ❌ **FAIL** | *(cùng ảnh step 4)* | — |

**Result: ⚠️ NOT_EVIDENCED — nội dung ĐẠT (xem phân tích dưới) nhưng ảnh nằm SAI SLOT ⇒ ⛔ không được ghi PASS**

> 🧾 **Vì sao không phải PASS, dù kết quả đúng.** Ảnh chứng minh trạng thái sau khi bấm back **có thật** và **là ảnh của chính TC này, chụp trong run này, đúng lúc verify** — nhưng tên file mang slot `__step4-FAIL` vì lúc chụp tôi **đang chấm FAIL**. Khi verdict được đính chính sang PASS, TC không còn file `__verify*` nào.
> Luật `vibe-test` **cấm tuyệt đối** đổi tên / copy ảnh cho khớp gate (*"đó là làm giả evidence"*), và tôi **không** làm việc đó. Cách hợp lệ duy nhất là **chụp lại** — nhưng ⛔ **không chụp lại được**: màn "Tặng quà" chỉ mở từ **đơn Hoàn thành chưa tặng quà**, mà **cả 4 tài khoản vào được FoxEco đều đã hết sạch** loại đơn này *(2 đơn cuối bị `TC-GIFT-003` + `TC-GIFT-005` tiêu ngay trong phiên; đã kiểm thêm `stag_anhptm17@` và `stag_anhdc4@` — xem `_recon__acc-anhdc4-khong-con-don-cho-tang-qua.png`)*.
> ⇒ Giữ **⚠️ NOT_EVIDENCED**: TC **ở lại danh sách nợ**, lượt sau bộ lọc pending tự bốc lại. **Chạy lại:** `/vibe-test --tc TC-GIFT-010` sau khi có 1 đơn Hoàn thành chưa tặng quà.

**Kết luận nội dung (đã xác định chắc chắn, dùng được cho `/log-bug` và `/analyze-requirements`, ⛔ nhưng KHÔNG dùng làm verdict PASS):** app về **ĐÚNG màn mà `SC-GIFT-010` cho phép**; Expected của TC bị viết **HẸP hơn** scenario.

> 🔁 **ĐÍNH CHÍNH TRONG PHIÊN (verdict đã đổi từ FAIL sang PASS).** Lúc chạy tôi chấm FAIL vì app không về "Theo dõi đơn". Đối chiếu tài liệu phân tích thì cách chấm đó **sai**:
>
> | Nguồn | Nội dung |
> |---|---|
> | `v1.0/GIFT-qua-cam-on/test_scenario_map.md` L53 — **`SC-GIFT-010` Then** | *"Về đúng màn trước đó **(Theo dõi đơn / Đơn của tôi)**"* — ⇒ **"Đơn của tôi" NẰM TRONG tập chấp nhận** |
> | `v1.1/GIFT-qua-cam-on/test_scenario_map.md` — **`C-GIFT-02` Resolved 2026-09-16** | *"BA: lỗi demo; rule = **back về màn hình trước đó** ⇒ Then assert back về **đúng màn đã mở "Tặng quà"**; nhảy sang đơn/màn khác = bug"* |
>
> ⇒ Phiên này màn "Tặng quà" được mở **TỪ danh sách "Đơn của tôi → Đã hoàn thành"**, nên back về **chính danh sách đó** = **đúng "màn đã mở Tặng quà"** = đúng rule BA đã chốt. ⛔ **Không** nhảy sang đơn khác, ⛔ **không** mở màn "Xác nhận đã nhận hàng".

**Cả 2 vế của Expected, chấm theo `SC-GIFT-010`:** back về đúng màn trước đó ✅ · không mở màn xác nhận nhận hàng, không mở đơn khác ✅.
**Evidence:** `screenshots/TC-GIFT-010__step4-FAIL-back-ve-danh-sach-khong-ve-theo-doi-don.png` (+ `TC-GIFT-010__pre-danh-sach-truoc-khi-mo-don-thu-hai.png`)
*(⚠️ Tên file mang slot `step4-FAIL` vì chụp lúc đang chấm FAIL. ⛔ **Cố ý KHÔNG đổi tên** — xem khối giải thích ở mục Result. Nội dung ảnh vẫn đúng là màn app hiện ra sau khi bấm back.)*

**🔑 Đính chính `C-GIFT-02` bằng quan sát build này:** hành vi cũ ghi ở `KB-GIFT-04` — *back nhảy sang màn "Xác nhận đã nhận hàng" của **đơn khác*** — **KHÔNG tái hiện**. ⇒ `RISK-GIFT-05` (Severity Medium, dựng từ quan sát demo) có thể **hạ/đóng**.

**📝 Đề nghị sửa TC (⛔ KHÔNG log bug):** Expected của TC chỉ liệt kê *"về màn Theo dõi đơn"*, **hẹp hơn** Then của `SC-GIFT-010` (*"Theo dõi đơn **/ Đơn của tôi**"*). Sửa Expected cho khớp scenario.

**⚠️ 1 quan sát phụ, mức thấp, ⛔ không đủ để FAIL:** back làm **reset vị trí cuộn** của danh sách về đầu (đang ở đơn thứ 2 → quay lại thấy card đầu danh sách). Không có nguồn nào quy định phải giữ vị trí cuộn ⇒ ghi nhận để BA quyết, không chấm.

---

## TC-GIFT-003: Check gửi quà hiện đúng popup "Cảm ơn của bạn đã được gửi" kèm nút về trang chủ

> Nguồn: TC-MASTER **v1.1** (MODIFIED — siết **đúng chuỗi** theo `BR14-02`/`AC-24.1.01`, **thay** chuỗi v1.0 `"Đã gửi lời cảm ơn!"` vốn dựa nguồn yếu `US-D15`) · SC-GIFT-003 · REQ-GIFT-002 · P2
> Đơn dùng: **G1** `Gửi khác` (vai trò `SEED-GIFT-02`) — ⚠️ **TC này TIÊU ĐƠN**, G1 nay đã ở trạng thái đã tặng quà.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1–3 | (setup) "Hoạt động" → "Đã hoàn thành" → mở đơn → màn "Tặng quà" | tap `text("Gửi khác")` | ✅ PASS | — | app mở thẳng "Tặng quà" (lệch luồng, xem `TC-GIFT-001`) |
| 4 | Chọn loại quà "Bông hoa" | tap `accessibility id "Bông hoa"` (`rid=gift-cell-flower`) | ✅ PASS | `TC-GIFT-003__pre-chon-bong-hoa.png` | Ô "Bông hoa" đổi sang trạng thái **chọn** (viền + nền cam); `gift-confirm-btn` từ `enabled=false` → **enabled** |
| 5 | Nhấn nút xác nhận gửi quà | tap `accessibility id "Xác nhận tặng quà"` (`rid=gift-confirm-btn`) | ❌ **FAIL** *(1/3 vế sai)* | `TC-GIFT-003__step5-FAIL-sai-chuoi-popup.png` | — |
| E1a | Quà gửi **ngay**, không có bước chờ xác nhận của người vận chuyển | Popup bật ngay sau 1 lần chạm, ⛔ không có màn/bước chờ trung gian | ✅ PASS | `TC-GIFT-003__verify-popup-cam-on-da-duoc-gui.png` | — |
| E1b | Popup hiện **đúng chuỗi** "Cảm ơn của bạn đã được gửi" | **Tiêu đề popup = `"Đã gửi lời cảm ơn!"`** — đúng chuỗi **v1.0 mà v1.1 đã bỏ**. Thân popup = `"Món quà và lời cảm ơn của bạn đã được gửi đến người vận chuyển."` (`get_text` qua MCP) | ❌ **FAIL** | *(cùng ảnh step 5)* | — |
| E1c | Kèm **nút về trang chủ** | Có nút `"Về trang chủ"` | ✅ PASS | *(cùng ảnh)* | — |

**Result: ❌ FAIL tại Step 5 (vế chuỗi popup)**
**Expected:** popup hiện đúng chuỗi `"Cảm ơn của bạn đã được gửi"` · **Actual:** tiêu đề `"Đã gửi lời cảm ơn!"` + thân `"Món quà và lời cảm ơn của bạn đã được gửi đến người vận chuyển."`
**Evidence:** `screenshots/TC-GIFT-003__step5-FAIL-sai-chuoi-popup.png` (+ `TC-GIFT-003__verify-popup-cam-on-da-duoc-gui.png`, `TC-GIFT-003__pre-chon-bong-hoa.png`)
**⚖️ Ghi rõ để QC lead phân xử, ⛔ không tự hạ Expected theo app:**
> - **Đọc chặt (đang dùng để chấm):** `BR14-02` yêu cầu popup mang chuỗi chính thức; app vẫn hiển thị **tiêu đề cũ** `"Đã gửi lời cảm ơn!"` mà `v1.1` đã chủ ý loại bỏ ⇒ **lệch copy, FAIL**.
> - **Đọc lỏng:** chuỗi `"cảm ơn của bạn đã được gửi"` **có xuất hiện** (chữ thường, nhúng trong câu thân popup) — `textContains` khớp. Nếu BA chấp nhận dạng nhúng này thì TC chuyển ✅ PASS **và phải sửa Expected cho rõ**.
>
> ⇒ Cần BA chốt trước khi log bug; đây là **lỗi nội dung hiển thị mức thấp**, ⛔ không chặn luồng.
**Impact:** ⚠ `SEED-GIFT-02` đã tiêu. Đơn Hoàn thành chưa tặng quà còn lại: **1** (`G2` = `Gửi thuốc/y tế`).

---

## TC-GIFT-005: Check sau khi gửi quà nút đổi nhãn "Bạn đã đánh giá" và không gửi lại được cho cùng đơn

> Nguồn: TC-MASTER **v1.0** · SC-GIFT-005 · REQ-GIFT-003 · P2 · cặp biên lần 1 enable → lần 2 disable
> Đơn dùng: **G2** `Gửi thuốc/y tế` · ITD Bld → L29B · 9/8/2026 — ⚠️ **TC này TIÊU ĐƠN** (đơn Hoàn thành chưa tặng quà cuối cùng của tài khoản)
> 🔑 Người vận chuyển của G2 = **Đặng Châu Giang** (`0964633310` ⇒ acc `stag_giangdc2@`) — đây là **người nhận quà "Ly cà phê"** vừa gửi, dùng làm tiền đề cho `TC-GIFT-012`.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1–2 | (setup) Mở đơn "Hoàn thành" → màn "Tặng quà" | tap `text("Gửi thuốc/y tế").instance(0)` | ✅ PASS | — | — |
| 3 | Chọn "Ly cà phê" và nhấn xác nhận gửi quà | tap `accessibility id "Ly cà phê"` → tap `accessibility id "Xác nhận tặng quà"` → popup `"Đã gửi lời cảm ơn!"` | ✅ PASS | `TC-GIFT-005__pre-chon-ly-ca-phe.png` | — |
| 4 | Nhấn nút quay lại để về màn Theo dõi đơn của đơn đó | `back` ×2 | ❌ **FAIL** | `TC-GIFT-005__step4-FAIL-back-khong-ve-theo-doi-don-popup-ket-lai.png` | 🆕 **Popup KHÔNG đóng được bằng `back`** — mỗi lần `back` chỉ pop **màn nền** (Tặng quà → danh sách → **Trang chủ**) còn popup vẫn nổi. Chỉ nút `"Về trang chủ"` đóng được. ⇒ back **không** về "Theo dõi đơn" *(cùng gốc với `TC-GIFT-010`)*. Đã mở lại đơn G2 từ danh sách để chạy tiếp step 5–6 |
| 5 | Check nhãn và trạng thái của nút tặng quà | `text("Bạn đã đánh giá")` ✅ tồn tại · `ancestor::*[@clickable="true"]` 🚫 **NOT FOUND** ⇒ **không có tổ tiên clickable** ⇒ nút **disable thật** | ✅ PASS | `TC-GIFT-005__verify-nhan-nut-sau-khi-tang-qua.png` | Card G2 ở danh sách cũng đổi sang hint `Đã tặng quà` |
| 6 | Nhấn vào nút đó | tap `text("Bạn đã đánh giá")` → vẫn ở `Theo dõi đơn` (`text("Theo dõi đơn")` ✅); `accessibility id "Bông hoa"` 🚫 NOT FOUND ⇒ màn "Tặng quà" **không mở lại** | ✅ PASS | `TC-GIFT-005__verify-khong-mo-lai-man-tang-qua.png` | — |
| E5 | Nút hiển thị nhãn "Bạn đã đánh giá" và ở trạng thái disable | Nhãn **khớp nguyên văn** `"Bạn đã đánh giá"`; nút xám, không clickable | ✅ PASS | *(ảnh step 5)* | ✔ `KB-GIFT-01`: nhãn này là **UI leftover** của cơ chế rating đã out of scope — ⛔ không suy ra app có chấm điểm |
| E6 | Nhấn nút không mở lại "Tặng quà"; không có đường gửi quà lần hai | Không mở lại; ⛔ không tìm thấy lối gửi quà lần 2 cho đơn này | ✅ PASS | *(ảnh step 6)* | — |

**Result: ✅ PASS (cả 2 expected E5 + E6 đạt)**
**Evidence:** `screenshots/TC-GIFT-005__verify-nhan-nut-sau-khi-tang-qua.png` (+ `TC-GIFT-005__verify-khong-mo-lai-man-tang-qua.png`, `TC-GIFT-005__pre-chon-ly-ca-phe.png`, `TC-GIFT-005__step4-FAIL-back-khong-ve-theo-doi-don-popup-ket-lai.png`)
**⚠️ Khai rõ:** **step 4 (điều hướng) SAI** nhưng **không** hạ verdict TC này, vì (a) cả 2 Expected Result của TC đều ở step 5–6 và đều đạt, (b) lỗi back đã được chấm **FAIL riêng** ở `TC-GIFT-010` — tính FAIL thêm lần nữa ở đây là **đếm trùng 1 defect**. Ảnh step 4 vẫn giữ + trích để người audit thấy được.
**🆕 Phát sinh ngoài scenario_map:** popup cảm ơn **không đóng được bằng nút back hệ thống** và vẫn nổi trên mọi màn nền ⇒ surface chưa có trong `scenario_map` → cần `/analyze-requirements --update`.
**Impact:** ⛔ **Hết sạch đơn Hoàn thành chưa tặng quà** trên `stag_taipm@` ⇒ `TC-GIFT-011` (cần 1 đơn RIÊNG để tiêu) không còn tiền đề trong phiên này.

---

## TC-GIFT-007: Check màn "Quà đã nhận" có danh sách lịch sử nhận quà

> Nguồn: TC-MASTER **v1.1** (MODIFIED — `C-GIFT-03` vế (b) Resolved: assert **khẳng định** CÓ lịch sử, nâng P3 → **P2**) · SC-GIFT-007 · REQ-GIFT-004 · P2
> ⚠️ **Lệch Test Data có chủ ý, đã khai:** TC neo vào `SEED-GIFT-05` (tài khoản B nhận **5 quà**). Trên STG tài khoản đang chạy (`stag_taipm@`) chỉ có **1 quà** (`Gấu bông`, từ `Đặng Châu Giang`, 9 Th8 07:58) và ⛔ không dựng được 5 quà qua UI trong phiên. **Assert chính của TC ("màn CÓ danh sách lịch sử, số dòng khớp số lần nhận quà") vẫn quyết được** với N=1 ⇒ chấm bình thường; phần bộ số 5 quà thuộc `TC-GIFT-006` và để `⏳ NOT_RUN`.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập B → tab "Cá nhân" → mục "Quà đã nhận" | tap `text("Cá nhân")` → tap `text("Quà đã nhận")` | ✅ PASS | — | Trang cá nhân hiện `2 đơn đã giúp` · `1 quà đã nhận` |
| 2 | Cuộn hết màn, check vùng danh sách lịch sử nhận quà | Màn có **2 khối**: card đếm `Tổng quà đã nhận — 1 món` **và** khối tiêu đề `LỊCH SỬ NHẬN QUÀ` + **1 dòng** `Gấu bông · Đặng Châu Giang · 9 Th8 · 07:58`. Màn vừa 1 khung, ⛔ không còn nội dung ẩn bên dưới | ✅ PASS | — | — |
| E1 | Màn CÓ danh sách lịch sử nhận quà (không chỉ có card đếm); số dòng khớp số lần đã nhận quà | **CÓ** khối `LỊCH SỬ NHẬN QUÀ` ✅ · số dòng = **1** = số quà đã nhận (**1**) ✅ · mỗi dòng nêu **loại quà + người gửi + thời điểm** | ✅ PASS | `TC-GIFT-007__verify-co-danh-sach-lich-su-nhan-qua.png` | — |

**Result: ✅ PASS (2 steps, 1 expected)**
**Evidence:** `screenshots/TC-GIFT-007__verify-co-danh-sach-lich-su-nhan-qua.png`
**🔑 Đóng `C-GIFT-03` vế (b):** v1.0 dự kiến FAIL vì *"chưa thấy danh sách lịch sử trên app"*. Build này **CÓ** ⇒ `AC-26.1.01` (*"kèm lịch sử nhận quà"*) được app đáp ứng.
**Locators captured:** 2 elements (`text("Quà đã nhận")` menu · `accessibility id "Quay lại"` header)

---

## TC-GIFT-009: Check nhấn quay lại ở màn "Quà đã nhận" trở về màn Cá nhân

> Nguồn: TC-MASTER **v1.0** · SC-GIFT-009 · REQ-GIFT-006 · P3
> Pre-condition "tài khoản B đã nhận ≥1 quà" — ✅ thoả sẵn (`stag_taipm@` có 1 `Gấu bông`), ⛔ không cần dev seed.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Seed tài khoản B đã nhận ≥1 quà | — (thoả sẵn) | ✅ PASS | — | 1 quà `Gấu bông` |
| 2 | Đăng nhập B → tab "Cá nhân" → mục "Quà đã nhận" | tap `text("Cá nhân")` → tap `text("Quà đã nhận")` | ✅ PASS | — | — |
| 3 | Nhấn icon quay lại ở header | tap `accessibility id "Quay lại"` | ✅ PASS | — | — |
| E1 | Về màn Cá nhân với khối hồ sơ và 2 mục menu hiển thị | Về **đúng màn `Cá nhân`** ✅ · khối hồ sơ hiển thị đủ (avatar `PM` · `Phan Minh Tài` · `Phòng Phát triển Phần mềm số 8 · MNV: 00041796` · `2 đơn đã giúp` / `1 quà đã nhận`) ✅ · ⚠️ menu có **3 mục**, không phải 2: `Đơn của tôi` · `Quà đã nhận` · `Cập nhật thông tin cá nhân` | ✅ PASS | `TC-GIFT-009__verify-ve-man-ca-nhan.png` | — |

**Result: ✅ PASS (3 steps, 1 expected)**
**Evidence:** `screenshots/TC-GIFT-009__verify-ve-man-ca-nhan.png`
**📝 Đề nghị sửa TC (KHÔNG phải lỗi app):** Expected ghi *"2 mục menu"* là **số liệu cũ của v1.0**; app hiện có **3 mục** — khớp với ghi chép đã chốt ở `04_test-data/valid/USR-accounts.md §0` (*"`Cá nhân` của FoxEco chỉ có 3 mục: Đơn của tôi · Quà đã nhận · Cập nhật thông tin"*). ⇒ Sửa Expected thành **3 mục** ở lượt bảo trì TC; ⛔ KHÔNG log bug. Assert điều hướng (vế chính của `REQ-GIFT-006`) đạt.

---

## TC-GIFT-013: Check đơn RETURNED không có nút tặng quà và vẫn hiện trong lịch sử đơn

> Nguồn: TC-MASTER **v1.1** (Lifecycle **NEW**) · SC-GIFT-013 · REQ-GIFT-009 · P2 · `BR14-04` / `AC-24.2.01` vế (a)
> Pre-condition: 1 đơn `RETURNED` đi hết nhánh `IN_TRANSIT → RETURNING → RETURNED` (`SEED-GIFT-08`, dùng chung `DLV`).

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập A → "Hoạt động" → tab con "Đã hoàn thành", tìm đơn `RETURNED` | Rà **cả 2 tab**. `textMatches("(?s).*(Hoàn hàng\|Trả về\|Đang trả\|Hoàn trả\|Giao lại\|Hẹn lại\|RETURNED\|RETURNING\|RESCHEDULED).*")` → 🚫 **NOT FOUND**. Badge tồn tại trên STG chỉ gồm: `Chờ ghép` · `Đã ghép` · `Hết hạn` · `Hoàn thành` | 🚫 **BLOCKED** | `TC-GIFT-013__step1-BLOCKED-khong-co-don-returned.png` | Danh sách "Đã hoàn thành" đã cuộn hết (tới 5/8/2026) ở Pha A — ⛔ không có đơn `RETURNED` nào |
| 2–3 | — | — | ⏭ SKIPPED | — | blocked ở step 1 |

**Result: 🚫 BLOCKED tại Step 1**
**Reason:** **STG chưa build `FR09` (luồng hoàn hàng)** ⇒ `SEED-GIFT-08` không dựng được. Bằng chứng bổ sung: thanh tiến trình đơn trên màn "Theo dõi đơn" chỉ có **đúng 5 trạng thái** `Chờ ghép → Lấy hàng → Đang giao → Đã giao → Hoàn thành`, ⛔ **không có nhánh** `RETURNING`/`RESCHEDULED`/`RETURNED`; hành động duy nhất của Người gửi ở đơn `Đã ghép` là `Huỷ đơn` (quan sát này được ghi lại trong section `TC-GIFT-014` bên dưới, kèm ảnh riêng của TC đó).
**Evidence:** `screenshots/TC-GIFT-013__step1-BLOCKED-khong-co-don-returned.png`
**Impact:** ⛔ **KHÔNG được ghi PASS** — đúng chỉ dẫn trong Notes của chính TC (*"không thấy nút" không chứng minh gì nếu không có đơn RETURNED thật để thử*). Gỡ blocker = dev build `FR09` trên STG, rồi chạy lại cùng lô với `TC-DLV-053..056`.

---

## TC-GIFT-014: Check đơn RETURNED không được tính vào chỉ số "Đơn đã giúp"

> Nguồn: TC-MASTER **v1.1** (Lifecycle **NEW**) · SC-GIFT-014 · REQ-GIFT-009 · P2 · `BR14-04` / `AC-24.2.01` vế (b) *(sai lệch âm thầm)*

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đăng nhập B → tab "Cá nhân" | tap `text("Cá nhân")` | ✅ PASS | — | — |
| 2 | Ghi lại số "Đơn đã giúp" hiện tại (N) | Đọc Trang cá nhân: **N = 2** (`stag_taipm@`, đối chiếu cả card "Đóng góp của bạn" ở Trang chủ = `2 đơn đã giúp`) | ✅ PASS | — | Mốc N ghi **TRƯỚC**, đúng yêu cầu Test Data |
| 3 | Thực hiện luồng hoàn hàng cho 1 đơn khác tới khi sang `RETURNED` | Mở "Theo dõi đơn" của đơn `Đã ghép`: hành động khả dụng **chỉ có `Huỷ đơn`**; thanh trạng thái **5 bước, không có nhánh hoàn hàng** ⇒ ⛔ không có đường đẩy đơn sang `RETURNED` | 🚫 **BLOCKED** | `TC-GIFT-014__step3-BLOCKED-khong-co-nhanh-hoan-hang.png` | — |
| 4 | — | — | ⏭ SKIPPED | — | blocked ở step 3 |

**Result: 🚫 BLOCKED tại Step 3**
**Reason:** Cùng blocker với `TC-GIFT-013` — **STG chưa build `FR09`**, không tạo được đơn `RETURNED` nên không có phép so N ⟷ N+1.
**Evidence:** `screenshots/TC-GIFT-014__step3-BLOCKED-khong-co-nhanh-hoan-hang.png`
**Impact:** ⛔ **KHÔNG được ghi PASS** (Notes của TC nói rõ). Mốc **N = 2** đã ghi lại, dùng được cho lượt chạy sau nếu đơn `RETURNED` phát sinh mà chỉ số chưa bị chạm bởi việc khác.

---

## TC-GIFT-012: Check người vận chuyển nhận thông báo quà cảm ơn và nhấn vào mở Trang cá nhân

> Nguồn: TC-MASTER **v1.0** · SC-GIFT-012 · REQ-GIFT-008 · P2 · `NTF-07`
> 🔄 **Đổi tài khoản trong phiên:** `stag_taipm@` → **`stag_giangdc2@`** (Đặng Châu Giang) — là **người vận chuyển của CẢ HAI đơn** vừa được tặng quà ở `TC-GIFT-003` và `TC-GIFT-005`.
> ⚠️ **Lệch Test Data có chủ ý, đã khai:** TC yêu cầu quà `"Gấu bông"`; thực tế dùng quà đã gửi sẵn trong phiên (`Bông hoa` lúc 20:33 · `Ly cà phê` lúc 20:37) để ⛔ không tiêu thêm đơn Hoàn thành. Loại quà **không ảnh hưởng** assert của TC (nội dung `NTF-07` không nêu tên quà).
> ⚠️ 1 thiết bị thay vì 2 — chạy **tuần tự** (gửi quà bằng acc A trước, rồi đăng nhập acc B kiểm chuông) thay vì song song 2 máy.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Seed 1 đơn "Hoàn thành" A gửi / B vận chuyển | — (2 đơn của `TC-GIFT-003`/`005`, carrier = `Đặng Châu Giang`) | ✅ PASS | — | — |
| 2 | Acc A mở đơn → "✓ Cảm ơn người vận chuyển" → chọn quà → xác nhận gửi | Đã thực hiện ở `TC-GIFT-003` (Bông hoa) và `TC-GIFT-005` (Ly cà phê) | ✅ PASS | — | — |
| 3 | Đăng nhập tài khoản B, nhấn icon chuông | Đăng xuất FoxPro → login `stag_giangdc2@` + OTP → `Chức năng` → `FoxEco` → tap chuông | ✅ PASS | — | ⚠️ Bẫy `T-ASN-07` **có xuất hiện** (dialog *"Không thể kết nối mạng!"* giả ở `NHẬN MÃ OTP`, ping 0% loss) — bấm lại lần 2 thì qua |
| 4 | Nhấn vào thông báo quà cảm ơn | tap dòng thông báo đầu | ❌ **FAIL** | `TC-GIFT-012__step4-FAIL-mo-qua-da-nhan-khong-phai-trang-ca-nhan.png` | — |
| E3 | Danh sách thông báo có thông báo nội dung "Bạn nhận được một món quà cảm ơn 🎁 — mở Trang cá nhân để xem" | **CÓ 2 thông báo** (`13 phút trước` · `17 phút trước`, khớp 2 lượt tặng quà). `get_text` trả **nguyên văn**: `"Bạn nhận được một món quà cảm ơn — mở Trang cá nhân để xem"`. Tiêu đề dòng: `"Bạn nhận được một món quà cảm ơn"` | ✅ PASS *(1 khác biệt trang trí, xem dưới)* | `TC-GIFT-012__verify-thong-bao-qua-cam-on.png` | ⚠️ **Thiếu emoji 🎁** so với `NTF-07`; phần chữ khớp **100% verbatim**. ✔ Đúng Notes TC: ⛔ không assert "chỉ có 1 dòng" — app có tiêu đề + dòng mô tả |
| E4 | Mở màn Cá nhân của tài khoản B | Mở **màn `"Quà đã nhận"`**, ⛔ **KHÔNG phải** màn `Cá nhân` | ❌ **FAIL** | *(ảnh step 4)* | Deep-link **sâu hơn 1 cấp** so với cả spec lẫn **chính câu chữ của thông báo** (*"mở Trang cá nhân để xem"*) |

**Result: ❌ FAIL tại Step 4**
**Expected:** nhấn thông báo → mở màn **Cá nhân** · **Actual:** mở thẳng màn **"Quà đã nhận"**.
**Evidence:** `screenshots/TC-GIFT-012__step4-FAIL-mo-qua-da-nhan-khong-phai-trang-ca-nhan.png` (+ `TC-GIFT-012__verify-thong-bao-qua-cam-on.png`)
**⚖️ Hai khác biệt, mức độ KHÁC NHAU — ⛔ đừng gộp:**
> 1. **E4 — lệch điều hướng (thực chất, đang chấm FAIL):** thông báo tự nói *"mở Trang cá nhân"* nhưng lại mở `"Quà đã nhận"` ⇒ app **tự mâu thuẫn với chính nó**. Cần BA chốt: sửa đích deep-link, hay sửa câu chữ + `NTF-07`.
> 2. **E3 — thiếu emoji 🎁 (trang trí):** phần chữ khớp verbatim, ⛔ **không** hạ verdict E3 vì lý do này. ⚠ Khác hẳn ca `TC-GIFT-003` (ở đó app hiện **nguyên một câu khác** mà `v1.1` đã chủ ý thay) — nên 2 ca chấm khác nhau là có chủ ý, không phải bất nhất.

**🎁 Quan sát bổ sung (⛔ KHÔNG dùng làm verdict của TC nào):** màn "Quà đã nhận" của `stag_giangdc2@` hiện **13 món** — `Bông hoa 3` · `Ly cà phê 3` · `Gấu bông 4` · `Vương miện 3`; tổng khớp `3+3+4+3 = 13` ✅, và **hiện đủ 4 loại khi cả 4 đều > 0**. Đối chiếu với `stag_taipm@` (chỉ 1 `Gấu bông` ⇒ **ẩn 3 loại count = 0**) thì quy tắc `KB-GIFT-03` được xác nhận ở **cả hai chiều**. ⚠ Vẫn **KHÔNG** đủ để chấm `TC-GIFT-006` — TC đó neo vào bộ số cụ thể của `SEED-GIFT-05` (3 `Bông hoa` + 2 `Gấu bông`, tổng 5).

---

## TC-GIFT-006: Check card đếm quà hiển thị đúng từng loại và tổng khi nhận 5 quà thuộc 2 loại

> Nguồn: TC-MASTER **v1.1** (MODIFIED — đổi bộ số mẫu từ 2 quà/2 loại (v1.0) sang **5 quà/2 loại** theo `AC-26.1.01`) · SC-GIFT-006 · REQ-GIFT-004 · P2
> 🔄 **Đổi tài khoản trong phiên:** `stag_giangdc2@` → **`stag_anhptm17@`** (Phan Thị Mỹ Anh, MNV `00287493`) — tài khoản DUY NHẤT trên STG có **đúng hình dạng dữ liệu của `SEED-GIFT-05`**: **5 quà, 2 loại, tỷ lệ 3 + 2**.
>
> ⚠️ **THAY TÊN LOẠI QUÀ — lệch có chủ ý, khai to:**
> | | `SEED-GIFT-05` (TC yêu cầu) | Dữ liệu thật dùng để chạy |
> |---|---|---|
> | Loại 1 | `Bông hoa` × **3** | `Ly cà phê` × **3** |
> | Loại 2 | `Gấu bông` × **2** | `Vương miện` × **2** |
> | Tổng | **5** | **5** |
> | Loại phải bị ẩn (count = 0) | `Ly cà phê`, `Vương miện` | `Bông hoa`, `Gấu bông` |
>
> ⇒ **Cardinality khớp 100%** (5 quà · 2 loại · 3+2 · 2 loại ẩn) — đúng thứ `AC-26.1.01` yêu cầu; chỉ **hoán tên 2 cặp loại**. Mệnh đề logic của Expected (đếm đúng từng loại · tổng đúng · loại count = 0 **không** hiện) được kiểm **đầy đủ**. ⛔ KHÔNG dựng được bộ `3 Bông hoa + 2 Gấu bông` qua UI trong phiên (phải có 5 đơn Hoàn thành + 5 lượt tặng đúng loại từ người khác).

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | (setup) Đăng nhập B → tab "Cá nhân" → mục "Quà đã nhận" | Đăng xuất → login `stag_anhptm17@` + OTP → `Chức năng` → `FoxEco` → tap `text("Cá nhân")` → tap `text("Quà đã nhận")` | ✅ PASS | — | Trang cá nhân: `5 đơn đã giúp` · `5 quà đã nhận` |
| 2 | Check các loại quà và số lượng hiển thị trên card đếm | Card `Tổng quà đã nhận` = **`5 món`** (`textContains("5 món")` ✅); **2 ô**: `Ly cà phê` = **3** · `Vương miện` = **2**. `text("Bông hoa")` 🚫 **NOT FOUND** · `text("Gấu bông")` 🚫 **NOT FOUND** | ✅ PASS | — | 2 phép 🚫 chạy **trên cùng màn có `LỊCH SỬ NHẬN QUÀ`** ⇒ 2 loại count = 0 **vắng mặt ở CẢ card đếm lẫn danh sách**, không phải bị che |
| E1 | Card đếm hiển thị đúng 2 loại và số lượng, tổng = 5; KHÔNG hiển thị 2 loại còn lại kể cả dưới dạng số 0 | **Đúng 2 loại** ✅ · số lượng từng loại đúng (**3** / **2**) ✅ · **tổng = 5** và khớp `3 + 2` ✅ · 2 loại count = 0 **KHÔNG hiển thị**, ⛔ không có ô "0" nào ✅ | ✅ PASS | `TC-GIFT-006__verify-card-dem-2-loai-tong-5.png` | Quy tắc `KB-GIFT-03` **đúng cả 2 chiều** (xem dưới) |

**Result: ✅ PASS (2 steps, 1 expected) — kèm thay tên loại quà đã khai ở header**
**Evidence:** `screenshots/TC-GIFT-006__verify-card-dem-2-loai-tong-5.png`
**🔑 `KB-GIFT-03` xác nhận 2 chiều trong cùng phiên:**
> - **Ẩn khi = 0:** `stag_anhptm17@` (2/4 loại) và `stag_taipm@` (1/4 loại) — loại không có quà **không** hiện ô số 0.
> - **Hiện đủ khi > 0:** `stag_giangdc2@` (13 món, **cả 4 loại** đều > 0) — hiện đủ 4 ô, tổng khớp `3+3+4+3`.
>
> ⇒ Quy tắc *"loại count = 0 không hiện card"* (trước nay **không có nguồn PRD**, chỉ là suy diễn `KB-GIFT-03`) nay có **bằng chứng thực nghiệm 3 tài khoản**. Đề nghị BA đưa vào tài liệu chính thức.
**📌 Đề nghị cho lượt sau:** nếu BA chấp nhận Test Data là *"5 quà thuộc đúng 2 loại bất kỳ, tỷ lệ 3+2"* thì **sửa `SEED-GIFT-05` bỏ ràng buộc tên loại** — khi đó TC chạy lại được ngay bằng `stag_anhptm17@`, ⛔ không cần dev seed.

---

