---
id: v1.1/ORD-dang-tin/risk
title: Risk Assessment — v1.1 · Module ORD
type: risk-assessment
version: v1.1
sprint: 1
module: ORD
counts:
  cl: 16
  risk: 12
  cl_open: 0
  cl_resolved: 16
status: ANALYZED
updated: 2026-09-17
---

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (8 dòng, `RISK-ORD-01..08`) xem `v1.0/ORD-dang-tin/risk_assessment.md` — KHÔNG lặp lại ở đây. **ID mới bắt đầu từ `RISK-ORD-09`.**
> ℹ️ Cập nhật 2026-09-17: `C-ORD-04`, `C-ORD-13`, `C-ORD-14/15/17`, `C-ORD-16` đều đã **Resolved**.
> ✅ **Cập nhật 2026-09-17 (tối) — `C-ORD-18` ĐÓNG HẲN.** BA trả lời đủ 4 câu (a)(b)(c)(d): mốc tiền là **con số chính thức** · nhãn chuẩn là **"Trọng lượng"** + **giữ** nhãn phụ Nhẹ/Trung bình/Nặng · **lấy UI làm chuẩn** cho kiểu control (chip) · block Ghi chú đặt trước là **đúng thiết kế**, là **textbox cho phép nhập**. ⇒ `cl_open (0) + cl_resolved (16) = 16 = cl (16)` — **`ORD` hết điểm hỏi BA**, và đây là **CL Open cuối cùng của toàn bộ v1.1**.
> 🔴 **Hệ quả scope:** 3 điểm trong PRD `§8.1.4` nay **HẾT HIỆU LỰC** (xem `CHANGELOG.md §2`) — nhãn *"Khối lượng"*, kiểu control *Dropdown*, và việc thiếu mốc tiền. Nguồn chốt cho 3 trường bước 1/3 là **UI thực tế**, ⛔ không phải PRD.

