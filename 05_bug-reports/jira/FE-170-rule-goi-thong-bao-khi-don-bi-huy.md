# FE-170 — [TC_03 - Thông báo ]: Rule gởi thông báo khi đơn bị hủy không đúng 

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-170 · **Module:** NTF · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-170 |
| Module | NTF |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-09 |
| Verify Date | 2026-08-09 |
| Done At | 2026-08-09 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 2 |
| Due date | 2026-08-06 |
| Reporter | AnhDC4 |
| Assignee | HungHT32 |
| Created | 2026-08-05 |
| Updated | 2026-08-09 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**Điều kiện test:** Đơn đã ghép

**Bước thực hiện:** 

1. Người vận chuyển thao tác hủy đơn
2. Check thông báo

**> Bug:** 

- Chỉ gởi thông báo hủy cho Gởi, không gởi cho người nhận  =>phải gởi cả 2 (Gởi cho cá bên liên quan còn lại của đơn)
- Nội dung thông báo hủy không đúng brd

![attachment](d533c97d-12e1-4d3c-b1d1-56444f98abae)
