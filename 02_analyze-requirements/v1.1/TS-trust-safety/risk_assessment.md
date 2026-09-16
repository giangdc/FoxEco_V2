---
id: v1.1/TS-trust-safety/risk
title: Risk Assessment — v1.1 · Module TS
type: risk-assessment
version: v1.1
sprint: 1
module: TS
counts:
  cl: 3
  risk: 7
  cl_open: 2
  cl_resolved: 1
status: ANALYZED
updated: 2026-09-16
---

# Risk Assessment — v1.1 · Module TS (DELTA)

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (5 dòng, không đổi) xem `v1.0/TS-trust-safety/risk_assessment.md` — KHÔNG lặp lại ở đây.

## Tổng quan
| Module | Risk Level | Rủi ro chính (delta v1.1) |
|--------|-----------|--------------|
| TS | **Medium** (không đổi so với v1.0) | `FR16` Báo cáo sự cố **đảo kết luận out-of-scope của `C-CNL-01` (v1.0)** — `RISK-TS-06`: `CNL`/`DLV` chưa rà lại nên người đọc từ 2 module đó vẫn thấy "out of scope". `RISK-TS-07`: đối chiếu MNV là quy trình Admin, không có bề mặt test qua UI |

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-TS-06 | TS / Báo sự cố | **(risk mới)** Tính năng mới đảo ngược kết luận `C-CNL-01` (v1.0: màn "Báo sự cố" out of scope) — nhưng chỉ trong phạm vi `TS` sở hữu; module `CNL` (nơi `C-CNL-01` là home canonical) và `DLV` (nơi `REQ-DLV-015` tham chiếu `C-CNL-01`) **chưa được rà lại** ở lượt delta này ⇒ nguy cơ người đọc sau trích `C-CNL-01` từ `CNL`/`DLV` tưởng vẫn "out of scope" | Medium | `DOC-v1.1-01` §8.16 vs `v1.0/CNL-huy-don/risk_assessment.md` (`C-CNL-01`) | `SC-TS-008..015` chỉ test bề mặt `TS` sở hữu (nút trigger + form + WebView) | Đã ghi cảnh báo chéo ở `requirement_traceability.md §2 REQ-TS-006`; **KHÔNG sửa file `CNL`/`DLV`** vì chưa rà lại chính thức lượt này | Open (ghi nhận, non-blocking) | REQ-TS-006 |
| RISK-TS-07 | TS / Đối chiếu MNV | **(risk mới)** BR16-03 "đối chiếu MNV ở khâu xử lý" là **quy trình phía Admin/vận hành** (ngoài app, ngoài WebView) — không có bề mặt để test qua UI end-user | Low | `DOC-v1.1-01` §8.16.1 BR16-03 | — (không test được qua app) | Ghi nhận là quy trình ngoài phạm vi automation/manual UI test; nêu rõ trong test report nếu có | Open (ghi nhận, non-blocking) | REQ-TS-006 |

## Clarifications (home của CL quote — layout v2)

> Lượt delta 2026-09-15 không mở CL mới. ⚠️ **Rà sâu 2026-09-16 phát hiện nhận định *"FR16 không có vùng mơ hồ"* là chưa đúng** — có 2 chỗ PRD tự mâu thuẫn / thiếu, mở 2 CL dưới. CL của v1.0 giữ nguyên — xem `v1.0/TS-trust-safety/risk_assessment.md`.

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-TS-02 | Nút "Báo cáo sự cố" hiện ở **trạng thái** nào; gửi form có **tự chuyển đơn sang INCIDENT** không | 🔴 **Open (mới 2026-09-16)** | 2026-09-16 | REQ-TS-006, SC-TS-015, SC-CNL-006, SC-CNL-015, SC-DLV-034 |
| C-TS-03 | Trường prefill: chỉ mã đơn (`BR16-02`) hay 9 trường (`AC-31.1.01`); mã đơn chỉ đọc hay sửa được (`BR16-03`); Custom Tabs có làm được nút "Thử lại"/"Quay lại đơn hàng" | 🔴 **Open (mới 2026-09-16)** | 2026-09-16 | REQ-TS-006, SC-TS-008, SC-TS-012, SC-TS-014 |

