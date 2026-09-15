---
id: v1.1/USR-tai-khoan/changelog
title: Changelog — Module USR
type: changelog
version: v1.1
sprint: 1
module:
  code: USR
  dir: USR-tai-khoan
  name: Tài khoản & Hồ sơ
doc_source:
  - id: DOC-v1.1-01
    section: "§8.15 FR15 (Hồ sơ & cập nhật thông tin) · §8.15.1 BR15-01..05 · §8.15.2 UI/Field Spec · §6.1 US30 · §6.2 AC-30.1.01 / AC-30.1.02 / AC-30.2.01 / AC-30.2.02"
id_range:
  req: "REQ-USR-008, REQ-USR-009, REQ-USR-010 (NEW) + REQ-USR-002, REQ-USR-006 (MODIFIED, giữ ID sprint 1)"
  sc: "SC-USR-013..020 (NEW, 8) + SC-USR-002, SC-USR-003, SC-USR-012 (MODIFIED, giữ ID sprint 1)"
  cl: "C-USR-05 (NEW) + C-USR-03 (ĐẢO → Resolved), C-USR-04 (→ Partially Resolved) — giữ ID sprint 1"
  risk: "RISK-USR-06, RISK-USR-07, RISK-USR-08 (NEW) + RISK-USR-01, RISK-USR-03 (Status/Why cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-15
---

# Changelog — Module USR (`USR`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-15 | ĐÍNH CHÍNH | 🔴 **Quyết định *"`USR` không có delta ở v1.1"* (ghi ở `MASTER-MEMORY §2` ghi chú registry, cùng ngày) là SAI và đã được gỡ.** Hai bằng chứng: (a) `FR15` đặc tả **một màn mới** (`"Cập nhật thông tin"`) với 5 BR + 4 AC — đây là thay đổi hành vi thật, không phải "đề xuất xung đột"; (b) **chính lượt delta trước đã trích `AC-30.1.01` — một AC THUỘC `FR15`** — làm nguồn resolve `C-ORD-10`, tức đã dùng `FR15` làm căn cứ trong khi tuyên bố nó ngoài phạm vi | QC GiangDC2 nêu lại 2026-09-15 (*"1.1 chỗ profile có update"*); rà lại `DOC-v1.1-01` §8.15 toàn văn | Module chuyển từ *"không delta"* sang **có delta**; `v1.1/MEMORY.md` §1/§2 và `MASTER-MEMORY` §1/§3/§4/§5/§8b phải cập nhật theo |
| 2026-09-15 | UPDATE | **DELTA v1.1 (lượt bù thứ hai).** Kết quả: **+3 REQ, +8 SC, +3 RISK, +1 CL**; **2 REQ / 3 SC MODIFIED**. Ba việc lớn: (a) `C-USR-03` **ĐẢO** — hồ sơ từ *view-only hoàn toàn* thành *có màn sửa 2 trường*, `SC-USR-003` lật chiều; (b) `BR15-03`/`BR15-04` thêm **2 rule truy vết hai chiều** — thành viên thứ tư của nhóm rule mà app đã vi phạm 1 lần; (c) `C-USR-04` đóng được **nửa** (nhãn menu), `C-USR-05` mở mới cho 3 trường PRD không nhắc | `DOC-v1.1-01` §8.15 + §8.15.1 + §8.15.2 · §6.1 US30 · §6.2 AC-30.x | Risk Level module **Low → Medium**; 8 SC mới phụ thuộc app đã build `FR15` chưa (`RISK-USR-06`) |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | 🔴 **`SC-USR-003` phải lấy bản `v1.1/`** — bản v1.0 và v1.1 có Then **ngược nhau** ở phần *"có control sửa hay không"* | `C-USR-03` bị `FR15` đảo. **Cả hai bản đều chạy được** nên không có gì báo lỗi khi lấy nhầm | Chạy nhầm bản cho kết luận ngược, và **im lặng** — cùng bẫy `SC-CNL-006` |
| 3 | ⛔ **KHÔNG đọc `C-USR-03` thành "hồ sơ sửa được"** — hồ sơ có **2 vùng**: SSO chỉ đọc (4 trường) ⟷ sửa được (đúng **2** trường) | `BR15-01` giữ nguyên tinh thần view-only cho vùng SSO; `FR15` chỉ mở 2 trường | Viết TC cho phép sửa tên/email ⇒ FAIL vĩnh viễn trên một hành vi đúng |
| 4 | ⛔ **KHÔNG lấy `§8.15.2` làm danh sách trường của TRANG CÁ NHÂN** — đó là field spec của **màn "Cập nhật thông tin"**, một màn khác | `C-USR-04` mới Partially Resolved; trang Cá nhân vẫn chưa có bằng chứng UI đầy đủ | `SC-USR-002` assert sai danh sách trường |
| 5 | ⭐ **`SC-USR-014` · `017` · `018` bắt buộc có bước "ghi lại giá trị TRƯỚC"** | Banner xanh chỉ chứng minh app *nói* đã lưu; sai lệch hồ sơ/đơn không nhìn ra được nếu chỉ đọc số một lần | Cả ba PASS giả cho một màn/rule đang hỏng |
| 6 | ⛔ **KHÔNG nhân bản SC prefill sang `ORD`** — `SC-ORD-025` kiểm *wizard nhận đúng giá trị*, `SC-USR-018` kiểm *hồ sơ không bị ghi đè* | Hai đầu của cùng một sợi dây, fail độc lập | TC trùng; hoặc tệ hơn: cả hai cùng kiểm một đầu, đầu kia không ai kiểm |
| 7 | ⛔ **KHÔNG đưa avatar · khu vực/văn phòng · kênh liên hệ vào Test Data** | PRD không nhắc 3 trường này ở `§8.15` (`C-USR-05` Open); `KB-USR-01` lại ghi nhận app **có** avatar | Suy diễn *"không nhắc = đã bỏ"* ⇒ mất 1 SC đang đúng hoặc viết TC cho thứ không tồn tại |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"màn Cá nhân view-only hoàn toàn — KHÔNG có chức năng sửa hồ sơ"** (`C-USR-03`, Resolved 2026-07-24 **theo quan sát app STG**, home canonical ở `v1.0/USR-tai-khoan/risk_assessment.md`) **HẾT HIỆU LỰC kể từ v1.1** — đừng trích lại. Hiện hành: **CÓ** màn `"Cập nhật thông tin"` (trang Cá nhân, dưới mục "Quà đã nhận") cho sửa **đúng 2 trường** — `Số điện thoại mặc định` · `Địa chỉ mặc định`; 4 trường SSO vẫn chỉ đọc (`DOC-v1.1-01 §8.15`). Bản v1.0 **giữ nguyên không sửa** làm hồ sơ lịch sử.

