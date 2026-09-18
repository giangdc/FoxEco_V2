---
id: v1.1/ASN-ghep-noi/risk
title: Risk Assessment — v1.1 · Module ASN
type: risk-assessment
version: v1.1
sprint: 1
module: ASN
counts:
  cl: 5
  risk: 8
  cl_open: 0
  cl_resolved: 5
status: ANALYZED
updated: 2026-09-17
---

# Risk Assessment — v1.1 · Module ASN

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module ASN của v1.1 (delta).
> Chỉ ghi risk MỚI hoặc risk MODIFIED (đổi Status/Solution) so với v1.0. Risk không đổi → xem `v1.0/ASN-ghep-noi/risk_assessment.md`, không lặp lại.

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| ASN | **High** (không đổi so với v1.0) | Vẫn là module rủi ro cao nhất do double-accept + bảo mật liên hệ; riêng auto-match đã được PRD v1.1 chốt phần lớn tham số (`RISK-ASN-04`/`06` → Resolved), rủi ro còn lại chuyển sang "giá trị cấu hình trần thông báo chưa có số cứng" (risk mới) |

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-ASN-04 | ASN / Auto-match | *(cập nhật Status)* 3 tham số auto-match — 2/3 đã chốt: định nghĩa khớp (điểm + ngày overlap + buổi overlap) và chu kỳ quét (≤60s); còn "ngưỡng gộp thông báo" chuyển sang risk mới `RISK-ASN-08` | High → **hạ mức, xem RISK-ASN-08** | `DOC-v1.1-01` §8.4 BR04-01/02 · §9 NFR-04 | `SC-ASN-011` (đủ 4 nhánh a-d theo overlap thật) | Đã Resolved qua PRD v1.1; ghi ràng buộc `CHANGELOG §2` | **Resolved** | REQ-ASN-007, SC-ASN-011 |
| RISK-ASN-06 | ASN / Ưu tiên gợi ý | *(cập nhật Status)* Tiêu chí "độ gần tuyến" — trước đây coi là vô hiệu (nhị phân, không còn thang đo); PRD xác nhận vẫn là tầng ưu tiên số 1, có hiệu lực dù nhị phân | Medium → **Resolved** | `DOC-v1.1-01` §8.3 BR03-06 | `SC-ASN-015` (2 tầng ưu tiên) | Đã làm rõ qua PRD v1.1, không cần hỏi BA thêm | **Resolved** | REQ-ASN-009, SC-ASN-015 |
| RISK-ASN-02 | ASN / Double-accept | *(cập nhật Solution)* Nhánh cạnh tranh thật vẫn khó test bằng manual — nhưng giờ có ngưỡng + phương pháp chính thức để giao cho automation | High (không đổi) | `DOC-v1.1-01` §9 NFR-06 (50 request đồng thời, 0% trùng, concurrency test trên staging) | `SC-ASN-006` nhánh (b) | **Cập nhật:** giao nhánh cạnh tranh thật cho automation/backend concurrency test theo đúng ngưỡng NFR-06, không còn "đề xuất" chung chung như v1.0 | Open (nhánh manual) / **có hướng automation rõ ràng** | REQ-ASN-003, SC-ASN-006 |
| RISK-ASN-05 | ASN / Realtime | *(cập nhật Solution)* Bằng chứng đồng bộ realtime trước đây chỉ từ demo giả lập — giờ có ngưỡng định lượng để test thật | Medium (không đổi) | `DOC-v1.1-01` §9 NFR-08 (≤5 giây) | `SC-ASN-008` | **Cập nhật:** dùng ngưỡng ≤5s làm oracle pass/fail khi test trên 3 thiết bị thật, thay vì chỉ quan sát định tính | Open — chờ chạy test thật để xác nhận đạt ngưỡng | REQ-ASN-005, SC-ASN-008 |
| RISK-ASN-08 | ASN / Auto-match | **(risk mới 2026-09-15)** Ngưỡng "trần thông báo khớp/ngày" (`BR04-04`) không có số cứng. **BA 2026-09-16: KHÔNG có trần theo ngày — tài liệu bị dư**; thay bằng *"mỗi lần đăng Tôi nhận giao hàng thì bắn 5 thông báo / 1 tin đăng"* ⇒ rủi ro gốc **hết**, nhưng rule thay thế chưa đủ định nghĩa (`C-ASN-04`) | Medium → **Closed (thay bằng `C-ASN-04`)** | `DOC-v1.1-01 §8.4 BR04-04 · page 38` · BA trả lời 2026-09-16 | `SC-ASN-014` — viết lại theo rule "5 thông báo / 1 tin OFFER"; ✅ định nghĩa **đã đủ** từ `C-ASN-04` Resolved 2026-09-17 | ⛔ Không viết TC trần/ngày nữa. ✅ **Hết việc hỏi BA** — `C-ASN-04` đóng 2026-09-17 | Closed | REQ-ASN-008, SC-ASN-014 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-NTF-02 | Định nghĩa "khớp tuyến" & tham số vận hành (**home canonical ở ASN**, bản gốc `v1.0/ASN-ghep-noi/`) | ✅ **Resolved 2026-09-16 — BA: không có trần theo ngày; "5 thông báo / 1 tin đăng OFFER"** | 2026-07-27 | REQ-ASN-006, REQ-ASN-007, REQ-ASN-008 |
| C-ASN-03 | Đăng tin mới ghi đè đơn đang có, không tạo song song (bản gốc `v1.0/ASN-ghep-noi/`) | ✅ **Resolved 2026-09-16 — BA: giới hạn bản demo; app không giới hạn đăng tin** | kế thừa 2026-07 | REQ-ASN-012, SC-ASN-018 |
| C-ASN-04 | Rule "5 thông báo / 1 tin đăng OFFER" — ai nhận, chọn 5 tin nào, có quét lại khi có tin NEED mới không | ✅ **Resolved 2026-09-17** — BA trả lời đủ (a)-(e), trần độc lập theo từng tuyến | 2026-09-16 | REQ-ASN-006, REQ-ASN-008, REQ-ASN-009, SC-ASN-013, SC-ASN-014 |
| C-ASN-05 | "Trùng điểm lấy và điểm giao" được so thế nào khi địa chỉ là **ô văn bản tự do ≤ 200 ký tự** | ✅ **Resolved 2026-09-17** — BA: khớp chính xác, dùng danh mục văn phòng nên không cần chuẩn hoá | 2026-09-16 | REQ-ASN-007, SC-ASN-011 |
| C-ASN-06 | Người bấm nhận sau (double-accept) thấy câu nào: "Tin này đã có…" hay "Đơn này đã có…"; dạng toast/popup/push | ✅ **Resolved 2026-09-17 — Accepted**, BA: lấy 1 câu bất kỳ trong 15 thông báo | 2026-09-16 | REQ-ASN-003, SC-ASN-006, SC-ASN-010 |

