---
id: v1.0/FEED-bang-tin/risk
title: Risk Assessment — v1.0 · Module FEED
type: risk-assessment
version: v1.0
sprint: 1
module: FEED
counts:
  cl: 7
  risk: 5
  cl_open: 1
  cl_resolved: 6
status: ANALYZED
updated: 2026-09-17
---

# Risk Assessment — v1.0 · Module FEED

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module FEED.
> 🔑 Frontmatter `counts:` = nguồn canonical CL/RISK — **chỉ đếm CL có home ở module này**; CL tham chiếu (home ở module khác) KHÔNG tính vào `counts`. **Layout v2 ⇒ đây là home của Clarification.**
> ℹ️ `cl_open (1) + cl_resolved (6) = 7 = cl (7)` — cập nhật 2026-09-17 sau BA trả lời `C-FEED-02..04`; mở `C-FEED-05`.

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| FEED | **High** | Chứa **2 vi phạm rule đã được BA xác nhận là bug** ngay trên bề mặt công khai: **lộ SĐT trước khi ghép** (`BR-CON-02`) và **cho chủ tin tự nhận đơn của mình** (`OPR-05`). Cả hai chưa được log bug ở đợt cũ |

## Chi tiết rủi ro (bảng hợp nhất)
| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-FEED-01 | FEED / Bảo mật liên hệ | **SĐT người gửi hiển thị công khai từ trạng thái "Chờ ghép"** — vi phạm `BR-CON-02`+`OPR-07`; bất kỳ CBNV nào xem bảng tin cũng lấy được SĐT mà không cần ghép | **High** | `DOC-v1.0-02` §3.4 đoạn lưu ý · §7 dòng 1 · phán quyết `C-ASN-01` Resolved | `SC-FEED-010` — assert theo rule, dự kiến FAIL | Log bug ngay khi execute (chưa log ở đợt cũ); ⛔ không sửa expected cho PASS | Open | REQ-FEED-006, SC-FEED-010 |
| RISK-FEED-02 | FEED / Logic vai trò | **Chủ tin và Người nhận của đơn vẫn bấm được "Tôi mang giúp được"** — vi phạm `OPR-05`; tạo được cặp ghép người gửi = người vận chuyển | **High** | `DOC-v1.0-02` §3.3 đoạn 5 · §7 dòng 9 · phán quyết `C-ASN-02` Resolved | `SC-FEED-011`, `SC-FEED-012` — assert theo rule, dự kiến FAIL | Log bug; kiểm chéo với `SC-ASN-012` (rule phía engine) | Open | REQ-FEED-007, SC-FEED-011, SC-FEED-012 |
| RISK-FEED-03 | FEED / Nhãn loại hàng | Danh mục "Loại hàng" từng lệch 3 nguồn (BRD 5 giá trị · PRD 8 chip có "Tài liệu" · app STG mặc định "Giấy tờ, hồ sơ"). **BA chốt 2026-09-16: nhãn chuẩn "Tài liệu"** | High → **Resolved** | `DOC-v1.1-01` §8.1.4 · BA trả lời `C-ORD-09` 2026-09-16 (home `ORD`) | Assert nhãn **"Tài liệu"** trên card/chi tiết | App hiện "Giấy tờ, hồ sơ" ⇒ log bug UI | **Resolved** | REQ-FEED-001, SC-FEED-002 |
| RISK-FEED-04 | FEED / Vị trí CTA | *(cập nhật Status)* `US-D07` nói nút "Tôi mang giúp được" có **ngay tại thẻ tin** hoặc màn chi tiết; `§3.3` liệt kê 6 thành phần card **không có nút** ⇒ TC completeness card có thể assert thừa/thiếu nút | Medium → **Resolved** | `DOC-v1.0-01` §D1b `US-D07` L176 vs `DOC-v1.0-02` §3.3 đoạn 3 · vibe-check demo 2026-09-16 | `SC-FEED-002` (hết gap, assert cứng KHÔNG có CTA trên card) | Vibe-check qua demo xác nhận card **không có** nút CTA; nút chỉ có ở màn Chi tiết tin — khớp Nguồn B (`§3.3`), bác `US-D07` phần "ngay tại thẻ tin" | **Resolved** | REQ-FEED-004, SC-FEED-002 |
| RISK-FEED-05 | FEED / Bản đồ | Khung "Bản đồ · ~X km" trên demo là placeholder tĩnh — không rõ bản chính thức có bản đồ thật. **BA 2026-09-16: CÓ hiển thị bản đồ thật**; một số văn phòng **thiếu location** thì không hiển thị được map — sẽ cấp file data khi test | Medium | `DOC-v1.0-02` §3.4 · §7 dòng 10 · BA trả lời `C-FEED-01(b)` 2026-09-16 | `SC-FEED-009` — viết lại: bản đồ thật + nhánh văn phòng thiếu location | Chờ file data văn phòng thiếu location + hành vi UI khi thiếu (`C-FEED-02`) | Resolved (hành vi nhánh thiếu location → `C-FEED-02`) | REQ-FEED-005, SC-FEED-009 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-ASN-01 | SĐT lộ lúc nào? (bề mặt Chi tiết tin) | ✅ Resolved — **chỉ sau khi ghép**; hành vi prototype là bug | 2026-07-27 | REQ-FEED-006 |
| C-ASN-02 | Chủ tin có tự nhận mang giúp tin của mình được không? | ✅ Resolved — **KHÔNG**; hành vi prototype là bug | 2026-07-27 | REQ-FEED-007 |
| C-FEED-01 | Vị trí nút CTA (card vs chi tiết) + bản đồ thật hay placeholder | ✅ **Resolved 2026-09-16** — (a) CTA **chỉ ở Chi tiết tin** (demo + BA); (b) **có bản đồ thật**, văn phòng thiếu location thì không hiện map (BA) | mở 2026-09-07 | REQ-FEED-004, REQ-FEED-005 |
| C-ORD-06 | Text empty state (mở rộng sang màn Bảng tin) | ✅ **Resolved 2026-09-15 ở home `ACT`** — `EMP-04`: "Chưa có tin nào" + gợi ý mở rộng khu vực hoặc đăng tin + CTA "Đăng tin" (tham chiếu, không đếm ở đây) | kế thừa 2026-07-29 | REQ-FEED-009 |
| C-FEED-02 | Văn phòng **thiếu location**: khung bản đồ hiện gì; khoảng cách "~X km" tính từ đâu | ✅ **Resolved 2026-09-17** — placeholder + thông báo · thiếu ⇒ **0 km** · km từ điểm nhận → điểm giao · **ảnh tĩnh có vẽ tuyến** · data đã cấp (lỗi data → `C-FEED-05`) | 2026-09-16 | REQ-FEED-005, SC-FEED-009 |
| C-FEED-03 | Bảng tin "cả hai tab" (`EMP-04`) là 2 tab nào; lọc / tìm kiếm / "mở rộng khu vực" hoạt động ra sao | ✅ **Resolved 2026-09-17** — **1 danh sách, không tab, không lọc/tìm kiếm** (như demo); vế "mở rộng khu vực" chuyển `C-HOME-04` vòng 2 | 2026-09-16 | REQ-FEED-001, REQ-FEED-009, SC-FEED-001, SC-FEED-013 |
| C-FEED-04 | Trước khi ghép, Chi tiết tin hiện những gì: tên người gửi/người nhận? địa chỉ đầy đủ hay rút gọn (`AC-13.1.02` ⟷ `NFR-10`)? | ✅ **Resolved 2026-09-17** — **chỉ ẩn SĐT**; tên hiện; địa chỉ hiện **đầy đủ theo data đã gửi** (PRD `BR03-03`/`NFR-10` chưa cập nhật) | 2026-09-16 | REQ-FEED-004, REQ-FEED-006, SC-FEED-007, SC-FEED-010 |
| C-FEED-05 | File `location_address_catalog.xlsx`: 399/399 dòng `coordinate_status = MISSING`, 61 dòng thiếu lat/lng, 34 dòng toạ độ ngoài Việt Nam — bản đồ/"km" lấy toạ độ từ đâu; chỉ 1 trong 2 điểm thiếu thì hiện gì | 🔴 **Open (mới 2026-09-17)** | 2026-09-17 | REQ-FEED-005, SC-FEED-009, SC-FEED-015 |

