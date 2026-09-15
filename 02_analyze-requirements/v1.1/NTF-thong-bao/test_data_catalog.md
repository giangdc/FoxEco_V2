# Test Data Catalog — v1.1 · Module NTF (Delta)

> Tạo bởi: analyze-requirements (**stage: analyze**, DELTA).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.
> Chỉ liệt kê field **MỚI hoặc THAY ĐỔI** so với v1.0. Field CARRIED (kênh gửi, nhóm thời gian, chấm đỏ, cơ chế đánh dấu đã đọc...) xem `v1.0/NTF-thong-bao/test_data_catalog.md`.

## Module NTF — Thông báo (DOC-v1.1-01 §8.13.1)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Sự kiện kích hoạt | Fixture | **15 sự kiện chính thức** `NTF-01..15` (thay vì 8 có SC + 12 ứng viên chưa chốt của v1.0) | sự kiện không thuộc `NTF-01..15` | Danh mục **đã chốt** — không còn "ứng viên chưa chọn" | `DOC-v1.1-01 §8.13.1` |
| Nội dung thông báo `NTF-06` | Master | text đã chốt: *"Đơn đã hoàn tất — cảm ơn bạn!"* | *"Đơn đã hoàn thành — đánh giá ngay"* (bản cũ, KHÔNG dùng nữa) | — | `DOC-v1.1-01 §8.13.1` dòng NTF-06 |
| Nội dung thông báo `NTF-10..15` | Master | text mẫu theo bảng `§8.13.1`, có biến `{tên}` / `{ngày · giờ}` / `{nơi hẹn}` / `{vai trò}` cần thay đúng giá trị runtime | biến không được điền (hiện literal `{...}`) · chứa số điện thoại | mỗi loại phải đúng **người nhận** theo cột "Người nhận" (1 hoặc 2 người) | `DOC-v1.1-01 §8.13.1` |
| Tiền đề dựng dữ liệu `NTF-10..15` | Fixture | đơn đi qua nhánh phụ FR08 (không liên lạc được người nhận) hoặc FR09 (cầm hàng về) bên `DLV` | đơn đi thẳng nhánh chính (không phát sinh 6 sự kiện này) | cần **ít nhất 1 lượt qua mỗi nhánh phụ** (uỷ quyền / quầy lễ tân / quầy bảo vệ / hẹn giao lại / trả hàng) để quan sát đủ 6 loại | `DOC-v1.1-01 §8.13.1` + `DLV-giao-nhan` delta v1.1 |

## Ghi chú chung
- Field CARRIED không đổi: xem `v1.0/NTF-thong-bao/test_data_catalog.md` (kênh gửi in-app/push, nhóm thời gian, chấm đỏ, cơ chế đánh dấu đã đọc — vẫn Open, cơ chế lazy-load).
- ⚠️ **Danh mục `Loại thông báo ngoài BRD`/`Loại thông báo đã loại` của v1.0 (dòng "#10 Sắp đến khung giờ hẹn giao") KHÔNG còn cần theo dõi** — PRD v1.1 không đưa vào danh mục chính thức, coi như đã đóng, không phải sự kiện của v1.1.
- Tiền đề nặng nhất của delta này: phải dựng đủ đơn đi qua **cả 2 nhánh phụ FR08 và FR09** mới quan sát được hết `NTF-10..15` — nên chạy chung lô với vibe-test `DLV`, không seed riêng cho NTF.
