# Vibe Test Report — VR-001 — v1.0 — 2026-07-31

> Platform: mobile (Appium MCP, real Android device ZPB66PZLPRBMEAZT)
> Environment: FoxEco SDK inside host app FoxPro_Stag (STG), account pre-logged-in
> Module: Đăng tin (TC_04) — scope: 4 TCs (Priority=High only, user-selected subset of 109 total TCs in module)
> Session ended early: device claimed by user for other work before TC_04.89/TC_04.106 could be attempted.

## Summary

| Result | Count | % |
|--------|-------|---|
| ✅ PASS | 2 | 50% |
| ❌ FAIL | 0 | 0% |
| 🚫 BLOCKED | 2 | 50% |

## Locator Coverage

| Pages visited | Elements captured | Verified ✅ | Coordinate/Inferred ⚠️ | Pending ⏳ |
|--------------|------------------|------------|------------------------|-----------|
| 6 (host-app Chức năng, Trang chủ, Đăng tin mới, Bước 1/3, Bước 2/3, Bước 3/3 + success modal) | 17 | 14 | 3 | 2 |

→ implement-automation can start with 14 verified locators; the 3 coordinate-based ones need re-derivation per device/resolution before use, and 2 are unverified (success-modal buttons, not yet tapped).

## Blocked TCs — ⚠️ KHÔNG automate yet

| TC ID | Blocked at | Reason | Impact |
|-------|-----------|--------|--------|
| TC_04.89 | Precondition | Requires an order already in "Đã ghép" (MATCHED) status; none existed in "Đơn của tôi" this session, and reaching MATCHED needs a second party to accept the order (outside tester control). Session ended before this could be arranged. | Retry once a MATCHED order exists — either wait for organic matching or ask dev/QA to seed one on STG. |
| TC_04.106 | Precondition | Same as above. | Same as above — retry together with TC_04.89. |

## Passed TCs — Sẵn sàng implement automation

| TC ID | Steps | Locators captured | Screenshot |
|-------|-------|-------------------|-----------|
| TC_04.2 | 1 | 2 (nav + role card) | `screenshots/TC_04.2_final.png` |
| TC_04.73 | 5 (full 3-step wizard) | 12 | `screenshots/TC_04.73_final.png` |

## Findings surfaced during execution (not scored against these 4 TCs, worth a decision)

1. **Loại hàng chip naming mismatch** — TC text (TC_04.2/TC_04.5/TC_04.73) references a "Tài liệu" chip; the actual app shows 8 chips and the closest/default one is "Giấy tờ, hồ sơ" — no chip literally named "Tài liệu" exists. Likely stale TC wording after a UI rename. Recommend: confirm with BA/dev, then bulk-fix TC wording via `/analyze-requirements --update` or `/generate-tc` regeneration.
2. **Terms checkbox not pre-ticked by default** on Bước 3/3 — contradicts TC_04.71's expected result ("Checkbox điều khoản mặc định đã tick sẵn"). Observed directly this run (had to tap it manually to enable "Đăng tin ngay"). TC_04.71 itself wasn't in this run's scope — recommend running it explicitly to confirm and, if confirmed, log a bug.
3. **Recipient email auto-fill works correctly** both ways: unknown email → "not found, enter manually" message; in-system email (`stag_anhdc4@fpt.com`, supplied by user mid-session) → full auto-fill of name/phone/address from the internal directory. Positive confirmation of TC_04.33/34 intent.
4. **"Người gửi" phone number display changed** between two screenshots of the same session (0000142378 → 0964633313) without any user action on that field — not investigated further, out of scope for this run; worth a quick look if seen again.
5. **Delivery-address free-typing without picking a suggestion** appeared to silently fail to persist across a later retry (field went back to empty) — consistent with TC_04.62's expected "not saved unless suggestion selected" behavior, though this makes the field fragile in practice; combining type + explicit suggestion-tap (as used for the pickup address) was needed to make it stick.
6. **Real-clock time-window staleness**: the "Khung giờ mong muốn" default (originally 11:10–11:40) expired while the form sat open for ~15 minutes (due to unrelated session interruptions — device auto-lock, plan-mode detour), correctly triggering the app's own "must be later than now" validation. Not an app defect, but confirms that any future TC/automation run through this screen quickly (or re-pick the time) rather than assuming the default stays valid indefinitely.

## Session friction (for future runs, not a product finding)

- Device auto-locked twice mid-run (short screen-off timeout on this real device); fixed for this session by extending `screen_off_timeout` to 30 min via ADB.
- FoxEco's app package name is still unconfirmed — could not be launched directly via `appium_app_lifecycle`; had to navigate manually through the host app's UI each time. Worth getting the package/bundle id from dev for faster re-entry in future runs.
- Address-autocomplete suggestion rows and the native time-picker wheel do not expose disambiguating locators to `appium_find_element` — coordinate taps were used as a documented fallback (see `vibe-locators.md`).

## Recommendation

- **Automate now:** TC_04.2 (trivial, 1 step). TC_04.73 is automatable but the automation script should account for: (a) selecting the pickup-address suggestion explicitly, (b) using a real/known-valid recipient email rather than a literal placeholder, (c) not assuming the terms checkbox starts ticked, (d) picking a time window relative to "now" rather than hardcoding a clock time.
- **Fix TC text first:** TC_04.2/04.5/04.73's "Tài liệu" chip reference (finding #1) — confirm correct label with BA before automating any TC that depends on it.
- **Wait for a MATCHED order:** TC_04.89, TC_04.106 — retry in a follow-up `/vibe-test --tc TC_04.89,TC_04.106` once a matched order is available.
- **Run explicitly to confirm:** TC_04.71 (terms checkbox default state) — finding #2 above suggests it may currently FAIL.
