# FE-105 — [TC_04 - Đăng tin - Tôi nhận giao hàng]: Kiểm tra thời gian khởi hành < đến nơi khi chọn Từ ngày khác Đến ngày

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-105 · **Module:** ORD · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-105 |
| Module | ORD |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-06 |
| Verify Date | 2026-08-07 |
| Done At | 2026-08-06 |
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
| Due date | 2026-08-04 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-08-03 |
| Updated | 2026-08-07 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**Step:**

**Tại màn hình đăng tin Tôi nhận giao hàng**

1. Chọn  từ ngày là ngày 3 
2. Chọn đến ngày khác ngày 3 (ngày 4/5/6)
3. Chọn thời gian Đến nơi > khởi hành 

**Actual:** Hiển thị thông báo Giờ đến phải lớn hơn <khởi hành>

==> Từ ngày/đến ngày khác nhau nên ko check điều kiện này 

![](blob:https://media.staging.atl-paas.net/?type=file&localId=e33f194dc878&id=1a17b9ad-16a3-480c-9ade-cecab0528a33&&collection=&height=636&occurrenceKey=null&width=814&__contextId=null&__displayType=null&__external=false&__fileMimeType=null&__fileName=null&__fileSize=null&__mediaTraceId=null&url=null)
