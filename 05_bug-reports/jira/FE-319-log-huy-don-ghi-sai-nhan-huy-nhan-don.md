# FE-319 — [TC_03 - Huỷ đơn] - Log người gửi huỷ đơn lại ghi nhãn Đã huỷ nhận đơn

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-319 · **Module:** CNL · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-319 |
| Module | CNL |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-09-23 |
| Verify Date | 2026-09-23 |
| Done At | 2026-09-23 |
| Fix Version | V1.0 |
| Priority | Low |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Interface |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date | 2026-09-23 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-22 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: A người gửi `stag_anhdc4@` — đơn `MATCHED` (đã ghép, tài khoản B `stag_anhptm17@` là bên nhận)
- Trình duyệt / Thiết bị: emulator-5554 (Android), UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Đơn `MATCHED`, block LỊCH SỬ đã có mốc "Ghép thành công" trước đó.

**Steps:**

1. Đăng nhập bằng A, mở màn Theo dõi đơn của đơn `MATCHED`, mở block LỊCH SỬ, ghi lại số dòng log hiện có (2 dòng).
2. Nhấn "Huỷ đơn", nhập lý do "Huy vi trung lich", nhấn "Xác nhận".
3. Không rời màn Theo dõi đơn, mở lại block LỊCH SỬ, check số dòng log mới và nội dung dòng đó.

**Expected result:**

- Block LỊCH SỬ có thêm đúng 1 dòng; dòng mới ghi đủ 3 thành phần: vai "Người gửi", lý do "Huy vi trung lich" và thời điểm huỷ _(TC-CNL-009; PRD_ `DOC-v1.1-01` `BR11-02` + `AC-25.1.01`).

**Actual result:**

- Có thêm đúng 1 dòng, đủ lý do và thời điểm (`23:34`) — nhưng nhãn hành động ghi là **"Đã huỷ nhận đơn"** (`Hôm nay · 23:34 · Đặng Châu Anh · Lý do: Huy vi trung lich`). Đây là hành động **A (người gửi) huỷ đơn**, nhưng nhãn "Đã huỷ nhận đơn" lại đúng là nhãn dùng cho khi **người vận chuyển huỷ nhận đơn** (xem `TC-CNL-010`) ⇒ người đọc log dễ hiểu nhầm bên huỷ là người vận chuyển.
