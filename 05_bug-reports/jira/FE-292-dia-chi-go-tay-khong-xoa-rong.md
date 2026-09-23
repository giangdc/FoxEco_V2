# FE-292 — [TC_11 - Tài khoản & Hồ sơ] - Địa chỉ gõ tay không bị xoá rỗng khi rời field, bị lưu làm mặc định

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-292 · **Module:** USR · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-292 |
| Module | USR |
| Status | In Progress |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 1 |
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

- Field "Địa chỉ mặc định" tự động trở về rỗng sau khi rời field. chỉ lưu data khi chọn lên từ gợi ý

**Actual result:**

- Field vẫn giữ nguyên `asdfghjkl1` sau khi rời field. Đã loại trừ khả năng "chưa thật sự rời field" bằng 3 tín hiệu độc lập.
- Nếu bấm "Lưu thay đổi", chuỗi rác được lưu thành công làm địa chỉ mặc định.
- ⚠️ Ảnh hưởng ngoài phạm vi USR: prefill sang địa chỉ lấy hàng khi tạo đơn ở module ORD.

**Hình ảnh mô tả:** đính kèm 2 ảnh evidence (TC-USR-028, TC-USR-030) theo attachment của issue này.