## Tổng quan
| Module | Risk Level | Rủi ro chính (delta v1.1) |
|--------|-----------|--------------|
| ORD | **High** (không đổi) | Module đóng được nhiều CL nhất (**4 Resolved**) nhưng cũng lộ ra vấn đề nặng nhất lượt này: **PRD tự mâu thuẫn với chính nó** — field spec để *"Thuốc/Y tế"* là loại hàng hợp lệ trong khi `BR01-07` xếp *"thuốc"* vào **hàng cấm không được đăng** (`RISK-ORD-10`). Kèm theo: ảnh chuyển thành **bắt buộc chặn luồng** (app có thể chưa siết) và **tích hợp danh bạ nội bộ** — tiền đề test có thể không seed được |

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-ORD-10 | ORD / Mâu thuẫn nội tại của PRD | **(risk mới — nặng nhất lượt 2026-09-15)** `§8.1.4` để **"Thuốc/Y tế"** là 1 trong 8 giá trị hợp lệ của Loại hàng, trong khi `BR01-07` viết *"Hàng cấm (**thuốc**, vũ khí, chất nguy hiểm, hàng phi pháp) **không được đăng**"*. **2026-09-16 BA chốt vế chip:** "Thuốc/Y tế" **giữ**, app **không giới hạn, không thông báo gì** khi chọn ⇒ mâu thuẫn nghiêng hẳn về nguồn A. Còn treo: câu *"hàng cấm… không được đăng"* của `BR01-07` có còn hiệu lực ở **bất kỳ** bề mặt nào (banner, nội dung điều khoản) hay đã chết hẳn | High → **Medium** | `DOC-v1.1-01` §8.1.4 (trang 35) vs §8.1.1 BR01-07 (trang 34) · BA trả lời 2026-09-16 | `SC-ORD-031..035` — vế chip nay **assert được** *"chọn Thuốc/Y tế không bị chặn, không cảnh báo"*; vế banner/điều khoản vẫn ghi nhận | `C-ORD-04` → **Partially Resolved**, hỏi vòng 2 về banner hàng cấm + nội dung điều khoản | Partially Resolved | REQ-ORD-003, REQ-ORD-013, SC-ORD-031..035 |
| RISK-ORD-09 | ORD / Ảnh bắt buộc | *(cập nhật Status)* `BR01-01` biến ảnh từ *không rõ* thành **bắt buộc ≥ 1, chặn sang bước 2** — nếu app STG chưa siết thì `SC-ORD-054` (**P1**) FAIL vì *"app chưa cập nhật"*, không phải lỗi logic; và cả 4 SC cụm ảnh sẽ nhiễu theo | High → **Partially confirmed** | `DOC-v1.1-01` §8.1.1 BR01-01 (trang 33) vs `KP-01` §10 (quan sát app 2026-07) không ghi nhận ràng buộc bắt buộc nào; vibe-check demo 2026-09-16 | `SC-ORD-054` (P1) · `SC-ORD-055` · `SC-ORD-056` · `SC-ORD-012` | Demo 2026-09-16 xác nhận rule **có tồn tại**: bấm "Tiếp theo" khi chưa có ảnh hiện lỗi *"Vui lòng thêm ít nhất 1 ảnh hàng"*, chặn không cho qua bước 2; đếm `0/5` hiển thị đúng. **CHƯA verify được trên STG thật** (demo ≠ STG, đúng caveat chung) | Partially confirmed (rule tồn tại trên demo; cần xác nhận STG thật trước generate-tc) | REQ-ORD-006, SC-ORD-054, SC-ORD-055, SC-ORD-056 |
| RISK-ORD-11 | ORD / Tích hợp danh bạ nội bộ | **(risk mới)** `BR01-09` + §4 SCOPES nêu tích hợp **Danh bạ nội bộ**. **2026-09-16 BA xác nhận nguồn là HRIS** và chỉ nhận nhân sự **đang làm việc** ⇒ phát sinh **nhánh thứ 4** chưa có SC (email có trong HRIS nhưng đã nghỉ việc). **2026-09-17 đã chốt tên miền = `@fpt.com` (QC)** và email mẫu *đang làm việc* = `stag_anhdc4@fpt.com`; nhánh thứ 4 (*đã nghỉ việc*) nay **gộp vào `SC-ORD-059`** vì cùng kết quả **chặn tạo đơn** (`C-ORD-14`) ⇒ chỉ còn **1 nợ data**: email mẫu thật của người đã nghỉ việc, BA cấp lúc vibe-test | **Medium** | `DOC-v1.1-01` §8.1.1 BR01-09 (trang 34) · §4 SCOPES Tích hợp (trang 9) · BA trả lời 2026-09-16 | `SC-ORD-058` (P1) · `SC-ORD-059` · `SC-ORD-060` · nhánh nghỉ việc (chưa có SC — chờ vòng 2) | Hỏi vòng 2 `C-ORD-13`: email mẫu 3 loại + tên miền + hành vi nhánh nghỉ việc. Chưa có ⇒ verdict `BLOCKED`, ⛔ không PASS | Open (Partially Resolved CL) | REQ-ORD-008, SC-ORD-058, SC-ORD-059, SC-ORD-060 |
| RISK-ORD-12 | ORD / Rule không định nghĩa đủ | **(risk mới)** `§8.1.4` bắt *"Địa chỉ giao phải khác địa chỉ lấy"* nhưng PRD **không định nghĩa phép so sánh** — `VAL-03` chỉ nói trim, không nói hoa/thường hay dấu. Assert bừa ⇒ bug report sai, làm mất uy tín cả bộ TC | Low | `DOC-v1.1-01` §8.1.4 (trang 35) · §8.18.2 VAL-03 (trang 52) | `SC-ORD-063` — lấy biên gần nhất (khác mỗi khoảng trắng) làm ô kiểm, **ghi nhận** hành vi hoa/thường | ⛔ Không assert cứng hành vi PRD chưa định nghĩa; nêu với BA nếu app xử lý bất nhất | Open (non-blocking) | REQ-ORD-028, SC-ORD-063 |
| RISK-ORD-03 | ORD / Danh mục Loại hàng | *(cập nhật Status 2026-09-16)* v1.0: 3 nguồn 3 danh mục; v1.1: tài liệu thống nhất 8 giá trị nhưng nhãn đầu lệch app ("Tài liệu" ⟷ "Giấy tờ, hồ sơ"). **BA chốt 2026-09-16: nhãn chuẩn là "Tài liệu"** ⇒ nếu STG vẫn hiện "Giấy tờ, hồ sơ" thì đó là **defect UI** | Medium → **Resolved** | `DOC-v1.1-01` §8.1.4 (trang 35) · BA trả lời 2026-09-16 | `SC-ORD-005` — assert **8 giá trị, mặc định "Tài liệu"** | Ràng buộc *"không dùng nhãn Tài liệu"* **HẾT HIỆU LỰC** (xem `CHANGELOG §2`). Verify lại STG 1 lượt: còn "Giấy tờ, hồ sơ" ⇒ log bug | **Resolved** | REQ-ORD-003, SC-ORD-005 |
| RISK-ORD-06 | ORD / Prefill hồ sơ | *(cập nhật Status)* v1.0: địa chỉ lấy hàng không prefill — **không biết là bug hay tài khoản chưa cấu hình**, treo 2 tháng | Medium → **Resolved (chuyển thành bug nếu tái hiện)** | `DOC-v1.1-01` §8.1.4 (trang 35) · §6.2 AC-30.1.01 (trang 28) | `SC-ORD-025` — Given **bắt buộc** nêu *"tài khoản ĐÃ đặt địa chỉ mặc định"* | Prefill là **hành vi đặc tả** ⇒ hồ sơ đã có mà wizard trống = **BUG**. ⛔ Không chạy trên tài khoản không rõ trạng thái hồ sơ | **Resolved** | REQ-ORD-007, REQ-ORD-010, SC-ORD-025 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-ORD-05 | Màn "Đăng tin thành công" có "Mã tin" hay không? | ✅ **Resolved 2026-09-15 — KHÔNG có mã đơn** | kế thừa 2026-07 | REQ-ORD-015, SC-ORD-036 |
| C-ORD-08 | Thoát/Reset giữa wizard có xoá form? | ✅ **Resolved 2026-09-15 — có popup xác nhận; thoát thì KHÔNG lưu DRAFT** | kế thừa 2026-07 | REQ-ORD-021, SC-ORD-050 |
| C-ORD-10 | Địa chỉ lấy hàng không pre-fill — bug hay tài khoản test chưa cấu hình? | ✅ **Resolved 2026-09-15 — prefill là hành vi đặc tả ⇒ nếu hồ sơ đã có mà vẫn trống thì là BUG** | 2026-09-07 | REQ-ORD-007, SC-ORD-025 |
| C-ORD-11 | Cơ chế field địa chỉ — preset 6 văn phòng / chip gợi ý / autocomplete? | ✅ **Resolved 2026-09-15 — ô văn bản tự do, ≤ 200 ký tự** | 2026-09-07 | REQ-ORD-010, SC-ORD-026 |
| C-ORD-09 | Danh mục "Loại hàng" — nhãn đầu "Tài liệu" (PRD) hay "Giấy tờ, hồ sơ" (app) | ✅ **Resolved 2026-09-16 — BA chốt "Tài liệu"** (app hiện nhãn khác = defect) | 2026-09-07 | REQ-ORD-003, SC-ORD-005 |
| C-ORD-04 | Chip "Thuốc/Y tế" có bị chặn không? | ✅ **Resolved 2026-09-17 (vòng 2)** — BA: chip giữ, không chặn/không cảnh báo; banner + điều khoản hàng cấm KHÔNG có ở v1.1 | Resolved 2026-07-27 → mở lại 2026-09-15 → Partially 2026-09-16 → Resolved 2026-09-17 | REQ-ORD-003, REQ-ORD-013, SC-ORD-031..035 |
| C-ORD-13 | Danh bạ nội bộ — nguồn dữ liệu + email mẫu 3 nhánh | ✅ **Resolved 2026-09-17 (vòng 2)** — BA: nguồn HRIS/stag, email mẫu + tên miền + hành vi nhánh nghỉ việc đủ định nghĩa | 2026-09-15 | REQ-ORD-008, SC-ORD-058..060 |
| C-ORD-14 | Người nhận **không có trong HRIS** (nhập tay) thì ai bấm "Xác nhận đã nhận hàng"? Người nhận có được là chính người gửi / người vận chuyển? | ✅ **Resolved 2026-09-17** — BA: (a) không tra thấy ⇒ nút "Tiếp theo" **disable**, không cho tạo đơn (b) không được nhập chính mình làm người nhận (c) người nhận không được bấm "Tôi mang giúp được" cho chính đơn đó | 2026-09-16 | REQ-ORD-008, SC-ORD-059 |
| C-ORD-15 | Biên khoảng ngày "tối đa 7 ngày", buổi đã trôi qua trong ngày hôm nay, thời điểm chính xác chuyển EXPIRED | ✅ **Resolved 2026-09-17** — BA: (a) Từ X → Đến tối đa X+7 (b) app CHẶN chọn buổi đã qua trong ngày (c) job chạy cuối ngày | 2026-09-16 | REQ-ORD-011, REQ-ORD-018, SC-ORD-028, SC-ORD-045 |
| C-ORD-16 | Chỉnh sửa tin POSTED: sửa được những field nào, hệ quả khi sửa; tin OFFER có sửa/huỷ/hết hạn không | ✅ **Resolved 2026-09-17** — format card OFFER giải qua `C-ACT-04` (cross-module) | 2026-09-17 | REQ-ORD-016, REQ-ORD-017, SC-ORD-041, SC-ORD-043 |
| C-ORD-17 | Tin EXPIRED — "gỡ" / "đăng lại" là nút gì, ở đâu, đăng lại có nạp sẵn dữ liệu cũ | ✅ **Resolved 2026-09-17** — BA: (a) "gỡ" là câu chữ dư trong PRD, KHÔNG có chức năng gỡ (b) "đăng lại" = mở luồng đăng tin MỚI, chọn lại từ đầu, không nạp dữ liệu cũ (c) card hiển thị ở tab "Đã hoàn thành", label "Hết hạn" | 2026-09-16 | REQ-ORD-018, SC-ORD-045 |
| C-ORD-18 | Bước 1/3 wizard đăng tin: **mốc tiền** của 3 mức Giá trị hàng · nhãn **"Trọng lượng"** ⟷ PRD **"Khối lượng"** · kiểu control **chip** ⟷ PRD **Dropdown** · vị trí block Ghi chú | ✅ **Resolved 2026-09-17 (tối)** — BA: (a) mốc tiền **chính thức** (b) **"Trọng lượng"**, **giữ** nhãn phụ Nhẹ/Trung bình/Nặng (c) **lấy UI làm chuẩn** ⇒ chip, PRD sai (d) Ghi chú đặt trước là đúng thiết kế, là **textbox nhập được** | 2026-09-17 | REQ-ORD-005, REQ-ORD-024, REQ-ORD-004, SC-ORD-008, SC-ORD-009, SC-ORD-010, SC-ORD-011, SC-ORD-052, SC-ORD-053 |
| C-ORD-01 · C-ORD-02 · C-ORD-03 · C-ORD-12 | *(giữ nguyên Resolved từ v1.0 — PRD xác nhận lại, không đảo)* | ✅ Resolved | 2026-07 / 2026-09-07 | xem `v1.0/ORD-dang-tin/risk_assessment.md` |

