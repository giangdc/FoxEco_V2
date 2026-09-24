# FE-148 — [TC_02 - Cá nhân]: Header thiếu MNV (mã nhân viên) + badge tier "Hạng Đồng hành"

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-148 · **Module:** USR · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-148 |
| Module | USR |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-06 |
| Verify Date | 2026-08-07 |
| Done At | 2026-08-06 |
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
| Due date | 2026-08-05 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-08-04 |
| Updated | 2026-08-07 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

Điều kiện test: Đã đăng nhập app FoxPro STG (thử trên 2 account: stag_TaiPM@fpt.com, stag_giangdc2@fpt.com), đã vào SDK FoxEco.

**Tại màn hình Cá nhân**

1. Tab "Chức năng" → tile "FoxEco" → vào SDK FoxEco
2. Bấm tab "Cá nhân" ở bottom nav
3. Quan sát toàn bộ header cam đầu màn

**Phần 1 — Thiếu MNV (mã nhân viên)**
Actual: Dòng phòng ban chỉ hiện tên phòng ("Phòng Phát triển Phần mềm số 8" / "Ban Giám đốc"), KHÔNG có phần "· MNV: \[mã NV\]".  
=> Bug: Thiếu trường MNV trên hồ sơ Cá nhân — xác nhận trên cả 2 tài khoản test.  
KQMM: Đúng định dạng "Phòng \[ban\] · MNV: \[mã NV\]" (vd "Phòng Kỹ thuật · MNV: FTEL2291").

**Phần 2 — Thiếu badge tier "Hạng Đồng hành"**
Actual: KHÔNG có badge tier nào trên header, ở cả 2 tài khoản test.  
=> Bug: Thiếu badge tier "🏆 Hạng Đồng hành" tại header màn Cá nhân.  
KQMM: Có badge dạng text tĩnh "🏆 Hạng Đồng hành" (C-USR-01: chưa cần logic tính hạng, chỉ cần hiển thị display-only).

![](blob:https://media.staging.atl-paas.net/?type=file&localId=1cb290b1063b&id=2afd7286-2608-42e1-ad6a-1dd361a3c813&&collection=&height=555&occurrenceKey=null&width=872&__contextId=null&__displayType=null&__external=false&__fileMimeType=null&__fileName=null&__fileSize=null&__mediaTraceId=null&url=null)
‌

---

**Environment:** FoxPro STG, package com.hrisproject.stag, emulator-5554 (Android, Appium MCP)
**Version:** v1.0
**Module:** Cá nhân
**Traceability:** VR-004 (vibe-test) → TC_02.1, TC_02.2, TC_02.3 → REQ-USR-002, REQ-USR-003, REQ-USR-004
