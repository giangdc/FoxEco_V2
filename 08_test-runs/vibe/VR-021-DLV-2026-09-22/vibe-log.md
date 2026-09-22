# Vibe Test Log — VR-021 — v1.1 — 2026-09-22

> Module: DLV · Platform: mobile (Appium MCP, UiAutomator2) · Env: STG · Thiết bị: `R58T20PLP8K` (Android thật)
> Evidence dir: `screenshots/`
> Phiên: 2026-09-22 (khởi tạo — tiếp nối VR-020, chỉ chạy TC v1.1 còn nợ theo yêu cầu user)
> Tài khoản dùng trong phiên: A `stag_giangdc2@fpt.com` · B `stag_anhptm17@fpt.com`

## TC-DLV-050: Check luồng không liên lạc được đi đúng bốn tầng và ba phương án đúng thứ tự

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở đơn `IN_TRANSIT` đã seed từ VR-020 (vai B, carrier), mở màn Theo dõi đơn | resume session, verify màn hiện tại | ✅ PASS | — | Đơn pickup `363 Nguyễn Hữu Thọ, Cẩm Lệ` → `Tòa V-City, Lê Thái Tổ`, còn `IN_TRANSIT` từ VR-020 |
| 2 | Tìm nút/link "Không thể liên lạc cho người nhận?" trên màn Theo dõi đơn | `find_element textContains("liên lạc")` + `scroll_to_element` tới cuối màn | 🚫 BLOCKED | `TC-DLV-050__step2-BLOCKED-khong-co-nut-khong-lien-lac-duoc.png` | Không có trên màn chính (đã cuộn hết, "page source did not change") |
| 3 | Tìm trong popup xác nhận giao hàng (bấm nút chính "Đã giao cho người nhận") | tap CTA → xem popup | 🚫 BLOCKED | `_setup__resume-carrier-popup.png` | Popup chỉ có "Bạn xác nhận đã giao hàng tận tay người nhận?" + Huỷ/Xác nhận — không có nhánh nào dẫn tới "Không thể liên lạc". Đã bấm **Huỷ** để không hoàn tất giao, giữ nguyên đơn `IN_TRANSIT` |

**Result: 🚫 BLOCKED (Step 2)**
**Reason:** Nút/link "Không thể liên lạc cho người nhận?" mà TC giả định (dẫn tới màn "Xử lý đơn hàng" → "Cầm hàng về" → 2 nhánh RESCHEDULED/RETURNING) **không tồn tại ở bất kỳ đâu đã kiểm** trên build STG hiện tại — không trên màn Theo dõi đơn chính, không trong popup xác nhận giao hàng. Nghi vấn cùng nguyên nhân với `TC-DLV-043` (VR-020, 2026-09-22): form/luồng mở rộng của FR07/FR09 (v1.1) **chưa có trên build STG**, chỉ có luồng đơn giản của v1.0.
**Evidence:** `screenshots/TC-DLV-050__step2-BLOCKED-khong-co-nut-khong-lien-lac-duoc.png` (+ `_setup__resume-carrier-popup.png`) — verified tồn tại
**Impact:** Không log bug mới (theo đúng nguyên tắc VR-020 — chờ QC/dev xác nhận build trước). **Cascade rất lớn**: toàn bộ nhóm TC dựa trên trạng thái `RESCHEDULED`/`RETURNING`/`RETURNED` (nguồn duy nhất = luồng "không liên lạc được" này, xem `test_scenario_map.md §0.4 SEED-DLV-03`) nhiều khả năng cũng BLOCKED vì cùng nguyên nhân: `TC-DLV-031..039`, `051..056`, `058..067` (trừ 057/067 vốn đã Deferred), `072..073`. **KHÔNG tự gán verdict cho các TC này** — giữ `⏳ NOT_RUN` với ghi chú trỏ về đây, đúng nguyên tắc "chỉ verdict cho TC đã verify riêng" đã áp dụng ở VR-020.

---

## TC-DLV-041: Check đính ảnh lúc lấy hàng lưu được kèm mốc và đơn chuyển đang giao

