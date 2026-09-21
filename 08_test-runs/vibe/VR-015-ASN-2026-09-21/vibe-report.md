# Vibe Test Report — VR-015 — v1.1 — 2026-09-21

> Platform: **mobile** (Appium MCP · UiAutomator2 · **2 session song song**: `emulator-5554` + real device `R58T20PLP8K`)
> Environment: STG — host app FoxPro `com.hrisproject.stag`, SDK nhúng FoxEco
> Module: **ASN (Ghép nối)** · Tập chạy phiên này: **1 TC — `TC-ASN-006`** (nhóm đa thiết bị QC để lại từ 2026-09-19)

## Scope Coverage ★★ *(trạng thái CẢ MODULE sau khi merge run này)*

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module ASN)** | **26** | 100% |
| Chạy **trong run này** | 1 | 4% |
| ✅ PASS từ **run trước** | 22 | 85% *(20 + `016` + `025` sau recheck)* |
| ❌ FAIL từ run trước | 0 | 0% *(2 FAIL của VR-010 — `016`,`025` — đã đổi PASS 2026-09-21 theo QC recheck)* |
| 🚫 BLOCKED (QC chốt 2026-09-21) | 3 | 12% |
| ⏳ **NOT_RUN (còn nợ)** | **0** | **0%** |
| ⚠️ NOT_EVIDENCED (còn nợ) | 0 | 0% |

*(Cộng: 1 PASS trong run này + 22 PASS run trước = **23 PASS**; 23 + 0 + 3 = 26. Chỉ v1.1: **10 PASS · 3 BLOCKED / 13**.)*
**Còn nợ = 0 TC** ⇒ mọi TC của module đều có verdict cuối. Các TC FAIL/BLOCKED **chưa** đóng — xem sổ module.

- Chi tiết từng TC **của module (xuyên run)**: `08_test-runs/vibe/coverage/coverage-ASN.md` ← **xem cái này**
- Chi tiết **run này làm gì**: `scope-ledger.md`

## Kết quả các TC chạy trong run này

| Result | Count | % trên 1 |
|--------|-------|---|
| ✅ PASS | 1 | 100% |
| ❌ FAIL | 0 | 0% |
| 🚫 BLOCKED | 0 | 0% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | **1/1 (100%)** |
| File ảnh trong `screenshots/` | 6 |
| TC thiếu evidence (⚠️ NOT_EVIDENCED) | — *(không có)* |
| Gate `verify_evidence.py` | xem §Gate cuối báo cáo |

## 🟢 `TC-ASN-006` — PASS (đủ mọi vế)

2 người vận chuyển (`stag_taipm@` trên real device, `stag_anhptm17@` trên emulator) bấm `Xác nhận` trên **cùng 1 tin** cách nhau **≤ ~95 ms**:
**emulator thắng** → màn `Theo dõi đơn` vai người vận chuyển; **real device thua** → toast **"Tin đã có người nhận vận chuyển"** và ở lại `Chi tiết tin`. Đúng nguyên văn Expected.

