# Requirement Traceability — v1.0 · Module FEED

> Tạo bởi: analyze-requirements (INIT 2026-09-07) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation: FR/VR` ⇒ **Schema A**.
> ⚠️ Module này ở đợt v1.0 cũ bị gộp vào `ASN` (2 scenario / 31 TC) — tách riêng từ 2026-09-07.
> ⚠️ **Ranh giới với `ASN`:** file này phủ **bề mặt hiển thị** Bảng tin + Chi tiết tin. **Rule ghép nối** (ghép ngay, ẩn tin sau khi ghép, chống double-accept) thuộc `ASN`.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module FEED — DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-06

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-FEED-001 | — (bảng §3.3 không đánh số) | `DOC-v1.0-02` §3.3 · §2 dòng "Tab Bảng tin" | SC-FEED-001, SC-FEED-002 | — |
| REQ-FEED-002 | — | `DOC-v1.0-02` §3.3 · đoạn 3 | SC-FEED-003, SC-FEED-004 | — |
| REQ-FEED-003 | — | `DOC-v1.0-02` §3.3 · đoạn 4 | SC-FEED-005, SC-FEED-014 | — |
| REQ-FEED-004 | `US-D07` | `DOC-v1.0-02` §3.4 · §4.2 · `DOC-v1.0-01` §D1b L176 | SC-FEED-006, SC-FEED-007 | — |
| REQ-FEED-005 | — | `DOC-v1.0-02` §3.4 · dòng "Lộ trình" · §7 dòng 10 | SC-FEED-009 | C-FEED-01 |
| REQ-FEED-006 | `BR-CON-02`, `OPR-07` | `DOC-v1.0-01` §A5 L78 · §D7 L343 · `DOC-v1.0-02` §3.4 dòng "Người gửi" · §7 dòng 1 | SC-FEED-010 | C-ASN-01 |
| REQ-FEED-007 | `OPR-05` | `DOC-v1.0-01` §D7 L341 · `DOC-v1.0-02` §3.3 đoạn 5 · §7 dòng 9 | SC-FEED-011, SC-FEED-012 | C-ASN-02 |
| REQ-FEED-008 | — | `DOC-v1.0-02` §3.4 · dòng "Ảnh sản phẩm" | SC-FEED-008 | — |
| REQ-FEED-009 | — | `DOC-v1.0-06` KP-05 §3 · `C-ORD-06` | SC-FEED-013 | C-ORD-06 |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-FEED-001 · Bảng tin — danh sách tin cộng đồng và cấu trúc card
📍 `DOC-v1.0-02 §3.3 "Màn hình Bảng tin" · đoạn 2-3` · `§2 · dòng "Tab Bảng tin"`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-02` §3.3 đoạn 3:
> "Mỗi card: icon/ảnh hàng, loại hàng | giá trị, badge "Tin của bạn" nếu là tin tự đăng, thời gian đăng, "Nhận:"/"Giao:" rút gọn, khung giờ."

> Nguồn #2 — `DOC-v1.0-02` §2 dòng "Tab Bảng tin":
> "Tab Bảng tin | Danh sách toàn bộ tin đăng gửi hàng của cộng đồng"

↳ **Ghi chú:** Card có **6 thành phần** liệt kê tường minh ⇒ 1 SC completeness đối chiếu đủ 6. Phạm vi danh sách = *"toàn bộ tin đăng của cộng đồng"*, khác với section "Tin mới" ở Trang chủ (bản rút gọn, số lượng đang tranh chấp — `C-HOME-03`). ⚠️ Tin **OFFER** (tuyến của Carrier) **không** lên bảng tin (`US-D11` §D1b L185) ⇒ danh sách chỉ gồm tin NEED; đây là ranh giới dễ bỏ sót.

---

### REQ-FEED-002 · Badge "Tin của bạn" trên card tin tự đăng
📍 `DOC-v1.0-02 §3.3 · đoạn 3`  ·  Clarif: —

> "badge "Tin của bạn" nếu là tin tự đăng"

↳ **Ghi chú:** Rule có điều kiện ⇒ fan-out 2 SC (positive: tin của mình có badge · negative: tin người khác không có badge). Badge này cũng là **bằng chứng gián tiếp** cho `REQ-FEED-007`: app **biết** ai là chủ tin ⇒ việc vẫn hiện nút "Tôi mang giúp được" cho chủ tin là lỗi logic ẩn nút, không phải thiếu thông tin.

---

### REQ-FEED-003 · Bấm card → mở Chi tiết tin
📍 `DOC-v1.0-02 §3.3 · đoạn 4`  ·  Clarif: —

> "Bấm vào 1 tin → mở Chi tiết tin."

