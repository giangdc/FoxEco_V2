---
bug_id: BUG-009
jira_project: FE
jira_issue_type: Bug
jira_key:
jira_url:
module: ORD - Đăng tin & Quản lý tin
bug_desc: Chặn sang bước sau nhưng không hiện lỗi ở trường thiếu
priority: P2
severity: Major
components: [ORD]
affects_versions: [v1.1]
traceability: TC-ORD-063 → SC-ORD-054 → REQ-ORD-006 · TC-ORD-064 → SC-ORD-052 → REQ-ORD-024 · TC-ORD-066 → SC-ORD-053 → REQ-ORD-024 · TC-ORD-083 → SC-ORD-063 → REQ-ORD-028 · TC-ORD-084 → SC-ORD-063 → REQ-ORD-028 · TC-ORD-077 → SC-ORD-060 → REQ-ORD-008
status: To Do
effect: Usability
defect_type: Interface
platform: App
test_method: Manual
test_round: R1
reject_number:
resolution:
reason_for_wontfix:
attachments: [08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-063__step6-FAIL-chan-nhung-khong-co-thong-bao-loi.png, 08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-064__step6-FAIL-chan-nhung-khong-co-thong-bao-loi.png, 08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-066__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png, 08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-083__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png, 08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-084__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png, 08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-077__step4-FAIL-khong-co-loi-dinh-dang.png]
reported_by: GiangDC2
reported_on: 2026-09-18
assignee:
due_date:
last_synced:
---

# [ORD - Đăng tin & Quản lý tin] - Chặn sang bước sau nhưng không hiện lỗi ở trường thiếu

> Jira: [chưa push] · Status: Open

<!-- jira:description:start — copy nguyên khối dưới đây vào field Description của Jira -->

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: CBNV `Đặng Châu Giang`, MNV 00131946 (tài khoản A) — vai SENDER
- Trình duyệt / Thiết bị: emulator-5554, Android, 1080x2400, UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Tài khoản A là CBNV có hồ sơ đầy đủ trên STG, đã đăng nhập host app FoxPro.
- Thư viện ảnh thiết bị có sẵn bộ ảnh mẫu `SEED-ORD-01` (dùng cho các nhánh cần tải ảnh).

**Steps:** *(luồng đại diện — nhánh thiếu ẢNH HÀNG, `TC-ORD-063`, P1)*

1. Đăng nhập app FoxPro → menu "Chức năng" → nhấn icon FoxEco
2. Nhấn "+ Đăng tin" → nhấn card "Tôi cần gửi hàng"
3. Chọn chip "Thấp (Dưới 1 triệu đ)" ở khối "GIÁ TRỊ HÀNG (ƯỚC TÍNH)"
4. Chọn chip "Dưới 5 kg (Nhẹ)" ở khối "TRỌNG LƯỢNG"
5. Chọn chip "Nhỏ · Cầm tay" ở khối "KÍCH THƯỚC"
6. Nhấn "Tiếp theo" khi **chưa tải ảnh nào**
7. Quan sát khối "ẢNH HÀNG" — tìm thông báo lỗi

**Expected result:**

- Wizard vẫn ở bước 1, không sang được bước 2, **và có thông báo lỗi ở khối "ẢNH HÀNG"**.
- Tương tự cho 5 nhánh validate còn lại: mỗi nhánh vừa chặn vừa **hiện lỗi tại đúng trường thiếu/sai** (bảng dưới).

**Actual result:**

- Vế **chặn** đúng ở cả 6 nhánh (nút "Tiếp theo" `enabled=false` / wizard giữ nguyên bước).
- Vế **báo lỗi SAI ở cả 6 nhánh**: không có thông báo lỗi nào xuất hiện. Người dùng bị khoá nút mà **không có bất kỳ dấu hiệu nào cho biết thiếu/sai ở đâu**.

