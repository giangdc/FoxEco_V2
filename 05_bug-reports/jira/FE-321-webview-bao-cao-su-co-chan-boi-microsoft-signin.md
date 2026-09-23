# FE-321 — [TC_10 - Trust & Safety] - Form Báo cáo sự cố bắt buộc đăng nhập Microsoft (do có trường tải file) — đề xuất bỏ bắt buộc đăng nhập

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-321 · **Module:** TS · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-321 |
| Module | TS |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Low |
| Severity | Suggest (weight 0) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Other |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date |  |
| Reporter | GiangDC2 |
| Assignee | LinhDCC |
| Created | 2026-09-22 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: đã thử cả 3 vai — `stag_giangdc2@` (A/người gửi), `stag_anhptm17@` (B/người vận chuyển), `stag_taipm@` (C/người nhận) — cùng 1 đơn `SEED-TS-01`
- Trình duyệt / Thiết bị: `emulator-5554` (Android) + `R58T20PLP8K` (Android thật, WiFi), UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả**

**Pre-condition:**

- Đơn `SEED-TS-01` đã tồn tại ở các trạng thái `Chờ ghép` / `Đã ghép` / `Đang giao`.
- Mạng thiết bị hoạt động bình thường (WiFi thật, đã xác nhận internet OK).

**Steps:**

1. Mở màn "Theo dõi đơn" của đơn `SEED-TS-01` (thử ở cả 3 trạng thái, cả 3 vai).
2. Nhấn nút "Báo cáo sự cố" ở góc trên bên phải.
3. Đợi WebView tải xong (10–20 giây).
4. Quan sát nội dung hiển thị trong WebView.

**Actual (đã xác nhận nguyên nhân với Dev):**

- WebView luôn dừng ở màn đăng nhập Microsoft ("Microsoft — Đăng nhập — Email hoặc điện thoại") trước khi vào được form thật — tái hiện 100% (nhiều lần, cả 2 thiết bị, cả 3 tài khoản, cả 3 trạng thái đơn). Test account STG (`stag_*@fpt.com`) không có tài khoản Microsoft/Azure AD tương ứng ⇒ không vượt qua được màn này bằng tài khoản test, nên 13/17 TC v1.1 của module TS không kiểm được nội dung form thật (`TC-TS-008/009/010/011/012/013/014/015/017/019/020/021/024`).
- Dev đã xác nhận nguyên nhân: form có trường "Hình ảnh đính kèm" (tải file) — đây là tính năng của Microsoft Forms bắt buộc người phản hồi phải đăng nhập tài khoản Microsoft mới dùng được input tải file. Đây là giới hạn/quy định của nền tảng Microsoft Forms, không phải lỗi code phía app FoxEco.

**Đề xuất (thay cho "Expected result"):**

- **Form "Báo cáo sự cố" về bản chất là một khảo sát/báo cáo nhanh — người dùng bấm vào giữa lúc đang thao tác trên đơn hàng, kỳ vọng điền và gửi ngay, không phải một tác vụ họ chủ động dành thời gian chuẩn bị đăng nhập. Bắt đăng nhập Microsoft giữa luồng này nhiều khả năng khiến người dùng bỏ dở (rời màn ngay khi thấy màn đăng nhập lạ, không rõ dùng tài khoản nào) — làm giảm hẳn số lượng báo cáo sự cố thực nhận được, đi ngược mục tiêu ban đầu của tính năng** `FR16`.
- Đề xuất BA/Dev cân nhắc 1 trong 2 hướng để bỏ yêu cầu đăng nhập bắt buộc, ưu tiên sự tiện lợi cho người dùng cuối:

    1. Bỏ trường "Hình ảnh đính kèm" khỏi form (nếu ảnh không phải thông tin bắt buộc để xử lý sự cố) ⇒ Microsoft Forms không còn lý do đòi đăng nhập.
    2. Nếu ảnh đính kèm là bắt buộc về nghiệp vụ, đổi nền tảng form sang loại hỗ trợ tải file mà không cần đăng nhập (Google Form công khai, hoặc form tự dựng trong hệ thống nội bộ) — đúng như giả định ban đầu của tài liệu phân tích (`test_data_catalog.md` dùng chữ "Google Form").
    
- Nếu BA/Dev xác nhận giữ nguyên yêu cầu đăng nhập (đánh đổi lấy khả năng đính kèm ảnh), đề nghị ít nhất: (a) thêm 1 dòng cảnh báo trước khi mở WebView — "Bạn sẽ cần đăng nhập Microsoft để gửi báo cáo kèm ảnh" — để người dùng không bị bất ngờ giữa chừng, và (b) xác nhận `test_data_catalog.md`/`test_scenario_map.md` của TS đang mô tả sai (ghi "Google Form", ngụ ý không cần đăng nhập).
