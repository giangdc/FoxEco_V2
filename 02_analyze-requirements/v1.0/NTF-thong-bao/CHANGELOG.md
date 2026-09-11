---
id: v1.0/NTF-thong-bao/changelog
title: Changelog — Module NTF
type: changelog
version: v1.0
sprint: 1
module:
  code: NTF
  dir: NTF-thong-bao
  name: Thông báo
doc_source:
  - id: DOC-v1.0-01
    section: "§D6 (L315-329, NTF-01..09) · §D7 (OPR-07) · §D1b (US-D12)"
  - id: DOC-v1.0-02
    section: "§2 (dòng Header) · §3.2 (Table 4)"
  - id: DOC-v1.0-04
    section: "ảnh màn Thông báo (3e626d39…)"
  - id: DOC-v1.0-06
    section: "KP-01 §8 (KB-NTF-01..03) · KP-02 §4/§5/§6 · KP-05 §3 (#6) · KP-07 (bảng unified 12 hàng)"
id_range:
  req: REQ-NTF-001..011
  sc: "SC-NTF-001..016 (NEW) — ⚠ ID SC-NTF-006 của lượt này KHÔNG liên quan SC-NTF-006 của đợt v1.0 cũ (đã DEPRECATED)"
  cl: "C-NTF-01 · C-NTF-03 (cả 2 home canonical ở đây) · C-NTF-02 (tham chiếu — home ở ASN)"
  risk: RISK-NTF-01..06
status: ANALYZED
updated: 2026-09-07
---

