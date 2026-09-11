---
id: v1.0/ASN-ghep-noi/scenario-map
title: Test Scenario Map — v1.0 · Module ASN
type: scenario-map
version: v1.0
sprint: 1
module: ASN
counts:
  req: 12
  sc: 18
  new: 18
  modified: 0
  carried: 0
  deprecated: 0
  p1: 6
  p2: 10
  p3: 2
status: ANALYZED
updated: 2026-09-07
---

# Test Scenario Map — v1.0 · Module ASN

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module ASN.
> ⚠️ **Module rủi ro cao nhất dự án** — 6/18 SC là P1: rule cạnh tranh (double-accept), rule bảo mật liên hệ, engine không tự khớp chính mình.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Fan-out mỗi role · **mỗi state-transition** · lớp EP · boundary · nhánh lỗi = 1 SC.
> Module này fan-out chủ yếu theo **state-transition** (`POSTED → MATCHED`, `MATCHED → POSTED`) và **nhánh điều kiện khớp** (trùng/không trùng · trong trần/vượt trần).
> Trần: display-only/Phase-2/duplicate → `coverage-gap-report.md`.

## Tổng quan
- Tổng số scenarios: **18** (NEW: 18, MODIFIED: 0, CARRIED: 0, DEPRECATED: 0)
- Phân bổ priority: P1: 6 | P2: 10 | P3: 2
- **SC khó thực thi nhất dự án nằm ở đây:** `SC-ASN-006` (2 Carrier bấm gần đồng thời) và `SC-ASN-008` (đồng bộ realtime 3 vai) — cần **2–3 thiết bị/phiên** phối hợp thời điểm.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### ASN — Ghép nối

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-ASN-001 | Ghép qua "Tôi mang giúp được" | REQ-ASN-001 | DOC-v1.0-01 §A5 BR-CON-01 L77 · DOC-v1.0-02 §4.2 | Có 1 tin NEED ở "Chờ ghép" do tài khoản A đăng; tài khoản B (Carrier) đang xem Chi tiết tin đó | B bấm "Tôi mang giúp được" → modal hiện → bấm "Xác nhận" | Đơn chuyển trạng thái "Đã ghép" (MATCHED); B trở thành Người vận chuyển của đơn | P1 | Functional | NEW |
| SC-ASN-002 | Huỷ ở modal xác nhận | REQ-ASN-001 | DOC-v1.0-02 §4.2 | B đang ở Chi tiết tin của 1 tin "Chờ ghép" | B bấm "Tôi mang giúp được" → modal hiện → bấm "Huỷ" | Đơn VẪN ở "Chờ ghép"; không ghép; SĐT không lộ | P2 | Business Rule | NEW |
| SC-ASN-003 | Ghép ngay, không cần chủ tin duyệt | REQ-ASN-001 | DOC-v1.0-01 §A5 BR-CON-01 L77 | B vừa xác nhận mang giúp tin của A | A (chủ tin) mở đơn ngay sau đó | Đơn đã ở "Đã ghép" mà A KHÔNG phải thực hiện bước chấp nhận/duyệt nào | P1 | Business Rule | NEW |
| SC-ASN-004 | Lộ SĐT cho 2 người trong cặp | REQ-ASN-002 | DOC-v1.0-01 §A5 BR-CON-02 L78 · §D7 OPR-07 L343 | Đơn vừa chuyển "Đã ghép" giữa A (Sender) và B (Carrier) | A và B lần lượt mở màn Theo dõi đơn | Cả A và B đều thấy SĐT của bên còn lại (B còn thấy cả SĐT Người nhận theo US-D08) | P1 | Business Rule | NEW |
| SC-ASN-005 | Người thứ ba không thấy SĐT | REQ-ASN-002 | DOC-v1.0-01 §D7 OPR-07 L343 | Đơn đã "Đã ghép" giữa A và B; tài khoản D không thuộc cặp ghép và không phải Người nhận | D tìm/mở đơn đó qua mọi bề mặt truy cập được | D KHÔNG thấy SĐT của A hoặc B | P2 | Business Rule | NEW |
| SC-ASN-006 | Chống double-accept | REQ-ASN-003 | DOC-v1.0-01 §D3 ASN-03 L249 · §D7 OPR-03 L339 | 1 tin NEED "Chờ ghép"; 2 Carrier B và C cùng mở Chi tiết tin của tin đó | B và C bấm "Tôi mang giúp được" → xác nhận **gần đồng thời** | Chỉ **1 người** ghép thành công; người còn lại bị chặn/nhận thông báo tin đã có người nhận; đơn có đúng 1 cặp active | P1 | Business Rule | NEW |
| SC-ASN-007 | Tin ẩn khỏi bảng tin + luồng gợi ý | REQ-ASN-004 | DOC-v1.0-01 §D7 OPR-03 L339 · OPR-08 L344 | 1 tin vừa chuyển "Đã ghép" | Tài khoản C (Carrier khác) mở Bảng tin và kiểm tra thông báo gợi ý | Tin KHÔNG còn trên Bảng tin và KHÔNG xuất hiện trong gợi ý cho C; C không bấm được "Tôi mang giúp được" cho tin đó | P1 | Business Rule | NEW |
| SC-ASN-008 | Đồng bộ realtime 3 vai | REQ-ASN-005 | DOC-v1.0-02 §4.2 · DOC-v1.0-01 §A5 BR-INT-05 L81 | 1 đơn "Chờ ghép" mở đồng thời trên 3 phiên/thiết bị khác nhau (Sender · Carrier · Receiver) | Carrier xác nhận mang giúp | Cả 3 phiên cập nhật trạng thái "Đã ghép" mà không cần thao tác làm mới thủ công | P2 | Functional | NEW |
| SC-ASN-009 | Auto-match sinh thông báo | REQ-ASN-006 | DOC-v1.0-01 §D3 MTCH-01 L254 · §D1b US-D12 L186 | Carrier B đã đăng 1 tin OFFER (tuyến A→B, khung giờ X) | Tài khoản khác đăng 1 tin NEED **trùng điểm lấy & điểm giao** và khung giờ giao nhau | B nhận thông báo "Tìm thấy đơn hàng phù hợp tuyến của bạn"; bấm thông báo → mở Chi tiết tin NEED đó | P2 | Functional | NEW |
| SC-ASN-010 | "Nhận giao" từ tin khớp tuyến | REQ-ASN-006 | DOC-v1.0-01 §D1b US-D13 L187 | B đang ở Chi tiết tin NEED được khớp tuyến | B bấm nút "Nhận giao" | Đơn chuyển MATCHED; lộ liên hệ 2 bên; điều hướng vào màn Theo dõi đơn | P2 | Functional | NEW |
| SC-ASN-011 | Không khớp khi lệch điểm/khung giờ | REQ-ASN-007 | DOC-v1.0-01 §D7 OPR-02 L338 · KP-01 §4 KB-ASN-04 | Carrier B đã đăng tin OFFER (tuyến A→B, khung giờ X) | (a) Đăng tin NEED có điểm giao KHÁC; (b) đăng tin NEED trùng điểm nhưng khung giờ **tách rời hoàn toàn** khung X | Cả 2 trường hợp: B KHÔNG nhận thông báo khớp tuyến | P2 | Business Rule | NEW |
| SC-ASN-012 | Không tự khớp tin của chính mình | REQ-ASN-010 | DOC-v1.0-01 §D7 OPR-05 L341 | Tài khoản A vừa đăng 1 tin NEED; A cũng đang có tin OFFER trùng tuyến | Kiểm tra thông báo và danh sách gợi ý của A | A KHÔNG được gợi ý / không nhận thông báo khớp cho tin do chính A đăng | P1 | Business Rule | NEW |
| SC-ASN-013 | Trần 5 tin gợi ý / carrier | REQ-ASN-008 | DOC-v1.0-01 §D7 OPR-01 L337 | Carrier B có tuyến OFFER khớp với **6 tin NEED** cùng lúc | Kiểm tra số tin gợi ý B nhận được | B chỉ được gợi ý tối đa **5 tin** (mới & gần tuyến nhất) | P2 | Business Rule | NEW |
| SC-ASN-014 | Trần 5 thông báo / mỗi tin OFFER | REQ-ASN-008 | DOC-v1.0-06 KP-01 §4 KB-ASN-03 | Carrier B có 1 tin OFFER; hệ thống đã bắn 5 thông báo khớp cho tin OFFER đó | Có thêm tin NEED thứ 6 khớp tuyến của tin OFFER đó | KHÔNG bắn thêm thông báo cho tin OFFER đó (trần tính **riêng theo từng tin**, KHÔNG cộng dồn theo ngày). Test ở 3 mốc: 3 / 5 / 6 tin | P2 | Business Rule | NEW |
| SC-ASN-015 | Thứ tự ưu tiên gợi ý | REQ-ASN-009 | DOC-v1.0-01 §D7 OPR-04 L340 | Có ≥3 tin NEED cùng khớp tuyến của B, đăng ở 3 thời điểm khác nhau | Xem danh sách gợi ý của B | Tin đăng mới hơn xếp trước (tiêu chí "độ gần tuyến" là nhị phân trùng/không trùng nên không phân biệt được thứ tự — xem Analyst Note) | P3 | Business Rule | NEW |
| SC-ASN-016 | Tin quá hạn bị loại khỏi luồng khớp | REQ-ASN-009 | DOC-v1.0-01 §D7 OPR-04 L340 | Có 1 tin NEED khớp tuyến của B nhưng đã quá "Đến ngày" (Hết hạn) | Kiểm tra gợi ý/thông báo của B | Tin Hết hạn KHÔNG xuất hiện trong gợi ý và KHÔNG bắn thông báo khớp | P2 | Business Rule | NEW |
| SC-ASN-017 | Carrier huỷ nhận → tin khớp lại được | REQ-ASN-011 | DOC-v1.0-01 §D7 OPR-08 L344 · OPR-09 L345 | Đơn đang "Đã ghép" với Carrier B, B **chưa** bấm "Tôi đã lấy hàng" | B huỷ nhận đơn | Đơn về "Chờ ghép", hiển thị lại trên Bảng tin, và Carrier C **ghép được** đơn đó | P2 | Business Rule | NEW |
| SC-ASN-018 | [GAP] Wizard không tạo listing độc lập | REQ-ASN-012 | DOC-v1.0-06 KP-01 §4 KB-ASN-05 · KP-02 §5 | Nghi vấn từ prototype: tin đăng qua wizard không thành listing độc lập trong feed Carrier/Receiver | Tài khoản A đăng 2 tin NEED liên tiếp; tài khoản B mở Bảng tin | GHI NHẬN: có đủ 2 listing độc lập hay không; ⛔ KHÔNG kết luận bug — có thể là giới hạn bản demo (C-ASN-03 Open) | P3 | Functional | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-ASN-001 / SC-ASN-002 / SC-ASN-003 — Ghép qua "Tôi mang giúp được" (modal · huỷ · không cần duyệt)

