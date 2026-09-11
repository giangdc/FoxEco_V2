# TC Baseline v1.0 — Ghi chú chuyển đổi

## Đã làm gì

Chuyển **323 TC** từ template ISC SDLC **42 cột** (định dạng của bộ skill cũ) sang **schema 16 cột A–P** mà
`generate-tc` v1.1 dùng làm TC-MASTER. Mục đích: có **parent TC-MASTER** để cơ chế `CARRIED` hoạt động khi
chạy `/analyze-requirements --delta` ở version sau.

> Skill ghi rõ: *"CARRIED scenarios không có TC-MASTER-v[parent] → **Skip regression, log warning**"*.
> Không có file này thì mọi scenario CARRIED sẽ bị bỏ qua âm thầm.

## Nội dung thư mục

| File | Mô tả |
|---|---|
| `TC-MASTER-v1.0.xlsx` | 16 cột · sheet `Overview` + `ALL` (323 dòng, canonical) + 9 sheet per-module |
| `fragments/TC-<MODULE>-v1.0.md` | 9 fragment Markdown đúng format v1.1 (`fragment-meta` + `## Test Cases` + `## Coverage Matrix`) |
| `TC-SC-MAPPING-TODO.md` | ⚠ Việc còn thiếu — bảng 89 scenario + số TC từng scenario, có checksum |
| `ISC_FoxEco_v1.0_TC_v1_R1.xlsx` | **Bản gốc 42 cột**, giữ nguyên để đối chiếu |

## Bảng ánh xạ cột

| Mới (16 cột) | Cũ (42 cột) | Ghi chú |
|---|---|---|
| A Testcase ID | (formula) | **Giữ nguyên ID gốc** `TC_01.1`…`TC_09.16` — xem lý do bên dưới |
| B Scenario ID | — | ⚠ **KHÔNG có ở nguồn** → để trống |
| C Req ID | B Req ID | |
| D DOC Source | C DOC Source | |
| E Group | D Group | |
| F Priority | E Priority | `High→P1` · `Medium→P2` · `Low→P3` |
| G Test Title | F Test Title | |
| H Pre-condition | G Pre-condition | |
| I Steps | H Test Steps | |
| J Expected Result | I Expected Result | |
| K Test Data | — | ⚠ Nguồn để inline trong Steps → để trống |
| L Status | AO Status | |
| M Notes | AP Remark | + tên **Block** gốc + tag carried + marker SC chưa map |
| N Version Origin | — | `v1.0` |
| O Lifecycle | — | `CARRIED` |
| P Assigned To | — | trống (Solo mode) |

**Cột nguồn bị bỏ:** `J Origin` · `K Review` · `L Automated` · `M Script` · `N–AL` (dữ liệu 5 round R1–R5, toàn bộ trống vì chưa execute) · `AM–AN` (KQ tổng).

## Hai quyết định cần biết

### 1. Giữ nguyên Testcase ID gốc (`TC_01.1`), KHÔNG đổi sang `TC-[MODULE]-[NNN]`

Schema mới quy ước `TC-[MODULE]-[NNN]`, nhưng ID cũ được **giữ nguyên có chủ đích**:

- ID `TC_04.22`, `TC_08.7`… đã được trích dẫn trong **evidence vibe-test**, `KP-04`, `KP-05` và `review-report-v1.0.md`
- Nguyên tắc 9 của skill: *"**KHÔNG rewrite citation** trong artifact/report đã ký khi file nguồn bị xoá"*

Đổi số = làm mồ côi toàn bộ tham chiếu đó. TC sinh mới ở version sau sẽ dùng format mới của `generate-tc`; baseline carried mang format cũ là chấp nhận được và trung thực hơn.

### 2. Cột `Scenario ID` để TRỐNG, không suy đoán

Template ISC 42 cột **không có** cột `Scenario ID` (bị bỏ khi migrate 2026-07-21), nên dữ liệu này **không tồn tại**
ở bất kỳ đâu — cả TC-MASTER lẫn 9 fragment gốc.

Có thể suy ra bằng vị trí (Coverage Matrix là phân hoạch chính xác, tổng khớp 9/9 module), nhưng suy đoán vị trí
có thể sai âm thầm — đúng loại lỗi mà `Project_rule §10.1` sinh ra để chặn. Vì vậy: **để trống + đánh dấu**
`⚠ SC ID chưa map` ở Notes, kèm `TC-SC-MAPPING-TODO.md` có đủ dữ liệu và checksum để hoàn thiện.

## Verify sau chuyển đổi

| Kiểm tra | Kết quả |
|---|---|
| Tổng TC | **323 / 323** ✅ |
| Per-module | 20 · 17 · 27 · 109 · 32 · 31 · 44 · 27 · 16 ✅ khớp tài liệu |
| Coverage Matrix là phân hoạch đúng | ✅ 9/9 module, tổng `Total TCs` = số TC thật |
| Dòng section/Block bị loại khỏi bảng TC | ✅ (67 dòng section, giữ tên Block vào Notes) |
| Dữ liệu round R1–R5 | ✅ bỏ hết (vốn trống 100%) |

## ⚠ Chất lượng nội dung — KHÔNG dùng làm chuẩn

Chuyển đổi này chỉ đổi **định dạng**, không sửa nội dung. Bộ TC v1.0 có lỗi đã biết:

1. Mọi TC nhắc chip **"Tài liệu"** đều sai chữ — app thật là **"Giấy tờ, hồ sơ"**
2. Scenario "Loại hàng bắt buộc" **không kiểm chứng được** qua UI (chip luôn có default)
3. `TC_04.71` expected "checkbox điều khoản tick sẵn" — thực tế **không tick sẵn**
4. TC về "Tên Người gửi read-only" — thực tế **edit được và bị xoá trắng**
5. TC về "Địa chỉ lấy hàng pre-fill" — thực tế **không pre-fill**

Ngoài ra chỉ **17/323 TC** từng chạy thật trên app; điểm review 84/100 đến từ **self-review** (Direct mode, cap 85).

→ Chi tiết: `../02_seed/KP-04_prior-analysis-baseline.md §4` và `../00_input-seed/_knowledge-pack/KP-05`.
