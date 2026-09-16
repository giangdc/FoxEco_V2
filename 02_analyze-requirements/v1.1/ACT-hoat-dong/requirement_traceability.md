# Requirement Traceability — v1.1 · Module ACT

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation` của `DOC-v1.1-01` = `FR<NN>` / `BR<FF>-NN` / `EMP-NN` / `AC-{US}.{Scenario}.{Case}` ⇒ **Schema A**.
> Chỉ chứa REQ **NEW + MODIFIED** của lượt delta này. REQ CARRIED nguyên trạng — xem `v1.0/ACT-hoat-dong/requirement_traceability.md`.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module ACT — DOC-v1.1-01

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-ACT-010 | `BR17-01`, `BR17-02`, `BR17-03`, `FR17` Pre-Conditions | `DOC-v1.1-01` §8.17 (trang 50-51) · §8.17.2 BR17-01..03 (trang 51) · §6.2 AC-29.1.01 (trang 28) | SC-ACT-016, SC-ACT-017 | — |
| REQ-ACT-008 *(MODIFIED)* | `EMP-05`, `EMP-06`, `AC-29.1.01` | `DOC-v1.1-01` §8.17.1 EMP-05/EMP-06 (trang 51) · §6.2 AC-29.1.01 (trang 28) | SC-ACT-012, SC-ACT-014 | C-ORD-06 |
| REQ-ACT-001 *(MODIFIED)* | `EMP-05`, `EMP-06`, `AC-09.1.01` | `DOC-v1.1-01` §8.17.1 (trang 51) · §6.2 AC-09.1.01 (trang 19) | SC-ACT-001 | C-ACT-02 |
| REQ-ACT-004 *(MODIFIED)* | `AC-24.2.01`, `AC-09.1.01` | `DOC-v1.1-01` §6.2 AC-24.2.01 (trang 25) · AC-09.1.01 (trang 19) | SC-ACT-005, SC-ACT-015 | — |
| REQ-ACT-005 *(MODIFIED)* | `BR05-03`, `AC-09.1.01` | `DOC-v1.1-01` §8.5.1 BR05-03 (trang 38) · §6.2 AC-09.1.01 (trang 19) | SC-ACT-008, SC-ACT-009 | — |
| REQ-ACT-009 *(MODIFIED)* | `BR14-03`, §4 SCOPES Out of Scope | `DOC-v1.1-01` §8.14.1 BR14-03 (trang 49) · §4 (trang 9) | SC-ACT-013 | — |

> ℹ️ `REQ-ACT-002` · `REQ-ACT-003` · `REQ-ACT-006` · `REQ-ACT-007` **CARRIED không đổi** — PRD không mô tả cơ chế switch tab, đích tap card, hay quy tắc ẩn đơn "Đã huỷ" khỏi màn này.

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-ACT-010 · Quy tắc chung của empty state: cấu trúc, phân biệt loading, không che tab bar
📍 `DOC-v1.1-01 §8.17.2 BR17-01..03 · trang 51` · `§8.17 dòng Pre-Conditions · trang 50` · `§6.2 AC-29.1.01 · trang 28`  ·  Clarif: —

> Nguồn #1 — BR17-01..03 (§8.17.2, trang 51):
> "BR17-01 | Mỗi empty state gồm: icon nét mảnh màu neutral + một dòng tiêu đề + một dòng giải thích + tối đa một CTA."
> "BR17-02 | Không dùng ảnh minh hoạ nặng; không hiện skeleton vô hạn — phân biệt rõ đang tải và không có dữ liệu."
> "BR17-03 | Empty state không được che thanh tab dưới và vẫn cuộn được."

> Nguồn #2 — FR17 Pre-Conditions (§8.17, trang 50):
> "Cờ dữ liệu rỗng của khu vực đó bằng true (không dựa vào null của từng field)"

↳ **Ghi chú:** ⭐ **REQ MỚI dạng cross-cutting, nhưng home đặt ở `ACT` có chủ đích.** `FR17` áp cho **8 khu vực / 5 màn**; phần **danh mục text** đã chia về từng module (`EMP-01..03` → `HOME` · `EMP-04` → `FEED` · `EMP-05/06` → `ACT` · `EMP-07` → `NTF` · `EMP-08` → `GIFT`). Nhưng **3 rule về hình thức** (`BR17-01..03`) và **điều kiện hiển thị** (cờ rỗng, không phải null field) là **chung cho cả 8** — nếu để mỗi module tự assert thì sinh 8 bản sao của cùng 1 rule. ⇒ Đặt home ở `ACT` vì đây là màn **duy nhất có 2 empty state cạnh nhau** (`EMP-05` + `EMP-06`, mỗi tab một cái) nên kiểm 2 rule hình thức trong 1 lượt là rẻ nhất; các module khác **trỏ tới đây**, ⛔ không nhân bản. ⚠️ `BR17-02` (*"không hiện skeleton vô hạn — phân biệt rõ đang tải và không có dữ liệu"*) là rule **khó verify qua UI** ở mạng nhanh — cần throttle mạng; ghi ở `test_data_catalog.md`.

---

### REQ-ACT-008 · Text empty state 2 tab nay có bản chính thức *(MODIFIED)*
📍 `DOC-v1.1-01 §8.17.1 bảng Danh mục empty state, dòng EMP-05 / EMP-06 · trang 51` · `§6.2 AC-29.1.01 · trang 28`  ·  Clarif: `C-ORD-06`

> Nguồn (v1.0) — `DOC-v1.0-06 KP-02 §5 dòng C-ORD-06`: text empty state **chưa chốt** — từng Resolved 2026-07-28 rồi **REVERT** 2026-07-29 vì chốt không kèm bằng chứng.

> Nguồn (v1.1) #1 — EMP-05 (§8.17.1, trang 51):
> "EMP-05 | Đơn của tôi — tab Đang chạy | "Không có đơn đang thực hiện" | "Đăng tin gửi hàng""

> Nguồn (v1.1) #2 — EMP-06 (§8.17.1, trang 51):
> "EMP-06 | Đơn của tôi — tab Hoàn tất | "Chưa có đơn hoàn tất" — ẩn luôn khối lịch sử | —"

↳ **Ghi chú (diff):** ⭐ **Đây là CL lan rộng nhất của dự án được đóng** — `C-ORD-06` chạm **5 màn / 6 SC** và **home canonical của nó là module này**. Lần chốt trước bị revert sau đúng 1 ngày vì không kèm bằng chứng; lần này nguồn là **tài liệu đã phê duyệt** liệt kê đủ 8 dòng ⇒ Resolved bền. **Hai bất đối xứng phải assert, không được bỏ qua:** (a) `EMP-05` **có CTA** (`"Đăng tin gửi hàng"`) nhưng `EMP-06` **không** (cột CTA = `—`) — hai tab cạnh nhau, khác nhau có chủ đích; (b) `EMP-06` có thêm mệnh đề **"ẩn luôn khối lịch sử"** — một hành vi **ngoài** cấu trúc chuẩn của `BR17-01`, chỉ tab này có. ⇒ `SC-ACT-012`/`SC-ACT-014` hết `[GAP]`, nâng **P3 → P2**.

---

### REQ-ACT-001 · Nhãn 2 tab — theo app "Đang diễn ra / Đã hoàn thành" *(MODIFIED · BA chốt 2026-09-16)*
📍 `DOC-v1.1-01 §8.17.1 EMP-05 / EMP-06 · trang 51` · `§6.2 AC-09.1.01 · trang 19`  ·  Clarif: `C-ACT-02`

> Nguồn (v1.0) — `DOC-v1.0-02 §3.7` + `KP-01 §3 KB-ORD-07` (quan sát app 2026-07-27):
> "Màn Hoạt động có 2 tab: **Đang diễn ra** / **Đã hoàn thành**."

> Nguồn (v1.1) #1 — EMP-05 / EMP-06 (§8.17.1, trang 51):
> "Đơn của tôi — tab **Đang chạy**" · "Đơn của tôi — tab **Hoàn tất**"

> Nguồn (v1.1) #2 — AC-09.1.01 Then (§6.2, trang 19):
> "Hiện badge "Hết hạn" ở tab **Hoàn tất** kèm lý do "Không có ai nhận mang giúp trong thời gian đăng"."

↳ **Ghi chú (diff):** 🔴 **Xung đột nhãn giữa PRD và app STG.** PRD gọi 2 tab là **"Đang chạy"** / **"Hoàn tất"**, nhất quán ở **3 chỗ độc lập** (`EMP-05`, `EMP-06`, `AC-09.1.01`) — không phải lỗi đánh máy một lần. App STG (quan sát 2026-07-27, `KB-ORD-07`) hiển thị **"Đang diễn ra"** / **"Đã hoàn thành"**. PRD cũng gọi cả màn là **"Đơn của tôi"** trong khi v1.0 ghi nhận tên màn là *"Hoạt động"* (bottom nav) với tiêu đề trong màn là *"Đơn của tôi"*. ⇒ Theo `Project_rule §Custom Rules §10.1` (*UI phải khớp Tài liệu mới được viết TC*), đây là **xung đột cần chốt trước khi assert nhãn** — mở `C-ACT-02`. ⛔ **KHÔNG tự chọn bên nào**: chọn PRD thì TC FAIL hàng loạt trên app hiện tại; chọn app thì hợp thức hoá việc app lệch đặc tả. `SC-ACT-001` giữ assert *"có đúng 2 tab"* và **hạ phần nhãn xuống ghi nhận** cho tới khi `C-ACT-02` được chốt.

⛔ **Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC, đừng trích lại:** BA trả lời `C-ACT-02` — *"a. Đơn của tôi. Tab Đang diễn ra|Đã hoàn thành · b. PRD Ba chưa cập nhật nhé · c. Vẫn là Hoạt động"*. Hiện hành: nhãn **theo app**, PRD lỗi thời ⇒ `SC-ACT-001` assert cứng "Đơn của tôi" · "Đang diễn ra" · "Đã hoàn thành" · nav "Hoạt động".

---

### REQ-ACT-004 · Nội dung tab "Hoàn tất": thêm đơn RETURNED và đơn EXPIRED *(MODIFIED)*
📍 `DOC-v1.1-01 §6.2 AC-24.2.01 · trang 25` · `AC-09.1.01 · trang 19`  ·  Clarif: —

> Nguồn (v1.0) — `DOC-v1.0-02 §3.7 đoạn 3` + `DOC-v1.0-01 §D1b US-D04 L166`:
> "Tab 'Đã hoàn thành' liệt kê các đơn đã kết thúc."

> Nguồn (v1.1) #1 — AC-24.2.01 Then (§6.2, trang 25):
> "Đơn hiển thị lý do hoàn hàng và nằm trong lịch sử đơn, nhưng không cộng vào "Đơn đã giúp" của người vận chuyển."

> Nguồn (v1.1) #2 — AC-09.1.01 Then (§6.2, trang 19):
> "Tin chuyển sang EXPIRED, biến khỏi bảng tin và khỏi luồng khớp tuyến. Hiện badge "Hết hạn" ở tab Hoàn tất kèm lý do "Không có ai nhận mang giúp trong thời gian đăng"."

↳ **Ghi chú (diff):** v1.1 sinh thêm **một kết cục đơn chưa từng có ở v1.0** — `RETURNED` (hoàn hàng, từ `FR09`) — và `AC-24.2.01` nói rõ nó **nằm trong lịch sử đơn** kèm **lý do hoàn hàng**. ⇒ `SC-ACT-015` **NEW**: đơn `RETURNED` phải xuất hiện ở tab kết thúc **và hiện lý do**, chứ không biến mất như đơn "Đã huỷ" (`SC-ACT-007`, rule ẩn của v1.0). Đây là **cặp đối chứng đáng giá**: cùng là đơn kết thúc bất thường nhưng một cái **ẩn** (`CANCELLED`) và một cái **hiện kèm lý do** (`RETURNED`) — dễ bị dev xử lý gộp thành một nhánh. `AC-09.1.01` đồng thời **chốt vị trí** của đơn `EXPIRED` là **tab Hoàn tất** (v1.0 chỉ biết có badge "Hết hạn", không chắc nó nằm tab nào) ⇒ `SC-ACT-005` siết thêm.

---

### REQ-ACT-005 · Card "Hết hạn": lý do nay có chuỗi verbatim *(MODIFIED)*
📍 `DOC-v1.1-01 §8.5.1 BR05-03 · trang 38` · `§6.2 AC-09.1.01 · trang 19`  ·  Clarif: —

> Nguồn (v1.0) — `DOC-v1.0-06 KP-01 §3 KB-ORD-07 (#4,#6)` (quan sát app): card "Hết hạn" **có** lý do, nhưng **chuỗi lý do lấy từ màn hình**, không từ tài liệu.

> Nguồn (v1.1) — BR05-03 (§8.5.1, trang 38):
> "Hết ngày cuối của khoảng ngày mà đơn vẫn POSTED thì chuyển EXPIRED; hiện badge "Hết hạn" kèm lý do "Không có ai nhận mang giúp trong thời gian đăng"."

↳ **Ghi chú (diff):** Hành vi không đổi; **chuỗi lý do nay là text chính thức** ⇒ `SC-ACT-008` đổi từ *"card có kèm lý do"* (PASS với bất kỳ chuỗi nào) sang **assert verbatim**. `BR05-03` còn phát biểu rõ **điều kiện kích hoạt** — *"hết ngày cuối của khoảng ngày mà đơn **vẫn POSTED**"* — tức đơn đã `MATCHED` thì không chuyển `EXPIRED` dù quá ngày; v1.0 chưa nêu vế `vẫn POSTED` này. ⚠️ Cross-ref: ngưỡng `EXPIRED` = **"Đến ngày"** đã Resolved ở `C-ORD-03` (v1.0) — PRD xác nhận lại, không đảo.

---

### REQ-ACT-009 · ★★★★★ leftover trên card tab Hoàn tất — nay là defect xác nhận *(MODIFIED)*
📍 `DOC-v1.1-01 §8.14.1 BR14-03 · trang 49` · `§4 SCOPES dòng Out of Scope · trang 9`  ·  Clarif: —

> Nguồn (v1.0) — `DOC-v1.0-02 §3.7 đoạn 3` + `KP-01 §6 KB-GIFT-02`, gắn `C-GIFT-01` Resolved *"Out of scope **v1.0**"* ⇒ SC chỉ **ghi nhận**.

> Nguồn (v1.1) #1 — BR14-03 (§8.14.1, trang 49):
> "Không có chấm sao 1–5, không điểm, không tier/xếp hạng, không chỉ số môi trường."

> Nguồn (v1.1) #2 — §4 SCOPES, Out of Scope (trang 9):
> "Đánh giá sao 1–5 và mọi hình thức xếp hạng/tier/điểm thưởng — thay bằng quà ảo"

↳ **Ghi chú (diff):** 🔴 **Đổi phân loại, không đổi hành vi.** Ở v1.0, phán quyết *"out of scope **v1.0**"* khiến ★ leftover đọc được thành *"tính năng phase sau lộ sớm"* ⇒ `SC-ACT-013` chỉ dám gắn nhãn `[GAP]` và **không log bug**. v1.1 đưa đánh giá sao vào **Out of Scope của cả sản phẩm** với chữ *"thay bằng quà ảo"* (thay thế, không phải hoãn) ⇒ ★ còn sót **là defect**, đủ căn cứ log bug. Home của phán quyết là `C-GIFT-01` ở module `GIFT` — ở đây chỉ **áp dụng**, ⛔ không tạo CL trùng.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