**Source Quote:**
> Rule (`DOC-v1.0-01` §A5 `BR-CON-01` L77): "Người B bấm "Tôi mang giúp được" → hệ thống ghép ngay, không cần bước chủ tin duyệt"
> Bề mặt (`DOC-v1.0-02` §4.2): "Bấm "Tôi mang giúp được" → hiện modal xác nhận:" · "Modal "Xác nhận mang giúp" — SĐT hai bên sẽ được lộ sau khi xác nhận" · "Bấm Xác nhận → đơn chuyển trạng thái "Đã ghép""

**Source Location:** `DOC-v1.0-01 §A5 · bảng Rule/Mô tả · L77` ⟷ `DOC-v1.0-02 §4.2 "Màn hình Chi tiết tin — hành động chính của vai trò này"`

**Analyst Note:** ⚠️ **BRD mâu thuẫn nội bộ:** `BR-CON-01` + sơ đồ `§A5` L62-64 nói **ghép ngay**; `ASN-02` (§D3 L248) và sơ đồ `§D2` L209 lại có bước *"Chủ tin chấp nhận / Xem hồ sơ tin cậy CARRIER → Chấp nhận"*. PRD (bề mặt thật) khớp `BR-CON-01`: chỉ có modal xác nhận **của chính Carrier**. ⇒ Chốt **ghép ngay**; `SC-ASN-003` là SC **bảo vệ kết luận** này. `SC-ASN-002` (nhánh Huỷ modal) quan trọng vì modal là **điểm không thể quay lại** — sau khi xác nhận thì SĐT đã lộ.

