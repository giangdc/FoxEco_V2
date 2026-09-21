# Vibe Test Report — VR-016 — v1.1 (module FEED) — 2026-09-21

> Platform: mobile (Appium MCP, UiAutomator2, `emulator-5554`)
> Environment: STG — `com.hrisproject.stag`
> Total TCs chạy trong run này: **5** (theo yêu cầu QC: chỉ TC thuộc v1.1)

## Summary

## Scope Coverage ★★ (bảng ĐẦU TIÊN)

> Mẫu số LUÔN là SCOPE_TOTAL của module (15), không phải số TC đã chạy phiên này (5).
> Phiên này **cố ý** chỉ chạy 5 TC thuộc v1.1 theo yêu cầu QC — 10 TC carried v1.0 không tính là "còn nợ do hết sức phiên", nhưng vẫn là **còn nợ của module**.

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module FEED)** | **15** | 100% |
| Chạy **trong run này** | 5 | 33% |
| ✅ PASS từ run trước | 0 | 0% |
| ⛔ N-A | 0 | 0% |
| ⏳ **NOT_RUN (còn nợ)** | **10** | **67%** |
| ⚠️ NOT_EVIDENCED (còn nợ) | 0 | 0% |

**Còn nợ = 10 TC → §8 = PARTIAL.**

- Chi tiết từng TC (xuyên run): `08_test-runs/vibe/coverage/coverage-FEED.md` ← xem cái này
- Chi tiết run này làm gì: `scope-ledger.md`

## Kết quả các TC chạy trong run này

> ⚠️ `TC-FEED-009` **retest cùng ngày**: chạy lần 1 → BLOCKED (không có data hợp lệ), QC cấp 2 địa chỉ cụ thể → chạy lại → PASS.
> ⚠️ `TC-FEED-015` **đổi verdict cùng ngày sau khi QC review bug**: chạy → FAIL → log `BUG-029` → QC chấp nhận hành vi hiện tại là đúng, sửa Expected Result theo app → **PASS**, `BUG-029` rút lại.
> ⚠️ `TC-FEED-007` **retest cùng ngày theo yêu cầu QC**: chạy lần 1 (account Giang, data thiếu toạ độ) → FAIL 1 sub-clause → retest với account `stag_anhdc4@fpt.com` + data hợp lệ → **PASS** đủ 4/4 sub-clause.
> Bảng dưới là verdict **cuối cùng** của run.

| Result | Count | % trên 5 |
|--------|-------|---|
| ✅ PASS | 4 | 80% |
| ❌ FAIL | 0 | 0% |
| 🚫 BLOCKED | 1 | 20% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | 5/5 (100%) |
| File ảnh trong `screenshots/` (không tính `_setup__`/`_recon__`) | 10 (`TC-FEED-002__verify` · `TC-FEED-007__verify-bottom-section` (lần 1, hồ sơ) + `TC-FEED-007__verify-anhdc4-bottom-with-cta` (verdict cuối) + `TC-FEED-007__verify-anhdc4-sg09sg07-no-cta` (phát hiện phụ) · `TC-FEED-009__step2-BLOCKED` (lần 1, hồ sơ) + `TC-FEED-009__verify-real-map-route` (verdict cuối) · `TC-FEED-013__step1-BLOCKED` · `TC-FEED-015__step2-FAIL` ×2 (hồ sơ) + `TC-FEED-015__verify-accepted-behavior` (verdict cuối)) |
| TC thiếu evidence | (không có) |
| Gate `verify_evidence.py` | xem kết quả bên dưới §Gate |

→ QC lead verify lại từng case bằng `screenshots/TC-FEED-*__verify*.png` / `__stepN-*.png`.

## Locator Coverage

| Pages visited | Elements captured | Verified ✅ | Not found ❌ |
|--------------|------------------|------------|-------------|
| 2 (Bảng tin, Chi tiết tin) | 8 | 7 | 0 |

→ implement-automation có thể bắt đầu với 7 locators đã verified (xem `vibe-locators.md` + merge vào `locators/vibe-locators-latest.md`).

## Blocked TCs — ⚠️ KHÔNG automate

| TC ID | Blocked at | Reason | Impact |
|-------|-----------|--------|--------|
| TC-FEED-013 | Step 1 (precondition) | Bảng tin là danh sách cộng đồng toàn hệ thống, hiện có ≥5 tin Chờ ghép, một số là fixture của module ASN — không thể/không nên tự dọn qua UI | Chờ dev/QA chuẩn bị môi trường riêng (cửa sổ test tách biệt hoặc STG phụ) |

## Failed TCs — Cần review TC hoặc fix app

(không có — cả 4 TC chạy được trong phạm vi VR-016 đều kết thúc ✅ PASS)

