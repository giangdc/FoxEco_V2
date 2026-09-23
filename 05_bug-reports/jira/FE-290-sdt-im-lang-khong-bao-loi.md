# FE-290 — [TC_11 - Tài khoản & Hồ sơ]:  Chặn lưu SĐT im lặng, không báo lỗi

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-290 · **Module:** USR · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-290 |
| Module | USR |
| Status | In Progress |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 1 |
| Due date | 2026-09-23 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-18 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**Module:** USR (Tài khoản & Hồ sơ) · **Màn:** Cập nhật thông tin → field "Số điện thoại mặc định"
**Môi trường:** STG · Platform: mobile (Appium MCP / UiAutomator2), Pixel 7 AVD 1080x2400
**Test case liên quan:** TC-USR-021, TC-USR-022
**Nguồn:** Vibe Test VR-001-USR-2026-09-18 (`08_test-runs/vibe/VR-001-USR-2026-09-18/vibe-report.md`)

## Mô tả

Khi nhập số điện thoại mặc định sai định dạng (có khoảng trắng hoặc tiền tố +84) rồi bấm "Lưu thay đổi", app **chặn lưu đúng** nhưng **không hiển thị bất kỳ thông báo lỗi nào** — người dùng bấm Lưu và không nhận được phản hồi gì, không biết vì sao thao tác thất bại.

## Steps to reproduce

1. Vào màn "Cập nhật thông tin" (Cá nhân → Cập nhật thông tin)
2. Nhập `0912 345 678` (có khoảng trắng) vào field "Số điện thoại mặc định" — field vẫn nhận input
3. Nhấn nút "Lưu thay đổi"

(Case 2 tương tự với input `+84912345678`)

## Expected

Hiển thị thông báo lỗi đỏ "Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)" ngay dưới field.

## Actual

- Hiển thị thông toast “Không lưu được thông tin vui lòng thử lại“

## Ghi chú kỹ thuật cho dev (giả thuyết, chưa xác nhận)

Validator regex có thể chỉ chạy sau một bước sanitize; input chứa ký tự ` ` (khoảng trắng) hoặc `+` rơi ra khỏi cả 2 nhánh xử lý (không bị nhận là hợp lệ, cũng không kích hoạt hiển thị lỗi).

## Evidence

- `TC-USR-021__step5-FAIL-khong-hien-thong-bao-loi.png`
- `TC-USR-022__step5-FAIL-khong-hien-thong-bao-loi.png`
- Đường dẫn: `08_test-runs/vibe/VR-001-USR-2026-09-18/screenshots/`

## Ref

foxeco-v2 · Bug B2 · Report: `08_test-runs/vibe/VR-001-USR-2026-09-18/vibe-report.md`
