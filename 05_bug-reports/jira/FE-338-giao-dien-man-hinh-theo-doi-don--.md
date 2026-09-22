# FE-338 — [TC_04 - Giao nhận & Theo dõi đơn]- Giao diện màn hình Theo dõi đơn - Luồng  hẹn giao lại

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-338 · **Module:** DLV · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-338 |
| Module | DLV |
| Status | To Do |
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
- Account/Role: A người vận chuyển `stag_anhdc4@`
- Trình duyệt / Thiết bị: emulator-5554 (Android), UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Đơn đang được Hẹn giao lại

**Steps**:

1. Vào màn hình Theo dõi đơn
2. Check lại thông tin trên màn hình 

Actual: thiến block Giao lại cho người nhận, lịch sử + btn sai 

![attachment](76115a72-5a47-4b1d-9944-c37731c2965a)
