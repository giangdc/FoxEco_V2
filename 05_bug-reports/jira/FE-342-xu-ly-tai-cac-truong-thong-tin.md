# FE-342 — [TC_04 - Giao nhận & Theo dõi đơn]- xử lý tại các trường thông tin tại luồng Cầm hàng về - chưa hợp lý

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-342 · **Module:** DLV · **Sync:** 2026-09-24 (R2)

| Field | Value |
|-------|-------|
| Key | FE-342 |
| Module | DLV |
| Status | In Progress |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R2 |
| Effect | Usability |
| Defect Type | Interface |
| Platform | Web |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 1 |
| Due date | 2026-09-24 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-23 |
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

* Điều hướng vào màn hình xử lý đơn hàng thành công 

**Steps**:

1. Tap chọn Cầm hàng về 
2. Chọn Tôi sẽ giao lại sau/Tôi sẽ trả về cho người gởi 
3. Check các trường thông tin tại block Hẹn giao lại/Hẹn trả hàng 

Actual: 

* Thời gian Từ đang = thời gian đến => mặc định nên cách nhau luôn 30p luôn 
* Nơi giao lại /Nơi nhân lại hàng: mặc định đang rỗng và nhập bất kỳ=> mặc định nên load theo địa chỉ đơn hàng đang có, và chỉ chọn trong tập data có sẵn 

![](blob:https://media.staging.atl-paas.net/?type=file&localId=c079e04258fd&id=38d5ee2d-205b-4476-a509-4d1dc640105f&&collection=&height=860&occurrenceKey=null&width=1315&__contextId=null&__displayType=null&__external=false&__fileMimeType=null&__fileName=null&__fileSize=null&__mediaTraceId=null&url=null)
