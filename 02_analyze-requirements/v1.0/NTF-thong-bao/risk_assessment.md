---
id: v1.0/NTF-thong-bao/risk
title: Risk Assessment — v1.0 · Module NTF
type: risk-assessment
version: v1.0
sprint: 1
module: NTF
counts:
  cl: 2
  risk: 6
  cl_open: 1
  cl_resolved: 0
status: ANALYZED
updated: 2026-09-07
---

# Risk Assessment — v1.0 · Module NTF

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module NTF.
> 🔑 Frontmatter `counts:` = nguồn canonical CL/RISK — **chỉ đếm CL có home ở module này**; CL tham chiếu (home ở module khác) KHÔNG tính vào `counts`. **Layout v2 ⇒ đây là home của Clarification.**
> 📌 **Home canonical của `C-NTF-01`** (danh sách loại thông báo) và **`C-NTF-03`** (đánh dấu đã đọc + phân trang). `C-NTF-02` (khớp tuyến) home ở `ASN`.

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| NTF | **Medium** | **Danh sách loại thông báo chính thức chưa chốt** — 3 nguồn cho 3 danh sách, BRD tự khai `§D6` là *"Nháp — chờ BA review & bổ sung"* ⇒ không assert được nội dung/danh mục. Kèm rủi ro bảo mật: **push có thể lọt SĐT** |