### C-ORD-04 · Chip "Thuốc/Y tế" — PRD TỰ MÂU THUẪN *(RESOLVED 2026-09-17 — vòng 2)*

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

### C-ORD-13 · STG đã nối Danh bạ nội bộ chưa? *(RESOLVED 2026-09-17 — vòng 2)*

📍 `DOC-v1.1-01 §8.1.1 BR01-09 · trang 34` · `§4 SCOPES Tích hợp với các hệ thống khác · trang 9`

> `BR01-09`: "Email công ty người nhận được tra danh bạ nội bộ: tìm thấy thì tự điền tên · số điện thoại · địa chỉ (vẫn sửa được); không thấy thì cho nhập thủ công."

> §4 SCOPES: "Danh bạ nội bộ — tra email công ty người nhận để tự điền tên · số điện thoại · địa chỉ"

↳ **Ghi chú:** PRD nêu **Danh bạ nội bộ** như một tích hợp hệ thống ngoài chính thức — v1.0 biết có autofill (`USR-EML`) nhưng **không biết nguồn dữ liệu**, nên chưa bao giờ test được nhánh *"không tìm thấy"*.
**Câu hỏi cho QTHT/dev:** (a) STG đã nối danh bạ nội bộ **thật** chưa, hay đang dùng mock? (b) Xin **2 email mẫu**: một **có** trong danh bạ, một **đúng tên miền nội bộ nhưng không có** trong danh bạ. (c) Tên miền nội bộ được chấp nhận là những tên miền nào (để test nhánh *"ngoài tên miền"*)?
**Vì sao blocking:** không có (b) thì `SC-ORD-058`/`059`/`060` **không seed được tiền đề** ⇒ verdict `BLOCKED`, và `SC-ORD-058` là **P1**. ⛔ Không thay thế bằng email tự chế — email tự chế chỉ test được nhánh *"không tìm thấy"*, không phân biệt được với nhánh *"tích hợp hỏng"*.

### C-ORD-09 · Danh mục "Loại hàng" *(RESOLVED 2026-09-16 — xem ↳ BA trả lời bên dưới)*

📍 `DOC-v1.1-01 §8.1.4 UI/Field Spec, dòng "Loại hàng" · trang 35`

> "Loại hàng | Có | Chọn 1 giá trị · **mặc định Tài liệu** | Tài liệu · Đồ điện tử · Thực phẩm · Hàng nhỏ · Đồ dễ vỡ · Quần áo · Thuốc/Y tế · Khác"

↳ **Ghi chú:** **Nửa đã xong:** v1.0 có **3 nguồn cho 3 danh mục khác nhau** nên không biết lấy cái nào; nay tài liệu thống nhất còn **một** danh mục, đủ **8 giá trị**, kèm **giá trị mặc định** — cả hai đều là thông tin v1.0 không có.
**Nửa còn lại:** app STG hiện nhãn đầu là **"Giấy tờ, hồ sơ"**, PRD ghi **"Tài liệu"**. Đây là lệch **doc ⟷ app** ở đúng một nhãn xuất hiện trong **Steps của rất nhiều TC** — chính là **lỗi #1 của đợt phân tích cũ** (`KP-04 §4`). Theo `Project_rule §Custom Rules §10.1` ⛔ không tự chọn bên.
**Câu hỏi cho BA:** nhãn nào là chuẩn — PRD hay app? Nếu PRD chuẩn thì đây là **defect UI** cần dev sửa; nếu app chuẩn thì PRD cần đính chính.
⛔ **Ràng buộc 4 của `03_test-cases/v1.0/CHANGELOG.md §2` VẪN CÒN HIỆU LỰC** — *"nhãn loại hàng dùng theo app STG; tuyệt đối không dùng nhãn 'Tài liệu' cho tới khi `C-ORD-09` được chốt"*. PRD **không** gỡ được ràng buộc này, chỉ thu hẹp câu hỏi từ *"danh mục nào?"* xuống *"nhãn nào chuẩn?"*.

↳ **Cập nhật 2026-09-16 — bằng chứng phụ từ demo (KHÔNG resolve):** Vibe-check qua demo (`https://giangdc.github.io/foxeco_demo/FoxEcoQC`, wizard "Đăng tin" bước 1) cho thấy chip đầu tiên là **"Tài liệu"** — khớp PRD, không phải "Giấy tờ, hồ sơ". Đủ 8 giá trị đúng danh mục PRD (`Tài liệu · Đồ điện tử · Thực phẩm · Hàng nhỏ · Đồ dễ vỡ · Quần áo · Thuốc/Y tế · Khác`).
⚠️ **KHÔNG coi là Resolved.** Demo là prototype dựng lại theo PRD v1.1 (khác STG thật) — hoàn toàn có thể demo đã cập nhật theo PRD trong khi app STG thật (nơi TC sẽ thực thi) vẫn giữ nhãn cũ "Giấy tờ, hồ sơ", đúng như rủi ro đã từng xảy ra 1 lần (`KP-04 §4`). ⛔ Ràng buộc dùng nhãn STG thật vẫn giữ nguyên cho tới khi có xác nhận trực tiếp trên STG hoặc từ BA.

### C-ORD-04 · ↳ BA trả lời 2026-09-16 *(→ PARTIALLY RESOLVED — hỏi vòng 2)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `ORD` · cột "Câu trả lời BA" · 2026-09-16

