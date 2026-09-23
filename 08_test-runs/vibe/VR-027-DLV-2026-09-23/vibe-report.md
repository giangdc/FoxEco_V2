# Vibe Report — VR-027 — DLV — 2026-09-23

> Mode: **RETEST** các bug Jira DLV (Giao nhận & Theo dõi đơn) đang **In review** · STG · emulator-5554 · chi tiết ở `vibe-log.md`
> ⛔ Chỉ comment + đính kèm ảnh lên Jira, **không đổi trạng thái bug**. Không cập nhật TC-MASTER / §8 / coverage.

## Kết quả

| Bug (TC) | Verdict | Evidence chính | Kết luận |
|---|---|---|---|
| [FE-327](https://foxproject.atlassian.net/browse/FE-327) (BUG-044) · TC-DLV-043 | ✅ PASS | `TC-DLV-043__verify-bam-nut-vao-thang-man-xac-nhan-da-giao.png` | Nút đã đổi tên thành "Đã đến địa điểm giao hàng", bấm vào thẳng màn "Xác nhận đã giao", không còn popup ⇒ **đã fix** |
| [FE-334](https://foxproject.atlassian.net/browse/FE-334) · TC-DLV-044 | ✅ PASS | `TC-DLV-044__verify-*-sdt-1-so-bam-gui-bi-chan.png` ×3 + `__verify-doi-chung-*` | SĐT `1` ⇒ báo lỗi "Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)" và chặn gửi ở cả 3 lựa chọn (có ảnh; đối chứng bằng SĐT hợp lệ thì nút bật) ⇒ **đã fix** |
| [FE-331](https://foxproject.atlassian.net/browse/FE-331) · TC-DLV-032 | ❌ FAIL | `TC-DLV-032__verify-hen-giao-lai-moi-lich-su-va-nut.png` | Lịch sử vẫn thiếu dòng "giữ hàng để giao lại" / "không liên lạc được cả 2 bên", dòng hẹn thiếu ngày và nơi giao lại. Nút vẫn "Đến hẹn, tiếp tục giao hàng" |
| [FE-338](https://foxproject.atlassian.net/browse/FE-338) · TC-DLV-032 | ❌ FAIL | `TC-DLV-032__verify-hen-giao-lai-moi-dau-man-thieu-block.png` | Vẫn thiếu block "Sẽ giao lại cho người nhận" |
| [FE-337](https://foxproject.atlassian.net/browse/FE-337) · TC-DLV-035 | ❌ FAIL (1 phần đã sửa) | `TC-DLV-035__verify-dang-hoan-hang-lich-su-va-nut.png` | Đã có nút trạng thái "Đang trả hàng · chờ người gửi xác nhận". Lịch sử vẫn sai: không có "Hẹn trả hàng" (giờ/nơi), thiếu 2 dòng ngoại lệ, chấm cùng một màu |

**Tổng:** 2 PASS · 3 FAIL. FE-331/338 được kiểm trên cả đơn có sẵn (22/9) lẫn đơn hẹn giao lại **mới tạo sau bản fix**, cả 2 cho cùng kết quả.

## Jira
- Comment: FE-327 `31128` · FE-334 `31129` · FE-331 `31130` · FE-338 `31131` · FE-337 `31132` (16:17). Attachment id `32353`–`32366` (14 ảnh, tên trên Jira mang tiền tố `FE-<key>__` — map sang tên local ở đầu `vibe-log.md`).
- **Không đổi trạng thái**: cả 5 vẫn `In review` (đã kiểm lại sau khi comment).

## Ghi nhận ngoài phạm vi (chuyển QC quyết)
1. "Xác nhận đã giao" → Quầy bảo vệ: **để trống SĐT** thì nút gửi vẫn bật ⇒ SĐT không bắt buộc với lựa chọn quầy. Chưa đối chiếu spec. Đã nhắc trong comment FE-334.
2. Sau khi "Xác nhận xử lý" (hẹn giao lại/trả hàng), màn Theo dõi đơn **không tự refresh**: vẫn hiện nút "Đã đến địa điểm giao hàng" cho tới khi thoát ra rồi vào lại. Chưa log bug.

## Dữ liệu thay đổi trên STG (carrier `stag_anhptm17@`)
- Đơn `363 Nguyễn Hữu Thọ → Tòa V-City` (ghi chú `SEED-TS-01`, gửi `giangdc2`, nhận `taipm`): `Đang giao` → **`Hẹn giao lại`** (16:10, hẹn Hôm nay 16:30–18:30).
- Đơn `FPT Tân Thuận 1 → Tòa V-City` (gửi `anhdc4`, nhận `giangdc2`): `Đang giao` → **`Đang hoàn hàng`** (16:14, hẹn trả 16:30–18:30 tại "FPT Tan Thuan 1").
- Đơn `FPT Tân Thuận 1 → Tòa V-City` (gửi `giangdc2`, nhận `taipm`): chỉ mở form "Xác nhận đã giao" rồi **không gửi**, đơn vẫn `Đang giao`.
