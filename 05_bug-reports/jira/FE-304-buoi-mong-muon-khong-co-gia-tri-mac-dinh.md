# FE-304 — [TC_04 - Đăng tin - Tôi cần gửi hàng] Buổi mong muốn không có giá trị mặc định Sau giờ làm

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-304 · **Module:** ORD · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-304 |
| Module | ORD |
| Status | To Do |
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
| Reject Number | — |
| Due date |  |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-21 |
| Updated | 2026-09-21 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: CBNV `Đặng Châu Giang`, MNV 00131946 (tài khoản A) — vai SENDER
- Trình duyệt / Thiết bị: emulator-5554, Android, 1080x2400, UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Tài khoản A là CBNV có hồ sơ đầy đủ trên STG, đã đăng nhập host app FoxPro.

**Steps:**

1. Đăng nhập app FoxPro → menu "Chức năng" → nhấn icon FoxEco
2. Nhấn "+ Đăng tin" → nhấn card "Tôi cần gửi hàng" → nhập đủ trường bước 1 → nhấn "Tiếp theo"
3. Ở bước 2, quan sát nhóm "Thời gian" → field buổi mong muốn, **khi chưa chạm vào field**

**Expected result:**

- Buổi **"Sau giờ làm (17–19)"** đang ở trạng thái **được chọn sẵn**.

**Actual result:**

- **KHÔNG buổi nào được chọn sẵn.** Cả 4 chip (`Sáng (8–12)` · `Chiều (13–17)` · `Sau giờ làm (17–19)` · `Giờ nào cũng được`) đều ở trạng thái chưa chọn.
- App còn hiện **luôn lỗi đỏ "Chọn ít nhất 1 buổi"** ngay khi màn vừa mở, trong khi người dùng chưa thao tác gì.

**Phạm vi ảnh hưởng:**

- Mọi người dùng đăng tin NEED đều phải tự chọn buổi, mất đi giá trị mặc định mà PRD thiết kế để rút ngắn thao tác.
- Hiện lỗi đỏ ngay khi chưa thao tác làm form trông như đang sai, dù người dùng chưa nhập gì.
- ⚠️ **Nghi lan sang form OFFER**: PRD đặt **cùng giá trị mặc định** cho field `Buổi di chuyển` của FR02 (*"Chọn nhiều · mặc định Sau giờ làm"*). Nhánh OFFER **chưa được test** ở phiên này — đề nghị dev kiểm cả hai form khi fix.

**Căn cứ (PRD v1.1 — 2 chỗ):**

- `§8.1.4` UI / Field Spec (FR01): `Buổi mong muốn | Có | Chọn nhiều · mặc định Sau giờ làm | Sáng (8–12) · Chiều (13–17) · Sau giờ làm (17–19) · Giờ nào cũng được`
- `AC-06.1.01` (Given): *"Người dùng đang ở nhóm 'Thời gian' ở bước 2, mặc định Từ ngày = hôm nay, Đến ngày = Từ ngày, ****buổi = Sau giờ làm****."*

**Hình ảnh mô tả:** đính kèm file ảnh trên issue này (`TC-ORD-058__verify-buoi-mac-dinh.png`)
