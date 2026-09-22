# FE-334 — [TC_04 - Giao nhận & Theo dõi đơn]- Không  validate SĐT tại Ngươi được ủy quyền/Quầy lễ tân/Quầy bảo vệ

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-334 · **Module:** DLV · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-334 |
| Module | DLV |
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
| Updated | 2026-09-22 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: A người vận chuyển `stag_anhdc4@`
- Trình duyệt / Thiết bị: emulator-5554 (Android), UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Đơn có trạng thái đang giao → login acc người vận chuyển

1. Vào màn hình Theo dõi đơn
2. Tap Đã giao cho người nhận (Đã đến địa điểm giao hàng)
3. Tap chọn các option Ngươi được ủy quyền/Quầy lễ tân/Quầy bảo vệ

Actual: Nhập SDT không đúng định dạng (chỉ nhập 1 số ) ->Vẫn submit được 

![attachment](3bb026df-9708-41a4-b3c4-4b29fd90cbf5)
