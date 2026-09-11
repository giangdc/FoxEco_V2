---
id: v1.0/FEED-bang-tin/scenario-map
title: Test Scenario Map — v1.0 · Module FEED
type: scenario-map
version: v1.0
sprint: 1
module: FEED
counts:
  req: 9
  sc: 14
  new: 14
  modified: 0
  carried: 0
  deprecated: 0
  p1: 2
  p2: 7
  p3: 5
status: ANALYZED
updated: 2026-09-07
---

# Test Scenario Map — v1.0 · Module FEED

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module FEED.
> ⚠️ Đợt v1.0 cũ: Bảng tin + Chi tiết tin chỉ có **2 scenario** (`SC-ASN-005`, `SC-ASN-014`) nhưng **31 TC** (sheet `TC_06`).

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Fan-out mỗi role · mỗi state · mỗi lớp EP · mỗi boundary · mỗi nhánh lỗi = 1 SC.
> Trần: display-only/Phase-2/duplicate → `coverage-gap-report.md`.

## Tổng quan
- Tổng số scenarios: **14** (NEW: 14, MODIFIED: 0, CARRIED: 0, DEPRECATED: 0)
- Phân bổ priority: P1: 2 | P2: 7 | P3: 5
- **2 SC P1 đều là SC negative bảo vệ rule** (`SC-FEED-010` không lộ SĐT trước ghép · `SC-FEED-011` ẩn CTA với chủ tin) — **dự kiến FAIL trên app hiện tại**, và FAIL là kết quả đúng.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### FEED — Bảng tin & Chi tiết tin

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-FEED-001 | Danh sách Bảng tin | REQ-FEED-001 | DOC-v1.0-02 §3.3 · §2 | Cộng đồng có ≥2 tin NEED ở trạng thái Chờ ghép | Mở tab "Bảng tin" | Hiển thị danh sách tin NEED của cả cộng đồng (không giới hạn tin của mình); tin OFFER KHÔNG xuất hiện | P2 | Functional | NEW |
| SC-FEED-002 | Completeness card tin | REQ-FEED-001 | DOC-v1.0-02 §3.3 đoạn 3 | Bảng tin đang có ≥1 tin | Đối chiếu từng thành phần của 1 card | Card đủ 6 thành phần: icon/ảnh hàng · loại hàng\|giá trị · badge "Tin của bạn" (nếu là tin mình) · thời gian đăng · "Nhận:"/"Giao:" rút gọn · khung giờ | P2 | UI | NEW |
| SC-FEED-003 | Badge "Tin của bạn" | REQ-FEED-002 | DOC-v1.0-02 §3.3 đoạn 3 | Tài khoản A đã đăng 1 tin đang Chờ ghép | A mở Bảng tin, tìm tin của mình | Card tin đó có badge "Tin của bạn" | P3 | UI | NEW |
| SC-FEED-004 | Không badge với tin người khác | REQ-FEED-002 | DOC-v1.0-02 §3.3 đoạn 3 | Bảng tin có tin do tài khoản B đăng | A mở Bảng tin, xem card tin của B | Card tin của B KHÔNG có badge "Tin của bạn" | P3 | Business Rule | NEW |
| SC-FEED-005 | Mở Chi tiết tin | REQ-FEED-003 | DOC-v1.0-02 §3.3 đoạn 4 | Bảng tin có ≥1 tin | Bấm vào 1 tin cụ thể | Mở màn Chi tiết tin của đúng tin đó (loại hàng/lộ trình/khung giờ khớp card vừa bấm) | P2 | Functional | NEW |
| SC-FEED-006 | Chi tiết tin — phần trên | REQ-FEED-004 | DOC-v1.0-02 §3.4 | Đang ở Chi tiết tin của 1 tin có ảnh + có ghi chú | Quan sát phần trên màn | Hiển thị: ảnh sản phẩm · Loại hàng · Giá trị (2 cột) · Ghi chú | P2 | UI | NEW |
| SC-FEED-007 | Chi tiết tin — phần dưới | REQ-FEED-004 | DOC-v1.0-02 §3.4 · DOC-v1.0-01 §D1b US-D07 | Đang ở Chi tiết tin của 1 tin Chờ ghép | Cuộn xuống phần dưới màn | Hiển thị: Lộ trình (điểm Lấy hàng + Giao hàng + khung "Bản đồ · ~X km") · Khung giờ mong muốn · cụm Người gửi · nút CTA "Tôi mang giúp được" | P2 | UI | NEW |
| SC-FEED-008 | Ảnh mặc định | REQ-FEED-008 | DOC-v1.0-02 §3.4 dòng "Ảnh sản phẩm" | Có 1 tin được đăng KHÔNG kèm ảnh sản phẩm | Mở Chi tiết tin của tin đó | Hiển thị ảnh mặc định (placeholder), layout không vỡ; KHÔNG assert nội dung ảnh | P3 | UI | NEW |
| SC-FEED-009 | Bản đồ là placeholder tĩnh | REQ-FEED-005 | DOC-v1.0-02 §3.4 · §7 dòng 10 | Đang ở Chi tiết tin | Bấm/kéo/zoom vào khung "Bản đồ · ~X km" | Khung là placeholder tĩnh — KHÔNG mở bản đồ thật, KHÔNG zoom/pan; chỉ hiện khoảng cách ước tính | P3 | UI | NEW |
| SC-FEED-010 | [GAP·bug] SĐT trước khi ghép | REQ-FEED-006 | DOC-v1.0-01 §A5 BR-CON-02 L78 · §D7 OPR-07 L343 | 1 tin ở trạng thái "Chờ ghép" (chưa ai nhận); tài khoản đang xem KHÔNG thuộc cặp ghép | Mở Chi tiết tin của tin đó, xem cụm "Người gửi" | KHÔNG hiển thị SĐT và KHÔNG có nút "Gọi" (BR-CON-02). ⚠ Dự kiến FAIL trên app hiện tại → log bug, KHÔNG sửa TC | P1 | Business Rule | NEW |
| SC-FEED-011 | [GAP·bug] CTA với chủ tin | REQ-FEED-007 | DOC-v1.0-01 §D7 OPR-05 L341 · DOC-v1.0-02 §3.3 đoạn 5 | Tài khoản A là chủ tin của 1 tin đang Chờ ghép | A mở Chi tiết tin của chính tin mình đăng | Nút "Tôi mang giúp được" KHÔNG hiển thị (OPR-05). ⚠ Dự kiến FAIL trên app hiện tại → log bug | P1 | Business Rule | NEW |
| SC-FEED-012 | [GAP·bug] CTA với người nhận của đơn | REQ-FEED-007 | DOC-v1.0-02 §7 dòng 9 | Tài khoản C là **Người nhận** được khai trong 1 tin đang Chờ ghép | C mở Chi tiết tin của tin đó | Nút "Tôi mang giúp được" KHÔNG hiển thị. ⚠ Dự kiến FAIL → log bug | P2 | Business Rule | NEW |
| SC-FEED-013 | [GAP] Empty state Bảng tin | REQ-FEED-009 | DOC-v1.0-06 KP-05 §3 · C-ORD-06 | Cộng đồng không có tin NEED nào ở Chờ ghép (hoặc mọi tin đã ghép nên bị ẩn) | Mở tab "Bảng tin" | GHI NHẬN hiển thị thực tế; ⛔ KHÔNG assert text — chưa có đặc tả (C-ORD-06 Open) | P3 | UI | NEW |
| SC-FEED-014 | Back về Bảng tin | REQ-FEED-003 | DOC-v1.0-02 §2 | Đang ở Chi tiết tin mở từ Bảng tin | Bấm nút quay lại (←) | Về đúng màn Bảng tin, giữ vị trí danh sách | P3 | Functional | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-FEED-001 — Bảng tin hiển thị tin của cả cộng đồng

