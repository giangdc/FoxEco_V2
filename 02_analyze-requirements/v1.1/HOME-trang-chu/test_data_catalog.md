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
| Số đơn đã giúp (hero) — theo vai *(2026-09-17)* | Fixture | tài khoản đã làm **Người vận chuyển** N đơn Hoàn thành ⇒ hero = N | tài khoản chỉ làm Người gửi/Người nhận (≥1 đơn Hoàn thành) ⇒ hero **= 0** | đơn **Đã trả người gửi** không tính (`BR14-04`) | BA trả lời `C-HOME-06(a)` 2026-09-17 · `DOC-v1.1-01` BR14-04 |
| "[x] đơn · [y] người" cộng đồng *(2026-09-17)* | Runtime | x = đơn Hoàn thành **toàn hệ thống**, cập nhật **realtime** — ghi x trước, hoàn thành 1 đơn ⇒ x+1 | — | ⛔ không assert y ("người tham gia" chờ vòng 2) | BA trả lời `C-HOME-06(b)(c)` 2026-09-17 |
| Môi trường load-test (NFR01) | — | 1.000 user đồng thời, mạng 4G | — | ngưỡng **< 2 giây (p95)** — cần công cụ load-test, ⛔ không test tay | `DOC-v1.1-01` §9 NFR01 |

## Ghi chú chung
- ⚠️ **Tiền đề khó nhất:** tài khoản "sạch" hoàn toàn (0 lịch sử) để kích đủ 3 empty state cùng lúc — nên seed riêng, không dùng account đã chạy các module khác.
- Field perf (NFR01) không phải test data theo nghĩa thông thường — ghi lại để `generate-tc`/`execute-maintain` biết cần defer cho automation/load-test, không viết TC manual assert số đo.
- ⚠️ **2026-09-17 — BA nói tin load toàn quốc (`C-HOME-04` vòng 2):** empty state "Tin mới" (`SC-HOME-025`) chỉ kích được khi **cả hệ thống STG** không có tin NEED hợp lệ ⇒ gần như không dựng được trên STG dùng chung. Cần môi trường riêng/khung giờ dọn dữ liệu, hoặc ghi BLOCKED có lý do.
