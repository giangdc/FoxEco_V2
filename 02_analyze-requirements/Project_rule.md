
# Project Rules — foxeco-v2

> Bản runtime mọi skill đọc. Framework default: `~/.claude/skills/init-project/`.
> Sửa tại đây để override cho project này.
> ⚠️ Skill trích section theo **TÊN**, không theo số — thêm section mới thì đặt cuối file.

## Project Info

- **Tên project:** foxeco-v2
- **App type:** App
  <!-- SDK tích hợp vào app mobile FoxPro có sẵn (host app `FoxPro_Stag`,
       package `vn.fpt.ftel.sop.stg`) — KHÔNG phải web app độc lập.
       Nguồn: DOC-v1.0-06 KP-03 §1. Cập nhật 2026-09-07. -->
  <!-- Dùng ĐÚNG từ vựng của `§Jira Integration > custom_fields.Platform` (Web · App ·
       "Web, App") để 1 khái niệm không có 2 tên. ⛔ KHÔNG viết `Mobile` — đó là tên cũ,
       Jira đã đổi sang `App`. `API`/`Desktop` chỉ dùng cho App type, KHÔNG có trong
       danh mục Platform của bug (thêm vào đó phải sửa kèm §1a template ISC).
       → Điền khi có tài liệu đầu vào ở `00_input/v1.0/`. -->
- **Loại kiểm thử:** Functional, Regression, Smoke
- **Môi trường:** STG (mặc định) — URL/host: TBD, ghi vào `07_environments/environments.md`
- **Team:** Solo
- **QC phụ trách (owner):** GiangDC2
- **Thành viên:** — (Solo)
- **Version hiện tại:** v1.0
- **Ngôn ngữ viết TC:** Tiếng Việt

## Module Codes

> Bảng map **mã chức năng ↔ module ↔ thư mục** — nguồn duy nhất. `sync-jira-bugs` map bug → module bằng
> prefix summary `[<mã> - <tên>]`; `analyze-requirements` dùng cột **`Dir`** làm tên thư mục fragment,
> cột **`Module`** làm token ID (`REQ-<Module>-NNN` · `SC-<Module>-NNN` · `TC-<Module>-NNN`).
> 🔴 **`Module` ≠ `Dir` là CHỦ Ý** (đổi 2026-09-07): `Module` là mã ngắn đi vào ID, `Dir` là tên thư mục
> có gợi nghĩa cho người mới đọc. ⛔ Đổi `Module` = đổi toàn bộ ID đã phát hành — KHÔNG làm.
> Đổi `Dir` thì phải sửa kèm: frontmatter `id:` + `module.dir` của 6 file trong thư mục đó,
> cột `Dir` ở `v[X]/MEMORY.md §1`, và mọi cross-ref `<Dir>/<file>.md`.
> Module ngừng phát triển thì đổi `Status` = `DEPRECATED`, **KHÔNG xoá dòng** — 0 REQ/SC/TC của
> module DEPRECATED là ĐÚNG, không phải coverage gap; `health-check` đọc cột này để khỏi báo nhầm.

| Mã | Module (token ID) | Dir (thư mục) | Tên chức năng | Status |
|---|---|---|---|---|
| TC-01 | USR | `USR-tai-khoan/` | Tài khoản & Hồ sơ — màn Cá nhân (view-only), SSO qua host app FoxPro | Active |
| TC-02 | HOME | `HOME-trang-chu/` | Trang chủ — header, banner, card "Đóng góp của bạn", section "Tin mới", bottom nav | Active |
| TC-03 | FEED | `FEED-bang-tin/` | Bảng tin & Chi tiết tin — danh sách tin cộng đồng + màn chi tiết 1 tin | Active |
| TC-04 | ORD | `ORD-dang-tin/` | Đăng tin & Quản lý tin — wizard NEED 3 bước, form OFFER 1 trang, Đăng tin thành công, sửa tin, validate form | Active |
| TC-05 | ACT | `ACT-hoat-dong/` | Hoạt động ("Đơn của tôi") — 2 tab Đang diễn ra / Đã hoàn thành | Active |
| TC-06 | ASN | `ASN-ghep-noi/` | Ghép nối — ghép ngay, lộ SĐT sau ghép, chống double-accept, tự khớp tuyến OFFER↔NEED, trần gợi ý | Active |
| TC-07 | DLV | `DLV-giao-nhan/` | Giao nhận & Theo dõi đơn — ma trận nhãn nút 3 vai × 5 trạng thái, xác nhận đã nhận, ảnh/GPS/chi phí | Active |
| TC-08 | GIFT | `GIFT-qua-cam-on/` | Quà cảm ơn — tặng quà sau Hoàn thành + màn "Quà đã nhận" | Active |
| TC-09 | CNL | `CNL-huy-don/` | Huỷ đơn / Huỷ nhận đơn — lý do bắt buộc, ghi vai trò người huỷ | Active |
| TC-10 | NTF | `NTF-thong-bao/` | Thông báo — danh sách, đánh dấu đã đọc, phân trang, **9 sự kiện chính thức `NTF-01..09`** (12 hàng ứng viên ở `KP-07`, chưa chốt — `C-NTF-01` Open) | Active |
| TC-11 | TS | `TS-trust-safety/` | Trust & Safety — log tương tác bất biến, Admin can thiệp (phần lớn backend/Admin) | Active |

> **Tách module so với đợt v1.0 cũ (2026-09-07, QC GiangDC2):** đợt cũ dùng 8 mã domain, trong đó
> `ORD` gánh 3 màn (Đăng tin + Hoạt động + Trang chủ) và `ASN` gánh Bảng tin ⇒ fragment phình,
> không map 1:1 với sheet TC. Bản này tách thêm `HOME` · `FEED` · `ACT` để
> **module ↔ fragment ↔ sheet `export-tc-rp`** thành 1:1.

