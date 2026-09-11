---
id: v1.0/DLV-giao-nhan/risk
title: Risk Assessment — v1.0 · Module DLV
type: risk-assessment
version: v1.0
sprint: 1
module: DLV
counts:
  cl: 3
  risk: 7
  cl_open: 1
  cl_resolved: 2
status: ANALYZED
updated: 2026-09-07
---

# Risk Assessment — v1.0 · Module DLV

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module DLV.
> 🔑 Frontmatter `counts:` = nguồn canonical CL/RISK — **chỉ đếm CL có home ở module này**; CL tham chiếu (home ở module khác) KHÔNG tính vào `counts`. **Layout v2 ⇒ đây là home của Clarification.**

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| DLV | **High** | Chứa **quyền hạn chốt đơn** (chỉ Receiver) mà BRD **tự mâu thuẫn** (`DLV-03` ghi RECEIVER/SENDER), **chi phí thiết lập tiền đề cao nhất dự án** (15 ô ma trận × trạng thái một chiều không lùi được), và 1 SC cần **chờ 4 giờ thực tế** |

## Chi tiết rủi ro (bảng hợp nhất)
| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-DLV-01 | DLV / Quyền chốt đơn | **BRD mâu thuẫn nội bộ:** `DLV-03` (§D3) ghi *"RECEIVER/SENDER xác nhận"* ⟷ `BR-INT-03`+`US-D21`+PRD §5.2+5 ảnh Figma chốt **Receiver-only**. Chọn nhánh sai ⇒ cho Sender tự chốt đơn của mình = mất hoàn toàn giá trị xác nhận 2 phía | **High** | `DLV-03` L255 vs `BR-INT-03` L79 · `US-D21` L197 · `KB-DLV-02` | `SC-DLV-022` + 3 ô ma trận `SC-DLV-010/011/012` | `C-DLV-01` Resolved theo Receiver-only (4 nguồn thắng 1); ghi ràng buộc `CHANGELOG §2` | Resolved | REQ-DLV-005, SC-DLV-022 |
| RISK-DLV-02 | DLV / Tiền đề ma trận | 15 ô cần **1 đơn qua đủ 5 trạng thái × 3 tài khoản**, mà trạng thái **một chiều không lùi được** (mọi transition qua popup, không undo) ⇒ bỏ sót 1 vai ở 1 trạng thái là phải tạo đơn mới từ đầu | **High** | `test_data_catalog.md` §Ghi chú chung · KP-01 §5.1 | Chạy theo lô: **mỗi trạng thái xem bằng cả 3 vai trước khi đẩy tiếp** | Lập checklist 15 ô theo thứ tự trạng thái; 3 phiên đăng nhập song song | Open | REQ-DLV-002, SC-DLV-001..015 |
| RISK-DLV-03 | DLV / Nguồn ma trận | Ma trận **không có trong BRD/PRD** — chỉ `QA-obs` + Figma. Nếu Figma đã lỗi thời so với app STG thì 15 SC assert nhãn text sẽ FAIL hàng loạt vì lý do không phải bug | Medium | `KP-01` §5.1 (nguồn `QA-obs` 2026-07-24 + Figma) | Vibe-test 1 lượt đối chiếu nhãn thật trước khi generate-tc | Vibe-test màn Theo dõi đơn ở đủ 5 trạng thái; lệch → `/analyze --update` | Open | REQ-DLV-002, SC-DLV-001..015 |
| RISK-DLV-04 | DLV / Mốc thời gian | `SC-DLV-024` cần **2 giờ + 4 giờ thực tế** ⇒ dễ bị bỏ qua hoặc "đánh PASS cho xong"; nhánh *"admin hỗ trợ"* lại thuộc Admin Portal (out of scope) nên chỉ verify được hệ quả phía user | Medium | `BR-CNF-04` L266 · `US-D14` L193 · `C-TS-01` (Admin out of scope) | Chạy có kế hoạch riêng hoặc nhờ dev seed timestamp | ⛔ Nếu chưa chạy đủ mốc thì GHI RÕ, không khai coverage | Open | REQ-DLV-007, SC-DLV-024 |
| RISK-DLV-05 | DLV / Nhánh phụ scope | **3 REQ không có SC** (`PUP-03` ảnh hàng · `GPS-01` vị trí · `COST-01` chi phí) vì PM chưa trả lời câu hỏi scope #2 và không có bề mặt UI nào trong ma trận/82 ảnh ⇒ nếu PM chốt "có trong scope" thì phải bổ sung SC gấp | Medium | `KP-05` §1 câu #2 (treo tới 2026-07-30) · `C-DLV-02`, `C-DLV-03` | — (gap có chủ đích, ghi `CHANGELOG §3`) | Hỏi PM chốt scope nhánh phụ; nếu vào scope → `/analyze --update` bổ sung SC | Pending | REQ-DLV-012, REQ-DLV-013, REQ-DLV-014 |
| RISK-DLV-06 | DLV / Timeline lịch sử | `C-CNL-02` ghi nhận **huỷ nhận đơn XOÁ dòng "Ghép thành công"** khỏi LỊCH SỬ ⇒ nếu `SC-DLV-029` chạy trên đơn từng bị huỷ nhận thì thiếu mốc và bị chẩn đoán sai thành bug của DLV | Medium | `KP-01` §7 KB-CNL-01 (live-verify 2026-07-29) | Given của `SC-DLV-029` = đơn đi **thẳng** tới Hoàn thành | Ghi ràng buộc `CHANGELOG §2`; bug xoá log thuộc `CNL` (`SC-CNL-009`) | Open | REQ-DLV-010, SC-DLV-029 |
| RISK-DLV-07 | DLV / Thuật ngữ | **Hai danh sách mốc khác nhau** (thanh trạng thái vs block Lịch sử) và **2 chữ cho 1 trạng thái `MATCHED`** ("Đã ghép" badge vs "Lấy hàng" mốc) ⇒ TC completeness dễ assert sai danh sách | Low | `KP-01` §5.1 (lưu ý thuật ngữ) · `DOC-v1.0-02` §3.6 | Assert đúng danh sách theo từng thành phần | Ghi ràng buộc `CHANGELOG §2`; nêu với BA để thống nhất nhãn trước automation | Resolved | REQ-DLV-001, REQ-DLV-010 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-DLV-01 | Ai được xác nhận "Đã nhận hàng"? | ✅ Resolved — **chỉ Receiver** (xác nhận qua 5 ảnh Figma) | 2026-07-24 | REQ-DLV-005 |
| C-DLV-02 | 🔴 Chia sẻ vị trí (`GPS-01`) mặc định bật hay tắt | 🔴 **Open** (non-blocking) | kế thừa 2026-07 | REQ-DLV-013 |
| C-DLV-03 | Màn xác nhận nhận hàng dùng bản nào? | ✅ Resolved — **modal đơn giản**; form đầy đủ không áp dụng v1.0 | 2026-07-27 | REQ-DLV-008 |
| C-CNL-01 | Màn "Báo sự cố" (Incident) | ✅ Resolved — **Out of scope v1.0** (tham chiếu — home ở `CNL`) | 2026-07-27 | REQ-DLV-015 |

