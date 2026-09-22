# FE-302 — [TC_04 - Đăng tin - Tôi cần gửi hàng] Thoát wizard không hiện popup xác nhận, mất dữ liệu đã nhập

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-302 · **Module:** ORD · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-302 |
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
3. Ở bước 2, nhập "Số 9 Duy Tân" vào ô "Địa chỉ giao hàng"
4. Nhấn nút quay lại để đóng wizard (nhấn 2 lần: bước 2 → bước 1 → thoát)
5. Quan sát popup xác nhận thoát

**Expected result:**

- Hiện popup đúng chuỗi **"Thoát và bỏ nội dung đã nhập?"**; sau khi chọn *ở lại*, ô "Địa chỉ giao hàng" vẫn giữ nguyên "Số 9 Duy Tân".

**Actual result:**

- **Không có popup nào** — tìm phần tử chứa text "Thoát" → NOT FOUND.
- Nhấn "Quay lại" ở bước 1 **thoát thẳng khỏi wizard**, **toàn bộ dữ liệu đang soạn dở bị xoá sạch**, không có bất kỳ cảnh báo nào.
- Ghi nhận thêm về điều hướng: ở bước 2, "Quay lại" **về bước 1** (không đóng wizard) — nên phải nhấn 2 lần mới tới điểm thoát.

**Phạm vi ảnh hưởng:**

- Người dùng lỡ tay chạm "Quay lại" sau khi đã nhập gần hết form 2 bước sẽ **mất toàn bộ công nhập liệu**, không có đường hoàn tác.
- Nhánh *"chọn thoát trên popup"* (`TC-ORD-062`) cũng không thực hiện đúng kịch bản được vì popup không tồn tại.

**Căn cứ:** `AC-01.2.01` + `C-ORD-08` (BA chốt 2026-09-15: assert **verbatim** chuỗi popup).

**Hình ảnh mô tả:** đính kèm file ảnh trên issue này (`TC-ORD-053__step4-FAIL-khong-co-popup-thoat.png`)
