---
id: v1.0/ASN-ghep-noi/changelog
title: Changelog — Module ASN
type: changelog
version: v1.0
sprint: 1
module:
  code: ASN
  dir: ASN-ghep-noi
  name: Ghép nối
doc_source:
  - id: DOC-v1.0-01
    section: "§A5 (BR-CON-01/02, BR-INT-05) · §D2 (L209) · §D3 (ASN-01/02/03, MTCH-01) · §D4 (BR-MTCH-01) · §D5 (L293) · §D7 (OPR-01..09) · §D1b (US-D07/D08/D12/D13)"
  - id: DOC-v1.0-02
    section: "§4.2 · §7 (dòng 3, 9) · §1.4"
  - id: DOC-v1.0-06
    section: "KP-01 §4 (KB-ASN-01..05) · KP-02 §2/§4/§5"
id_range:
  req: REQ-ASN-001..012
  sc: "SC-ASN-001..018 (NEW)"
  cl: "C-NTF-02 (home canonical) · C-ASN-03 · C-ASN-01/02 (tham chiếu — home ở FEED)"
  risk: RISK-ASN-01..07
status: ANALYZED
updated: 2026-09-07
---

# Changelog — Module ASN (`ASN`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-07 | INIT | Phân tích lần đầu §A5/§D3/§D7 — 12 REQ (`001..012`), 18 SC, 3 CL, 7 RISK. Điểm nghiệp vụ đáng chú ý nhất: **BRD mâu thuẫn nội bộ về cơ chế ghép** (`BR-CON-01` ghép ngay ⟷ `ASN-02`/`§D2`/`§D5` chủ tin duyệt) — chốt theo *ghép ngay* vì khớp bề mặt thật `DOC-v1.0-02` §4.2 | `DOC-v1.0-01` §A5/§D3/§D5/§D7/§D1b · `DOC-v1.0-02` §4.2 · `DOC-v1.0-06` KP-01 §4 | Dựng đủ 5 deliverable + `CHANGELOG.md` |
| 2026-09-07 | REFACTOR | **Thu hẹp phạm vi module.** Đợt v1.0 cũ để Bảng tin + Chi tiết tin trong `ASN`; lượt này 2 màn đó tách sang `FEED`, `ASN` chỉ còn **rule ghép nối** (engine + state-transition) | Quyết định QC GiangDC2 2026-09-07 | Dải `SC-ASN-*` đánh lại từ 001; ⛔ ID cũ (`SC-ASN-005`, `SC-ASN-014` = bề mặt Bảng tin) **KHÔNG** map 1-1 sang dải mới |
| 2026-09-07 | INIT | **Nhận home canonical của `C-NTF-02`** (định nghĩa "khớp tuyến" + tham số vận hành) — rule thuộc engine ghép nối, không thuộc màn Thông báo | Trước đây CL này gắn nhãn `NTF` nhưng nội dung là rule matching | `NTF-thong-bao/risk_assessment.md` chỉ tham chiếu; `SC-ASN-011` chịu giới hạn từ CL này |
| 2026-09-07 | INIT | Ghi nhận **`OPR-06` đã bị BA đảo kết luận**: trần thông báo tính **riêng theo từng tin OFFER**, KHÔNG cộng dồn theo ngày (`KB-ASN-03`, 2026-07-29) | BA trả lời; scenario cũ `SC-NTF-006` đã DEPRECATED ở đợt cũ | `SC-ASN-014` dùng rule mới với 3 mốc BA chốt **3/5/6**; ⛔ không tái tạo scenario theo-ngày |
| 2026-09-07 | REFACTOR | Đổi tên thư mục module `ASN/` → `ASN-ghep-noi/` — tên gợi nghĩa để người mới đọc thư mục là biết chức năng. Cập nhật kèm: frontmatter `id:` của 5 deliverable + `module.dir` ở file này + mọi cross-ref `ASN/<file>.md` | Yêu cầu QC GiangDC2 2026-09-07 (mã 2–4 chữ không nói lên chức năng) · `Project_rule §Module Codes` nay có cột `Dir` riêng | ⛔ **Mã module `ASN` và toàn bộ ID (`REQ-ASN-*` · `SC-ASN-*`) KHÔNG đổi** — chỉ đường dẫn thư mục đổi. TC chưa sinh nên không TC nào bị ảnh hưởng |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Cơ chế ghép = GHÉP NGAY khi Carrier xác nhận** (theo `BR-CON-01` + `DOC-v1.0-02` §4.2), ⛔ KHÔNG có bước chủ tin duyệt | `ASN-02` L248 · `§D2` L209 · `§D5` L293 nói ngược lại nhưng bề mặt thật không có bước duyệt | Mọi SC luồng ghép sai tiền đề: TC chờ Sender bấm "Chấp nhận" ⇒ treo mãi ở bước không tồn tại |
| 2 | ⛔ **`SC-ASN-005` phải dùng tài khoản thứ tư** không thuộc cặp ghép và không phải Người nhận | Đây là vế duy nhất kiểm được *"chỉ cho đúng 2 người trong cặp"* của `OPR-07` | Thiếu tài khoản thứ tư ⇒ rule bảo mật liên hệ **không được kiểm chứng** mà vẫn tưởng đã phủ |
| 3 | ⛔ **Trần thông báo khớp = 5 / MỖI TIN OFFER**, ⛔ KHÔNG phải 5/ngày cộng dồn | BA đảo kết luận `OPR-06` ngày 2026-07-29 (`KB-ASN-03`); `SC-NTF-006` đợt cũ đã DEPRECATED | Tái tạo scenario theo-ngày = làm sống lại một kết luận đã bị BA bác |
| 4 | ⛔ **Dùng đúng 3 mốc biên `3 / 5 / 6`** cho trần gợi ý và trần thông báo | `KB-ASN-03` ghi rõ *"giá trị test 3/5/6 tin là **giá trị chốt**, không phải mock"* | Tự nghĩ mốc khác ⇒ kết quả không đối chiếu được với kỳ vọng BA đã chốt |
| 5 | ⛔ **KHÔNG test biên độ lệch khung giờ** khi khớp tuyến — chỉ dùng 2 khung **tách rời hoàn toàn** cho nhánh negative | `C-NTF-02` Partially Resolved: định nghĩa *"khung giờ phù hợp"* chưa chốt | TC biên FAIL/PASS tuỳ cách hiểu, không có oracle để phán quyết ⇒ tranh luận vô ích với dev |
| 6 | ⛔ **KHÔNG dùng bán kính GPS / khoảng cách địa lý** làm tiêu chí khớp | `KB-ASN-04`: khớp bằng **địa chỉ đã chọn** | Thiết kế TC theo khoảng cách ⇒ không tài nào thiết lập được tiền đề, TC bị BLOCKED hàng loạt |
| 7 | ⚠️ **`SC-ASN-006` (double-accept): nếu chỉ chạy nhánh tuần tự thì GHI RÕ** — ⛔ không khai coverage cho nhánh cạnh tranh thật | Nhánh cạnh tranh cần 2 thiết bị bấm trong cùng cửa sổ ms (`RISK-ASN-02`) | Khai coverage cho nhánh chưa test = báo cáo sai; đúng loại lỗi mà `vibe-test` gate evidence sinh ra để chặn |
| 8 | ⚠️ **`SC-ASN-008` (realtime) phải dùng 3 phiên/thiết bị khác nhau**, ⛔ không đổi vai trên cùng 1 phiên | Bằng chứng realtime chỉ đến từ demo *"1 đơn / 3 khung cùng bộ nhớ"* (`DOC-v1.0-02` §1.4) | Đổi vai trên 1 phiên luôn "PASS" vì đọc cùng 1 state ⇒ không kiểm chứng được gì |
| 9 | ⚠️ **Phân biệt 2 nhãn nút:** "Tôi mang giúp được" (luồng NEED thủ công) ⟷ "Nhận giao" (luồng OFFER khớp tuyến) | `US-D07` L176 vs `US-D13` L187 | Dùng lẫn ⇒ TC/automation trỏ sai luồng, và báo cáo coverage gán sai nhánh nghiệp vụ |
| 10 | ⚠️ **`OPR-04` chỉ kiểm được nửa** — tiêu chí *"độ gần tuyến"* thành nhị phân sau `KB-ASN-04` ⇒ chỉ assert thứ tự theo **thời gian đăng** | `OPR-04` L340 vs `KB-ASN-04` | Assert thứ tự theo "độ gần" ⇒ không có cách nào thiết lập 2 mức độ gần khác nhau, TC vô nghĩa |

