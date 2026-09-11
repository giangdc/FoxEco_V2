# FoxEco — Bộ bàn giao sang project mới (bộ skill v1.1)

> **Đóng gói:** 2026-09-04 · **Nguồn:** `/home/giangdc2/AI/FoxEco` (git `main`, commit `3be4b01`)
> **Mục đích:** dựng lại project FoxEco trên bộ skill mới (qc-claude-v1 **v1.1**, layout `module-first`) mà **không mất** kiến thức nghiệp vụ đã tích luỹ từ 2026-07-24 → 2026-07-31.
>
> **Trạng thái:** PRD version mới **chưa có** (PM chưa gửi). Bộ này chuẩn bị sẵn để khi PRD về là chạy được ngay.

---

## 1. Nội dung

```
_handoff-v1.0/                          9,3 MB
├── README.md                           ← file này (runbook)
│
├── 00_input-seed/                      → thả vào 00_input/<version>/ của project mới
│   ├── docs/                           4 tài liệu gốc
│   │   ├── FoxEco BRD v3.2.md                      nền, phần lớn requirement
│   │   ├── tổng hợp từ file demo.docx              PRD tái dựng từ demo
│   │   ├── FoxEco Demo 3 vai tro (2).html          prototype, reference-only
│   │   ├── Fox Eco Doc/images/  (82 ảnh)           Figma — bằng chứng UI
│   │   └── Screenshot From 2026-07-27 15-23-25.png
│   └── _knowledge-pack/                kiến thức NGOÀI tài liệu
│       ├── KP-01_business-knowledge.md        ⭐ 40 mục, gom theo module
│       ├── KP-02_clarification-register.md    25 clarification + trả lời BA/PO
│       ├── KP-03_scope-and-project-rules.md   scope Phase 1 + custom rule
│       ├── KP-05_open-gaps-and-conflicts.md   10 câu hỏi treo + 9 nghi vấn bug
│       ├── KP-06_source-document-registry.md  cạm bẫy kỹ thuật từng loại file
│       ├── KP-07_notification-matrix.md       12 sự kiện thông báo × 3 nguồn (C-NTF-01)
│       └── evidence/                          ⭐ 25 screenshot + log + 17 locator
│
├── 02_seed/                            → KHÔNG bỏ vào 00_input
│   ├── Project_rule-seed.md            block dán vào Project_rule.md TRƯỚC khi init
│   └── KP-04_prior-analysis-baseline.md  ⛔ inventory cũ — chỉ dùng ở bước đối chiếu
│
└── 03_tc-baseline-v1.0/                → 03_test-cases/<version>/ (nếu cần regression)
    ├── TC-MASTER-v1.0.xlsx             323 TC, schema 16 cột mới
    ├── fragments/TC-<MODULE>-v1.0.md   9 fragment Markdown format v1.1
    ├── TC-SC-MAPPING-TODO.md           ⚠ việc còn thiếu (Scenario ID)
    ├── CONVERSION-NOTES.md             bảng ánh xạ cột + 2 quyết định
    └── ISC_FoxEco_v1.0_TC_v1_R1.xlsx   bản gốc 42 cột, tham chiếu
│
└── 04_archive-project-v1.0/            → lưu trữ, KHÔNG dùng khi analyze
    ├── analyze-v1.0/                   5 file phân tích cũ (MEMORY 193K, scenario_map 125K…)
    ├── MASTER-MEMORY.md · Project_rule.md · CLAUDE-v1.0.md
    ├── tc-review/                      review report + TC CHANGELOG
    └── docs-superseded/FoxEco BRD v3.1.md
```

> **Bộ này TỰ ĐỨNG ĐƯỢC** — không còn chỗ nào phải quay lại repo cũ. Project cũ có thể đóng băng/xoá sau khi bàn giao.

---

## 2. Runbook — làm theo thứ tự

### Bước 0 — Gỡ pin skill cũ
Project hiện tại có `.claude/skills/` pin bản **v1.0**, ghi đè bản global v1.1. Project mới **đừng copy thư mục đó sang**, để dùng thẳng `~/.claude/skills/`.

Kiểm tra `~/.claude/skills/review-tc/review-agent/AGENT.md` có tồn tại không — thiếu file này thì `review-tc` chạy **Direct mode**, điểm bị cap 85 + mang bias self-review (đúng lỗi của đợt cũ).

