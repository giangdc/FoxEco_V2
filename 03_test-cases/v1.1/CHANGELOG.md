# CHANGELOG — Test Cases v1.1

> **TC Generation Log** — đích write-back của `generate-tc` (⛔ KHÔNG ghi vào version MEMORY `§4`/`§9` — router chỉ trỏ, không chứa nội dung).
> Cột `Review Status` do `review-tc` cập nhật sau; `generate-tc` ghi `⏳`.

## 1. TC Generation Log

| Ngày | Action | DOC ID | Module | Tổng TC | File output | Priority | Mode | Techniques | Review Status |
|---|---|---|---|--:|---|---|---|---|---|
| 2026-09-16 | GENERATE | DOC-v1.1-01 · DOC-v1.1-03 · DOC-v1.1-04 | USR | 29 | `fragments/TC-USR-v1.1.md` | P1:2, P2:23, P3:4 | standard | N/A | ⏳ |
| 2026-09-17 | REVISE | DOC-v1.1-01 · DOC-v1.1-02 | USR | 29 | `fragments/TC-USR-v1.1.md` | P1:2, P2:23, P3:4 | standard | N/A | ⏳ |
| 2026-09-16 | REVISE | DOC-v1.1-01 · DOC-v1.1-02 · DOC-v1.1-04 | USR | 29 | `fragments/TC-USR-v1.1.md` | P1:2, P2:23, P3:4 | standard | N/A | ⏳ |

> **REVISE 2026-09-17 (`USR`, BA trả lời CL):** chuỗi lỗi SĐT (`TC-USR-016/017/019/020/036`) BA xác nhận giữ theo demo ⇒ bỏ ghi chú "lấy tạm, chờ BA". Expected/số TC/ID/priority không đổi.
> **REVISE 2026-09-16 (`USR`, sửa theo spot-check `/review-tc` module):** R3-02 `016/017/019/020/036` thêm chuỗi lỗi verbatim (tạm theo demo, chờ xác nhận) · R3-01 `022` tách bước mở lại Theo dõi đơn qua tab "Hoạt động" · R3-09 `034` ghi rõ thoát bằng nút back thiết bị · R3-14 `025` chuyển tiền đề "địa chỉ khác rỗng" thành bước setup · R3-03 `032/033/035/036` ghi cần bổ sung tài khoản C/D vào catalog · R3-06 `028` tách bước xoá/nhập · R3-12 `002` bỏ placeholder · R4-01 thống nhất "field nhập liệu" và "số điện thoại" · R4-07 `026..031` thêm `DOC-v1.1-01` · R3-18 bỏ "Mục đích" thừa ở `015`. Số TC/ID/priority không đổi.
> **GENERATE 2026-09-16 (`USR`):** scope NEW + MODIFIED = 17 SC. 24 TC NEW (`TC-USR-014..037`) + 5 TC MODIFIED giữ ID v1.0 (`TC-USR-002/003/008/012/013`). CARRIED 7 SC dùng TC v1.0 (`TC-USR-001/004/005/006/007/009/010/011`), không chép sang fragment v1.1. Không gỡ TC nào ⇒ không cần khai lỗ ID.

## 2. Ràng buộc còn hiệu lực

1. **Mode `standard`** — kế thừa v1.0 (BA chốt 2026-09-07), ⛔ không trộn mode trong cùng version.
2. 🔴 **`TC-USR-003` và `TC-USR-008` có kỳ vọng NGƯỢC bản v1.0 cùng ID** — consolidate/execute phải lấy bản v1.1.
3. **Rule BA chốt ngoài PRD, demo đang lệch** (`Project_rule §10.1` chưa có bằng chứng UI STG): `TC-USR-002/008/012/021/025..037`. Lệch trên STG ⇒ log bug, ⛔ không sửa TC theo demo.

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🟡 **Chưa consolidate** TC-MASTER v1.1 | Chỉ có fragment `USR` | `/generate-tc --consolidate` khi đủ module |
| 2 | 🟡 **Chưa review** (gate G1) | ⏳ | `/review-tc` |
| 3 | 🟡 **Chưa vibe-test STG** cho các điểm demo lệch rule (avatar · badge · ô địa chỉ · nguồn HRIS · bản nháp · icon khiên) | `RISK-USR-06` Partially | `/vibe-test --module USR` trước lô execute |
| 4 | 🟡 **Cần 4 tài khoản** (A · B · C chưa lưu + HRIS có dữ liệu · D chưa lưu + HRIS trống) | Chưa chuẩn bị | Xin dev/HR tài khoản C, D; chạy `TC-USR-032/033/035/036` trước |
| 5 | ✅ ~~Chuỗi thông báo lỗi SĐT lấy tạm theo demo~~ (`TC-USR-016/017/019/020/036`) | **Đóng 2026-09-17** — BA xác nhận chuỗi demo là chính thức | Đã bỏ chữ "tạm" trong 5 TC; không đổi Expected |
