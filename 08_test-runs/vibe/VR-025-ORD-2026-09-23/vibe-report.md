# Vibe Report — VR-025 — ORD — 2026-09-23

> Mode: **RETEST** bug Jira ORD (Đăng tin) đang **In review** · STG · emulator-5554 · tài khoản `stag_giangdc2@` · chi tiết: `vibe-log.md` · verdict: `scope-ledger.md`
> ⛔ Chỉ comment + đính kèm ảnh lên Jira, **không đổi trạng thái bug**; không tạo dữ liệu trên STG.

## Kết quả

| Bug | TC | Verdict | Kết luận |
|---|---|---|---|
| [FE-301](https://foxproject.atlassian.net/browse/FE-301) (BUG-009) | TC-ORD-063 · 064 · 066 · 023 · 077 · 021 · 024 · 051 · 083 · 084 · 043 | ✅ 11/11 PASS | Cả 9 nhánh validate (NEED Bước 1, Bước 2, OFFER) nay **có thông báo lỗi tại đúng trường** + cuộn tới ô lỗi ⇒ **đã fix** |
| [FE-303](https://foxproject.atlassian.net/browse/FE-303) (BUG-011) | TC-ORD-059 | ✅ PASS | 15:01 buổi Sáng mờ, không chọn được ⇒ **đã fix** (khớp VR-023) |
| [FE-330](https://foxproject.atlassian.net/browse/FE-330) | — (không có TC) | ✅ PASS | Email người nhận = email người gửi ⇒ lỗi "Email người nhận không được trùng email của bạn", không sang được bước 3 ⇒ **đã fix** |

**Tổng:** 12 TC + 1 kịch bản bug đều PASS · 3 bug sẵn sàng đóng (QC tự chuyển trạng thái).

## Ghi nhận nhỏ (không chặn đóng bug)
- `TC-ORD-064`: chuỗi lỗi "Vui lòng chọn **khối lượng**" — nhãn khối là "TRỌNG LƯỢNG".
- `TC-ORD-021`: email thiếu `@` dùng chung chuỗi "Email phải thuộc tên miền nội bộ…", không có chuỗi "sai định dạng" riêng.
- Bước 2: sau khi autofill tên/SĐT hợp lệ, dòng lỗi cũ dưới 2 ô vẫn còn đến lần bấm "Tiếp theo" kế tiếp.
- FE-330: nút "Tiếp theo" hiển thị sáng như enable dù còn lỗi trùng email (bấm vẫn không đi tiếp).

## Jira
- FE-301: attach 13 ảnh + comment `31090` (15:11) · FE-303: attach 1 ảnh + comment `31091` · FE-330: attach 2 ảnh + comment `31092`. **Không đổi trạng thái** — cả 3 vẫn `In review`.
