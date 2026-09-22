# Vibe Test Report — VR-018 — module CNL — v1.1 — 2026-09-21

> Platform: **mobile** (Appium MCP / UiAutomator2) · `emulator-5554` · STG · host app `com.hrisproject.stag` (FoxPro) → FoxEco
> Tập chạy: **chỉ 13 TC v1.1** theo yêu cầu QC. 🔓 QC cho phép đổi trạng thái đơn trên STG (đăng tin · ghép · lấy hàng · huỷ đơn / huỷ nhận đơn).
> Tài khoản: A người gửi `stag_anhdc4@` · B người vận chuyển `stag_anhptm17@` · C người nhận `stag_giangdc2@`. 3 lượt đổi tài khoản.

## Scope Coverage ★★ (mẫu số = SCOPE_TOTAL của module — gồm cả CARRIED v1.0)

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module CNL)** | **22** | 100% |
| Chạy **trong run này** | **13** | 59,1% |
| ✅ PASS từ **run trước** | 0 | 0% |
| ⛔ N-A | 0 | 0% |
| ⏳ **NOT_RUN (còn nợ)** | **9** | 40,9% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

**Còn nợ 9 TC → §8 = PARTIAL.** Cả 9 là **CARRIED v1.0** (`001 002 003 005 007 008 011 013 014`) — ngoài phạm vi QC yêu cầu.
⚠️ Header fragment v1.1 ghi 8 CARRIED, **thiếu `TC-CNL-014`** (đối chiếu ID 2 file TC-MASTER ra 9).

**📊 Riêng v1.1: 13/13 có verdict cuối (100%)** · ✅ 9 · ❌ 2 · 🚫 2 *(sau đính chính nội dung + follow-up chụp bù evidence 2026-09-22, xem khối dưới)*.

- Sổ tích lũy: `coverage/coverage-CNL.md` · audit phiên: `scope-ledger.md` · lát cắt v1.1: `coverage/PROGRESS-v1.1.md`

> 🔁 **ĐÍNH CHÍNH 2026-09-22 (QC GiangDC2) — 4 TC đổi ❌ FAIL → ✅ PASS:**
> - **`017`/`018`/`019`** — TC viết sai giả định nút "Yêu cầu hoàn hàng" (không tồn tại trong PRD). Đối chiếu trực tiếp PRD (`AC-25.2.01` §6.2 trang 27 · `BR11-04` §8.11.1 trang 45 · `FR09` §8.9 trang 43): PRD chỉ đảm bảo mức trạng thái, luồng hoàn hàng thật là **Người vận chuyển** bấm xác nhận tại điểm giao → màn "Xử lý đơn hàng" → chọn "Cầm hàng về". Expected 3 TC đã sửa lại theo đúng luồng — app **đúng đặc tả**. `BUG-033` đã xoá.
> - **`010`** — vế "ghi tên thay vì vai" được QC chấp nhận (app nhất quán ghi tên ở mọi dòng LỊCH SỬ). Expected đã sửa, không còn vướng mắc nào khác.
> - **`009` vẫn FAIL** — vế "tên thay vai" cũng được chấp nhận như `010`, nhưng vế **nhãn hành động sai** ("Đã huỷ nhận đơn" cho hành động Người gửi huỷ đơn) là lỗi độc lập, giữ nguyên `BUG-034`.
> ⚠️ **Follow-up evidence 2026-09-22:** ảnh gốc của cả 4 TC mang slot `__step*-FAIL` (chụp lúc chấm FAIL theo Expected cũ) — gate đòi PASS phải có `__verify`, không được đổi tên ảnh để né gate. Đã đăng nhập lại đủ 3 vai (A/B/C) và **chụp bù ảnh đúng slot**, không cần lặp lại thao tác huỷ/ghép nào vì log LỊCH SỬ bất biến (`BR11-03`) và ma trận nút của `Đang giao` không đổi theo thời gian. Chi tiết: `vibe-log.md` §"Follow-up 2026-09-22" · `coverage/coverage-CNL.md` khối "ĐÍNH CHÍNH 2026-09-22" + "FOLLOW-UP 2026-09-22".

## Kết quả các TC chạy trong run này (13 TC)

| Result | Count | % N_run |
|--------|-------|---|
| ✅ PASS | 9 (`006` `010` `012` `015` `016` `017` `018` `019` `022`) | 69% |
| ❌ FAIL | 2 (`004` `009`) | 15% |
| 🚫 BLOCKED | 2 (`020` `021`) | 15% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

*(bảng trên đã áp đính chính nội dung + follow-up chụp bù evidence 2026-09-22; số liệu lúc chạy phiên gốc 2026-09-21 là 5 PASS / 6 FAIL / 2 BLOCKED)*

## Evidence Coverage ★

| Chỉ số | Giá trị |
|---|---|
| TC có evidence / tổng TC đã chạy | **13/13** |
| File ảnh trong `screenshots/` | 29 (23 ảnh TC + 6 `_setup`) · gồm 4 ảnh `__verify` chụp bù follow-up 2026-09-22 · 0 cặp trùng md5 |
| Gate `.claude/hooks/verify_evidence.py` | xem mục Gate cuối file |