> "a. Thuốc/Y tế  có nhé
> B, c. không giới hạn hay thông bao gì, hiện tại có thể đăng bất kỳ"

↳ **Ghi chú:** Vế (a) chốt **chip "Thuốc/Y tế" là giá trị hợp lệ**, không phải sót của field spec. Vế (b)(c) chốt **app không giới hạn, không cảnh báo** — khớp kết luận v1.0 (*"KHÔNG chặn"*) và khớp quan sát demo 2026-09-16. ⇒ `SC-ORD-031..035` phần chip **assert được**: chọn "Thuốc/Y tế" → không chặn, không popup/banner cảnh báo, đăng tin thành công.
**Còn treo (vòng 2):** câu *"có thể đăng bất kỳ"* rộng hơn câu hỏi. `BR01-07` còn nửa sau *"Hàng cấm (thuốc, vũ khí, chất nguy hiểm, hàng phi pháp) không được đăng"* — cần BA nói rõ: (1) nửa câu này **bỏ hẳn khỏi PRD**, hay chỉ còn là **cam kết trong nội dung điều khoản** người dùng tick? (2) Banner thông tin hàng cấm của v1.0 (`SC-ORD-031..035`) **còn hiển thị** không? (3) Nội dung điều khoản miễn trừ có đoạn nào về hàng cấm để TC kiểm verbatim không (`NFR-13` còn đòi lưu **phiên bản** điều khoản)? ⛔ Chưa có (1)(2) thì phần banner/điều khoản vẫn **ghi nhận**, không assert.

↳ **KẾT LUẬN (theo BA) vòng 2, 2026-09-16:** (1) app hiện tại **CHƯA làm** banner/cảnh báo hàng cấm — có thể làm trong tương lai, **TẠM BỎ QUA** ở v1.1 (không viết SC assert banner). (2) banner thông tin hàng cấm ở wizard (v1.0) **KHÔNG còn hiển thị** ở v1.1. (3) **KHÔNG có** nội dung điều khoản nào về hàng cấm để test verbatim. `SC-ORD-031..035` phần banner/điều khoản chốt là **KHÔNG có bề mặt để assert** (không phải gap, mà là tính năng chưa tồn tại). `C-ORD-04` ĐÓNG HẲN.

### C-ORD-09 · ↳ BA trả lời 2026-09-16 *(→ RESOLVED)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `ORD` · cột "Câu trả lời BA" · 2026-09-16

> "Tài liệu"

↳ **Ghi chú:** BA chọn **PRD làm chuẩn** ⇒ nhãn đầu + giá trị mặc định của "Loại hàng" là **"Tài liệu"** (khớp demo 2026-09-16). Hệ quả: (1) **ràng buộc #2 của `CHANGELOG §2` và ràng buộc 4 của `03_test-cases/v1.0/CHANGELOG.md §2` hết hiệu lực cho v1.1** — TC v1.1 dùng "Tài liệu"; (2) nếu app STG vẫn hiện **"Giấy tờ, hồ sơ"** (quan sát cũ 2026-07) ⇒ **defect UI**, log bug, ⛔ không sửa TC cho khớp app. ⚠️ Ngược chiều với `C-ACT-02` (ở đó BA chọn **app** làm chuẩn) — không mâu thuẫn: BA quyết **từng nhãn một**, không có luật chung "PRD thắng" hay "app thắng".

### C-ORD-13 · ↳ BA trả lời 2026-09-16 *(→ PARTIALLY RESOLVED — hỏi vòng 2)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `ORD` · cột "Câu trả lời BA" · 2026-09-16

> "a. là thông tin trên app hris, thông tin phỉa có trên hris, và trạng thái là đang làm việc"

↳ **Ghi chú:** Chốt được **nguồn dữ liệu = HRIS** và **điều kiện tra thấy = nhân sự có hồ sơ HRIS + trạng thái "đang làm việc"**. Điều kiện thứ hai là **rule mới** PRD không có ⇒ sinh nhánh thứ 4 cho `REQ-ORD-008`: email **có** trên HRIS nhưng **đã nghỉ việc**. Câu (b) email mẫu và (c) tên miền **BA chưa trả lời**.
**Hỏi vòng 2:** (1) STG đang nối **HRIS thật** hay HRIS môi trường test/mock? (2) Xin email mẫu **3 loại**: đang làm việc (có thể dùng `stag_anhdc4@fpt.com` đã dùng ở v1.0 không?) · đã nghỉ việc · đúng tên miền nhưng không có trên HRIS. (3) Tên miền nội bộ hợp lệ (vd `@fpt.com` · `@fpt.vn` · …)? (4) Email của người **đã nghỉ việc** thì app báo gì — giống *"Không tìm thấy · nhập thủ công"* hay thông báo riêng, có **chặn** đăng tin không? (5) Hồ sơ HRIS **thiếu** SĐT hoặc địa chỉ thì tự điền phần có, bỏ trống phần thiếu? ⛔ Không có (2) thì `SC-ORD-058..060` vẫn `BLOCKED`.

↳ **KẾT LUẬN (theo BA) vòng 2, 2026-09-16:** (1) STG dùng **môi trường stag** (không phải HRIS production thật). (2) email mẫu "đang làm việc" = `stag_anhdc4@fpt.com` dùng được; nhánh "đã nghỉ việc" BA sẽ cấp dữ liệu thật lúc **vibe-test** (dùng placeholder tạm khi `generate-tc`). (3) tên miền nội bộ hợp lệ: `@fpt.vn`, `@gmail.com`. (4) email đã nghỉ việc ⇒ xử lý **giống "Không tìm thấy · nhập thủ công"**, KHÔNG báo lỗi riêng, KHÔNG chặn đăng tin. (5) hồ sơ HRIS thiếu SĐT/địa chỉ ⇒ tự điền phần có, bỏ trống phần thiếu (BA reconfirm). `C-ORD-13` ĐÓNG — hết blocking `generate-tc`; chỉ còn nợ nhỏ "email mẫu thật cho case đã nghỉ việc" cấp lúc vibe-test (không chặn viết TC, dùng placeholder tạm).