## Naming Conventions

> Framework default (`~/.claude/skills/init-project/references/naming-conventions.md`).
> Sửa tại đây để override cho project này — mọi skill đọc section này, không đọc file framework.

| Type | Pattern |
|---|---|
| Document | `DOC-v[VERSION]-[NN]` |
| Requirement | `REQ-[MODULE]-[NNN]` |
| Scenario | `SC-[MODULE]-[NNN]` |
| Testcase | `TC-[MODULE]-[NNN]` — tiêu đề để ở cột riêng ("Test Title"), **KHÔNG** nhét slug vào ID *(sửa 2026-09-14 theo `health-check` F-04 — 219/219 TC thực tế dùng dạng này, pattern cũ có `-[short-title]` chưa từng khớp)* |
| Clarification | `C-[MODULE]-[NN]` *(bổ sung 2026-09-14 — dùng 649+ lần nhưng chưa có nguồn chuẩn, theo `health-check` F-04 lượt 2026-09-07)* |
| Risk | `RISK-[MODULE]-[NN]` *(bổ sung 2026-09-14, cùng lý do)* |
| Bug ID | `BUG-[NNN]` |
| Test run | `TR-[SPRINT]-[YYYY-MM-DD]` |
| TC-MASTER | `TC-MASTER-v[VERSION].xlsx` |
| Report | `REPORT-[MODE]-[CTX]-[YYYY-MM-DD].{md,xlsx}` |

### Bug — 2 field điền, còn lại dẫn xuất
- Điền: `module` (từ section `Module Codes`) + `bug_desc` (tiếng Việt, ≤12 từ)
- `title` = `[<module>] - <bug_desc>` → dùng cho **cả H1 md và Jira Summary** (nguyên văn)
- File: `draft/BUG-<NNN>-<slug(bug_desc)>.md` → sau push: `jira/<JIRA-KEY>-<slug>.md`
- Label bắt buộc khi push: `bug-<nnn>` (dùng cho `match_jql`)

### Ngôn ngữ
- Narrative (test case, mô tả bug, steps): **Tiếng Việt**
- Tech terms · code block · enum Status/Priority/Severity: **English**

### Enum
- Bug Status: `Open` · `In Progress` · `Fixed` · `Verified Fixed` · `Closed` · `Closed (False Positive)` · `Won't Fix`
- Priority: `P1` · `P2` · `P3` — Severity: `Critical` · `Major` · `Medium` · `Low` (weight 20/10/5/2)
- TC Status: `Pass` · `Fail` · `Blocked` · `Skipped` · `Not Run`

## Layout Conventions

> Quy ước máy đọc — quyết định skill GHI vào đâu và health-check TÌM ở đâu.
> Đổi giá trị ở đây là đổi hành vi skill; đừng đổi giữa chừng 1 version.

```yaml
analyze_layout:     module-first   # module-first (mặc định) | flat (legacy, 1 module)
                                   # module-first v2 (mặc định project mới): v[X]/MEMORY.md = router
                                   #   (CHỈ §1 Function Register + §2 Module Summary)
                                   #   + v[X]/<MODULE>/{CHANGELOG, requirement_traceability,
                                   #     test_scenario_map, test_data_catalog, risk_assessment}.md
                                   #   KHÔNG có _global/ — CL về <MODULE>/risk_assessment.md
                                   # module-first v1 (project đang chạy): v[X]/<MODULE>/{4 file} + v[X]/_global/
                                   # flat:         4 file monolith thẳng trong v[X]/
                                   # ⚠️ Skill DÒ layout bằng SỰ TỒN TẠI của <MODULE>/CHANGELOG.md,
                                   #   KHÔNG bằng field này (field chỉ có 2 nhánh module-first|flat).
tc_fragment_format: md             # md (mặc định) | xlsx — TC-MASTER luôn .xlsx dù chọn gì
bug_folders:
  jira:  05_bug-reports/jira/      # bug ĐÃ log Jira — mirror do sync-jira-bugs ghi đè, KHÔNG sửa tay
  draft: 05_bug-reports/draft/     # bug LOCAL chưa log Jira
  index: 05_bug-reports/bug-index.md
  # GHI phẳng ở gốc 2 thư mục trên. ĐỌC phải ĐỆ QUY (`jira/**/*.md`) — close-sprint
  # dồn bug vào sub-folder theo sprint lúc đóng sổ; glob phẳng đọc ra 0 bug mà KHÔNG
  # báo lỗi (health-check E-07).
runs_layout:
  auto:  08_test-runs/             # execute-maintain
  vibe:  08_test-runs/vibe/        # vibe-test
router_filename:    README.md      # README.md (mặc định) | INDEX.md — tên file router của 08_/09_
```

## DOC Notation

