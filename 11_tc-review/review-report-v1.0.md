# TC Review Report — v1.0

> Generated: 2026-09-07 · Run by: GiangDC2
> Mode: **FULL** · Reviewer: **4 instance context-độc-lập** (mỗi instance chỉ nhận catalog check + payload dữ liệu, không biết TC do ai viết) — chia theo chiều check: R1+R4 · R2 · R3 (`ORD`/`DLV`/`HOME`) · R3 (8 module còn lại)
> TC-MASTER: `03_test-cases/v1.0/TC-MASTER-v1.0.xlsx` — 219 TC / 11 module, parse bằng openpyxl từ sheet `ALL`
> Score: **0/100** — **REJECTED** · Quality Gate G1 (≥70): **FAIL** ⇒ block downstream

⚠️ **Disclaimer — score cap:** không có `ANTHROPIC_API_KEY` trong env nên KHÔNG gọi được independent reviewer qua Anthropic API như `reviewer-agent.md §4` quy định. Thay thế bằng 4 instance context-độc-lập (không mang theo context tạo TC). Theo `§6`, nhánh không-API vẫn áp **score cap 85** — lượt này cap không có hiệu lực vì score thô đã dưới ngưỡng.

📌 **Đính chính:** persona reviewer **CÓ tồn tại** ở `~/.claude/skills/review-tc/references/reviewer-agent.md`. Đường dẫn `review-agent/AGENT.md` mà `KP-05 §6` (đợt cũ) báo thiếu là **vị trí cũ đã bị bỏ** (không đúng Agent Skills spec) — không phải nguyên nhân cap.

## Setup áp luật

| Hạng mục | Giá trị |
|---|---|
| Mode (TC Gen Log) | `standard` ⇒ áp **R1-14**; skip **R1-15 · R2-13 · R2-14** |
| Loại module | 100% UI (0 TC `Group="API"`) ⇒ `testcase-guide §A + §B`; không áp §C |
| R3-13 | **CÓ áp** — analyze có Source Detail (119 Source Quote per-SC) |
| Legacy style cutoff | **Không miễn trừ** — 219/219 TC `Version Origin = v1.0` sinh 2026-09-07 (sau mốc 2026-08-10) ⇒ chấm đủ severity |
| Severity | Chuẩn hoá lại theo catalog `full.md` Step 4 — **0/89 finding lệch nhãn** so với nhãn reviewer tự gán |

## Summary

| Severity | Count |
|----------|-------|
| 🔴 CRITICAL | 0 |
| 🟠 MAJOR | 36 |
| 🟡 MINOR | 36 |
| 🔵 INFO | 17 |
| **Tổng** | **89** |

## Findings

### 🔴 CRITICAL (0)

Không có. `R1-01` (ID trùng), `R1-03` (anchor integrity — 835 dòng Steps / 344 dòng Expected: 0 dangling · 0 gộp dải `N-M.` · 0 mã tham chiếu trong Steps), `R2-01`/`R2-02` (SC chưa có TC) đều 0 finding.

### 🟠 MAJOR (36) — nhóm theo check

| Check | # | TC / phạm vi | Vấn đề |
|---|--:|---|---|
| **R2-04** | 1 | `module:ORD` | **Biên 200/201 ký tự** của `Địa chỉ lấy hàng` (`D8.1` L364) và `Điểm xuất phát` form OFFER (`D8.2` L381) **0 TC phủ**, và omission **không được khai** ở header fragment — trong khi `HOME`/`USR`/`FEED` đều dùng khuôn "Không sinh TC khẳng định cho…". Kèm nhánh chặn **29 phút** của `Thời gian di chuyển` OFFER (`D8.2` L385) chỉ phủ ở wizard NEED |
| **R3-01** | 7 | `TC-ORD-004 · TC-ORD-022 · TC-ORD-023 · TC-ORD-026 · TC-ORD-027 · TC-ORD-028 · TC-ORD-029 · TC-ORD-033 · TC-ORD-034 · TC-ORD-038 · TC-ORD-043 · TC-ORD-052 (12 TC, gộp 1 finding)`, `TC-DLV-021`, `TC-DLV-024`, `TC-ORD-053` … (+3) | Step test (không nhãn `(setup)`) viết mô tả chung, thiếu element hoặc giá trị cụ thể: "nhập đủ thông tin", "khung giờ hợp lệ", "sửa tin", "nhấn nút quay lại nhiều lần", hoặc có nhánh "nếu còn hiển thị" / "hoặc chờ thêm 2 giờ" ⇒ 2 người chạy ra 2 kết quả |
| **R3-02** | 8 | `TC-ORD-024`, `TC-ORD-025`, `TC-ORD-032`, `TC-ORD-021` … (+4) | Expected ghi "hiện thông báo lỗi …" **không có chuỗi verbatim** ⇒ app hiện thông báo sai nội dung vẫn PASS (§B.4.1). Chính bộ TC này đã làm verbatim ở `TC-ORD-009/019/020` nên là bỏ sót, không phải thiếu nguồn |
| **R3-03** | 1 | `TC-ORD-004 · TC-ORD-018 · TC-ORD-022 · TC-ORD-023 · TC-ORD-026 · TC-ORD-033 · TC-ORD-038 · TC-ORD-043 · TC-ORD-052 (9 TC, gộp 1 finding)` | Steps tiêu thụ dữ liệu (địa chỉ, email, ngày, khung giờ) nhưng cột Test Data chỉ khai phần biến thiên của rule đang test |
| **R3-09** | 1 | `TC-ORD-042 · TC-ORD-043 · TC-ORD-044 · TC-ORD-050 (4 TC, gộp 1 finding)` | Nút submit form OFFER gọi bằng mô tả chung "nút đăng tin", không có nhãn verbatim trong ngoặc kép (§A.3) — trong khi luồng NEED dùng đúng "Đăng tin ngay" |
| **R3-14** | 12 | `TC-DLV-001`, `TC-HOME-004`, `TC-HOME-019`, `TC-HOME-021` … (+8) | Pre-condition khẳng định trạng thái phải-dựng: **lặp lại** đúng thứ mà step `(setup)` đã dựng (35 TC), hoặc **không có step dựng nào** (7 TC). Vi phạm luật vàng §B.2 |
| **R3-17** | 4 | `TC-ORD-024`, `TC-ORD-025`, `TC-ORD-030`, `TC-DLV-024` | Expected liệt kê **2 kỳ vọng thay thế nhau bằng "hoặc"** ⇒ không assert cứng, nhánh nào cũng PASS (§B.4.4) |
| **R4-02** | 2 | `TC-HOME-006`, `TC-USR-012` | Priority không nhất quán trong cùng module: `TC-HOME-006` (P3) là cặp đối chứng âm của `TC-HOME-005` (P2) — và chính nó là TC **dự kiến FAIL**; `TC-USR-012` (P3) phủ 6 thành phần header, bao trùm `TC-USR-002` (P2) phủ 4 trường |

