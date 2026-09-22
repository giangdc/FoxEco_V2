# FE-298 — [TC_11 - Tài khoản & Hồ sơ]: Gợi ý địa chỉ tìm địa chỉ không đúng

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-298 · **Module:** USR · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-298 |
| Module | USR |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Medium (weight 5) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Data |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date |  |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-18 |
| Updated | 2026-09-22 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (mobile app, không phải web)
- Account/Role: FOXECO_STG_USER_A — Đặng Châu Giang, MNV 00131946, Ban Giám đốc
- Trình duyệt / Thiết bị: emulator-5554, Pixel 7 AVD, 1080x2400, UiAutomator2
- Build/Version: STG · v1.1

**II. Mô tả Bug**

**Pre-condition:** Đã đăng nhập FoxEco, đang ở màn "Cập nhật thông tin", field "Địa chỉ mặc định" đang rỗng.

**Steps:**

1. Nhấn vào field "Địa chỉ mặc định"
2. Nhập từ khoá "hcm" (≥ 3 ký tự, đúng biên dưới cho phép gợi ý)
3. Quan sát danh sách gợi ý trả về

**Expected result:**

- Không hiển thị gợi ý nào, vì rule đã chốt là chỉ tìm theo tên văn phòng (name), không theo mã tỉnh (C-USR-05, BA chốt 2026-09-16) — không văn phòng nào có name chứa chuỗi "hcm"

**Actual result:**

- App trả về 12 gợi ý, toàn bộ là văn phòng thuộc tỉnh HCM (FTEL SG07, FTEL SG09, FTEL SG11, FPT Tân Thuận 1, FPT Tân Thuận 3, FTEL SG10 QL 50, FTEL SG01 Quận 9, FTEL SG02 Quận 6, FTEL SG02 Quận 8, FTEL SG04 Quận 1, FTEL SG08 Gò Vấp, FTEL SG16 Quận 7) — không tên nào chứa chuỗi "hcm", chỉ khớp qua tiền tố mã tỉnh
- Kết luận này độc lập với lệch master data STG (danh mục VP trên STG khác DOC-v1.1-04) — chỉ cần "tên không chứa hcm mà vẫn được trả về" là đủ chứng minh app đang khớp trên field sai
- Bằng chứng đối chiếu file dữ liệu gốc location_address_catalog.xlsx (399 dòng): cột search_alias_text = search_text (đã bỏ dấu, lowercase) ghép thêm mã tỉnh ở đầu. Ví dụ dòng 12: name = "82/20 Quang Trung, Gò Vấp" → search_alias_text = "hcm 82 20 quang trung go vap". Toàn bộ 34 dòng tỉnh HCM đều có search_alias_text bắt đầu bằng "hcm " ⇒ gõ "hcm" khớp được cả 12/34 dòng này chính vì app đang so khớp trên search_alias_text, không phải name
- Đã verify lại 2 lần trong 2 phiên độc lập, tái hiện y hệt cả 2 lần

**Hình ảnh mô tả:** đính kèm file ảnh trên issue này
