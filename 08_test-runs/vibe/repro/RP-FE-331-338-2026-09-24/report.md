# Repro — retest FE-338 · FE-331 — 2026-09-24 (14:07–14:19)

> Mode: **repro** (retest bug In review · Fixed lúc 09:27/12:21, không sinh verdict TC) · STG · emulator-5554 · FoxPro 3.0.8
> Tài khoản: `stag_anhptm17@` (Phan Thị Mỹ Anh, người vận chuyển) · Oracle: demo `FoxEco Demo 3 vai tro v4.0` (trackAction + historyItems + showRetryCard/showReturnCard)
> Đơn dùng (`SEED-DLV-VR022-RESCHEDULE`, gửi `giangdc2`, nhận Phan Minh Tài): Hẹn giao lại (11:30) → Giao lại cho người nhận (14:10) → **Hẹn giao lại mới 14:15** (14:30–15:00, "Sanh V-City Le Thai To") → Giao lại (14:16) → **Cầm hàng về · trả người gửi 14:18** (14:30–15:00, "FPT Tan Thuan 1") ⇒ hiện **Đang hoàn hàng**. Dữ liệu tạo SAU bản fix.

| Bug | Kết luận | Evidence |
|---|---|---|
| FE-338 — thiếu block "Sẽ giao lại cho người nhận" | ✅ **HẾT** | `FE-338__block-se-giao-lai-va-nut-giao-lai.png` |
| FE-331 — lịch sử + nút đơn Hẹn giao lại (vai carrier) | ⚠️ **FIX 1 PHẦN** — nút ✅, dòng hẹn đủ ngày/giờ/nơi ✅, **thiếu 2 dòng lịch sử** ❌ | `FE-331__lich-su-hen-moi-sau-fix-thieu-2-dong.png` |

## Chi tiết
- **FE-338:** block có "Đã hẹn giao lại · 24/09 · 14:30–15:00" · nơi · "Giao lại cho: Phan Minh Tài" · ô Người vận chuyển "Đang giữ hàng" / Trạng thái "Chờ giao lại". Khác demo nhỏ: dòng phụ "Giao lại đúng lịch hẹn để người nhận chủ động nhận hàng" (demo: "Không giao được lần này — người vận chuyển giữ hàng và quay lại giao theo lịch hẹn"); ô 2 nhãn "Trạng thái" (demo "Người nhận"); không hiện "Ghi chú của người vận chuyển" (không nhập ghi chú).
- **FE-331:** nút cuối = **"Giao lại cho người nhận"** (cam) → popup "Bạn xác nhận đã đến lịch hẹn và tiếp tục giao hàng?" → "Đã tiếp tục giao hàng!". Lịch sử có "Đã hẹn giao lại · 24/09 · 14:30–15:00" + nơi, "Không liên lạc được người nhận"; **thiếu** "Không liên lạc được cả người gửi và người nhận" + "Người vận chuyển giữ hàng để giao lại" (demo có).
- **Ghi nhận thêm (chưa log):** mỗi lần bấm "Giao lại cho người nhận", lịch sử thêm dòng **"Lấy hàng resumed"** — nhãn lẫn tiếng Anh, không có trong demo.
- FE-341 (nhánh trả hàng, bổ sung): đơn vừa chuyển Đang hoàn hàng vẫn hiện ở Đơn của tôi › Đang diễn ra.

> Tách từ phiên chung `RP-FE-331-334-337-338-2026-09-24` (hợp đồng repro ≤3 ảnh/thư mục). Cùng phiên: `RP-FE-331-338-2026-09-24` · `RP-FE-334-2026-09-24` · `RP-FE-337-2026-09-24`.
