---
id: v1.1/ORD-dang-tin/risk
title: Risk Assessment — v1.1 · Module ORD
type: risk-assessment
version: v1.1
sprint: 1
module: ORD
counts:
  cl: 11
  risk: 12
  cl_open: 2
  cl_resolved: 8
status: ANALYZED
updated: 2026-09-16
---

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (8 dòng, `RISK-ORD-01..08`) xem `v1.0/ORD-dang-tin/risk_assessment.md` — KHÔNG lặp lại ở đây. **ID mới bắt đầu từ `RISK-ORD-09`.**
> ℹ️ `cl_open (2) + cl_resolved (8) = 10 < cl (11)` — **đúng, không lệch cộng**: `C-ORD-09` ở trạng thái **🟡 Partially Resolved**, không thuộc 2 ô đó (cùng quy ước với `C-NTF-02` ở `ASN`).

## Tổng quan
| Module | Risk Level | Rủi ro chính (delta v1.1) |
|--------|-----------|--------------|
| ORD | **High** (không đổi) | Module đóng được nhiều CL nhất (**4 Resolved**) nhưng cũng lộ ra vấn đề nặng nhất lượt này: **PRD tự mâu thuẫn với chính nó** — field spec để *"Thuốc/Y tế"* là loại hàng hợp lệ trong khi `BR01-07` xếp *"thuốc"* vào **hàng cấm không được đăng** (`RISK-ORD-10`). Kèm theo: ảnh chuyển thành **bắt buộc chặn luồng** (app có thể chưa siết) và **tích hợp danh bạ nội bộ** — tiền đề test có thể không seed được |

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-ORD-10 | ORD / Mâu thuẫn nội tại của PRD | **(risk mới — nặng nhất lượt này)** `§8.1.4` để **"Thuốc/Y tế"** là 1 trong 8 giá trị hợp lệ của Loại hàng, trong khi `BR01-07` viết *"Hàng cấm (**thuốc**, vũ khí, chất nguy hiểm, hàng phi pháp) **không được đăng**"*. Hai câu **không thể cùng đúng** ⇒ không biết viết TC theo chiều nào; và vì v1.0 đã Resolved *"KHÔNG chặn"*, người đọc dễ lướt qua mà không thấy mâu thuẫn | **High** | `DOC-v1.1-01` §8.1.4 UI/Field Spec (trang 35) vs §8.1.1 BR01-07 (trang 34) — **cùng một tài liệu, cách nhau 1 trang** | `SC-ORD-031..035` (cụm consent + hàng cấm) — GHI NHẬN hành vi thật, ⛔ không assert chiều nào | **`C-ORD-04` MỞ LẠI.** Hỏi BA/PM: chip "Thuốc/Y tế" là lỗi sót của field spec, hay `BR01-07` chỉ cấm *thuốc kê đơn/chất gây nghiện*? | Open | REQ-ORD-003, REQ-ORD-013, SC-ORD-031..035 |
| RISK-ORD-09 | ORD / Ảnh bắt buộc | *(cập nhật Status)* `BR01-01` biến ảnh từ *không rõ* thành **bắt buộc ≥ 1, chặn sang bước 2** — nếu app STG chưa siết thì `SC-ORD-054` (**P1**) FAIL vì *"app chưa cập nhật"*, không phải lỗi logic; và cả 4 SC cụm ảnh sẽ nhiễu theo | High → **Partially confirmed** | `DOC-v1.1-01` §8.1.1 BR01-01 (trang 33) vs `KP-01` §10 (quan sát app 2026-07) không ghi nhận ràng buộc bắt buộc nào; vibe-check demo 2026-09-16 | `SC-ORD-054` (P1) · `SC-ORD-055` · `SC-ORD-056` · `SC-ORD-012` | Demo 2026-09-16 xác nhận rule **có tồn tại**: bấm "Tiếp theo" khi chưa có ảnh hiện lỗi *"Vui lòng thêm ít nhất 1 ảnh hàng"*, chặn không cho qua bước 2; đếm `0/5` hiển thị đúng. **CHƯA verify được trên STG thật** (demo ≠ STG, đúng caveat chung) | Partially confirmed (rule tồn tại trên demo; cần xác nhận STG thật trước generate-tc) | REQ-ORD-006, SC-ORD-054, SC-ORD-055, SC-ORD-056 |
| RISK-ORD-11 | ORD / Tích hợp danh bạ nội bộ | **(risk mới)** `BR01-09` + §4 SCOPES nêu tích hợp **Danh bạ nội bộ** — hệ thống ngoài đầu tiên được đặc tả. 3 SC (`SC-ORD-058..060`) cần **email thật có trong danh bạ** và **email đúng tên miền nhưng không có trong danh bạ**; STG có thể chưa nối danh bạ thật ⇒ không seed được tiền đề | **Medium** | `DOC-v1.1-01` §8.1.1 BR01-09 (trang 34) · §4 SCOPES Tích hợp (trang 9) | `SC-ORD-058` (P1) · `SC-ORD-059` · `SC-ORD-060` | Xin QTHT/dev xác nhận STG đã nối danh bạ chưa + cấp 2 email mẫu. Chưa có ⇒ verdict `BLOCKED`, ⛔ không PASS. Mở `C-ORD-13` | Open | REQ-ORD-008, SC-ORD-058, SC-ORD-059, SC-ORD-060 |
| RISK-ORD-12 | ORD / Rule không định nghĩa đủ | **(risk mới)** `§8.1.4` bắt *"Địa chỉ giao phải khác địa chỉ lấy"* nhưng PRD **không định nghĩa phép so sánh** — `VAL-03` chỉ nói trim, không nói hoa/thường hay dấu. Assert bừa ⇒ bug report sai, làm mất uy tín cả bộ TC | Low | `DOC-v1.1-01` §8.1.4 (trang 35) · §8.18.2 VAL-03 (trang 52) | `SC-ORD-063` — lấy biên gần nhất (khác mỗi khoảng trắng) làm ô kiểm, **ghi nhận** hành vi hoa/thường | ⛔ Không assert cứng hành vi PRD chưa định nghĩa; nêu với BA nếu app xử lý bất nhất | Open (non-blocking) | REQ-ORD-028, SC-ORD-063 |
| RISK-ORD-03 | ORD / Danh mục Loại hàng | *(cập nhật Status + Why)* v1.0: **3 nguồn 3 danh mục**, không biết lấy cái nào. Nay tài liệu **thống nhất còn 1 danh mục 8 giá trị + mặc định**, nhưng **nhãn đầu vẫn lệch app** ("Tài liệu" ⟷ "Giấy tờ, hồ sơ") | High → **Medium** (đã bớt 1 tầng mơ hồ) | `DOC-v1.1-01` §8.1.4 (trang 35) vs `KP-01` §10.2/§10.3 (app STG) | `SC-ORD-005` — assert **số lượng 8**, **ghi nhận** nhãn | **Ràng buộc 4 của `03_test-cases/v1.0/CHANGELOG.md §2` VẪN HIỆU LỰC** — ⛔ tuyệt đối không dùng nhãn "Tài liệu" trong TC cho tới khi `C-ORD-09` chốt hẳn | Open | REQ-ORD-003, SC-ORD-005 |
| RISK-ORD-06 | ORD / Prefill hồ sơ | *(cập nhật Status)* v1.0: địa chỉ lấy hàng không prefill — **không biết là bug hay tài khoản chưa cấu hình**, treo 2 tháng | Medium → **Resolved (chuyển thành bug nếu tái hiện)** | `DOC-v1.1-01` §8.1.4 (trang 35) · §6.2 AC-30.1.01 (trang 28) | `SC-ORD-025` — Given **bắt buộc** nêu *"tài khoản ĐÃ đặt địa chỉ mặc định"* | Prefill là **hành vi đặc tả** ⇒ hồ sơ đã có mà wizard trống = **BUG**. ⛔ Không chạy trên tài khoản không rõ trạng thái hồ sơ | **Resolved** | REQ-ORD-007, REQ-ORD-010, SC-ORD-025 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-ORD-05 | Màn "Đăng tin thành công" có "Mã tin" hay không? | ✅ **Resolved 2026-09-15 — KHÔNG có mã đơn** | kế thừa 2026-07 | REQ-ORD-015, SC-ORD-036 |
| C-ORD-08 | Thoát/Reset giữa wizard có xoá form? | ✅ **Resolved 2026-09-15 — có popup xác nhận; thoát thì KHÔNG lưu DRAFT** | kế thừa 2026-07 | REQ-ORD-021, SC-ORD-050 |
| C-ORD-10 | Địa chỉ lấy hàng không pre-fill — bug hay tài khoản test chưa cấu hình? | ✅ **Resolved 2026-09-15 — prefill là hành vi đặc tả ⇒ nếu hồ sơ đã có mà vẫn trống thì là BUG** | 2026-09-07 | REQ-ORD-007, SC-ORD-025 |
| C-ORD-11 | Cơ chế field địa chỉ — preset 6 văn phòng / chip gợi ý / autocomplete? | ✅ **Resolved 2026-09-15 — ô văn bản tự do, ≤ 200 ký tự** | 2026-09-07 | REQ-ORD-010, SC-ORD-026 |
| C-ORD-09 | Danh mục "Loại hàng" — 3 nguồn 3 danh mục; app không có chip "Tài liệu" | 🟡 **Partially Resolved 2026-09-15** — phía tài liệu đã thống nhất (8 giá trị, mặc định "Tài liệu"); **lệch doc ⟷ app vẫn còn** | 2026-09-07 | REQ-ORD-003, SC-ORD-005 |
| C-ORD-04 | Chip "Thuốc/Y tế" có bị chặn không? | 🔴 **MỞ LẠI 2026-09-15** — PRD tự mâu thuẫn (xem dưới) | Resolved 2026-07-27 → **mở lại** 2026-09-15 | REQ-ORD-003, REQ-ORD-013, SC-ORD-031..035 |
| C-ORD-13 | STG đã nối **Danh bạ nội bộ** chưa, và có email mẫu để test 3 nhánh không? | 🔴 **Open (blocking cho 3 SC)** | 2026-09-15 | REQ-ORD-008, SC-ORD-058..060 |
| C-ORD-01 · C-ORD-02 · C-ORD-03 · C-ORD-12 | *(giữ nguyên Resolved từ v1.0 — PRD xác nhận lại, không đảo)* | ✅ Resolved | 2026-07 / 2026-09-07 | xem `v1.0/ORD-dang-tin/risk_assessment.md` |

