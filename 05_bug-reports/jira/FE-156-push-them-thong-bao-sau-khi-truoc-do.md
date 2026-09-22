# FE-156 — [TC_03 - Thông báo]: push thêm thông báo sau khi trước đó đã gởi 5 tin -> có 1 tin Xác nhận

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-156 · **Module:** NTF · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-156 |
| Module | NTF |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-05 |
| Verify Date | 2026-08-08 |
| Done At | 2026-08-05 |
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
| Due date | 2026-08-05 |
| Reporter | GiangDC2 |
| Assignee | HungHT32 |
| Created | 2026-08-04 |
| Updated | 2026-08-08 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

Điều kiện test: đã gởi  5 thông báo tìm thấy đơn hàng phù hợp

1. Người đăng tin tôi nhận giao hàng Vào màn hình thông báo 
2. Click vào thông báo khớp tuyến đường bất kỳ 
3. Xác nhận Tôi mang giúp được 
4. Check lại màn hình thông báo

Actual: Nhận thêm thông báo đơn hàng phù hợp sau khi xác nhận tại b3

==> BA confim trước đó đã gởi 5 tin rồi thì không gởi thêm thông báo nữa

(trong Video đã nhận 1 tin → push thêm 1 tin trên đầu)

![attachment](1153a708-b691-4025-9cd9-2182f3123076)
