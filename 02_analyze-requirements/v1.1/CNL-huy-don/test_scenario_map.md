---
id: v1.1/CNL-huy-don/scenario-map
title: Test Scenario Map — v1.1 · Module CNL
type: scenario-map
version: v1.1
sprint: 1
module: CNL
counts:
  req: 9
  sc: 17
  new: 4
  modified: 5
  carried: 8
  deprecated: 0
  p1: 6
  p2: 9
  p3: 2
status: ANALYZED
updated: 2026-09-15
---

# Test Scenario Map — v1.1 · Module CNL

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module CNL **tính tới v1.1** (bao gồm CARRIED từ v1.0) — cùng nghĩa với mọi module delta khác.
> Parent: `v1.0/CNL-huy-don/` — 8 SC không đổi (CARRIED), 5 SC MODIFIED (giữ ID v1.0, bản v1.1 authoritative), 4 SC NEW.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Delta lần này fan-out theo: ngưỡng được-huỷ phát biểu theo **hành động** (sinh 1 ô biên mới) · 2 đường thoát sau `IN_TRANSIT` · hệ quả trạng thái của `INCIDENT` · actor mới không có bề mặt.
> Trần: bề mặt **báo sự cố** (form WebView, trần 5 ảnh, prefill) thuộc `TS` (`SC-TS-008..015`) ⇒ ⛔ không nhân bản ở đây.