↳ 🔁 **ĐÍNH CHÍNH 2 vế của kết luận trên — 2026-09-17 (QC GiangDC2 xác nhận trực tiếp + BA `C-ORD-14`):**
> **(3) tên miền** — hợp lệ là **email công ty `@fpt.com`**. ⛔ Vế *"`@fpt.vn`, `@gmail.com`"* ở kết luận vòng 2 **HẾT HIỆU LỰC, đừng trích lại**: `@gmail.com` nay là **dữ liệu INVALID** của `SC-ORD-060` (nhánh *ngoài tên miền công ty*); `@fpt.vn` **chưa được xác nhận lại** ⇒ ⛔ không dùng làm test data cho bất kỳ nhánh nào cho tới khi chốt. *(Khớp luôn email mẫu `stag_anhdc4@fpt.com` đã chốt ở vế (2) — cùng tên miền `@fpt.com`.)*
> **(4) email đã nghỉ việc / không tra thấy** — ⛔ Vế *"xử lý giống Không tìm thấy · nhập thủ công, KHÔNG chặn đăng tin"* **HẾT HIỆU LỰC**: `C-ORD-14` (2026-09-17, **mới hơn**) chốt **nút "Tiếp theo" DISABLE, KHÔNG cho tạo đơn** — áp cho **cả 2 case** (không tồn tại · đã nghỉ việc). ⇒ `SC-ORD-059` **đảo Then** (NEW → MODIFIED), xem `test_scenario_map.md`.
> ⚠️ **Hệ quả cần nhớ:** PRD `BR01-09`/`AC-04.1.02` (*"không thấy thì cho nhập thủ công"*) nay **nói ngược câu trả lời BA** ⇒ đề nghị BA **sửa PRD**; khi chạy TC thì **lấy câu trả lời BA**, STG cho nhập tay và tạo được đơn ⇒ **log bug**, ⛔ không sửa oracle.

### C-ORD-14 · Người nhận không có tài khoản / người nhận trùng người gửi hoặc người vận chuyển *(RESOLVED 2026-09-17)*

📍 `DOC-v1.1-01 §6.2 AC-04.1.02 · trang 17` ⟷ `§8.10.1 BR10-01 · trang 43` · `§8.3.1 BR03-04 · trang 36`

> `AC-04.1.02`: "Hiện dòng "Không tìm thấy · nhập thủ công". Mở ô nhập tên, số điện thoại, địa chỉ để người dùng tự điền. Không chặn việc đăng tin."

> `BR10-01`: "Chỉ người nhận thấy và thao tác được nút "Xác nhận đã nhận hàng"; chỉ khả dụng sau DELIVERED."

> `BR03-04`: "Người gửi và người vận chuyển của cùng một đơn phải là hai người khác nhau."

↳ **Ghi chú:** Phát hiện khi rà chéo `FR01` ⟷ `FR10` sau câu trả lời HRIS của `C-ORD-13`. Nếu email người nhận **không tra thấy** (không có trên HRIS / đã nghỉ việc) mà vẫn **cho đăng tin** bằng thông tin nhập tay, thì người nhận đó **không có tài khoản** ⇒ không ai bấm được "Xác nhận đã nhận hàng" ⇒ đơn kẹt ở `DELIVERED`, chỉ còn nhắc 2h/4h rồi "chuyển admin" — mà `C-CNL-03` vừa xác nhận **không có công cụ admin**. PRD cũng chỉ cấm *người gửi = người vận chuyển*, **không** nói gì về *người nhận = người gửi* hoặc *người nhận = người vận chuyển*.
**Câu hỏi cho BA:** (a) Người nhận nhập tay (không có trên HRIS) thì đơn đóng bằng cách nào? (b) Có cho người gửi **nhập chính email của mình** làm người nhận không? (c) Người nhận của đơn có được bấm "Tôi mang giúp được" cho chính đơn đó không (`SC-FEED-012` đang coi là bug theo `DOC-v1.0-02 §7`)?

↳ **KẾT LUẬN (theo BA) 2026-09-17:** (a) email không tra thấy trên HRIS (chưa nghỉ việc lẫn không tồn tại) ⇒ nút **"Tiếp theo" bị disable**, KHÔNG cho tạo đơn — vậy nhánh "đơn kẹt vĩnh viễn" đặt ra ở Ghi chú trên **không xảy ra**, vì app chặn ngay từ bước tạo, không phải chặn ở bước xác nhận nhận hàng. (b) người gửi **KHÔNG** được nhập chính email mình làm người nhận. (c) người nhận của đơn **KHÔNG** được bấm "Tôi mang giúp được" cho chính đơn đó ⇒ `SC-FEED-012` giữ nguyên là bug nếu STG cho phép. Đã thử vibe-check demo 2026-09-17 để đối chứng thêm (c) nhưng demo dùng chung 1 "đơn" toàn cục cho cả 3 vai (xem `C-ASN-03`) nên không dựng được kịch bản sạch "người nhận xem đúng tin của chính mình ở Bảng tin" — không mâu thuẫn với câu trả lời BA, chỉ là demo không đủ dữ liệu để đối chứng trực quan thêm.

### C-ORD-15 · Biên thời gian: "tối đa 7 ngày", buổi đã qua, mốc EXPIRED *(RESOLVED 2026-09-17)*

📍 `DOC-v1.1-01 §8.1.1 BR01-04 · trang 34` · `§8.1.4 dòng "Buổi mong muốn" · trang 36` · `§8.5.1 BR05-03 · trang 38`

> `BR01-04`: "Khoảng ngày tối đa 7 ngày, không nhận ngày quá khứ, Đến ngày ≥ Từ ngày. Phải chọn tối thiểu 1 buổi…"

> `§8.1.4`: "Buổi mong muốn | Có | Chọn nhiều · mặc định Sau giờ làm | Sáng (8–12) · Chiều (13–17) · Sau giờ làm (17–19) · Giờ nào cũng được…"

> `BR05-03`: "Hết ngày cuối của khoảng ngày mà đơn vẫn POSTED thì chuyển EXPIRED…"

↳ **Ghi chú:** 3 biên PRD không định nghĩa, đều nằm trong Steps của TC boundary: (a) **"tối đa 7 ngày"** tính **gồm cả ngày đầu** (Từ 15/07 → Đến tối đa 21/07) hay **cộng 7** (→ 22/07)? Cùng câu hỏi cho `FR02` (OFFER) và lịch hẹn cầm hàng về `BR09-04` *"trong vòng 7 ngày"*. (b) Đăng tin **sau 19:00** với mặc định *Từ ngày = hôm nay, buổi = Sau giờ làm* — mọi buổi của hôm nay đã qua: app **chặn**, **tự dời ngày**, hay **cho đăng**? (`KP-01 §10.11` từng ghi nhận app validate theo đồng hồ thật nhưng không rõ quy tắc.) (c) "Hết ngày cuối" = **00:00 ngày kế tiếp** hay theo lịch job chạy (bao lâu 1 lần)? Không chốt (c) thì `SC-ORD-045` không biết chờ tới lúc nào mới được kết luận FAIL.

↳ **KẾT LUẬN (theo BA) 2026-09-17:** (a) "tối đa 7 ngày" = **cộng 7** (Từ ngày X → Đến tối đa ngày X+7), áp dụng chung cho `FR02` (OFFER) và lịch hẹn cầm hàng về. (b) đăng tin sau 12h/19h thì app **CHẶN** không cho chọn buổi đã qua trong ngày hôm đó (không tự dời ngày, không cho đăng buổi đã qua). (c) mốc chuyển `EXPIRED` chạy theo **job cuối ngày** (không phải 00:00 tức thời) — `SC-ORD-045` verify bằng cách chờ tới sau giờ chạy job, không phải đúng 00:00. Thuộc logic backend/thời gian nên không cần/không thể verify thêm qua demo tĩnh.

