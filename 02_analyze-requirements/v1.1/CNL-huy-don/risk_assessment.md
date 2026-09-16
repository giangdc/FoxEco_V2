---
id: v1.1/CNL-huy-don/risk
title: Risk Assessment — v1.1 · Module CNL
type: risk-assessment
version: v1.1
sprint: 1
module: CNL
counts:
  cl: 3
  risk: 8
  cl_open: 0
  cl_resolved: 3
status: ANALYZED
updated: 2026-09-16
---

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (6 dòng, `RISK-CNL-01..06`) xem `v1.0/CNL-huy-don/risk_assessment.md` — KHÔNG lặp lại ở đây. **ID mới bắt đầu từ `RISK-CNL-07`.**

## Tổng quan
| Module | Risk Level | Rủi ro chính (delta v1.1) |
|--------|-----------|--------------|
| CNL | **High** (tăng từ Medium-High) | 3 gap đã live-verify của v1.0 (`RISK-CNL-01/02/03`) chuyển từ *"app khác tài liệu tham khảo"* thành **vi phạm đặc tả đã phê duyệt** — `BR11-02`/`BR11-03` nói trúng đúng hành vi đang lỗi. Thêm `RISK-CNL-07`: `INCIDENT` là trạng thái duy nhất **chỉ admin đóng được** mà app không có bất kỳ đường nào tới admin ⇒ nguy cơ đơn treo vĩnh viễn |

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-CNL-01 | CNL / Audit trail | *(cập nhật Severity + Why)* **Huỷ nhận đơn XOÁ dòng "Ghép thành công"** — nay vi phạm **trực tiếp** `BR11-03` (*"bản ghi lần ghép trước vẫn giữ trong nhật ký"*) và `AC-25.1.02` (*"không xoá được"*), không còn phải suy từ `BR-INT-04` | High → **High (căn cứ mạnh hơn hẳn)** | `DOC-v1.1-01` §8.11.1 BR11-03 · §6.2 AC-25.1.02 vs `KP-01` §7 KB-CNL-01 (live-verify 2026-07-29) | `SC-CNL-010` — **nâng P2 → P1** | Log bug ngay, gộp 1 report với `SC-TS-003` + `SC-DLV-062`; ⛔ không sửa expected cho PASS | Open | REQ-CNL-006, SC-CNL-010 |
| RISK-CNL-02 | CNL / Log huỷ | *(cập nhật Why)* **Huỷ đơn không ghi log nào**, chỉ banner đỏ — nay vi phạm `BR11-02`, và `BR11-02` còn đòi **3 thành phần** (vai trò · lý do · **thời điểm**) chứ không phải 2 như v1.0 assert | High | `DOC-v1.1-01` §8.11.1 BR11-02 · §6.2 AC-25.1.01 vs `KP-01` §7 KB-CNL-01 | `SC-CNL-009` (siết thêm timestamp) · `SC-CNL-008` khi generate TC | Log bug; `C-CNL-02` không còn là "override" mà là **Resolved theo doc** | Open | REQ-CNL-006, SC-CNL-009 |
| RISK-CNL-03 | CNL / VAL-03+VAL-04 | *(cập nhật Why + Test Focus)* Ngưỡng 5 ký tự không enforce **và** không trim — nay có **3 nguồn PRD độc lập** (`BR11-01` · `VAL-04` · `AC-25.1.03`) cộng `VAL-03` áp cho toàn bộ form | Medium | `DOC-v1.1-01` §8.11.1 BR11-01 · §8.18.2 VAL-03/VAL-04 · §6.2 AC-25.1.03 vs `KP-01` §7 KB-CNL-02 | `SC-CNL-004` + `SC-CNL-012` — Then siết thêm *"nút vô hiệu hoá"* + *"lỗi dưới ô lý do"* | Log 2 bug riêng (2 lỗi khác nhau) | Open | REQ-CNL-002, SC-CNL-004, SC-CNL-012 |
| RISK-CNL-06 | CNL / Scope | *(cập nhật Status)* PM xếp `CNL` out of scope Phase 1 (`KP-03 §3.1`) — nhưng **PRD v1.1 đặc tả đầy đủ `FR11`** và đưa huỷ đơn vào business process chính (`S-04`) ⇒ căn cứ "out of scope" đã yếu hẳn | Low → **Low (nghiêng về IN scope)** | `DOC-v1.1-01` §7.2 dòng FR11 · §5 Business Process vs `KP-03` §3.1 (2026-07) | — | Vẫn cần PM xác nhận bằng văn bản, nhưng **mặc định lập kế hoạch là IN scope** vì PRD mới hơn `KP-03` 2 tháng | Pending | toàn module |
| RISK-CNL-07 | CNL / Trạng thái treo | **(risk mới 2026-09-15)** `AC-25.2.01`: đơn `INCIDENT` *"phải qua admin hỗ trợ"* nhưng PRD không mô tả bề mặt Admin. **BA 2026-09-16 xác nhận:** chỉ nhận báo cáo qua Google Form, **dev hỗ trợ tay**, **không có màn hình hay tool**; dev đưa đơn về **trạng thái tuỳ ý**; người dùng **không thấy gì** trong lúc chờ ⇒ đơn thoát khỏi INCIDENT **hoàn toàn phụ thuộc thao tác tay của dev**, không SLA | High → **Accepted (rủi ro vận hành đã biết)** | `DOC-v1.1-01` §6.2 AC-25.2.01 · §8.11 Actor · BA trả lời `C-CNL-03` 2026-09-16 | `SC-CNL-015` (đơn không tự đóng) · `SC-CNL-017` (assert cứng: **không có** bề mặt Admin trong app) | Không còn là câu hỏi nghiệp vụ. ⚠️ Nêu trong test report như **rủi ro vận hành được chấp nhận** (đơn INCIDENT có thể treo nếu dev không xử lý); ⛔ không log bug cho việc thiếu bề mặt admin | Accepted | REQ-CNL-008, REQ-CNL-009, SC-CNL-015, SC-CNL-017 |
| RISK-CNL-08 | CNL / Ranh giới CNL⟷TS | **(risk mới)** Bề mặt *báo sự cố* có **2 home**: nút thoát + hệ quả trạng thái ở `CNL` (`SC-CNL-006/014/015`), form WebView + ảnh ở `TS` (`SC-TS-008..015`) ⇒ dễ viết trùng TC hoặc bỏ sót vùng giao | Low | Phân chia module theo `Project_rule §Module Codes`; `FR16` nằm vắt qua 2 module | — | Đã ghi ranh giới ở `requirement_traceability.md REQ-CNL-007` + `CHANGELOG §2`; khi `generate-tc` chạy 2 module này phải đọc chéo | Open (ghi nhận, non-blocking) | REQ-CNL-007, REQ-TS-006 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-CNL-01 | Màn "Báo sự cố" (Incident) — có đặc tả không? (**home canonical ở đây**) | ✅ **Resolved 2026-09-15 — ĐẢO kết luận v1.0: CÓ đặc tả, VÀO scope** | 2026-07-27 | REQ-CNL-003, REQ-CNL-007, REQ-CNL-008 |
| C-CNL-02 | Huỷ đơn / Huỷ nhận đơn có ghi log LỊCH SỬ không? (**home canonical ở đây**) | ✅ **Resolved 2026-09-15 — nâng cấp căn cứ: từ "override QA" thành "đặc tả PM"** | 2026-07-30 | REQ-CNL-006 |
| C-CNL-03 | Ai thực hiện được "huỷ không thường" / đóng đơn `INCIDENT`, và qua bề mặt nào? | ✅ **Resolved 2026-09-16 — BA: dev hỗ trợ tay qua báo cáo Google Form, không có màn/tool; trạng thái đích tuỳ dev; người dùng không thấy gì** | 2026-09-15 | REQ-CNL-008, REQ-CNL-009, SC-CNL-015, SC-CNL-017 |

