---
id: v1.1/GIFT-qua-cam-on/changelog
title: Changelog — Module GIFT
type: changelog
version: v1.1
sprint: 1
module:
  code: GIFT
  dir: GIFT-qua-cam-on
  name: Quà cảm ơn
doc_source:
  - id: DOC-v1.1-01
    section: "§8.14 FR14 (Quà ảo & thống kê cá nhân) · §8.14.1 BR14-01..04 · §6.2 AC-24.1.01 / AC-24.2.01 / AC-26.1.01 / AC-26.2.01 · §8.17.1 EMP-08 · §4 SCOPES Out of Scope"
id_range:
  req: "REQ-GIFT-009 (NEW) + REQ-GIFT-001, REQ-GIFT-002, REQ-GIFT-004, REQ-GIFT-005, REQ-GIFT-007 (MODIFIED, giữ ID sprint 1)"
  sc: "SC-GIFT-013, SC-GIFT-014 (NEW) + SC-GIFT-002, SC-GIFT-003, SC-GIFT-006, SC-GIFT-007, SC-GIFT-008, SC-GIFT-011 (MODIFIED, giữ ID sprint 1)"
  cl: "(không mở CL mới) — C-GIFT-01 và C-GIFT-03 chuyển Resolved, giữ ID sprint 1"
  risk: "RISK-GIFT-06 (NEW) + RISK-GIFT-02, RISK-GIFT-05 (Status/Why cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-15
---

# Changelog — Module GIFT (`GIFT`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-15 | UPDATE | **DELTA v1.1 (lượt bù — module này bị bỏ sót ở lượt delta đầu).** `FR14` + 4 AC lấp gap dày nhất so với kích cỡ module: **3 SC dạng `[GAP]` hết gap cùng lúc** (`SC-GIFT-007` lịch sử nhận quà · `SC-GIFT-008` text empty state · `SC-GIFT-011` không sao/điểm/tier). Thêm **1 REQ / 2 SC NEW** cho trạng thái `RETURNED` (`BR14-04` + `AC-24.2.01`) — trạng thái hoàn toàn mới do `FR09` của `DLV` sinh ra. **2 CL đóng** (`C-GIFT-01`, `C-GIFT-03`) | `DOC-v1.1-01` §8.14/§8.14.1 · §6.2 AC-24/AC-26 · §8.17.1 EMP-08 · §4 SCOPES | 3 SC hết gap phải **regenerate TC** (Then đổi từ *ghi nhận* sang *assert khẳng định*), ⛔ không patch TC cũ; 2 SC mới **phụ thuộc `DLV`/`FR09`** — có thể `BLOCKED` |
| 2026-09-15 | ĐÍNH CHÍNH | Phán quyết `C-GIFT-01` ở v1.0 — *"Out of scope **v1.0**"* — nay đọc được thành *"có thể có ở phase sau"*, khiến ★ leftover bị xem là dấu vết hợp lệ. Bản hiện hành: **out of scope VĨNH VIỄN** (§4 SCOPES, *"thay bằng quà ảo"*) | `DOC-v1.1-01` §4 SCOPES Out of Scope · §8.14.1 BR14-03 | `SC-ACT-013` (★ leftover ở `ACT`) chuyển từ *"[GAP] ghi nhận"* sang **defect đủ căn cứ log bug** |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | ⛔ **`SC-GIFT-013`/`SC-GIFT-014` không seed được ⇒ verdict `BLOCKED`, KHÔNG phải PASS** | Cả 2 là **vế phủ định**; không có đơn `RETURNED` nào thì *"không thấy nút tặng quà"* chẳng chứng minh điều gì | PASS oan — che mất việc bộ đếm có thể đang tính nhầm đơn hoàn hàng, lỗi âm thầm không ai thấy bằng mắt |
| 3 | ⚠️ **`SC-GIFT-014` bắt buộc có bước "ghi lại số TRƯỚC"** trong Steps/Test Data | Sai lệch 1 đơn trên bộ đếm không nhìn ra được nếu chỉ đọc số một lần | TC không phát hiện được lỗi nó sinh ra để bắt |
| 4 | ⚠️ **Rule *"loại `count = 0` không hiện card"* (`SC-GIFT-006`) KHÔNG có nguồn PRD** — vẫn đứng trên quan sát app v1.0 (`KB-GIFT-03`) | PRD chỉ nói *"card đếm quà theo từng loại"*, không nói gì về loại rỗng | Người sau tưởng rule đó có tài liệu chống lưng rồi log bug sai chiều |
| 5 | ⛔ **KHÔNG nhân bản SC cho bộ đếm "Đơn đã giúp"** sang `USR`/`HOME` — 3 màn cùng 1 con số, chạy 1 lượt so cả 3 | `BR14-04` áp cho bộ đếm, không cho màn cụ thể | TC trùng; và tệ hơn: 3 TC pass riêng lẻ nhưng 3 màn vẫn lệch nhau |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"Rating 1–5 sao — Out of scope *v1.0*"** (`C-GIFT-01`, Resolved 2026-07-27) **KHÔNG SAI nhưng ĐÃ HẸP** — đừng trích nguyên văn hai chữ "v1.0". Hiện hành: **out of scope của cả sản phẩm**, *"thay bằng quà ảo"* (`DOC-v1.1-01 §4 SCOPES`), và `BR14-03` mở rộng sang **điểm · tier/xếp hạng · chỉ số môi trường**. Hệ quả: mọi ★/điểm/tier còn sót trong app **đều là defect**, ⛔ không còn đường diễn giải "dấu vết phase sau".

## 3. Nợ đang mở

| # | Nợ | Vì sao còn treo | Hướng xử lý |
|---|---|---|---|
| 1 | 🟡 **`SC-GIFT-013`/`SC-GIFT-014` chờ nhánh `FR09` trên STG** | Trạng thái `RETURNED` là mới ở v1.1; `RISK-DLV-08` cảnh báo app có thể chưa build lại theo PRD | Gộp lô chạy với `SC-DLV-053..056` sau khi `vibe-test` xác nhận nhánh hoàn hàng đã có (`RISK-GIFT-06`) |
| 2 | 🔴 **`C-GIFT-02` vẫn Open** — nút back màn "Tặng quà" nhảy sang đơn khác | PRD không nhắc tới lỗi điều hướng này; nguồn vẫn là `QA-obs` 2026-07-29 | Tiếp tục xin BA xác nhận; `SC-GIFT-010` giữ nguyên dạng `[GAP·bug]` |
| 3 | 🟡 **Tài khoản "trắng" cho `SC-GIFT-008`** | Cần tài khoản chưa từng nhận quà — khó tái tạo khi môi trường đã có dữ liệu từ lô khác | Cùng nhóm khó với `SC-HOME-025..027`; xin 1 tài khoản mới tinh dùng chung cho cả cụm empty state |
