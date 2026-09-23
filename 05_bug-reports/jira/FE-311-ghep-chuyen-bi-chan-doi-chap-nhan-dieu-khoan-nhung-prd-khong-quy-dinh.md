# FE-311 — [TC_02 - Ghép nối] - Ghép chuyến bị chặn đòi chấp nhận điều khoản nhưng PRD không quy định

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-311 · **Module:** ASN · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-311 |
| Module | ASN |
| Status | In Progress |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | High |
| Severity | Medium (weight 5) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date | 2026-09-23 |
| Reporter | GiangDC2 |
| Assignee | HungHT32 |
| Created | 2026-09-21 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: CBNV `Nguyễn Thị Thanh Thủy` (`stag_thuyntt22@`, MNV `00002352`) — vai người vận chuyển (Carrier); tài khoản chưa từng đăng tin/ghép chuyến (0 đơn đã giúp)
- Trình duyệt / Thiết bị: emulator-5554 (Android 15, 1080×2400), UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Có 1 tin NEED đang `Chờ ghép` do người khác đăng (không phải của tài khoản test, không khai tài khoản test là người nhận).
- Tài khoản test chưa từng đăng tin hay ghép chuyến.

**Steps:**

1. Đăng nhập app FoxPro bằng `stag_thuyntt22@` → menu "Chức năng" → nhấn icon FoxEco
2. Mở tab "Bảng tin" → nhấn vào 1 tin `Chờ ghép` của người khác
3. Nhấn nút "Tôi mang giúp được"
4. Trong modal "Xác nhận mang giúp" nhấn "Xác nhận"

**Expected result:**

- Theo PRD v1.1 (`DOC-v1.1-01`): luồng ghép chỉ có modal xác nhận lộ SĐT; **"Ghép ngay khi người vận chuyển bấm nhận — không có bước chủ tin duyệt"** (`§8.3.1 BR03-01`). Điều khoản miễn trừ chỉ được yêu cầu **trước khi đăng tin/đăng tuyến** (`§8.1.1 BR01-07`, `§8.18.2 VAL-01`, `§9 NFR-13`: _"hiển thị và bắt buộc tick trước khi đăng tin/đăng tuyến"_). ⇒ đơn được ghép, mở màn "Theo dõi đơn".
- _(Nếu nghiệp vụ thực sự muốn chặn ghép khi chưa consent — như_ `DOC-v1.0-01 §A8`: "buộc consent trước khi đăng/ghép" — thì luồng ghép phải có chỗ để người dùng đọc và chấp nhận điều khoản.)

**Actual result:**

- Modal đóng, xuất hiện toast đỏ **"Bạn cần chấp nhận điều khoản hiện hành trước khi đăng tin hoặc ghép chuyến"**; người dùng ở lại "Chi tiết tin", **không ghép được**.
- Trong luồng ghép **không có** checkbox, đường dẫn, link đọc hay màn nào để chấp nhận điều khoản ⇒ người dùng bị chặn mà không biết chấp nhận ở đâu.
- Đối chứng: `stag_anhptm17@` (đã có 6 đơn đã giúp) và `stag_taipm@` cùng thao tác trên cùng loại tin → ghép được, không hiện toast này.

**Hình ảnh mô tả:** xem file đính kèm trên issue (`_recon__lan-1-khong-hop-le-chua-chap-nhan-dieu-khoan.png` — dải 6 khung liên tiếp, toast hiện rõ từ khung 2).
