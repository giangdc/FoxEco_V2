# FE-293 — [TC_11 - Tài khoản & Hồ sơ] - Avatar chữ viết tắt sai quy tắc dẫn xuất

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-293 · **Module:** USR · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-293 |
| Module | USR |
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
| Defect Type | Logic |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | — |
| Due date | 2026-09-23 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-18 |
| Updated | 2026-09-24 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

* URL: N/A (mobile app, không phải web)
* Account/Role: FOXECO_STG_USER_A — Đặng Châu Giang, MNV 00131946, Ban Giám đốc
* Trình duyệt / Thiết bị: emulator-5554, Pixel 7 AVD, 1080x2400, UiAutomator2
* Build/Version: STG · v1.1

**II. Mô tả Bug**

**Pre-condition:** Đã đăng nhập FoxEco với tài khoản có tên "Đặng Châu Giang".

**Steps:**

1. Vào tab "Cá nhân"
2. Xem avatar chữ viết tắt ở đầu trang

**Expected result:**

* Avatar = chữ viết tắt của 2 từ CUỐI trong tên, không dấu, viết hoa → "Đặng Châu Giang" → `CG`

**Actual result:**

* Avatar hiện `ĐC` — sai 2 điểm cùng lúc: lấy 2 từ ĐẦU thay vì 2 từ cuối, và còn giữ dấu
* Các phần khác (tên, dòng phòng ban·MNV, vắng SĐT/email/địa chỉ) đều đúng — chỉ riêng logic tạo avatar sai

**Hình ảnh mô tả:** đính kèm ảnh evidence (TC-USR-002) theo attachment của issue này.
