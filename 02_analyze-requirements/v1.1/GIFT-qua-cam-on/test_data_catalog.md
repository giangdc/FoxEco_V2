# Test Data Catalog — v1.1 · Module GIFT

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> Chỉ liệt kê data **mới/đổi** của lượt delta. Data v1.0 xem `v1.0/GIFT-qua-cam-on/test_data_catalog.md`.

| Data | Loại data | Valid | Invalid | Boundary | Nguồn |
|------|-----------|-------|---------|----------|-------|
| Đơn ở `RETURNED` | Runtime | 1 đơn đi hết nhánh `FR09`: `IN_TRANSIT → RETURNING → RETURNED` (người gửi xác nhận đã nhận lại hàng) | Đơn `CANCELLED` (khác kết cục, không dùng thay thế được) | ⚠ **Có thể KHÔNG seed được** nếu STG chưa build `FR09` ⇒ verdict `BLOCKED`, ⛔ không PASS | `DOC-v1.1-01` §8.14 Pre-Conditions · §6.2 AC-24.2.01 |
| Chỉ số "Đơn đã giúp" | Runtime | Số **N** đọc được **trước** khi phát sinh đơn `RETURNED` — phải ghi lại | — | ⭐ Bộ số ví dụ của PRD: **7 đơn đã giúp / 5 quà** (`AC-26.1.01`) — dùng thẳng làm data mẫu | `DOC-v1.1-01` §6.2 AC-26.1.01 · §8.14.1 BR14-04 |
| 4 loại quà | Master | **bông hoa · ly cà phê · gấu bông · vương miện** — đúng tên, đúng số lượng | Bất kỳ loại thứ 5 nào | Đủ 4 / thiếu 1 / sai tên 1 loại | `DOC-v1.1-01` §8.14.1 BR14-01 |
| Text popup sau khi gửi quà | Master | `"Cảm ơn của bạn đã được gửi"` — verbatim, kèm **nút về trang chủ** | Chuỗi gần đúng (vd thiếu chữ "của bạn") | — | `DOC-v1.1-01` §8.14.1 BR14-02 · §6.2 AC-24.1.01 |
| Text empty state "Quà đã nhận" | Master | `"Chưa nhận được quà nào"` — verbatim, **KHÔNG có CTA** | Có bất kỳ nút CTA nào (sai `EMP-08`) | Thống kê đồng thời phải hiện **0 đơn đã giúp / 0 quà đã nhận** | `DOC-v1.1-01` §8.17.1 EMP-08 · §6.2 AC-26.2.01 |
| Tài khoản chưa nhận quà nào | Fixture | Tài khoản **mới tinh** (0 đơn, 0 quà) | Tài khoản đã dùng cho lô test khác | ⚠ Khó tái tạo khi môi trường đã có dữ liệu — cùng nhóm khó với `SC-HOME-025..027` | `DOC-v1.1-01` §8.17.1 EMP-08 |
| Quà nhiều loại để kiểm card đếm | Fixture | ≥ 5 quà gồm **ít nhất 2 loại khác nhau**, nhận ở các thời điểm khác nhau | Toàn bộ cùng 1 loại (không kiểm được "card theo từng loại") | Đúng 5 quà (khớp ví dụ `AC-26.1.01`); 1 loại có `count = 0` | `DOC-v1.1-01` §6.2 AC-26.1.01 |

## Ghi chú
- **Tiền đề nặng nhất của module là đơn `RETURNED`** — tái dùng đơn của lô `DLV` `SC-DLV-053..056` thay vì dựng riêng; nếu lô đó `BLOCKED` thì `SC-GIFT-013`/`014` cũng `BLOCKED`.
- **`SC-GIFT-014` bắt buộc có bước "ghi lại số trước"** trong Test Data của TC — không có bước đó thì TC không phát hiện được sai lệch 1 đơn.
- Đơn `COMPLETED` để tặng quà: tái dùng `SEED-GIFT-01..05` đã khai ở `03_test-cases/v1.0/CHANGELOG.md` (REVISE `GIFT` nhóm 2/N), ⛔ không seed mới.