```yaml
req_notation: FR/VR
# ⚠️ Đặc thù dự án (xác nhận 2026-09-07 từ DOC-v1.0-06 KP-03 §5): BRD CÓ đánh số requirement
# nhưng theo ID riêng TỪNG DOMAIN, không phải một cặp FR/VR thống nhất. Nhóm ID thực tế:
#   ORD-NN · ASN-NN · DLV-NN (biến thể PUP/GPS/COST) · GIFT-NN · CNL-NN · MTCH-NN · LOC-NN
#                                            → §D3 (Functional Requirements)
#   BR-<MODULE>-NN                           → §D4 / §A5 (Business Rules)
#   VAL-NN                                   → §D8 (Validate & Giá trị mặc định)
#   NTF-NN → §D6 · OPR-NN → §D7 · NT/USR/TS-NN → §A2/§A6/§A8
#   US-D<NN>                                 → §D1b (User Story, có cột Acceptance Criteria)
# QUY TẮC: cột "Maps (Ref DOC)" dùng TRỰC TIẾP ID gốc (vd `ORD-01`, `BR-CNL-01`, `US-D16`),
#          ⛔ KHÔNG quy đổi sang ký hiệu FR-NN/VR-NN chuẩn hoá.
# PRD .docx KHÔNG có ID riêng → định vị bằng `§section · Table N`.
# FR/VR   : doc đánh số Functional/Validation Rule
# AC      : doc dùng Acceptance Criteria
# UC      : doc dùng Use Case
# US-key  : doc dùng key user story (vd PRJ-123)
# none    : doc KHÔNG đánh số → traceability dùng DOC-ID §section (traceability Schema B)
# auto    : chưa rõ → analyze-requirements tự phát hiện lần chạy đầu rồi GHI NGƯỢC giá trị thật vào đây
#
# ⚠️ DOC-v1.1-01 (PRD chính thức "FoxEco — Gửi Hàng", 1.0-BM/PM/HDCV/FTEL) dùng ký hiệu KHÁC hẳn v1.0:
#   FR<NN>        → §8 Feature Detail (đặc tả chức năng, có Business Rules con)
#   BR<FF>-NN     → §8.<x>.1 Business Rules của từng FR (vd BR03-01 thuộc FR03)
#   US<NN>        → §6.1 User Story
#   AC-{US}.{Scenario}.{Case} → §6.2 Acceptance Criteria (Given/When/Then), trace tới US
#   NFR-NN        → §9 Non-Functional Requirements
#   VAL-NN        → §8.18.2 Quy tắc chung cho toàn bộ form
# QUY TẮC riêng cho DOC-v1.1-01: cột "Maps (Ref DOC)" dùng TRỰC TIẾP ID gốc (vd `FR08`, `BR08-02`,
# `AC-07.1.01`, `NFR-04`), không quy đổi. Không nhầm `BR<FF>-NN` (FF = số FR cha) với `BR-<MODULE>-NN`
# của DOC-v1.0-01 — 2 hệ ký hiệu khác nhau, chỉ trùng chữ "BR".
```

## Jira Integration

> ✅ **ĐÃ CẤU HÌNH 2026-09-18** — kết nối qua Atlassian connector (claude.ai OAuth), xác nhận bằng
> `atlassianUserInfo` (account `GiangDC2`) + `getAccessibleAtlassianResources` (site `foxproject.atlassian.net`).
> Project khớp app đang test: `FE` — "Fox Eco". Bug đầu tiên push thủ công: `FE-290` (B2, module USR).
>
> ⚠️ Subject convention của Jira project này **khác** convention local (`§Naming Conventions` trên):
> project FE đang dùng `[TC_NN - <mô tả ngắn>]` (số TC theo cách đánh số riêng trong Jira, không phải mã module
> ACT/ORD/USR...). Đã quan sát qua các bug có sẵn (`FE-175`..`FE-202`). Giữ nguyên convention này khi push tiếp
> để nhất quán với lịch sử project, trừ khi QC/BA chốt đổi.
>
> Custom field bắt buộc của issue type Bug trong `FE` (ngoài field chuẩn Jira):
> `Severity` (thang 0/2/5/10/20, cascading select) · `Test Round` (1-7, **mặc định = 1** — QC chốt 2026-09-18,
> áp dụng mọi bug từ đây) · `Platform` (App/Web/Web,App) ·
> `Effect` (Functionality/Performance/Security/Serviceability/Usability) · `Test method` (Auto/Manual, default Manual) ·
> `Defect Type` (Data/Interface/Logic/Requirement/Server/Other) · `Duplicate` (No/Yes, default No) ·
> **`Parent` (bắt buộc) = `FE-1`** (`"[FoxEco] Triển khai Phase 1 - Nền tảng chung & Gửi hàng (MVP)"`, issue type Request) ·
> **`Fix versions` (bắt buộc) = `V1.0`**.
>
> ⚠️ `FE-290`/`FE-291` (B2/B3) push lúc đầu bị set `Test Round=2` nhầm — QC đã tự sửa tay trên Jira về `1`
> ngày 2026-09-18; local mirror đã cập nhật khớp. Từ bug tiếp theo trở đi dùng thẳng `test_round_default: 1` dưới đây.

```yaml
mcp_axis:    connector
qc_name:     GiangDC2
site:        https://foxproject.atlassian.net
project_key: FE
parent_issue: FE-1        # bắt buộc khi tạo Bug — không set sẽ bị Jira reject
fix_version:  V1.0         # bắt buộc khi tạo Bug — không set sẽ bị Jira reject
test_round_default: 1     # customfield_10679, id option "1" = 10365 — QC chốt 2026-09-18, áp dụng MỌI bug từ đây
subject_convention: "[TC_NN - <mô tả ngắn>]"   # khác local §Naming Conventions, giữ theo lịch sử Jira project FE
# custom_fields đầy đủ (id + allowedValues) — xem 05_bug-reports/jira/FE-290-*.md làm ví dụ mapping
# severity_map, match_jql, userstory…: log-bug tự khám phá + bổ sung khi chạy --push-jira lần sau
```

## Automation Rules

> `implement-automation` + `review-src-tc` đọc. Chưa có automation ⇒ ghi `N/A`.

**N/A** — project chạy manual (Q7 = Không có automation). Khi bật automation:
chạy `/init-source-code --archetype <playwright-ts|selenium-java|appium-java>`, rồi khôi phục
bộ rule mặc định từ `~/.claude/skills/init-project/assets/project-rule-template.md §Automation Rules`
(TC là contract · comment `// Step N:` / `// Expected N:` · annotation mang TC ID + SC ID ·
test data đúng giá trị TC · theo convention `10_source-code/MEMORY.md`) và điền bảng
**Locator Strategy Priority** theo stack đã chọn.

## Execution Rules

> `execute-maintain` + `vibe-test` đọc.

