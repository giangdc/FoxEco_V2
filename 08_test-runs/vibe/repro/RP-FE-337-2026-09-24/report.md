# Repro — retest FE-337 — 2026-09-24 (14:07–14:19)

> Mode: **repro** (retest bug In review · Fixed lúc 09:27/12:21, không sinh verdict TC) · STG · emulator-5554 · FoxPro 3.0.8
> Tài khoản: `stag_anhptm17@` (Phan Thị Mỹ Anh, người vận chuyển) · Oracle: demo `FoxEco Demo 3 vai tro v4.0` (trackAction + historyItems + showRetryCard/showReturnCard)
> Đơn dùng (`SEED-DLV-VR022-RESCHEDULE`, gửi `giangdc2`, nhận Phan Minh Tài): Hẹn giao lại (11:30) → Giao lại cho người nhận (14:10) → **Hẹn giao lại mới 14:15** (14:30–15:00, "Sanh V-City Le Thai To") → Giao lại (14:16) → **Cầm hàng về · trả người gửi 14:18** (14:30–15:00, "FPT Tan Thuan 1") ⇒ hiện **Đang hoàn hàng**. Dữ liệu tạo SAU bản fix.

| Bug | Kết luận | Evidence |
|---|---|---|
| FE-337 — màn Theo dõi đơn Đang hoàn hàng (vai carrier) | ❌ **CHƯA FIX** — thiếu block "Đơn chuyển sang trả hàng", nút vẫn xám, thiếu 2 dòng lịch sử | `FE-337__tra-hang-moi-thieu-block-nut-xam.png` · `FE-337__lich-su-tra-hang-moi-thieu-2-dong.png` |

## Chi tiết
- **FE-337:** dưới timeline là thẳng LỘ TRÌNH (không có block trả hàng: tiêu đề "Đơn chuyển sang trả hàng", giờ/nơi hẹn, ô trạng thái 2 bên). Nút carrier = xám "Đang trả hàng · chờ người gửi xác nhận" (demo: **"Đã trả hàng cho người gửi"** bấm được). Lịch sử: "Đang hoàn hàng · 24/09 · 14:30–15:00 · FPT Tan Thuan 1" (demo: "Hẹn trả hàng · …") · thiếu "Không liên lạc được cả người gửi và người nhận" + "Người vận chuyển cầm hàng về để trả người gửi" · mọi chấm cùng màu.

> Tách từ phiên chung `RP-FE-331-334-337-338-2026-09-24` (hợp đồng repro ≤3 ảnh/thư mục). Cùng phiên: `RP-FE-331-338-2026-09-24` · `RP-FE-334-2026-09-24` · `RP-FE-337-2026-09-24`.
