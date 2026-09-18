---
id: v1.1/NTF-thong-bao/risk
title: Risk Assessment — v1.1 · Module NTF (Delta)
type: risk-assessment
version: v1.1
sprint: 1
module: NTF
counts:
  cl: 4
  risk: 7
  cl_open: 0
  cl_resolved: 4
status: ANALYZED
updated: 2026-09-17
---

# Risk Assessment — v1.1 · Module NTF (Delta)

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk **mới** của module NTF ở v1.1.
> 🔑 `counts:` chỉ đếm CL/RISK **mới mở** ở lượt này. Risk/CL CARRIED (không đổi) xem `v1.0/NTF-thong-bao/risk_assessment.md`; risk/CL **đổi Status** liệt kê lại đầy đủ ở đây (không phải mới, nhưng cần cập nhật authoritative).

## Tổng quan
| Module | Risk Level | Rủi ro chính (delta v1.1) |
|--------|-----------|--------------|
| NTF | **Low** (giảm từ Medium) | Nguy cơ lớn nhất của v1.0 (danh mục thông báo chưa chốt) đã Resolved. Rủi ro còn lại: 6 sự kiện mới cần tiền đề nghiệp vụ từ `DLV` mới quan sát được |

## Cập nhật Status risk/CL đã có (không phải RISK/CL mới — ghi lại đầy đủ vì đổi Status)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-NTF-01 | NTF / Danh mục thông báo | (mô tả gốc xem v1.0) — 3 nguồn 3 danh sách, BRD tự khai "Nháp" | High | `DOC-v1.1-01 §8.13.1` | `SC-NTF-014` giờ **assert** đủ 15 loại | **Đã resolve**: PRD v1.1 FR13 §8.13.1 chốt 15 sự kiện chính thức, ngày 2026-09-15 | **Resolved** | REQ-NTF-010, SC-NTF-014 |
| RISK-NTF-04 | NTF / Text `NTF-06` | (mô tả gốc xem v1.0) — 2 nguồn 2 text | Medium | `DOC-v1.1-01 §8.13.1` dòng `NTF-06` | `SC-NTF-005` giờ **assert** đúng text | PRD v1.1 dùng đúng bản BRD cũ ("cảm ơn bạn!"), loại bỏ nghi vấn "đánh giá ngay" | **Resolved** | REQ-NTF-003, SC-NTF-005 |
| RISK-NTF-02 | NTF / Bảo mật push | (mô tả gốc xem v1.0) — push dễ lọt SĐT nhất | High | `DOC-v1.1-01 §8.13.1` (đối chiếu đủ 15 dòng, không dòng nào có SĐT) | `SC-NTF-008` mở rộng phạm vi sang **15 sự kiện** | Chạy sớm, phủ đủ 15 sự kiện kể cả 6 sự kiện mới; FAIL → log bug P1 | Open (mở rộng phạm vi, chưa test) | REQ-NTF-005, SC-NTF-008 |

## RISK mới (delta v1.1)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-NTF-07 | NTF / Tiền đề 6 sự kiện mới | 6 sự kiện `NTF-10..15` chỉ phát sinh khi đơn đi qua nhánh phụ FR08/FR09 của `DLV` (không liên lạc được người nhận → gửi quầy/uỷ quyền → cầm hàng về → hẹn giao lại/hoàn hàng) — tiền đề dựng tốn công hơn nhánh chính, dễ bị bỏ qua khi lên lịch test | Medium | `DOC-v1.1-01 §8.13.1` + phụ thuộc `DLV-giao-nhan/test_scenario_map.md` (delta v1.1) | `SC-NTF-017..022` | Chạy `NTF` **cùng lô** với vibe-test nhánh FR08/FR09 của `DLV`, không seed riêng cho NTF | Open | REQ-NTF-012, SC-NTF-017..022 |

