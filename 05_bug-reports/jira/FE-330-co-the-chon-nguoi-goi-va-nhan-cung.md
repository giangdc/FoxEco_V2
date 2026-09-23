# FE-330 — [TC_09 - Đăng tin]- Có thể chọn người gởi và nhận cùng email 

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-330 · **Module:** ORD · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-330 |
| Module | ORD |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-09-23 |
| Verify Date | 2026-09-23 |
| Done At | 2026-09-23 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date | 2026-09-23 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-22 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: A người gửi `stag_anhbptm17@`
- Trình duyệt / Thiết bị: note 12t pro, andorid 15
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Điều hướng đến bước 2 Địa điểm và thời gian

**Steps:**

1. Nhập người gởi và người nhận trùng thông tin email
2.  Nhập các thông tin bắt buộc khác 
3. Tap Tiếp theo 
4. Nhập thông tin bắt buộc 
5. Tap Đăng tin ngay 

**Actual result:** Có thể đang tin thành công, vào màn hình chi tiết hiển các btn của cả 2 role → cần chặn chỗ này vì ko hợp lý

![attachment](e310daaa-c51e-4b04-a834-77473984ef6e)
