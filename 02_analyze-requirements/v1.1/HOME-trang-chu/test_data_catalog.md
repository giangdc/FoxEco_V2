# Test Data Catalog — v1.1 · Module HOME (DELTA)

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.
> Bảng v1.0 xem `v1.0/HOME-trang-chu/test_data_catalog.md` — KHÔNG lặp lại ở đây.

## Module HOME — Trang chủ (delta DOC-v1.1-01 §6/§8.17/§9)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Số tin NEED trong khu vực (section "Tin mới") | Fixture | 12 tin POSTED, gồm ≥1 MATCHED + ≥1 EXPIRED + ≥1 của chính người dùng (theo `AC-11.1.01`) | — | **đúng 5 tin hiển thị** (không phải 1) — 3 lớp loại trừ: MATCHED / EXPIRED / của chính mình | `DOC-v1.1-01` §6.2 AC-11.1.01 |
| Tổng tin hợp lệ (điều kiện hiện nút "Xem thêm") | Fixture | > 5 tin hợp lệ (đã loại MATCHED/EXPIRED/của chính mình) | ≤ 5 tin hợp lệ (nút KHÔNG hiện) | **biên đúng 5 (ẩn) vs 6 (hiện)** | `DOC-v1.1-01` §6.2 AC-11.1.01 |
| Tài khoản "sạch" cho empty state Trang chủ | Fixture | tài khoản mới, **0 tin trong khu vực · 0 đơn hoạt động · 0 đóng góp** | tài khoản đã có lịch sử (→ không kích được empty state) | ⚠️ **3 điều kiện phải đồng thời rỗng** để test đủ cả 3 empty state (`EMP-01/02/03`) trong 1 lượt | `DOC-v1.1-01` §8.17.1 |
| Môi trường load-test (NFR01) | — | 1.000 user đồng thời, mạng 4G | — | ngưỡng **< 2 giây (p95)** — cần công cụ load-test, ⛔ không test tay | `DOC-v1.1-01` §9 NFR01 |

## Ghi chú chung
- ⚠️ **Tiền đề khó nhất:** tài khoản "sạch" hoàn toàn (0 lịch sử) để kích đủ 3 empty state cùng lúc — nên seed riêng, không dùng account đã chạy các module khác.
- Field perf (NFR01) không phải test data theo nghĩa thông thường — ghi lại để `generate-tc`/`execute-maintain` biết cần defer cho automation/load-test, không viết TC manual assert số đo.
