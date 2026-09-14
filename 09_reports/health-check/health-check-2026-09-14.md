# Health Check Report — foxeco-v2 · v1.0

> Generated: 2026-09-14 · Mode: **FULL** · Run by: GiangDC2
> ✅ **Remediation pass hoàn tất cùng ngày — xem `## Remediation Log (2026-09-14)` ở cuối file.** 10/12 finding đã sửa trực tiếp; 2 finding (C-04, H-06) vốn không cần hành động (đúng trạng thái từ đầu, chỉ là informational).
> Layout dò được: **analyze = module-first v2** (`<Dir>/CHANGELOG.md` tồn tại ở cả 11 module) · **runs = v2** (`08_test-runs/runs/{INDEX.md,FAIL-REGISTRY.md}`)
> Mode TC (suy từ artifact): **standard** — 0 sheet `Coverage Matrix`, 0/219 TC Notes có tag `Technique:` ⇒ C-08/C-09 không áp, và việc thiếu 2 sheet/tag đó là **đúng**, không phải lỗi.
> So với lượt trước (`health-check-2026-09-07.md`, chạy TRƯỚC `generate-tc`/`review-tc`): Group C nay áp dụng được — kết quả **sạch 100%**.

## Files checked

| Nguồn | Trạng thái |
|---|---|
| `PIPELINE.md` · `CLAUDE.md` · `COMMANDS.md` | ✅ |
| `02_analyze-requirements/MASTER-MEMORY.md` · `Project_rule.md` | ✅ |
| `02_analyze-requirements/v1.0/MEMORY.md` (router) + 11 module × 5 file = 55 file | ✅ |
| `03_test-cases/v1.0/TC-MASTER-v1.0.xlsx` (parse qua openpyxl) + `TC-MASTER-LATEST.xlsx` + `CHANGELOG.md` (TC Gen Log) + 11 fragment `.md` | ✅ |
| `11_tc-review/review-report-v1.0.md` | ✅ |
| `08_test-runs/runs/{INDEX.md, FAIL-REGISTRY.md}` · `08_test-runs/vibe/` | ✅ (template rỗng — 0 dòng RUN/FAIL, đúng trạng thái) |
| `05_bug-reports/{jira,draft}/**` (đệ quy) · `bug-index.md` | ✅ 0 bug `.md` · index chưa tồn tại (đúng — `log-bug` NOT_STARTED) |
| `07_environments/environments.md` · `06_checklists/*` | ✅ |
| `00_input/v1.0/` (liệt kê file cho F-07/F-08) | ✅ 6 DOC-ID · 82 ảnh Figma khớp |
| `.claude/settings.json` · `.claude/hooks/` | ✅ |
| `10_source-code/` | ⬜ N/A — không tồn tại, đúng (`Automation Rules = N/A`) |

## Verified canonical counts

| Metric | Giá trị | Đối chiếu |
|---|---|---|
| REQ | **116** | Σ frontmatter `counts.req` = Σ table rows thực tế (11/11 module khớp, 0 lệch) |
| SC | **211** | Σ frontmatter `counts.sc` = Σ table rows thực tế (11/11 module khớp, 0 lệch) |
| CL | **35** (home-only, đúng quy ước router) | 40 dòng CL trên bảng thô (5 dòng thêm là "tham chiếu — home ở module khác", có nhãn rõ — không phải drift) |
| RISK | **64** | Σ frontmatter `counts.risk` = Σ table rows thực tế, khớp 100% |
| TC | **219** | TC Gen Log Σ 14+21+14+30+14+12+24+16+54+7+13 = 219 = số dòng `Testcase ID` thực trong sheet `ALL` của `TC-MASTER-v1.0.xlsx` (0 trùng ID, 0 ID sai format) |

**Kết luận:** mọi con số canonical (REQ/SC/CL/RISK/TC) khớp 100% xuyên suốt MASTER-MEMORY ↔ router ↔ module frontmatter ↔ TC Gen Log ↔ TC-MASTER thật.

