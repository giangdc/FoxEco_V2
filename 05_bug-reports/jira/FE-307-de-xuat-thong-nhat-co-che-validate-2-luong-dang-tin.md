---
bug_id: BUG-016
jira_project: FE
jira_issue_type: Bug
jira_key: FE-307
jira_url: https://foxproject.atlassian.net/browse/FE-307
module: ORD - Đăng tin & Quản lý tin
bug_desc: Đề xuất thống nhất cơ chế validate giữa 2 luồng đăng tin
priority: P4
severity: Suggest
components: [ORD]
affects_versions: [v1.1]
traceability: TC-ORD-050 → SC-ORD-047 → REQ-ORD-020
status: To Do
effect: Usability
defect_type:
platform: App
test_method: Manual
test_round: R1
reject_number:
resolution:
reason_for_wontfix:
attachments: [08_test-runs/vibe/VR-004-ORD-2026-09-18/screenshots/TC-ORD-050__step8-FAIL-offer-nut-gui-enabled-khi-thieu-du-lieu.png, 08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-063__step6-FAIL-chan-nhung-khong-co-thong-bao-loi.png]
reported_by: GiangDC2
reported_on: 2026-09-21
assignee: Tuanvm37
due_date:
last_synced: 2026-09-21
---

# [Suggest][ORD - Đăng tin & Quản lý tin] - Đề xuất thống nhất cơ chế validate giữa 2 luồng đăng tin

> Jira: [FE-307](https://foxproject.atlassian.net/browse/FE-307) · Status: To Do · `Suggest` do QC GiangDC2 quyết định (2026-09-21)

<!-- jira:description:start — copy nguyên khối dưới đây vào field Description của Jira -->

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: CBNV `Đặng Châu Giang`, MNV 00131946 (tài khoản A) — vai SENDER
- Trình duyệt / Thiết bị: emulator-5554, Android, UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Đề xuất:** thống nhất cách xử lý khi form thiếu dữ liệu giữa hai luồng đăng tin **"Tôi cần gửi hàng"** (wizard) và **"Tôi nhận giao hàng"** (form 1 trang). Hiện hai luồng dùng hai cơ chế khác nhau cho cùng một tình huống, và cả hai đều lệch so với đặc tả ở một điểm.

**Hiện trạng:**

| | "Tôi cần gửi hàng" (NEED) | "Tôi nhận giao hàng" (OFFER) |
| --- | --- | --- |
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
- `VAL-02` (`§D8.3 L393`, `SC-ORD-048`): _"Lỗi hiện ngay dưới ô nhập khi rời ô (on blur), không dùng popup; cuộn tới ô lỗi đầu tiên khi bấm submit"_. OFFER làm được một phần; NEED chưa làm (`FE-301`).

**Đề xuất hướng thống nhất (BA/Dev chọn):**

- **Phương án A — theo `VAL-01`:** cả hai luồng **khoá nút** cho tới khi đủ dữ liệu, **kèm lỗi inline tại từng trường** (`VAL-02`) để người dùng biết thiếu gì. OFFER chuyển sang khoá nút; NEED bổ sung lỗi inline (đang theo dõi ở `FE-301`).
- **Phương án B — bỏ khoá nút:** cả hai luồng để nút **luôn bật**; khi bấm thiếu dữ liệu thì hiện lỗi inline và cuộn tới ô lỗi đầu tiên (`VAL-02`). Cần BA sửa `VAL-01`; NEED bỏ khoá nút.
- Cả hai phương án đều đòi NEED hiển thị được lỗi inline. Lưu ý khi chọn A: nếu chỉ khoá nút mà không có lỗi inline thì lặp lại đúng tình trạng `FE-301`.

**Hình ảnh mô tả:** đính kèm 2 ảnh — OFFER trống với nút "Đăng tin ngay" đang bật và lỗi `Chọn ít nhất 1 buổi` (`TC-ORD-050`); NEED nút "Tiếp theo" khoá không báo lỗi (`TC-ORD-063`)

<!-- jira:description:end -->

## Status History

| Ngày | Status | Ghi chú | Ref |
|---|---|---|---|
| 2026-09-21 | Draft | Soạn từ `TC-ORD-050` FAIL (VR-004). QC quyết định log dạng `Suggest` (severity 0) để đồng bộ 2 luồng, thay vì log là lỗi của OFFER | VR-004-ORD-2026-09-18 |
| 2026-09-21 | Draft | Thử push (severity `0`, không Defect Type, assignee Tuanvm37) → Jira từ chối: `Field Defect Type is required`. Chờ QC chọn: điền Defect Type hay đổi severity | — |
| 2026-09-21 | To Do | Push Jira → FE-307 theo lựa chọn của QC: giữ `Suggest` (severity 0), **điền Defect Type = `Requirement`** vì board bắt buộc. QC sẽ tự xem và chỉnh tay trên Jira. Assignee Tuanvm37, Priority Low | — |

## Ghi chú nội bộ (không push Jira)

- **Vì sao là `Suggest`:** OFFER lệch chữ `VAL-01` nhưng hành vi (chặn + lỗi inline) **tốt hơn** NEED. Log như lỗi của OFFER dễ khiến Dev "sửa OFFER cho giống NEED" — ngược hướng (VR-004 đã cảnh báo). Log như đề xuất thống nhất thì để Dev/BA chọn hướng.
- **Quan hệ với `FE-301`:** `FE-301` lo phần NEED thiếu lỗi inline. Đề xuất này lo phần còn lại: khác biệt trạng thái nút giữa 2 luồng. Nếu `FE-301` được sửa bằng cách thêm lỗi inline cho NEED thì chỉ còn khác biệt về nút.
- **Theo luật `Suggest` của skill:** H1 có tiền tố `[Suggest]`; `defect_type` để **trống**; `traceability` không có `FAIL-`/`RUN-`; không tính vào KPI Critical/Major.
- ⚠️ **Rủi ro khi push:** board `FE` có option severity `0` (đã kiểm metadata 2026-09-21), nhưng tiền lệ `BUG-007`/`FE-297` ghi *"đổi từ `Suggest` sang `Low` do board bắt buộc Defect Type lúc tạo issue"*. Nếu Jira từ chối vì thiếu Defect Type thì QC phải chọn: điền một loại (vd `Requirement`) — mâu thuẫn quy tắc "Suggest không có defect_type" và làm bảng Defect Type của Report Test lệch — hoặc đổi sang `Low`. Cần quyết định lúc push, mình sẽ thử tạo không có Defect Type trước.
- Khi push: tiêu đề theo convention Jira `[Suggest][TC_04 - Đăng tin] …`; nhớ `Parent = FE-1`, `Fix versions = V1.0`, `Test Round = 1`, Severity option `0` (id `10360`), Priority Low.

- **Đã push (2026-09-21):** front-matter `defect_type` vẫn để trống theo luật `Suggest`, nhưng **trên Jira Defect Type = `Requirement`** (board bắt buộc). Bảng Defect Type của Report Test sẽ tính thêm 1 dòng `Requirement` từ issue này — QC đã chấp nhận.
