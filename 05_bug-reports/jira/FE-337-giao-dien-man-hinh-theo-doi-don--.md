# FE-337 — [TC_04 - Giao nhận & Theo dõi đơn]- Giao diện màn hình Theo dõi đơn - Luồng xác nhận trả hàng cho người gởi không đúng 

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-337 · **Module:** DLV · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-337 |
| Module | DLV |
| Status | In Progress |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Medium (weight 5) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 1 |
| Due date | 2026-09-23 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-22 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: A người vận chuyển `stag_anhdc4@`
- Trình duyệt / Thiết bị: emulator-5554 (Android), UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Đơn đang được người Vẫn chuyển trả về cho người gởi 

**Steps**:

1. Vào màn hình Theo dõi đơn
2. Checl thông tin lịch sử và các btn 

Actual: màu sác và thông tin lịch sử không giông ui , không có btn dưới cùng màn hình như ui 

![attachment](447edf66-0dd1-4414-88c9-379cd848f1f9)
