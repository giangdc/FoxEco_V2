# Coverage — module CNL — SCOPE_TOTAL = 22 TC

> Sổ cái TÍCH LŨY xuyên run cho module **CNL** (Huỷ đơn / Huỷ nhận đơn) — scope = **v1.1 (13 TC: 5 MODIFIED + 8 NEW)** + **CARRIED v1.0 (9 TC)**, cùng quy ước với `coverage-ACT.md`.
> **Cập nhật lần cuối: VR-018 follow-up (2026-09-22)** · Nguồn scope: `03_test-cases/v1.1/fragments/TC-CNL-v1.1.md` + `03_test-cases/v1.0/fragments/TC-CNL-v1.0.md` (đối chiếu ID 2 file TC-MASTER)
> **Tổng: có verdict cuối 13/22 · CÒN NỢ 9** (9 NOT_RUN + 0 NOT_EVIDENCED)
> Verdict hợp lệ: ✅ PASS · ❌ FAIL · 🚫 BLOCKED · ⚠️ NOT_EVIDENCED · ⏳ NOT_RUN · ⛔ N-A

> 🔵 **2026-09-21 (VR-018) — phạm vi do QC chỉ định: chỉ 13 TC v1.1.** 9 TC CARRIED v1.0 chưa chạy vì ngoài phạm vi được yêu cầu. ⚠️ Header fragment v1.1 liệt kê 8 CARRIED, **thiếu `TC-CNL-014`** — đối chiếu 2 file TC-MASTER ra 9.
> 🔓 QC cho phép đổi trạng thái đơn trên STG (đăng / ghép / lấy hàng / huỷ). Chỉ có 1 thiết bị ⇒ `021` BLOCKED.

## Tiến độ theo run

| Run | Ngày | TC chạy trong run | Verdict thu được |
|-----|------|-------------------|------------------|
| VR-018 | 2026-09-21 + follow-up 2026-09-22 | 13 (toàn bộ v1.1) | 9P / 2F / 2B *(sau đính chính nội dung + chụp bù evidence 2026-09-22 — xem khối cuối file)* |

## Chi tiết từng TC

