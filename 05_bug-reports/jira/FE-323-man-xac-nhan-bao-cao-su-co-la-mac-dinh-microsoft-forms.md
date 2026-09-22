# FE-323 — [TC_10 - Trust & Safety] - Màn xác nhận sau khi gửi báo cáo sự cố là mặc định Microsoft Forms, không đúng đặc tả

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-323 · **Module:** TS · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-323 |
| Module | TS |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Low |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Requirement |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date |  |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-22 |
| Updated | 2026-09-22 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: `stag_anhptm17@fpt.com` — vai B (carrier), đơn `SEED-TS-01` đang `IN_TRANSIT`
- Trình duyệt / Thiết bị: `R58T20PLP8K` (Android thật), WebView Microsoft Forms trong Custom Tab
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Đơn `SEED-TS-01` đang `IN_TRANSIT`. WebView "Báo cáo sự cố" đã bypass được màn đăng nhập Microsoft (dùng tài khoản Microsoft 365 thật, xem `BUG-037`).

**Steps:**

1. Mở "Báo cáo sự cố" từ màn Theo dõi đơn.
2. Chọn Loại yêu cầu "Sự cố đơn hàng", nhập Mô tả chi tiết, đính 2 ảnh, nhập SĐT liên hệ lại hợp lệ.
3. Nhấn "Gửi".
4. Quan sát màn hiển thị ngay sau khi gửi thành công.

**Expected result:**

- Màn hiển thị "Đã ghi nhận phản hồi" kèm đúng câu "Đội hỗ trợ FoxEco sẽ liên hệ lại số [SĐT] trong vòng 24 giờ làm việc" và nút "Quay lại đơn hàng" (theo `SC-TS-008`/`AC-31.1.01`).
- ![attachment](edfc9833-e3d3-48e7-aebb-6620424e2678)

**Actual result:**

- Màn hiển thị là màn xác nhận mặc định của Microsoft Forms: "Đã gửi phản hồi của bạn." + nút "Lưu câu trả lời của tôi" + link "Gửi phản hồi khác" + thẻ quảng cáo "Microsoft Forms — Hãy chuẩn bị cho lời mời sự kiện của riêng bạn!". Hoàn toàn không có cam kết "24 giờ làm việc" và không có nút "Quay lại đơn hàng" — muốn thoát phải dùng nút "←" (native header, không phải nút app-branded).

**Ghi chú:** Clarification `C-TS-03(d)` (Resolved 2026-09-17) từng kết luận màn này do APP vẽ, dựa trên quan sát demo/phân tích trước khi từng đăng nhập qua được màn Microsoft. Nay có bằng chứng thật (đã submit thành công) cho thấy kết luận đó sai — cần `/analyze-requirements --update` mở lại `C-TS-03(d)` trước khi quyết định đây là lỗi cần Dev sửa hay là spec cần cập nhật theo hành vi thật của nền tảng Microsoft Forms (form bên thứ ba, có thể không tuỳ biến được màn xác nhận).
