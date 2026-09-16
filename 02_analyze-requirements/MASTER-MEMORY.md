# MASTER-MEMORY — Cross-Version Registry

> Cập nhật lần cuối: 2026-09-15
> Active version: **v1.0** (thực thi/test) · **v1.1 đang DELTA analyze song song** — v1.0 pipeline (review-tc REJECTED, vibe-test/log-bug chưa chạy) vẫn còn dở nên KHÔNG áp dụng §10 Version Cutover; §8 dưới đây vẫn là bảng sống của v1.0.
>
> **⚠️ Tầng 1 (project) — ROUTER cross-version.** Chứa registry (version / DOC / TC-file / downstream path), quyết định cross-version. **KHÔNG chứa chi tiết SC/data/risk per-module** (sống ở tầng 3 module fragment). **KHÔNG lặp** cùng 1 bảng ở version `MEMORY.md`: §2 DOC Registry là **nguồn duy nhất** ở đây; §3 giữ **lifecycle cross-version**.

## 1. Version Registry
| Version | Release Date | Input Folder | Analyze Folder | Status | Tổng DOC | Tổng SC (all) | Tổng SC (new+mod) | Parent |
|---------|-------------|-------------|----------------|--------|----------|--------------|-------------------|--------|
| v1.0 | TBD | `00_input/v1.0/` | `02_analyze-requirements/v1.0/` | ANALYZED | 6 | 211 | 211 | — (version đầu của chuỗi phân tích mới) |
| v1.1 | TBD | `00_input/v1.1/` | `02_analyze-requirements/v1.1/` | **ANALYZED** (delta 10/11 module có thư mục · `FEED` sửa tại chỗ ở `v1.0/` — xem §3) | 3 | 302 | Δ 136 (91 NEW + 45 MODIFIED) · 2 DEPRECATED | v1.0 |

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
| DOC-v1.1-01 | v1.1 | `FoxEco PRD v1.0 - Gui Hang.pdf` | PDF — **PRD chính thức** (mã `1.0-BM/PM/HDCV/FTEL`, PRD Standard v1.2, rev 08/09/2026 "[A] Bổ sung flow exit giao hàng"). ⚠️ **Cùng tính năng "Gửi Hàng" đã phân tích ở v1.0** (khớp gần 1:1 cả 11 module qua FR01–FR18), KHÔNG phải sản phẩm mới — bản thân PRD tự nhận "MỚI HOÀN TOÀN" chỉ vì PM viết độc lập, không đối chiếu bộ phân tích v1.0. Chi tiết/chính thức hơn hẳn `DOC-v1.0-01/02` | Active | — | USR, HOME, FEED, ORD, ACT, ASN, DLV, GIFT, CNL, NTF, TS |
| DOC-v1.1-02 | v1.1 | `FoxEco Demo 3 vai tro (standalone) v4.0 (1).html` | HTML — prototype 3 vai trò bản **v4.0** (kế thừa `DOC-v1.0-03`), reference-only ⛔ không trích làm nguồn rule | Active | — | (mô tả, không citation — như `DOC-v1.0-03`) |
| DOC-v1.1-03 | v1.1 | `design/` — 26 ảnh PNG chụp demo `DOC-v1.1-02` (tiền tố tên file = module: `ASN_01..03` · `DLV_01..07` · `FEED_01..02` · `HOME_01..04` · `NTF_01..03` · `TS_01..05` · `USR_01..02`) | Ảnh bằng chứng UI từ vibe-check demo 2026-09-15/16 — **evidence phụ**, ⚠ demo ≠ STG; ⛔ không trích làm nguồn rule (rule lấy từ `DOC-v1.1-01` hoặc câu trả lời BA). Đăng ký 2026-09-16 theo health-check F-08 | Active | — | ASN, DLV, FEED, HOME, NTF, TS, USR *(Source Location của CL/SC)* |
| DOC-v1.1-04 | v1.1 | `location_address_catalog.xlsx` | Excel — **danh mục 399 văn phòng FTEL** (cột `name` · `search_text` · mã tỉnh · toạ độ). BA cung cấp 2026-09-16 làm **nguồn danh sách gợi ý "Địa chỉ mặc định"**. Dữ liệu master, không phải tài liệu rule; ⚠ 118 `name` bị cắt 30 ký tự, toạ độ MISSING toàn bộ. Profile + từ khoá test: `04_test-data/valid/USR-office-catalog.md` | Active | — | USR *(prefill sang ORD, ASN)* |