## Pipeline Status (MASTER-MEMORY §8)

✅ 3 COMPLETED (`init-project`, `analyze-requirements`, `generate-tc`) · ❌ 1 COMPLETED-nhưng-REJECTED (`review-tc`, 0/100, G1 FAIL) · ⬜ 7 NOT_STARTED · ⏭️ 5 SKIPPED (no automation) · 0 IN_PROGRESS · 0 FAILED.

**A-01…A-05: PASS.** Không skill nào treo IN_PROGRESS; không FAILED; downstream của gate `review-tc` REJECTED (vibe-test, implement-automation, review-src-tc, execute-maintain, log-bug, sync-jira-bugs, test-report) đều đang NOT_STARTED/SKIPPED — **đúng hành vi**, không ai chạy vượt qua gate đã REJECTED, nên **không phải vi phạm A-02/A-03**. Active version `v1.0` khớp registry.

---

## Findings by Severity

### 🔴 CRITICAL (2)

#### [G-02] "12 sự kiện thông báo" vs "9 sự kiện NTF-01..09" — 1 con số, 2 giá trị không đối chiếu (tồn tại từ lượt trước, CHƯA fix)

- **`Project_rule.md §Module Codes` dòng `TC-10`:** *"...phân trang, **12 sự kiện** thông báo"*
- **`02_analyze-requirements/v1.0/MEMORY.md` §2 (Module Summary):** *"**9 sự kiện** `NTF-01..09`"*
- Bản thân `NTF-thong-bao/risk_assessment.md` + `CHANGELOG.md §2` **có** giải thích rành mạch: 9 = event chính thức theo BRD (`NTF-01..09`), 12 = số ứng viên gộp thêm từ `KP-07` (gồm cả hàng chỉ có ở Demo/Figma), còn chờ BA chốt (`C-NTF-01` Open) — nhưng lời giải thích đó **không được mang lên** 2 nơi tóm tắt cấp cao (`Project_rule` + router), nên người chỉ đọc 1 trong 2 file sẽ thấy 1 con số duy nhất, mâu thuẫn với file kia.
- **Vì sao CRITICAL** (không hạ xuống như lượt trước): `Project_rule.md` là file **mọi skill đọc trước tiên** — số sai ở đây có nguy cơ lan vào TC/report tương lai nếu ai đó viết thêm TC theo "12 sự kiện".
- **Fix:** sửa dòng `TC-10` thành *"9 sự kiện chính thức `NTF-01..09` (12 ứng viên gộp — chờ `C-NTF-01`)"*; router `§2` nên thêm chú thích tương tự.

#### [G-06b③] `07_environments/environments.md` còn nói "chờ env" trong khi env đã được CHỐT là N/A vĩnh viễn

- **Register primary (có ngày + người quyết):** `Project_rule.md §Test Data Rules` + `CLAUDE.md` — *"Base URL/endpoint = N/A — FoxEco là SDK nhúng trong host app FoxPro (`vn.fpt.ftel.sop.stg`), không có URL riêng"*. Đây **không phải** trạng thái "chưa xác định", mà là kết luận kiến trúc đã chốt.
- **Register kể lại (chưa cập nhật):** `07_environments/environments.md` vẫn giữ `URL / API URL / Database = TBD` — ngôn ngữ "chờ", đúng pattern G-06b③ mô tả (*"nơi nào còn ghi chưa deploy/chưa có URL/chờ env trong khi... đã Resolved"*). Bảng account cũng chỉ có 2 dòng generic `Admin/User` thay vì đúng 3 vai `SENDER/CARRIER/RECEIVER` mà `§Test Data Rules` yêu cầu.
- **Vì sao CRITICAL** (khác cách lượt trước xếp WARNING — nâng lại cho khớp bảng severity của chính skill): đây khớp đúng khuôn "tiền đề môi trường/hạ tầng" mà skill định nghĩa = CRITICAL, vì `vibe-test`/`execute-maintain` đọc trực tiếp file này — nếu chạy theo file này sẽ đi tìm URL không tồn tại.
- **Fix:** sửa `environments.md` theo `§Test Data Rules`: URL = N/A + ghi rõ package host app; bảng account đổi thành 3 vai; `~/.foxeco-v2/credentials.env` vẫn chưa tồn tại — cần tạo trước `vibe-test`.

