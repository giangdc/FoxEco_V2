# Repro — retest FE-301 (+ FE-302 chưa chạy) — 2026-09-24 (15:16–15:24) · ⏸ DỪNG GIỮA CHỪNG

> Mode: **repro** (retest bug In review · Fixed 09:27, không sinh verdict TC) · STG · emulator-5554 · FoxPro 3.0.8
> Tài khoản: `stag_giangdc2@` (Đặng Châu Giang, người gửi) — AI tự đăng nhập OTP
> Phạm vi: FE-301 — 3 ghi nhận QC comment 23/09 15:24 · FE-302 — popup thoát wizard

| Bug / ghi nhận | Kết luận | Evidence |
|---|---|---|
| FE-301 ① câu lỗi "khối lượng" ≠ nhãn "TRỌNG LƯỢNG" | ✅ **HẾT** — lỗi hiện "Vui lòng chọn trọng lượng" | `FE-301__loi-trong-luong-dung-nhan.png` |
| FE-301 ② email thiếu `@` dùng câu "tên miền nội bộ" | ⏳ **CHƯA KIỂM** | — |
| FE-301 ③ lỗi cũ dưới tên/SĐT còn sau khi autofill | ⏳ **CHƯA KIỂM** | — |
| FE-302 popup "Thoát và bỏ nội dung đã nhập?" | ⏳ **CHƯA KIỂM** | — |

## Vì sao dừng
- Bước 1: xác nhận ảnh bằng **Chụp ảnh** (camera) → app bật về Trang chủ FoxEco, wizard mất.
- Sau đó app hiện màn OTP cũ của `stag_anhptm17@`; force-stop + mở lại → FoxEco chào **Phan Thị Mỹ Anh** (không phải tài khoản vừa login `stag_giangdc2@`) và tự nhảy vào các màn Theo dõi đơn của đơn khác (FTEL SG07 → SG16, người giao Nguyễn Tấn Vũ, thao tác 14:45–15:00).
- Chưa phân biệt được: lỗi app (FoxEco giữ phiên tài khoản cũ sau khi đổi account FoxPro) hay có người dùng chung emulator/tài khoản ⇒ **dừng, hỏi QC**. Chưa comment Jira.

## Chạy tiếp
Đăng nhập lại `stag_giangdc2@` → ảnh Bước 1 chọn **từ thư viện** (tránh camera) → Bước 2 kiểm ② ③ → thoát wizard kiểm FE-302.