- **Chạy test thật**, parse output thật. KHÔNG bịa số liệu — chạy không được thì báo blocked.
- **Classify fail:** `LOCATOR_STALE` · `ASSERTION_FAIL` · `ENV_ERROR` · `UNKNOWN`.
- **KHÔNG auto-fix.** Skill report → người/`implement-automation` sửa.
- **Credentials:** `<env-file>` = `~/.foxeco-v2/credentials.env` (ngoài repo, `chmod 600`).
  ⛔ KHÔNG inline password vào command · ⛔ KHÔNG đọc file credentials rồi copy giá trị ra context.
  Check bằng `test -n "$<VAR>" && echo ENV_OK || echo ENV_MISSING` (KHÔNG echo giá trị).
- **Env vars cần thiết:** `FOXECO_STG_USER` · `FOXECO_STG_PASS` (KHÔNG ghi giá trị ở đây).
- 🚪 **Mở app FoxEco trên STG — 3 bước** *(QC GiangDC2 hướng dẫn 2026-09-18)*:
  1. Mở **app FoxPro** (`vn.fpt.ftel.sop.stg`) và **đăng nhập thành công** (tài khoản `stag_*@fpt.com` + pass dùng chung + **mã OTP**).
  2. Vào menu bar **"Chức năng"**.
  3. Nhấn **icon FoxEco** → vào thẳng FoxEco với danh tính SSO của tài khoản vừa đăng nhập.
  🔑 **FoxPro = HRIS, cùng 1 hệ thống, khác bề mặt** (QC chốt 2026-09-18): **HRIS là bản WEB**, **FoxPro là bản APP mobile**.
  ⇒ Test FoxEco **luôn đi đường app FoxPro**; ⛔ không tìm FoxEco trên web HRIS. Dữ liệu hồ sơ/SĐT/địa chỉ mà TC gọi là *"HRIS"* chính là dữ liệu của hệ thống này.
  ⇒ FoxEco **không có icon riêng ngoài launcher** và **không có URL** — mọi TC đều bắt đầu từ 3 bước này.
  ⚠️ **OTP phải nhập tay** — AI không lấy được mã ⇒ `vibe-test` cần người mở app + đăng nhập **1 lần đầu phiên**, sau đó AI chạy tiếp.
  ⛔ Đổi tài khoản (vd sang vai B) = **đăng xuất khỏi app FoxPro rồi lặp lại 3 bước**, không chỉ thoát FoxEco.
  📌 Tài khoản + vai: `04_test-data/valid/USR-accounts.md`.
- **Thiết bị:** Android thật, SDK trong host app `vn.fpt.ftel.sop.stg`. Trước khi chạy: `adb` set
  `screen_off_timeout` ≥ 30 phút (auto-lock đã cắt ngang 2 phiên vibe-test v1.0).
- **Evidence vibe-test:** ≥1 ảnh riêng / TC tại điểm verify; giữ ảnh phụ chỉ khi FAIL/BLOCKED.

## Bug Rules

> `log-bug` đọc.

- **Bug từ evidence**, không suy đoán. `LOCATOR_STALE` ≠ app bug (trừ khi UI thật sự đổi).
- **Traceability không đứt:** Bug → FAIL → RUN → Method → TC → SC → REQ.
- **Lifecycle:** `Open → In Progress → Fixed → Verified Fixed → Closed`. KHÔNG skip bước.
- **Source of truth phía local** = file bug `.md`; mirror `jira/**/*.md` (đệ quy) do `sync-jira-bugs` ghi đè,
  KHÔNG sửa tay. Đổi trạng thái trên Jira ⇒ chạy `/sync-jira-bugs`, đừng sửa mirror.
- **Aging:** cảnh báo bug `Open` > <7> ngày. Version đã đóng ⇒ miễn cảnh báo (nếu không sẽ đỏ mãi).
- **Severity ↔ Priority** theo enum ở `§Naming Conventions`; map sang Jira ở `§Jira Integration`.

## Test Data Rules

> `generate-tc` + `review-tc` đọc. Đây là **DỮ LIỆU riêng dự án**;
> quy tắc TRÌNH BÀY nằm ở `~/.claude/skills/generate-tc/references/testcase-guide.md`.

- **Base URL / endpoint theo env:** **N/A** — FoxEco là **SDK nhúng trong app mobile FoxPro**,
  không có URL riêng. Bề mặt test = UI trong host app `FoxPro_Stag`, package `vn.fpt.ftel.sop.stg` (STG).
- **HTTP Status Contract:** chưa có đặc tả API ⇒ TBD (tài liệu v1.0 chỉ mô tả UI/nghiệp vụ).
- **Bộ `error.code`:** chưa có ⇒ TBD.
- **Response envelope:** chưa có ⇒ TBD.
- **Tài khoản test theo role:** 🔑 **QC cấp 5 tài khoản STG 2026-09-19.**
  ⭐ **Registry canonical (email · MNV · vai · chiến lược luân phiên · dữ liệu đã tạo): `04_test-data/valid/USR-accounts.md`**
  — ⛔ đừng nhân bản danh sách ra chỗ khác, mọi skill đọc ở đó.
  Secret (OTP dùng chung, mật khẩu) ở `~/.foxeco-v2/credentials.env` (`chmod 600`, ngoài repo).
  🔑 **OTP staging CỐ ĐỊNH, dùng chung mọi account, không đổi theo thời gian ⇒ AI TỰ ĐĂNG NHẬP ĐƯỢC.**
  🔴 Ghi chép cũ *"OTP nhập tay, AI không lấy được"* (VR-001 `§0` · VR-003 · VR-004) **ĐÃ LỖI THỜI**;
  TC từng `NOT_RUN` **chỉ vì OTP** nay chạy được.
  Đăng xuất: **FoxPro → `Cá nhân` → cuộn cuối → `Đăng xuất`** (⛔ không có trong FoxEco).
  Email nội bộ test auto-fill người nhận: `stag_anhdc4@fpt.com` (= *Đặng Châu Anh*, MNV `00286248`).
  *(⛔ Câu cũ "pre-logged-in tên hiển thị Chung Hoàng Liêm" là của 2 phiên vibe-test **đợt v1.0 CŨ** — không còn dùng.)*