### C-TS-02 · Phạm vi hiển thị nút + hệ quả trạng thái *(OPEN — mới 2026-09-16)*

📍 `DOC-v1.1-01 §6.2 AC-31.1.01 · trang 29` · `§8.12.2 dòng INCIDENT · trang 45` · `§8.12.3 · trang 46` · `§5.2 S-14 · trang 12` ⟷ BA trả lời `C-CNL-03` 2026-09-16

> `AC-31.1.01`: "Given: Người dùng đang ở màn theo dõi đơn với vai trò bất kỳ."

> `§8.12.2`: "INCIDENT | Có sự cố | Có báo cáo sự cố sau khi đơn đã sang IN_TRANSIT | Bất kỳ bên nào | (chờ admin hỗ trợ, không tự về COMPLETED)"

> `§8.12.3`: "IN_TRANSIT | Theo dõi · Báo sự cố | … Báo sự cố | Theo dõi · Báo sự cố" · "DELIVERED | Theo dõi · Báo sự cố | (không còn thao tác) | "Xác nhận đã nhận hàng""

> S-14: "…đơn **có thể** chuyển INCIDENT để admin hỗ trợ dựa trên nhật ký + ảnh."

↳ **Ghi chú:** (a) `AC-31.1.01` nói nút có ở màn theo dõi đơn **mọi trạng thái** (vai bất kỳ), nhưng `§8.12.3` chỉ liệt kê "Báo sự cố" ở **IN_TRANSIT** (3 vai) và **DELIVERED** (chỉ Sender) — còn POSTED/MATCHED/COMPLETED/đơn đã đóng thì sao? (b) Từ điển nói INCIDENT = *"có báo cáo sự cố sau IN_TRANSIT"* ⇒ gửi form là **tự động** chuyển INCIDENT; nhưng S-14 viết *"có thể"*, và BA vừa nói *"dev hỗ trợ tay, không có tool"* — form Google **không gọi được API** của app ⇒ gần như chắc chắn **không tự chuyển**. **Hỏi:** ai/cái gì đưa đơn **vào** INCIDENT? Nếu không ai ⇒ trạng thái INCIDENT **không bao giờ xuất hiện** trên app ⇒ `SC-CNL-015`/`SC-DLV-034` **out of scope**. (c) Loại yêu cầu "Lỗi ứng dụng"/"Góp ý" (không phải sự cố đơn) có làm đơn đổi trạng thái không?

### C-TS-03 · Prefill form + khả thi kỹ thuật của WebView *(OPEN — mới 2026-09-16)*

📍 `DOC-v1.1-01 §8.16.1 BR16-01 / BR16-02 / BR16-03 / BR16-04 · trang 50` · `§8.16.2 dòng "Mã đơn hàng" · trang 51` · `§6.2 AC-31.1.01 / AC-31.2.01 · trang 29-30`

> `BR16-02`: "Ứng dụng tự đẩy mã đơn hàng sang google form"

> `AC-31.1.01`: "Mã đơn, vai trò, trạng thái đơn, MNV, họ tên, phòng ban, số điện thoại, phiên bản ứng dụng và hệ điều hành được điền sẵn."

> `BR16-03`: "Trường prefill là dạng câu trả lời ngắn, người dùng vẫn sửa được — đối chiếu MNV ở khâu xử lý."

> `§8.16.2`: "Mã đơn hàng | Có | Chỉ đọc · tự điền từ ứng dụng | Không sửa"

> `BR16-01`: "Mở WebView toàn màn hình (SFSafariViewController trên iOS · Chrome Custom Tabs trên Android) có thanh URL chỉ đọc và nút đóng."

