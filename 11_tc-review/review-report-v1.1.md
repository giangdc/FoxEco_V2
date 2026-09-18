# TC Review Report — v1.1

> Generated: 2026-09-17
> Mode: **Direct** (fallback — không có `ANTHROPIC_API_KEY`, theo `review-tc/references/reviewer-agent.md §6`)
> TC-MASTER: `03_test-cases/v1.1/TC-MASTER-v1.1.xlsx` — 223 TC · 11 module · mode `standard`
> Score: **80/100** — **CONDITIONAL (fix recommended)** · Quality Gate G1 **PASS**
> 🔄 **Recheck 2026-09-17: 85/100** — 0 CRITICAL · 0 MAJOR · 0 MINOR (điểm thô 100, cap direct mode 85). Xem mục `Recheck` cuối file.
> ✅ **Cập nhật 2026-09-17: TOÀN BỘ 2 MAJOR + 14 MINOR ĐÃ FIX** — xem mục `Fix applied` cuối file. Score ở dòng trên là **điểm lúc review**, ⛔ chưa tính lại; chạy `/review-tc --recheck` để chốt (dự kiến **85** = 86 bị cap direct mode).

> ⚠️ **Self-review disclaimer.** TC do AI tạo trong cùng chuỗi session; không gọi được independent reviewer agent
> (thiếu `ANTHROPIC_API_KEY`) nên đây là **direct review**, **score cap 85** đã áp. Khuyến nghị review chéo bởi
> team member trước khi coi G1 là kết luận cuối.

## Summary

| Severity | Count |
|----------|------:|
| 🔴 CRITICAL | 0 |
| 🟠 MAJOR | 2 |
| 🟡 MINOR | 14 |
| 🔵 INFO | 3 |

**Bối cảnh chấm:** Mode = `standard` (17/17 dòng TC Gen Log) ⇒ áp R1-14, **skip** R1-15 · R2-13 · R2-14.
`Group = API`: **0 TC** ⇒ toàn bộ chấm theo `testcase-guide.md §A + §B` (UI).
**Legacy style cutoff KHÔNG áp:** TC v1.0 sinh 2026-09-07/15, v1.1 sinh 2026-09-16/17 — đều **sau** mốc 2026-08-09/10
⇒ 223/223 TC chấm đủ severity, không TC nào được miễn trừ.

---

## Findings

### 🔴 CRITICAL (0)

Không có.

### 🟠 MAJOR (2) — ✅ **cả 2 đã fix 2026-09-17**

#### M-1 · `R1-03` (tinh thần "TC phải TỰ ĐỦ") — Khối **Seed dùng chung KHÔNG có trong TC-MASTER**

| | |
|---|---|
| **Phạm vi** | **88/223 TC (39%)** trỏ tới **21 mã `SEED-*`** · trong đó **17 TC** ghi thẳng *"xem ghi chú Seed dùng chung **đầu fragment**"* |
| **Mã bị trỏ** | `SEED-ACT-02/03` · `SEED-ASN-01` · `SEED-DLV-01..05` · `SEED-GIFT-01/02/05/06/08` · `SEED-HOME-01..03` · `SEED-ORD-01..04` · `SEED-TS-01` |
| **Vấn đề** | Định nghĩa 21 khối seed này chỉ tồn tại ở `fragments/TC-*-v1.1.md`. Quét toàn bộ 13 sheet của `TC-MASTER-v1.1.xlsx`: **0 định nghĩa** — chỉ có các dòng *tham chiếu* trong ô `Pre-condition`. |
| **Vì sao đây là lỗi thật** | `MASTER-MEMORY §6` + `CLAUDE.md` đều chốt **TC-MASTER.xlsx là artifact mà `execute`/`vibe-test` mở**. Người chạy mở workbook sẽ thấy `SEED-ASN-01` và câu *"xem ghi chú đầu fragment"* mà **không có cách nào tra trong chính file đó** ⇒ 88 TC không tự chạy được. Điều này đánh thẳng vào mục đích của `Project_rule §10.3` (*"để `/vibe-test` tự chủ chạy được, không phải dừng lại chờ dev mỗi TC"*). |
| **KHÔNG phải lỗi của generate-tc** | `§10.3` quy định *"**Fragment** phải khai 1 khối Seed dùng chung… Mỗi TC chỉ dẫn chiếu lại mã seed đó"* — generate-tc làm **đúng** luật. Lỗ hổng nằm ở chỗ **không luật nào bắt bước `--consolidate` mang khối Seed sang workbook**. |
| **Fix** | Thêm sheet `Seed` (hoặc block trong sheet `Overview`) chứa đủ 21 định nghĩa khi consolidate → chạy `/generate-tc --consolidate`. Kèm bổ sung 1 câu vào `Project_rule §10.3`: *"khối Seed phải được carry sang TC-MASTER lúc consolidate"* — nếu không, lượt sau tái phát. |