## Tổng quan
- Tổng số scenarios (tính tới v1.1): **17** (NEW: 4, MODIFIED: 5, CARRIED: 8)
- Phân bổ priority: P1: 6 | P2: 9 | P3: 2
- Delta lớn nhất: **`SC-CNL-006` lật chiều** — từ *"ghi nhận KHÔNG có bề mặt tạo sự cố"* thành *"bề mặt PHẢI tồn tại"*; và **`SC-CNL-010` nâng P2 → P1** vì `BR11-03` biến bug audit thành vi phạm đặc tả đã phê duyệt.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### CNL — Huỷ đơn / Huỷ nhận đơn (delta v1.1)

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-CNL-014 | Sau IN_TRANSIT chỉ còn 2 đường thoát | REQ-CNL-008 | DOC-v1.1-01 §6.2 AC-25.2.01 | Đơn ở `IN_TRANSIT` hoặc muộn hơn | Lần lượt cả 3 vai mở màn Theo dõi đơn và rà toàn bộ nút hành động | KHÔNG vai nào còn thao tác huỷ đơn thường; chỉ còn đúng 2 đường: **hoàn hàng (RETURNING)** và **báo sự cố (INCIDENT)** | P1 | Business Rule | NEW |
| SC-CNL-015 | Đơn INCIDENT không tự về COMPLETED | REQ-CNL-008 | DOC-v1.1-01 §6.2 AC-25.2.01 | Đơn đã vào trạng thái `INCIDENT` | Người nhận thử bấm "Xác nhận đã nhận hàng" (nếu có) và quan sát đơn qua thời gian | Đơn **KHÔNG** tự chuyển `COMPLETED`; hệ thống nêu rõ phải qua admin hỗ trợ. ⚠ Dự kiến chưa test được nếu app chưa build trạng thái `INCIDENT` → ghi nhận, không đánh PASS | P2 | Business Rule | NEW |
| SC-CNL-016 | Biên: MATCHED nhưng ĐÃ bấm "Tôi đã lấy hàng" | REQ-CNL-003 | DOC-v1.1-01 §8.11 Pre-Conditions · §6.2 AC-25.1.01 | Đơn còn hiển thị `MATCHED` nhưng người vận chuyển **đã bấm** "Tôi đã lấy hàng" (popup xác nhận đang mở / request chưa trả về) | Người gửi mở màn Theo dõi đơn ở phiên song song và thử bấm "Huỷ đơn" | Huỷ **bị chặn** — Pre-Condition là *"MATCHED **khi chưa bấm** Tôi đã lấy hàng"*, không phải *"MATCHED"* đơn thuần | P2 | Business Rule | NEW |
| SC-CNL-017 | [GAP] Không có bề mặt Admin vận hành | REQ-CNL-009 | DOC-v1.1-01 §8.11 dòng Actor | Đã đăng nhập bằng tài khoản CBNV thường (không có vai Admin) | Rà toàn bộ màn Theo dõi đơn + Trang cá nhân tìm chức năng huỷ/can thiệp của "Admin vận hành" | GHI NHẬN GAP: không có bề mặt Admin trong app end-user (`C-CNL-03`). ⛔ KHÔNG viết TC khẳng định cho hành vi Admin | P3 | Functional | NEW |
| SC-CNL-004 | [GAP·bug] Lý do tối thiểu 5 ký tự — siết theo AC-25.1.03 | REQ-CNL-002 | DOC-v1.1-01 §8.11.1 BR11-01 · §8.18.2 VAL-04 · §6.2 AC-25.1.03 | Popup huỷ đơn đang mở | Nhập lý do **4 ký tự** rồi quan sát nút xác nhận và vùng dưới ô lý do | Nút xác nhận **ở trạng thái vô hiệu hoá** (không phải bấm được rồi mới báo lỗi) VÀ **hiện lỗi ngay dưới ô lý do** VÀ trạng thái đơn không đổi. ⚠ Dự kiến FAIL — app hiện cho qua → log bug | P2 | Business Rule | MODIFIED |
| SC-CNL-006 | Bề mặt "Báo cáo sự cố" PHẢI tồn tại *(lật chiều so với v1.0)* | REQ-CNL-003, REQ-CNL-007 | DOC-v1.1-01 §8.16 · §4 SCOPES In-scope · §6.2 AC-25.2.01 | Đơn ở `IN_TRANSIT` trở đi, đăng nhập lần lượt cả 3 vai | Mở màn Theo dõi đơn, tìm nút "Báo cáo sự cố" ở góc trên bên phải | Nút **tồn tại** và mở được luồng báo sự cố. ⚠ Dự kiến FAIL nếu app STG chưa build `FR16` — khi đó là **gap giữa PRD và app**, ⛔ KHÔNG quay lại kết luận "out of scope" của v1.0 | P2 | Business Rule | MODIFIED |
| SC-CNL-009 | [GAP·bug] Huỷ đơn phải ghi log đủ 3 thành phần | REQ-CNL-006 | DOC-v1.1-01 §8.11.1 BR11-02 · §6.2 AC-25.1.01 | Đơn ở "Chờ ghép" hoặc "Đã ghép", block LỊCH SỬ đang mở được | Người gửi huỷ đơn kèm lý do hợp lệ, rồi mở block LỊCH SỬ | Có dòng log mới ghi đủ **vai trò người huỷ** + **lý do** + **thời điểm (timestamp)** — cả ba, không thiếu thành phần nào. ⚠ Dự kiến FAIL — app hiện chỉ hiện banner đỏ, không ghi log → log bug | P2 | Business Rule | MODIFIED |
| SC-CNL-010 | [GAP·bug] Huỷ nhận đơn KHÔNG được xoá bản ghi lần ghép | REQ-CNL-006 | DOC-v1.1-01 §8.11.1 BR11-03 · §6.2 AC-25.1.02 | Đơn ở "Đã ghép"; LỊCH SỬ **đã có** dòng "Ghép thành công" | Người vận chuyển bấm "Huỷ nhận đơn" + nhập lý do, rồi mở block LỊCH SỬ | Dòng "Ghép thành công" **VẪN CÒN** (*"không xoá được"* — `AC-25.1.02`) + có thêm dòng log huỷ nhận + đơn về `POSTED` và **hiện lại trên bảng tin**. ⚠ Dự kiến FAIL — app hiện XOÁ dòng đó → log bug | P1 | Business Rule | MODIFIED |
| SC-CNL-012 | [GAP·bug] Trim khoảng trắng trước khi đếm ký tự | REQ-CNL-002 | DOC-v1.1-01 §8.18.2 VAL-03 + VAL-04 · §6.2 AC-25.1.03 | Popup huỷ đơn đang mở | Nhập lý do gồm **5 dấu cách** rồi quan sát nút xác nhận | Nút xác nhận **bị khoá** (sau khi *"tự cắt khoảng trắng đầu/cuối"* theo `VAL-03` thì lý do rỗng ⇒ vi phạm `VAL-04`). ⚠ Dự kiến FAIL — app hiện cho qua → log bug | P3 | Business Rule | MODIFIED |

#### Source Detail per Scenario (verbatim quotes)

##### SC-CNL-014 / SC-CNL-015 — Hai đường thoát sau IN_TRANSIT · hệ quả của INCIDENT
📍 `DOC-v1.1-01 §6.2 AC-25.2.01 "Sau khi hàng đã lên đường" · trang 26`

> "Then: Không còn thao tác huỷ đơn thường cho bất kỳ ai. Chỉ còn hai đường: hoàn hàng (RETURNING) hoặc báo sự cố (INCIDENT). Đơn ở INCIDENT không tự về COMPLETED, phải qua admin hỗ trợ."