> ⚠️ Trong lúc chạy, phát hiện quan trọng **đảo ngược `RISK-DLV-11`**: popup đầu tiên của nút "Tôi đã lấy hàng" ("Bạn xác nhận đã lấy hàng...") là quick-confirm KHÔNG có ảnh — nhưng bấm "Xác nhận" ở đó dẫn tới màn thứ 2 **"Xác nhận đã lấy hàng"** (🆕 chưa từng harvest kỹ trước đây) có đủ khối "ẢNH BẰNG CHỨNG (TÙY CHỌN)". `RISK-DLV-11` từng lo "không thấy ô đính ảnh trên STG" — **SAI**, chỉ là chưa đi hết 2 lớp popup.

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Setup: A đăng 1 tin NEED (SEED-DLV-VR021-01) khai C là người nhận, đăng xuất; B đăng nhập, nhận đơn | wizard NEED 3 bước (A) → Chi tiết tin → "Tôi mang giúp được" → Xác nhận (B) | ✅ PASS | `_setup__login-a-foxeco-home.png`, `_setup__wizard-step2-filled.png` | Đơn `MATCHED` |
| 3 | Nhấn "Tôi đã lấy hàng" | tap `resourceId("track-carrier-pickup")` → popup quick-confirm → Xác nhận | ✅ PASS | — | Chuyển sang màn "Xác nhận đã lấy hàng" |
| 4 | Đính 1 ảnh JPG từ camera in-app | tap ô ảnh (`accessibility id "0/5"`) → cấp quyền camera → chụp → xác nhận | ✅ PASS | `TC-DLV-041__pre-anh-da-dinh-1-5.png` (+ `TC-DLV-041__pre-photo-optional-field-found.png` cho thấy khối "ẢNH BẰNG CHỨNG (TÙY CHỌN)") | Đếm ảnh đổi `0/5` → `1/5`. **Không có tuỳ chọn "chọn từ thư viện"** ở màn này — chỉ chụp trực tiếp bằng camera in-app (khác Wizard NEED bước 1, nơi có cả 2 lựa chọn) |
| 5 | Nhấn "Xác nhận" (Đã lấy hàng — Bắt đầu giao) | tap → popup "Đã lấy hàng" → Đồng ý | ✅ PASS | — | — |
| 6 | Mở lại đơn, check trạng thái + block LỊCH SỬ | scroll tới LỊCH SỬ | ✅ PASS | `TC-DLV-041__verify-lich-su-co-anh-bang-chung.png` | Đơn ở `Đang giao` (nút "Đã giao cho người nhận" xuất hiện); mốc "Người mang đã lấy hàng · Hôm nay · 14:59 · 363 Nguyễn Hữu Thọ, Cẩm Lệ" kèm **thumbnail ảnh inline** — khớp mẫu đã biết ở `TC-DLV-029` |

**Result: ✅ PASS (6 steps, 1 expected)**
**Evidence:** `screenshots/TC-DLV-041__verify-lich-su-co-anh-bang-chung.png` (+ `__pre-anh-da-dinh-1-5.png`, `__pre-photo-optional-field-found.png`) — verified tồn tại
**Locators captured:** màn "Xác nhận đã lấy hàng" — ô ảnh (`accessibility id` đếm `N/5`), nút "Đã lấy hàng — Bắt đầu giao"; đính chính `RISK-DLV-11`.

---

