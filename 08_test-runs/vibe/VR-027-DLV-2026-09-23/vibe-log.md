# Vibe Test Log — VR-027 — v1.1 — 2026-09-23

> Module: DLV (Giao nhận & Theo dõi đơn) · Platform: mobile (Appium MCP + adb, UiAutomator2) · Env: STG · app `com.hrisproject.stag` (FoxPro) · Evidence dir: `screenshots/`
> Phiên: 2026-09-23 (15:51–16:18)
> Mode: **RETEST** bug Jira DLV đang **In review** (JQL 15:50): FE-327 (`TC-DLV-043`) · FE-334 (`TC-DLV-044`) · FE-331 + FE-338 (`TC-DLV-032`) · FE-337 (`TC-DLV-035`).
> Thiết bị: emulator-5554 · Tài khoản: `stag_anhptm17@` (Phan Thị Mỹ Anh, người vận chuyển). Đổi tài khoản 1 lần (giangdc2 → anhptm17).
> Đối chiếu: ảnh gốc (demo UI) đính kèm trong bug + PRD v1.1 §8.12.3 (`requirement_traceability.md` DLV dòng 31–32).
> ⛔ Theo yêu cầu QC: chỉ comment + đính kèm ảnh lên Jira, **KHÔNG đổi trạng thái bug**. Không cập nhật TC-MASTER / §8 / coverage trong run này.
> 📎 **Tên file trên Jira khác tên file local:** ảnh được upload lên Jira (attachment `32353`–`32366`) **trước** khi đổi sang quy ước `TC-<ID>__…`, nên trên Jira ảnh mang tiền tố `FE-<key>__` với cùng slug, nội dung giống hệt. Map tên: `FE-327__*`→`TC-DLV-043__*` · `FE-334__*`→`TC-DLV-044__*` (`FE-334__control-sdt-hop-le-…` = `TC-DLV-044__verify-doi-chung-sdt-hop-le-…`) · `FE-331__verify-hen-giao-lai-lich-su-va-nut` = `TC-DLV-032__verify-hen-giao-lai-cu-lich-su-va-nut` · `FE-331__verify-hen-giao-lai-moi-…`→`TC-DLV-032__verify-hen-giao-lai-moi-…` · `FE-338__verify-hen-giao-lai-dau-man` = `TC-DLV-032__verify-hen-giao-lai-cu-dau-man` · `FE-338__verify-hen-giao-lai-moi-dau-man-thieu-block`→`TC-DLV-032__…` · `FE-337__*`→`TC-DLV-035__*`.

## Dữ liệu thay đổi trên STG
- Đơn `363 Nguyễn Hữu Thọ → Tòa V-City` (ghi chú `SEED-TS-01`, gửi `giangdc2`, nhận `taipm`): `Đang giao` → **`Hẹn giao lại`** (16:10, hẹn Hôm nay 16:30–18:30).
- Đơn `FPT Tân Thuận 1 → Tòa V-City` (gửi `anhdc4`, nhận `giangdc2`): `Đang giao` → **`Đang hoàn hàng`** (16:14, hẹn trả 16:30–18:30, "FPT Tan Thuan 1").
- Đơn `FPT Tân Thuận 1 → Tòa V-City` (gửi `giangdc2`, nhận `taipm`): chỉ mở form "Xác nhận đã giao", **không gửi**, đơn vẫn `Đang giao`.

## TC-DLV-043: Nút xác nhận đến nơi giao + vào thẳng form (retest FE-327)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở đơn `Đang giao` (FPT Tân Thuận 1 → V-City), vai carrier | tap card | ✅ PASS | `TC-DLV-043__pre-carrier-dang-giao-nut-da-den-dia-diem.png` | nút chính = "Đã đến địa điểm giao hàng" |
| 2 | Bấm nút | tap | ✅ PASS | `TC-DLV-043__verify-bam-nut-vao-thang-man-xac-nhan-da-giao.png` | vào thẳng màn "Xác nhận đã giao", không có popup trung gian |