**Source Quote:**
> "Tab Bảng tin | Danh sách toàn bộ tin đăng gửi hàng của cộng đồng"

**Source Location:** `DOC-v1.0-02 §2 · bảng Thành phần/Mô tả · dòng "Tab Bảng tin"`

**Analyst Note:** Then thêm mệnh đề **"tin OFFER KHÔNG xuất hiện"** — suy ra từ `US-D11` (`DOC-v1.0-01` §D1b L185: *"tuyến đường của mình không hiển thị công khai lên bảng tin mà chỉ lưu vào hệ thống chờ khớp"*). Đây là ranh giới hay bị bỏ sót: người viết TC dễ mặc định "bảng tin = mọi tin đăng". Cross-ref `SC-ORD-030`.

##### SC-FEED-002 — Completeness card tin (6 thành phần)

**Source Quote:**
> "Mỗi card: icon/ảnh hàng, loại hàng | giá trị, badge "Tin của bạn" nếu là tin tự đăng, thời gian đăng, "Nhận:"/"Giao:" rút gọn, khung giờ."

**Source Location:** `DOC-v1.0-02 §3.3 "Màn hình Bảng tin" · đoạn 3`

**Analyst Note:** ⛔ **Không** assert nút CTA trên card: `US-D07` nói nút có *"ngay tại thẻ tin hoặc màn chi tiết"* nhưng `§3.3` không liệt kê nút trong 6 thành phần ⇒ lệch nguồn về vị trí CTA, đưa về `C-FEED-01`. Badge là thành phần **có điều kiện** ⇒ chỉ assert khi tin là của mình (đã tách riêng `SC-FEED-003/004`).

