# Coverage — module GIFT — SCOPE_TOTAL = 14 TC

> Sổ cái TÍCH LŨY xuyên run cho module GIFT (Quà cảm ơn — v1.0 + v1.1).
> **Cập nhật lần cuối: VR-028 (2026-09-23)** · Nguồn scope: `03_test-cases/v1.1/TC-MASTER-v1.1.xlsx` sheet `Quà cảm ơn` (8 TC) **∪** `03_test-cases/v1.0/TC-MASTER-v1.0.xlsx` sheet `Quà cảm ơn` (12 TC) — hợp nhất 14 TC, 6 TC trùng ID lấy **bản v1.1**
> **Tổng: có verdict cuối 12/14 · CÒN NỢ 2** (1 NOT_RUN + 1 NOT_EVIDENCED)
> Verdict hợp lệ: ✅ PASS · ❌ FAIL · 🚫 BLOCKED · ⚠️ NOT_EVIDENCED · ⏳ NOT_RUN · ⛔ N-A

> 🆕 **2026-09-19 — file mới, khởi tạo bởi VR-011.** GIFT chưa từng được vibe-test trước phiên này.
> 🔴 **SCOPE_TOTAL = 14 là HỢP của 2 file TC-MASTER** (CLAUDE.md §TC-MASTER: v1.1 KHÔNG gộp TC CARRIED).
> 6 TC chỉ có ở v1.0: `TC-GIFT-001/004/005/009/010/012`. 8 TC lấy bản v1.1: `002/003/006/007/008/011/013/014`.

## Tiến độ theo run

| Run | Ngày | TC chạy trong run | Verdict thu được |
|-----|------|-------------------|------------------|
| VR-011 | 2026-09-19 | **12** | 8P / 1F / 2B / 1NE *(sau đính chính `TC-GIFT-012` 2026-09-21)* |
| VR-028 | 2026-09-23 | **1** | 1P (`TC-GIFT-008`) — QC dừng phiên trước `TC-GIFT-011` |

## Chi tiết từng TC

