# Vibe Locators — VR-014 — module HOME — 2026-09-21
> Captured via Appium MCP. ✅ Verified = MCP find + action OK trong run này.

## Màn: Trang chủ (Thủy — tài khoản sạch)
| Element | Action | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| Số đơn đã giúp (hero) | get_text | id | `home-helped-count` → `0` | ✅ | 027 028 |
| Chuỗi hero rỗng | get_text | -android uiautomator | `text(" · Chưa có đóng góp nào")` | ✅ | 028 |
| Dòng cộng đồng | get_text | -android uiautomator | `textContains("Cộng đồng FoxEco")` → `Cộng đồng FoxEco: 325 đơn · 23743 người` | ✅ | 028 |
| Nút CTA vùng hero | find | accessibility id | `Xem bảng tin gửi hàng` | ✅ | 028 |
| Section `Đơn của tôi` (rỗng) | find | -android uiautomator | `text("Đơn của tôi")` · `text("Chưa có đơn nào")` | ✅ | 027 |
| CTA `Tạo đơn gửi hàng` / chuỗi `Bạn chưa có đơn nào đang chạy` | find | -android uiautomator | `textContains(...)` | 🚫 NOT FOUND | 027 |
| Nút cuối `Tin mới` | tap | -android uiautomator | `text("Xem thêm trên Bảng tin")` | ✅ | 019 021 025 |
| Card `Bảng tin` | find | accessibility id | `feed-post-card-0` … `-6` | ✅ | 021 025 |

## 🪤 Bẫy mới
| # | Bẫy | Cách làm đúng |
|---|---|---|
| T30 | Dữ liệu STG bị **người khác đăng song song** (xuất hiện tin lạ `FTEL SG07 → FTEL SG03` giữa phiên) ⇒ số tin thay đổi giữa lúc kiểm tiền đề và lúc chạy | đo lại số tin ngay trước khi kết luận các TC về biên (`019/021/025`) |
| T31 | Card `Tin mới` ở Trang chủ có `content-desc` gộp, còn cây con đủ `TextView`; phải cuộn để card đầu không bị cắt | đếm theo cụm `Nhận:`/`Giao:` hoặc dùng ảnh chụp |
