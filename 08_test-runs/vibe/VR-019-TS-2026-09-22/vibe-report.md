# Vibe Test Report — VR-019 — v1.1 — 2026-09-22

> Platform: mobile (Appium MCP, Android, 2 thiết bị song song trong run gốc; 1 thiết bị thật trong follow-up)
> Environment: STG · host app FoxPro (`com.hrisproject.stag`) · FoxEco SDK nhúng
> Total TCs trong scope: 17 (`TC-TS-008..024`, module TS, chỉ phạm vi v1.1 theo yêu cầu QC)
> Phiên: 2026-09-22 (khởi tạo) · 2026-09-22 (follow-up — retest 12 TC sau khi bypass được màn login Microsoft)

## Summary

**Kết quả CUỐI CÙNG (run gốc + follow-up + hiệu chỉnh sau log-bug 2026-09-22): 11 PASS · 5 FAIL · 1 BLOCKED · 0 NOT_EVIDENCED — scope 17/17 có verdict, evidence 17/17.**

Run gốc: 3 PASS · 1 FAIL · 13 BLOCKED (12 do `BUG-037` — màn đăng nhập Microsoft, 1 do `BUG-038` +
1 theo sau). Follow-up cùng ngày: QC tự đăng nhập tài khoản Microsoft **thật** trên thiết bị thật
`R58T20PLP8K`, yêu cầu dùng thiết bị này retest 12 TC bị chặn ở màn login. **Bypass thành công** —
WebView tải được form Microsoft Forms thật → 12 TC đảo verdict thành 9 PASS / 3 FAIL (7 FAIL tổng).

🔁 **Hiệu chỉnh sau khi log bug (cùng ngày):** `TC-TS-010`/`TC-TS-011` FAIL vì giả định "nút Gửi
disable" trong khi thực tế MS Forms dùng inline error — QC xác nhận **không phải bug** (`BUG-040`
đã xoá), sửa lại Expected theo đúng hành vi thật ⇒ 2 TC đảo verdict **FAIL → PASS**. `TC-TS-012`
vẫn FAIL nhưng lý do hẹp lại còn 1 vế (SĐT sai định dạng không bị chặn, `BUG-041` còn giữ).

🔴 **3 trong 5 FAIL còn lại đảo ngược clarification đã "Resolved" trước đó** (các clarification đó
dựa trên quan sát demo/phân tích TRƯỚC KHI từng đăng nhập qua được màn Microsoft — nay có bằng
chứng thật):
- `TC-TS-009` — màn xác nhận sau khi gửi là **mặc định Microsoft Forms**, không phải app-branded
  như `C-TS-03(d)` (Resolved) kết luận.
- `TC-TS-013` — "Hình ảnh đính kèm" **THỰC RA bắt buộc**, ngược giả định "biên dưới hợp lệ".
- `TC-TS-021` — ô "Mã đơn hàng" **THỰC RA sửa được**, ngược `C-TS-03(b)` (Resolved: "không sửa được").

`TC-TS-016` vẫn FAIL, `TC-TS-017` vẫn BLOCKED — cả hai do `BUG-038` (không liên quan màn login,
chưa nằm trong đợt retest này).

## Scope Coverage ★★ (module TS, xuyên run)

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module TS, v1.1)** | **17** | 100% |
| Chạy trong run gốc + follow-up | 17 | 100% |
| ✅ PASS từ run trước (không chạy lại) | 0 | 0% |
| ⛔ N-A | 0 | 0% |
| ⏳ NOT_RUN (còn nợ) | 0 | 0% |
| ⚠️ NOT_EVIDENCED (còn nợ) | 0 | 0% |

**Còn nợ = 0 TC → §8 = COMPLETED.**

- Chi tiết từng TC (xuyên run): `08_test-runs/vibe/coverage/coverage-TS.md`
- Chi tiết run này làm gì: `scope-ledger.md` (cùng thư mục)
- Chi tiết retest 12 TC + phân tích từng phát hiện: `vibe-log.md` §"🆕 Follow-up 2026-09-22"

