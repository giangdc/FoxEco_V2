---
id: v1.1/ASN-ghep-noi/changelog
title: Changelog — Module ASN
type: changelog
version: v1.1
sprint: 1
module:
  code: ASN
  dir: ASN-ghep-noi
  name: Ghép nối
doc_source:
  - id: DOC-v1.1-01
    section: "§8.3 FR03 (Ghép nối & lộ liên hệ) · §8.4 FR04 (Khớp tuyến OFFER↔NEED) · §9 NFR-04/06/08/11"
id_range:
  req: "REQ-ASN-013 (NEW) + REQ-ASN-005, REQ-ASN-007, REQ-ASN-008, REQ-ASN-009 (MODIFIED, giữ ID sprint 1)"
  sc: "SC-ASN-019 (NEW) + SC-ASN-006, SC-ASN-008, SC-ASN-011, SC-ASN-014, SC-ASN-015 (MODIFIED, giữ ID sprint 1)"
  cl: "(không mở CL mới — C-ASN-03/C-NTF-02 giữ nguyên trạng thái v1.0) + C-ASN-04..06 (NEW 2026-09-16) · C-NTF-02, C-ASN-03 → Resolved (2026-09-16)"
  risk: "RISK-ASN-08 (NEW) + RISK-ASN-02, RISK-ASN-04, RISK-ASN-05, RISK-ASN-06 (Status/Solution cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-17
---

