# MASTER-MEMORY — Cross-Version Registry

> Cập nhật lần cuối: 2026-09-15
> Active version: **v1.0** (thực thi/test) · **v1.1 đang DELTA analyze song song** — v1.0 pipeline (review-tc REJECTED, vibe-test/log-bug chưa chạy) vẫn còn dở nên KHÔNG áp dụng §10 Version Cutover; §8 dưới đây vẫn là bảng sống của v1.0.
>
> **⚠️ Tầng 1 (project) — ROUTER cross-version.** Chứa registry (version / DOC / TC-file / downstream path), quyết định cross-version. **KHÔNG chứa chi tiết SC/data/risk per-module** (sống ở tầng 3 module fragment). **KHÔNG lặp** cùng 1 bảng ở version `MEMORY.md`: §2 DOC Registry là **nguồn duy nhất** ở đây; §3 giữ **lifecycle cross-version**.

## 1. Version Registry
| Version | Release Date | Input Folder | Analyze Folder | Status | Tổng DOC | Tổng SC (all) | Tổng SC (new+mod) | Parent |
|---------|-------------|-------------|----------------|--------|----------|--------------|-------------------|--------|
| v1.0 | TBD | `00_input/v1.0/` | `02_analyze-requirements/v1.0/` | ANALYZED | 6 | 211 | 211 | — (version đầu của chuỗi phân tích mới) |
| v1.1 | TBD | `00_input/v1.1/` | `02_analyze-requirements/v1.1/` | IN_PROGRESS (delta analyze) | 2 | TBD (211 carried + Δ — cập nhật khi §8 dòng `analyze-requirements` chuyển COMPLETED) | Δ TBD | v1.0 |

> 📌 **v1.0 được PHÂN TÍCH LẠI TỪ ĐẦU ngày 2026-09-07** bằng bộ skill `qc-claude-v1 v1.1` (layout `module-first v2`, 11 module). Bản phân tích v1.0 **cũ** (bộ skill v1.0, layout `flat`, 8 module — 46 REQ / 92 SC / 323 TC) được lưu trữ ở `_handoff-v1.0/04_archive-project-v1.0/` và **KHÔNG phải parent** của bản này: cùng version, cùng tài liệu nguồn, khác phương pháp phân tích. ⛔ Không dùng archive làm baseline regression cho v1.0 (xem §9).

## 2. DOC ID Registry (Global)
> **`Status`** — trạng thái của FILE: `Active` = có trên disk trong `00_input/`, bản latest · `Superseded` = còn file nhưng đã có bản mới · `Removed <ngày>` = đã xoá khỏi working tree — **DOC-ID vẫn giữ**.
> ⚠️ **KHÔNG BAO GIỜ xoá dòng khỏi registry này.** Đổi `Status` + điền `Superseded by`.
> ⚠️ Đổi tên / gộp / xoá file input phải cập nhật cột `File` NGAY (`health-check` F-07).

