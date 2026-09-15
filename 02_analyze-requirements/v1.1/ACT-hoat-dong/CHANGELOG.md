---
id: v1.1/ACT-hoat-dong/changelog
title: Changelog — Module ACT
type: changelog
version: v1.1
sprint: 1
module:
  code: ACT
  dir: ACT-hoat-dong
  name: Hoạt động (Đơn của tôi)
doc_source:
  - id: DOC-v1.1-01
    section: "§8.17 FR17 (Empty state) · §8.17.1 EMP-05/EMP-06 (+ bảng 8 dòng) · §8.17.2 BR17-01..03 · §6.2 AC-29.1.01 / AC-09.1.01 / AC-24.2.01 · §8.5.1 BR05-03 · §8.14.1 BR14-03 · §4 SCOPES"
id_range:
  req: "REQ-ACT-010 (NEW) + REQ-ACT-001, REQ-ACT-004, REQ-ACT-005, REQ-ACT-008, REQ-ACT-009 (MODIFIED, giữ ID sprint 1)"
  sc: "SC-ACT-015, SC-ACT-016, SC-ACT-017 (NEW) + SC-ACT-001, SC-ACT-005, SC-ACT-008, SC-ACT-012, SC-ACT-013, SC-ACT-014 (MODIFIED, giữ ID sprint 1)"
  cl: "C-ACT-02 (NEW) + C-ORD-06 (home canonical ở module này — chuyển Resolved, giữ ID) · C-ACT-01 (không đổi)"
  risk: "RISK-ACT-06, RISK-ACT-07, RISK-ACT-08 (NEW) + RISK-ACT-03, RISK-ACT-04 (Status/Severity cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-15
---

# Changelog — Module ACT (`ACT`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-15 | UPDATE | **DELTA v1.1 (lượt bù — module này bị bỏ sót ở lượt delta đầu).** Kết quả: **+1 REQ, +3 SC, +3 RISK, +1 CL**; **5 REQ / 6 SC MODIFIED**. Ba việc lớn: (a) **`C-ORD-06` ĐÓNG** — CL lan rộng nhất dự án (5 màn / 6 SC), home canonical ở module này, lần này Resolved bằng **tài liệu đã phê duyệt** chứ không phải lời chốt miệng như lần bị REVERT 2026-07-29; (b) `RETURNED` — kết cục đơn hoàn toàn mới — tạo cặp **đối chứng với `CANCELLED`** (`SC-ACT-015`); (c) `SC-ACT-013` (★ leftover) chuyển từ `[GAP]` sang **defect đủ căn cứ log bug** | `DOC-v1.1-01` §8.17/§8.17.1/§8.17.2 · §6.2 AC-29/AC-09/AC-24 · §8.5.1 BR05-03 · §8.14.1 BR14-03 · §4 | 2 SC empty state hết gap ⇒ **regenerate TC**, ⛔ không patch; `C-ACT-02` (nhãn tab) phải chốt **trước** `generate-tc` |
| 2026-09-15 | ĐÍNH CHÍNH | Phát hiện **xung đột nhãn PRD ⟷ app**: PRD gọi 2 tab "Đang chạy"/"Hoàn tất" và màn là "Đơn của tôi"; app STG hiển thị "Đang diễn ra"/"Đã hoàn thành", bottom nav "Hoạt động". `SC-ACT-001` **tạm hạ phần nhãn xuống ghi nhận**, ⛔ không assert cứng bên nào | `DOC-v1.1-01` §8.17.1 EMP-05/EMP-06 · §6.2 AC-09.1.01 vs `KP-01` §3 KB-ORD-07 · áp `Project_rule §Custom Rules §10.1` | Mở `C-ACT-02`; nhãn tab nằm trong Steps của nhiều TC ở nhiều module ⇒ chốt muộn sẽ phải sửa rải rác |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | ⛔ **KHÔNG assert cứng nhãn 2 tab** cho tới khi `C-ACT-02` được chốt | PRD ≠ app, và cả 2 nguồn đều "chính thức" theo cách của nó (`§Custom Rules §10.1`) | Chọn PRD ⇒ TC FAIL hàng loạt vì lý do không phải bug; chọn app ⇒ hợp thức hoá việc app lệch đặc tả đã phê duyệt |
| 3 | ⭐ **Bất đối xứng CTA giữa `EMP-05` và `EMP-06` là nội dung PHẢI assert** — tab đang-chạy **có** CTA, tab hoàn-tất **không** | `BR17-01` viết *"tối đa một CTA"* ⇒ "không có" là lựa chọn thiết kế hợp lệ, không phải thiếu sót | Bỏ qua ⇒ app hiện thừa/thiếu nút mà TC vẫn PASS |
| 4 | ⭐ **`EMP-06` phải assert thêm *"ẩn luôn khối lịch sử"*** — hành vi NGOÀI cấu trúc chuẩn `BR17-01`, chỉ tab này có | Khung lịch sử rỗng vẫn hiện thì trông "gần đúng" nên rất dễ lọt | Lỗi hiển thị lọt qua vì TC chỉ kiểm chuỗi text |
| 5 | ⛔ **KHÔNG tách `SC-ACT-015` thành 2 SC rời** — Given phải có **cả** đơn `CANCELLED` lẫn đơn `RETURNED` | Giá trị của SC nằm ở phép **đối chứng**: 2 kết cục bất thường, 2 cách xử lý ngược nhau (`RISK-ACT-07`) | Tách ra ⇒ mất đúng cái SC sinh ra để bắt (dev gộp 2 nhánh thành 1) |
| 6 | ⛔ **KHÔNG nhân bản text `EMP-01..04`, `EMP-07`, `EMP-08`** sang module này — chỉ giữ `EMP-05`/`EMP-06` + rule hình thức chung | `C-ORD-06` chạm 5 màn; mỗi text có home ở module sở hữu màn đó | 8 bản sao của cùng 1 bảng ⇒ 8 chỗ để drift |
| 7 | ⚠️ **`SC-ACT-017` giữ nhãn `[GAP]`** — *"cờ dữ liệu rỗng, không dựa null từng field"* là rule **backend**, UI chỉ thấy triệu chứng | `§Custom Rules §10.1` bước 3: ghi nhận, không viết TC khẳng định cho rule không có bề mặt | TC khẳng định cho rule không verify được ⇒ FAIL vĩnh viễn hoặc PASS giả |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"text empty state chưa chốt — chỉ ghi nhận, không assert"** (`C-ORD-06`, REVERT 2026-07-29) **HẾT HIỆU LỰC** — đừng trích lại. Hiện hành: **8 empty state có text chính thức** ở `DOC-v1.1-01 §8.17.1`, phân chia về từng module; `SC-ACT-012`/`SC-ACT-014` assert **verbatim**.

