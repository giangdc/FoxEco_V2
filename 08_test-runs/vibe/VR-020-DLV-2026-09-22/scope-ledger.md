# Scope Ledger — VR-020 — module DLV — SCOPE_TOTAL = 81 TC

> Seed từ: `coverage/coverage-DLV.md` (trạng thái trước phiên: có verdict 19/81)
> Tập chạy phiên này: chỉ các TC v1.1 còn nợ (`TC-DLV-031..081`, loại trừ CARRIED v1.0), theo yêu cầu user.
> ⚠️ Phiên dừng SỚM theo yêu cầu user (lo hết token ~80%) — không chạy hết batch dự kiến.

## Việc đã làm trong phiên

1. Đăng nhập A (`stag_giangdc2@fpt.com`) — đăng 4 tin NEED mới (`SEED-DLV-VR020-01..04`), người nhận C (`stag_taipm@fpt.com`), tuyến pickup `FPT Tân Thuận 1`/`363 Nguyễn Hữu Thọ, Cẩm Lệ` → `Tòa V-City, Lê Thái Tổ`, buổi Sáng.
2. Đăng nhập B (`stag_anhptm17@fpt.com`) — nhận cả 4 đơn (`Tôi mang giúp được`) + xác nhận `Tôi đã lấy hàng` (màn mới có ảnh bằng chứng tuỳ chọn — khác v1.0). ⚠️ Lúc dừng phiên chỉ 2/4 đơn xác nhận chắc chắn `IN_TRANSIT` — 2 đơn còn lại cần soát lại đầu phiên sau.
3. Chạy `TC-DLV-043` trên đơn `SEED-DLV-VR020-01` (`IN_TRANSIT`) → phát hiện form mở rộng FR07 không tồn tại → verdict `BLOCKED`, evidence đầy đủ (xem `vibe-log.md`). Kiểm tra chéo (không tính verdict riêng) trên `SEED-DLV-VR020-02` — cùng kết quả.
4. KHÔNG tự gán verdict cho `TC-DLV-044..053`/`069..071` dù cùng nguyên nhân — giữ `⏳ NOT_RUN` vì chưa verify riêng từng TC (đúng luật evidence-per-TC).

## Verdict cuối phiên

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-DLV-043 | 🚫 BLOCKED | 1 | run này | `TC-DLV-043__step3-BLOCKED-form-mo-rong-khong-ton-tai.png` |
| TC-DLV-044..053, 069..071 (13 TC) | ⏳ NOT_RUN | — | — | cùng nghi vấn với TC-DLV-043 nhưng chưa verify riêng — xem coverage-DLV.md |
| Tất cả TC v1.1 còn lại (031-036, 054-068 trừ 068, 072-073, 077, 079) | ⏳ NOT_RUN | — | — | Chưa chạm tới — phiên dừng sớm theo yêu cầu user |

## Bằng chứng thu thêm cho BUG-044 (không phải TC mới, củng cố evidence đã log trước)

- `screenshots/BUG-044__verify-nut-van-cu-2026-09-22.png` — đơn `SEED-DLV-VR020-01` (`IN_TRANSIT`, tạo MỚI trong chính phiên này) vẫn hiện nút "Đã giao cho người nhận", KHÔNG phải "Đã đến địa điểm giao hàng". Bằng chứng ĐỘC LẬP, mới hơn `VR-018` (2026-09-21).

## Tiếp tục ở phiên sau

Xem bảng "4 đơn seed còn sống" ở cuối `coverage/coverage-DLV.md` — 4 đơn `SEED-DLV-VR020-01..04` đã tạo,
dùng lại được ngay (khỏi tốn 4 lượt seed NEED+accept mới) — nhưng **soát lại trạng thái thật của cả 4
đơn trước** (2 đơn nghi ngờ chưa chắc `IN_TRANSIT`). Việc còn nợ lớn: 13 TC cùng nhóm với `TC-DLV-043`
(nên thử verify riêng từng cái nếu muốn có verdict chính thức, hoặc chờ QC xác nhận build trước); nhóm
RESCHEDULED/RETURNING (`TC-DLV-031..036`, `072`, `073`) — nên kiểm tra nhánh "Không thể liên lạc được"
TRƯỚC trên 1 đơn sẵn có, trước khi seed thêm.