---

### 🟡 WARNING (5)

#### [F-01] `DOC-v1.0-03` được khai 3 module (FEED/ASN/DLV) nhưng 0 citation thực

- `grep -rl "DOC-v1.0-03" */requirement_traceability.md` → rỗng. `ASN-ghep-noi/requirement_traceability.md` và `FEED-bang-tin/requirement_traceability.md` mô tả hành vi "prototype" nhiều chỗ nhưng không trích ID.
- Registry đã ghi chú *"reference-only, ⛔ không trích làm nguồn rule"* nên 0 citation hợp lý về nghiệp vụ, nhưng cột `Modules` khai 3 module là thông tin không kiểm chứng được.
- **Fix:** đổi `Modules` = `—` cho DOC reference-only, hoặc ghi rõ "3 module này là bề mặt mô tả, không phải nơi citation".

#### [F-08] 3 file trong `00_input/v1.0/Design/Fox Eco Doc/` chưa có DOC-ID (chưa fix từ lượt trước)

`canvas.fig` (nguồn Figma gốc) · `meta.json` · `thumbnail.png` — `DOC-v1.0-04` chỉ đăng ký `images/*`. **Fix:** mở rộng cột `File` của `DOC-v1.0-04` thành `Design/Fox Eco Doc/` hoặc thêm dòng loại trừ.

#### [G-03] Verbatim quote bị lặp nơi — vẫn còn, mẫu đại diện xác nhận

Luật: REQ quote → `requirement_traceability.md §2` là home duy nhất; `test_scenario_map.md` chỉ được **trỏ** tới khối REQ, không quote lại nguyên văn. Thực tế: `ORD-dang-tin` có ít nhất **49/90** REQ quote bị lặp verbatim sang `test_scenario_map.md` (vd *"Chọn vai trò đăng tin: Gửi hàng / Nhận giao hàng"*); `ACT-hoat-dong` cũng có ít nhất 1 cặp lặp (*"Tab Hoạt động | 'Đơn của tôi' — 2 tab con..."*). Khớp mô tả "66 cặp, nặng nhất NTF/ASN/ORD" của lượt trước — nợ này chưa được dọn.
**Fix:** `/analyze-requirements --update` — đổi quote ở `test_scenario_map.md` thành pointer `[[REQ-xxx]]`, giữ nguyên quote gốc ở traceability.

#### [G-06b①] `06_checklists/smoke-checklist.md` + `release-checklist.md` còn 100% template framework

`smoke-checklist.md` nhắc "Luồng quên mật khẩu" và "API endpoints (network tab)" — cả hai đều **không tồn tại** trong scope dự án (SSO qua host app, chưa có đặc tả API — `§Test Data Rules`: HTTP status/error.code/envelope = TBD). `[Luồng quan trọng 1..3]` chưa điền. `release-checklist.md` 0 từ khoá dự án.
**Fix:** điền 5 luồng Phase 1 thật vào smoke checklist hoặc ghi "chưa cấu hình" để không ai chạy nhầm bề mặt.

#### [H-03] `Project_rule.md` thiếu section bắt buộc `## Memory / Write-back Policy`

`grep -n "^## " Project_rule.md` liệt kê 15 section (Project Info … Custom Rules) nhưng **không có** `Memory / Write-back Policy` — section này bắt buộc vì hook `memory-guard.py` đọc trần ghi/bảng đích write-back ở đó; thiếu ⇒ hook rơi về trần mặc định của chính nó mà không cảnh báo ai. (`Online Sheet Integration` thiếu là hợp lệ — project không dùng review-tc-ba/sheet online.)
**Fix:** thêm section này vào `Project_rule.md`, tham khảo `~/.claude/skills/init-project/assets/project-rule-template.md`.