↳ **Ghi chú:** Điều hướng 1 chiều đơn giản; SC ngược lại (back về Bảng tin) là **suy diễn từ `DOC-v1.0-02` §2** (*"màn hình con… chỉ có nút quay lại (←)"*) ⇒ `SC-FEED-014` ghi rõ đây là hành vi nền tảng, không phải đặc tả riêng của Chi tiết tin.

---

### REQ-FEED-004 · Chi tiết tin — thành phần và CTA
📍 `DOC-v1.0-02 §3.4 "Màn hình Chi tiết tin" · bảng Trường/Thành phần` · `§4.2` · `DOC-v1.0-01 §D1b US-D07 · L176`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-02` §3.4:
> "Ảnh sản phẩm | Ảnh minh hoạ hàng hoá (hoặc ảnh mặc định nếu người đăng không tải ảnh)"
> "Thông tin hàng | Loại hàng, Giá trị (2 cột), Ghi chú"
> "Lộ trình | Điểm Lấy hàng, điểm Giao hàng, khung "Bản đồ · ~X km" (placeholder tĩnh, không phải bản đồ thật)"
> "Khung giờ | Khung giờ mong muốn giao nhận"
> "Người gửi | Tên, SĐT + nút "Gọi""
> "Nút "Tôi mang giúp được" | CTA chính — hành động của vai trò Người vận chuyển"

> Nguồn #2 — `DOC-v1.0-01` §D1b `US-D07` L176:
> "Là Carrier, tôi muốn bấm "Tôi mang giúp được" ngay tại thẻ tin hoặc màn chi tiết, để gửi đề nghị nhanh cho Sender."

↳ **Ghi chú:** 6 khối thành phần, chia 2 SC theo **phần trên** (ảnh + thông tin hàng) và **phần dưới** (lộ trình + khung giờ + liên hệ + CTA) đúng như doc trình bày 2 ảnh riêng. ⚠️ `US-D07` nói nút CTA có **ngay tại thẻ tin** (Bảng tin) **hoặc** màn chi tiết, còn `DOC-v1.0-02` §3.3 chỉ mô tả nút ở màn chi tiết ⇒ **lệch nguồn về vị trí CTA**; `SC-FEED-002` completeness card **không** assert nút CTA trên card, ghi lệch vào `C-FEED-01`.

---

### REQ-FEED-005 · Khung "Bản đồ · ~X km" là placeholder tĩnh
📍 `DOC-v1.0-02 §3.4 · dòng "Lộ trình"` · `§7 · bảng "Các điểm cần làm rõ" · dòng 10`  ·  Clarif: `C-FEED-01`

> Nguồn #1 — `DOC-v1.0-02` §3.4 dòng "Lộ trình":
> "khung "Bản đồ · ~X km" (placeholder tĩnh, không phải bản đồ thật)"

> Nguồn #2 — `DOC-v1.0-02` §7 dòng 10:
> "10 | Bản đồ chỉ là placeholder | Khung "Bản đồ · ~X km" chỉ ghi khoảng cách ước tính tĩnh — cần xác nhận phạm vi bản chính thức có tích hợp bản đồ thật (GPS/Google Maps) hay không."

↳ **Ghi chú:** Doc tự đặt câu hỏi mở ⇒ SC assert **placeholder tĩnh** (không tương tác được, không zoom/pan), ⛔ không viết TC bản đồ thật. `~X km` là **số ước tính tĩnh** ⇒ không assert giá trị khoảng cách. Cross-ref `GPS-01` (`REQ-DLV-013`) — chia sẻ vị trí là nhánh phụ khác, đừng trộn.

---

### REQ-FEED-006 · SĐT người gửi hiển thị ở Chi tiết tin khi CHƯA ghép — trái rule
📍 `DOC-v1.0-01 §A5 BR-CON-02 · L78` · `§D7 OPR-07 · L343` · `DOC-v1.0-02 §3.4 dòng "Người gửi"` · `§7 dòng 1`  ·  Clarif: `C-ASN-01`

> Nguồn #1 — RULE (`DOC-v1.0-01` §A5 `BR-CON-02` L78):
> "BR-CON-02 | Sau khi ghép: lộ SĐT + kênh liên hệ cho đúng 2 người trong cặp ghép; trước khi ghép không lộ SĐT"

> Nguồn #2 — RULE (`DOC-v1.0-01` §D7 `OPR-07` L343):
> "OPR-07 | Lộ liên hệ có kiểm soát | SĐT chỉ lộ sau khi ghép, chỉ cho đúng 2 người trong cặp; không đưa SĐT vào nội dung push"

> Nguồn #3 — HÀNH VI PROTOTYPE (`DOC-v1.0-02` §7 dòng 1):
> "1 | Thời điểm lộ SĐT chưa nhất quán | Banner "Đăng tin mới" nói SĐT chỉ lộ SAU KHI ghép, nhưng "Chi tiết tin" đã hiện sẵn SĐT + nút Gọi của Người gửi ngay từ trạng thái "Chờ ghép"."

> Nguồn #4 — PHÁN QUYẾT (`DOC-v1.0-06` KP-01 §4 KB-ASN-01):
> "BA/PO xác nhận **rule chính thức = lộ sau ghép** (khớp `BR-CON-02`); hành vi prototype là **bug**, không phải hành vi mong muốn."

↳ **Ghi chú:** ⭐ **REQ quan trọng nhất của module.** Hai rule BRD đồng thuận (không lộ trước ghép); prototype làm ngược; `C-ASN-01` Resolved 2026-07-27 chốt **theo rule**, hành vi prototype là **bug**. ⇒ `SC-FEED-010` là **SC negative P1** assert *"KHÔNG hiện SĐT + nút Gọi ở trạng thái Chờ ghép"* — dự kiến **FAIL trên app hiện tại** và đó là **kết quả đúng** (bắt bug thật), ⛔ đừng "sửa TC cho PASS". Bề mặt sau khi ghép thuộc `DLV` (`REQ-DLV-009`).

---

### REQ-FEED-007 · Nút "Tôi mang giúp được" hiện với cả chủ tin / người nhận — trái `OPR-05`
📍 `DOC-v1.0-01 §D7 OPR-05 · L341` · `DOC-v1.0-02 §3.3 đoạn 5` · `§7 dòng 9`  ·  Clarif: `C-ASN-02`

> Nguồn #1 — RULE (`DOC-v1.0-01` §D7 `OPR-05` L341):
> "OPR-05 | Không tự khớp với chính mình | Không gợi ý tin do chính người đó đăng; người gửi ≠ người vận chuyển của cùng một đơn"

> Nguồn #2 — HÀNH VI (`DOC-v1.0-02` §3.3 đoạn 5):
> "⚠ Lưu ý: Tin của chính Người gửi vẫn hiển thị trong Bảng tin và khi mở Chi tiết tin vẫn thấy nút "Tôi mang giúp được" (hành động dành cho vai trò vận chuyển) — cần rà soát logic ẩn nút khi người xem chính là chủ tin."

> Nguồn #3 — HÀNH VI (`DOC-v1.0-02` §7 dòng 9):
> "9 | Chủ tin / Người nhận có thể tự "nhận mang giúp" | Chi tiết tin cho phép chính chủ tin hoặc Người nhận của đơn tự bấm "Tôi mang giúp được" trên tin liên quan đến mình — nên rà soát logic ẩn/hiện nút theo vai trò thực."

↳ **Ghi chú:** `C-ASN-02` Resolved 2026-07-27: **không được phép**, hành vi prototype là bug. Fan-out **2 SC** vì doc nêu **2 chủ thể khác nhau**: chủ tin (`SC-FEED-011`, P1) và **người nhận của đơn** (`SC-FEED-012`, P2 — chủ thể này chỉ có ở `§7 dòng 9`, `§3.3` không nhắc). ⚠️ `DOC-v1.0-06` KP-01 §4 KB-ASN-02 ghi rõ **phạm vi**: bug ở màn **Chi tiết tin (public)**, còn màn **Theo dõi đơn đã role-aware đúng** ⇒ ⛔ đừng viết SC này cho màn Theo dõi đơn. Rule engine phía ghép nối ở `REQ-ASN-009`.

---

### REQ-FEED-008 · Ảnh mặc định khi tin không có ảnh sản phẩm
📍 `DOC-v1.0-02 §3.4 · bảng Trường/Thành phần · dòng "Ảnh sản phẩm"`  ·  Clarif: —

> "Ảnh sản phẩm | Ảnh minh hoạ hàng hoá (hoặc ảnh mặc định nếu người đăng không tải ảnh)"

↳ **Ghi chú:** Ảnh là **tuỳ chọn** khi đăng tin (`D8.1` dòng "Ảnh sản phẩm" — `REQ-ORD-003`) ⇒ nhánh không-ảnh là đường đi thường gặp, không phải edge case. Doc **không mô tả ảnh mặc định là ảnh gì** ⇒ Then assert *có ảnh placeholder, không vỡ layout*, ⛔ không assert nội dung ảnh.

---

### REQ-FEED-009 · Empty state Bảng tin
📍 `DOC-v1.0-06 KP-05 §3` · `C-ORD-06`  ·  Clarif: `C-ORD-06`

> *(Implicit — không có quote đặc tả trực tiếp.)*

↳ **Ghi chú:** Derivation: `C-ORD-06` mở cho 3 màn (Hoạt động · Quà đã nhận · Thông báo) nhưng **Bảng tin cũng có trạng thái rỗng** (cộng đồng chưa có tin nào / mọi tin đã ghép nên bị ẩn theo `OPR-03`) mà không doc nào mô tả ⇒ mở rộng phạm vi `C-ORD-06` sang màn thứ tư. SC viết dạng ghi nhận, ⛔ không assert text.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
