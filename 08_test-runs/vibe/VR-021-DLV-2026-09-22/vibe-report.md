# Vibe Test Report — VR-021 — v1.1 — 2026-09-22

> Platform: mobile (Appium MCP, UiAutomator2) · Thiết bị: `R58T20PLP8K`
> Environment: STG · app `com.hrisproject.stag` (FoxPro → FoxEco)
> Module: DLV — Giao nhận & Theo dõi đơn · Phiên tiếp nối VR-020, chỉ chạy TC v1.1 còn nợ theo yêu cầu user

> 🔴 **ĐÍNH CHÍNH 2026-09-22 (QC chỉ ra trực tiếp, follow-up cùng ngày):** báo cáo này đã được viết lại
> sau khi phát hiện verdict `BLOCKED` ban đầu của `TC-DLV-043`/`TC-DLV-050` là **SAI** — nguyên nhân do
> dừng test ở popup quick-confirm lớp 1 (bấm Huỷ để giữ đơn) mà chưa từng bấm Xác nhận để thấy màn đầy
> đủ "Xác nhận đã giao" (có đúng cả form FR07 + link "Không thể liên lạc"). Chi tiết quá trình đính
> chính: `vibe-log.md` mục "🆕 Follow-up — đính chính BLOCKER". Báo cáo dưới đây là **bản đã sửa**.

## Scope Coverage ★★ (mẫu số = SCOPE_TOTAL module, không phải số TC chạy phiên này)

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module DLV)** | **81** | 100% |
| Chạy **trong run này** | 5 | 6.2% |
| ✅ PASS từ **run trước** (VR-012, không chạy lại) | 20 | 24.7% |
| ⛔ N-A (cố ý không test qua UI, có lý do) | 4 | 4.9% |
| ⏳ **NOT_RUN (còn nợ)** | **58** | **71.6%** |
| ⚠️ NOT_EVIDENCED (còn nợ) | 0 | 0% |

**Còn nợ = 58 TC → §8 = PARTIAL.**

- Chi tiết từng TC của module (xuyên run): `08_test-runs/vibe/coverage/coverage-DLV.md` ← xem cái này
- Chi tiết run này làm gì: `scope-ledger.md` trong run folder

## Kết quả các TC chạy trong run này

| Result | Count | % trên N_run=5 |
|--------|-------|---|
| ✅ PASS | 5 | 100% |
| ❌ FAIL | 0 | 0% |
| 🚫 BLOCKED | 0 | 0% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | 5/5 (100%) |
| File ảnh trong `screenshots/` | 13 |
| TC thiếu evidence | — |

## Locator Coverage

| Pages visited | Elements captured mới | Verified ✅ |
|--------------|------------------|------------|
| 3 màn mới harvest đầy đủ ("Xác nhận đã lấy hàng", "Xác nhận đã giao" — form FR07, bottom sheet "Không liên lạc được người nhận?") | ~20 | ~18 |

→ implement-automation có thể dùng ngay locator của cả 3 màn — xem `vibe-locators-latest.md`.

## 🔑 2 phát hiện chính của phiên

**1. Đính chính `RISK-DLV-11`:** ô ảnh bằng chứng lúc lấy hàng CÓ tồn tại (màn "Xác nhận đã lấy hàng",
lớp popup thứ 2, không phải lớp quick-confirm đầu). `TC-DLV-041` (1 ảnh) / `TC-DLV-042` (0 ảnh) PASS.

**2. Đính chính verdict BLOCKED của `TC-DLV-043`/`TC-DLV-050`:** cả 2 verdict BLOCKED ban đầu đều SAI.
Nút "Đã giao cho người nhận" có **2 lớp popup**: lớp 1 quick-confirm (Huỷ/Xác nhận), lớp 2 là màn đầy
đủ **"Xác nhận đã giao"** — có sẵn form FR07 (GIAO CHO 4 lựa chọn + ảnh bắt buộc) **và** link "Không thể
liên lạc cho người nhận?" ngay đầu màn. Retest thật: `TC-DLV-043` PASS (giao "Người nhận", log đúng
mẫu câu), `TC-DLV-050` PASS (bottom sheet 2 lựa chọn đúng thứ tự spec). **Bài học:** không kết luận
BLOCKED/tính năng-không-tồn-tại chỉ từ việc bấm Huỷ ở popup lớp 1 để giữ đơn — phải xác nhận đi tiếp
ít nhất 1 lần bằng đơn phụ.

## Passed TCs — Sẵn sàng implement automation

| TC ID | Steps | Evidence file |
|-------|-------|---------------|
| TC-DLV-041 | 6 | `screenshots/TC-DLV-041__verify-lich-su-co-anh-bang-chung.png` |
| TC-DLV-042 | 5 | `screenshots/TC-DLV-042__verify-xac-nhan-thanh-cong-khong-loi.png` |
| TC-DLV-043 | 5 | `screenshots/TC-DLV-043__verify-lich-su-giao-tan-tay.png` |
| TC-DLV-050 | 2 (quan sát đủ bằng chứng) | `screenshots/TC-DLV-050__verify-man-lien-he-nguoi-gui.png` |

## Recommendation

- **Automate now:** 4 TC (`TC-DLV-041`/`042`/`043`/`050`) — locators sẵn sàng trong `vibe-locators-latest.md`.
- **CHẠY TIẾP bình thường** (không còn nghi blocker): family `TC-DLV-044..053`/`069..071`/`031..039`/
  `051..056`/`058..067`/`072..073` (~40 TC) giờ chỉ là pending thông thường — form FR07 và luồng
  "không liên lạc" đã xác nhận CÓ tồn tại trên STG. `/vibe-test --module DLV` (bộ lọc pending tự bốc).
- **`TC-DLV-050` cần hoàn thiện:** đã quan sát tầng 2 (2 lựa chọn "Liên hệ người gửi"/"Xử lý đơn hàng"),
  còn nợ tầng 3 (bấm "Xử lý đơn hàng" → xem 3 phương án "Cầm hàng về"/"Quầy lễ tân"/"Quầy bảo vệ" đúng
  thứ tự) — cần 1 đơn riêng ở phiên sau để đi hết 4 tầng.
- **Deferred (cần dev hỗ trợ, không tự seed qua UI được):** `TC-DLV-057`, `TC-DLV-067` (mốc thời gian
  4h/24h) — gộp chung lô với `TC-DLV-024`(v1.0)/`SC-TS-006` khi có dev hỗ trợ lùi timestamp. `TC-DLV-040`
  cũng cần dev hỗ trợ lùi timestamp ở step cuối.