**Analyst Note:** Một câu AC chứa **hai khẳng định kiểm được độc lập** ⇒ tách 2 SC. `SC-CNL-014` kiểm **ma trận đường thoát** (đếm đủ và đúng 2 đường, cho cả 3 vai — `BR11-04` viết *"bất kỳ vai trò nào"*); `SC-CNL-015` kiểm **thuộc tính của trạng thái `INCIDENT`** (không tự đóng). ⚠️ `SC-CNL-015` phụ thuộc app đã build `INCIDENT` — nếu chưa, kết quả đúng là **BLOCKED**, ⛔ không đánh PASS vì "không thấy đơn tự chuyển COMPLETED" (không có đơn `INCIDENT` nào để quan sát thì không chứng minh được gì). Liên hệ chéo: đường *hoàn hàng* (`RETURNING`) có home ở `DLV` (`SC-DLV-053/054`), ⛔ không nhân bản.

---

##### SC-CNL-016 — Biên "đã bấm nhưng chưa chuyển trạng thái"
📍 `DOC-v1.1-01 §8.11 dòng Pre-Conditions · trang 44` · `§6.2 AC-25.1.01 · trang 26`

> Pre-Conditions (§8.11): "Đơn ở POSTED, hoặc MATCHED khi chưa bấm "Tôi đã lấy hàng""

> AC-25.1.01 Given (§6.2): "Đơn ở POSTED hoặc MATCHED, người vận chuyển chưa bấm "Tôi đã lấy hàng"."

**Analyst Note:** ⭐ **SC này chỉ lộ ra vì PRD đổi cách phát biểu ngưỡng.** v1.0 phát biểu theo **trạng thái** (`OPR-11`: *"sau khi đã nhận hàng (IN_TRANSIT) thì KHÔNG ai được huỷ"*) ⇒ mọi TC đều dựng tiền đề bằng cách đẩy đơn sang `IN_TRANSIT`, và ô *"còn `MATCHED` nhưng đã bấm"* **không ai nghĩ tới**. v1.1 phát biểu theo **hành động** (*"chưa bấm"*) ⇒ khoảng giữa hai thời điểm (bấm nút ↔ trạng thái thực sự đổi) trở thành vùng phải kiểm. Đây là vùng dễ có lỗi race thật: nếu backend chỉ kiểm `status == MATCHED` thì huỷ sẽ lọt. ⚠️ Cần **2 phiên song song** (Sender + Carrier) — ghi ở `test_data_catalog.md`.

---

##### SC-CNL-017 — [GAP] Actor "Admin vận hành" không có bề mặt
📍 `DOC-v1.1-01 §8.11 dòng Actor · trang 44`

> "Actor: Người gửi · Người vận chuyển · Người nhận · Admin vận hành"

**Analyst Note:** PRD nâng Admin thành actor chính thức của `FR11` và `AC-25.2.01` giao cho admin việc đóng đơn `INCIDENT`, **nhưng không mục nào mô tả bề mặt đó** (không màn, không field, không ma trận quyền Admin). Theo `Project_rule §Custom Rules §10.1` — *UI phải khớp tài liệu mới được viết TC* — bước 3 cho phép **ghi nhận sự thiếu vắng**, ⛔ không viết TC khẳng định. Cùng loại với `C-TS-01` (Admin Portal out of scope, v1.0). ⇒ Đây là **gap nghiệp vụ cần nêu với PM**, không phải bug: nếu `INCIDENT` chỉ admin đóng được mà app không có đường nào tới admin, đơn sẽ **treo vĩnh viễn**.

---

##### SC-CNL-004 / SC-CNL-012 — `VAL-04` + `VAL-03` nay là đặc tả đã phê duyệt
📍 `DOC-v1.1-01 §8.11.1 BR11-01 · trang 44` · `§8.18.2 VAL-03 / VAL-04 · trang 52` · `§6.2 AC-25.1.03 · trang 26`

> BR11-01: "Lý do huỷ là bắt buộc, tối thiểu 5 ký tự, mới bật nút xác nhận."

> VAL-03: "Tự cắt khoảng trắng đầu/cuối; chuẩn hoá số điện thoại trước khi lưu."

> AC-25.1.03 Then: "Nút xác nhận huỷ vô hiệu hoá; hiện lỗi dưới ô lý do. Trạng thái đơn không đổi."

**Analyst Note (diff):** Rule **không đổi một chữ** so với `DOC-v1.0-01 §D8.3`; cái đổi là **ai bảo chứng cho nó**. v1.0: chỉ BRD + 1 quyết định override của QA ⇒ khi log bug còn có thể bị hỏi *"tài liệu tham khảo thôi mà"*. v1.1: PM phát biểu ở **3 chỗ độc lập** (`BR11-01` · `VAL-04` · `AC-25.1.03`) trong PRD đã phê duyệt. ⇒ 2 SC giữ nguyên **dự kiến FAIL**, ⛔ không sửa expected, và **log bug với căn cứ mạnh hơn hẳn**. Bổ sung 2 chi tiết Then mà v1.0 chưa có: nút phải **vô hiệu hoá sẵn** (không phải bấm rồi báo lỗi) và lỗi hiện **dưới ô lý do** (vị trí cụ thể, `VAL-02` cũng nói *"lỗi hiện ngay dưới ô nhập khi rời ô"*).

