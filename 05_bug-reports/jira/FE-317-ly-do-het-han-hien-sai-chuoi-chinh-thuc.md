# FE-317 — [TC_01- Hoạt động] - Lý do trên card đơn Hết hạn hiện sai chuỗi chính thức

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-317 · **Module:** ACT · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-317 |
| Module | ACT |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-09-23 |
| Verify Date | 2026-09-23 |
| Done At | 2026-09-23 |
| Fix Version | V1.0 |
| Priority | Lowest |
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
- Account/Role: CBNV `Đặng Châu Anh` (`stag_anhdc4@`) — người gửi, có nhiều tin đã hết hạn
- Trình duyệt / Thiết bị: emulator-5554 (Android), UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Tài khoản có ít nhất 1 tin đã hết hạn (không ai nhận mang giúp trong thời gian đăng).

**Steps:**

1. Đăng nhập app FoxPro → menu "Chức năng" → nhấn icon FoxEco
2. Nhấn tab "Hoạt động" ở thanh tab dưới, rồi nhấn tab con "Đã hoàn thành"
3. Quan sát badge và dòng lý do trên card đơn "Hết hạn"

**Expected result:**

- Card hiển thị badge "Hết hạn" kèm dòng lý do đúng chuỗi **"Không có ai nhận mang giúp trong thời gian đăng"** _(TC-ACT-008; PRD_ `DOC-v1.1-01` §8.5.1 BR05-03 + AC-09.1.01).

**Actual result:**

- Badge "Hết hạn" đúng, nhưng dòng lý do là **"Không có ai nhận mang giúp trong thời gian đăng — tin đã tự động đóng."** — thừa vế "— tin đã tự động đóng." so với chuỗi chính thức. Lặp lại ở **mọi** card Hết hạn trong danh sách (\~30 card).
