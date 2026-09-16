---
id: v1.0/GIFT-qua-cam-on/risk
title: Risk Assessment — v1.0 · Module GIFT
type: risk-assessment
version: v1.0
sprint: 1
module: GIFT
counts:
  cl: 3
  risk: 5
  cl_open: 2
  cl_resolved: 1
status: ANALYZED
updated: 2026-09-16
---

# Risk Assessment — v1.0 · Module GIFT

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module GIFT.
> 🔑 Frontmatter `counts:` = nguồn canonical CL/RISK — **chỉ đếm CL có home ở module này**; CL tham chiếu (home ở module khác) KHÔNG tính vào `counts`. **Layout v2 ⇒ đây là home của Clarification.**

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| GIFT | **Low** | Tính năng *"tương tác xã hội, không bắt buộc"*, không chặn luồng nào. Rủi ro thật: **toàn module phụ thuộc tiền đề đơn "Hoàn thành"**, và **nút chỉ dùng 1 lần/đơn** nên mỗi lần test tiêu 1 đơn |

## Chi tiết rủi ro (bảng hợp nhất)
| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-GIFT-01 | GIFT / Tiền đề | **12/12 SC phụ thuộc đơn ở "Hoàn thành"** — mà để có đơn Hoàn thành cần 3 vai phối hợp qua đủ 5 trạng thái; thêm nữa **nút chỉ dùng 1 lần/đơn** ⇒ mỗi lần test tiêu 1 đơn | Medium | `§A7` L107 · KP-01 §6 KB-GIFT-01 | Seed nhiều đơn Hoàn thành trước khi chạy lô | Chạy `GIFT` **ngay sau** `DLV` trong cùng lô để tái dùng đơn vừa hoàn tất | Open | REQ-GIFT-001, REQ-GIFT-003 |
| RISK-GIFT-02 | GIFT / Text popup | **2 nguồn 2 text popup** (`US-D15` *"Cảm ơn của bạn đã được gửi"* ⟷ PRD+Figma *"Đã gửi lời cảm ơn!"*) ⇒ TC assert text sẽ FAIL ở 1 trong 2 cách hiểu | Low | `US-D15` L194 vs `DOC-v1.0-02` §3.8 + Figma | Assert theo PRD+Figma (2 nguồn bề mặt) | Hỏi BA chốt (`C-GIFT-03`); tới khi đó dùng bản PRD+Figma | Open | REQ-GIFT-002, SC-GIFT-003 |
| RISK-GIFT-03 | GIFT / Danh sách lịch sử | Thành phần *"danh sách lịch sử nhận quà"* **chỉ có 1 nguồn văn bản** (`US-D20`), không có ảnh Figma/app ⇒ nếu viết TC khẳng định sẽ vi phạm `§Custom Rules §10.1` | Medium | `US-D20` L196 · KP-01 §6 KB-GIFT-03 (ghi chú: *"cần vibe-test xác nhận… không im lặng bỏ qua"*) | `SC-GIFT-007` ghi nhận có/không | Vibe-test màn "Quà đã nhận"; không có → mở CL, ⛔ không im lặng bỏ qua | Open | REQ-GIFT-004, SC-GIFT-007 |
| RISK-GIFT-04 | GIFT / UI leftover | Nhãn *"Bạn đã đánh giá"* và chuỗi *"Hoàn thành & đã đánh giá"* dùng từ **"đánh giá"** cho hành động **tặng quà** ⇒ người đọc sau dễ kết luận v1.0 có tính năng rating và viết TC chấm sao | Medium | KP-01 §6 KB-GIFT-01/KB-GIFT-02 · `DOC-v1.0-02` §5.2 | `SC-GIFT-011` assert-absent màn chấm sao | Ghi ràng buộc `CHANGELOG §2`; nêu với BA để đổi nhãn nếu được | Resolved | REQ-GIFT-003, REQ-GIFT-005 |
| RISK-GIFT-05 | GIFT / Back navigation | *(cập nhật Severity)* Nút back màn "Tặng quà" nhảy sang màn của **đơn khác** — đã tái hiện được với **đơn thật** (không chỉ item mẫu) qua vibe-check demo 2026-09-16, không còn là giả thuyết | Low → **Medium** | KP-01 §6 KB-GIFT-04 (`C-GIFT-02` Open) · vibe-check demo 2026-09-16 | `SC-GIFT-010` với **đơn thật** — nay có bằng chứng tái hiện, ưu tiên chạy sớm | Verify lại trên STG thật (khác kỹ thuật SPA của demo); nếu tái hiện → log bug ngay, mức độ **cao hơn đánh giá ban đầu** vì user có thể thao tác nhầm lên đơn của người khác | Open (ưu tiên cao hơn) | REQ-GIFT-006, SC-GIFT-010 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-GIFT-01 | Rating 1–5 sao (`RAT-01/02`) có thuộc v1.0? | ✅ Resolved — **Out of scope v1.0**; v1.0 chỉ có Quà ảo | 2026-07-27 | REQ-GIFT-005 |
| C-GIFT-02 | 🔴 Nút back màn "Tặng quà" nhảy sang màn của đơn khác | 🔴 **Open — tái hiện với đơn thật 2026-09-16, mức độ cao hơn đánh giá ban đầu** | kế thừa 2026-07-29 | REQ-GIFT-006 |
| C-GIFT-03 | 🔴 Text popup sau khi gửi quà + có "danh sách lịch sử nhận quà" hay không | 🔴 **Open** | mở 2026-09-07 | REQ-GIFT-002, REQ-GIFT-004 |
| C-ORD-06 | Text empty state (tham chiếu — home ở `ACT`) | 🔴 **Open** | mở lại 2026-07-29 | REQ-GIFT-007 |