##### SC-ASN-004 / SC-ASN-005 — Lộ SĐT đúng 2 người trong cặp (positive + negative)

**Source Quote:**
> "BR-CON-02 | Sau khi ghép: lộ SĐT + kênh liên hệ cho đúng 2 người trong cặp ghép; trước khi ghép không lộ SĐT"
> "OPR-07 | Lộ liên hệ có kiểm soát | SĐT chỉ lộ sau khi ghép, **chỉ cho đúng 2 người trong cặp**; không đưa SĐT vào nội dung push"

**Source Location:** `DOC-v1.0-01 §A5 · BR-CON-02 · L78` và `§D7 · OPR-07 · L343`

**Analyst Note:** Rule có **2 vế**, lượt này phủ vế **"sau khi ghép"**; vế **"trước khi ghép không lộ"** đã có SC bắt lỗi ở `FEED` (`SC-FEED-010`) ⇒ ⛔ không nhân bản. `SC-ASN-005` (negative) là SC **bảo mật**: cần tài khoản thứ tư không thuộc cặp; nếu FAIL thì đây là lỗ dữ liệu cá nhân nghiêm trọng hơn cả `SC-FEED-010` (vì ở đó ít nhất tin còn công khai). Lưu ý `US-D08` cho Carrier thấy SĐT **cả 2 đầu** (Người gửi + Người nhận) ⇒ "2 người trong cặp" không có nghĩa Carrier chỉ thấy 1 số.

