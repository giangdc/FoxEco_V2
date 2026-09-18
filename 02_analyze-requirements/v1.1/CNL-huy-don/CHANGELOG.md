---
id: v1.1/CNL-huy-don/changelog
title: Changelog — Module CNL
type: changelog
version: v1.1
sprint: 1
module:
  code: CNL
  dir: CNL-huy-don
  name: Huỷ đơn / Huỷ nhận đơn
doc_source:
  - id: DOC-v1.1-01
    section: "§8.11 FR11 (Huỷ đơn có lý do) · §8.11.1 BR11-01..04 · §6.2 AC-25.1.01/.02/.03 + AC-25.2.01 · §8.18.2 VAL-03/VAL-04 · §8.16 FR16 (đảo C-CNL-01) · §4 SCOPES"
id_range:
  req: "REQ-CNL-008, REQ-CNL-009 (NEW) + REQ-CNL-002, REQ-CNL-003, REQ-CNL-006, REQ-CNL-007 (MODIFIED, giữ ID sprint 1)"
  sc: "SC-CNL-014..017 (NEW) + SC-CNL-004, SC-CNL-006, SC-CNL-009, SC-CNL-010, SC-CNL-012 (MODIFIED, giữ ID sprint 1)"
  cl: "C-CNL-03 (NEW) + C-CNL-01, C-CNL-02 (giữ ID sprint 1 — cùng câu hỏi, trả lời lại bằng nguồn mạnh hơn) + C-CNL-03 → Resolved (2026-09-16)"
  risk: "RISK-CNL-07, RISK-CNL-08 (NEW) + RISK-CNL-01, RISK-CNL-02, RISK-CNL-03, RISK-CNL-06 (Severity/Why/Status cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-17
---