## Cập nhật Clarifications đã đổi Status (home canonical vẫn ở đây)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-NTF-01 | 🔴 Danh sách loại thông báo chính thức (3 nguồn, nay đã hợp nhất) | ✅ **Resolved 2026-09-15** — chính thức **15 sự kiện** theo `DOC-v1.1-01 §8.13.1` | 2026-09-15 (mở từ 2026-07) | REQ-NTF-001..004, REQ-NTF-010, REQ-NTF-012 |
| C-NTF-03 | Đánh dấu đã đọc **(a)** — mark-all hay từng item (bản gốc `v1.0/NTF-thong-bao/`) | ✅ **Resolved 2026-09-16 — BA: bấm "Đánh dấu đã đọc" = đánh dấu TẤT CẢ đã đọc** | 2026-07-29 | REQ-NTF-007, REQ-NTF-008, SC-NTF-011, SC-NTF-013 |
| C-NTF-04 | Chạm từng loại thông báo (`NTF-01..15`) mở màn nào; chạm 1 thông báo có đánh dấu đã đọc riêng thông báo đó không | ✅ **Resolved 2026-09-17** — BA: v1.1 mọi loại → "Theo dõi đơn"; tự đánh dấu đã đọc riêng | 2026-09-16 | REQ-NTF-007, REQ-NTF-010, SC-NTF-010, SC-NTF-014 |
| C-NTF-05 | Người nhận thông báo ở các sự kiện PRD viết mơ hồ: Carrier huỷ nhận · giao uỷ quyền/quầy có gửi kèm `NTF-05` · `NTF-08` "các bên còn lại" khi đơn còn POSTED | ✅ **Resolved 2026-09-17** — BA trả lời đủ (a)(b)(c) | 2026-09-16 | REQ-NTF-003, REQ-NTF-012, SC-NTF-006, SC-NTF-017, SC-NTF-018 |

### C-NTF-01 · 🔴 Danh sách loại thông báo chính thức — RESOLVED 2026-09-15

**Source Quote (resolve):**
> "§8.13.1 Danh mục thông báo" — bảng 15 dòng `NTF-01`..`NTF-15` (ID | Sự kiện kích hoạt | Người nhận | Nội dung mẫu), `DOC-v1.1-01` page 48.

**Source Location:** `DOC-v1.1-01 §8.13.1 · page 48`

**Analyst Note:** Resolved theo PRD chính thức (đã qua Approval §12), thay thế hoàn toàn 3 nguồn mâu thuẫn cũ (BRD tự nhận "Nháp", PRD-demo, Figma). 9 sự kiện cũ (`NTF-01..09`) giữ nguyên nội dung/người nhận đúng bản BRD; 6 sự kiện mới (`NTF-10..15`) bổ sung cho nhánh xử lý giao hàng không thành công. Hàng "Sắp đến khung giờ hẹn giao" mà `KP-07` (v1.0) nghi ngờ BRD bỏ sót — **không** có trong danh mục chính thức v1.1 ⇒ xác nhận không phải sự kiện chính thức, đóng nghi vấn cũ.

