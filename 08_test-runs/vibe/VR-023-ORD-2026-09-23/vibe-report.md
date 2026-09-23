# Vibe Test Report — VR-023 — v1.1 — 2026-09-23

> Platform: mobile (Appium MCP, UiAutomator2) · Thiết bị: emulator-5554
> Environment: STG · app `com.hrisproject.stag` (FoxPro 3.0.8 → FoxEco)
> Module: ORD — Đăng tin & Quản lý tin · Mode: RETEST 3 bug Jira In review

## Kết quả retest

| TC | Bug | Before | After | Evidence after |
|---|---|---|---|---|
| TC-ORD-053 | FE-302 (BUG-010) | ❌ FAIL (VR-002) | ❌ **FAIL** — vẫn không có popup thoát, mất dữ liệu | `screenshots/TC-ORD-053__step4-FAIL-khong-co-popup-thoat.png` |
| TC-ORD-059 | FE-303 (BUG-011) | ❌ FAIL (VR-002) | ✅ **PASS** — buổi đã qua bị vô hiệu hoá | `screenshots/TC-ORD-059__verify-buoi-sang-da-qua-bi-chan.png` |
| TC-ORD-058 | FE-304 (BUG-012) | ❌ FAIL (VR-002) | ✅ **PASS** — "Sau giờ làm" chọn sẵn (NEED + OFFER) | `screenshots/TC-ORD-058__verify-buoi-mac-dinh-need.png` |

## Scope Coverage (mẫu số = SCOPE_TOTAL module)

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module ORD)** | **88** | 100% |
| Chạy **trong run này** | 3 | 3.4% |
| Còn nợ theo `coverage-ORD.md` (không đổi trong run này) | 3 | 3.4% |

Run này chỉ retest, **không** ghi §8 và chưa merge vào `coverage-ORD.md` (theo yêu cầu QC).

## Việc đã làm trên Jira
Comment kết quả recheck lên FE-302 (comment 31035) · FE-303 (31036) · FE-304 (31037). **Không đổi trạng thái** — cả 3 vẫn `In review` (đã kiểm lại sau khi comment).

## Việc chưa làm
- Merge verdict 053/058/059 vào `coverage-ORD.md` + TC-MASTER (Status) — chờ QC quyết.
- Đính kèm ảnh vào Jira — connector không hỗ trợ upload; QC upload tay nếu dev cần.
