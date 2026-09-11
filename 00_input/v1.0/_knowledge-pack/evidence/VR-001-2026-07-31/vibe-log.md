# Vibe Test Log — VR-001 — v1.0 — 2026-07-31

> Platform: mobile (Appium MCP, real Android device ZPB66PZLPRBMEAZT)
> Module: Đăng tin (TC_04) — Priority=High subset (4 TCs), user-scoped
> App: FoxEco SDK, opened from host app FoxPro_Stag (Chức năng → icon FoxEco)
> Account: pre-logged-in, "Chung Hoàng Liêm"

## TC_04.2: Check chọn 'Tôi cần gửi hàng' chuyển sang Wizard đăng tin Bước 1/3

| # | Step | Action | Result | Notes |
|---|------|--------|--------|-------|
| 1 | Bấm 'Tôi cần gửi hàng' | tap (uiautomator textContains) | ✅ PASS | — |
| E1 | Chuyển sang màn Wizard đăng tin Bước 1/3 (Thông tin hàng) | screenshot verify | ✅ PASS | Header shows "Bước 1/3 · Thông tin hàng" |

**Result: ✅ PASS (1 step, 1 expected)**
**Screenshot:** `screenshots/TC_04.2_final.png`
**Observation (not a TC_04.2 failure, informational):** Loại hàng chip default-selected = "Giấy tờ, hồ sơ". No chip literally labeled "Tài liệu" exists among the 8 Loại hàng options (Giấy tờ hồ sơ / Điện tử / Quần áo / Thực phẩm đồ uống / Sách văn phòng phẩm / Đồ gia dụng nhỏ / Quà tặng / Khác). TC_04.5's expected text ("mặc định = 'Tài liệu'") and TC_04.73's step text ("chọn Loại hàng 'Tài liệu'") both reference a chip name that does not exist in the current build — likely a stale TC wording vs. renamed UI label. Not in this run's scope (TC_04.5 not selected) — flagged for follow-up.

---

## TC_04.73: Check hoàn tất đăng tin NEED qua đủ 3 bước với dữ liệu hợp lệ

| # | Step | Action | Result | Notes |
|---|------|--------|--------|-------|
| 1 | Bước 1/3: chọn Loại hàng 'Tài liệu' [→ used default "Giấy tờ, hồ sơ", see note above], Giá trị hàng 'Vừa' | tap chip "Giá trị vừa" | ✅ PASS | 2 chips selected: Loại hàng default + Giá trị=Vừa |
| 2 | Bấm 'Tiếp theo' | tap | ✅ PASS | Advanced to Bước 2/3 without error |
| 3a | Nhập Địa chỉ lấy hàng | type + tap autocomplete suggestion | ✅ PASS | "Lô 37-39A KCX Tân Thuận" — required selecting the dropdown suggestion, typing alone was not sufficient (confirms TC_04.29/31 behavior) |
| 3b | Nhập Người nhận: email | type `tranthib@fpt.com.vn` | ❌ FAIL (wrong test data) | App responded "Không tìm thấy email này — vui lòng nhập tay". User corrected: valid in-system email is `stag_anhdc4@fpt.com` |
| 3b-retry | Nhập Email công ty người nhận (corrected) | type `stag_anhdc4@fpt.com` | ✅ PASS | App responded "Đã tìm thấy trong hệ thống nội bộ" and **auto-filled** Tên="Đặng Châu Anh", SĐT="0965633388", Địa chỉ giao hàng="L29B-31B-33B KCX Tân Thuận" (real contact data — accepted as substitute for the TC's literal placeholder values "Trần Thị B"/"0901234567"/"89 Nguyễn Thị Minh Khai, Q.3", since TC intent = "valid recipient data", satisfied by the auto-fill path) |
| 3c | Giữ nguyên Thời gian mặc định | — | ⚠️ deviation | Default "Khung giờ mong muốn" (11:10–11:40) went **stale** while the form sat open (~15 min due to interruptions) — app correctly blocked submit with "Khung giờ mong muốn phải lớn hơn giờ hiện tại". Manually reset to 12:10–12:40 via time picker to unblock. This is environmental (real-clock drift during a long interactive session), not an app defect. |
| 4 | Bấm 'Tiếp theo' | tap | ✅ PASS | Advanced to Bước 3/3 (Xác nhận & Đăng tin) once all fields valid |
| 5a | Giữ Checkbox điều khoản đã tick | — | ❌ FINDING | Checkbox was **NOT pre-ticked** by default — contradicts TC_04.71 ("Checkbox điều khoản mặc định đã tick sẵn"). Had to tap it manually to enable "Đăng tin ngay". |
| 5b | Bấm 'Đăng tin ngay' | tap | ✅ PASS | — |
| E5 | Tin được tạo thành công, trạng thái 'Chờ ghép' (POSTED) | screenshot verify | ✅ PASS | "Đăng tin thành công!" modal shown with "Theo dõi đơn" / "Về trang chủ" buttons |

**Result: ✅ PASS overall (core flow completed successfully end-to-end)**
**Screenshot:** `screenshots/TC_04.73_final.png`
**Findings surfaced during this TC (report separately, not necessarily bugs against TC_04.73 itself):**
1. Recipient-email lookup: wrong/unknown email correctly shows "not found, enter manually"; a real in-system email correctly triggers full auto-fill (positive finding, confirms TC_04.33/34 logic works).
2. Terms checkbox NOT pre-ticked by default on Bước 3/3 — conflicts with TC_04.71's expected result. Needs re-verification as its own TC run.
3. "Người gửi" phone number displayed changed between screenshots (0000142378 → 0964633313) without user action — possibly a display refresh/placeholder quirk on STG, not investigated further (out of scope).
4. "Loại hàng" chip naming mismatch (see TC_04.2 note above).

---

## TC_04.89: Check timeline hiển thị đầy đủ mốc kèm timestamp khi tin đã qua ≥2 trạng thái

**Result: 🚫 BLOCKED — precondition not satisfiable this session**
**Reason:** Requires an existing order that has progressed through ≥2 statuses (e.g. Chờ ghép → Đã ghép/MATCHED). The "Đơn của tôi" list observed during this run only showed "Đã huỷ" and "Chờ ghép" orders — no "Đã ghép" order existed. The new order created by TC_04.73 is freshly POSTED (1 status only) and reaching MATCHED requires a second party to accept/match it, which is outside this session's control. Device became unavailable (user needed it for other work) before this could be resolved.
**Impact:** Not automatable yet — needs a MATCHED-status order first. Retry in a future vibe-test run once one exists (naturally, or seeded by QA/dev).

---

## TC_04.106: Check khoá chỉnh sửa khi tin đã 'Đã ghép' (MATCHED)

**Result: 🚫 BLOCKED — same precondition gap as TC_04.89**
**Reason:** Same as above — no MATCHED-status order available in "Đơn của tôi" during this session.
**Impact:** Retry together with TC_04.89 once a MATCHED order exists.