⚠️ **Kết luận bị đảo:** kết luận cũ *"⛔ KHÔNG assert danh mục / danh sách loại thông báo"* (`v1.0/NTF-thong-bao/CHANGELOG.md §2` ràng buộc #3) và *"⛔ KHÔNG assert text NTF-06"* (ràng buộc #4) **HẾT HIỆU LỰC kể từ v1.1** — đừng trích lại 2 ràng buộc đó cho v1.1; hiện hành là **assert đủ 15 loại + đúng text NTF-06** theo `DOC-v1.1-01 §8.13.1`.

### C-NTF-03 · ↳ BA trả lời 2026-09-16 *(→ RESOLVED vế a)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `NTF` · cột "Câu trả lời BA" · 2026-09-16

> "Click vao đánh dấu tất cả là đã đọc nhé"

↳ **Ghi chú:** Nút "Đánh dấu đã đọc" là **mark-all** — một lần bấm đưa **mọi** thông báo về trạng thái đã đọc. ⇒ `SC-NTF-011` hết `[GAP]`: Then assert sau khi bấm, **không còn** chấm đỏ ở bất kỳ item nào; `SC-NTF-013`: badge chuông về **0 / ẩn**. Vế (b) phân trang vẫn N/A như v1.0. BA **không nói** chạm vào **một** thông báo có đánh dấu riêng item đó không → gộp vào `C-NTF-04`.

### C-NTF-04 · Đích điều hướng khi chạm thông báo + đọc từng item *(RESOLVED 2026-09-17)*

📍 `DOC-v1.1-01 §8.13 Post-Conditions · trang 47` · `§8.13.1 NTF-07 · trang 47` · `§11 DoD #7 · trang 56`

> `§8.13` Post-Conditions: "Thông báo hiển thị ở màn Thông báo; chạm vào mở đúng đơn/màn liên quan"

> `NTF-07`: "Bạn nhận được một món quà cảm ơn — mở Trang cá nhân để xem"

> DoD #7: "15 mẫu thông báo được kiểm thử trên thiết bị thật (iOS + Android), nội dung đúng mẫu và mở đúng màn đích."

↳ **Ghi chú:** DoD bắt test *"mở đúng màn đích"* cho cả 15 loại, nhưng PRD chỉ nêu đích của **1** loại (`NTF-07` → Trang cá nhân). **Hỏi:** (a) bảng đích cho từng `NTF-01..15` — vd `NTF-03` → màn chi tiết đơn có nút "Nhận giao" (`AC-22.1.01`); `NTF-06` → Theo dõi đơn hay thẳng màn Tặng quà (cho Sender)?; `NTF-09` → đơn hết hạn hay wizard đăng lại? (b) chạm **1** thông báo có tự đánh dấu **riêng nó** đã đọc không (ảnh demo `NTF_03_thongbao_sau_tap_item_CNTF03.png`)? (c) Chạm thông báo của **đơn đã đóng/đã bị người khác nhận** thì mở màn gì?

↳ **KẾT LUẬN (theo BA) 2026-09-17:** (a) ở **v1.1** (bản này), **TẤT CẢ 15 loại thông báo** chạm vào đều mở màn **"Theo dõi đơn"** — BA đơn giản hoá, chưa phân loại đích riêng theo từng `NTF-01..15` như DoD #7 kỳ vọng (không có bảng đích chi tiết như câu hỏi gợi ý, vd `NTF-06`/`NTF-09`). (b) chạm 1 thông báo **CÓ** tự đánh dấu **riêng** thông báo đó đã đọc (ngoài cơ chế "đánh dấu tất cả" đã chốt ở `C-NTF-03`). (c) chạm thông báo của đơn đã đóng/đã bị người khác nhận ⇒ hiển thị thông báo **"đơn không tồn tại"** (không mở "Theo dõi đơn" của đơn đó). `C-NTF-04` ĐÓNG HẲN — `SC-NTF-010/014` + DoD #7 có oracle: màn đích thống nhất = "Theo dõi đơn" cho mọi loại (trừ đơn không tồn tại).

### C-NTF-05 · Người nhận thông báo ở các sự kiện mơ hồ *(RESOLVED 2026-09-17)*

📍 `DOC-v1.1-01 §6.2 AC-25.1.02 · trang 26` · `§8.13.1 NTF-05 / NTF-08 / NTF-10 / NTF-11 · trang 47` · `§8.7.2 bước 6 · trang 40`

> `AC-25.1.02`: "Đơn quay về POSTED và hiển thị lại trên bảng tin để người khác nhận. Người gửi nhận thông báo."

> `NTF-08`: "Đơn bị huỷ (kèm lý do) | Các bên còn lại | "Đơn đã bị huỷ bởi {vai trò} — lý do: {…}""

> `NTF-10`: "Giao cho người được uỷ quyền | Người nhận · Người gửi | "Hàng đã được giao cho {tên người nhận thay} (uỷ quyền bởi {người gửi/người nhận}) — có ảnh bằng chứng""

↳ **Ghi chú:** (a) **Carrier huỷ nhận** (đơn về POSTED, *không* bị huỷ): *"người gửi nhận thông báo"* — là `NTF-08` (câu *"Đơn đã bị huỷ bởi…"* sai nghĩa) hay thông báo riêng chưa có trong danh mục? **Người nhận** có được báo không? (b) Giao cho **người uỷ quyền / quầy**: người nhận chỉ nhận `NTF-10`/`NTF-11` (không có lời nhắc *"vui lòng xác nhận"*), hay nhận **thêm `NTF-05`**? Người nhận vẫn là người duy nhất bấm được "Xác nhận đã nhận hàng" nên thiếu lời nhắc là rủi ro kẹt đơn. (c) `NTF-08` khi Sender huỷ đơn còn **POSTED** (chưa có Carrier): "các bên còn lại" = chỉ người nhận?

↳ **KẾT LUẬN (theo BA) 2026-09-16:** (a) Carrier **HUỶ NHẬN**: người gửi nhận `NTF-08`; người nhận **CŨNG** được báo (không chỉ người gửi). (b) giao cho người uỷ quyền/quầy: người nhận **CÓ** nhận THÊM `NTF-05` "vui lòng xác nhận đã nhận hàng" (không chỉ `NTF-10`/`NTF-11`) — giảm rủi ro kẹt đơn vì thiếu lời nhắc. (c) người gửi huỷ đơn khi còn "Chờ ghép"/POSTED: "các bên còn lại" của `NTF-08` = **CHỈ người nhận** (đúng như giả định). `C-NTF-05` ĐÓNG HẲN — `SC-NTF-006`, `SC-NTF-017/018` xác định rõ người nhận thông báo cho cả 3 tình huống.

## Vibe-check bổ sung 2026-09-15 (không resolve CL nào — ghi nhận để không lặp lại hướng đã thử)

**`C-NTF-03(a)` — cơ chế "Đánh dấu đã đọc" (home canonical `v1.0/NTF-thong-bao/risk_assessment.md`):** đã thử trực tiếp trên demo `foxeco_demo/FoxEcoQC`, đúng khuyến nghị cũ *"vibe-test thử cả 2 cách (tap item / bấm nút)"*:
> Ảnh `00_input/v1.1/design/NTF_02_thongbao_sau_danhdaudadoc_CNTF03.png` — sau khi bấm nút "Đánh dấu đã đọc" (mark-all), 3 chấm đỏ unread **VẪN CÒN NGUYÊN**, không đổi.
> Ảnh `00_input/v1.1/design/NTF_03_thongbao_sau_tap_item_CNTF03.png` — sau khi tap vào 1 item ("Tìm thấy đơn hàng phù hợp tuyến của bạn") và quay lại, chấm đỏ của item đó **VẪN CÒN**, không đổi.

↳ **Kết luận: KHÔNG resolve được `C-NTF-03(a)` qua demo này** — cả 2 cách thử đều không có hiệu ứng, tức cơ chế đọc trong demo là **dữ liệu tĩnh/mock, không nối logic thật**. Đây là giới hạn của công cụ tham chiếu (demo), không phải câu trả lời cho câu hỏi nghiệp vụ. **KHÔNG dùng 2 ảnh trên làm bằng chứng "app không có tính năng đánh dấu đã đọc"** — chỉ ghi nhận để tránh người sau lặp lại đúng 2 phép thử này trên cùng demo rồi tưởng đã có kết luận. Câu hỏi `C-NTF-03(a)` **vẫn Open**, cần hỏi BA hoặc verify trên STG thật.

↳ **Tái xác nhận độc lập 2026-09-16 (không lặp lại đúng 2 phép thử cũ):** Thử thêm 1 cách khác — tap trực tiếp vào 1 item thông báo cụ thể (không phải nút "Đánh dấu đã đọc"). Lần này item **CÓ điều hướng thật** (mở đúng "Chi tiết tin" tương ứng với nội dung thông báo, dùng dữ liệu đơn thật vừa tạo trong phiên) — khác hẳn 2 phép thử cũ (đều không có hiệu ứng gì trên item mẫu tĩnh). Nhưng quay lại danh sách Thông báo, chấm đỏ của item đó **vẫn còn nguyên**, không đổi. Bấm "Đánh dấu đã đọc" (mark-all) cũng **không đổi** bất kỳ chấm đỏ nào. ⇒ Củng cố thêm: điều hướng trong danh sách thông báo có hoạt động (route thật), nhưng **trạng thái đã đọc hoàn toàn không được cài đặt/lưu** trong bản demo này — dù dùng route thật hay item mẫu. Không đủ để kết luận cơ chế nghiệp vụ, `C-NTF-03(a)` **giữ nguyên Open**.

## Khuyến nghị tổng thể (delta v1.1)
1. **Không còn blocker** — `C-NTF-01` đã Resolved, không cần hỏi BA trước khi generate-tc phần NTF.
2. **Ưu tiên test P1:** `SC-NTF-008` mở rộng — phải test đủ 15/15 sự kiện, không chỉ 9 sự kiện cũ.
3. **Cần môi trường/tiền đề:** 6 SC mới (`SC-NTF-017..022`) phụ thuộc trực tiếp tiến độ vibe-test nhánh FR08/FR09 bên `DLV` — lên lịch chạy chung, không tách riêng.
4. ✅ **`C-NTF-03` Resolved 2026-09-16 (BA)** — "Đánh dấu đã đọc" = **đánh dấu tất cả** (mark-all). `RISK-NTF-03`, `RISK-NTF-05`, `RISK-NTF-06` — PRD v1.1 không đề cập, giữ nguyên Open/Pending như v1.0. Việc mới: `C-NTF-04` (màn đích khi chạm thông báo) · `C-NTF-05` (người nhận ở sự kiện mơ hồ).