- **Định dạng dữ liệu đặc thù:**
  - **Khung giờ mong muốn phải TƯƠNG ĐỐI so với "now"**, ⛔ KHÔNG hardcode giờ — app validate theo
    đồng hồ thật, giá trị mặc định hết hạn nếu form mở lâu (`DOC-v1.0-06 KP-01 §10.11`).
  - Chip **"Loại hàng"**: **8 chip**, nhãn chuẩn + mặc định là **`Tài liệu`** — BA chốt 2026-09-16
    (`C-ORD-09`, `v1.1/ORD-dang-tin/risk_assessment.md`). Quan sát app STG 2026-07 hiện `Giấy tờ, hồ sơ`
    ⇒ nếu STG còn nhãn đó là **defect UI**, ⛔ không sửa TC theo app. *(Ghi chú cũ "không tồn tại chip
    Tài liệu" hết hiệu lực cho v1.1.)*
  - Lý do huỷ đơn: tối thiểu **5 ký tự** (`VAL-04`) — UI hiện **chưa enforce** (`KP-01 §KB-CNL-02`).
- **Ràng buộc thiết lập dữ liệu:** TC cần đơn ở trạng thái `Đã ghép` trở đi **cần bên thứ 2 nhận đơn**
  — ngoài tầm kiểm soát tester ⇒ nhờ dev/QA seed dữ liệu STG (`KP-01 §10.12`).

## Report Rules & Quality Gates

> `test-report` + `create-test-plan` đọc.

- **Aggregation, không generation.** KHÔNG estimate, KHÔNG suy diễn số chưa có.
- **Trung thực:** NO-GO thì ghi NO-GO.
- **Trùng ngày ⇒ thêm suffix, KHÔNG ghi đè** file report cùng loại.
- **Nhiều người chạy cùng ngày ⇒ mỗi người 1 file** (suffix `-<account>`) để tránh conflict git.

**Quality Gates** (G1–G6 là baseline framework; G7+ là gate riêng project):

| Gate | Tiêu chí | Ngưỡng | Skill chịu trách nhiệm |
|---|---|---|---|
| G1 | TC Review score | ≥ 70 | review-tc |
| G2 | P1 TC đã execute | 100% | execute-maintain → test-report |
| G3 | Pass rate (effective) | ≥ 90% | test-report |
| G4 | P1 bug còn Open | = 0 | log-bug → test-report |
| G5 | Bug fix rate | ≥ 80% | test-report |
| G6 | Summary report đã tạo + review | Yes | test-report |
| G7+ | <gate riêng project — vd API schema validation, accessibility audit> | <...> | <...> |

## Automation Context

> ⚠️ Section này do `/init-source-code` GHI (append/replace). Không có automation ⇒ để `N/A`.
> Downstream (`scan-source-code`, `implement-automation`, `execute-maintain`, `review-src-tc`)
> đọc `Language` ở đây + `10_source-code/MEMORY.md §2 Tech Stack` để route đúng biến thể stack.

N/A — chưa scaffold source code. Chạy `/init-source-code --archetype <stack>` để sinh.

## Memory / Write-back Policy

> Section này trả lời: **file nào được phép to tới đâu**, và **lịch sử làm việc bị cắt ra thì đi
> về đâu**. Hook `memory-guard.py` đọc ở đây và cưỡng chế. Không khai ⇒ hook dùng trần khởi điểm
> của chính nó, ⛔ không tự đoán theo project.
>
> ℹ️ `/package-version` **KHÔNG đọc section này** — skill đó tự chứa luật đóng gói. Nếu section này
> khai luật đóng gói và **lệch** với skill: 🛑 skill DỪNG và báo, ⛔ không tự chọn bên thắng.

**① Trần dung lượng từng tầng** (khớp `.claude/hooks/memory-guard.py` hiện hành — không đổi số ở đây mà không sửa kèm hook):

| Tầng | File | Trần |
|---|---|---|
| 1 | `02_analyze-requirements/MASTER-MEMORY.md` | 60 KB |
| 2 | `02_analyze-requirements/v1.0/MEMORY.md` (router) | 90 KB |
| 3 | `02_analyze-requirements/v1.0/<MODULE>/*.md` (lá) | 250 KB (450 KB nếu module ≥150 SC — hiện chưa module nào chạm) |
| 4 | `WORKING-STATE.md` | 16 KB |
| 5 | `10_source-code/MEMORY.md` | 130 KB — N/A, project chưa scaffold automation |
| 6 | `08_test-runs/runs/FAIL-REGISTRY.md` | 200 KB |

🔴 **Trần nào làm file của sprint ĐÃ ĐÓNG đỏ là trần SAI** — nới trần, ⛔ đừng sửa file đã chốt.

**② Đích write-back chính thức** — lịch sử cắt ra khỏi MEMORY đi về đây, ⛔ không đẻ file mới (`docs/history/`, `*-log.md`, `*.bak`):

| Loại lịch sử | Đích |
|---|---|
| Lịch sử phân tích từng lượt | `02_analyze-requirements/v1.0/<MODULE>/CHANGELOG.md §1` (layout `module-first v2`) |
| Lịch sử sinh TC | `03_test-cases/v1.0/CHANGELOG.md` (TC Gen Log) |
| Lịch sử chạy test | `08_test-runs/runs/RUN-*.md` + `08_test-runs/runs/INDEX.md` |
| Lịch sử implement | `10_source-code/MEMORY.md` §Implementation Log — N/A hiện tại |
| Quyết định xuyên version | `MASTER-MEMORY.md §9 Notes` |
| Còn lại | `git log -p` — ⛔ không chép ra file |

**③ Nguồn canonical của số đếm:** frontmatter `counts:` của `<module>/test_scenario_map.md` (REQ/SC/NEW/MOD/CARRIED/DEPR/P1-P3) và `<module>/risk_assessment.md` (CL/RISK) — router `v1.0/MEMORY.md §2` và `MASTER-MEMORY.md §3` chỉ là bản dẫn xuất/roll-up; lệch thì **frontmatter module thắng**.

**④ Khối bất khả xâm phạm:** mọi dòng có `⛔`, cộng thêm mọi dòng `🔴`/`⚠️` mang ngày + người quyết ở `§Active Memory Rules` và `§Custom Rules`.

## Active Memory Rules

> Rule riêng của project mà framework không biết: UI quirk theo platform, ràng buộc môi trường
> build, quy ước field custom, định dạng dữ liệu đặc thù, quyết định đã chốt với BA/Dev…
> Mỗi rule ghi kèm **ngày** + **ai quyết** — để lần sau còn biết rule nào đã hết hiệu lực.

| Ngày | Rule | Người quyết |
|---|---|---|
| 2026-07-24 | `§Custom Rules §10.1` — UI phải khớp tài liệu mới được viết TC khẳng định | QA GiangDC2 |
| 2026-07-27 | `§Custom Rules §10.2` — màn có tab ⇒ mỗi tab ≥1 TC riêng verify data | QA GiangDC2 |
| 2026-09-15 | `§Custom Rules §10.3` — gộp seed dữ liệu dùng chung cho nhóm TC cùng module, ưu tiên tạo trạng thái qua UI flow thay vì nhờ dev seed DB | QA GiangDC2 |
| 2026-09-17 | `§Custom Rules §10.4` — Expected Result chỉ ghi tại step cuối cùng, không liệt kê Expected cho các bước giữa | QA GiangDC2 |
| 2026-09-17 | Xác nhận scope `CNL` = **IN scope v1.1** (`RISK-CNL-06` Resolved) — không còn treo PM. `NTF`/`TS` vẫn Pending, xử lý riêng khi tới lượt | QC GiangDC2 |
| 2026-07-27 | "Đánh giá" trong scope Phase 1 = **Quà ảo** (`GIFT-01`); chấm 1–5 sao là phase sau | BA/PO |
| 2026-09-07 | Tách 11 module (thêm `HOME`/`FEED`/`ACT`) thay 8 mã domain của đợt v1.0 cũ | QC GiangDC2 |
| 2026-09-07 | Phân tích lại v1.0 từ đầu theo bộ skill v1.1 (`module-first v2`); **scope = toàn bộ 11 module**, không giới hạn 5 luồng Phase 1 | QC GiangDC2 |
| 2026-09-07 | Chạy trên tài liệu hiện có (BRD v3.2 + PRD tái dựng từ demo). PRD version mới của PM khi có ⇒ chạy `--delta` version sau | QC GiangDC2 |
| 2026-09-07 | Thư mục module đổi sang `<CODE>-<slug>` (`ORD-dang-tin/`…) — xem cột `Dir` ở `§Module Codes`. **Token ID giữ mã ngắn** (`SC-ORD-001`), ⛔ không nhét slug vào ID | QC GiangDC2 |
| 2026-09-07 | **Scope viết TC = TOÀN BỘ 11 module (211 SC)**, gồm cả `CNL`/`NTF`/`TS` mà PM xếp out-of-scope Phase 1 — ⚠️ xác nhận PM cho **execute** vẫn treo (`RISK-CNL-06`/`RISK-NTF-06` Pending) | QC GiangDC2 |
| 2026-09-07 | **Mode `generate-tc` = `standard`** (1-1 scenario→TC, không áp technique B1–B8) ⇒ fragment KHÔNG có `## Coverage Matrix`, Notes `Technique:` là tuỳ chọn | QC GiangDC2 |

## Quy ước đếm scenario

> `analyze-requirements` + `health-check` đọc. Đợt v1.0 cũ chỉ ghi quy ước này ở `CLAUDE.md`
> (nơi skill KHÔNG đọc) nên bị `health-check` flag lặp lại mỗi lần chạy.

```
Tổng SC       = đếm TOÀN BỘ scenario, GỒM CẢ DEPRECATED
P1/P2/P3      = chỉ đếm scenario CÒN HIỆU LỰC (loại trừ DEPRECATED)
⇒ P1+P2+P3 CÓ THỂ NHỎ HƠN Tổng SC — KHÔNG phải sai số liệu
```

## Custom Rules

> Rule do QA ban hành, **không suy ra được từ tài liệu**. Áp cho MỌI skill sinh/viết TC
> (`analyze-requirements`, `generate-tc`, `vibe-test`) và cả khi liệt kê case trực tiếp trong chat.
> Nguồn: `DOC-v1.0-06 KP-03 §4` (chép nguyên văn).

### §10.1 — UI phải khớp Tài liệu mới được viết TC *(2026-07-24, QA GiangDC2)*

Chỉ viết TC **khẳng định** một field / nút / màn hình / hành vi UI khi **CẢ HAI** nguồn khớp nhau:
(a) tài liệu yêu cầu (BRD / PRD / US), **và** (b) bằng chứng UI thật (ảnh Figma hoặc app STG).

Không khớp ⇒ **KHÔNG tự suy đoán vị trí/hành vi UI**. Bắt buộc:
1. Ghi clarification mới `C-[MODULE]-NN`, đánh dấu rõ *"chưa xác nhận UI"*
2. **KHÔNG viết TC khẳng định** field/hành vi đó cho tới khi có xác nhận (BA/PO hoặc vibe-test)
3. Cần thiết thì viết 1 TC dạng **"GAP finding"** ghi nhận sự thiếu vắng, thay vì TC test hành vi giả định

**Case gốc:** `USR-07` "Cấu hình kênh liên hệ" — có trong BRD nhưng không có ở bất kỳ ảnh Figma
nào của màn Cá nhân và không thấy trên app STG.

### §10.2 — Màn có tab → mỗi tab 1 TC riêng verify data *(2026-07-27, QA GiangDC2)*

Màn có tab switcher lọc dữ liệu theo trạng thái (vd `Đang diễn ra` / `Đã hoàn thành`):
- **KHÔNG gộp** verify data nhiều tab vào 1 TC "chuyển tab qua lại"
- Mỗi tab **≥1 TC riêng** verify đúng data khi tab đó active (không lẫn dữ liệu tab khác)
- TC verify **cơ chế switch tab** giữ riêng, độc lập với các TC verify-data-theo-tab

**Lý do:** TC gộp khi FAIL không chỉ ra ngay tab nào sai. **Case gốc:** màn "Hoạt động" (`ACT`).

### §10.3 — Gộp seed dữ liệu dùng chung cho nhóm TC cùng module *(2026-09-15, QA GiangDC2)*

FoxEco không có API/admin seed (`§Test Data Rules`: SDK nhúng, không có URL riêng) ⇒ mọi trạng thái đơn
không tự tạo được bằng tay tester phải qua dev/QA hoặc qua flow UI thật. Khi ≥2 TC trong cùng module
cần cùng một nhóm trạng thái đơn:

1. **Seed 1 lần dùng chung**, KHÔNG lặp lại bước "Nhờ dev/QA seed …" đầy đủ ở từng TC riêng lẻ.
   Fragment phải khai 1 khối **"Seed dùng chung"** ngay sau dòng `Nguồn:` ở đầu file, đặt tên mã
   (`SEED-<MODULE>-NN`) và liệt kê đủ bộ đơn/trạng thái cần có cho cả nhóm TC dùng chung. Mỗi TC trong
   nhóm chỉ dẫn chiếu lại mã seed đó ở `Pre-condition`/`Test Data`.
2. **Ưu tiên tạo trạng thái qua flow UI thật** (multi-role: tài khoản phụ SENDER đăng tin → CARRIER
   nhận/giao) khi trạng thái tái tạo được qua app (`Chờ ghép`/`Đã ghép`/`Đang giao`/`Đã giao`/`Hoàn
   thành`) — để `/vibe-test` tự chủ chạy được, không phải dừng lại chờ dev mỗi TC. Chỉ ghi "Nhờ dev/QA
   seed" khi trạng thái **không tái tạo được qua UI** trong thời gian hợp lý (vd `Hết hạn` cần chờ thời
   gian thật hoặc sửa thẳng DB) — case này đánh dấu `⛔ không seed được qua UI` để `review-tc`/`vibe-test`
   biết cần chuẩn bị trước, không phải chờ giữa chừng.
