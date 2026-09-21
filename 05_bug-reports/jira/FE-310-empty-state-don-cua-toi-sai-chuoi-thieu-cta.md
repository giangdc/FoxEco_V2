---
bug_id: BUG-026
jira_project: FE
jira_issue_type: Bug
jira_key: FE-310
jira_url: https://foxproject.atlassian.net/browse/FE-310
module: HOME - Trang chủ
bug_desc: Empty state Đơn của tôi sai chuỗi, thiếu CTA và icon
priority: P3
severity: Low
components: [HOME]
affects_versions: [v1.1]
traceability: TC-HOME-027 → SC-HOME-026 → REQ-HOME-012
status: To Do
effect: Usability
defect_type: Interface
platform: App
test_method: Manual
test_round: R1
reject_number:
resolution:
reason_for_wontfix:
attachments: [08_test-runs/vibe/VR-014-HOME-2026-09-21/screenshots/TC-HOME-027__step3-FAIL-empty-state-chua-co-don-nao-thieu-cta-tao-don-gui-hang.png, 08_test-runs/vibe/VR-014-HOME-2026-09-21/screenshots/TC-HOME-028__step3-BLOCKED-cong-dong-325-don-khong-phai-0-he-thong-da-co-don-hoan-thanh.png]
reported_by: GiangDC2
reported_on: 2026-09-21
assignee: Tuanvm37
due_date:
last_synced: 2026-09-21
---

# [HOME - Trang chủ] - Empty state Đơn của tôi sai chuỗi, thiếu CTA và icon

> Jira: [FE-310](https://foxproject.atlassian.net/browse/FE-310) · Status: To Do · Assignee: Tuanvm37

<!-- jira:description:start — copy nguyên khối dưới đây vào field Description của Jira -->

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: CBNV `Nguyễn Thị Thanh Thủy` (`stag_thuyntt22@`) — tài khoản "sạch": 0 đơn đang chạy, 0 đóng góp
- Trình duyệt / Thiết bị: emulator-5554 (Android 13, 1080×2400), UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Tài khoản không có đơn nào đang chạy (hero `0 · Chưa có đóng góp nào`).

**Steps:**

1. Đăng nhập app FoxPro bằng tài khoản không có đơn → menu "Chức năng" → nhấn icon FoxEco
2. Mở tab "Trang chủ"
3. Quan sát section "Đơn của tôi"

**Expected result:**

- Section "Đơn của tôi" **vẫn hiển thị**, bên trong có **icon nét mảnh**, dòng **"Bạn chưa có đơn nào đang chạy"** và nút CTA **"Tạo đơn gửi hàng"** *(TC-HOME-027; PRD `DOC-v1.1-01` §8.17.1, `EMP-02`; BA chốt hiển thị ở `C-HOME-05`)*.

**Actual result:**

- Section vẫn hiển thị *(đúng)*, nhưng bên trong chỉ có dòng **"Chưa có đơn nào"** — sai chuỗi `EMP-02`; **không có** nút "Tạo đơn gửi hàng"; **không thấy** icon.
- Đối chiếu cùng màn: empty state của "Tin mới" hiển thị đúng chuỗi `EMP-01` ⇒ chỉ `EMP-02` lệch.

**Hình ảnh mô tả:**

![BUG-026-01](../../08_test-runs/vibe/VR-014-HOME-2026-09-21/screenshots/TC-HOME-027__step3-FAIL-empty-state-chua-co-don-nao-thieu-cta-tao-don-gui-hang.png)

<!-- jira:description:end -->

## Status History

| Ngày | Status | Ghi chú | Ref |
|---|---|---|---|
| 2026-09-21 | Pushed | Soạn từ `TC-HOME-027` FAIL (VR-014); push Jira `FE-310`, assign Tuanvm37, đính kèm ảnh | |

## Ghi chú nội bộ (không push Jira) — 🔎 phần để QC review

- **Có phải bug thật không? — CÓ THỂ, tin cậy trung bình-cao:** app hiện `Chưa có đơn nào` (chuỗi ngắn kiểu v1.0?) trong khi PRD v1.1 chốt `EMP-02`. Nếu BA/dev xác nhận bản build STG chưa cập nhật `EMP-02` thì vẫn là bug "chưa làm theo PRD". Nếu BA đổi ý về chuỗi thì sửa `TC-HOME-027`.
- Tài khoản test "sạch" = `stag_thuyntt22@` (0 đơn · 0 đóng góp) — dùng lại được để tái hiện; ⚠️ đừng dùng cho việc khác trước.
- `defect_type: Interface` là lựa chọn của người soạn (lệch spec, không phải lỗi logic) — QC chỉnh nếu board dùng giá trị khác.
- Mức đề xuất: P3 · Low.