| Testcase ID | Verdict | Scenario ID | Priority | Title | Run | Evidence | Ghi chú |
|---|---|---|---|---|---|---|---|
| TC-CNL-001 | ⏳ NOT_RUN | SC-CNL-001 | P1 | Check huỷ đơn ở "Chờ ghép" đưa đơn sang "Đã huỷ" | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-018 (QC chỉ yêu cầu TC v1.1) |
| TC-CNL-002 | ⏳ NOT_RUN | SC-CNL-002 | P1 | Check huỷ đơn ở "Đã ghép" thì hai vai còn lại thấy đơn đã huỷ | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-018 (QC chỉ yêu cầu TC v1.1) |
| TC-CNL-003 | ⏳ NOT_RUN | SC-CNL-003 | P2 | Check nút "Xác nhận" bị khoá khi ô lý do để trống | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-018. (Quan sát kèm VR-018: ô trống thì `cancel-order-confirm` `enabled=false`) |
| TC-CNL-004 | ❌ FAIL | SC-CNL-004 | P2 | Check lý do huỷ 4 ký tự bị chặn ngay từ nút xác nhận | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-004__step4-FAIL-nut-xac-nhan-khoa-nhung-khong-co-loi-duoi-o-ly-do.png` | Nút `Xác nhận` khoá sẵn ✅, đơn không đổi ✅ — **thiếu dòng lỗi dưới ô lý do** ❌. 🐞 ứng viên bug |
| TC-CNL-005 | ⏳ NOT_RUN | SC-CNL-005 | P1 | Check đơn ở "Đang giao" không vai nào huỷ được | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-018. (Quan sát kèm VR-018: cả 3 vai đều không có nút huỷ ở `Đang giao`) |
| TC-CNL-006 | ✅ PASS | SC-CNL-006 | P2 | Check nút "Báo cáo sự cố" tồn tại cho vai Người gửi khi đơn đang giao | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-006__verify-nguoi-gui-bam-bao-cao-su-co-mo-luong-bao-su-co.png` | mở webview Microsoft Sign in (form ngoài app) |
| TC-CNL-007 | ⏳ NOT_RUN | SC-CNL-007 | P1 | Check huỷ nhận đơn đưa đơn về "Chờ ghép" chứ không "Đã huỷ" | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-018 (QC chỉ yêu cầu TC v1.1) |
| TC-CNL-008 | ⏳ NOT_RUN | SC-CNL-008 | P2 | Check các bên còn lại thấy vai người huỷ kèm lý do | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-018 (QC chỉ yêu cầu TC v1.1) |
| TC-CNL-009 | ❌ FAIL | SC-CNL-009 | P2 | Check huỷ đơn ghi log đủ vai trò, lý do và thời điểm | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-009__step8-FAIL-log-nguoi-gui-huy-ghi-nhan-da-huy-nhan-don-khong-co-vai.png` | +1 dòng ✅ lý do ✅ thời điểm ✅ — ghi tên thay vai ✅ *(đính chính 2026-09-22, chấp nhận)* + **nhãn sai "Đã huỷ nhận đơn"** cho hành động người gửi huỷ ❌ **vẫn FAIL**. 🐞 `BUG-034` (giữ, chờ push Jira) |
| TC-CNL-010 | ✅ PASS | SC-CNL-010 | P1 | Check huỷ nhận đơn giữ nguyên log ghép cũ và đơn về lại bảng tin | VR-018 (+follow-up 2026-09-22) | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-010__verify-lich-su-huy-nhan-giu-nguyen-sau-dinh-chinh.png` | Log cũ giữ nguyên ✅ lý do ✅ đơn về bảng tin ✅ · ghi **tên** thay vai "Người vận chuyển" ✅ chấp nhận theo đính chính 2026-09-22. Ảnh đúng slot `__verify` chụp bù 2026-09-22 (đọc lại LỊCH SỬ hiện tại của O2, log bất biến `BR11-03` nên không cần lặp thao tác huỷ nhận) |
| TC-CNL-011 | ⏳ NOT_RUN | SC-CNL-011 | P2 | Check ba phiên ba vai cùng cập nhật trạng thái huỷ không cần làm mới | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-018; cần 3 thiết bị |
| TC-CNL-012 | ✅ PASS | SC-CNL-012 | P3 | Check lý do huỷ gồm năm dấu cách bị chặn sau khi cắt khoảng trắng | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-012__verify-5-dau-cach-nut-xac-nhan-vo-hieu-hoa.png` | app đã sửa `KB-CNL-02` (dự kiến FAIL) |
| TC-CNL-013 | ⏳ NOT_RUN | SC-CNL-013 | P2 | Check quyền huỷ của ba vai khi đơn ở trạng thái "Chờ ghép" | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-018 (QC chỉ yêu cầu TC v1.1) |
| TC-CNL-014 | ⏳ NOT_RUN | SC-CNL-013 | P2 | Check quyền huỷ của ba vai khi đơn ở trạng thái "Đã ghép" | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-018 (header fragment v1.1 quên liệt kê TC này) |
| TC-CNL-015 | ✅ PASS | SC-CNL-006 | P2 | Check nút "Báo cáo sự cố" tồn tại cho vai Người vận chuyển khi đơn đang giao | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-015__verify-nguoi-van-chuyen-bam-bao-cao-su-co-mo-luong-bao-su-co.png` | mở webview Microsoft Sign in |
| TC-CNL-016 | ✅ PASS | SC-CNL-006 | P2 | Check nút "Báo cáo sự cố" tồn tại cho vai Người nhận khi đơn đang giao | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-016__verify-nguoi-nhan-bam-bao-cao-su-co-mo-luong-bao-su-co.png` | mở webview Microsoft Sign in |
| TC-CNL-017 | ✅ PASS | SC-CNL-014 | P1 | Check chỉ còn đúng 2 đường thoát cho vai Người gửi sau khi đơn đang giao | VR-018 (+follow-up 2026-09-22) | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-017__verify-vai-nguoi-gui-chi-co-bao-cao-su-co.png` | Không nút huỷ ✅ · có `Báo cáo sự cố` ✅ · không có nút "hoàn hàng" ✅ đúng theo Expected mới (đính chính 2026-09-22). Ảnh đúng slot `__verify` chụp bù 2026-09-22 |
| TC-CNL-018 | ✅ PASS | SC-CNL-014 | P1 | Check chỉ còn đúng 2 đường thoát cho vai Người vận chuyển sau khi đơn đang giao | VR-018 (+follow-up 2026-09-22) | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-018__verify-vai-nguoi-van-chuyen-bao-cao-su-co-va-duong-giao-hang.png` | Không nút huỷ ✅ · có `Báo cáo sự cố` ✅ · đường hoàn hàng đi qua `Đã giao cho người nhận` → "Xử lý đơn hàng" → *Cầm hàng về* (`FR09`) ✅ đúng thiết kế. Ảnh đúng slot `__verify` chụp bù 2026-09-22 |
| TC-CNL-019 | ✅ PASS | SC-CNL-014 | P1 | Check chỉ còn đúng 2 đường thoát cho vai Người nhận sau khi đơn đang giao | VR-018 (+follow-up 2026-09-22) | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-019__verify-vai-nguoi-nhan-chi-co-bao-cao-su-co.png` | như `017` — nội dung đúng. Ảnh đúng slot `__verify` chụp bù 2026-09-22 |
| TC-CNL-020 | 🚫 BLOCKED | SC-CNL-015 | P2 | Check đơn ở trạng thái sự cố không tự chuyển hoàn thành | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-020__step1-BLOCKED-khong-dung-duoc-don-su-co-van-dang-giao.png` | Không tạo được đơn `INCIDENT`: báo sự cố = form Microsoft ngoài app. Cần dev seed |
| TC-CNL-021 | 🚫 BLOCKED | SC-CNL-016 | P2 | Check huỷ đơn bị chặn khi đơn còn hiện Đã ghép nhưng người vận chuyển đã bấm lấy hàng | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-021__step2-BLOCKED-popup-lay-hang-dang-mo-o-phien-b-khong-co-phien-a-song-song.png` | Cần 2 phiên song song — chỉ có 1 thiết bị. Cắm máy thật rồi chạy lại |
| TC-CNL-022 | ✅ PASS | SC-CNL-017 | P3 | Check không tồn tại bề mặt Admin vận hành trong app end-user | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-022__verify-trang-ca-nhan-khong-co-be-mat-admin.png` |  |

## Tổng hợp

| Verdict | Số | TC |
|---|---|---|
| ✅ PASS | 9 | `TC-CNL-006` · `010` · `012` · `015` · `016` · `017` · `018` · `019` · `022` (VR-018; `010`/`017`/`018`/`019` chốt PASS sau follow-up chụp bù evidence 2026-09-22) |
| ❌ FAIL | 2 | `TC-CNL-004` (thiếu lỗi dưới ô lý do — `BUG-036`) · `009` (log sai nhãn hành động — `BUG-034`) |
| 🚫 BLOCKED | 2 | `TC-CNL-020` (không có đơn INCIDENT) · `021` (cần 2 thiết bị) |
| ⚠️ NOT_EVIDENCED | 0 | — |
| ⏳ NOT_RUN | 9 | `TC-CNL-001` · `002` · `003` · `005` · `007` · `008` · `011` · `013` · `014` (CARRIED v1.0, ngoài phạm vi) |
| ⛔ N-A | 0 | — |
| **Tổng** | **22** | |

**Có verdict cuối: 13/22 · CÒN NỢ: 9** (9 NOT_RUN, toàn bộ CARRIED v1.0) ⇒ §8 = **PARTIAL**.

> 📊 **Riêng v1.1: 13/13 có verdict cuối (100%)** — 9 PASS · 2 FAIL · 2 BLOCKED *(sau đính chính nội dung + chụp bù evidence 2026-09-22)*.
> 🔴 2 FAIL đã QC review, đã `/log-bug`: `BUG-034` (`009`, nhãn hành động sai) · `BUG-036` (`004`, thiếu dòng lỗi hiển thị) — cả 2 **chờ QC push Jira** (chưa push).
> 🚫 `021` gỡ khi có 2 thiết bị; `020` gỡ khi dev seed đơn `INCIDENT`.
>
> 🔁 **ĐÍNH CHÍNH 2026-09-22 — nội dung 4 TC đổi ❌ FAIL → ✅ PASS (QC chốt), 2 bug draft đã xoá:**
> - **`TC-CNL-017`/`018`/`019` (→ `BUG-033` xoá):** TC viết sai giả định — PRD (`AC-25.2.01` + `BR11-04`, `DOC-v1.1-01` §6.2 trang 27 · §8.11.1 trang 45, đã đọc trực tiếp PDF) chỉ đảm bảo ở **mức trạng thái** ("hoàn hàng vẫn là 1 trong 2 lối thoát hợp lệ sau IN_TRANSIT"), KHÔNG đặt tên nút UI "Yêu cầu hoàn hàng". Luồng hoàn hàng thật đặc tả ở `FR09` (§8.9, trang 43): **Người vận chuyển** bấm xác nhận tại điểm giao ("Đã đến địa điểm giao hàng"/"Đã giao cho người nhận") → màn **"Xử lý đơn hàng"** → chọn chế độ **"Cầm hàng về"** (`return`). Sender/Receiver không có control kích hoạt trực tiếp. Expected 3 TC đã sửa theo đúng luồng (xem fragment). App hiện tại **đúng đặc tả**.
> - **`TC-CNL-010` (→ vế "tên thay vai" của `BUG-035` xoá):** QC chấp nhận app ghi **tên người thực hiện** thay vì vai trò ở dòng log huỷ nhận — hành vi **nhất quán với mọi dòng LỊCH SỬ khác** trong toàn app (không riêng dòng huỷ), không phải lỗi cục bộ. Expected đã sửa; TC không còn vướng mắc nào khác.
> - **`TC-CNL-009` vẫn FAIL** — vế "tên thay vai" cũng được chấp nhận như trên, **nhưng** vế **nhãn hành động sai** ("Đã huỷ nhận đơn" hiển thị cho hành động Người gửi huỷ đơn, đúng ra phải là nhãn của luồng huỷ đơn) là lỗi **độc lập, chưa được chấp nhận** ⇒ vẫn FAIL, giữ `BUG-034` chờ push Jira.
> - **`BUG-036` (`TC-CNL-004`) giữ nguyên, chưa xử lý** — chờ QC push Jira sau.
>
> 🔁 **FOLLOW-UP 2026-09-22 — chụp bù evidence đúng slot `__verify` cho `TC-CNL-010`/`017`/`018`/`019`:** ảnh gốc của phiên 2026-09-21 mang tên slot `__step*-FAIL` (chụp lúc đang chấm FAIL theo Expected cũ) — không đủ cho verdict PASS theo gate `verify_evidence.py` (đòi `__verify`). Đã đăng nhập lại đủ 3 vai (A/B/C) và đọc lại state hiện tại của O2 (vẫn `IN_TRANSIT`/Đang giao) để chụp 4 ảnh đúng slot — **không cần lặp lại thao tác huỷ/ghép nào** vì log LỊCH SỬ bất biến (`BR11-03`) và ma trận nút của `Đang giao` không đổi theo thời gian. Chi tiết: `VR-018-CNL-2026-09-21/vibe-log.md` §"Follow-up 2026-09-22". Ảnh cũ **giữ nguyên, không xoá** — vẫn được trích làm hồ sơ lúc chạy gốc.
