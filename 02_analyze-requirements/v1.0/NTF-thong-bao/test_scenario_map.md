---
id: v1.0/NTF-thong-bao/scenario-map
title: Test Scenario Map — v1.0 · Module NTF
type: scenario-map
version: v1.0
sprint: 1
module: NTF
counts:
  req: 11
  sc: 16
  new: 16
  modified: 0
  carried: 0
  deprecated: 0
  p1: 1
  p2: 9
  p3: 6
status: ANALYZED
updated: 2026-09-14
---

# Test Scenario Map — v1.0 · Module NTF

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module NTF.
> ⚠️ `NTF-07` (thông báo nhận quà) **có SC ở `GIFT`** (`SC-GIFT-012`) — ⛔ không nhân bản ở đây.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Fan-out **mỗi state-transition sinh thông báo** = 1 SC; mỗi nhánh cơ chế (chấm đỏ · phân trang · nhóm thời gian) = 1 SC.
> Trần: display-only/Phase-2/duplicate → `coverage-gap-report.md`. `NTF-07` không tạo SC vì đã có ở `GIFT`.

## Tổng quan
- Tổng số scenarios: **16** (NEW: 16, MODIFIED: 0, CARRIED: 0, DEPRECATED: 0)
- Phân bổ priority: P1: 1 | P2: 8 | P3: 7
- ⚠️ **Đặc tả `§D6`/`§D7` của BRD tự khai là "Nháp — chờ BA review & bổ sung"** ⇒ module có nhiều SC dạng ghi nhận; danh sách loại thông báo chính thức **chưa chốt** (`C-NTF-01`, bảng unified 12 hàng ở `KP-07`).

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### NTF — Thông báo

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-NTF-001 | NTF-01/02 — ghép ngay | REQ-NTF-001 | DOC-v1.0-01 §D6 L319-320 | Có đơn "Chờ ghép" với Sender A, Receiver C được khai | Carrier B bấm "Tôi mang giúp được" → xác nhận | A nhận thông báo "Đã có người nhận mang giúp đơn của bạn — SĐT đã được lộ để liên hệ"; C nhận "Đơn gửi tới bạn đã có người vận chuyển nhận giao" | P2 | Functional | NEW |
| SC-NTF-002 | NTF-03 — khớp tuyến OFFER | REQ-NTF-002 | DOC-v1.0-01 §D6 L321 · §D1b US-D12 L186 | Carrier B đã đăng tin OFFER; có tin NEED trùng điểm lấy & giao, khung giờ giao nhau | Chờ hệ thống khớp tuyến | B nhận thông báo "Tìm thấy đơn hàng phù hợp tuyến của bạn — xem chi tiết để nhận giao"; ⛔ KHÔNG assert độ trễ (chu kỳ quét chưa chốt — C-NTF-02) | P2 | Functional | NEW |
| SC-NTF-003 | NTF-04 — Carrier đã lấy hàng | REQ-NTF-003 | DOC-v1.0-01 §D6 L322 | Đơn ở "Đã ghép" | Carrier bấm "Tôi đã lấy hàng" → xác nhận | **Cả Sender và Receiver** nhận thông báo "Người vận chuyển đã lấy hàng và bắt đầu giao" | P2 | Functional | NEW |
| SC-NTF-004 | NTF-05 — Carrier đã giao | REQ-NTF-003 | DOC-v1.0-01 §D6 L323 | Đơn ở "Đang giao" | Carrier bấm "Đã giao cho người nhận" → xác nhận | **Cả Receiver và Sender** nhận thông báo "Đơn đã được giao — vui lòng xác nhận đã nhận hàng" | P2 | Functional | NEW |
| SC-NTF-005 | NTF-06 — đơn hoàn tất | REQ-NTF-003 | DOC-v1.0-01 §D6 L324 · KP-07 hàng #6 | Đơn ở "Đã giao" | Receiver bấm "Xác nhận đã nhận hàng" → xác nhận | **Cả Sender và Carrier** nhận thông báo hoàn tất. ⚠ BRD ghi "Đơn đã hoàn tất — cảm ơn bạn!" nhưng Figma+PRD ghi "Đơn đã hoàn thành — đánh giá ngay" → GHI NHẬN text thật, ⛔ không assert (C-NTF-01) | P2 | Functional | NEW |
| SC-NTF-006 | NTF-08 — đơn bị huỷ | REQ-NTF-004 | DOC-v1.0-01 §D6 L326 · KP-07 hàng #8 | Đơn ở "Đã ghép" (đủ 3 vai) | 1 vai huỷ đơn kèm lý do | Các bên còn lại nhận thông báo nêu rõ **ai huỷ** + **lý do**; nhánh Carrier huỷ nhận: Figma còn thêm câu "Đơn đang chờ người vận chuyển mới..." | P2 | Functional | NEW |
| SC-NTF-007 | NTF-09 — tin quá hạn | REQ-NTF-004 | DOC-v1.0-01 §D6 L327 | Có tin "Chờ ghép" với "Đến ngày" vừa trôi qua, chưa ai nhận | Chờ hệ thống chuyển tin sang Hết hạn | Người đăng nhận thông báo "Tin của bạn đã quá hạn — gỡ hoặc đăng lại nếu vẫn cần" | P2 | Functional | NEW |
| SC-NTF-008 | SĐT không có trong nội dung thông báo | REQ-NTF-005 | DOC-v1.0-01 §D7 OPR-07 L343 · §D6 L315 | Đơn vừa ghép (SĐT đã lộ trong app cho 2 người trong cặp) | Đọc toàn bộ nội dung thông báo **in-app** và **push** của mọi sự kiện | KHÔNG thông báo nào chứa **số điện thoại**; được phép **nhắc tới việc SĐT đã lộ** (như NTF-01) nhưng không kèm số | P1 | Business Rule | NEW |
| SC-NTF-009 | Nhóm theo mốc thời gian | REQ-NTF-006 | DOC-v1.0-02 §3.2 · DOC-v1.0-04 3e626d39… | Tài khoản có thông báo phát sinh hôm nay, hôm qua và trong tuần | Mở màn Thông báo (bấm chuông ở header) | Danh sách nhóm theo "Hôm nay" / "Hôm qua" / "Tuần này"; ⛔ KHÔNG assert nhóm cho thông báo cũ hơn 1 tuần (không có nguồn) | P2 | UI | NEW |
| SC-NTF-010 | Chấm đỏ theo từng item | REQ-NTF-007 | DOC-v1.0-06 KP-01 §8 KB-NTF-01 · DOC-v1.0-04 3e626d39… | Tài khoản có ≥2 thông báo chưa đọc và ≥1 thông báo đã đọc trong **cùng 1 nhóm thời gian** | Mở màn Thông báo | Item chưa đọc có chấm đỏ riêng; item đã đọc KHÔNG có — trạng thái theo **từng item**, không theo nhóm | P3 | UI | NEW |
| SC-NTF-011 | [GAP] Cơ chế "Đánh dấu đã đọc" | REQ-NTF-007 | DOC-v1.0-06 KP-01 §8 KB-NTF-01 (`C-NTF-03a` Open) | Có ≥2 thông báo chưa đọc | (a) Tap vào 1 thông báo; (b) bấm nút "Đánh dấu đã đọc" | GHI NHẬN cơ chế thật: tap 1 item chỉ đọc item đó? nút là mark-all hay mark-per-item? ⛔ KHÔNG assert (C-NTF-03a Open) | P3 | Functional | NEW |
| SC-NTF-012 | Scroll / lazy-load | REQ-NTF-008 | DOC-v1.0-06 KP-01 §8 KB-NTF-02 | Tài khoản có danh sách thông báo dài hơn 1 trang hiển thị | Cuộn xuống cuối danh sách | Load thêm dữ liệu (không dừng ở trang đầu); ⛔ KHÔNG assert số item/trang (không có nguồn) | P3 | Functional | NEW |
| SC-NTF-013 | Chuông đồng bộ số chưa đọc | REQ-NTF-009 | DOC-v1.0-02 §2 dòng "Header" | Tài khoản có ≥1 thông báo chưa đọc | Quan sát chuông ở header, mở màn Thông báo, đọc hết rồi quay lại Trang chủ | Chấm đỏ ở chuông **khớp với** tình trạng còn/hết thông báo chưa đọc trong danh sách | P2 | Functional | NEW |
| SC-NTF-014 | [GAP] Danh sách loại thông báo chính thức | REQ-NTF-010 | DOC-v1.0-01 §D6 L317-327 vs DOC-v1.0-02 §3.2 vs DOC-v1.0-04 · KP-07 | 3 nguồn cho 3 danh sách khác nhau; `KP-07` có bảng unified **12 hàng sự kiện** | Liệt kê toàn bộ loại thông báo thực tế app bắn ra trong 1 vòng đời đơn trọn vẹn | GHI NHẬN danh sách thật, đối chiếu với 12 hàng của `KP-07`; ⛔ KHÔNG assert danh sách nào là đúng (C-NTF-01 Open) | P3 | Functional | NEW |
| SC-NTF-015 | [GAP] Empty state màn Thông báo | REQ-NTF-011 | DOC-v1.0-06 KP-02 §5 · C-ORD-06 | Tài khoản **chưa có thông báo nào** | Mở màn Thông báo | GHI NHẬN hiển thị thực tế; ⛔ KHÔNG assert text — chưa có đặc tả (C-ORD-06 Open) | P3 | UI | NEW |
| SC-NTF-016 | Nút back màn Thông báo | REQ-NTF-011 | DOC-v1.0-02 §2 · DOC-v1.0-06 KP-05 §3 (#6) | Đang ở màn Thông báo (mở từ chuông ở header Trang chủ) | Bấm nút quay lại (←) | Về đúng màn trước đó (Trang chủ). ⚠ Đích "Trang chủ" là suy diễn từ đường vào — nếu mở chuông từ màn khác thì ghi nhận đích thật | P3 | Functional | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-NTF-001 — NTF-01/02 khi ghép ngay

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-NTF-001`)*

**Source Location:** `DOC-v1.0-01 §D6 "Thông báo (Notifications)" · bảng · NTF-01 · L319` và `NTF-02 · L320`

**Analyst Note:** ⚠️ **PRD mô tả CƠ CHẾ khác:** *"[Tên] ngỏ ý mang giúp '...'. **Xác nhận để lộ SĐT.**"* — tức có bước duyệt, trái `BR-CON-01` (ghép ngay). `KP-07` hàng #1 ghi rõ lệch này *"liên quan C-ASN-01"*. ⇒ Assert theo **BRD** (đã chốt ghép ngay ở `ASN`). 1 SC phủ 2 người nhận vì cùng 1 sự kiện kích hoạt; Then kiểm cả A và C.

##### SC-NTF-002 — NTF-03 khớp tuyến

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-NTF-002`)*

