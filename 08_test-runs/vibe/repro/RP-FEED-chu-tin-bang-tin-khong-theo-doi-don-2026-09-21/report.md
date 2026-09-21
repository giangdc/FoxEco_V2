# Repro Report — RP-FEED-chu-tin-bang-tin-khong-theo-doi-don — 2026-09-21

> **Hợp đồng NHẸ** (`repro/`): report + ≤3 ảnh, ⛔ KHÔNG per-TC evidence.
> Platform: mobile (Appium MCP + `adb`) · `emulator-5554` · app `com.hrisproject.stag` · Tài khoản chủ tin: **`stag_giangdc2@`** (Đặng Châu Giang)
> Mục tiêu: QC báo *"chủ tin bấm tin từ Trang chủ → Theo dõi đơn, nhưng từ Bảng tin → Chi tiết tin (đúng phải là Theo dõi đơn)"* — rà PRD rồi tái hiện. Kết quả: `BUG-028` / Jira (xem cuối).

## Vì sao là `repro/` chứ không phải `VR-`

Không có TC nào của scope bị chạy/chấm verdict trong phiên này (đây là kiểm tra 1 hành vi theo yêu cầu QC), nên **không đủ điều kiện mở run `VR-`** (hợp đồng đầy đủ đòi ≥1 TC kèm evidence per-TC).

## Kết quả rà PRD (`00_input/v1.1/FoxEco PRD v1.0 - Gui Hang.pdf` = `DOC-v1.1-01`)

| Câu hỏi | Kết quả |
|---|---|
| PRD có quy định chủ tin bấm tin của mình ở **Bảng tin** phải mở **Theo dõi đơn** không? | ❌ **Không có** câu nào quy định |
| Sơ đồ điều hướng | `§7.1` trang 30/57: `Bảng tin → Danh sách tin NEED → Chi tiết tin → "Tôi mang giúp được"` · `Đơn hàng → Tab Đang chạy → Theo dõi đơn` — hai luồng tách nhau, **không phân biệt vai** |
| Chủ tin mở tin của mình | `AC-12.2.01` trang 20: *"Người dùng mở tin của chính mình → không có nút 'Tôi mang giúp được'"* ⇒ ngầm định chủ tin vẫn mở được **Chi tiết tin** (chỉ không có nút) |
| TC liên quan | `TC-FEED-005` (bấm card ở Bảng tin mở Chi tiết tin) · `TC-FEED-011` (chủ tin không thấy nút nhận đơn) |

⇒ Hành vi hiện tại **không vi phạm câu chữ nào của PRD**; bug này là **gap yêu cầu/UX** do QC nêu (xem lý do QC ở dưới), **không phải lệch spec**.

## Tái hiện (`stag_giangdc2@`, tin `Thuốc/Y tế` · `FTEL Đà Nẵng Cẩm Lệ → Tòa V-City` · `Chờ ghép`)

| Đường vào | Màn mở ra | Có `Chỉnh sửa`/`Huỷ đơn`? |
|---|---|---|
| **Hoạt động** (`Đơn của tôi` → tab `Đang diễn ra`) → bấm tin | **`Theo dõi đơn`** — stepper `Chờ ghép`, dòng *"Đang chờ người vận chuyển nhận đơn"* | ✅ **Có** cả `Chỉnh sửa` và `Huỷ đơn` |
| **Bảng tin** → bấm card có badge **`Tin của bạn`** (cùng tin) | **`Chi tiết tin`** — chỉ xem: ảnh, thông tin hàng, lộ trình, khung giờ, người gửi | ❌ **Không** có `Chỉnh sửa`, ❌ **không** có `Huỷ đơn`, không có CTA nào |
| **Trang chủ** → `Đơn của tôi` | *(QC báo → Theo dõi đơn)* | ⚠️ **Chưa tự tái hiện**: tin NEED `Chờ ghép` này **không nằm trong 5 đơn** hiển thị ở Trang chủ; đã xác nhận đường **Hoạt động** (cùng nguồn "Đơn của tôi") |

Cùng 1 tin, cùng trạng thái `Chờ ghép`, **khác đường vào ⇒ khác màn hình và khác hành động khả dụng**.

**Ảnh (3):**
- `_recon__hoat-dong-mo-theo-doi-don-co-chinh-sua-huy-don.png` — Hoạt động → Theo dõi đơn (có `Chỉnh sửa` · `Huỷ đơn`)
- `_recon__bang-tin-tin-cua-ban-co-badge.png` — Bảng tin, card `Thuốc/Y tế` có badge `Tin của bạn`
- `_recon__bang-tin-mo-chi-tiet-tin-khong-co-chinh-sua-huy-don.png` — Chi tiết tin (cuối trang): **không** có nút nào

## Lý do QC yêu cầu log

QC GiangDC2: *"nếu là người dùng nên hiển thị nút Chỉnh sửa/Huỷ đơn để người ta tiện thao tác hơn, và cùng 1 trạng thái thì các nguồn vào khác nhau vẫn nên giống nhau."* QC tự chỉnh phân loại (Suggest) trên Jira.

## Giới hạn / chưa kiểm

- Chỉ kiểm **1 tin** (`Thuốc/Y tế`, `Chờ ghép`) và **1 tài khoản**. Chưa kiểm chủ tin ở trạng thái `Đã ghép`/`Đang giao` từ Bảng tin (tin `MATCHED` bị ẩn khỏi Bảng tin theo `BR03-05`, nên gần như chỉ còn tin `Chờ ghép` để đối chiếu).
- Chưa kiểm sau khi bấm `Chỉnh sửa` ở Theo dõi đơn (ngoài phạm vi).