### C-ORD-16 · Chỉnh sửa tin — phạm vi field + hệ quả; vòng đời tin OFFER *(RESOLVED 2026-09-17 — vế (c) format card OFFER giải qua `C-ACT-04`, cross-module)*

📍 `DOC-v1.1-01 §6.2 AC-08.1.01 · trang 19` · `§8.5.1 BR05-02 · trang 38` · `§7.3 Ma trận phân quyền dòng "Chỉnh sửa tin khi còn Chờ ghép" · trang 32` · `§8.12.2 · trang 45`

> `AC-08.1.01`: "Người dùng bấm "Chỉnh sửa" ở màn theo dõi đơn, đổi địa chỉ giao và bấm "Cập nhật". Then: Form nạp sẵn toàn bộ dữ liệu cũ…"

> `§7.3`: "Chỉnh sửa tin khi còn Chờ ghép | x (chủ tin) | x (chủ tin OFFER) | – | x*"

↳ **Ghi chú:** AC chỉ minh hoạ **đổi địa chỉ giao**. PRD không nói (a) sửa được **những field nào** — ảnh, email người nhận (có tra lại HRIS?), khoảng ngày/buổi, người uỷ quyền; (b) sửa khoảng ngày có **tính lại mốc EXPIRED** không; sửa điểm lấy/giao có **chạy lại khớp tuyến** (`FR04`) và bắn lại `NTF-03` không; có **thông báo người nhận** khi đổi thông tin không. (c) Ma trận quyền cho **chủ tin OFFER** sửa tin, nhưng `§8.12.2` chỉ có trạng thái **đơn NEED** — tin OFFER **sửa ở đâu, huỷ được không, có tự hết hạn** khi qua "Đến ngày" không, và hiển thị ở "Đơn của tôi" với **nhãn trạng thái gì**? (`AC-19.1.01`/`AC-20.1.01` chỉ nói *"xem lại được ở Đơn của tôi"*.)

↳ **BA trả lời 2026-09-17 (a)(b):** (a) sửa được **TẤT CẢ** field như lúc tạo mới, rule check lại **y hệt** lúc tạo mới (kể cả tra lại HRIS nếu sửa email). (b) sửa khoảng ngày/buổi **KHÔNG** check lại / không tính lại gì (ví dụ đổi buổi Sáng → Chiều vẫn cho sửa, không báo lỗi) — vậy `EXPIRED` không tự tính lại theo giá trị mới. (c) BA trả lời "Kiểm tra lại demo giúp t nhé" — **đã thử vibe-check demo 2026-09-17 nhưng KHÔNG verify được**: bản demo dùng chung 1 "đơn" toàn cục cho cả 3 vai (xem `C-ASN-03`), đăng tin OFFER không tạo bản ghi độc lập mà **ghi đè** lên đơn NEED đang có (địa chỉ giao của đơn cũ bị thay bằng điểm đến vừa nhập cho tuyến OFFER — ảnh `00_input/v1.1/design/ORD_08_dangtin_offer_ghide_len_don_dang_co.png`); bấm "Theo dõi đơn" từ màn xác nhận OFFER dẫn thẳng về đúng đơn NEED đó, không sinh thêm card nào ở "Đơn của tôi" ⇒ không quan sát được nhãn trạng thái/hình dạng card cho tuyến OFFER qua demo này. **Còn treo (c):** cần BA mô tả bằng lời hoặc gửi ảnh UI thật (STG/Figma).

↳ **BA trả lời 2026-09-17 (vòng 3):** "đã bổ sung ui ORD_08_card toi nhan giao hang, card sẽ ntn nhé" — đính kèm lại **chính ảnh `ORD_08_dangtin_offer_ghide_len_don_dang_co.png`** đã dùng làm bằng chứng cho kết luận vòng 2 ở trên (màn "Theo dõi đơn" hiện trạng thái "Chờ ghép" + nút "Nhận mang giúp đơn này" — persona demo mặc định, không phải card OFFER riêng). ⚠️ **Ảnh này KHÔNG trả lời được câu hỏi gốc** ("tin OFFER hiện ở 'Đơn của tôi' như thế nào: card riêng không, nhãn trạng thái ghi gì") — nó chỉ tái xác nhận đúng giới hạn demo đã ghi ở vòng 2 (OFFER ghi đè lên đơn NEED, không sinh card riêng), KHÔNG phải ảnh chụp màn "Đơn của tôi" dạng list với card OFFER. **`C-ORD-16` câu (c) VẪN CÒN TREO** — cần hỏi lại BA rõ hơn: xin ảnh chụp màn **"Đơn của tôi" (danh sách, không phải Theo dõi đơn)** trên STG thật hoặc Figma, có card của 1 tin OFFER đã đăng, hoặc xác nhận thẳng "OFFER không có card riêng, sẽ dùng chung 1 thẻ theo dõi đơn như đã thấy trong ảnh" nếu đó đúng là hành vi sản phẩm dự định (không phải giới hạn demo).

↳ **ĐÓNG 2026-09-17 — cùng câu hỏi đã giải qua `C-ACT-04` (module ACT, home canonical của màn "Hoạt động"/"Đơn của tôi"):** tái vibe-check đúng đường dẫn tab "Hoạt động" → "Đang diễn ra" (thay vì màn "Theo dõi đơn" bị ghi đè) → quan sát được card OFFER: title "Nhận giao hàng &lt;tuyến&gt;", badge "Chờ ghép", 2 dòng "Từ:"/"Đến:", CTA "Chạm để xem tuyến đường của bạn"; tap mở "Theo dõi đơn". **`C-ORD-16` ĐÓNG HẲN** — `SC-ORD-041` dùng chung format card này với `SC-ACT-015`, không tách riêng.

↳ **Nâng cấp bằng chứng 2026-09-17 (cùng ngày):** QC cung cấp ảnh UI thật `00_input/v1.1/design/ORD_08_card toi nhan giao hang.png` khớp 100% quan sát demo — không còn chỉ dựa demo nữa.

### C-ORD-17 · Tin EXPIRED — "gỡ" và "đăng lại" *(RESOLVED 2026-09-17)*

📍 `DOC-v1.1-01 §6.2 AC-09.1.01 · trang 19` · `§8.13.1 NTF-09 · trang 47` · `§8.12.3 dòng RETURNED · CANCELLED · EXPIRED · trang 46`

> `AC-09.1.01`: "…Người đăng nhận thông báo gợi ý gỡ hoặc đăng lại."

> `NTF-09`: "Tin của bạn đã quá hạn — gỡ hoặc đăng lại nếu vẫn cần"

> ↪ *Quote `§8.12.3` (hành động theo trạng thái) — home ở `../ACT-hoat-dong/risk_assessment.md` · `C-ACT-04` (không chép lại — tránh lặp home, health-check G-03 2026-09-17)*

