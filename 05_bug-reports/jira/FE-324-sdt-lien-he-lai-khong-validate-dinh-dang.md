# FE-324 — [TC_10 - Trust & Safety] - SĐT liên hệ lại trong form báo cáo sự cố không validate định dạng

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-324 · **Module:** TS · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-324 |
| Module | TS |
| Status | To Do |
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
| Reject Number | — |
| Due date |  |
| Reporter | GiangDC2 |
| Assignee | LinhDCC |
| Created | 2026-09-22 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: `stag_anhptm17@fpt.com` — vai B (carrier), đơn `SEED-TS-01` đang `IN_TRANSIT`
- Trình duyệt / Thiết bị: `R58T20PLP8K` (Android thật), WebView Microsoft Forms trong Custom Tab
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- WebView "Báo cáo sự cố" đã bypass được màn đăng nhập Microsoft (xem `BUG-037`).

**Steps:**

1. Mở "Báo cáo sự cố". Chọn Loại yêu cầu "Góp ý / đề xuất", nhập Mô tả chi tiết hợp lệ.
2. Nhập "0912abc" (sai định dạng, có chữ cái xen số) vào ô "Số điện thoại liên hệ lại".
3. Bấm "Gửi" (đã đính đủ ảnh yêu cầu ở câu hỏi 4).
4. Quan sát thông báo lỗi.

**Expected result:**

- Nút "Gửi" ở trạng thái vô hiệu hoá / hoặc hiện cảnh báo định dạng sai, không cho gửi với SĐT không hợp lệ (theo `SC-TS-009`/`AC-31.1.02`).

**Actual result:**

- Không có bất kỳ cảnh báo nào về định dạng SĐT. Thông báo cuối cùng dưới nút "Gửi" chỉ còn liệt kê các câu hỏi bắt buộc CHƯA điền khác (nếu có) — câu hỏi SĐT không nằm trong danh sách dù giá trị là "0912abc". Nếu đính đủ ảnh, form sẽ gửi thành công với SĐT rác này, có thể khiến đội hỗ trợ không liên hệ lại được người báo cáo.

**Ghi chú:** Ô "Số điện thoại liên hệ lại" trên Microsoft Forms hiện được cấu hình là câu hỏi dạng văn bản tự do, chỉ validate "không rỗng", không có ràng buộc định dạng số điện thoại. Có thể khắc phục bằng cách đổi loại câu hỏi trên Microsoft Forms (nếu nền tảng hỗ trợ) hoặc chấp nhận rủi ro data quality này (QC/BA quyết định).