### C-CNL-01 · Màn "Báo sự cố" — ĐẢO kết luận *(RESOLVED 2026-09-15)*

📍 `DOC-v1.1-01 §4 SCOPES dòng In-scope · trang 9` · `§8.16 · trang 50` · `§6.2 AC-25.2.01 · trang 26`

> ↪ *Quote `Báo cáo sự cố qua Google Form nhúng W…` — home ở `requirement_traceability.md` · `REQ-CNL-007` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

> `AC-25.2.01` Then: "Chỉ còn hai đường: hoàn hàng (RETURNING) hoặc báo sự cố (INCIDENT)."

↳ **Ghi chú:** 🔴 **Đây là lần đảo kết luận đầu tiên của dự án và nó xảy ra đúng ở home canonical.** Phán quyết cũ (2026-07-27) là *"Out of scope v1.0 — chưa có đặc tả field"*; lý do đó **hết hiệu lực** vì PRD v1.1 đã xếp In-scope + đặc tả đủ 6 business rule ở `FR16`. **Bản v1.0 KHÔNG bị sửa** (giữ nguyên làm hồ sơ lịch sử, đúng `Project_rule`) — dòng này là bản hiện hành. ⚠️ Hệ quả lan sang 2 chỗ khác đang trích `C-CNL-01`: `v1.0/DLV-giao-nhan/risk_assessment.md` (dòng CL tham chiếu) và `v1.0/DLV-giao-nhan/requirement_traceability.md REQ-DLV-015` — **2 chỗ đó thuộc v1.0, không sửa**; người đọc lần ra bản hiện hành qua dòng này và qua `CHANGELOG §2`.

