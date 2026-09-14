# Smoke Test Checklist — foxeco-v2

> Chạy trước mỗi chu kỳ kiểm thử. Nếu bất kỳ mục nào fail, chặn testing và thông báo cho dev.
> Sửa 2026-09-14 theo `health-check` G-06b① — bản cũ là template framework generic (web app, có login/forgot-password/API riêng), **không khớp bề mặt dự án thật**: FoxEco là SDK nhúng trong host app FoxPro, SSO qua host app (không có màn đăng nhập/quên mật khẩu riêng), chưa có đặc tả API (`Project_rule.md §Test Data Rules`).

## Truy cập (Access)
- [ ] Mở host app `FoxPro_Stag` (`vn.fpt.ftel.sop.stg`) trên STG, SSO vào được SDK FoxEco (không có màn đăng nhập riêng của FoxEco)
- [ ] Trang chủ FoxEco load không lỗi, đủ 5 tab bottom nav

## 5 luồng chính Phase 1 (PM chốt — `KP-03 §3`, xem ghi chú scope ở `MASTER-MEMORY.md §9`)
- [ ] **Đăng tin** — tạo được 1 tin NEED và 1 tin OFFER (module `ORD`)
- [ ] **Bảng tin** — danh sách tin cộng đồng hiện đúng, mở được chi tiết 1 tin (module `FEED`)
- [ ] **Ghép nối** — ghép được 1 đơn (luồng thủ công; auto-match OFFER↔NEED ngoài Phase 1 — xem `KP-03 §3.1`) (module `ASN`)
- [ ] **Giao nhận / Xác nhận nhận hàng** — đi hết luồng tới "Hoàn thành" cho core confirm (ảnh/GPS/chi phí là nhánh phụ ngoài Phase 1) (module `DLV`)
- [ ] **Quà cảm ơn** — tặng được Quà ảo sau khi đơn Hoàn thành (module `GIFT`)

> ⚠️ `CNL`/`NTF`/`TS` nằm ngoài scope Phase 1 theo PM nhưng **có trong scope viết TC v1.0 (211 SC toàn bộ 11 module)** — xem `MASTER-MEMORY.md §9 #3`; smoke test này chỉ cover Phase 1, KHÔNG thay thế regression đầy đủ.

## Hạ tầng (Infrastructure)
- [ ] App không crash / không treo khi thao tác 5 luồng trên
- [ ] Không có hình ảnh bị hỏng hoặc tài nguyên bị thiếu trong FoxEco UI
- [ ] *(API endpoints — N/A, chưa có đặc tả API ở tầng tài liệu, xem `§Test Data Rules`)*

---
Kiểm thử bởi: ___________  Ngày: ___________  Build: ___________
