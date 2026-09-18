# [TC_11 - Tài khoản & Hồ sơ] - Thiếu icon khiên cạnh field Email công ty

- **Jira:** [FE-295](https://foxproject.atlassian.net/browse/FE-295)
- **Project:** FE (Fox Eco) · **Parent:** FE-1
- **Assignee:** Tuanvm37
- **Priority:** Low · **Severity:** 2 · **Test Round:** 1 · **Platform:** App · **Effect:** Usability · **Defect Type:** Interface · **Fix version:** V1.0
- **Status:** To Do
- **Labels:** bug-005, tc-usr-024
- **Module:** USR (Tài khoản & Hồ sơ) · **Màn:** Cập nhật thông tin
- **Môi trường:** STG · Platform test: mobile (Appium MCP / UiAutomator2), Pixel 7 AVD 1080x2400
- **Test case liên quan:** TC-USR-024
- **Nguồn:** Vibe Test `VR-001-USR-2026-09-18` (`08_test-runs/vibe/VR-001-USR-2026-09-18/vibe-report.md`, ứng viên bug **B8**)
- **Evidence:** ✅ đã đính kèm trên Jira (verify 2026-09-18 15:20 qua `getJiraIssue` → 1 attachment thật) — `TC-USR-024__step8-FAIL-thieu-icon-khien-email.png` (id `31505`)
- **ID local:** `BUG-005` (draft cũ đã chuyển sang `jira/`, xem `bug-index.md`)

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
