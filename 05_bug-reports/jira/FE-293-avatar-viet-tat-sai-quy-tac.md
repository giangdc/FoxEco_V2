# [TC_11 - Tài khoản & Hồ sơ] - Avatar chữ viết tắt sai quy tắc dẫn xuất

- **Jira:** [FE-293](https://foxproject.atlassian.net/browse/FE-293)
- **Project:** FE (Fox Eco) · **Parent:** FE-1
- **Assignee:** Tuanvm37
- **Priority:** Low · **Severity:** 2 · **Test Round:** 1 · **Platform:** App · **Effect:** Usability · **Defect Type:** Logic · **Fix version:** V1.0
- **Status:** To Do
- **Labels:** bug-003, tc-usr-002
- **Module:** USR (Tài khoản & Hồ sơ) · **Màn:** Cá nhân
- **Môi trường:** STG · Platform test: mobile (Appium MCP / UiAutomator2), Pixel 7 AVD 1080x2400
- **Test case liên quan:** TC-USR-002
- **Nguồn:** Vibe Test `VR-001-USR-2026-09-18` (`08_test-runs/vibe/VR-001-USR-2026-09-18/vibe-report.md`, ứng viên bug **B6**)
- **Evidence:** ✅ đã đính kèm trên Jira (verify 2026-09-18 15:20 qua `getJiraIssue` → 1 attachment thật) — `TC-USR-002__step3-FAIL-avatar-chu-viet-tat-sai.png` (id `31503`)
- **ID local:** `BUG-003` (draft cũ đã chuyển sang `jira/`, xem `bug-index.md`)

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (mobile app, không phải web)
- Account/Role: FOXECO_STG_USER_A — Đặng Châu Giang, MNV 00131946, Ban Giám đốc
- Trình duyệt / Thiết bị: emulator-5554, Pixel 7 AVD, 1080x2400, UiAutomator2
- Build/Version: STG · v1.1

**II. Mô tả Bug**

**Pre-condition:** Đã đăng nhập FoxEco với tài khoản có tên "Đặng Châu Giang".

**Steps:**

1. Vào tab "Cá nhân"
2. Xem avatar chữ viết tắt ở đầu trang

**Expected result:**

- Avatar = chữ viết tắt của 2 từ CUỐI trong tên, không dấu, viết hoa → "Đặng Châu Giang" → `CG`

**Actual result:**

- Avatar hiện `ĐC` — sai 2 điểm cùng lúc: lấy 2 từ ĐẦU thay vì 2 từ cuối, và còn giữ dấu
- Các phần khác (tên, dòng phòng ban·MNV, vắng SĐT/email/địa chỉ) đều đúng — chỉ riêng logic tạo avatar sai
