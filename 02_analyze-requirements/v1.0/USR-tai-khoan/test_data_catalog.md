# Test Data Catalog — v1.0 · Module USR

> Tạo bởi: analyze-requirements (**stage: analyze** — sinh sớm để generate-tc dùng cho EP/BVA).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.

## Module USR — Tài khoản & Hồ sơ (DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-04)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Tài khoản SSO | Master | CBNV FPT còn hiệu lực (STG: tài khoản pre-logged-in tên hiển thị "Chung Hoàng Liêm") | tài khoản ngoài FPT / hết hiệu lực (→ không vào được SDK — chặn ở host app) | — (không có dải giá trị) | `USR-01` §A6 L99 |
| Tên hiển thị | Master | lấy từ hồ sơ nhân viên, không sửa được ở FoxEco | — (view-only, không có đường nhập) | — | `USR-02` §A6 L100 |
| Phòng ban | Master | tên phòng ban trong hồ sơ nhân viên (vd "Phòng Kỹ thuật") | — (view-only) | **hồ sơ THIẾU phòng ban → cần biết UI hiện gì (chưa có đặc tả)** | `USR-04` §A6 L101 |
| MNV (mã nhân viên) | Master | mã dạng `FTEL####` (vd `FTEL2291`) | — (view-only) | — | `DOC-v1.0-02` §1.1 |
| Avatar | Master | ảnh hồ sơ nhân viên | — (view-only) | **hồ sơ KHÔNG có avatar → placeholder mặc định (chưa có đặc tả)** | `USR-02` §A6 L100 |
| Badge hạng thành viên | Master | text tĩnh "Hạng Đồng hành" | — (không có logic đổi hạng ở v1.0) | — (1 giá trị duy nhất ở v1.0) | `DOC-v1.0-04` ảnh `570ad9d3…` · `C-USR-01` |
| Số "đơn đã giúp" | Runtime | số nguyên ≥ 0, tăng 1 khi 1 đơn mình vận chuyển chuyển sang Hoàn thành | — | **0 (tài khoản mới — cần biết card hiện "0" hay ẩn)** | `USR-05` §A6 L102 |
| Số "quà đã nhận" | Runtime | số nguyên ≥ 0, tăng 1 mỗi lần Sender gửi quà cảm ơn | — | **0 (chưa nhận quà nào → xem SC-GIFT-008 empty state)** | `USR-05` §A6 L102 · `US-D20` |
| Điểm ECO / Điểm uy tín / CO₂ | — | ⛔ **KHÔNG tồn tại ở v1.0** — dùng làm giá trị assert-absent cho SC-USR-006 | — | — | `DOC-v1.0-01` §A7 L111 · `C-USR-01` |

## Ghi chú chung
- **Cột `Loại data`:** `Master` = có sẵn từ hệ thống (hồ sơ nhân viên/SSO), KHÔNG seed được từ phía QC — **giá trị thực xác nhận lại ở vibe-test**. `Runtime` = sinh khi chạy (đếm theo lịch sử đơn/quà).
- **Module này KHÔNG có `Fixture`** — toàn bộ dữ liệu hồ sơ đến từ hệ thống nhân sự, tester không tạo/sửa được. Đây là lý do các SC hiển thị dùng oracle **"khớp hồ sơ nhân viên"** thay vì giá trị hằng.
- Boundary in **đậm** là ứng viên BVA cho generate-tc. Ba boundary của module này (**hồ sơ thiếu phòng ban** · **không có avatar** · **chỉ số = 0**) **chưa có đặc tả** ⇒ generate-tc viết TC dạng ghi nhận, không assert text cụ thể (xem `risk_assessment.md` CL `C-ORD-06` nhánh empty state).
- **Tài khoản test:** cần ≥1 tài khoản có lịch sử (đơn đã giúp > 0, quà đã nhận > 0) và ≥1 tài khoản "trắng" (cả 2 chỉ số = 0) để phủ boundary. Giá trị đăng nhập ở `~/.foxeco-v2/credentials.env` (`Project_rule §Execution Rules`), ⛔ không ghi ở đây.
