# FE-142 — [TC_05 - Trang chủ]: Hệ thống load số lượng đơn tối đa trong Đơn của tôi không khớp giữa các vai trò

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-142 · **Module:** HOME · **Sync:** 2026-09-22 (R1)

| Field | Value |
|-------|-------|
| Key | FE-142 |
| Module | HOME |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-08 |
| Verify Date | 2026-08-08 |
| Done At | 2026-08-08 |
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
| Due date | 2026-08-08 |
| Reporter | anhptm17 |
| Assignee | Tuanvm37 |
| Created | 2026-08-04 |
| Updated | 2026-08-08 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**Data**:

- Account Sender: [stag_dienlt2@fpt.com](mailto:stag_dienlt2@fpt.com)
- Account Carrier: [stag_vanmtt3@fpt.com](mailto:stag_chintl12@fpt.com)
- Account Receiver: [stag_chinlt12@fpt.com](mailto:stag_chinlt12@fpt.com)

**Step:**

1. Mở app FoxEco đăng nhập acc Sender
2. Quan sát card trong section "Đơn của tôi" ở màn hình trang chủ => Load tối đa 2 đơn
3. Mở app FoxEco đăng nhập acc Carrier
4. Quan sát card trong section "Đơn của tôi" ở màn hình trang chủ =>Load 4 đơn
5. Mở app FoxEco đăng nhập acc Receiver
6. Quan sát card trong section "Đơn của tôi" ở màn hình trang chủ => Load tối đa 2 đơn

**=> Bug: Hệ thống load số lượng đơn tối đa hiên thị trong Đơn của tôi không khớp giữa các vai trò**

**KQMM: Hệ thống load số lượng đơn tối đa 5 **

![attachment](d18ecfcb-2a35-4b7f-912f-3b9e26275901)

![attachment](8aef056c-3924-42a8-8204-7be53c3d8936)
