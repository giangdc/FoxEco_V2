# FE-150 — [TC_07 - Theo dõi đơn] Màn Xác nhận đã lấy hàng/đã giao: Hệ thống mở máy ảnh khi chọn Chụp lại hoặc Chọn ảnh khác

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-150 · **Module:** DLV · **Sync:** 2026-09-24 (R1)

| Field | Value |
|-------|-------|
| Key | FE-150 |
| Module | DLV |
| Status | Done |
| Resolution | Fixed |
| Resolved | 2026-08-08 |
| Verify Date | 2026-08-08 |
| Done At | 2026-08-08 |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Low (weight 2) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Interface |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 1 |
| Due date | 2026-08-05 |
| Reporter | anhptm17 |
| Assignee | Tuanvm37 |
| Created | 2026-08-04 |
| Updated | 2026-08-08 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**Data**:

* Account: [stag\_](mailto:stag_chintl12@fpt.com)vanmtt3@fpt.com

**Step:**

1. Tại màn hình Xác nhận đã lấy hàng => Hiển thị text Chụp ảnh khi nhận hàng 
2. Chụp ảnh => hiển thị 2 btn Chụp lại và Chọn ảnh khác
3. Click 2 btn Chụp lại và Chọn ảnh khác => Hệ thống đều mở máy ảnh 
4. Chon Đã lầy hàng - bắt đầu giao
5. Chon Đã giao cho người nhận 
6. Tại màn hình Xác nhận đã giao => Hệ thống hiển thị text Chụp ảnh hoặc chọn từ thư viện
7. Click 2 btn Chụp lại và Chọn ảnh khác => Hệ thống đều mở máy ảnh 

**=> Bug:**

* **Hệ thống mở máy ảnh khi chọn Chụp lại hoặc Chọn ảnh khác**
* **Màn hình Xác nhận đã lấy hàng hiển thị text ‘chọn từ thư viện’ nhưng không cho chọn** 

Ref màn hình Xác nhận đã lấy hàng

![](blob:https://media.staging.atl-paas.net/?type=file&localId=27bc4f9ae268&id=a7054d53-da67-4c20-9c43-d1107122e756&&collection=&height=null&occurrenceKey=null&width=null&__contextId=null&__displayType=null&__external=false&__fileMimeType=null&__fileName=null&__fileSize=null&__mediaTraceId=null&url=null)
Ref màn hình Xác nhận đã giao 

![](blob:https://media.staging.atl-paas.net/?type=file&localId=0c4c2f4242b7&id=c89238d0-c76e-4e38-8bf1-5265c5f3679e&&collection=&height=null&occurrenceKey=null&width=null&__contextId=null&__displayType=null&__external=false&__fileMimeType=null&__fileName=null&__fileSize=null&__mediaTraceId=null&url=null)
‌
