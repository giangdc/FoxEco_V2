# FE-318 — [TC_01 - Hoạt động] - Empty state tab Đang diễn ra thiếu dòng giải thích

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-318 · **Module:** ACT · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-318 |
| Module | ACT |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-09-23 |
| Verify Date | 2026-09-23 |
| Done At | 2026-09-23 |
| Fix Version | V1.0 |
| Priority | Low |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Requirement |
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
- Account/Role: CBNV `Nguyễn Đình Nhật Minh` (`stag_MinhNDN2@`) — tài khoản trắng, 0 đơn ở cả 2 tab
- Trình duyệt / Thiết bị: emulator-5554 (Android), UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Tài khoản không có đơn nào đang thực hiện (từ "Chờ ghép" đến "Đã giao").

**Steps:**

1. Đăng nhập app FoxPro bằng tài khoản không có đơn → menu "Chức năng" → nhấn icon FoxEco
2. Nhấn tab "Hoạt động" ở thanh tab dưới (mặc định mở tab con "Đang diễn ra")
3. Quan sát vùng danh sách: icon, dòng tiêu đề, dòng giải thích, số nút CTA

**Expected result:**

- Vùng danh sách hiện icon nét mảnh màu neutral, dòng tiêu đề đúng chuỗi "Không có đơn đang thực hiện", **1 dòng giải thích**, và đúng 1 nút CTA nhãn "Đăng tin gửi hàng" _(TC-ACT-012; PRD_ `DOC-v1.1-01` §8.17.1 EMP-05 + §8.17.2 BR17-01: "Mỗi empty state gồm: icon nét mảnh màu neutral + một dòng tiêu đề + một dòng giải thích + tối đa một CTA.").

**Actual result:**

- Có icon, tiêu đề "Không có đơn đang thực hiện" và đúng 1 nút "Đăng tin gửi hàng", nhưng **không có dòng giải thích** nào giữa tiêu đề và nút (page source chỉ có 2 text trong vùng danh sách).