### C-ORD-04 · Chip "Thuốc/Y tế" — PRD TỰ MÂU THUẪN *(MỞ LẠI 2026-09-15)*

📍 `DOC-v1.1-01 §8.1.4 UI/Field Spec, dòng "Loại hàng" · trang 35` ⟷ `§8.1.1 BR01-07 · trang 34`

> Nguồn A — §8.1.4 (trang 35):
> "Loại hàng | Có | Chọn 1 giá trị · mặc định Tài liệu | Tài liệu · Đồ điện tử · Thực phẩm · Hàng nhỏ · Đồ dễ vỡ · Quần áo · **Thuốc/Y tế** · Khác"

> Nguồn B — `BR01-07` (trang 34):
> "Bắt buộc tick đồng ý điều khoản miễn trừ trách nhiệm mới bật nút đăng tin. Hàng cấm (**thuốc**, vũ khí, chất nguy hiểm, hàng phi pháp) không được đăng."

↳ **Ghi chú:** 🔴 **Đây là mâu thuẫn NỘI TẠI của một tài liệu đã phê duyệt — loại vấn đề nặng hơn hẳn "2 tài liệu nói khác nhau".** Nguồn A cho **"Thuốc/Y tế"** là giá trị hợp lệ để chọn; nguồn B xếp **"thuốc"** vào hàng cấm **không được đăng**. Hai câu cách nhau **1 trang trong cùng một mục `FR01`**, ⇒ không thể áp thứ tự ưu tiên nguồn (`MASTER-MEMORY §2`) để phân xử — cả hai đều là `DOC-v1.1-01`.
**Vì sao phải MỞ LẠI thay vì giữ Resolved:** v1.0 chốt *"KHÔNG chặn ở v1.0; banner chỉ là thông tin tĩnh"* dựa trên `BR-ORD-04` + quan sát app. Kết luận đó vẫn **khớp với nguồn A** nhưng **nghịch với nguồn B**, và nguồn B là câu **mới xuất hiện ở v1.1**. Giữ Resolved sẽ khiến người sau trích *"KHÔNG chặn"* mà không biết có một dòng PRD nói ngược.
**Câu hỏi cho BA/PM:** (a) chip "Thuốc/Y tế" là **sót của field spec** (phải bỏ khỏi danh mục), hay (b) `BR01-07` chỉ nhắm **thuốc kê đơn / chất gây nghiện** còn "Thuốc/Y tế" thông thường vẫn được? (c) Nếu (b) thì app chặn ở đâu — lúc chọn chip, hay chỉ cảnh báo qua banner?
⛔ **Cho tới khi chốt:** `SC-ORD-031..035` **GHI NHẬN hành vi thật của app**, ⛔ không assert chiều nào. Viết TC theo nguồn B mà app theo nguồn A (hoặc ngược lại) sẽ tạo bug report sai.

