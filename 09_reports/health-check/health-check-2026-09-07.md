# Health Check Report — foxeco-v2 · v1.0

> Generated: 2026-09-07 · Mode: **FULL** · Run by: GiangDC2
> Layout dò được: **analyze = module-first v2** (có `<Dir>/CHANGELOG.md`) · **runs = v2** (`08_test-runs/runs/`)
> Mode TC (suy từ artifact): **standard** — không có TC-MASTER, không có Technique tag, không có Coverage Matrix ⇒ **C-08/C-09 không áp**

## Files checked

| Nguồn | Trạng thái |
|---|---|
| `PIPELINE.md` · `CLAUDE.md` · `COMMANDS.md` | ✅ |
| `02_analyze-requirements/MASTER-MEMORY.md` · `Project_rule.md` | ✅ |
| `02_analyze-requirements/v1.0/MEMORY.md` (router) + **11 module × 5 file = 55 file** | ✅ |
| `08_test-runs/runs/{INDEX.md, FAIL-REGISTRY.md}` | ✅ (template rỗng — 0 dòng RUN/FAIL) |
| `07_environments/environments.md` · `.claude/settings.json` · `.claude/hooks/` | ✅ |
| `00_input/v1.0/` (liệt kê file cho F-07/F-08) | ✅ 6 DOC-ID · 82 ảnh Figma |
| `03_test-cases/v1.0/TC-MASTER-v1.0.xlsx` | ⬜ [MISSING] — `generate-tc` NOT_STARTED |
| `03_test-cases/v1.0/CHANGELOG.md` (TC Gen Log) | ⬜ [MISSING] — chưa có lượt generate |
| `05_bug-reports/bug-index.md` | ⬜ [MISSING] — `log-bug` NOT_STARTED |
| `10_source-code/MEMORY.md` | ⬜ [MISSING] — project manual, `SKIPPED` có chủ đích |

## Pipeline Status (MASTER-MEMORY §8)

✅ 2 COMPLETED (`init-project`, `analyze-requirements`) · ⬜ 8 NOT_STARTED · ⏭️ 5 SKIPPED (no automation) · 0 IN_PROGRESS · 0 FAILED

Không anomaly: **A-01** (0 skill treo IN_PROGRESS) · **A-02** (0 FAILED) · **A-03** (0 downstream chạy trước upstream) · **A-04** (§8 tồn tại, 16 skill đủ) · **A-05** (active version `v1.0` khớp registry).

---

## Findings by Severity

### 🔴 CRITICAL (0)

Không có. Pipeline đi tiếp được.

---

### 🟡 WARNING (6)

#### [G-03] 84 Source Quote bị lặp nơi — vi phạm luật "1 quote 1 home"

