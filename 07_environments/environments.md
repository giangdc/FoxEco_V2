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

> 🔐 **Secret** (OTP dùng chung · mật khẩu) → **`~/.foxeco-v2/credentials.env`** (`chmod 600`, ngoài repo, đã `.gitignore`).
> 📋 **Registry đầy đủ** (email · MNV · vai · chiến lược luân phiên · dữ liệu đã tạo) → **`04_test-data/valid/USR-accounts.md`** ⭐ — sửa ở đó, ⛔ đừng nhân bản danh sách ra đây.

🔑 **OTP staging CỐ ĐỊNH, dùng chung mọi account** ⇒ **AI tự đăng nhập được** (✅ kiểm chứng 2026-09-19). **Login chỉ cần email + OTP — KHÔNG có mật khẩu.**
🔴 Ghi chép cũ *"OTP nhập tay, AI không lấy được"* (VR-001/003/004) **ĐÃ LỖI THỜI**.

| Vai | Email | Ghi chú |
|---|---|---|
| **A** — chủ tin / quan sát | `stag_giangdc2@fpt.com` | đăng NEED, chấm verdict |
| **B** — carrier | `stag_anhdc4@fpt.com` | ✅ xác nhận = *Đặng Châu Anh*, MNV `00286248` |
| **C** — người nhận | `stag_taipm@fpt.com` | xác nhận đã nhận hàng |
| **D** — người ngoài cặp | `stag_huyennhk@fpt.com` | kiểm không lộ SĐT (`TC-ASN-005`) |
| **dự phòng / sạch** | `stag_anhptm17@fpt.com` | ⚠️ giữ *chưa lưu hồ sơ* — cần cho `TC-USR-040/043`, `TC-HOME-027/028/029` |

**Đăng xuất:** FoxPro → `Cá nhân` → cuộn cuối → `Đăng xuất` (⛔ không có trong FoxEco).
**Vào lại FoxEco:** FoxPro → `Chức năng` → `scroll_to_element` icon `FoxEco`.

> Email nội bộ test auto-fill người nhận: `stag_anhdc4@fpt.com`. Email **đã nghỉ việc**: `stag_binhnt23@fpt.com` (MNV `00026682`). Email **không tồn tại**: `stag_khongtontai@fpt.com`.
> 🔴 **Không có tài khoản HRIS trống** ⇒ `TC-USR-041/044` vẫn BLOCKED (`DOC-v1.1-05`).
