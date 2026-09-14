# Test Environments

> Nguồn quyết định: `02_analyze-requirements/Project_rule.md §Test Data Rules` (canonical) — sửa 2026-09-14 theo `health-check` G-06b③.

## STG
| Field    | Value |
|----------|-------|
| URL      | **N/A** — FoxEco là SDK nhúng trong host app mobile FoxPro (`FoxPro_Stag`, package `vn.fpt.ftel.sop.stg`), không có URL/domain riêng |
| API URL  | **N/A** — chưa có đặc tả API (`§Test Data Rules`: HTTP status/error.code/response envelope đều TBD ở tầng tài liệu, không phải TBD ở tầng môi trường) |
| Database | **N/A** — không truy cập trực tiếp DB; dữ liệu quan sát qua UI app thật trên STG |
| Bề mặt test | UI trong host app `FoxPro_Stag` (package `vn.fpt.ftel.sop.stg`), môi trường **STG** |
| Thiết bị | Android thật, SDK cài trong host app (`§Execution Rules`) — trước khi chạy: `adb` set `screen_off_timeout` ≥ 30 phút |

## Tài khoản kiểm thử (Test Accounts)
> Không lưu mật khẩu thực ở đây. Giá trị đăng nhập thật để ở `~/.foxeco-v2/credentials.env` (`chmod 600`, biến `FOXECO_STG_USER`/`FOXECO_STG_PASS`) — **chưa tồn tại tại thời điểm ghi**, cần tạo trước khi chạy `vibe-test`.

| Vai trò | Username | Ghi chú |
|---------|----------|---------|
| SENDER   |  | Vai gửi hàng (đăng tin NEED/OFFER) |
| CARRIER  |  | Vai vận chuyển — cần ghép đơn để test luồng giao nhận |
| RECEIVER |  | Vai nhận hàng — pre-logged-in dùng ở vibe-test v1.0: tên hiển thị "Chung Hoàng Liêm" |

> Email nội bộ dùng test auto-fill người nhận: `stag_anhdc4@fpt.com` (`§Test Data Rules`). Đơn ở trạng thái "Đã ghép" trở đi cần bên thứ 2 nhận đơn — nhờ dev/QA seed dữ liệu STG (`KP-01 §10.12`).