##### SC-ASN-006 — Chống double-accept (2 Carrier bấm gần đồng thời)

**Source Quote:**
> "ASN-03 | Chống ghép trùng | 1 tin chỉ 1 cặp active (DB constraint + tx lock)"
> "OPR-03 | 1 tin — 1 cặp ghép | **Ghép ngay cho người bấm "Tôi mang giúp được" đầu tiên**; ngay khi có người nhận, tin bị ẩn khỏi bảng tin và không ai bấm "Tôi mang giúp được" được nữa (chống double-accept)"

**Source Location:** `DOC-v1.0-01 §D3 · ASN-03 · L249` và `§D7 · OPR-03 · L339` (và `§D5 · L293`)

**Analyst Note:** ⚠️ `§D5` L293 lệch cơ chế (*"Chủ tin chọn"*) — chốt theo `OPR-03` (**first-come**). **SC khó thực thi nhất dự án**: cần 2 Carrier bấm trong cùng cửa sổ vài trăm ms ⇒ 2 thiết bị/2 phiên + phối hợp thời điểm; với 1 tester thì gần như chỉ kiểm chứng được **nhánh tuần tự** (người thứ hai bấm sau khi tin đã ẩn). Ghi rõ giới hạn này ở `risk_assessment.md` `RISK-ASN-02` — ⛔ đừng khai coverage cho nhánh cạnh tranh thật khi chỉ chạy được nhánh tuần tự.