#### M-2 · `R2/R4` cross-file — `MASTER-MEMORY §3` thiếu `SC-FEED-002` ⇒ **mẫu số coverage sai**

| | |
|---|---|
| **Bằng chứng** | `v1.0/FEED-bang-tin/test_scenario_map.md` L45: `SC-FEED-002` ghi *"**hết gap CTA 2026-09-16**"*, `DOC Source` = *"vibe-check demo 2026-09-16"* ⇒ **SC này bị sửa ở v1.1**. Fragment `TC-FEED-v1.1.md` cũng khai: *"4 TC ứng với **4 SC vừa đổi Then** (`TC-FEED-002/007/009/013`)"*, và `TC-FEED-002` mang `Lifecycle = MODIFIED`. |
| **Lệch** | `MASTER-MEMORY §3` dòng `FEED` chỉ liệt `SC-FEED-007` · `009` · `013` — **thiếu `SC-FEED-002`**. |
| **Hệ quả** | Mẫu số *"SC phải test"* đang ghi **139**; số đúng là **140**. Coverage thật = **139/140 = 99.3%** (không phải 138/139). `§8b` + `03_test-cases/v1.1/CHANGELOG.md` ghi *"140 SC"* — hoá ra **2 nguồn đó đúng**, `§3`/`§4`/`§1` sai. |
| **Fix** | Thêm `SC-FEED-002` vào cột MODIFIED của dòng `FEED` ở `§3`; sửa `139 → 140` ở `§1` · `§3` (khối ⚠️ FEED) · `§4`. ⛔ Không đụng TC — TC đã đúng. |

### 🟡 MINOR (14)

#### R3-19 · Step thuần setup thiếu nhãn `(setup)` — **12 TC**

Luật `testcase-guide.md §B.3`. Đối chứng: **563 step ở 208/223 TC đã gắn nhãn đúng** ⇒ luật được áp, chỉ **không đều**.

| Nhóm | TC | Chi tiết |
|---|---|---|
| **TC không dùng nhãn nào** (7) | `TC-CNL-006` · `015` · `016` · `017` · `018` · `019` · `020` | Step 1 = *"Đăng nhập bằng tài khoản X, mở màn Theo dõi đơn của đơn đó."* — thuần đăng nhập + điều hướng |
| **Lệch NỘI BỘ** (5) — TC có gắn nhãn ở step khác nhưng bỏ sót step này | `TC-HOME-008` (step 5) · `TC-HOME-029` (step 4) · `TC-HOME-031` (step 4) | *"Đăng nhập lại bằng tài khoản A và mở Trang chủ."* |
| | `TC-ORD-048` (step 3, 4) | *"Đăng nhập bằng tài khoản B, nhấn tab Bảng tin…"* |
| | `TC-GIFT-008` (step 2) | *"Nhấn tab Cá nhân và nhấn mục menu Quà đã nhận."* — step 1 đã có nhãn |

**Fix:** thêm ` (setup)` vào cuối các step trên.

> ⚠️ **8 TC khác bị bộ dò bắt nhưng KHÔNG flag** (`TC-ACT-016/017` · `TC-CNL-010` · `TC-DLV-043..047/050/062` · `TC-USR-025/042`):
> các step đó là **điều hướng NẰM TRONG luồng đang test** (vd `TC-DLV-043` step 3 *"Nhấn nút mở màn Xác nhận đã giao"* chính là
> hành vi được kiểm), không phải dựng tiền đề ⇒ gắn `(setup)` vào đó mới là sai.

#### Bookkeeping (2)