↳ **Ghi chú:** 3 mâu thuẫn trong cùng `FR16`: (a) **Số trường prefill**: `BR16-02` chỉ nói **mã đơn**, `AC-31.1.01` liệt kê **9 trường** — demo 2026-09-15 (`TS_02`) cho thấy bao nhiêu? (b) **Mã đơn**: `§8.16.2` *"Chỉ đọc · Không sửa"* ⟷ `BR16-03` *"trường prefill… người dùng vẫn sửa được"* — Google Form **không khoá được** câu trả lời ngắn đã prefill ⇒ `SC-TS-014` assert chiều nào? (c) `BR16-01` dùng **Custom Tabs / SFSafariViewController** (trình duyệt hệ thống) — app **không vẽ được** màn lỗi + nút "Thử lại" bên trong (`AC-31.2.01`), và nút **"Quay lại đơn hàng"** nằm trên trang xác nhận của Google Form thì **không điều khiển được app**. **Hỏi BA/Dev:** đang build bằng WebView nhúng hay Custom Tabs? Nút "Thử lại" và "Quay lại đơn hàng" do **app** hay **Google Form** hiển thị? ⛔ Chưa chốt thì `SC-TS-012`/`SC-TS-014` ghi nhận.

## Vibe-check bổ sung 2026-09-15 — xác nhận luồng end-to-end trên demo

Đã chạy thử trực tiếp luồng "Báo cáo sự cố" trên demo `foxeco_demo/FoxEcoQC` (vai Sender), khác với `DLV`/`RISK-DLV-08` ở chỗ ô "Thêm ảnh" ở màn này **hoạt động thật** (mock có tăng đếm, không bị chặn như dropzone bên DLV):
> `00_input/v1.1/design/TS_03_baocaosucos_5anh_hople.png` — đính đủ 5 ảnh, nút "Thêm ảnh khác" tự **disabled** → khớp `SC-TS-011` (trần cứng 5, không cho thêm ảnh thứ 6).
> `00_input/v1.1/design/TS_04_baocaosucos_dudieukien_gui_enabled.png` — điền đủ Loại yêu cầu + Mô tả + SĐT → nút "Gửi" chuyển từ disabled sang enabled, đúng `SC-TS-009` chiều dương.
> `00_input/v1.1/design/TS_05_baocaosucos_daghinhanphanhoi.png` — sau khi Gửi: "Đã ghi nhận phản hồi" + đúng câu "Đội hỗ trợ FoxEco sẽ liên hệ lại số {SĐT} trong vòng 24 giờ làm việc" + nút "Quay lại đơn hàng" — khớp verbatim `SC-TS-008` Then.

↳ **Đây là module duy nhất trong lượt vibe-check này verify được TOÀN BỘ happy path + boundary end-to-end** (không bị chặn kỹ thuật như `DLV`). Nâng độ tin cậy cho `SC-TS-008/009/010/011` trước `generate-tc` — không cần dự phòng "app chưa cập nhật" như `RISK-DLV-08`/`RISK-DLV-11`.

## Khuyến nghị tổng thể
1. **Bề mặt `TS` (nút trigger + form + WebView) test đầy đủ được** — 8 SC phủ happy path, validation, boundary ảnh, mất mạng, vòng đời phiên, field prefill, đa vai trò. **Đã verify thật qua demo 2026-09-15** cho happy path + boundary ảnh + validation (xem mục Vibe-check trên) — mức tin cậy cao nhất trong các module rà đợt này.
2. **KHÔNG mở rộng phạm vi sang xử lý phía Admin** — "liên hệ lại trong 24 giờ làm việc" và "đối chiếu MNV" là quy trình ngoài app, chỉ ghi nhận cam kết hiển thị trên UI (`SC-TS-008`), không verify hành động thật của Admin.
3. **Khi delta `CNL`/`DLV` chạy ở lượt sau:** rà lại `C-CNL-01` và cross-ref `REQ-DLV-015` — hiện tại 2 file đó **chưa sửa**, chỉ có cảnh báo ở `RISK-TS-06` và ở `requirement_traceability.md` module này.