##### SC-ASN-007 — Tin ẩn khỏi bảng tin và luồng gợi ý

**Source Quote:**
> "ngay khi có người nhận, tin bị ẩn khỏi bảng tin và không ai bấm "Tôi mang giúp được" được nữa"
> "OPR-08 | Vòng đời tin trong luồng khớp | Tin đang MATCHED/IN_TRANSIT không xuất hiện ở gợi ý cho carrier khác…"

**Source Location:** `DOC-v1.0-01 §D7 · OPR-03 · L339` và `OPR-08 · L344`

**Analyst Note:** Gộp 2 bề mặt (bảng tin + luồng gợi ý) vào 1 SC vì cùng **một hành vi nguyên tử**: tin rời khỏi tập khả dụng. Then có 3 mệnh đề kiểm được độc lập ⇒ generate-tc sẽ fan-out thành 3 TC. Hệ quả đã ghi ở `FEED`: **bảng tin có thể rỗng dù hệ thống đang nhiều đơn**.

##### SC-ASN-008 — Đồng bộ realtime 3 vai

**Source Quote:**
> "Bấm Xác nhận → đơn chuyển trạng thái "Đã ghép"; CẢ 3 khung (Người gửi / Người vận chuyển / Người nhận) đổi trạng thái tức thời — đây là điểm nhấn chính của bản demo (đồng bộ dữ liệu thời gian thực)."

**Source Location:** `DOC-v1.0-02 §4.2 · đoạn 3`

**Analyst Note:** ⚠️ **Cẩn trọng nguồn:** câu này mô tả **bản demo**, mà demo *"chỉ mô phỏng MỘT đơn hàng duy nhất cho cả 3 khung xem cùng lúc"* (`§1.4`) — 3 khung là 3 view của **cùng 1 state trong bộ nhớ**, ⛔ **không chứng minh** đồng bộ qua backend giữa 3 thiết bị thật. `BR-INT-05` (§A5 L81) có yêu cầu *"đồng bộ realtime cả 3 bên"* nhưng cho luồng **huỷ**. ⇒ Given ghi rõ **3 phiên/thiết bị khác nhau**; nếu app cần refresh thủ công thì đó là finding cần BA phán quyết, không tự kết luận bug.

##### SC-ASN-009 / SC-ASN-010 — Auto-match: thông báo · "Nhận giao"

**Source Quote:**
> "MTCH-01 | Tự khớp tuyến OFFER ↔ NEED | Trùng điểm lấy & điểm giao → đẩy thông báo cho Carrier duyệt "Nhận giao""
> "Khi một tin NEED trùng điểm lấy & điểm giao với tuyến → hệ thống đẩy thông báo "Tìm thấy đơn hàng phù hợp tuyến của bạn"; bấm vào thông báo → mở màn chi tiết tin cần vận chuyển đó"
> "Tại chi tiết tin NEED phù hợp có nút "Nhận giao"; bấm → ghép (MATCHED) → lộ liên hệ 2 bên → vào màn Theo dõi đơn"

**Source Location:** `DOC-v1.0-01 §D3 · MTCH-01 · L254` · `§D1b · US-D12 · L186` · `US-D13 · L187`