↳ **Cập nhật 2026-09-16 — bằng chứng phụ từ demo (KHÔNG resolve):** Chọn chip **"Thuốc/Y tế"** ở wizard Đăng tin bước 1 trên demo — chip được chọn bình thường (viền cam), **không có cảnh báo/chặn nào xuất hiện**. Không thể đi tiếp tới bước xác nhận cuối (nơi có thể có checkbox cam kết "hàng không thuộc danh mục cấm" theo tinh thần `BR01-07`) vì **wizard này không có `<input type=file>` trong DOM** — nút "Tiếp theo" bị validation chặn vĩnh viễn ở bước 1 do không đính được ảnh bắt buộc (khác với dropzone ảnh ở màn "Xác nhận đã giao" của DLV, nơi input tồn tại và hoạt động được). ⇒ Chỉ trả lời được một phần của câu hỏi (c) — không chặn ở bước chọn chip — nhưng **không xác nhận được** có chặn ở bước cuối hay không. Giữ nguyên **Mở lại**, vẫn cần hỏi BA/PM.

### C-ORD-13 · STG đã nối Danh bạ nội bộ chưa? *(OPEN — blocking cho 3 SC)*

📍 `DOC-v1.1-01 §8.1.1 BR01-09 · trang 34` · `§4 SCOPES Tích hợp với các hệ thống khác · trang 9`

