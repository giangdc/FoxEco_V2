# Test Data Catalog — v1.1 · Module USR

> Tạo bởi: analyze-requirements (DELTA 2026-09-15, lượt bù thứ hai) · layout **module-first v2**.
> Chỉ liệt kê data **mới/đổi** của lượt delta. Data v1.0 xem `v1.0/USR-tai-khoan/test_data_catalog.md`.

| Data | Loại data | Valid | Invalid | Boundary | Nguồn |
|------|-----------|-------|---------|----------|-------|
| Số điện thoại mặc định | Fixture | Định dạng VN: **10 số, đầu 0** (vd `0901234567`) | **Để trống** (chặn lưu) · `123` · `84901234567` · `0901234` (9 số) · chữ | ⭐ **10 số đầu 0** (hợp lệ) · **9 số** · **11 số** · **để trống** — cả 3 đều phải chặn lưu | `DOC-v1.1-01` §8.15.1 BR15-02 · §8.15.2 · §6.2 AC-30.1.02 |
| Địa chỉ mặc định | Fixture | ≤ 200 ký tự; **bỏ trống VẪN hợp lệ** | — | ⭐ **để trống** (hợp lệ — cột `Bắt buộc` = *Không*) · **200** ký tự · **201** ký tự. ⛔ Đừng viết TC "bỏ trống thì lỗi" | `DOC-v1.1-01` §8.15.2 |
| Trường SSO (tên · phòng ban · MNV · email) | Master | Giá trị đồng bộ từ SSO, **chỉ đọc** | — | ⭐ **Email phải có icon khoá** và **không có ô nhập** — 2 assert riêng, không gộp | `DOC-v1.1-01` §8.15.1 BR15-01 · §6.2 AC-30.2.01 |
| Text banner lưu thành công | Master | `"Đã lưu thông tin của bạn"` — verbatim, **banner xanh** | Chuỗi gần đúng | Banner phải **tự ẩn khi người dùng sửa tiếp** (`BR15-05`), ⛔ không cần bấm đóng | `DOC-v1.1-01` §8.15.1 BR15-05 · §6.2 AC-30.1.01 |
| Cặp giá trị hồ sơ TRƯỚC/SAU | Runtime | Ghi lại SĐT **X** + địa chỉ **Y** trước khi sửa; đổi sang **X'** / **Y'** | — | ⭐ **Bắt buộc có bước "ghi lại giá trị TRƯỚC"** cho `SC-USR-014` · `017` · `018` — không có bước này thì 3 TC không phát hiện được gì | `DOC-v1.1-01` §8.15.1 BR15-03/BR15-04 |
| Đơn đã tạo TRƯỚC khi sửa hồ sơ | Runtime | ≥ 1 đơn đã đăng, **ghi lại SĐT + địa chỉ lấy hàng hiển thị trên đơn đó** | Đơn tạo **sau** khi sửa (không kiểm được rule) | ⭐ Cần **cả hai**: 1 đơn cũ (giữ giá trị cũ) + 1 đơn tạo mới sau khi sửa (dùng giá trị mới) — `AC-30.2.02` assert cả 2 vế | `DOC-v1.1-01` §8.15.1 BR15-03 · §6.2 AC-30.2.02 |
| Tài khoản có mục "Cập nhật thông tin" | Fixture | Tài khoản trên bản app **đã build `FR15`** | — | 🔴 App quan sát 2026-07-24 là **view-only hoàn toàn** ⇒ nếu STG chưa build thì **8 SC mới `BLOCKED`**, ⛔ không PASS (`RISK-USR-06`) | `DOC-v1.1-01` §8.15 Trigger vs `KP-01` §2 KB-USR-01 |
| Avatar · khu vực/văn phòng · kênh liên hệ | — | — | — | ⛔ **KHÔNG đưa vào Test Data** — PRD không nhắc tới 3 trường này ở `§8.15` (`C-USR-05` Open). Đừng assert chiều nào | `DOC-v1.0-01` §A6 USR-02 vs `DOC-v1.1-01` §8.15 |

## Ghi chú
- 🔴 **Tiền đề chặn nhất: app đã build `FR15` chưa.** Toàn bộ 8 SC mới phụ thuộc mục menu "Cập nhật thông tin" tồn tại. **Vibe-test trước `generate-tc`** (`RISK-USR-06`).
- ⭐ **Ba TC bắt buộc có bước "ghi lại giá trị TRƯỚC"**: `SC-USR-014` (kiểm persist thật, không tin banner) · `SC-USR-017` (đơn cũ không đổi) · `SC-USR-018` (hồ sơ không bị ghi đè). Thiếu bước này thì cả ba PASS giả.
- **SĐT mẫu dùng chung với `ORD`** — `BR01-08`/`§8.1.4` cũng dùng định dạng VN 10 số đầu 0 cho SĐT người gửi/người nhận/người uỷ quyền; chuẩn bị **1 bộ SĐT hợp lệ + invalid** dùng cho cả 2 module, ⛔ đừng làm 2 bộ.
- **Đơn `RETURNED` cho `SC-USR-005`**: tái dùng lô `DLV` `SC-DLV-053..056` và chạy **cùng lượt** với `SC-GIFT-014` + `SC-HOME-008` để so 3 màn bằng 1 đơn.