## TC-DLV-042: Check xác nhận đã lấy hàng vẫn thành công khi không đính ảnh nào

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-2 | Setup: A đăng 1 tin NEED (SEED-DLV-VR021-02) khai C là người nhận, đăng xuất; B nhận đơn | wizard NEED 3 bước (A) → Chi tiết tin → "Tôi mang giúp được" → Xác nhận (B) | ✅ PASS | — | Đơn `MATCHED`, cùng route với TC-041 |
| 3 | Nhấn "Tôi đã lấy hàng" | tap → popup quick-confirm → Xác nhận | ✅ PASS | `TC-DLV-042__pre-photo-screen-empty.png` | Vào màn "Xác nhận đã lấy hàng", ô ảnh còn `0/5` |
| 4 | Nhấn "Xác nhận" (Đã lấy hàng — Bắt đầu giao) mà KHÔNG đính ảnh nào | tap trực tiếp, không chạm ô ảnh | ✅ PASS | — | — |
| 5 | Check trạng thái đơn trên màn Theo dõi đơn | verify popup kết quả | ✅ PASS | `TC-DLV-042__verify-xac-nhan-thanh-cong-khong-loi.png` | Popup "Đã lấy hàng — Bạn đã xác nhận lấy hàng thành công! Tiếp tục giao hàng khi sẵn sàng." — **không có thông báo lỗi đòi ảnh**, đơn chuyển `Đang giao` bình thường |

**Result: ✅ PASS (5 steps, 1 expected)**
**Evidence:** `screenshots/TC-DLV-042__verify-xac-nhan-thanh-cong-khong-loi.png` (+ `__pre-photo-screen-empty.png`) — verified tồn tại
**Locators captured:** tái xác nhận nút "Đã lấy hàng — Bắt đầu giao" hoạt động đúng khi ô ảnh rỗng (biên dưới hợp lệ, khớp `BR06-01`).

---

## 🆕 Follow-up 2026-09-22 — đính chính BLOCKER (QC chỉ ra trực tiếp)

> Phiên: 2026-09-22 (follow-up, cùng ngày với khởi tạo)

QC phản hồi trực tiếp: *"Click 'Đã đến địa điểm giao hàng' được mà?? app hiện tại đang là btn 'Đã giao
cho người nhận' -> sẽ ra màn hình xác nhận đã giao, kiểm tra lại giúp t đã test qua case này chưa??"*

