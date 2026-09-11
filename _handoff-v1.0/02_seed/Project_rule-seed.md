# Project_rule — SEED cho project mới

> Dán các block dưới vào `02_analyze-requirements/Project_rule.md` của project mới **TRƯỚC KHI** chạy `/analyze-requirements --init`.
> Skill v1.1 đọc `§Layout Conventions` · `§Module Codes` · `§DOC Notation` ngay ở Step 1 — thiếu thì nó phải tự đoán.
>
> Nội dung nghiệp vụ đầy đủ (scope, custom rule, quality gate): xem `00_input-seed/_knowledge-pack/KP-03`.

---

## Layout Conventions

```
analyze_layout: module-first
```

- `module-first` = mỗi module 1 thư mục + `_global/` chứa primary register cross-cutting. **Đây là mặc định của v1.1.**
- Không dùng `flat` — project cũ dùng `flat` và đã dẫn tới `MEMORY.md` 193 KB + `test_scenario_map.md` 125 KB monolith, drift số đếm nhiều lần.

## Module Codes

```
USR · ORD · ASN · DLV · GIFT · CNL · NTF · TS
```

| Code | Tên | Ghi chú |
|---|---|---|
| `USR` | Tài khoản & Hồ sơ | SSO thuộc host app FoxPro — không test trực tiếp được |
| `ORD` | Đăng tin & Quản lý tin | Module lớn nhất |
| `ASN` | Ghép nối | Risk cao nhất |
| `DLV` | Giao nhận | |
| `GIFT` | Quà cảm ơn | |
| `CNL` | Huỷ đơn | |
| `NTF` | Thông báo | |
| `TS` | Trust & Safety | Phần lớn backend/Admin, ít bề mặt UI |

> ⚠ Cân nhắc: 2 màn dùng chung **Trang chủ** và **Bảng tin** ở đợt cũ bị nhét vào `ORD`/`ASN`. Với `module-first` nên tách riêng để fragment gọn hơn.

## DOC Notation

```
req_notation: FR/VR (doc-native, module-prefixed)
```

BRD **CÓ** đánh số requirement nhưng theo ID riêng từng domain, không phải một cặp FR/VR thống nhất:

| Nhóm ID | Nguồn | Ví dụ |
|---|---|---|
| `ORD-NN` `ASN-NN` `DLV-NN` `GIFT-NN` `CNL-NN` `MTCH-NN` `LOC-NN` `RAT-NN` | `§D3` | `ORD-01`, `MTCH-03` |
| `BR-<MODULE>-NN` | `§D4` / `§A5` | `BR-CON-02`, `BR-INT-03` |
| `NTF-NN` | `§D6` | `NTF-05` |
| `OPR-NN` | `§D7` | `OPR-01`, `OPR-05` |
| `NT-NN` `USR-NN` `TS-NN` | `§A2` / `§A6` / `§A8` | `USR-07`, `TS-03` |
| `US-D<NN>` | `§D1b` (có cột Acceptance Criteria) | `US-D06`, `US-D20` |
| `VAL-NN` | `§D8` (mới ở BRD v3.2) | `VAL-04` |

**Quy tắc:** cột "Maps (Ref DOC)" dùng **TRỰC TIẾP ID gốc**, KHÔNG quy đổi sang FR/VR chuẩn hoá.
PRD `.docx` không có ID riêng → định vị bằng `§section · Table N`.

## Quy ước đếm scenario

```
Tổng SC       = đếm TOÀN BỘ scenario, gồm cả DEPRECATED
P1/P2/P3      = chỉ đếm scenario CÒN HIỆU LỰC (loại trừ DEPRECATED)
⇒ P1+P2+P3 có thể NHỎ HƠN Tổng SC — KHÔNG phải sai số liệu
```

> Project cũ chỉ ghi quy ước này ở `CLAUDE.md` (nơi skill không đọc) nên bị `health-check` flag lặp lại mỗi lần chạy.

## Jira Integration

> ⚠ Project cũ **CHƯA** cấu hình block này → `/fetch-us` và phần push/pull Jira của `/log-bug`, `/sync-jira-bugs` **không chạy được**.
> Điền nếu dự án dùng Jira, xoá cả block nếu không.

```
jira_site:      <https://<your-site>.atlassian.net>
jira_project:   <KEY>
us_issue_type:  Story
ac_field:       <tên field chứa Acceptance Criteria>
bug_issue_type: Bug
```

## Custom Rules

> Chép nguyên văn 2 rule từ `KP-03 §4` — đây là rule do QA ban hành, không suy ra được từ tài liệu.

### §10.1 — UI phải khớp Tài liệu mới được viết TC
Chỉ viết TC **khẳng định** một field/nút/màn hình/hành vi khi **CẢ HAI** khớp nhau: (a) tài liệu yêu cầu, **và** (b) bằng chứng UI thật (ảnh Figma / app STG). Không khớp → mở clarification `C-[MODULE]-NN`, **KHÔNG viết TC khẳng định**, cần thiết thì viết TC dạng "GAP finding".

### §10.2 — Màn có tab → mỗi tab 1 TC riêng verify data
Không gộp verify data nhiều tab vào 1 TC "chuyển tab qua lại". Mỗi tab ≥1 TC riêng. TC verify cơ chế switch tab giữ độc lập.
