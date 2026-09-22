# FE-327 — [TC_04 - Giao nhận] - Nút xác nhận đến nơi giao chưa đổi tên theo đặc tả v1.1

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-327 · **Module:** DLV · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-327 |
| Module | DLV |
| Status | To Do |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Interface |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date |  |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-22 |
| Updated | 2026-09-22 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: `stag_anhptm17@` — vai Người vận chuyển (Carrier), đơn `IN_TRANSIT` (`SEED-DLV-01`)
- Trình duyệt / Thiết bị: thiết bị Android thật (vibe-test VR-018)
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

**Pre-condition:**

- Đơn ở checkpoint 2 (`IN_TRANSIT`/Đang giao) của `SEED-DLV-01`.

**Steps:**

1. Đăng nhập bằng tài khoản B (Người vận chuyển), mở màn Theo dõi đơn của đơn `IN_TRANSIT`.
2. Rà toàn bộ nút hành động chính trên màn.

**Expected result:**

- Nút hành động chính mở luồng xác nhận giao hàng có tên "Đã đến địa điểm giao hàng" — tên chính thức đã chốt cho v1.1 (`TC-CNL-018`, `TC-DLV-043..047`), thay cho tên cũ "Đã giao cho người nhận" của v1.0.
- Khi click Qua thăng màn hinh xác nhận đã giao luôn, không cần xác nhận ở bước này 

**Actual result:**

- Nút vẫn hiển thị nguyên tên cũ "Đã giao cho người nhận" — chưa đổi theo tên mới của v1.1.
- Click btn Đã giao cho người nhận → hiên thị popup Xác nhận (bạn xác nhận đã giao hàng tận tay cho ngưởi nhần) >click xác nhận >  qua màn hình Xác nhận đã giao 

![attachment](0214755d-c398-4595-8f53-15e9992b98f7)
