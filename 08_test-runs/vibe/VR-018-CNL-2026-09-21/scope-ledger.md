# Scope Ledger — VR-018 — module CNL — SCOPE_TOTAL = 22 TC

> Seed từ: `coverage/coverage-CNL.md` — **chưa tồn tại trước phiên** ⇒ tạo mới (trước phiên: 0/22).
> Tập chạy phiên này: **13 TC v1.1** theo yêu cầu QC · 1 lô · 3 tài khoản (`anhdc4` A · `anhptm17` B · `giangdc2` C).
> Kết quả phiên: **13/13 có verdict cuối** (**9P / 2F / 2B** — sau đính chính nội dung + follow-up chụp bù evidence `TC-CNL-010`/`017`/`018`/`019` 2026-09-22, xem khối cuối file).

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-CNL-001 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi VR-018 (QC chỉ yêu cầu TC v1.1) |
| TC-CNL-002 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi VR-018 (QC chỉ yêu cầu TC v1.1) |
| TC-CNL-003 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi VR-018. (Quan sát kèm VR-018: ô trống thì `cancel-order-confirm` `enabled=false`) |
| TC-CNL-004 | ❌ FAIL | 1 | run này | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-004__step4-FAIL-nut-xac-nhan-khoa-nhung-khong-co-loi-duoi-o-ly-do.png` |
| TC-CNL-005 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi VR-018. (Quan sát kèm VR-018: cả 3 vai đều không có nút huỷ ở `Đang giao`) |
| TC-CNL-006 | ✅ PASS | 1 | run này | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-006__verify-nguoi-gui-bam-bao-cao-su-co-mo-luong-bao-su-co.png` |
| TC-CNL-007 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi VR-018 (QC chỉ yêu cầu TC v1.1) |
| TC-CNL-008 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi VR-018 (QC chỉ yêu cầu TC v1.1) |
| TC-CNL-009 | ❌ FAIL | 1 | run này | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-009__step8-FAIL-log-nguoi-gui-huy-ghi-nhan-da-huy-nhan-don-khong-co-vai.png` |
| TC-CNL-010 | ✅ PASS *(đính chính nội dung 2026-09-22; evidence chụp bù follow-up 2026-09-22)* | 1 | run này + follow-up | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-010__verify-lich-su-huy-nhan-giu-nguyen-sau-dinh-chinh.png` |
| TC-CNL-011 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi VR-018; cần 3 thiết bị |
| TC-CNL-012 | ✅ PASS | 1 | run này | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-012__verify-5-dau-cach-nut-xac-nhan-vo-hieu-hoa.png` |
| TC-CNL-013 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi VR-018 (QC chỉ yêu cầu TC v1.1) |
| TC-CNL-014 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi VR-018 (header fragment v1.1 quên liệt kê TC này) |
| TC-CNL-015 | ✅ PASS | 1 | run này | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-015__verify-nguoi-van-chuyen-bam-bao-cao-su-co-mo-luong-bao-su-co.png` |
| TC-CNL-016 | ✅ PASS | 1 | run này | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-016__verify-nguoi-nhan-bam-bao-cao-su-co-mo-luong-bao-su-co.png` |
| TC-CNL-017 | ✅ PASS *(đính chính nội dung 2026-09-22; evidence chụp bù follow-up 2026-09-22)* | 1 | run này + follow-up | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-017__verify-vai-nguoi-gui-chi-co-bao-cao-su-co.png` |
| TC-CNL-018 | ✅ PASS *(đính chính nội dung 2026-09-22; evidence chụp bù follow-up 2026-09-22)* | 1 | run này + follow-up | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-018__verify-vai-nguoi-van-chuyen-bao-cao-su-co-va-duong-giao-hang.png` |
| TC-CNL-019 | ✅ PASS *(đính chính nội dung 2026-09-22; evidence chụp bù follow-up 2026-09-22)* | 1 | run này + follow-up | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-019__verify-vai-nguoi-nhan-chi-co-bao-cao-su-co.png` |
| TC-CNL-020 | 🚫 BLOCKED | 1 | run này | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-020__step1-BLOCKED-khong-dung-duoc-don-su-co-van-dang-giao.png` |
| TC-CNL-021 | 🚫 BLOCKED | 1 | run này | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-021__step2-BLOCKED-popup-lay-hang-dang-mo-o-phien-b-khong-co-phien-a-song-song.png` |
| TC-CNL-022 | ✅ PASS | 1 | run này | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-022__verify-trang-ca-nhan-khong-co-be-mat-admin.png` |

**Lô 1 xong · đã chạy 13/13 TC v1.1 · module: 13/22 có verdict cuối, còn nợ 9 (9 CARRIED NOT_RUN).**

## 🔁 Đính chính 2026-09-22 — nội dung `TC-CNL-017`/`018`/`019`/`010` đổi ❌ FAIL → ✅ PASS (QC chốt)

- **`017`/`018`/`019`** — nội dung đổi **❌ FAIL → ĐẠT**: TC viết sai giả định nút "Yêu cầu hoàn hàng" — không tồn tại trong PRD (`AC-25.2.01` §6.2 trang 27 · `BR11-04` §8.11.1 trang 45 · `FR09` §8.9 trang 43, đã đọc trực tiếp PDF `00_input/v1.1/FoxEco PRD v1.0 - Gui Hang.pdf`). PRD chỉ đảm bảo ở mức trạng thái; luồng hoàn hàng thật là **Người vận chuyển** bấm xác nhận tại điểm giao → màn "Xử lý đơn hàng" → chọn "Cầm hàng về". Expected 3 TC đã sửa theo đúng luồng. Draft `BUG-033` **đã xoá**.
- **`010`** — nội dung đổi **❌ FAIL → ĐẠT**: vế "ghi tên thay vì vai" được QC chấp nhận — app ghi tên người thực hiện nhất quán ở mọi dòng LỊCH SỬ, không riêng dòng huỷ. Expected đã sửa. Draft `BUG-035` **đã xoá**.
- **`009` vẫn ❌ FAIL** — vế "tên thay vai" cũng được chấp nhận như `010`, nhưng vế **nhãn hành động sai** ("Đã huỷ nhận đơn" cho hành động Người gửi huỷ đơn) là lỗi độc lập, chưa được chấp nhận. Giữ `BUG-034` (chờ QC push Jira).
- File Expected đã sửa: `03_test-cases/v1.1/fragments/TC-CNL-v1.1.md` + `03_test-cases/v1.1/TC-MASTER-v1.1.xlsx` + `03_test-cases/TC-MASTER-LATEST.xlsx`.

## 🔁 Follow-up 2026-09-22 — chụp bù evidence đúng slot `__verify`, chốt verdict PASS

⚠️ **Ảnh gốc không đủ cho PASS:** ảnh duy nhất của cả 4 TC ở phiên gốc mang tên slot `__step*-FAIL` (chụp lúc đang chấm FAIL theo Expected cũ). Gate `verify_evidence.py` bắt buộc verdict `PASS` phải có ảnh slot `__verify`. ⛔ **KHÔNG đổi tên/copy ảnh để né gate** (= fabrication).

✅ **Đã chụp bù trong phiên follow-up cùng ngày** — đăng nhập lại đủ 3 vai (A `stag_anhdc4@` · B `stag_anhptm17@` · C `stag_giangdc2@`), đọc lại state hiện tại của O2 (vẫn `IN_TRANSIT`/Đang giao, không đổi trạng thái đơn) và chụp 4 ảnh đúng slot `__verify`:
- `TC-CNL-017__verify-vai-nguoi-gui-chi-co-bao-cao-su-co.png`
- `TC-CNL-010__verify-lich-su-huy-nhan-giu-nguyen-sau-dinh-chinh.png`
- `TC-CNL-018__verify-vai-nguoi-van-chuyen-bao-cao-su-co-va-duong-giao-hang.png`
- `TC-CNL-019__verify-vai-nguoi-nhan-chi-co-bao-cao-su-co.png`

Không cần lặp lại thao tác huỷ/ghép nào vì log LỊCH SỬ bất biến (`BR11-03`) và ma trận nút của `Đang giao` không đổi theo thời gian. Cả 4 TC verdict cuối: **✅ PASS**. Ảnh cũ giữ nguyên, không xoá — vẫn được trích làm hồ sơ lúc chạy gốc. Gate `verify_evidence.py` chạy lại sau follow-up: **GATE PASS**.
