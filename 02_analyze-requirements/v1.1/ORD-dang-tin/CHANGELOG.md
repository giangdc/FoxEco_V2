---
id: v1.1/ORD-dang-tin/changelog
title: Changelog — Module ORD
type: changelog
version: v1.1
sprint: 1
module:
  code: ORD
  dir: ORD-dang-tin
  name: Đăng tin & Quản lý tin
doc_source:
  - id: DOC-v1.1-01
    section: "§8.1 FR01 (Đăng tin NEED) + §8.1.1 BR01-01..09 + §8.1.3 + §8.1.4 UI/Field Spec · §8.2 FR02 (OFFER) + §8.2.1 BR02-01..04 · §8.5 FR05 (Quản lý tin) + §8.5.1 BR05-01..04 · §8.18 FR18 + §8.18.1 BR18-01..05 + §8.18.2 VAL-01..07 · §6.2 AC-01..AC-09, AC-19, AC-20, AC-30"
id_range:
  req: "REQ-ORD-023..028 (NEW, 6) + REQ-ORD-003, 005, 006, 007, 008, 009, 010, 011, 012, 013, 015, 016, 017, 018, 021 (MODIFIED, 15, giữ ID sprint 1)"
  sc: "SC-ORD-052..065 (NEW, 14) + SC-ORD-005, 012, 025, 026, 028, 029, 036, 041, 043, 044, 045, 050 (MODIFIED, 12, giữ ID sprint 1)"
  cl: "C-ORD-13 (NEW) + C-ORD-04 (MỞ LẠI), C-ORD-05, C-ORD-08, C-ORD-09, C-ORD-10, C-ORD-11 (đổi Status, giữ ID sprint 1) + C-ORD-14..17 (NEW 2026-09-16) · C-ORD-09 → Resolved, C-ORD-04/13 → Partially (2026-09-16)"
  risk: "RISK-ORD-09..12 (NEW, 4) + RISK-ORD-03, RISK-ORD-06 (Status/Severity cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-16
---

