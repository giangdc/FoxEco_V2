# FE-300 — [TC_11 - Tài khoản & Hồ sơ] - Không load SĐT và địa chỉ mặc định từ HRIS

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-300 · **Module:** USR · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-300 |
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
| Defect Type | Data |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 1 |
| Due date | 2026-09-23 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-21 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

* URL: N/A (mobile app, không phải web)
* Account/Role: CBNV `stag_thuyntt22@fpt.com` — Nguyễn Thị Thanh Thủy, MNV 00002352, Phòng Hành chính phía Bắc (tài khoản **chưa từng lưu thông tin** ở màn "Cập nhật thông tin")
* Trình duyệt / Thiết bị: emulator-5554, Android, 1080x2400, UiAutomator2
* Build/Version: STG · v1.1

**II. Mô tả Bug**

**Pre-condition:**

* CBNV chưa từng bấm "Lưu thay đổi" ở màn "Cập nhật thông tin" của FoxEco (lần đầu mở màn).
* HRIS có sẵn **cả** số điện thoại **lẫn** địa chỉ làm việc của CBNV đó — đây là **dữ liệu mặc định luôn có**: khi tạo nhân viên trên HRIS, 2 trường này là **bắt buộc** (QC GiangDC2 chốt 2026-09-18).

**Steps:**

1. Đăng nhập app FoxPro bằng tài khoản CBNV → vào menu "Chức năng" → nhấn icon FoxEco
2. Nhấn tab "Cá nhân" ở bottom nav
3. Nhấn mục menu "Cập nhật thông tin cá nhân"
4. Quan sát field "Số điện thoại mặc định" và field "Địa chỉ mặc định" ngay khi màn vừa mở, **trước khi** gõ gì

**Expected result:**

* Field "Số điện thoại mặc định" hiển thị đúng số điện thoại của CBNV trên HRIS và cho phép nhập.
* Field "Địa chỉ mặc định" hiển thị đúng địa chỉ làm việc của CBNV trên HRIS và cho phép nhập.
* Căn cứ: BA chốt 2026-09-16 (_"mặc định load HRIS, cho sửa"_) + PRD `§8.15.2` (_"số điện thoại hiện tại"_, _"địa chỉ làm việc trong hồ sơ"_).

**Actual result:**

* **CẢ HAI field đều RỖNG** — chỉ hiển thị chữ gợi ý (placeholder) `09xx xxx xxx` và `Toà nhà, đường, quận`. App **không load bất kỳ giá trị nào từ HRIS**.
* Xác nhận bằng accessibility tree: cả 2 `EditText` đều có `showing-hint="true"` (⚠️ thuộc tính `text` vẫn trả về chuỗi placeholder, nên nhìn qua log dễ tưởng field có dữ liệu).
* Đối chiếu HRIS **của chính tài khoản này**, đọc tại chỗ cùng ngày (FoxPro → Cá nhân → Thông tin cá nhân → Thông tin): trường **"Điện thoại" CÓ giá trị hợp lệ** (10 số, bắt đầu bằng 0).
* Vế _"cho phép nhập"_ của Expected thì **ĐẠT** (con trỏ + bàn phím hiện đúng) — lỗi nằm ở **vế nạp dữ liệu**.

**Phạm vi ảnh hưởng:**

* Tái hiện trên **2 tài khoản khác nhau, 2 phiên test khác nhau**: tài khoản A (MNV 00131946, VR-001 — tài khoản có địa chỉ HRIS đã biết là `HCM LôB3,E-Office,KCN TânThuận`) và tài khoản MNV 00002352 (VR-003) ⇒ **không phải lỗi dữ liệu của một tài khoản**.
* Ảnh hưởng **100% CBNV dùng FoxEco lần đầu**: ai cũng phải tự gõ lại thông tin mà hệ thống đã có sẵn.
* **Lan sang module ORD:** địa chỉ mặc định rỗng ⇒ ô "địa chỉ lấy hàng" khi đăng tin cũng không có gì để prefill.

**Hình ảnh mô tả:** đính kèm file ảnh trên issue này (`TC-USR-043__step5-FAIL-sdt-khong-prefill-hris.png`, `TC-USR-040__step5-FAIL-dia-chi-khong-prefill-hris.png`)
