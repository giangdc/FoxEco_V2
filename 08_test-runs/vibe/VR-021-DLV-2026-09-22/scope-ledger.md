# Scope Ledger — VR-021 — module DLV — SCOPE_TOTAL = 81 TC

> Seed từ: `coverage/coverage-DLV.md` (trạng thái trước phiên: có verdict 20/81)
> Tập chạy phiên này: chỉ TC v1.1 còn nợ (`TC-DLV-031..081`, loại trừ CARRIED v1.0), tiếp nối VR-020, theo yêu cầu user.
> Chi tiết đầy đủ 81 dòng (kể cả TC không chạm trong phiên này): xem `coverage/coverage-DLV.md` — file này chỉ liệt kê phần **phiên này thực sự làm**, tránh lặp lại nguyên bảng.

## Việc đã làm trong phiên

1. Resume session mobile trên thiết bị thật `R58T20PLP8K` (tiếp nối app đang mở từ VR-020, vai B đứng ở đơn `IN_TRANSIT` cũ).
2. **`TC-DLV-050`**: kiểm tra nút/link "Không thể liên lạc cho người nhận?" — không tìm thấy ở màn Theo dõi đơn chính lẫn trong popup xác nhận giao hàng → `BLOCKED`. Bấm Huỷ ở popup để không tiêu đơn `IN_TRANSIT` cũ.
3. Đăng nhập A (`stag_giangdc2@fpt.com`) — đăng 2 tin NEED mới (`SEED-DLV-VR021-01/02`), người nhận C (`stag_taipm@fpt.com`), cùng tuyến `363 Nguyễn Hữu Thọ, Cẩm Lệ` → `Tòa V-City, Lê Thái Tổ`.
4. Đăng nhập B (`stag_anhptm17@fpt.com`) — nhận cả 2 đơn qua Bảng tin → Chi tiết tin → "Tôi mang giúp được".
5. **`TC-DLV-041`**: xác nhận lấy hàng đơn `SEED-DLV-VR021-01`, đính 1 ảnh JPG (chụp bằng camera in-app ở màn "Xác nhận đã lấy hàng" — màn này trước đây chưa harvest kỹ, phát hiện đính chính `RISK-DLV-11`) → `PASS`.
6. **`TC-DLV-042`**: xác nhận lấy hàng đơn `SEED-DLV-VR021-02`, KHÔNG đính ảnh nào → `PASS` (0 ảnh là biên dưới hợp lệ, không lỗi).

## Verdict cuối phiên

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|-------------------|
| TC-DLV-050 | 🚫 BLOCKED | 1 | run này | `TC-DLV-050__step2-BLOCKED-khong-co-nut-khong-lien-lac-duoc.png` |
| TC-DLV-041 | ✅ PASS | 1 | run này | `TC-DLV-041__verify-lich-su-co-anh-bang-chung.png` |
| TC-DLV-042 | ✅ PASS | 1 | run này | `TC-DLV-042__verify-xac-nhan-thanh-cong-khong-loi.png` |
| TC-DLV-031..039, 051..056, 058..067 (trừ 057/067 Deferred), 072..073 (~30 TC) | ⏳ NOT_RUN | — | — | **Nghi vấn cascade từ cùng root cause với `TC-DLV-050`** (luồng "không liên lạc được" không tồn tại trên build STG) — chưa verify riêng từng TC, giữ nguyên `NOT_RUN` theo đúng nguyên tắc "không tự gán verdict thiếu evidence" (đã áp dụng ở VR-020 cho family `TC-DLV-044..053`/`069..071`). Xem `coverage-DLV.md` ghi chú BLOCKER hợp nhất VR-020+VR-021 |
| Tất cả TC v1.1 khác chưa chạm (040, 054..057, 067, 077, 079) | ⏳ NOT_RUN | — | — | Chưa tới lượt / cần dev hỗ trợ lùi timestamp (040/057/067) — phiên dừng theo yêu cầu user sau khi có phát hiện blocker lớn |

## Quyết định dừng phiên

Sau khi xác nhận `TC-DLV-050` BLOCKED (cùng nguyên nhân nghi vấn với `TC-DLV-043` của VR-020) — ước tính **cascade tới ~30 TC còn lại** của family "không liên lạc được"/RESCHEDULED/RETURNING/RETURNED — quyết định **không** tiếp tục chạy thử từng TC trong family này (sẽ nhiều khả năng cùng BLOCKED, tốn context mà không tạo thêm thông tin mới), thay vào đó hoàn thành 2 TC độc lập còn pending không phụ thuộc blocker (`TC-DLV-041`/`042` — luồng lấy hàng) rồi dừng sạch, báo cáo đầy đủ cho QC quyết định hướng tiếp theo (xác nhận build với dev trước khi retry family bị nghi blocked).

## Tiếp tục ở phiên sau

- **Việc cần QC/dev xác nhận trước:** build STG có thiếu 2 tính năng FR07 (giao cho X loại đối tượng) VÀ FR09 (không liên lạc được) hay không — cả 2 đều không tìm thấy entry point sau khi kiểm kỹ (VR-020 + VR-021). Nếu xác nhận thiếu thật → cân nhắc log 1 bug chung (không phải theo từng TC) hoặc chờ build mới.
- Nếu build đã có 2 tính năng này ở lần sau → chạy lại `TC-DLV-043` + `TC-DLV-050` trước để xác nhận, rồi mở khoá toàn bộ family còn lại theo lô.
- TC còn pending không phụ thuộc blocker: `TC-DLV-040` (cần dev lùi timestamp), `077`/`079` (phụ thuộc màn "Xác nhận đã giao" mở rộng — CŨNG thuộc family FR07, khác giả định trước đó ở VR-021 lúc lên kế hoạch — xem đính chính trong `vibe-report.md`).

## 🆕 Follow-up 2026-09-22 — đính chính (QC chỉ ra trực tiếp)

| TC ID | Verdict cũ | Verdict mới | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|-----------|-------------|----|---------------|-------------------|
| TC-DLV-043 | 🚫 BLOCKED (VR-020) | ✅ PASS | follow-up | run này | `TC-DLV-043__verify-lich-su-giao-tan-tay.png` |
| TC-DLV-050 | 🚫 BLOCKED (VR-021, section trên) | ✅ PASS | follow-up | run này | `TC-DLV-050__verify-man-lien-he-nguoi-gui.png` |

Nguyên nhân sai + chi tiết retest: xem `vibe-log.md` mục "🆕 Follow-up — đính chính BLOCKER". Family
`044..053`/`069..071`/`031..039`/`051..056`/`058..067`/`072..073` (~40 TC) **không còn nghi cascade** —
verdict vẫn `⏳ NOT_RUN` (chưa test thật) nhưng lý do "chung blocker" trong `coverage-DLV.md` đã lỗi thời.
