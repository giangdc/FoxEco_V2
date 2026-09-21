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

**📊 Riêng v1.1: 13/13 có verdict (100%)** · ✅ 5 · ❌ 6 · 🚫 2.

- Sổ tích lũy: `coverage/coverage-CNL.md` · audit phiên: `scope-ledger.md` · lát cắt v1.1: `coverage/PROGRESS-v1.1.md`

## Kết quả các TC chạy trong run này (13 TC)

| Result | Count | % N_run |
|--------|-------|---|
| ✅ PASS | 5 (`006` `012` `015` `016` `022`) | 38% |
| ❌ FAIL | 6 (`004` `009` `010` `017` `018` `019`) | 46% |
| 🚫 BLOCKED | 2 (`020` `021`) | 15% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|---|---|
| TC có evidence / tổng TC đã chạy | **13/13** |
| File ảnh trong `screenshots/` | 25 (19 ảnh TC + 6 `_setup`) · 0 cặp trùng md5 |
| Gate `.claude/hooks/verify_evidence.py` | xem mục Gate cuối file |

## 🐞 Ứng viên bug (⛔ chưa `/log-bug` — chờ QC review)

| # | TC | Nội dung | Mức gợi ý | Căn cứ |
|---|---|---|---|---|
| 1 | **`017` `018` `019`** ❌ | Khi đơn **Đang giao**, cả 3 vai **không có nút "Yêu cầu hoàn hàng"** — chỉ có `Báo cáo sự cố`. Hoàn hàng chỉ đi gián tiếp qua màn giao hàng của người vận chuyển | P1 · Major | `AC-25.2.01` + `BR11-04`. ⚠️ hỏi BA trước: nút riêng hay đường gián tiếp là đủ? Gộp **1 bug** cho 3 vai |
| 2 | **`009`** ❌ | Người gửi **huỷ đơn** nhưng LỊCH SỬ ghi **"Đã huỷ nhận đơn"** — nhãn của người vận chuyển huỷ nhận ⇒ người đọc log hiểu sai bên huỷ | P2 · Medium | `BR11-02` + `AC-25.1.01` |
| 3 | **`009` `010`** ❌ | Dòng log huỷ ghi **tên người** thay vì **vai** ("Người gửi" / "Người vận chuyển") | P3 · Low | `BR11-02`. ⚠️ **cần QC chốt** — app ghi tên người ở mọi dòng LỊCH SỬ; chấp nhận thì sửa Expected |
| 4 | **`004`** ❌ | Lý do huỷ 4 ký tự: nút `Xác nhận` khoá đúng nhưng **không có dòng lỗi dưới ô lý do** | P3 · Low | `VAL-04` + `AC-25.1.03` |

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
