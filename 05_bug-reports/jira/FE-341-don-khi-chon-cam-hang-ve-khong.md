# FE-341 — [TC_01- Hoạt động] - Đơn khi chọn Cầm hàng về không hiển thị tại đơn của tôi (đang ko hiển thị tại bất kỳ màn hình nào )

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-341 · **Module:** ACT · **Sync:** 2026-09-23 (R2)

| Field | Value |
|-------|-------|
| Key | FE-341 |
| Module | ACT |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Medium (weight 5) |
| Test Round | R2 |
| Effect | Functionality |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date |  |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-23 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: CBNV `stag_vunt60`— người vận chuyển
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Có đang trang thái đang giao 

**Steps:**

1. Đăng nhập app FoxPro → menu "Chức năng" → nhấn icon FoxEco
2. Nhấn tab "Hoạt động" ở thanh tab dưới, rồi nhấn tab con "Đang diễn ra"
3. Tap tin trạng thái đã giao
4. Tap đã giao cho người nhận > xác nhận 
5. Tap Không thể liên lạc cho người nhận → Xử lý đơn hàng > Tap Cầm hàng về
6. Tap chọn Tôi sẽ giao lại sau/Tôi sẽ trả về cho cho người gời 
7. Nhập các thông tin bắt buộc và click Xác nhận xử lý 
8. Kiểm tra lại tin vừa thao tác tại màn hình Đơn của tôi  

**Expected result:**

- Vân hiển thị và load đúng thông tin với trạng thái này 

**Actual result:**

- Đơn không còn hiển thị lại bất kỳ đâu trên app nữa 

![attachment](e464b55d-f647-4f99-b426-6f0dbfebd482)