### C-GIFT-01 · Rating 1–5 sao có thuộc v1.0?

**Source Quote (ambiguous — BRD mâu thuẫn 3-1):**
> Nguồn A (`DOC-v1.0-01` §D3 `RAT-01/02` L256): "RAT-01/02 | Đánh giá 2 chiều | 1–5 sao + nhận xét"
> Nguồn B (`§A5` `BR-INT-06` L82): "**Không đánh giá sao**; ghi nhận thiện chí bằng quà ảo người gửi tặng người vận chuyển sau khi hoàn tất"
> Nguồn C (`§A8` L125): "Phạm vi hiện tại: chỉ ghi log + admin can thiệp hỗ trợ. **KHÔNG có chấm sao/đánh giá**…"
> Nguồn D (`§A7` L111): "Không tính điểm, không tier/xếp hạng, không CO₂, không quy đổi tiền / thanh toán in-app"

**Source Location:** `DOC-v1.0-01 §D3 · RAT-01/02 · L256` ⟷ `§A5 · BR-INT-06 · L82` ⟷ `§A8 · L125` ⟷ `§A7 · L111`

**Analyst Note:** Resolved 2026-07-27: **out of scope v1.0** — 3 nguồn thắng 1, và `KB-GIFT-02` ghi rõ chuỗi `★★★★★ Đã đánh giá` trên card là **UI leftover**. 📌 **Hệ quả scope lớn nhất của cả dự án:** *"Đánh giá"* trong 5 luồng Phase 1 mà PM chốt (`KP-03 §3` dòng 5) = **Quà ảo (`GIFT-01`)**, không phải chấm sao ⇒ luồng #5 của Phase 1 chính là module này. ⛔ Không viết TC chấm sao ở bất kỳ module nào (`ACT` `SC-ACT-013`, `USR` `SC-USR-006`, `DLV` `SC-DLV-023` đều có ràng buộc tương ứng).

### C-GIFT-02 · 🔴 Nút back màn "Tặng quà" nhảy sai màn

**Source Quote (ambiguous):**
> "Bấm back (←) từ màn "Tặng quà" (mở từ item mẫu tab "Đã hoàn thành") nhảy tới màn "Xác nhận đã nhận hàng" của **một đơn KHÁC không liên quan**, thay vì quay về "Đơn của tôi"."
> "Clarification: `C-GIFT-02` Open — nhiều khả năng là giới hạn của bản demo (item mẫu tĩnh chưa wiring back-stack), CA đánh giá không nghiêm trọng."

**Source Location:** `DOC-v1.0-06 KP-01 §6 "KB-GIFT-04"`

**Analyst Note (2026-09-07):** Phát hiện trong ngữ cảnh **item mẫu tĩnh của bản demo** ⇒ chính nguồn cũng nghiêng về *"giới hạn demo"*. ⇒ `SC-GIFT-010` yêu cầu Given là **đơn thật trên STG**, ⛔ không kết luận bug từ dữ liệu mẫu. Nếu tái hiện với đơn thật thì mức độ: user có thể **thao tác nhầm trên đơn không liên quan** (vd bấm xác nhận nhận hàng của đơn khác) ⇒ nghiêm trọng hơn đánh giá ban đầu. **Non-blocking.**