> ℹ️ `C-NTF-02` và `C-ASN-03` có bản gốc ở `v1.0/ASN-ghep-noi/risk_assessment.md` (giữ nguyên làm hồ sơ lịch sử, ⛔ không sửa); **bản hiện hành là 2 dòng trên** + khối trả lời BA bên dưới.

### C-NTF-02 · ↳ BA trả lời 2026-09-16 *(→ RESOLVED — phần trần thông báo)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `ASN` · cột "Câu trả lời BA" · 2026-09-16

> "Không có ngường ngày, tài liệu bị dư → mỗi lần đăng Tôi nhận giao hàng thì bắn 5 thông báo/ 1 tin đăng, không có giới hạn ngày"

↳ **Ghi chú:** `BR04-04` (*"Trần số thông báo khớp mỗi ngày cho một người dùng do admin cấu hình"*) là **dư — không có trong sản phẩm**; kéo theo dòng *"Cấu hình ngưỡng thông báo khớp tuyến"* ở `§7.3` và *"cấu hình ngưỡng thông báo"* ở Persona Admin cũng không áp dụng. ⇒ `RISK-ASN-08` **Closed**. 🔁 **Kết luận bị đảo lần 2:** v1.0 (BA 2026-07-29, `KB-ASN-03`) *"trần tính riêng theo từng tin OFFER"* → v1.1 PRD *"trần theo ngày/người dùng"* → nay BA quay về **theo từng tin đăng** (*"5 thông báo / 1 tin đăng"*). Rule thay thế chưa đủ để viết TC → `C-ASN-04`.

### C-ASN-03 · ↳ BA trả lời 2026-09-16 *(→ RESOLVED)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `ASN` · cột "Câu trả lời BA" · 2026-09-16

> "Hiện tại không giói hạn đăng tin, đây là giới hạn bản demo"

↳ **Ghi chú:** Hiện tượng *"đăng tin mới ghi đè đơn đang có"* là **giới hạn của demo**, không phải hành vi sản phẩm. Rule chốt: **không giới hạn số tin đăng** của một người ⇒ `SC-ASN-018` hết `[GAP]`, Then assert: đăng tin thứ 2 khi tin thứ 1 còn `POSTED` → **cả 2 tin cùng tồn tại** trên Bảng tin + "Đơn của tôi". Nếu STG ghi đè ⇒ **bug**. ⚠️ "Không giới hạn" — BA không nói có trần chống spam hay không; không viết TC boundary số lượng.

### C-ASN-04 · Rule "5 thông báo / 1 tin đăng" — định nghĩa đủ để test *(RESOLVED 2026-09-17)*

