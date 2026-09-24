# FE-346 — [TC_04 - Giao nhận & Theo dõi đơn] - Cầm hàng về: Hệ thống tạo ra 2 đơn hàng hoàn thành và Đã gửi lại người gửi sau khi người gửi xác nhận đã nhận lại hàng

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-346 · **Module:** DLV · **Sync:** 2026-09-24 (R2)

| Field | Value |
|-------|-------|
| Key | FE-346 |
| Module | DLV |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R2 |
| Effect | Functionality |
| Defect Type | Data |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date |  |
| Reporter | anhptm17 |
| Assignee | Tuanvm37 |
| Created | 2026-09-24 |
| Updated | 2026-09-24 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

Account: [dienlt2@fpt.com](mailto:dienlt2@fpt.com)

Vai trò: Người gửi 

Step:

1. Đăng nhập bằng tài khoản A, đăng 1 tin NEED khai tài khoản C là người nhận, rồi đăng xuất. (setup)
2. Đăng nhập bằng tài khoản B, nhận đơn đó, nhấn "Tôi đã lấy hàng" và xác nhận. (setup)
3. Mở màn "Xác nhận đã giao", nhấn "Không thể liên lạc cho người nhận?", đi tiếp tới màn "Xử lý đơn hàng", nhấn "Cầm hàng về", chọn "Tôi sẽ trả về cho người gửi", nhập lịch hẹn hợp lệ và xác nhận, rồi đăng xuất. (setup)
4. Đăng nhập bằng tài khoản A, nhấn tab "Hoạt động" và mở đơn đó. (setup)
5. Nhấn "Xác nhận đã nhận lại hàng" và đồng ý ở popup xác nhận.
6. Check trạng thái đơn và tab chứa đơn. => tạo ra 2 đơn hàng hoàn thành và Đã gửi lại người gửi ở tab "Đã hoàn thành".

**=> Bug: Tạo ra 2 đơn hàng trạng thái hoàn thành và Đã gửi lại người gửi ở tab "Đã hoàn thành".**

**KQMM:Đơn chuyển sang trạng thái đã trả lại người gửi và nằm ở tab "Đã hoàn thành".**