---

### 🔵 INFO (5)

| # | ID | Finding |
|---|---|---|
| 1 | **B-06** | Priority distribution lệch giữa frontmatter `counts:` và bảng SC thực — 4/11 module (`DLV` P1:5→thực 4, `FEED` P2:7/P3:5→thực 6/6, `HOME` P2:11/P3:12→thực 12/11, `NTF` P2:8/P3:7→thực 9/6). **Không ảnh hưởng downstream**: `generate-tc` đã tự xác nhận trong `CHANGELOG.md §2` là dùng priority per-row thực tế (không dùng frontmatter cũ) khi sinh TC — TC Gen Log per-module khớp bảng SC thật, chỉ frontmatter module là số cũ chưa đồng bộ. Fix nhẹ: `/analyze-requirements --update` 4 module này. |
| 2 | **C-04** | Không phát hiện drift giữa fragment `.md` và TC-MASTER — cả hai sinh cùng ngày 2026-09-07, đối chiếu mẫu (`TC-ACT-v1.0.md` = 14 dòng = sheet `ACT`) khớp. Ghi nhận informational, không phải finding thật. |
| 3 | **F-04** | 100% trong 219 TC ID dùng dạng `TC-<MODULE>-NNN` (vd `TC-ACT-001`), không có suffix `-[short-title]` như `§Naming Conventions` khai (`TC-[MODULE]-[NNN]-[short-title]`); tiêu đề nằm ở cột "Test Title" riêng. Áp dụng nhất quán 100% — nhiều khả năng là convention thật của project chưa được cập nhật vào bảng naming, không phải lỗi random. Fix: sửa pattern trong `§Naming Conventions` cho khớp thực tế, hoặc đổi ID nếu muốn theo đúng pattern đã khai. |
| 4 | **H-04** | `.claude/settings.json` wire `PostToolUse(Write\|Edit\|MultiEdit)` gọi thẳng `python3 .claude/hooks/memory-guard.py`, không qua wrapper `run-python.mjs` như convention framework mô tả — `run-python.mjs` **không tồn tại** trong `.claude/hooks/`. Hook vẫn chạy được (gọi trực tiếp), chỉ lệch pattern wiring tài liệu hoá. `Stop→validate-vibe-run.mjs` và `SessionStart→inject-project-rule.mjs` đều đúng. |
| 5 | **H-06** | `.claude/hooks/oracle_runs.py` chưa tồn tại — đúng, vì `package-version` chưa từng chạy (chỉ cần trước khi đóng gói version). Không raise WARNING theo đúng rule edge-case của skill. |

---

## Check đã chạy và SẠCH

