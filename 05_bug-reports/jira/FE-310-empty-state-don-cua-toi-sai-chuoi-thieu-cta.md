# FE-310 — [TC_07 - Trang chủ - Đơn của tôi] Empty state Đơn của tôi sai chuỗi, thiếu CTA và icon

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-310 · **Module:** HOME · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-310 |
| Module | HOME |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-09-23 |
| Verify Date | 2026-09-23 |
| Done At | 2026-09-23 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Interface |
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

* URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
* Account/Role: CBNV `Nguyễn Thị Thanh Thủy` (`stag_thuyntt22@`) — tài khoản "sạch": 0 đơn đang chạy, 0 đóng góp
* Trình duyệt / Thiết bị: emulator-5554 (Android 13, 1080×2400), UiAutomator2
* Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

* Tài khoản không có đơn nào đang chạy (hero `0 · Chưa có đóng góp nào`).

**Steps:**

1. Đăng nhập app FoxPro bằng tài khoản không có đơn → menu "Chức năng" → nhấn icon FoxEco
2. Mở tab "Trang chủ"
3. Quan sát section "Đơn của tôi"

**Expected result:**

* Section "Đơn của tôi" **vẫn hiển thị**, bên trong có **icon nét mảnh**, dòng **"Bạn chưa có đơn nào đang chạy"** và nút CTA **"Tạo đơn gửi hàng"** _(TC-HOME-027; PRD_ `DOC-v1.1-01` _§8.17.1,_ `EMP-02`_; BA chốt hiển thị ở_ `C-HOME-05`_)_.

**Actual result:**

* Section vẫn hiển thị _(đúng)_, nhưng bên trong chỉ có dòng **"Chưa có đơn nào"** — sai chuỗi `EMP-02`; **không có** nút "Tạo đơn gửi hàng"; **không thấy** icon.
* Đối chiếu cùng màn: empty state của "Tin mới" hiển thị đúng chuỗi `EMP-01` ⇒ chỉ `EMP-02` lệch.

**Hình ảnh mô tả:** xem file đính kèm trên issue (`TC-HOME-027__step3-FAIL-empty-state-chua-co-don-nao-thieu-cta-tao-don-gui-hang.png`).
