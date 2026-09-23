# FE-312 — [TC_05 - Bảng tin & Chi tiết tin] [Suggest]- Chủ tin mở tin từ Bảng tin không có Chỉnh sửa/Huỷ đơn

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-312 · **Module:** FEED · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-312 |
| Module | FEED |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Suggest (weight 0) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Interface |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date |  |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-21 |
| Updated | 2026-09-21 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: CBNV `Đặng Châu Giang` (`stag_giangdc2@`) — vai người gửi (chủ tin)
- Trình duyệt / Thiết bị: emulator-5554 (Android 15, 1080×2400), UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Tài khoản A (chủ tin) đã đăng 1 tin NEED, đang ở trạng thái "Chờ ghép" (chưa có người vận chuyển nhận).

**Steps:**

1. Đăng nhập app FoxPro bằng tài khoản A → menu "Chức năng" → nhấn icon FoxEco
2. Cách 1: từ Trang chủ (mục "Đơn của tôi") hoặc tab "Hoạt động" → bấm vào tin vừa đăng → quan sát màn hình mở ra
3. Quay lại → chọn tab "Bảng tin" → tìm card tin của mình (có badge "Tin của bạn") → bấm vào → quan sát màn hình mở ra

**Expected result:**

- Cùng 1 tin, cùng trạng thái "Chờ ghép", dù vào từ Trang chủ, Hoạt động hay Bảng tin thì đều mở **cùng 1 màn hình**: màn "Theo dõi đơn" với nút **"Chỉnh sửa"** và **"Huỷ đơn"**, để chủ tin thao tác thuận tiện. _(Theo QC: người dùng cần thấy Chỉnh sửa/Huỷ đơn ngay khi mở tin của mình; cùng một trạng thái thì các nguồn vào khác nhau nên nhất quán.)_
- _Ghi chú: PRD v1.1 không quy định rõ hành vi này — sơ đồ điều hướng §7.1 (trang 30) tách_ `Bảng tin → Chi tiết tin` _và_ `Đơn hàng → Theo dõi đơn`_;_ `AC-12.2.01` _(trang 20) chỉ nói mở tin của chính mình thì không có nút "Tôi mang giúp được"._

**Actual result:**

- Từ Trang chủ / Hoạt động → mở **"Theo dõi đơn"**: có stepper "Chờ ghép", dòng "Đang chờ người vận chuyển nhận đơn" và nút **"Chỉnh sửa"**, **"Huỷ đơn"**.
- Từ Bảng tin → mở **"Chi tiết tin"**: chỉ xem (ảnh, thông tin hàng, lộ trình, khung giờ, người gửi), **không có** "Chỉnh sửa", **không có** "Huỷ đơn", không có nút nào.
- ⇒ Chủ tin muốn sửa/huỷ phải thoát ra và tìm lại tin ở Hoạt động; cùng 1 tin nhưng khác nguồn vào lại ra 2 màn khác nhau.
- _(Trang chủ: theo QC báo; đã tự xác nhận đường Hoạt động cùng nguồn "Đơn của tôi".)_

**Hình ảnh mô tả:** xem 3 file đính kèm trên issue — `_recon__hoat-dong-mo-theo-doi-don-co-chinh-sua-huy-don.png` (Theo dõi đơn có Chỉnh sửa/Huỷ đơn) · `_recon__bang-tin-tin-cua-ban-co-badge.png` (card có badge "Tin của bạn") · `_recon__bang-tin-mo-chi-tiet-tin-khong-co-chinh-sua-huy-don.png` (Chi tiết tin, không có nút).