**Source Location:** `DOC-v1.0-01 §D6 · bảng · NTF-03 · L321`

**Analyst Note:** 3 nguồn gần đồng thuận text (Figma khớp BRD hơn PRD — `KP-07` hàng #3) ⇒ assert được phần đầu câu. ⛔ **Không assert độ trễ** nhận thông báo: **chu kỳ quét khớp chưa chốt** (`C-NTF-02` Partially Resolved, home ở `ASN`). Luồng ghép sau khi bấm thông báo = `SC-ASN-009/010` ⇒ SC này chỉ assert **nội dung thông báo**.

##### SC-NTF-003 / SC-NTF-004 / SC-NTF-005 — NTF-04/05/06 theo mốc vận chuyển

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-NTF-003`)*

**Source Location:** `DOC-v1.0-01 §D6 · bảng · NTF-04..06 · L322-324`

**Analyst Note:** 3 SC theo **3 state-transition** của `DLV`; mỗi thông báo có **2 người nhận** ⇒ Then kiểm cả 2. ⚠️ **Mức bằng chứng không đều** (`KP-07`): `NTF-04` *"Không quan sát trong 82 ảnh"*; `NTF-05` PRD *"Không có mục riêng"*; `NTF-06` Figma **khớp Y HỆT PRD** với text *"Đơn đã hoàn thành — **đánh giá ngay**"* — dùng từ "đánh giá" trong khi rating đã defer (`C-GIFT-01`) ⇒ `SC-NTF-005` **ghi nhận text thật thay vì assert**.

##### SC-NTF-006 / SC-NTF-007 — NTF-08 huỷ đơn · NTF-09 tin quá hạn

**Source Quote:** *(NTF-08/NTF-09 quote đầy đủ ở `requirement_traceability.md §2 REQ-NTF-004`)*
> Figma (`KP-07` hàng #8): ""Đơn của bạn đã bị người vận chuyển huỷ" — "Lý do: 'bận họp gấp'. Đơn đang chờ người vận chuyển mới...""

**Source Location:** `DOC-v1.0-01 §D6 · NTF-08 · L326` và `NTF-09 · L327` ⟷ `DOC-v1.0-06 KP-07 · hàng #8`

**Analyst Note:** `NTF-08` có **2 mức chi tiết**: BRD dùng template `[vai trò]`/`[…]`; Figma thêm *"Đơn đang chờ người vận chuyển mới..."* — câu này **chỉ đúng cho nhánh Carrier huỷ nhận** (đơn về `POSTED`, xem `SC-CNL-007`), ⛔ không đúng khi Sender huỷ (đơn `CANCELLED`) ⇒ Then phân nhánh. `SC-NTF-007` phụ thuộc tiền đề **đơn quá hạn** (⛔ không seed qua UI — nhờ dev, xem `ORD` `RISK-ORD-06`).

##### SC-NTF-008 — SĐT không có trong nội dung thông báo

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-NTF-005`)*
> "OPR-07 | Lộ liên hệ có kiểm soát | SĐT chỉ lộ sau khi ghép, chỉ cho đúng 2 người trong cặp; **không đưa SĐT vào nội dung push**"

**Source Location:** `DOC-v1.0-01 §D7 · OPR-07 · L343` và `§D6 · đoạn mở đầu · L315`

**Analyst Note:** **SC P1 duy nhất của module** — rule bảo mật, 2 nguồn đồng thuận. ⚠️ Phân biệt tinh tế: `NTF-01` **được phép nhắc** *"SĐT đã được lộ để liên hệ"* (không chứa số) ⟷ ⛔ **không được chứa số điện thoại**. Phải kiểm **cả 2 kênh** (in-app **và** push notification) — push là kênh dễ lọt vì nội dung do backend đẩy, không đi qua UI.

##### SC-NTF-009 / SC-NTF-010 — Nhóm thời gian · chấm đỏ theo item

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-NTF-006` và `REQ-NTF-007`)*

