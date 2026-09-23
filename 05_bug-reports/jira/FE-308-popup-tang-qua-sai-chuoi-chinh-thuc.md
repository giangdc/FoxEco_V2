# FE-308 — [TC_08 - Quà cảm ơn - Tặng quà] Popup sau khi tặng quà hiện chuỗi cũ, sai chuỗi chính thức BR14-02

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-308 · **Module:** GIFT · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-308 |
| Module | GIFT |
| Status | In review |
| Resolution | Fixed |
| Resolved | 2026-09-23 |
| Verify Date |  |
| Done At |  |
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

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: CBNV `Phan Minh Tài` (`stag_taipm@`), MNV 00041796 — vai SENDER (người gửi quà)
- Trình duyệt / Thiết bị: emulator-5554, Android, 720x1280, UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Tài khoản người gửi có 1 đơn ở trạng thái **Hoàn thành**, **chưa từng tặng quà** (card đơn có hint `Chạm để tặng quà`).

**Steps:**

1. Đăng nhập app FoxPro → menu "Chức năng" → nhấn icon FoxEco
2. Nhấn tab "Hoạt động" → tab con "Đã hoàn thành"
3. Nhấn card đơn Hoàn thành chưa tặng quà → mở màn "Tặng quà"
4. Chọn loại quà "Bông hoa"
5. Nhấn nút "Xác nhận tặng quà"
6. Đọc tiêu đề và nội dung popup vừa hiện

**Expected result:**

- Quà gửi ngay, không có bước chờ xác nhận của người vận chuyển; popup hiện đúng chuỗi **"Cảm ơn của bạn đã được gửi"** kèm nút về trang chủ. _(BR14-02 · AC-24.1.01,_ `DOC-v1.1-01` §8.14.1 trang 49 · §6.2 trang 25)

**Actual result:**

- Popup hiện **tiêu đề** `Đã gửi lời cảm ơn!` — chuỗi của v1.0 mà v1.1 đã chủ ý thay.
- Nội dung popup: `Món quà và lời cảm ơn của bạn đã được gửi đến người vận chuyển.`
- Chuỗi `Cảm ơn của bạn đã được gửi` **không xuất hiện** ở tiêu đề. Chỉ có cụm chữ thường `cảm ơn của bạn đã được gửi` nằm lẫn trong câu nội dung.
- Các vế còn lại đúng: quà gửi ngay (không có màn chờ), có nút `Về trang chủ`.

**Hình ảnh mô tả:** đính kèm file ảnh trên issue này (`TC-GIFT-003__step5-FAIL-sai-chuoi-popup.png`)

![attachment](969f8ee9-cd7b-48c4-a731-98d473c6482c)
