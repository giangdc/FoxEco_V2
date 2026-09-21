# Coverage — module ACT — SCOPE_TOTAL = 18 TC

> Sổ cái TÍCH LŨY xuyên run cho module **ACT** (Hoạt động — Đơn của tôi) — scope = **v1.1 (10 TC: 6 MODIFIED + 4 NEW)** + **CARRIED v1.0 (8 TC)**, cùng quy ước với `coverage-FEED.md`.
> **Cập nhật lần cuối: VR-017 (2026-09-21)** · Nguồn scope: `03_test-cases/v1.1/fragments/TC-ACT-v1.1.md` + `03_test-cases/v1.0/fragments/TC-ACT-v1.0.md`
> **Tổng: có verdict cuối 10/18 · CÒN NỢ 8** (8 NOT_RUN + 0 NOT_EVIDENCED)
> Verdict hợp lệ: ✅ PASS · ❌ FAIL · 🚫 BLOCKED · ⚠️ NOT_EVIDENCED · ⏳ NOT_RUN · ⛔ N-A

> 🔄 **2026-09-21 (sau VR-017) — `TC-ACT-017` FAIL → ✅ PASS.** QC chốt: tab rỗng không cuộn/không phản hồi vuốt là **đúng** ⇒ Expected sửa theo app, `BUG-032` xoá.
> 🔄 **2026-09-21 (sau VR-017) — `TC-ACT-015` FAIL → 🚫 BLOCKED.** QC GiangDC2 chốt: đơn "Đã huỷ" hiện ở tab "Đang diễn ra" **không phải bug** ⇒ sửa Expected theo app (fragment + 2 file TC-MASTER, `§10.5` giữ nguyên Title/số TC). Vế đó nay đúng; vế đơn `RETURNED` còn thiếu dữ liệu. ⚠️ `TC-ACT-007` (CARRIED) vẫn assert kỳ vọng cũ — chạy sẽ FAIL oan, chờ QC quyết.
> 🔵 **2026-09-21 (VR-017) — phạm vi do QC chỉ định: chỉ 10 TC v1.1.** 8 TC CARRIED v1.0 (`002 003 004 006 007 009 010 011`) chưa chạy vì **ngoài phạm vi được yêu cầu**, không phải hết sức phiên.
> 🔒 **VR-017 chạy ở chế độ chỉ đọc** (chưa có quyền đổi trạng thái đơn trên STG) ⇒ `TC-ACT-005` BLOCKED vì thiếu đơn `RETURNED`.

## Tiến độ theo run

| Run | Ngày | TC chạy trong run | Verdict thu được |
|-----|------|-------------------|------------------|
| VR-017 | 2026-09-21 | 10 (`001 005 008 012 013 014 015 016 017 018`) | 6P / 2F / 2B *(`015` FAIL→BLOCKED, `017` FAIL→PASS sau khi QC sửa Expected theo app)* |

## Chi tiết từng TC