- **Luật (layout v2):** REQ quote → `requirement_traceability.md §2` · SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`. ⛔ **SC chỉ TRỎ tới khối REQ, cấm quote lại.**
- **Thực tế:** 84 blockquote xuất hiện ở ≥2 file. Phân bố cặp file:

| Số quote | Cặp file |
|--:|---|
| 66 | `requirement_traceability` ↔ `test_scenario_map` ← **đúng dạng luật cấm** |
| 5 | `requirement_traceability` ↔ `risk_assessment` ↔ `test_scenario_map` |
| 4 | `requirement_traceability` ↔ `requirement_traceability` (2 module khác nhau) |
| 4 + 2 | biến thể 3–4 file |
| 2 | `requirement_traceability` ↔ `risk_assessment` |
| 1 | `test_scenario_map` ↔ `test_scenario_map` |

- **Phạm vi:** 71 trùng **trong cùng module**, 13 trùng **chéo module**. Nặng nhất: `NTF-thong-bao` 27 · `ASN-ghep-noi` 26 · `ORD-dang-tin` 24.
- **Impact:** `export-tc-rp` parse heading `REQ-*` trong traceability để dựng cột RTM — quote trùng ở scenario_map làm nguồn RTM mờ, và mỗi lần sửa nguyên văn phải sửa 2 chỗ (đây chính là cơ chế sinh drift).
- **Fix:** `/analyze-requirements --update` — đổi quote ở `test_scenario_map.md` thành pointer tới khối `REQ-*` trong traceability, giữ nguyên quote gốc ở home.

#### [F-08] 3 file trong `00_input/` chưa có DOC-ID

| File | Ghi chú |
|---|---|
| `Design/Fox Eco Doc/canvas.fig` | **File nguồn Figma** của bộ 82 ảnh — đáng chú ý nhất |
| `Design/Fox Eco Doc/meta.json` | metadata export |
| `Design/Fox Eco Doc/thumbnail.png` | ảnh thumbnail |

- **Nguyên nhân:** `DOC-v1.0-04` chỉ đăng ký `Design/Fox Eco Doc/images/*` (82 ảnh), không phủ 3 file cùng thư mục.
- **Impact:** file input tồn tại mà không có ID để cite; nếu ai đó mở `canvas.fig` lấy thông số UI thì không có đường trích dẫn hợp lệ.
- **Fix:** sửa tay cột `File` của `DOC-v1.0-04` (mở rộng thành `Design/Fox Eco Doc/`) hoặc thêm ghi chú loại trừ rõ ràng dưới registry. ⛔ Không chạy lại analyze để "tự sửa".

#### [F-01] `DOC-v1.0-03` được khai 3 module nhưng 0 citation

- **Registry (`MASTER-MEMORY §2` + router frontmatter):** `modules: [FEED, ASN, DLV]`.
- **Thực tế:** 0/11 file `requirement_traceability.md` reference `DOC-v1.0-03`.
- **Bối cảnh:** registry cũng ghi *"reference-only, ⛔ không trích làm nguồn rule"* ⇒ 0 citation là **hợp lý về nghiệp vụ**, nhưng khi đó cột `Modules` khai 3 module là **thông tin không kiểm chứng được**.
- **Fix:** để `Modules` = `—` cho DOC reference-only, hoặc thêm 1 câu ở registry: *"3 module này là bề mặt prototype mô tả, không phải nơi citation"*.

#### [G-02] "12 sự kiện thông báo" vs "9 sự kiện `NTF-01..09`" — 1 con số, 2 giá trị

| Nguồn | Giá trị |
|---|---|
| `Project_rule.md §Module Codes` dòng `TC-10 / NTF` | *"…phân trang, **12 sự kiện** thông báo"* |
| `v1.0/MEMORY.md §1` + `NTF-thong-bao/*` | *"**9 sự kiện** `NTF-01..09`"* |
| `C-NTF-01` (Open) | 9 loại chính thức · **12 hàng ứng viên** ở `KP-07` |

- **Impact:** `Project_rule` là file mọi skill đọc trước ⇒ số 12 (thực chất là số ứng viên chưa chốt) đang nằm ở nguồn có thẩm quyền cao nhất.
- **Fix:** sửa dòng `TC-10` thành *"9 sự kiện `NTF-01..09` (12 ứng viên — chờ `C-NTF-01`)"*.

#### [G-06b③] `07_environments/environments.md` còn template, nói ngược `§Test Data Rules`

| Register | Nội dung |
|---|---|
| `Project_rule §Test Data Rules` (primary, có ngày) | Base URL = **N/A** — SDK nhúng trong host app `vn.fpt.ftel.sop.stg`; cần **3 vai** SENDER · CARRIER · RECEIVER |
| `07_environments/environments.md` (chưa cập nhật) | `URL / API URL / Database = TBD` · *"Dữ liệu mirror từ production (đã ẩn danh)"* · bảng account chỉ có 2 dòng **Admin / User** |

- **Impact:** `vibe-test` + `execute-maintain` đọc env file; 2 vai placeholder không tồn tại trong dự án, còn 3 vai thật thì không có chỗ khai. Thêm nữa `~/.foxeco-v2/credentials.env` **chưa tồn tại** (`FOXECO_STG_USER` / `FOXECO_STG_PASS`).
- **Fix:** sửa `environments.md` theo primary: URL = N/A + package host app, bảng account đổi thành 3 vai, xoá câu "mirror từ production" nếu chưa xác nhận.

#### [G-06b①] `06_checklists/*` còn 100% template framework

- `smoke-checklist.md`: *"Luồng quên mật khẩu hoạt động"*, *"API endpoints phản hồi (kiểm tra network tab)"*, `[Luồng quan trọng 1..3]` chưa điền.
- `release-checklist.md`: 0 từ khoá dự án.
- **Mâu thuẫn:** dự án là **SDK trong app mobile, SSO qua host app FoxPro** (không có luồng quên mật khẩu thuộc scope) và **chưa có đặc tả API** (`§Test Data Rules`: HTTP status / error.code / envelope = TBD).
- **Fix:** điền 5 luồng Phase 1 vào smoke checklist, hoặc ghi rõ *"chưa cấu hình"* để không ai chạy checklist sai bề mặt.

---

### 🔵 INFO (7)

| # | ID | Finding |
|---|---|---|
| 1 | **C-01** | **211/211 SC chưa có TC** — đúng trạng thái pipeline (`generate-tc` NOT_STARTED), **không phải lỗi dữ liệu**. Sẽ thành WARNING thật nếu còn tồn sau lượt generate. |
| 2 | **F-04** | `§Naming Conventions` **không khai pattern** cho Clarification (`C-<MODULE>-NN`, dùng 649 lần) và Risk (`RISK-<MODULE>-NN`, dùng 122 lần). Convention đang dùng nhất quán nhưng không có nguồn chuẩn để đối chiếu. |
| 3 | **F-02** | `DLV-giao-nhan/CHANGELOG.md §3` mô tả 3 REQ gap bằng **ID tài liệu gốc** (`PUP-03` · `GPS-01` · `COST-01`) thay vì REQ ID ⇒ tra `REQ-DLV-012/013/014` trong §3 không ra. Ngoài ra `REQ-DLV-015` có SC ở module khác (`SC-CNL-005`) nên không tính vào `req_without_sc: 4` — đúng, nhưng nên ghi rõ để người sau không nghĩ là bỏ sót. |
| 4 | **G-02** (nhẹ) | *"CL còn OPEN — 17/35"* phụ thuộc cách xếp `C-NTF-03` (🟡 `(a) Open · (b) N/A`); grep `Open` ra **18** dòng. Nên ghi *"17 Open + 1 partial"*. |
| 5 | **CL notation** | `FEED-bang-tin/risk_assessment.md` dòng `C-ORD-06` **thiếu nhãn** `(tham chiếu — home ở ACT)` như các module khác ⇒ đếm máy ra 4 CL home thay vì 3. Frontmatter `cl: 3` **đúng**; chỉ lệch notation. |
| 6 | **PIPELINE §4** | Bảng snapshot lệch bản live (`analyze-requirements` ghi NOT_STARTED, live = COMPLETED). Banner đã khai *"MASTER-MEMORY §8 thắng"* nên không nâng severity — nhưng nên thêm **ngày chụp** hoặc xoá bảng để người mới không đọc số cũ. |
| 7 | **H-04** | `.claude/hooks/verify_evidence.py` **có trên đĩa nhưng chưa wire** trong `.claude/settings.json` (hiện wire `Stop` · `SessionStart` · `PostToolUse` cho `inject-project-rule` · `validate-vibe-run` · `memory-guard`). Gate evidence chỉ chạy khi `vibe-test` tự gọi script. |


### 🔵 INFO bổ sung — phát hiện trong lượt `generate-tc` cùng ngày

#### [B-06] Priority distribution lệch giữa frontmatter `counts:` và bảng SC — 4/11 module

| Module | frontmatter `p1/p2/p3` | đếm thực tế trên bảng SC | lệch |
|---|---|---|---|
| `DLV-giao-nhan` | 5 / 22 / 3 | **4 / 25 / 1** | 3 SC |
| `FEED-bang-tin` | 2 / 7 / 5 | **2 / 6 / 6** | 1 SC |
| `HOME-trang-chu` | 1 / 11 / 12 | **1 / 12 / 11** | 1 SC |
| `NTF-thong-bao` | 1 / 8 / 7 | **1 / 9 / 6** | 1 SC |

- **Tổng SC không đổi** ở cả 4 module (30 / 14 / 24 / 16) ⇒ không ảnh hưởng B-01/B-05; chỉ lệch **phân bổ**.
- `DLV` lệch cả **P1** (5 khai vs 4 thực) ⇒ ảnh hưởng mẫu số **Quality Gate G2** (*"P1 TC đã execute = 100%"*) và `§Tổng quan` dòng 37 của chính file scenario map cũng ghi 5.
- **Xử lý ở lượt generate-tc:** TC lấy priority theo **từng dòng SC** (giá trị per-item, có Analyst Note biện minh — vd `SC-DLV-021/023` ghi rõ *"P1 vì…"*), KHÔNG lấy theo aggregate.
- **Fix:** `/analyze-requirements --update` cho 4 module — sửa `counts:` cho khớp bảng SC (hoặc sửa priority của SC nếu aggregate mới là ý định), rồi đồng bộ router `§2` + `MASTER-MEMORY`. ⛔ generate-tc không tự sửa artifact analyze.

---

## Check đã chạy và SẠCH

| Group | Kết quả |
|---|---|
| **A** Pipeline Status | A-01…A-05 ✅ (16 skill, 1 dòng/skill, 0 treo, 0 FAILED) |
| **B** Scenario | B-01…B-07 ✅ — frontmatter `counts:` **khớp 100%** nội dung: SC 211/211, REQ 116/116, RISK 64/64, CL 35 unique. Roll-up `MASTER §3` khớp canonical **từng module**. `P1+P2+P3 = 28+113+70 = 211 = Tổng SC` (0 DEPRECATED) |
| **C** TC | C-02…C-07 ⏭️ N/A (chưa có TC-MASTER) · C-08/C-09 không áp (mode `standard`) · C-01 → INFO #1 |
| **D** Source code | ⏭️ N/A — project manual, `10_source-code/` chưa scaffold (SKIPPED có chủ đích) |
| **E** Bug | E-01…E-07 ✅ — 0 bug `.md` (quét **đệ quy** `jira/**` + `draft/**`), 0 dòng FAIL-REGISTRY, 0 `RUN-*.md`; **E-06** 0 ID trùng · **E-07** consumer đọc 0 **khớp** đĩa 0 (không phải xanh giả) |
| **F** Cross-ref | F-03 ✅ (6/6 DOC-ID đúng pattern) · **F-05 ✅ 116/116 REQ có block Source Detail** · **F-06 ✅ 11/11 scenario_map có section Source Detail** · **F-07 ✅ 6/6 path registry resolve trên đĩa, `images/` đúng 82 ảnh** |
| **G** Governance | **G-01 ✅** router chỉ có §1 Function Register + §2 Module Summary (+2 phụ lục luật) · **G-08 ✅** không có §4/§9 mọc lại, 0 banner *"Cập nhật lần cuối"* trong deliverable · **G-05 ✅** 1 dòng/skill · **G-07 ✅** N/A (không có `_global/`) · **G-06b②** ✅ 0 dòng `BLOCKING`, khớp tuyên bố *"0 blocker"* của router · **G-06b①** scope: `RISK-CNL-06` + `RISK-NTF-06` ghi đúng trạng thái *"PM xếp out-of-scope Phase 1, Pending xác nhận"*, khớp `MASTER §9 #3` |
| **H** Constitution | **H-01/H-02** ⏭️ N/A — 0 vibe run trong `08_test-runs/vibe/` (evidence `VR-001`/`VR-002` nằm trong `00_input/_knowledge-pack/` = archive đóng băng của đợt cũ, không phải run của project này) · **H-03 ✅** 8/8 section bắt buộc của `Project_rule` đủ · **H-05 ✅** `verify_evidence.py` khớp bản toolkit |

### Kiểm bổ sung — đổi tên thư mục module (2026-09-07)

| Phép kiểm | Kết quả |
|---|---|
| 11 thư mục trên đĩa khớp cột `Dir` của `§Module Codes` | ✅ 11/11 |
| frontmatter `id:` + `module.dir` khớp tên thư mục thật | ✅ 55/55 file |
| link cột `Dir` ở router §1 resolve | ✅ 11/11 |
| cross-ref `<Dir>/<file>.md` chết | ✅ 0 |
| ID bị nhiễm slug (`SC-ORD-dang-tin-*`) | ✅ 0 (1 hit duy nhất là **ví dụ phản chứng** trong ghi chú router) |

---

## Recommendation

**Thứ tự xử lý trước khi chạy `generate-tc`:**

1. **Sửa tay 4 finding rẻ, không cần chạy skill** (≈15 phút): `Project_rule` dòng `TC-10` (12→9 sự kiện) · `MASTER-MEMORY §2` cột `File` của `DOC-v1.0-04` + cột `Modules` của `DOC-v1.0-03` · `07_environments/environments.md` theo `§Test Data Rules` · thêm pattern `C-`/`RISK-` vào `§Naming Conventions`.
2. **[G-03] quyết định có dọn 84 quote trùng hay không.** Dọn = `/analyze-requirements --update` (đổi quote SC → pointer). Không dọn cũng không chặn `generate-tc`, nhưng nợ này lớn dần theo mỗi version và là nguồn drift nguyên văn.
3. **Không có CRITICAL ⇒ `generate-tc` chạy được ngay** sau khi chốt 2 quyết định scope đã nêu ở `MASTER §9 #3` (3 module out-of-scope Phase 1 = 36 SC) và mode (`standard` vs `--mode comprehensive`).
4. **Trước `vibe-test`:** tạo `~/.foxeco-v2/credentials.env` (`chmod 600`) + điền `environments.md` — hiện cả 2 đều chưa có.
5. **Ngoài phạm vi check nhưng đang treo:** ≥9 bug/nghi vấn đã biết ở `KP-05 §5` chưa log, và Jira chưa cấu hình (`§Jira Integration` còn comment) ⇒ `log-bug --push-jira` sẽ dừng và hỏi.

**Tổng: 0 CRITICAL · 6 WARNING · 7 INFO** — data nhất quán ở mọi số đếm canonical; toàn bộ WARNING là *nợ registry/config*, không phải sai dữ liệu phân tích.
