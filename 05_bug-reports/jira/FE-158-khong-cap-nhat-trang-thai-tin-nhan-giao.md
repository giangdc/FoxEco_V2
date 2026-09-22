# FE-158 — [TC_01 - Hoạt động]: Không cập nhật trạng thái tin Nhận giao hàng khi có đơn hàng phù hợp -> đồng ý giao ->  hoàn tất đơn

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-158 · **Module:** ACT · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-158 |
| Module | ACT |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-08 |
| Verify Date | 2026-08-09 |
| Done At | 2026-08-08 |
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
| Due date | 2026-08-05 |
| Reporter | GiangDC2 |
| Assignee | HungHT32 |
| Created | 2026-08-04 |
| Updated | 2026-08-09 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**Điều kiện test:** Đã tạo tôi nhận giao hàng + có 1 tin khớp

**Bước thực hiện: **

1. Người đăng tin tôi nhận giao hàng Vào màn hình thông báo
2. Click vào thông báo khớp tuyến đường
3. Xác nhận Tôi mang giúp được →  thao tác hoàn tất đơn này 
4. Vào trang chủ check lại Tin nhân giao hàng 

Actual:  Đã ghép-> hoàn tất đơn nhưng tin Nhận giao hàng  vẫn hiện ở trang chủ/ đơn của tôi

=> Ẩn đơn hoàn tất

![attachment](634e5ff4-f59f-4fc9-a879-89d5d0104a9e)

![attachment](5ae8f88c-9cdc-4d52-abf5-0724d888c56f)
