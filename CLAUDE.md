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
- **Version đang phân tích/sinh TC:** **v1.1** (delta của v1.0) — `02_analyze-requirements/v1.1/` · `03_test-cases/v1.1/`
- **Version đang thực thi/test:** **v1.0** — pipeline v1.0 còn dở (`review-tc` REJECTED, `vibe-test`/`log-bug` chưa chạy)
  nên `MASTER-MEMORY §10 Version Cutover` **chưa áp dụng**; §8 vẫn là bảng sống của v1.0, v1.1 dùng bảng riêng **§8b**.
- **Version history:** v1.0 (initial, 2026-09-07) → v1.1 (delta, ANALYZED 2026-09-17)
- **MASTER-MEMORY:** `02_analyze-requirements/MASTER-MEMORY.md`
- **Project Rules:** `02_analyze-requirements/Project_rule.md`

### TC-MASTER — 🔴 đọc kỹ, có **2 file** và phải mở **song song**

| File | TC | Phủ | Trạng thái |
|---|--:|---|---|
| `03_test-cases/v1.1/TC-MASTER-v1.1.xlsx` | **223** | 139 SC NEW+MODIFIED của v1.1 | ✅ Consolidated 2026-09-17 · ⏳ chưa review |
| `03_test-cases/v1.0/TC-MASTER-v1.0.xlsx` | 219 | 211 SC của v1.0 (chứa **163 TC CARRIED** mà v1.1 KHÔNG gộp lại) | ✅ Consolidated 2026-09-07 · ❌ review 0/100 REJECTED |

- 🔒 **SỐ LƯỢNG TC ĐÃ CHỐT VỚI TEAM 2026-09-18 — FREEZE** (`Project_rule.md §Custom Rules §10.5`): trong quá trình test ⛔ **không thêm/xoá/tách/gộp TC**, chỉ được sửa Steps · Expected · Test Data · Pre-condition · Notes · Status · Lifecycle. Case không còn đúng nghiệp vụ ⇒ đánh `DESCOPED` + `Skipped`, **giữ nguyên dòng**. Bảng chốt per-module + phép kiểm nhanh nằm ở §10.5.
- 🔴 **v1.1 KHÔNG gộp CARRIED** (QC chốt 2026-09-17) ⇒ muốn phủ đủ **302 SC** thì phải mở **cả 2 file**.
- ⚠️ **54 TC ID trùng giữa 2 file** (SC MODIFIED giữ ID v1.0) — **LUÔN lấy bản v1.1**.
  5 TC kỳ vọng **NGƯỢC nhau**: `TC-ACT-008/013/014` · `TC-USR-003/008`. Lấy nhầm bản ⇒ kết luận ngược mà không có gì báo lỗi.
- **`03_test-cases/TC-MASTER-LATEST.xlsx` = bản copy của `v1.1`** *(verify md5 2026-09-17 — trước đây file này bị khai nhầm là copy của v1.0)*.
- TC Gen Log: `03_test-cases/v1.1/CHANGELOG.md` (v1.1) · `03_test-cases/v1.0/CHANGELOG.md` (v1.0).
- 🔑 **Số canonical không nằm ở file này.** REQ/SC/priority → frontmatter `counts:` của `<module>/test_scenario_map.md`;
  CL/RISK → `<module>/risk_assessment.md`. File này chỉ trỏ đường.

## 🔑 Tài khoản test STG + OTP (đọc TRƯỚC khi chạy `vibe-test`)

| Cần gì | Ở đâu |
|---|---|
| **Secret** — OTP dùng chung, (mật khẩu nếu có) | **`~/.foxeco-v2/credentials.env`** (`chmod 600`, **ngoài repo**, đã `.gitignore`) — biến `FOXECO_STG_OTP` · `FOXECO_STG_PASS` · `FOXECO_STG_USER_1..5` |
| **Không secret** — email · MNV · vai · chiến lược luân phiên · dữ liệu đã tạo trên STG | **`04_test-data/valid/USR-accounts.md`** ⭐ |
| Nguồn gốc QC cung cấp | `04_test-data/account.txt` — 🔒 **đã gitignore, ⛔ KHÔNG commit, ⛔ không in ra output** |

🔑 **OTP staging CỐ ĐỊNH, dùng chung cho MỌI account, không đổi theo thời gian.**
⇒ **AI TỰ ĐĂNG NHẬP ĐƯỢC**, ⛔ không cần người nhập tay — ✅ **đã kiểm chứng thật 2026-09-19** (tự logout → login `stag_taipm@` thành công).
🔑 **Login chỉ cần EMAIL + OTP — ⛔ KHÔNG có trường mật khẩu.** Luồng 5 bước dùng lại được ở `USR-accounts.md §0b`.
🔴 **Mọi ghi chép cũ nói *"OTP nhập tay, AI không lấy được"*** (VR-001 `§0` · VR-003 · VR-004 ledger · các dòng `NOT_RUN` viện lý do OTP) **ĐÃ LỖI THỜI** — viết khi chưa biết OTP là cố định. TC nào từng `NOT_RUN` **chỉ vì OTP** thì nay **chạy được**.

**Đăng xuất / đổi tài khoản:** FoxPro → `Cá nhân` → cuộn cuối → **`Đăng xuất`**. ⛔ Không có trong FoxEco.
**Vào lại FoxEco:** FoxPro → `Chức năng` → `scroll_to_element` tới icon **`FoxEco`**.
**Luân phiên:** gom việc **theo TÀI KHOẢN**, không theo TC (mỗi lần đổi tốn ~8–10 MCP call) — bảng phân vai A/B/C/D ở `USR-accounts.md §2`.

## Quy trình làm việc (Workflow)
> Thay `v[X]` bằng version đang làm (hiện hành: **v1.1** cho analyze/generate-tc, **v1.0** cho execute).
```
00_input/v[X]/ (tài liệu gốc)
  → 01_test-plans/ (create-test-plan)
    → 02_analyze-requirements/v[X]/ (analyze-requirements)
      → 03_test-cases/v[X]/ (generate-tc → consolidate → TC-MASTER)
        → 11_tc-review/ (review-tc + review-src-tc)
          → 08_test-runs/ (execute)
            → 05_bug-reports/ (log bugs)
              → 09_reports/ (summary report)
```

## MEMORY Files
- **MASTER-MEMORY:** `02_analyze-requirements/MASTER-MEMORY.md` — cross-version registry
- **Version MEMORY (router):** `02_analyze-requirements/v1.1/MEMORY.md` (hiện hành) · `02_analyze-requirements/v1.0/MEMORY.md`
  ⛔ Router **chỉ có §1 Function Register + §2 Module Summary** (layout `module-first v2`) — nội dung thật ở `v[X]/<MODULE>/` (5 file/module).
  ⚠️ `FEED` **không có thư mục v1.1** — home duy nhất của nó là `v1.0/FEED-bang-tin/`.
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
| 00 | input/v[X]/ | Tài liệu đầu vào (theo version) — `v1.0/` · `v1.1/` | analyze-requirements |
| 00 | input/shared/ | Tài liệu dùng chung | analyze-requirements |
| 01 | test-plans/ | Test plan tổng thể | create-test-plan |
| 02 | analyze-requirements/ | MASTER-MEMORY + Project_rule | analyze-requirements |
| 02 | analyze-requirements/v[X]/ | Analysis output theo version — router + `<MODULE>/` (5 file) | analyze-requirements |
| 03 | test-cases/v[X]/ | TC-MASTER + fragments — ⚠️ v1.0 và v1.1 **cùng sống**, xem §Version Info | generate-tc |
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
