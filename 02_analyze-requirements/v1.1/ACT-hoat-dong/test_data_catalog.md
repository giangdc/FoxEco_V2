# Test Data Catalog — v1.1 · Module ACT

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> Chỉ liệt kê data **mới/đổi** của lượt delta. Data v1.0 xem `v1.0/ACT-hoat-dong/test_data_catalog.md`.

| Data | Loại data | Valid | Invalid | Boundary | Nguồn |
|------|-----------|-------|---------|----------|-------|
| Text empty state tab đang-chạy | Master | `"Không có đơn đang thực hiện"` + **đúng 1 CTA** nhãn `"Đăng tin gửi hàng"` | Thiếu CTA · CTA sai nhãn · chuỗi gần đúng | — | `DOC-v1.1-01` §8.17.1 EMP-05 |
| Text empty state tab hoàn-tất | Master | `"Chưa có đơn hoàn tất"` + **KHÔNG CTA** + **khối lịch sử bị ẩn hẳn** | Có CTA (sai `EMP-06`) · khối lịch sử hiện khung rỗng | ⭐ Bất đối xứng với tab kia — đây là **assert**, không phải chi tiết trình bày | `DOC-v1.1-01` §8.17.1 EMP-06 |
| Text lý do "Hết hạn" | Master | `"Không có ai nhận mang giúp trong thời gian đăng"` — verbatim | Chuỗi tự chế của app | — | `DOC-v1.1-01` §8.5.1 BR05-03 · §6.2 AC-09.1.01 |
| Bộ 3 đơn kết thúc | Runtime | 1 đơn `COMPLETED` + 1 đơn `EXPIRED` + 1 đơn `RETURNED` **cùng 1 tài khoản** | Chỉ có `COMPLETED` (không phân biệt được 3 nhánh) | ⚠ `RETURNED` cần nhánh `FR09` của `DLV` — có thể **chưa build** ⇒ `SC-ACT-005`/`SC-ACT-015` `BLOCKED` từng phần | `DOC-v1.1-01` §6.2 AC-09.1.01 · AC-24.2.01 |
| Cặp đối chứng `CANCELLED` ⟷ `RETURNED` | Runtime | 1 đơn `CANCELLED` (phải **ẩn**) + 1 đơn `RETURNED` (phải **hiện kèm lý do**) — cùng tài khoản, xem trong 1 lượt | Chỉ 1 trong 2 (mất phép đối chứng) | ⭐ Giá trị của `SC-ACT-015` nằm ở **cặp**, ⛔ không seed lẻ | `DOC-v1.1-01` §6.2 AC-24.2.01 vs `KP-01` §3 KB-ORD-07 (#7) |
| Đơn NEED quá "Đến ngày" **vẫn POSTED** | Runtime | Tin NEED có "Đến ngày" đã qua VÀ **chưa ai ghép** | Tin đã `MATCHED` rồi mới quá ngày (⛔ không chuyển `EXPIRED` — `BR05-03`) | ⭐ Vế *"vẫn POSTED"* là điều kiện v1.0 chưa nêu — dev hay chỉ kiểm mỗi ngày hết hạn | `DOC-v1.1-01` §8.5.1 BR05-03 |
| Tài khoản trắng | Fixture | Tài khoản **chưa có đơn nào** ở cả 2 tab | Tài khoản đã dùng cho lô test khác | ⚠ Khó tái tạo khi môi trường đã có dữ liệu — **gộp lô** với `SC-HOME-025..027` + `SC-GIFT-008`, dùng chung 1 tài khoản mới tinh | `DOC-v1.1-01` §8.17.1 · §6.2 AC-29.1.01 |
| Tốc độ mạng | Fixture | Mạng bình thường | — | ⭐ **Throttle về 3G chậm** — bắt buộc cho `SC-ACT-017`: mạng nhanh thì pha loading trôi qua quá nhanh, không phân biệt được *đang tải* ⟷ *không có dữ liệu* | `DOC-v1.1-01` §8.17.2 BR17-02 |

## Ghi chú
- **Tài khoản trắng là tài nguyên khan hiếm nhất của lượt này** — cả `ACT`, `HOME` và `GIFT` đều cần. Xin **1 tài khoản mới tinh dùng chung**, chạy hết cụm empty state trong 1 lượt rồi mới để nó "bẩn" đi; ⛔ đừng để mỗi module tự xin một tài khoản.
- **Đơn `RETURNED` tái dùng từ lô `DLV`** (`SC-DLV-053..056`), ⛔ không dựng riêng. Nếu lô đó `BLOCKED` thì `SC-ACT-015` cũng `BLOCKED` và `SC-ACT-005` chỉ chạy được phần `COMPLETED` + `EXPIRED`.
- **Đơn `EXPIRED`** cần chờ thời gian thật hoặc seed timestamp — cùng nhóm khó với `SC-DLV-024`/`SC-DLV-048`/`SC-TS-006`; gộp chung 1 kế hoạch seed thời gian, ⛔ đừng chạy rời rạc nhiều lần.