| # | TC/Đối tượng | Vấn đề | Fix |
|---|---|---|---|
| B-1 | `SC-DLV-060` | Đã DESCOPED (BA chốt role admin **out of scope v1.1**; chính ô `When` của SC ghi *"ngoài phạm vi test — Admin Portal out of scope `C-TS-01`"*) nhưng vẫn mang **`Lifecycle = NEW`** ⇒ nằm trong mẫu số và sẽ **kích hoạt lại `R2-01` mỗi lượt review**. | Đổi lifecycle sang `DEPRECATED` (hoặc cột trạng thái descope) ở `DLV/test_scenario_map.md`, trừ khỏi mẫu số |
| B-2 | `fragments/TC-ORD-v1.1.md` header | Còn ghi *"`SC-ORD-059` là MODIFIED"* — **hết hiệu lực** sau đính chính lifecycle 2026-09-17 (SC sinh ở v1.1, giữ `NEW`). TC-MASTER đã đúng (`TC-ORD-075/076` = `NEW`). | Sửa 1 câu trong header fragment |

### 🔵 INFO (3)

| # | Check | Nội dung |
|---|---|---|
| I-1 | R3-11 | `TC-NTF-008` có 1 step **212 ký tự** (ngưỡng 200) — cân nhắc tách |
| I-2 | R2-10 | Coverage **139/140 SC = 99.3%**; 1 SC hở là `SC-DLV-060` (descoped có chủ đích) |
| I-3 | R2-06 | `SC-DLV-060` blocked-by-scope, không phải gap chất lượng |

---

## Các check chạy SẠCH (0 finding) — ghi lại để lượt recheck không phải dò lại

| Nhóm | Kết quả |
|---|---|
| **R1-01** TC ID trùng | **0** (223 ID duy nhất) |
| **R1-02** ID nhảy số | **0 finding** — 9 module có gap, nhưng **cả 9 đều khai ở `§0.1` header fragment** (chiến lược (a) để lỗ / (b) renumber + `ID cũ:`), đúng `testcase-guide.md §A.2` |
| **R1-03** anchor integrity | **0** — không TC nào gộp dải `N-M.`, không neo step không tồn tại, không trỏ `TC-*`/`Setup-*` trong Steps/Expected. `Project_rule §10.4` (1 dòng Expected neo step cuối) áp đúng 223/223 |
| **R1-04..R1-13** | **0** — không ô trống ở SC ID/REQ ID/DOC Source/Steps/Expected; Priority 223/223 hợp lệ; Lifecycle 223/223 hợp lệ; Version Origin đủ |
| **R1-09** Test Data trống | 3 TC (`TC-ACT-001`, `TC-USR-013/014`) — **đều `Group = UI`**, luật ghi rõ *"acceptable cho UI TCs"* ⇒ không tính finding |
| **R1-14** Notes trống | **0/223** |
| **R2-01/02** | Chỉ `SC-DLV-060` (đã xử lý ở B-1/I-3) |
| **R2-03/R2-08** | **0** — mọi module đều có cả happy-path lẫn negative (bộ dò regex ban đầu báo `ACT`/`FEED`/`GIFT` thiếu positive — **kiểm tay là dương tính giả**) |
| **R2-12** | **0** — 2 SC DEPRECATED (`SC-HOME-010/024`) đã gỡ đúng, 2 ID bỏ trống vĩnh viễn |
| **R3-14** Luật vàng Pre-condition | **0** — 6 ứng viên đều là tham chiếu `SEED-*` hợp lệ theo `Project_rule §10.3` (vấn đề thật đã tách ra M-1) |
| **R3-15/R3-05** Title | **0** — 223/223 bắt đầu bằng `Check`, **0 dấu `→`**, 0 technique tag lọt Title |
| **R3-16** rationale lọt Expected | **0** — không mã `VR-`/`FR`/`AC-`/`BR`/`§x.y` nào trong Expected |
| **R3-17** Expected assert cứng | **0** — 4 ứng viên đều **dương tính giả**: `TC-TS-009/013` chứa chuỗi **UI verbatim** *"Đã ghi nhận phản hồi"*; `TC-ASN-026` là *hệ thống* ghi audit log; `TC-FEED-009` assert cứng ảnh bản đồ |
| **R3-20** Pre-condition dồn dòng | **0** — **222/223 TC** tách mỗi điều kiện 1 dòng |
| **R4-06** TC trùng | **0** |
| **R4-08** Module grouping | **0** — 223/223 prefix TC khớp prefix SC |
| **R4-09/R4-10** Lifecycle | **0** — không TC nào `CARRIED` (NEW 169 · MODIFIED 54). 20 cặp TC⟷SC lệch NEW/MODIFIED là **hợp lệ**: TC-lifecycle và SC-lifecycle là 2 đối tượng khác nhau (vd `TC-FEED-002` MODIFIED phủ `SC-FEED-002` NEW — SC giữ lifecycle NEW từ v1.0 theo thiết kế) |

