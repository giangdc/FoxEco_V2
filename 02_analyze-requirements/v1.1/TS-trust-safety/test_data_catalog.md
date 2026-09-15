# Test Data Catalog — v1.1 · Module TS (DELTA)

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.
> v1.0 module TS không có test data catalog riêng (module log-only, không có form nhập) — đây là bảng **đầu tiên** của module, phát sinh hoàn toàn từ `FR16` mới.

## Module TS — Báo cáo sự cố & hỗ trợ (DOC-v1.1-01 §8.16)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Loại yêu cầu | Fixture | 1 trong 3: `Sự cố đơn hàng` · `Lỗi ứng dụng` · `Góp ý / đề xuất` | chưa chọn (→ nút Gửi disable) | — | `DOC-v1.1-01` §8.16.2 |
| Mô tả chi tiết | Fixture | văn bản bất kỳ, không rỗng | rỗng (→ nút Gửi disable) | — (không có giới hạn ký tự công bố) | `DOC-v1.1-01` §8.16.2 |
| Số điện thoại liên hệ lại | Fixture | định dạng Việt Nam hợp lệ, gợi ý sẵn từ hồ sơ (sửa được) | định dạng sai (→ nút Gửi disable) | — | `DOC-v1.1-01` §8.16.2 |
| Hình ảnh đính kèm | Fixture | 0–5 ảnh, xoá được từng ảnh | > 5 ảnh (→ chặn thêm) | **0 (hợp lệ, tuỳ chọn) · 5 (trần, hợp lệ) · 6 (chặn)** | `DOC-v1.1-01` §8.16.2 |
| Mã đơn hàng (prefill) | Runtime | tự điền từ đơn đang xem, **chỉ đọc** | — | — | `DOC-v1.1-01` §8.16.2 |
| Vai trò / trạng thái đơn / MNV / họ tên / phòng ban / SĐT / phiên bản app / hệ điều hành (prefill) | Runtime + Master | tự điền từ phiên đăng nhập + hồ sơ, **sửa được** (trừ mã đơn) | — | — | `DOC-v1.1-01` §6.2 AC-31.1.01 · §8.16.1 BR16-03 |
| Trạng thái kết nối mạng | Runtime | có mạng → WebView tải bình thường | mất mạng → lỗi + nút "Thử lại" | — | `DOC-v1.1-01` §6.2 AC-31.2.01 |

## Ghi chú chung
- **`Loại data`:** `Fixture` = tester tự nhập vào form · `Runtime` = hệ thống tự điền từ session/hồ sơ đăng nhập (prefill) · `Master` = dữ liệu hồ sơ có sẵn (MNV, phòng ban) dùng làm nguồn prefill.
- ⚠️ **Tiền đề khó nhất:** mô phỏng mất mạng đúng lúc mở WebView (cần bật/tắt mạng thiết bị thật hoặc network throttle) cho `SC-TS-012`.
- Trần **5 ảnh** ở đây **độc lập** với trần ảnh bằng chứng giao hàng (`DLV`/`FR07`/`FR18`) — 2 form khác nhau, không dùng chung field hay state, dù cùng số 5.
