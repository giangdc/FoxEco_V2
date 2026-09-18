---
id: v1.0/DLV-giao-nhan/changelog
title: Changelog — Module DLV
type: changelog
version: v1.0
sprint: 1
module:
  code: DLV
  dir: DLV-giao-nhan
  name: Giao nhận & Theo dõi đơn
doc_source:
  - id: DOC-v1.0-01
    section: "§A2 (NT-03) · §A5 (BR-INT-03) · §D2 (L213, L215, L232) · §D3 (DLV-03, PUP-03, GPS-01, COST-01, ORD-04) · §D4 (BR-CNF-01/04, BR-COST-01, BR-ASN-03) · §D5 (L294, L295, L311) · §D1b (US-D05/D08/D09/D14/D21)"
  - id: DOC-v1.0-02
    section: "§3.6 · §4.3 · §5.2 · §5.3 · §6 (L191) · §7 (dòng 11)"
  - id: DOC-v1.0-04
    section: "15 ô ma trận (dc8cf987… · 2e2ff7bc… · 974b5c52… · c8cae4c3… · e1699c4f… · ca5e7239… · 8563adc1… · 91b08fb1… · 7d8b4a8c… · 5dc3ce81… · 82d9aace… · 19490aa9… · 2658b17b… · 76e115a2…)"
  - id: DOC-v1.0-06
    section: "KP-01 §5.1 (KB-DLV-01) · §5 (KB-DLV-02..05) · §7 (KB-CNL-01) · KP-02 §2/§3/§4/§5 · KP-05 §1"
id_range:
  req: REQ-DLV-001..016
  sc: "SC-DLV-001..030 (NEW)"
  cl: "C-DLV-01 · C-DLV-02 · C-DLV-03 · C-CNL-01 (tham chiếu — home ở CNL)"
  risk: RISK-DLV-01..07
status: ANALYZED
updated: 2026-09-07
---

