---
id: v1.1/ASN-ghep-noi/changelog
title: Changelog — Module ASN
type: changelog
version: v1.1
sprint: 1
module:
  code: ASN
  dir: ASN-ghep-noi
  name: Ghép nối
doc_source:
  - id: DOC-v1.1-01
    section: "§8.3 FR03 (Ghép nối & lộ liên hệ) · §8.4 FR04 (Khớp tuyến OFFER↔NEED) · §9 NFR-04/06/08/11"
id_range:
  req: "REQ-ASN-013 (NEW) + REQ-ASN-005, REQ-ASN-007, REQ-ASN-008, REQ-ASN-009 (MODIFIED, giữ ID sprint 1)"
  sc: "SC-ASN-019 (NEW) + SC-ASN-006, SC-ASN-008, SC-ASN-011, SC-ASN-014, SC-ASN-015 (MODIFIED, giữ ID sprint 1)"
  cl: "(không mở CL mới — C-ASN-03/C-NTF-02 giữ nguyên trạng thái v1.0)"
  risk: "RISK-ASN-08 (NEW) + RISK-ASN-02, RISK-ASN-04, RISK-ASN-05, RISK-ASN-06 (Status/Solution cập nhật, giữ ID sprint 1)"
status: ANALYZED
updated: 2026-09-15
---

# Changelog — Module ASN (`ASN`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-15 | UPDATE | **DELTA v1.1** — PRD chính thức (`DOC-v1.1-01`) chốt định nghĩa khớp tuyến (`BR04-01/02`), chu kỳ quét (`NFR-04` ≤60s), 3 ngưỡng NFR mới (concurrency `NFR-06`, realtime `NFR-08`, security API `NFR-11`), và **đảo kết luận** trần thông báo khớp (`BR04-04`: theo ngày/người dùng thay vì theo tin OFFER). +1 REQ mới (`REQ-ASN-013`), +1 SC mới (`SC-ASN-019`), 4 REQ + 5 SC MODIFIED. Resolve `RISK-ASN-04`/`RISK-ASN-06`; mở `RISK-ASN-08` (nợ giá trị cấu hình) | `DOC-v1.1-01` §8.3/§8.4/§9 | `RISK-ASN-04`/`RISK-ASN-06` đóng; `SC-ASN-014` đảo kết luận v1.0; `SC-ASN-006`/`SC-ASN-008` có ngưỡng NFR cho automation |
| 2026-09-15 | UPDATE | Bổ sung UI reference (`00_input/v1.1/design/ASN_01..03`, demo `foxeco_demo/FoxEcoQC`) — xác nhận cấu trúc màn "Bảng tin" (`SC-ASN-015`), "Chi tiết tin" + nút "Tôi mang giúp được" (`SC-ASN-006` nhánh a), và form "Tôi nhận giao hàng" đúng 2 field PRD mới mô tả (Khoảng thời gian + Buổi, đủ 4 lựa chọn buổi kể cả "Giờ nào cũng được") khớp `BR04-01/02`. **Không phát sinh CL mới, không resolve CL nào** — `C-ASN-03`/`C-NTF-02` (home ASN) không đổi vì ảnh chỉ xác nhận cấu trúc UI (§Custom Rules §10.1), không chạm tới câu hỏi nghiệp vụ của 2 CL đó (đa đơn song song / tham số vận hành khớp tuyến) | Vibe-check thủ công qua Playwright, theo yêu cầu QC GiangDC2 2026-09-15 | Không ảnh hưởng generate-tc — chỉ là bằng chứng UI-match bổ sung |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **Sprint/module khác KHÔNG sửa** — thư mục dùng lại qua nhiều sprint, phân biệt bắt buộc bằng `id_range` + đường dẫn version | Nguyên tắc chung dự án | Mất truy vết; ID trùng nhưng nội dung lệch |
| 2 | ⛔ **`SC-ASN-014` KHÔNG dùng lại mốc `3/5/6`** của v1.0 (mốc đó thuộc `SC-ASN-013` — trần gợi ý 5 tin/carrier, rule độc lập không đổi) | 2 rule khác nhau dễ nhầm vì cùng nhóm "trần" | Viết sai boundary — test nhầm rule, bug thật bị bỏ sót |
| 3 | ⚠️ **`NFR-06`/`NFR-08`/`NFR-11` cần công cụ ngoài UI thuần** (concurrency tool · đa thiết bị đồng bộ · API client) | PRD chỉ định phương pháp đo cụ thể (Concurrency test / Integration test đa thiết bị / Security test) | Test tay không đo được ngưỡng → PASS giả trên case không đại diện |

### 🔁 Kết luận bị đảo

⛔ Kết luận **"trần thông báo khớp tính RIÊNG theo từng tin OFFER"** (bản v1.0, `KB-ASN-03`, BA 2026-07-29) **HẾT HIỆU LỰC kể từ v1.1 — đừng trích lại**; hiện hành là **trần tính theo NGÀY, gộp cho MỘT NGƯỜI DÙNG** (`DOC-v1.1-01 §8.4 BR04-04`), giá trị số "do admin cấu hình" — chưa có trong tài liệu.

⛔ Kết luận **"tiêu chí độ gần tuyến vô hiệu vì nhị phân, chỉ còn thời gian đăng"** (`RISK-ASN-06` bản v1.0) **HẾT HIỆU LỰC** — hiện hành là **độ gần tuyến vẫn là tầng ưu tiên số 1** (dù nhị phân), thời gian đăng chỉ là tầng 2 khi 2 tin cùng trùng tuyến (`DOC-v1.1-01 §8.3 BR03-06`).

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 `RISK-ASN-08` — trần "gộp thông báo khớp/ngày" (`BR04-04`) không có giá trị số cứng trong PRD | Open — chặn viết TC boundary chính xác cho `SC-ASN-014` | Hỏi admin/vận hành giá trị cấu hình thật **trước `generate-tc`**; không hardcode số |
| 2 | 🟡 `SC-ASN-019` cần công cụ gọi API trực tiếp (Postman/tương đương) | Chưa có kế hoạch môi trường | Lên kế hoạch trước khi `vibe-test`/`execute-maintain` chạy nhánh security |