| Testcase ID | Verdict | Scenario ID | Priority | Title | Run | Evidence | Ghi chú |
|---|---|---|---|---|---|---|---|
| TC-ACT-001 | ✅ PASS | SC-ACT-001 | P2 | Check màn Hoạt động dùng đúng bộ nhãn của app cho tên màn và hai tab | VR-017 | `VR-017-ACT-2026-09-21/screenshots/TC-ACT-001__verify-nhan-hoat-dong-don-cua-toi-2-tab.png` | v1.1 MODIFIED |
| TC-ACT-002 | ⏳ NOT_RUN | SC-ACT-002 | P2 | Check tab "Đang diễn ra" active mặc định khi mở màn Hoạt động | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-017 (QC chỉ yêu cầu TC v1.1) |
| TC-ACT-003 | ⏳ NOT_RUN | SC-ACT-003 | P3 | Check cơ chế chuyển qua lại giữa hai tab đổi đúng tab active | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-017 (QC chỉ yêu cầu TC v1.1) |
| TC-ACT-004 | ⏳ NOT_RUN | SC-ACT-004 | P2 | Check tab "Đang diễn ra" chỉ chứa đơn đang hoạt động | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-017 (QC chỉ yêu cầu TC v1.1) |
| TC-ACT-005 | 🚫 BLOCKED | SC-ACT-005 | P2 | Check tab Đã hoàn thành chứa đủ cả ba loại đơn kết thúc | VR-017 | `VR-017-ACT-2026-09-21/screenshots/TC-ACT-005__step3-BLOCKED-chi-co-hoan-thanh-va-het-han-khong-co-don-tra-lai.png` | Thiếu đơn `RETURNED` (phải dựng qua `TC-DLV-063`, cần quyền đổi trạng thái đơn). 2 vế còn lại đúng: có `Hoàn thành` + `Hết hạn`, không có badge đơn đang chạy |
| TC-ACT-006 | ⏳ NOT_RUN | SC-ACT-006 | P2 | Check card đơn ở màn Hoạt động đủ năm trường theo thiết kế | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-017 (QC chỉ yêu cầu TC v1.1) |
| TC-ACT-007 | ⏳ NOT_RUN | SC-ACT-007 | P2 | Check đơn "Đã huỷ" không xuất hiện ở cả hai tab của màn Hoạt động | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-017. ⚠️ Expected v1.0 (Đã huỷ ẩn khỏi cả 2 tab) **ngược** kết luận QC 2026-09-21 — chạy sẽ FAIL oan, chờ QC sửa/`DESCOPED` |
| TC-ACT-008 | ❌ FAIL | SC-ACT-008 | P3 | Check card đơn Hết hạn hiện badge và đúng chuỗi lý do chính thức | VR-017 | `VR-017-ACT-2026-09-21/screenshots/TC-ACT-008__step2-FAIL-ly-do-het-han-ban-dai-tin-da-tu-dong-dong.png` | App hiện bản **dài** `… — tin đã tự động đóng.`; Expected v1.1 là bản **ngắn**. 🐞 **BUG-030** (draft, chờ QC review) |
| TC-ACT-009 | ⏳ NOT_RUN | SC-ACT-009 | P3 | Check card đơn "Hết hạn" không thao tác được khi nhấn vào | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-017 (QC chỉ yêu cầu TC v1.1) |
| TC-ACT-010 | ⏳ NOT_RUN | SC-ACT-010 | P2 | Check nhấn card đơn khác "Hết hạn" mở màn của đúng đơn vừa nhấn | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-017 (QC chỉ yêu cầu TC v1.1) |
| TC-ACT-011 | ⏳ NOT_RUN | SC-ACT-011 | P3 | Check nhấn card đơn của chính mình mở màn Theo dõi đơn | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-017 (QC chỉ yêu cầu TC v1.1) |
| TC-ACT-012 | ❌ FAIL | SC-ACT-012 | P2 | Check empty state tab Đang diễn ra hiện đúng chuỗi và đúng một nút đăng tin | VR-017 | `VR-017-ACT-2026-09-21/screenshots/TC-ACT-012__step3-FAIL-thieu-dong-giai-thich-duoi-tieu-de.png` | Icon + tiêu đề + đúng 1 CTA đúng; **thiếu dòng giải thích** (`BR17-01`). 🐞 **BUG-031** (draft, chờ QC review) |
| TC-ACT-013 | ✅ PASS | SC-ACT-013 | P2 | Check card đơn Hoàn thành không còn dấu vết sao điểm tier hay chỉ số môi trường | VR-017 | `VR-017-ACT-2026-09-21/screenshots/TC-ACT-013__verify-card-hoan-thanh-cuoi-danh-sach-khong-sao-diem-tier.png` | rà toàn bộ ~17 card `Hoàn thành` của `anhdc4` |
| TC-ACT-014 | ✅ PASS | SC-ACT-014 | P2 | Check empty state tab Đã hoàn thành hiện đúng chuỗi không có CTA và ẩn hẳn khối lịch sử | VR-017 | `VR-017-ACT-2026-09-21/screenshots/TC-ACT-014__verify-chua-co-don-hoan-tat-khong-cta-khong-khoi-lich-su.png` | chạy trên `thuyntt22` (tab `Đã hoàn thành` rỗng) |
| TC-ACT-015 | 🚫 BLOCKED | SC-ACT-015 | P2 | Check đơn đã trả người gửi hiện kèm lý do còn đơn đã huỷ vẫn bị ẩn | VR-017 | `VR-017-ACT-2026-09-21/screenshots/TC-ACT-015__step4-BLOCKED-tab-da-hoan-thanh-khong-co-don-tra-lai-nguoi-gui.png` | 🔄 FAIL→BLOCKED 2026-09-21: QC chốt đơn "Đã huỷ" hiện ở tab "Đang diễn ra" **không phải bug**, Expected sửa theo app — vế này nay đúng. Còn thiếu đơn `RETURNED` để kiểm vế kia |
| TC-ACT-016 | ✅ PASS | SC-ACT-016 | P3 | Check empty state không che thanh tab dưới ở cả hai tab rỗng | VR-017 | `VR-017-ACT-2026-09-21/screenshots/TC-ACT-016__verify-tab-da-hoan-thanh-rong-thanh-tab-duoi-du-5-muc.png` | 5/5 mục bấm được ở cả 2 tab |
| TC-ACT-017 | ✅ PASS | SC-ACT-016 | P3 | Check màn vẫn cuộn được khi đang hiện empty state ở cả hai tab rỗng | VR-017 | `VR-017-ACT-2026-09-21/screenshots/TC-ACT-017__verify-tab-da-hoan-thanh-vuot-man-dung-yen-khong-treo.png` | 🔄 FAIL→PASS 2026-09-21: QC chốt màn rỗng không cuộn là đúng ⇒ Expected sửa theo app, `BUG-032` xoá. Title còn lệch (nợ #28) |
| TC-ACT-018 | ✅ PASS | SC-ACT-017 | P3 | Check tab rỗng phân biệt rõ trạng thái đang tải với trạng thái không có dữ liệu | VR-017 | `VR-017-ACT-2026-09-21/screenshots/TC-ACT-018__verify-tab-da-hoan-thanh-chuyen-han-empty-state-sau-tai.png` | 3G (384 kbit/s): skeleton → empty state ở cả 2 tab, không lặp |

## Tổng hợp

| Verdict | Số | TC |
|---|---|---|
| ✅ PASS | 6 | `TC-ACT-001` · `013` · `014` · `016` · `017` · `018` (VR-017) |
| ❌ FAIL | 2 | `TC-ACT-008` (`BUG-030`) · `012` (`BUG-031`) |
| 🚫 BLOCKED | 2 | `TC-ACT-005` · `015` (cùng thiếu đơn `RETURNED`) |
| ⚠️ NOT_EVIDENCED | 0 | — |
| ⏳ NOT_RUN | 8 | `TC-ACT-002` · `003` · `004` · `006` · `007` · `009` · `010` · `011` (CARRIED v1.0, ngoài phạm vi) |
| ⛔ N-A | 0 | — |
| **Tổng** | **18** | |

**Có verdict cuối: 10/18 · CÒN NỢ: 8** ⇒ §8 = **PARTIAL**.

> 📊 **Riêng v1.1: 10/10 có verdict (100%)** — 6 PASS · 2 FAIL · 2 BLOCKED.
> 🐞 2 FAIL đã log draft `BUG-030/031` — chờ QC review trước khi push Jira. (`BUG-032` đã xoá — QC chốt `TC-ACT-017` app đúng.)
> 🚫 `TC-ACT-005` + `015` chỉ gỡ được khi có 1 đơn `RETURNED` trên cùng tài khoản — dựng qua luồng hoàn hàng (`TC-DLV-063`), cần QC cấp quyền đổi trạng thái đơn trên STG.