> ✅ **`TC-FEED-007` — retest account `stag_anhdc4@fpt.com` cùng ngày, đủ 4/4 sub-clause.** FAIL lần 1 (account Giang, data `FTEL SG09/SG07` thiếu toạ độ) xác nhận đúng là do chọn nhầm test data, không phải bug — khớp kết luận đã rút ra từ retest `TC-FEED-009`.
> ✅ **`TC-FEED-015` — QC review `BUG-029` xong, chấp nhận hành vi hiện tại là đúng** (không phải bug): dòng cảnh báo text thay cho khung placeholder + "0km" khi văn phòng thiếu toạ độ. Expected Result đã sửa theo app, verdict đổi **FAIL → PASS**, `BUG-029` rút lại.
>
> 🔍 **Phát hiện phụ khi retest `TC-FEED-007`** (QC yêu cầu kiểm thêm): với `anhdc4`, CTA "Tôi mang giúp được" **vắng mặt có chọn lọc theo TỪNG TIN** — 2/3 tin không phải của `anhdc4` vẫn có CTA bình thường, chỉ 1 tin (`FTEL SG09→SG07`, người gửi Nguyễn Thị Thanh Thủy) không có. Khớp rule đã biết `OPR-05`/`SC-FEED-012`: người nhận được khai không thấy CTA — `anhdc4` nhiều khả năng là người nhận đã khai của đúng tin đó. **Không phải bug**, nhưng là data thật hữu ích cho `TC-FEED-012` (còn `⏳ NOT_RUN`, thuộc 10 TC carried v1.0).

## Passed TCs — Sẵn sàng implement automation

| TC ID | Steps | Locators captured | Evidence file |
|-------|-------|------------------|---------------|
| TC-FEED-002 | 2 | 3 (`feed-post-card-0..4`, `feed-post-own-badge`, CTA absent) | `screenshots/TC-FEED-002__verify-card0-no-cta.png` |
| TC-FEED-007 | 3 (retest: đăng xuất → đăng nhập `anhdc4` → mở tin Giang) | luồng đăng xuất/đăng nhập FoxPro (`USR-accounts.md §0b`), `feed-post-card-0` | `screenshots/TC-FEED-007__verify-anhdc4-bottom-with-cta.png` |
| TC-FEED-009 | 3 + tự tạo tin (Đăng tin wizard 3 bước) | 2 màn (Bảng tin, Chi tiết tin) + wizard address autocomplete | `screenshots/TC-FEED-009__verify-real-map-route.png` |
| TC-FEED-015 | 2 | — (dùng lại `feed-post-card-4`) | `screenshots/TC-FEED-015__verify-accepted-behavior.png` (bản copy của `__step2-FAIL-lo-trinh-no-map-box.png`, nội dung không đổi — chỉ đổi tên để khớp verdict cuối PASS sau khi QC sửa Expected Result; 2 file FAIL gốc vẫn giữ làm hồ sơ) |

## NOT_EVIDENCED TCs — ⚠️ KHÔNG tính là PASS

(không có)

## 🚦 Gate — `verify_evidence.py`

```
python3 .claude/hooks/verify_evidence.py 08_test-runs/vibe/VR-016-FEED-2026-09-21 \
  || python3 ~/.claude/skills/vibe-test/scripts/verify_evidence.py 08_test-runs/vibe/VR-016-FEED-2026-09-21
```

Kết quả: xem log lệnh chạy ngay sau report này trong phiên làm việc. Nếu exit ≠ 0 vì lý do (B) "còn nợ coverage" — đây là kỳ vọng đúng của phiên này (10 TC carried cố ý chưa chạy), KHÔNG phải lỗi cần sửa.

## Recommendation

- **✅ Đã xử lý:** `TC-FEED-015` — QC review `BUG-029`, chấp nhận hành vi hiện tại (dòng cảnh báo text) là đúng. Expected Result đã sửa theo app, `BUG-029` rút lại, không push Jira.
- **✅ Đã xử lý:** `TC-FEED-007` — retest account `anhdc4` + data hợp lệ → PASS đủ 4/4 sub-clause. Không log bug.
- **🎯 Cả 4 TC v1.1 chạy được trong VR-016 đều PASS.** Chỉ còn `TC-FEED-013` (BLOCKED, chờ dev/QA dọn môi trường cộng đồng) — không phải nợ kiểm thử của QC.
- **🔍 Gợi ý ưu tiên tiếp theo:** `TC-FEED-012` (carried v1.0, còn `⏳ NOT_RUN`) — đã có sẵn 1 cặp tin+tài khoản (`anhdc4` + tin `FTEL SG09→SG07`) xác nhận đúng điều kiện "người nhận được khai không thấy CTA", chạy case này sẽ tận dụng được ngay.
- **Cần môi trường riêng:** `TC-FEED-013` — chờ dev/QA dọn Bảng tin cộng đồng (không tự làm qua UI vì phá fixture module khác).
- **Automate ngay:** `TC-FEED-002`, `TC-FEED-007`, `TC-FEED-009`, `TC-FEED-015` — locator đã verified, có fixture data cố định.
- **🔑 Fixture mới cho module FEED (và các module khác cần văn phòng có toạ độ):** `FTEL An Giang Trần Hưng Đạo - Long Xuyên` ↔ `FTEL An Giang VPGD Bình Hòa` — đã xác nhận render bản đồ thật. ⛔ **KHÔNG dùng `location_address_catalog.xlsx` để tra cứu** văn phòng nào có toạ độ hợp lệ (100% dòng đều gắn `MISSING` bất kể lat/lng thật).
- **CHẠY TIẾP phần còn nợ của module:** 10 TC carried v1.0 (`001/003/004/005/006/008/010/011/012/014`) — `/vibe-test --module FEED` (bỏ giới hạn v1.1) khi QC muốn phủ nốt SCOPE_TOTAL = 15. Lưu ý `010`/`011` dự kiến FAIL theo thiết kế TC (bug đã biết, chưa log — `CHANGELOG.md §3 Nợ #1`).
