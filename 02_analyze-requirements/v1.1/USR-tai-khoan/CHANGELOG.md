---
id: v1.1/USR-tai-khoan/changelog
title: Changelog — Module USR
type: changelog
version: v1.1
sprint: 1
module:
  code: USR
  dir: USR-tai-khoan
  name: Tài khoản & Hồ sơ
doc_source:
  - id: DOC-v1.1-01
    section: "§8.15 FR15 (Hồ sơ & cập nhật thông tin) · §8.15.1 BR15-01..05 · §8.15.2 UI/Field Spec · §6.1 US30 · §6.2 AC-30.1.01 / AC-30.1.02 / AC-30.2.01 / AC-30.2.02"
id_range:
  req: "REQ-USR-008, REQ-USR-009, REQ-USR-010 (NEW) + REQ-USR-002, REQ-USR-006 (MODIFIED, giữ ID sprint 1)"
  sc: "SC-USR-013..023 (NEW, 12 — 021..024 thêm 2026-09-16) + SC-USR-002, SC-USR-003, SC-USR-007, SC-USR-011, SC-USR-012 (MODIFIED — 007/011 từ 2026-09-16, giữ ID sprint 1)"
  cl: "C-USR-05 (NEW, Open) + C-USR-03 (ĐẢO → Resolved), C-USR-04 (→ Resolved 2026-09-16 qua demo) — giữ ID sprint 1 + C-USR-06 (NEW 2026-09-16) · C-USR-05 → Partially → **Resolved** (2026-09-16) · C-USR-06 → Resolved (2026-09-16)"
  risk: "RISK-USR-06, RISK-USR-07, RISK-USR-08 (NEW) + RISK-USR-01, RISK-USR-03 (Status/Why cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-17
---

