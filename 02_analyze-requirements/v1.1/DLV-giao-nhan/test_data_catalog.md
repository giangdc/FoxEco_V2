# Test Data Catalog — v1.1 · Module DLV (DELTA)

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.
> Bảng v1.0 xem `v1.0/DLV-giao-nhan/test_data_catalog.md` — KHÔNG lặp lại ở đây.

## Module DLV — Giao nhận & Theo dõi đơn (delta DOC-v1.1-01 §8.6-§8.9/§8.12/§9/§8.18)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Ảnh lúc lấy hàng | Fixture | 0-5 ảnh (tuỳ chọn) | — | **0 (hợp lệ) · 5 (trần, hợp lệ) · 6 (chặn)** | `DOC-v1.1-01` §8.6.1 BR06-01 |
| Đối tượng nhận (giao hàng) | Fixture | 1 trong 4: `Người nhận` · `Người được uỷ quyền` · `Quầy lễ tân` · `Quầy bảo vệ` | chưa chọn (→ nút xác nhận disable) | — | `DOC-v1.1-01` §8.7.1 BR07-01 |
| Tên người nhận thay | Fixture | 2-60 ký tự, prefill nếu người gửi đã khai người uỷ quyền | rỗng khi đối tượng ≠ "Người nhận" (→ bắt buộc) · < 2 hoặc > 60 ký tự | **2 ký tự (hợp lệ) · 1 (chặn) · 60 (hợp lệ) · 61 (chặn)** | `DOC-v1.1-01` §8.7.3 |
| SĐT người nhận thay | Fixture | định dạng VN hợp lệ (khuyến nghị, không bắt buộc) | định dạng sai (không chặn submit, chỉ khuyến nghị) | — | `DOC-v1.1-01` §8.7.3 |
| Ảnh bằng chứng giao hàng | Fixture | 1-5 ảnh | 0 ảnh (→ nút xác nhận disable) | **1 (trần dưới, hợp lệ) · 5 (trần trên, hợp lệ) · 6 (chặn) · 0 (chặn)** | `DOC-v1.1-01` §8.7.1 BR07-02 |
| Tên người trực quầy | Fixture | 2-60 ký tự, cụ thể (không chấp nhận ghi chung chung) | rỗng · ghi chung chung kiểu "quầy lễ tân" (→ bị từ chối theo rule, tuy không có validate tự động rõ ràng — ghi nhận khi execute) | — | `DOC-v1.1-01` §8.7.1 BR07-03 · §8.8.1 BR08-04 |
| Chế độ cầm hàng về | Fixture | 1 trong 2: `retry` (giao lại sau) · `return` (trả về người gửi) | chưa chọn (→ bắt buộc) | — | `DOC-v1.1-01` §8.9.2 BR09-02 |
| Ngày hẹn (cầm hàng về) | Fixture | hôm nay .. +7 ngày | quá khứ · quá +7 ngày | **+7 ngày (hợp lệ) · +8 ngày (chặn)** | `DOC-v1.1-01` §8.9.2 BR09-04 |
| Giờ hẹn từ–đến | Fixture | giờ đến > giờ từ, khoảng ≥ 30 phút | giờ đến ≤ giờ từ · khoảng < 30 phút | **30 phút (hợp lệ) · 29 phút (chặn)** | `DOC-v1.1-01` §8.9.2 BR09-03 |
| Nơi hẹn | Fixture | 1-200 ký tự, nhãn đổi theo chế độ | > 200 ký tự | **200 ký tự (hợp lệ) · 201 (chặn)** | `DOC-v1.1-01` §8.9.2 |
| Trạng thái đơn (mở rộng) | Fixture | 12 trạng thái đầy đủ: `POSTED/MATCHED/IN_TRANSIT/DELIVERED/RESCHEDULED/RETURNING/RETURNED/COMPLETED/CANCELLED/EXPIRED/INCIDENT` | transition không nằm trong bảng `§8.12.2` (→ request bị từ chối) | ranh giới **đúng transition hợp lệ vs không hợp lệ** theo bảng `§8.12.2` | `DOC-v1.1-01` §8.12.2 |
| Upload ảnh (hiệu năng) | Runtime | 5 ảnh ≤5MB/ảnh, mạng 4G | — | ngưỡng **< 15 giây (p95)** | `DOC-v1.1-01` §9 NFR-03 |

## Ghi chú chung
- **Tiền đề khó nhất mới:** đưa đơn qua đủ các trạng thái hậu-FR09 (`RESCHEDULED`/`RETURNING`/`RETURNED`) đòi hỏi 1 đơn đi qua nhánh "không liên lạc được" + "cầm hàng về" — chuỗi thao tác dài hơn nhiều so với luồng happy-path 5 trạng thái gốc.
- Trần **5 ảnh** dùng nhất quán cho mọi điểm bằng chứng của module (lấy hàng/giao hàng/gửi quầy) theo `BR18-01` dùng chung — không lặp lại giải thích rule chung ở mỗi dòng.
- ⚠️ Field "Tên người trực quầy" không có validate tự động rõ ràng cho "ghi chung chung" — đây là rule diễn giải bằng con người (reviewer/QA), ghi nhận khi execute chứ không assert cứng bằng string matching.