| DOC ID | Version | File | Loại | Status | Superseded by | Modules |
|--------|---------|------|------|--------|---------------|---------|
| DOC-v1.0-01 | v1.0 | `Doc/FoxEco BRD v3.2.md` | Markdown — **BRD v3.2** (27/07/2026). **Nguồn nghiệp vụ chính, THẮNG khi mâu thuẫn về rule** | Active | — | USR, HOME, FEED, ORD, ACT, ASN, DLV, GIFT, CNL, NTF, TS |
| DOC-v1.0-02 | v1.0 | `Doc/tổng hợp từ file demo.docx` | Word — **PRD (Nháp)** tái dựng từ demo standalone. **THẮNG khi mô tả chi tiết màn hình/field**; ⛔ hành vi demo KHÔNG dùng làm oracle | Active | — | USR, HOME, FEED, ORD, ACT, ASN, DLV, GIFT, NTF |
| DOC-v1.0-03 | v1.0 | `Design/FoxEco Demo 3 vai tro (standalone) (2).html` | HTML — prototype tương tác 3 vai trò, **reference-only, ⛔ không trích làm nguồn rule** ⇒ cột `Modules` là **bề mặt prototype mô tả 3 màn này**, KHÔNG phải nơi citation — 0 citation trong `requirement_traceability.md` là ĐÚNG, không phải orphan | Active | — | FEED, ASN, DLV *(mô tả, không citation)* |
| DOC-v1.0-04 | v1.0 | `Design/Fox Eco Doc/` — gồm `images/*` (82 ảnh, nguồn UI chi tiết nhất) + `canvas.fig` (nguồn Figma gốc) + `meta.json` + `thumbnail.png` | Figma UI mockup. ⚠ status bar "9:41" = mẫu chuẩn Apple, **không phải screenshot máy thật** | Active | — | USR, HOME, FEED, ORD, DLV, GIFT, NTF |
| DOC-v1.0-05 | v1.0 | `Design/Screenshot From 2026-07-27 15-23-25.png` | Ảnh mockup màn Hoạt động (⚠ cùng cảnh báo "9:41") | Active | — | ACT |
| DOC-v1.0-06 | v1.0 | `_knowledge-pack/` (KP-01, 02, 03, 05, 06, 07 + `evidence/`) | Knowledge pack — kiến thức nghiệp vụ **NGOÀI tài liệu** (BA-chat · QA-obs · Figma · vibe-test). ⛔ KHÔNG là nguồn requirement gốc | Active | — | USR, HOME, FEED, ORD, ACT, ASN, DLV, GIFT, CNL, NTF, TS |
| DOC-v1.1-01 | v1.1 | `FoxEco PRD v1.0 - Gui Hang.pdf` | PDF — **PRD chính thức** (mã `1.0-BM/PM/HDCV/FTEL`, PRD Standard v1.2, rev 08/09/2026 "[A] Bổ sung flow exit giao hàng"). ⚠️ **Cùng tính năng "Gửi Hàng" đã phân tích ở v1.0** (khớp gần 1:1 cả 11 module qua FR01–FR18), KHÔNG phải sản phẩm mới — bản thân PRD tự nhận "MỚI HOÀN TOÀN" chỉ vì PM viết độc lập, không đối chiếu bộ phân tích v1.0. Chi tiết/chính thức hơn hẳn `DOC-v1.0-01/02` | Active | — | HOME, ASN, DLV, GIFT, CNL, NTF, TS, ORD, ACT (xem ghi chú USR dưới) |
| DOC-v1.1-02 | v1.1 | `FoxEco Demo 3 vai tro (standalone) v4.0 (1).html` | HTML — prototype 3 vai trò bản **v4.0** (kế thừa `DOC-v1.0-03`), reference-only ⛔ không trích làm nguồn rule | Active | — | (mô tả, không citation — như `DOC-v1.0-03`) |

**Ghi chú registry:**
- **`DOC-v1.1-01` không kéo `USR` vào delta.** FR15 của PRD đề xuất cho sửa SĐT/địa chỉ mặc định, xung đột trực tiếp với `SC-USR-003`/`C-USR-03` (v1.0 — màn Cá nhân view-only, resolved theo quan sát app STG). QC **GiangDC2 quyết định 2026-09-15: giữ nguyên view-only**, FR15 không áp dụng ở v1.1 ⇒ `USR-tai-khoan/` KHÔNG có delta, không tạo `v1.1/USR-tai-khoan/`. Quyết định ghi lại ở đây vì đây là nơi duy nhất so sánh 2 DOC — đừng hiểu nhầm là bị bỏ sót khi rà lại.
- **Đánh số giữ nguyên theo đợt v1.0 cũ** (01 = BRD · 02 = PRD demo · 03 = prototype HTML · 04 = ảnh Figma) để citation trong `_handoff-v1.0/04_archive-project-v1.0/` và `KP-04` còn đối chiếu được. `05` (screenshot) và `06` (knowledge pack) là DOC-ID **mới** của lượt này.
- **`DOC-v1.0-06` KHÔNG phải tài liệu yêu cầu.** Toàn bộ `§D3` Functional Requirements, `§D4` Business Rules, `§D1b` User Story + AC, `§D8` Validate rules nằm ở `DOC-v1.0-01`. KP chỉ chứa **phán quyết clarification** và **hành vi app thật** — dùng để quyết định khi 2 nguồn tài liệu mâu thuẫn.
- **Thứ tự thắng khi mâu thuẫn** (áp dụng suốt lượt phân tích này): (1) **`DOC-v1.0-06`** nếu có phán quyết BA/PO có ngày hoặc bằng chứng app/Figma cụ thể → (2) **`DOC-v1.0-01`** (BRD, bản mới nhất 27/07) → (3) **`DOC-v1.0-02`** (PRD demo) → (4) `DOC-v1.0-04`/`05` (mockup, chỉ đối chiếu cấu trúc) → (5) `DOC-v1.0-03` (prototype, reference-only). Mỗi lần áp thứ tự này đều ghi rõ ở Analyst Note của REQ/CL tương ứng.
- **BRD v3.1** (bản cũ hơn) **KHÔNG** nằm trong `00_input/` — lưu ở `_handoff-v1.0/04_archive-project-v1.0/docs-superseded/`, đúng rule input retention (chỉ bản latest trong input).
- **Lấy lại file đã xoá:** `git show <commit-trước-khi-xoá>:'00_input/v1.0/<path>'`.

