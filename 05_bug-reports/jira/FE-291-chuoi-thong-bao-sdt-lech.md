# [TC_11 - Tài khoản & Hồ sơ] - Chuỗi thông báo lỗi SĐT lệch chuỗi BA đã chốt

- **Jira:** [FE-291](https://foxproject.atlassian.net/browse/FE-291)
- **Project:** FE (Fox Eco) · **Parent:** FE-1
- **Assignee:** Tuanvm37
- **Priority:** Medium · **Severity:** 5 · **Test Round:** 1 · **Platform:** App · **Effect:** Usability · **Defect Type:** Requirement · **Fix version:** V1.0
- **Status:** To Do
- **Labels:** bug-001, tc-usr-017, tc-usr-018, tc-usr-020, tc-usr-023
- **Module:** USR (Tài khoản & Hồ sơ) · **Màn:** Cập nhật thông tin → field "Số điện thoại mặc định"
- **Môi trường:** STG · Platform test: mobile (Appium MCP / UiAutomator2), Pixel 7 AVD 1080x2400
- **Test case liên quan:** TC-USR-017, TC-USR-018, TC-USR-020, TC-USR-023
- **Nguồn:** Vibe Test `VR-001-USR-2026-09-18` (`08_test-runs/vibe/VR-001-USR-2026-09-18/vibe-report.md`, ứng viên bug **B3**)
- **Evidence:** ✅ đã đính kèm trên Jira (verify 2026-09-18 15:11 qua `getJiraIssue` → 4 attachment thật) — `TC-USR-017__step5-FAIL-chuoi-thong-bao-lech.png` (id `31490`) · `TC-USR-018__step5-FAIL-chuoi-thong-bao-lech.png` (id `31491`) · `TC-USR-020__step5-FAIL-chuoi-thong-bao-lech.png` (id `31492`) · `TC-USR-023__step5-FAIL-chuoi-thong-bao-lech.png` (id `31493`). Upload qua REST fallback `curl` (`~/.config/jira/.env`).
- **ID local:** `BUG-001` (draft cũ đã chuyển sang `jira/`, xem `bug-index.md`)

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (mobile app, không phải web)
- Account/Role: FOXECO_STG_USER_A — Đặng Châu Giang, MNV 00131946, Ban Giám đốc
- Trình duyệt / Thiết bị: emulator-5554, Pixel 7 AVD, 1080x2400, UiAutomator2
- Build/Version: STG · v1.1

**II. Mô tả Bug**

**Pre-condition:** Đã đăng nhập FoxEco, đang ở màn "Cập nhật thông tin" (Cá nhân → Cập nhật thông tin).

**Steps:**

1. Vào field "Số điện thoại mặc định"
2. Nhập một trong các giá trị sai định dạng sau:
   - để trống (TC-USR-017)
   - `091234567` — 9 số (TC-USR-018)
   - `1912345678` — không bắt đầu bằng 0 (TC-USR-020)
   - `09123a5678` — chứa chữ (TC-USR-023)
3. Nhấn nút "Lưu thay đổi"

**Expected result:**

- TC-USR-017: thông báo lỗi đỏ "Vui lòng nhập số điện thoại"
- TC-USR-018 / TC-USR-020 / TC-USR-023: thông báo lỗi đỏ "Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)"
- (các vế khác đều đạt: màu đỏ, vị trí ngay dưới field, chặn lưu đúng, không banner "Đã lưu…" giả)

**Actual result:**

- TC-USR-017: hiện "Số điện thoại không được để trống" (khác hẳn câu kỳ vọng)
- TC-USR-018 / TC-USR-020 / TC-USR-023: hiện "Số điện thoại không hợp lệ" — thiếu hẳn phần `(10 số, bắt đầu bằng 0)` trong ngoặc
- Chuỗi kỳ vọng lấy từ demo `DOC-v1.1-02`, BA xác nhận 2026-09-17 là chuỗi chính thức
- Hành vi chặn lưu bản thân đúng ở cả 4 case — chỉ sai nội dung text thông báo
