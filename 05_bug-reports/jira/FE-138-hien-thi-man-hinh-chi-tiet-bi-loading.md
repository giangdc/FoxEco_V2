# FE-138 — [TC_03 - Thông báo ]: Hiển thị màn hình chi tiết bị loading + thông báo "bạn không có quyền thực hiên thao tác này" khi click vào thông báo tìm thấy tuyến đường phù hợp-trường hợp đơn đã hủy

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-138 · **Module:** NTF · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-138 |
| Module | NTF |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-09 |
| Verify Date | 2026-08-09 |
| Done At | 2026-08-09 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Medium (weight 5) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 2 |
| Due date | 2026-08-05 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-08-04 |
| Updated | 2026-08-09 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

Điều kiện test: 

- Account A tạo tin Tôi nhận giao hàng thành công 
- Account B tạo tin Tôi cần gởi hàng khớp với account A → khi này account B nhận thông báo tuyến đường phù hợp
- Account A hủy đơn đã tạo đi

**Tại màn hình thông báo - account B**

1. Tap vào thông báo tuyến đường phù hợp

Actual: Hiển thị màn hình chi tiết bị loading kèm thông báo "bạn không có quyền thực hiên thao tác này" 

=>Chỗ này brd ko miêu tả hành vi cụ thế, nếu chốt giữ thông báo như hiện tại cần fix chỗ loading

![attachment](b46efc82-3fab-4a2a-aab2-5497b351eed1)