| Group | Kết quả |
|---|---|
| **A** Pipeline Status | A-01…A-05 ✅ |
| **B** Scenario | B-01…B-05 ✅ (211 SC / 116 REQ / 64 RISK khớp 100% mọi nguồn), B-07 ✅ (0 DEPRECATED). B-06 → INFO #1. |
| **C** TC (nay áp dụng lần đầu) | **C-01…C-03, C-05…C-09 ✅ SẠCH TUYỆT ĐỐI** — 0 SC thiếu TC, 0 TC orphan, TC count khớp logged 219=219, 0 CARRIED (đúng, v1.0 đầu chuỗi), Lifecycle 219/219 = NEW khớp MASTER §3, Version Origin 219/219 = v1.0, Coverage Matrix/Technique tag vắng mặt đúng vì mode `standard`. review-tc REJECTED verdict (0/100, 36 Major·36 Minor·17 Info·0 Critical = 89) đối chiếu khớp `11_tc-review/review-report-v1.0.md` — **REJECTED là vì hình thức trình bày TC (pre-condition/expected/step), không phải vì data-consistency mà health-check kiểm.** |
| **D** Source code | ⏭️ N/A toàn bộ — `10_source-code/` chưa scaffold, đúng chủ đích |
| **E** Bug | E-01…E-07 ✅ — 0 bug `.md` (quét đệ quy), `bug-index.md` chưa tồn tại (đúng), 0 dòng FAIL-REGISTRY/INDEX, 0 vibe report |
| **F** Cross-ref | F-02 ✅, F-03 ✅ (6/6 DOC-ID đúng pattern), **F-05 ✅ 116/116 REQ có block Source Detail**, **F-06 ✅ 211/211 SC có Source Detail**, **F-07 ✅ 6/6 path registry resolve, 82/82 ảnh khớp** |
| **G** Governance | **G-01/G-08 ✅** router chỉ có §1+§2, không mọc lại §4/§9 · **G-05 ✅** 1 dòng/skill, không trùng · **G-06 ✅** không có report trùng loại mâu thuẫn · **G-07 ✅** không có `_global/`, không derived file · **G-04** chưa đánh giá hết (116 REQ × case-by-case, ngoài ngân sách lượt này — để ngỏ, không tính PASS) |
| **H** Constitution | H-01/H-02 ✅ (0 vibe run, không có gì để vi phạm) · **H-05 ✅** `verify_evidence.py` khớp 100% bản toolkit (diff rỗng) |

---

## Recommendation

**So với lượt trước:** Group C (TC Consistency) nay áp dụng lần đầu và **sạch tuyệt đối** — việc `generate-tc` sinh 219 TC từ 211 SC không có gap/orphan/count-drift nào. `review-tc` REJECTED (0/100) là vấn đề **chất lượng trình bày TC** (pre-condition lẫn setup, expected không verbatim, thiếu element trong step — 42+12+~20 TC theo 3 pattern chính), nằm ngoài phạm vi health-check nhưng **chặn pipeline thật** (G1 FAIL) — cần xử lý trước khi `vibe-test`.

**Thứ tự xử lý đề xuất:**

1. **2 CRITICAL trước tiên** (đều sửa tay, không cần chạy lại skill, ~10 phút): dòng `TC-10` của `Project_rule.md` (12→"9 chính thức, 12 ứng viên") · `07_environments/environments.md` (URL=N/A + 3 vai + xoá "mirror production" chưa xác nhận).
2. **Xử lý `review-tc` REJECTED** — đây là việc chặn pipeline thật sự, không phải health-check: sửa 42 TC pattern `R3-14` (Pre-condition⇄Setup) + 12 TC pattern verbatim/step, rồi `review-tc --recheck`.
3. **5 WARNING** — ưu tiên `H-03` (thêm section Memory/Write-back Policy, ảnh hưởng hành vi hook đang chạy ngầm) và `G-03` (nợ quote trùng nơi, càng để càng khó dọn qua version sau).
4. **Trước `vibe-test`:** vẫn cần tạo `~/.foxeco-v2/credentials.env` (`chmod 600`, `FOXECO_STG_USER`/`FOXECO_STG_PASS`) — chưa tồn tại.
5. **5 INFO** — sửa khi tiện, không chặn gì.

**Tổng: 2 CRITICAL · 5 WARNING · 5 INFO** (12 finding). Không có finding nào chỉ ra data-integrity thật sự bị hỏng — toàn bộ số canonical (REQ/SC/CL/RISK/TC) khớp 100%; CRITICAL đến từ 2 tài liệu tóm tắt cấp cao (Project_rule, environments.md) chưa phản ánh đúng quyết định đã chốt ở nơi khác.

---

## Remediation Log (2026-09-14)

> Chạy ngay sau report ở trên, theo yêu cầu user "fix tất cả kết quả health-check". Theo đúng `§Fix Routing` của skill: phần **sửa tay được** (registry/doc/config) do QC sửa trực tiếp; phần **thuộc trách nhiệm skill khác** (G-03 — dedupe quote thuộc `analyze-requirements`) được xử lý riêng, có kiểm chứng lại bằng script trước/sau, không sửa bằng cảm tính.