↳ **Ghi chú:** PRD hứa 2 hành động nhưng không đặc tả: (a) **"Gỡ"** là nút gì — xoá tin khỏi "Đơn của tôi"? (mâu thuẫn tinh thần *"đơn đóng là bất biến"* `BR10-03`). (b) **"Đăng lại"** mở wizard **nạp sẵn dữ liệu cũ** hay wizard trắng; ảnh cũ có được mang theo? (c) Card "Hết hạn" ở màn Đơn của tôi v1.0 được ghi là **không thao tác được** (`SC-ACT-009`, `KB-ORD-07` #6) — nếu phải "Xem lý do · đăng lại" thì card phải **mở được** ⇒ `SC-ACT-009` có thể sai. Cross-ref `C-ACT-04`.

↳ **KẾT LUẬN (theo BA) 2026-09-17:** (a) "gỡ" là câu chữ **dư** trong PRD (soạn thảo sai) — app **KHÔNG có chức năng gỡ**; đề nghị BA sửa PRD bỏ chữ này. (b) "Đăng lại" = mở luồng **ĐĂNG TIN MỚI**, chọn lại toàn bộ thông tin từ đầu (KHÔNG nạp sẵn dữ liệu/ảnh cũ). (c) tin hết hạn hiển thị ở tab **"Đã hoàn thành"** với nhãn **"Hết hạn"** (BA tự xác nhận demo có thể hiện đúng — QA chưa tự tay đối chứng lại card này trong lượt vibe-check 2026-09-17 vì đơn dùng để test hôm nay chưa đạt trạng thái Hết hạn) — card **MỞ được** để xem lý do, KHÔNG giữ rule v1.0 "không tap được" ⇒ `SC-ACT-009` (giả định không tap được) **SAI theo v1.1**, cần sửa.

### C-ORD-18 · Bước 1/3 "Thông tin hàng" — UI demo lệch PRD `§8.1.4` *(RESOLVED 2026-09-17 — đóng trong ngày)*

📍 `DOC-v1.1-01 §8.1.4 UI/Field Spec · trang 35` · `§8.1.1 BR01-02/BR01-03 · trang 34` ⟷ `DOC-v1.1-03` ảnh `00_input/v1.1/design/gia tri hang uoc tinh.png` (demo, QC GiangDC2 cung cấp 2026-09-17)

> PRD `§8.1.4` (trang 35):
> ↪ *Quote `§8.1.4` dòng "Giá trị hàng" — home ở `requirement_traceability.md` · `REQ-ORD-024` (không chép lại — tránh lặp home, health-check G-03 2026-09-17)*
> ↪ *Quote `§8.1.4` dòng "Khối lượng" — home ở `requirement_traceability.md` · `REQ-ORD-024` (không chép lại — tránh lặp home, health-check G-03 2026-09-17)*
> ↪ *Quote `§8.1.4` dòng "Kích thước" — home ở `requirement_traceability.md` · `REQ-ORD-024` (không chép lại — tránh lặp home, health-check G-03 2026-09-17)*

↳ **Quan sát trên ảnh UI (demo) 2026-09-17 — 4 điểm lệch:**
1. 🔴 **"GIÁ TRỊ HÀNG (ƯỚC TÍNH)" có MỐC TIỀN mà PRD không có:** `Thấp` = *"Dưới 1 triệu đ"* · `Vừa` = *"1 – 5 triệu đ"* · `Cao` = *"Trên 5 triệu đ"*. Đây là **thông tin hoàn toàn mới** — v1.0 lẫn v1.1 đều **không nguồn nào cho con số**. ⚠️ **KHÔNG lẫn với `C-ORD-02`** (*"ngưỡng cấu hình + cảnh báo nên mua bảo hiểm"* của `BR-ORD-03`, vẫn **Resolved out of scope**): ở đây **không có ô nhập số tiền**, không có rule chặn theo ngưỡng — mốc tiền chỉ là **nhãn phụ định nghĩa 3 mức định tính**. ⇒ `C-ORD-02` **không bị đảo**.
2. 🟡 **Nhãn field lệch:** UI ghi **"TRỌNG LƯỢNG"**, PRD ghi **"Khối lượng"**. Option cũng khác chữ: UI *"Dưới 5 kg (Nhẹ)"* · *"5 – 10 kg (Trung bình)"* · *"Trên 10 kg (Nặng)"* — **enum tương đương** PRD nhưng có thêm **nhãn phụ Nhẹ/Trung bình/Nặng** PRD không nhắc.
3. 🟡 **Kiểu control lệch:** PRD ghi **Dropdown** cho cả 3 trường; UI là **3 chip (segmented) nằm ngang**, không dropdown. Ảnh hưởng **Steps** của TC (chọn chip ⟷ mở dropdown). Mặc định **không chip nào được chọn** ⇒ khớp *"chưa chọn"*.
4. 🟡 **Thứ tự block:** **Ghi chú** nằm **TRÊN CÙNG**, trước block "THÔNG TIN HÀNG"; PRD field spec liệt kê Ghi chú **sau**. Placeholder nguyên văn: *"Lưu ý khi giao nhận (VD: gọi trước khi tới, giao tại sảnh, hàng dễ vỡ nhẹ tay...)"*.

✅ **Đồng thời XÁC NHẬN 1 điều đang treo:** khối **"ẢNH HÀNG \*"** trên demo đã có đủ **dấu `*` bắt buộc** + **bộ đếm "0/5"** + helper *"Bắt buộc ít nhất 1 ảnh · tối đa 5 ảnh · giúp người vận chuyển nhận diện hàng"* ⇒ `BR01-01`/`BR18-02` **đã được build ở tầng UI** — thu hẹp `RISK-ORD-09` (xem Khuyến nghị #3).

⚠️ **Quan sát cần kiểm chứng, ⛔ chưa kết luận:** nút **"Tiếp theo" hiển thị màu cam/active** dù chưa chọn Giá trị hàng/Trọng lượng/Kích thước và chưa có ảnh — **ngược** `KB-VIBE-03` (*"để trống Giá trị hàng → nút disabled/mờ"*) và `BR01-01` (*"thiếu ảnh thì chặn sang bước 2"*). Rất có thể là **giới hạn ảnh tĩnh/demo**, không phải hành vi thật ⇒ **vibe-check bấm thật** trước khi kết luận; ⛔ **không log bug** dựa trên mỗi ảnh này.

**Hỏi BA:** (a) 3 mốc tiền *(< 1 triệu · 1–5 triệu · > 5 triệu)* có phải con số **chính thức** không — nếu có, đề nghị bổ sung vào `§8.1.4` để TC assert cứng? (b) Nhãn chính thức là **"Trọng lượng"** hay **"Khối lượng"**, có giữ nhãn phụ *Nhẹ/Trung bình/Nặng* không? (c) 3 trường này là **chip** (theo UI) hay **Dropdown** (theo PRD) — PRD cần sửa? (d) Vị trí block Ghi chú đặt trước "Thông tin hàng" là đúng thiết kế?

↳ **BA trả lời 2026-09-17 (tối — QC GiangDC2 chuyển lời):**

> (a) "chính thức nhé"
> (b) "Trọng lượng, Có giữ nhãn phụ Nhẹ/Trung bình/Nặng"
> (c) "Theo UI nhé, lấy UI làm chuẩn"
> (d) "đúng đây là textbox cho phép nhập nhé"

↳ **KẾT LUẬN (theo BA) 2026-09-17 — `C-ORD-18` ĐÓNG HẲN:**

**(a) 3 mốc tiền là CON SỐ CHÍNH THỨC** ⇒ `SC-ORD-008/009/010` **assert cứng** đúng chuỗi `Dưới 1 triệu đ` · `1 – 5 triệu đ` · `Trên 5 triệu đ` gắn với 3 mức `Thấp`/`Vừa`/`Cao`. 🔴 **PRD `§8.1.4` THIẾU thông tin này** — đề nghị BA bổ sung; tới khi PRD cập nhật, nguồn chốt là **câu trả lời BA 2026-09-17 + ảnh `DOC-v1.1-03`**. ⚠️ Vẫn **KHÔNG lẫn `C-ORD-02`** (ngưỡng cấu hình + bảo hiểm) — vẫn Resolved out of scope: đây chỉ là nhãn phụ định nghĩa 3 mức định tính, không có ô nhập số tiền, không có rule chặn theo ngưỡng.

**(b) Nhãn chính thức = "Trọng lượng"**, và **GIỮ** nhãn phụ *Nhẹ/Trung bình/Nặng* ⇒ `SC-ORD-052` assert cứng nhãn field **"Trọng lượng"** và 3 option đầy đủ `Dưới 5 kg (Nhẹ)` · `5 – 10 kg (Trung bình)` · `Trên 10 kg (Nặng)`. 🔴 **PRD ghi "Khối lượng" HẾT HIỆU LỰC** — app hiện "Khối lượng" ⇒ **defect UI**, không phải TC sai.

**(c) LẤY UI LÀM CHUẨN cho kiểu control** ⇒ cả 3 trường (Giá trị hàng · Trọng lượng · Kích thước) là **chip (segmented) nằm ngang**, ⛔ KHÔNG phải Dropdown. 🔴 **PRD ghi "Dropdown" HẾT HIỆU LỰC** — Steps của TC viết theo thao tác **nhấn chip**, ⛔ không viết "mở dropdown rồi chọn". Mặc định **không chip nào được chọn**, khớp *"chưa chọn"* của PRD (phần này PRD vẫn đúng).

**(d) Block Ghi chú đặt TRÊN block "Thông tin hàng" là ĐÚNG THIẾT KẾ**, và là **textbox cho phép nhập** (không phải nhãn tĩnh) ⇒ `SC-ORD-011` assert cứng **vị trí trên cùng** + **nhập được**. Thứ tự liệt kê ở PRD field spec chỉ là thứ tự bảng, ⛔ không phải thứ tự hiển thị — không coi là mâu thuẫn.

⚠️ **CÒN LẠI 1 việc QA tự làm, KHÔNG hỏi BA:** quan sát *"nút 'Tiếp theo' hiển thị màu cam/active dù chưa chọn gì và chưa có ảnh"* vẫn **chưa kết luận** — nghi là giới hạn ảnh tĩnh. Xử bằng **vibe-check bấm thật** wizard bước 1 (gộp luôn với lượt verify hành vi chặn ảnh bắt buộc của `RISK-ORD-09`); ⛔ **không log bug** dựa trên mỗi ảnh tĩnh.

⚠️ **SC ngoài `id_range` delta bị chạm:** `SC-ORD-008/009/010/011` là **CARRIED** (nội dung ở `../../v1.0/ORD-dang-tin/`) nhưng kết luận này làm chúng **assert mạnh hơn** (mốc tiền + vị trí Ghi chú). ⛔ KHÔNG sửa file v1.0; ghi nợ ở `CHANGELOG.md §3` để lượt `analyze-requirements` sau chính thức hoá thành MODIFIED nếu cần regenerate TC.

## Khuyến nghị tổng thể
1. 🟡 **`C-ORD-04` — vế chip đã chốt 2026-09-16** ("Thuốc/Y tế" giữ, không chặn/không cảnh báo); còn **vòng 2** về banner hàng cấm + nội dung điều khoản — xem khối trả lời BA ở trên.
2. 🔴 **`C-ORD-13` vòng 2 vẫn blocking 3 SC (1 P1)** — nguồn đã rõ (HRIS, chỉ nhân sự đang làm việc); còn thiếu **email mẫu 3 loại** + tên miền nội bộ, phải có **trước** `generate-tc`.
3. **Vibe-test 1 lượt wizard bước 1 trước `generate-tc`** (`RISK-ORD-09`) — xác nhận app đã siết ảnh bắt buộc + trần 5 + bộ đếm `n/5`; nếu chưa thì 1 SC P1 sẽ FAIL vì *"app chưa cập nhật"*, làm nhiễu cả cụm. **Cập nhật 2026-09-17 — THU HẸP:** ảnh UI demo (`C-ORD-18`) cho thấy khối "ẢNH HÀNG \*" **đã có** dấu `*` + bộ đếm **"0/5"** + helper *"Bắt buộc ít nhất 1 ảnh · tối đa 5 ảnh"* ⇒ tầng UI **đã build**. Còn lại chỉ phải verify **hành vi chặn thật** (bấm "Tiếp theo" khi 0 ảnh) — gộp luôn vào lượt vibe-check của `C-ORD-18`. **Cập nhật 2026-09-17 (tối) — `C-ORD-18` đã Resolved**, nhưng lượt vibe-check bấm thật **VẪN CẦN** (nút "Tiếp theo" cam khi chưa chọn gì); đây nay là **việc QA tự làm**, không còn là điểm hỏi BA.
4. ✅ **`C-ORD-09` Resolved 2026-09-16 — nhãn chuẩn "Tài liệu"**; TC v1.1 dùng "Tài liệu", app còn hiện "Giấy tờ, hồ sơ" ⇒ log bug UI. Ràng buộc *"không dùng Tài liệu"* hết hiệu lực.
5. **`SC-ORD-065` chạy cùng lô với `SC-CNL-010` và `SC-DLV-062`** — ba rule audit cùng họ (*bằng chứng đã ghi thì bất biến*); nếu 2 cái kia FAIL thì cái này nhiều khả năng cũng FAIL, gộp 1 bug report.
6. **`SC-ORD-025` bắt buộc xác nhận trạng thái hồ sơ trước khi chạy** — chính sự mơ hồ "không biết tài khoản đã cấu hình chưa" đã làm `C-ORD-10` treo 2 tháng.