### C-ASN-01 · Thời điểm lộ SĐT — rule vs prototype

**Source Quote (ambiguous):**
> Nguồn A — RULE (`DOC-v1.0-01` §A5 `BR-CON-02` L78): "Sau khi ghép: lộ SĐT + kênh liên hệ cho đúng 2 người trong cặp ghép; trước khi ghép không lộ SĐT"
> Nguồn B — HÀNH VI (`DOC-v1.0-02` §7 dòng 1): "Thời điểm lộ SĐT chưa nhất quán | Banner "Đăng tin mới" nói SĐT chỉ lộ SAU KHI ghép, nhưng "Chi tiết tin" đã hiện sẵn SĐT + nút Gọi của Người gửi ngay từ trạng thái "Chờ ghép"."

**Source Location:** `DOC-v1.0-01 §A5 · bảng Rule/Mô tả · L78` (và `§D7 OPR-07 · L343`) ⟷ `DOC-v1.0-02 §3.4 · đoạn lưu ý cuối` · `§7 · dòng 1`

**Analyst Note:** BA/PO chốt 2026-07-27: **rule chính thức = lộ sau ghép**, hành vi prototype là **bug** (`DOC-v1.0-06` KP-01 §4 KB-ASN-01). Đủ chuẩn `Resolved` theo `KP-02 §6` (câu trả lời BA có ngày + 2 rule BRD đồng thuận). ⇒ SC viết theo rule; FAIL trên app là **bug thật cần log**, không phải TC sai. Đây là lý do `SC-FEED-010` để P1 dù chỉ là hành vi hiển thị.

