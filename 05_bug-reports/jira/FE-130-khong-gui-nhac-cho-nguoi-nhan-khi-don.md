# FE-130 — [TC_07 - Theo dõi đơn] Không gửi nhắc cho người nhận khi đơn ở "Đã giao" quá 2 giờ mà chưa xác nhận

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-130 · **Module:** DLV · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-130 |
| Module | DLV |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-08 |
| Verify Date | 2026-08-08 |
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
| Due date | 2026-08-04 |
| Reporter | anhptm17 |
| Assignee | HungHT32 |
| Created | 2026-08-03 |
| Updated | 2026-08-08 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**Data**:

* Account: [stag_chintl12@fpt.com](mailto:stag_chintl12@fpt.com)

**Step:**

1. Đưa 1 đơn về trạng thái "Đã giao" và ghi nhận thời điểm chuyển trạng thái
2. Chờ vượt mốc 2 giờ (hoặc mock thời gian hệ thống vượt mốc này)
3. Kiểm tra danh sách thông báo của Receiver

**=> Bug: Không gửi nhắc cho người nhận khi đơn ở "Đã giao" quá 2 giờ mà chưa xác nhận**

**KQMM: Receiver nhận được thông báo nhắc xác nhận đã nhận hàng**

![](blob:https://media.staging.atl-paas.net/?type=file&localId=b3dd5f79dd0d&id=4cb0fd5c-92b2-46f7-83a5-0862adc5add2&&collection=&height=null&occurrenceKey=null&width=null&__contextId=null&__displayType=null&__external=false&__fileMimeType=null&__fileName=null&__fileSize=null&__mediaTraceId=null&url=null)
