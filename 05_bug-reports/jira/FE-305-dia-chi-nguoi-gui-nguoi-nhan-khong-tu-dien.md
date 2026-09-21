---
bug_id: BUG-013
jira_project: FE
jira_issue_type: Bug
jira_key: FE-305
jira_url: https://foxproject.atlassian.net/browse/FE-305
module: ORD - Đăng tin & Quản lý tin
bug_desc: Địa chỉ người gửi và người nhận không được tự điền
priority: P2
severity: Medium
components: [ORD]
affects_versions: [v1.1]
traceability: TC-ORD-017 → SC-ORD-016 → REQ-ORD-007 · TC-ORD-043 → SC-ORD-040 → REQ-ORD-016 · TC-ORD-019 → SC-ORD-018 → REQ-ORD-008 · TC-ORD-074 → SC-ORD-058 → REQ-ORD-008
status: To Do
effect: Functionality
defect_type: Data
platform: App
test_method: Manual
test_round: R1
reject_number:
resolution:
reason_for_wontfix:
attachments: [08_test-runs/vibe/VR-004-ORD-2026-09-18/screenshots/TC-ORD-017__step3-FAIL-dia-chi-lay-hang-khong-prefill.png, 08_test-runs/vibe/VR-004-ORD-2026-09-18/screenshots/TC-ORD-043__verify-diem-xuat-phat-khong-prefill.png, 08_test-runs/vibe/VR-004-ORD-2026-09-18/screenshots/TC-ORD-019__step4-FAIL-autofill-thieu-o-dia-chi-giao.png, 08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-074__step5-FAIL-dia-chi-giao-khong-tu-dien.png]
reported_by: GiangDC2
reported_on: 2026-09-21
assignee: Tuanvm37
due_date:
last_synced: 2026-09-21
---

# [ORD - Đăng tin & Quản lý tin] - Địa chỉ người gửi và người nhận không được tự điền

