# FE-303 — [TC_04 - Đăng tin - Tôi cần gửi hàng] Vẫn chọn được buổi đã trôi qua trong ngày hôm nay

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-303 · **Module:** ORD · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-303 |
| Module | ORD |
| Status | In review |
| Resolution | Fixed |
| Resolved | 2026-09-23 |
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
| Due date | 2026-09-23 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-21 |
| Updated | 2026-09-23 |

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
- **Thời điểm chạy là sau 12 giờ trưa** để buổi "Sáng (8–12)" đã trôi qua _(phiên test thực hiện lúc 13:44)_.

**Steps:**

1. Đăng nhập app FoxPro → menu "Chức năng" → nhấn icon FoxEco
2. Nhấn "+ Đăng tin" → nhấn card "Tôi cần gửi hàng" → nhập đủ trường bước 1 → nhấn "Tiếp theo"
3. Ở bước 2, chọn "Từ ngày" và "Đến ngày" đều là **ngày hiện tại**
4. Nhấn chọn buổi **"Sáng (8–12)"**
5. Quan sát trạng thái chọn của chip "Sáng (8–12)"

**Expected result:**

- Buổi "Sáng (8–12)" **không chọn được**, giữ nguyên trạng thái không được chọn hoặc bị vô hiệu hoá.

**Actual result:**

- Buổi "Sáng (8–12)" **CHỌN ĐƯỢC bình thường** — chip chuyển sang trạng thái đã chọn (viền cam + chữ cam), không bị vô hiệu hoá, không có cảnh báo nào.

**Phạm vi ảnh hưởng:**

- Người gửi có thể đăng tin hẹn giao vào một khung giờ **đã trôi qua** ngay trong ngày ⇒ tin không thể được đáp ứng, người vận chuyển nhận rồi mới phát hiện vô nghĩa.

**Căn cứ:** `C-ORD-15(b)` — BA chốt 2026-09-17: _"app CHẶN chọn buổi đã qua trong ngày"_. ⚠️ Rule này **không có trong PRD**; câu trả lời của BA tại `C-ORD-15` là **nguồn chốt duy nhất**.

**Hình ảnh mô tả:** đính kèm file ảnh trên issue này (`TC-ORD-059__step4-FAIL-chon-duoc-buoi-da-qua.png`)
