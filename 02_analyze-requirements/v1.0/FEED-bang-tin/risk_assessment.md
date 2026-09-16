---
id: v1.0/FEED-bang-tin/risk
title: Risk Assessment — v1.0 · Module FEED
type: risk-assessment
version: v1.0
sprint: 1
module: FEED
counts:
  cl: 3
  risk: 5
  cl_open: 0
  cl_resolved: 2
status: ANALYZED
updated: 2026-09-16
---

# Risk Assessment — v1.0 · Module FEED

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module FEED.
> 🔑 Frontmatter `counts:` = nguồn canonical CL/RISK — **chỉ đếm CL có home ở module này**; CL tham chiếu (home ở module khác) KHÔNG tính vào `counts`. **Layout v2 ⇒ đây là home của Clarification.**
> ℹ️ `cl_open (0) + cl_resolved (2) = 2 < cl (3)` — đúng, không lệch cộng: `C-FEED-01` ở trạng thái **🟡 Partially Resolved** (vế (a) Resolved 2026-09-16, vế (b) vẫn Pending), không thuộc 2 ô đó.

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| FEED | **High** | Chứa **2 vi phạm rule đã được BA xác nhận là bug** ngay trên bề mặt công khai: **lộ SĐT trước khi ghép** (`BR-CON-02`) và **cho chủ tin tự nhận đơn của mình** (`OPR-05`). Cả hai chưa được log bug ở đợt cũ |

