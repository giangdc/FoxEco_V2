---
id: v1.1/DLV-giao-nhan/changelog
title: Changelog — Module DLV
type: changelog
version: v1.1
sprint: 1
module:
  code: DLV
  dir: DLV-giao-nhan
  name: Giao nhận & Theo dõi đơn
doc_source:
  - id: DOC-v1.1-01
    section: "§8.6 FR06 · §8.7 FR07 · §8.8 FR08 · §8.9 FR09 · §8.10.1 BR10-04 · §8.12 FR12 (state machine + log) · §8.18.1 BR18-04 · §9 NFR-03/07/12"
id_range:
  req: "REQ-DLV-017..023 (NEW) + REQ-DLV-002, REQ-DLV-007, REQ-DLV-012 (MODIFIED, giữ ID sprint 1)"
  sc: "SC-DLV-031..064 (NEW, 34 SC) — gắn REQ MODIFIED lẫn NEW"
  cl: "C-DLV-04 (NEW, Resolved cùng lượt)"
  risk: "RISK-DLV-08, RISK-DLV-09, RISK-DLV-10, RISK-DLV-11 (NEW) + RISK-DLV-05 (Status cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-15
---

# Changelog — Module DLV (`DLV`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-15 | UPDATE | **DELTA v1.1 — delta lớn nhất của version.** PRD chính thức (`DOC-v1.1-01`) đưa vào 2 luồng hoàn toàn mới (FR08 "Không liên lạc được người nhận", FR09 "Cầm hàng về") + mở rộng lớn màn "Xác nhận giao hàng" (FR07, 4 loại đối tượng nhận, thay 1 nút+popup đơn giản) + state machine 12 trạng thái đầy đủ (FR12, thay 5 trạng thái cốt lõi) + mẫu câu nhật ký chính xác (§8.12.4) + resolve gap `PUP-03` (ảnh lúc lấy hàng). +7 REQ mới (`REQ-DLV-017..023`), +34 SC mới, 3 REQ MODIFIED (giữ ID). `GPS-01`/`COST-01` vẫn ngoài scope | `DOC-v1.1-01` §8.6-§8.10, §8.12, §8.18.1, §9 | Module từ 16 REQ/30 SC (v1.0) lên 26 REQ/64 SC (v1.1); rủi ro execute cao ở `RISK-DLV-08` (app STG cần vibe-test xác nhận trước) |
| 2026-09-15 | UPDATE | Vibe-check qua demo (`00_input/v1.1/design/DLV_01..07`) — hạ `RISK-DLV-08` xuống Partially confirmed (cấu trúc form "Xác nhận giao hàng" khớp PRD, 4 loại đối tượng nhận; chưa verify submit end-to-end vì demo không upload ảnh được). Phát hiện `RISK-DLV-11` (mới): popup "Tôi đã lấy hàng" trên demo thiếu field ảnh dù `C-DLV-04`/`BR06-01` đã resolve field này tồn tại. Không chụp được màn kết quả `RESCHEDULED`/`RETURNING`/nhóm đóng (`SC-DLV-031..033`) — form escalation bị chặn ở đúng ô ảnh bằng chứng | Vibe-check thủ công qua Playwright, theo yêu cầu QC GiangDC2 2026-09-15 | `SC-DLV-037..042` giảm rủi ro FAIL-oan; `RISK-DLV-11` cần verify STG; `SC-DLV-031..033` vẫn thiếu bằng chứng màn kết quả |
| 2026-09-15 | ĐÍNH CHÍNH | 3 sai số ở frontmatter `counts:`: (a) `req: 26` đếm trùng 3 REQ MODIFIED (16 v1.0 + 10 dòng v1.1, trong đó 3 dòng là REQ cũ) ⇒ **23**; (b) `new: 31 / modified: 3` không khớp bảng — cả **34** dòng chi tiết đều gắn Lifecycle `NEW` ("MODIFIED-context" nói về **REQ** giữ ID, không phải SC) ⇒ `new: 34 / modified: 0`; (c) `P 9/33/22` ⇒ **10/42/12** (v1.0 CARRIED 4/25/1 + v1.1 NEW 6/17/11) | `health-check` 2026-09-15 G-02; đếm lại theo chỉ số cột `Priority`/`Lifecycle` của bảng | Tổng SC **64 không đổi**. Phân bổ priority đổi đáng kể (P3 22→12) ⇒ `generate-tc` lấy priority **theo từng dòng SC**, ⛔ không lấy theo aggregate |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — thư mục dùng lại qua nhiều sprint, phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | ⛔ **KHÔNG nhầm `REQ-DLV-017` (Carrier, FR07) với `C-DLV-03` (Receiver, FR10)** — 2 màn hình, 2 vai trò, 2 chiều transition khác nhau | Cả 2 đều dính từ khoá "xác nhận giao/nhận hàng", rất dễ nhầm khi đọc lướt | Trích sai quote cho SC sai màn; viết TC vào nhầm màn hình |
| 3 | ⚠️ **`RISK-DLV-08` — BẮT BUỘC vibe-test màn "Xác nhận giao hàng" trước `generate-tc`** | Thay đổi từ 1 nút+popup sang form 4 loại đối tượng nhận — rủi ro app STG chưa build lại | Nếu bỏ qua: `SC-DLV-037..042` FAIL hàng loạt vì "app chưa cập nhật", báo cáo sai lệch coverage thật |
| 4 | ⚠️ **`SC-DLV-062` dự kiến FAIL có chủ đích cho tới khi bug `RISK-TS-01` được fix** | NFR-07 (log append-only) đối chiếu trực tiếp bug đã biết (huỷ nhận đơn xoá log) | Nếu không ghi rõ trong test report → hiểu nhầm coverage 100% pass |
| 5 | ⛔ **`GPS-01`/`COST-01` KHÔNG viết SC** — PRD v1.1 đã rà toàn văn, không nhắc | `RISK-DLV-05` cập nhật: chỉ `PUP-03` được resolve | Viết SC không có nguồn — vi phạm nguyên tắc "không sáng tạo scenario ngoài requirement" |