## Kết quả cuối cùng (17 TC)

| Result | Count | % trên 17 |
|--------|-------|---|
| ✅ PASS | 11 | 64.7% |
| ❌ FAIL | 5 | 29.4% |
| 🚫 BLOCKED | 1 | 5.9% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | 17/17 (100%) |
| File ảnh mới trong `screenshots/` (follow-up) | 15 (`TC-TS-008`×2, `TC-TS-009`×2, `TC-TS-010`×1, `TC-TS-011`×1, `TC-TS-012`×1, `TC-TS-013`×1, `TC-TS-014`×1, `TC-TS-015`×1, `TC-TS-019`×2, `TC-TS-020`×1, `TC-TS-021`×1, `TC-TS-024`×1) |
| TC thiếu evidence (⚠️ NOT_EVIDENCED) | (không có) |
| Gate `verify_evidence.py` | xem Step 6.5 bên dưới |

## Locator Coverage

| Pages visited/re-verified | Elements captured mới | Verified ✅ | Not found ❌ |
|--------------|------------------|------------|-------------|
| 6 run gốc + Microsoft Forms content (follow-up) | 8 (+ ghi nhận **giới hạn kỹ thuật**: nội dung form KHÔNG expose input qua accessibility tree — không có locator để capture, tương tác bằng toạ độ) | 6 | 2 *(kết quả kiểm đúng của TC-TS-016/017, không phải locator sai)* |

→ implement-automation: `track-report-incident` sẵn sàng dùng (verify nút hiện/nhấn được).
⛔ **KHÔNG implement automation cho phần "điền form"/"gửi form"** — nội dung nằm trong Custom Tab
tách biệt, không có locator ổn định để automation dùng (xem `vibe-locators.md`).

## Failed TCs — Cần review TC / cập nhật spec (KHÔNG phải lỗi code app, trừ khi ghi chú khác)

| TC ID | Failed at | Expected | Actual |
|-------|----------|----------|--------|
| TC-TS-009 | Step 9 (check màn sau gửi) | Màn "Đã ghi nhận phản hồi" + cam kết 24h + nút "Quay lại đơn hàng" | Màn mặc định Microsoft Forms, không có 2 nội dung trên — 🔴 đảo `C-TS-03(d)` Resolved |
| TC-TS-012 | Step 7 | SĐT sai định dạng phải bị chặn *(Expected đã sửa 2026-09-22, xem `BUG-041`)* | SĐT sai định dạng **KHÔNG bị chặn** — `BUG-041` |
| TC-TS-013 | Step 8 (gửi 0 ảnh) | Gửi thành công | **Bị chặn** — Hình ảnh đính kèm THỰC RA bắt buộc — 🔴 đảo giả định gốc |
| TC-TS-016 | Step 6 | Thông báo lỗi thân thiện kèm nút "Thử lại" | Trang lỗi Chromium kỹ thuật (`net::ERR_INTERNET_DISCONNECTED`), không có nút "Thử lại" — `BUG-038` |
| TC-TS-021 | Step 5 (chạm ô Mã đơn hàng) | Nhãn tĩnh, không sửa được | **Sửa được** — bàn phím bật, ký tự chèn vào giá trị — 🔴 đảo `C-TS-03(b)` Resolved |

## Passed TCs — Sẵn sàng implement automation (phần không đụng nội dung form)