**Ghi chú registry:**
- **`DOC-v1.1-01` CÓ kéo `USR` vào delta** *(sửa 2026-09-15 — ghi chú trước đó SAI)*. Bản trước ghi *"FR15 không áp dụng ở v1.1 ⇒ `USR` không có delta"* vì cho rằng `FR15` (cho sửa SĐT/địa chỉ mặc định) **xung đột** với `SC-USR-003`/`C-USR-03` (màn Cá nhân view-only, chốt 2026-07-24 theo quan sát app). ⛔ **Lập luận đó nhầm một xung đột CẦN PHÂN TÍCH thành lý do bỏ qua cả FR.** Bằng chứng rõ nhất: chính lượt delta đó đã trích `AC-30.1.01` — một AC **thuộc `FR15`** — làm nguồn resolve `C-ORD-10`. Hiện hành: `FR15` **áp dụng**, `C-USR-03` **bị đảo** (có màn `"Cập nhật thông tin"` sửa được **đúng 2 trường**; 4 trường SSO vẫn chỉ đọc). Phân tích đầy đủ: `v1.1/USR-tai-khoan/`.
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

### v1.1 (delta — 10/11 module)
> Từ version delta trở đi liệt kê **per-SC** cho MODIFIED / DEPRECATED; NEW gom theo dải; CARRIED không liệt kê lại.
> ✅ Bảng **đã đóng**: 10 module có thư mục v1.1; `FEED` không dựng thư mục — PRD có chạm bề mặt Bảng tin nhưng thay đổi 2026-09-16 (`SC-FEED-009`/`013` viết lại, giữ lifecycle NEW) được **sửa tại chỗ ở `v1.0/FEED-bang-tin/`**. ⚠️ `USR` được bù ngày 2026-09-15 sau khi phát hiện khai nhầm *"không có delta"* — xem `v1.1/USR-tai-khoan/CHANGELOG.md §1`.

| Module | NEW (dải) | MODIFIED (per-SC — giữ ID v1.0, bản v1.1 authoritative) | DEPRECATED | Tổng tới v1.1 |
|---|---|---|---|--:|
| USR | `SC-USR-013..024` (12 SC) | `SC-USR-002` · `SC-USR-003` · `SC-USR-007` · `SC-USR-011` · `SC-USR-012` | — | 24 |
| HOME | `SC-HOME-025..030` | `SC-HOME-008` · `SC-HOME-019` · `SC-HOME-021` | `SC-HOME-024` · `SC-HOME-010` | 30 |
| FEED | `SC-FEED-015` *(sửa tại chỗ ở v1.0, 2026-09-17)* | `SC-FEED-007`, `SC-FEED-009`, `SC-FEED-013` *(sửa tại chỗ ở v1.0, giữ lifecycle NEW)* | — | 15 *(không có thư mục v1.1)* |
| ORD | `SC-ORD-052..065` (14 SC) | `SC-ORD-005` · `012` · `025` · `026` · `028` · `029` · `036` · `041` · `043` · `044` · `045` · `050` | — | 65 |
| ACT | `SC-ACT-015..017` | `SC-ACT-001` · `005` · `008` · `012` · `013` · `014` | — | 17 |
| ASN | `SC-ASN-019` | `SC-ASN-006` · `008` · `011` · `014` · `015` | — | 19 |
| DLV | `SC-DLV-031..064` (34 SC) | — *(3 REQ đổi nhưng SC gắn vào là SC mới)* | — | 64 |
| GIFT | `SC-GIFT-013` · `SC-GIFT-014` | `SC-GIFT-002` · `003` · `006` · `007` · `008` · `011` | — | 14 |
| CNL | `SC-CNL-014..017` | `SC-CNL-004` · `006` · `009` · `010` · `012` | — | 17 |
| NTF | `SC-NTF-017..022` | `SC-NTF-005` · `008` · `014` | — | 22 |
| TS | `SC-TS-008..015` | — | — | 15 |
| **Tổng** | **91 NEW** | **45 MODIFIED** | **2 DEPRECATED** | **302** |