⛔ Kết luận **"★ leftover là dấu vết của phase sau, không log bug"** (suy từ `C-GIFT-01` *"out of scope v1.0"*) **HẾT HIỆU LỰC**. Hiện hành: đánh giá sao bị loại trừ **vĩnh viễn** (`§4 SCOPES`, `BR14-03`) ⇒ ★ còn sót **là defect**. Home phán quyết ở `GIFT`.

## 3. Nợ đang mở

| # | Nợ | Vì sao còn treo | Hướng xử lý |
|---|---|---|---|
| 1 | 🔴 **`C-ACT-02`** — nhãn 2 tab + tên màn theo PRD hay app | PRD nhất quán 3 chỗ, app nhất quán theo cách khác; không bên nào sai rõ ràng | **Chốt trước `generate-tc`** — nhãn tab nằm trong Steps của nhiều TC ở nhiều module (`RISK-ACT-06`) |
| 2 | 🔴 **`C-ACT-01` vẫn Open** — tap card mở "Chi tiết tin" hay "Theo dõi đơn" | PRD không nêu đích điều hướng của card ở màn này | Giữ `SC-ACT-011` dạng `[GAP]`; hỏi BA cùng lượt với `C-ACT-02` |
| 3 | 🟡 **`SC-ACT-015` / phần `RETURNED` của `SC-ACT-005` chờ nhánh `FR09`** | Trạng thái `RETURNED` mới ở v1.1, `RISK-DLV-08` cảnh báo app có thể chưa build | Gộp lô với `SC-DLV-053..056`; nếu chưa có thì verdict `BLOCKED`, ⛔ không PASS |
| 4 | 🟡 **Tài khoản trắng dùng chung** cho `SC-ACT-012/014/016/017` | Cùng nhu cầu với `SC-HOME-025..027` và `SC-GIFT-008`; môi trường đã có dữ liệu thì không tái tạo được | Xin **1 tài khoản mới tinh**, chạy hết cụm empty state trong 1 lượt rồi mới để nó "bẩn" |
| 5 | 🟡 **`SC-ACT-017` cần throttle mạng** | Mạng nhanh thì pha loading trôi quá nhanh, không phân biệt được *đang tải* ⟷ *không có dữ liệu* | Ghi rõ bước throttle 3G trong Steps của TC |
