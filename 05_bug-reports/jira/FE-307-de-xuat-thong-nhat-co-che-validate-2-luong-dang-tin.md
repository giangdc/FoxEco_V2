# FE-307 — [TC_04 - Đăng tin][Suggest] Đề xuất thống nhất cơ chế validate giữa 2 luồng đăng tin

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-307 · **Module:** ORD · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-307 |
| Module | ORD |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Low |
| Severity | Suggest (weight 0) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Requirement |
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
- Trình duyệt / Thiết bị: emulator-5554, Android, UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Đề xuất:** thống nhất cách xử lý khi form thiếu dữ liệu giữa hai luồng đăng tin **"Tôi cần gửi hàng"** (wizard) và **"Tôi nhận giao hàng"** (form 1 trang). Hiện hai luồng dùng hai cơ chế khác nhau cho cùng một tình huống, và cả hai đều lệch so với đặc tả ở một điểm.

**Hiện trạng:**

|  | "Tôi cần gửi hàng" (NEED) | "Tôi nhận giao hàng" (OFFER) |
|---|---|---|
| Nút gửi/tiếp khi thiếu dữ liệu | **khoá** (`enabled=false`) | **luôn bật** |
| Khi bấm lúc thiếu dữ liệu | không có phản hồi nào | không đăng, hiện lỗi đỏ inline `Chọn ít nhất 1 buổi` |
| Người dùng biết thiếu gì? | **không** (xem `FE-301`) | **có**, ít nhất ở nhánh "chưa chọn buổi" |
| Lỗi đỏ hiện ngay khi vừa mở form, chưa thao tác? | có (xem `FE-304`) | có (`Chọn ít nhất 1 buổi`) |

**Steps quan sát:**

1. Đăng nhập app FoxPro → menu "Chức năng" → nhấn icon FoxEco
2. **OFFER:** nhấn "+ Đăng tin" → card "Tôi nhận giao hàng" → không nhập gì → cuộn xuống cuối, quan sát nút "Đăng tin ngay" và dòng lỗi dưới khối "BUỔI MONG MUỐN"
3. **NEED:** nhấn "+ Đăng tin" → card "Tôi cần gửi hàng" → không nhập gì → quan sát nút "Tiếp theo" và các khối bắt buộc

**Căn cứ đặc tả:**

- `VAL-01` (`DOC-v1.0-01 §D8.3 L392`, `SC-ORD-047`): nút gửi **vô hiệu hoá tới khi form hợp lệ** — áp cho cả NEED và OFFER. NEED làm đúng; OFFER để nút bật ⇒ lệch chữ `VAL-01`.
- `VAL-02` (`§D8.3 L393`, `SC-ORD-048`): *"Lỗi hiện ngay dưới ô nhập khi rời ô (on blur), không dùng popup; cuộn tới ô lỗi đầu tiên khi bấm submit"*. OFFER làm được một phần; NEED chưa làm (`FE-301`).

**Đề xuất hướng thống nhất (BA/Dev chọn):**

- **Phương án A — theo **`VAL-01`: cả hai luồng **khoá nút** cho tới khi đủ dữ liệu, **kèm lỗi inline tại từng trường** (`VAL-02`) để người dùng biết thiếu gì. OFFER chuyển sang khoá nút; NEED bổ sung lỗi inline (đang theo dõi ở `FE-301`).
- **Phương án B — bỏ khoá nút:** cả hai luồng để nút **luôn bật**; khi bấm thiếu dữ liệu thì hiện lỗi inline và cuộn tới ô lỗi đầu tiên (`VAL-02`). Cần BA sửa `VAL-01`; NEED bỏ khoá nút.
- Cả hai phương án đều đòi NEED hiển thị được lỗi inline. Lưu ý khi chọn A: nếu chỉ khoá nút mà không có lỗi inline thì lặp lại đúng tình trạng `FE-301`.

**Hình ảnh mô tả:** đính kèm 2 ảnh — OFFER trống với nút "Đăng tin ngay" đang bật và lỗi `Chọn ít nhất 1 buổi` (`TC-ORD-050`); NEED nút "Tiếp theo" khoá không báo lỗi (`TC-ORD-063`)