**Result: ✅ PASS — bug FE-327 ĐÃ fix**
**Evidence:** `TC-DLV-043__verify-bam-nut-vao-thang-man-xac-nhan-da-giao.png`
⚠️ Chỉ retest phạm vi bug (tên nút + bỏ popup); các expected khác của TC (log mẫu câu sau khi giao) không chạy lại trong phiên này.

## TC-DLV-044: Validate SĐT ở Người được uỷ quyền / Quầy lễ tân / Quầy bảo vệ (retest FE-334)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Chọn "Người được uỷ quyền", tên "Nguyen Van Retest", SĐT `1`, rời ô | set_value + tap nhãn | ✅ PASS | `TC-DLV-044__pre-uy-quyen-sdt-1-so-hien-loi.png` | lỗi "Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)" |
| 2 | Thêm 1 ảnh bằng chứng (camera) → bấm "Xác nhận đã giao hàng" | tap | ✅ PASS | `TC-DLV-044__verify-uy-quyen-sdt-1-so-bam-gui-bi-chan.png` | nút mờ, không gửi |
| 3 | Đổi sang "Quầy lễ tân" (giữ dữ liệu) → bấm gửi | tap | ✅ PASS | `TC-DLV-044__verify-quay-le-tan-sdt-1-so-bam-gui-bi-chan.png` | lỗi vẫn hiện, không gửi |
| 4 | Đổi sang "Quầy bảo vệ" → bấm gửi | tap | ✅ PASS | `TC-DLV-044__verify-quay-bao-ve-sdt-1-so-bam-gui-bi-chan.png` | lỗi vẫn hiện, không gửi |
| 5 | Đối chứng: SĐT `0912345678` | set_value | ✅ PASS | `TC-DLV-044__verify-doi-chung-sdt-hop-le-nut-xac-nhan-bat.png` | lỗi mất, nút bật. **Không bấm gửi**, back ra thì đơn vẫn `Đang giao` |

**Result: ✅ PASS — bug FE-334 ĐÃ fix**
**Evidence:** `TC-DLV-044__verify-uy-quyen-sdt-1-so-bam-gui-bi-chan.png` · `TC-DLV-044__verify-quay-le-tan-sdt-1-so-bam-gui-bi-chan.png` · `TC-DLV-044__verify-quay-bao-ve-sdt-1-so-bam-gui-bi-chan.png` · `TC-DLV-044__verify-doi-chung-sdt-hop-le-nut-xac-nhan-bat.png`
⚠️ Ngoài phạm vi: lúc `set_value` lỗi stale element, ô SĐT bị xoá trống và nút **bật** ở "Quầy bảo vệ" ⇒ SĐT trống vẫn được chấp nhận với lựa chọn quầy (đã nhắc trong comment FE-334, chưa log bug). Chỉ retest phạm vi validate SĐT; nhật ký "uỷ quyền bởi" của TC không chạy lại.

