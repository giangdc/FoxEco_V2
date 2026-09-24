# FE-143 — [TC_03 - Thông báo ]: Hiện lại chấp đỏ tại tin đã đọc sau khi reload màn hình thông báo

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-143 · **Module:** NTF · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-143 |
| Module | NTF |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-06 |
| Verify Date | 2026-08-07 |
| Done At | 2026-08-06 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date | 2026-08-05 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-08-04 |
| Updated | 2026-08-07 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

Điều kiện test:

* Còn thông báo chưa đọc

**Tại màn hình thông báo** 

1. Tap vào thông báo chưa đọc
2. Back lại màn thông báo 
3. Thao tác reload màn hình thông báo 
4. Check lại icon chấm đỏ tại tin đã đọc

Actual: Tin đã đọc tại bước 1 hiện lại icon chấm đỏ

![](blob:https://media.staging.atl-paas.net/?type=file&localId=43eb153ac64a&id=79086585-1ba7-4c47-83ff-23d24882b868&&collection=&height=null&occurrenceKey=null&width=null&__contextId=null&__displayType=null&__external=false&__fileMimeType=null&__fileName=null&__fileSize=null&__mediaTraceId=null&url=null)
