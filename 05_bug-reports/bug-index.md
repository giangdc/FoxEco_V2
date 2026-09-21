# Bug Index — Router

> Chỉ trả lời "cần biết X thì đọc ở đâu". KHÔNG dựng bảng trạng thái/tường thuật ở đây —
> xem `SKILL.md §bug-index` của skill `log-bug`.

## Nguồn chuẩn

| Cần gì | Đọc ở đâu |
|---|---|
| Bug đã push Jira (mirror, trạng thái mới nhất) | `05_bug-reports/jira/<KEY>-*.md` (glob đệ quy) |
| Bug local chưa push Jira | `05_bug-reports/draft/BUG-NNN-*.md` (glob đệ quy) — hiện **0** file (`BUG-029` rút lại 2026-09-21, xem ghi chú cuối trang) |
| Tổng quan status/aging | `/log-bug --status` (sinh on-demand, không lưu ở đây) |

## Bug → ID local → RUN

> Chỉ để tra `BUG-NNN` cũ khi file đã chuyển sang `jira/` (Jira không giữ thông tin này).

| BUG-NNN (local) | Jira Key | Nguồn (RUN/vibe-test) |
|---|---|---|
| BUG-001 | [FE-291](https://foxproject.atlassian.net/browse/FE-291) | VR-001-USR-2026-09-18 (ứng viên bug B3) |
| BUG-002 | [FE-292](https://foxproject.atlassian.net/browse/FE-292) | VR-001-USR-2026-09-18 (ứng viên bug B4) |
| BUG-003 | [FE-293](https://foxproject.atlassian.net/browse/FE-293) | VR-001-USR-2026-09-18 (ứng viên bug B6) |
| BUG-004 | [FE-294](https://foxproject.atlassian.net/browse/FE-294) | VR-001-USR-2026-09-18 (ứng viên bug B7) |
| BUG-005 | [FE-295](https://foxproject.atlassian.net/browse/FE-295) | VR-001-USR-2026-09-18 (ứng viên bug B8) |
| BUG-006 | [FE-298](https://foxproject.atlassian.net/browse/FE-298) | VR-001-USR-2026-09-18 (ứng viên bug B5, `TC-USR-039`) |
| BUG-007 | [FE-297](https://foxproject.atlassian.net/browse/FE-297) | recheck 2026-09-18 (MNV bị cắt trên màn "Cập nhật thông tin", `TC-USR-024`) — pushed `severity: Low`/`defect_type: Interface` sau khi đổi từ `Suggest` do board bắt buộc Defect Type lúc tạo issue |
| BUG-008 | [FE-300](https://foxproject.atlassian.net/browse/FE-300) | VR-003-USR-2026-09-18 (ứng viên bug B9, `TC-USR-040`/`TC-USR-043`) |
| BUG-009 | [FE-301](https://foxproject.atlassian.net/browse/FE-301) | VR-002-ORD-2026-09-18 (ứng viên bug B1, 6 TC FAIL) |
| BUG-010 | [FE-302](https://foxproject.atlassian.net/browse/FE-302) | VR-002-ORD-2026-09-18 (`TC-ORD-053`) |
| BUG-011 | [FE-303](https://foxproject.atlassian.net/browse/FE-303) | VR-002-ORD-2026-09-18 (`TC-ORD-059`) |
| BUG-012 | [FE-304](https://foxproject.atlassian.net/browse/FE-304) | VR-002-ORD-2026-09-18 (`TC-ORD-058`) |
| BUG-013 | [FE-305](https://foxproject.atlassian.net/browse/FE-305) | VR-002 + VR-004 ORD (gộp `BUG-013` prefill người gửi + `BUG-014` autofill người nhận; `TC-ORD-017`/`043`/`019`/`074`) |
| BUG-016 | [FE-307](https://foxproject.atlassian.net/browse/FE-307) | VR-004 ORD (`TC-ORD-050`) — dạng `Suggest` (severity 0); Jira có Defect Type `Requirement` do board bắt buộc |
| BUG-021 | [FE-308](https://foxproject.atlassian.net/browse/FE-308) | VR-011-GIFT-2026-09-19 (`TC-GIFT-003`) — popup tặng quà sai chuỗi `BR14-02`; assignee Tuanvm37 |
| BUG-025 | [FE-309](https://foxproject.atlassian.net/browse/FE-309) | VR-014-HOME-2026-09-21 (`TC-HOME-025`) |
| BUG-026 | [FE-310](https://foxproject.atlassian.net/browse/FE-310) | VR-014-HOME-2026-09-21 (`TC-HOME-027`) |
| BUG-027 | [FE-311](https://foxproject.atlassian.net/browse/FE-311) | VR-015-ASN-2026-09-21 (`TC-ASN-006` lần chạy 1 — toast đòi chấp nhận điều khoản khi ghép; assignee Tuanvm37) |
| BUG-028 | [FE-312](https://foxproject.atlassian.net/browse/FE-312) | `repro/RP-FEED-chu-tin-bang-tin-khong-theo-doi-don-2026-09-21` (chủ tin mở tin từ Bảng tin ra Chi tiết tin, không có Chỉnh sửa/Huỷ đơn; QC tự chỉnh sang Suggest) |
| *(không có — xem ghi chú)* | [FE-290](https://foxproject.atlassian.net/browse/FE-290) | VR-001-USR-2026-09-18 (ứng viên bug B2) — push thủ công **trước khi** `/log-bug` được gọi lần đầu trong dự án này, nên không có draft `BUG-NNN` gốc |

> 🗑️ `BUG-019` (ảnh ~5MB im lặng) **đã xoá 2026-09-21** — VR-013 đo lại: đúng 5 MiB được nhận, >5 MiB có thông báo (nằm dưới viewport, phải cuộn) ⇒ không phải bug. Số `BUG-019` bỏ trống, không tái sử dụng.

> 🗑️ `BUG-020` (API 400 khi đăng NEED), `BUG-022` (người nhận mất cụm liên hệ ở `Đang giao`), `BUG-023` (form sửa cho xoá ảnh tin đã đăng), `BUG-024` (lightbox không đóng khi chạm nền) **đã xoá 2026-09-21** — QC kiểm lại: app đúng, không phải bug (`BUG-020` không tái hiện ở VR-013). TC liên quan đã sửa theo app / trả về bản gốc. Các số này bỏ trống, không tái sử dụng.

> 🗑️ `BUG-029` (`TC-FEED-015` — thiếu khung placeholder + "0km" khi văn phòng thiếu toạ độ) **đã xoá 2026-09-21** — QC chấp nhận hành vi hiện tại của app (chỉ hiện dòng cảnh báo text, không khung, không "0km") là đúng, không phải bug. `TC-FEED-015` Expected Result đã sửa lại theo app (`03_test-cases/v1.1/fragments/TC-FEED-v1.1.md` + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`), verdict đổi FAIL → PASS. Số `BUG-029` bỏ trống, không tái sử dụng.