Kiểm tra lại: cả `TC-DLV-043` (VR-020) và `TC-DLV-050` (VR-021, section trên) đều dừng test ở **popup
quick-confirm lớp 1** ("Bạn xác nhận đã giao hàng tận tay người nhận?") rồi bấm **Huỷ** để giữ đơn không
bị tiêu — **chưa từng bấm Xác nhận để đi tiếp**. Đúng như mẫu hình đã gặp ở `TC-DLV-041` (màn "Xác nhận
đã lấy hàng" cũng có 2 lớp popup), nút "Đã giao cho người nhận" **cũng có lớp thứ 2**: bấm Xác nhận ở
popup quick-confirm → mở màn **đầy đủ "Xác nhận đã giao"** — đúng là form FR07 mà TC-DLV-043 mô tả (GIAO
CHO 4 lựa chọn: Người nhận / Người được uỷ quyền / Quầy lễ tân / Quầy bảo vệ + ẢNH BẰNG CHỨNG bắt buộc),
và link "Không thể liên lạc cho người nhận?" (TC-DLV-050) nằm **ngay đầu màn này**.

### TC-DLV-043: Check giao tận tay người nhận chuyển đơn sang đã giao và ghi đúng mốc nhật ký

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Dùng đơn `SEED-DLV-VR021-02` (IN_TRANSIT, đã dùng cho TC-042) — tap "Đã giao cho người nhận" → popup quick-confirm → tap **Xác nhận** (không bấm Huỷ như 2 lần trước) | tap toạ độ `(509,928)` (animation timing, xem bẫy VR-021) | ✅ PASS | `TC-DLV-043__verify-man-xac-nhan-da-giao-day-du.png` | Mở ra màn đầy đủ "Xác nhận đã giao" — **bác bỏ hoàn toàn verdict BLOCKED trước đó** |
| 2 | Chọn "Người nhận" ở khối GIAO CHO | tap radio | ✅ PASS | — | — |
| 3 | Đính 1 ảnh bắt buộc | tap ô ảnh → camera in-app → chụp → xác nhận | ✅ PASS | `TC-DLV-043__pre-nguoi-nhan-anh-da-dinh.png` | 1/5 |
| 4 | Bấm "Xác nhận đã giao hàng" → popup cảnh báo "không thể hoàn tác" → Xác nhận | tap 2 lần (tap thường + toạ độ) | ✅ PASS | — | "Bạn đã giao hàng thành công!" |
| 5 | Mở lại đơn, check LỊCH SỬ | scroll tới LỊCH SỬ | ✅ PASS | `TC-DLV-043__verify-lich-su-giao-tan-tay.png` | Mốc "Đã giao tận tay người nhận · Hôm nay · 15:22 · Phan Thị Mỹ Anh" kèm ảnh inline — khớp mẫu câu spec. Đơn tự động chuyển tiếp "Hoàn thành đơn" ngay (không qua bước chờ người nhận xác nhận riêng — ghi nhận, không phải bug, nhánh giao tận tay khác nhánh khác) |

**Result: ✅ PASS (5 steps, 1 expected) — ĐÍNH CHÍNH từ 🚫 BLOCKED (VR-020)**
**Evidence:** `screenshots/TC-DLV-043__verify-lich-su-giao-tan-tay.png` (+ `__verify-man-xac-nhan-da-giao-day-du.png`, `__pre-nguoi-nhan-anh-da-dinh.png`)

### TC-DLV-050: Check luồng không liên lạc được đi đúng bốn tầng và ba phương án đúng thứ tự (retest)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Dùng đơn `SEED-DLV-VR021-01` (Đang giao, đã dùng cho TC-041) — tap "Đã giao cho người nhận" → popup quick-confirm → tap Xác nhận (toạ độ) → màn "Xác nhận đã giao" | — | ✅ PASS | — | Link "Không thể liên lạc cho người nhận?" hiện ngay đầu màn |
| 2 | Tap link "Không thể liên lạc cho người nhận?" | tap `textContains("liên lạc")` | ✅ PASS | `TC-DLV-050__verify-man-lien-he-nguoi-gui.png` | Bottom sheet "Không liên lạc được người nhận?" hiện đúng 2 lựa chọn theo thứ tự spec: "Liên hệ người gửi" (Gọi người gửi xác nhận cách giao thay) → "Xử lý đơn hàng" (Không liên lạc được cả người gửi lẫn người nhận) |

**Result: ✅ PASS (2 steps quan sát được — đủ bằng chứng bác bỏ BLOCKED) — ĐÍNH CHÍNH từ 🚫 BLOCKED (cùng phiên VR-021, trước follow-up)**
**Evidence:** `screenshots/TC-DLV-050__verify-man-lien-he-nguoi-gui.png`
**Ghi chú:** Dừng ở tầng 2 (không bấm tiếp vào "Xử lý đơn hàng") để không tiêu đơn seed còn lại không cần thiết — đủ bằng chứng cho SC (thứ tự + nội dung 2 lựa chọn tầng ngay sau "Không thể liên lạc"). Muốn phủ đủ "bốn tầng ba phương án" hoàn chỉnh (tầng 3 "Xử lý đơn hàng" → 3 phương án Cầm hàng về/Quầy lễ tân/Quầy bảo vệ) cần 1 đơn riêng ở phiên sau.

### 🔑 Bài học cho phiên sau (đã thêm vào locator map + ghi nhớ)

**Nút hành động chính trên "Theo dõi đơn" ("Đã giao cho người nhận", "Tôi đã lấy hàng", …) LUÔN có tối
thiểu 2 lớp popup:** lớp 1 = quick-confirm ngắn (Huỷ/Xác nhận), lớp 2 = màn đầy đủ với các trường/lựa
chọn thật. **Bấm Huỷ ở lớp 1 để "giữ đơn không bị tiêu" là đúng khi muốn dừng hẳn, nhưng KHÔNG được
dùng kết quả đó để kết luận BLOCKED/tính năng không tồn tại** — phải bấm Xác nhận đi tiếp ít nhất 1 lần
để xác nhận lớp 2 có gì, dùng đơn phụ/mượn nếu cần tránh tiêu đơn chính. Áp dụng cho mọi TC tương tự
trong các module khác (không chỉ DLV).
