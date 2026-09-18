# [TC_11 - Tài khoản & Hồ sơ] - Nhãn mục menu thứ 3 lệch tài liệu, không nhất quán tiêu đề màn đích

- **Jira:** [FE-294](https://foxproject.atlassian.net/browse/FE-294)
- **Project:** FE (Fox Eco) · **Parent:** FE-1
- **Assignee:** Tuanvm37
- **Priority:** Low · **Severity:** 2 · **Test Round:** 1 · **Platform:** App · **Effect:** Usability · **Defect Type:** Requirement · **Fix version:** V1.0
- **Status:** To Do
- **Labels:** bug-004, tc-usr-013
- **Module:** USR (Tài khoản & Hồ sơ) · **Màn:** Cá nhân
- **Môi trường:** STG · Platform test: mobile (Appium MCP / UiAutomator2), Pixel 7 AVD 1080x2400
- **Test case liên quan:** TC-USR-013
- **Nguồn:** Vibe Test `VR-001-USR-2026-09-18` (`08_test-runs/vibe/VR-001-USR-2026-09-18/vibe-report.md`, ứng viên bug **B7**)
- **Evidence:** ✅ đã đính kèm trên Jira (verify 2026-09-18 15:20 qua `getJiraIssue` → 1 attachment thật) — `TC-USR-013__step3-FAIL-nhan-menu-thu-ba.png` (id `31504`)
- **ID local:** `BUG-004` (draft cũ đã chuyển sang `jira/`, xem `bug-index.md`)

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
