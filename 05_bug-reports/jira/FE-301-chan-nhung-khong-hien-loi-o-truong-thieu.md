# FE-301 — [TC_04 - Đăng tin - Tôi cần gửi hàng] Chặn sang bước sau nhưng không hiện lỗi ở trường thiếu

🔗 **Jira:** https://foxproject.atlassian.net/browse/FE-301 · **Module:** ORD · **Sync:** 2026-09-23 (R1)

| Field | Value |
|-------|-------|
| Key | FE-301 |
| Module | ORD |
| Status | In Progress |
| Resolution |  |
| Resolved |  |
| Verify Date |  |
| Done At |  |
| Fix Version | V1.0 |
| Priority | Medium |
| Severity | Medium (weight 5) |
| Test Round | R1 |
| Effect | Usability |
| Defect Type | Interface |
| Platform | App |
| Test method | Manual |
| Duplicate | No |
| Reject Number | Lần 1 |
| Due date | 2026-09-23 |
| Reporter | GiangDC2 |
| Assignee | Tuanvm37 |
| Created | 2026-09-21 |
| Updated | 2026-09-23 |

> ⚠️ **Nguồn chuẩn = Jira** — sửa trên Jira rồi `/sync-jira-bugs`, KHÔNG sửa tay file này.

---

## Nội dung từ Jira

**I. Môi trường**

- URL: N/A (FoxEco là SDK nhúng trong host app mobile FoxPro, không có URL riêng)
- Account/Role: CBNV `Đặng Châu Giang`, MNV 00131946 (tài khoản A) — vai SENDER
- Trình duyệt / Thiết bị: emulator-5554, Android, 1080x2400, UiAutomator2
- Build/Version: STG · v1.1 · host app `com.hrisproject.stag` (FoxPro)

**II. Mô tả Bug**

Ở nhiều nhánh validate của form đăng tin (wizard "Tôi cần gửi hàng" bước 1 và bước 2, form "Tôi nhận giao hàng"), app **chặn thao tác tiếp theo** (nút "Tiếp theo" bị khoá, hoặc "Đăng tin ngay" không đăng) nhưng **không hiện thông báo lỗi tại trường thiếu/sai**, và khi bấm submit màn **không cuộn tới ô lỗi đầu tiên**. Người dùng không có dấu hiệu nào cho biết phải sửa gì, ở đâu.

**Pre-condition:**

- Tài khoản A là CBNV có hồ sơ đầy đủ trên STG, đã đăng nhập host app FoxPro.
- Thư viện ảnh thiết bị có sẵn bộ ảnh mẫu (dùng cho các nhánh cần tải ảnh).
- Với các nhánh ở Bước 2: ô "Địa chỉ lấy hàng" phải được điền bằng cách **chạm chọn một gợi ý** (`address-suggestion-N`).

**Steps:** _(luồng đại diện — nhánh thiếu ẢNH HÀNG,_ `TC-ORD-063`, P1)

1. Đăng nhập app FoxPro → menu "Chức năng" → nhấn icon FoxEco
2. Nhấn "+ Đăng tin" → nhấn card "Tôi cần gửi hàng"
3. Chọn chip "Thấp (Dưới 1 triệu đ)" ở khối "GIÁ TRỊ HÀNG (ƯỚC TÍNH)"
4. Chọn chip "Dưới 5 kg (Nhẹ)" ở khối "TRỌNG LƯỢNG"
5. Chọn chip "Nhỏ · Cầm tay" ở khối "KÍCH THƯỚC"
6. Nhấn "Tiếp theo" khi **chưa tải ảnh nào**
7. Quan sát khối "ẢNH HÀNG" — tìm thông báo lỗi

Các nhánh còn lại tái hiện tương tự: vào đúng màn, để trạng thái sai như cột "Nhánh validate" ở bảng dưới, bấm "Tiếp theo" (hoặc "Đăng tin ngay" ở form OFFER), rồi tìm thông báo lỗi.

**Expected result:**

- Wizard vẫn ở màn hiện tại, không đi tiếp được, **và có thông báo lỗi hiện ngay dưới đúng trường thiếu/sai**; khi bấm submit màn cuộn tới ô lỗi đầu tiên.
- Căn cứ `VAL-02`: _"Lỗi hiện ngay dưới ô nhập khi rời ô (on blur), không dùng popup; cuộn tới ô lỗi đầu tiên khi bấm submit"_.

**Actual result:**

- Vế **chặn** đúng ở mọi nhánh (nút "Tiếp theo" `enabled=false` / "Đăng tin ngay" không gửi request).
- Vế **báo lỗi SAI ở mọi nhánh trong bảng**: không có thông báo lỗi nào xuất hiện. Người dùng bị khoá nút mà **không có bất kỳ dấu hiệu nào cho biết thiếu/sai ở đâu**.