## Chi tiết rủi ro (bảng hợp nhất)
| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-FEED-01 | FEED / Bảo mật liên hệ | **SĐT người gửi hiển thị công khai từ trạng thái "Chờ ghép"** — vi phạm `BR-CON-02`+`OPR-07`; bất kỳ CBNV nào xem bảng tin cũng lấy được SĐT mà không cần ghép | **High** | `DOC-v1.0-02` §3.4 đoạn lưu ý · §7 dòng 1 · phán quyết `C-ASN-01` Resolved | `SC-FEED-010` — assert theo rule, dự kiến FAIL | Log bug ngay khi execute (chưa log ở đợt cũ); ⛔ không sửa expected cho PASS | Open | REQ-FEED-006, SC-FEED-010 |
| RISK-FEED-02 | FEED / Logic vai trò | **Chủ tin và Người nhận của đơn vẫn bấm được "Tôi mang giúp được"** — vi phạm `OPR-05`; tạo được cặp ghép người gửi = người vận chuyển | **High** | `DOC-v1.0-02` §3.3 đoạn 5 · §7 dòng 9 · phán quyết `C-ASN-02` Resolved | `SC-FEED-011`, `SC-FEED-012` — assert theo rule, dự kiến FAIL | Log bug; kiểm chéo với `SC-ASN-012` (rule phía engine) | Open | REQ-FEED-007, SC-FEED-011, SC-FEED-012 |
| RISK-FEED-03 | FEED / Nhãn loại hàng | Danh mục "Loại hàng" **lệch 3 nguồn** (BRD 5 giá trị có "Tài liệu" · PRD 8 chip có "Tài liệu" · app STG 8 chip **không** có "Tài liệu", mặc định "Giấy tờ, hồ sơ") ⇒ TC assert nhãn sai lan khắp cả FEED và ORD | **High** | `D8.1` §D8.1 L357 · `DOC-v1.0-02` §3.5.1 · `DOC-v1.0-06` KP-01 §10.2 KB-VIBE-01 (có screenshot) | Dùng nhãn app STG; assert danh mục thực tế 1 lần rồi tham chiếu | Hỏi BA (`C-ORD-09`, home ở `ORD`); tới khi đó dùng `Giấy tờ, hồ sơ` | Open | REQ-FEED-001, SC-FEED-002 |
| RISK-FEED-04 | FEED / Vị trí CTA | *(cập nhật Status)* `US-D07` nói nút "Tôi mang giúp được" có **ngay tại thẻ tin** hoặc màn chi tiết; `§3.3` liệt kê 6 thành phần card **không có nút** ⇒ TC completeness card có thể assert thừa/thiếu nút | Medium → **Resolved** | `DOC-v1.0-01` §D1b `US-D07` L176 vs `DOC-v1.0-02` §3.3 đoạn 3 · vibe-check demo 2026-09-16 | `SC-FEED-002` (hết gap, assert cứng KHÔNG có CTA trên card) | Vibe-check qua demo xác nhận card **không có** nút CTA; nút chỉ có ở màn Chi tiết tin — khớp Nguồn B (`§3.3`), bác `US-D07` phần "ngay tại thẻ tin" | **Resolved** | REQ-FEED-004, SC-FEED-002 |
| RISK-FEED-05 | FEED / Bản đồ | Khung "Bản đồ · ~X km" là placeholder; nếu bản chính thức tích hợp bản đồ thật thì toàn bộ SC/TC quanh lộ trình phải viết lại | Low | `DOC-v1.0-02` §3.4 dòng "Lộ trình" · §7 dòng 10 (doc tự đặt câu hỏi mở) | Assert placeholder tĩnh, không assert bản đồ | ⚠️ Vibe-check demo 2026-09-16 xác nhận **hiện trạng** vẫn là placeholder tĩnh (icon + text "~X km", không phải bản đồ tương tác) — nhưng đây là câu hỏi **scope cho bản chính thức**, demo không trả lời được ý định sản phẩm. Vẫn phải hỏi BA/PM | Pending | REQ-FEED-005, SC-FEED-009 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-ASN-01 | SĐT lộ lúc nào? (bề mặt Chi tiết tin) | ✅ Resolved — **chỉ sau khi ghép**; hành vi prototype là bug | 2026-07-27 | REQ-FEED-006 |
| C-ASN-02 | Chủ tin có tự nhận mang giúp tin của mình được không? | ✅ Resolved — **KHÔNG**; hành vi prototype là bug | 2026-07-27 | REQ-FEED-007 |
| C-FEED-01 | Vị trí nút CTA (card vs chi tiết) + bản đồ thật hay placeholder | 🟡 **Partially Resolved 2026-09-16** — (a) vị trí CTA Resolved qua demo; (b) bản đồ thật/placeholder vẫn Pending (câu hỏi scope, không hỏi được qua demo) | mở 2026-09-07 | REQ-FEED-004, REQ-FEED-005 |
| C-ORD-06 | Text empty state (mở rộng sang màn Bảng tin) | 🔴 **Open** | kế thừa 2026-07-29 (revert Resolved→Open) | REQ-FEED-009 |

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

## Khuyến nghị tổng thể
1. **Resolve blocker trước generate-tc:** không có blocker cứng, nhưng `RISK-FEED-03` (nhãn "Loại hàng") **phải chốt trước** khi viết TC assert chip — nếu không, lỗi sai chữ của đợt cũ lặp lại nguyên xi.
2. **Ưu tiên test P1 high-risk:** `SC-FEED-010` (SĐT trước ghép) và `SC-FEED-011` (CTA với chủ tin) — chạy sớm để **log 2 bug đã biết mà đợt cũ chưa log** (`KP-05 §5`).
3. **Cần môi trường/dữ liệu:** 3 tài khoản (chủ tin · người xem · người nhận) + 1 tin OFFER để verify không lên bảng tin. Không có tài khoản thứ ba thì `SC-FEED-012` blocked.
4. ✅ **`C-FEED-01(a)` đã Resolved 2026-09-16 qua demo** — CTA "Tôi mang giúp được" chỉ ở màn Chi tiết tin, không trên card; dùng luôn cho locator automation sau này.
5. 🟡 **`C-FEED-01(b)` (bản đồ thật/placeholder) vẫn cần hỏi BA/PM** — là câu hỏi scope sản phẩm, không thể tự trả lời qua vibe-test/demo.