## Chi tiết rủi ro (bảng hợp nhất)
| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-NTF-01 | NTF / Danh mục thông báo | **3 nguồn 3 danh sách**; BRD `§D6` tự khai *"Nháp — chờ BA review & bổ sung"*; `KP-07` có 12 hàng ứng viên mà BA **chưa chọn** ⇒ không assert được danh mục, và có nguy cơ bỏ sót loại thông báo thật (vd #10 *"Sắp đến khung giờ hẹn giao"* có ở Demo+Figma nhưng không có trong BRD) | **High** | `§D6` L315 · `DOC-v1.0-02` §3.2 · `DOC-v1.0-04` · `KP-07` (bảng unified) | `SC-NTF-014` ghi nhận danh sách thật, đối chiếu 12 hàng | Hỏi BA chọn 1 trong 3 hướng của `KP-07`; tới khi đó dùng **hướng (c)** làm baseline | Open | REQ-NTF-010, SC-NTF-014 |
| RISK-NTF-02 | NTF / Bảo mật push | Nội dung **push do backend đẩy, không đi qua UI** ⇒ là kênh dễ lọt SĐT nhất; `OPR-07` cấm đưa SĐT vào push | **High** | `OPR-07` L343 · `§D6` L315 | `SC-NTF-008` (P1) — kiểm **cả in-app và push** cho mọi sự kiện | Chạy sớm; FAIL → log bug P1 (rủi ro dữ liệu cá nhân) | Open | REQ-NTF-005, SC-NTF-008 |
| RISK-NTF-03 | NTF / Cơ chế đọc | Cơ chế *"Đánh dấu đã đọc"* (mark-all vs mark-per-item) **chưa chốt** và bằng chứng chấm đỏ chỉ là **gián tiếp** (suy từ 1 ảnh Figma) ⇒ `SC-NTF-013` (chuông đồng bộ) khó thực hiện nhất quán vì bước "đọc hết" không xác định | Medium | `KP-01` §8 KB-NTF-01 (`C-NTF-03a` Open) | `SC-NTF-011` ghi nhận cơ chế; `SC-NTF-010` assert trạng thái hiển thị | Hỏi BA (`C-NTF-03a`); vibe-test thử cả 2 cách (tap item / bấm nút) | Open | REQ-NTF-007, SC-NTF-011, SC-NTF-013 |
| RISK-NTF-04 | NTF / Text `NTF-06` | **2 nguồn 2 text** cho thông báo hoàn tất: BRD *"Đơn đã hoàn tất — cảm ơn bạn!"* ⟷ PRD+Figma *"Đơn đã hoàn thành — **đánh giá ngay**"* — bản sau dùng từ "đánh giá" trong khi rating đã defer | Medium | `§D6` L324 vs `KP-07` hàng #6 · `C-GIFT-01` | `SC-NTF-005` ghi nhận text thật, ⛔ không assert | Đưa vào `C-NTF-01` để BA chốt cùng danh mục | Open | REQ-NTF-003, SC-NTF-005 |
| RISK-NTF-05 | NTF / Tiền đề | Mọi thông báo là **hệ quả của sự kiện ở module khác** ⇒ phủ 16 SC cần chạy trọn 1 vòng đời đơn + 1 lượt huỷ + 1 tin quá hạn (⛔ không seed qua UI) | Medium | `test_data_catalog.md` §Ghi chú chung | Chạy `NTF` **cuối lô** để tận dụng thông báo đã phát sinh | Lập lịch chạy `NTF` sau `ORD`/`ASN`/`DLV`/`GIFT`/`CNL`; nhờ dev seed tin quá hạn | Open | toàn module |
| RISK-NTF-06 | NTF / Scope | PM xếp `NTF` **out of scope Phase 1** (`KP-03 §3.1`) nhưng đợt cũ **vẫn viết 27 TC** (sheet `TC_03`); lượt này phân tích đầy đủ 16 SC theo quyết định 2026-09-07 | Low | `KP-03` §3.1 · quyết định scope 2026-09-07 | — | Xác nhận lại với PM trước khi lên kế hoạch execute | Pending | toàn module |

## Clarifications (home của CL quote — layout v2)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-NTF-01 | 🔴 Danh sách **9 loại thông báo chính thức** — 3 nguồn khác nhau (**home canonical ở đây**) | 🔴 **Open** | kế thừa 2026-07 (bảng unified lập 2026-07-27) | REQ-NTF-001..004, REQ-NTF-010 |
| C-NTF-03 | Đánh dấu đã đọc **(a)** + phân trang **(b)** (**home canonical ở đây**) | 🟡 **(a) Open · (b) N/A** | 2026-07-29 | REQ-NTF-007, REQ-NTF-008 |
| C-NTF-02 | Định nghĩa "khớp tuyến" & tham số vận hành (tham chiếu — home ở `ASN`) | 🟡 Partially Resolved | 2026-07-27 | REQ-NTF-002 |

### C-NTF-01 · 🔴 Danh sách loại thông báo chính thức (home canonical)

**Source Quote (ambiguous — 3 nguồn 3 danh sách):**
> Nguồn A — BRD tự khai (`DOC-v1.0-01` §D6 L315): "Danh sách sự kiện bắn thông báo dựa trên flow & màn hình hiện có của prototype. **Nháp — chờ BA review & bổ sung.** Kênh: in-app + push"
> Nguồn B — PRD (`DOC-v1.0-02` §3.2, trích): "Có người muốn mang giúp đơn của bạn | ... · **Bạn nhận được đánh giá 5 sao** | Kèm nhận xét từ đối tác đơn hàng · ... · **Cộng đồng FoxEco vừa đạt mốc X đơn** | Thông điệp 'tiết kiệm Y kg CO₂' — gamification"
> Nguồn C — Figma (`DOC-v1.0-06` KP-07): "Ảnh Figma thực tế cho ra danh sách **THỨ BA** — cũng khác cả BRD D6 lẫn demo Table 4."
> Nguồn D — BRD còn tự nêu thiếu (`§D6` L329): "Chờ BA bổ sung: ngưỡng thời gian nhắc, gộp/không gộp thông báo, thông báo cho người thứ 3 (VD người nhận khi carrier huỷ), cấu hình bật/tắt theo loại."

**Source Location:** `DOC-v1.0-01 §D6 · L315` và `L317-327` và `L329` ⟷ `DOC-v1.0-02 §3.2 · Table 4` ⟷ `DOC-v1.0-04` (qua `DOC-v1.0-06 KP-07` — bảng unified 12 hàng)

**Analyst Note:** ⭐ **CL lớn nhất của module, kế thừa nguyên trạng từ đợt cũ.** `KP-07` đã làm phần khó nhất: xếp **12 hàng sự kiện × 3 nguồn** để BA chọn 1 lần thay vì đọc rời rạc — **BA chưa trả lời**.
**Đã thu hẹp được nhờ 2 CL khác:** hàng **#6b** (*"nhận đánh giá 5 sao"*) loại theo `C-GIFT-01`; hàng **#11** (*"cộng đồng đạt mốc X đơn / CO₂"*) loại theo `C-USR-01`.
**Điểm cần BA chú ý nhất:** hàng **#10** (*"Sắp đến khung giờ hẹn giao"*) có bằng chứng ở **cả Demo và Figma** nhưng **không có trong BRD `§D6`** ⇒ khả năng cao **BRD sót một loại thông báo thật**.
`KP-07` khuyến nghị **hướng (c)** (hợp nhất ~10 loại) làm baseline cho generate-tc. **Non-blocking** nhưng giới hạn: ⛔ không assert danh mục, ⛔ không assert text `NTF-06`. Ngoài ra `§D6` L329 còn 4 tham số chưa có (ngưỡng nhắc · gộp thông báo · thông báo người thứ 3 · cấu hình bật/tắt) ⇒ 4 nhóm SC **không tồn tại ở lượt này**, sẽ mở khi BA bổ sung.

### C-NTF-03 · Đánh dấu đã đọc (a) + phân trang (b) — home canonical

**Source Quote (ambiguous):**
> Nhánh (a) — `DOC-v1.0-06` KP-01 §8 `KB-NTF-01`: "Ảnh Figma `3e626d398e3a616a45f5c638df62be830d2f4357`: 2 thông báo mới nhất có chấm đỏ riêng, 2 thông báo cũ hơn **cùng nhóm "Hôm nay"** thì không → gợi ý trạng thái đã-đọc/chưa-đọc theo item." · "🔴 **Không chứng minh được cơ chế tương tác**: bấm nút "Đánh dấu đã đọc" là mark-all hay mark-per-item? → chờ BA."
> Nhánh (b) — `KB-NTF-02`: "Không có đặc tả phân trang ở bất kỳ tài liệu nào. QA GiangDC2 xác nhận (2026-07-29): đây là **hành vi UI nền tảng bắt buộc** cho danh sách lớn, không cần BA xác nhận riêng như một business rule."

**Source Location:** `DOC-v1.0-06 KP-01 §8 "KB-NTF-01"` và `"KB-NTF-02"` · `KP-02 §4`

**Analyst Note:** **Hai nhánh xử lý khác nhau** — đây là lý do CL này được đếm ở nhóm *Partially Resolved*:
**(a) Open:** chấm đỏ có bằng chứng **gián tiếp** (ảnh cho thấy trạng thái theo item) nhưng **cơ chế tương tác chưa rõ**: tap 1 item chỉ đọc item đó, hay nút "Đánh dấu đã đọc" là mark-all? ⇒ `SC-NTF-010` assert **trạng thái hiển thị**, `SC-NTF-011` chỉ **ghi nhận** cơ chế.
**(b) N/A:** phân trang được QA quyết định là **yêu cầu UI nền tảng**, không phải business rule cần BA chốt ⇒ `SC-NTF-012` assert được hành vi load thêm, nhưng ⛔ không assert **kích thước trang**.
⚠️ CL này cũng là 1 trong 2 ca **từng bị revert `Resolved → Open`** ở đợt cũ (`KP-02 §6`) ⇒ ⛔ không đánh Resolved lại khi chưa có bằng chứng cơ chế.

### C-NTF-02 · Định nghĩa "khớp tuyến" & tham số vận hành *(tham chiếu)*

**Source Quote:**
> "🔴 Còn thiếu: "khung giờ phù hợp" là trùng hoàn toàn hay có độ lệch cho phép? Chu kỳ quét khớp? Ngưỡng gộp thông báo?"

**Source Location:** `DOC-v1.0-06 KP-01 §4 "KB-ASN-04"` (home canonical: `ASN-ghep-noi/risk_assessment.md`)

**Analyst Note:** Tuy mang nhãn `NTF` từ đợt cũ, nội dung CL là **rule engine ghép nối** ⇒ home canonical chuyển về `ASN` ở lượt này. Ảnh hưởng tới module này ở 1 điểm: **chu kỳ quét khớp chưa chốt** ⇒ `SC-NTF-002` ⛔ không assert **độ trễ** nhận thông báo khớp tuyến. Ngoài ra *"ngưỡng gộp thông báo"* trùng với 1 trong 4 tham số còn thiếu ở `§D6` L329.

## Khuyến nghị tổng thể
1. **Resolve trước generate-tc:** `C-NTF-01` — đây là CL **chặn nhiều nhất** ở module này: không chốt danh mục thì không assert được nội dung/danh sách thông báo. `KP-07` đã dọn sẵn bảng 12 hàng + 3 hướng chọn ⇒ BA chỉ cần chọn 1 lần.
2. **Ưu tiên test P1 high-risk:** `SC-NTF-008` (SĐT không có trong nội dung thông báo — kiểm **cả push**) — rủi ro dữ liệu cá nhân, và push là kênh dễ lọt nhất.
3. **Cần môi trường/dữ liệu:** chạy `NTF` **cuối lô** sau `ORD`/`ASN`/`DLV`/`GIFT`/`CNL` để tận dụng thông báo đã phát sinh; cần thêm **1 tin quá hạn** (nhờ dev) và **2 loại tài khoản** (có item đã đọc + chưa đọc cùng nhóm · chưa có thông báo nào).
4. **ID/text cleanup (non-blocking, cần trước automation):** chốt text `NTF-06` (*"cảm ơn bạn!"* vs *"đánh giá ngay"*) và bản text `NTF-08` (BRD template vs Figma cụ thể) — cả 2 sẽ là assert text trong TC.
