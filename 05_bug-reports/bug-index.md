# Bug Index — Router

> Chỉ trả lời "cần biết X thì đọc ở đâu". KHÔNG dựng bảng trạng thái/tường thuật ở đây —
> xem `SKILL.md §bug-index` của skill `log-bug`.

## Nguồn chuẩn

> 🔄 **Sync gần nhất: 2026-09-23 (lượt 2, chiều) — `/sync-jira-bugs` (PULL, không cờ lọc).**
> JQL: `project = FE AND issuetype = Bug ORDER BY key ASC` ⇒ **phạm vi = TOÀN BỘ project FE, 121 bug** (`FE-93` … `FE-342`).
> Index này **phản ánh đủ project**, không bị cắt phạm vi ⇒ lượt đối chiếu sau kết luận `only-local` là đáng tin.
> Trục: Atlassian MCP connector (`searchJiraIssuesUsingJql`, markdown).

| Cần gì | Đọc ở đâu |
|---|---|
| Bug đã push Jira (mirror, trạng thái mới nhất) | `05_bug-reports/jira/<KEY>-*.md` (glob đệ quy) — **121 file**, ghi đè toàn bộ mỗi lượt sync, ⛔ KHÔNG sửa tay |
| Bug local chưa push Jira | `05_bug-reports/draft/BUG-NNN-*.md` (glob đệ quy) — hiện **0** file (11 file trước đó — `BUG-030/031/034/036/037/038/039/041/042/043/044` — đã push Jira 2026-09-22, xem `jira/FE-317..327-*.md` + bảng `Bug → ID local → RUN` bên dưới) |
| Tổng quan status/aging | `/log-bug --status` (sinh on-demand, không lưu ở đây) |

> 🗑️ `BUG-040` (nút "Gửi" trên form Báo cáo sự cố không vô hiệu hoá khi thiếu trường bắt buộc —
> `TC-TS-010/011/012`) **đã xoá 2026-09-22** — QC quyết định đây **không phải bug**: cơ chế inline
> error sau khi bấm Gửi của Microsoft Forms vẫn chặn đúng submit khi thiếu trường bắt buộc (đúng ý
> đồ nghiệp vụ), chỉ khác cách thể hiện UI so với giả định "nút disable" ban đầu — không phải lỗi
> đáng log. Expected của `TC-TS-010/011/012` đã sửa lại theo đúng hành vi thật
> (`03_test-cases/v1.1/fragments/TC-TS-v1.1.md` + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`),
> verdict FAIL → **✅ PASS**. Số `BUG-040` bỏ trống, không tái sử dụng.
>
> 🗑️ `BUG-033` (đơn `IN_TRANSIT` thiếu nút "Yêu cầu hoàn hàng" — `TC-CNL-017`/`018`/`019`) **đã xoá 2026-09-22** — QC xác nhận **TC viết sai giả định**: PRD (`AC-25.2.01` + `BR11-04`) chỉ đảm bảo ở mức trạng thái ("hoàn hàng vẫn là 1 trong 2 lối thoát hợp lệ"), không hề đặt tên nút "Yêu cầu hoàn hàng"; luồng hoàn hàng thật (`FR09` §8.9) do **Người vận chuyển** khởi tạo — bấm "Đã đến địa điểm giao hàng" → màn "Xử lý đơn hàng" → chọn "Cầm hàng về", không phải nút riêng trên màn Theo dõi đơn của Sender/Receiver. Expected `TC-CNL-017/018/019` đã sửa lại theo đúng luồng (`03_test-cases/v1.1/fragments/TC-CNL-v1.1.md` + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`), verdict FAIL → **✅ PASS** (evidence đúng slot `__verify` chụp bù ở follow-up 2026-09-22 — ảnh gốc `__step2-FAIL` không đủ cho gate, giữ nguyên không xoá). Số `BUG-033` bỏ trống, không tái sử dụng.