## Version-Specific Checks

| Check | Result |
|-------|--------|
| CARRIED TCs included | **KHÔNG — có chủ đích.** QC chốt 2026-09-17 không gộp; 163 TC CARRIED ở `TC-MASTER-v1.0.xlsx`. Đã cảnh báo ở sheet `Overview` + `CLAUDE.md` |
| DEPRECATED TCs removed | ✅ `TC-HOME-010` + `TC-HOME-024` đã gỡ, ID bỏ trống vĩnh viễn |
| Version Origin filled | ✅ 223/223 (v1.1: 192 · v1.0: 31) |
| Lifecycle matches MASTER-MEMORY | ✅ sau đính chính `SC-ORD-059` 2026-09-17 (còn 1 câu stale ở header fragment — B-2) |
| Trùng ID với file v1.0 | ⚠️ **54 TC** trùng ID; **5 TC kỳ vọng NGƯỢC** (`TC-ACT-008/013/014`, `TC-USR-003/008`) — đã cảnh báo ở `Overview` + `CLAUDE.md`. **LUÔN lấy bản v1.1** |

## Score Breakdown

```
Score = 100 − (CRITICAL×5 + MAJOR×3 + MINOR×1)
      = 100 − (0×5 + 2×3 + 14×1)
      = 100 − 20 = 80
Direct mode cap: min(80, 85) = 80
```

**Quality Gate G1: PASS** (≥ 70) → downstream **KHÔNG bị block**.

## So sánh v1.0 → v1.1

| | v1.0 (2026-09-07) | v1.1 (2026-09-17) |
|---|---|---|
| Score | **0/100 — REJECTED** | **80/100 — CONDITIONAL** |
| Critical / Major / Minor | 0 / 36 / 36 (+17 Info) | **0 / 2 / 14** (+3 Info) |
| 3 pattern Major của v1.0 | `R3-14` 42 TC · `R3-02`+`R3-17` 12 TC · `R3-01/09/03` | **cả 3 đều 0 finding ở v1.1** |

3 pattern từng đánh chìm v1.0 đã được xử lý triệt để: `R3-14` nhờ `Project_rule §10.3` (seed dùng chung) +
nhãn `(setup)`; `R3-02`/`R3-17` nhờ `§10.4` (1 dòng Expected neo step cuối, assert cứng); `R3-01/09` nhờ
Steps nêu rõ element + giá trị.

## Recommendation

| Ưu tiên | Việc | Ai |
|---|---|---|
| 1 | **M-1** — carry 21 khối `SEED-*` vào TC-MASTER (`/generate-tc --consolidate`) + bổ sung luật vào `Project_rule §10.3`. ⚠️ **Nên làm TRƯỚC `/vibe-test`**, nếu không 88 TC sẽ kẹt giữa chừng | generate-tc |
| 2 | **M-2** — sửa `MASTER §3` dòng FEED (+`SC-FEED-002`) và mẫu số `139 → 140` ở `§1`/`§3`/`§4` | sửa tay |
| 3 | **B-1** — đổi lifecycle `SC-DLV-060`, trừ khỏi mẫu số | analyze-requirements |
| 4 | **R3-19 ×12** + **B-2** — thêm nhãn `(setup)`, sửa header fragment ORD | generate-tc |
| 5 | Chạy lại `/review-tc --recheck` sau khi fix; nếu có `ANTHROPIC_API_KEY` thì chạy **agent mode** để bỏ cap 85 | — |

---

## Fix applied — 2026-09-17 (cùng ngày review)

> Ghi ở đây để lượt `--recheck` biết cái gì đã đụng. ⛔ Score **chưa** tính lại — re-score phải qua `/review-tc --recheck`.