| # | Finding | Severity gốc | Hành động | File thay đổi | Kiểm chứng |
|---|---|---|---|---|---|
| 1 | **G-02** — 12 vs 9 sự kiện NTF | 🔴 CRITICAL | Sửa dòng `TC-10` trong `§Module Codes` thành "9 sự kiện chính thức `NTF-01..09` (12 ứng viên — chờ `C-NTF-01`)", khớp router | `Project_rule.md` | Đọc lại: 1 con số duy nhất, có chú thích 2 nguồn |
| 2 | **G-06b③** — `environments.md` còn "TBD" trong khi env đã chốt N/A | 🔴 CRITICAL | Viết lại theo `§Test Data Rules`: URL/API/DB = N/A + lý do (SDK nhúng host app), 3 vai SENDER/CARRIER/RECEIVER thay 2 dòng Admin/User generic | `07_environments/environments.md` | Đối chiếu câu chữ khớp `§Test Data Rules` |
| 3 | **F-01** — `DOC-v1.0-03` khai 3 module, 0 citation | 🟡 WARNING | Sửa cột `Modules` ghi rõ "*(mô tả, không citation)*", giải thích lý do reference-only trong cùng ô | `MASTER-MEMORY.md §2` | Đọc lại dòng registry |
| 4 | **F-08** — 3 file input chưa có DOC-ID | 🟡 WARNING | Mở rộng `DOC-v1.0-04` cột `File` từ `images/*` thành cả thư mục `Design/Fox Eco Doc/` (phủ `canvas.fig`/`meta.json`/`thumbnail.png`) | `MASTER-MEMORY.md §2` | 3 file nay nằm trong path đã đăng ký |
| 5 | **G-03** — 102 dòng quote REQ bị lặp verbatim ở `test_scenario_map.md` | 🟡 WARNING | Subagent xử lý 11 module: block trùng hoàn toàn → thay bằng pointer `*(quote đầy đủ ở requirement_traceability.md §2 REQ-xxx)*`; block trùng một phần → giữ dòng khác biệt, bỏ dòng trùng. `requirement_traceability.md`/`risk_assessment.md` giữ nguyên (đúng vai "home") | 11× `<MODULE>/test_scenario_map.md` | Script line-level trước/sau: **102 → 2** dòng trùng còn lại (2 dòng ở `DLV-giao-nhan` là excerpt có chủ đích, cùng mẫu đã có sẵn trong file — chấp nhận, không phải drift). Đã re-verify độc lập (không chỉ tin báo cáo của subagent). Sanity check bổ sung: 211/211 SC vẫn đủ Source Detail heading, frontmatter `sc:` vẫn khớp bảng thật ở cả 11 module — không có nội dung nào bị mất khi dọn quote |
| 6 | **G-06b①** — `06_checklists/*` còn 100% template, nhắc luồng không tồn tại | 🟡 WARNING | `smoke-checklist.md`: bỏ "quên mật khẩu"/"API network tab" (không áp dụng — SSO qua host app, chưa có đặc tả API), thay bằng 5 luồng Phase 1 thật (`KP-03 §3`: Đăng tin/Bảng tin/Ghép nối/Xác nhận nhận hàng/Quà cảm ơn) + ghi chú scope CNL/NTF/TS. `release-checklist.md`: gắn đúng gate G1-G4 của project thay vì mục chung chung | `06_checklists/smoke-checklist.md`, `06_checklists/release-checklist.md` | Đọc lại — không còn nhắc tính năng ngoài scope |
| 7 | **H-03** — thiếu section `## Memory / Write-back Policy` | 🟡 WARNING | Thêm section đầy đủ 4 mục (①trần dung lượng ②đích write-back ③nguồn canonical ④khối bất khả xâm phạm), khớp trần thật đang chạy trong `memory-guard.py` (60/90/250/16/130/200 KB). **Phát hiện thêm lúc sửa:** bản `memory-guard.py` của project đang trích dẫn tên section CŨ `§Memory Policy` (lệch bản toolkit hiện hành) — đồng bộ luôn theo `~/.claude/skills/init-project/assets/hooks/memory-guard.py` (diff → 0 sau khi sync) | `Project_rule.md`, `.claude/hooks/memory-guard.py` | `diff` với bản toolkit = rỗng |
| 8 | **B-06** — priority frontmatter lệch 4 module | 🔵 INFO | Tính lại tally thật bằng script (đếm cột Priority trên bảng SC, xử lý đúng ký tự `\|` escaped trong 2 ô dữ liệu), sửa `p1/p2/p3` trong frontmatter DLV/FEED/HOME/NTF + đồng bộ bảng roll-up + tổng số ở router `v1.0/MEMORY.md §2` (P1 28→27, P2 113→117, P3 70→67, vẫn cộng đúng 211) | `test_scenario_map.md` ×4 module, `v1.0/MEMORY.md §2` | Script đếm lại khớp 100% số đã ghi |
| 9 | **F-04** — TC ID thiếu suffix so với pattern khai | 🔵 INFO | Sửa pattern trong `§Naming Conventions` cho khớp thực tế (`TC-[MODULE]-[NNN]`, tiêu đề ở cột riêng) thay vì đổi 219 TC ID đang dùng nhất quán. Tiện thể bổ sung pattern còn thiếu cho `Clarification`/`Risk` (phát hiện từ lượt health-check 2026-09-07, chưa từng fix) | `Project_rule.md` | Đọc lại bảng naming |
| 10 | **H-04** — `PostToolUse` gọi thẳng `python3`, thiếu wrapper | 🔵 INFO | Copy `run-python.mjs` từ toolkit vào `.claude/hooks/`, sửa `settings.json` trỏ qua wrapper | `.claude/hooks/run-python.mjs` (mới), `.claude/settings.json` | Smoke-test `node run-python.mjs memory-guard.py < /dev/null` → exit 0 |
| 11 | **C-04** | 🔵 INFO | Không cần hành động — vốn đã là "không phát hiện drift" (informational, không phải lỗi) | — | — |
| 12 | **H-06** | 🔵 INFO | Không cần hành động — `oracle_runs.py` đúng là chưa cần tồn tại tới khi `package-version` chạy lần đầu | — | — |

