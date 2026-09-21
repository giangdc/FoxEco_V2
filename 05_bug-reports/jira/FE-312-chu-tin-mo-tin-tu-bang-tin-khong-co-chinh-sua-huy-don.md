---
bug_id: BUG-028
jira_project: FE
jira_issue_type: Bug
jira_key: FE-312
jira_url: https://foxproject.atlassian.net/browse/FE-312
module: FEED - Bảng tin & Chi tiết tin
bug_desc: Chủ tin mở tin từ Bảng tin không có Chỉnh sửa/Huỷ đơn
priority: P3
severity: Low
components: [FEED]
affects_versions: [v1.1]
traceability: TC-FEED-005 → SC-FEED-005 → REQ-FEED-003
status: To Do
effect: Usability
defect_type: Requirement
platform: App
test_method: Manual
test_round: R1
reject_number:
resolution:
reason_for_wontfix:
attachments: [08_test-runs/vibe/repro/RP-FEED-chu-tin-bang-tin-khong-theo-doi-don-2026-09-21/_recon__hoat-dong-mo-theo-doi-don-co-chinh-sua-huy-don.png, 08_test-runs/vibe/repro/RP-FEED-chu-tin-bang-tin-khong-theo-doi-don-2026-09-21/_recon__bang-tin-tin-cua-ban-co-badge.png, 08_test-runs/vibe/repro/RP-FEED-chu-tin-bang-tin-khong-theo-doi-don-2026-09-21/_recon__bang-tin-mo-chi-tiet-tin-khong-co-chinh-sua-huy-don.png]
reported_by: GiangDC2
reported_on: 2026-09-21
assignee: NhungPTH13
due_date:
last_synced: 2026-09-21
---

# [FEED - Bảng tin & Chi tiết tin] - Chủ tin mở tin từ Bảng tin không có Chỉnh sửa/Huỷ đơn

> Jira: [FE-312](https://foxproject.atlassian.net/browse/FE-312) · Status: To Do · Assignee: NhungPTH13 *(gán tự động bởi Jira, QC không chỉ định)*

<!-- jira:description:start — copy nguyên khối dưới đây vào field Description của Jira -->

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: CBNV `Đặng Châu Giang` (`stag_giangdc2@`) — vai người gửi (chủ tin)
- Trình duyệt / Thiết bị: emulator-5554 (Android 15, 1080×2400), UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Tài khoản A (chủ tin) đã đăng 1 tin NEED, đang ở trạng thái "Chờ ghép" (chưa có người vận chuyển nhận).

**Steps:**

1. Đăng nhập app FoxPro bằng tài khoản A → menu "Chức năng" → nhấn icon FoxEco
2. Cách 1: từ Trang chủ (mục "Đơn của tôi") hoặc tab "Hoạt động" → bấm vào tin vừa đăng → quan sát màn hình mở ra
3. Quay lại → chọn tab "Bảng tin" → tìm card tin của mình (có badge "Tin của bạn") → bấm vào → quan sát màn hình mở ra

**Expected result:**

- Cùng 1 tin, cùng trạng thái "Chờ ghép", dù vào từ Trang chủ, Hoạt động hay Bảng tin thì đều mở **cùng 1 màn hình**: màn "Theo dõi đơn" với nút **"Chỉnh sửa"** và **"Huỷ đơn"**, để chủ tin thao tác thuận tiện. *(Theo QC: người dùng cần thấy Chỉnh sửa/Huỷ đơn ngay khi mở tin của mình; cùng một trạng thái thì các nguồn vào khác nhau nên nhất quán.)*
- *Ghi chú: PRD v1.1 không quy định rõ hành vi này — sơ đồ điều hướng §7.1 (trang 30) tách `Bảng tin → Chi tiết tin` và `Đơn hàng → Theo dõi đơn`; `AC-12.2.01` (trang 20) chỉ nói mở tin của chính mình thì không có nút "Tôi mang giúp được".*

**Actual result:**

- Từ Trang chủ / Hoạt động → mở **"Theo dõi đơn"**: có stepper "Chờ ghép", dòng "Đang chờ người vận chuyển nhận đơn" và nút **"Chỉnh sửa"**, **"Huỷ đơn"**.
- Từ Bảng tin → mở **"Chi tiết tin"**: chỉ xem (ảnh, thông tin hàng, lộ trình, khung giờ, người gửi), **không có** "Chỉnh sửa", **không có** "Huỷ đơn", không có nút nào.
- ⇒ Chủ tin muốn sửa/huỷ phải thoát ra và tìm lại tin ở Hoạt động; cùng 1 tin nhưng khác nguồn vào lại ra 2 màn khác nhau.
- *(Trang chủ: theo QC báo; đã tự xác nhận đường Hoạt động cùng nguồn "Đơn của tôi".)*

**Hình ảnh mô tả:** xem 3 file đính kèm trên issue — `_recon__hoat-dong-mo-theo-doi-don-co-chinh-sua-huy-don.png` (Theo dõi đơn có Chỉnh sửa/Huỷ đơn) · `_recon__bang-tin-tin-cua-ban-co-badge.png` (card có badge "Tin của bạn") · `_recon__bang-tin-mo-chi-tiet-tin-khong-co-chinh-sua-huy-don.png` (Chi tiết tin, không có nút).

<!-- jira:description:end -->

## Status History

| Ngày | Status | Ghi chú | Ref |
|---|---|---|---|
| 2026-09-21 | Pushed | Push Jira `FE-312`, đính kèm 3 ảnh (id 31801–31803); Jira tự gán assignee `NhungPTH13` (mặc định của project). QC tự chỉnh Suggest/phân loại sau |  |
| 2026-09-21 | Open | QC GiangDC2 nêu; rà PRD (không có rule tường minh) + tái hiện; QC yêu cầu log & push, tự chỉnh phân loại (Suggest) trên Jira | RP-FEED-chu-tin-bang-tin-khong-theo-doi-don-2026-09-21 |

## Ghi chú nội bộ (không push Jira) — 🔎 phần để QC review

- **Không phải lỗi lệch spec:** PRD v1.1 **không có câu nào** quy định chủ tin bấm tin của mình ở Bảng tin phải mở Theo dõi đơn; hành vi hiện tại còn khớp `AC-12.2.01` + `TC-FEED-005/011`. Bug này là **đề xuất nhất quán UX** do QC nêu ⇒ `defect_type: Requirement`.
- **`severity: Low` là mặc định của người soạn** vì QC nói sẽ **tự chỉnh sang Suggest** trên Jira (AI không tự gán `Suggest` — `log.md §Severity Suggest`). Khi QC đổi sang `Suggest`: H1 cần tiền tố `[Suggest]`, `defect_type` để trống, traceability FAIL/RUN để trống (đã trống sẵn).
- Tái hiện **1 tin, 1 tài khoản**; đường Trang chủ chưa tự chạm (tin không nằm trong 5 đơn hiển thị).
- `assignee`: QC không chỉ định; **Jira tự gán `NhungPTH13`** (mặc định) — QC đổi nếu cần.
- Repro: `08_test-runs/vibe/repro/RP-FEED-chu-tin-bang-tin-khong-theo-doi-don-2026-09-21/report.md`.