### ✅ M-1 — Seed dùng chung đã carry vào TC-MASTER

| Việc | Kết quả |
|---|---|
| Sheet **`Seed`** mới trong `TC-MASTER-v1.1.xlsx` (vị trí 2, ngay sau `Overview`) | **9 khối** phủ **21/21 mã `SEED-*`** |
| Ô `Pre-condition`/`Test Data` trỏ ra ngoài workbook | **34 ô ở 4 sheet** → đổi sang *"xem sheet `Seed` của chính file này"* |
| Kiểm chứng tự-đủ | mã `SEED-*` bị TC trỏ = **21** · có định nghĩa ở sheet `Seed` = **21** · **0 thiếu** · **0 ô** còn trỏ `"đầu fragment"` / `v1.0/CHANGELOG` |
| `TC-MASTER-LATEST.xlsx` | đã đồng bộ (14 sheet · 223 TC) |
| Dữ liệu TC | **không đụng** — vẫn 223 TC, chỉ thêm sheet + sửa câu trỏ đường |

🔴 **Phát hiện thêm trong lúc fix, nặng hơn bản báo cáo gốc:** `SEED-DLV-01` — mã bị **3 module** (`CNL` · `HOME` · `NTF`)
trỏ tới — **không định nghĩa ở fragment v1.1 nào cả**, mà nằm ở **file thứ ba**: `03_test-cases/v1.0/CHANGELOG.md §1`
(dòng REVISE 2026-09-15). Nay đã chép đủ nội dung vào sheet `Seed`, kèm cảnh báo *"trạng thái đơn một chiều"* và
ngoại lệ `TC-DLV-024` (không dùng seed này — cần real-time, phải nhờ dev/QA).

**Chặn tái phát:** `Project_rule.md §Custom Rules §10.3` thêm **mục 4** — consolidate **bắt buộc** sinh sheet `Seed`
đủ mọi mã được trỏ, và mọi ô chỉ được trỏ sheet `Seed` của chính file. Kèm phép kiểm nhanh:
*tập `SEED-*` bị TC trỏ phải bằng tập được định nghĩa ở sheet `Seed`*.

### ✅ M-2 — Mẫu số coverage 139 → 140

| Chỗ sửa | Trước | Sau |
|---|---|---|
| `§3` dòng `FEED`, cột MODIFIED | `007` · `009` · `013` | **`002`** · `007` · `009` · `013` |
| `§3` khối ⚠️ FEED | "4 SC của FEED bị chạm" | "**5** SC" |
| `§1` · `§3` · `§5` mẫu số | 139 | **140** |
| `§4` Phải test | `139 SC` = 90 NEW + 45 MOD + 4 SC FEED | **`140 SC`** = 90 NEW + 45 MOD + **5** SC FEED |
| `§4` Đối chiếu coverage | 138/139 | **139/140 (99,3%)** |
| `§4` FEED không cần test | `FEED (11/15)` | **`FEED (10/15)`**, thêm `SC-FEED-002` vào nhóm phải test lại |

Ghi kèm **3 nguồn độc lập** chứng minh `SC-FEED-002` thuộc nhóm bị chạm (scenario_map *"hết gap CTA 2026-09-16"* ·
fragment khai *"4 SC vừa đổi Then"* · TC-MASTER `Lifecycle = MODIFIED`), để lần sau không ai gỡ ra lại.

### Còn lại sau fix

| Severity | Count | Nội dung |
|---|---:|---|
| 🔴 CRITICAL | 0 | — |
| 🟠 MAJOR | **0** | *(M-1, M-2 đã đóng)* |
| 🟡 MINOR | 14 | R3-19 ×12 · B-1 `SC-DLV-060` lifecycle · B-2 header `TC-ORD-v1.1.md` |
| 🔵 INFO | 3 | — |

**Score dự kiến sau recheck:** `100 − (0×5 + 0×3 + 14×1) = 86` → **cap direct mode 85**.
⚠️ Muốn vượt 85 phải chạy **agent mode** (`ANTHROPIC_API_KEY`). Chạy `/review-tc --recheck` để chốt điểm chính thức.

### Chưa đụng (có chủ đích)