✅ **Vế chủ tin ĐÃ KIỂM (2026-09-21 16:58):** đăng nhập `stag_giangdc2@` → `Hoạt động` → mở đơn race: `LỊCH SỬ` ghi *"Ghép thành công · 16:22 · Phan Thị Mỹ Anh"* — đúng 1 người vận chuyển = người thắng; đơn còn lại (tin #1) ghi *"Ghép thành công · 16:13 · Phan Minh Tài"*. Ảnh: `TC-ASN-006__verify-chu-tin-thay-1-nguoi-van-chuyen-la-nguoi-thang.png`.

⚖️ Giới hạn: 1 mẫu ⇒ ⛔ không thay `TC-ASN-024` (50 request, NFR-06).

## 🔴 Lần chạy đầu KHÔNG hợp lệ — bài học

Lần 1 (16:13) emulator là `stag_thuyntt22@`; nút `Xác nhận` bị từ chối với toast **"Bạn cần chấp nhận điều khoản hiện hành trước khi đăng tin hoặc ghép chuyến"** ⇒ tài khoản này **chưa chấp nhận điều khoản** nên **không thể ghép ngay từ đầu**. Nếu lúc đó chỉ nhìn "một bên thành công, một bên bị chặn" thì **suýt ghi PASS oan** — ảnh chụp sau 6s lúc đầu thậm chí **không thấy toast** (đã tắt). Phải đọc **nội dung** toast, ⛔ không đọc "có toast là đúng".
⇒ **Luật cho mọi TC đa tài khoản:** trước khi tính vào cuộc đua, mỗi tài khoản phải **ghép được 1 tin độc lập** (hoặc đã có `đơn đã giúp` > 0) để chắc điều khoản đã chấp nhận.

## Phát hiện / đề nghị

| # | Phát hiện | Đề nghị |
|---|---|---|
| 1 | `stag_thuyntt22@` (Nguyễn Thị Thanh Thủy, MNV `00002352`, 0 đơn) **chưa chấp nhận điều khoản** ⇒ `Tôi mang giúp được` → toast chặn | Ghi vào `USR-accounts.md §1b`: không dùng làm carrier. Đề nghị BA xác nhận **điều khoản hiện ở đâu** với tài khoản mới (không thấy màn chấp nhận nào trước khi bấm ghép) |
| 2 | `stag_anhdc4@` **không thấy nút `Tôi mang giúp được`** ở 2 tin của `stag_giangdc2@` (cùng tuyến), dù `Thủy` / `taipm` / `anhptm17` **thấy**. Đã chờ 9–10s để loại trừ lỗi tải | Chưa rõ nguyên nhân (nghi `anhdc4` là người nhận của các tin này, hoặc rule khác). ⇒ QC/DEV xem; ⛔ chưa kết luận là bug |
| 3 | `credentials.env` **không có biến `FOXECO_STG_OTP`** như `CLAUDE.md`/`USR-accounts.md` mô tả; chỉ có `FOXECO_STG_PASS` (6 ký tự). Dùng `FOXECO_STG_PASS` làm mã ở màn `Xác nhận OTP` **đăng nhập được** (2/2 lần) | Sửa tài liệu **hoặc** thêm biến `FOXECO_STG_OTP`. ⚠️ Giá trị này **đã hiện trong ảnh chụp màn hình OTP của phiên** |
| 4 | `stag_anhptm17@` **đã có FoxEco + đã chấp nhận điều khoản** ⇒ carrier dùng được | Ghi vào `USR-accounts.md §1` |
| 5 | Real device `R58T20PLP8K` **timeout mạng ngắt quãng** (`Kết nối quá thời gian chờ`), màn danh sách có lúc **trống giả** | Khi dùng máy này: đợi 8–10s, ⛔ không kết luận "không có đơn" từ 1 ảnh |
| 6 | Sau lần 1, `Đơn của tôi` của `stag_taipm@` không còn thấy đơn `Giao … Đã ghép` (tin #1) — trùng lúc máy timeout | ✅ **Đã làm rõ 2026-09-21:** chủ tin thấy đơn tin #1 vẫn `Đã ghép` — `Ghép thành công · 16:13 · Phan Minh Tài`. Ở `taipm` chỉ là **tải lỗi do timeout mạng**, ⛔ không phải mất dữ liệu |
| 7 | Sự cố thao tác: 1 lần chạm nhầm trúng nút `Huỷ nhận đơn` trên emulator (16:25) | Đã bấm `Huỷ` đóng modal, **không** xác nhận huỷ — đơn của Mỹ Anh vẫn ở `Lấy hàng` |

## 🗂️ Dữ liệu STG bị tiêu thụ trong phiên

| Tin | Chủ tin | Kết quả |
|---|---|---|
| tin #1 `FTEL Đà Nẵng Cẩm Lệ → Tòa V-City` (~52′ tuổi) | `stag_giangdc2@` | **ghép bởi `stag_taipm@`** (lần 1, không hợp lệ) — ⚠️ xem phát hiện #6 |
| tin #2 cùng tuyến (~1 giờ tuổi) | `stag_giangdc2@` | **ghép bởi `stag_anhptm17@`** (lần 2, hợp lệ) — đang ở `Lấy hàng` |

Trạng thái đăng nhập cuối phiên: real device = `stag_taipm@`, emulator = `stag_giangdc2@` *(đổi từ `stag_anhptm17@` để chạy vế chủ tin)* *(trước phiên: `stag_anhdc4@` / `stag_thuyntt22@`)*.

## Recommendation

- ✅ Vế chủ tin của `TC-ASN-006` đã khép (2026-09-21 16:58).
- ✅ `TC-ASN-023` (thuộc VR-007): QC chấp nhận độ trễ đo được (2026-09-21) — không cần đo lại.
- ~~`/log-bug` cho `016`/`025`~~ — **HỦY 2026-09-21**: QC recheck xác nhận đó không phải bug (trần 5 theo tài khoản là quy tắc thực tế). `014`/`017` không cần chạy lại. ✅ BA đã xác nhận lại 2026-09-21 (qua QC) — rule cũ `C-ASN-04(e)` bị thay.
- **Cần cập nhật tài liệu:** `USR-accounts.md` (điểm 1, 2, 3, 4 ở trên).