> 📌 **`SC-HOME-024` · `SC-HOME-010` DEPRECATED** (010 từ 2026-09-17, BA chốt `C-HOME-05`) — theo `Project_rule §Quy ước đếm scenario`, 2 SC này **vẫn trong tổng 302** nhưng **không** vào P1/P2/P3 (40+171+89 = 300).
> 📌 **SC MODIFIED giữ nguyên ID v1.0 và bản v1.1 là authoritative** — ⛔ không sửa bản v1.0 của chúng. 🔴 **Hai SC có Then NGƯỢC NHAU giữa 2 bản, và cả hai bản đều chạy được nên không có gì báo lỗi khi lấy nhầm:** `SC-CNL-006` (v1.0: PASS = *không thấy* nút Báo sự cố · v1.1: PASS = *thấy*) và `SC-USR-003` (v1.0: PASS = *không có control sửa nào* · v1.1: chỉ vùng SSO chỉ đọc, **có** lối vào màn sửa). Điểm chung: cả hai kết luận v1.0 đều Resolved **theo quan sát app**, không theo tài liệu.

## 4. Regression Scope
### v1.0
**Phải test (new + modified):** toàn bộ **211 SC** (version đầu của chuỗi phân tích mới — không có SC CARRIED).

**Nên regression (carried — high risk):** — *(không có: v1.0 không có parent trong chuỗi phân tích mới)*

**Không cần test (carried — low risk, stable):** — *(không có)*

> 📌 **Bộ TC baseline của đợt v1.0 cũ (323 TC) KHÔNG được dùng làm regression scope.** Lý do: (a) **0/323 TC có Scenario ID** (`_handoff-v1.0/03_tc-baseline-v1.0/TC-SC-MAPPING-TODO.md`) ⇒ không map được sang 211 SC mới; (b) bộ TC cũ có **5 lỗi đã biết** (`KP-04 §4`); (c) chỉ **~17/323 TC** từng chạy thật trên app. ⇒ Quyết định 2026-09-07: coi trạng thái hiện tại là **baseline mới**, chuỗi `--delta` bắt đầu từ version kế tiếp.

### v1.1 — Regression Scope

**Phải test (new + modified):** **132 SC** = 88 NEW + 44 MODIFIED. Đây là mẫu số bắt buộc của v1.1.

**Nên regression (carried — high risk):** SC của 3 module `Risk Level = High` mà v1.1 có chạm tới — `ORD` (39 carried) · `ASN` (13) · `DLV` (30) · `CNL` (8, nâng High ở v1.1). Ưu tiên cụm liên quan trực tiếp tới thay đổi: vòng đời đơn · nhật ký · ghép nối.

**Không cần test (carried — low risk, stable):** `FEED` (11/15) — ⚠️ **trừ `SC-FEED-007` (tên hiện trước ghép) · `SC-FEED-009` (ảnh bản đồ tĩnh vẽ tuyến) · `SC-FEED-013` (empty state `EMP-04`) · `SC-FEED-015` (mới — thiếu toạ độ)** phải test lại vì Then đổi 2026-09-16/17; ngoài ra `SC-FEED-010/011/012` là P1/bug đã biết nên vẫn nên regression. `GIFT` carried (6) · `NTF` carried (13) · `USR` carried (9) rủi ro thấp.

