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
  cl: "C-ORD-13 (NEW) + C-ORD-04 (MỞ LẠI), C-ORD-05, C-ORD-08, C-ORD-09, C-ORD-10, C-ORD-11 (đổi Status, giữ ID sprint 1) + C-ORD-14..17 (NEW 2026-09-16) + C-ORD-18 (NEW 2026-09-17) · C-ORD-09 → Resolved, C-ORD-04/13 → Partially (2026-09-16) · C-ORD-04/13/14/15/16/17 → Resolved, C-ORD-18 NEW rồi Resolved cùng ngày (2026-09-17) ⇒ cl_open = 0"
  risk: "RISK-ORD-09..12 (NEW, 4) + RISK-ORD-03, RISK-ORD-06 (Status/Severity cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-17
---

# Changelog — Module ORD (`ORD`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-18 | UPDATE | ✅ **Gỡ phụ thuộc dev cho 2 TC hết hạn** — thêm **`SEED-ORD-05`** (fragment §0.5 + sheet `Seed` của TC-MASTER theo `§10.3` bước 4) với 3 lối lấy data xếp ưu tiên: 🥇 dùng **tin cũ có sẵn trên STG** đã tự quá "Đến ngày" · 🥈 tự đăng tin "Từ ngày" = "Đến ngày" = hôm nay rồi kiểm sáng hôm sau · 🥉 nhờ dev (chỉ khi 2 cách trên hỏng). Viết lại **Pre-condition · Steps · Test Data · Notes** của `TC-ORD-048` (5→6 step) và `TC-ORD-061` (5→4 step), **Expected giữ nguyên**, neo đúng step cuối (`§10.4`). Thêm 1 dòng `Tin đã quá "Đến ngày"` vào `test_data_catalog`. | QC GiangDC2 chốt 2026-09-18: *"2 case này có thể dùng data cũ đã tạo trước đó"* — STG đã chạy từ v1.0 nên có sẵn tin quá hạn | **2 TC hết Blocked** ⇒ ORD **88/88 = 100%** có data (86 → 88). ⛔ Số lượng TC **không đổi** (`§10.5`). drift fragment↔xlsx **0/48**, LATEST khớp md5. 🔁 Cách này áp được cho `TC-DLV-057/067` · `TC-ACT-008` · `TC-HOME-030` · `SC-TS-006` — nên rà lại kế hoạch "nhờ dev seed thời gian" của các module đó |
| 2026-09-18 | UPDATE | ✅ **`SEED-ORD-02` ② đã đủ** — email người **đã nghỉ việc** = `stag_binhnt23@fpt.com` (MNV 00026682), lấy từ `DOC-v1.1-05` `00_input/v1.1/datatest` mục *nghỉ việc*. Gỡ nợ §0.4 #2 của fragment, cập nhật §0.5 `SEED-ORD-02`, `TC-ORD-076` (Pre-condition · Test Data · Notes) ở fragment + TC-MASTER + LATEST (drift 0/48), và `test_data_catalog` dòng *Email công ty người nhận* (Fixture: cần QTHT cấp → ĐÃ ĐỦ). | QC GiangDC2 cung cấp 2026-09-18 (`DOC-v1.1-05`) — email này **đã nằm sẵn trong file datatest**, lượt rà trước bỏ sót | `TC-ORD-076` **hết Blocked** ⇒ ORD còn **2 TC** phải chờ dev (`TC-ORD-048`/`061` — lùi "Đến ngày", không seed được qua UI). ⚠️ Email này chỉ dùng làm **giá trị nhập** ở ô người nhận, ⛔ không đăng nhập bằng nó |
| 2026-09-17 | ĐÍNH CHÍNH | **`SC-ORD-059` giữ lifecycle `NEW` — huỷ nhãn `MODIFIED` gán cùng ngày.** `counts:` của `test_scenario_map.md` sửa `new 13→14` · `modified 13→12`; cột `Lifecycle` của dòng `SC-ORD-059` đổi `MODIFIED → NEW`. ⛔ Nội dung SC **không đổi** — Then vẫn là bản BA chốt ở `C-ORD-14` (nút "Tiếp theo" disable). | `health-check` lượt 2 ngày 2026-09-17. **Nhãn `MODIFIED` sai theo đúng định nghĩa của dự án** (*"giữ nguyên ID v1.0"*): `SC-ORD-059` sinh ở v1.1, v1.0 chỉ có `SC-ORD-001..051`. 🔬 Phép kiểm bắt được: `carried+modified+deprecated` của module ở v1.1 phải = tổng SC v1.0 của module đó — 10/11 module khớp, riêng `ORD` ra 52 ⟷ 51. ✅ Chứng cứ 2: `TC-MASTER-v1.1.xlsx` đã ghi `TC-ORD-075/076` là `Lifecycle NEW`. | Chỉ số đếm: `ORD` 14 NEW / 12 MOD · router §2a Tổng `90 NEW / 45 MODIFIED` · `MASTER §1/§3/§4/§5` đồng bộ. ⛔ **Không** đụng TC, không đụng Then, không đụng `C-ORD-14`. 📌 Bài học: *đảo oracle trong cùng version = sửa nội dung, ghi ở §2 Kết luận bị đảo — KHÔNG đổi cột `Lifecycle`.* |
| 2026-09-17 | ĐÍNH CHÍNH | **Sửa 2 chỗ nói ngược câu trả lời BA, phát hiện khi QC trả bài (drift `G-06b`).** (a) **`SC-ORD-059` ĐẢO Then:** vẫn ghi theo PRD `BR01-09`/`AC-04.1.02` *"không thấy → 3 ô mở cho nhập tay, luồng vẫn đi tiếp"* trong khi `C-ORD-14` (BA, 2026-09-17) đã chốt **nút "Tiếp theo" DISABLE, KHÔNG cho tạo đơn** — `CHANGELOG` lượt trước có ghi câu trả lời BA nhưng **quên sửa `test_scenario_map.md`**. Nay đảo Then, gộp luôn case *đã nghỉ việc* (cùng kết quả), Lifecycle NEW → **MODIFIED**. (b) **Tên miền nội bộ:** kết luận `C-ORD-13(3)` *"`@fpt.vn`, `@gmail.com`"* **bị đính chính** — hợp lệ là **email công ty `@fpt.com`**; `@gmail.com` chuyển thành **dữ liệu INVALID** của `SC-ORD-060`, `@fpt.vn` **chưa xác nhận lại ⇒ không dùng**. Đồng thời vế `C-ORD-13(4)` (*"đã nghỉ việc ⇒ nhập thủ công, không chặn"*) **hết hiệu lực** vì `C-ORD-14` mới hơn | QC GiangDC2 xác nhận trực tiếp 2026-09-17 (tên miền) · BA `C-ORD-14` 2026-09-17 (chặn tạo đơn) · rà chéo lúc trả bài | `counts` sc 65 **không đổi** · new 14→**13** · modified 12→**13** (SC-ORD-059 đổi Lifecycle). `SC-ORD-060` dựng được nhánh *ngoài tên miền* bằng `@gmail.com`. ⚠️ PRD `BR01-09`/`AC-04.1.02` nay **nói ngược BA** ⇒ thêm vào danh sách đề nghị BA sửa tài liệu |
| 2026-09-17 | UPDATE | **QC cung cấp ảnh UI thật wizard Bước 1/3 `gia tri hang uoc tinh.png` — đối chiếu với PRD `§8.1.4`, MỞ `C-ORD-18` (4 điểm lệch).** (1) 🔴 **"GIÁ TRỊ HÀNG (ƯỚC TÍNH)" có MỐC TIỀN** không nguồn nào từng có: `Thấp` *Dưới 1 triệu đ* · `Vừa` *1 – 5 triệu đ* · `Cao` *Trên 5 triệu đ* — ⚠️ KHÔNG lẫn với `C-ORD-02` (ngưỡng cấu hình + bảo hiểm, vẫn out of scope): đây chỉ là **nhãn phụ mô tả 3 mức định tính**, không có ô nhập tiền, không rule chặn. (2) nhãn UI **"TRỌNG LƯỢNG"** ⟷ PRD **"Khối lượng"**, option thêm nhãn phụ *Nhẹ/Trung bình/Nặng*. (3) kiểu control là **3 chip** ⟷ PRD ghi **Dropdown** ⇒ Steps TC viết "chọn chip". (4) block **Ghi chú nằm TRÊN CÙNG**, trước "Thông tin hàng". ✅ Đồng thời xác nhận khối **"ẢNH HÀNG \*"** đã có dấu `*` + bộ đếm **"0/5"** + helper bắt buộc ≥1/tối đa 5 ⇒ `BR01-01`/`BR18-02` đã build ở tầng UI, **thu hẹp `RISK-ORD-09`**. ⚠️ Nút "Tiếp theo" trên ảnh vẫn cam khi chưa chọn gì — nghi giới hạn ảnh tĩnh, **chưa kết luận, không log bug** | Ảnh UI demo `00_input/v1.1/design/gia tri hang uoc tinh.png` (`DOC-v1.1-03`), QC GiangDC2 cung cấp 2026-09-17 · đối chiếu `DOC-v1.1-01 §8.1.4` (tr.35) | `counts` cl 15→16 · cl_open 0→**1** (ORD **mở lại** 1 điểm hỏi BA). `SC-ORD-008/009/010/011/012` (v1.0) + `SC-ORD-052/053` cập nhật Given/Steps theo chip + GHI NHẬN nhãn; ⛔ không assert cứng mốc tiền, không FAIL vì tên nhãn |
| 2026-09-17 | UPDATE | **Rà lại `CL-hoi-BA-v1.1.xlsx` lần 2 theo yêu cầu QC — phát hiện dòng `C-ORD-16 (vòng 3)` có câu trả lời mới chưa xử lý.** BA đính lại đúng ảnh `ORD_08_dangtin_offer_ghide_len_don_dang_co.png` đã dùng ở vòng 2 — ảnh này KHÔNG trả lời được câu hỏi gốc (card OFFER trong list "Đơn của tôi" trông ra sao), chỉ tái xác nhận giới hạn demo (OFFER ghi đè đơn NEED). Câu (c) tạm còn treo — cần hỏi lại BA rõ hơn. **Đóng ngay sau đó cùng ngày** khi phát hiện `C-ACT-04` (cùng câu hỏi, module ACT) vừa giải được qua tái vibe-check đúng đường dẫn tab "Hoạt động" → "Đang diễn ra": card OFFER title "Nhận giao hàng &lt;tuyến&gt;", badge "Chờ ghép", CTA "Chạm để xem tuyến đường của bạn" — dùng chung kết quả cho cả 2 module. **`C-ORD-16` ĐÓNG HẲN** | Rà lại `CL-hoi-BA-v1.1.xlsx` theo yêu cầu QC 2026-09-17 · cross-ref kết quả vibe-check `C-ACT-04` | `counts` cl_resolved 14→15, module ORD **HẾT điểm hỏi BA**; `SC-ORD-041` dùng chung format card với `SC-ACT-015` |
| 2026-09-17 | UPDATE | **Rà soát toàn bộ workbook (không chỉ mục nhắc demo) theo yêu cầu QC.** Đóng nốt vòng 2 của `C-ORD-04` (banner/điều khoản hàng cấm — app CHƯA làm, tạm bỏ qua ở v1.1) và `C-ORD-13` (email mẫu + tên miền + hành vi nhánh nghỉ việc — hết blocking `generate-tc`) — 2 câu trả lời BA này đã nằm sẵn trong `CL-hoi-BA-v1.1.xlsx` từ 2026-09-16 nhưng chưa được đóng sổ ở file này | BA trả lời `CL-hoi-BA-v1.1.xlsx` sheet `ORD` 2026-09-16 (bỏ sót ở lượt trước) | `counts` cl_resolved 12→14; chỉ còn `C-ORD-16` (câu c) partial |
| 2026-09-17 | UPDATE | **Đồng bộ câu trả lời BA từ `CL-hoi-BA-v1.1.xlsx` (chưa được ghi vào file này ở lượt trước) + vibe-check demo.** `C-ORD-14/15/17` → **Resolved** (người nhận không tra HRIS ⇒ disable nút Tiếp theo, không kẹt đơn; biên 7 ngày = cộng 7; job EXPIRED chạy cuối ngày; "gỡ" là chữ dư PRD, "đăng lại" = đăng mới, card Hết hạn ở tab Đã hoàn thành mở được ⇒ `SC-ACT-009` cần sửa). `C-ORD-16` → **Partially Resolved** (a)(b) đã chốt (sửa được mọi field, không tính lại EXPIRED); (c) tin OFFER hiển thị ở "Đơn của tôi" **KHÔNG verify được qua demo** — demo dùng chung 1 đơn toàn cục, đăng OFFER ghi đè lên đơn NEED thay vì tạo card riêng (ảnh `ORD_08_dangtin_offer_ghide_len_don_dang_co.png`) | BA trả lời 2026-09-16/17 (`CL-hoi-BA-v1.1.xlsx`) · vibe-check demo QA GiangDC2 2026-09-17 (Playwright MCP) | `counts` cl_open 4→0, cl_resolved 9→12; `SC-ACT-009` (module ACT) cần sửa giả định "card Hết hạn không tap được"; `C-ORD-16` câu (c) đặt lại câu hỏi cho BA (không dựa demo) |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa INFO health-check F-06:** bổ sung khối *Source Detail per Scenario* cho **12 SC** (`SC-ORD-028/029/041/043/044/045/052/053/057/061/062/064`); gỡ ghi chú cũ *"quote gắn ở cột DOC Source"* — mỗi khối có 📍 location · quote AC riêng của SC (quote BR/field spec đã có home thì trỏ `↪` về `requirement_traceability.md`, không chép lại) · Analyst Note nêu chi tiết AC chưa phản ánh trong Then và phụ thuộc CL đang Open | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu | Không đổi `counts`/Then trong bảng SC — khi `generate-tc` đọc Analyst Note để siết Steps/Expected |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa WARNING health-check G-03:** thay 3 trích dẫn bị chép lặp sang file khác bằng dòng trỏ `↪` về đúng home (REQ → `requirement_traceability.md` · CL → `risk_assessment.md`) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Nội dung quote không mất — chỉ còn 1 home |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa theo health-check VERSION v1.1 (G-06b CRITICAL):** các đoạn register sống còn kể lại kết luận cũ của CL vừa Resolved (`C-ORD-09` · `C-ORD-04` · `C-ORD-13` — Khuyến nghị #1/#2/#4, ghi chú `REQ-ORD-003`, Source Detail `SC-ORD-005`) — đổi mục Khuyến nghị / heading / data catalog sang kết luận hiện hành và thêm dòng *"⛔ Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC"* sau các ghi chú gốc (giữ nguyên nội dung cũ làm hồ sơ, không xoá lặng lẽ) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Không đổi `counts`, không đổi Then SC — chỉ đồng bộ chữ với CL section |
| 2026-09-16 | UPDATE | **Áp câu trả lời BA** (`CL-hoi-BA-v1.1.xlsx`) + rà sâu lại `FR01/FR02/FR05`. (a) `C-ORD-09` → **Resolved** — nhãn chuẩn **"Tài liệu"**; `SC-ORD-005` assert cứng; `RISK-ORD-03` Resolved. (b) `C-ORD-04` → **Partially** — chip "Thuốc/Y tế" giữ, **không chặn/không cảnh báo**; còn vòng 2 về banner + điều khoản; `RISK-ORD-10` High → Medium. (c) `C-ORD-13` → **Partially** — nguồn **HRIS**, chỉ nhân sự **đang làm việc** (rule mới ⇒ thêm nhánh nghỉ việc); còn vòng 2 email mẫu + tên miền. (d) **Mở 4 CL mới** từ rà sâu: `C-ORD-14` (người nhận không có tài khoản ⇒ ai đóng đơn) · `C-ORD-15` (biên 7 ngày / buổi đã qua / mốc EXPIRED) · `C-ORD-16` (phạm vi sửa tin + vòng đời OFFER) · `C-ORD-17` (gỡ / đăng lại tin hết hạn) | BA trả lời 2026-09-16 · QC GiangDC2 yêu cầu rà kỹ từng chức năng | `counts` cl 11→15; ràng buộc #2 **hết hiệu lực**, #3 thu hẹp; `SC-ORD-005` + cụm `SC-ORD-031..035` cần **regenerate TC** |
| 2026-09-16 | UPDATE | Vibe-check qua demo (Playwright, wizard "Đăng tin" bước 1) — 3 phát hiện, KHÔNG resolve CL nào: (a) chip "Loại hàng" đầu tiên là **"Tài liệu"** khớp PRD (không phải "Giấy tờ, hồ sơ") — nhưng demo ≠ STG, `C-ORD-09` giữ nguyên ràng buộc dùng nhãn STG; (b) chọn chip **"Thuốc/Y tế"** không bị chặn/cảnh báo ngay — nhưng không tới được bước cuối để xem có checkbox cam kết hàng cấm không, vì (c) **wizard này không có `<input type=file>`** ⇒ không đính ảnh được ⇒ validation chặn vĩnh viễn ở bước 1, cũng là bằng chứng xác nhận `RISK-ORD-09` (ảnh bắt buộc) có tồn tại (lỗi "Vui lòng thêm ít nhất 1 ảnh hàng" khi bấm Tiếp theo mà chưa có ảnh) | Vibe-check thủ công qua Playwright, theo yêu cầu QC GiangDC2 2026-09-16 | `RISK-ORD-09` hạ xuống Partially confirmed; `C-ORD-04`/`C-ORD-09` giữ nguyên trạng thái, chỉ thêm bằng chứng phụ trong `risk_assessment.md` |
| 2026-09-15 | UPDATE | **DELTA v1.1 (lượt bù — module này bị bỏ sót ở lượt delta đầu).** Module lớn nhất dự án, và PRD đặc tả `FR01` dày nhất (9 BR + ~20 dòng field spec + 8 nhóm AC). Kết quả: **+6 REQ, +14 SC, +4 RISK, +1 CL**; **15 REQ / 12 SC MODIFIED**. Nhóm thay đổi lớn: (a) **ảnh món hàng từ *không rõ* → BẮT BUỘC ≥ 1, chặn sang bước 2** (`SC-ORD-054` P1); (b) **tra danh bạ nội bộ** — tích hợp hệ thống ngoài nêu tên lần đầu, 3 nhánh (`SC-ORD-058..060`); (c) **người nhận uỷ quyền khai ngay lúc đăng tin** — khái niệm mới, nối thẳng sang `FR07` của `DLV`; (d) `FR18` tiện ích dùng chung (carousel/lightbox · copy nhanh · ảnh gắn mốc bất biến) | `DOC-v1.1-01` §8.1/§8.2/§8.5/§8.18 · §6.2 AC-01..09, AC-19/20/30 | **4 CL đóng** ⇒ 4 SC hết dạng ghi-nhận, phải **regenerate TC**; 1 SC P1 mới phụ thuộc app đã siết ảnh chưa (`RISK-ORD-09`); 3 SC phụ thuộc STG có danh bạ chưa (`C-ORD-13`) |
| 2026-09-15 | ĐÍNH CHÍNH | 🔴 **Phát hiện PRD TỰ MÂU THUẪN** — `§8.1.4` để **"Thuốc/Y tế"** là giá trị hợp lệ của Loại hàng, `§8.1.1 BR01-07` lại xếp **"thuốc"** vào hàng cấm *"không được đăng"*; hai câu cách nhau 1 trang trong cùng `FR01`. ⇒ **`C-ORD-04` MỞ LẠI** (v1.0 đã Resolved *"KHÔNG chặn"*) | `DOC-v1.1-01` §8.1.4 (trang 35) vs §8.1.1 BR01-07 (trang 34) | Không phân xử được bằng thứ tự ưu tiên nguồn (cả hai đều là `DOC-v1.1-01`) ⇒ `SC-ORD-031..035` **GHI NHẬN**, ⛔ không assert chiều nào (`RISK-ORD-10`) |
| 2026-09-17 | UPDATE | **`C-ORD-18` Resolved trong ngày** — BA trả lời đủ 4 câu: (a) 3 mốc tiền `Dưới 1 triệu đ`/`1 – 5 triệu đ`/`Trên 5 triệu đ` là **con số chính thức** (b) nhãn chuẩn **"Trọng lượng"**, **giữ** nhãn phụ Nhẹ/Trung bình/Nặng (c) **lấy UI làm chuẩn** ⇒ 3 trường là **chip**, PRD ghi Dropdown là sai (d) block Ghi chú đặt trên "Thông tin hàng" là **đúng thiết kế**, là **textbox nhập được** | BA trả lời · QC GiangDC2 chuyển lời · `CL-hoi-BA-v1.1.xlsx` sheet `ORD` | `cl_open` 1 → **0** ⇒ `ORD` hết điểm hỏi BA, và là **CL Open cuối cùng của toàn v1.1**. `SC-ORD-052/053` bỏ rào *"ghi nhận nhãn, không FAIL vì tên nhãn"* → **assert cứng**. 3 điểm PRD `§8.1.4` hết hiệu lực (xem §2). `SC-ORD-008/009/010/011` (CARRIED) bị chạm — ghi nợ §3 |

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
| 9 | 🔴 **3 trường Bước 1/3 assert theo UI, ⛔ KHÔNG theo PRD `§8.1.4`** — nhãn **"Trọng lượng"** (không phải "Khối lượng") · control là **chip** (không phải Dropdown) · mốc tiền `Dưới 1 triệu đ`/`1 – 5 triệu đ`/`Trên 5 triệu đ` **assert cứng** | `C-ORD-18` Resolved 2026-09-17 — BA: *"Theo UI nhé, lấy UI làm chuẩn"*; mốc tiền là con số chính thức | Steps viết "mở dropdown" ⇒ người chạy không tìm thấy control; assert nhãn "Khối lượng" ⇒ FAIL oan trên hành vi đúng |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"nhãn Loại hàng dùng theo app STG ('Giấy tờ, hồ sơ'), tuyệt đối không dùng 'Tài liệu'"** (ràng buộc #2 ở đây + ràng buộc 4 `03_test-cases/v1.0/CHANGELOG.md §2`) **HẾT HIỆU LỰC cho v1.1 kể từ 2026-09-16** — đừng trích lại. Hiện hành: nhãn chuẩn **"Tài liệu"** (BA chốt, `C-ORD-09`).


⛔ Kết luận **"Email người nhận không tra thấy trong danh bạ → cho nhập thủ công, luồng đăng tin vẫn đi tiếp"** (`BR01-09` · `AC-04.1.02` · và cả `C-ORD-13(4)` BA vòng 2 2026-09-16 cho case *đã nghỉ việc*) **HẾT HIỆU LỰC từ 2026-09-17 — đừng trích lại.** Hiện hành: **nút "Tiếp theo" DISABLE, KHÔNG cho tạo đơn** cho **cả 2 case** (không tồn tại · đã nghỉ việc) — BA `C-ORD-14`, mới hơn. `SC-ORD-059` đảo Then, NEW → MODIFIED.

⛔ Kết luận **"tên miền nội bộ hợp lệ: `@fpt.vn`, `@gmail.com`"** (`C-ORD-13(3)`, BA vòng 2 2026-09-16) **HẾT HIỆU LỰC từ 2026-09-17** — QC GiangDC2 đính chính: hợp lệ là **email công ty `@fpt.com`**. `@gmail.com` nay là **dữ liệu INVALID** (nhánh *ngoài tên miền* của `SC-ORD-060`); `@fpt.vn` **chưa xác nhận lại ⇒ ⛔ không dùng**.

⛔ Kết luận **"Chip 'Thuốc/Y tế' KHÔNG bị chặn ở v1.0; banner chỉ là thông tin tĩnh"** (`C-ORD-04`, Resolved 2026-07-27) **KHÔNG CÒN AN TOÀN ĐỂ TRÍCH** — `DOC-v1.1-01 §8.1.1 BR01-07` nói ngược (*"Hàng cấm (thuốc, …) không được đăng"*). CL **mở lại**; hiện hành là **chưa có phán quyết**, chờ BA.

⛔ Kết luận **"địa chỉ lấy hàng không pre-fill — chưa rõ bug hay tài khoản chưa cấu hình"** (`C-ORD-10`, Open 2026-09-07) **HẾT HIỆU LỰC**. Hiện hành: **prefill là hành vi đặc tả** (`§8.1.4` + `AC-30.1.01`) ⇒ hồ sơ đã có địa chỉ mặc định mà wizard trống = **BUG**.

⛔ Kết luận **"màn Đăng tin thành công — chưa rõ có Mã tin hay không"** (`C-ORD-05`) và **"thoát wizard — chưa rõ có xoá form"** (`C-ORD-08`) **HẾT HIỆU LỰC**. Hiện hành: **không có mã đơn** (`AC-07.1.01` + `§8.1.3` bước 8) · **có popup xác nhận, thoát thì không lưu DRAFT** (`AC-01.2.01`).

⛔ Kết luận **"cơ chế ô địa chỉ chưa rõ — preset / chip / autocomplete?"** (`C-ORD-11`) **HẾT HIỆU LỰC**. Hiện hành: **ô văn bản tự do, ≤ 200 ký tự** (`§8.1.4`).

⛔ **3 điểm trong PRD `§8.1.4` (field spec Bước 1/3) HẾT HIỆU LỰC từ 2026-09-17 — đừng trích lại** (`C-ORD-18` Resolved, BA: *"Theo UI nhé, lấy UI làm chuẩn"*):
> (1) nhãn field **"Khối lượng"** → hiện hành là **"Trọng lượng"**, kèm nhãn phụ *Nhẹ/Trung bình/Nặng* mà PRD không có;
> (2) kiểu control **"Dropdown"** cho Giá trị hàng / Trọng lượng / Kích thước → hiện hành là **chip (segmented) nằm ngang** ⇒ Steps của TC viết *"nhấn chip"*, ⛔ không viết *"mở dropdown"*;
> (3) PRD **không có mốc tiền** cho 3 mức Giá trị hàng → hiện hành có và là **con số chính thức**: `Thấp` = *"Dưới 1 triệu đ"* · `Vừa` = *"1 – 5 triệu đ"* · `Cao` = *"Trên 5 triệu đ"*.
> ⇒ Nguồn chốt cho 3 trường này là **UI thực tế + câu trả lời BA 2026-09-17**, ⛔ KHÔNG phải PRD. App hiện theo PRD (nhãn "Khối lượng", dropdown) ⇒ **defect UI**, không phải TC sai. Đề nghị BA cập nhật `§8.1.4`.

## 3. Nợ đang mở

| # | Nợ | Vì sao còn treo | Hướng xử lý |
|---|---|---|---|
| 1 | ✅ ~~**`C-ORD-04` vòng 2** — banner hàng cấm + nội dung điều khoản~~ | **Đóng 2026-09-17** — BA: chip giữ, không chặn/không cảnh báo; **banner + nội dung điều khoản hàng cấm KHÔNG có ở v1.1** | Đã áp vào ràng buộc §2 #3; ⛔ không assert banner/điều khoản |
| 2 | 🟢 **`C-ORD-13` Resolved 2026-09-17 — còn 1 nợ DATA, không phải nợ CL** | Nguồn HRIS + tên miền `@fpt.com` + email *đang làm việc* `stag_anhdc4@fpt.com` đã có; nhánh *nghỉ việc* gộp vào `SC-ORD-059` (cùng kết quả chặn) | Chỉ còn xin BA **1 email mẫu thật của người đã nghỉ việc**, lấy lúc vibe-test; ⛔ không chặn `generate-tc` |
| 3 | ✅ ~~**4 CL mới mở 2026-09-16** (`C-ORD-14..17`)~~ | **Đóng hết 2026-09-17** — BA trả lời đủ 4 CL | `C-ORD-14` đảo Then của `SC-ORD-059` (xem §2 Kết luận bị đảo); `C-ORD-16` giải qua `C-ACT-04` cross-module |
| 4 | 🟢 **Chưa xác nhận app đã siết ảnh bắt buộc — THU HẸP 2026-09-17** | Ảnh UI demo cho thấy khối "ẢNH HÀNG \*" đã có dấu `*` + bộ đếm **"0/5"** + helper *"Bắt buộc ít nhất 1 ảnh · tối đa 5 ảnh"* ⇒ tầng UI đã build | Chỉ còn verify **hành vi chặn thật** (bấm "Tiếp theo" khi 0 ảnh) — gộp vào lượt vibe-check của `C-ORD-18` |
| 5 | ✅ ~~**`C-ORD-18`** — mốc tiền · nhãn · chip ⟷ Dropdown · vị trí Ghi chú~~ | **Đóng 2026-09-17** — BA trả lời đủ 4 câu, lấy UI làm chuẩn | Đã áp vào `risk_assessment.md` + ràng buộc §2 #9; ⛔ không hỏi lại |
| 6 | 🟡 **Vibe-check bấm thật wizard Bước 1/3** — nút "Tiếp theo" hiển thị cam/active dù chưa chọn gì và chưa có ảnh | Nghi là giới hạn ảnh tĩnh của demo, ⛔ chưa kết luận. **Không còn là điểm hỏi BA** — việc QA tự làm | Gộp 1 lượt vibe-check với nợ #4 (verify hành vi chặn ảnh bắt buộc); ⛔ **không log bug** dựa trên mỗi ảnh tĩnh |
| 7 | 🟡 **`SC-ORD-008/009/010/011` (CARRIED) bị `C-ORD-18` chạm nhưng chưa chính thức hoá MODIFIED** — nay assert mạnh hơn (mốc tiền chính thức · Ghi chú ở trên cùng, nhập được) | Ngoài `id_range` delta hiện tại; nội dung ở `../../v1.0/ORD-dang-tin/` mà `Project_rule` cấm sửa file v1.0 | Cân nhắc mở `analyze-requirements --module ORD` chính thức hoá 4 SC này thành MODIFIED nếu muốn regenerate TC cho chúng |
| 8 | 🟡 **`SC-ORD-041` chỉ kiểm được 2/3 vế** | Vế *"mở link trực tiếp"* không có đường thử trên mobile app | Ghi nhận giới hạn trong TC; nếu có bản web/API thì bổ sung sau, ⛔ không PASS giả |
| 9 | 🟡 **`SC-ORD-044` phần backend không verify được** | `BR05-01` *"request sửa bị từ chối"* + `AC-08.1.02` *"không ghi mốc vào nhật ký"* là hành vi API | Ghi nhận theo `§Custom Rules §10.1` bước 3; cần API test thì để `implement-automation` sau |

## 4. Vibe Status — kết quả thực thi trên STG

> ⚠️ **Vì sao ghi ở đây, không ở `v1.1/MEMORY.md §4`:** router v1.1 theo layout `module-first v2` **chỉ có**
> §1 Function Register + §2 Module Summary (`CLAUDE.md §MEMORY Files`) — không có §4 Vibe Status.
> Sổ cái verdict per-TC canonical là **`08_test-runs/vibe/coverage/coverage-ORD.md`**; mục này là bản trỏ đường.

> 🔴 **CẢNH BÁO TRÙNG TÊN — đọc trước khi tra cứu:** nhãn **`VR-002`** trong `KP-01 §10.2/§10.3`
> (`KB-VIBE-01`, `KB-VIBE-02`, `TC_04.5`/`TC_04.6`) là **run của ĐỢT v1.0 CŨ**, **KHÔNG** phải phiên này.
> Phiên này là `08_test-runs/vibe/VR-002-ORD-2026-09-18/` — đánh số theo `08_test-runs/vibe/INDEX.md` của dự án hiện tại (VR-001 = USR 2026-09-18).

**VR-002 · 2026-09-18 · mobile (Appium MCP, emulator-5554) · tài khoản A (MNV `00131946`)**
`08_test-runs/vibe/VR-002-ORD-2026-09-18/`

| Chỉ số | Giá trị |
|---|---|
| SCOPE_TOTAL | **88 TC** = 48 (v1.1) + 40 (CARRIED v1.0) — v1.1 **không gộp CARRIED** |
| Chạy trong phiên | **43** (25 ✅ PASS · 14 ❌ FAIL · 3 🚫 BLOCKED · 1 chạy dở) |
| Có verdict cuối | **42/88** |
| Còn nợ | **46 ⏳ NOT_RUN** — hết sức phiên sau lô 3; ⛔ **không** blocker data nào chặn cứng (trừ `069`) |
| Evidence | **43/43 TC** có ảnh riêng · gate `verify_evidence.py` **0 vi phạm fabrication** |

### Ảnh hưởng tới các SC của module

| Nhóm SC | Kết luận từ app thật |
|---|---|
| `SC-ORD-005` Loại hàng | ✅ **Oracle `C-ORD-09` KHỚP APP**: đúng 8 chip, thứ tự y hệt, **mặc định "Tài liệu"**. 🔴 **`KB-VIBE-01` của `KP-01 §10.2` (đợt cũ) ĐÃ LỖI THỜI** — nó ghi *"app không có chip Tài liệu, mặc định Giấy tờ, hồ sơ"*; app hôm nay **không còn** nhãn `Giấy tờ, hồ sơ` ⇒ mọi ràng buộc dẫn `KB-VIBE-01` (kể cả ở module khác) phải **kiểm lại trước khi dùng**. |
| `SC-ORD-007` chip không deselect | ✅ `KB-VIBE-02` **vẫn đúng**: nhấn lại chip đang chọn **không** bỏ chọn ⇒ không tái hiện được trạng thái "chưa chọn loại hàng". |
| `SC-ORD-008..011` giá trị hàng + ghi chú | ✅ 3 chip tier + **mốc tiền là nhãn chính thức** (`Dưới 1 triệu đ` / `1 – 5 triệu đ` / `Trên 5 triệu đ`) · banner "Cao" **đúng nguyên văn** · khối GHI CHÚ **nằm TRÊN** khối Thông tin hàng, `max-text-length=300`, ⛔ không có ô nhập số tiền ⇒ **gỡ nợ §0.4 #1**: 2 điểm này nay **assert cứng được**, đủ căn cứ mở `MODIFIED` ở lượt analyze sau. |
| `SC-ORD-052/053` trọng lượng + kích thước | ✅ Nhãn **"TRỌNG LƯỢNG"** + Nhẹ/Trung bình/Nặng và **"KÍCH THƯỚC"** + Cầm tay/~20×20/> 20×20 **khớp 100%** oracle `C-ORD-18` ⇒ ⛔ **không có** defect nhãn "Khối lượng"/Dropdown như §0.2 dự phòng. ❌ Nhưng **thiếu thông báo lỗi** khi chưa chọn (bug chặn-im-lặng). |
| `SC-ORD-054/055/056` ảnh | ✅ Tầng UI đúng (`ẢNH HÀNG *`, `0/5`, helper nguyên văn) · ✅ chặn ảnh > 5MB **có thông báo** · ❌ **chặn thiếu ảnh KHÔNG có thông báo** (P1) · 🐞 **trần thực tế chỉ 4/5 ảnh** (nút thêm mất sau ảnh 4, ảnh 4 không xoá được) ⇒ `RISK-ORD-09` **mở lại ở chiều khác**: tầng UI có, nhưng **chính khối ảnh** lỗi. |
| `SC-ORD-058/059/060` email người nhận | ✅ `C-ORD-14` **được thi hành**: email không có trên HRIS / đã nghỉ việc ⇒ `Tiếp theo` **disable kể cả khi điền tay đủ** ⇒ ⛔ không cho tạo đơn. ❌ Nhưng **chuỗi hướng dẫn còn của v1.0** (*"vui lòng nhập tay…"*) và **email sai định dạng KHÔNG có lỗi định dạng**. ⚠️ App **không phân biệt** *ngoài tên miền* vs *không có trên HRIS*. ❌ Autofill chỉ **2/3 ô** (thiếu địa chỉ giao) — **cần BA chốt** `AC-04.x`. |
| `SC-ORD-025/026` địa chỉ | ✅ Prefill **địa chỉ mặc định hồ sơ** đúng `C-ORD-10` + sửa được · ✅ ô **văn bản tự do**, ⛔ không preset/gợi ý (khác hẳn ô địa chỉ của module USR) · ✅ trần **200 ký tự** đúng biên. |
| `SC-ORD-028/029` ngày + buổi | ✅ `C-ORD-15(a)` đúng cả 2 chiều: khoảng **7 ngày hợp lệ**, **8 ngày** hiện lỗi *"Đến ngày tối đa 7 ngày kể từ Từ ngày"* · ✅ chặn ngày quá khứ + chặn `Đến < Từ` **ở tầng picker** (làm mờ ngày). ❌ **`C-ORD-15(b)` KHÔNG được thi hành**: 13:44 vẫn chọn được buổi `Sáng (8–12h)` của hôm nay. ❌ Buổi mong muốn **không có mặc định** (PRD `§8.1.4` chốt `Sau giờ làm`). |
| `SC-ORD-050` thoát wizard | ❌ **KHÔNG có popup** `Thoát và bỏ nội dung đã nhập?` — back ở bước 1 **thoát thẳng + xoá dữ liệu soạn dở**, trái `AC-01.2.01` + `C-ORD-08`. ✅ Vế *"không lưu nháp"* thì **đúng**: mở lại wizard là form trắng, 2 tab Hoạt động không có tin nháp. ⚠️ Back ở **bước 2** = **lùi về bước 1**, không đóng wizard ⇒ Steps của `TC-ORD-053`/`062` mô tả sai đường đi. |
| **Bề mặt chưa có trong scenario_map** | (1) host app FoxPro **đổi tab** sang THÔNG BÁO sau khi FoxEco đóng photo picker (nhánh ảnh > 5MB) · (2) một thông báo dùng chung cho 2 nhánh email invalid · (3) tầng lọc định dạng file thuộc app hay OS picker (`TC-ORD-069` BLOCKED). ⇒ 📨 route `/analyze-requirements` (xem `vibe-report.md §Phản hồi ngược`). |

### Nợ đã gỡ / phát sinh từ phiên này

| Nợ §0.4 | Trạng thái sau VR-002 |
|---|---|
| #1 mốc tiền + vị trí khối Ghi chú chưa có TC | ✅ **Đủ căn cứ assert cứng** (đo trực tiếp trên app) — vẫn cần lượt `analyze-requirements --module ORD` để chính thức hoá `MODIFIED` |
| #2 email người nghỉ việc | ✅ **Đã gỡ từ 2026-09-18**, `TC-ORD-076` chạy được và **PASS** |
| #3 nút "Tiếp theo" hiện cam dù chưa chọn gì | ✅ **Đã kiểm: KHÔNG phải defect** — trên app thật nút có `enabled=false` và bị làm mờ; ảnh tĩnh của demo gây nhầm |
| #4 `SC-ORD-041` vế "mở link trực tiếp" | ⏳ chưa tới (thuộc 46 TC còn nợ) |
| #5 `SC-ORD-044` vế "request sửa bị từ chối" | ⏳ chưa tới |
| **MỚI** | 🐞 trần ảnh 4/5 (`SC-ORD-056` không kiểm được hết) · 🔴 `KB-VIBE-01` lỗi thời · 🔴 4 TC CARRIED hết hiệu lực (`006`/`007`/`008`/`014`) chờ QC chốt `DESCOPED` |