## 3. Scenario Lifecycle (Cross-Version)
> Version ĐẦU (tất cả NEW) — dùng roll-up gọn theo Module. Từ version delta trở đi liệt kê per-SC cho MODIFIED/CARRIED/DEPRECATED.

| Module | Origin | Lifecycle | Count |
|--------|--------|-----------|-------|
| USR | v1.0 | NEW | 12 |
| HOME | v1.0 | NEW | 24 |
| FEED | v1.0 | NEW | 14 |
| ORD | v1.0 | NEW | 51 |
| ACT | v1.0 | NEW | 14 |
| ASN | v1.0 | NEW | 18 |
| DLV | v1.0 | NEW | 30 |
| GIFT | v1.0 | NEW | 12 |
| CNL | v1.0 | NEW | 13 |
| NTF | v1.0 | NEW | 16 |
| TS | v1.0 | NEW | 7 |
| **Tổng** | | | **211** |

## 4. Regression Scope
### v1.0
**Phải test (new + modified):** toàn bộ **211 SC** (version đầu của chuỗi phân tích mới — không có SC CARRIED).

**Nên regression (carried — high risk):** — *(không có: v1.0 không có parent trong chuỗi phân tích mới)*

**Không cần test (carried — low risk, stable):** — *(không có)*

> 📌 **Bộ TC baseline của đợt v1.0 cũ (323 TC) KHÔNG được dùng làm regression scope.** Lý do: (a) **0/323 TC có Scenario ID** (`_handoff-v1.0/03_tc-baseline-v1.0/TC-SC-MAPPING-TODO.md`) ⇒ không map được sang 211 SC mới; (b) bộ TC cũ có **5 lỗi đã biết** (`KP-04 §4`); (c) chỉ **~17/323 TC** từng chạy thật trên app. ⇒ Quyết định 2026-09-07: coi trạng thái hiện tại là **baseline mới**, chuỗi `--delta` bắt đầu từ version kế tiếp.

## 5. Version Comparison
*(Từ v2.0 trở đi)*

## 6. TC Files Registry
| Version | TC-MASTER File | Tổng TC | Ngày consolidate | Status |
|---------|---------------|---------|-------------------|--------|
| v1.0 | `03_test-cases/v1.0/TC-MASTER-v1.0.xlsx` | 219 | 2026-09-07 | ✅ Consolidated · ❌ **Review 0/100 REJECTED** (2026-09-07, G1 FAIL) — 13 sheet (Overview + ALL + 11 sheet module). Bản copy: `03_test-cases/TC-MASTER-LATEST.xlsx` |

> 📌 Bộ TC của đợt v1.0 **cũ** (323 TC, schema 16 cột đã convert) lưu ở `_handoff-v1.0/03_tc-baseline-v1.0/` — **KHÔNG** đưa vào `03_test-cases/v1.0/` (xem §4).

## 7. Downstream Path Registry
| Skill | Active Version Path |
|-------|-------------------|
| analyze-requirements | `02_analyze-requirements/v1.0/` (router `MEMORY.md` + 11 module) |
| generate-tc | `03_test-cases/v1.0/` (fragments `.md` + `TC-MASTER-v1.0.xlsx`) |
| export-tc-rp | `03_test-cases/v1.0/exports/` (phase design) · `09_reports/` (phase report) |
| review-tc | `11_tc-review/` |
| vibe-test | `08_test-runs/vibe/` |
| execute-maintain | `08_test-runs/` |
| log-bug | `05_bug-reports/draft/` · `05_bug-reports/jira/` (recursive) |
| test-report | `09_reports/` |
| scan-source-code / implement-automation | `10_source-code/` — **N/A** (project manual, chưa scaffold) |

