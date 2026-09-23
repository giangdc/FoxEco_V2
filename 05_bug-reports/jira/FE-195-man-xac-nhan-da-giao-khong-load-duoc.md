# FE-195 — [TC_07 - Theo dõi đơn] Màn Xác nhận đã giao _ không load được thông tin nguồi nhận/địa chỉ giao --> không hoàn tất được đơn

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-195 · **Module:** DLV · **Sync:** 2026-09-23 (R2)

| Field | Value |
|-------|-------|
| Key | FE-195 |
| Module | DLV |
| Status | Pending |
| Resolution | Fixed |
| Resolved | 2026-08-09 |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | High |
| Severity | Major (weight 10) |
| Test Round | R2 |
| Effect | Functionality |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 1 |
| Due date | 2026-08-09 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-08-09 |
| Updated | 2026-08-09 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**Điều kiện test:**

-  có > 1 đơn tôi cần gởi hàng
- account test: stag_giangdc2@fpt.com

1. Người nhận tạo tin tôi nhận giao hàng phù hợp (> 2 tin khớp)
2. Đông ý ghép thành công
3. Xác nhận đã lấy hàng 
4. Xác nhận Đã giao hàng 
5. Thao tác trên màn hinh Xác nhận đã giao 

Actual: Không load thông tin người nhận + địa chỉ giao → Không xác nhận được. → Không hoàn tất được đơn

![attachment](e8fe6531-670f-48d5-978b-260acb53dfb6)