### 🔁 Kết luận bị đảo (khi có)

> ⛔ Kết luận **"trần thông báo khớp giới hạn theo NGÀY cho mỗi carrier"** (`OPR-06` §D7 L342, cơ sở của `SC-NTF-006` đợt v1.0 cũ) **HẾT HIỆU LỰC — đừng trích lại**; hiện hành là **"trần 5 thông báo cho MỖI TIN OFFER, không cộng dồn theo ngày"** (`DOC-v1.0-06` KP-01 §4 `KB-ASN-03`, BA xác nhận 2026-07-29).
> ⛔ Kết luận **"chủ tin phải chấp nhận 1 người quan tâm mới ghép"** (`ASN-02` §D3 L248 · sơ đồ `§D2` L209 · `§D5` L293) **HẾT HIỆU LỰC ở v1.0 — đừng trích lại**; hiện hành là **"ghép ngay khi Carrier xác nhận, không cần chủ tin duyệt"** (`BR-CON-01` §A5 L77 + bề mặt thật `DOC-v1.0-02` §4.2).

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 `C-NTF-02` — 3 tham số auto-match chưa chốt (định nghĩa "khung giờ phù hợp" · chu kỳ quét · ngưỡng gộp thông báo) | Partially Resolved từ 2026-07-27; BRD tự ghi *"Nháp — chờ BA bổ sung"* | Hỏi BA; tới khi đó `SC-ASN-011` chỉ dùng khung giờ tách rời hoàn toàn |
| 2 | 🔴 **Nhánh cạnh tranh thật của `SC-ASN-006`** chưa có cách thực thi bằng manual | `RISK-ASN-02` Open | Cần 2 thiết bị + phối hợp thời điểm; hoặc đề xuất test ở tầng API/backend với dev |
| 3 | 🔴 Seed **4 tài khoản + 2–3 phiên đồng thời + 6 tin khớp cùng tuyến + 1 tin quá hạn** | `RISK-ASN-07` Open | Nhờ dev/QA seed STG; ưu tiên nhóm P1 nếu thiếu thiết bị |
| 4 | 🟡 `C-ASN-03` — wizard không tạo listing độc lập (nghi giới hạn demo) | Open, cần backend thật | Chạy `SC-ASN-018` với 2 tin liên tiếp trên STG; nếu app cũng ghi đè đơn → escalate |
| 5 | 🟡 `OPR-04` còn hiệu lực ở dạng nào sau khi "độ gần tuyến" thành nhị phân | `RISK-ASN-06` Pending | Nêu với BA cùng lượt `C-NTF-02` |
| 6 | 🟡 Đồng bộ realtime chưa có bằng chứng ngoài bản demo 1-đơn | `RISK-ASN-05` Open | Chạy `SC-ASN-008` với 3 thiết bị thật; nếu cần refresh thủ công → finding cho BA |
