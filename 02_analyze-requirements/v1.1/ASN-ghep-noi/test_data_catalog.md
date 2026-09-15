# Test Data Catalog — v1.1 · Module ASN (DELTA)

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.
> Chỉ chứa data **mới/thay đổi** của lượt delta này. Bảng đầy đủ v1.0 (10 dòng, không đổi) xem `v1.0/ASN-ghep-noi/test_data_catalog.md` — KHÔNG lặp lại ở đây.

## Module ASN — Ghép nối (delta DOC-v1.1-01 §8.3/§8.4/§9)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Định nghĩa "khớp" (auto-match, BR04-01) | Fixture | đủ **3 điều kiện**: điểm lấy/giao trùng + khoảng ngày overlap + buổi di chuyển overlap | thiếu 1/3 điều kiện (→ không khớp) | **overlap = có phần chung, KHÔNG cần trùng tuyệt đối** — ranh giới "0 phần chung" vs "≥1 phần chung" | `DOC-v1.1-01` §8.4 BR04-01 |
| Chu kỳ quét auto-match (BR04-02) | Runtime | quét lại **≤ 60 giây** sau khi có tin mới | > 60s chưa quét (→ lỗi hiệu năng) | **60s là ngưỡng SLA**, không phải giá trị cố định — SC ghi nhận "trong ngưỡng", không assert giây chính xác | `DOC-v1.1-01` §8.4 BR04-02 |
| Trần "gộp thông báo khớp"/ngày (BR04-04) | — | **CHƯA CÓ giá trị** — "do admin cấu hình" | — | ⛔ **KHÔNG hardcode số** — khác mốc `3/5/6` đã chốt (trần gợi ý/carrier, `v1.0` không đổi) | `DOC-v1.1-01` §8.4 BR04-04 · `RISK-ASN-08` (Open) |
| Concurrency double-accept (NFR-06) | Runtime | **50 request đồng thời** → đúng 1 người ghép, **0%** trùng | > 0% trùng (→ FAIL bảo mật dữ liệu) | **50 request** là ngưỡng đo NFR, cần công cụ load/concurrency test — ⛔ không test tay được | `DOC-v1.1-01` §9 NFR-06 |
| Đồng bộ realtime 3 vai (NFR-08) | Runtime | 3 vai thấy cùng trạng thái trong **≤ 5 giây** | > 5 giây (→ FAIL NFR) | mốc **5 giây** đo trên 3 thiết bị thật | `DOC-v1.1-01` §9 NFR-08 |
| Request đọc tin OFFER qua API (NFR-11) | Fixture | request bởi **chủ tin** → cho phép | request bởi **không phải chủ tin** → chặn lỗi + ghi audit log | ranh giới **chủ tin vs không phải chủ tin** — cần công cụ gọi API trực tiếp (không thuần UI) | `DOC-v1.1-01` §9 NFR-11 |

## Ghi chú chung
- **Không đổi** so với v1.0: 3 mốc `3/5/6` (trần gợi ý/carrier) và ranh giới khớp nhị phân theo địa chỉ — bảng gốc `v1.0/ASN-ghep-noi/test_data_catalog.md` vẫn là nguồn cho các field đó.
- ⚠️ **`RISK-ASN-08`** (trần gộp thông báo) là field duy nhất của lượt này **chưa có giá trị test được** — hỏi admin/vận hành trước `generate-tc`, đừng tái dùng mốc `3/5/6` cũ (thuộc rule khác).
- 3 field NFR (`NFR-06`/`NFR-08`/`NFR-11`) đều cần **công cụ ngoài UI thuần** (concurrency tool / đa thiết bị đồng bộ / API client) — phù hợp giao automation/backend test hơn manual.