### C-ASN-02 · Chủ tin / người nhận tự nhận đơn của mình

**Source Quote (ambiguous):**
> Nguồn A — RULE (`DOC-v1.0-01` §D7 `OPR-05` L341): "Không tự khớp với chính mình | Không gợi ý tin do chính người đó đăng; người gửi ≠ người vận chuyển của cùng một đơn"
> Nguồn B — HÀNH VI (`DOC-v1.0-02` §3.3 đoạn 5): "Tin của chính Người gửi vẫn hiển thị trong Bảng tin và khi mở Chi tiết tin vẫn thấy nút "Tôi mang giúp được"… cần rà soát logic ẩn nút khi người xem chính là chủ tin."

**Source Location:** `DOC-v1.0-01 §D7 · bảng ID/Rule/Mô tả · L341` ⟷ `DOC-v1.0-02 §3.3 · đoạn 5` · `§7 · dòng 9`

**Analyst Note:** BA/PO chốt 2026-07-27: **không được phép**; prototype là bug. ⚠️ **Ghi rõ phạm vi** (`DOC-v1.0-06` KP-01 §4 KB-ASN-02): bug ở màn **Chi tiết tin (public)**; màn **Theo dõi đơn đã role-aware đúng**. Lưu ý `OPR-05` có **2 mệnh đề**: (a) không **gợi ý** tin của chính mình (thuộc engine — `SC-ASN-012`), (b) người gửi ≠ người vận chuyển cùng đơn (thuộc bề mặt — `SC-FEED-011`). Hai mệnh đề, hai module, đừng gộp.

