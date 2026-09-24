# FE-326 — [TC_10 - Trust & Safety] - Ô mã đơn hàng trong form báo cáo sự cố sửa được, sai đặc tả chỉ đọc

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-326 · **Module:** TS · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-326 |
| Module | TS |
| Status | Done |
| Resolution | Won't Fix |
| Resolved | 2026-09-24 |
| Verify Date | 2026-09-24 |
| Done At | 2026-09-24 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Medium (weight 5) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Requirement |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Reason for Wontfix | Dev không fix do Phụ thuộc thông tin các bên liên quan ngoài ISC |
| Due date | 2026-09-24 |
| Reporter | GiangDC2 |
| Assignee | LinhDCC |
| Created | 2026-09-22 |
| Updated | 2026-09-24 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

* URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
* Account/Role: `stag_anhptm17@fpt.com` — vai B (carrier), đơn `SEED-TS-01` đang `IN_TRANSIT`
* Trình duyệt / Thiết bị: `R58T20PLP8K` (Android thật), WebView Microsoft Forms trong Custom Tab
* Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

* WebView "Báo cáo sự cố" đã bypass được màn đăng nhập Microsoft (xem `BUG-037`). Ô "Mã đơn hàng" đang hiển thị giá trị prefill `01a0c6fd-4730-74d6-8e99-d3e416b5bb56`.

**Steps:**

1. Mở "Báo cáo sự cố" từ đơn `SEED-TS-01`.
2. Chạm vào ô "Mã đơn hàng".
3. Gõ thử ký tự "X".
4. Quan sát bàn phím và giá trị trong ô.

**Expected result:**

* Ô "Mã đơn hàng" hiển thị dạng nhãn tĩnh chứ không phải textbox, bàn phím không bật lên, và giá trị giữ nguyên không có ký tự "X" (theo `§8.16.2` — "Chỉ đọc · Không sửa").

**Actual result:**

* Bàn phím Android bật lên (chứng minh đây là ô nhập liệu thật) và ký tự "X" được chèn vào giữa chuỗi → giá trị đổi thành `01a0c6fd-4730-74d6-8Xe99-d3e416b5bb56`. Ô hoàn toàn sửa được.

**Ghi chú:** Clarification `C-TS-03(b)` (Resolved 2026-09-17) từng kết luận ô này "nhãn tĩnh, không sửa được", dựa trên quan sát demo trước khi từng đăng nhập qua được màn Microsoft. Bằng chứng thật trên chính form cho thấy kết luận đó sai — khớp lại với `BR16-03` gốc ("cho phép sửa, dạng câu trả lời ngắn") mà `C-TS-03(b)` từng bác bỏ. Cần `/analyze-requirements --update` mở lại `C-TS-03(b)` trước khi quyết định đây là bug cần Dev khoá field, hay `§8.16.2` mới là bản đặc tả sai. **Rủi ro nếu không sửa: người dùng có thể vô tình/cố ý đổi mã đơn hàng trước khi gửi, làm sai lệch dữ liệu báo cáo mà đội hỗ trợ nhận được (báo cáo bị gắn nhầm đơn hàng).**
