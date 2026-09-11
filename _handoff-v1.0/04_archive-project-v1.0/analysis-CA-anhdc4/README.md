# Phân tích của QC anhdc4 — bản lưu trữ

> Khôi phục từ commit `6f0b0cd` của project v1.0 (thư mục `02_analyze-requirements CA/`, đã xoá khỏi working tree ngày 2026-07-30 sau khi merge xong).
> Gói kèm ở đây để bộ bàn giao **không phụ thuộc vào git history của repo cũ**.

## Bối cảnh

Team có 2 người. QC **anhdc4** phân tích độc lập trên project riêng, **dựa trên demo HTML**. Ngày 2026-07-29 quyết định lấy project của GiangDC2 làm base và gộp lại thành một.

## Đã merge những gì

- **15/15 clarification** của anhdc4 đã rà hết: 10 trùng khớp sẵn với project base, **5 merge mới** → `C-ORD-07` · `C-CNL-02` · `C-ORD-08` · `C-ASN-03` · `C-GIFT-02` (xem `KP-02`)
- TC của anhdc4 **chỉ dùng làm checklist field tham khảo** — mọi Source Quote/Location đều trích trực tiếp từ tài liệu gốc của project base, đúng `Project_rule §10.1`
- **6 nhóm case** chỉ có ở bộ TC của anhdc4 mà project base không có nguồn tài liệu → **cố ý không viết TC**, để lại chờ đợt phân tích sau (xem `KP-05 §3`)

## Vì sao vẫn giữ

Dùng khi cần kiểm chứng xuất xứ một quyết định merge, hoặc rà lại 6 nhóm case chưa có nguồn. **Không dùng làm nguồn requirement** — nội dung đã được chắt lọc vào `KP-02` và `KP-05`.

## Nội dung khôi phục (14 file)

| | |
|---|---|
| `MASTER-MEMORY.md` · `Project_rule.md` | Cấu hình project riêng của anhdc4 |
| `v1.0/` · `v1.1/` | 5 file phân tích mỗi version (MEMORY, traceability, scenario_map, data_catalog, risk) |
| `TestCases-CA.xlsx` | Bộ TC gốc của anhdc4 |
