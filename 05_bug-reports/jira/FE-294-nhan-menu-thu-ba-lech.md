# FE-294 — [TC_11 - Tài khoản & Hồ sơ] - Nhãn mục menu thứ 3 lệch tài liệu, không nhất quán tiêu đề màn đích

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-294 · **Module:** USR · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-294 |
| Module | USR |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
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
| Due date |  |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-18 |
| Updated | 2026-09-18 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (mobile app, không phải web)
- Account/Role: FOXECO_STG_USER_A — Đặng Châu Giang, MNV 00131946, Ban Giám đốc
- Trình duyệt / Thiết bị: emulator-5554, Pixel 7 AVD, 1080x2400, UiAutomator2
- Build/Version: STG · v1.1

**II. Mô tả Bug**

**Pre-condition:** Đã đăng nhập FoxEco, đang ở tab "Cá nhân".

**Steps:**

1. Xem nhãn mục menu thứ 3 (nằm ngay dưới "Quà đã nhận")

**Expected result:**

- Nhãn = "Cập nhật thông tin" (theo `DOC-v1.1-01 §8.15`)

**Actual result:**

- Nhãn = "Cập nhật thông tin cá nhân" (thừa 2 chữ "cá nhân")
- Vị trí (ngay dưới "Quà đã nhận") đúng
- ⚠️ App tự mâu thuẫn: tiêu đề của màn đích lại đúng verbatim là "Cập nhật thông tin"

**Hình ảnh mô tả:** đính kèm ảnh evidence (TC-USR-013) theo attachment của issue này.
