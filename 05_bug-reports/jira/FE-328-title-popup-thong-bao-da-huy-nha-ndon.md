# FE-328 — [TC_03 - Huỷ đơn]- Title popup thông báo Đã hủy nhận đơn không đúng bị hiển thị trên 2 dòng

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-328 · **Module:** CNL · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-328 |
| Module | CNL |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Interface |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date |  |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-22 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

* Account/Role: A người gửi `stag_anhdc4@`
* Trình duyệt / Thiết bị: emulator-5554 (Android), UiAutomator2
* Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

* Đơn ở trạng thái "Chờ ghép", đang mở popup "Huỷ đơn".

**Steps:**

1. Nhập "abssssssscd" vào ô lý do huỷ.
2. Check trạng thái nút "Xác nhận" và vùng dưới ô lý do.
3. Check hiển thị dữ liệu trên popup Đã hủy 

**Expected result:**

* Hiển thị : Title ngắn nên nằm trên cùng 1 dòng 

**Actual result:**

* Hiển thị title Đã hủy (nằm trên 2 dòng )

![](blob:https://media.staging.atl-paas.net/?type=file&localId=38fe93835eb6&id=b535ae70-493c-4364-badc-18a582b01536&&collection=&height=433&occurrenceKey=null&width=581&__contextId=null&__displayType=null&__external=false&__fileMimeType=null&__fileName=null&__fileSize=null&__mediaTraceId=null&url=null)