📍 BA trả lời `C-NTF-02` 2026-09-16 ⟷ `DOC-v1.1-01 §6.2 AC-21.1.01 · trang 24` · `§8.3.1 BR03-06 · trang 36` · `§8.4 Trigger · trang 37`

> `AC-21.1.01`: "…mỗi lần gợi ý tối đa 5 tin, ưu tiên độ gần tuyến rồi tới thời gian đăng."

> `BR03-06`: "Trần gợi ý cho một người vận chuyển: tối đa 5 tin phù hợp, ưu tiên độ gần tuyến rồi tới thời gian đăng."

> `§8.4` Trigger: "Có tin NEED mới được đăng, hoặc có tin OFFER mới được đăng"

↳ **Ghi chú:** Câu BA *"mỗi lần đăng Tôi nhận giao hàng thì bắn 5 thông báo / 1 tin đăng"* thay trần/ngày, nhưng còn 5 điểm không assert được: (a) **Ai nhận** 5 thông báo — người đăng OFFER (Carrier) được báo 5 tin NEED khớp? (b) Có **>5** tin NEED khớp thì chọn 5 tin nào — có phải cùng thứ tự ưu tiên `BR03-06`? Tức **"5 thông báo" và "trần gợi ý 5 tin" là cùng một rule** (`SC-ASN-013` ⟷ `SC-ASN-014` gộp được)? (c) Có **<5** tin khớp thì gửi đúng số tin khớp, **0** tin thì không gửi gì? (d) Chiều ngược lại theo `§8.4` Trigger: khi có **tin NEED mới** khớp một OFFER **đã đăng trước đó**, Carrier có nhận thêm thông báo không — và có bị tính vào con số 5 của tin OFFER đó không? (e) Hệ thống quét lại theo chu kỳ (`NFR-04` ≤ 60s) — tin NEED đăng **sau** khi OFFER đã bắn đủ 5 thì còn được báo không?

↳ **KẾT LUẬN (theo BA) 2026-09-16:** (a) người **ĐĂNG TUYẾN** (Carrier) là người nhận 5 thông báo. (b) chọn 5 tin theo **ưu tiên thời gian đăng** (tin đăng trước ưu tiên trước) — **ĐÂY LÀ CÙNG 1 RULE** với "trần gợi ý 5 tin" của `BR03-06`, không phải 2 rule khác nhau ⇒ `SC-ASN-013`/`SC-ASN-014` gộp được. (c) có <5 tin khớp thì gửi đúng số đó; 0 tin thì không gửi. (d) tin NEED mới đăng sau khi tuyến đã đăng: NẾU tuyến CHƯA đủ 5 thông báo thì vẫn gửi thêm; NẾU tuyến đã bắn đủ 5 rồi thì **KHÔNG gửi thêm** cho tin mới đó. (e) mỗi tuyến (mỗi lần đăng "Tôi nhận giao hàng") có trần **ĐỘC LẬP** 5 thông báo — đăng 2 tuyến thì tối đa nhận 10 thông báo (5+5), không cộng dồn chung 1 trần. `C-ASN-04` ĐÓNG HẲN — đủ định nghĩa để viết Then chính xác cho `SC-ASN-013/014`.

### C-ASN-05 · "Trùng điểm lấy/giao" với ô địa chỉ tự do *(RESOLVED 2026-09-17)*

📍 `DOC-v1.1-01 §8.4.1 BR04-01 · trang 37` · `§8.1.4 dòng "Địa chỉ lấy hàng" · trang 35` · `§8.2.2 dòng "Điểm xuất phát"/"Điểm đến" · trang 36` · `§4 Out of Scope · trang 9`

> `BR04-01`: "Điều kiện khớp: trùng điểm lấy và điểm giao · khoảng ngày của NEED và OFFER có ngày giao nhau · tập buổi có buổi giao nhau."

> `§8.1.4`: "Địa chỉ lấy hàng | Có | Văn bản · prefill địa chỉ mặc định | Không để trống, ≤ 200 ký tự"

> `§4 Out of Scope`: "Ghép nối tự động nâng cao theo độ gần địa lý bằng bản đồ/toạ độ — MVP dùng khớp điểm lấy/giao + khoảng ngày + buổi"

↳ **Ghi chú:** Điểm lấy/giao và điểm xuất phát/đến đều là **văn bản tự do** (`C-ORD-11` Resolved). PRD bắt *"trùng"* nhưng không nói phép so: (a) **so khớp chuỗi chính xác** (khác 1 dấu cách/hoa-thường là không khớp)? (b) **chuẩn hoá** (trim, bỏ dấu, không phân biệt hoa thường)? (c) khớp theo **văn phòng / toà nhà / tỉnh** trích từ địa chỉ? Không chốt thì **không dựng được dữ liệu** cho 4 nhánh của `SC-ASN-011` — tester gõ lại địa chỉ bằng tay sẽ ra kết quả ngẫu nhiên. Liên quan `RISK-ORD-12` (so sánh *"địa chỉ giao khác địa chỉ lấy"* cũng chưa định nghĩa) — nên hỏi chung 1 câu: **quy tắc so sánh địa chỉ** dùng chung cho cả 2 rule.

