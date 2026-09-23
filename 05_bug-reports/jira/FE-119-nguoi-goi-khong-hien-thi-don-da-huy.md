# FE-119 — [TC_01 - Hoạt động(Đơn của tôi)]: Người gởi Không hiển thị đơn đã hủy tại màn hình Đơn của tôi

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-119 · **Module:** ACT · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-119 |
| Module | ACT |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-06 |
| Verify Date | 2026-08-08 |
| Done At | 2026-08-06 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Data |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date | 2026-08-04 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-08-03 |
| Updated | 2026-08-08 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**Tại màn hình Đơn của tôi**

1. Người gởi tap vào tab Đang diễn ra 
2. Tap vào đơn bất kỳ người gởi đã tạo 
3. Thao tác hủy thành công 

**Actual:** 

- Sau khi hủy thành công quay lại màn tab đang diên ra nhưng không tự động reload lại data → tự động reload và cập nhật lại trạng thái mới nhất
- sau khi reload thì người gởi không hiển thị đơn trạng thái hủy tại tab Đang diễn ra (người nhận thì có hiển thị đơn trạng thái hủy) → link demo case này có hiển thi

![attachment](b54ed501-3415-4094-9e28-2a7afc516d00)
‌

![attachment](4f23d4d9-78b5-4181-a069-69e2f8575511)