> `BR01-09`: "Email công ty người nhận được tra danh bạ nội bộ: tìm thấy thì tự điền tên · số điện thoại · địa chỉ (vẫn sửa được); không thấy thì cho nhập thủ công."

> §4 SCOPES: "Danh bạ nội bộ — tra email công ty người nhận để tự điền tên · số điện thoại · địa chỉ"

↳ **Ghi chú:** PRD nêu **Danh bạ nội bộ** như một tích hợp hệ thống ngoài chính thức — v1.0 biết có autofill (`USR-EML`) nhưng **không biết nguồn dữ liệu**, nên chưa bao giờ test được nhánh *"không tìm thấy"*.
**Câu hỏi cho QTHT/dev:** (a) STG đã nối danh bạ nội bộ **thật** chưa, hay đang dùng mock? (b) Xin **2 email mẫu**: một **có** trong danh bạ, một **đúng tên miền nội bộ nhưng không có** trong danh bạ. (c) Tên miền nội bộ được chấp nhận là những tên miền nào (để test nhánh *"ngoài tên miền"*)?
**Vì sao blocking:** không có (b) thì `SC-ORD-058`/`059`/`060` **không seed được tiền đề** ⇒ verdict `BLOCKED`, và `SC-ORD-058` là **P1**. ⛔ Không thay thế bằng email tự chế — email tự chế chỉ test được nhánh *"không tìm thấy"*, không phân biệt được với nhánh *"tích hợp hỏng"*.

### C-ORD-09 · Danh mục "Loại hàng" *(PARTIALLY RESOLVED 2026-09-15)*

📍 `DOC-v1.1-01 §8.1.4 UI/Field Spec, dòng "Loại hàng" · trang 35`

> "Loại hàng | Có | Chọn 1 giá trị · **mặc định Tài liệu** | Tài liệu · Đồ điện tử · Thực phẩm · Hàng nhỏ · Đồ dễ vỡ · Quần áo · Thuốc/Y tế · Khác"