### C-FEED-01 · 🟡 Vị trí CTA + bản đồ thật hay placeholder *(PARTIALLY RESOLVED 2026-09-16)*

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-01` §D1b `US-D07` L176): "Là Carrier, tôi muốn bấm "Tôi mang giúp được" **ngay tại thẻ tin hoặc màn chi tiết**, để gửi đề nghị nhanh cho Sender."
> Nguồn B (`DOC-v1.0-02` §3.3 đoạn 3): "Mỗi card: icon/ảnh hàng, loại hàng | giá trị, badge "Tin của bạn" nếu là tin tự đăng, thời gian đăng, "Nhận:"/"Giao:" rút gọn, khung giờ." *(không có nút CTA)*
> Nguồn C (`DOC-v1.0-02` §7 dòng 10): "Bản đồ chỉ là placeholder | … cần xác nhận phạm vi bản chính thức có tích hợp bản đồ thật (GPS/Google Maps) hay không."

**Source Location:** `DOC-v1.0-01 §D1b · US-D07 · L176` ⟷ `DOC-v1.0-02 §3.3 · đoạn 3` · `§7 · dòng 10`

**Analyst Note (2026-09-07):** Hai câu hỏi gộp 1 CL vì cùng bề mặt Bảng tin/Chi tiết tin và cùng cần 1 lượt BA:
**(a)** Nút *"Tôi mang giúp được"* có xuất hiện **trên card** ở Bảng tin (theo `US-D07`) hay chỉ ở màn Chi tiết tin (theo `§3.3`)? Ảnh hưởng TC completeness card + số bước của luồng ghép.
**(b)** Bản chính thức v1.0 có tích hợp bản đồ thật không, hay giữ placeholder? Chính doc đặt câu hỏi này.
**Non-blocking** — `SC-FEED-002` đã cố ý không assert CTA, `SC-FEED-009` assert trạng thái hiện tại.

↳ **Cập nhật 2026-09-16 — vế (a) Resolved qua demo:** Vibe-check trực tiếp qua demo `https://giangdc.github.io/foxeco_demo/FoxEcoQC` (vai Carrier), dùng Playwright:
> Ảnh `00_input/v1.1/design/FEED_01_bangtin_carrier_khongco_CTA.png` — màn Bảng tin (vai Carrier): mỗi card chỉ hiện icon/ảnh hàng, loại hàng | giá trị, thời gian đăng, "Nhận:"/"Giao:", khung giờ, cân nặng/kích thước. **KHÔNG có nút CTA nào trên card.**
> Ảnh `00_input/v1.1/design/FEED_02_chitiettin_cta_va_bandoplaceholder.png` — mở 1 tin từ Bảng tin sang màn **Chi tiết tin**: có đầy đủ thông tin hàng, lộ trình, khung giờ, người gửi + nút gọi, và nút cam to **"Tôi mang giúp được"** ở cuối màn.

**Analyst Note:** Bằng chứng khớp chính xác **Nguồn B** (`§3.3` — card không có nút), bác bỏ cách đọc "ngay tại thẻ tin" của **Nguồn A** (`US-D07`). ⇒ **Resolve (a) theo hành vi thật**: CTA *"Tôi mang giúp được"* **chỉ** có ở màn Chi tiết tin, không có trên card Bảng tin. `SC-FEED-002` hết gap, có thể assert cứng "card KHÔNG có CTA" thay vì cố ý bỏ qua như trước.
⚠️ Vẫn khuyến nghị double-check nhanh trên STG thật trước khi hardening automation locator (đúng caveat chung khi dùng demo làm nguồn), nhưng với 2 ảnh đối chứng trực tiếp (card vs chi tiết), **không coi là blocker** cho `generate-tc`.

**Vế (b) vẫn Pending — KHÔNG resolve được qua demo:** demo chỉ cho biết **hiện trạng đang là placeholder tĩnh** (ảnh `FEED_02` ở trên: khung "Bản đồ · ~8 km" chỉ là icon + text, không phải bản đồ tương tác, không có route/marker). Điều đó **không trả lời được** câu hỏi thật của `RISK-FEED-05`: *bản chính thức v1.0 có DỰ ĐỊNH tích hợp bản đồ thật hay không* — đây là quyết định phạm vi sản phẩm, không phải hành vi có thể quan sát qua demo. **Giữ nguyên Pending, cần hỏi BA/PM.**

### C-ORD-06 · Text empty state (mở rộng sang Bảng tin)

**Source Quote (ambiguous):** *(Không có quote — chính sự thiếu vắng là nội dung của clarification)*

**Source Location:** `DOC-v1.0-06 KP-02 §5 · dòng "C-ORD-06"` · `KP-05 §3 · dòng 4`

**Analyst Note:** CL này gốc mở cho 3 màn (Hoạt động · Quà đã nhận · Thông báo), **từng Resolved 2026-07-28 rồi REVERT về Open 2026-07-29** vì rà lại 82 ảnh Figma + BRD + PRD **không tìm thấy bằng chứng nào** cho text *"Hiện tại chưa có dữ liệu"* (`KP-02 §5`). Lượt này **mở rộng phạm vi sang màn Bảng tin** (`SC-FEED-013`) và **Trang chủ** (`SC-HOME-024`) — cùng bản chất, cùng 1 câu trả lời của BA. Home canonical của CL này ở `ACT-hoat-dong/risk_assessment.md`; đây là bản tham chiếu.