- **Fragment `.md`** giữ nguyên câu *"xem ghi chú Seed dùng chung đầu fragment"* — **đúng** trong ngữ cảnh fragment (§10.3 mục 1).
- ⚠️ Nhưng `TC-CNL-v1.1.md` vẫn trỏ `SEED-DLV-01` sang `03_test-cases/v1.0/CHANGELOG.md` mà **không định nghĩa tại chỗ** — fragment đó chưa tự đủ. Ngoài phạm vi M-1 (M-1 nói về TC-MASTER); ghi nợ cho lượt `/generate-tc` kế tiếp.

---

## Fix applied (đợt 2) — 14 MINOR · 2026-09-17

### ✅ #1 · R3-19 — 12 TC thêm nhãn `(setup)`

Sửa **cả 2 nơi** (`TC-MASTER-v1.1.xlsx` sheet `ALL` + sheet module, và fragment `.md`) — **+12 step** có nhãn (563 → 575).
`TC-CNL-006/015/016/017/018/019/020` (step 1) · `TC-HOME-008` (5) · `TC-HOME-029` (4) · `TC-HOME-031` (4) ·
`TC-ORD-048` (4) · `TC-GIFT-008` (2).

🔍 **Sửa lại kết luận của chính báo cáo gốc:** báo cáo ghi `TC-ORD-048` **step 3 + 4**; khi fix mới thấy **step 3 KHÔNG phải setup** —
Expected step 5 assert *"kết quả tìm ở step 3"*, tức step 3 sinh ra quan sát được dùng để phán quyết. Gắn `(setup)` vào đó
sẽ **nới sai luật chấm cho đúng phần cần chấm chặt** (đúng chiều ngược mà R3-19 cấm). ⇒ chỉ gắn **step 4**.

⚠️ **7 step vẫn cố ý KHÔNG gắn nhãn** (`TC-ACT-016/017` · `TC-CNL-010` · `TC-DLV-050/062` · `TC-USR-025/042`): là
**điều hướng NẰM TRONG luồng đang test**, không phải dựng tiền đề.

### ✅ #2 · B-1 — `SC-DLV-060` → `DEPRECATED`

`DLV/test_scenario_map.md`: Lifecycle `NEW → DEPRECATED` (kèm lý do descope role admin), `counts` `new 34→33` ·
`deprecated 0→1` · `p3 12→11`. Lan số qua **3 tầng**: router §2a/§2b (Tổng `89 NEW / 45 MOD / 3 DEPR`, P3 `82→81`) ·
MASTER §1 · §3 · §4 · §5.

**Hệ quả tốt:** SC rời mẫu số ⇒ mẫu số `140 → 139`, coverage **139/139 = 100%** (không còn "SC hở"), và `R2-01`
sẽ **không báo đỏ oan mỗi lượt review** nữa.

🔴 **Phát sinh và đã xử lý:** phép kiểm `carried + modified + deprecated == SC v1.0` (do chính lượt health-check sáng
nay đặt ra) **báo CRITICAL oan cho `DLV`** sau khi sửa — vì nó giả định **mọi SC DEPRECATED đều sinh ở version trước**.
`SC-DLV-060` sinh ở v1.1 rồi descope ngay trong v1.1. Đã sửa **định nghĩa phép kiểm** ở `MASTER §3`: tách rõ
**2 loại DEPRECATED** (① sinh version trước → vào vế trái · ② sinh chính version này → KHÔNG vào), kèm cách phân loại
bằng máy (đối chiếu `id_range` ở `<module>/CHANGELOG.md`). Chạy lại: **10/10 module khớp**.

### ✅ #3 · B-2 — header `TC-ORD-v1.1.md`

Bỏ câu *"trong đó `SC-ORD-059` là MODIFIED"*, thay bằng đính chính đầy đủ + trỏ chứng minh ở `MASTER §3`.

### ✅ (thêm) Nợ #23 — `TC-CNL-v1.1.md` tự đủ

Chép **định nghĩa đầy đủ `SEED-DLV-01`** vào ngay fragment (trước đó chỉ trỏ sang `03_test-cases/v1.0/CHANGELOG.md`),
kèm cảnh báo *"trạng thái đơn MỘT CHIỀU"* + ngoại lệ `TC-DLV-024`. Nợ này do chính lượt fix M-1 mở ra.

### Trạng thái sau đợt 2

