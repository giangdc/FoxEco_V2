# FE-167 — [TC_01 - Hoạt động] Chức năng tặng quà tại màn hình Hoạt động (Đơn của tôi) không đúng 

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-167 · **Module:** ACT · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-167 |
| Module | ACT |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-09 |
| Verify Date | 2026-08-09 |
| Done At | 2026-08-09 |
| Fix Version | V1.0 |
| Priority | High |
| Severity | Major (weight 10) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 4 |
| Due date | 2026-08-06 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-08-05 |
| Updated | 2026-08-09 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**Điều kiện test:** 

- account: [stag_tampnh2@fpt.com](mailto:stag_tampnh2@fpt.com) → người gởi
- data: Có đơn đã hoàn thành

**Bước thực hiện**

1. Mở app Foxeco →vào màn hình Hoạt động(Đơn của tôi)/Tab Đã hoàn thành
2. Thao tác tặng quà

**Bug: (tham khảo thêm video)**

- Đơn đã tặng quà rồi nhưng mặc định đang hiển thị là Chạm để tặng quà → vẫn cho thao tác tặng quà thành công 
- Sau khi tặng quà 1 đơn → thao tác tặng tiếp thì báo lỗi idempotency-key đã dùng cho gift khác 
- Sau khi tặng xong Tắt app mở lại → <Đã tặng quà> cập nhật thành <Chạm để tặng quà>

\*\*\*\*\*\* Cần check lại do file demo ko rõ ràng + brd cũng không mô tả luồng tặng quà chỗ này

![attachment](260be93a-9f02-4cc2-93e5-e642a8a7886b)