### C-FEED-01 · ↳ BA trả lời 2026-09-16 *(→ RESOLVED cả 2 vế)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `FEED` · cột "Câu trả lời BA" · 2026-09-16

> "a, chỉ xuất hiện ở chi tiết tin
> b. có hiển thị được map nhé (sẽ có vài case không hiển thị được map cho data văn phòng bị thiếu location ) → khi test sẽ được cung cấp file data"

↳ **Ghi chú:** (a) BA xác nhận đúng kết luận demo 2026-09-16: nút *"Tôi mang giúp được"* **chỉ** ở màn Chi tiết tin. ⚠️ `DOC-v1.1-01 AC-12.1.01`/`US12` vẫn viết *"tại thẻ tin **hoặc** màn chi tiết tin"* ⇒ **PRD chưa cập nhật** (cùng kiểu `C-ACT-02`); TC theo BA. (b) **Đảo kết luận `SC-FEED-009`**: bản chính thức **có bản đồ thật** — không còn là placeholder tĩnh. Có nhánh **văn phòng thiếu location** ⇒ không hiện được map; data test do BA cấp. Hành vi UI của nhánh này chưa rõ → `C-FEED-02`.
⚠️ Hệ quả phụ cho module **không có delta**: PRD v1.1 thực ra **có** chạm bề mặt Bảng tin/Chi tiết tin (`AC-12.1.01`, `AC-13.1.02`, `AC-03.1.01` carousel, `BR18-04` copy nhanh, `EMP-04`, ảnh bắt buộc `BR01-01` làm `SC-FEED-008` *"tin không ảnh"* chỉ còn áp cho dữ liệu cũ) — xem `CHANGELOG §3`.

### C-FEED-02 · Bản đồ khi văn phòng thiếu location *(RESOLVED 2026-09-17 — xem ↳ BA trả lời)*

📍 BA trả lời `C-FEED-01(b)` 2026-09-16 · `DOC-v1.0-02 §3.4` (khung "Bản đồ · ~X km")

↳ **Ghi chú:** BA nói *"vài case không hiển thị được map cho data văn phòng bị thiếu location"* nhưng không nói **hiển thị gì thay thế**: (a) ẩn hẳn khung bản đồ, (b) hiện placeholder + thông báo, hay (c) hiện map chỉ 1 điểm? (d) Dòng **"~X km"** tính theo toạ độ văn phòng — thiếu location thì ẩn hay hiện "—"? (e) Bản đồ **tương tác** (zoom/pan, mở Google Maps) hay ảnh tĩnh có vẽ tuyến? (f) Xin **file data** văn phòng thiếu location trước `generate-tc` để viết Given cụ thể.

### C-FEED-03 · Hai tab + lọc/tìm kiếm của Bảng tin *(RESOLVED 2026-09-17 — xem ↳ BA trả lời)*

📍 `DOC-v1.1-01 §8.17.1 EMP-04 · trang 51` · `§7.1 "Danh sách tin NEED (lọc/tìm kiếm)" · trang 30` · `§6.2 AC-20.1.01 · trang 24`

> `EMP-04`: "Bảng tin (cả hai tab) | "Chưa có tin nào" + gợi ý mở rộng khu vực hoặc đăng tin | "Đăng tin""

> `AC-20.1.01`: "Tin OFFER không xuất hiện ở bất kỳ tab nào của bảng tin và không tìm được."

↳ **Ghi chú:** PRD nói Bảng tin có **2 tab** và có **lọc/tìm kiếm**, nhưng không đặc tả gì thêm; `SC-FEED-001` (v1.0) không ghi nhận tab nào, demo `FEED_01` chỉ thấy 1 danh sách. **Hỏi:** (a) 2 tab là gì (vd "Gợi ý cho bạn" / "Tất cả")? (b) Có ô tìm kiếm / bộ lọc nào (theo khu vực, ngày, loại hàng)? (c) *"Gợi ý mở rộng khu vực"* là nút hay chỉ là câu chữ? Liên quan `C-HOME-04`. Theo `§Custom Rules §10.2`, nếu có 2 tab thì **mỗi tab cần ≥1 SC riêng** — hiện chưa có.