3. Rà nhóm trạng thái/tài khoản đặc biệt dùng chung được (vd tài khoản "trắng" 0 đơn) và gộp seed tương
   tự bước 1, kể cả khi các TC không liền kề ID nhau.
4. 🔴 **CONSOLIDATE PHẢI MANG KHỐI SEED SANG TC-MASTER** *(bổ sung 2026-09-17 sau `review-tc` M-1)*.
   `/generate-tc --consolidate` phải sinh sheet **`Seed`** trong `TC-MASTER-v[X].xlsx` chứa **đủ định nghĩa của
   MỌI mã `SEED-*` mà TC trong file đó trỏ tới**, và mọi ô `Pre-condition`/`Test Data` chỉ được trỏ **sheet `Seed`
   của chính file**, ⛔ KHÔNG trỏ `"đầu fragment"` hay file khác.
   **Vì sao bắt buộc:** `TC-MASTER.xlsx` là artifact mà `execute`/`vibe-test` mở (`MASTER-MEMORY §6` · `CLAUDE.md`).
   Bước 1 ở trên chỉ bắt **fragment** khai khối Seed ⇒ trước lượt sửa này, **88/223 TC (39%) của v1.1** trỏ 21 mã
   `SEED-*` mà workbook **không có định nghĩa nào**; riêng `SEED-DLV-01` còn nằm ở **file thứ ba**
   (`03_test-cases/v1.0/CHANGELOG.md`). Người chạy mở workbook không tra được ⇒ đúng thứ mà §10.3 sinh ra để tránh.
   **Kiểm nhanh:** tập `SEED-*` bị TC trỏ **phải bằng** tập được định nghĩa ở sheet `Seed`; lệch ⇒ chưa consolidate xong.

