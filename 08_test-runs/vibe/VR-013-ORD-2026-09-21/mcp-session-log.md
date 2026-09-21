# MCP Session Log — VR-013 — 2026-09-21

## Session info
- Platform: mobile (Appium MCP, UiAutomator2) — **2 session song song** (mọi call truyền `sessionId`)
- **EMU** `emulator-5554` (1080×2400, Android 13) — Session ID `b944ccd4-ceb7-4812-bdc2-864228ca23e8` — tài khoản A **Đặng Châu Giang**
- **REAL** `R58T20PLP8K` (SM-A127F, 720×1600) — Session ID `9ffdf4be-b083-4068-b84e-8a19b6d29a9a` — tài khoản B **Đặng Châu Anh**
- Host app: `com.hrisproject.stag` / `com.hrisproject.MainActivity`
- Pre-flight: ✅ `select_device` ×2 + `session create` ×2 (`autoLaunch=false`, `noReset=true`) + evidence-path (`_setup__*.png` ×2 tồn tại)
- Đổi tài khoản EMU (QC duyệt): Thủy → Giang qua FoxPro `Cá nhân` → `Đăng xuất` → `Đồng ý` → email → `NHẬN MÃ OTP` → OTP (biến `FOXECO_STG_PASS`, không in) → `ĐĂNG NHẬP` → `Chức năng` → `FoxEco`.
- 🧾 Evidence bằng `adb exec-out screencap` (tiền lệ VR-004); locator/thao tác 100% qua MCP.

## Pre-flight + Pha A
| # | MCP method | Args | Result | Note |
|--:|-----------|------|--------|------|
| 1-2 | select_device + session create | EMU | OK `b944ccd4` | Pre-flight |
| 3-4 | select_device + session create | REAL | OK `9ffdf4be` | Pre-flight |
| A1 | find_element ×~10 | FoxPro login/logout, FoxEco Trang chủ | OK | re-verify locator VR-011 |
| A2 | find_element (resourceId) | `value-tier-chip-option-low` · `weight-tier-chip-option-light/heavy` · `size-tier-chip-option-small/large` · `receiver-name-input` · `receiver-phone-input` | OK | **nâng ⚠️ → ✅** |

## Pha B — tổng hợp (không ghi từng call)
| Nhóm TC | Thiết bị | Snapshot (page_source) | Kết quả |
|---|---|---|---|
| 004·038·039·040·041·049·060·046·085 | EMU | 9 (màn thành công, tracking, edit form, Hoạt động) | ✅ ×9 |
| 065·072·073·088 | EMU (+ máy thật đối chứng `073`) | 6 | ✅ 065·072 · ❌ 073·088 |
| 052·083·084·068 | EMU | 0 (find_element + ảnh) | ✅ 052·083·068 · 🚫 084 |
| 061·048·044·045 | EMU + REAL | 12 (Hoạt động, Bảng tin ×2 máy) | ✅ ×4 |
| 080 | EMU + REAL | 4 | ⚠️ NOT_EVIDENCED |

## Statistics (ước lượng, không đếm từng call)
- Tổng MCP call ≈ 650 · tổng `get_page_source` ≈ 35 (đa số tự ghi ra file; màn nhỏ trả inline ~15k ký tự — `T24`) · số màn harvest ≈ 14
- find_element NOT FOUND đáng kể: `textContains("5MB")` (lỗi ảnh nằm dưới viewport) · `textContains("phải khác")` (đường gõ tay) · `resourceId("activity-order-card-0")` (bẫy T2)
- ⚠️ 1 lệnh `tap` dùng elementUUID cũ (màn đã đổi) vẫn báo *"Successfully tapped"* — đã kiểm không có tác dụng phụ (`T29`)
- Gate cuối run: xem lệnh chạy ở `vibe-report.md §Gate`