### C-FEED-04 · Thông tin hiển thị trước khi ghép *(RESOLVED 2026-09-17 — xem ↳ BA trả lời)*

📍 `DOC-v1.1-01 §6.2 AC-13.1.02 · trang 21` ⟷ `§9 NFR-10 · trang 54` · `§8.3.1 BR03-03 · trang 36`

> `AC-13.1.02`: "Không hiển thị số điện thoại của người gửi và người nhận. Chỉ hiển thị thông tin đủ để quyết định: loại hàng, khối lượng, kích thước, ảnh, điểm lấy/giao, khoảng ngày · buổi, phòng ban người gửi."

> `NFR-10`: "Số điện thoại và địa chỉ chỉ trả về cho đúng hai người trong cặp ghép (và admin); kiểm tra quyền ở tầng máy chủ, không chỉ ẩn trên giao diện."

> `BR03-03`: "Sau khi ghép, lộ họ tên · số điện thoại · phòng ban cho đúng hai người trong cặp…"

↳ **Ghi chú:** (a) `AC-13.1.02` liệt kê **"phòng ban người gửi"** nhưng **không** có **họ tên**; `BR03-03` nói *họ tên* chỉ lộ **sau** ghép ⇒ trước ghép **ẩn tên** người gửi? (demo `FEED_02` đang hiện tên + nút gọi.) Tên **người nhận** có hiện? (b) `AC-13.1.02` cho hiện **"điểm lấy/giao"** trước ghép, `NFR-10` lại nói **địa chỉ** chỉ trả cho cặp ghép ⇒ trước ghép hiện **địa chỉ đầy đủ** hay chỉ **rút gọn** (quận/toà nhà)? Ảnh hưởng trực tiếp `SC-FEED-007` và `SC-FEED-010` (P1, bug lộ SĐT) — phạm vi "thông tin nhạy cảm trước ghép" hiện chỉ gồm SĐT.

### C-FEED-02 · ↳ BA trả lời 2026-09-17 *(→ RESOLVED)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `FEED`

> "a, hiển placehoder + thông báo (nhưng case này do data sai thôi có thể ko cần viết tc đâu)
> b. thiếu thì hiện 0km , tính từ điểm nhận đến điểm giao
> c. ảnh tĩnh có vẽ tuyến
> d. cung cấp r nhé"

↳ **Ghi chú:** (a) Văn phòng thiếu location ⇒ **placeholder + thông báo**; BA cho phép **không viết TC** vì là lỗi data ⇒ `SC-FEED-015` giữ **P3**, `generate-tc` có thể bỏ qua (ghi rõ lý do). (b) Khoảng cách tính **từ điểm nhận tới điểm giao**; thiếu toạ độ ⇒ **"0km"** — nhánh này **assert được** (giá trị cố định), khác ràng buộc #5 *"không assert ~X km"* (vẫn áp cho nhánh có toạ độ). (c) Bản đồ là **ảnh tĩnh có vẽ tuyến** — ⛔ không test zoom/pan/mở Google Maps. (d) Đã nhận file (`DOC-v1.1-04`). ⚠️ Rà file phát hiện dữ liệu toạ độ lỗi diện rộng ⇒ mở `C-FEED-05`.

### C-FEED-03 · ↳ BA trả lời 2026-09-17 *(→ RESOLVED)*

> "a. Chỉ có 1 dánh danh đâu có tab gì
> b. không có gì như demo đang đúng r
> c. "

↳ **Ghi chú:** Bảng tin = **1 danh sách, không tab, không ô tìm kiếm/bộ lọc** (khớp demo `FEED_01`). ⇒ `§Custom Rules §10.2` (mỗi tab 1 SC) **không áp dụng**; `SC-FEED-001` giữ nguyên. PRD `EMP-04` *"cả hai tab"*, `§7.1` *"lọc/tìm kiếm"*, `AC-20.1.01` *"không tìm được"* ⇒ **PRD chưa cập nhật** (đề nghị BA sửa — sheet `FEED`). Vế (c) *"gợi ý mở rộng khu vực"* BA để trống; vì BA nói tin load toàn quốc (`C-HOME-04(d)`) nên khả năng câu này thừa ⇒ gộp hỏi ở `C-HOME-04` vòng 2. `SC-FEED-013` bỏ chữ *"cả hai tab"*, ⛔ chưa assert câu *"gợi ý mở rộng khu vực"*.