### C-CNL-02 · Log LỊCH SỬ khi huỷ — nâng cấp căn cứ *(RESOLVED 2026-09-15)*

📍 `DOC-v1.1-01 §8.11.1 BR11-02 / BR11-03 · trang 44`

> "BR11-02 | Nhật ký ghi rõ vai trò người huỷ, lý do và thời điểm; trạng thái đồng bộ cho cả ba vai trò."

> "BR11-03 | Người vận chuyển huỷ nhận khi chưa lấy hàng → đơn về POSTED và hiển thị lại trên bảng tin; bản ghi lần ghép trước vẫn giữ trong nhật ký."

↳ **Ghi chú:** CL này ở v1.0 đã `Resolved` **theo hướng override** — user chốt *"PHẢI ghi log; hành vi hiện tại là gap cần dev bổ sung"* ngày 2026-07-30, nhưng **không có tài liệu nào chống lưng**. Nay PRD phát biểu trực tiếp ⇒ **kết luận không đổi, thẩm quyền đổi**. Ghi lại ở đây vì đây là thứ quyết định **severity của bug** khi log: trước là "app không theo mong muốn QA", nay là "app không theo đặc tả đã phê duyệt".

### C-CNL-03 · "Huỷ không thường" và đóng đơn INCIDENT — ai làm, qua đâu? *(mở 2026-09-15 → RESOLVED 2026-09-16, xem khối trả lời BA bên dưới)*

📍 `DOC-v1.1-01 §8.11.1 BR11-04 · trang 44` · `§8.11 dòng Actor · trang 44` · `§6.2 AC-25.2.01 · trang 26`

> `BR11-04`: "Từ IN_TRANSIT trở đi không còn huỷ đơn **thường** cho bất kỳ vai trò nào."

> `FR11` Actor: "Người gửi · Người vận chuyển · Người nhận · **Admin vận hành**"

> `AC-25.2.01`: "Đơn ở INCIDENT không tự về COMPLETED, **phải qua admin hỗ trợ**."

↳ **Ghi chú:** Ba câu trên cùng ám chỉ một đường xử lý **không-thường** do admin thực hiện, nhưng PRD **không đặc tả** nó: không màn, không field, không ma trận quyền, không SLA. Chữ *"thường"* ở `BR11-04` là chữ của PRD — đã rà toàn văn §8.1–§8.18 và §9, không mục nào định nghĩa "huỷ không thường". ⇒ **Câu hỏi cho BA/PM:** (a) Admin vận hành thao tác qua bề mặt nào — back-office riêng hay Google Form của `FR16`? (b) Đơn `INCIDENT` kết thúc ở trạng thái nào, và ai chuyển? (c) Người dùng cuối có thấy gì trong lúc chờ không? **Non-blocking** cho `generate-tc` (2 SC liên quan đều là dạng ghi nhận/GAP), nhưng **blocking cho việc kết luận đơn có bị treo hay không** — xem `RISK-CNL-07`.