##### SC-FEED-003 / SC-FEED-004 — Badge "Tin của bạn" (positive + negative)

**Source Quote:**
> "badge "Tin của bạn" nếu là tin tự đăng"

**Source Location:** `DOC-v1.0-02 §3.3 · đoạn 3 · mệnh đề 3`

**Analyst Note:** Cần **2 tài khoản** (A đăng tin, B đăng tin) để phủ cả 2 nhánh. Badge là bằng chứng app **biết** chủ tin ⇒ củng cố `SC-FEED-011`: nút CTA hiện với chủ tin là **lỗi logic ẩn nút**, không phải app thiếu thông tin vai trò.

##### SC-FEED-005 — Bấm card mở Chi tiết tin đúng tin

**Source Quote:**
> "Bấm vào 1 tin → mở Chi tiết tin."

**Source Location:** `DOC-v1.0-02 §3.3 · đoạn 4`

**Analyst Note:** Then yêu cầu **đối chiếu dữ liệu** (loại hàng/lộ trình/khung giờ khớp card vừa bấm), không chỉ "mở được màn" — vì bản demo *"chỉ mô phỏng MỘT đơn hàng duy nhất cho cả 3 khung xem"* (`DOC-v1.0-02` §1.4) nên nhánh "mở sai tin" là rủi ro thật khi lên backend nhiều đơn.

##### SC-FEED-006 / SC-FEED-007 — Completeness Chi tiết tin (2 phần)

**Source Quote:**
> "Chi tiết tin (phần trên): mô tả, ảnh, thông tin hàng"
> "Chi tiết tin (phần dưới): lộ trình, khung giờ, liên hệ, nút hành động"

**Source Location:** `DOC-v1.0-02 §3.4 "Màn hình Chi tiết tin" · 2 dòng tiêu đề ảnh`

**Analyst Note:** Tách 2 SC theo đúng cách doc trình bày (2 ảnh, 2 nhóm thành phần) — giúp FAIL chỉ ra ngay nửa màn nào sai. ⚠️ `SC-FEED-007` Then **có** liệt kê cụm "Người gửi" (thành phần tồn tại), nhưng **nội dung SĐT** của cụm đó thì `SC-FEED-010` mới phán quyết — 2 SC không mâu thuẫn: một assert *có cụm*, một assert *cụm không được chứa SĐT khi chưa ghép*.

##### SC-FEED-008 — Ảnh mặc định khi tin không có ảnh

**Source Quote:**
> "Ảnh sản phẩm | Ảnh minh hoạ hàng hoá (hoặc ảnh mặc định nếu người đăng không tải ảnh)"

**Source Location:** `DOC-v1.0-02 §3.4 · bảng Trường/Thành phần · dòng "Ảnh sản phẩm"`

**Analyst Note:** Doc **không nói ảnh mặc định là ảnh gì** ⇒ Then assert *có placeholder + layout không vỡ*, ⛔ không assert nội dung/ảnh cụ thể (`§Custom Rules §10.1`). Given cần Fixture: 1 tin cố ý đăng không kèm ảnh — dễ tạo vì ảnh là trường tuỳ chọn (`D8.1`).

##### SC-FEED-009 — Khung bản đồ là placeholder tĩnh

**Source Quote:**
> "10 | Bản đồ chỉ là placeholder | Khung "Bản đồ · ~X km" chỉ ghi khoảng cách ước tính tĩnh — cần xác nhận phạm vi bản chính thức có tích hợp bản đồ thật (GPS/Google Maps) hay không."

**Source Location:** `DOC-v1.0-02 §7 "Các điểm cần làm rõ / kiểm thử kỹ trước khi test chính thức" · bảng · dòng 10`

**Analyst Note:** SC assert **trạng thái hiện tại** (placeholder) chứ không assert kỳ vọng tương lai. ⛔ Không assert giá trị `~X km` — là số ước tính tĩnh. Nếu app STG **có** bản đồ thật thì SC FAIL và đó là dữ liệu để đóng `C-FEED-01`, không phải bug.

##### SC-FEED-010 — [GAP·bug] SĐT không được lộ trước khi ghép