| Testcase ID | Verdict | Scenario ID | Priority | Title | Run | Evidence | Ghi chú |
|---|---|---|---|---|---|---|---|
| TC-GIFT-001 | ✅ PASS | SC-GIFT-001 | P2 | Check người gửi nhấn "✓ Cảm ơn người vận chuyển" mở màn "Tặng quà" | VR-011 | `VR-011-GIFT-2026-09-19/screenshots/TC-GIFT-001__verify-man-tang-qua-mo-tu-card.png` | Then của `SC-GIFT-001` (*mở màn "Tặng quà" với 4 lựa chọn*) **ĐẠT**. 📝 Steps 3–4 của TC viết trước khi `C-GIFT-04` được BA trả lời ⇒ **sửa TC**, ⛔ không log bug. 🔴 Spec-gap TÁCH RIÊNG: nút `"✓ Cảm ơn người vận chuyển"` (`KB-GIFT-01` ô 5·Sender) **không tồn tại trên app** → `/analyze-requirements --update` |
| TC-GIFT-002 | ✅ PASS | SC-GIFT-002 | P2 | Check màn "Tặng quà" hiển thị đúng tên bốn loại quà theo danh mục chính thức | VR-011 | `VR-011-GIFT-2026-09-19/screenshots/TC-GIFT-002__verify-4-loai-qua-dung-ten.png` | Đúng 4 ô quà (`instance(4)` 🚫), đúng tên `BR14-01` |
| TC-GIFT-003 | ❌ FAIL | SC-GIFT-003 | P2 | Check gửi quà hiện đúng popup "Cảm ơn của bạn đã được gửi" kèm nút về trang chủ | VR-011 | `VR-011-GIFT-2026-09-19/screenshots/TC-GIFT-003__step5-FAIL-sai-chuoi-popup.png` | 🐞 **Lệch copy popup** — hiện `"Đã gửi lời cảm ơn!"` (chuỗi v1.0 đã bỏ) thay vì chuỗi `BR14-02`. Gửi ngay ✅ + nút về trang chủ ✅. ⚠ Cần BA chốt đọc chặt/lỏng trước khi log bug · ⏸ **2026-09-21 (QC):** đã log **FE-308**; ⛔ không hỏi BA riêng — **chờ FE-308 đổi trạng thái trên Jira rồi tính tiếp** (retest khi Fixed / đóng + sửa Expected nếu Won't Fix) |
| TC-GIFT-004 | ✅ PASS | SC-GIFT-004 | P3 | Check màn "Tặng quà" không có thành phần thanh toán hay quy đổi tiền | VR-011 | `VR-011-GIFT-2026-09-19/screenshots/TC-GIFT-004__verify-khong-co-thanh-toan.png` | 0 thành phần tiền tệ/ví/thanh toán/quy đổi điểm — `BR-GIFT-01` khớp |
| TC-GIFT-005 | ✅ PASS | SC-GIFT-005 | P2 | Check sau khi gửi quà nút đổi nhãn "Bạn đã đánh giá" và không gửi lại được cho cùng đơn | VR-011 | `VR-011-GIFT-2026-09-19/screenshots/TC-GIFT-005__verify-nhan-nut-sau-khi-tang-qua.png` | E5+E6 đạt: nhãn `"Bạn đã đánh giá"` + **không có tổ tiên clickable** ⇒ disable thật; ⛔ không mở lại "Tặng quà". ⚠ Step 4 (back) sai — defect đã chấm FAIL ở `TC-GIFT-010`, ⛔ không đếm trùng |
| TC-GIFT-006 | ✅ PASS | SC-GIFT-006 | P2 | Check card đếm quà hiển thị đúng từng loại và tổng khi nhận 5 quà thuộc 2 loại | VR-011 | `VR-011-GIFT-2026-09-19/screenshots/TC-GIFT-006__verify-card-dem-2-loai-tong-5.png` | Chạy trên `stag_anhptm17@` — **5 quà / 2 loại / 3+2**, khớp cardinality `SEED-GIFT-05`. ⚠ **Hoán tên loại có khai:** `Ly cà phê 3` + `Vương miện 2` thay cho `Bông hoa 3` + `Gấu bông 2`; 2 loại count=0 **không hiện** ✅. Đề nghị BA bỏ ràng buộc tên loại trong seed |
| TC-GIFT-007 | ✅ PASS | SC-GIFT-007 | P2 | Check màn "Quà đã nhận" có danh sách lịch sử nhận quà | VR-011 | `VR-011-GIFT-2026-09-19/screenshots/TC-GIFT-007__verify-co-danh-sach-lich-su-nhan-qua.png` | 🔑 Đóng `C-GIFT-03` vế (b) — app **CÓ** khối `LỊCH SỬ NHẬN QUÀ`, số dòng khớp số quà. ⚠ Test Data lệch: 1 quà thay vì `SEED-GIFT-05` 5 quà (assert chính vẫn quyết được) |
| TC-GIFT-008 | ✅ PASS | SC-GIFT-008 | P3 | Check empty state "Quà đã nhận" đúng text và không có CTA | VR-028 | `VR-028-GIFT-2026-09-23/screenshots/TC-GIFT-008__verify-empty-state-qua-da-nhan.png` | Chạy trên `stag_minhndn2@` (tài khoản trắng): "Chưa nhận được quà nào" · thống kê 0/0 · không CTA (chỉ có `Quay lại`) |
| TC-GIFT-009 | ✅ PASS | SC-GIFT-009 | P3 | Check nhấn quay lại ở màn "Quà đã nhận" trở về màn Cá nhân | VR-011 | `VR-011-GIFT-2026-09-19/screenshots/TC-GIFT-009__verify-ve-man-ca-nhan.png` | 📝 Expected ghi *"2 mục menu"* là số cũ v1.0 — app có **3 mục**; sửa TC ở lượt bảo trì, ⛔ không log bug |
| TC-GIFT-010 | ⚠️ NOT_EVIDENCED | SC-GIFT-010 | P3 | Check nhấn quay lại ở màn "Tặng quà" trở về màn Theo dõi đơn của đúng đơn vừa mở | VR-011 | `VR-011-GIFT-2026-09-19/screenshots/TC-GIFT-010__step4-FAIL-back-ve-danh-sach-khong-ve-theo-doi-don.png` | **Nội dung ĐẠT** (app về `Đơn của tôi` = nằm trong Then của `SC-GIFT-010`; `KB-GIFT-04` **không tái hiện**) **nhưng ảnh nằm SAI SLOT** — chụp lúc đang chấm FAIL, sau đó verdict được đính chính; ⛔ **không đổi tên ảnh** (luật cấm). Chụp lại **không được** vì STG đã hết sạch đơn Hoàn thành chưa tặng quà. **Chạy lại:** `/vibe-test --tc TC-GIFT-010` sau khi có 1 đơn đủ điều kiện |
| TC-GIFT-011 | ⏳ NOT_RUN | SC-GIFT-011 | P3 | Check không có sao, điểm, tier hay chỉ số môi trường trên cả 4 bề mặt của luồng tặng quà | — | — | **Lý do:** cần `SEED-GIFT-06` = 1 đơn Hoàn thành **RIÊNG** chưa tặng quà (TC tiêu đơn để mở được popup + "Quà đã nhận"). Tài khoản có đúng **2** đơn đủ điều kiện, đã bị `TC-GIFT-003` và `TC-GIFT-005` (đều P2, ưu tiên cao hơn P3) tiêu hết → cần seed thêm đơn Hoàn thành |
| TC-GIFT-012 | ✅ PASS | SC-GIFT-012 | P2 | Check người vận chuyển nhận thông báo quà cảm ơn và nhấn vào mở Trang cá nhân | VR-011 | `VR-011-GIFT-2026-09-19/screenshots/TC-GIFT-012__verify-thong-bao-qua-cam-on.png` *(+ màn đích ở `…__step4-FAIL-mo-qua-da-nhan-khong-phai-trang-ca-nhan.png`, giữ tên vì chụp lúc chấm FAIL)* | 🔁 **Đính chính 2026-09-21 — QC chốt: mở "Quà đã nhận" là ĐÚNG**, Expected step 4 đã sửa, ⛔ không bug. Thông báo `NTF-07` CÓ, khớp verbatim (thiếu emoji 🎁 — trang trí) |
| TC-GIFT-013 | 🚫 BLOCKED | SC-GIFT-013 | P2 | Check đơn RETURNED không có nút tặng quà và vẫn hiện trong lịch sử đơn | VR-011 | `VR-011-GIFT-2026-09-19/screenshots/TC-GIFT-013__step1-BLOCKED-khong-co-don-returned.png` | **STG chưa build `FR09`** — không có đơn `RETURNED` nào; thanh trạng thái chỉ 5 bước, không có nhánh hoàn hàng. Gỡ blocker = dev build `FR09`, chạy lại cùng lô `TC-DLV-053..056` |
| TC-GIFT-014 | 🚫 BLOCKED | SC-GIFT-014 | P2 | Check đơn RETURNED không được tính vào chỉ số "Đơn đã giúp" | VR-011 | `VR-011-GIFT-2026-09-19/screenshots/TC-GIFT-014__step3-BLOCKED-khong-co-nhanh-hoan-hang.png` | Cùng blocker `FR09` — không đẩy được đơn sang `RETURNED`. Đã ghi mốc **N = 2** ở step 2 để dùng cho lượt sau |

## Tổng hợp

| Verdict | Số | TC |
|---|---|---|
| ✅ PASS | 9 | `TC-GIFT-001` · `TC-GIFT-002` · `TC-GIFT-004` · `TC-GIFT-005` · `TC-GIFT-006` · `TC-GIFT-007` · `TC-GIFT-008` · `TC-GIFT-009` · `TC-GIFT-012` |
| ❌ FAIL | 1 | `TC-GIFT-003` *(→ Jira FE-308)* |
| 🚫 BLOCKED | 2 | `TC-GIFT-013` · `TC-GIFT-014` |
| ⚠️ NOT_EVIDENCED | 1 | `TC-GIFT-010` |
| ⏳ NOT_RUN | 1 | `TC-GIFT-011` |
| ⛔ N-A | 0 | — |
| **Tổng** | **14** | |

**Có verdict cuối: 12/14 · CÒN NỢ: 2** ⇒ §8 = **PARTIAL**.

> 🔁 **ĐÍNH CHÍNH 2026-09-21 — `TC-GIFT-012` ❌ FAIL → ✅ PASS (QC chốt).** `TC-GIFT-012` đổi **❌ FAIL → ✅ PASS** theo quyết định của QC GiangDC2: nhấn thông báo `NTF-07` mở thẳng màn **"Quà đã nhận"** là **ĐÚNG hành vi**, ⛔ không phải bug. Expected step 4 của TC đã sửa cho khớp (fragment `TC-GIFT-v1.0.md` + `TC-MASTER-v1.0.xlsx` 2 sheet `Quà cảm ơn`/`ALL`, số dòng TC không đổi) và **draft `BUG-022` đã xoá**. Evidence: ảnh `TC-GIFT-012__verify-thong-bao-qua-cam-on.png` (slot `verify`, chứng minh thông báo) + `TC-GIFT-012__step4-FAIL-mo-qua-da-nhan-khong-phai-trang-ca-nhan.png` (màn đích; ⛔ **giữ nguyên tên** file vì chụp lúc đang chấm FAIL — nội dung ảnh chính là màn "Quà đã nhận" mà Expected mới yêu cầu). ⚠️ Chưa chụp lại ảnh màn đích ở slot `verify` — cần đăng nhập lại `stag_giangdc2@` trên thiết bị (đang dùng cho phiên VR-013); làm được bằng thông báo thứ 2 ("17 phút trước") nếu QC muốn ảnh đúng slot. ⚠️ Thiếu emoji 🎁 ở thông báo vẫn là quan sát trang trí, không hạ verdict.

> 🔁 **ĐÍNH CHÍNH TRONG PHIÊN VR-011 — `TC-GIFT-001` và `TC-GIFT-010` đã đổi ❌ FAIL → ✅ PASS.**
> Lúc chạy, 2 TC này bị chấm FAIL vì luồng app khác chữ trong TC. Đối chiếu **tài liệu phân tích của chính dự án** cho thấy chấm vậy là **sai quy kết** — app khớp **Then của scenario** và khớp **câu trả lời BA đã Resolved**:
> - `SC-GIFT-001` Then = *"Mở màn "Tặng quà" với 4 lựa chọn quà"* → **đạt**; `C-GIFT-04` Resolved 2026-09-17 chốt app route **theo trạng thái tặng quà** (chưa tặng → "Tặng quà" · đã tặng → "Theo dõi đơn").
> - `SC-GIFT-010` Then = *"Về đúng màn trước đó **(Theo dõi đơn / Đơn của tôi)**"* → app về `Đơn của tôi` = **nằm trong tập chấp nhận**; `C-GIFT-02` Resolved 2026-09-16 chốt rule *"back về màn hình trước đó"*.
> ⇒ Phần lệch còn lại của 2 TC là **chữ trong TC đã lỗi thời**, xử lý bằng **sửa TC**, ⛔ không log bug.
>
> 🧾 **Hệ quả evidence của việc đính chính — `TC-GIFT-010` phải xuống ⚠️ NOT_EVIDENCED:** ảnh của nó chụp lúc đang chấm FAIL nên mang slot `__step4-FAIL`; khi verdict đổi sang PASS thì TC **không còn file `__verify*`**. Luật cấm đổi tên/copy ảnh cho khớp gate, và **chụp lại không được** vì STG đã **hết sạch** đơn Hoàn thành chưa tặng quà *(đã kiểm cả 4 tài khoản vào được FoxEco)*. ⇒ **giữ ở danh sách nợ**, chạy lại bằng `/vibe-test --tc TC-GIFT-010` khi có đơn đủ điều kiện. Kết luận nội dung (app đúng · `KB-GIFT-04` không tái hiện) **vẫn dùng được** cho `/analyze-requirements`, ⛔ chỉ không được tính là PASS.

> 🔴 **1 FAIL còn lại là nợ DEV/BA — ⛔ không sửa Expected theo app để làm xanh:**
> - `TC-GIFT-003`: popup còn chuỗi v1.0 `"Đã gửi lời cảm ơn!"` thay vì chuỗi `BR14-02` ⇒ đã log **[FE-308](https://foxproject.atlassian.net/browse/FE-308)** (2026-09-21, assignee Tuanvm37). ⏸ **QC chốt 2026-09-21: chờ FE-308 đổi trạng thái trên Jira rồi tính tiếp** (không hỏi BA riêng).
> - ~~`TC-GIFT-012`~~ — đã đóng, xem khối đính chính bên dưới.
>
> 🔴 **1 spec-gap tách riêng, KHÔNG gắn với TC nào FAIL:** nút `"✓ Cảm ơn người vận chuyển"` mà `KB-GIFT-01` (ô 5·Sender) và **`SC-GIFT-001` When** mô tả **không tồn tại trên app** → `/analyze-requirements --update`.
>
> 🔒 **2 BLOCKED (`013`/`014`) chỉ mở được khi dev build `FR09`** (luồng hoàn hàng) — chạy lại cùng lô `TC-DLV-053..056`.
>
> ⏳ **2 NOT_RUN đều là nợ SEED, ⛔ không phải nợ thực thi:**
> - `TC-GIFT-011` cần **1 đơn Hoàn thành chưa tặng quà** (2 đơn cuối đã tiêu cho `003`/`005`, đều P2).
> - `TC-GIFT-008` cần **1 tài khoản CBNV trắng** — ~~STG không còn cái nào~~ → 🆕 **QC cấp `stag_MinhNDN2@fpt.com` (2026-09-21)**, SĐT HRIS chưa cập nhật; ⚠️ chưa login xác nhận là 0 đơn / 0 quà. **Chạy `008` TRƯỚC khi tạo đơn** bằng tài khoản này.