**Lý do:** seed lặp lại theo từng TC khiến `/vibe-test` phải dừng xin dev/QA seed nhiều lần cho cùng
1 module thay vì 1 lần, giảm mạnh hiệu quả "AI thay manual tester". **Case gốc:** `ACT` — 8/14 TC lặp
lại bước seed riêng lẻ dù dùng chung được 1 bộ đơn (`SEED-ACT-01`) + 1 tài khoản trắng (`SEED-ACT-02`).

### §10.4 — Expected Result chỉ ghi tại step cuối cùng *(2026-09-17, QA GiangDC2)*

Mỗi TC chỉ có **ĐÚNG 1 dòng Expected Result**, neo vào **step CUỐI CÙNG** của TC. **KHÔNG** liệt kê
Expected cho các step giữa — vd TC có 9 step thì Expected chỉ ghi cho step 9, không ghi step 6/7/8
(kể cả khi step 6/7/8 là step quan sát/`Check`).

> Ghi đè `testcase-guide.md §B.4.3` của skill `generate-tc` (bản gốc cho phép TC validation/security
> nhiều tầng có 2–3 dòng Expected neo nhiều step) — dự án này chỉ áp **1 dòng Expected/TC**, không có
> ngoại lệ nhiều tầng.

Khi 1 scenario vốn có nhiều điểm kiểm chứng độc lập (không gộp được vào 1 câu Expected cuối mà không
mất khả năng bắt lỗi riêng của từng điểm), xử lý theo đúng thứ tự ưu tiên:

