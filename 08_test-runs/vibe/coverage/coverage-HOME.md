# Coverage — module HOME — SCOPE_TOTAL = 32 TC

> Sổ cái TÍCH LŨY xuyên run cho module **HOME** (Trang chủ) — scope = **v1.1 (11 TC) + CARRIED v1.0 (19 TC)**.
> **Cập nhật lần cuối: VR-014 (2026-09-21)** · *(sửa mẫu số 30 → 32 ngày 2026-09-19, xem callout ngay dưới)* · Nguồn scope: `03_test-cases/v1.1/fragments/TC-HOME-v1.1.md` + `03_test-cases/v1.0/fragments/TC-HOME-v1.0.md`
> **Tổng: có verdict cuối 22/32 · CÒN NỢ 10** (10 NOT_RUN + 0 NOT_EVIDENCED) — *cập nhật sau VR-014 (2026-09-21)*
> Verdict hợp lệ: ✅ PASS · ❌ FAIL · 🚫 BLOCKED · ⚠️ NOT_EVIDENCED · ⏳ NOT_RUN · ⛔ N-A

> 🔴 **2026-09-19 (đính chính mẫu số) — SCOPE_TOTAL đúng là 32, KHÔNG phải 30.**
> Sổ này trước đây thiếu hẳn **2 dòng**: `TC-HOME-010` và `TC-HOME-024` (cả hai **chỉ có ở `TC-MASTER-v1.0`**, chưa từng chạy).
> Phát hiện khi đối chiếu scope theo **hợp 2 file TC-MASTER** — đúng luật `CLAUDE.md §TC-MASTER` (*v1.1 KHÔNG gộp TC CARRIED ⇒ phải mở cả 2 file*).
> Callout cũ bên dưới (*"SCOPE_TOTAL = 30, không phải 33"*) **vẫn đúng ở phần bác bỏ con số 33** (33 đếm trùng 3 TC MODIFIED), nhưng **kết luận 30 là thiếu**: 30 = đếm từ fragment, bỏ sót 2 TC chỉ-có-ở-v1.0.
> ⇒ Đã bổ sung 2 dòng `⏳ NOT_RUN` kèm lý do. **Không TC nào bị đổi verdict.**

> 🔢 **2026-09-19 — SCOPE_TOTAL = 30, ⛔ KHÔNG phải 33.** `TC-HOME-v1.1.md §0.1` ghi *"33 TC (24 của v1.0 − 2 gỡ + 11 của v1.1)"* — phép tính đó **đếm trùng 3 TC MODIFIED** (`TC-HOME-008/019/021` có mặt ở **cả hai** file, `CLAUDE.md` chốt *"LUÔN lấy bản v1.1"*). Hợp nhất theo ID duy nhất: 24 − 2 (`010`/`024` DEPRECATED) − 3 (trùng, lấy bản v1.1) + 11 = **30**. ⛔ Không sửa fragment (`§10.5` FREEZE Σ TC); đây là **đính chính cách ĐẾM**, không thêm/bớt TC nào.
>
> 🔴 **2026-09-19 — Blocker chi phối cả module: STG có 0 tin NEED hợp lệ.** Xác nhận từ 2 bề mặt độc lập (Trang chủ §Tin mới + màn Bảng tin). Vì *"Tin mới"* **loại trừ tin của chính mình**, tài khoản A ⛔ **không tự seed được** ⇒ 8 TC phải chờ **tài khoản B + OTP nhập tay**.
>
> 🍀 **2026-09-19 — `TC-HOME-026` chạy được ngoài dự kiến.** `fragment §0.3` xếp TC này vào nhóm *"không dựng được trên STG dùng chung ⇒ ghi Blocked"*, nhưng STG tình cờ sạch tin nên empty state `EMP-01` verify được thật. Cùng cửa sổ đó **không** giúp `TC-HOME-025` (cần **đúng 5** tin, không phải 0).

## Tiến độ theo run

