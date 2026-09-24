# FE-291 — [TC_11 - Tài khoản & Hồ sơ] - Chuỗi thông báo lỗi SĐT lệch chuỗi BA đã chốt

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-291 · **Module:** USR · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-291 |
| Module | USR |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-09-23 |
| Verify Date | 2026-09-23 |
| Done At | 2026-09-23 |
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
| Due date | 2026-09-23 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-18 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

* URL: N/A (mobile app, không phải web)
* Account/Role: FOXECO_STG_USER_A — Đặng Châu Giang, MNV 00131946, Ban Giám đốc
* Trình duyệt / Thiết bị: emulator-5554, Pixel 7 AVD, 1080x2400, UiAutomator2
* Build/Version: STG · v1.1

**II. Mô tả Bug**

**Pre-condition:** Đã đăng nhập FoxEco, đang ở màn "Cập nhật thông tin" (Cá nhân → Cập nhật thông tin).

**Steps:**

1. Vào field "Số điện thoại mặc định"
2. Nhập một trong các giá trị sai định dạng sau:

    * để trống (TC-USR-017)
    * `091234567` — 9 số (TC-USR-018)
    * `1912345678` — không bắt đầu bằng 0 (TC-USR-020)
    * `09123a5678` — chứa chữ (TC-USR-023)
    
3. Nhấn nút "Lưu thay đổi"

**Expected result:**

* TC-USR-017: thông báo lỗi đỏ "Vui lòng nhập số điện thoại"
* TC-USR-018 / TC-USR-020 / TC-USR-023: thông báo lỗi đỏ "Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)"
* (các vế khác đều đạt: màu đỏ, vị trí ngay dưới field, chặn lưu đúng, không banner "Đã lưu…" giả)

**Actual result:**

* TC-USR-017: hiện "Số điện thoại không được để trống" (khác hẳn câu kỳ vọng)
* TC-USR-018 / TC-USR-020 / TC-USR-023: hiện "Số điện thoại không hợp lệ" — thiếu hẳn phần `(10 số, bắt đầu bằng 0)` trong ngoặc
* Chuỗi kỳ vọng lấy từ demo `DOC-v1.1-02`, BA xác nhận 2026-09-17 là chuỗi chính thức
* Hành vi chặn lưu bản thân đúng ở cả 4 case — chỉ sai nội dung text thông báo

**Hình ảnh mô tả:** đính kèm 4 ảnh evidence (TC-USR-017/018/020/023) theo attachment của issue này.