↳ **Ghi chú:** **Nửa đã xong:** v1.0 có **3 nguồn cho 3 danh mục khác nhau** nên không biết lấy cái nào; nay tài liệu thống nhất còn **một** danh mục, đủ **8 giá trị**, kèm **giá trị mặc định** — cả hai đều là thông tin v1.0 không có.
**Nửa còn lại:** app STG hiện nhãn đầu là **"Giấy tờ, hồ sơ"**, PRD ghi **"Tài liệu"**. Đây là lệch **doc ⟷ app** ở đúng một nhãn xuất hiện trong **Steps của rất nhiều TC** — chính là **lỗi #1 của đợt phân tích cũ** (`KP-04 §4`). Theo `Project_rule §Custom Rules §10.1` ⛔ không tự chọn bên.
**Câu hỏi cho BA:** nhãn nào là chuẩn — PRD hay app? Nếu PRD chuẩn thì đây là **defect UI** cần dev sửa; nếu app chuẩn thì PRD cần đính chính.
⛔ **Ràng buộc 4 của `03_test-cases/v1.0/CHANGELOG.md §2` VẪN CÒN HIỆU LỰC** — *"nhãn loại hàng dùng theo app STG; tuyệt đối không dùng nhãn 'Tài liệu' cho tới khi `C-ORD-09` được chốt"*. PRD **không** gỡ được ràng buộc này, chỉ thu hẹp câu hỏi từ *"danh mục nào?"* xuống *"nhãn nào chuẩn?"*.

↳ **Cập nhật 2026-09-16 — bằng chứng phụ từ demo (KHÔNG resolve):** Vibe-check qua demo (`https://giangdc.github.io/foxeco_demo/FoxEcoQC`, wizard "Đăng tin" bước 1) cho thấy chip đầu tiên là **"Tài liệu"** — khớp PRD, không phải "Giấy tờ, hồ sơ". Đủ 8 giá trị đúng danh mục PRD (`Tài liệu · Đồ điện tử · Thực phẩm · Hàng nhỏ · Đồ dễ vỡ · Quần áo · Thuốc/Y tế · Khác`).
⚠️ **KHÔNG coi là Resolved.** Demo là prototype dựng lại theo PRD v1.1 (khác STG thật) — hoàn toàn có thể demo đã cập nhật theo PRD trong khi app STG thật (nơi TC sẽ thực thi) vẫn giữ nhãn cũ "Giấy tờ, hồ sơ", đúng như rủi ro đã từng xảy ra 1 lần (`KP-04 §4`). ⛔ Ràng buộc dùng nhãn STG thật vẫn giữ nguyên cho tới khi có xác nhận trực tiếp trên STG hoặc từ BA.

## Khuyến nghị tổng thể
1. 🔴 **Đưa `C-ORD-04` (PRD tự mâu thuẫn) lên đầu danh sách hỏi BA** — đây là loại vấn đề không tự phân xử được bằng thứ tự ưu tiên nguồn, vì cả hai vế đều là `DOC-v1.1-01`. Để lâu thì TC cụm consent/hàng cấm không viết được dứt khoát.
2. 🔴 **`C-ORD-13` blocking 3 SC (1 P1)** — xin QTHT/dev xác nhận STG đã nối danh bạ + cấp 2 email mẫu **trước** `generate-tc`, ⛔ đừng để tới lúc execute mới phát hiện không seed được.
3. **Vibe-test 1 lượt wizard bước 1 trước `generate-tc`** (`RISK-ORD-09`) — xác nhận app đã siết ảnh bắt buộc + trần 5 + bộ đếm `n/5`; nếu chưa thì 1 SC P1 sẽ FAIL vì *"app chưa cập nhật"*, làm nhiễu cả cụm.
4. **`C-ORD-09` vẫn chưa gỡ được ràng buộc nhãn** — ⛔ tuyệt đối không dùng "Tài liệu" trong TC. Gộp câu hỏi nhãn này với `C-ACT-02` (nhãn 2 tab) thành **một lượt hỏi BA về nhãn UI**, vì cùng bản chất doc ⟷ app.
5. **`SC-ORD-065` chạy cùng lô với `SC-CNL-010` và `SC-DLV-062`** — ba rule audit cùng họ (*bằng chứng đã ghi thì bất biến*); nếu 2 cái kia FAIL thì cái này nhiều khả năng cũng FAIL, gộp 1 bug report.
6. **`SC-ORD-025` bắt buộc xác nhận trạng thái hồ sơ trước khi chạy** — chính sự mơ hồ "không biết tài khoản đã cấu hình chưa" đã làm `C-ORD-10` treo 2 tháng.
