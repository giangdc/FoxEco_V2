# FE-115 — [TC_07 - Theo dõi đơn ]: Không hiển thị nút "✓ Xác nhận đã nhận hàng" khi đơn = "Đã giao" và login tài khoản người nhận

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-115 · **Module:** DLV · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-115 |
| Module | DLV |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-06 |
| Verify Date | 2026-08-07 |
| Done At | 2026-08-06 |
| Fix Version | V1.0 |
| Priority | High |
| Severity | Major (weight 10) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date | 2026-08-04 |
| Reporter | anhptm17 |
| Assignee | Tuanvm37 |
| Created | 2026-08-03 |
| Updated | 2026-08-07 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

Data: 

* Account: stag_Chintl12@fpt.com

Step:

1. Mở app FoxEco bằng tài khoản Người nhận (Receiver)
2. Bấm tab "Hoạt động", mở đơn cần theo dõi để vào màn "Theo dõi đơn"
3. Quan sát nút CTA ở đáy màn hình 

**=> Bug: Không hiển thị nút "✓ Xác nhận đã nhận hàng" kích hoạt (cam, bấm được) khi đơn = "Đã giao"**

**KQMM: Nút hiển thị nhãn "✓ Xác nhận đã nhận hàng" ở trạng thái kích hoạt (nền cam, bấm được) — đây là partition DUY NHẤT nút này active**

![](blob:https://media.staging.atl-paas.net/?type=file&localId=e2c8a2bb2037&id=7aa6c6b0-0a28-4187-b50e-ac36f5de9427&&collection=&height=null&occurrenceKey=null&width=null&__contextId=null&__displayType=null&__external=false&__fileMimeType=null&__fileName=null&__fileSize=null&__mediaTraceId=null&url=null)