### 🟡 MINOR (36) — nhóm theo check

| Check | # | Vấn đề |
|---|--:|---|
| R3-04 | 1 | Test Data không khớp catalog (`TC-HOME-007`) |
| R3-05 | 4 | Title dài ≥18 từ (39 TC) vượt trần ~12–15 từ của §B.1; 3 TC thiếu vế cụ thể |
| R3-06 | 2 | Step test gộp 2–4 hành động vào 1 số — **125 TC / ~200 step** |
| R3-10 | 2 | Trộn Anh/Việt trong cùng TC (11 TC) |
| R3-12 | 7 | Expected thiếu giá trị đo được cụ thể ("hiển thị đúng" thay vì con số/chuỗi) |
| R3-19 | 3 | Step dựng tiền đề **thiếu nhãn `(setup)`** — **70 TC**; kèm 1 ca ngược (`TC-USR-005` s2 gắn nhãn cho step mang chính oracle) |
| R3-20 | 2 | Pre-condition ≥2 điều kiện dồn 1 dòng (`TC-HOME-002` + 3 TC) |
| R4-01 | 6 | **Trộn 2 hệ thuật ngữ cho 3 vai** — `Sender/Carrier/Receiver` ⟷ "người gửi/người vận chuyển/người nhận": 67 TC dùng EN · 104 TC dùng VI · **37 TC dùng cả hai trong cùng dòng**. Vi phạm §A.3 "1 khái niệm = 1 từ" |
| R4-03 | 4 | Pre-condition cùng nội dung nhưng viết khác nhau giữa các TC (34 TC) |
| R4-07 | 5 | **DOC Source 15 biến thể**, đảo thứ tự cho cùng tập nguồn: `01 · 02` 9 TC ⟷ `02 · 01` 10 TC; `06 · 02` 4 ⟷ `02 · 06` 8; lệch ngay trong cùng hàng ma trận DLV ⇒ RTM/pivot đếm sai |

### 🔵 INFO (17) — không trừ điểm

| Check | # | Nội dung |
|---|--:|---|
| R1-14 | 1 | Notes trống ở một số TC (Mode `standard` ⇒ Info) |
| R2-06 | 1 | **15 SC bị chặn bởi 8 CL còn Open** (`C-ORD-06` chiếm 6/15). Coverage đủ, nhưng SC gốc yêu cầu "GHI NHẬN, không assert" còn TC đã assert cứng theo §B.4.4 ⇒ rủi ro viết lại khi BA chốt |
| R2-10 | 2 | Coverage **211/211 SC · 0 orphan · Req ID khớp 100% SC** (0/219 mismatch). REQ-level 110/116 — 6 REQ trắng là gap chủ đích ở analyze, **CHANGELOG tầng TC chỉ khai 1/6** |
| R3-07 | 2 | Expected chứa nhiều verification trong 1 dòng (82 TC) |
| R3-13 | 5 | Drift nhẹ TC ⟷ Source Quote (5 ca) — đáng chú ý: `SC-FEED-002` ghi **6 thành phần** card, `TC-FEED-002` ghi **5** (badge tách sang `TC-FEED-003/004`, đã khai ở Notes nhưng số liệu Title lệch SC) |
| R3-18 | 3 | `Mục đích` chỉ nói lại Title/tag (3 TC) |
| R4-04 | 1 | Data reuse giữa nhiều TC |
| R4-06 | 2 | 2 cặp TC nghi trùng cách kiểm |