**Source Location:** `DOC-v1.0-02 §3.2 · dòng tiêu đề ảnh` ⟷ `DOC-v1.0-06 KP-01 §8 "KB-NTF-01"`

**Analyst Note:** `SC-NTF-009`: ⛔ không suy diễn nhóm thứ tư (thông báo cũ hơn 1 tuần) — không nguồn nào nói. `SC-NTF-010`: Given yêu cầu item đã đọc và chưa đọc **trong cùng 1 nhóm thời gian** — đúng cấu hình đã sinh ra bằng chứng ở ảnh Figma; đây là cách duy nhất phân biệt "chấm đỏ theo item" với "chấm đỏ theo nhóm".

##### SC-NTF-011 / SC-NTF-012 — [GAP] cơ chế đánh dấu đã đọc · lazy-load

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-NTF-007`)*
> "QA GiangDC2 xác nhận (2026-07-29): đây là **hành vi UI nền tảng bắt buộc** cho danh sách lớn, không cần BA xác nhận riêng như một business rule."

**Source Location:** `DOC-v1.0-06 KP-01 §8 "KB-NTF-01"` và `"KB-NTF-02"`

**Analyst Note:** Hai nhánh của `C-NTF-03` được xử lý **khác nhau**: **(a)** cơ chế đánh dấu đã đọc — **Open**, chỉ ghi nhận (`SC-NTF-011`); **(b)** phân trang — **N/A** (QA quyết định là yêu cầu UI nền tảng) ⇒ viết SC assert được (`SC-NTF-012`), nhưng ⛔ không assert **số item/trang** vì không có nguồn.

##### SC-NTF-013 — Chuông đồng bộ số chưa đọc

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-NTF-009`)*