# Changelog — Module NTF (`NTF`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-07 | INIT | Phân tích lần đầu §D6 — 11 REQ (`001..011`), 16 SC, 3 CL, 6 RISK. Điểm nghiệp vụ đáng chú ý nhất: **BRD tự khai `§D6` là "Nháp — chờ BA review & bổ sung"** và 3 nguồn cho 3 danh sách thông báo khác nhau ⇒ `C-NTF-01` vẫn là CL lớn nhất | `DOC-v1.0-01` §D6/§D7/§D1b · `DOC-v1.0-02` §2/§3.2 · `DOC-v1.0-04` · `DOC-v1.0-06` KP-01 §8 + KP-07 | Dựng đủ 5 deliverable + `CHANGELOG.md` |
| 2026-09-07 | INIT | **Nhận home canonical của `C-NTF-01`** (danh sách loại thông báo) và **`C-NTF-03`** (đánh dấu đã đọc + phân trang) | 2 CL thuộc bề mặt màn Thông báo | `KP-07` (12 hàng unified) là dữ liệu chính của `C-NTF-01` |
| 2026-09-07 | REFACTOR | **Chuyển `C-NTF-02` (định nghĩa "khớp tuyến") về home canonical ở `ASN`** — CL mang nhãn `NTF` từ đợt cũ nhưng nội dung là rule engine ghép nối | Sửa chỗ đặt CL cho đúng bản chất | Module này chỉ **tham chiếu**; ảnh hưởng: `SC-NTF-002` ⛔ không assert độ trễ |
| 2026-09-07 | SCOPE↓ | `NTF-07` (thông báo nhận quà) **KHÔNG tạo SC ở module này** — đã có `SC-GIFT-012` | Trần Scenario Sufficiency Rule: duplicate ⇒ không tạo SC rác | Traceability ghi rõ ở dòng cuối `requirement_traceability.md §1` |
| 2026-09-07 | INIT | Ghi nhận: `§D6` L329 còn **4 tham số chưa có** (ngưỡng thời gian nhắc · gộp/không gộp thông báo · thông báo cho người thứ 3 · cấu hình bật/tắt theo loại) ⇒ **4 nhóm SC không tồn tại ở lượt này** | BRD tự nêu thiếu | Sẽ mở SC mới khi BA bổ sung (`/analyze --update`) |
| 2026-09-07 | REFACTOR | Đổi tên thư mục module `NTF/` → `NTF-thong-bao/` — tên gợi nghĩa để người mới đọc thư mục là biết chức năng. Cập nhật kèm: frontmatter `id:` của 5 deliverable + `module.dir` ở file này + mọi cross-ref `NTF/<file>.md` | Yêu cầu QC GiangDC2 2026-09-07 (mã 2–4 chữ không nói lên chức năng) · `Project_rule §Module Codes` nay có cột `Dir` riêng | ⛔ **Mã module `NTF` và toàn bộ ID (`REQ-NTF-*` · `SC-NTF-*`) KHÔNG đổi** — chỉ đường dẫn thư mục đổi. TC chưa sinh nên không TC nào bị ảnh hưởng |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **`SC-NTF-006` của lượt này KHÔNG liên quan `SC-NTF-006` của đợt v1.0 cũ** (đã DEPRECATED — trần thông báo/ngày) | Dải ID được đánh lại từ 001 ở lượt phân tích mới; ID trùng số nhưng nội dung khác hoàn toàn | Trace sai giữa 2 nội dung khác nhau cùng ID; quy chiếu **bắt buộc bằng `id_range` + đường dẫn sprint** |
| 2 | ⛔ **KHÔNG tái tạo scenario "trần thông báo khớp / NGÀY"** (`OPR-06`) | BA đã đảo kết luận 2026-07-29: trần tính **riêng theo từng tin OFFER** (`KB-ASN-03`); rule hiện hành ở `ASN` (`SC-ASN-014`) | Làm sống lại một kết luận đã bị BA bác, và tạo SC trùng chức năng với `ASN` |
| 3 | ⛔ **KHÔNG assert danh mục / danh sách loại thông báo** | `C-NTF-01` Open — 3 nguồn 3 danh sách, BRD `§D6` tự khai là "Nháp" | TC chọn 1 danh sách ⇒ FAIL vì lý do chưa chốt; và có thể bỏ sót loại thông báo thật (vd #10 *"Sắp đến khung giờ hẹn giao"*) |
| 4 | ⛔ **KHÔNG assert text `NTF-06`** (*"cảm ơn bạn!"* vs *"đánh giá ngay"*) | 2 nguồn 2 text; bản PRD+Figma dùng từ "đánh giá" trong khi rating đã defer (`C-GIFT-01`) | Assert sai text ⇒ FAIL; hoặc tệ hơn: hợp thức hoá từ "đánh giá" cho tính năng không có ở v1.0 |
| 5 | ⚠️ **`SC-NTF-008` phải kiểm CẢ 2 KÊNH** in-app **và** push | Nội dung push do backend đẩy, **không đi qua UI** ⇒ kênh dễ lọt SĐT nhất (`OPR-07` cấm) | Chỉ kiểm in-app ⇒ bỏ sót đúng kênh có rủi ro cao nhất về dữ liệu cá nhân |
| 6 | ⚠️ **Phân biệt "nhắc SĐT" ⟷ "chứa số SĐT"** — `NTF-01` được phép nói *"SĐT đã được lộ để liên hệ"* | `OPR-07` chỉ cấm **đưa SĐT vào nội dung**, không cấm nhắc tới việc đã lộ | Log bug oan cho `NTF-01` (text đúng spec), làm loãng bug thật nếu có |
| 7 | ⛔ **KHÔNG assert cơ chế nút "Đánh dấu đã đọc"** (mark-all vs mark-per-item) | `C-NTF-03(a)` Open — bằng chứng chấm đỏ chỉ **gián tiếp** (suy từ 1 ảnh Figma) | Vi phạm `§Custom Rules §10.1`; và CL này từng bị revert `Resolved → Open` vì chốt không kèm bằng chứng |
| 8 | ⛔ **KHÔNG assert số item/trang khi lazy-load** và **nhóm cho thông báo cũ hơn 1 tuần** | Không nguồn nào nêu; `C-NTF-03(b)` chỉ xác nhận **có** hành vi load thêm | TC assert con số bịa ⇒ FAIL không có cơ sở phán quyết |
| 9 | ⚠️ **`SC-NTF-002` ⛔ không assert độ trễ** nhận thông báo khớp tuyến | **Chu kỳ quét khớp chưa chốt** (`C-NTF-02` Partially Resolved, home ở `ASN`) | TC timeout vì chờ theo kỳ vọng tự đặt ⇒ FAIL/BLOCKED không đúng bản chất |

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 `C-NTF-01` — danh sách loại thông báo chính thức (3 nguồn, 12 hàng ứng viên) | Kế thừa từ 2026-07; `KP-07` đã dọn sẵn bảng + 3 hướng chọn nhưng **BA chưa trả lời** | Hỏi BA chọn 1 trong 3 hướng của `KP-07`; nêu riêng hàng **#10** (*"Sắp đến khung giờ hẹn giao"*) — có ở Demo+Figma nhưng BRD sót |
| 2 | 🔴 **4 tham số `§D6` L329 chưa có** (ngưỡng nhắc · gộp thông báo · thông báo người thứ 3 · cấu hình bật/tắt theo loại) ⇒ 4 nhóm SC chưa tồn tại | BRD tự nêu thiếu; chưa hỏi BA | Hỏi BA cùng lượt `C-NTF-01`; có câu trả lời → `/analyze --update` mở SC mới |
| 3 | 🟡 `C-NTF-03(a)` — cơ chế "Đánh dấu đã đọc" (mark-all vs mark-per-item) | Open từ 2026-07-29; bằng chứng chỉ gián tiếp | Vibe-test thử **cả 2 cách** (tap item / bấm nút) rồi `/analyze --update`; ⛔ không đánh Resolved khi chưa có bằng chứng cơ chế |
| 4 | 🟡 Text `NTF-06` và bản text `NTF-08` chưa chốt | `RISK-NTF-04` Open | Đưa vào cùng lượt trả lời `C-NTF-01` |
| 5 | 🟡 Tiền đề: cần **trọn 1 vòng đời đơn** + 1 lượt huỷ + **1 tin quá hạn** (⛔ không seed qua UI) | `RISK-NTF-05` Open | Chạy `NTF` **cuối lô**; nhờ dev seed tin quá hạn cùng lô với `SC-ORD-045` |
| 6 | 🟡 Xác nhận lại **scope module với PM** — PM xếp `NTF` out of scope Phase 1 nhưng đã phân tích đầy đủ 16 SC | `RISK-NTF-06` Pending | Hỏi PM trước khi lên kế hoạch execute |
