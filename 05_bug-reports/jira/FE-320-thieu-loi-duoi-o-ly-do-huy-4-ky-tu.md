# FE-320 — [TC_03 - Huỷ đơn][Suggest] - Thiếu dòng lỗi dưới ô lý do khi nhập 4 ký tự

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-320 · **Module:** CNL · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-320 |
| Module | CNL |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Low |
| Severity | Suggest (weight 0) |
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
| Updated | 2026-09-22 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: A người gửi `stag_anhdc4@`
- Trình duyệt / Thiết bị: emulator-5554 (Android), UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Đơn ở trạng thái "Chờ ghép", đang mở popup "Huỷ đơn".

**Steps:**

1. Nhập "abcd" (4 ký tự) vào ô lý do huỷ.
2. Check trạng thái nút "Xác nhận" và vùng dưới ô lý do.

**Expected result:**

- Nút "Xác nhận" vô hiệu hoá **ngay** (không phải bấm được rồi mới báo lỗi); **hiện lỗi ngay dưới ô lý do**; trạng thái đơn không đổi *(TC-CNL-004; PRD *`DOC-v1.1-01` `BR11-01` + `VAL-04` + `AC-25.1.03`).

**Actual result:**

- Nút "Xác nhận" đã khoá đúng (`enabled=false`) và trạng thái đơn không đổi — nhưng **không có dòng lỗi hiển thị dưới ô lý do** (page source giữa ô lý do và hàng nút không có text nào).