**Analyst Note:** Nút ở luồng này là **"Nhận giao"**, khác **"Tôi mang giúp được"** của luồng NEED thủ công ⇒ ⛔ đừng dùng lẫn tên nút trong TC. ⚠️ **Scope:** PM chưa trả lời auto-match có thuộc Phase 1 (`KP-05 §1` câu #1) — đợt cũ có scenario **không có TC** vì lý do này; lượt này scope = toàn bộ 11 module nên vẫn viết SC. Chi phí tiền đề cao: cần 1 tin OFFER + 1 tin NEED khớp chính xác điểm lấy/giao.

##### SC-ASN-011 — Không khớp khi lệch điểm hoặc khung giờ (negative)

**Source Quote:**
> "OPR-02 | Điều kiện khớp | Chỉ khớp khi trùng điểm lấy & điểm giao (cùng khu vực/tuyến) và giao nhau về khung giờ"
> "= **trùng địa chỉ giao hàng đã chọn** + **khung giờ phù hợp**. **KHÔNG dùng bán kính GPS / khoảng cách địa lý.**"

**Source Location:** `DOC-v1.0-01 §D7 · OPR-02 · L338` ⟷ `DOC-v1.0-06 KP-01 §4 "KB-ASN-04"`

**Analyst Note:** `C-NTF-02` **Partially Resolved**: đã chốt **không dùng bán kính GPS**; **chưa chốt** *"khung giờ phù hợp"* là trùng hoàn toàn hay có độ lệch. ⇒ nhánh (b) của Then chỉ dùng **2 khung giờ tách rời hoàn toàn** (vd 08:00–09:00 vs 20:00–21:00) để không phụ thuộc định nghĩa chưa chốt; ⛔ không test biên độ lệch. Chính BRD ghi *"Nháp — chờ BA review & bổ sung"* ở đầu §D7 (L333).

##### SC-ASN-012 — Engine không gợi ý tin của chính mình

**Source Quote:**
> "OPR-05 | Không tự khớp với chính mình | **Không gợi ý tin do chính người đó đăng**; người gửi ≠ người vận chuyển của cùng một đơn"

**Source Location:** `DOC-v1.0-01 §D7 · OPR-05 · L341`

**Analyst Note:** Phủ **mệnh đề (a)** của `OPR-05` (engine gợi ý). Mệnh đề (b) (*"người gửi ≠ người vận chuyển"*, bề mặt CTA) đã có SC ở `FEED` (`SC-FEED-011/012`) ⇒ ⛔ không nhân bản. P1 vì nếu engine gợi ý tin của chính mình thì user tự ghép được và làm sai lệch mọi số liệu match rate; đồng thời `C-ASN-02` đã xác nhận prototype vi phạm ở bề mặt.

##### SC-ASN-013 / SC-ASN-014 — Trần gợi ý (5 tin) · trần thông báo (5/tin OFFER)

**Source Quote:**
> "OPR-01 | Trần số tin gợi ý cho 1 carrier | Mỗi người vận chuyển chỉ nhận thông báo tối đa 5 tin cần gửi phù hợp (mới & gần tuyến nhất); tránh làm phiền/spam"
> "OPR-06 | Trần thông báo khớp / ngày | Giới hạn số lần bắn thông báo khớp cho mỗi carrier **trong ngày** (ngưỡng admin cấu hình)"
> Phán quyết (`DOC-v1.0-06` KP-01 §4 KB-ASN-03): "Không phải "5 thông báo/ngày" cộng dồn — tính **riêng theo từng tin**." · "⚠ Giá trị test 3/5/6 tin là **giá trị chốt**, không phải mock."

**Source Location:** `DOC-v1.0-01 §D7 · OPR-01 · L337` · `OPR-06 · L342` ⟷ `DOC-v1.0-06 KP-01 §4 "KB-ASN-03"`

**Analyst Note:** ⭐ **`OPR-06` đã bị BA đảo kết luận** (2026-07-29): trần tính **riêng theo từng tin OFFER**, KHÔNG cộng dồn theo ngày ⇒ scenario cũ `SC-NTF-006` (*"trần thông báo khớp/ngày"*) đã bị **DEPRECATED** ở đợt v1.0 cũ. Lượt này **không tái tạo** scenario theo-ngày đó. Biên **3 / 5 / 6** là giá trị BA chốt ⇒ dùng đúng 3 mốc cho BVA, ⛔ không tự nghĩ mốc khác. Tiền đề 6 tin khớp cùng tuyến ⇒ chi phí seed cao.

##### SC-ASN-015 / SC-ASN-016 — Thứ tự ưu tiên · loại tin quá hạn

**Source Quote:**
> "OPR-04 | Ưu tiên gợi ý | Sắp xếp theo độ gần tuyến → thời gian đăng (mới trước); tin quá hạn loại khỏi luồng khớp"

**Source Location:** `DOC-v1.0-01 §D7 · OPR-04 · L340`

**Analyst Note:** ⚠️ **Tiêu chí thứ nhất gần như không kiểm chứng được ở v1.0:** `KB-ASN-04` đã chốt khớp bằng **địa chỉ đã chọn, không dùng khoảng cách địa lý** ⇒ *"độ gần tuyến"* trở thành **nhị phân** (trùng/không trùng), không còn thang để sắp xếp. Còn lại tiêu chí **thời gian đăng (mới trước)** là tiêu chí duy nhất assert được ⇒ `SC-ASN-015` để P3 và Then nói rõ giới hạn này. `SC-ASN-016` (loại tin quá hạn) độc lập và kiểm chứng được ⇒ P2; phụ thuộc tiền đề đơn Hết hạn (cần dev seed, xem `ORD` `RISK-ORD-06`).

##### SC-ASN-017 — Carrier huỷ nhận → tin khớp lại được

**Source Quote:**
> "tin huỷ bởi carrier quay lại "Chờ ghép" và được khớp lại"
> "OPR-09 | Carrier huỷ khi chưa lấy hàng → trả đơn về bảng tin | Người vận chuyển huỷ ở trạng thái Đã ghép (chưa "Tôi đã lấy hàng") → đơn tự động về "Chờ ghép" và hiển thị lại trên bảng tin cho người khác nhận"

**Source Location:** `DOC-v1.0-01 §D7 · OPR-08 · L344` và `OPR-09 · L345`

**Analyst Note:** SC phủ **hệ quả phía ghép nối**: tin trở lại tập khả dụng **và ghép lại được bởi người khác** (mệnh đề thứ hai là phần dễ bị bỏ sót — nhiều TC chỉ kiểm tin về "Chờ ghép" rồi dừng). **Hành động huỷ + popup lý do bắt buộc** thuộc `CNL` (`REQ-CNL-004`) ⇒ 2 module, 2 SC, không trùng. Ranh giới trạng thái: **chỉ khi chưa "Tôi đã lấy hàng"**.

##### SC-ASN-018 — [GAP] Wizard không tạo listing độc lập

**Source Quote:**
> "Ghi nhận trên prototype. Chưa rõ là giới hạn kiến trúc bản demo (chấp nhận được) hay hành vi cần fix."

**Source Location:** `DOC-v1.0-06 KP-01 §4 "KB-ASN-05" · đoạn 1`

**Analyst Note:** *(Implicit — chỉ có ghi nhận quan sát, không có đặc tả.)* Rất có thể là **giới hạn bản demo**: `DOC-v1.0-02` §7 dòng 3 ghi *"Đăng tin mới sẽ ghi đè đơn đang có, không tạo song song nhiều đơn"*. ⇒ Given dùng **2 tin liên tiếp** để phân định; ⛔ không kết luận bug — `C-ASN-03` cần xác nhận lại **khi có backend thật**.

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| — | *(không có — v1.0 là version đầu của chuỗi phân tích mới)* | — | — | — | — |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có ở dải `SC-ASN-*` lượt này)* | — | — | — |

> 📌 **Ghi chú lịch sử:** đợt v1.0 **cũ** có `SC-NTF-006` (*"Carrier bị giới hạn trần thông báo khớp/ngày"*) bị **DEPRECATED 2026-07-29** khi BA xác nhận trần tính **riêng theo từng tin** (`KB-ASN-03`). Lượt phân tích mới **không tái tạo** scenario theo-ngày đó; rule hiện hành nằm ở `SC-ASN-014`. Đây là ghi chú tham chiếu — ⛔ không phải dòng DEPRECATED của dải ID lượt này.