---

##### SC-CNL-006 — Lật chiều: từ "ghi nhận KHÔNG có" thành "PHẢI có"
📍 `DOC-v1.1-01 §4 SCOPES dòng In-scope · trang 9` · `§8.16 · trang 50`

> §4 SCOPES, In-scope: "Báo cáo sự cố qua Google Form nhúng WebView (Phase 1)"

**Analyst Note (diff):** 🔴 **Đây là SC bị đảo chiều hoàn toàn.** Bản v1.0 của `SC-CNL-006` có Then là *"GHI NHẬN GAP: không tồn tại bề mặt tạo sự cố ở v1.0 (đúng phạm vi — `C-CNL-01`)"* — tức PASS nghĩa là **không tìm thấy** nút. Bản v1.1 đảo ngược: PASS nghĩa là **tìm thấy** nút. ⛔ **Chạy bản v1.0 của SC này ở v1.1 sẽ cho kết luận ngược 180°** — đây chính xác là lý do `Project_rule` bắt ghi *"kết luận hết hiệu lực"* thay vì xoá lặng lẽ (xem `CHANGELOG §2`). Nếu app STG chưa build `FR16` thì kết quả đúng là **FAIL + log gap PRD↔app**, ⛔ tuyệt đối không diễn giải thành "vậy là vẫn out of scope".

---

##### SC-CNL-009 / SC-CNL-010 — Nhật ký huỷ nay là spec, không còn là override
📍 `DOC-v1.1-01 §8.11.1 BR11-02 / BR11-03 · trang 44` · `§6.2 AC-25.1.02 · trang 26`

> BR11-02: "Nhật ký ghi rõ vai trò người huỷ, lý do và thời điểm; trạng thái đồng bộ cho cả ba vai trò."

> BR11-03: "Người vận chuyển huỷ nhận khi chưa lấy hàng → đơn về POSTED và hiển thị lại trên bảng tin; bản ghi lần ghép trước vẫn giữ trong nhật ký."

> AC-25.1.02 Then: "Nhật ký giữ nguyên bản ghi lần ghép trước (không xoá được)."

**Analyst Note (diff):** ⭐ **`SC-CNL-010` nâng P2 → P1.** Ở v1.0 nó là SC suy ra từ `BR-INT-04` (*"không sửa được sau khi ghi"*) — một rule về **thuộc tính audit chung**. Nay `BR11-03` + `AC-25.1.02` nói **trúng đúng hành vi đang lỗi**, bằng chính từ ngữ của lỗi (*"bản ghi lần ghép trước vẫn giữ"*, *"không xoá được"*) ⇒ không còn khoảng cách diễn giải nào giữa spec và bug. `SC-CNL-009` bổ sung thành phần **timestamp** vào Then (v1.0 chỉ assert vai trò + lý do). ⚠️ Kiểm chéo bắt buộc với `SC-TS-003` (cùng bug, nhìn từ thuộc tính audit) và `SC-DLV-062` (`NFR-07` log append-only) — **chạy cùng lô, gộp 1 bug report 3 góc nhìn**, ⛔ đừng log 3 bug rời.

---

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| SC-CNL-001 | Huỷ đơn ở "Chờ ghép" | CNL | v1.0 | P1 | → `v1.0/CNL-huy-don/test_scenario_map.md` |
| SC-CNL-002 | Huỷ đơn ở "Đã ghép" | CNL | v1.0 | P1 | → như trên |
| SC-CNL-003 | Nút Xác nhận khoá tới khi có lý do | CNL | v1.0 | P2 | → như trên |
| SC-CNL-005 | Không huỷ được từ "Đang giao" | CNL | v1.0 | P1 | → như trên — `BR11-04` xác nhận lại, không đổi nội dung |
| SC-CNL-007 | Carrier huỷ nhận → đơn về "Chờ ghép" | CNL | v1.0 | P1 | → như trên — `BR11-03`/`AC-25.1.02` xác nhận lại |
| SC-CNL-008 | Ghi rõ vai trò người huỷ + lý do | CNL | v1.0 | P2 | → như trên — ⚠️ khi generate TC nhớ **siết thêm timestamp** (`BR11-02`) |
| SC-CNL-011 | Đồng bộ realtime 3 bên khi huỷ | CNL | v1.0 | P2 | → như trên — `BR11-02` *"đồng bộ cho cả ba vai trò"* xác nhận lại |
| SC-CNL-013 | Ma trận quyền huỷ theo vai × trạng thái | CNL | v1.0 | P2 | → như trên — ⚠️ cột `Admin` vẫn không test được (`SC-CNL-017`) |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
