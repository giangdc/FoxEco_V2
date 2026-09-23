# CHANGELOG — Test Cases v1.1

> **TC Generation Log** — đích write-back của `generate-tc` (⛔ KHÔNG ghi vào version MEMORY `§4`/`§9` — router chỉ trỏ, không chứa nội dung).
> Cột `Review Status` do `review-tc` cập nhật sau; `generate-tc` ghi `⏳`.

## 1. TC Generation Log

| Ngày | Action | DOC ID | Module | Tổng TC | File output | Priority | Mode | Techniques | Review Status |
|---|---|---|---|--:|---|---|---|---|---|
| 2026-09-23 | REVISE | QC GiangDC2 — lượt 2 sau vibe-check demo bằng Playwright: `TC-DLV-031..036` Expected so theo NGHĨA (PRD §8.12.3 ô không ngoặc kép là mô tả, không phải nhãn nút); áp quyết định QC "chỉ người gửi đóng đơn trả hàng" vào `034/035/063`; ghi nợ "nhóm trạng thái đóng chưa có UI" vào `037..039/064/065/073` | DLV | 51 *(số lượng không đổi)* | `fragments/TC-DLV-v1.1.md` · `TC-MASTER-v1.1.xlsx` · `TC-MASTER-LATEST.xlsx` · `exports/ISC_FoxEco_v1.0_TestCase.xlsx` (sheet DLV, ô I8–I13) | P1:8, P2:28, P3:15 | standard | N/A | ⏳ |
| 2026-09-23 | REVISE | QC GiangDC2 — TC DLV khó đọc làm VR-020/021 chấm BLOCKED sai (`TC-DLV-043/050` nhấn "Huỷ" ở popup lớp 1). Chuẩn hoá cả 51 TC, chỉ sửa cột được phép theo §10.5: (1) Steps dùng đơn seed thay vì tạo đơn mới mỗi TC; ghi rõ 2 lớp popup lấy hàng / mở màn "Xác nhận đã giao" (lớp 1 nhấn "Xác nhận"); tên nút "Đã đến địa điểm giao hàng" kèm tên STG (BUG-044); đường tới "Xử lý đơn hàng" theo STG + FE-333 (QC chọn giữ Expected BA chốt `C-DLV-06`, log bug). (2) Viết lại seed: `SEED-DLV-03` → `03-A` (giao lại → trả hàng → RETURNED, 1 đơn theo thứ tự) + `03-B` (gửi quầy); thêm `SEED-DLV-06` (đơn Đã ghép cho 078/080/081); sửa gán sai `SEED-DLV-05`/đơn #4; bảng mã trạng thái ↔ nhãn. (3) Data cụ thể cho lịch hẹn (ngày mai · 09:00–10:00 · "Sảnh toà FPT Tower"); Expected 053/054–056/063/064/068–071 rõ oracle (chữ cảnh báo/"có ảnh bằng chứng" lấy từ demo, PRD không đặc tả — so theo nghĩa). (4) `TC-DLV-050` Pass → **Fail** (VR-021 chỉ tới bottom sheet, FE-333); `TC-DLV-078` bỏ proxy, Skipped → chạy được; `TC-DLV-040` gắn Deferred; `TC-DLV-032` bỏ vế "nhấn được" (062 phủ); `TC-DLV-077` đo 10 lần trên 1 đơn. ⚠ Demo 2026-09-23 lệch PRD ở nhãn nhóm trạng thái mới (031–039) và luồng RETURNED (063–065, 073) — giữ oracle PRD, ghi vào Notes. | DLV | 51 *(số lượng không đổi)* | `fragments/TC-DLV-v1.1.md` · `TC-MASTER-v1.1.xlsx` (sheet DLV + ALL + Seed) · `TC-MASTER-LATEST.xlsx` | P1:8, P2:28, P3:15 | standard | N/A | ⏳ |
| 2026-09-22 | REVISE | QC GiangDC2 chốt sau `VR-019` follow-up (`TC-TS-010/011/012`: sửa Expected theo cơ chế thật của Microsoft Forms — nút "Gửi" không disable, validate qua inline error "Câu hỏi này là bắt buộc." sau khi bấm; `TC-TS-012` giữ nguyên phần "SĐT sai định dạng vẫn phải bị chặn" vì đây là bug thật riêng — `BUG-041`. `BUG-040` xoá vì QC xác nhận cơ chế inline error không phải bug) | TS | 17 *(số lượng không đổi — §10.5)* | `fragments/TC-TS-v1.1.md` · `TC-MASTER-v1.1.xlsx` · `TC-MASTER-LATEST.xlsx` — sửa **Expected Result** của `TC-TS-010/011/012`; `Test Title` giữ nguyên (vẫn ghi "vô hiệu hoá" — xem nợ #30) | không đổi | standard | N/A | — |
| 2026-09-22 | REVISE | QC GiangDC2 chốt sau `VR-018` (`TC-CNL-017/018/019`: TC sai giả định nút "Yêu cầu hoàn hàng" — không có trong PRD, đối chiếu trực tiếp `AC-25.2.01`/`BR11-04`/`FR09`; `TC-CNL-009/010`: chấp nhận app ghi tên người thay vì vai trò ở dòng log huỷ — `BUG-033`/`BUG-035` xoá, `TC-CNL-009` vẫn FAIL vì nhãn hành động sai, giữ `BUG-034`) | CNL | 13 *(số lượng không đổi — §10.5)* | `fragments/TC-CNL-v1.1.md` · `TC-MASTER-v1.1.xlsx` · `TC-MASTER-LATEST.xlsx` — sửa **Expected Result/Notes** của `TC-CNL-009/010/017/018/019`; `Test Title` giữ nguyên | không đổi | standard | N/A | — |
| 2026-09-21 | REVISE | QC GiangDC2 chốt sau `VR-017` (tab `Hoạt động` rỗng không cuộn/không phản hồi vuốt là đúng — `BUG-032` xoá) | ACT | 10 *(số lượng không đổi — §10.5)* | `fragments/TC-ACT-v1.1.md` · `TC-MASTER-v1.1.xlsx` · `TC-MASTER-LATEST.xlsx` | không đổi | standard | N/A | — |
| 2026-09-21 | REVISE | QC GiangDC2 chốt sau `VR-017` (đơn "Đã huỷ" hiện ở tab "Đang diễn ra" là đúng — thay `C-ACT-04(b)` 2026-09-17) | ACT | 10 *(số lượng không đổi — §10.5)* | `fragments/TC-ACT-v1.1.md` · `TC-MASTER-v1.1.xlsx` · `TC-MASTER-LATEST.xlsx` | không đổi | standard | N/A | — |
| 2026-09-21 | REVISE | QC GiangDC2 recheck (trần thông báo khớp tuyến tính theo TÀI KHOẢN, không phải theo tuyến — BA đã xác nhận lại 2026-09-21 qua QC — thay `C-ASN-04(e)` cũ) | ASN | 13 *(số lượng không đổi — §10.5)* | `fragments/TC-ASN-v1.1.md` · `TC-MASTER-v1.1.xlsx` · `TC-MASTER-LATEST.xlsx` — sửa **Steps/Pre-condition/Expected/Test Data/Notes** của `TC-ASN-016` + `TC-ASN-025`; `Test Title` giữ nguyên | P1:2, P2:10, P3:1 | standard | N/A | ⏳ |
| 2026-09-18 | DESCOPE | QC GiangDC2 chốt (HRIS bắt buộc SĐT + địa chỉ làm việc) | USR | 38 *(36 chạy + **2 DESCOPED**)* | `fragments/TC-USR-v1.1.md` (+ §0.1 mới) · `TC-MASTER-v1.1.xlsx` · `TC-MASTER-LATEST.xlsx` | P1:3, P2:28, P3:5 *(mẫu số khi chạy)* | standard | N/A | `TC-USR-041` · `TC-USR-044` → Status `Skipped` · Lifecycle `DESCOPED`: nhánh (B) *"HRIS trống"* của `SC-USR-022`/`SC-USR-023` **không xảy ra trong thực tế**, không seed được data. **Σ TC-MASTER vẫn 223** (không xoá TC, giữ để truy vết) · drift fragment↔xlsx **0/38** · LATEST khớp md5. ✅ Không mất coverage `BR15-02` — vế *"SĐT rỗng ⇒ Lưu bị chặn"* phủ bởi `TC-USR-017` |
| 2026-09-17 | CONSOLIDATE | `review-tc` M-1 | **11/11 module** | 223 | `TC-MASTER-v1.1.xlsx` (+ sheet **`Seed`**) | P1:22, P2:145, P3:56 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-16 | GENERATE | DOC-v1.1-01 · DOC-v1.1-03 · DOC-v1.1-04 | USR | 29 | `fragments/TC-USR-v1.1.md` | P1:2, P2:23, P3:4 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | REVISE | DOC-v1.1-01 · DOC-v1.1-02 | USR | 29 | `fragments/TC-USR-v1.1.md` | P1:2, P2:23, P3:4 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-16 | REVISE | DOC-v1.1-01 · DOC-v1.1-02 · DOC-v1.1-04 | USR | 29 | `fragments/TC-USR-v1.1.md` | P1:2, P2:23, P3:4 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | REVISE | `Project_rule.md §Custom Rules §10.4` | USR | 38 | `fragments/TC-USR-v1.1.md` | P1:3, P2:30, P3:5 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | GENERATE | DOC-v1.1-01 | CNL | 13 | `fragments/TC-CNL-v1.1.md` | P1:4, P2:7, P3:2 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | GENERATE | DOC-v1.1-01 | GIFT | 8 | `fragments/TC-GIFT-v1.1.md` | P1:0, P2:6, P3:2 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | GENERATE | DOC-v1.1-01 | ASN | 13 | `fragments/TC-ASN-v1.1.md` | P1:2, P2:10, P3:1 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | GENERATE | DOC-v1.1-01 | NTF | 9 | `fragments/TC-NTF-v1.1.md` | P1:1, P2:7, P3:1 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | GENERATE | DOC-v1.1-04 | FEED | 5 | `fragments/TC-FEED-v1.1.md` | P1:0, P2:2, P3:3 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | REVISE | `testcase-guide.md §B.3` | GIFT | 8 | `fragments/TC-GIFT-v1.1.md` | P1:0, P2:6, P3:2 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | REVISE | BA trả lời `C-HOME-04` vòng 3 | FEED | 5 | `fragments/TC-FEED-v1.1.md` | P1:0, P2:2, P3:3 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | GENERATE | DOC-v1.1-01 · DOC-v1.1-03 | DLV | 51 | `fragments/TC-DLV-v1.1.md` | P1:8, P2:28, P3:15 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | GENERATE | DOC-v1.1-01 · DOC-v1.1-02 | ACT | 10 | `fragments/TC-ACT-v1.1.md` | P1:0, P2:6, P3:4 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | GENERATE | DOC-v1.1-01 · DOC-v1.1-03 | TS | 17 | `fragments/TC-TS-v1.1.md` | P1:2, P2:9, P3:6 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | GENERATE | DOC-v1.1-01 | HOME | 11 | `fragments/TC-HOME-v1.1.md` | P1:0, P2:3, P3:8 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | GENERATE | DOC-v1.1-01 · DOC-v1.1-03 | ORD | 48 | `fragments/TC-ORD-v1.1.md` | P1:2, P2:37, P3:9 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |
| 2026-09-17 | **CONSOLIDATE** | — | **11/11 module** | **223** | `TC-MASTER-v1.1.xlsx` | P1:22, P2:145, P3:56 | standard | N/A | ✅ **85/100 CONDITIONAL** · G1 PASS (recheck 2026-09-17, direct — điểm thô 100, cap 85) |

> **CONSOLIDATE 2026-09-17 — `TC-MASTER-v1.1.xlsx` (223 TC · 13 sheet).** Gộp 11 fragment `.md` → Overview + ALL (phẳng
> canonical, sort Module→Priority→TC ID) + 11 sheet/module (gom nhóm theo REQ, có dòng section `▬▬`; `TS`/`USR` gom theo
> chức năng con vì 1 REQ ôm quá nhiều TC). Validate: **0 trùng ID** · 444 ô đã convert `<br>` → xuống dòng thật · 0 ô còn
> sót `<br>` · Σ 11 sheet module = 223 = ALL. `TC-USR-v1.1-ID-MAPPING.md` **bị bỏ qua đúng** (không có `fragment-meta`,
> là file mapping chứ không phải fragment).
>
> 🔴 **KHÔNG gộp CARRIED — QC GiangDC2 chốt 2026-09-17.** File chỉ chứa TC của **140 SC NEW+MODIFIED**. Hệ quả phải nhớ:
> **163 TC CARRIED của v1.1 nằm ở `TC-MASTER-v1.0.xlsx`** ⇒ execute/vibe-test/test-report phải mở **SONG SONG 2 file** mới
> phủ đủ 302 SC của v1.1; mở mỗi file v1.1 là **hụt 163 TC**. Đã ghi cảnh báo này vào sheet `Overview` (2 dòng ⚠️/🔴) để
> người mở file thấy ngay, không phải tra CHANGELOG.
>
> ⚠️ **54 TC ID tồn tại ở CẢ 2 file** (SC MODIFIED giữ ID v1.0) — **LUÔN lấy bản v1.1**. Trong đó **5 TC có kỳ vọng NGƯỢC
> nhau** giữa 2 bản: `TC-ACT-008` (chuỗi lý do Hết hạn dài⟷ngắn) · `TC-ACT-013` (★ leftover: ghi nhận⟷defect) ·
> `TC-ACT-014` (empty state: chỉ đếm card⟷assert verbatim + ẩn khối lịch sử) · `TC-USR-003`/`TC-USR-008` (ràng buộc §2.2).
> Chạy nhầm bản v1.0 ⇒ verdict ngược hoàn toàn.
>
> ✅ **Đã GỠ `TC-HOME-010` + `TC-HOME-024`** khỏi bộ (nợ #16 đóng) — verify lại: 2 ID này **không lọt** vào TC-MASTER-v1.1.
> ⚠️ Nhưng chúng **vẫn sống trong `TC-MASTER-v1.0.xlsx`** ⇒ ⛔ **không chạy 2 TC đó** khi mở file v1.0 lấy TC CARRIED.
> 2 ID bỏ trống **VĨNH VIỄN**, không tái sử dụng.
>
> ℹ️ **Số trống trong dải ID mỗi module là BÌNH THƯỜNG** — đó là TC CARRIED đang sống ở fragment v1.0, ⛔ không phải lỗ ID.
> Lỗ ID thật chỉ có 2 cái ở `HOME` và đã khai đúng theo `testcase-guide.md §A.2` chiến lược (a).
> `TC-MASTER-LATEST.xlsx` nay trỏ **v1.1**.

> **GENERATE 2026-09-17 (`ORD`) — MODULE CUỐI, ĐỦ 11/11:** scope = **26 SC** (14 dòng `SC-ORD-052..065` gồm `SC-ORD-059`
> lifecycle MODIFIED · + 12 SC MODIFIED giữ ID v1.0) → **48 TC**. 14 TC giữ ID v1.0; 34 TC NEW → `TC-ORD-055..088` liên tục.
> Áp `§10.4` ngay từ đầu. Không gỡ TC nào.
>
> 🔴 **BẪY ID — `TC-ORD` LỆCH PHA với `SC-ORD` từ `SC-ORD-040` trở đi.** v1.0 có **54 TC cho 51 SC** (3 SC fan-out 2 TC)
> ⇒ ⛔ **KHÔNG suy TC ID từ SC ID**; bảng map 12 SC MODIFIED khai ở header fragment §0.1. Hệ quả cụ thể: `SC-ORD-054`
> (ảnh bắt buộc, **P1**) là SC NEW nhưng **KHÔNG** lấy ID `TC-ORD-054` (đã thuộc `SC-ORD-051` ở v1.0) — nhận `TC-ORD-063`.
>
> 🔑 **Oracle Bước 1/3 — LẤY UI LÀM CHUẨN, ⛔ KHÔNG theo PRD `§8.1.4`** (`C-ORD-18` Resolved 2026-09-17, BA *"Theo UI nhé"*):
> nhãn **"Trọng lượng"** (PRD "Khối lượng" **hết hiệu lực**) · kiểu control **chip** (PRD "Dropdown" **hết hiệu lực**) ⇒ Steps
> viết *"nhấn chip"*, quét lại fragment **0 chỗ còn chữ "dropdown"** · mốc tiền `Dưới 1 triệu đ`/`1 – 5 triệu đ`/`Trên 5 triệu đ`
> là **con số chính thức**. App hiện theo PRD ⇒ **defect UI**, ⛔ không phải TC sai. `TC-ORD-064` bỏ rào *"ghi nhận nhãn,
> không FAIL vì tên nhãn"* → **assert cứng**.
>
> 🔑 **5 oracle khác đã chốt, áp thẳng:** `C-ORD-09` nhãn **"Tài liệu"** (ràng buộc cũ *"không dùng nhãn Tài liệu"* **hết hiệu
> lực** — `TC-ORD-005` nay FAIL nếu app hiện "Giấy tờ, hồ sơ") · `C-ORD-04` chip "Thuốc/Y tế" **giữ, không chặn**, banner hàng
> cấm **không có ở v1.1** ⇒ ⛔ không assert · `C-ORD-14` **ĐẢO `BR01-09`/`AC-04.1.02`**: email không tra thấy HRIS ⇒ nút
> "Tiếp theo" **DISABLE**, ⛔ KHÔNG mở ô nhập tay (`TC-ORD-075/076`) · tên miền hợp lệ **chỉ `@fpt.com`**, `@gmail.com` nay là
> **data INVALID** (`TC-ORD-078`), ⛔ `@fpt.vn` chưa xác nhận lại · `C-ORD-15` Từ X → Đến tối đa **X+7**, app **chặn buổi đã
> qua trong ngày** (`TC-ORD-059` — rule **không có trong PRD**, chưa SC nào phủ trước lượt này), `EXPIRED` do **job cuối ngày**
> (đưa vào setup của `TC-ORD-048` để người chạy không kiểm quá sớm) · `C-ORD-17` **không có chức năng "gỡ"** tin hết hạn.
>
> ⚠️ **5 nợ khai rõ ở header §0.4, không giấu:** (1) **mốc tiền + vị trí/tính nhập được của block Ghi chú** nay assert cứng
> được nhưng **chưa có TC** — thuộc `SC-ORD-008/009/010/011` là **CARRIED**, ngoài `id_range` delta, `Project_rule` cấm sửa
> file v1.0 ⇒ nợ ở `v1.1/ORD-dang-tin/CHANGELOG.md §3` #7. (2) **email mẫu người đã nghỉ việc** chưa có ⇒ `TC-ORD-076` ghi
> `Blocked`, ⛔ không PASS. (3) nút "Tiếp theo" cam khi chưa đủ điều kiện — **QA tự vibe-check**, ⛔ không log bug theo ảnh tĩnh.
> (4) `SC-ORD-041` vế *"mở link trực tiếp"* không có đường thử trên mobile ⇒ ⛔ **không PASS chỉ vì không thử được**.
> (5) `SC-ORD-044` vế *"request sửa bị từ chối"* là backend, `TC-ORD-047` chỉ assert nút không hiển thị.
>
> 🔗 **`SEED-ORD-01` (bộ ảnh mẫu) chuẩn bị 1 lần dùng chung 3 module** `ORD`/`DLV`/`TS` — `BR18-01` áp cùng trần, ⛔ đừng
> chuẩn bị 3 bộ. Đơn `EXPIRED` (`TC-ORD-048/061`) ⛔ không seed được qua UI — gộp kế hoạch seed thời gian với `TC-DLV-057`/`067`,
> `TC-ACT-008`, `TC-HOME-030`, `SC-TS-006`. ⛔ Không hardcode ngày/giờ — chọn tương đối so với hiện tại.
> CARRIED (39 SC) dùng lại TC v1.0, không chép sang fragment này.

> **GENERATE 2026-09-17 (`HOME`):** scope = **6 SC NEW** (`SC-HOME-025..030`) + **3 SC MODIFIED** (`SC-HOME-008/019/021`)
> + **2 SC DEPRECATED** → **11 TC**. 3 TC MODIFIED giữ ID v1.0; 8 TC NEW → `TC-HOME-025..032`. Áp `§10.4` ngay từ đầu.
>
> 🔴 **LƯỢT ĐẦU TIÊN CỦA DỰ ÁN PHẢI GỠ TC — chiến lược ID (a) "ĐỂ LỖ", ID KHÔNG tái sử dụng** (`testcase-guide.md §A.2`):
> `TC-HOME-010` (SC assert *"Trang chủ KHÔNG có section 'Đơn của tôi'"* — `C-HOME-05` Resolved 2026-09-17 chốt **NGƯỢC HẲN**:
> HIỆN empty state `EMP-02`) và `TC-HOME-024` (SC gộp mọi empty state vào 1 dòng, nay tách thành 3 SC atomic
> `SC-HOME-025/026/027`). Chọn **(a) để lỗ** thay vì renumber vì bộ v1.0 **đã phát hành** — `11_tc-review/review-report-v1.0.md`
> và `TC-MASTER-v1.0.xlsx` (219 TC) đều trích ID này. ⇒ **`TC-HOME-010` và `TC-HOME-024` bỏ trống VĨNH VIỄN**, dải NEW bắt
> đầu từ `TC-HOME-025`, ⛔ không lấp vào 2 lỗ. Sau consolidate module `HOME` có **33 TC** (24 − 2 + 11), chạy tới `TC-HOME-032`
> với 2 lỗ tại `010`/`024`. 🔑 **Consolidate PHẢI gỡ 2 TC này khỏi TC-MASTER** — bỏ sót là còn 2 TC kỳ vọng ngược nhau trong bộ.
>
> 📐 **9 SC ra 11 TC:** `SC-HOME-019` tách 2 (**đếm đúng 5 tin** ⟷ **3 lớp loại trừ** — app có thể trả đủ 5 nhưng lẫn tin đã
> ghép) · `SC-HOME-021` tách 2 (cặp biên **đúng 5 ẩn nút** ⟷ **>5 hiện nút**) · `SC-HOME-008` **giữ 1** vì hero + dòng cộng đồng
> + vắng CO₂/ECO cùng 1 trạng thái tĩnh (`§10.4` mục 1), vế *"x toàn hệ thống"* verify ở `TC-HOME-031` bằng phép đo tăng.
>
> 🔑 **Áp 4 CL đã đóng:** `C-HOME-03` (**đúng 5 tin**, siết từ *"nhiều nhất 5"* của v1.0 — app từng hiện đúng 1 tin mà vẫn PASS
> theo bản cũ) · `C-HOME-04` (tin load **toàn quốc**, nhưng chuỗi `EMP-01` **giữ nguyên chữ PRD** *"…trong khu vực của bạn"*
> theo BA ⇒ assert cứng chuỗi cũ dù chữ không còn khớp hành vi) · `C-HOME-05` (HIỆN `EMP-02`, ảnh demo `HOME_03` nay là
> **lệch demo ↔ rule**, ⛔ không còn là oracle) · `C-HOME-06` (hero = đơn Hoàn thành ở vai **người vận chuyển**; x toàn hệ thống,
> **realtime**; ⛔ **không assert y** — BA đề nghị bỏ qua định nghĩa "người tham gia").
>
> ⚠️ **PHÁT HIỆN MỚI khi viết TC — 2 TC không dựng được trên STG dùng chung:** `C-HOME-04` chốt tin load **toàn quốc** nên mọi
> TC cần *"cả hệ thống có ≤N tin hợp lệ"* phải dọn dữ liệu **toàn STG**. `test_data_catalog.md` mới chỉ cảnh báo cho `SC-HOME-025`
> (`EMP-01`); **`SC-HOME-021` nhánh ẩn nút (`TC-HOME-025`) dính cùng ràng buộc nhưng catalog chưa ghi** — ghi nợ để
> `analyze-requirements` bổ sung. Không có môi trường riêng ⇒ ghi **`Blocked` kèm lý do**, ⛔ KHÔNG đánh PASS cho xong.
> ✅ Ngược lại `TC-HOME-030` (3 lớp loại trừ) **dựng được bình thường** — chỉ cần chứng minh 3 tin CỤ THỂ vắng mặt.
>
> ⚠️ **1 TC `Deferred`** — `TC-HOME-032` (`NFR01` <2s p95 @1.000 user đồng thời) cần công cụ load-test, ⛔ không test tay.
> Viết TC để giữ traceability cho `NFR01` thay vì bỏ hẳn SC (`test_data_catalog §HOME` ghi rõ *"không viết TC manual assert số đo"*),
> loại khỏi mẫu số pass-rate. 🔗 **Tài khoản "sạch" `SEED-HOME-01` dùng chung với `ACT` (`SEED-ACT-02`) và `GIFT`
> (`SC-GIFT-008`)** — xin 1 tài khoản mới tinh, chạy hết cụm empty state của cả 3 module trong 1 lượt.
> CARRIED (19 SC) dùng lại TC v1.0, không chép sang fragment này.

> **GENERATE 2026-09-17 (`TS`):** scope NEW = **8 SC** (`SC-TS-008..015`), 0 MODIFIED → **17 TC** (`TC-TS-008..024`,
> nối tiếp ID cao nhất v1.0 là `TC-TS-007`, dải liên tục). Toàn bộ gắn 1 REQ mới `REQ-TS-006` — `FR16` "Báo cáo sự cố &
> hỗ trợ" là **tính năng hoàn toàn mới**, v1.0 module này là log-only không có form nhập. Áp `§10.4` ngay từ đầu.
> Fan-out: `SC-TS-009` → 3 TC (3 nhánh OR của điều kiện bắt buộc) · `SC-TS-015` → 4 TC · `SC-TS-008/011/012/013` → 2 TC
> mỗi SC · `SC-TS-010/014` giữ 1-1. Không gỡ TC nào.
>
> 🔴 **2 SC có Then ĐÃ LỖI THỜI — TC viết theo bản Resolved, NGƯỢC scenario map** (`testcase-guide.md §B.4.4`, cùng cách
> `ASN`/`NTF`/`FEED` đã làm). `test_scenario_map.md` viết 2026-09-15, `C-TS-03` đóng hẳn 2026-09-17 và đảo 2 kết luận:
> (1) **`SC-TS-008`** — scenario map theo `AC-31.1.01` ghi **9 trường prefill**; bản Resolved: form prefill **ĐÚNG 1 trường
> "Mã đơn hàng"** kèm ghi chú *"Tự động điền từ ứng dụng"*, ba ô Loại yêu cầu / Mô tả / SĐT đều **TRỐNG** ⇒ `BR16-02` đúng,
> **`AC-31.1.01` là PRD sai/thừa**. (2) **`SC-TS-014`** — scenario map theo `BR16-03` ghi *"trường prefill CHO PHÉP sửa"*;
> bản Resolved: ô "Mã đơn hàng" là **nhãn tĩnh, KHÔNG phải textbox, KHÔNG sửa được** ⇒ `§8.16.2` đúng, **`BR16-03` là PRD sai**.
> ⚠️ **Nợ:** `test_scenario_map.md` của `TS` **chưa write-back** 2 kết luận này (`risk_assessment.md` đã có đủ) — reviewer đọc
> scenario map sẽ tưởng TC viết sai. Đồng bộ ở lượt `analyze-requirements`/`health-check` kế tiếp.
>
> 🔑 **3 oracle khác đã chốt, áp thẳng:** (a) `C-TS-02(a)` — nút "Báo cáo sự cố" hiện ở **MỌI trạng thái** (Chờ ghép · Đã ghép ·
> Đang giao) và **MỌI vai**, ⛔ KHÔNG giới hạn `IN_TRANSIT`/`DELIVERED` như `§8.12.3` liệt kê (`AC-31.1.01` đúng, `§8.12.3`
> là PRD thiếu) ⇒ `TC-TS-022/023/024`. (b) `C-TS-02(b)(c)` — gửi form **KHÔNG làm đơn đổi trạng thái**; `§8.12.2` định nghĩa
> `INCIDENT` = *"có báo cáo sự cố sau khi đơn đã sang IN_TRANSIT"* đọc được là tự chuyển, nên sinh hẳn `TC-TS-020` làm oracle
> chặn cách đọc sai đó — đây cũng là căn cứ để `SC-CNL-015`/`SC-DLV-034` **out of scope test qua UI**. (c) `C-TS-03(c)` Dev
> trả lời *"App hiển thị nhé"* — nút "Thử lại" khi mất mạng do **CHÍNH APP** vẽ ⇒ `TC-TS-016` assert được dù `BR16-01` dùng
> Custom Tabs; ⛔ không assert công nghệ nhúng cụ thể (không quan sát được từ UI).
>
> ✅ **Độ tin cậy oracle cao nhất trong các module lượt này** — `TS` là module **duy nhất verify được TOÀN BỘ happy path +
> boundary end-to-end qua demo** (ô "Thêm ảnh" hoạt động thật, không bị chặn như `DLV`): ảnh `TS_03` (đủ 5 ảnh → nút "Thêm ảnh
> khác" tự disable) · `TS_04` (đủ 3 trường → nút "Gửi" enable) · `TS_05` (màn "Đã ghi nhận phản hồi" + câu 24 giờ verbatim).
> ⇒ TC assert cứng, ⛔ **không cần dự phòng "app chưa cập nhật"** như `RISK-DLV-08`/`RISK-DLV-11`.
>
> ⛔ **Ngoài phạm vi, không viết TC:** xử lý phía Admin (*"liên hệ lại trong 24 giờ làm việc"*, *"đối chiếu MNV"* là quy trình
> ngoài app — chỉ assert **cam kết hiển thị trên UI** ở `TC-TS-009`) · trạng thái `INCIDENT` (không vào được qua UI).
> 🔗 **Seed `SEED-TS-01` tái dùng thẳng đơn #1 của `SEED-DLV-02` tại checkpoint CP2** — chạy cụm `TS` **TRƯỚC** `TC-DLV-043`
> vì TC đó đẩy đơn sang "Đã giao". CARRIED (7 SC) dùng lại TC v1.0, không chép sang fragment này.

> **GENERATE 2026-09-17 (`ACT`):** scope NEW + MODIFIED = **9 SC** (`SC-ACT-015/016/017` NEW · `SC-ACT-001/005/008/012/013/014`
> MODIFIED) → **10 TC**. 6 TC MODIFIED giữ nguyên ID v1.0 (map SC↔TC 1-1 sạch); 4 TC NEW nối tiếp `TC-ACT-014` → `TC-ACT-015..018`.
> Áp `§10.4` ngay từ đầu. Không gỡ TC nào ⇒ không lỗ ID (số trống trong fragment là TC CARRIED sống ở fragment v1.0).
>
> 📐 **9 SC ra 10 TC, KHÔNG phải 12 — khai tường minh ở header §0.1 để `review-tc` không đọc nhầm là bỏ sót:**
> `SC-ACT-015` **cố ý không tách 2** dù Then có 2 vế — giá trị của SC nằm ở **phép đối chứng** `RETURNED` hiện ⟷ `CANCELLED` ẩn,
> tách rời là mất đúng thứ nó sinh ra để bắt (`risk_assessment.md` Khuyến nghị #3 + `test_data_catalog.md` *"⛔ không seed lẻ"*);
> hai đơn xem cùng 1 lượt trên cùng trạng thái tĩnh ⇒ gộp theo `§10.4` mục 1. `SC-ACT-005` **giữ 1 TC** vì 2/3 vế Then đã có home
> ở TC khác cùng lô (`TC-ACT-008` chuỗi lý do "Hết hạn" · `TC-ACT-015` lý do hoàn hàng) — không nhân bản assert, **không mất
> coverage** (`§10.4` mục 3). Ngược lại `SC-ACT-016` **tách 2** vì che-thanh-tab-dưới và khoá-cuộn fail độc lập (`§10.4` mục 2).
>
> 🔑 **Áp 3 CL đã đóng, 2 trong đó ĐẢO hướng đọc PRD:** (1) `C-ACT-02` Resolved 2026-09-16 — nhãn **theo app**
> (màn "Đơn của tôi" · tab "Đang diễn ra"/"Đã hoàn thành" · nav "Hoạt động"); PRD ghi "Đang chạy"/"Hoàn tất" ở **3 chỗ độc lập**
> là **PRD chưa cập nhật**, ⛔ KHÔNG phải defect app. (2) `C-ACT-04(b)` Resolved 2026-09-17 — đơn **"Đã huỷ" vẫn ẨN khỏi cả 2 tab**,
> rule v1.0 CÒN HIỆU LỰC; `§8.12.3` cho mọi vai *"Xem lý do"* đơn huỷ là PRD chưa cập nhật ⇒ `TC-ACT-015` assert ẩn, đơn hiện ra
> thì log bug. (3) `C-ACT-04(a)` — `RESCHEDULED`/`RETURNING`/`INCIDENT` → tab "Đang diễn ra"; `RETURNED`/`EXPIRED` → "Đã hoàn thành".
>
> 🔴 **3 TC ĐẢO/SIẾT kỳ vọng so với bản v1.0 CÙNG ID — consolidate/execute phải lấy bản v1.1:** `TC-ACT-008` chuỗi lý do "Hết hạn"
> đổi sang bản **ngắn** *"Không có ai nhận mang giúp trong thời gian đăng"* (PRD v1.1 `§8.5.1 BR05-03` + `AC-09.1.01` gọi tên chuỗi
> lần đầu ⇒ thắng bản dài của `KB-ORD-07` #4 mà v1.0 đang assert) · `TC-ACT-013` từ *"nhấn vào ★ không mở màn chấm điểm"* siết thành
> **sự tồn tại của ★/điểm/tier/chỉ số môi trường đã là defect phải log bug** · `TC-ACT-014` từ *"không có card nào"* siết thành
> assert verbatim `EMP-06` + **KHÔNG CTA** + **ẩn hẳn khối lịch sử**. `TC-ACT-012` cũng siết theo `EMP-05` nhưng không đảo hướng.
>
> ⚠️ **Mâu thuẫn BA đã biết, KHÔNG chạm TC lượt này:** `C-ACT-03(c)` nói tin **Hết hạn không cho tương tác** ⟷ `C-ORD-17` nói card
> Hết hạn **có "Xem lý do/đăng lại"**. `TC-ACT-008` cố ý **chỉ đọc card, không tap** (giữ cách v1.0) nên không dính; SC về đích tap
> card (`SC-ACT-009/010/011`) là CARRIED, không regenerate ⇒ để `analyze-requirements` đối chiếu lại với BA trước khi đụng tới.
>
> 🔗 **Phụ thuộc lô `DLV`:** `SEED-ACT-03` ⛔ KHÔNG dựng đơn `RETURNED` riêng mà tái dùng thẳng đơn của `SEED-DLV-03`
> (đã đẩy tới trạng thái này qua `TC-DLV-063`). Lô `DLV` BLOCKED ⇒ `TC-ACT-015` BLOCKED và `TC-ACT-005` chỉ chạy được phần
> `COMPLETED` + `EXPIRED`. Đơn `EXPIRED` ⛔ không seed được qua UI — gộp kế hoạch seed thời gian với `TC-DLV-057`/`067` + `SC-TS-006`.
> **Tài khoản trắng `SEED-ACT-02` là tài nguyên khan hiếm nhất lượt này** — dùng chung với `HOME` (`SC-HOME-025..027`) và
> `GIFT` (`SC-GIFT-008`), chạy hết cụm empty state của cả 3 module trong 1 lượt. CARRIED (8 SC) dùng lại TC v1.0, không chép sang.

> **GENERATE 2026-09-17 (`DLV`):** scope NEW = **34 SC** (`SC-DLV-031..064`), 0 MODIFIED → **51 TC** (`TC-DLV-031..081`,
> nối tiếp ID cao nhất v1.0 là `TC-DLV-030`). Áp `Project_rule.md §Custom Rules §10.4` ngay từ đầu — **1 dòng Expected/TC
> neo step cuối**, không cần renumber sau. Fan-out chỉ ở SC có nhiều điểm fail độc lập: 3 SC ma trận trạng thái ×3 vai
> (`SC-DLV-031/032/033` → 9 TC), `SC-DLV-047` ×3 vai, `SC-DLV-049` → 4 TC (2 nhãn chế độ + 2 cặp biên ngày/giờ),
> 6 mẫu câu nhật ký `SC-DLV-055/056/057` → 6 TC, `SC-DLV-052` → 2 TC (bước tặng quà ⟷ chỉ số "Đơn đã giúp" là 2 bề mặt
> fail độc lập), `SC-DLV-039/059/064` → 2 TC mỗi SC.
>
> 🔴 **1 SC DESCOPED, 0 TC — `SC-DLV-060`** (admin can thiệp được ghi log): BA 2026-09-17 chốt **mọi bề mặt role admin
> OUT OF SCOPE v1.1**, và Then của SC chỉ còn vế "GHI NHẬN" — không có oracle PASS/FAIL, `testcase-guide.md §B.4.4` cấm
> TC dạng ghi-nhận. Khai ở header fragment §0.1. Không gỡ TC nào ⇒ **không phát sinh lỗ ID**, dải `031..081` liên tục.
>
> 🔑 **Áp 2 CL vừa đóng, ĐẢO oracle so với PRD:** (1) `C-DLV-06` Resolved 2026-09-17 — luồng "không liên lạc được" là
> chuỗi **4 tầng** (màn "Xác nhận đã giao" → màn "Liên hệ người gửi" → modal "Chưa liên lạc được?" → màn "Xử lý đơn hàng")
> với thứ tự **"Gửi tại chốt bảo vệ" → "Gửi tại quầy lễ tân" → "Cầm hàng về"**, NGƯỢC `BR08-02` (lễ tân trước, 1 danh sách
> 4 bước) ⇒ `TC-DLV-050` assert theo bản demo BA đã xác nhận, ⛔ không theo `BR08-02`. (2) `C-DLV-05` Resolved 2026-09-17 —
> **Carrier tự bấm** "Giao lại theo lịch" (không phải hệ thống tự chuyển như `AC-18.1.01`), không gate theo giờ, không giới
> hạn số lần hẹn, và **timeline giữ đúng 5 mốc cố định** với "Đang giao" active xuyên suốt ⇒ `TC-DLV-031..036` ⛔ không FAIL
> vì thiếu mốc mới trên thanh tiến trình.
>
> ⛔ **Không assert (out of scope v1.1, role admin chưa build — `C-DLV-07`/`C-DLV-08(d)`):** vế "chuyển admin hỗ trợ"
> (`AC-23.2.01`/`BR08-06`/`BR09-04`) và hạn giữ hàng tại quầy 4h/24h — **không log bug** khi không thấy. `TC-DLV-057`/`067`
> chỉ còn assert *"có gửi thông báo nhắc"* + *"đơn KHÔNG tự đóng"*; không assert giờ cụ thể của "cuối ngày", không FAIL vì
> kênh push hay in-app.
>
> 🟡 **Nợ oracle — `C-DLV-08` (a)(b) còn Partially:** `TC-DLV-045/046/052` **chưa assert** cờ "không liên lạc được" và
> `NTF-05` ⟷ `NTF-11` cho đường chọn quầy trực tiếp. Chỉ assert phần đã chốt (2 ô quầy bắt buộc · đơn sang "Đã giao" ·
> dòng log verbatim). BA đã chỉ chỗ tự đọc ở block "LỊCH SỬ" ⇒ **không hỏi BA nữa**, QA vibe-check rồi mở
> `analyze-requirements --module DLV` chính thức hoá trước khi siết 3 TC này.
>
> 🔴 **`TC-DLV-078` dự kiến FAIL có chủ đích** (`RISK-DLV-09`) — bug audit đã biết `RISK-TS-01` (huỷ nhận đơn xoá dòng
> "Ghép thành công") vi phạm trực tiếp `NFR-07` log append-only. FAIL ⇒ log bug, ⛔ không hạ Expected theo hành vi hiện tại.
>
> ⚠️ **2 TC `Deferred`** (`TC-DLV-057` mốc 4h/cuối ngày · `TC-DLV-067` quá hẹn 24h) — cần dev/QA lùi timestamp, chạy chung
> lô với `TC-DLV-024` (v1.0) và `SC-TS-006`. **4 TC cần proxy ngoài app** (`TC-DLV-074/075/076/078`) — module `DLV` là **UI**
> (không có API spec/HTTP Status Contract trong dự án) nên Expected vẫn là hành vi quan sát được trên màn, ⛔ không viết
> `HTTP status:`. CARRIED (30 SC) dùng lại TC v1.0, không chép sang fragment v1.1.

> **REVISE 2026-09-17 (`GIFT`, sửa theo phản hồi QC):** 4 TC (`TC-GIFT-002/003/011/013`) có step 1 gộp 2-3 thao tác
> vào 1 dòng mơ hồ ("mở đơn Hoàn thành đó từ tab 'Hoạt động' và nhấn...") — vi phạm `§B.3` "1 step = 1 tương tác
> quan sát được" + "Steps phải TỰ ĐỦ", khiến người chạy/AI vibe-test không biết mở đơn ở màn nào, tap card nào.
> Tách lại thành các step riêng (điều hướng tab con → tap card mở Theo dõi đơn → nhấn CTA), khớp đúng pattern
> `TC-GIFT-001` gốc ở v1.0 mà lúc regenerate đã lỡ condense mất. Không đổi Expected/assertion, chỉ đổi Steps +
> dịch số neo Expected theo step cuối mới (`§10.4`). Số TC/priority không đổi.

> **REVISE 2026-09-17 (`FEED`, áp câu trả lời BA `C-HOME-04` vòng 3):** BA trả lời *"giữ nguyên nhé"* cho câu
> cuối cùng còn treo của `C-HOME-04` ⇒ chuỗi empty state `EMP-04` **giữ nguyên chữ PRD** dù Bảng tin load tin
> **toàn quốc**. `TC-FEED-013` bỏ rào *"chưa assert câu gợi ý mở rộng khu vực"* → Expected thêm assert câu
> **gợi ý mở rộng khu vực hoặc đăng tin**. Chỉ sửa Expected + Notes của 1 TC; số TC/priority không đổi.

> **GENERATE 2026-09-17 (`FEED`):** ⚠️ Ngoại lệ kiến trúc — module không có thư mục `v1.1/`, thay đổi sửa tại
> chỗ trong `02_analyze-requirements/v1.0/FEED-bang-tin/` (10/11 module có v1.1 riêng, FEED thì không — xem
> `v1.1/MEMORY.md`). 4 SC đổi Then (`SC-FEED-002/007/009/013`) → 4 TC MODIFIED giữ ID v1.0; 1 SC hoàn toàn mới
> (`SC-FEED-015`) → 1 TC NEW nối tiếp ID cao nhất v1.0 (`TC-FEED-014`) → `TC-FEED-015`. Điểm đảo lớn nhất:
> `TC-FEED-009` đảo từ "placeholder tĩnh" sang "CÓ bản đồ thật, ảnh tĩnh vẽ tuyến" (`C-FEED-01(b)`/`C-FEED-02(c)`
> Resolved). 10 SC không đổi dùng lại TC v1.0 nguyên trạng, gồm 2 bug P1 đã biết chưa log (`TC-FEED-010/011`).
> Áp thẳng bản Resolved của `C-FEED-01..05` dù `CHANGELOG.md §3`/`risk_assessment.md` gốc của FEED chưa kịp
> write-back đầy đủ. Không gỡ TC nào.

> **GENERATE 2026-09-17 (`NTF`):** scope NEW + MODIFIED = 9 SC (`SC-NTF-017..022` NEW · `SC-NTF-005/008/014`
> MODIFIED) → **9 TC** (1-1, không fan-out). 3 TC MODIFIED giữ ID v1.0 (`TC-NTF-005/008/014`); 6 TC NEW nối tiếp
> từ ID cao nhất đã dùng ở v1.0 (`TC-NTF-016`) → dải mới `TC-NTF-017..022`. Áp thẳng 2 kết luận BA vừa Resolved
> 2026-09-17 (`C-NTF-04` đích điều hướng = "Theo dõi đơn" cho mọi loại · `C-NTF-05` người nhận ở 3 sự kiện mơ hồ) —
> `CHANGELOG.md`/`risk_assessment.md` gốc của `02_analyze-requirements/v1.1/NTF-thong-bao/` chưa kịp write-back.
> `TC-NTF-006`/`010` (CARRIED, bị `C-NTF-05`/`C-NTF-04` chạm tới nhưng KHÔNG nằm trong `id_range` MODIFIED chính
> thức) **không sửa** ở lượt này — ghi nợ cho `analyze-requirements` chính thức hoá lại nếu cần. Toàn bộ
> `TC-NTF-017..022` + phần mở rộng của `TC-NTF-008`/`014` **phụ thuộc hoàn toàn nhánh FR08/FR09 bên `DLV`**
> (`SC-DLV-038/039/044/049`) — `DLV` **chưa có fragment TC v1.1**, Pre-condition tạm mô tả trực tiếp hành động,
> sẽ đổi sang tham chiếu TC-DLV khi module đó generate xong; chạy chung lô vibe-test với `DLV` (`RISK-NTF-07`).
> CARRIED (13 SC) dùng lại TC v1.0, không chép sang fragment v1.1. Không gỡ TC nào.

> **GENERATE 2026-09-17 (`ASN`):** scope NEW + MODIFIED = 6 SC (`SC-ASN-019` NEW · `SC-ASN-006/008/011/014/015`
> MODIFIED) → **13 TC** (SC fan-out nhiều TC vì chính SC liệt kê nhiều nhánh: `SC-ASN-006` 2 TC, `SC-ASN-011` 4 TC,
> `SC-ASN-014` 4 TC). 8 TC MODIFIED giữ ID v1.0 (`TC-ASN-006/008/011/012/015/016/017/018`); 5 TC NEW nối tiếp từ ID
> cao nhất đã dùng ở v1.0 (`TC-ASN-021`) → dải mới `TC-ASN-022..026`. Áp đủ 3 kết luận BA vừa Resolved 2026-09-17
> (`C-ASN-04` rule 5 thông báo/tuyến độc lập · `C-ASN-05` so khớp địa chỉ chính xác · `C-ASN-06` câu thông báo lấy
> từ 15 danh mục có sẵn) — 2 file `CHANGELOG.md`/`risk_assessment.md` gốc của `02_analyze-requirements/v1.1/ASN-ghep-noi/`
> chưa kịp write-back các dòng cũ ghi "Open", generate-tc đã áp thẳng bản Resolved. Quyết định KHÔNG gộp
> `SC-ASN-013` (CARRIED) với `SC-ASN-014` (MODIFIED) dù cùng thuật toán chọn-5 — giữ tách vì 2 bề mặt (gợi ý vs
> thông báo) có thể FAIL độc lập; nêu rõ trong header fragment để review-tc cân nhắc lại nếu cần. `TC-ASN-024`
> (concurrency `NFR-06`) và `TC-ASN-026` (API security `NFR-11`) cần công cụ ngoài UI (load tool/Postman), không
> chạy manual thuần. CARRIED (13 SC) dùng lại TC v1.0, không chép sang fragment v1.1. Không gỡ TC nào.

> **GENERATE 2026-09-17 (`GIFT`):** scope NEW + MODIFIED = 8 SC (`SC-GIFT-013/014` NEW · `SC-GIFT-002/003/006/007/008/011`
> MODIFIED) → **8 TC**, áp `Project_rule.md §Custom Rules §10.4` ngay từ đầu. 6 TC MODIFIED giữ ID v1.0
> (`TC-GIFT-002/003/006/007/008/011`); 2 TC NEW nối tiếp từ ID cao nhất đã dùng ở v1.0 (`TC-GIFT-012`) → dải mới
> `TC-GIFT-013/014`. `TC-GIFT-007` nâng Priority P3→P2 (hết `[GAP]` của `C-GIFT-03`). `TC-GIFT-011` đổi seed riêng
> (`SEED-GIFT-06`, tiêu đơn) để mở rộng phạm vi rà đủ 4 bề mặt theo `BR14-03` (v1.0 chỉ rà 3 bề mặt, dùng chung
> `SEED-GIFT-01`). `TC-GIFT-013`/`014` phụ thuộc nhánh `RETURNED` của `DLV` (`FR09`) — có thể BLOCKED nếu STG
> chưa build. CARRIED (6 SC: `SC-GIFT-001/004/005/009/010/012`) dùng lại TC v1.0, không chép sang fragment v1.1.
> Không gỡ TC nào ⇒ không cần khai lỗ ID.

> **GENERATE 2026-09-17 (`CNL`):** scope NEW + MODIFIED = 9 SC → **13 TC**, áp `Project_rule.md §Custom Rules §10.4`
> ngay từ đầu (không cần renumber sau). 5 TC MODIFIED giữ ID v1.0 (`TC-CNL-004/006/009/010/012`); 8 TC NEW nối
> tiếp từ ID cao nhất đã dùng ở v1.0 (`TC-CNL-014`) → dải mới `TC-CNL-015..022`. 2 SC (`SC-CNL-006`, `SC-CNL-014`)
> fan-out 3 TC/SC theo vai (Người gửi/vận chuyển/nhận — mỗi vai fail độc lập theo `BR11-04`), 7 SC còn lại 1 TC/SC.
> CARRIED (8 SC) dùng lại TC v1.0, không chép sang fragment v1.1 — riêng `TC-CNL-008` cần siết thêm timestamp khi
> tái dùng. Scope module đã xác nhận IN 2026-09-17 (`RISK-CNL-06` Resolved) trước khi generate.

> **REVISE 2026-09-17 (`USR`, áp `Project_rule.md §Custom Rules §10.4` — Expected Result chỉ ghi ở step cuối):**
> 29 TC → **38 TC**. 6 SC có nhiều điểm kiểm chứng độc lập được tách thêm TC theo ưu tiên "tối đa hoá số case
> vibe-test được, không mất coverage" (`SC-USR-014` 1→2 · `SC-USR-015` phần khoảng-trắng/+84/chữ 1→3 ·
> `SC-USR-020` 1→3 · `SC-USR-021` phần biên-2/3-ký-tự 1→2 + phần 3-biến-thể-dấu 1→3 · `SC-USR-024` 1→2).
> Các TC còn lại: gộp nhiều điểm kiểm tĩnh vào 1 step Check cuối (`TC-USR-003`/`021`→`024`), đổi thứ tự step để
> điểm kiểm chính rơi đúng step cuối (`TC-USR-032`/`035`→`040`/`043`), hoặc bỏ hẳn dòng Expected phụ ở step giữa
> khi điểm đó không tự thân là 1 case fail độc lập (`TC-USR-018`/`022`/`024`/`027`/`036`→`019`/`025`/`027`/`033`/`044`).
> Dải ID NEW đổi từ `014..037` sang `014..046` (renumber liên tục theo `testcase-guide.md §A.2` chiến lược (b));
> mapping đầy đủ ở `fragments/TC-USR-v1.1-ID-MAPPING.md`. 5 TC MODIFIED giữ nguyên ID (`002/003/008/012/013`).
> **`TC-USR-022`(mới `025`) bỏ vế "wizard nhận giá trị mới"** — trùng phạm vi `SC-ORD-025`, không tạo TC bù.

> **REVISE 2026-09-17 (`USR`, BA trả lời CL):** chuỗi lỗi SĐT (`TC-USR-016/017/019/020/036`) BA xác nhận giữ theo demo ⇒ bỏ ghi chú "lấy tạm, chờ BA". Expected/số TC/ID/priority không đổi.
> **REVISE 2026-09-16 (`USR`, sửa theo spot-check `/review-tc` module):** R3-02 `016/017/019/020/036` thêm chuỗi lỗi verbatim (tạm theo demo, chờ xác nhận) · R3-01 `022` tách bước mở lại Theo dõi đơn qua tab "Hoạt động" · R3-09 `034` ghi rõ thoát bằng nút back thiết bị · R3-14 `025` chuyển tiền đề "địa chỉ khác rỗng" thành bước setup · R3-03 `032/033/035/036` ghi cần bổ sung tài khoản C/D vào catalog · R3-06 `028` tách bước xoá/nhập · R3-12 `002` bỏ placeholder · R4-01 thống nhất "field nhập liệu" và "số điện thoại" · R4-07 `026..031` thêm `DOC-v1.1-01` · R3-18 bỏ "Mục đích" thừa ở `015`. Số TC/ID/priority không đổi.
> **GENERATE 2026-09-16 (`USR`):** scope NEW + MODIFIED = 17 SC. 24 TC NEW (`TC-USR-014..037`) + 5 TC MODIFIED giữ ID v1.0 (`TC-USR-002/003/008/012/013`). CARRIED 7 SC dùng TC v1.0 (`TC-USR-001/004/005/006/007/009/010/011`), không chép sang fragment v1.1. Không gỡ TC nào ⇒ không cần khai lỗ ID.

> **REVISE 2026-09-18 (`ORD` — `TC-ORD-070`, QC GiangDC2 chốt sau recheck `VR-002`):** sửa **Expected + Steps + Notes**, ⛔ **không đổi** ID/Title/Priority/số TC (`Project_rule §10.5`). Lý do: bộ đếm `n/5` được vẽ **bên trong ô thêm ảnh** ở cuối dải ⇒ vế *"ẩn nút thêm khi đủ 5"* của `BR18-02` tất yếu làm bộ đếm biến mất ở mức 5/5. Expected cũ đòi **đồng thời** `bộ đếm 5/5` **và** `nút thêm ẩn` — **tự mâu thuẫn, không app nào đạt được**. Nay bỏ vế `5/5`, chuyển mốc assert bộ đếm về `4/5`, thêm bước **cuộn dải ảnh** vào Steps. ⇒ `TC-ORD-070` đổi verdict ❌ FAIL → ✅ **PASS**, ⛔ **không log bug** cho hành vi này. ⚠️ **Title giữ nguyên** (*"bộ đếm đạt trần"*) vì `§10.5` không cho sửa Title — câu chữ hơi lệch Expected mới, đã ghi nợ ở `§3`.

> **REVISE 2026-09-21 (`ORD` — `TC-ORD-073`, `TC-ORD-088`, QC GiangDC2 kiểm lại sau `VR-013`):** `BUG-024`/`BUG-023` bị huỷ vì app đúng ⇒ sửa **Expected + Steps + Test Data + Notes** theo hành vi thật (`073`: lightbox chỉ đóng bằng nút ×, chạm nền không đóng · `088`: form sửa tin đã đăng vẫn xoá được ảnh, tin còn 4/5 ảnh), ⛔ **không đổi** ID/Title/Priority/số TC (`§10.5`). Ghi ở `fragments/TC-ORD-v1.1.md` + `TC-MASTER-v1.1.xlsx` (sheet `ALL` + `Đăng tin & Quản lý tin`) + `TC-MASTER-LATEST.xlsx`. Verdict ✅ PASS.

> **REVISE 2026-09-21 (`ACT` — `TC-ACT-015`, QC GiangDC2 chốt sau `VR-017`):** app hiện đơn "Đã huỷ" ở tab "Đang diễn ra" (badge "Đã huỷ") — QC xác nhận **không phải bug** ⇒ sửa **Expected + step 4 + Notes** theo app: đơn "Đã huỷ" nằm ở tab "Đang diễn ra", KHÔNG ở tab "Đã hoàn thành"; vế đơn đã trả người gửi giữ nguyên. ⛔ **Không đổi** ID/Title/Priority/số TC (`Project_rule §10.5`) ⇒ Title còn lệch (nợ #27). Ứng viên bug của VR-017 cho TC này **huỷ, không log**. ⚠️ `TC-ACT-007` (CARRIED v1.0) vẫn assert kỳ vọng cũ.

> **REVISE 2026-09-21 (`ACT` — `TC-ACT-017`, QC GiangDC2 chốt sau `VR-017`):** ở tab rỗng, empty state đứng yên khi vuốt (không có phần tử cuộn được) — QC xác nhận **app đúng** ⇒ sửa **Expected + step 5 + Notes** theo app; `BUG-032` xoá khỏi `draft/`, không push. ⛔ Không đổi ID/Title/Priority/số TC (`§10.5`) ⇒ Title *"Check màn vẫn cuộn được…"* còn lệch (nợ #28).

## 2. Ràng buộc còn hiệu lực

1. **Mode `standard`** — kế thừa v1.0 (BA chốt 2026-09-07), ⛔ không trộn mode trong cùng version.
2. 🔴 **`TC-USR-003` và `TC-USR-008` có kỳ vọng NGƯỢC bản v1.0 cùng ID** — consolidate/execute phải lấy bản v1.1.
3. **Rule BA chốt ngoài PRD, demo đang lệch** (`Project_rule §10.1` chưa có bằng chứng UI STG): `TC-USR-002/008/012/024/028..042/045/046`. Lệch trên STG ⇒ log bug, ⛔ không sửa TC theo demo.
4. 🔴 **`Project_rule.md §Custom Rules §10.4`** — Expected Result chỉ neo 1 dòng ở step cuối mỗi TC. Áp cho mọi TC generate/regenerate từ 2026-09-17 trở đi, mọi module — không chỉ `USR`.

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | ✅ ~~**Chưa consolidate** TC-MASTER v1.1~~ | **Đóng 2026-09-17** — `TC-MASTER-v1.1.xlsx` 223 TC, 13 sheet, 0 trùng ID | — |
| 2 | 🟡 **Chưa review** (gate G1) | ⏳ | `/review-tc` |
| 3 | 🟡 **Chưa vibe-test STG** cho các điểm demo lệch rule (avatar · badge · ô địa chỉ · nguồn HRIS · bản nháp · icon khiên) | `RISK-USR-06` Partially | `/vibe-test --module USR` trước lô execute |
| 4 | 🟡 **Cần 4 tài khoản** (A · B · C chưa lưu + HRIS có dữ liệu · D chưa lưu + HRIS trống) | Chưa chuẩn bị | Xin dev/HR tài khoản C, D; chạy `TC-USR-040/041/043/044` trước |
| 5 | ✅ ~~Chuỗi thông báo lỗi SĐT lấy tạm theo demo~~ (`TC-USR-017/018/020/021`) | **Đóng 2026-09-17** — BA xác nhận chuỗi demo là chính thức | Đã bỏ chữ "tạm" trong các TC liên quan; không đổi Expected |
| 6 | ✅ ~~**module chưa generate**~~ | **Đóng 2026-09-17 — đủ 11/11 module**, `§10.4` áp ở cả 11 | — |
| 10 | 🟡 **`TC-FEED-015` viết dù BA đánh giá "có thể không cần viết TC" (lỗi data STG, không phải bug app)** | QC chưa xác nhận có giữ TC này khi consolidate không | Hỏi QC trước consolidate — giữ để có coverage nhánh lỗi, hay bỏ theo gợi ý BA |
| 7 | ✅ ~~**`CHANGELOG.md`/`risk_assessment.md` của `ASN-ghep-noi/` và `NTF-thong-bao/` chưa write-back kết luận CL Resolved 2026-09-17**~~ (`C-ASN-04/05/06`, `C-NTF-04/05`) | **Đóng 2026-09-17 (health-check lượt 2 kiểm lại)** — cả 5 CL **đã** write-back đầy đủ: bảng Status ghi `✅ Resolved 2026-09-17` + có khối `↳ KẾT LUẬN (theo BA)` riêng cho từng CL ở `risk_assessment.md`, và `CHANGELOG.md` của cả 2 module đều có dòng ngày 2026-09-17. ⚠️ **Dòng nợ này chính nó mới là chỗ bị stale** — nó kể lại tình trạng của register khác rồi không được cập nhật (đúng lớp lỗi `health-check G-06b`). Cùng lượt đã sửa nốt `ASN/risk_assessment.md` KN#2 (còn ghi *"việc còn lại: hỏi BA C-ASN-04/C-ASN-05"*). | — |
| 8 | 🟡 **`TC-NTF-017..022` + phần mở rộng `TC-NTF-008`/`014` cần rà lại Pre-condition** theo luồng `DLV` đã chốt | ✅ `DLV` **đã generate 2026-09-17** (`TC-DLV-031..081`) ⇒ nợ này nay xử lý được | Rà 8 TC ở `TC-NTF-v1.1.md`: đổi mô tả tiền đề sang đúng chuỗi 4 tầng của `C-DLV-06` (màn "Xác nhận đã giao" → "Liên hệ người gửi" → modal "Chưa liên lạc được?" → "Xử lý đơn hàng"); ⛔ vẫn KHÔNG nhét mã `TC-DLV-NNN` vào Steps (`testcase-guide.md §B.3`) |
| 22 | ✅ ~~**Khối `Seed dùng chung` không có trong TC-MASTER**~~ | **Đóng 2026-09-17 (`review-tc` M-1)** — thêm sheet `Seed` (9 khối, phủ **21/21** mã `SEED-*`); sửa **34 ô** trỏ *"đầu fragment"* → *"sheet `Seed` của chính file"*; `Project_rule §10.3` thêm **mục 4** bắt consolidate phải carry. 🔴 Phát hiện kèm: `SEED-DLV-01` (3 module trỏ) trước đó nằm ở **file thứ ba** `03_test-cases/v1.0/CHANGELOG.md` | — |
| 23 | ✅ ~~**`TC-CNL-v1.1.md` chưa tự đủ**~~ | **Đóng 2026-09-17** — chép định nghĩa đầy đủ `SEED-DLV-01` vào fragment (5 checkpoint, cảnh báo *trạng thái một chiều*, ngoại lệ `TC-DLV-024`) | — |
| 24 | ✅ ~~**R3-19 · 12 TC thiếu nhãn `(setup)`**~~ | **Đóng 2026-09-17 (`review-tc` đợt 2)** — sửa cả TC-MASTER lẫn fragment, step có nhãn 563→**575**. ⚠️ `TC-ORD-048` chỉ gắn **step 4**; step 3 sinh quan sát dùng cho Expected nên KHÔNG phải setup | — |
| 20 | 🔴 **TC-MASTER-v1.1 KHÔNG chứa 163 TC CARRIED** — execute/vibe-test phải mở song song `TC-MASTER-v1.0.xlsx` | QC chốt 2026-09-17 không gộp regression | Ghi rõ trong test plan / lệnh execute: **2 file**. Hoặc chạy lại `--consolidate` với regression nếu đổi ý |
| 21 | ⚠️ **54 TC ID trùng giữa 2 file, 5 TC kỳ vọng NGƯỢC nhau** (`TC-ACT-008/013/014`, `TC-USR-003/008`) | SC MODIFIED giữ ID v1.0 theo `§A.2` | Người chạy **LUÔN lấy bản v1.1**; đã cảnh báo ở sheet `Overview` của TC-MASTER-v1.1 |
| 18 | 🟡 **`TC-ORD-076` thiếu email mẫu người đã nghỉ việc** | QTHT/BA cấp lúc vibe-test; fragment dùng placeholder | Xin email `@fpt.com` đã nghỉ việc trước lô execute; chưa có ⇒ ghi `Blocked`, ⛔ không PASS |
| 19 | 🟡 **Mốc tiền + block Ghi chú chưa có TC** — `SC-ORD-008/009/010/011` là CARRIED, ngoài `id_range` delta | `C-ORD-18` làm 4 SC này assert mạnh hơn nhưng `Project_rule` cấm sửa file v1.0 | Mở `analyze-requirements --module ORD` chính thức hoá thành MODIFIED nếu muốn regenerate TC cho 4 SC này |
| 16 | ✅ ~~**Consolidate phải gỡ `TC-HOME-010`/`024`**~~ | **Đóng 2026-09-17** — verify 2 ID không lọt vào TC-MASTER-v1.1 | ⚠️ Còn lại: 2 TC này **vẫn sống trong `TC-MASTER-v1.0.xlsx`** ⇒ ⛔ không chạy khi lấy TC CARRIED từ file v1.0 |
| 17 | 🟡 **`test_data_catalog.md` của `HOME` chưa ghi ràng buộc môi trường cho `SC-HOME-021` nhánh ẩn nút** | Catalog mới chỉ cảnh báo cho `SC-HOME-025` (`EMP-01`); phát hiện khi viết TC | Bổ sung ở lượt `analyze-requirements` kế tiếp — cả 2 TC đều cần dọn dữ liệu toàn STG do `C-HOME-04` chốt tin load toàn quốc |
| 15 | 🔴 **`test_scenario_map.md` của `TS` chưa write-back `C-TS-03`** — Then của `SC-TS-008` (9 trường prefill) và `SC-TS-014` (prefill sửa được) đã lỗi thời | `risk_assessment.md` đã có đủ kết luận; generate-tc áp thẳng bản Resolved | Đồng bộ scenario map ở lượt `analyze-requirements`/`health-check` kế tiếp — nếu không, reviewer đọc scenario map sẽ tưởng `TC-TS-008`/`021` viết sai |
| 13 | 🔴 **3 TC `ACT` đảo/siết kỳ vọng so với bản v1.0 CÙNG ID** (`TC-ACT-008`/`013`/`014`) | Đã khai ở header fragment §0.2 | Consolidate/execute **phải lấy bản v1.1**; ⛔ không merge nhầm bản v1.0 |
| 14 | 🟡 **`C-ACT-03(c)` ⟷ `C-ORD-17` nói ngược nhau** về việc card "Hết hạn" có tương tác được không | Chưa chạm TC (SC đích tap card là CARRIED) | Đối chiếu lại với BA ở lượt `analyze-requirements` kế tiếp, TRƯỚC khi regenerate `SC-ACT-009/010/011` |
| 11 | 🟡 **`TC-DLV-045/046/052` chưa assert cờ "không liên lạc được" + `NTF-05` ⟷ `NTF-11`** (`C-DLV-08` (a)(b) Partially) | Không hỏi BA nữa — BA đã chỉ chỗ tự đọc ở block "LỊCH SỬ" | `/vibe-test --module DLV` đọc log 2 đường chọn quầy → `/analyze-requirements --module DLV` chính thức hoá → siết lại 3 TC |
| 12 | 🟡 **`SC-DLV-060` DESCOPED (0 TC)** — admin can thiệp, role admin out of scope v1.1 | Đã khai ở header fragment §0.1 + log GENERATE | Mở lại khi phase sau build role admin; ⛔ không tính vào mẫu số coverage v1.1 |
| 9 | 🟡 **`TC-NTF-006`/`010` (CARRIED) bị chạm bởi `C-NTF-05`/`C-NTF-04` nhưng chưa chính thức hoá MODIFIED** | Ngoài `id_range` delta hiện tại | Cân nhắc mở lại `analyze-requirements --module NTF` để chính thức hoá 2 SC này thành MODIFIED nếu cần regenerate TC |
| 25 | 🟡 **Title `TC-ORD-070` lệch Expected mới** — vẫn ghi *"bộ đếm đạt trần"* trong khi Expected 2026-09-18 chốt *bộ đếm biến mất ở 5/5* | `§10.5` freeze không cho sửa Title, chỉ cho sửa Steps/Expected/Test Data/Pre-condition/Notes/Status/Lifecycle | Xin QC/team mở khoá Title ở lượt chốt TC kế tiếp, hoặc giữ nguyên và dựa vào Expected — ⛔ không tự sửa |
| 26 | 🟡 **Title `TC-ORD-073` / `TC-ORD-088` lệch Expected mới** — `073` còn ghi *"cả nút đóng lẫn chạm nền"*, `088` còn ghi *"không xoá được ảnh"*; Expected nay theo app (`073`: chỉ nút ×; `088`: xoá được) | `§10.5` không cho sửa Title | Xin QC/team mở khoá Title ở lượt chốt TC kế tiếp. Đồng thời hỏi BA: `BR18-03` (chạm nền) và `BR18-05` (ảnh bất biến truy vết) có cần sửa/xoá khỏi PRD không |
| 27 | 🟡 **Title `TC-ACT-015` lệch Expected mới** — Title còn ghi *"…còn đơn đã huỷ vẫn bị ẩn"*, Expected 2026-09-21 chốt theo app: đơn "Đã huỷ" hiện ở tab "Đang diễn ra" | `§10.5` không cho sửa Title. Kèm: `TC-ACT-007` (CARRIED, `TC-MASTER-v1.0`) vẫn assert "Đã huỷ ẩn khỏi cả 2 tab" ⇒ **sẽ FAIL oan** nếu chạy; `risk_assessment.md` ACT còn ghi kết luận cũ `C-ACT-04(b)` | Xin QC/team mở khoá Title ở lượt chốt TC kế tiếp · `/analyze-requirements --update` ghi đè `C-ACT-04(b)` · QC quyết định `TC-ACT-007` sửa Expected hay `DESCOPED` |
| 28 | 🟡 **Title `TC-ACT-017` lệch Expected mới** — Title còn ghi *"Check màn vẫn cuộn được khi đang hiện empty state…"*, Expected 2026-09-21 chốt theo app: màn rỗng đứng yên khi vuốt | `§10.5` không cho sửa Title; `BR17-03` PRD vẫn ghi *"vẫn cuộn được"* | Xin QC/team mở khoá Title ở lượt chốt TC kế tiếp · hỏi BA có cần sửa câu chữ `BR17-03` |
| 29 | 🟡 **Title `TC-CNL-009` lệch Expected mới** — Title còn ghi *"Check huỷ đơn ghi log đủ vai trò, lý do và thời điểm"*, Expected 2026-09-22 chốt theo app: ghi **tên người**, không ghi vai trò (chấp nhận) | `§10.5` không cho sửa Title | Xin QC/team mở khoá Title ở lượt chốt TC kế tiếp — hoặc giữ nguyên và dựa vào Expected |
| 30 | 🟡 **Title `TC-TS-010`/`011`/`012` lệch Expected mới** — cả 3 Title còn ghi *"…nút Gửi vô hiệu hoá…"*, Expected 2026-09-22 chốt theo app thật (Microsoft Forms): nút "Gửi" **không** disable — validate qua lỗi inline "Câu hỏi này là bắt buộc." sau khi bấm (nghiệp vụ vẫn chặn được submit, chỉ khác cơ chế UI). `BUG-040` (đã log cho phát hiện này) **đã xoá** — QC xác nhận không phải bug | `§10.5` không cho sửa Title | Xin QC/team mở khoá Title ở lượt chốt TC kế tiếp — hoặc giữ nguyên và dựa vào Expected. `TC-TS-012` còn 1 vế khác chưa đóng: SĐT sai định dạng vẫn phải bị chặn nhưng thực tế KHÔNG bị chặn (`BUG-041`, còn giữ) ⇒ `TC-TS-012` vẫn FAIL vì lý do này, không phải vì cơ chế nút |
