# Scope Ledger — VR-011 — module GIFT — SCOPE_TOTAL = 14 TC

> Seed từ: `coverage-GIFT.md` (trạng thái trước phiên: có verdict 0/14 — file mới, GIFT chưa từng vibe-test)
> Tập chạy phiên này: **pending 14 TC** (không có TC nào đã PASS ⇒ ⛔ không cần hỏi Step 1.2) · Lô 20 TC ⇒ 1 lô
> Nguồn scope: hợp 2 file TC-MASTER (v1.1 8 TC ∪ v1.0 6 TC riêng) — xem `coverage-GIFT.md`
> Tài khoản chạy (theo thứ tự, gom việc **theo TÀI KHOẢN** đúng `USR-accounts.md §2`):
> - **Lô 1** — `stag_taipm@fpt.com` (Phan Minh Tài, MNV `00041796`) — vai **Người gửi**: TC-001/002/003/004/005/007/009/010/013/014
> - **Lô 2** — `stag_giangdc2@fpt.com` (Đặng Châu Giang) — vai **Người vận chuyển nhận quà**: TC-012
> - **Lô 3** — `stag_anhptm17@fpt.com` (Phan Thị Mỹ Anh, MNV `00287493`) — tài khoản có **5 quà / 2 loại**: TC-006 · thăm dò TC-008 + TC-011
>
> Kết quả phiên: **12/14 có verdict cuối** (**7P / 2F / 2B / 1 NOT_EVIDENCED** — sau đính chính `TC-GIFT-001`/`010`, xem cuối file) · **còn nợ 2** (TC-GIFT-008 · TC-GIFT-011, cả hai là **nợ SEED**)

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-GIFT-001 | ✅ PASS | 1 | run này | `TC-GIFT-001__verify-man-tang-qua-mo-tu-card.png` |
| TC-GIFT-002 | ✅ PASS | 1 | run này | `TC-GIFT-002__verify-4-loai-qua-dung-ten.png` |
| TC-GIFT-003 | ❌ FAIL | 1 | run này | `TC-GIFT-003__step5-FAIL-sai-chuoi-popup.png` |
| TC-GIFT-004 | ✅ PASS | 1 | run này | `TC-GIFT-004__verify-khong-co-thanh-toan.png` |
| TC-GIFT-005 | ✅ PASS | 1 | run này | `TC-GIFT-005__verify-nhan-nut-sau-khi-tang-qua.png` |
| TC-GIFT-006 | ✅ PASS | 3 | run này | `TC-GIFT-006__verify-card-dem-2-loai-tong-5.png` |
| TC-GIFT-007 | ✅ PASS | 1 | run này | `TC-GIFT-007__verify-co-danh-sach-lich-su-nhan-qua.png` |
| TC-GIFT-008 | ⏳ NOT_RUN | 3 | *(thăm dò, không chạy được)* | **Lý do:** ⛔ **KHÔNG còn tài khoản CBNV "trắng" nào trên STG.** `stag_anhptm17@` — tài khoản vẫn được `USR-accounts.md §2` giữ làm *"dự phòng/sạch"* — thực tế đã **5 đơn đã giúp / 5 quà đã nhận** (kiểm 2026-09-19, ảnh `_recon__ca-nhan-anhptm17-5-don-5-qua.png`). 4 acc còn lại cũng bẩn (`taipm` 2/1 · `giangdc2` 13/13 · `anhdc4` 3/2 · `huyennhk` không vào được FoxEco). ⇒ **cần dev/QA cấp account mới tinh** (dùng chung với `SEED-ACT-02` + `SEED-HOME-01`) |
| TC-GIFT-009 | ✅ PASS | 1 | run này | `TC-GIFT-009__verify-ve-man-ca-nhan.png` |
| TC-GIFT-010 | ⚠️ NOT_EVIDENCED | 1 | run này | `TC-GIFT-010__step4-FAIL-back-ve-danh-sach-khong-ve-theo-doi-don.png` |
| TC-GIFT-011 | ⏳ NOT_RUN | — | *(hết tiền đề)* | **Lý do:** cần `SEED-GIFT-06` = 1 đơn Hoàn thành **RIÊNG** chưa tặng quà (TC tiêu đơn để mở được popup + "Quà đã nhận"). Tài khoản có đúng **2** đơn đủ điều kiện, đã bị `TC-GIFT-003` và `TC-GIFT-005` (đều P2, ưu tiên cao hơn P3) tiêu hết → cần seed thêm đơn Hoàn thành |
| TC-GIFT-012 | ❌ FAIL | 2 | run này | `TC-GIFT-012__step4-FAIL-mo-qua-da-nhan-khong-phai-trang-ca-nhan.png` |
| TC-GIFT-013 | 🚫 BLOCKED | 1 | run này | `TC-GIFT-013__step1-BLOCKED-khong-co-don-returned.png` |
| TC-GIFT-014 | 🚫 BLOCKED | 1 | run này | `TC-GIFT-014__step3-BLOCKED-khong-co-nhanh-hoan-hang.png` |

## 🔁 Đính chính trong phiên — `TC-GIFT-001` · `TC-GIFT-010`: ❌ FAIL → ✅ PASS

Hai TC này **lúc chạy bị chấm FAIL** vì luồng app khác chữ trong TC. Đối chiếu tài liệu phân tích của chính dự án cho thấy chấm vậy **sai quy kết**:

| TC | Căn cứ đổi verdict |
|---|---|
| `TC-GIFT-001` | `SC-GIFT-001` **Then** = *"Mở màn "Tặng quà" với 4 lựa chọn quà"* → **app đạt**. `C-GIFT-04` **Resolved 2026-09-17** chốt app route **theo trạng thái tặng quà** (chưa tặng → "Tặng quà" · đã tặng → "Theo dõi đơn") ⇒ luồng app là **đúng thiết kế đã chốt**, không phải defect |
| `TC-GIFT-010` | `SC-GIFT-010` **Then** = *"Về đúng màn trước đó **(Theo dõi đơn / Đơn của tôi)**"* ⇒ app về `Đơn của tôi` **nằm trong tập chấp nhận**. `C-GIFT-02` **Resolved 2026-09-16**: rule = *"back về màn hình trước đó"* — màn đã mở "Tặng quà" chính là danh sách |

⇒ Phần lệch còn lại của 2 TC là **chữ trong TC đã lỗi thời** ⇒ xử lý bằng **sửa TC ở lượt bảo trì**, ⛔ **không log bug**.
⚠️ Ảnh evidence **giữ nguyên tên** (`TC-GIFT-001__step3-FAIL-*`, `TC-GIFT-010__step4-FAIL-*`) — chụp lúc đang chấm FAIL; **đổi tên ảnh sau khi chụp là thao tác bị cấm**, và nội dung ảnh vẫn đúng.

🧾 **Hệ quả: `TC-GIFT-010` phải xuống ⚠️ NOT_EVIDENCED.** `TC-GIFT-001` vẫn có ảnh `__verify` riêng nên lên PASS được; `TC-GIFT-010` thì **không còn file `__verify*`** sau khi đổi verdict. Chụp lại **bất khả thi trong phiên**: màn "Tặng quà" chỉ mở từ đơn Hoàn thành **chưa tặng quà**, mà cả 4 tài khoản vào được FoxEco đều đã hết loại đơn này (2 đơn cuối bị `TC-GIFT-003`/`005` tiêu; đã kiểm thêm `stag_anhptm17@` + `stag_anhdc4@`). ⇒ **Chạy lại:** `/vibe-test --tc TC-GIFT-010`.