### C-DLV-01 · Ai được xác nhận "Đã nhận hàng"?

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-01` §D3 `DLV-03` L255): "DLV-03 | **RECEIVER/SENDER** xác nhận đã nhận | Quá N giờ chưa xác nhận → nhắc → admin hỗ trợ"
> Nguồn B (`DOC-v1.0-01` §A5 `BR-INT-03` L79): "Hoàn thành cần **người nhận** xác nhận đã nhận hàng; nếu không xác nhận → nhắc + admin hỗ trợ"
> Nguồn C (`DOC-v1.0-01` §D1b `US-D21` L197): "**chỉ Receiver mới thấy & bấm được** "Xác nhận đã nhận hàng""
> Nguồn D (`DOC-v1.0-02` §5.2): "⇒ Đây là quyền hạn ĐẶC BIỆT DUY NHẤT của vai trò Người nhận: chỉ Người nhận mới có thể chốt đơn "Hoàn thành""

**Source Location:** `DOC-v1.0-01 §D3 · DLV-03 · L255` ⟷ `§A5 · BR-INT-03 · L79` ⟷ `§D1b · US-D21 · L197` ⟷ `DOC-v1.0-02 §5.2 · đoạn kết`

**Analyst Note:** Resolved 2026-07-24 theo **Receiver-only** — `KB-DLV-02` ghi *"Ảnh Figma xác nhận nhất quán qua 5 ảnh: nút chỉ active với Receiver; Sender/Carrier cùng bước "Đã giao" chỉ thấy nhãn disabled."* ⇒ **4 nguồn + 5 ảnh thắng 1 nguồn** (`DLV-03`). Đủ chuẩn `Resolved` theo `KP-02 §6` (có ảnh Figma cụ thể). ⚠️ Hệ quả nghiệp vụ nếu chọn sai: cho Sender tự chốt đơn của mình ⇒ mất hoàn toàn giá trị của xác nhận 2 phía, và `BR-CNF-04` (nhắc/admin) trở nên vô nghĩa.

### C-DLV-02 · 🔴 Chia sẻ vị trí mặc định bật hay tắt

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-01` §D3 `GPS-01` L251): "GPS-01 | Chia sẻ vị trí khi đang giao | Tùy chọn; chỉ active khi đang giao; xóa sau khi đóng"
> Nguồn B (`DOC-v1.0-01` §D5 L311 — chính BRD tự hỏi): "Chia sẻ vị trí mặc định bật/tắt?"
> Nguồn C (`DOC-v1.0-06` KP-01 §5 `KB-DLV-04`): "BRD tự nêu câu hỏi mở. BA/PO trả lời "phase sau" nhưng **chưa cho giá trị cụ thể**."

**Source Location:** `DOC-v1.0-01 §D3 · GPS-01 · L251` · `§D5 · L311` ⟷ `DOC-v1.0-06 KP-01 §5 "KB-DLV-04"`