| Severity | Lúc review | Sau fix |
|---|---:|---:|
| 🔴 CRITICAL | 0 | **0** |
| 🟠 MAJOR | 2 | **0** |
| 🟡 MINOR | 14 | **0** |
| 🔵 INFO | 3 | 3 *(không trừ điểm)* |

**Score dự kiến sau `/review-tc --recheck`: `100 − 0 = 100` → cap direct mode ⇒ **85**.**
Muốn vượt 85 bắt buộc chạy **agent mode** (`ANTHROPIC_API_KEY`) — cap là luật của `reviewer-agent.md §6`, không bỏ được.

**Dữ liệu TC không bị đụng:** vẫn **223 TC**, 0 trùng ID. Mọi thay đổi chỉ là nhãn `(setup)`, lifecycle 1 SC, và câu chỉ đường.

---

# Recheck — 2026-09-17

> Mode: **Direct** (vẫn chưa có `ANTHROPIC_API_KEY`) · TC-MASTER: `03_test-cases/v1.1/TC-MASTER-v1.1.xlsx` — 223 TC, 14 sheet
> **Previous score: 80 → New score: 85 (+5)** · Verdict `CONDITIONAL` → **`CONDITIONAL`** · **G1: PASS → PASS ✅**

## Trạng thái từng finding

| Finding | Previous | Now | Status |
|---|---|---|---|
| **M-1** `R1-03` Seed không có trong TC-MASTER | 88 TC trỏ 21 mã `SEED-*`, workbook 0 định nghĩa, 17 TC trỏ *"đầu fragment"* | sheet **`Seed`** 9 khối · **21 mã trỏ == 21 định nghĩa** · **0 ô** trỏ ra ngoài workbook | ✅ **Fixed** |
| **M-2** `R2/R4` `§3` thiếu `SC-FEED-002` | mẫu số ghi 139, `§3` liệt 3 SC FEED | `§3` liệt **4 SC FEED** (+`SC-FEED-002`) · mẫu số **139** *(sau B-1)* · coverage **139/139** | ✅ **Fixed** |
| **R3-19** ×12 TC thiếu nhãn `(setup)` | 12 TC / 13 step | step có nhãn **563 → 575 (+12)** · 0/12 TC đích còn sót | ✅ **Fixed** |
| **B-1** `SC-DLV-060` còn `Lifecycle NEW` | trong mẫu số, `R2-01` báo đỏ mỗi lượt | `DEPRECATED` + `counts` 33/1, lan đủ 3 tầng | ✅ **Fixed** |
| **B-2** header `TC-ORD-v1.1.md` stale | *"`SC-ORD-059` là MODIFIED"* | đã thay bằng đính chính + trỏ chứng minh | ✅ **Fixed** |
| **I-1** `R3-11` `TC-NTF-008` step 212 ký tự | Info | vẫn 212 ký tự, không gắn `(setup)` | 🔵 **Still Open** *(Info — không trừ điểm)* |
| **I-2** `R2-10` coverage | 139/140 = 99,3% | **139/139 = 100%** | ✅ **Superseded** |
| **I-3** `R2-06` `SC-DLV-060` blocked-by-scope | Info | hết hiệu lực — SC đã `DEPRECATED`, rời mẫu số | ✅ **Resolved** |

## Battery R1–R4 chạy lại đầy đủ (không chỉ verify finding cũ)

