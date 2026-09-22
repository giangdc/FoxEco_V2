# Vibe Log — VR-020 — module DLV — 2026-09-22

> Platform: mobile (Appium MCP · UiAutomator2) · Device `R58T20PLP8K` (thật) · App `com.hrisproject.stag`
> Môi trường: STG · Tài khoản dùng: A `stag_giangdc2@fpt.com` (Đặng Châu Giang) · B `stag_anhptm17@fpt.com`
> (Phan Thị Mỹ Anh) · C `stag_taipm@fpt.com` (Phan Minh Tài)
> ⚠️ **Phiên dừng SỚM theo yêu cầu user** (lo hết token giữa chừng, ~80% đã dùng) — chỉ hoàn tất bước
> seed + chạy được **1 TC tới verdict chính thức** (`TC-DLV-043`, BLOCKED) trước khi dừng.

## Setup (không phải TC, chuẩn bị dữ liệu)

1. Login A → đăng 4 tin NEED (`SEED-DLV-VR020-01..04`), người nhận C, tuyến `FPT Tân Thuận 1`/`363
   Nguyễn Hữu Thọ, Cẩm Lệ` → `Tòa V-City, Lê Thái Tổ`, buổi Sáng. Cả 4 đăng thành công.
2. Login B → nhận cả 4 đơn (`Tôi mang giúp được` → popup `Xác nhận`) + `Tôi đã lấy hàng`. Màn "Tôi đã
   lấy hàng" của v1.1 nay là màn riêng "Xác nhận đã lấy hàng" có ô ảnh bằng chứng TÙY CHỌN (0/5) — khác
   v1.0 (chỉ 1 popup đơn giản), khớp `PUP-03` đã resolve theo CHANGELOG DLV. Không phải TC nào trong scope
   (không có SC nào assert riêng bước này ở v1.1), chỉ ghi nhận làm setup.
3. Theo `Hoạt động` của B lúc dừng phiên: 2/4 đơn hiện `Đang giao`, 2/4 vẫn hiện `Đã ghép` — nghi có
   thao tác `lấy hàng` bị "stale element" (tap không có tác dụng) chưa kịp soát lại. Xem bảng trạng thái
   chi tiết ở `coverage/coverage-DLV.md` §"4 đơn seed còn sống" — cần verify lại đầu phiên sau trước khi
   dùng tiếp.

## TC-DLV-043: Check giao tận tay người nhận chuyển đơn sang đã giao và ghi đúng mốc nhật ký

**Steps thực hiện:**

| # | Step | Evidence |
|---|---|---|
| 1 | Đăng nhập B, mở "Theo dõi đơn" của `SEED-DLV-VR020-01` (`IN_TRANSIT`) | — |
| 2 | Rà màn, xác nhận nhãn nút chính vẫn là "Đã giao cho người nhận" (chưa đổi theo `BUG-044`) | `screenshots/BUG-044__verify-nut-van-cu-2026-09-22.png` |
| 3 | Bấm nút chính, kỳ vọng mở màn "Xác nhận đã giao" (form 4 loại đối tượng nhận + ảnh bắt buộc theo `DOC-v1.1-01 §8.7`) | `screenshots/TC-DLV-043__step3-BLOCKED-form-mo-rong-khong-ton-tai.png` |
| 4 | Kiểm tra chéo: lặp lại bước 3 trên đơn `SEED-DLV-VR020-02` (route pickup khác) | (không chụp thêm — cùng kết quả hệt bước 3, không phải TC khác nên không cần ảnh riêng) |

**Result:** 🚫 BLOCKED

**Actual:** Bấm nút chính ở bước 3 ra THẲNG popup xác nhận đơn giản y hệt v1.0 — *"Xác nhận — Bạn xác
nhận đã giao hàng tận tay người nhận? [Huỷ] [Xác nhận]"*. KHÔNG có field "Giao cho" (Người nhận/Người
được uỷ quyền/Quầy lễ tân/Quầy bảo vệ), không có bước ảnh bắt buộc, không có link "Không thể liên lạc".
Bấm "Huỷ" để không hoàn tất giao (giữ đơn `IN_TRANSIT` cho phiên sau — không đổi trạng thái, không thêm
dòng LỊCH SỬ, đã xác nhận bằng cách rà lại màn Theo dõi đơn).

**Evidence:** `screenshots/TC-DLV-043__step3-BLOCKED-form-mo-rong-khong-ton-tai.png`

**⚠️ Mâu thuẫn cần QC đối chiếu (không tự kết luận là bug, không log bug mới):**
- `RISK-DLV-08` (`02_analyze-requirements/v1.1/DLV-giao-nhan/risk_assessment.md`) từng ghi "Confirmed
  qua demo 2026-09-16" — cấu trúc UI + luồng submit đã khớp PRD.
- Module CNL, TC liên quan đến FR09 (chạy ở `VR-018`, 2026-09-21, hôm qua) mô tả luồng gián tiếp qua
  "Không thể liên lạc cho người nhận?" → "Xử lý đơn hàng" → "Cầm hàng về" tồn tại và bấm được.
- Hôm nay, trên đơn MỚI tạo, KHÔNG thấy dấu vết nào của các bước trên. Không rõ nguyên nhân: STG
  rollback build giữa 2 ngày? Feature flag theo tài khoản/role? Phiên trước quan sát nhầm (demo tĩnh thay
  vì STG thật)? **Cần QC/dev xác nhận build hiện tại trước khi retest hoặc log bug chính thức.**

**Tác động tới các TC khác cùng nhóm:** `TC-DLV-044..053`, `069..071` (13 TC, cùng phụ thuộc màn mở rộng
này) nhiều khả năng cũng sẽ BLOCKED vì cùng nguyên nhân — nhưng KHÔNG được tự gán verdict BLOCKED vì
chưa verify riêng từng TC (không có evidence riêng), giữ nguyên `⏳ NOT_RUN` trong `coverage-DLV.md`.

## Evidence bổ sung cho BUG-044 (đã log ở phiên trước — không tạo bug mới, không phải verdict TC)

Đơn `SEED-DLV-VR020-01` — TẠO MỚI trong chính phiên này (không phải đơn cũ) — vẫn hiện nút **"Đã giao
cho người nhận"**, KHÔNG phải **"Đã đến địa điểm giao hàng"** như QC đã chốt tên mới cho v1.1.
**Evidence:** `screenshots/BUG-044__verify-nut-van-cu-2026-09-22.png` (đã trích ở bước 2 của `TC-DLV-043`
ở trên). Củng cố `BUG-044` bằng dữ liệu độc lập, mới hơn evidence gốc (`VR-018`, 2026-09-21).

## Verdict cuối phiên

Chỉ **1 TC đạt verdict chính thức**: `TC-DLV-043` = 🚫 BLOCKED (evidence ở trên). Toàn bộ TC v1.1 pending
khác (031-036, 044-067 trừ 043, 069-073, 077, 079) vẫn `⏳ NOT_RUN` — CHƯA CHẠM TỚI, phiên dừng sớm theo
yêu cầu user trước khi kịp seed nhánh RESCHEDULED/RETURNING.
