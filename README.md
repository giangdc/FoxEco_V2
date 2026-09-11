# foxeco-v2 — Manual Testing Project

## Mục đích (Purpose)
Dự án kiểm thử thủ công cho **foxeco-v2**.

## Loại kiểm thử (Test Types)
Functional, Regression, Smoke

## Initial Version
v1.0

## Cấu trúc thư mục (Folder Structure)
| Thư mục | Mục đích |
|---------|----------|
| `00_input/[version]/` | Tài liệu đầu vào theo version |
| `00_input/shared/` | Tài liệu dùng chung mọi version |
| `01_test-plans/` | Kế hoạch kiểm thử theo release/feature |
| `02_analyze-requirements/` | MASTER-MEMORY + Project_rule + version analysis |
| `02_analyze-requirements/[version]/` | Kết quả phân tích theo version |
| `03_test-cases/[version]/` | TC-MASTER + fragments theo version |
| `04_test-data/` | Dữ liệu kiểm thử (valid/invalid) |
| `05_bug-reports/` | Báo cáo lỗi |
| `06_checklists/` | Checklist smoke test & release |
| `07_environments/` | Cấu hình môi trường |
| `08_test-runs/` | Log kết quả chạy test theo sprint |
| `09_reports/` | Báo cáo tổng kết cho stakeholders |
| `10_source-code/` | Automation source code + MEMORY tracking |
| `11_tc-review/` | TC review + SRC-TC review reports |

## Quy tắc đặt tên (Naming Conventions)
→ **Nguồn duy nhất: section `Naming Conventions` trong `02_analyze-requirements/Project_rule.md`.**
Mọi skill đọc ở đó, không hardcode. File này chỉ trỏ — chép bảng ra đây là tạo nguồn thứ 2 để drift.

## Môi trường mặc định (Default Environment)
**STG**

## Ngôn ngữ (Language)
- Nội dung test case, mô tả, bước thực hiện: **Tiếng Việt**
- Thuật ngữ kỹ thuật, keywords, status: **Tiếng Anh**

## Project Rules
→ Chi tiết: `02_analyze-requirements/Project_rule.md`

## Liên hệ (Contacts)
- QA Lead:
- Dev Lead:
- PM:
