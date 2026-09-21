# Coverage — module FEED — SCOPE_TOTAL = 15 TC

> Sổ cái TÍCH LŨY xuyên run cho module **FEED** (Bảng tin & Chi tiết tin) — scope = **v1.1 (5 TC) + CARRIED v1.0 (10 TC)**, cùng quy ước với `coverage-ASN.md`.
> **Cập nhật lần cuối: VR-016 (2026-09-21)** · Nguồn scope: `03_test-cases/v1.1/fragments/TC-FEED-v1.1.md` + `03_test-cases/v1.0/fragments/TC-FEED-v1.0.md`
> **Tổng: có verdict cuối 5/15 · CÒN NỢ 10** (10 NOT_RUN + 0 NOT_EVIDENCED)
> Verdict hợp lệ: ✅ PASS · ❌ FAIL · 🚫 BLOCKED · ⚠️ NOT_EVIDENCED · ⏳ NOT_RUN · ⛔ N-A

> 🟢 **2026-09-21 (VR-016, retest cùng ngày) — `TC-FEED-009` BLOCKED → ✅ PASS.** QC cấp 2 địa chỉ cụ thể có toạ độ hợp lệ (`FTEL An Giang Trần Hưng Đạo - Long Xuyên` ↔ `FTEL An Giang VPGD Bình Hòa`); tự tạo 1 tin NEED qua wizard Đăng tin bằng 2 địa chỉ này → Chi tiết tin hiện **bản đồ Google Maps thật, có vẽ tuyến cam + "17.2 km · 15 phút"**. Đồng thời phát hiện: `location_address_catalog.xlsx` (`DOC-v1.1-04`) **không đáng tin** để suy đoán văn phòng nào có toạ độ hợp lệ — 100% (399/399) dòng đều gắn `coordinate_status = MISSING` **kể cả 2 địa chỉ QC vừa cấp** (đều có lat/lng hợp lệ nhưng app vẫn render bản đồ thật) ⇒ phải kiểm THẬT qua app, không tra file.
> ✅ **ĐÍNH CHÍNH 2026-09-21 (retest theo yêu cầu QC) — `TC-FEED-007` FAIL → PASS.** Login `stag_anhdc4@fpt.com`, mở tin của `Đặng Châu Giang` (fixture `FTEL An Giang Trần Hưng Đạo - Long Xuyên` ↔ `FTEL An Giang VPGD Bình Hòa`) → đủ 4/4 sub-clause (lộ trình + bản đồ thật "17.2 km · 15 phút", khung giờ, người gửi đầy đủ không SĐT, CTA có). Xác nhận FAIL lần 1 đúng là do chọn nhầm data (`FTEL SG09`/`SG07` thiếu toạ độ), không phải bug.
> 🔍 **Phát hiện kèm (theo yêu cầu QC kiểm thêm):** với `anhdc4`, CTA "Tôi mang giúp được" **vắng mặt có chọn lọc** ở đúng 1 tin (`FTEL SG09→SG07`, người gửi Nguyễn Thị Thanh Thủy) trong khi 2 tin khác vẫn có CTA bình thường — khớp rule `OPR-05`/`SC-FEED-012` (người nhận được khai không thấy CTA). Không phải bug, nhưng là data hữu ích cho `TC-FEED-012` (còn `⏳ NOT_RUN`).
> ✅ **ĐÍNH CHÍNH 2026-09-21 (QC review `BUG-029`) — `TC-FEED-015` FAIL → PASS, `BUG-029` rút lại.** QC chấp nhận hành vi hiện tại của app (chỉ hiện dòng cảnh báo text, không khung placeholder, không "0km") là đúng — **không phải bug**. Expected Result của `TC-FEED-015` đã sửa lại theo app trong fragment + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx` (Title/Steps/số lượng TC giữ nguyên, đúng `§10.5`). `BUG-029` đã xoá khỏi `draft/`, không push Jira. Chi tiết: `VR-016-FEED-2026-09-21/vibe-log.md`.
> 🔵 **Phạm vi VR-016 do QC chỉ định:** chỉ 5 TC thuộc v1.1 (`002/007/009/013/015`) — 10 TC carried từ v1.0 chưa chạy trong phiên này (không phải hết sức phiên, mà là ngoài phạm vi được yêu cầu).

## Tiến độ theo run

| Run | Ngày | Tier | TC chạy trong run | Verdict thu được |
|-----|------|------|-------------------|------------------|
| VR-016 | 2026-09-21 | vibe-test | 5 (`002` `007` `009` `013` `015`) | 4P / 0F / 1B *(`009` BLOCKED→PASS retest; `015` FAIL→PASS sau khi QC sửa Expected theo app; `007` FAIL→PASS retest với account `anhdc4` + data hợp lệ)* |

## Chi tiết từng TC

| Testcase ID | Verdict | Scenario ID | Priority | Title | Run | Evidence | Ghi chú |
|---|---|---|---|---|---|---|---|
| TC-FEED-001 | ⏳ NOT_RUN | SC-FEED-001 | P2 | Check Bảng tin hiển thị tin NEED cộng đồng và không có tin OFFER | — | — | **Lý do:** ngoài phạm vi VR-016 (chỉ chạy 5 TC thuộc v1.1 theo yêu cầu QC) — TC carried nguyên trạng từ v1.0, chưa test lại |
| TC-FEED-002 | ✅ PASS | SC-FEED-002 | P2 | Check card tin ở Bảng tin đủ thành phần và không có nút CTA | VR-016 | `VR-016-FEED-2026-09-21/screenshots/TC-FEED-002__verify-card0-no-cta.png` | |
| TC-FEED-003 | ⏳ NOT_RUN | SC-FEED-003 | P3 | Check card tin do chính tài khoản đăng có badge "Tin của bạn" | — | — | **Lý do:** ngoài phạm vi VR-016 |
| TC-FEED-004 | ⏳ NOT_RUN | SC-FEED-004 | P3 | Check card tin do tài khoản khác đăng không có badge "Tin của bạn" | — | — | **Lý do:** ngoài phạm vi VR-016 |
| TC-FEED-005 | ⏳ NOT_RUN | SC-FEED-005 | P2 | Check nhấn card ở Bảng tin mở Chi tiết tin của đúng tin | — | — | **Lý do:** ngoài phạm vi VR-016 |
| TC-FEED-006 | ⏳ NOT_RUN | SC-FEED-006 | P2 | Check phần trên Chi tiết tin hiển thị ảnh, loại hàng, giá trị, ghi chú | — | — | **Lý do:** ngoài phạm vi VR-016 |
| TC-FEED-007 | ✅ PASS | SC-FEED-007 | P2 | Check phần dưới Chi tiết tin đủ lộ trình, khung giờ, tên người gửi và CTA | VR-016 | `VR-016-FEED-2026-09-21/screenshots/TC-FEED-007__verify-anhdc4-bottom-with-cta.png` | Đổi FAIL→PASS 2026-09-21: retest account `anhdc4` + tin của Giang (data hợp lệ) → đủ 4/4 sub-clause. FAIL lần 1 xác nhận do chọn nhầm data (`FTEL SG09/SG07` thiếu toạ độ). Kèm phát hiện: CTA vắng chọn lọc theo tin, khớp `OPR-05`/`SC-FEED-012` — data hữu ích cho `TC-FEED-012` |
| TC-FEED-008 | ⏳ NOT_RUN | SC-FEED-008 | P3 | Check tin đăng không kèm ảnh hiển thị ảnh mặc định và layout không vỡ | — | — | **Lý do:** ngoài phạm vi VR-016 |
| TC-FEED-009 | ✅ PASS | SC-FEED-009 | P3 | Check khung bản đồ ở Chi tiết tin là ảnh tĩnh có vẽ tuyến thật | VR-016 | `VR-016-FEED-2026-09-21/screenshots/TC-FEED-009__verify-real-map-route.png` | Retest cùng ngày: tự tạo tin NEED với `FTEL An Giang Trần Hưng Đạo - Long Xuyên` ↔ `FTEL An Giang VPGD Bình Hòa` (2 địa chỉ QC cấp) → bản đồ Google Maps thật + "17.2 km · 15 phút". Lần chạy đầu BLOCKED (ảnh `__step2-BLOCKED-no-valid-coord-office.png` giữ làm hồ sơ) do 5 tin có sẵn đều thiếu toạ độ |
| TC-FEED-010 | ⏳ NOT_RUN | SC-FEED-010 | P1 | Check Chi tiết tin ở "Chờ ghép" không hiển thị SĐT người gửi | — | — | **Lý do:** ngoài phạm vi VR-016 — lưu ý: dự kiến FAIL theo `CHANGELOG.md §3 Nợ #1` (bug đã biết, chưa log), viết theo rule không theo app |
| TC-FEED-011 | ⏳ NOT_RUN | SC-FEED-011 | P1 | Check chủ tin không thấy nút "Tôi mang giúp được" trên tin của mình | — | — | **Lý do:** ngoài phạm vi VR-016 — lưu ý: dự kiến FAIL theo `CHANGELOG.md §3 Nợ #1` (bug đã biết, chưa log) |
| TC-FEED-012 | ⏳ NOT_RUN | SC-FEED-012 | P2 | Check người nhận được khai không thấy nút "Tôi mang giúp được" | — | — | **Lý do:** ngoài phạm vi VR-016 |
| TC-FEED-013 | 🚫 BLOCKED | SC-FEED-013 | P3 | Check empty state Bảng tin đúng text và chỉ 1 danh sách không tab | VR-016 | `VR-016-FEED-2026-09-21/screenshots/TC-FEED-013__step1-BLOCKED-precondition-khong-rong.png` | Bảng tin là danh sách cộng đồng toàn hệ thống, hiện có ≥5 tin Chờ ghép (gồm fixture của module ASN) — cần dev/QA dọn môi trường riêng, AI không có quyền/không nên tự xoá dữ liệu chung |
| TC-FEED-014 | ⏳ NOT_RUN | SC-FEED-014 | P3 | Check nhấn quay lại ở Chi tiết tin về Bảng tin giữ vị trí cuộn | — | — | **Lý do:** ngoài phạm vi VR-016 |
| TC-FEED-015 | ✅ PASS | SC-FEED-015 | P3 | Check khung bản đồ hiện placeholder và 0km khi văn phòng thiếu toạ độ | VR-016 | `VR-016-FEED-2026-09-21/screenshots/TC-FEED-015__verify-accepted-behavior.png` | Đổi FAIL→PASS 2026-09-21: QC chấp nhận hành vi hiện tại (dòng cảnh báo text, không khung, không "0km") — Expected Result đã sửa theo app. `BUG-029` rút lại, không push Jira |