↳ **Cập nhật 2026-09-16 — TÁI HIỆN được với đơn thật, không còn là giả thuyết:** Vibe-check qua demo (Playwright) — tạo và hoàn tất **một đơn thật từ đầu đến cuối** (Sender đăng tin → Carrier nhận/lấy/giao → Receiver xác nhận → COMPLETED), sau đó vào tab "Đã hoàn thành" bấm 1 item, mở đúng màn **"Tặng quà"**. Bấm nút back (←) trên màn "Tặng quà" → nhảy tới màn **"Xác nhận đã nhận hàng"** của một đơn **hoàn toàn khác, không liên quan** (carrier "Trần Thị Lan", địa chỉ khác, không phải đơn vừa thao tác).
**Analyst Note:** Đây **không còn là giới hạn của "item mẫu tĩnh"** như phỏng đoán ban đầu (2026-09-07) — bug tái hiện y hệt ngay cả khi thao tác trên một luồng nghiệp vụ thật, đầy đủ. Nhiều khả năng là lỗi **back-stack/history của SPA** (điều hướng không push đúng lịch sử, back nhảy tới 1 route ngẫu nhiên/còn sót trong stack) chứ không phải do dữ liệu mẫu. ⚠️ **Nâng mức độ ưu tiên:** cần verify khẩn trên STG thật (kỹ thuật khác — có thể dùng native navigation, không chắc lặp lại lỗi này) TRƯỚC `generate-tc`; nếu tái hiện trên STG thì log bug ngay với severity Medium/High (rủi ro thao tác nhầm lên đơn của người khác), không chờ đến khi execute.

### C-GIFT-03 · 🔴 Text popup + danh sách lịch sử nhận quà

**Source Quote (ambiguous):**
> Text popup — Nguồn A (`US-D15` §D1b L194): "popup **"Cảm ơn của bạn đã được gửi"** → nút "Về trang chủ""
> Text popup — Nguồn B (`DOC-v1.0-02` §3.8): "Xác nhận → modal **"Đã gửi lời cảm ơn!"**"
> Lịch sử — Nguồn C (`US-D20` §D1b L196): "màn Quà đã nhận hiển thị 1 card đếm số bông hoa/ly cà phê/gấu bông/vương miện + **danh sách lịch sử nhận quà**"
> Lịch sử — Nguồn D (`DOC-v1.0-06` KP-01 §6 KB-GIFT-03): "⚠ Thành phần "Danh sách lịch sử" **chỉ có bằng chứng văn bản US-D20**, chưa có ảnh Figma/app → **cần vibe-test xác nhận**."

**Source Location:** `DOC-v1.0-01 §D1b · US-D15 · L194` ⟷ `DOC-v1.0-02 §3.8` · `DOC-v1.0-01 §D1b · US-D20 · L196` ⟷ `DOC-v1.0-06 KP-01 §6 "KB-GIFT-03"`

**Analyst Note:** Hai câu hỏi gộp 1 CL vì cùng bề mặt module GIFT và cùng cần 1 lượt BA:
**(a)** Text popup sau khi gửi quà: *"Đã gửi lời cảm ơn!"* (PRD+Figma) hay *"Cảm ơn của bạn đã được gửi"* (`US-D15`)? Tạm dùng bản PRD+Figma (2 nguồn bề mặt).
**(b)** Màn "Quà đã nhận" **có** danh sách lịch sử nhận quà không? Chỉ 1 nguồn văn bản, chưa có ảnh ⇒ `SC-GIFT-007` ghi nhận. Nguồn D **tự yêu cầu** *"nếu app không có → mở clarification, không im lặng bỏ qua"* ⇒ CL này là việc thực thi đúng yêu cầu đó. **Non-blocking.**

## Khuyến nghị tổng thể
1. **Resolve trước generate-tc:** `C-GIFT-03(a)` — chốt text popup để TC assert được; `C-GIFT-03(b)` nên giải quyết bằng **vibe-test** thay vì chờ BA (nhanh hơn).
2. **Ưu tiên test:** không có P1. Chạy `SC-GIFT-005` (nút đổi nhãn) và `SC-GIFT-006` (card đếm count>0) sớm vì 2 rule này **hoàn toàn ngoài tài liệu** — nếu quan sát cũ sai thì phải sửa REQ.
3. **Cần môi trường/dữ liệu:** **nhiều đơn "Hoàn thành"** (mỗi lần test tặng quà tiêu 1 đơn) + **3 trạng thái tài khoản Carrier** (0 loại quà · 2/4 loại · 4/4 loại). ⛔ Chạy `GIFT` **ngay sau** `DLV` để tái dùng đơn vừa hoàn tất.
4. **ID/text cleanup (non-blocking, cần trước automation):** nhãn *"Bạn đã đánh giá"* dùng từ "đánh giá" cho hành động tặng quà — nêu với BA đổi nhãn; nếu giữ thì ghi rõ trong TC để người sau không hiểu là có rating.