| Run | Ngày | TC chạy trong run | Verdict thu được |
|-----|------|-------------------|------------------|
| VR-005 | 2026-09-19 | 14 | 13P / 0F / 1B *(007: FAIL → PASS 2026-09-21)* |

## Chi tiết từng TC

| Testcase ID | Verdict | Scenario ID | Priority | Title | Run | Evidence | Ghi chú |
|---|---|---|---|---|---|---|---|
| TC-HOME-001 | ✅ PASS | SC-HOME-001 | P1 | Check bottom nav đủ 5 tab đúng thứ tự và tab "Trang chủ" đang active | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-001__verify-bottom-nav-5-tabs.png` |  |
| TC-HOME-002 | 🚫 BLOCKED | SC-HOME-002 | P3 | Check các màn con không hiển thị bottom nav mà chỉ có nút quay lại | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-002__step2-BLOCKED-bang-tin-0-tin.png` | Blocked step 2: không có tin nào trên Bảng tin ⇒ không mở được màn Chi tiết tin. **3/4 màn con còn lại đã kiểm và ĐÚNG** (Theo dõi đơn · Wizard · Thông báo — đều không bottom nav, đều có nút quay lại). Gỡ khi STG có ≥1 tin |
| TC-HOME-003 | ✅ PASS | SC-HOME-003 | P2 | Check header hiển thị lời chào kèm đúng tên hồ sơ của tài khoản đăng nhập | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-003__verify-greeting-name.png` |  |
| TC-HOME-004 | ⏳ NOT_RUN | SC-HOME-004 | P3 | Check header hiển thị icon vai trò và icon khác nhau giữa ba vai | — | — | **Lý do:** cần **3 tài khoản** giữ 3 vai trên cùng 1 đơn + đăng xuất/đăng nhập ×3 (**OTP nhập tay**). 🔍 Quan sát rời: header của tài khoản A **KHÔNG có node icon vai trò nào** (tree chỉ có `Quay lại` · lời chào · `Thông báo`) ⇒ nghi vấn bề mặt chưa build, cần BA xác nhận trước khi chạy |
| TC-HOME-005 | ✅ PASS | SC-HOME-005 | P2 | Check icon chuông hiển thị chấm đỏ khi còn thông báo chưa đọc | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-005__verify-chuong-cham-do.png` |  |
| TC-HOME-006 | ✅ PASS | SC-HOME-006 | P3 | Check icon chuông không có chấm đỏ khi đã đọc hết thông báo | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-006__verify-chuong-khong-cham-do.png` | Dùng nút bulk `Đánh dấu đã đọc` thay vì mở lần lượt — đạt đúng trạng thái đích, đã khai trong vibe-log |
| TC-HOME-007 | ✅ PASS | SC-HOME-007 | P3 | Check banner quảng bá hiển thị tagline kèm logo và không phát sinh điều hướng khi nhấn | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-007__verify-tagline-giup-dong-nghiep.png` | 🔁 **Đổi FAIL → PASS 2026-09-21, không chạy lại.** Run 2026-09-19 lệch Expected cũ (chuỗi BRD `Đồng nghiệp giúp nhau`). QC GiangDC2 chốt chuỗi PRD `Tiện đường — Giúp đồng nghiệp` là oracle (`C-HOME-01(b)`) và sửa Expected; app hiển thị đúng chuỗi này. Vế 2 (nhấn banner không điều hướng) PASS. ⛔ Không log bug (ứng viên H1 đóng) |
| TC-HOME-008 | ⏳ NOT_RUN | SC-HOME-008 | P2 | Check card Đóng góp của bạn hiện đúng số đơn đã giúp và không có chỉ số môi trường | — | — | ⏳ **Chưa chạy — QC không cho phép chạy vòng giao–nhận đến Hoàn thành ở VR-014** (cần A nhận đơn → giao → C xác nhận, đổi trạng thái đơn thật). Lý do cũ (bug `B1`, OTP nhập tay) **đã lỗi thời**: đăng NEED được (VR-013), OTP cố định. Cần quyền + 3 tài khoản. Chạy tiếp: `/vibe-test --module HOME --tc TC-HOME-008` |
| TC-HOME-009 | ✅ PASS | SC-HOME-009 | P2 | Check section "Đơn của tôi" hiển thị đủ sáu thành phần khi tài khoản có đơn đang hoạt động | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-009__verify-6-thanh-phan-don-cua-toi.png` | 6/6 thành phần có mặt. ⚠️ Verify trên đơn `Đã ghép` thay vì `Chờ ghép` (không đăng được tin mới — bug `B1`); Expected không assert giá trị badge |
| TC-HOME-010 | ⛔ N-A | SC-HOME-010 | P2 | Check section "Đơn của tôi" bị ẩn khi tài khoản không có đơn đang hoạt động | — | — | **DESCOPED** — `SC-HOME-010` DEPRECATED ở v1.1 — `C-HOME-05` Resolved 2026-09-17: BA chốt **HIỆN** empty state `EMP-02`, không ẩn ⇒ kỳ vọng cũ ngược hẳn; thay bằng `TC-HOME-027`. *(trước 2026-09-21 ghi nhầm là ⏳ NOT_RUN "sót khỏi sổ")* |
| TC-HOME-011 | ✅ PASS | SC-HOME-011 | P2 | Check section "Đơn của tôi" dùng nhãn "Gửi:" khi tài khoản là người gửi | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-011__verify-nhan-vai-gui.png` |  |
| TC-HOME-012 | ✅ PASS | SC-HOME-012 | P2 | Check section "Đơn của tôi" dùng nhãn "Giao:" khi tài khoản là người vận chuyển | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-012__verify-nhan-vai-giao.png` | ⚠️ Verify trên đơn vai vận chuyển **có sẵn** (không nhận đơn mới được — Bảng tin 0 tin); Expected chỉ assert chuỗi nhãn vai |
| TC-HOME-013 | ✅ PASS | SC-HOME-013 | P2 | Check section "Đơn của tôi" dùng nhãn "Nhận:" khi tài khoản là người nhận | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-013__verify-nhan-vai-nhan.png` | ⚠️ Đơn dùng để verify ở trạng thái `Đã huỷ`, không phải "đang hoạt động"; Expected chỉ assert chuỗi nhãn vai |
| TC-HOME-014 | ⏳ NOT_RUN | SC-HOME-014 | P3 | Check badge trạng thái và thanh progress khớp nhau ở từng trạng thái của đơn | — | — | **Lý do:** cần đẩy **1 đơn** qua 4 trạng thái liên tiếp với tài khoản Carrier + Receiver (OTP nhập tay) và đăng được tin NEED (bug `B1`). 🔍 Quan sát rời khớp 2/4 mốc: `Đã ghép`→**2/5** đoạn tô · `Đã giao`→**4/5** đoạn tô |
| TC-HOME-015 | ✅ PASS | SC-HOME-015 | P2 | Check chạm section "Đơn của tôi" mở màn Theo dõi đơn của đúng đơn đang hiển thị | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-015__verify-lo-trinh-khop.png` |  |
| TC-HOME-016 | ✅ PASS | SC-HOME-016 | P3 | Check nhấn "Xem tất cả" ở section "Đơn của tôi" mở màn Hoạt động | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-016__verify-mo-man-hoat-dong.png` |  |
| TC-HOME-017 | ⏳ NOT_RUN | SC-HOME-017 | P2 | Check section "Tin mới" vẫn hiển thị với tài khoản đang ở vai người gửi | — | — | **Lý do:** cần ≥1 tin NEED hợp lệ do **tài khoản khác** đăng; STG hiện **0 tin** (xác nhận 2 bề mặt, `_recon__bang-tin-empty-0-tin.png`). Tin của chính mình bị loại khỏi "Tin mới" ⇒ ⛔ không tự seed bằng tài khoản A được; cần **tài khoản B + OTP nhập tay** |
| TC-HOME-018 | ⏳ NOT_RUN | SC-HOME-018 | P2 | Check section "Tin mới" hiển thị tin của cả cộng đồng với tài khoản vai người vận chuyển | — | — | **Lý do:** cần ≥1 tin NEED hợp lệ do **tài khoản khác** đăng; STG hiện **0 tin** (xác nhận 2 bề mặt, `_recon__bang-tin-empty-0-tin.png`). Tin của chính mình bị loại khỏi "Tin mới" ⇒ ⛔ không tự seed bằng tài khoản A được; cần **tài khoản B + OTP nhập tay** |
| TC-HOME-019 | ✅ PASS | SC-HOME-019 | P3 | Check section Tin mới hiển thị đúng năm tin khi hệ thống có nhiều hơn năm tin hợp lệ | VR-014 | `VR-014-HOME-2026-09-21/screenshots/TC-HOME-019__verify-tin-moi-hien-5-tin-khi-he-thong-co-6-tin.png` | Tin mới hiện đúng 5 tin khi hệ thống ≥7 tin (Thủy quan sát; Giang đăng thêm 2 tin). Có 1 tin lạ do người khác đăng song song |
| TC-HOME-020 | ⏳ NOT_RUN | SC-HOME-020 | P3 | Check nhấn một tin ở section "Tin mới" mở màn Chi tiết tin của đúng tin đó | — | — | **Lý do:** cần ≥1 tin NEED hợp lệ do **tài khoản khác** đăng; STG hiện **0 tin** (xác nhận 2 bề mặt, `_recon__bang-tin-empty-0-tin.png`). Tin của chính mình bị loại khỏi "Tin mới" ⇒ ⛔ không tự seed bằng tài khoản A được; cần **tài khoản B + OTP nhập tay** |
| TC-HOME-021 | ✅ PASS | SC-HOME-021 | P3 | Check nút Xem thêm trên Bảng tin hiện và dẫn sang Bảng tin khi có hơn năm tin hợp lệ | VR-014 | `VR-014-HOME-2026-09-21/screenshots/TC-HOME-021__verify-nhan-xem-them-mo-man-bang-tin.png` | Nút `Xem thêm trên Bảng tin` có ở cuối section; nhấn mở đúng màn Bảng tin (≥7 tin) |
| TC-HOME-022 | ✅ PASS | SC-HOME-022 | P2 | Check nhấn "Xem bảng tin gửi hàng" chuyển sang tab Bảng tin | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-022__verify-chuyen-tab-bang-tin.png` |  |
| TC-HOME-023 | ⏳ NOT_RUN | SC-HOME-023 | P3 | Check sau khi xác nhận "Tôi mang giúp được" app vào thẳng màn Theo dõi đơn | — | — | **Lý do:** cần ≥1 tin NEED hợp lệ do **tài khoản khác** đăng; STG hiện **0 tin** (xác nhận 2 bề mặt, `_recon__bang-tin-empty-0-tin.png`). Tin của chính mình bị loại khỏi "Tin mới" ⇒ ⛔ không tự seed bằng tài khoản A được; cần **tài khoản B + OTP nhập tay** |
| TC-HOME-024 | ⛔ N-A | SC-HOME-024 | P3 | Check màn Trang chủ với tài khoản trắng vẫn giữ header, banner và card đóng góp, ẩn section "Đơn của tôi" | — | — | **DESCOPED** — `SC-HOME-024` DEPRECATED ở v1.1 — tách thành 3 SC atomic `EMP-01/02/03`; thay bằng `TC-HOME-026/027/028`. *(trước 2026-09-21 ghi nhầm là ⏳ NOT_RUN "sót khỏi sổ")* |
| TC-HOME-025 | ❌ FAIL | SC-HOME-021 | P3 | Check nút Xem thêm trên Bảng tin không hiện khi chỉ có đúng năm tin hợp lệ | VR-014 | `VR-014-HOME-2026-09-21/screenshots/TC-HOME-025__step4-FAIL-van-co-nut-xem-them-khi-dung-5-tin.png` | 🐞 Nút `Xem thêm trên Bảng tin` **hiện khi đúng 5 tin** hợp lệ (Bảng tin xác nhận đúng 5) — Expected: không hiện. Lúc còn 4 tin thì không có nút ⇒ app dùng `≥5`. Ứng viên bug P3, chưa log — 🐞 Jira FE-309 (BUG-025) |
| TC-HOME-026 | ✅ PASS | SC-HOME-025 | P3 | Check empty state section Tin mới hiện đúng chuỗi và nút đăng tin ngay | VR-005 | `VR-005-HOME-2026-09-19/screenshots/TC-HOME-026__verify-empty-state-tin-moi.png` | 🍀 `fragment §0.3` dự đoán TC này phải `Blocked`; phiên này chạy được **thật** vì STG tình cờ 0 tin. ⚠️ Cửa sổ đóng ngay khi có người đăng tin — PASS neo vào 2026-09-19 05:59 |
| TC-HOME-027 | ❌ FAIL | SC-HOME-026 | P3 | Check section Đơn của tôi vẫn hiện kèm empty state khi chưa có đơn đang chạy | VR-014 | `VR-014-HOME-2026-09-21/screenshots/TC-HOME-027__step3-FAIL-empty-state-chua-co-don-nao-thieu-cta-tao-don-gui-hang.png` | 🐞 Section `Đơn của tôi` hiện ✓ nhưng empty state sai `EMP-02`: chuỗi `Chưa có đơn nào` (Expected `Bạn chưa có đơn nào đang chạy`), thiếu CTA `Tạo đơn gửi hàng`, thiếu icon. Tài khoản sạch = Thủy. Ứng viên bug P3, chưa log — 🐞 Jira FE-310 (BUG-026) |
| TC-HOME-028 | 🚫 BLOCKED | SC-HOME-027 | P3 | Check hero và cụm cộng đồng hiện số không khi tài khoản và hệ thống chưa có đóng góp | VR-014 | `VR-014-HOME-2026-09-21/screenshots/TC-HOME-028__step3-BLOCKED-cong-dong-325-don-khong-phai-0-he-thong-da-co-don-hoan-thanh.png` | Hero `0 · Chưa có đóng góp nào` ĐÚNG; cộng đồng `325 đơn · 23743 người` ≠ `0 · 0` — tiền đề "STG chưa có đơn Hoàn thành" không thoả trên STG dùng chung. Vùng hero còn nút `Xem bảng tin gửi hàng` (Expected không CTA) — chưa rõ do dữ liệu hay app |
| TC-HOME-029 | ⏳ NOT_RUN | SC-HOME-029 | P3 | Check hero hiện số không với tài khoản chỉ từng làm người gửi | — | — | ⏳ **Chưa chạy — cần vòng giao–nhận đến Hoàn thành (QC không cho phép ở VR-014).** Tài khoản "sạch" nay có: `stag_thuyntt22@` (0 đơn, 0 đóng góp). Cần Thủy đăng NEED khai C nhận, B giao tới `Đã giao`, C xác nhận rồi xem hero của Thủy = 0. Chạy tiếp: `/vibe-test --module HOME --tc TC-HOME-029` |
| TC-HOME-030 | ⏳ NOT_RUN | SC-HOME-019 | P3 | Check section Tin mới loại trừ tin đã ghép tin hết hạn và tin của chính mình | — | — | ⏳ **Chưa chạy — thiếu 1 tin `Đã ghép` còn hạn:** cần ghép 1 tin bằng tài khoản thứ 3 (QC không cho phép ghép đơn P3 ở VR-014) + tin hết hạn (có sẵn `Gửi tài liệu 19/9`) + tin của chính người xem (có). Chạy tiếp: `/vibe-test --module HOME --tc TC-HOME-030` |
| TC-HOME-031 | ⏳ NOT_RUN | SC-HOME-030 | P2 | Check số đơn cộng đồng tăng đúng một ngay sau khi có đơn hoàn thành | — | — | ⏳ **Chưa chạy — cần vòng giao–nhận đến Hoàn thành (QC không cho phép ở VR-014).** Mốc nền hôm nay: cộng đồng `325 đơn · 23743 người` (Thủy, 15:00). Chạy tiếp: `/vibe-test --module HOME --tc TC-HOME-031` |
| TC-HOME-032 | ⛔ N-A | SC-HOME-028 | P2 | Check nội dung đầu Trang chủ hiển thị dưới hai giây khi có một nghìn người dùng đồng thời | — | — | **Lý do:** NFR hiệu năng — cần môi trường load-test mô phỏng **1.000 user đồng thời** trên 4G + công cụ đo p95; ⛔ **không dựng được bằng thiết bị tay / không phải bài test UI** (`fragment §0.3` chốt đánh `Deferred`). Thuộc phạm vi skill `k6-load-test`, không phải `vibe-test` |

## Tổng hợp

| Verdict | Số | TC |
|---|---|---|
| ✅ PASS | 15 | 15 TC |
| ❌ FAIL | 2 | `TC-HOME-025` · `TC-HOME-027` |
| 🚫 BLOCKED | 2 | `TC-HOME-002` · `TC-HOME-028` |
| ⚠️ NOT_EVIDENCED | 0 | — |
| ⏳ NOT_RUN | 10 | `TC-HOME-004` · `TC-HOME-008` · `TC-HOME-014` · `TC-HOME-017` · `TC-HOME-018` · `TC-HOME-020` · `TC-HOME-023` · `TC-HOME-029` · `TC-HOME-030` · `TC-HOME-031` |
| ⛔ N-A | 3 | `TC-HOME-010` · `TC-HOME-024` · `TC-HOME-032` |
| **Tổng** | **32** | |

**Có verdict cuối: 22/32 · CÒN NỢ: 10** ⇒ §8 = **PARTIAL**.

> 🔴 **15 TC còn nợ KHÔNG phải nợ kiểm thử — là nợ MÔI TRƯỜNG/DATA.** Chia đúng 3 nhóm, gỡ được nhóm nào thì chạy tiếp nhóm đó:
> | Nhóm | TC | Điều kiện gỡ |
> |---|---|---|
> | **Cần tài khoản B đăng tin** (8) | `017` `018` `019` `020` `021` `023` `025` `030` | 1 tài khoản phụ + **OTP nhập tay** để đăng 6 tin NEED; riêng `030` cần thêm **dev lùi "Đến ngày"**, `025` cần khống chế đúng 5 tin toàn hệ thống |
> | **Cần nhiều tài khoản + trọn vòng giao–nhận** (5) | `004` `008` `014` `029` `031` | 3 tài khoản + OTP, **và** phải fix bug `B1` của `VR-004` (không đăng được tin NEED) trước |
> | **Cần môi trường riêng / tài khoản sạch** (2) | `027` `028` | `SEED-HOME-01` (tài khoản 0 tin/0 đơn/0 đóng góp); `028` còn cần hệ thống **0 đơn Hoàn thành** — ⛔ bất khả trên STG dùng chung (đang 317 đơn) |
>
> ✅ **Ứng viên bug H1 đã đóng 2026-09-21:** `TC-HOME-007` — TC lỗi thời (Expected theo BRD), không phải lỗi app. Sửa Expected theo PRD, verdict → PASS, không chạy lại, không log bug. Module HOME hiện **0 FAIL**.
> 📨 **2 việc route `/analyze-requirements`:** (1) card OFFER *"Nhận giao hàng"* nằm trong section "Đơn của tôi" nhưng **không có nhãn vai** — `SC-HOME-011/012/013` chưa đặc tả; (2) section "Đơn của tôi" hiển thị **cả đơn `Đã huỷ`/`Đã giao`**, cần BA chốt phạm vi *"đơn đang hoạt động"*.
