# FE-295 — [TC_11 - Tài khoản & Hồ sơ] - Thiếu icon khiên cạnh field Email công ty

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-295 · **Module:** USR · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-295 |
| Module | USR |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Lowest |
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

**Pre-condition:** Đã đăng nhập FoxEco, đang ở màn "Cập nhật thông tin".

**Steps:**

1. Nhấn vào avatar, tên, dòng phòng ban·MNV, field "Email công ty" (đều là vùng chỉ đọc)
2. Quan sát icon cạnh field "Email công ty"

**Expected result:**

- Có icon khiên ở bên phải field "Email công ty" (theo rule BA chốt 2026-09-16, ngoài PRD gốc)

**Actual result:**

- Không có icon nào ở bên phải — chỉ có icon phong bì ✉ ở bên trái
- 4/4 vế còn lại của TC đều đúng — chỉ riêng icon khiên bị thiếu
- Demo `DOC-v1.1-02` cũng đang lệch điểm này — có thể cần chốt lại với BA

**Hình ảnh mô tả:** đính kèm ảnh evidence (TC-USR-024) theo attachment của issue này.

![attachment](908bef00-3b8b-49ae-81a3-9abf6f2953cf)