## 🐞 Bug đã log (draft, chờ QC push Jira — 2 ứng viên còn lại đã bị bác, xem đính chính trên)

| # | TC | Nội dung | Mức | Bug |
|---|---|---|---|---|
| 1 | **`009`** ❌ | Người gửi **huỷ đơn** nhưng LỊCH SỬ ghi **"Đã huỷ nhận đơn"** — nhãn của người vận chuyển huỷ nhận ⇒ người đọc log hiểu sai bên huỷ | P2 · Medium | `BUG-034` |
| 2 | **`004`** ❌ | Lý do huỷ 4 ký tự: nút `Xác nhận` khoá đúng nhưng **không có dòng lỗi dưới ô lý do** | P3 · Low | `BUG-036` |

~~`017`/`018`/`019` — thiếu nút "Yêu cầu hoàn hàng"~~ → **`BUG-033` đã xoá** (TC sai, xem đính chính trên).
~~`009`/`010` — log ghi tên người thay vì vai~~ → **`BUG-035` đã xoá** (QC chấp nhận hành vi app, xem đính chính trên).

## 🚫 Blocked

| TC | Blocked at | Lý do | Gỡ bằng cách |
|---|---|---|---|
| `TC-CNL-021` | Step 2 | Cần **2 phiên song song** (A + B), chỉ có 1 thiết bị | Cắm lại máy thật `R58T20PLP8K` hoặc bật emulator thứ 2 · ghi nhận: có **2 thời điểm** để thử cuộc đua (popup `Xác nhận` · màn trung gian `Xác nhận đã lấy hàng`) |
| `TC-CNL-020` | Step 1 | Không tạo được đơn `INCIDENT`: `Báo cáo sự cố` mở **webview đăng nhập Microsoft** (form ngoài app) | Dev seed 1 đơn `INCIDENT`, hoặc QC gửi thử form và dev xác nhận form có đổi trạng thái đơn |

## 📝 Ghi nhận ngoài Expected

- **2 TC "dự kiến FAIL" nay app đã chặn:** `012` (5 dấu cách → nút khoá — PASS) và `004` (4 ký tự → nút khoá, chỉ thiếu lỗi hiển thị). `009` dự kiến "không ghi log" — app **đã** ghi log.
- **Báo cáo sự cố = form Microsoft ngoài app** (webview `Sign in`), nút hiện ở **mọi trạng thái** đã thấy (cả `Chờ ghép`) — liên quan module `TS`.
- Sau **huỷ nhận** (B) app tự chuyển sang `Chi tiết tin` (không có LỊCH SỬ); sau **huỷ đơn** (A) app tự về danh sách `Đơn của tôi` ⇒ bước *"không rời màn Theo dõi đơn"* của `009`/`010` không làm được nguyên văn — LỊCH SỬ đọc bằng cách mở lại đơn.
- Người vận chuyển vừa huỷ nhận **vẫn nhận lại được** chính đơn đó từ Bảng tin (ghép lại 23:24).
- `TC-ACT-015` (Expected mới): đơn O1 `Đã huỷ` vẫn hiện ở tab `Đang diễn ra` của A — khớp.

## Locator Coverage

| Màn đã thăm | Element mới | Verified ✅ | Not found 🚫 |
|---|---|---|---|
| 6 (Theo dõi đơn 3 vai · popup huỷ · popup/màn lấy hàng · Báo sự cố · Chi tiết tin · Cá nhân) | 17 | 17 | 0 |

## Dữ liệu phát sinh trên STG

| Đơn | Trạng thái cuối | Ghi chú |
|---|---|---|
| **O1** — A `anhdc4` · Tòa V-City → FPT Cầu Giấy · người nhận `huyennhk` | **Đã huỷ** (23:34) | ghép bởi `anhptm17` 23:20 |
| **O2** — A `anhdc4` · FPT Tân Thuận 1 → Tòa V-City · người nhận `giangdc2` | **Đang giao** — carrier `anhptm17` | ⚠️ **còn mở**. LỊCH SỬ: đăng 23:16 · ghép 23:21 · huỷ nhận 23:22 · ghép lại 23:24 · lấy hàng 23:26. Dùng tiếp được cho `DLV` (giao / hoàn hàng → đơn `RETURNED` cho `TC-ACT-005/015`) |

**Máy ảo cuối phiên:** đăng nhập **`stag_giangdc2@`**.

▶️ Chạy nốt:
- `021` khi có 2 thiết bị: `/vibe-test --retest TC-CNL-021`
- `020` khi có đơn `INCIDENT`: `/vibe-test --retest TC-CNL-020`
- 9 TC CARRIED (nếu QC muốn): `/vibe-test --module CNL --tc TC-CNL-001,TC-CNL-002,TC-CNL-003,TC-CNL-005,TC-CNL-007,TC-CNL-008,TC-CNL-011,TC-CNL-013,TC-CNL-014`

## Gate
`python3 .claude/hooks/verify_evidence.py 08_test-runs/vibe/VR-018-CNL-2026-09-21` — kết quả ghi ở trả lời cuối phiên.
