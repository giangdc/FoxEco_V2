# FE-309 — [TC_07 - Trang chủ - Tin mới] Nút Xem thêm trên Bảng tin hiện khi đúng 5 tin

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-309 · **Module:** HOME · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-309 |
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
* Account/Role: CBNV `Nguyễn Thị Thanh Thủy` (`stag_thuyntt22@`) — tài khoản không có tin nào của chính mình
* Trình duyệt / Thiết bị: emulator-5554 (Android 13, 1080×2400), UiAutomator2
* Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

* Hệ thống có **đúng 5 tin NEED hợp lệ** (chưa ghép, chưa hết hạn), người xem không có tin nào của chính mình. _(Đã xác nhận bằng tab "Bảng tin" của chính tài khoản:_ `feed-post-card-0..4` = 5 tin.)

**Steps:**

1. Đăng nhập app FoxPro → menu "Chức năng" → nhấn icon FoxEco
2. Mở tab "Bảng tin", cuộn hết danh sách và đếm: đúng 5 tin
3. Về tab "Trang chủ"
4. Đếm số tin ở section "Tin mới" rồi cuộn xuống cuối section

**Expected result:**

* Section hiển thị đúng 5 tin và cuối section **KHÔNG có** nút "Xem thêm trên Bảng tin". Căn cứ `AC-11.1.01` / `SC-HOME-021`: nút chỉ hiện khi **hơn 5** tin hợp lệ; _"nếu tổng tin hợp lệ ≤5 thì nút KHÔNG hiện"_.

**Actual result:**

* "Tin mới" hiện 5 tin **và có nút** `Xem thêm trên Bảng tin ›` ở cuối section.
* Đối chiếu: khi hệ thống chỉ có **4** tin (cùng tài khoản, trước khi đăng thêm 1 tin) thì cuối section **không có** nút ⇒ app hiện nút từ `≥ 5` thay vì `> 5`.

**Hình ảnh mô tả:** xem file đính kèm trên issue (`TC-HOME-025__step4-FAIL-van-co-nut-xem-them-khi-dung-5-tin.png`, `TC-HOME-025__verify-bang-tin-5-tin-hop-le-toan-he-thong.png`).
