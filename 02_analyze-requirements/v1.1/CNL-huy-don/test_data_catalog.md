# Test Data Catalog — v1.1 · Module CNL

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> Chỉ liệt kê data **mới/đổi** của lượt delta. Data v1.0 xem `v1.0/CNL-huy-don/test_data_catalog.md` — KHÔNG lặp lại.

| Data | Loại data | Valid | Invalid | Boundary | Nguồn |
|------|-----------|-------|---------|----------|-------|
| Lý do huỷ | Fixture | ≥ 5 ký tự sau khi trim (vd `"Không gửi nữa"`) | `""` · `"abcd"` (4 ký tự) · `"     "` (5 dấu cách — rỗng sau trim) | **đúng 5 ký tự** sau trim · **4 ký tự** · **5 dấu cách** · `" abcd "` (6 ký tự thô, 4 sau trim) | `DOC-v1.1-01` §8.11.1 BR11-01 · §8.18.2 VAL-03/VAL-04 · §6.2 AC-25.1.03 |
| Đơn ở MATCHED **đã bấm "Tôi đã lấy hàng"** | Runtime | Đơn `MATCHED`, Carrier vừa bấm nút, popup xác nhận **đang mở** (chưa xác nhận) | — | ⭐ **Ô biên duy nhất của delta này** — cần 2 phiên song song Sender + Carrier, thao tác trong cùng khoảnh khắc | `DOC-v1.1-01` §8.11 Pre-Conditions · §6.2 AC-25.1.01 |
| Đơn ở `INCIDENT` | Runtime | Đơn đã vào trạng thái `INCIDENT` qua luồng báo sự cố (`FR16`) | — | ⚠ **Có thể KHÔNG seed được** nếu app STG chưa build `FR16`/`INCIDENT` ⇒ `SC-CNL-015` kết quả đúng là **BLOCKED**, ⛔ không đánh PASS | `DOC-v1.1-01` §6.2 AC-25.2.01 · §8.16 |
| Đơn ở `IN_TRANSIT` trở đi (đủ 3 vai) | Runtime | 1 đơn đi qua `IN_TRANSIT`, mở được trên cả 3 phiên Sender · Carrier · Receiver | — | Dùng chung `SEED-DLV-01` checkpoint 2 (`03_test-cases/v1.0/CHANGELOG.md`) — ⛔ không seed riêng | `DOC-v1.1-01` §8.11.1 BR11-04 · §6.2 AC-25.2.01 |
| Tài khoản "Admin vận hành" | Fixture | — | — | ⛔ **KHÔNG tồn tại trong phạm vi test** — PRD nêu actor nhưng không đặc tả bề mặt (`C-CNL-03`). `SC-CNL-017` assert-absent | `DOC-v1.1-01` §8.11 dòng Actor |

## Ghi chú
- **Tiền đề cần seed (tái dùng, không seed mới):** `SEED-DLV-01` checkpoint 1 (`MATCHED`) cho `SC-CNL-016`, checkpoint 2 (`IN_TRANSIT`) cho `SC-CNL-006`/`SC-CNL-014`. Xem `03_test-cases/v1.0/CHANGELOG.md` §1 dòng REVISE `DLV` nhóm 1/N.
- **3 phiên đồng thời** vẫn cần cho `SC-CNL-011` (carried) — không đổi so với v1.0.
- ⚠️ **Biên `"5 dấu cách"` là thứ dễ bị bỏ khi nhập tay** — ghi rõ trong Test Data của TC để tester không tự ý gõ `"     x"`.
