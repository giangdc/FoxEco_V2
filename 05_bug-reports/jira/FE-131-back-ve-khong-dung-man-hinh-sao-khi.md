# FE-131 — [TC_04 - Đăng tin- Tạo mới/Chỉnh sửa]: Back về không đúng màn hình sao khi đăng tin thành công -> thao tác back trên device

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-131 · **Module:** ORD · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-131 |
| Module | ORD |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-07 |
| Verify Date | 2026-08-08 |
| Done At | 2026-08-07 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Interface |
| Platform | Android - Not use |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 2 |
| Due date | 2026-08-04 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-08-03 |
| Updated | 2026-08-08 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

Thiết bị: Xiaomi redmid note 12T , android 15

**Tại màn hình tạo mới/Chỉnh sửa** - 

1. Nhập data hợp lệ → điều hướng đến popup đăng tin thành công
2. Thao tác back trên device (= phím cứng, tùy device )

**Actual:** Back về màn hình trước đó(màn trước khi submit tin) và cho phép tạo nhiều đơn trùng thông tin

==> Cần chôt lại chỗ case này sẽ back về màn hình nào->or chặn thao tác back

![attachment](3e7fd664-0a3f-4552-b074-6ec8becc235d)