### 🔁 Kết luận bị đảo

*(Không có kết luận nào bị đảo ở lượt này — `REQ-DLV-017` là MỞ RỘNG so với v1.0, không mâu thuẫn/đảo bất kỳ CL nào đã Resolved. Xem ràng buộc #2 để tránh nhầm với `C-DLV-03`.)*

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🟡 `RISK-DLV-08` — cấu trúc UI đã xác nhận qua demo (4 loại đối tượng nhận khớp PRD); CHƯA xác nhận luồng submit end-to-end trên STG thật (demo không upload ảnh được) | Partially confirmed — còn 1 phần cần vibe-test STG | Chạy `vibe-test` màn này trên STG (có ảnh thật) TRƯỚC `generate-tc`; nếu app chưa cập nhật, báo PM/dev |
| 1b | 🟡 `RISK-DLV-11` (mới) — popup "Tôi đã lấy hàng" trên demo thiếu field ảnh dù `C-DLV-04` đã resolve field này tồn tại (tuỳ chọn) | Open — cần vibe-test STG | Verify cùng lượt STG ở mục #1; nếu STG cũng thiếu → log bug (PRD/app lệch) |
| 1c | 🟡 Chưa chụp được màn kết quả `RESCHEDULED`/`RETURNING`/nhóm đóng (`SC-DLV-031..033`) | Blocked — demo không cho hoàn tất luồng "Xử lý đơn hàng" (ô ảnh bằng chứng không thao tác được) | Bổ sung ảnh khi có STG thật hoặc demo được sửa lại phần upload ảnh |
| 2 | 🔴 `RISK-DLV-09`/`SC-DLV-062` — bug log không bất biến (`RISK-TS-01`) chưa fix | Kế thừa từ v1.0, giờ có NFR chính thức xác nhận vi phạm | Ưu tiên `log-bug` nếu chưa log; theo dõi tiến độ fix trước khi coi `SC-DLV-062` là PASS thật |
| 3 | 🟡 `RISK-DLV-10` — `SC-DLV-048`/`SC-DLV-054` cần tiền đề thời gian dài (4h-24h) | Chưa có kế hoạch chạy cụ thể | Gộp lịch với `SC-DLV-024`/`SC-TS-006` (cùng nhóm tiền đề); dev seed timestamp nếu có thể |
| 4 | 🟡 `GPS-01`/`COST-01` vẫn Pending, không có SC | Ngoài phạm vi PRD v1.1 | Giữ nguyên tới khi có tài liệu mới nhắc tới 2 nhánh này |
