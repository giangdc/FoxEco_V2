# [TC_11 - Chặn lưu SĐT im lặng, không báo lỗi]:

- **Jira:** [FE-290](https://foxproject.atlassian.net/browse/FE-290)
- **Project:** FE (Fox Eco) · **Parent:** FE-1
- **Assignee:** Tuanvm37
- **Priority:** Medium · **Severity:** 2 · **Test Round:** 1 · **Platform:** App · **Effect:** Functionality · **Defect Type:** Logic · **Fix version:** V1.0
- **Status:** To Do
- **Module:** USR (Tài khoản & Hồ sơ) · **Màn:** Cập nhật thông tin → field "Số điện thoại mặc định"
- **Môi trường:** STG · Platform test: mobile (Appium MCP / UiAutomator2), Pixel 7 AVD 1080x2400
- **Test case liên quan:** TC-USR-021, TC-USR-022
- **Nguồn:** Vibe Test `VR-001-USR-2026-09-18` (`08_test-runs/vibe/VR-001-USR-2026-09-18/vibe-report.md`, ứng viên bug **B2**)
- **Evidence:** ✅ đã đính kèm trên Jira (verify 2026-09-18 15:04 qua `getJiraIssue` → 2 attachment thật) — `TC-USR-021__step5-FAIL-khong-hien-thong-bao-loi.png` (id `31486`) · `TC-USR-022__step5-FAIL-khong-hien-thong-bao-loi.png` (id `31487`). Upload qua REST fallback `curl` (`~/.config/jira/.env`), theo `log-bug references/push-jira.md` bước 5 — Atlassian MCP connector không có tool upload attachment.

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
- 0 thông báo lỗi, 0 banner xuất hiện
- Giá trị **không được lưu** (đã xác nhận: đóng màn mở lại → field rỗng)
- Đã kiểm 2 lượt độc lập để loại trừ false negative: lượt 1 bấm Lưu → check ngay → 0 thông báo; đóng/mở lại màn xác nhận không lưu; lượt 2 nhập lại + Lưu → vẫn 0 thông báo

## Ghi chú kỹ thuật cho dev (giả thuyết, chưa xác nhận)
Validator regex có thể chỉ chạy sau một bước sanitize; input chứa ký tự ` ` (khoảng trắng) hoặc `+` rơi ra khỏi cả 2 nhánh xử lý (không bị nhận là hợp lệ, cũng không kích hoạt hiển thị lỗi).

## Evidence
- `TC-USR-021__step5-FAIL-khong-hien-thong-bao-loi.png`
- `TC-USR-022__step5-FAIL-khong-hien-thong-bao-loi.png`
- Đường dẫn: `08_test-runs/vibe/VR-001-USR-2026-09-18/screenshots/`

## Ref
foxeco-v2 · Bug B2 · Report: `08_test-runs/vibe/VR-001-USR-2026-09-18/vibe-report.md`
