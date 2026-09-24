# FE-329 — [TC_08 - Thông báo]- Nội dung thông báo khi giao cho người được ủy quyền không đúng 

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-329 · **Module:** NTF · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-329 |
| Module | NTF |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-09-23 |
| Verify Date | 2026-09-24 |
| Done At | 2026-09-23 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Medium (weight 5) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Interface |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 1 |
| Due date | 2026-09-22 |
| Reporter | GiangDC2 |
| Assignee | HungHT32 |
| Created | 2026-09-22 |
| Updated | 2026-09-24 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

* URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
* Account/Role: A người gửi `stag_anhdc4@`
* Trình duyệt / Thiết bị: emulator-5554 (Android), UiAutomator2
* Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

* Thao tác giao cho người được ủy quyền thành công

**Steps:**

1. Đăng nhập tài khoản người nhận, nhấn icon chuông, check nội dung thông báo về đơn đó.
2. Đăng nhập tài khoản người gửi, nhấn icon chuông, check nội dung thông báo về đơn đó.

**Actual result:** Thông báo không đúng prd (tham khảo ảnh đính kèm).

**Bug tương tự cho NTF-11,  NTF-12, NTF-13, NTF-14, NTF-15**

![](blob:https://media.staging.atl-paas.net/?type=file&localId=8bf3d010bf05&id=c94fa3e4-98b4-40ec-a79c-c19cac43e85b&&collection=&height=792&occurrenceKey=null&width=617&__contextId=null&__displayType=null&__external=false&__fileMimeType=null&__fileName=null&__fileSize=null&__mediaTraceId=null&url=null)