| TC | Nhánh validate | Chặn? | Thông báo lỗi? | Kiểm chứng |
|---|---|---|---|---|
| `TC-ORD-063` **(P1)** | chưa tải ảnh nào | ✓ có | ✗ **không** | khối "ẢNH HÀNG" chỉ có dòng helper tĩnh |
| `TC-ORD-064` | chưa chọn TRỌNG LƯỢNG | ✓ có | ✗ **không** | nhãn khối + 3 chip hiển thị đúng, chỉ thiếu lỗi |
| `TC-ORD-066` | chưa chọn KÍCH THƯỚC | ✓ có | ✗ **không** | 3 chip hiển thị đúng, chỉ thiếu lỗi |
| `TC-ORD-083` | địa chỉ giao trùng hệt địa chỉ lấy | ✓ có | ✗ **không** | tìm text chứa "trùng" → NOT FOUND |
| `TC-ORD-084` | trùng, chỉ khác khoảng trắng đầu/cuối | ✓ có (có trim) | ✗ **không** | — |
| `TC-ORD-077` | email sai định dạng `stag_anhdc4@` | ✓ có | ✗ **không** | 3 ô tên/SĐT/địa chỉ vẫn trống (không tra danh bạ) — đúng; chỉ thiếu lỗi định dạng |

**Phạm vi ảnh hưởng:**

- 6 nhánh validate trải **cả bước 1 lẫn bước 2** của wizard NEED ⇒ người dùng có thể bị kẹt ở bất kỳ bước nào mà không biết lý do.
- Đây **không phải** hạn chế của framework hiển thị lỗi: app **CÓ** báo lỗi đúng ở 4 nhánh khác trong cùng màn — ảnh > 5MB (`TC-ORD-068`), chưa chọn buổi (`TC-ORD-058`: *"Chọn ít nhất 1 buổi"*), khoảng ngày > 7 (`TC-ORD-057`), email ngoài tên miền (`TC-ORD-078`) ⇒ là **bỏ sót ở 6 nhánh**, không phải thiếu cơ chế.

**Căn cứ:** `BR01-01` (*"Thiếu ảnh thì chặn sang bước 2"*) · `BR01-02` (*"không cho để trống"*) · `AC-03.1.02` · `AC-04.2.01` · `§8.1.4` (*"Địa chỉ giao phải khác địa chỉ lấy"*) · `VAL-03` (có trim).

**Hình ảnh mô tả:**

![BUG-009-01](../../08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-063__step6-FAIL-chan-nhung-khong-co-thong-bao-loi.png)

![BUG-009-02](../../08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-064__step6-FAIL-chan-nhung-khong-co-thong-bao-loi.png)

![BUG-009-03](../../08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-066__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png)

![BUG-009-04](../../08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-083__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png)

![BUG-009-05](../../08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-084__step5-FAIL-chan-nhung-khong-co-thong-bao-loi.png)

![BUG-009-06](../../08_test-runs/vibe/VR-002-ORD-2026-09-18/screenshots/TC-ORD-077__step4-FAIL-khong-co-loi-dinh-dang.png)

<!-- jira:description:end -->

## Status History

| Ngày | Status | Ghi chú | Ref |
|---|---|---|---|
| 2026-09-18 | Open | Log từ 6 TC FAIL cùng 1 nguyên nhân — ứng viên bug **B1** của VR-002 | VR-002-ORD-2026-09-18 |

## Ghi chú nội bộ (không push Jira)

- **Vì sao gộp 6 TC vào 1 bug:** cùng một nguyên nhân (nhánh validate chạy nhưng không render thông báo lỗi), cùng một wizard. Tách 6 bug sẽ tạo 6 luồng fix cho 1 nguyên nhân — `vibe-report` VR-002 đã chốt gộp.
- **`severity: Major`** (report đề xuất *High* — enum local không có `High`, `High` là Priority Jira). Có 1 TC **P1** trong nhóm (`TC-ORD-063`); nếu QC muốn nâng `priority` lên `P1` thì sửa trước khi push — AI không tự quyết.
- **`effect: Usability` / `defect_type: Interface`:** rule nghiệp vụ được **thi hành đúng**, phần hỏng là phản hồi cho người dùng. Nếu QC coi "hiện lỗi" là yêu cầu chức năng chưa làm thì đổi sang `Functionality`/`Logic`.
- ⛔ **Không được sửa Expected của 6 TC này theo app để làm xanh** — chúng là bằng chứng của bug (ghi rõ ở `vibe-report` VR-002).
- **Chưa push Jira** theo yêu cầu QC 2026-09-18. Khi push: `/log-bug --push-jira BUG-009` (nhớ `Parent = FE-1`, `Fix versions = V1.0`, `Test Round = 1`).