# Changelog — Module ORD (`ORD`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa INFO health-check F-06:** bổ sung khối *Source Detail per Scenario* cho **12 SC** (`SC-ORD-028/029/041/043/044/045/052/053/057/061/062/064`); gỡ ghi chú cũ *"quote gắn ở cột DOC Source"* — mỗi khối có 📍 location · quote AC riêng của SC (quote BR/field spec đã có home thì trỏ `↪` về `requirement_traceability.md`, không chép lại) · Analyst Note nêu chi tiết AC chưa phản ánh trong Then và phụ thuộc CL đang Open | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu | Không đổi `counts`/Then trong bảng SC — khi `generate-tc` đọc Analyst Note để siết Steps/Expected |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa WARNING health-check G-03:** thay 3 trích dẫn bị chép lặp sang file khác bằng dòng trỏ `↪` về đúng home (REQ → `requirement_traceability.md` · CL → `risk_assessment.md`) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Nội dung quote không mất — chỉ còn 1 home |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa theo health-check VERSION v1.1 (G-06b CRITICAL):** các đoạn register sống còn kể lại kết luận cũ của CL vừa Resolved (`C-ORD-09` · `C-ORD-04` · `C-ORD-13` — Khuyến nghị #1/#2/#4, ghi chú `REQ-ORD-003`, Source Detail `SC-ORD-005`) — đổi mục Khuyến nghị / heading / data catalog sang kết luận hiện hành và thêm dòng *"⛔ Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC"* sau các ghi chú gốc (giữ nguyên nội dung cũ làm hồ sơ, không xoá lặng lẽ) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Không đổi `counts`, không đổi Then SC — chỉ đồng bộ chữ với CL section |
| 2026-09-16 | UPDATE | **Áp câu trả lời BA** (`CL-hoi-BA-v1.1.xlsx`) + rà sâu lại `FR01/FR02/FR05`. (a) `C-ORD-09` → **Resolved** — nhãn chuẩn **"Tài liệu"**; `SC-ORD-005` assert cứng; `RISK-ORD-03` Resolved. (b) `C-ORD-04` → **Partially** — chip "Thuốc/Y tế" giữ, **không chặn/không cảnh báo**; còn vòng 2 về banner + điều khoản; `RISK-ORD-10` High → Medium. (c) `C-ORD-13` → **Partially** — nguồn **HRIS**, chỉ nhân sự **đang làm việc** (rule mới ⇒ thêm nhánh nghỉ việc); còn vòng 2 email mẫu + tên miền. (d) **Mở 4 CL mới** từ rà sâu: `C-ORD-14` (người nhận không có tài khoản ⇒ ai đóng đơn) · `C-ORD-15` (biên 7 ngày / buổi đã qua / mốc EXPIRED) · `C-ORD-16` (phạm vi sửa tin + vòng đời OFFER) · `C-ORD-17` (gỡ / đăng lại tin hết hạn) | BA trả lời 2026-09-16 · QC GiangDC2 yêu cầu rà kỹ từng chức năng | `counts` cl 11→15; ràng buộc #2 **hết hiệu lực**, #3 thu hẹp; `SC-ORD-005` + cụm `SC-ORD-031..035` cần **regenerate TC** |
| 2026-09-16 | UPDATE | Vibe-check qua demo (Playwright, wizard "Đăng tin" bước 1) — 3 phát hiện, KHÔNG resolve CL nào: (a) chip "Loại hàng" đầu tiên là **"Tài liệu"** khớp PRD (không phải "Giấy tờ, hồ sơ") — nhưng demo ≠ STG, `C-ORD-09` giữ nguyên ràng buộc dùng nhãn STG; (b) chọn chip **"Thuốc/Y tế"** không bị chặn/cảnh báo ngay — nhưng không tới được bước cuối để xem có checkbox cam kết hàng cấm không, vì (c) **wizard này không có `<input type=file>`** ⇒ không đính ảnh được ⇒ validation chặn vĩnh viễn ở bước 1, cũng là bằng chứng xác nhận `RISK-ORD-09` (ảnh bắt buộc) có tồn tại (lỗi "Vui lòng thêm ít nhất 1 ảnh hàng" khi bấm Tiếp theo mà chưa có ảnh) | Vibe-check thủ công qua Playwright, theo yêu cầu QC GiangDC2 2026-09-16 | `RISK-ORD-09` hạ xuống Partially confirmed; `C-ORD-04`/`C-ORD-09` giữ nguyên trạng thái, chỉ thêm bằng chứng phụ trong `risk_assessment.md` |
| 2026-09-15 | UPDATE | **DELTA v1.1 (lượt bù — module này bị bỏ sót ở lượt delta đầu).** Module lớn nhất dự án, và PRD đặc tả `FR01` dày nhất (9 BR + ~20 dòng field spec + 8 nhóm AC). Kết quả: **+6 REQ, +14 SC, +4 RISK, +1 CL**; **15 REQ / 12 SC MODIFIED**. Nhóm thay đổi lớn: (a) **ảnh món hàng từ *không rõ* → BẮT BUỘC ≥ 1, chặn sang bước 2** (`SC-ORD-054` P1); (b) **tra danh bạ nội bộ** — tích hợp hệ thống ngoài nêu tên lần đầu, 3 nhánh (`SC-ORD-058..060`); (c) **người nhận uỷ quyền khai ngay lúc đăng tin** — khái niệm mới, nối thẳng sang `FR07` của `DLV`; (d) `FR18` tiện ích dùng chung (carousel/lightbox · copy nhanh · ảnh gắn mốc bất biến) | `DOC-v1.1-01` §8.1/§8.2/§8.5/§8.18 · §6.2 AC-01..09, AC-19/20/30 | **4 CL đóng** ⇒ 4 SC hết dạng ghi-nhận, phải **regenerate TC**; 1 SC P1 mới phụ thuộc app đã siết ảnh chưa (`RISK-ORD-09`); 3 SC phụ thuộc STG có danh bạ chưa (`C-ORD-13`) |
| 2026-09-15 | ĐÍNH CHÍNH | 🔴 **Phát hiện PRD TỰ MÂU THUẪN** — `§8.1.4` để **"Thuốc/Y tế"** là giá trị hợp lệ của Loại hàng, `§8.1.1 BR01-07` lại xếp **"thuốc"** vào hàng cấm *"không được đăng"*; hai câu cách nhau 1 trang trong cùng `FR01`. ⇒ **`C-ORD-04` MỞ LẠI** (v1.0 đã Resolved *"KHÔNG chặn"*) | `DOC-v1.1-01` §8.1.4 (trang 35) vs §8.1.1 BR01-07 (trang 34) | Không phân xử được bằng thứ tự ưu tiên nguồn (cả hai đều là `DOC-v1.1-01`) ⇒ `SC-ORD-031..035` **GHI NHẬN**, ⛔ không assert chiều nào (`RISK-ORD-10`) |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | ~~🔴 KHÔNG dùng nhãn "Tài liệu" trong TC~~ — **HẾT HIỆU LỰC 2026-09-16** | `C-ORD-09` Resolved: BA chốt nhãn chuẩn là **"Tài liệu"**. Hiện hành: TC v1.1 dùng "Tài liệu"; app hiện "Giấy tờ, hồ sơ" = defect | Tiếp tục né "Tài liệu" ⇒ TC khẳng định sai nhãn, bug UI thật không bao giờ được log |
| 3 | 🟡 **"Thuốc/Y tế": assert *không chặn, không cảnh báo* khi chọn chip; ⛔ KHÔNG assert banner hàng cấm / nội dung điều khoản** | `C-ORD-04` Partially Resolved 2026-09-16 — vế chip đã chốt, vế banner/điều khoản chờ BA vòng 2 | Assert banner theo `BR01-07` trong khi BA nói *"đăng bất kỳ"* ⇒ bug report sai |
| 4 | ⛔ **KHÔNG tạo 1 SC cho mỗi dòng field spec** — PRD liệt kê ~20 dòng cho `FR01`; chỉ field mang **hành vi mới** (bắt buộc / chặn luồng / cross-field) mới sinh SC, còn lại **siết Then của SC sẵn có** | Áp `MASTER-MEMORY §9` biện pháp (b) — giảm rác thay vì fan-out máy móc. Module này đã 65 SC | SC phình vô ích; và `v1.1` vốn đã vượt ngưỡng gợi ý 200 SC/version |
| 5 | ⛔ **`SC-ORD-063` không assert cứng hành vi hoa/thường** | PRD bắt *"địa chỉ giao phải khác địa chỉ lấy"* nhưng **không định nghĩa phép so sánh**; `VAL-03` chỉ nói trim (`RISK-ORD-12`) | Bug report cho một hành vi tài liệu chưa định nghĩa |
| 6 | ⛔ **`SC-ORD-062`: bỏ trống SĐT uỷ quyền KHÔNG phải invalid** | `BR01-06` — khối uỷ quyền **không bắt buộc**; SĐT chỉ validate *"khi được nhập"* | TC "bỏ trống thì lỗi" sẽ FAIL vĩnh viễn trên một hành vi đúng |
| 7 | ⚠️ **Bộ ảnh mẫu chuẩn bị 1 lần, dùng chung 3 module** (`ORD` · `DLV` · `TS`) | `BR18-01` áp cùng trần 5 ảnh / ≤ 5MB / JPG-PNG cho **mọi điểm bằng chứng** | 3 bộ ảnh khác nhau ⇒ kết quả 3 module không so sánh được với nhau |
| 8 | ⛔ **`SC-ORD-041` không PASS chỉ vì "không có đường thử"** — vế *"mở link trực tiếp"* của `AC-20.1.02` không thực hiện được trên mobile | Không có URL trên app mobile ⇒ chỉ kiểm được vế *"không tìm, không xem"* | PASS giả cho một lớp kiểm soát truy cập chưa từng được kiểm |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"nhãn Loại hàng dùng theo app STG ('Giấy tờ, hồ sơ'), tuyệt đối không dùng 'Tài liệu'"** (ràng buộc #2 ở đây + ràng buộc 4 `03_test-cases/v1.0/CHANGELOG.md §2`) **HẾT HIỆU LỰC cho v1.1 kể từ 2026-09-16** — đừng trích lại. Hiện hành: nhãn chuẩn **"Tài liệu"** (BA chốt, `C-ORD-09`).


⛔ Kết luận **"Chip 'Thuốc/Y tế' KHÔNG bị chặn ở v1.0; banner chỉ là thông tin tĩnh"** (`C-ORD-04`, Resolved 2026-07-27) **KHÔNG CÒN AN TOÀN ĐỂ TRÍCH** — `DOC-v1.1-01 §8.1.1 BR01-07` nói ngược (*"Hàng cấm (thuốc, …) không được đăng"*). CL **mở lại**; hiện hành là **chưa có phán quyết**, chờ BA.

⛔ Kết luận **"địa chỉ lấy hàng không pre-fill — chưa rõ bug hay tài khoản chưa cấu hình"** (`C-ORD-10`, Open 2026-09-07) **HẾT HIỆU LỰC**. Hiện hành: **prefill là hành vi đặc tả** (`§8.1.4` + `AC-30.1.01`) ⇒ hồ sơ đã có địa chỉ mặc định mà wizard trống = **BUG**.

⛔ Kết luận **"màn Đăng tin thành công — chưa rõ có Mã tin hay không"** (`C-ORD-05`) và **"thoát wizard — chưa rõ có xoá form"** (`C-ORD-08`) **HẾT HIỆU LỰC**. Hiện hành: **không có mã đơn** (`AC-07.1.01` + `§8.1.3` bước 8) · **có popup xác nhận, thoát thì không lưu DRAFT** (`AC-01.2.01`).

⛔ Kết luận **"cơ chế ô địa chỉ chưa rõ — preset / chip / autocomplete?"** (`C-ORD-11`) **HẾT HIỆU LỰC**. Hiện hành: **ô văn bản tự do, ≤ 200 ký tự** (`§8.1.4`).

## 3. Nợ đang mở

| # | Nợ | Vì sao còn treo | Hướng xử lý |
|---|---|---|---|
| 1 | 🟡 **`C-ORD-04` vòng 2** — banner hàng cấm + nội dung điều khoản | Vế chip đã chốt 2026-09-16; câu *"hàng cấm không được đăng"* của `BR01-07` chưa rõ còn sống ở bề mặt nào | Chờ BA trả lời vòng 2 (sheet `ORD`) |
| 2 | 🔴 **`C-ORD-13` vòng 2** — email mẫu 3 loại (đang làm việc · nghỉ việc · không có) + tên miền | BA mới trả lời nguồn = HRIS; **không tự chế được** email mẫu | Hỏi BA/QTHT **trước `generate-tc`**; thiếu ⇒ `SC-ORD-058..060` (1 P1) `BLOCKED` |
| 3 | 🟡 **4 CL mới mở 2026-09-16** (`C-ORD-14..17`) | Phát hiện khi rà sâu `FR01/FR02/FR05` sau câu trả lời BA | Đã đưa vào `CL-hoi-BA-v1.1.xlsx` sheet `ORD`; `C-ORD-14` ưu tiên cao (đơn có thể kẹt vĩnh viễn) |
| 4 | 🟡 **Chưa xác nhận app đã siết ảnh bắt buộc** | `BR01-01` là hành vi mới; `KP-01 §10` không ghi nhận ràng buộc nào ở v1.0 | **Vibe-test 1 lượt wizard bước 1** trước `generate-tc` (`RISK-ORD-09`) |
| 5 | 🟡 **`SC-ORD-041` chỉ kiểm được 2/3 vế** | Vế *"mở link trực tiếp"* không có đường thử trên mobile app | Ghi nhận giới hạn trong TC; nếu có bản web/API thì bổ sung sau, ⛔ không PASS giả |
| 6 | 🟡 **`SC-ORD-044` phần backend không verify được** | `BR05-01` *"request sửa bị từ chối"* + `AC-08.1.02` *"không ghi mốc vào nhật ký"* là hành vi API | Ghi nhận theo `§Custom Rules §10.1` bước 3; cần API test thì để `implement-automation` sau |
