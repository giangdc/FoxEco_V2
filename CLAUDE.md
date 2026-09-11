# foxeco-v2 — Project Context

## Thông tin dự án (Project Info)
- **Tên dự án:** foxeco-v2
- **Loại kiểm thử:** Functional, Regression, Smoke
- **Môi trường:** STG
- **URL:** N/A
- **Team:** Solo
- **QC phụ trách:** GiangDC2
- **Automation:** Không có — project chạy manual (`10_source-code/` chưa scaffold)
- **Jira:** Chưa cấu hình — link sẽ bổ sung sau (xem `Project_rule.md §Jira Integration`)

## Version Info
- **Current version:** v1.0
- **Version history:** v1.0 (initial)
- **MASTER-MEMORY:** `02_analyze-requirements/MASTER-MEMORY.md`
- **Project Rules:** `02_analyze-requirements/Project_rule.md`
- **TC-MASTER:** `03_test-cases/v1.0/TC-MASTER-v1.0.xlsx` — **219 TC** / 211 SC, mode `standard`, consolidate 2026-09-07
  (bản copy `03_test-cases/TC-MASTER-LATEST.xlsx`; TC Gen Log ở `03_test-cases/v1.0/CHANGELOG.md`)

## Quy trình làm việc (Workflow)
```
00_input/v1.0/ (tài liệu gốc)
  → 01_test-plans/ (create-test-plan)
    → 02_analyze-requirements/v1.0/ (analyze-requirements)
      → 03_test-cases/v1.0/ (generate-tc → consolidate → TC-MASTER)
        → 11_tc-review/ (review-tc + review-src-tc)
          → 08_test-runs/ (execute)
            → 05_bug-reports/ (log bugs)
              → 09_reports/ (summary report)
```

## MEMORY Files
- **MASTER-MEMORY:** `02_analyze-requirements/MASTER-MEMORY.md` — cross-version registry
- **Version MEMORY:** `02_analyze-requirements/v1.0/MEMORY.md` — version-scoped analysis
- **Source-code MEMORY:** `10_source-code/MEMORY.md` — *(chưa có: project không automation)*

## Naming Conventions
→ **Nguồn duy nhất: section `Naming Conventions` trong `02_analyze-requirements/Project_rule.md`.**
Mọi skill đọc ở đó, không hardcode.
Bug: `bug_id` = `BUG-[NNN]` · file `draft/BUG-[NNN]-[slug].md` → sau push `jira/<JIRA-KEY>-[slug].md` ·
`title` = `[<mã module> - <tên module>] - <mô tả ngắn>` (dùng cho **cả** H1 md và Jira Summary).
Template bug: `assets/bug-report-template.md` của skill `log-bug` (KHÔNG copy vào repo).

## Folder Reference
| # | Folder | Mục đích | Skill liên quan |
|---|--------|----------|----------------|
| 00 | input/v1.0/ | Tài liệu đầu vào (theo version) | analyze-requirements |
| 00 | input/shared/ | Tài liệu dùng chung | analyze-requirements |
| 01 | test-plans/ | Test plan tổng thể | create-test-plan |
| 02 | analyze-requirements/ | MASTER-MEMORY + Project_rule | analyze-requirements |
| 02 | analyze-requirements/v1.0/ | Analysis output theo version | analyze-requirements |
| 03 | test-cases/v1.0/ | TC-MASTER + fragments | generate-tc |
| 04 | test-data/ | Dữ liệu test | — |
| 05 | bug-reports/ | Báo cáo lỗi | log-bug |
| 06 | checklists/ | Smoke + release checklists | — |
| 07 | environments/ | Config môi trường | — |
| 08 | test-runs/ | Logs chạy test | test-report |
| 09 | reports/ | Báo cáo tổng hợp | test-report |
| 10 | source-code/ | Automation code + MEMORY — *chưa scaffold (no automation)* | scan-source, implement-auto |
| 11 | tc-review/ | Review reports (TC + SRC-TC) | review-tc, review-src-tc |

## Project Rules
→ Xem chi tiết: `02_analyze-requirements/Project_rule.md`

## Pipeline & Commands
- **PIPELINE.md** (root) — bản đồ pipeline QA, skill registry, prerequisites, Pipeline Status
- **COMMANDS.md** (root) — cheat-sheet lệnh gọi từng skill theo thứ tự pipeline

> Tester đọc **COMMANDS.md** để biết cách gọi skill; **PIPELINE.md** để biết bước nào cần bước nào trước.

## Tools
- Manual testing project scaffolded by `init-project` skill
- Framework version: Multi-Version (MASTER-MEMORY enabled)
- Created on: 2026-09-07