### Bước 1 — Init
```bash
/init-project
```

### Bước 2 — Seed Project_rule TRƯỚC khi analyze
Dán các block trong `02_seed/Project_rule-seed.md` vào `02_analyze-requirements/Project_rule.md`:
`§Layout Conventions` · `§Module Codes` · `§DOC Notation` · `§Quy ước đếm scenario` · `§Custom Rules` · `§Jira Integration`.

> Skill v1.1 đọc 3 mục đầu ngay ở Step 1 (INVIOLABLE #1: *"ĐỌC Project_rule.md TRƯỚC KHI GHI — KHÔNG hardcode/đoán"*).

### Bước 3 — Đổ input
```
00_input/<version>/
├── (toàn bộ 00_input-seed/docs/)
├── <PRD version mới của PM>          ← khi có
└── _knowledge-pack/                   (toàn bộ 00_input-seed/_knowledge-pack/)
```

Gán DOC-ID rồi khai vào registry:

| DOC ID | File | Ghi chú |
|---|---|---|
| `DOC-<ver>-01` | FoxEco BRD v3.2.md | nền |
| `DOC-<ver>-02` | **PRD version mới** | ⭐ phải khai rõ **bản này thắng khi mâu thuẫn** |
| `DOC-<ver>-03` | tổng hợp từ file demo.docx | bổ trợ screen/field |
| `DOC-<ver>-04` | Fox Eco Doc/images/ (82 ảnh) | bằng chứng UI |
| `DOC-<ver>-05` | FoxEco Demo ....html | reference-only |
| `DOC-<ver>-06` | `_knowledge-pack/` | trích dạng `DOC-<ver>-06 KP-01 §5.1 KB-DLV-01` |

> ⚠ Skill yêu cầu: *"**Bổ sung ≠ thay thế.** Doc bổ sung lấy DOC-ID mới và phải ghi rõ bản nào thắng khi 2 bản mâu thuẫn. **Không âm thầm coi bản mới nhất là bản đúng.**"*

### Bước 4 — Analyze
```bash
/analyze-requirements --init @00_input/<version>/
/analyze-requirements --sweep          # rà lượt 2 tìm requirement bỏ sót
```

### Bước 5 — Đối chiếu coverage
Mở `02_seed/KP-04_prior-analysis-baseline.md`, so 92 scenario cũ với kết quả mới → scenario nào đợt cũ có mà đợt mới thiếu thì rà lại.

> Làm ở **bước này**, không sớm hơn. Để KP-04 trong `00_input` từ đầu thì bản analyze mới rất dễ "mót" thẳng từ đó thay vì đọc tài liệu — tái tạo luôn 5 lỗi đã biết.

### Bước 6 — Test case
```bash
/generate-tc --mode comprehensive
/review-tc
/export-tc-rp --phase design           # render ra workbook ISC 9 sheet để giao PM/Dev/BA
```

### Bước 7 — Từ version SAU trở đi
```bash
/analyze-requirements --delta --version <next>
```

---

## 3. Về regression traceability

Bạn nói *"nếu được thì càng tốt"* — nên tôi đã convert sẵn 323 TC sang schema 16 cột.

**Lý do cần:** skill ghi rõ *"CARRIED scenarios không có TC-MASTER-v[parent] → **Skip regression, log warning**"*. Không có file này thì scenario CARRIED bị bỏ qua **âm thầm**.

**Hai cách dùng:**

| | Cách | Khi nào |
|---|---|---|
| **(a)** | Không dùng baseline TC. Coi trạng thái hiện tại là **baseline mới**, INIT 1 lần, viết TC mới toàn bộ. Chuỗi `--delta` bắt đầu từ version kế tiếp | Rẻ nhất. Phù hợp vì bộ TC cũ có 5 lỗi đã biết và chỉ 17/323 TC từng chạy thật |
| **(b)** | Đặt `03_tc-baseline-v1.0/` thành `03_test-cases/v1.0/`, analyze baseline v1.0 trước rồi `--delta` sang version mới | Khi cần trả lời PM/khách hàng *"so với lần test trước đổi gì"* |

Chọn (b) thì phải hoàn thiện `TC-SC-MAPPING-TODO.md` trước — hiện **0/323 TC có Scenario ID** (template ISC 42 cột không có cột này). File đó đã có đủ 89 scenario + số TC từng scenario + checksum để làm nhanh.

---

## 4. ⚠ Bốn điều dễ sai

**Đừng coi knowledge pack là tài liệu yêu cầu.** Nó chỉ chứa kiến thức NGOÀI tài liệu. Toàn bộ `§D3` Functional Requirements, `§D4` Business Rules, `§D1b` User Story + AC, `§D8` Validate rules vẫn nằm trong BRD v3.2. Bỏ BRD ra = không quote verbatim được (mà verbatim quoting là ràng buộc INVIOLABLE) → citation mồ côi ngay từ INIT.

**Đừng để BRD v3.1 cạnh v3.2 trong input.** Rule input retention: *"`00_input/<version>/` chỉ chứa BẢN LATEST… 2 bản cùng chỗ là nguồn nhầm lẫn cho lần phân tích sau."* Bản v3.1 để riêng ở `04_archive-project-v1.0/docs-superseded/` — **đừng copy vào `00_input/`**.

**Hỏi BA trước ít nhất 1 câu.** Chip **"Tài liệu"** (tài liệu) hay **"Giấy tờ, hồ sơ"** (app thật)? Sai từ gốc, lan khắp bộ TC. Chín câu còn lại ở `KP-05 §1`.

**25 clarification sẵn có, 7 còn Open.** Skill có edge case: *"Clarification > 20 items chưa resolve → suggest user resolve trước khi tiếp generate-tc"*. Nên xử lý bớt trước khi tới bước 6.

---

## 5. Bảng tra nhanh — tìm gì ở đâu

| Cần gì | Mở file |
|---|---|
| Nhãn nút màn Theo dõi đơn (3 vai trò × 5 trạng thái) | `KP-01 §5.1` |
| App thật hoạt động thế nào (vibe-test) | `KP-01 §10` + `_knowledge-pack/evidence/` |
| BA đã trả lời gì, cái gì còn treo | `KP-02` |
| Scope Phase 1 / cái gì out-of-scope | `KP-03 §3` |
| 2 custom rule bắt buộc | `KP-03 §4` |
| Inventory 46 REQ / 92 SC / 323 TC đợt cũ | `02_seed/KP-04` (reference-only) |
| Câu hỏi treo, mâu thuẫn nguồn, bug chưa log | `KP-05` |
| Cạm bẫy khi đọc từng loại file nguồn | `KP-06 §1` |
| Bản đồ section BRD v3.2 | `KP-06 §4` |
| Package name STG, thiết bị, tài khoản test | `KP-01 §10.1` |

---

## 6. `04_archive-project-v1.0/` — đặt ở đâu và dùng khi nào

Đây là **toàn bộ phân tích của project v1.0**, gói kèm để project mới không phải phụ thuộc vào repo cũ.

| Đặt ở | `_archive/project-v1.0/` (thư mục riêng ở gốc project mới) |
|---|---|
| **Dùng khi** | Cần tra Block Definition chi tiết từng màn, Source Quote gốc, hash ảnh Figma, lý do một quyết định cũ, hoặc đối chiếu finding review |
| **KHÔNG dùng khi** | Chạy `analyze-requirements`. Để trong `00_input/` hoặc `02_analyze-requirements/v*/` sẽ bị `health-check` bắt là orphan/không đăng ký DOC-ID |

**Vì sao vẫn cần dù đã có knowledge pack:** KP chỉ trích phần kiến thức *ngoài tài liệu*. Những thứ sau chỉ có ở archive:

- `analyze-v1.0/test_scenario_map.md` (125 KB) — **Block Definitions từng màn**: liệt kê field/nút/rule của Wizard B1-B2-B3, Form OFFER, Bảng tin, Chi tiết tin, Huỷ đơn… kèm Source Quote + hash ảnh Figma từng block
- `analyze-v1.0/MEMORY.md` — Source Detail đầy đủ của 46 REQ + 92 SC
- `analyze-v1.0/requirement_traceability.md` — ma trận REQ ↔ ID gốc BRD (`ORD-01`, `BR-CON-02`, `US-D16`…)
- `tc-review/review-report-v1.0.md` — 18 finding + lý do
- `tc-review/TC-CHANGELOG-v1.0.md` — nhật ký mọi lần sinh/sửa TC

> 💡 Khi analyze mới xong, đối chiếu `analyze-v1.0/test_scenario_map.md` với kết quả mới để bắt block/field bị bỏ sót — làm cùng lúc với bước 5 (KP-04).