> 🗑️ `BUG-035` (dòng log huỷ ghi tên người thay vì vai trò — `TC-CNL-009`/`010`) **đã xoá 2026-09-22** — QC chấp nhận hành vi hiện tại của app (ghi **tên người thực hiện**, nhất quán với mọi dòng LỊCH SỬ khác trong toàn app, không riêng dòng huỷ) là **đúng, không phải bug**. Expected `TC-CNL-009`/`010` đã sửa lại theo app (fragment + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`). `TC-CNL-010` hết vướng mắc nội dung khác, verdict FAIL → **✅ PASS** (evidence đúng slot `__verify` chụp bù ở follow-up 2026-09-22 — ảnh gốc `__step8-FAIL` không đủ cho gate, giữ nguyên không xoá). `TC-CNL-009` **vẫn FAIL** — lý do khác, độc lập: nhãn hành động sai "Đã huỷ nhận đơn" thay vì nhãn đúng của luồng huỷ đơn (xem `BUG-034`, còn giữ). Số `BUG-035` bỏ trống, không tái sử dụng.

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
| BUG-030 | [FE-317](https://foxproject.atlassian.net/browse/FE-317) | VR-017-ACT-2026-09-21 (`TC-ACT-008`) — lý do "Hết hạn" thừa vế so với chuỗi chính thức; assignee Tuanvm37 |
| BUG-031 | [FE-318](https://foxproject.atlassian.net/browse/FE-318) | VR-017-ACT-2026-09-21 (`TC-ACT-012`) — empty state tab "Đang diễn ra" thiếu dòng giải thích (`BR17-01`); assignee Tuanvm37 |
| BUG-034 | [FE-319](https://foxproject.atlassian.net/browse/FE-319) | VR-018-CNL-2026-09-21 (`TC-CNL-009`) — log người gửi huỷ đơn ghi nhầm nhãn "Đã huỷ nhận đơn"; assignee Tuanvm37 |
| BUG-036 | [FE-320](https://foxproject.atlassian.net/browse/FE-320) | VR-018-CNL-2026-09-21 (`TC-CNL-004`) — thiếu dòng lỗi dưới ô lý do huỷ khi nhập 4 ký tự; assignee Tuanvm37 |
| BUG-037 | [FE-321](https://foxproject.atlassian.net/browse/FE-321) | VR-019-TS-2026-09-22 (`TC-TS-008..024`, 13 TC) — đề xuất bỏ bắt buộc đăng nhập Microsoft trên form Báo cáo sự cố; pushed dạng Bug/Defect Type=`Other` (board không có issue type "Suggestion" hay Defect Type "Suggest"); assignee Tuanvm37 |
| BUG-038 | [FE-322](https://foxproject.atlassian.net/browse/FE-322) | VR-019-TS-2026-09-22 (`TC-TS-016`) — mất mạng khi mở Báo cáo sự cố hiện trang lỗi Chromium kỹ thuật, không có nút "Thử lại"; assignee Tuanvm37 |
| BUG-039 | [FE-323](https://foxproject.atlassian.net/browse/FE-323) | VR-019-TS-2026-09-22 follow-up (`TC-TS-009`) — màn xác nhận sau khi gửi là mặc định Microsoft Forms, không đúng đặc tả; assignee Tuanvm37 |
| BUG-041 | [FE-324](https://foxproject.atlassian.net/browse/FE-324) | VR-019-TS-2026-09-22 follow-up (`TC-TS-012`) — SĐT liên hệ lại không validate định dạng; assignee Tuanvm37 |
| BUG-042 | [FE-325](https://foxproject.atlassian.net/browse/FE-325) | VR-019-TS-2026-09-22 follow-up (`TC-TS-013`) — trường ảnh đính kèm bắt buộc, ngược giả định `SC-TS-010`; assignee Tuanvm37 |
| BUG-043 | [FE-326](https://foxproject.atlassian.net/browse/FE-326) | VR-019-TS-2026-09-22 follow-up (`TC-TS-021`) — ô "Mã đơn hàng" sửa được, sai đặc tả chỉ đọc; assignee Tuanvm37 |
| BUG-044 | [FE-327](https://foxproject.atlassian.net/browse/FE-327) | VR-018-CNL-2026-09-21 evidence hồi cứu (`TC-CNL-018`) — nút xác nhận đến nơi giao chưa đổi tên theo v1.1; assignee Tuanvm37 |

> 🗑️ `BUG-019` (ảnh ~5MB im lặng) **đã xoá 2026-09-21** — VR-013 đo lại: đúng 5 MiB được nhận, >5 MiB có thông báo (nằm dưới viewport, phải cuộn) ⇒ không phải bug. Số `BUG-019` bỏ trống, không tái sử dụng.

> 🗑️ `BUG-020` (API 400 khi đăng NEED), `BUG-022` (người nhận mất cụm liên hệ ở `Đang giao`), `BUG-023` (form sửa cho xoá ảnh tin đã đăng), `BUG-024` (lightbox không đóng khi chạm nền) **đã xoá 2026-09-21** — QC kiểm lại: app đúng, không phải bug (`BUG-020` không tái hiện ở VR-013). TC liên quan đã sửa theo app / trả về bản gốc. Các số này bỏ trống, không tái sử dụng.

> 🗑️ `BUG-029` (`TC-FEED-015` — thiếu khung placeholder + "0km" khi văn phòng thiếu toạ độ) **đã xoá 2026-09-21** — QC chấp nhận hành vi hiện tại của app (chỉ hiện dòng cảnh báo text, không khung, không "0km") là đúng, không phải bug. `TC-FEED-015` Expected Result đã sửa lại theo app (`03_test-cases/v1.1/fragments/TC-FEED-v1.1.md` + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`), verdict đổi FAIL → PASS. Số `BUG-029` bỏ trống, không tái sử dụng.

> 🗑️ `BUG-032` (`TC-ACT-017` — tab `Hoạt động` rỗng không cuộn được) **đã xoá 2026-09-21** — QC xác nhận app đúng; Expected `TC-ACT-017` đã sửa theo app (fragment + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`), verdict FAIL → PASS. Số `BUG-032` bỏ trống, không tái sử dụng.