# Changelog — Module CNL (`CNL`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-17 | UPDATE | **Xác nhận scope `CNL` = IN scope v1.1.** `RISK-CNL-06` Pending → **Resolved**. Câu hỏi con đã dời sang module khác (đơn vào `INCIDENT` bằng cách nào → `C-TS-02`; "chuyển admin" ở các mốc nhắc → `C-DLV-07`) xử lý tại module đó, không mở lại ở `CNL` | QC GiangDC2 xác nhận 2026-09-17 | Nợ #3 (§3) đóng lại; chạy đủ 17 SC không cần chờ xác nhận PM thêm |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa WARNING health-check G-03:** thay 1 trích dẫn bị chép lặp sang file khác bằng dòng trỏ `↪` về đúng home (REQ → `requirement_traceability.md` · CL → `risk_assessment.md`) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Nội dung quote không mất — chỉ còn 1 home |
| 2026-09-16 | ĐÍNH CHÍNH | **Sửa theo health-check VERSION v1.1 (G-06b CRITICAL):** các đoạn register sống còn kể lại kết luận cũ của CL vừa Resolved (`C-CNL-03`/`RISK-CNL-07` — heading CL, Khuyến nghị #3) — đổi mục Khuyến nghị / heading / data catalog sang kết luận hiện hành và thêm dòng *"⛔ Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC"* sau các ghi chú gốc (giữ nguyên nội dung cũ làm hồ sơ, không xoá lặng lẽ) | `/health-check` 2026-09-16 · QC GiangDC2 yêu cầu sửa | Không đổi `counts`, không đổi Then SC — chỉ đồng bộ chữ với CL section |
| 2026-09-16 | UPDATE | **Áp câu trả lời BA**: `C-CNL-03` → **Resolved** — không có màn/tool admin, dev hỗ trợ tay qua Google Form, trạng thái đích tuỳ dev, người dùng không thấy gì. `RISK-CNL-07` High → **Accepted** (rủi ro vận hành đã biết). Câu hỏi còn lại về cách đơn **vào** INCIDENT chuyển sang `C-TS-02` (home `TS`); "chuyển admin" ở các mốc nhắc chuyển sang `C-DLV-07` | BA trả lời 2026-09-16 | `counts` cl_open 1→0, cl_resolved 2→3; `SC-CNL-017` assert cứng thay vì GAP |
| 2026-09-15 | UPDATE | **DELTA v1.1 (lượt bù — module này bị bỏ sót ở lượt delta đầu).** PRD chính thức đặc tả `FR11` đầy đủ: `BR11-01..04` + 4 AC. Kết quả: **+2 REQ, +4 SC, +2 RISK, +1 CL**; **4 REQ / 5 SC MODIFIED**. Ba thay đổi quan trọng nhất: (a) `C-CNL-01` **ĐẢO** — màn Báo sự cố từ *out of scope* thành *in scope*, `SC-CNL-006` lật chiều Then; (b) `C-CNL-02` nâng căn cứ từ *"override QA"* thành *đặc tả PM*, `SC-CNL-010` **P2→P1**; (c) ngưỡng được-huỷ phát biểu theo **hành động** thay vì **trạng thái** ⇒ lộ ra ô biên mới `SC-CNL-016` | `DOC-v1.1-01` §8.11/§8.11.1 · §6.2 AC-25.x · §8.18.2 VAL-03/04 · §8.16 · §4 | 3 bug đã biết nay có căn cứ PRD ⇒ severity cao hơn khi log; `SC-CNL-006` **không được chạy bản v1.0**; `generate-tc` phải đọc chéo `TS` (`RISK-CNL-08`) |
| 2026-09-15 | ĐÍNH CHÍNH | Nhận định *"PRD không mang thêm thông tin nào cho CNL"* — ghi ở `v1.1/TS-trust-safety/requirement_traceability.md §2 REQ-TS-006` trong lượt delta đầu — **SAI**. PRD có hẳn `FR11` + 4 AC riêng cho `CNL`, và chính `AC-25.2.01` (thuộc US25 của `CNL`) mới là câu đảo `C-CNL-01` dứt khoát nhất | Rà lại toàn văn PRD §8.11 + §6.2 trong lượt delta bù này | Nhận định cũ đã khiến `CNL` bị xếp "không cần delta" và nợ lại 8 ngày; ⛔ đừng trích lại câu đó |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — thư mục dùng lại qua nhiều sprint, phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | 🔴 **`SC-CNL-006` phải lấy bản `v1.1/`** — bản v1.0 và v1.1 có Then **NGƯỢC NHAU** (v1.0: PASS = *không thấy* nút Báo sự cố · v1.1: PASS = *thấy* nút) | `C-CNL-01` bị đảo bởi `FR16` | Chạy nhầm bản cho kết luận ngược 180°, và vì cả hai bản đều "chạy được" nên **không có gì báo lỗi** |
| 3 | ⛔ **KHÔNG sửa expected của `SC-CNL-004/009/010/012` cho PASS** — 4 SC viết theo spec, FAIL là kết quả ĐÚNG | 4 gap đã live-verify 2026-07-29 + nay có `BR11-01/02/03` + `VAL-03/04` + `AC-25.1.01/02/03` chống lưng | Hợp thức hoá việc xoá log audit và việc lý do huỷ có thể vô nghĩa; 4 bug sẽ không bao giờ được log |
| 4 | ⛔ **KHÔNG viết TC khẳng định cho hành vi "Admin vận hành"** — chỉ assert **không có** bề mặt Admin (`SC-CNL-017`) + đơn INCIDENT không tự đóng; ⛔ không assert trạng thái đích sau INCIDENT | `C-CNL-03` Resolved 2026-09-16: dev xử lý tay, trạng thái đích tuỳ dev, người dùng không thấy gì | TC cho màn/luồng không tồn tại ⇒ FAIL vĩnh viễn |
| 5 | ⛔ **KHÔNG nhân bản 8 SC của `TS`** (`SC-TS-008..015`) sang `CNL` — `CNL` chỉ giữ *nút thoát tồn tại* + *hệ quả trạng thái* | `FR16` vắt qua 2 module; bề mặt form WebView có home ở `TS` | TC trùng lặp; sửa 1 chỗ quên chỗ kia |
| 6 | ⚠️ **`SC-CNL-008` khi generate TC phải assert đủ 3 thành phần log** — vai trò · lý do · **thời điểm** | `BR11-02` nêu 3, bản v1.0 của SC chỉ assert 2 | Bug "log thiếu timestamp" lọt qua vì TC không kiểm |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"màn 'Báo sự cố' chưa có đặc tả — out of scope v1.0"** (`C-CNL-01`, Resolved 2026-07-27, home canonical ở `v1.0/CNL-huy-don/risk_assessment.md`) **HẾT HIỆU LỰC kể từ v1.1** — đừng trích lại. Hiện hành: **có đặc tả đầy đủ, VÀO scope** (`DOC-v1.1-01 §4 SCOPES` + `§8.16` + `§6.2 AC-25.2.01`). Bản v1.0 **giữ nguyên không sửa** làm hồ sơ lịch sử; bản hiện hành ở `v1.1/CNL-huy-don/risk_assessment.md`.

⛔ Kèm theo: **`REQ-CNL-007` không còn là "gap SC có chủ đích"** (nợ #2 của `v1.0/CNL-huy-don/CHANGELOG.md §3`) — nợ đó **đóng lại**, lý do *"không tài liệu nào mô tả field/màn"* đã hết đúng.

⛔ Và: ràng buộc số 5 của `v1.0/CNL-huy-don/CHANGELOG.md §2` — ***"⛔ KHÔNG viết TC luồng 'Báo sự cố'"*** — **HẾT HIỆU LỰC**. Hiện hành: TC cho luồng này **được viết**, home ở `TS` (`SC-TS-008..015`), `CNL` giữ phần nút thoát + hệ quả trạng thái.

## 3. Nợ đang mở

| # | Nợ | Vì sao còn treo | Hướng xử lý |
|---|---|---|---|
| 1 | 🟡 **`RISK-CNL-07` Accepted** — đơn INCIDENT phụ thuộc dev xử lý tay | BA xác nhận 2026-09-16 không có tool/SLA | Ghi rõ trong test report như rủi ro vận hành được chấp nhận; báo PM nếu cần SLA |
| 2 | 🟡 **`SC-CNL-015` có thể không seed được** | Cần đơn ở trạng thái `INCIDENT`; app STG có thể chưa build `FR16` | Verdict đúng khi đó là **BLOCKED**, ⛔ không PASS. Chạy sau khi `vibe-test` xác nhận `FR16` đã có trên STG |
| 3 | ✅ ~~Xác nhận scope `CNL` với PM~~ | **Đóng 2026-09-17** — QC GiangDC2 xác nhận IN scope (`RISK-CNL-06` Resolved) | Không còn treo — chạy đủ 17 SC |
| 4 | 🟡 **`v1.0/DLV-giao-nhan/` còn trích `C-CNL-01` theo nghĩa cũ** | 2 chỗ: dòng CL ở `risk_assessment.md` và `REQ-DLV-015` ở `requirement_traceability.md`. Thuộc v1.0 ⇒ **không sửa** theo `Project_rule` | Người đọc lần ra bản hiện hành qua `v1.1/CNL-huy-don/risk_assessment.md` + mục 🔁 trên. Nếu sau này `DLV` chạy delta lượt 2 thì ghi 1 dòng trỏ về đây |
