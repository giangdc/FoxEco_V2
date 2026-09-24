# Repro — retest FE-341 + FE-342 — 2026-09-24

> Mode: **repro** (retest 2 bug Jira đang In review · Fixed, không sinh verdict TC) · STG · emulator-5554 · FoxPro 3.0.8
> Tài khoản: `stag_anhptm17@` (Phan Thị Mỹ Anh, người vận chuyển) — QC tự đăng nhập OTP
> Đơn dùng: `FPT Tân Thuận 1 → Tòa V-City` (gửi `giangdc2`, nhận Phan Minh Tài) — **Đang giao → Hẹn giao lại** lúc 11:30 (Hôm nay 11:30–12:00, "Toa V-City Le Thai To")

| Bug | Kết luận | Evidence |
|---|---|---|
| [FE-341](https://foxproject.atlassian.net/browse/FE-341) — đơn Cầm hàng về biến mất khỏi Đơn của tôi | ✅ **HẾT** (chế độ giao lại) | `FE-341__don-vua-hen-giao-lai-van-hien-dang-dien-ra.png` |
| [FE-342](https://foxproject.atlassian.net/browse/FE-342) — mặc định các trường khối Hẹn giao lại/Hẹn trả hàng | ⚠️ **FIX MỘT PHẦN — còn lỗi** | `FE-342__hen-giao-lai-gio-30p-noi-giao-lai-trong.png` · `FE-342__noi-giao-lai-nhan-chuoi-bat-ky.png` |

## FE-341
- Sau khi xác nhận "Cầm hàng về → Tôi sẽ giao lại sau", đơn **nằm đầu tab "Đang diễn ra"** với nhãn **"Hẹn giao lại"**.
- Các đơn Hẹn giao lại / Đang hoàn hàng tạo hôm 23/09 (cả vai "Giao:" và "Gửi:") cũng hiện đủ ở tab này và ở khối "Đơn của tôi" trên Trang chủ.
- ⚠️ Chưa tạo mới đơn chế độ **trả về người gửi** sau bản fix (chỉ thấy các đơn "Đang hoàn hàng" cũ vẫn hiện).

## FE-342
1. **Giờ Từ/Đến: ĐÃ FIX** — mặc định `11:30` → `12:00` (cách 30 phút), cả 2 chế độ.
2. **Nơi giao lại / Nơi nhận lại hàng: CHƯA FIX** — mặc định vẫn **trống** (chỉ có placeholder), không load theo địa chỉ đơn; là ô gõ tự do (`EditText`), gõ `zzz abc 123` vẫn nhận, không có danh sách chọn, nút "Xác nhận xử lý" bật.
