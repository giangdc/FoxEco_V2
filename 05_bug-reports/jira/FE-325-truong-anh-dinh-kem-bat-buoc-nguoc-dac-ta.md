# FE-325 — [TC_10 - Trust & Safety] - Trường ảnh đính kèm trong báo cáo sự cố bắt buộc, ngược đặc tả

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-325 · **Module:** TS · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-325 |
| Module | TS |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-09-24 |
| Verify Date | 2026-09-24 |
| Done At | 2026-09-24 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Medium (weight 5) |
| Test Round | R1 |
| Effect | Functionality |
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
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

* WebView "Báo cáo sự cố" đã bypass được màn đăng nhập Microsoft (xem `BUG-037`).

**Steps:**

1. Mở "Báo cáo sự cố". Chọn Loại yêu cầu "Sự cố đơn hàng", nhập Mô tả chi tiết, nhập SĐT hợp lệ.
2. KHÔNG đính ảnh nào ở câu hỏi "Hình ảnh đính kèm".
3. Bấm "Gửi".

**Expected result:**

* Gửi thành công, hiển thị màn ghi nhận — 0 ảnh là biên dưới hợp lệ (theo `SC-TS-010`, `test_data_catalog.md §TS` liệt "Hình ảnh đính kèm" là trường không bắt buộc). → tài liệu \_ demo ko mô tả bắt buộc ảnh 
* ![](blob:https://media.staging.atl-paas.net/?type=file&localId=0825b66782ec&id=aaa77d0f-883f-4a7d-916b-1f6f4082bb6b&&collection=&height=63&occurrenceKey=null&width=1667&__contextId=null&__displayType=null&__external=false&__fileMimeType=null&__fileName=null&__fileSize=null&__mediaTraceId=null&url=null)

    



**Actual result:**

* Form KHÔNG gửi được. Thông báo "Cần hoàn thành 1 câu hỏi trước khi gửi: Câu hỏi 4." (= Hình ảnh đính kèm). Câu hỏi 4 trên Microsoft Forms có dấu `*` (bắt buộc thật), ngược hẳn giả định "biên dưới hợp lệ" đang dùng làm cơ sở thiết kế `SC-TS-010`.

**Ghi chú:** Đây là sai lệch giữa giả định phân tích (`test_data_catalog.md §TS` ghi ảnh không bắt buộc) và cấu hình thật của Microsoft Forms (ảnh bắt buộc). Cần `/analyze-requirements --update` sửa lại giả định trong `test_data_catalog.md`/`test_scenario_map.md`, đồng thời hỏi BA/Dev: có chủ ý bắt buộc ảnh (đổi nghiệp vụ) hay cấu hình form đang sai so với thiết kế ban đầu.