> ⚠️ **2 SC DEPRECATED** (`SC-HOME-024` · `SC-HOME-010` từ 2026-09-17) — bỏ khỏi mọi mẫu số pass-rate.
> 🔴 **Trừ ra khỏi mẫu số cho tới khi gỡ nợ:** `SC-ORD-058..060` (chờ `C-ORD-13` — danh bạ nội bộ) · `SC-GIFT-013/014` + `SC-ACT-015` + phần `RETURNED` của `SC-DLV-053..056` (chờ nhánh `FR09` có trên STG) · `SC-CNL-015` (chờ trạng thái `INCIDENT`) · `SC-ORD-031..035` (chờ `C-ORD-04`) · **`SC-USR-013..020` (8 SC — chờ xác nhận app đã build `FR15`; app quan sát 2026-07-24 còn view-only hoàn toàn)**. Verdict đúng khi chưa gỡ là **BLOCKED**, ⛔ không PASS.
> 📌 `CNL` · `NTF` · `TS` vẫn đang chờ PM xác nhận scope Phase 1 (`RISK-CNL-06` · `KP-03 §3.1`) — nhưng **PRD v1.1 đặc tả đầy đủ cả ba** và đặt `FR11`/`FR13`/`FR16` vào business process chính ⇒ **mặc định lập kế hoạch là IN scope**.

## 5. Version Comparison

### v1.0 → v1.1

| Chỉ số | v1.0 | v1.1 | Δ |
|---|--:|--:|--:|
| Module có phân tích | 11 | 11 *(10 có delta + 1 giữ nguyên)* | — |
| REQ | 116 | **142** | +26 |
| SC (tổng, gồm DEPRECATED) | 211 | **302** | +91 NEW · 45 MODIFIED giữ ID · 2 DEPRECATED |
| P1 / P2 / P3 | 27 / 117 / 67 | **40 / 171 / 89** | +13 / +54 / +22 |
| Clarification | 35 | **66** | +5 mở mới lượt delta 2026-09-15 · **+25 mở mới lượt UPDATE 2026-09-16** (rà sâu sau khi BA trả lời) · 1 mở lại |
| CL còn Open | 17 | **18** *(+ 5 Partially chờ BA vòng 2 — 2026-09-17)* | +1 · 43 Resolved — nguồn canonical: `counts:` ở `<module>/risk_assessment.md` |
| RISK | 64 | **87** | +23 |
| DOC nguồn | 6 | 2 *(v1.1)* | PRD chính thức thay thế BRD+PRD-demo làm nguồn chính |