**Analyst Note:** **Open, non-blocking.** BA nói *"phase sau"* nhưng không cho giá trị mặc định ⇒ không có oracle. Củng cố thêm: ma trận `KB-DLV-01` ở trạng thái **"Đang giao"** (ô #3) **không có** control chia sẻ vị trí ở bất kỳ vai nào, và 82 ảnh Figma không có màn nào cho tính năng này ⇒ khả năng cao **bề mặt không tồn tại ở v1.0**. ⇒ `REQ-DLV-013` để **gap SC có chủ đích** (`CHANGELOG §3`), ⛔ không viết SC khẳng định. Nếu PM chốt vào scope thì mở SC mới qua `/analyze --update`.

### C-DLV-03 · Màn xác nhận nhận hàng — modal đơn giản hay form đầy đủ?

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-02` §5.2): modal đơn giản — "Nút "Xác nhận đã nhận hàng" chỉ kích hoạt khi trạng thái = Đã giao"
> Nguồn B (`DOC-v1.0-02` §5.3): "phát hiện thêm một biến thể đầy đủ hơn… Thông tin Carrier | Tên + đơn vị/phòng ban + **điểm uy tín** (vd: Trần Thị Lan, Marketing, ★4.9)" · "**Ảnh bằng chứng** (khuyến nghị) | "Chụp ảnh hàng khi nhận — làm bằng chứng khi có tranh chấp""
> Nguồn C (`DOC-v1.0-02` §7 dòng 11): "Hai phiên bản màn hình "Xác nhận đã nhận hàng" | Modal đơn giản (Mục 5.2) và form đầy đủ có ảnh bằng chứng + điểm uy tín carrier (Mục 5.3) — cần chốt phiên bản chính thức."

**Source Location:** `DOC-v1.0-02 §5.2` ⟷ `§5.3` ⟷ `§7 · dòng 11` ⟷ phán quyết `DOC-v1.0-06 KP-01 §5 "KB-DLV-03"`

**Analyst Note:** Resolved 2026-07-27 theo **modal đơn giản** (BA chốt theo Figma; form đầy đủ **không áp dụng v1.0**). ⚠️ **Hệ quả lan sang 2 REQ khác:** form đầy đủ chứa **ảnh bằng chứng** (`PUP-03` — `REQ-DLV-012`) và **điểm uy tín ★4.9** (`C-USR-01` đã defer) ⇒ chốt modal đơn giản là chốt luôn rằng 2 thứ đó **không có bề mặt ở v1.0**. `SC-DLV-025` vì thế có vế phủ định (assert **không có** ảnh bằng chứng/điểm uy tín) — vế này quan trọng hơn vế khẳng định.

### C-CNL-01 · Màn "Báo sự cố" — out of scope v1.0 *(tham chiếu)*

**Source Quote:**
> "Màn "Báo sự cố" chưa có đặc tả — out of scope v1.0"

**Source Location:** `DOC-v1.0-06 KP-01 §5 "KB-DLV-05"` (home canonical: `CNL-huy-don/risk_assessment.md`)

**Analyst Note:** `BR-ASN-03` (§D4 L264) yêu cầu *"Sau khi nhận hàng (IN_TRANSIT) không hủy thường → phải tạo sự cố"* nhưng màn "Báo sự cố" **chưa có đặc tả** và out of scope v1.0 ⇒ chỉ assert được **vế chặn huỷ** (SC ở `CNL` — `SC-CNL-005`), ⛔ không assert luồng tạo sự cố. Ghi ở đây để traceability của `REQ-DLV-015` không đứt.

## Khuyến nghị tổng thể
1. **Resolve trước generate-tc:** không có blocker cứng (`C-DLV-01`/`C-DLV-03` đã Resolved). Cần **PM chốt scope nhánh phụ** (`KP-05 §1` câu #2) để biết `PUP-03`/`GPS-01`/`COST-01` có phải bổ sung SC hay không.
2. **Ưu tiên test P1 high-risk:** `SC-DLV-012` (Receiver là nút enable duy nhất) · `SC-DLV-022` (chỉ Receiver chốt đơn) · `SC-DLV-021` (không nhảy bước lấy hàng) · `SC-DLV-023` (Hoàn thành ngay — chặn `GIFT` nếu FAIL).
3. **Cần môi trường/dữ liệu:** **3 tài khoản 3 vai dùng chung 1 đơn** + **3 phiên đăng nhập song song**; đẩy đơn qua đủ 5 trạng thái theo **thứ tự một chiều** — checklist 15 ô phải hoàn tất **từng trạng thái trước khi đẩy tiếp**. `SC-DLV-024` cần **2h + 4h** hoặc dev seed timestamp.
4. **Vibe-test trước generate-tc:** đối chiếu **nhãn text thật** của 15 ô với ma trận `KB-DLV-01` — nguồn ma trận là `QA-obs` + Figma từ 2026-07, nếu app đã đổi nhãn thì 15 SC FAIL hàng loạt vì lý do không phải bug (`RISK-DLV-03`).
5. **ID/text cleanup (non-blocking, cần trước automation):** thống nhất **2 danh sách mốc** (thanh trạng thái vs Lịch sử) và **2 chữ cho `MATCHED`** ("Đã ghép" vs "Lấy hàng") — đây sẽ là locator text của automation.
