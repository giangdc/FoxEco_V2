# FE-333 — [TC_04 - Giao nhận & Theo dõi đơn]- Xử lý khi click btn Không thê liên lạc cho người nhận không đúng 

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-333 · **Module:** DLV · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-333 |
| Module | DLV |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
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

- Đơn có trạng thái đang giao → login acc người vận chuyển 

1. Vào màn hình Theo dõi đơn 
2. Tap Đã giao cho người nhận (Đã đến địa điểm giao hàng)
3. Tap Không thể liên lạc cho người nhận 

Actual: Hiển thị popup confirm (tham khảo đính kèm)

Expected: Mở thăng màn hình Liên hệ người gởi (link demo ) mà ko có popup nào 

![attachment](ab713a6a-630d-4ed4-9ecc-69251ded89ad)