## 8. Pipeline Status — v1.0
> Thứ tự + tên skill khớp `PIPELINE.md §2 Skill Registry`. Status ∈ NOT_STARTED / IN_PROGRESS / PARTIAL / COMPLETED / SKIPPED / FAILED.
> **CURRENT-STATE, OVERWRITE — đúng 1 dòng / skill.** ⛔ KHÔNG append thêm dòng cho mỗi lần chạy lại.

| # | Skill | Status | Last Run | Scope | Output | Notes |
|---|-------|--------|----------|-------|--------|-------|
| 0.5 | init-source-code | SKIPPED | — | — | — | Project chạy manual — không có automation (`Project_rule §Automation Rules` = N/A) |
| 1 | init-project | COMPLETED | 2026-09-07 | — | CLAUDE.md / PIPELINE.md / COMMANDS.md / Project_rule.md | Seed thêm 11 module codes + DOC notation + Custom Rules §10.1/§10.2 ngày 2026-09-07 |
| 2 | create-test-plan | NOT_STARTED | — | — | — | Không phải hard prerequisite của analyze |
| 3 | analyze-requirements | COMPLETED | 2026-09-07 | v1.0 · 11/11 module | `02_analyze-requirements/v1.0/` — router + **11 × 5 file** | INIT lại từ đầu theo bộ skill v1.1 (`module-first v2`). 116 REQ · 211 SC · 35 CL (17 Open, **0 blocker**) · 64 RISK |
| 4 | generate-tc | COMPLETED | 2026-09-07 | v1.0 · 11/11 module · mode `standard` | `03_test-cases/v1.0/` — `TC-MASTER-v1.0.xlsx` + 11 fragment `.md` + `CHANGELOG.md` | **219 TC** (P1 27 · P2 123 · P3 69) phủ **211/211 SC** · 0 SC hở · 0 TC trùng/orphan. Consolidate 2026-09-07. 13 TC **dự kiến FAIL có chủ đích** — xem `03_test-cases/v1.0/CHANGELOG.md §2` ràng buộc 6 |
| 4b | export-tc-rp | NOT_STARTED | — | — | — | Renderer deliverable FPT — chạy sau consolidate |
| 5 | review-tc | COMPLETED | 2026-09-07 | v1.0 · FULL · 219 TC · 4 reviewer context-độc-lập (R1+R4 · R2 · R3×2) | `11_tc-review/review-report-v1.0.md` | ❌ **Score 0/100 — REJECTED · G1 FAIL ⇒ block downstream.** 0 Critical · 36 Major · 36 Minor · 17 Info (89 finding, severity chuẩn hoá theo catalog). Major dồn ở 3 pattern hình thức: `R3-14` 42 TC (Pre-condition ⇄ Setup) · `R3-02`+`R3-17` 12 TC (Expected không verbatim / có "hoặc") · `R3-01`+`R3-09`+`R3-03` (step thiếu element/giá trị). Coverage sạch: 211/211 SC · 0 orphan · 0 Critical structural. ⚠️ Không có `ANTHROPIC_API_KEY` ⇒ không gọi API instance, cap 85 áp nhưng vô hiệu |
| 6 | scan-source-code | SKIPPED | — | — | — | Không có automation |
| 7 | vibe-test | NOT_STARTED | — | — | — | **Nên chạy TRƯỚC generate-tc** cho `ACT` (`KB-ORD-07`) và `DLV` (15 ô ma trận) — xem §9 |
| 8 | implement-automation | SKIPPED | — | — | — | Không có automation |
| 9 | review-src-tc | SKIPPED | — | — | — | Không có automation |
| 10 | execute-maintain | SKIPPED | — | — | — | Không có automation — execute thủ công / qua `vibe-test` |
| 11 | log-bug | NOT_STARTED | — | — | — | **≥9 bug/nghi vấn bug đã biết chưa log** (`KP-05 §5`) — xem §9 |
| 11b | sync-jira-bugs | NOT_STARTED | — | — | — | ⛔ Jira **chưa cấu hình** (`Project_rule §Jira Integration` còn comment) |
| 12 | test-report | NOT_STARTED | — | — | — | Phải nêu rõ nhánh Admin (`§D4` cột Admin) ngoài phạm vi v1.0 |
| 13 | health-check | COMPLETED | 2026-09-14 | FULL · toàn repo + remediation pass cùng ngày | `09_reports/health-check/health-check-2026-09-14.md` (kèm `## Remediation Log`) | **12 finding gốc (2 CRITICAL · 5 WARNING · 5 INFO) → 10 đã fix, 2 vốn không cần hành động.** Số canonical không đổi sau fix (211 SC / 116 REQ / 35 CL / 64 RISK / 219 TC). G-03 quote trùng: 102→2 dòng (2 dòng còn lại là excerpt chủ đích). Đồng bộ thêm `memory-guard.py` + thêm `run-python.mjs` theo bản toolkit. **Còn treo ngoài phạm vi health-check:** `review-tc` REJECTED (0/100) chặn `vibe-test` thật — chưa xử lý; `validate-vibe-run.mjs` cũng hardcode `python3` như H-04 nhưng chưa fix (phát hiện phụ, xem Remediation Log) |