## TC-DLV-032: Màn Theo dõi đơn vai người vận chuyển khi Hẹn giao lại (retest FE-331 + FE-338)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Mở đơn Hẹn giao lại có sẵn (`363 Nguyễn Hữu Thọ → V-City`, hẹn 22/9 15:47) | tap card | ❌ FAIL | `TC-DLV-032__verify-hen-giao-lai-cu-dau-man.png` | không có block "Sẽ giao lại cho người nhận" |
| 2 | Cuộn tới LỊCH SỬ | scroll | ❌ FAIL | `TC-DLV-032__verify-hen-giao-lai-cu-lich-su-va-nut.png` | "Đã hẹn giao lại" không có giờ/nơi; nút "Đến hẹn, tiếp tục giao hàng" |
| 3 | Tạo lịch hẹn mới trên đơn `SEED-TS-01`: Đã đến địa điểm giao hàng → "Không thể liên lạc cho người nhận?" → Xử lý đơn hàng → **Cầm hàng về → Tôi sẽ giao lại sau**, Hôm nay 16:30–18:30, "Toa V-City Le Thai To" → Xác nhận (16:10) | tap/set_value | ✅ PASS | `_setup__don2-hen-giao-lai-filled.png` | đường vào form theo hướng dẫn của QC trong phiên |
| 4 | Back → mở lại đơn (màn không tự refresh) | tap | ❌ FAIL | `TC-DLV-032__verify-hen-giao-lai-moi-dau-man-thieu-block.png` | vẫn thiếu block "Sẽ giao lại cho người nhận" (FE-338) |
| 5 | Cuộn tới LỊCH SỬ | scroll | ❌ FAIL | `TC-DLV-032__verify-hen-giao-lai-moi-lich-su-va-nut.png` | `Đã hẹn giao lại 16:30–18:30` · `Không liên lạc được người nhận` · …; thiếu "Người vận chuyển giữ hàng để giao lại" / "Không liên lạc được cả người gửi và người nhận", dòng hẹn thiếu ngày và nơi; nút "Đến hẹn, tiếp tục giao hàng" thay vì "Giao lại cho người nhận" (FE-331) |

**Result: ❌ FAIL — FE-331 và FE-338 CHƯA fix** (cùng kết quả trên đơn cũ và đơn hẹn mới tạo sau bản fix)
**Evidence:** `TC-DLV-032__verify-hen-giao-lai-moi-dau-man-thieu-block.png` · `TC-DLV-032__verify-hen-giao-lai-moi-lich-su-va-nut.png` · `TC-DLV-032__verify-hen-giao-lai-cu-dau-man.png` · `TC-DLV-032__verify-hen-giao-lai-cu-lich-su-va-nut.png`

## TC-DLV-035: Màn Theo dõi đơn vai người vận chuyển khi Đang hoàn hàng (retest FE-337)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đơn `FPT Tân Thuận 1 → V-City` (gửi `anhdc4`) → Cầm hàng về → **Tôi sẽ trả về cho người gửi**, 16:30–18:30, "FPT Tan Thuan 1" → Xác nhận (16:14) | tap/set_value | ✅ PASS | `_setup__don3-hen-tra-hang-filled.png` | đơn sang `Đang hoàn hàng` |
| 2 | Back → mở lại đơn, xem nút cuối | tap | ✅ PASS | `TC-DLV-035__pre-dang-hoan-hang-dau-man.png` | đã có nút (mờ) "Đang trả hàng · chờ người gửi xác nhận" |
| 3 | Cuộn tới LỊCH SỬ | scroll | ❌ FAIL | `TC-DLV-035__verify-dang-hoan-hang-lich-su-va-nut.png` | `Đang hoàn hàng · 16:14` · `Không liên lạc được người nhận · 16:12` · …; không có "Hẹn trả hàng" (giờ/nơi), thiếu 2 dòng ngoại lệ, chấm cùng màu cam; carrier không xem được lịch hẹn trả hàng (PRD §8.12.3) |

**Result: ❌ FAIL — FE-337 CHƯA fix hoàn toàn** (đã có nút cuối, lịch sử vẫn sai)
**Evidence:** `TC-DLV-035__verify-dang-hoan-hang-lich-su-va-nut.png` · `TC-DLV-035__pre-dang-hoan-hang-dau-man.png`

## Setup / môi trường
- `_setup__start.png`: trạng thái máy lúc mở phiên (đang ở `giangdc2`). `_setup__don2-363-dang-giao-truoc-hen-giao-lai.png`: đơn `SEED-TS-01` trước khi hẹn giao lại.
- Sau "Xác nhận xử lý", màn Theo dõi đơn giữ dữ liệu cũ (nút "Đã đến địa điểm giao hàng") cho tới khi back ra rồi mở lại (ngoài phạm vi, chưa log bug).