↳ **KẾT LUẬN (theo BA) 2026-09-16:** (a) so khớp "trùng điểm" = **KHỚP CHÍNH XÁC** (exact match) + điều kiện thời gian phù hợp (ngày/buổi overlap — cùng rule đã chốt ở `BR04-01`). (b) từ khi địa chỉ (lấy/giao/điểm xuất phát) đều **CHỌN TỪ DANH MỤC VĂN PHÒNG** (`C-USR-05`) thay vì gõ tự do, nên không cần thêm rule chuẩn hoá (bỏ khoảng trắng/dấu/hoa-thường) — 2 giá trị chọn từ cùng 1 danh mục thì khớp chuỗi chính xác là đủ. (c) **CÓ** — cùng 1 phép so "chính xác" áp dụng luôn cho rule "địa chỉ giao phải khác địa chỉ lấy" (`RISK-ORD-12`). `C-ASN-05` ĐÓNG HẲN — `SC-ASN-011` (4 nhánh) và `SC-ORD-063` dựng được dữ liệu theo mã văn phòng (id) thay vì gõ tay.

### C-ASN-06 · Thông báo cho người bấm nhận sau *(RESOLVED 2026-09-17)*

📍 `DOC-v1.1-01 §6.2 AC-12.1.02 · trang 20` ⟷ `§6.2 AC-22.2.01 · trang 25`

> `AC-12.1.02`: "Người sau nhận thông báo "Tin này đã có người nhận mang giúp" và tin biến khỏi bảng tin của họ."

> `AC-22.2.01`: "Hiện thông báo "Đơn này đã có người nhận mang giúp" và không tạo cặp ghép thứ hai. Màn chi tiết chuyển sang trạng thái chỉ xem."

↳ **Ghi chú:** Cùng một tình huống (tin đã có người nhận) nhưng 2 AC dùng **2 câu khác nhau** ("Tin này" ⟷ "Đơn này") theo 2 lối vào (Bảng tin ⟷ thông báo khớp tuyến), và câu đó **không có** trong danh mục 15 thông báo `§8.13.1` ⇒ không rõ là **toast/popup trong app** hay **push**. Hỏi: (a) giữ 2 câu riêng theo lối vào hay thống nhất 1 câu? (b) dạng hiển thị? Mức ưu tiên **thấp** — chỉ ảnh hưởng assert verbatim của `SC-ASN-006`/`SC-ASN-010`.

↳ **KẾT LUẬN (theo BA) 2026-09-16:** BA đề nghị **BỎ QUA** — chọn 1 câu bất kỳ trong danh mục 15 thông báo chính thức làm chuẩn, không cần định nghĩa câu riêng cho từng lối vào. `SC-ASN-006/010` assert theo câu đã có sẵn trong danh mục 15 thông báo (không tạo thêm biến thể câu chữ). `C-ASN-06` ĐÓNG theo hướng Accepted.


## Khuyến nghị tổng thể
1. **Không còn blocker cứng cho auto-match** — `RISK-ASN-04`/`RISK-ASN-06` đã Resolved qua PRD v1.1, coverage `SC-ASN-011`/`SC-ASN-015` có thể viết đầy đủ 4 nhánh + 2 tầng ưu tiên.
2. **Trước generate-tc:** ✅ **HẾT VIỆC** — `RISK-ASN-08` Closed (BA 2026-09-16) · `C-ASN-04` **Resolved 2026-09-17** (đủ (a)–(e), trần độc lập theo từng tuyến) · `C-ASN-05` **Resolved 2026-09-17** (khớp **chính xác**, địa chỉ chọn từ danh mục văn phòng nên không cần chuẩn hoá ⇒ `SC-ASN-011` dựng được 4 nhánh bằng mã văn phòng). ⛔ Dòng cũ *"việc còn lại: hỏi BA C-ASN-04/C-ASN-05"* **HẾT HIỆU LỰC** (sửa 2026-09-17, health-check G-06b).
3. **Ưu tiên chuyển cho automation:** nhánh cạnh tranh thật của `SC-ASN-006` (concurrency 50 request) và mốc ≤5s của `SC-ASN-008` — cả hai giờ có ngưỡng đo được rõ ràng (NFR-06, NFR-08), phù hợp hơn cho backend/integration test so với manual.
4. **SC mới `SC-ASN-019`** cần công cụ gọi API trực tiếp (Postman/tương đương) — không thực hiện được thuần qua UI, lập kế hoạch môi trường trước khi execute.