**Source Location:** `DOC-v1.0-02 §2 · bảng Thành phần/Mô tả · dòng "Header"`

**Analyst Note:** Bề mặt chuông (có/không có chấm đỏ) đã có SC ở `HOME` (`SC-HOME-005/006`); SC ở đây assert **tính đồng bộ** giữa chấm đỏ và **tình trạng thật của danh sách** sau khi đọc ⇒ 2 góc nhìn, không trùng. ⚠️ Phụ thuộc `C-NTF-03(a)`: nếu cơ chế đánh dấu đã đọc chưa chốt thì bước "đọc hết" trong When có thể không thực hiện được nhất quán ⇒ ghi nhận cách đã dùng.

##### SC-NTF-014 — [GAP] Danh sách loại thông báo chính thức

**Source Quote:**
> BRD tự khai (`§D6` L315): "Danh sách sự kiện bắn thông báo dựa trên flow & màn hình hiện có của prototype. **Nháp — chờ BA review & bổ sung.**"
> `KP-07`: "**Khuyến nghị cho BA/PO:** chọn 1 trong 3 hướng — (a) dùng nguyên BRD D6 (9 loại, NTF-01..09)… (b) dùng Figma + Demo… (c) hợp nhất cả 3 thành danh sách mới ~10 loại… Cho tới khi BA chọn, generate-tc tạm dùng **hướng (c)** làm baseline vì có bằng chứng UI thật nhiều nhất."