# Changelog — Module USR (`USR`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-17 | UPDATE | **BA trả lời 2 dòng không mã CL ở sheet `USR`:** (1) **chuỗi lỗi SĐT** — *"lấy theo demo đúng r nhé"* ⇒ chuỗi demo là **chính thức** (trống: "Vui lòng nhập số điện thoại" · sai định dạng: "Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)"); `test_data_catalog` + 5 TC (`TC-USR-016/017/019/020/036`) bỏ chữ "tạm". (2) **Đề nghị cập nhật PRD** — *"PRD cập nhật sau nhé"* ⇒ BA nhận, chưa có hạn; TC giữ theo câu trả lời BA | BA trả lời `CL-hoi-BA-v1.1.xlsx` sheet `USR` 2026-09-17 | Không đổi `counts`/Expected. Thêm Nợ #4 (theo dõi PRD bản sửa) |
| 2026-09-16 | UPDATE | **Rà lại điều hướng + thành phần màn "Cập nhật thông tin" qua code demo.** Gộp vào SC có sẵn (không thêm SC): `SC-USR-013` + header ← / tiêu đề, **không có thanh tab dưới**, lối vào duy nhất; `SC-USR-014` + **lưu xong vẫn ở lại màn**, bấm ← về trang Cá nhân. Ghi phát hiện: **demo giữ bản nháp chưa lưu** khi mở lại màn (lệch `SC-USR-024`) | Đọc code `DOC-v1.1-02` 2026-09-16 | Không đổi `counts` |
| 2026-09-16 | UPDATE | **BA trả lời lượt 5 — `C-USR-05` Resolved:** tên luôn ≥ 2 từ ("Trần A" → `TA`) ⇒ bỏ biên tên 1 từ; bấm ← khi chưa lưu ⇒ **không lưu, không hỏi xác nhận** ⇒ **+1 SC NEW `SC-USR-024`** (P3). Module USR **hết CL mở** | BA trả lời 2026-09-16 | `counts` sc 23→24 · new 11→12 · p3 6→7; cl_resolved 5→6; `RISK-USR-08` Resolved; tổng v1.1 298→299 |
| 2026-09-16 | UPDATE | **BA trả lời lượt 4:** chọn văn phòng ⇒ điền chuỗi `name`; khớp **chứa chuỗi** (thêm từ khoá `tan` = 36); **`C-USR-06` Resolved — badge "Hạng Đồng hành" KHÔNG hiện** ⇒ `SC-USR-007` lật chiều + `SC-USR-011` cập nhật header (CARRIED → **MODIFIED**); **SĐT mặc định khởi tạo từ HRIS** ⇒ **+1 SC NEW `SC-USR-023`**; SĐT = đầu 0 + đúng 10 ký tự số ⇒ `SC-USR-015` thêm lớp invalid (khoảng trắng · `+84` · chữ · 9/11 số · không đầu 0) | BA trả lời 2026-09-16 | `counts` sc 22→23 · new 10→11 · modified 3→5 · carried 9→7 · p2 13→14; cl_open 1→0, cl_resolved 4→5; `v1.1/MEMORY.md` + `MASTER-MEMORY` tổng 297→298 |
| 2026-09-16 | UPDATE | **Nhận file danh sách văn phòng** `00_input/v1.1/location_address_catalog.xlsx` → đăng ký `DOC-v1.1-04` (MASTER-MEMORY §1). Profile: 399 văn phòng active, oracle cột `name`; ⚠ 118 tên cắt 30 ký tự, toạ độ MISSING. Tạo `04_test-data/valid/USR-office-catalog.md` (từ khoá K1–K7 đã đối chiếu). `SC-USR-021` thay từ khoá giả định bằng từ khoá thật + số kết quả | BA cung cấp 2026-09-16 | Không đổi `counts`; đóng nợ #4 |
| 2026-09-16 | UPDATE | **BA trả lời lượt 3:** gợi ý văn phòng tìm theo **tên**, không phân biệt **dấu** + **hoa thường**; không khớp ⇒ **không gợi ý**; avatar chữ viết tắt **không dấu**; **`C-USR-05(b)` chốt CÓ** prefill địa chỉ mặc định sang lấy hàng · giao hàng · điểm xuất phát. `SC-USR-021` bỏ các điểm "không assert", thêm 3 dạng từ khoá + nhánh không khớp; `SC-USR-002`/test data avatar không dấu | BA trả lời 2026-09-16 | Không đổi `counts`; prefill giao hàng/điểm xuất phát có home ở `ORD`/`ASN` — ⛔ chưa sửa, cần lượt update riêng |
| 2026-09-16 | UPDATE | **Chi tiết rule `Địa chỉ mặc định`:** gợi ý từ **3 ký tự**; gõ tay không chọn ⇒ **rời ô thành rỗng, lưu rỗng**; **cho phép để trống**; mở màn: **đã lưu > HRIS > rỗng**; danh sách văn phòng lấy từ **file data (BA gửi sau)**. `SC-USR-020` đổi Then (rỗng thay vì giữ địa chỉ cũ); `SC-USR-021` thêm biên 2/3 ký tự; `SC-USR-022` fan-out 3 trường hợp nguồn giá trị; test data thêm dòng danh sách văn phòng + 3 tài khoản | BA trả lời 2026-09-16 | Không đổi `counts` (vẫn 22 SC); còn mở: khớp có dấu/không dấu · hiển thị khi không có kết quả |
| 2026-09-16 | UPDATE | **Chốt rule `Địa chỉ mặc định`:** load từ **HRIS**, cho sửa, sửa bằng **gõ → chọn từ danh sách văn phòng**, ⛔ không nhận text tự do. `SC-USR-020` viết lại (*"≤ 200 ký tự"* → *"không nhận text gõ tay"*, P3→P2); **+2 SC NEW** `SC-USR-021` (gợi ý + chọn) · `SC-USR-022` (khởi tạo từ HRIS); `SC-USR-014` bước sửa địa chỉ đổi sang chọn từ danh sách; test data bỏ biên 200/201. Demo (textarea tự do) **lệch rule** | BA xác nhận 2026-09-16 | `counts` sc 20→22, new 8→10, p2 10→13, p3 7→6; `v1.1/MEMORY.md` §2 + `MASTER-MEMORY` §1/§3/§4 cập nhật tổng 295→297 |
| 2026-09-16 | ĐÍNH CHÍNH | **Icon cạnh Email công ty là KHIÊN, không phải khoá.** Mô tả ảnh `USR_02` trước đó ghi nhầm "khoá" (chép theo PRD thay vì nhìn UI). `SC-USR-016` + test data đổi oracle sang **icon khiên**; quote PRD giữ nguyên verbatim ("icon khoá") và ghi lệch PRD ↔ UI | BA xác nhận 2026-09-16 · code demo `EcoIcons.Shield` | Không đổi `counts`; nên báo BA sửa chữ `BR15-01`/`AC-30.2.01`/`§8.15.2` |
| 2026-09-16 | UPDATE | **Chốt `C-USR-05(a)` avatar:** avatar trang Cá nhân và màn "Cập nhật thông tin" là **một**, hiện **chữ viết tắt 2 từ cuối của Tên** ("Trần Văn A" → `VA`), chỉ đọc. `SC-USR-002` bỏ *"icon placeholder"*, assert chữ viết tắt; `SC-USR-016` thêm avatar chỉ đọc; test data tách dòng Avatar. Demo trang Cá nhân hiện icon người ⇒ **lệch rule**, verify trên STG | BA xác nhận 2026-09-16 | Không đổi `counts`; `C-USR-05` vẫn Partially (còn câu b) |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa INFO health-check F-06:** bổ sung khối *Source Detail per Scenario* cho **2 SC** (`SC-USR-019`, `SC-USR-020`) — mỗi khối có 📍 location · quote AC riêng của SC (quote BR/field spec đã có home thì trỏ `↪` về `requirement_traceability.md`, không chép lại) · Analyst Note nêu chi tiết AC chưa phản ánh trong Then và phụ thuộc CL đang Open | `/health-check` 2026-09-16 | Không đổi `counts`/Then trong bảng SC — khi `generate-tc` đọc Analyst Note để siết Steps/Expected |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa WARNING health-check G-03:** thay 1 trích dẫn bị chép lặp sang file khác bằng dòng trỏ `↪` về đúng home (REQ → `requirement_traceability.md` · CL → `risk_assessment.md`) | `/health-check` 2026-09-16 | Nội dung quote không mất — chỉ còn 1 home |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa theo health-check VERSION v1.1 (G-06b CRITICAL):** các đoạn register sống còn kể lại kết luận cũ của CL vừa Resolved (`C-USR-05` — Khuyến nghị #5) — đổi mục Khuyến nghị / heading / data catalog sang kết luận hiện hành và thêm dòng *"⛔ Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC"* sau các ghi chú gốc (giữ nguyên nội dung cũ làm hồ sơ, không xoá lặng lẽ) | `/health-check` 2026-09-16 | Không đổi `counts`, không đổi Then SC — chỉ đồng bộ chữ với CL section |
| 2026-09-16 | UPDATE | **Áp câu trả lời BA** + rà sâu `FR14`/`FR15` đối chiếu SC CARRIED. (a) `C-USR-05` → **Partially Resolved**: (c) **kênh liên hệ bỏ hẳn** ⇒ `SC-USR-010` assert không tồn tại; (a) avatar *"load từ HRIS, không cho sửa ??"* và (b) *"khu vực/văn phòng load theo địa chỉ mặc định; địa chỉ lấy hàng/giao hàng/điểm xuất phát load theo địa chỉ mặc định ?"* — BA để dấu hỏi và (b) **sinh rule prefill mới ngoài PRD** đụng `AC-04.1.01` + `§8.2.2` ⇒ hỏi vòng 2. (b) **Mở `C-USR-06`**: badge "Hạng Đồng hành" (`SC-USR-007` v1.0 assert tồn tại) mâu thuẫn `BR14-03`/`AC-26.1.01` cấm mọi tier | BA trả lời 2026-09-16 | `counts` cl 5→6; `RISK-USR-08` Partially; `SC-USR-007` hạ xuống không assert; `SC-USR-010` regenerate TC |
| 2026-09-15 | ĐÍNH CHÍNH | 🔴 **Quyết định *"`USR` không có delta ở v1.1"* (ghi ở `MASTER-MEMORY §2` ghi chú registry, cùng ngày) là SAI và đã được gỡ.** Hai bằng chứng: (a) `FR15` đặc tả **một màn mới** (`"Cập nhật thông tin"`) với 5 BR + 4 AC — đây là thay đổi hành vi thật, không phải "đề xuất xung đột"; (b) **chính lượt delta trước đã trích `AC-30.1.01` — một AC THUỘC `FR15`** — làm nguồn resolve `C-ORD-10`, tức đã dùng `FR15` làm căn cứ trong khi tuyên bố nó ngoài phạm vi | BA nêu lại 2026-09-15 (*"1.1 chỗ profile có update"*); rà lại `DOC-v1.1-01` §8.15 toàn văn | Module chuyển từ *"không delta"* sang **có delta**; `v1.1/MEMORY.md` §1/§2 và `MASTER-MEMORY` §1/§3/§4/§5/§8b phải cập nhật theo |
| 2026-09-15 | UPDATE | **DELTA v1.1 (lượt bù thứ hai).** Kết quả: **+3 REQ, +8 SC, +3 RISK, +1 CL**; **2 REQ / 3 SC MODIFIED**. Ba việc lớn: (a) `C-USR-03` **ĐẢO** — hồ sơ từ *view-only hoàn toàn* thành *có màn sửa 2 trường*, `SC-USR-003` lật chiều; (b) `BR15-03`/`BR15-04` thêm **2 rule truy vết hai chiều** — thành viên thứ tư của nhóm rule mà app đã vi phạm 1 lần; (c) `C-USR-04` đóng được **nửa** (nhãn menu), `C-USR-05` mở mới cho 3 trường PRD không nhắc | `DOC-v1.1-01` §8.15 + §8.15.1 + §8.15.2 · §6.1 US30 · §6.2 AC-30.x | Risk Level module **Low → Medium**; 8 SC mới phụ thuộc app đã build `FR15` chưa (`RISK-USR-06`) |
| 2026-09-16 | UPDATE | Vibe-check qua demo (`https://giangdc.github.io/foxeco_demo/FoxEcoQC`, vai Sender, Playwright) — **đóng nốt nửa còn lại của `C-USR-04`**: chụp được cả trang Cá nhân (`00_input/v1.1/design/USR_01...png`) và màn "Cập nhật thông tin" (`USR_02...png`), xác nhận 2 màn có 2 bộ trường khác nhau đúng như cảnh báo. `RISK-USR-03` đóng theo. `RISK-USR-06` hạ xuống Partially confirmed (màn đã tồn tại + đúng field spec qua demo; persist trên STG thật chưa verify vì demo không có backend). Phát hiện phụ ngoài đặc tả: badge "Hạng Đồng hành" trên trang Cá nhân — không có trong BRD/PRD, chỉ ghi nhận không assert. `C-USR-05` vẫn Open nhưng có thêm bằng chứng: avatar không có control đổi ảnh trên cả 2 màn (câu (a) gần như trả lời được); "khu vực/văn phòng"/"kênh liên hệ" không xuất hiện ở đâu trong demo (chưa đủ để Resolve, chỉ thu hẹp câu hỏi còn (b)(c)) | Vibe-check thủ công qua Playwright 2026-09-16 | `SC-USR-002`/`SC-USR-012` hết `[GAP]`, có thể assert cứng danh sách trường trang Cá nhân; `counts.cl_resolved` 3→4 |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | 🔴 **`SC-USR-003` phải lấy bản `v1.1/`** — bản v1.0 và v1.1 có Then **ngược nhau** ở phần *"có control sửa hay không"* | `C-USR-03` bị `FR15` đảo. **Cả hai bản đều chạy được** nên không có gì báo lỗi khi lấy nhầm | Chạy nhầm bản cho kết luận ngược, và **im lặng** — cùng bẫy `SC-CNL-006` |
| 3 | ⛔ **KHÔNG đọc `C-USR-03` thành "hồ sơ sửa được"** — hồ sơ có **2 vùng**: SSO chỉ đọc (4 trường) ⟷ sửa được (đúng **2** trường) | `BR15-01` giữ nguyên tinh thần view-only cho vùng SSO; `FR15` chỉ mở 2 trường | Viết TC cho phép sửa tên/email ⇒ FAIL vĩnh viễn trên một hành vi đúng |
| 4 | ⛔ **KHÔNG lấy `§8.15.2` làm danh sách trường của TRANG CÁ NHÂN** — đó là field spec của **màn "Cập nhật thông tin"**, một màn khác | `C-USR-04` Resolved 2026-09-16 qua demo — 2 màn đã có bằng chứng UI riêng, đừng gộp | `SC-USR-002` assert sai danh sách trường |
| 5 | ⭐ **`SC-USR-014` · `017` · `018` bắt buộc có bước "ghi lại giá trị TRƯỚC"** | Banner xanh chỉ chứng minh app *nói* đã lưu; sai lệch hồ sơ/đơn không nhìn ra được nếu chỉ đọc số một lần | Cả ba PASS giả cho một màn/rule đang hỏng |
| 6 | ⛔ **KHÔNG nhân bản SC prefill sang `ORD`** — `SC-ORD-025` kiểm *wizard nhận đúng giá trị*, `SC-USR-018` kiểm *hồ sơ không bị ghi đè* | Hai đầu của cùng một sợi dây, fail độc lập | TC trùng; hoặc tệ hơn: cả hai cùng kiểm một đầu, đầu kia không ai kiểm |
| 7 | ⛔ **KHÔNG tạo test data/SC riêng cho "khu vực/văn phòng"** — đó chính là `Địa chỉ mặc định` (chọn từ danh sách văn phòng); kênh liên hệ chỉ assert **không tồn tại** | BA chốt 2026-09-16 (`C-USR-05`) | TC trùng cho cùng 1 trường |
| 8 | 🔴 **`SC-USR-007` phải lấy bản `v1.1/`** — v1.0 assert badge "Hạng Đồng hành" **có**, v1.1 assert **không có** | `C-USR-06` Resolved 2026-09-16 (BA chốt không hiện, khớp `BR14-03`) | Lấy nhầm bản v1.0 ⇒ PASS cho một defect — cùng bẫy `SC-USR-003` |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"màn Cá nhân view-only hoàn toàn — KHÔNG có chức năng sửa hồ sơ"** (`C-USR-03`, Resolved 2026-07-24 **theo quan sát app STG**, home canonical ở `v1.0/USR-tai-khoan/risk_assessment.md`) **HẾT HIỆU LỰC kể từ v1.1** — đừng trích lại. Hiện hành: **CÓ** màn `"Cập nhật thông tin"` (trang Cá nhân, dưới mục "Quà đã nhận") cho sửa **đúng 2 trường** — `Số điện thoại mặc định` · `Địa chỉ mặc định`; 4 trường SSO vẫn chỉ đọc (`DOC-v1.1-01 §8.15`). Bản v1.0 **giữ nguyên không sửa** làm hồ sơ lịch sử.

⛔ Kèm theo: khai **"`USR` không có delta ở v1.1 — `FR15` không áp dụng"** (`MASTER-MEMORY §2` ghi chú registry, 2026-09-15) **HẾT HIỆU LỰC**. Ghi chú đó nhầm **đề xuất xung đột** (`FR15` cho sửa SĐT/địa chỉ ⟷ `C-USR-03` view-only) thành **lý do bỏ qua cả FR** — trong khi xung đột đó chính là nội dung cần phân tích.

📌 **Bài học rút ra (áp cho mọi module):** cả hai lần đảo kết luận của dự án (`C-CNL-01` và `C-USR-03`) đều rơi vào CL được Resolved **theo quan sát app**, ⛔ không theo tài liệu. ⇒ CL loại này là **ứng viên số 1 để rà lại** mỗi khi có tài liệu mới; nên đánh dấu rõ khi ghi.

## 3. Nợ đang mở

| # | Nợ | Vì sao còn treo | Hướng xử lý |
|---|---|---|---|
| 1 | 🟡 **Chưa xác nhận persist thật trên STG** | Vibe-check 2026-09-16 xác nhận màn "Cập nhật thông tin" tồn tại + đúng field spec qua demo, nhưng demo không có backend nên nút "Lưu thay đổi" chưa verify được là có lưu thật | **Vibe-test 1 lượt trên STG thật trước `generate-tc`** — xác nhận persist. Nếu STG cũng khớp thì hạ hẳn `RISK-USR-06` xuống Resolved |
| 2 | 🟡 **SC prefill ở `ORD`/`ASN` chưa cập nhật** (`C-USR-05` đã Resolved 2026-09-16) | Rule prefill lấy hàng/giao hàng/điểm xuất phát chốt ở USR nhưng home SC ở module khác | 1 lượt update `ORD` (`SC-ORD-025`/`058`) + `ASN` (điểm xuất phát) |
| 3 | 🟡 **`SC-USR-017` chờ chạy cùng lô nhóm rule truy vết** | Cùng họ `SC-CNL-010` · `SC-ORD-065` · `SC-DLV-062`; app đã vi phạm nhóm này 1 lần | Chạy 4 SC cùng lô; cùng vỡ ⇒ **1 bug report cho nguyên nhân gốc**, ⛔ không log 4 bug rời (`RISK-USR-07`) |
| 4 | 🟡 **PRD chưa cập nhật các rule BA chốt ngoài PRD** (icon khiên · SĐT HRIS + định dạng · ô địa chỉ chọn văn phòng · điểm xuất phát OFFER · avatar/không badge · ← không hỏi) | BA 2026-09-17: *"PRD cập nhật sau"* — chưa có ngày | Khi nhận PRD bản sửa ⇒ `/analyze --update` đối chiếu lại; dev làm theo PRD cũ ⇒ log bug, dẫn câu trả lời BA |