**Source Quote:**
> Rule (`DOC-v1.0-01` §A5 `BR-CON-02` L78): "Sau khi ghép: lộ SĐT + kênh liên hệ cho đúng 2 người trong cặp ghép; trước khi ghép không lộ SĐT"
> Hành vi (`DOC-v1.0-02` §3.4 đoạn cuối): "⚠ Lưu ý: Màn "Đăng tin mới" cam kết SĐT chỉ lộ SAU KHI ghép, nhưng thực tế Chi tiết tin đã hiển thị sẵn SĐT + nút Gọi của Người gửi ngay từ trạng thái "Chờ ghép" (chưa ai xác nhận mang giúp). Cần xác nhận đây có phải hành vi dự kiến."

**Source Location:** `DOC-v1.0-01 §A5 · bảng Rule/Mô tả · L78` ⟷ `DOC-v1.0-02 §3.4 · đoạn lưu ý cuối section`

**Analyst Note:** ⭐ **SC P1 quan trọng nhất module.** `C-ASN-01` Resolved 2026-07-27 chốt theo rule: hành vi prototype là **bug**. SC viết theo **rule** ⇒ dự kiến FAIL trên app hiện tại và **FAIL là kết quả đúng** (`§Custom Rules §10.1` bước 3 — TC dạng GAP finding). ⛔ Tuyệt đối không "sửa expected cho PASS". Đây cũng là rule bảo mật dữ liệu cá nhân, không chỉ là lỗi UI.

##### SC-FEED-011 / SC-FEED-012 — [GAP·bug] CTA hiện với chủ tin / người nhận

**Source Quote:**
> Rule (`DOC-v1.0-01` §D7 `OPR-05` L341): "Không tự khớp với chính mình | Không gợi ý tin do chính người đó đăng; người gửi ≠ người vận chuyển của cùng một đơn"
> Hành vi (`DOC-v1.0-02` §7 dòng 9): "Chi tiết tin cho phép chính chủ tin hoặc Người nhận của đơn tự bấm "Tôi mang giúp được" trên tin liên quan đến mình — nên rà soát logic ẩn/hiện nút theo vai trò thực."

**Source Location:** `DOC-v1.0-01 §D7 · bảng ID/Rule/Mô tả · L341` ⟷ `DOC-v1.0-02 §7 · bảng · dòng 9` (và `§3.3 · đoạn 5`)

**Analyst Note:** Fan-out **2 chủ thể** vì doc nêu 2: chủ tin (P1 — vi phạm trực tiếp `OPR-05`) và **người nhận của đơn** (P2 — chỉ `§7 dòng 9` nhắc, `§3.3` không). ⚠️ **Phạm vi:** `DOC-v1.0-06` KP-01 §4 KB-ASN-02 ghi rõ bug này ở màn **Chi tiết tin (public)**; màn **Theo dõi đơn đã role-aware đúng** ⇒ ⛔ không nhân bản 2 SC này sang `DLV`. Rule phía engine ghép nối = `SC-ASN-012`.

##### SC-FEED-013 — [GAP] Empty state Bảng tin

**Source Quote:** *(Implicit — không có quote đặc tả trực tiếp)*

**Source Location:** `DOC-v1.0-06 KP-05 §3 · bảng "6 nhóm case chưa có nguồn tài liệu" · dòng 4` · liên quan `C-ORD-06`

**Analyst Note:** Derivation: `C-ORD-06` mở cho 3 màn (Hoạt động · Quà đã nhận · Thông báo); Bảng tin là **màn thứ tư** cũng có trạng thái rỗng — đặc biệt vì `OPR-03` ẩn tin đã ghép nên bảng tin **có thể rỗng ngay cả khi hệ thống đang có nhiều đơn**. Ghi nhận, ⛔ không assert text.

##### SC-FEED-014 — Back về Bảng tin

**Source Quote:**
> "Các màn hình con (Chi tiết tin, Theo dõi đơn, luồng Đăng tin theo bước, Thông báo, Tặng quà...) không hiển thị thanh tab này — chỉ có nút quay lại (←)."

**Source Location:** `DOC-v1.0-02 §2 · đoạn 1 · câu 2`

**Analyst Note:** Hành vi **nền tảng** (suy từ §2), không phải đặc tả riêng của Chi tiết tin ⇒ P3. Mệnh đề *"giữ vị trí danh sách"* là **suy diễn của analyst** về UX thông thường, chưa có nguồn ⇒ khi execute mà không giữ vị trí thì ghi nhận, ⛔ không log bug. Cross-ref `SC-GIFT-010` (nút back màn Tặng quà nhảy sai màn — `C-GIFT-02`).

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| — | *(không có — v1.0 là version đầu của chuỗi phân tích mới)* | — | — | — | — |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