| Nhóm | Kết quả |
|---|---|
| R1-01 · R1-04..R1-13 | **0** — 223 ID duy nhất, 0 ô trống/invalid |
| **R1-03** anchor integrity | **0** — 0 dangling · 0 gộp dải `N-M.` · 0 tham chiếu `TC-*`/`Setup-*` |
| R1-02 ID gap | **0** — 9 module có gap, cả 9 khai ở `§0.1` |
| R2-01/02 coverage | **139/139 = 100%** · **0 SC hở** |
| R2-11 CARRIED | 0 TC `CARRIED` — đúng chủ đích (v1.1 không gộp regression) |
| R2-12 DEPRECATED còn TC | **0** — `SC-DLV-060` (SC DEPRECATED duy nhất của delta) có **0 TC**, đúng |
| **R3-01** step mơ hồ · **R3-09** element không rõ | **0 · 0** |
| R3-06 step nhiều action | 1 ứng viên `TC-GIFT-011` step 4 — **dương tính giả** (*"Chọn 1 loại quà và nhấn xác nhận gửi"* là 1 thao tác nguyên tử mở popup) |
| R3-15 Title · R3-16 rationale · R3-20 Pre-condition | **0 · 0 · 0** |
| R3-17 assert cứng | 1 ứng viên `TC-FEED-009` — **dương tính giả** như lượt FULL (assert cứng ảnh bản đồ; ngoặc đơn chỉ khoanh phạm vi số km) |
| R4-01 thuật ngữ | nhất quán — **217 TC** dùng `"Đăng nhập"`, **0** dùng `"Login"`. 1 hit `Carrier/token` ở `TC-ASN-024` nằm trong ngữ cảnh API ⇒ đúng `Project_rule §Ngôn ngữ` (*tech term để English*) |
| R4-06 · R4-08 · R4-09 · R4-10 | **0 · 0 · 0 · 0** |

## 🔵 New — phát hiện khi recheck (Info, không trừ điểm)

**N-1 · `R3-19` chiều ngược — 2 step gắn `(setup)` nhưng output được Expected tham chiếu.**
`TC-HOME-008` step 1 và `TC-HOME-031` step 1 (*"…mở Trang chủ và **ghi lại con số**…"*) mang nhãn `(setup)`,
trong khi Expected assert *"lớn hơn đúng 1 so với con số đã ghi ở **step 1**"*.

**Không raise thành Minor**, lý do nêu rõ để lần sau khỏi tranh luận lại: hai step này chỉ **ghi mốc so sánh**;
hành vi *đọc số ở khối hero* đã có TC riêng (`TC-HOME-029`), còn thứ đang được test là **mức tăng**. Đúng định nghĩa
`(setup)` ở `testcase-guide.md §B.3` (*"hành vi đã có TC riêng ở module/chức năng khác"*).

⚖️ **Đối chiếu để thấy luật được áp nhất quán, không phải áp cho tiện:** cùng lượt fix, `TC-ORD-048` **step 3**
(*"nhấn tab Bảng tin và tìm tiêu đề của tin đó"*) **bị từ chối gắn nhãn** — vì tìm tin trên Bảng tin **chính là**
hành vi mà SC đang kiểm (tin hết hạn phải biến mất khỏi Bảng tin), không phải tiền đề. Hai quyết định ngược nhau
nhưng cùng một tiêu chí: *output đó là hành vi đang test, hay chỉ là mốc để so?*

⚠️ **Chưa kiểm được:** sheet `Seed` mới thêm có làm `export-tc-rp` (renderer template FPT) hiểu nhầm cấu trúc workbook
không — skill đó chưa chạy lần nào cho v1.1. Nếu render lỗi, nghi can đầu tiên là sheet này.

## Score Breakdown

```
Score = 100 − (CRITICAL×5 + MAJOR×3 + MINOR×1)
      = 100 − (0×5 + 0×3 + 0×1) = 100
Direct mode cap: min(100, 85) = 85
```

| | Previous | Now |
|---|---:|---:|
| 🔴 CRITICAL | 0 | **0** |
| 🟠 MAJOR | 2 | **0** |
| 🟡 MINOR | 14 | **0** |
| 🔵 INFO | 3 | 3 |
| **Score** | **80** | **85** |

**Quality Gate G1: PASS** (≥ 70) → downstream **KHÔNG bị block**.

> 🔴 **Vì sao 85 chứ không phải 100, và vì sao KHÔNG phải `APPROVED`.**
> Điểm thô đã là **100/100 — 0 finding trừ điểm**. Nhưng `reviewer-agent.md §6` cap **mọi** lượt direct ở **85**,
> và 85 rơi vào dải **70–89 ⇒ `CONDITIONAL`**. ⇒ **Ở direct mode, `APPROVED` (90+) là KHÔNG THỂ ĐẠT về mặt cấu trúc**,
> bất kể TC tốt tới đâu. Cap này tồn tại vì TC do AI sinh trong cùng session, self-review không tự chứng nhận được.
> **Muốn `APPROVED` thì bắt buộc có `ANTHROPIC_API_KEY`** để chạy agent mode — ⛔ không có đường nào khác,
> và fix thêm TC cũng không nâng được điểm.