**Source Location:** `DOC-v1.0-01 §D6 · đoạn mở đầu · L315` ⟷ `DOC-v1.0-06 KP-07 · bảng unified 12 hàng + đoạn Khuyến nghị`

**Analyst Note:** ⭐ **CL lớn nhất của module** (`C-NTF-01` Open). `KP-07` đã lập **bảng unified 12 hàng × 3 nguồn** để BA chọn 1 lần — chưa trả lời. 2 hàng loại được nhờ CL khác: **#6b** (*"nhận đánh giá 5 sao"* — `C-GIFT-01`) và **#11** (*"cộng đồng đạt mốc X đơn / CO₂"* — `C-USR-01`). Hàng **#10** (*"Sắp đến khung giờ hẹn giao"*) có bằng chứng ở **cả Demo và Figma** nhưng **không có trong BRD `§D6`** ⇒ khả năng cao BRD sót. ⇒ SC ghi nhận danh sách thật để đối chiếu 12 hàng, ⛔ không phán quyết danh sách nào đúng.

##### SC-NTF-015 / SC-NTF-016 — [GAP] Empty state · nút back

**Source Quote:** *(mệnh đề "nút back" quote đầy đủ ở `requirement_traceability.md §2 REQ-NTF-011`)*
> "**C-ORD-06** | Empty state của 3 màn (Hoạt động · Quà đã nhận · **Thông báo**) khi không có data"

**Source Location:** `DOC-v1.0-06 KP-02 §5 · dòng "C-ORD-06"` và `KP-05 §3 · bảng · dòng 6`

**Analyst Note:** Empty state: màn Thông báo là **màn thứ ba** của `C-ORD-06` (home canonical ở `ACT`) ⇒ ghi nhận, ⛔ không assert text. Nút back: là **1 trong 6 nhóm case "chưa có nguồn tài liệu"** của đợt cũ, nay có **nguồn nền tảng** ở `DOC-v1.0-02` §2 (*"màn hình con… chỉ có nút quay lại (←)"*) ⇒ viết SC được; nhưng đích *"về Trang chủ"* là **suy diễn từ đường vào** (chuông ở header Trang chủ) ⇒ Then ghi rõ điều kiện.

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| — | *(không có — v1.0 là version đầu của chuỗi phân tích mới)* | — | — | — | — |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có ở dải `SC-NTF-*` lượt này)* | — | — | — |

> 📌 **Ghi chú lịch sử:** đợt v1.0 **cũ** có `SC-NTF-006` (*"Carrier bị giới hạn trần thông báo khớp/ngày"* theo `OPR-06`) bị **DEPRECATED 2026-07-29** khi BA xác nhận trần tính **riêng theo từng tin OFFER** (`KP-01` §4 `KB-ASN-03`). Rule hiện hành nằm ở `ASN` (`SC-ASN-014`), ⛔ **không tái tạo** ở module này. Lưu ý: ID `SC-NTF-006` của **lượt phân tích mới** là *"NTF-08 — đơn bị huỷ"*, **không liên quan** tới scenario cũ cùng số — ⛔ đừng lẫn (xem `CHANGELOG` frontmatter `id_range`).