### Ngoài catalog — soát thêm (không tính điểm, không có check ID)

- **Cột `Group` không dùng giá trị `Validation` lần nào** (94 Business Rule · 63 UI · 62 Functional). Theo §A.5, ca maxlength/format/biên thuộc `Validation`; **28 TC** đang là `Business Rule` mang dấu hiệu validation. Enum vẫn hợp lệ nên không phải `R1-11`.
- **Payload trích SC lệch cột ở 2 dòng** (`SC-FEED-002`, `SC-HOME-009` — do ký tự `|` escape trong ô `Then`) ⇒ `R4-02` đối chiếu được 216/219 TC. Lỗi ở script trích payload, không phải ở TC-MASTER.

## Version-Specific Checks

| Check | Result |
|-------|--------|
| CARRIED TCs included | 0/0 — v1.0 không có SC CARRIED (`MASTER-MEMORY §4`) ✅ |
| DEPRECATED TCs removed | Y — 0 SC DEPRECATED ✅ |
| Version Origin filled | Y — 219/219 = `v1.0` ✅ |
| Lifecycle matches MASTER-MEMORY | Y — 219/219 `NEW`, khớp `§3` roll-up 211 SC NEW ✅ |

## Score Breakdown

```
Score = 100 - (CRITICAL 0×5 + MAJOR 36×3 + MINOR 36×1)
      = 100 - (0 + 108 + 36) = -44  -> clamp [0,100] = 0
Score cap direct/non-API (85): min(0, 85) = 0
```
**Quality Gate G1 (≥70): FAIL** — verdict `REJECTED` (thang 0-49) ⇒ **block downstream** (`vibe-test`, `export-tc-rp --phase report`, `test-report`).

> 📐 **Ghi chú cơ học điểm (không phải lý do miễn trừ):** 0 Critical, và 36 Major tập trung ở **3 pattern hệ thống** (`R3-14` 12 · `R3-02` 8 · `R3-01` 7 = 27/36). Công thức trừ tuyến tính trên bộ 219 TC nên chỉ ~34 Major là chạm sàn 0 ⇒ score 0 **không** phân biệt được "3 lỗi hình thức lặp trên nhiều TC" với "bộ TC vô giá trị". Đây đúng hiện tượng `full.md` Step 5 mô tả ở mục legacy cutoff, nhưng miễn trừ đó **không áp** cho TC sinh sau 2026-08-10 ⇒ verdict giữ nguyên FAIL.

## Fix routing — thứ tự khuyến nghị

| # | Việc | Phạm vi | Điểm thu hồi | Ai sửa |
|---|---|---|--:|---|
| 1 | **Expected verifiable + assert cứng**: thêm chuỗi verbatim hoặc đổi sang hệ quả quan sát được (nút disable / wizard không chuyển bước / field giữ N ký tự); bỏ mọi "hoặc" | `R3-02` 8 TC + `R3-17` 4 TC + `R3-12` 7 TC | +43 | `/generate-tc --regenerate --module ORD` · `DLV` · `TS` |
| 2 | **Tách Pre-condition ⇄ Setup**: xoá mệnh đề data khỏi Pre-condition khi đã có step `(setup)`; thêm step dựng khi thiếu | `R3-14` 42 TC (12 finding) | +36 | như trên (HOME nặng nhất) |
| 3 | **Step test thiếu element/giá trị** | `R3-01` 15 TC + `R3-09` 4 TC + `R3-03` 9 TC | +27 | như trên |
| 4 | **Bổ sung TC biên 200/201 + nhánh 29 phút form OFFER**, hoặc khai miễn trừ ở header fragment | `R2-04` module ORD | +3 | `/generate-tc --regenerate --module ORD` |
| 5 | **Chuẩn hoá thuật ngữ 3 vai** (chọn 1 hệ, replace toàn bộ) + **thứ tự DOC Source** + nhãn `(setup)` + tách 1-step-1-action + rút Title | `R4-01` `R4-07` `R4-03` `R3-19` `R3-06` `R3-05` `R3-10` `R3-04` `R3-20` | +33 | refactor cơ học 1 lượt |
| 6 | **Priority `TC-HOME-006` / `TC-USR-012`** — ⚠️ 2 TC này **kế thừa nguyên priority từ SC** (chỉ `TC-USR-006` là do generate-tc tự hạ) ⇒ sửa ở tầng analyze rồi đồng bộ TC | `R4-02` 2 TC | +6 | `/analyze-requirements --update` |

Sửa hết mục 1–5 (không đụng thiết kế TC — chỉ hình thức Steps/Expected/Pre-condition + 1 nhóm TC biên mới) đưa score về vùng **APPROVED**. Chạy `/review-tc --recheck` để cập nhật score.
