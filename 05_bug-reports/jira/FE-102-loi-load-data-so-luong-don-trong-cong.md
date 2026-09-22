# FE-102 — [TC_05 - Trang chủ]: Lỗi load data số lượng đơn trong Cộng đồng không realtime

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-102 · **Module:** HOME · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-102 |
| Module | HOME |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-08 |
| Verify Date | 2026-08-08 |
| Done At | 2026-08-08 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Data |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 2 |
| Due date | 2026-08-04 |
| Reporter | anhptm17 |
| Assignee | Tuanvm37 |
| Created | 2026-08-03 |
| Updated | 2026-08-08 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**Step**

1. Truy cập trang chủ
2. Quan sát Card "Đóng góp của bạn" => load 20 đơn 
3. Click chọn đăng tin /Tôi cần gửi hàng
4. Tạo đơn hàng thành cộng → chọn quay về trang chủ 
5. Quan sát Card "Đóng góp của bạn" => load 20 đơn 
6. Click vào bảng tin → back về trang chủ 
7. Quan sát Card "Đóng góp của bạn" => load 21 đơn 

**=> Bug: Hệ thống load data số lượng đơn trong Cộng đồng không realtime**

**KQMM: Hệ thống load data realtime **

![attachment](203ed5cd-1eb5-45b8-9880-501e0537f229)