### C-FEED-04 · ↳ BA trả lời 2026-09-17 *(→ RESOLVED)*

> "a, chỉ ẩn sdt thôi mà ?? đâu có rule ẩn tên
> b. hiên thị theo data đã gởi"

↳ **Ghi chú:** Trước ghép, Chi tiết tin **hiện họ tên** (người gửi) + **địa chỉ lấy/giao đầy đủ theo data đã đăng**; **chỉ ẩn SĐT** (và nút Gọi — `SC-FEED-010` giữ nguyên, vẫn P1). ⇒ `SC-FEED-007` thêm assert *cụm Người gửi có tên, không SĐT*. ⚠️ PRD `BR03-03` (*"Sau khi ghép, lộ họ tên · số điện thoại · phòng ban"*) và `NFR-10` (*"Số điện thoại **và địa chỉ** chỉ trả về cho đúng hai người trong cặp ghép"*) **ngược câu BA** ⇒ đưa vào dòng đề nghị cập nhật PRD. ⛔ Không log bug vì tên/địa chỉ hiện trước ghép.

### C-FEED-05 · Dữ liệu toạ độ văn phòng lỗi *(OPEN — mới 2026-09-17)*

📍 `00_input/v1.1/location_address_catalog.xlsx` (`DOC-v1.1-04`) ⟷ BA trả lời `C-FEED-02(b)`

↳ **Ghi chú:** Rà file BA cấp: **cả 399 dòng** có `coordinate_status = MISSING`; **61 dòng** thiếu lat/lng; **34 dòng** toạ độ nằm ngoài Việt Nam (vd `51.93, -8.62`). Nếu app lấy toạ độ từ file này thì gần như **mọi** tin sẽ rơi vào nhánh placeholder/"0km" — không dựng được Given *"văn phòng có location"* cho `SC-FEED-009`. **Hỏi:** (a) Toạ độ bản đồ lấy từ đâu (cột lat/lng file này, geocode địa chỉ, hay DB khác)? `coordinate_status = MISSING` nghĩa là gì? (b) 34 dòng toạ độ ngoài VN: app vẽ sai vị trí hay coi là thiếu? (c) Chỉ **1 trong 2** điểm thiếu toạ độ ⇒ vẫn "0km" + placeholder? (d) Xin danh sách **cặp văn phòng mẫu**: 1 cặp đủ toạ độ đúng · 1 cặp thiếu toạ độ.

## Khuyến nghị tổng thể
1. ✅ **`RISK-FEED-03` Resolved 2026-09-16** — nhãn Loại hàng chuẩn là "Tài liệu" (`C-ORD-09`). *(2026-09-17)* `C-FEED-02..04` Resolved; blocker còn lại trước generate-tc: **`C-FEED-05`** (toạ độ văn phòng lỗi — không dựng được Given bản đồ thật).
2. **Ưu tiên test P1 high-risk:** `SC-FEED-010` (SĐT trước ghép) và `SC-FEED-011` (CTA với chủ tin) — chạy sớm để **log 2 bug đã biết mà đợt cũ chưa log** (`KP-05 §5`).
3. **Cần môi trường/dữ liệu:** 3 tài khoản (chủ tin · người xem · người nhận) + 1 tin OFFER để verify không lên bảng tin. Không có tài khoản thứ ba thì `SC-FEED-012` blocked.
4. ✅ **`C-FEED-01(a)` đã Resolved 2026-09-16 qua demo** — CTA "Tôi mang giúp được" chỉ ở màn Chi tiết tin, không trên card; dùng luôn cho locator automation sau này.
5. ✅ **`C-FEED-01(b)` Resolved 2026-09-16 (BA)** — **có bản đồ thật**; văn phòng thiếu location thì không hiện map ⇒ `SC-FEED-009` viết lại; hành vi UI nhánh thiếu location hỏi tiếp ở `C-FEED-02`.