> ⚠️ `C-CNL-01` và `C-CNL-02` đều **giữ ID v1.0** (không cấp ID mới) vì là **cùng một câu hỏi** được trả lời lại bằng nguồn mạnh hơn, không phải câu hỏi mới.

### C-CNL-03 · ↳ BA trả lời 2026-09-16 *(→ RESOLVED)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `CNL` · cột "Câu trả lời BA" · 2026-09-16

> "a. hiên tại chỉ  nhận báo cáo quá gg form, dev hỗ trợ tay, không có màn hình hay tool
> b. dev hỗ trợ đến trạng tùy ý (phụ thuộc dev)
> c. Không"

↳ **Ghi chú:** (a) **Không có** bề mặt Admin — kênh duy nhất là Google Form của `FR16`, dev xử lý **ngoài app** ⇒ `SC-CNL-017` assert cứng *"không có chức năng Admin trong app end-user"*; `SC-DLV-060` (admin can thiệp có log) chỉ quan sát được **nếu** dev thao tác qua API ghi log — không đảm bảo. (b) Đơn `INCIDENT` kết thúc ở **trạng thái bất kỳ** dev chọn ⇒ ⛔ không viết TC assert trạng thái đích sau INCIDENT. (c) Người dùng **không** nhận thông báo/thông tin gì trong lúc chờ ⇒ ⛔ không viết TC chờ banner/thông báo "đang được hỗ trợ". `RISK-CNL-07` → **Accepted**. ⚠️ Câu trả lời **không nói** đơn **vào** `INCIDENT` bằng cách nào (tự động khi gửi form hay dev đặt tay) → hỏi ở `C-TS-02`; và *"chuyển admin hỗ trợ"* ở các mốc nhắc → `C-DLV-07`.

## Khuyến nghị tổng thể
1. **3 bug đã biết của module này nay có căn cứ PRD — ưu tiên log ngay** (`SC-CNL-004` · `SC-CNL-009` · `SC-CNL-010` · `SC-CNL-012`). Gộp `SC-CNL-010` + `SC-TS-003` + `SC-DLV-062` thành **1 bug report 3 góc nhìn** (luồng huỷ · thuộc tính audit · `NFR-07` append-only), ⛔ đừng log 3 bug rời cho cùng một nguyên nhân gốc.
2. **`SC-CNL-006` là SC nguy hiểm nhất khi chạy nhầm bản** — bản v1.0 và v1.1 có Then **ngược nhau**. Trước khi execute phải xác nhận đang dùng bản `v1.1/`; xem cảnh báo ở `CHANGELOG §2`.
3. 🟡 **`RISK-CNL-07` Accepted 2026-09-16** — BA xác nhận không có màn/tool admin, dev xử lý tay, không SLA ⇒ **ghi vào test report như rủi ro vận hành được chấp nhận** (đơn INCIDENT có thể treo nếu dev không xử lý); ⛔ không log bug cho việc thiếu bề mặt admin. Nguồn gốc trạng thái INCIDENT → `C-TS-02`.
4. **Xác nhận lại scope với PM** (`RISK-CNL-06`): `KP-03 §3.1` (2026-07) xếp `CNL` out-of-scope Phase 1, nhưng PRD v1.1 (09/2026) đặc tả đầy đủ `FR11` và đặt nó vào business process chính ⇒ **mặc định lập kế hoạch là IN scope**.
5. **Khi `generate-tc` chạy `CNL` và `TS`, đọc chéo ranh giới** (`RISK-CNL-08`) — `FR16` vắt qua 2 module, dễ sinh TC trùng.