**Ngoài phạm vi 12 finding (không tự ý đụng vào):**
- `review-tc` REJECTED (0/100, G1 FAIL) — đây là vấn đề trình bày TC (pre-condition⇄setup, expected không verbatim...), thuộc trách nhiệm sửa TC/`review-tc --recheck`, **không phải** artifact phân tích mà health-check kiểm tra. Chưa đụng vào 219 TC.
- `~/.foxeco-v2/credentials.env` vẫn chưa tồn tại — cần user tự tạo (chứa thông tin đăng nhập thật, ngoài phạm vi sửa file text).
- **Phát hiện phụ, chưa fix** (nằm ngoài 12 finding gốc, phát hiện trong lúc đối chiếu H-04/H-05): `.claude/hooks/validate-vibe-run.mjs` của project cũng đang hardcode `python3` (không qua `pyBin()` cross-platform như bản toolkit mới nhất) — cùng loại vấn đề với H-04 nhưng ở hook khác, chưa nằm trong 12 finding gốc nên **chưa sửa**, nêu ở đây để theo dõi.

**Kết quả sau remediation:** 10/12 finding đã xử lý trực tiếp (2 CRITICAL, 5 WARNING → 4 fixed nguyên vẹn + 1 (G-03) giảm từ 102 xuống 2 dòng chấp nhận được, 3 INFO fixed), 2 INFO không cần hành động. Số canonical (REQ 116 / SC 211 / CL 35 / RISK 64 / TC 219) xác nhận **không đổi** sau toàn bộ đợt sửa — mọi thay đổi là sửa văn bản/registry/hook, không đụng vào nội dung phân tích gốc.
