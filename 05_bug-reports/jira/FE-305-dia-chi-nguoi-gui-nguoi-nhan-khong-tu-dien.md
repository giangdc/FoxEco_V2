# FE-305 — [TC_04 - Đăng tin - Tôi cần gửi hàng/Tôi nhận giao hàng] Địa chỉ người gửi/người nhận/Thông tin của tôi mặc định không load thông tin từ màn hình Cập nhật thông tin 

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-305 · **Module:** ORD · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-305 |
| Module | ORD |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Low |
| Severity | Low (weight 2) |
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
| Created | 2026-09-21 |
| Updated | 2026-09-24 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

* URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
* Account/Role: CBNV `Đặng Châu Giang`, MNV 00131946 (tài khoản A) — vai SENDER
* Trình duyệt / Thiết bị: emulator-5554, Android, UiAutomator2
* Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

Khi đăng tin, các ô **địa chỉ** không được tự điền dù hệ thống đáng lẽ đã có dữ liệu: (A) địa chỉ của **người gửi** không được điền sẵn từ hồ sơ; (B) địa chỉ giao của **người nhận** không được điền khi tra danh bạ nội bộ. Người dùng phải tự nhập tay cả hai, và vì ô địa chỉ là autocomplete bắt buộc chạm gợi ý (xem `FE-301`) nên dễ bị kẹt ở bước này.

Liên quan: `FE-300` (SĐT và địa chỉ mặc định không được nạp từ HRIS vào hồ sơ FoxEco).

**Pre-condition:**

* Tài khoản A đã đăng nhập host app FoxPro. Hồ sơ FoxEco của tài khoản A  **có "Địa chỉ mặc định"** (xem `FE-300`).
* Email người nhận `stag_anhdc4@fpt.com` — email nội bộ có trên danh bạ (email mẫu BA cung cấp, `C-ORD-13`).

**Steps A — địa chỉ người gửi:**

1. Đăng nhập app FoxPro → menu "Chức năng" → nhấn icon FoxEco
2. Nhấn "+ Đăng tin" → card "Tôi cần gửi hàng" → nhập đủ trường bước 1 → "Tiếp theo"
3. Ở Bước 2, quan sát ô "Địa chỉ lấy hàng" ngay khi vừa vào màn
4. Quay lại "Đăng tin mới" → card "Tôi nhận giao hàng" → quan sát ô "Điểm xuất phát (A)"

**Steps B — địa chỉ người nhận:**

1. Ở Bước 2 của wizard "Tôi cần gửi hàng", nhập `stag_anhdc4@fpt.com` vào ô "Email công ty người nhận" rồi rời ô
2. Quan sát 3 ô Tên · Số điện thoại · Địa chỉ giao hàng của nhóm "NGƯỜI NHẬN"

**Expected result:**

* **A:** "Địa chỉ lấy hàng" (NEED) và "Điểm xuất phát (A)" (OFFER) được **điền sẵn địa chỉ nơi làm việc** và sửa được, không chỉ là chữ gợi ý. Căn cứ `SC-ORD-016` / `REQ-ORD-007` (`DOC-v1.0-01 §D8.1 L364`); OFFER `§D8.2 L381-382`.
* **B:** tra thấy ⇒ **tự điền cả 3 ô** tên · số điện thoại · địa chỉ, vẫn sửa được. Căn cứ `BR01-09` (`DOC-v1.1-01 §8.1.1`, trang 34): _"Email công ty người nhận được tra danh bạ nội bộ: tìm thấy thì tự điền tên · số điện thoại · địa chỉ (vẫn sửa được); không thấy thì cho nhập thủ công."_

**Actual result:**

* **A:** "Địa chỉ lấy hàng" và "Điểm xuất phát (A)" **RỖNG**, chỉ có placeholder (`Địa chỉ lấy hàng` / `Bạn đang ở đâu / xuất phát từ đâu`). Cùng tài khoản A, phiên VR-002 (sáng 2026-09-18) ô này **có** prefill `363 Nguyễn Hữu Thọ, Cẩm Lệ`; phiên VR-004 (cùng ngày, sau các phiên test màn "Cập nhật thông tin") thì rỗng.
* **B:** app hiện dòng xanh `Đã tìm thấy trong hệ thống nội bộ · vui lòng bổ sung SĐT/địa chỉ giao còn thiếu.` Tên `Đặng Châu Anh` ✓ · SĐT `0343439724` ✓ · **Địa chỉ giao hàng RỖNG** ✗. Tái hiện ở 2 phiên độc lập, 2 version TC: `TC-ORD-074` (VR-002, P1) và `TC-ORD-019` (VR-004, P1).
* Nghịch lý ở B: chính thông báo của app nói "vui lòng bổ sung … địa chỉ giao còn thiếu" — app tự nhận là chưa điền đủ, nhưng SĐT thì điền được.

**Phạm vi ảnh hưởng:**

* Mọi lần đăng tin, người dùng phải tự nhập tay địa chỉ lấy hàng (nếu hồ sơ chưa có địa chỉ mặc định) và địa chỉ giao của người nhận, dù hệ thống nội bộ đã tra thấy người đó.

**Hình ảnh mô tả:** đính kèm 4 ảnh (mỗi TC 1 ảnh: `TC-ORD-017`, `TC-ORD-043`, `TC-ORD-019`, `TC-ORD-074`)