## Tổng hợp

| Verdict | Số | TC |
|---|---|---|
| ✅ PASS | 4 | `TC-FEED-002` · `TC-FEED-007` (retest account `anhdc4` + data hợp lệ) · `TC-FEED-009` (retest với data QC cấp) · `TC-FEED-015` (Expected sửa theo app, QC chấp nhận) |
| ❌ FAIL | 0 | — |
| 🚫 BLOCKED | 1 | `TC-FEED-013` (precondition cần dọn môi trường cộng đồng) |
| ⚠️ NOT_EVIDENCED | 0 | — |
| ⏳ NOT_RUN | 10 | `TC-FEED-001` `003` `004` `005` `006` `008` `010` `011` `012` `014` (carried v1.0, ngoài phạm vi VR-016) |
| ⛔ N-A | 0 | — |
| **Tổng** | **15** | |

**Có verdict cuối: 5/15 · CÒN NỢ: 10** ⇒ §8 = **PARTIAL**.

> 🟢 **Cả 5 TC v1.1 trong phạm vi VR-016 đã xong: 4 PASS + 1 BLOCKED (`013`, chờ dev/QA — không phải nợ kiểm thử).** Không còn TC v1.1 nào cần hành động thêm của QC.
> 🔍 Phát hiện phụ (không phải TC riêng): CTA "Tôi mang giúp được" vắng mặt chọn lọc theo tin (khớp `OPR-05`/`SC-FEED-012`) — dữ liệu hữu ích khi chạy `TC-FEED-012` (còn `⏳ NOT_RUN`).
> 🟡 10 TC còn nợ là **carried nguyên trạng từ v1.0**, chưa từng vibe-test lần nào (không riêng gì VR-016) — chạy tiếp bằng `/vibe-test --module FEED` (không giới hạn v1.1) khi QC muốn phủ nốt.
