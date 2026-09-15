# Requirement Traceability — v1.1 · Module CNL

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation` của `DOC-v1.1-01` = `FR<NN>` / `BR<FF>-NN` / `AC-{US}.{Scenario}.{Case}` / `VAL-NN` ⇒ **Schema A**.
> Chỉ chứa REQ **NEW + MODIFIED** của lượt delta này. REQ CARRIED nguyên trạng — xem `v1.0/CNL-huy-don/requirement_traceability.md`, KHÔNG lặp lại ở đây.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module CNL — DOC-v1.1-01

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-CNL-008 | `AC-25.2.01`, `BR11-04`, `FR16` | `DOC-v1.1-01` §6.2 AC-25.2.01 (trang 26) · §8.11.1 BR11-04 (trang 44) · §8.16 (trang 50) | SC-CNL-014, SC-CNL-015 | C-CNL-01 |
| REQ-CNL-002 *(MODIFIED)* | `VAL-04`, `VAL-03`, `BR11-01`, `AC-25.1.03` | `DOC-v1.1-01` §8.18.2 VAL-03/VAL-04 (trang 52) · §8.11.1 BR11-01 (trang 44) · §6.2 AC-25.1.03 (trang 26) | SC-CNL-004, SC-CNL-012 | — |
| REQ-CNL-003 *(MODIFIED)* | `BR11-04`, `AC-25.2.01`, `FR11` Pre-Conditions | `DOC-v1.1-01` §8.11 (trang 44) · §8.11.1 BR11-04 · §6.2 AC-25.2.01 (trang 26) | SC-CNL-005, SC-CNL-006, SC-CNL-016 | C-CNL-01 |
| REQ-CNL-006 *(MODIFIED)* | `BR11-02`, `BR11-03`, `AC-25.1.01`, `AC-25.1.02` | `DOC-v1.1-01` §8.11.1 BR11-02/BR11-03 (trang 44) · §6.2 AC-25.1.01/AC-25.1.02 (trang 26) | SC-CNL-009, SC-CNL-010 | C-CNL-02 |
| REQ-CNL-007 *(MODIFIED)* | `FR16`, `AC-25.2.01` | `DOC-v1.1-01` §8.16 (trang 50) · §6.2 AC-25.2.01 (trang 26) | SC-CNL-006 *(hết gap chủ đích)* | C-CNL-01 |
| REQ-CNL-009 | `FR11` Actor | `DOC-v1.1-01` §8.11 dòng Actor (trang 44) | SC-CNL-017 | C-CNL-03 |

> ℹ️ `REQ-CNL-001` · `REQ-CNL-004` · `REQ-CNL-005` **CARRIED không đổi** — PRD `BR11-01..04` và `AC-25.1.01/02` xác nhận lại đúng nội dung đã phân tích ở v1.0, không thêm ràng buộc mới ⇒ ⛔ không tạo dòng MODIFIED giả.

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-CNL-008 · Sau IN_TRANSIT chỉ còn hai đường thoát: hoàn hàng hoặc báo sự cố (`AC-25.2.01`)
📍 `DOC-v1.1-01 §6.2 AC-25.2.01 "Sau khi hàng đã lên đường" · trang 26`  ·  Clarif: `C-CNL-01`

> Nguồn #1 — AC-25.2.01 (§6.2, trang 26):
> "Given: Đơn ở IN_TRANSIT hoặc muộn hơn. When: Bất kỳ vai trò nào mở màn theo dõi đơn. Then: Không còn thao tác huỷ đơn thường cho bất kỳ ai. Chỉ còn hai đường: hoàn hàng (RETURNING) hoặc báo sự cố (INCIDENT). Đơn ở INCIDENT không tự về COMPLETED, phải qua admin hỗ trợ."

> Nguồn #2 — BR11-04 (§8.11.1, trang 44):
> "Từ IN_TRANSIT trở đi không còn huỷ đơn thường cho bất kỳ vai trò nào."

↳ **Ghi chú:** ⭐ **REQ MỚI — đây là mảnh ghép mà v1.0 thiếu.** v1.0 chỉ chốt được **vế chặn** (`SC-CNL-005`: không huỷ được từ "Đang giao") vì `BR-ASN-03` nói *"phải tạo sự cố"* nhưng không tài liệu nào mô tả màn đó ⇒ `C-CNL-01` Resolved theo hướng **out of scope**, `REQ-CNL-007` để **gap SC có chủ đích**. PRD v1.1 giờ nêu đủ **cả hai đường thoát** và đặc tả luồng báo sự cố ở `FR16` ⇒ vế *"phải tạo sự cố"* **có oracle để assert**. ⚠️ Chữ **"huỷ đơn thường"** ở `BR11-04` là chữ của PRD — nó hàm ý tồn tại đường huỷ **không thường** (qua admin, từ `INCIDENT`), nhưng PRD **không đặc tả** đường đó ⇒ xem `C-CNL-03`. **Ranh giới module:** bề mặt *báo sự cố* (nút trigger + form WebView) thuộc `TS` (`REQ-TS-006`, `SC-TS-008..015`); ở `CNL` chỉ assert **ma trận đường thoát** và **hệ quả trạng thái** — ⛔ không nhân bản SC của `TS`.

---

### REQ-CNL-002 · Lý do huỷ ≥ 5 ký tự và phải trim khoảng trắng trước khi đếm (`VAL-04` + `VAL-03`) *(MODIFIED)*
📍 `DOC-v1.1-01 §8.18.2 VAL-03/VAL-04 · trang 52` · `§8.11.1 BR11-01 · trang 44` · `§6.2 AC-25.1.03 · trang 26`  ·  Clarif: —

> Nguồn (v1.0) — `DOC-v1.0-01 §D8.3 VAL-04 · L395`:
> "Huỷ đơn: bắt buộc lý do ≥ 5 ký tự mới bật nút xác nhận."

> Nguồn (v1.1) #1 — VAL-04 (§8.18.2, trang 52) — **nguyên văn không đổi**:
> "Huỷ đơn: bắt buộc lý do ≥ 5 ký tự mới bật nút xác nhận."

> Nguồn (v1.1) #2 — VAL-03 (§8.18.2, trang 52):
> "Tự cắt khoảng trắng đầu/cuối; chuẩn hoá số điện thoại trước khi lưu."

> Nguồn (v1.1) #3 — BR11-01 (§8.11.1, trang 44):
> "Lý do huỷ là bắt buộc, tối thiểu 5 ký tự, mới bật nút xác nhận."

> Nguồn (v1.1) #4 — AC-25.1.03 (§6.2, trang 26):
> "Given: Người dùng đang ở popup huỷ đơn. When: Người dùng nhập lý do dưới 5 ký tự hoặc để trống. Then: Nút xác nhận huỷ vô hiệu hoá; hiện lỗi dưới ô lý do. Trạng thái đơn không đổi."

↳ **Ghi chú (diff):** **Nội dung rule KHÔNG đổi — nhưng THẨM QUYỀN của nó đổi hẳn, và đó mới là điều quan trọng.** Ở v1.0, `VAL-03`/`VAL-04` chỉ có trong BRD trong khi app cho qua cả "4 ký tự" lẫn "5 dấu cách" ⇒ 2 SC (`SC-CNL-004`, `SC-CNL-012`) viết theo spec và **dự kiến FAIL**, nhưng nền tảng để log bug là BRD + 1 quyết định override của QA. Nay **PRD chính thức của PM** (mã `1.0-BM/PM/HDCV/FTEL`) lặp lại rule ở **ba chỗ độc lập** (`BR11-01`, `VAL-04`, `AC-25.1.03`) và bổ sung `VAL-03` áp cho **toàn bộ form** ⇒ 2 gap này không còn là "app khác tài liệu tham khảo" mà là **vi phạm đặc tả đã phê duyệt**. ⇒ ⛔ **Không còn chỗ cho lập luận "sửa expected cho PASS"**; log bug với severity cao hơn v1.0. ⚠️ `AC-25.1.03` nêu thêm **2 hành vi mà v1.0 chưa assert**: nút *"vô hiệu hoá"* (chứ không phải bấm được rồi báo lỗi) và *"hiện lỗi **dưới ô** lý do"* (vị trí cụ thể) ⇒ 2 SC MODIFIED phải siết Then theo đúng 2 chi tiết này.

---

### REQ-CNL-003 · Điều kiện được huỷ: POSTED, hoặc MATCHED khi chưa bấm "Tôi đã lấy hàng" *(MODIFIED)*
📍 `DOC-v1.1-01 §8.11 dòng Pre-Conditions · trang 44` · `§8.11.1 BR11-04` · `§6.2 AC-25.2.01 · trang 26`  ·  Clarif: `C-CNL-01`

> Nguồn (v1.0) — `DOC-v1.0-01 §D7 OPR-11 · L347`:
> "Sau khi người vận chuyển đã nhận hàng (IN_TRANSIT) thì KHÔNG ai được huỷ đơn thường."

> Nguồn (v1.1) #1 — FR11 Pre-Conditions (§8.11, trang 44):
> "Đơn ở POSTED, hoặc MATCHED khi chưa bấm "Tôi đã lấy hàng""

> Nguồn (v1.1) #2 — AC-25.1.01 (§6.2, trang 26):
> "Given: Đơn ở POSTED hoặc MATCHED, người vận chuyển chưa bấm "Tôi đã lấy hàng"."

↳ **Ghi chú (diff):** v1.0 mô tả ngưỡng bằng **trạng thái** (`IN_TRANSIT` trở đi thì cấm). v1.1 mô tả bằng **hành động** (*"chưa bấm 'Tôi đã lấy hàng'"*) — **cùng một ngưỡng, nhưng phát biểu theo hành động cho ra một ô test mà cách phát biểu theo trạng thái không lộ ra**: khoảnh khắc đơn **vẫn đang `MATCHED`** nhưng người vận chuyển **đã bấm** "Tôi đã lấy hàng" (bấm rồi nhưng popup xác nhận chưa xong / request chưa trả về). ⇒ `SC-CNL-016` **NEW** cho đúng ô đó. Vế *"phải tạo sự cố"* của `BR-ASN-03` (v1.0 không assert được) nay có đích đến rõ ràng — xem `REQ-CNL-008`.

---

### REQ-CNL-006 · Nhật ký huỷ: ghi đủ vai trò + lý do + thời điểm, và KHÔNG được xoá bản ghi lần ghép trước *(MODIFIED)*
📍 `DOC-v1.1-01 §8.11.1 BR11-02 / BR11-03 · trang 44` · `§6.2 AC-25.1.01 / AC-25.1.02 · trang 26`  ·  Clarif: `C-CNL-02`

> Nguồn (v1.0) — `DOC-v1.0-06 KP-01 §7 KB-CNL-01` (live-verify 2026-07-29) + `C-CNL-02` Resolved-override 2026-07-30:
> "Huỷ đơn không ghi log nào, chỉ hiện banner đỏ. Huỷ nhận đơn XOÁ dòng 'Ghép thành công' khỏi LỊCH SỬ."

> Nguồn (v1.1) #1 — BR11-02 (§8.11.1, trang 44):
> "Nhật ký ghi rõ vai trò người huỷ, lý do và thời điểm; trạng thái đồng bộ cho cả ba vai trò."

> Nguồn (v1.1) #2 — BR11-03 (§8.11.1, trang 44):
> "Người vận chuyển huỷ nhận khi chưa lấy hàng → đơn về POSTED và hiển thị lại trên bảng tin; bản ghi lần ghép trước vẫn giữ trong nhật ký."

> Nguồn (v1.1) #3 — AC-25.1.02 (§6.2, trang 26):
> "Then: Đơn quay về POSTED và hiển thị lại trên bảng tin để người khác nhận. Người gửi nhận thông báo. Nhật ký giữ nguyên bản ghi lần ghép trước (không xoá được)."

↳ **Ghi chú (diff):** ⭐ **Thay đổi quan trọng nhất của lượt delta này cho module `CNL`.** Ở v1.0, `REQ-CNL-006` là **REQ do QA/user ban hành để OVERRIDE hành vi hiện tại** — cột `Maps (Ref DOC)` ghi thẳng *"— (override hành vi hiện tại)"* vì **không tài liệu nào yêu cầu** giữ log; nó chỉ dựa vào `BR-INT-04`/`TS-02` suy ra. Nay PRD phát biểu **trực tiếp, bằng chính ngôn ngữ của lỗi**: `BR11-03` viết *"bản ghi lần ghép trước **vẫn giữ** trong nhật ký"* và `AC-25.1.02` đóng đinh *"(không xoá được)"*. ⇒ `SC-CNL-010` chuyển từ *"SC theo rule suy ra, dự kiến FAIL"* thành **vi phạm đặc tả đã phê duyệt** — nâng **P2 → P1**, và `C-CNL-02` không còn là *"Resolved theo hướng override"* mà là **Resolved theo doc**. ⚠️ `BR11-02` nêu **ba** thành phần bắt buộc của dòng log (vai trò · lý do · **thời điểm**); v1.0 `SC-CNL-008` mới assert 2 (vai trò + lý do) ⇒ SC đó cần siết thêm **timestamp** khi generate TC.

---

### REQ-CNL-007 · Màn "Báo sự cố" — hết gap chủ đích, chuyển giao bề mặt sang `TS` *(MODIFIED)*
📍 `DOC-v1.1-01 §8.16 "FR16 — Báo cáo sự cố & hỗ trợ" · trang 50` · `§6.2 AC-25.2.01 · trang 26`  ·  Clarif: `C-CNL-01`

> Nguồn (v1.0) — `DOC-v1.0-01 §D2 · L233` (`[INCIDENT]` có tên trong sơ đồ vòng đời nhưng không mô tả field/màn) ⇒ `C-CNL-01` Resolved: *"Out of scope v1.0 (chưa có đặc tả field)"*.

> Nguồn (v1.1) — §4 SCOPES, dòng In-scope (trang 9):
> "Báo cáo sự cố qua Google Form nhúng WebView (Phase 1)"

↳ **Ghi chú (diff):** 🔴 **Kết luận v1.0 bị ĐẢO.** `REQ-CNL-007` ở v1.0 là **gap SC có chủ đích** (`CHANGELOG §3` nợ #2) với lý do *"không tài liệu nào mô tả field/màn"*. Lý do đó **không còn đúng**: PRD v1.1 xếp tính năng vào **In-scope** và đặc tả đủ ở `FR16`. ⇒ gap chủ đích **đóng lại**; `SC-CNL-006` (v1.0 chỉ *ghi nhận sự thiếu vắng bề mặt*) phải **lật thành assert khẳng định** — nút "Báo cáo sự cố" **phải tồn tại** ở màn theo dõi đơn. ⚠️ **Bề mặt chi tiết KHÔNG thuộc module này:** form WebView, trần 5 ảnh, prefill ngữ cảnh đơn… đã có home ở `TS` (`REQ-TS-006`). `CNL` chỉ giữ **vế nút thoát tồn tại** và **hệ quả trạng thái** (`REQ-CNL-008`) — ⛔ đừng viết lại 8 SC của `TS` ở đây.

---

### REQ-CNL-009 · "Admin vận hành" là actor của luồng huỷ đơn (`FR11` Actor)
📍 `DOC-v1.1-01 §8.11 dòng Actor · trang 44`  ·  Clarif: `C-CNL-03`

> Nguồn — FR11 Actor (§8.11, trang 44):
> "Người gửi · Người vận chuyển · Người nhận · Admin vận hành"

↳ **Ghi chú:** **REQ MỚI nhưng gần như chắc chắn KHÔNG test được qua UI end-user.** v1.0 liệt kê 3 vai (`§D4` permission matrix có cột `Admin` đánh `✓` nhưng đã kết luận Admin Portal out of scope — `C-TS-01`). PRD v1.1 đưa **Admin vận hành** thành actor chính thức của `FR11`, và `AC-25.2.01` nói đơn `INCIDENT` *"phải qua admin hỗ trợ"* — nhưng **không mục nào của PRD mô tả bề mặt Admin** (không màn, không field, không quyền cụ thể). ⇒ Ghi nhận REQ để traceability không đứt, `SC-CNL-017` là **SC dạng [GAP] ghi nhận** theo `Project_rule §Custom Rules §10.1` bước 3 — ⛔ KHÔNG viết TC khẳng định cho hành vi Admin. Câu hỏi mở ở `C-CNL-03`.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