## 9. Notes (quyết định cross-version — KHÔNG phải per-run count log)

**Quyết định phương pháp (2026-09-07, QC GiangDC2):**
1. **Phân tích lại v1.0 từ đầu** bằng bộ skill v1.1 thay vì migrate bản phân tích cũ — vì bản cũ dùng layout `flat` (MEMORY.md 193 KB monolith, drift số đếm nhiều lần) và mang 5 lỗi đã biết (`KP-04 §4`).
2. **Tách 11 module** thay 8 mã domain của đợt cũ: thêm `HOME` · `FEED` · `ACT` để **module ↔ fragment ↔ sheet `export-tc-rp`** thành 1:1. Đợt cũ để `ORD` gánh 3 màn (33 SC / 161 TC) và `ASN` gánh Bảng tin (2 SC / 31 TC).
3. **Scope = toàn bộ 11 module**, không giới hạn 5 luồng Phase 1 mà PM chốt (`KP-03 §3`). ⚠️ `CNL` · `NTF` · `TS` được PM xếp **out of scope Phase 1** — cần **xác nhận lại với PM trước khi execute** (36 SC thuộc 3 module này).
4. **Chạy trên tài liệu hiện có** (BRD v3.2 + PRD tái dựng từ demo). PRD version mới của PM khi có ⇒ chạy `/analyze-requirements --delta --version <next>`, **không** ghi đè v1.0.
5. **Không dùng bộ TC cũ (323 TC) làm regression baseline** — lý do đầy đủ ở §4.
6. **Tên thư mục module = `<CODE>-<slug>`** (đổi 2026-09-07, trước khi chạy `generate-tc`): `USR-tai-khoan` · `HOME-trang-chu` · `FEED-bang-tin` · `ORD-dang-tin` · `ACT-hoat-dong` · `ASN-ghep-noi` · `DLV-giao-nhan` · `GIFT-qua-cam-on` · `CNL-huy-don` · `NTF-thong-bao` · `TS-trust-safety`. Framework tách sẵn `module.code` (token ID) khỏi `module.dir` (thư mục) nên **ID không đổi một ký tự**. ⚠️ **Áp cho mọi version sau** — mở v1.1/v2.0 thì dùng đúng bộ `Dir` này, ⛔ không quay về tên thư mục chỉ có mã. Cột `Dir` canonical ở `Project_rule.md §Module Codes`; lịch sử per-module ở `<Dir>/CHANGELOG.md §1` (dòng `REFACTOR` 2026-09-07).