# Changelog — Module ASN (`ASN`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-17 | UPDATE | **QC cung cấp ảnh UI thật `Goi dien.png`** — bấm nút "Gọi" cạnh SĐT (sau khi lộ liên hệ) mở action sheet: header tên + SĐT, rồi "Gọi điện thoại"/"Gọi Zalo"/"Copy số điện thoại"/"Huỷ". Theo yêu cầu QC, **bỏ "Gọi Fchat"** (có trong ảnh gốc nhưng không đưa vào danh mục chính thức để viết TC). Component dùng chung cho mọi nơi có "SĐT + nút Gọi" (`ASN`/`FEED`/`DLV`) — chỉ viết 1 TC ở đây, các module khác cross-ref | Ảnh UI thật `00_input/v1.1/design/Goi dien.png`, QC GiangDC2 cung cấp 2026-09-17 | Thêm 1 dòng `test_data_catalog.md`; trước đây "nút Gọi" chỉ được ghi nhận là TỒN TẠI, chưa ai assert được bấm vào ra gì — nay có oracle rõ ràng |
| 2026-09-17 | UPDATE | **Vibe-check demo 3-role mới** (`https://giangdc.github.io/foxeco_demo/`, khác demo `FoxEcoQC` cũ 1-role). (a) Quan sát được **4 lựa chọn "Buổi"** khi đăng tin OFFER: "Sáng"/"Chiều"/"Sau giờ làm"/"Giờ nào cũng được" — bổ sung `test_data_catalog.md` (QA-obs, chưa phải chốt chính thức). (b) Xác nhận trực tiếp đồng bộ realtime 3 vai hoạt động (NFR-08) — 3 panel cập nhật "Đã ghép" tức thì khi Carrier bấm nhận đơn. (c) Xác nhận demo 3-role **CÙNG giới hạn "1 đơn toàn cục"** với demo cũ khi xem lại qua màn "Theo dõi đơn" sau submit — đăng OFFER mới ghi đè/xoá đơn NEED đang "Đã ghép". ⚠️ **Cập nhật cùng ngày:** phát hiện cách lách được giới hạn này — điều hướng thẳng vào tab "Hoạt động" → "Đang diễn ra" (không qua màn Theo dõi đơn) — quan sát được card OFFER riêng biệt, đã dùng để đóng `C-ORD-16`/`C-ACT-04` (xem CHANGELOG các module đó) | Vibe-check thủ công qua Chrome, theo yêu cầu QC GiangDC2 2026-09-17 | `test_data_catalog.md` thêm 1 dòng "Buổi"; không đổi SC/TC counts; `TC-ASN-011/012/022/023` (đã generate) có thể cập nhật nhãn "Buổi" cụ thể thay placeholder |
| 2026-09-17 | UPDATE | **Rà soát toàn bộ workbook (không chỉ mục nhắc demo) theo yêu cầu QC — đồng bộ câu trả lời BA từ `CL-hoi-BA-v1.1.xlsx` vào file này (đã nằm sẵn trong xlsx từ 2026-09-16 nhưng chưa đóng sổ).** `C-ASN-04` → **Resolved** (định nghĩa đủ rule "5 thông báo/tuyến": người đăng tuyến nhận, ưu tiên thời gian đăng, trần độc lập theo từng tuyến). `C-ASN-05` → **Resolved** (so khớp địa chỉ = chính xác, vì đã chọn từ danh mục văn phòng thay vì gõ tự do). `C-ASN-06` → **Resolved (Accepted)** — BA: dùng 1 câu bất kỳ trong 15 thông báo có sẵn | BA trả lời `CL-hoi-BA-v1.1.xlsx` sheet `ASN` 2026-09-16 (bỏ sót ở lượt trước) | `counts` cl_open 3→0, cl_resolved 2→5 — module ASN **HẾT điểm hỏi BA** |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa WARNING health-check G-03:** thay 7 trích dẫn bị chép lặp sang file khác bằng dòng trỏ `↪` về đúng home (REQ → `requirement_traceability.md` · CL → `risk_assessment.md`) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Nội dung quote không mất — chỉ còn 1 home |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa theo health-check VERSION v1.1 (G-06b CRITICAL):** các đoạn register sống còn kể lại kết luận cũ của CL vừa Resolved (`C-NTF-02`/`RISK-ASN-08` — `test_data_catalog` dòng trần/ngày + ghi chú chung, Khuyến nghị #2, heading + ghi chú `REQ-ASN-008`, Source Detail `SC-ASN-014`) — đổi mục Khuyến nghị / heading / data catalog sang kết luận hiện hành và thêm dòng *"⛔ Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC"* sau các ghi chú gốc (giữ nguyên nội dung cũ làm hồ sơ, không xoá lặng lẽ) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Không đổi `counts`, không đổi Then SC — chỉ đồng bộ chữ với CL section |
| 2026-09-16 | UPDATE | **Áp câu trả lời BA** + rà sâu `FR03/FR04`. (a) `C-NTF-02` → **Resolved**: **không có trần thông báo theo ngày** (`BR04-04` dư) — thay bằng *"5 thông báo / 1 tin đăng OFFER"*; `RISK-ASN-08` Closed; `SC-ASN-014` viết lại. (b) `C-ASN-03` → **Resolved**: ghi đè đơn là giới hạn demo, app **không giới hạn** đăng tin; `SC-ASN-018` hết GAP. (c) **Mở 3 CL mới:** `C-ASN-04` (định nghĩa rule 5 thông báo) · `C-ASN-05` (so khớp "trùng điểm" với địa chỉ văn bản tự do — chặn dựng data `SC-ASN-011`) · `C-ASN-06` (2 câu thông báo khác nhau cho người nhận sau) | BA trả lời 2026-09-16 · rà kỹ theo yêu cầu QC GiangDC2 | `counts` cl 2→5 (bổ sung bảng CL v1.1 — trước chỉ có ghi chú trỏ v1.0); `SC-ASN-014` + `SC-ASN-018` regenerate TC |
| 2026-09-15 | UPDATE | **DELTA v1.1** — PRD chính thức (`DOC-v1.1-01`) chốt định nghĩa khớp tuyến (`BR04-01/02`), chu kỳ quét (`NFR-04` ≤60s), 3 ngưỡng NFR mới (concurrency `NFR-06`, realtime `NFR-08`, security API `NFR-11`), và **đảo kết luận** trần thông báo khớp (`BR04-04`: theo ngày/người dùng thay vì theo tin OFFER). +1 REQ mới (`REQ-ASN-013`), +1 SC mới (`SC-ASN-019`), 4 REQ + 5 SC MODIFIED. Resolve `RISK-ASN-04`/`RISK-ASN-06`; mở `RISK-ASN-08` (nợ giá trị cấu hình) | `DOC-v1.1-01` §8.3/§8.4/§9 | `RISK-ASN-04`/`RISK-ASN-06` đóng; `SC-ASN-014` đảo kết luận v1.0; `SC-ASN-006`/`SC-ASN-008` có ngưỡng NFR cho automation |
| 2026-09-15 | UPDATE | Bổ sung UI reference (`00_input/v1.1/design/ASN_01..03`, demo `foxeco_demo/FoxEcoQC`) — xác nhận cấu trúc màn "Bảng tin" (`SC-ASN-015`), "Chi tiết tin" + nút "Tôi mang giúp được" (`SC-ASN-006` nhánh a), và form "Tôi nhận giao hàng" đúng 2 field PRD mới mô tả (Khoảng thời gian + Buổi, đủ 4 lựa chọn buổi kể cả "Giờ nào cũng được") khớp `BR04-01/02`. **Không phát sinh CL mới, không resolve CL nào** — `C-ASN-03`/`C-NTF-02` (home ASN) không đổi vì ảnh chỉ xác nhận cấu trúc UI (§Custom Rules §10.1), không chạm tới câu hỏi nghiệp vụ của 2 CL đó (đa đơn song song / tham số vận hành khớp tuyến) | Vibe-check thủ công qua Playwright, theo yêu cầu QC GiangDC2 2026-09-15 | Không ảnh hưởng generate-tc — chỉ là bằng chứng UI-match bổ sung |
| 2026-09-15 | ĐÍNH CHÍNH | Frontmatter `counts:` của `risk_assessment.md` đang là **delta-only** (`cl: 0` · `risk: 1`) ⇒ sửa về cumulative `cl: 2` (`C-ASN-03` Open · `C-NTF-02` Partially Resolved — cả 2 home ở ASN) · `risk: 8` (v1.0 `RISK-ASN-01..07` + `RISK-ASN-08` mới). `test_scenario_map.md` **đã đúng**, không sửa | `health-check` 2026-09-15 G-02; thống nhất nghĩa `counts:` = cumulative | `cl_open + cl_resolved = 1 < cl = 2` là **đúng**: `C-NTF-02` ở trạng thái *Partially Resolved*, không thuộc 2 ô đó |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — thư mục dùng lại qua nhiều sprint, phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | ⚠️ **`SC-ASN-014` nay là rule "5 thông báo / 1 tin OFFER"** — ⛔ không còn trần theo ngày; ⛔ không gộp với `SC-ASN-013` (trần gợi ý 5 tin) cho tới khi `C-ASN-04` xác nhận 2 rule là một | BA 2026-09-16 bỏ trần/ngày; con số 5 trùng với `BR03-06` nhưng chưa rõ cùng rule | Gộp nhầm ⇒ test 1 rule, bỏ sót rule kia; tách nhầm ⇒ 2 TC kiểm cùng 1 hành vi |
| 3 | ⚠️ **`NFR-06`/`NFR-08`/`NFR-11` cần công cụ ngoài UI thuần** (concurrency tool · đa thiết bị đồng bộ · API client) | PRD chỉ định phương pháp đo cụ thể (Concurrency test / Integration test đa thiết bị / Security test) | Test tay không đo được ngưỡng → PASS giả trên case không đại diện |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"trần thông báo khớp tính theo NGÀY, gộp cho một người dùng, do admin cấu hình"** (bản v1.1 2026-09-15, theo `BR04-04`) **HẾT HIỆU LỰC 2026-09-16** — BA: *"Không có ngưỡng ngày, tài liệu bị dư"*. Hiện hành: **5 thông báo / 1 tin đăng OFFER** (chi tiết chờ `C-ASN-04`). ⚠️ Đây là lần đảo **thứ hai** của cùng rule (v1.0 theo tin OFFER → v1.1 PRD theo ngày → nay lại theo tin đăng).


⛔ Kết luận **"trần thông báo khớp tính RIÊNG theo từng tin OFFER"** (bản v1.0, `KB-ASN-03`, BA 2026-07-29) **HẾT HIỆU LỰC kể từ v1.1 — đừng trích lại**; hiện hành là **trần tính theo NGÀY, gộp cho MỘT NGƯỜI DÙNG** (`DOC-v1.1-01 §8.4 BR04-04`), giá trị số "do admin cấu hình" — chưa có trong tài liệu.

⛔ Kết luận **"tiêu chí độ gần tuyến vô hiệu vì nhị phân, chỉ còn thời gian đăng"** (`RISK-ASN-06` bản v1.0) **HẾT HIỆU LỰC** — hiện hành là **độ gần tuyến vẫn là tầng ưu tiên số 1** (dù nhị phân), thời gian đăng chỉ là tầng 2 khi 2 tin cùng trùng tuyến (`DOC-v1.1-01 §8.3 BR03-06`).

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 `C-ASN-04` + `C-ASN-05` (mới 2026-09-16) — rule 5 thông báo chưa đủ định nghĩa; phép so "trùng điểm" với địa chỉ tự do chưa định nghĩa | Open — `C-ASN-05` chặn dựng data cho `SC-ASN-011` (4 nhánh) | Hỏi BA (sheet `ASN`) **trước `generate-tc`**; hỏi chung quy tắc so sánh địa chỉ với `RISK-ORD-12` |
| 2 | 🟡 `SC-ASN-019` cần công cụ gọi API trực tiếp (Postman/tương đương) | Chưa có kế hoạch môi trường | Lên kế hoạch trước khi `vibe-test`/`execute-maintain` chạy nhánh security |

## 4. Vibe Status — kết quả thực thi trên STG

> ⚠️ **Vì sao ghi ở đây, không ở `v1.1/MEMORY.md §4`:** router v1.1 theo layout `module-first v2` **chỉ có**
> §1 Function Register + §2 Module Summary (`CLAUDE.md §MEMORY Files`) — không có §4 Vibe Status.
> Sổ cái verdict per-TC canonical là **`08_test-runs/vibe/coverage/coverage-ASN.md`**; mục này là bản trỏ đường.

**Trạng thái module sau VR-009 (2026-09-19):**

| Chỉ số | Giá trị |
|---|---|
| SCOPE_TOTAL | **26 TC** = 13 (v1.1) + 21 (CARRIED v1.0) − 8 ID trùng *(lấy bản v1.1)* |
| ✅ PASS | **15** |
| ⛔ N-A | **2** (`TC-ASN-024` concurrency API · `TC-ASN-026` API + audit log) |
| ⏳ NOT_RUN | **9** |
| ❌ FAIL / 🚫 BLOCKED / ⚠️ NOT_EVIDENCED | **0 / 0 / 0** |
| **Có verdict cuối** | **17/26** ⇒ §8 = **PARTIAL** |

| Phiên | Ngày | TC thu verdict |
|---|---|---|
| `VR-007` | 2026-09-19 | 3 — `013` · `021` · `023` |
| `VR-008` | 2026-09-19 | 5 — `001` · `002` · `003` · `004` · `009` |
| **`VR-009`** | 2026-09-19 | **7** — `005` · `007` · `010` · `011` · `012` · `020` · `022` |

**9 TC còn nợ + lý do:**

| TC | Lý do |
|---|---|
| `014` `015` `016` `017` `018` `025` | Hết sức phiên — nhóm trần/thứ tự gợi ý cần **tuyến OFFER mới sạch + 3–6 tin NEED + 3 lượt đổi tài khoản**; ⛔ không bị chặn kỹ thuật |
| `006` · `008` | Cần **2–3 thiết bị** (bấm cách <2s / đo ≤5s) — máy chỉ có 1 AVD. **QC chốt 2026-09-19: giữ `NOT_RUN`** |
| `019` | Cần dev/QA lùi `Đến ngày` để có tin **Hết hạn** — ⛔ không tạo được qua UI |

### 🔴 Spec-gap phát hiện khi vibe-test — cần route `/analyze-requirements --update`

> **Vòng đời / hết hiệu lực của THÔNG BÁO GỢI Ý khớp tuyến hiện KHÔNG có scenario nào mô tả.**
> Quan sát VR-009 (2026-09-19, ⚠️ **giả thuyết chưa chốt**): lúc **14:49** chuông của tài khoản B có **3** thông báo
> `Tìm thấy đơn hàng phù hợp tuyến của bạn` — tất cả thuộc các tin buổi **`Sáng (8–12h)`**; sau đó nhóm `HÔM NAY`
> **rỗng**, và **`force-stop` + relaunch app vẫn rỗng** ⇒ ⛔ không phải lỗi refresh phía client.
>
> Đối chứng ngược cùng phiên (15:46): thông báo của tin **đã được ghép** thì **VẪN CÒN** trong danh sách
> (chỉ chuyển sang trạng thái *đã đọc*) ⇒ **việc bị ghép KHÔNG phải nguyên nhân biến mất**.
>
> ⇒ Nghi vấn: **thông báo gợi ý hết hiệu lực khi khung giờ khớp trôi qua.**
> `test_scenario_map.md` hiện chỉ mô tả **điều kiện SINH** thông báo (`SC-ASN-011`, `SC-ASN-014` trần 5) và
> **thứ tự** (`SC-ASN-015`), ⛔ **không có SC nào** cho *thời điểm thông báo mất hiệu lực / bị gỡ*.
> Đây đúng loại spec-gap mà `SKILL.md §Phản hồi ngược` yêu cầu đưa về `analyze-requirements`, ⛔ không chỉ ghi vào MEMORY.
>
> 📌 Lệnh đề xuất:
> `/analyze-requirements --update "Vòng đời thông báo gợi ý khớp tuyến: thông báo có tự hết hiệu lực/bị gỡ khi khung giờ (buổi) của tin trôi qua không? Quan sát VR-009 2026-09-19: 3 thông báo của các tin buổi Sáng biến mất sau 12h, force-stop+relaunch vẫn mất; trong khi thông báo của tin ĐÃ GHÉP thì vẫn còn (chỉ đổi sang đã đọc)."`

### 📨 Sai lệch tài liệu ↔ app (đề nghị QC/BA sửa TC, ⛔ không phải bug app)

| TC | Tài liệu ghi | App thật | Bằng chứng |
|---|---|---|---|
| `TC-ASN-010` | nút **`"Nhận giao"`** | **`Tôi mang giúp được`** | `find textContains("Nhận giao")` 🚫 **NOT FOUND**; nghiệp vụ chạy đúng ⇒ TC vẫn **PASS** |
| `TC-ASN-012` | khung giờ `08:00–09:00` vs `20:00–21:00` | app dùng **khoảng NGÀY + tập BUỔI**, ⛔ không nhập giờ tự do | đã hiện thực đúng *ý định* TC bằng khoảng ngày (Hôm nay vs 22/09) |
| `TC-ASN-021` | loại hàng `"Giấy tờ, hồ sơ"` | `Tài liệu` (`C-ORD-09`) | VR-007 |
| fragment `§0` | buổi *"Sáng (6–12h)"* | **`Sáng (8–12h)`** | xác nhận **3 lần** (VR-007/008/009) |
