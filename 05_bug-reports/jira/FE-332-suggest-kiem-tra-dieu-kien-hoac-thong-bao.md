# FE-332 — [TC_04 - Giao nhận & Theo dõi đơn]- suggest kiêm tra điều kiện hoặc thông báo cho người dùng khi SĐT không tồn tại zalo

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-332 · **Module:** DLV · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-332 |
| Module | DLV |
| Status | Done |
| Resolution | Won't Fix |
| Resolved | 2026-09-24 |
| Verify Date | 2026-09-24 |
| Done At | 2026-09-24 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Suggest (weight 0) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Interface |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 0 |
| Reason for Wontfix | Dev không fix do Phụ thuộc thông tin các bên liên quan ngoài ISC |
| Due date | 2026-09-23 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-22 |
| Updated | 2026-09-24 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

* URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
* Account/Role: A người vận chuyển `stag_anhdc4@`
* Trình duyệt / Thiết bị: emulator-5554 (Android), UiAutomator2
* Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

* Đơn đã ghép + SĐT chưa sử dụng zalo (account: stag_taipm)

**Steps:**

1. Vào màn hình theo dõi đơn 
2. Click icon Gọi  tại thông tin của stag_taipm

Actual: Điều hướng qua page zalo không tồn tại 

Expected: check ko đúng thì chặn ko hiển thị zalo hoặc custom lại thông báo thân thiện hơn → như thế này khi người dùng gọi sẽ không biết bị gì, sẽ nghĩ lỗi app