| TC | Màn | Nhánh validate | Chặn? | Thông báo lỗi? | Kiểm chứng |
| --- | --- | --- | --- | --- | --- |
| `TC-ORD-063` **(P1)** | NEED · Bước 1 | chưa tải ảnh nào | ✓ có | ✗ **không** | khối "ẢNH HÀNG" chỉ có dòng helper tĩnh |
| `TC-ORD-064` | NEED · Bước 1 | chưa chọn TRỌNG LƯỢNG | ✓ có | ✗ **không** | nhãn khối + 3 chip hiển thị đúng, chỉ thiếu lỗi |
| `TC-ORD-066` | NEED · Bước 1 | chưa chọn KÍCH THƯỚC | ✓ có | ✗ **không** | 3 chip hiển thị đúng, chỉ thiếu lỗi |
| `TC-ORD-023` **(P1)** | NEED · Bước 2 | để trống cả nhóm "NGƯỜI NHẬN" (email, tên, SĐT, địa chỉ giao) | ✓ có (nút khoá) | ✗ **không** | cuộn tới nhóm "NGƯỜI NHẬN": 4 ô chỉ có placeholder, không dòng lỗi nào |
| `TC-ORD-077`, `TC-ORD-021` | NEED · Bước 2 | email sai định dạng: `stag_anhdc4@` (077) · `stag_anhdc4.fpt.com` thiếu `@` (021) | ✓ có | ✗ **không** | 3 ô tên/SĐT/địa chỉ vẫn trống (không tra danh bạ) — đúng; quét 3 chuỗi `định dạng` / `không hợp lệ` / `Không tìm thấy` đều không có (021) |
| `TC-ORD-024`, `TC-ORD-051` | NEED · Bước 2 | "Tên người nhận" chỉ 1 ký tự (`A`) rồi rời ô | nút khoá, nhưng chưa tách được do tên hay do ô khác chưa hợp lệ | ✗ **không** | không có dòng lỗi dưới ô tên. Đối chiếu: ô "Tên người nhận uỷ quyền" cùng màn có lỗi `Tên phải từ 2–60 ký tự` (`TC-ORD-081`) |
| `TC-ORD-051` | NEED · Bước 2 | bấm "Tiếp theo" khi còn nhiều ô sai (tên 1 ký tự, SĐT và địa chỉ giao để trống), đang đứng ở cuối form | ✓ có | ✗ **không** | màn đứng nguyên ở vùng "BUỔI MONG MUỐN", **không cuộn lên** ô lỗi đầu tiên (ô tên người nhận) |
| `TC-ORD-083`, `TC-ORD-084` | NEED · Bước 2 | địa chỉ giao **gõ tay, không chạm chọn gợi ý** (083: trùng hệt địa chỉ lấy · 084: chỉ khác khoảng trắng đầu/cuối) | ✓ có, nút khoá vĩnh viễn | ✗ **không** | xem "Cơ chế nhánh địa chỉ" ngay dưới bảng |
| `TC-ORD-043` | OFFER (1 trang) | điểm đến trùng điểm xuất phát (cùng chọn `FTEL Đà Nẵng Cẩm Lệ`), đã tick điều khoản và chọn buổi | ✓ có ("Đăng tin ngay" không đăng, logcat không có request) | ✗ **không** | đã cuộn kiểm cả 2 nửa form, không có dòng lỗi |

**Cơ chế nhánh địa chỉ (**`TC-ORD-083`/`084`): 2 ô địa chỉ ở Bước 2 ("Địa chỉ lấy hàng", "Địa chỉ giao hàng") chỉ được ghi nhận khi người dùng **chạm chọn một gợi ý**. Gõ tay đủ chữ thì chữ vẫn hiển thị nhưng nút "Tiếp theo" khoá vĩnh viễn và không có dòng lỗi nào — người dùng không có cách biết phải chạm gợi ý. Khi cả 2 địa chỉ đều được chọn từ gợi ý và trùng nhau, app **có** hiện lỗi đỏ `Địa chỉ giao phải khác địa chỉ lấy hàng` (`TC-ORD-026` PASS) ⇒ luật "địa chỉ giao khác địa chỉ lấy" không bị thiếu lỗi; thiếu lỗi là ở nhánh "địa chỉ chưa được chọn từ gợi ý". Vì cả 2 địa chỉ ở `TC-ORD-084` đều gõ tay nên **chưa kiểm được** biên khoảng trắng (trim).

**Phạm vi ảnh hưởng:**

- 8 nhánh validate trải **Bước 1, Bước 2 của wizard NEED và cả form OFFER** ⇒ người dùng có thể bị kẹt ở bất kỳ màn nào mà không biết lý do.
- Đây **không phải** hạn chế của framework hiển thị lỗi: app **CÓ** báo lỗi inline đúng ở các nhánh khác — NEED: ảnh > 5MB (`TC-ORD-068`), chưa chọn buổi (`TC-ORD-058`: _"Chọn ít nhất 1 buổi"_), khoảng ngày > 7 (`TC-ORD-057`), SĐT người nhận sai định dạng (`TC-ORD-025`), SĐT uỷ quyền (`TC-ORD-079`), tên uỷ quyền (`TC-ORD-081`), trùng địa chỉ khi chọn từ gợi ý (`TC-ORD-026`); OFFER: chưa chọn buổi (`Chọn ít nhất 1 buổi`, `TC-ORD-050`) ⇒ là **bỏ sót ở từng nhánh**, không phải thiếu cơ chế.

**Căn cứ:** `VAL-02` (`TC-ORD-051`) · `BR01-01` (_"Thiếu ảnh thì chặn sang bước 2"_) · `BR01-02` (_"không cho để trống"_) · `AC-03.1.02` · `AC-04.2.01` · `KB-ORD-01` (người nhận bắt buộc, `TC-ORD-023`) · `§D8.1` L366-368 (email, tên 2–60, SĐT) · `§D8.2` L381-382 (OFFER: điểm đến ≠ điểm xuất phát) · `§8.1.4` (_"Địa chỉ giao phải khác địa chỉ lấy"_) · `VAL-03` (có trim).

**Hình ảnh mô tả:** đính kèm các file ảnh FAIL trên issue này, mỗi TC ít nhất 1 ảnh (`TC-ORD-063`, `064`, `066`, `077`, `083`, `084` đã có trước; bổ sung `023`, `021`, `024`, `051` (2 ảnh: ô tên + không cuộn), `043` (2 ảnh))