**Số liệu đông cứng theo mốc 2026-09-07** *(⚠ không phải số current — số current đọc ở `v1.0/MEMORY.md §2`, canonical ở frontmatter module)*:
- 116 REQ · 211 SC (211 NEW) · 35 CL (17 Open · 0 blocker) · 64 RISK · 11 module.
- **111/116 REQ có ≥1 SC**; 5 REQ gap chủ đích (`REQ-DLV-011..014`, `REQ-CNL-007`) — lý do ở `<module>/CHANGELOG.md §3`.
- ⚠️ **211 SC vượt ngưỡng gợi ý 200 SC/version** của skill (`SKILL.md §Common Edge Cases`). Đã áp cả 2 biện pháp mà skill đề xuất: **(a)** split — 11 module thay 8; **(b)** giảm rác — 5 REQ để gap chủ đích thay vì tạo SC, và altitude SC ở form nhiều trường dừng ở mức rule (EP/BVA từng trường để `generate-tc` fan-out, xem `ORD-dang-tin/CHANGELOG.md §2` ràng buộc 8). Con số 211 là **hệ quả của scope "toàn bộ 11 module" + fan-out đúng luật** (riêng ma trận `DLV` 15 ô đã là 15 SC), không phải SC rác. ⇒ Nếu cần giảm: cắt scope 3 module out-of-scope Phase 1 (`CNL` 13 + `NTF` 16 + `TS` 7 = **36 SC**) → còn 175 SC.

**So sánh với đợt phân tích v1.0 CŨ** *(reference-only — nguồn `_handoff-v1.0/02_seed/KP-04`)*:
| | Đợt cũ (skill v1.0, flat) | Lượt này (skill v1.1, module-first v2) |
|---|---|---|
| Module | 8 | **11** |
| REQ | 46 | **116** |
| SC | 92 (91 hiệu lực + 1 DEPRECATED) | **211** |
| Clarification | 25 | **35** (kế thừa 25 + mở mới 10) |
| Bề mặt thiếu SC nặng nhất | Trang chủ 1 SC/32 TC · Bảng tin 2 SC/31 TC · `DLV` 14 SC cho ma trận 15 ô | `HOME` 24 SC · `FEED` 14 SC · `DLV` 30 SC (15 ô = 15 SC) |

**Nợ cross-version cần xử lý trước khi execute:**
- 🔴 **≥9 bug/nghi vấn bug đã biết mà đợt cũ CHƯA log Jira** (`KP-05 §5`): lộ SĐT trước ghép · chủ tin tự nhận đơn · Tên người gửi không read-only + bị xoá trắng · địa chỉ lấy hàng không pre-fill · SĐT tự đổi giữa phiên · app báo lỗi SĐT nó tự auto-fill · `VAL-04` không enforce (2 lỗi) · log LỊCH SỬ khi huỷ (2 lỗi). ⇒ Jira **chưa cấu hình** ⇒ cần bật `Project_rule §Jira Integration` trước khi `/log-bug --push-jira`.
- 🔴 **Vibe-test nên chạy TRƯỚC `generate-tc`** cho 2 module có nguồn mỏng/cũ: `ACT` (6/9 REQ chỉ dựa 1 lượt `QA-obs` 2026-07-27) và `DLV` (15 ô ma trận từ `QA-obs` + Figma 2026-07-24). Nếu app đã đổi nhãn thì 15 SC của `DLV` FAIL hàng loạt vì lý do không phải bug.
- 🟡 **6 CL ưu tiên hỏi BA** (bảng ở `v1.0/MEMORY.md §2`) — đứng đầu là `C-ORD-09` (danh mục "Loại hàng": app không có chip "Tài liệu").
- 🟡 **Câu hỏi mới phát sinh ở lượt này** (chưa từng có ở đợt cũ): rule `§A8` yêu cầu consent *"trước khi đăng/**ghép**"* nhưng luồng ghép chỉ có modal xác nhận lộ SĐT — có phải **gap tuân thủ pháp lý**? (`TS-trust-safety/risk_assessment.md` `RISK-TS-04`).

## 10. Version Cutover — Compaction Rule
> Khi mở version mới (v1.0 → v1.1/v2.0):
> 1. **Archive** append-log cũ sang file lịch sử; §8 Pipeline Status **reset** về NOT_STARTED cho version mới.
> 2. **Không mang** số current của version cũ sang — recompute cho version mới từ frontmatter `counts:` của module.
> 3. Số "đông cứng theo mốc" ở §9 giữ nguyên (có nhãn ngày), ⛔ KHÔNG "sửa cho khớp" version mới.
> 4. Chạy `health-check` xác nhận: 0 drift count · 0 router-tier chứa nội dung leaf · 0 orphan reference.
