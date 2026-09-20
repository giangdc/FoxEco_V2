# Scope Ledger — VR-004 — module ORD — SCOPE_TOTAL = 88 TC

> Seed từ: `coverage-ORD.md` (trạng thái trước phiên: có verdict cuối **42**/88 · còn nợ **46**)
> Tập chạy phiên này: **toàn bộ 88 TC** (`--all`, user truyền tường minh) · 5 lô
> **Phiên này chốt 46 TC** — **27 PASS · 17 FAIL · 2 BLOCKED**. Trong đó **28 TC lần đầu có verdict**, 18 TC chạy lại theo `--all`.
> **1 TC ĐỔI verdict:** `TC-ORD-017` PASS (VR-002) → **FAIL** (VR-004) — prefill địa chỉ lấy hàng đã mất.
> Sau phiên: có verdict cuối **69**/88 · **CÒN NỢ 19** ⇒ §8 = **PARTIAL**.
> Seed data: **SEED-ORD-02** (dựng lại 2026-09-18 23:43 — `/sdcard` emulator đã trống, `SEED-ORD-01` của VR-002 KHÔNG còn)

> 🛑 **Lý do dừng — KHÔNG phải hết sức phiên:** đã chạy **hết mọi TC có thể chạy**. 19 TC còn nợ đều **chặn tiền đề**: 17 TC cần 1 đơn NEED đăng thành công (bug `TC-ORD-004` — API 400), 2 TC cần tài khoản B.

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-ORD-001 | ✅ PASS | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-001__verify-dang-tin-moi-4-thanh-phan.png` |
| TC-ORD-002 | ✅ PASS | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-002__verify-buoc-1-3-thong-tin-hang.png` |
| TC-ORD-003 | ✅ PASS | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-003__verify-form-1-trang-khong-step-indicator.png` |
| TC-ORD-004 | ❌ FAIL | 2 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-004__step11-FAIL-khong-dang-duoc-tin-api-400.png` |
| TC-ORD-005 | ✅ PASS | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-005__verify-8-chip-mac-dinh-tai-lieu.png` |
| TC-ORD-006 | ❌ FAIL | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-006__step3-FAIL-co-chip-tai-lieu.png` |
| TC-ORD-007 | ❌ FAIL | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-007__verify-nhan-lai-chip-van-duoc-chon.png` |
| TC-ORD-008 | ❌ FAIL | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-008__step6-FAIL-tiep-theo-van-disable-sau-khi-chon-thap.png` |
| TC-ORD-009 | ✅ PASS | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-009__verify-banner-hang-gia-tri-cao.png` |
| TC-ORD-010 | ✅ PASS | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-010__verify-thap-khong-co-banner.png` |
| TC-ORD-011 | ❌ FAIL | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-011__verify-ghi-chu-dung-300-ky-tu.png` |
| TC-ORD-012 | ✅ PASS | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-012__verify-bo-dem-1-tren-5.png` |
| TC-ORD-013 | ✅ PASS | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-013__verify-anh-hang-bat-buoc-0-5-helper.png` |
| TC-ORD-014 | ❌ FAIL | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-014__step4-FAIL-khong-sang-buoc-2-khong-bao-loi-anh.png` |
| TC-ORD-015 | ✅ PASS | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-015__verify-prefill-ten-sdt-nguoi-gui.png` |
| TC-ORD-016 | ✅ PASS | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-016__verify-ten-nguoi-gui-chi-doc.png` |
| TC-ORD-017 | ❌ FAIL | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-017__step3-FAIL-dia-chi-lay-hang-khong-prefill.png` |
| TC-ORD-018 | ✅ PASS | 4 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-018__verify-sdt-nguoi-gui-khong-doi.png` |
| TC-ORD-019 | ❌ FAIL | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-019__step4-FAIL-autofill-thieu-o-dia-chi-giao.png` |
| TC-ORD-020 | ✅ PASS | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-020__verify-email-khong-tra-duoc.png` |
| TC-ORD-021 | ❌ FAIL | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-021__step3-FAIL-khong-bao-loi-email-sai-dinh-dang.png` |
| TC-ORD-022 | ✅ PASS | 4 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-022__verify-sdt-autofill-duoc-chap-nhan-sang-buoc-3.png` |
| TC-ORD-023 | ❌ FAIL | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-023__step5-FAIL-khong-co-thong-bao-loi-nhom-nguoi-nhan.png` |
| TC-ORD-024 | ❌ FAIL | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-024__verify-ten-nguoi-nhan-bien-60-61.png` |
| TC-ORD-025 | ✅ PASS | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-025__verify-sdt-10-so-hop-le.png` |
| TC-ORD-026 | ✅ PASS | 4 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-026__verify-loi-trung-dia-chi-hien-dung.png` |
| TC-ORD-027 | ✅ PASS | — | — | Prefill đúng `363 Nguyễn Hữu Thọ, Cẩm Lệ` (khớp hồ sơ) + sửa được |
| TC-ORD-028 | ✅ PASS | — | — | Ô tự do, không preset/chip gợi ý (`address-suggestion-0` NOT FOUND) |
| TC-ORD-029 | ✅ PASS | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-029__verify-dropdown-autocomplete-khong-co-chip-preset.png` |
| TC-ORD-030 | ✅ PASS | — | — | Ngày quá khứ **mờ/disabled** trong picker; tap ngày 17 không có tác dụng |
| TC-ORD-031 | ✅ PASS | — | — | Sau khi Từ ngày=21/09, các ngày 19–20 chuyển disabled ⇒ không chọn được Đến ngày sớm hơn |
| TC-ORD-032 | ✅ PASS | 4 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-032__verify-gio-nao-cung-duoc-bo-chon-cac-buoi.png` |
| TC-ORD-033 | 🚫 BLOCKED | 4 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-033__step5-BLOCKED-v11-khong-co-khung-gio-mac-dinh.png` |
| TC-ORD-034 | ✅ PASS | 2 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-034__verify-tom-tat-buoc-3.png` |
| TC-ORD-035 | ✅ PASS | 2 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-035__verify-banner-hang-cam.png` |
| TC-ORD-036 | ✅ PASS | 2 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-036__verify-checkbox-dieu-khoan-chua-tick.png` |
| TC-ORD-037 | ✅ PASS | 2 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-037__verify-step6-dang-tin-ngay-enable.png` |
| TC-ORD-038 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần đăng tin loại `Thuốc/Y tế` |
| TC-ORD-039 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần màn *Đăng tin thành công* |
| TC-ORD-040 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần màn *Đăng tin thành công* (2 lần) |
| TC-ORD-041 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần màn *Đăng tin thành công* |
| TC-ORD-042 | ✅ PASS | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-042__verify-form-offer-nhom-truong-giua.png` |
| TC-ORD-043 | ❌ FAIL | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-043__step8-FAIL-khong-co-thong-bao-loi-diem-den-trung.png` |
| TC-ORD-044 | ⏳ NOT_RUN | — | — | ⏳ **Chặn vì thiếu tài khoản B** — TC đòi 2 CBNV khác nhau, phiên chỉ có OTP của tài khoản A |
| TC-ORD-045 | ⏳ NOT_RUN | — | — | ⏳ **Chặn vì thiếu tài khoản B** — TC đòi 2 CBNV khác nhau, phiên chỉ có OTP của tài khoản A |
| TC-ORD-046 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần đơn ở trạng thái `Chờ ghép` (đơn có sẵn duy nhất đang `Đã ghép`) |
| TC-ORD-047 | ✅ PASS | 5 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-047__verify-tin-da-ghep-khong-co-nut-chinh-sua.png` |
| TC-ORD-048 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần đơn `Chờ ghép` quá hạn `Đến ngày` |
| TC-ORD-049 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · Expected đòi timestamp **khớp thời điểm bấm đăng** ⇒ không dùng được đơn cũ |
| TC-ORD-050 | ❌ FAIL | 2 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-050__step8-FAIL-offer-nut-gui-enabled-khi-thieu-du-lieu.png` |
| TC-ORD-051 | ❌ FAIL | 5 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-051__step3-FAIL-khong-co-loi-duoi-o-ten-nguoi-nhan.png` |
| TC-ORD-052 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần đơn đã lưu để đọc lại tên/SĐT sau chuẩn hoá |
| TC-ORD-053 | ❌ FAIL | — | — | 🐞🔴 Bug thật — KHÔNG có popup "Thoát và bỏ nội dung đã nhập?", app thoát thẳng + xoá dữ liệu soạn dở (trái `AC-01.2.01`/`C-ORD-08`). Cùng họ `TC-USR-045` ⇒ nghi lỗi hệ thống chung (F4) |
| TC-ORD-054 | ✅ PASS | 1 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-054__verify-khong-co-field-so-tien.png` |
| TC-ORD-055 | ✅ PASS | 3 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-055__verify-dia-chi-giao-dung-200-ky-tu.png` |
| TC-ORD-056 | ✅ PASS | — | — | Khoảng đúng 7 ngày (18→25/09) được nhận, không lỗi ⇒ biên trên hợp lệ đúng `C-ORD-15(a)` |
| TC-ORD-057 | ✅ PASS | — | — | Nhận giá trị +8 nhưng **hiện lỗi inline** "Đến ngày tối đa 7 ngày kể từ Từ ngày" ⇒ thoả nhánh "hoặc hiện lỗi" của Expected. 🔑 Ca đối chứng cho F3/F7 |
| TC-ORD-058 | ❌ FAIL | — | — | 🐞 Không có buổi nào được chọn sẵn (Expected: `Sau giờ làm (17–19)`); app hiện luôn lỗi "Chọn ít nhất 1 buổi". Căn cứ log bug: PRD `§8.1.4` |
| TC-ORD-059 | ❌ FAIL | — | — | 🐞 13:44 vẫn chọn được buổi `Sáng (8–12h)` của hôm nay ⇒ trái `C-ORD-15(b)`. Khi log bug PHẢI dẫn `C-ORD-15(b)` (rule không có trong PRD) |
| TC-ORD-060 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần đơn `Chờ ghép` để mở form sửa |
| TC-ORD-061 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần đơn `Đã ghép` quá hạn `Đến ngày` |
| TC-ORD-062 | ✅ PASS | — | — | Form mở lại trắng + 2 tab Hoạt động không có tin nháp. Step 3 thực hiện lệch vì popup không tồn tại (defect do `TC-ORD-053` sở hữu) |
| TC-ORD-063 | ❌ FAIL | — | — | 🐞🔴 Ứng viên bug P1 — CHẶN ĐÚNG nhưng chặn IM LẶNG, không có thông báo lỗi ở khối ẢNH HÀNG (F3) |
| TC-ORD-064 | ❌ FAIL | — | — | 🐞 F3 — chặn đúng + 3 nhãn chip khớp oracle `C-ORD-18` ("TRỌNG LƯỢNG", Nhẹ/Trung bình/Nặng), nhưng KHÔNG có thông báo lỗi ở khối |
| TC-ORD-065 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · Expected là *đăng tin được bình thường* |
| TC-ORD-066 | ❌ FAIL | — | — | 🐞 F3 — chặn đúng + 3 nhãn chip Kích thước khớp Expected, nhưng KHÔNG có thông báo lỗi ở khối |
| TC-ORD-067 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · Expected là *đăng tin được bình thường* |
| TC-ORD-068 | ✅ PASS | — | — | Từ chối + thông báo "Ảnh vượt quá 5MB, vui lòng chọn ảnh nhỏ hơn." + bộ đếm vẫn 0/5 |
| TC-ORD-069 | 🚫 BLOCKED | — | — | Không có đường UI để chọn `.pdf` (chỉ camera + Android Photo Picker, picker lọc sẵn ảnh) ⇒ không quan sát được thông báo lỗi của app. 📨 QC chốt N-A hoặc đổi Expected; ⛔ không PASS vì thiếu đường thử |
| TC-ORD-070 | ✅ PASS | — | — | ♻️ **2 lần đổi verdict**: 🚫 BLOCKED → ❌ FAIL → ✅ **PASS**. QC GiangDC2 chốt 2026-09-18 *"đủ 5 file bỏ bộ đếm luôn"* ⇒ **Expected đã sửa** (bỏ vế `5/5`, assert bộ đếm ở `4/5`) ⇒ app đúng, ⛔ không bug |
| TC-ORD-071 | ✅ PASS | — | — | ♻️ **Recheck 2026-09-18 chiều — đổi 🚫 BLOCKED → ✅ PASS.** Dựng được 5 ảnh, xoá **đúng ảnh thứ ba**, bộ đếm về `4/5`, nút thêm hiện lại |
| TC-ORD-072 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần đơn kèm **5 ảnh** (đơn có sẵn không đủ ảnh) |
| TC-ORD-073 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần đơn kèm 5 ảnh để mở lightbox |
| TC-ORD-074 | ❌ FAIL | — | — | 🐞 P1 — chỉ 2/3 ô tự điền (tên ✓ SĐT ✓, **địa chỉ giao RỖNG**). Cần BA chốt trước khi log bug: HRIS có địa chỉ ⇒ bug app, hay spec chỉ autofill 2 ô ⇒ sửa Expected. 📨 route analyze |
| TC-ORD-075 | ✅ PASS | — | — | Chặn đúng `C-ORD-14` (nút disable kể cả khi điền tay đủ). 🚩 Chuỗi hướng dẫn còn của v1.0 ("vui lòng nhập tay…") ⇒ text-defect, xem F5 |
| TC-ORD-076 | ✅ PASS | — | — | Email người nghỉ việc cũng chặn; app không phân biệt "nghỉ việc" vs "không tồn tại" (cùng 1 chuỗi) |
| TC-ORD-077 | ❌ FAIL | — | — | 🐞 F3 — vế "không tra danh bạ" đúng (3 ô vẫn trống), vế "hiện lỗi định dạng" SAI: không có thông báo nào |
| TC-ORD-078 | ✅ PASS | — | — | Có dòng lỗi + 3 ô vẫn trống ⇒ PASS. 🚩 Chuỗi là thông báo chung "không tìm thấy email", không nói rõ ngoài tên miền (F5) |
| TC-ORD-079 | ✅ PASS | 4 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-079__verify-sdt-uy-quyen-sai-dinh-dang-bao-loi.png` |
| TC-ORD-080 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần đơn đã đăng để đọc nhãn `Người gửi chỉ định` |
| TC-ORD-081 | ✅ PASS | 4 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-081__verify-ten-uy-quyen-1-ky-tu-bi-chan.png` |
| TC-ORD-082 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần đăng tin thành công sau khi xoá khối uỷ quyền |
| TC-ORD-083 | ❌ FAIL | 4 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-083__step5-FAIL-khong-co-loi-o-o-dia-chi-giao.png` |
| TC-ORD-084 | ❌ FAIL | 4 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-084__step5-FAIL-khong-co-loi-khi-chi-khac-khoang-trang.png` |
| TC-ORD-085 | ❌ FAIL | 5 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-085__verify-copy-dia-chi-giao.png` |
| TC-ORD-086 | 🚫 BLOCKED | 5 | **run này (VR-004)** | `VR-004-ORD-2026-09-18/screenshots/TC-ORD-086__step3-BLOCKED-khong-co-sdt-tren-man-chi-tiet.png` |
| TC-ORD-087 | ✅ PASS | — | — | Xoá đúng ảnh được chọn, bộ đếm 2/5 → 1/5 |
| TC-ORD-088 | ⏳ NOT_RUN | — | — | ⏳ **Chặn bởi bug `TC-ORD-004`** — cần 1 đơn NEED đăng thành công, hiện API trả 400. KHÔNG phải hết sức phiên · cần đơn `Chờ ghép` có 2 ảnh + nút `Chỉnh sửa` |
