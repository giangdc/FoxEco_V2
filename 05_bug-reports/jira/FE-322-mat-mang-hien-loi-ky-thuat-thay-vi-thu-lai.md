# FE-322 — [TC_10 - Trust & Safety] - Mất mạng khi mở Báo cáo sự cố hiện trang lỗi kỹ thuật, không có nút Thử lại

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-322 · **Module:** TS · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-322 |
| Module | TS |
| Status | Done |
| Resolution | Won't Fix |
| Resolved | 2026-09-24 |
| Verify Date | 2026-09-24 |
| Done At | 2026-09-24 |
| Fix Version | V1.0 |
| Priority | Low |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Usability |
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
* Account/Role: `stag_taipm@fpt.com` — vai B (carrier), đơn `SEED-TS-01` đang `Đang giao`
* Trình duyệt / Thiết bị: `R58T20PLP8K` (Android thật) — tắt WiFi qua `adb shell svc wifi disable` để mô phỏng mất mạng
* Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

* Đơn đang ở trạng thái `Đang giao` (IN_TRANSIT). Thiết bị đã tắt hoàn toàn WiFi (không có mạng nào khác).

**Steps:**

1. Từ màn "Theo dõi đơn", ngắt hoàn toàn kết nối mạng của thiết bị.
2. Nhấn "Báo cáo sự cố".
3. Đợi khoảng 3 giây, quan sát nội dung hiển thị.

**Expected result:**

* Theo `DOC-v1.1-01` §6.2 `AC-31.2.01`: màn hiển thị thông báo lỗi thân thiện (không tải được) kèm nút "Thử lại" do chính app vẽ.
* ![](blob:https://media.staging.atl-paas.net/?type=file&localId=8550e63e3df2&id=84e69c6b-59f6-49a9-af7d-542280bbb403&&collection=&height=51&occurrenceKey=null&width=1708&__contextId=null&__displayType=null&__external=false&__fileMimeType=null&__fileName=null&__fileSize=null&__mediaTraceId=null&url=null)

    



**Actual result:**

* Màn hiển thị nguyên văn trang lỗi kỹ thuật của WebView/Chromium: "Error loading page / Domain: undefined / Error Code: -2 / Description: net::ERR_INTERNET_DISCONNECTED" — toàn bộ bằng tiếng Anh, lộ chi tiết kỹ thuật (error code, domain) không phù hợp cho người dùng cuối. Không có nút "Thử lại" nào trên màn (đã `find` bằng `textContains("Thử lại")` → NOT FOUND).
* Hệ quả: `TC-TS-017` (thử lại sau khi có mạng) cũng không thực hiện được vì không có nút để bấm.
