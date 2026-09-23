# FE-139 — [TC_06 - Bảng tin & Chi tiết tin - Bảng tin] Danh sách không tự refresh sau khi đơn hàng đã được ghép

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-139 · **Module:** FEED · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-139 |
| Module | FEED |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-08 |
| Verify Date | 2026-08-09 |
| Done At | 2026-08-08 |
| Fix Version | V1.0 |
| Priority | Low |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Data |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 1 |
| Due date | 2026-08-04 |
| Reporter | AnhDC4 |
| Assignee | Tuanvm37 |
| Created | 2026-08-04 |
| Updated | 2026-08-09 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

1. 2 account cùng mở màn hình Danh sách Bảng tin
2. Check account 1 ghép đơn thành công → **Bug: back về màn hình Danh sách không mất khỏi Bảng tin**
3. Check account 2 tiếp tục nhấn vào đơn hàng account 1 vừa ghép thành công → **Bug:  Treo loading và thông báo không có quyền thực hiện thao tác → Back về danh sách đơn không mất khỏi Bảng tin**

=> **Expected**: Danh sách đơn ở bảng tin tự clear đơn hàng đã ghép, không cần user refresh thủ công

**Evidence**:

![attachment](c6bf063e-262d-4d0b-8a0b-ba1ea628fa77)
![attachment](adef7e30-34b5-4522-a8d4-a04940250a6d)