**Điều gì thực sự đổi (không phải số):**
1. **Nguồn nghiệp vụ đổi hạng.** v1.0 chạy trên BRD v3.2 + một PRD *tái dựng từ demo*; v1.1 có **PRD chính thức của PM** (`1.0-BM/PM/HDCV/FTEL`) với 18 FR, ~90 business rule, 31 US và bộ AC đầy đủ. Phần lớn Δ là **chi tiết hoá**, không phải tính năng mới.
2. **Nhánh giao-không-thành-công là tính năng mới thật.** `FR08`/`FR09` sinh ra 3 trạng thái chưa từng có (`RESCHEDULED` · `RETURNING` · `RETURNED`) và kéo theo delta ở `DLV` (34 SC) · `NTF` (6 sự kiện) · `GIFT` (2 SC) · `ACT` (1 SC).
3. **Hai bug đã biết chuyển hạng.** `SC-CNL-010` (huỷ nhận xoá log) và `SC-CNL-009` (huỷ đơn không ghi log) ở v1.0 dựa trên **override của QA**; `BR11-02`/`BR11-03` nay nói trúng đúng hành vi lỗi ⇒ thành **vi phạm đặc tả đã phê duyệt**, `SC-CNL-010` nâng P2→P1.
4. **HAI kết luận bị đảo 180°, và cả hai cùng một kiểu.** `C-CNL-01` (*"màn Báo sự cố out of scope"* → `FR16` đưa vào scope) và `C-USR-03` (*"hồ sơ view-only hoàn toàn"* → `FR15` cho sửa 2 trường). ⭐ **Điểm chung đáng ghi nhớ: cả hai đều là CL được Resolved theo QUAN SÁT APP, không theo tài liệu** — đó là loại phán quyết dễ bị đảo nhất khi có doc mới. Hệ quả kiểm thử: `SC-CNL-006` và `SC-USR-003` có Then **ngược nhau giữa 2 bản**, và **cả hai bản đều chạy được** nên lấy nhầm bản sẽ cho kết luận ngược mà không có gì báo lỗi.
5. **Xuất hiện loại vấn đề mới: tài liệu tự mâu thuẫn.** `C-ORD-04` — `§8.1.4` cho *"Thuốc/Y tế"* là loại hàng hợp lệ trong khi `BR01-07` xếp *"thuốc"* vào hàng cấm. ⛔ Không phân xử được bằng thứ tự ưu tiên nguồn vì **cả hai vế cùng là `DOC-v1.1-01`**.
6. **Tích hợp hệ thống ngoài được nêu tên lần đầu** — Danh bạ nội bộ (`BR01-09`), ảnh hưởng tiền đề test (`C-ORD-13`).
7. **Nhóm rule "bằng chứng đã ghi thì bất biến" nay có 4 thành viên** — `BR11-03` (`SC-CNL-010`) · `BR18-05` (`SC-ORD-065`) · `NFR-07` (`SC-DLV-062`) · `BR15-03`/`BR15-04` (`SC-USR-017`/`018`). App **đã vi phạm nhóm này 1 lần đã live-verify** (`KB-CNL-01`) ⇒ chạy cùng lô, cùng vỡ thì gộp **1 bug report cho nguyên nhân gốc**.

## 6. TC Files Registry
| Version | TC-MASTER File | Tổng TC | Ngày consolidate | Status |
|---------|---------------|---------|-------------------|--------|
| v1.0 | `03_test-cases/v1.0/TC-MASTER-v1.0.xlsx` | 219 | 2026-09-07 | ✅ Consolidated · ❌ **Review 0/100 REJECTED** (2026-09-07, G1 FAIL) — 13 sheet (Overview + ALL + 11 sheet module). Bản copy: `03_test-cases/TC-MASTER-LATEST.xlsx` |

> 📌 Bộ TC của đợt v1.0 **cũ** (323 TC, schema 16 cột đã convert) lưu ở `_handoff-v1.0/03_tc-baseline-v1.0/` — **KHÔNG** đưa vào `03_test-cases/v1.0/` (xem §4).