> Jira: [FE-305](https://foxproject.atlassian.net/browse/FE-305) · Status: To Do · *(gộp từ BUG-013 + BUG-014 cũ)*

<!-- jira:description:start — copy nguyên khối dưới đây vào field Description của Jira -->

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: CBNV `Đặng Châu Giang`, MNV 00131946 (tài khoản A) — vai SENDER
- Trình duyệt / Thiết bị: emulator-5554, Android, UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

Khi đăng tin, các ô **địa chỉ** không được tự điền dù hệ thống đáng lẽ đã có dữ liệu: (A) địa chỉ của **người gửi** không được điền sẵn từ hồ sơ; (B) địa chỉ giao của **người nhận** không được điền khi tra danh bạ nội bộ. Người dùng phải tự nhập tay cả hai, và vì ô địa chỉ là autocomplete bắt buộc chạm gợi ý (xem `FE-301`) nên dễ bị kẹt ở bước này.

Liên quan: `FE-300` (SĐT và địa chỉ mặc định không được nạp từ HRIS vào hồ sơ FoxEco).

**Pre-condition:**

- Tài khoản A đã đăng nhập host app FoxPro. Hồ sơ FoxEco của tài khoản A **không có "Địa chỉ mặc định"** (xem `FE-300`).
- Email người nhận `stag_anhdc4@fpt.com` — email nội bộ có trên danh bạ (email mẫu BA cung cấp, `C-ORD-13`).

**Steps A — địa chỉ người gửi:**

1. Đăng nhập app FoxPro → menu "Chức năng" → nhấn icon FoxEco
2. Nhấn "+ Đăng tin" → card "Tôi cần gửi hàng" → nhập đủ trường bước 1 → "Tiếp theo"
3. Ở Bước 2, quan sát ô "Địa chỉ lấy hàng" ngay khi vừa vào màn
4. Quay lại "Đăng tin mới" → card "Tôi nhận giao hàng" → quan sát ô "Điểm xuất phát (A)"

**Steps B — địa chỉ người nhận:**

1. Ở Bước 2 của wizard "Tôi cần gửi hàng", nhập `stag_anhdc4@fpt.com` vào ô "Email công ty người nhận" rồi rời ô
2. Quan sát 3 ô Tên · Số điện thoại · Địa chỉ giao hàng của nhóm "NGƯỜI NHẬN"

**Expected result:**

- **A:** "Địa chỉ lấy hàng" (NEED) và "Điểm xuất phát (A)" (OFFER) được **điền sẵn địa chỉ nơi làm việc** và sửa được, không chỉ là chữ gợi ý. Căn cứ `SC-ORD-016` / `REQ-ORD-007` (`DOC-v1.0-01 §D8.1 L364`); OFFER `§D8.2 L381-382`.
- **B:** tra thấy ⇒ **tự điền cả 3 ô** tên · số điện thoại · địa chỉ, vẫn sửa được. Căn cứ `BR01-09` (`DOC-v1.1-01 §8.1.1`, trang 34): _"Email công ty người nhận được tra danh bạ nội bộ: tìm thấy thì tự điền tên · số điện thoại · địa chỉ (vẫn sửa được); không thấy thì cho nhập thủ công."_

**Actual result:**

- **A:** "Địa chỉ lấy hàng" và "Điểm xuất phát (A)" **RỖNG**, chỉ có placeholder (`Địa chỉ lấy hàng` / `Bạn đang ở đâu / xuất phát từ đâu`). Cùng tài khoản A, phiên VR-002 (sáng 2026-09-18) ô này **có** prefill `363 Nguyễn Hữu Thọ, Cẩm Lệ`; phiên VR-004 (cùng ngày, sau các phiên test màn "Cập nhật thông tin") thì rỗng.
- **B:** app hiện dòng xanh `Đã tìm thấy trong hệ thống nội bộ · vui lòng bổ sung SĐT/địa chỉ giao còn thiếu.` Tên `Đặng Châu Anh` ✓ · SĐT `0343439724` ✓ · **Địa chỉ giao hàng RỖNG** ✗. Tái hiện ở 2 phiên độc lập, 2 version TC: `TC-ORD-074` (VR-002, P1) và `TC-ORD-019` (VR-004, P1).
- Nghịch lý ở B: chính thông báo của app nói "vui lòng bổ sung … địa chỉ giao còn thiếu" — app tự nhận là chưa điền đủ, nhưng SĐT thì điền được.

**Phạm vi ảnh hưởng:**

- Mọi lần đăng tin, người dùng phải tự nhập tay địa chỉ lấy hàng (nếu hồ sơ chưa có địa chỉ mặc định) và địa chỉ giao của người nhận, dù hệ thống nội bộ đã tra thấy người đó.

**Hình ảnh mô tả:** đính kèm 4 ảnh (mỗi TC 1 ảnh: `TC-ORD-017`, `TC-ORD-043`, `TC-ORD-019`, `TC-ORD-074`)

<!-- jira:description:end -->

## Status History

| Ngày | Status | Ghi chú | Ref |
|---|---|---|---|
| 2026-09-21 | Draft | Gộp `BUG-013` (prefill người gửi) + `BUG-014` (autofill người nhận) theo yêu cầu QC — cùng họ "địa chỉ không được tự điền" | VR-002 · VR-004 |
| 2026-09-21 | To Do | Push Jira → FE-305 theo yêu cầu QC (assignee Tuanvm37, P2→High, severity Medium=5). ⚠️ Vế B (`019`/`074`) còn chờ xác minh bản ghi HRIS của `stag_anhdc4`; vế A phụ thuộc `FE-300` — xem ghi chú nội bộ | — |

## Ghi chú nội bộ (không push Jira) — 🔎 điều kiện còn treo sau khi push

- **Gộp được, nhưng 2 vế KHÔNG cùng nguồn — đọc kỹ trước khi push.**
  - **Vế A** (`017`, `043`) đi qua **màn "Cập nhật thông tin" (USR)**: ô lấy hàng đọc "Địa chỉ mặc định" trong hồ sơ của **chính người gửi** ⇒ đúng là lây từ `FE-300`.
  - **Vế B** (`019`, `074`) đi qua **tra danh bạ nội bộ theo email người nhận** — đọc bản ghi HRIS/danh bạ của **người khác**, **không đi qua hồ sơ FoxEco của người gửi**. Nó chỉ *có thể* cùng gốc với `FE-300` (địa chỉ từ HRIS không bao giờ được app đọc) — điều này **chưa được chứng minh**.
  - ⇒ **Hệ quả khi gộp:** sửa `FE-300` (hồ sơ nạp được địa chỉ HRIS) sẽ chữa **vế A**, nhưng **không tự chữa vế B**. Nếu Dev thấy `FE-300` xong rồi đóng issue này thì vế B bị bỏ sót. ⇒ Khi retest phải kiểm **cả 2 vế** riêng (Steps A, Steps B).
- **Có phải bug thật không?**
  - **Vế A — khả năng cao là hệ quả của `FE-300` + nhiễu dữ liệu test.** Hồ sơ tài khoản A đã bị đổi ở các phiên USR (VR-001/003: `TC-USR-040` field "Địa chỉ mặc định" rỗng mà app vẫn cho lưu; `FE-292` cho lưu chuỗi rác làm địa chỉ), nên `TC-ORD-017` đổi PASS→FAIL giữa VR-002 và VR-004 có thể do test làm rỗng dữ liệu.
  - **Vế B — chưa chắc.** BA vòng 2 (`C-ORD-13`, ý 5) trả lời: *"hồ sơ HRIS thiếu SĐT/địa chỉ ⇒ tự điền phần có, bỏ trống phần thiếu"*. Nếu HRIS của `stag_anhdc4` không có địa chỉ thì app điền 2/3 là **đúng**. Ngược lại, QC đã chốt (ở `FE-300`) rằng HRIS luôn có SĐT + địa chỉ bắt buộc ⇒ nếu vậy autofill phải điền được.
- **Hai phép kiểm để chốt (làm độc lập):**
  1. **Vế A:** đặt lại "Địa chỉ mặc định" hợp lệ cho tài khoản A, mở lại wizard. Có prefill ⇒ ORD đọc hồ sơ đúng ⇒ thuộc `FE-300`. Vẫn rỗng ⇒ bug riêng của ORD.
  2. **Vế B:** nhờ Dev/BA tra bản ghi HRIS/danh bạ của `stag_anhdc4@fpt.com` có địa chỉ không (app HRIS mobile không phơi field địa chỉ nên QC không tự đọc được — đã ghi ở `BUG-008`).
- **Quyết định sau phép kiểm:**
  - A → thuộc `FE-300` **và** B → bản ghi không có địa chỉ: **không push issue này**; thêm `TC-ORD-017`/`043` làm dẫn chứng vào `FE-300`; sửa Expected `TC-ORD-019`/`074` qua QC (`§10.5`: chỉ sửa Expected, không thêm/xoá TC).
  - A → thuộc `FE-300` **và** B → bản ghi CÓ địa chỉ mà app không điền: push issue này **rút gọn còn vế B**, gắn "relates to `FE-300`".
  - A vẫn rỗng dù hồ sơ có địa chỉ: push đủ 2 vế.
- Mức đề xuất: P2 · Medium. Hai TC của vế B mang priority P1 nhưng ảnh hưởng thực tế là *phải gõ thêm 1 ô* — QC chốt.
- Khi push: tiêu đề theo convention Jira `[TC_04 - Đăng tin - Tôi cần gửi hàng] …`; thêm issue link "relates to" `FE-300`.
