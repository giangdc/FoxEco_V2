# [TC_11 - Tài khoản & Hồ sơ] - Địa chỉ gõ tay không bị xoá rỗng khi rời field, bị lưu làm mặc định

- **Jira:** [FE-292](https://foxproject.atlassian.net/browse/FE-292)
- **Project:** FE (Fox Eco) · **Parent:** FE-1
- **Assignee:** Tuanvm37
- **Priority:** High · **Severity:** 10 · **Test Round:** 1 · **Platform:** App · **Effect:** Functionality · **Defect Type:** Logic · **Fix version:** V1.0
- **Status:** To Do
- **Labels:** bug-002, tc-usr-028, tc-usr-029, tc-usr-030
- **Module:** USR (Tài khoản & Hồ sơ) · **Màn:** Cập nhật thông tin → field "Địa chỉ mặc định"
- **Môi trường:** STG · Platform test: mobile (Appium MCP / UiAutomator2), Pixel 7 AVD 1080x2400
- **Test case liên quan:** TC-USR-028 (+ dây chuyền TC-USR-029, TC-USR-030 — không mở bug riêng)
- **Nguồn:** Vibe Test `VR-001-USR-2026-09-18` (`08_test-runs/vibe/VR-001-USR-2026-09-18/vibe-report.md`, ứng viên bug **B4**)
- **Evidence:** ✅ đã đính kèm trên Jira (verify 2026-09-18 15:20 qua `getJiraIssue` → 2 attachment thật) — `TC-USR-028__step6-FAIL-khong-xoa-rong-khi-roi-field.png` (id `31501`) · `TC-USR-030__step10-FAIL-khong-rong-giu-text-go-tay.png` (id `31502`)
- **ID local:** `BUG-002` (draft cũ đã chuyển sang `jira/`, xem `bug-index.md`)

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (mobile app, không phải web)
- Account/Role: FOXECO_STG_USER_A — Đặng Châu Giang, MNV 00131946, Ban Giám đốc
- Trình duyệt / Thiết bị: emulator-5554, Pixel 7 AVD, 1080x2400, UiAutomator2
- Build/Version: STG · v1.1

**II. Mô tả Bug**

**Pre-condition:** Đã đăng nhập FoxEco, đang ở màn "Cập nhật thông tin", field "Địa chỉ mặc định".

**Steps:**

1. Gõ tay `asdfghjkl1` vào field "Địa chỉ mặc định" (không chọn gợi ý nào)
2. Nhấn ra vùng trống ngoài field để rời field (blur)
3. Bấm nút "Lưu thay đổi"

**Expected result:**

- Field "Địa chỉ mặc định" tự động trở về rỗng sau khi rời field.

**Actual result:**

- Field vẫn giữ nguyên `asdfghjkl1` sau khi rời field. Đã loại trừ khả năng "chưa thật sự rời field" bằng 3 tín hiệu độc lập: `focused=false`, bàn phím ẩn, thử 2 vùng trống khác nhau.
- Nếu bấm "Lưu thay đổi", chuỗi rác được lưu thành công làm địa chỉ mặc định (mở lại màn vẫn thấy).
- ⚠️ Ảnh hưởng ngoài phạm vi USR: prefill sang địa chỉ lấy hàng khi tạo đơn ở module ORD.