## 7. Downstream Path Registry
| Skill | Active Version Path |
|-------|-------------------|
| analyze-requirements | `02_analyze-requirements/v1.0/` (router `MEMORY.md` + 11 module — **thực thi/test hiện hành**) · `02_analyze-requirements/v1.1/` (router + 10 module delta, **ANALYZED** 2026-09-16 — `FEED` đọc ở `v1.0/`; bảng hỏi BA `v1.1/CL-hoi-BA-v1.1.xlsx`) |
| generate-tc | `03_test-cases/v1.0/` (fragments `.md` + `TC-MASTER-v1.0.xlsx`) · v1.1: `03_test-cases/v1.1/` — fragment `TC-USR-v1.1.md` (PARTIAL, chưa có TC-MASTER v1.1, xem §8b) |
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
| 13 | health-check | COMPLETED | 2026-09-15 | QUICK · toàn repo (v1.0 + v1.1) · lượt 2 trong ngày | inline summary (mode QUICK — không sinh file report) | **0 CRITICAL · 8 WARNING · 5 INFO.** 🟢 **3 CRITICAL của lượt sáng đã xử lý:** router `v1.1/MEMORY.md` đã dựng · nghĩa `counts:` chốt cumulative (10/10 chỉ số khớp 3 tầng module↔router↔MASTER) · `C-CNL-01` nay có khối `🔁 Kết luận bị đảo` ở `v1.1/CNL-huy-don/CHANGELOG.md §2` (hạ WARNING — v1.0 bị `Project_rule` cấm sửa nên pointer chỉ đi được 1 chiều). **WARNING treo từ lượt trước, chưa ai xử lý (4):** TC-MASTER.xlsx drift diện rộng 9/11 module (Nợ #6) · §8 `generate-tc` Last Run còn 2026-09-07 · TC `CHANGELOG §2` ràng buộc 3 stale (drift B-06 đã fix 2026-09-14) · `validate-vibe-run.mjs` lệch toolkit (hardcode `python3`). **WARNING mới (4):** G-03 quote lặp home **16→21** (+6 do 5 module delta bù, nặng nhất `v1.1/ASN` 7 dòng) · F-08 22 ảnh `00_input/v1.1/design/` vẫn chưa có DOC-ID **và nay đã bị cite làm Source Location** · `MASTER §7` Downstream Path chỉ trỏ `v1.0/` trong khi v1.1 đã ANALYZED · `C-USR-03` lặp pattern đảo-kết-luận của `C-CNL-01`. **Sạch:** F-05/F-06 21/21 module (REQ-rows == quote-blocks) · F-07 8/8 DOC Active resolve · G-01/G-08 cả 2 router chỉ §1+§2 · G-05 0 dòng trùng · E-01..E-07 registry rỗng đúng trạng thái · H-03 9/9 section · H-04 5/5 hook. **Chưa sửa gì — health-check chỉ report.** |

## 8b. Pipeline Status — v1.1 (delta, chạy song song)
> Bảng riêng vì **§10 Version Cutover CHƯA áp dụng** — v1.0 còn dở (`review-tc` REJECTED, `vibe-test`/`log-bug` chưa chạy) nên §8 vẫn là bảng sống của v1.0.
> Cùng luật với §8: **CURRENT-STATE, OVERWRITE — đúng 1 dòng / skill.** Skill chưa chạm v1.1 thì không cần dòng.

| # | Skill | Status | Last Run | Scope | Output | Notes |
|---|-------|--------|----------|-------|--------|-------|
| 3 | analyze-requirements | **COMPLETED** | 2026-09-16 | v1.1 · **10/11 module** + `FEED` (v1.0) — DELTA ×3 lượt + UPDATE ×2 (vibe-check demo · **áp câu trả lời BA + rà sâu từng chức năng**) | `02_analyze-requirements/v1.1/` — router `MEMORY.md` + 10 × 5 file · `v1.1/CL-hoi-BA-v1.1.xlsx` (bảng hỏi BA, dẫn xuất) | **142 REQ · 295 SC · 65 CL (37 Resolved · 3 Partially · 25 Open, 0 blocker execute) · 87 RISK.** Lượt 2026-09-16: BA trả lời **13 CL → 10 Resolved + 3 Partially** (vòng 2: `C-ORD-04` · `C-ORD-13` · `C-USR-05`); rà sâu PRD ⟷ SC **mở 25 CL mới** (chi tiết `<module>/CHANGELOG.md §1`). Kết luận đảo: trần thông báo khớp **không theo ngày** mà *5 thông báo / 1 tin OFFER* · `SC-FEED-009` bản đồ **thật** · nhãn Loại hàng **"Tài liệu"** · nhãn tab theo app. 🔴 **Nợ chặn `generate-tc`:** `C-ORD-13` vòng 2 (email mẫu HRIS) · `C-ASN-05` (so khớp địa chỉ tự do) · 3 cặp SC mâu thuẫn (`C-HOME-05` · `C-DLV-06` · `C-USR-06`) · `C-ACT-03/04` · `RISK-ORD-09` · `RISK-DLV-11` · `RISK-USR-06`. ⚠️ Downstream: TC v1.1 chưa generate ⇒ chưa cần reset |
| 4 | generate-tc | **PARTIAL** | 2026-09-16 | v1.1 · **1/11 module** (`USR`) · mode `standard` | `03_test-cases/v1.1/fragments/TC-USR-v1.1.md` + `CHANGELOG.md` | **29 TC** (P1 2 · P2 23 · P3 4) cho 17 SC NEW+MODIFIED; chưa consolidate, chưa review. ⚠️ v1.0 `review-tc` vẫn REJECTED |
| 13 | health-check | COMPLETED | 2026-09-16 | VERSION · v1.1 (+ `v1.0/FEED-bang-tin` vì là home duy nhất của FEED) | inline summary (mode VERSION — không sinh file report) | **2 CRITICAL · 5 WARNING · 3 INFO.** 🔴 **G-02** `MASTER §5` còn *CL 40 / Open 10* trong khi canonical module = **65 (37 Resolved · 3 Partially · 25 Open)**. 🔴 **G-06b** ~15 chỗ register sống (Khuyến nghị tổng thể · `test_data_catalog` · ghi chú REQ ở traceability · heading CL) còn nói ngược CL đã Resolved 2026-09-16 — nặng nhất: `ORD` KN#4 + `FEED` data catalog *"không dùng Tài liệu"*, `REQ-FEED-005` *"không viết TC bản đồ thật"*, `ASN` data catalog + KN#2 *"trần/ngày hỏi admin"*, `GIFT` KN#5, `NTF` KN#4. 🟡 F-01 router `doc_source.modules` thiếu 5 module · F-08 26 ảnh `design/` chưa DOC-ID · G-03 ≈18 quote lặp home · router/MASTER §4 còn *"FEED không delta, PRD không đụng"* · MASTER §7 chỉ trỏ v1.0. 🔵 F-06 thiếu Source Detail 14 SC (`ORD` 12, `USR-019/020`) · A-05 active version v1.0 (chủ đích) · C/D/E N/A (v1.1 chưa có TC/run). **Sạch:** B counts module↔router 10/10 · P1+P2+P3 khớp · F-05 · F-07 2/2 · G-01/G-08 · G-05 · H-03 9/9 · H-04 3/3 hook · H-05/H-06 khớp toolkit. ✅ **2 CRITICAL đã sửa cùng ngày** (MASTER §5 → 65 CL / 25 Open / 3 Partially; 9 module sửa chữ register sống + dòng `ĐÍNH CHÍNH` ở `CHANGELOG §1`, quét lại 0 chỗ còn nói ngược). ✅ **5 WARNING đã sửa cùng ngày:** F-01 router `doc_source.modules` đủ 11 module · F-08 đăng ký `DOC-v1.1-03` cho 26 ảnh `design/` (+ router) · G-03 thay 20 quote lặp bằng dòng trỏ `↪` về home (quét lại 0) · G-06b bỏ nhận định *"FEED không delta, PRD không đụng"* ở router/MASTER §3/§4, `SC-FEED-009/013` vào phạm vi test lại · MASTER §7 thêm path v1.1. ✅ **INFO F-06 đã sửa cùng ngày:** thêm 13 khối Source Detail cho 14 SC (`ORD` 12 · `USR-019/020`), quét lại 0 SC thiếu, G-03 vẫn 0. Còn lại chỉ A-05 (active version v1.0 — chủ đích). |

## 9. Notes (quyết định cross-version — KHÔNG phải per-run count log)

**Quyết định phương pháp (2026-09-07):**
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
