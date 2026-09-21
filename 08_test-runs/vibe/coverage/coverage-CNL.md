# Coverage — module CNL — SCOPE_TOTAL = 22 TC

> Sổ cái TÍCH LŨY xuyên run cho module **CNL** (Huỷ đơn / Huỷ nhận đơn) — scope = **v1.1 (13 TC: 5 MODIFIED + 8 NEW)** + **CARRIED v1.0 (9 TC)**, cùng quy ước với `coverage-ACT.md`.
> **Cập nhật lần cuối: VR-018 (2026-09-21)** · Nguồn scope: `03_test-cases/v1.1/fragments/TC-CNL-v1.1.md` + `03_test-cases/v1.0/fragments/TC-CNL-v1.0.md` (đối chiếu ID 2 file TC-MASTER)
> **Tổng: có verdict cuối 13/22 · CÒN NỢ 9** (9 NOT_RUN + 0 NOT_EVIDENCED)
> Verdict hợp lệ: ✅ PASS · ❌ FAIL · 🚫 BLOCKED · ⚠️ NOT_EVIDENCED · ⏳ NOT_RUN · ⛔ N-A

> 🔵 **2026-09-21 (VR-018) — phạm vi do QC chỉ định: chỉ 13 TC v1.1.** 9 TC CARRIED v1.0 chưa chạy vì ngoài phạm vi được yêu cầu. ⚠️ Header fragment v1.1 liệt kê 8 CARRIED, **thiếu `TC-CNL-014`** — đối chiếu 2 file TC-MASTER ra 9.
> 🔓 QC cho phép đổi trạng thái đơn trên STG (đăng / ghép / lấy hàng / huỷ). Chỉ có 1 thiết bị ⇒ `021` BLOCKED.

## Tiến độ theo run

