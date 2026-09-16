# Test Data — Danh sách văn phòng (gợi ý "Địa chỉ mặc định")

> Nguồn: `00_input/v1.1/location_address_catalog.xlsx` (`DOC-v1.1-04`) — BA cung cấp 2026-09-16.
> Dùng cho: `SC-USR-020` · `SC-USR-021` · `SC-USR-022` (màn "Cập nhật thông tin") và prefill địa chỉ ở `ORD`/`ASN`.
> Rule (BA chốt 2026-09-16, home `02_analyze-requirements/v1.1/USR-tai-khoan/risk_assessment.md` · `C-USR-05`): gõ **≥ 3 ký tự** → gợi ý theo **tên văn phòng** (cột `name`), **không phân biệt dấu + hoa thường**; không khớp ⇒ không gợi ý.
> ⛔ Không chép lại 399 dòng ở đây — file xlsx là nguồn duy nhất. File này chỉ giữ **hồ sơ dữ liệu + từ khoá test đã đối chiếu**.

## 1. Hồ sơ file (profile 2026-09-16)

| Mục | Giá trị |
|---|---|
| Sheet | `location_address_catalog (1)` — 1 sheet, 23 cột |
| Số dòng dữ liệu | **399** văn phòng, tất cả `is_active = t` |
| Cột oracle | `name` (chuỗi hiển thị, 8–28 ký tự, **không trùng**) · `search_text` (= `name` bỏ dấu, lowercase, ký tự đặc biệt → khoảng trắng — khớp 399/399) |
| Cột KHÔNG dùng để tìm | `search_alias_text` = `search_text` + **mã tỉnh ở đầu** (vd `hcm 128 hth …`) — rule chỉ tìm theo **tên** |
| Phân bổ tỉnh (top) | HNI 54 · HCM 34 · DNI 16 · THA 11 · QNH 11 · PTO 10 · … |
| `source_section` | KINH_DOANH 368 · HO 26 · FTI_FPL 5 |

⚠️ **`name` là chuỗi kiểu địa chỉ** (vd `363 Nguyễn Hữu Thọ,Cẩm Lệ`, `Tầng 20, FPT Tower`) — không có cột "địa chỉ" tách riêng ⇒ chọn 1 văn phòng thì ô được điền **chính chuỗi `name`** — ✅ BA xác nhận 2026-09-16. Cơ chế khớp: **chứa chuỗi** (BA xác nhận 2026-09-16).

## 2. Từ khoá test (đã đối chiếu với file, so khớp "chứa chuỗi" sau khi bỏ dấu + lowercase)

| # | Mục đích | Gõ | Kỳ vọng theo file | SC |
|---|---|---|---|---|
| K1 | Biên **2 ký tự** — chưa gợi ý | `fp` | **Không hiện** danh sách (dù có 8 dòng chứa "fp") | SC-USR-021 |
| K2 | Biên **3 ký tự** — khớp **nhiều** | `fpt` | **8**: Tầng 20, FPT Tower · Tầng 19, FPT Tower · Tầng 8, FPT Tower · Tầng 9, FPT Tower · FPT Cầu Giấy · Tầng 17,18 FPT Tower · Lô A4-1, KĐT Công nghệ FPT · ĐH FPT, KĐT An Phú Thịnh | SC-USR-021 |
| K3 | Khớp **đúng 1** | `Lê Thái Tổ` | **1**: Tòa V-City, Lê Thái Tổ | SC-USR-021 |
| K4 | **Có dấu / không dấu / HOA** cho cùng kết quả | `Cẩm Lệ` · `cam le` · `CAM LE` | Cả 3 ra **2**: 363 Nguyễn Hữu Thọ,Cẩm Lệ · 36 Nhơn Hòa 4, Cẩm Lệ | SC-USR-021 |
| K5 | **Không khớp** | `xyz` | 0 ⇒ **không hiện gợi ý** | SC-USR-021 |
| K6 | Chỉ tìm theo **tên**, không theo mã tỉnh | `hcm` | Theo `name`: **0** ⇒ không gợi ý. ⚠ Nếu app hiện 34 dòng HCM ⇒ app đang tìm theo `search_alias_text` — **lệch rule** | SC-USR-021 |
| K8 | Khớp **chứa chuỗi** (dính giữa từ) | `tan` | **36** — gồm cả `Tầng 20, FPT Tower` (tan ⊂ tang). Ra ít hơn ⇒ app đang khớp đầu từ — **lệch rule** | SC-USR-021 |
| K7 | Text gõ tay không chọn | `asdfghjkl1` | Không gợi ý; rời ô ⇒ **rỗng** | SC-USR-020 |

## 3. Chất lượng dữ liệu — ghi nhận (không phải rule)

| Vấn đề | Số dòng | Ví dụ | Ảnh hưởng test |
|---|--:|---|---|
| `name` bị **cắt ở 30 ký tự** (`TRUNCATED_30`) | 118 | `BGG177TrườngChinhTTThắngHiệpHò` · `ALK36-06,KĐTPhía Nam,Ttiến` | Chuỗi prefill sang **địa chỉ lấy hàng** có thể cụt/khó đọc — ghi nhận khi chạy `SC-ORD-025`, ⛔ không log bug app vì lỗi ở dữ liệu nguồn |
| Thiếu khoảng trắng giữa từ | nhiều | `LôB3,E-Office,KCN TânThuận` | Gõ `tan thuan` **không ra** dòng này (chỉ ra 3 dòng khác) — ⛔ đừng coi là lỗi tìm kiếm |
| Khớp "chứa chuỗi" dính giữa từ | — | `tan` khớp cả `Tầng 20, FPT Tower` (36 dòng) | ✅ Đúng rule (BA chốt **chứa chuỗi** 2026-09-16) ⇒ dùng làm từ khoá K8 |
| Toạ độ `coordinate_status = MISSING` | 399 | 61 dòng `lat` rỗng · 34 dòng toạ độ **ngoài Việt Nam** (vd `51.93, -8.62`) | Không ảnh hưởng USR. ⚠ Nếu module khác (bản đồ/khoảng cách) dùng toạ độ từ file này ⇒ rủi ro |
| Demo gán cứng `Toà nhà Lô B3, KCX Tân Thuận, Q.7` | — | **Không có** trong file | Demo không dùng catalog ⇒ không làm oracle |