| TC ID | Steps | Locators captured | Evidence file |
|-------|-------|------------------|---------------|
| TC-TS-008 | 5 | `track-report-incident` | `TC-TS-008__verify-only-madon-prefilled.png` |
| TC-TS-010 | 6 | `track-report-incident` | `TC-TS-010__verify-gui-empty-required-behavior.png` *(Expected sửa 2026-09-22, `BUG-040` xoá)* |
| TC-TS-011 | 6 | `track-report-incident` | `TC-TS-011__verify-mota-empty-blocks-submit.png` *(cùng lý do `TC-TS-010`)* |
| TC-TS-014 | 6 | `track-report-incident` | `TC-TS-014__verify-5-anh-them-anh-bi-vo-hieu.png` |
| TC-TS-015 | 6 | `track-report-incident` | `TC-TS-015__verify-xoa-anh-3-con-4-anh.png` |
| TC-TS-018 | 7 | `track-report-incident`, `Quay lại` (đóng WebView) | `TC-TS-018__verify-quay-lai-dung-man-in-transit.png` |
| TC-TS-019 | 6 | `track-report-incident` | `TC-TS-019__verify-2-mota-empty-newsession.png` |
| TC-TS-020 | 7 | `track-report-incident` | `TC-TS-020__verify-trang-thai-khong-doi-sau-gui.png` |
| TC-TS-022 | 6 (3 checkpoint) | `track-report-incident`, card đơn `descriptionStartsWith` | `TC-TS-022__verify-observation3-intransit.png` |
| TC-TS-023 | 5 (2 checkpoint) | `track-report-incident`, `Tôi mang giúp được`, `Tôi đã lấy hàng` | `TC-TS-023__verify-observation2-intransit.png` |
| TC-TS-024 | 6 | `track-report-incident` | `TC-TS-024__verify-form-loaded-after-ms-login.png` |

⚠️ Automation cho các TC trên chỉ nên implement tới bước **mở WebView/check nút** — KHÔNG automate
việc điền/đọc nội dung bên trong Microsoft Forms (không có locator ổn định, xem Locator Coverage).

## BLOCKED TCs — còn nợ

| TC ID | Blocked at | Reason | Impact |
|-------|-----------|--------|--------|
| TC-TS-017 | Step 6 (nhấn Thử lại) | `BUG-038` — nút không tồn tại | Chờ fix `BUG-038`; KHÔNG liên quan màn login Microsoft nên chưa nằm trong đợt retest follow-up |

## NOT_EVIDENCED TCs — ⚠️ KHÔNG tính là PASS

(không có)

## Recommendation

- **Automate now (giới hạn tới bước mở form/check nút):** 11 TC PASS — locators ready trong `vibe-locators-latest.md`.
- **🔴 Route ngược `/analyze-requirements --update`:** mở lại `C-TS-03(b)` (mã đơn hàng sửa được,
  không phải nhãn tĩnh) và `C-TS-03(d)` (màn xác nhận là mặc định MS Forms, không phải app-branded);
  sửa `test_data_catalog.md`/`test_scenario_map.md` §TS: Hình ảnh đính kèm → bắt buộc (không phải
  optional), SĐT → không có validate định dạng.
- **`review-tc`/`generate-tc`:** cập nhật Expected của `TC-TS-008/009/013/019/020/021` trong
  `TC-MASTER-v1.1.xlsx` sau khi có clarification mới — vibe-test không tự sửa TC-MASTER.
  (`TC-TS-010/011/012` **đã sửa xong** 2026-09-22.)
- ✅ **Đã log 2026-09-22 (`05_bug-reports/draft/`, chưa push Jira):** `BUG-039` (màn xác nhận mặc định
  MS Forms) · `BUG-041` (SĐT không validate định dạng) · `BUG-042` (ảnh đính kèm bắt buộc, ngược
  giả định) · `BUG-043` (mã đơn hàng sửa được, ngược `C-TS-03(b)`).
  🗑️ `BUG-040` (nút Gửi không disable) **đã xoá** — QC xác nhận không phải bug, sửa Expected thay
  vì giữ bug (`TC-TS-010/011/012` cập nhật theo, xem trên).
- **Fix DEV (P2, bug thật, không đổi):** `TC-TS-016` FAIL + `TC-TS-017` BLOCKED chờ `BUG-038` (thêm
  nút "Thử lại" đúng spec khi WebView load lỗi mạng, thay trang lỗi Chromium mặc định).
- **CHẠY TIẾP phần còn nợ:** 0 TC actionable qua vibe-test — scope module TS (v1.1) đã **COMPLETED**
  17/17 verdict, evidence 17/17. `TC-TS-017` chờ Dev fix trước khi retest được.