| Run | Ngày | TC chạy trong run | Verdict thu được |
|-----|------|-------------------|------------------|
| VR-018 | 2026-09-21 | 13 (toàn bộ v1.1) | 5P / 6F / 2B |

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
| TC-CNL-009 | ❌ FAIL | SC-CNL-009 | P2 | Check huỷ đơn ghi log đủ vai trò, lý do và thời điểm | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-009__step8-FAIL-log-nguoi-gui-huy-ghi-nhan-da-huy-nhan-don-khong-co-vai.png` | +1 dòng ✅ lý do ✅ thời điểm ✅ — ghi tên thay vai ❌ + **nhãn sai "Đã huỷ nhận đơn"** cho hành động người gửi huỷ ❌. 🐞 ứng viên bug |
| TC-CNL-010 | ❌ FAIL | SC-CNL-010 | P1 | Check huỷ nhận đơn giữ nguyên log ghép cũ và đơn về lại bảng tin | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-010__step8-FAIL-log-huy-nhan-ghi-ten-khong-ghi-vai-nguoi-van-chuyen.png` | Log cũ giữ nguyên ✅ lý do ✅ đơn về bảng tin ✅ — ghi **tên** thay vai "Người vận chuyển" ❌. ⚠️ chờ QC chốt tên = vai? |
| TC-CNL-011 | ⏳ NOT_RUN | SC-CNL-011 | P2 | Check ba phiên ba vai cùng cập nhật trạng thái huỷ không cần làm mới | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-018; cần 3 thiết bị |
| TC-CNL-012 | ✅ PASS | SC-CNL-012 | P3 | Check lý do huỷ gồm năm dấu cách bị chặn sau khi cắt khoảng trắng | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-012__verify-5-dau-cach-nut-xac-nhan-vo-hieu-hoa.png` | app đã sửa `KB-CNL-02` (dự kiến FAIL) |
| TC-CNL-013 | ⏳ NOT_RUN | SC-CNL-013 | P2 | Check quyền huỷ của ba vai khi đơn ở trạng thái "Chờ ghép" | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-018 (QC chỉ yêu cầu TC v1.1) |
| TC-CNL-014 | ⏳ NOT_RUN | SC-CNL-013 | P2 | Check quyền huỷ của ba vai khi đơn ở trạng thái "Đã ghép" | — | — | **Lý do:** CARRIED v1.0 — ngoài phạm vi VR-018 (header fragment v1.1 quên liệt kê TC này) |
| TC-CNL-015 | ✅ PASS | SC-CNL-006 | P2 | Check nút "Báo cáo sự cố" tồn tại cho vai Người vận chuyển khi đơn đang giao | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-015__verify-nguoi-van-chuyen-bam-bao-cao-su-co-mo-luong-bao-su-co.png` | mở webview Microsoft Sign in |
| TC-CNL-016 | ✅ PASS | SC-CNL-006 | P2 | Check nút "Báo cáo sự cố" tồn tại cho vai Người nhận khi đơn đang giao | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-016__verify-nguoi-nhan-bam-bao-cao-su-co-mo-luong-bao-su-co.png` | mở webview Microsoft Sign in |
| TC-CNL-017 | ❌ FAIL | SC-CNL-014 | P1 | Check chỉ còn đúng 2 đường thoát cho vai Người gửi sau khi đơn đang giao | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-017__step2-FAIL-vai-nguoi-gui-dang-giao-khong-co-yeu-cau-hoan-hang.png` | Không nút huỷ ✅ · có `Báo cáo sự cố` ✅ · **thiếu `Yêu cầu hoàn hàng`** ❌. 🐞 ứng viên bug (gộp 017/018/019) |
| TC-CNL-018 | ❌ FAIL | SC-CNL-014 | P1 | Check chỉ còn đúng 2 đường thoát cho vai Người vận chuyển sau khi đơn đang giao | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-018__step2-FAIL-vai-nguoi-van-chuyen-dang-giao-khong-co-yeu-cau-hoan-hang.png` | như `017`; hoàn hàng chỉ đi gián tiếp qua `Đã giao cho người nhận` → *Cầm hàng về* |
| TC-CNL-019 | ❌ FAIL | SC-CNL-014 | P1 | Check chỉ còn đúng 2 đường thoát cho vai Người nhận sau khi đơn đang giao | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-019__step2-FAIL-vai-nguoi-nhan-dang-giao-khong-co-yeu-cau-hoan-hang.png` | như `017` |
| TC-CNL-020 | 🚫 BLOCKED | SC-CNL-015 | P2 | Check đơn ở trạng thái sự cố không tự chuyển hoàn thành | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-020__step1-BLOCKED-khong-dung-duoc-don-su-co-van-dang-giao.png` | Không tạo được đơn `INCIDENT`: báo sự cố = form Microsoft ngoài app. Cần dev seed |
| TC-CNL-021 | 🚫 BLOCKED | SC-CNL-016 | P2 | Check huỷ đơn bị chặn khi đơn còn hiện Đã ghép nhưng người vận chuyển đã bấm lấy hàng | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-021__step2-BLOCKED-popup-lay-hang-dang-mo-o-phien-b-khong-co-phien-a-song-song.png` | Cần 2 phiên song song — chỉ có 1 thiết bị. Cắm máy thật rồi chạy lại |
| TC-CNL-022 | ✅ PASS | SC-CNL-017 | P3 | Check không tồn tại bề mặt Admin vận hành trong app end-user | VR-018 | `VR-018-CNL-2026-09-21/screenshots/TC-CNL-022__verify-trang-ca-nhan-khong-co-be-mat-admin.png` |  |

## Tổng hợp

| Verdict | Số | TC |
|---|---|---|
| ✅ PASS | 5 | `TC-CNL-006` · `012` · `015` · `016` · `022` (VR-018) |
| ❌ FAIL | 6 | `TC-CNL-004` (thiếu lỗi dưới ô lý do) · `009` (log sai nhãn + thiếu vai) · `010` (log thiếu vai) · `017` · `018` · `019` (thiếu "Yêu cầu hoàn hàng") |
| 🚫 BLOCKED | 2 | `TC-CNL-020` (không có đơn INCIDENT) · `021` (cần 2 thiết bị) |
| ⚠️ NOT_EVIDENCED | 0 | — |
| ⏳ NOT_RUN | 9 | `TC-CNL-001` · `002` · `003` · `005` · `007` · `008` · `011` · `013` · `014` (CARRIED v1.0, ngoài phạm vi) |
| ⛔ N-A | 0 | — |
| **Tổng** | **22** | |

**Có verdict cuối: 13/22 · CÒN NỢ: 9** ⇒ §8 = **PARTIAL**.

> 📊 **Riêng v1.1: 13/13 có verdict (100%)** — 5 PASS · 6 FAIL · 2 BLOCKED.
> 🔴 6 FAIL chờ QC review trước khi `/log-bug` (⛔ chưa log). `010`/`009` vế "tên thay vai" cần QC chốt; vế **nhãn sai** của `009` là lỗi độc lập.
> 🚫 `021` gỡ khi có 2 thiết bị; `020` gỡ khi dev seed đơn `INCIDENT`.
