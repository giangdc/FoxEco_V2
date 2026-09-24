# Repro — retest FE-334 — 2026-09-24 (14:07–14:19)

> Mode: **repro** (retest bug In review · Fixed lúc 09:27/12:21, không sinh verdict TC) · STG · emulator-5554 · FoxPro 3.0.8
> Tài khoản: `stag_anhptm17@` (Phan Thị Mỹ Anh, người vận chuyển) · Oracle: demo `FoxEco Demo 3 vai tro v4.0` (trackAction + historyItems + showRetryCard/showReturnCard)
> Đơn dùng (`SEED-DLV-VR022-RESCHEDULE`, gửi `giangdc2`, nhận Phan Minh Tài): Hẹn giao lại (11:30) → Giao lại cho người nhận (14:10) → **Hẹn giao lại mới 14:15** (14:30–15:00, "Sanh V-City Le Thai To") → Giao lại (14:16) → **Cầm hàng về · trả người gửi 14:18** (14:30–15:00, "FPT Tan Thuan 1") ⇒ hiện **Đang hoàn hàng**. Dữ liệu tạo SAU bản fix.

| Bug | Kết luận | Evidence |
|---|---|---|
| FE-334 — validate SĐT người được uỷ quyền (+ case bổ sung 23/09) | ✅ SĐT `1` báo lỗi + khoá nút · ✅ "TÊN NGƯỜI NHẬN THAY *" đã có dấu bắt buộc · ⚠️ thiếu tên → nút khoá **không kèm thông báo** | `FE-334__sdt-1-so-bao-loi-nut-khoa.png` · `FE-334__uy-quyen-thieu-ten-nut-khoa-khong-bao-loi.png` |

## Chi tiết
- **FE-334:** Xác nhận đã giao → Người được uỷ quyền + 1 ảnh: SĐT `1` → lỗi "Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)", nút khoá ✅ · nhãn "TÊN NGƯỜI NHẬN THAY *" ✅ · tên + ảnh, SĐT trống → nút bật (SĐT không bắt buộc) · tên trống → nút khoá, **không có thông báo** ⚠️

> Tách từ phiên chung `RP-FE-331-334-337-338-2026-09-24` (hợp đồng repro ≤3 ảnh/thư mục). Cùng phiên: `RP-FE-331-338-2026-09-24` · `RP-FE-334-2026-09-24` · `RP-FE-337-2026-09-24`.