⛔ Kèm theo: khai **"`USR` không có delta ở v1.1 — `FR15` không áp dụng"** (`MASTER-MEMORY §2` ghi chú registry, 2026-09-15) **HẾT HIỆU LỰC**. Ghi chú đó nhầm **đề xuất xung đột** (`FR15` cho sửa SĐT/địa chỉ ⟷ `C-USR-03` view-only) thành **lý do bỏ qua cả FR** — trong khi xung đột đó chính là nội dung cần phân tích.

📌 **Bài học rút ra (áp cho mọi module):** cả hai lần đảo kết luận của dự án (`C-CNL-01` và `C-USR-03`) đều rơi vào CL được Resolved **theo quan sát app**, ⛔ không theo tài liệu. ⇒ CL loại này là **ứng viên số 1 để rà lại** mỗi khi có tài liệu mới; nên đánh dấu rõ khi ghi.

## 3. Nợ đang mở

| # | Nợ | Vì sao còn treo | Hướng xử lý |
|---|---|---|---|
| 1 | 🔴 **Chưa xác nhận app STG đã build `FR15`** | App quan sát 2026-07-24 là **view-only hoàn toàn**; PRD rev 08/09/2026 | **Vibe-test 1 lượt trang Cá nhân trước `generate-tc`**. Chưa có ⇒ 8 SC mới verdict `BLOCKED`, ⛔ không PASS và ⛔ không quay lại kết luận v1.0 (`RISK-USR-06`) |
| 2 | 🔴 **`C-USR-05`** — avatar · khu vực/văn phòng · kênh liên hệ | BRD `USR-02` liệt kê 6 trường, `FR15` xử lý 5 (+email); 3 trường này PRD **không nhắc ở đâu** | Gộp vào lượt hỏi BA chung với `C-ORD-04` · `C-ORD-09` · `C-ACT-02` — đều là câu hỏi doc ⟷ app / doc thiếu |
| 3 | 🟡 **`C-USR-04` mới đóng một nửa** | Nhãn menu đã biết; **danh sách trường của trang Cá nhân** vẫn chưa có bằng chứng UI | Bổ sung bằng vibe-test cùng lượt với nợ #1 (cùng màn, 1 lượt chụp là đủ cả hai) |
| 4 | 🟡 **`SC-USR-017` chờ chạy cùng lô nhóm rule truy vết** | Cùng họ `SC-CNL-010` · `SC-ORD-065` · `SC-DLV-062`; app đã vi phạm nhóm này 1 lần | Chạy 4 SC cùng lô; cùng vỡ ⇒ **1 bug report cho nguyên nhân gốc**, ⛔ không log 4 bug rời (`RISK-USR-07`) |