1. **Ưu tiên sắp xếp lại Steps** để điểm kiểm chứng **quan trọng nhất** rơi đúng vào step cuối. Các
   quan sát phụ (không tự thân là 1 case fail độc lập, hoặc đã được TC khác trong cùng lô cover) giữ
   làm Steps bình thường (không gắn Expected) — hoặc nếu nhiều quan sát cùng thuộc **1 trạng thái tĩnh
   không đổi giữa các quan sát** (vd nhấn lần lượt vào nhiều field chỉ-đọc rồi check chung 1 lần) thì
   **gộp thành 1 step Check cuối cùng + 1 câu Expected duy nhất** liệt kê đủ các quan sát.
2. **Chỉ khi (1) làm mất khả năng vibe-test một hành vi/case cụ thể** — case đó có thể FAIL độc lập với
   các case còn lại trong TC (vd 2 định dạng invalid khác nhau, 2 chiều Given/Then đối lập, cặp biên
   BVA) — thì **tách thành TC riêng**, mỗi TC 1 điểm kiểm chứng đúng ở step cuối. Áp dụng chiến lược ID
   theo `testcase-guide.md §A.2` (renumber liên tục + `*-ID-MAPPING.md`, hoặc để lỗ) khi tách TC làm
   lệch dải ID đã phát hành.
3. **CẤM xoá âm thầm coverage đã có** — mọi điểm kiểm chứng đang tồn tại phải được giữ lại bằng (1)
   hoặc (2), không được bỏ hẳn để "cho gọn". Mục tiêu tối thượng là **tối đa số case vibe-test được**,
   không phải tối thiểu số dòng Expected.

**Case gốc:** lô `TC-USR-v1.1` (generate 2026-09-16/17) — nhiều TC có 2–5 dòng Expected neo nhiều step
giữa (vd `TC-USR-022` cũ neo cả step 13 "đơn cũ giữ nguyên" và step 15 "wizard nhận giá trị mới";
`TC-USR-021` cũ neo 5 step kiểm 5 trường chỉ-đọc khác nhau).

### §10.5 — 🔒 SỐ LƯỢNG TC ĐÃ CHỐT VỚI TEAM — AI KHÔNG ĐƯỢC THAY ĐỔI *(2026-09-18, QA GiangDC2)*

> Áp cho **mọi skill chạm TC sau ngày chốt**: `vibe-test` · `execute-maintain` · `log-bug` · `test-report`
> · `export-tc-rp` · `health-check` — và cả khi liệt kê/sửa TC trực tiếp trong chat.

**Số lượng test case tính đến 2026-09-18 đã chốt với team dự án ⇒ FREEZE.** Trong quá trình test, AI
**KHÔNG được thay đổi số lượng TC** dưới bất kỳ hình thức nào: ⛔ không thêm TC mới · ⛔ không xoá TC ·
⛔ không tách 1 TC thành nhiều · ⛔ không gộp nhiều TC thành 1 · ⛔ không đổi dải ID.

**Bảng chốt (nguồn: `TC-MASTER`, sheet `ALL`, đếm 2026-09-18):**

| Version | Σ TC | ACT | ASN | CNL | DLV | FEED | GIFT | HOME | NTF | ORD | TS | USR |
|---|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|
| **v1.1** | **223** | 10 | 13 | 13 | 51 | 5 | 8 | 11 | 9 | 48 | 17 | 38 |
| **v1.0** | **219** | 14 | 21 | 14 | 30 | 14 | 12 | 24 | 16 | 54 | 7 | 13 |

**Được phép sửa (không đụng số lượng):** `Steps` · `Expected Result` · `Test Data` · `Pre-condition` ·
`Notes` · `Status` (`Pass`/`Fail`/`Blocked`/`Skipped`) · `Lifecycle` (vd `DESCOPED` cho case không còn
xảy ra trong thực tế) · `Assigned To`.

**Case không chạy được / không còn đúng nghiệp vụ:** đánh `DESCOPED` + `Skipped` kèm lý do và nguồn
chốt, **giữ nguyên dòng TC trong fragment + TC-MASTER để truy vết** — ⛔ TUYỆT ĐỐI KHÔNG xoá dòng.
Mẫu số coverage khi báo cáo thì trừ các TC `DESCOPED` ra, nhưng Σ TC của bảng trên **không đổi**.

**Phát hiện thiếu case / thừa case khi test:** ghi vào `Notes` của TC gần nhất + 1 dòng ở
`<module>/CHANGELOG.md`, rồi **báo QC** — ⛔ không tự thêm/bớt. Số lượng chỉ được đổi qua một lượt
`generate-tc` / `review-tc-ba` **mới, có QC duyệt và chốt lại với team**, và lượt đó phải cập nhật
lại bảng chốt ở trên.

**Kiểm nhanh (mọi skill tự chạy trước khi ghi kết quả):** đếm số dòng TC theo module ở `TC-MASTER`
phải **khớp đúng bảng chốt**; lệch ⇒ dừng, không ghi §8, báo QC.

**Lý do:** số lượng TC là con số đã cam kết với team dự án (scope + effort + tiến độ báo cáo). Tự ý
thêm/bớt giữa lượt test làm lệch mọi mẫu số coverage, báo cáo round và cam kết đã phát hành.