# Changelog — Module DLV (`DLV`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-17 | UPDATE | **Áp câu trả lời BA `C-DLV-07` (home ở `v1.1/DLV-giao-nhan/`) — thu hẹp phạm vi `SC-DLV-024`.** BA: hệ thống **CHỈ gửi remind**, *"phase này các chỗ liên quan đến role admin chưa làm"* ⇒ vế *"sau 4 giờ chuyển admin hỗ trợ"* **OUT OF SCOPE v1.1**, không assert, không log bug khi không thấy; phần còn lại assert: **có thông báo nhắc** sau 2h + **đơn KHÔNG tự chuyển "Hoàn thành"**. Bỏ nhãn `[GAP]` ở tiêu đề `SC-DLV-024` | BA trả lời 2026-09-17 (QC GiangDC2 chuyển lời) · `CL-hoi-BA-v1.1.xlsx` sheet `DLV` | `counts` không đổi (CL home ở `v1.1`); `RISK-DLV-04` Status ghi rõ đã thu hẹp phạm vi |
| 2026-09-07 | INIT | Phân tích lần đầu §D3/§D4/§3.6/§4.3/§5.2 — 16 REQ (`001..016`), 30 SC, 4 CL, 7 RISK. Điểm nghiệp vụ đáng chú ý nhất: **ma trận nhãn nút 5 trạng thái × 3 vai (15 ô)** — mục giá trị nhất của knowledge pack, hoàn toàn không có trong BRD/PRD; và **BRD tự mâu thuẫn về quyền chốt đơn** (`DLV-03` ghi RECEIVER/SENDER ⟷ 4 nguồn khác chốt Receiver-only) | `DOC-v1.0-01` §A5/§D3/§D4/§D1b · `DOC-v1.0-02` §3.6/§4.3/§5.2/§5.3 · `DOC-v1.0-04` (15 ô) · `DOC-v1.0-06` KP-01 §5.1 | Dựng đủ 5 deliverable + `CHANGELOG.md` |
| 2026-09-07 | INIT | **Fan-out ma trận thành 15 SC (1 ô = 1 SC).** Đợt v1.0 cũ chỉ có **14 SC cho toàn module `DLV`** trong khi ma trận đã 15 ô ⇒ module thiếu SC rõ rệt nhất | Scenario Sufficiency Rule (mỗi role × mỗi state = 1 SC) | `SC-DLV-001..015`; FAIL chỉ ra ngay ô nào (trạng thái × vai) sai nhãn |
| 2026-09-07 | SCOPE↓ | **4 REQ để gap SC có chủ đích:** `REQ-DLV-011` (bản đồ — trùng `SC-FEED-009`) · `REQ-DLV-012` (`PUP-03` ảnh hàng) · `REQ-DLV-013` (`GPS-01` vị trí) · `REQ-DLV-014` (`COST-01` chi phí) | Duplicate (011) và nhánh phụ PM chưa chốt scope + không có bề mặt UI trong ma trận/82 ảnh (012/013/014) | Ghi ở §3 Nợ đang mở; ⛔ không tạo SC rác. Nếu PM chốt vào scope → `/analyze --update` |
| 2026-09-07 | INIT | Ghi nhận `REQ-DLV-015` (`BR-ASN-03` — không huỷ thường sau IN_TRANSIT) **có SC ở `CNL`** (`SC-CNL-005`), không tạo SC trùng ở đây | Hành động là **huỷ** ⇒ thuộc `CNL`; màn "Báo sự cố" out of scope (`C-CNL-01`) | Traceability không đứt; ⛔ không nhân bản SC |
| 2026-09-07 | REFACTOR | Đổi tên thư mục module `DLV/` → `DLV-giao-nhan/` — tên gợi nghĩa để người mới đọc thư mục là biết chức năng. Cập nhật kèm: frontmatter `id:` của 5 deliverable + `module.dir` ở file này + mọi cross-ref `DLV/<file>.md` | Yêu cầu QC GiangDC2 2026-09-07 (mã 2–4 chữ không nói lên chức năng) · `Project_rule §Module Codes` nay có cột `Dir` riêng | ⛔ **Mã module `DLV` và toàn bộ ID (`REQ-DLV-*` · `SC-DLV-*`) KHÔNG đổi** — chỉ đường dẫn thư mục đổi. TC chưa sinh nên không TC nào bị ảnh hưởng |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **CHỈ Receiver được xác nhận "Đã nhận hàng"** — ⛔ KHÔNG theo `DLV-03` (*"RECEIVER/SENDER"*) | `C-DLV-01` Resolved 2026-07-24: `BR-INT-03`+`US-D21`+PRD §5.2+**5 ảnh Figma** thắng `DLV-03` | Cho Sender tự chốt đơn của mình ⇒ mất hoàn toàn giá trị xác nhận 2 phía; `BR-CNF-04` (nhắc/admin) thành vô nghĩa |
| 2 | ⛔ **Ma trận nút CHỈ áp cho màn Theo dõi đơn** (role-aware) — ⛔ KHÔNG áp cho màn Chi tiết tin public | `KP-01` §5.1 ghi rõ phạm vi; màn Chi tiết tin có bug role-aware riêng (`SC-FEED-011`) | Log bug oan cho màn đã làm đúng, và làm loãng bug thật ở màn Chi tiết tin |
| 3 | ⛔ **KHÔNG gộp 15 ô ma trận theo trạng thái** (5 SC thay vì 15) | Mỗi ô = 1 tiền đề riêng (1 trạng thái × 1 vai); gộp thì FAIL không chỉ ra vai nào sai | Đúng loại lỗi mà `§Custom Rules §10.2` sinh ra để chặn; và mất chính giá trị lớn nhất của knowledge pack |
| 4 | ⚠️ **Trạng thái đơn là MỘT CHIỀU, không lùi được** — mỗi trạng thái phải xem bằng **cả 3 vai TRƯỚC KHI** đẩy sang trạng thái kế tiếp | Mọi transition đi qua popup xác nhận, không có undo (`DOC-v1.0-02` §6 L191) | Bỏ sót 1 vai ở 1 trạng thái ⇒ phải tạo đơn mới và chạy lại từ đầu; chi phí gấp đôi |
| 5 | ⚠️ **`SC-DLV-029` (Lịch sử) chỉ chạy trên đơn đi THẲNG tới Hoàn thành** | `C-CNL-02`/`KB-CNL-01`: huỷ nhận đơn **XOÁ dòng "Ghép thành công"** khỏi LỊCH SỬ | Thiếu mốc bị chẩn đoán sai thành bug của `DLV`, trong khi bug thật thuộc `CNL` |
| 6 | ⚠️ **Hai danh sách mốc khác nhau** — thanh trạng thái (`Chờ ghép → Lấy hàng → Đang giao → Đã giao → Hoàn thành`) ⟷ block Lịch sử (`Đăng tin → Ghép thành công → Lấy hàng → Đã giao → Hoàn thành`) | `DOC-v1.0-02` §3.6 (2 dòng bảng khác nhau) | TC completeness assert sai danh sách ⇒ FAIL ở mốc không thuộc thành phần đang kiểm |
| 7 | ⚠️ **"Đã ghép" (badge) và "Lấy hàng" (mốc) là CÙNG trạng thái `MATCHED`** | `KP-01` §5.1 lưu ý thuật ngữ | TC đòi 2 chỗ cùng một chữ ⇒ FAIL ở 1 trong 2 chỗ và kết luận sai là app hiện sai trạng thái |
| 8 | ⛔ **KHÔNG assert ảnh bằng chứng / điểm uy tín carrier** ở màn xác nhận nhận hàng | `C-DLV-03` Resolved: dùng **modal đơn giản**; form đầy đủ không áp dụng v1.0 | Assert thành phần ngoài scope ⇒ FAIL, và kéo `PUP-03` + điểm uy tín (đã defer) vào scope một cách không chủ đích |
| 9 | ⛔ **KHÔNG assert chuỗi lịch sử "Hoàn thành & đã đánh giá"** | *"đã đánh giá"* là UI leftover của rating đã bị `C-GIFT-01` defer | Viết TC cho tính năng đánh giá không tồn tại ở v1.0 |
| 10 | ⚠️ **`SC-DLV-024` (nhắc 2h/admin 4h): chưa chạy đủ mốc thời gian thì GHI RÕ** | Cần chờ thật hoặc dev seed timestamp (`RISK-DLV-04`) | Khai coverage cho nhánh chưa chạy = báo cáo sai; nhánh này lại là cơ chế bảo vệ khi Receiver vắng mặt |

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 **Seed tiền đề 15 ô ma trận:** 3 tài khoản 3 vai + 3 phiên song song + 1 đơn qua đủ 5 trạng thái | `RISK-DLV-02` Open — chi phí thiết lập cao nhất dự án | Lập checklist 15 ô theo thứ tự trạng thái; hoàn tất từng trạng thái trước khi đẩy tiếp |
| 2 | 🔴 **Vibe-test đối chiếu nhãn thật 15 ô** với ma trận `KB-DLV-01` (nguồn `QA-obs` + Figma từ 2026-07) | `RISK-DLV-03` Open | `/vibe-test` màn Theo dõi đơn ở đủ 5 trạng thái **trước** generate-tc; lệch → `/analyze --update` |
| 3 | 🔴 **`SC-DLV-024`** cần 2 giờ + 4 giờ thực tế hoặc dev seed timestamp | `RISK-DLV-04` Open | Kế hoạch chạy riêng; hoặc nhờ dev seed `delivered_at` lùi 4 giờ |
| 4 | 🟡 **3 REQ gap SC chủ đích** — `PUP-03` (ảnh hàng) · `GPS-01` (vị trí) · `COST-01` (chi phí): chờ PM chốt scope nhánh phụ (`KP-05 §1` câu #2, treo từ 2026-07-24) | `RISK-DLV-05` Pending | Hỏi PM; nếu vào scope → `/analyze --update` bổ sung SC. ⛔ Không tự viết SC khẳng định khi chưa có bề mặt UI |
| 5 | 🟡 `C-DLV-02` — chia sẻ vị trí mặc định bật/tắt (BA nói "phase sau" nhưng chưa cho giá trị) | Open, non-blocking | Hỏi BA cùng lượt với câu hỏi scope của PM |
| 6 | 🟡 `REQ-DLV-011` (bản đồ ở Theo dõi đơn) gap SC vì trùng `SC-FEED-009` — nếu `C-FEED-01(b)` chốt có bản đồ thật thì phải mở SC riêng cho màn này | Quyết định có chủ đích 2026-09-07 | Theo dõi `C-FEED-01`; chốt "có bản đồ thật" → `/analyze --update` |
