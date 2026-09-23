# FE-297 — [TC_11 - Tài khoản & Hồ sơ] - Mã nhân viên bị cắt, hiển thị không đầy đủ

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-297 · **Module:** USR · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-297 |
| Module | USR |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-09-23 |
| Verify Date | 2026-09-23 |
| Done At | 2026-09-23 |
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
| Due date | 2026-09-23 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-18 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (mobile app, không phải web)
- Account/Role: stag_anhptm17@fpt.com
- Trình duyệt / Thiết bị: emulator-5554, Pixel 7 AVD, 1080x2400, UiAutomator2
- Build/Version: STG · v1.1

**II. Mô tả Bug**

**Pre-condition:** Đã đăng nhập FoxEco, đang ở màn "Cập nhật thông tin".

**Steps:**

1. Vào màn "Cập nhật thông tin"
2. Quan sát dòng "Phòng ban · MNV" ngay dưới tên nhân viên

**Expected result:**

- Mã nhân viên (MNV) hiển thị đầy đủ, người dùng xem được trọn vẹn để đối chiếu/cập nhật thông tin khi cần

**Actual result:**

- QC quan sát trực tiếp: với phòng ban có tên dài, dòng "Phòng ban · MNV: xxxxxxxx" bị cắt bớt, MNV không hiển thị đủ ⇒ người dùng không xem được MNV đầy đủ

**Hình ảnh mô tả:** đính kèm file ảnh trên issue này

![attachment](c3d37182-82e3-4756-b78d-ea0c60765cba)
