# Vibe Test Report — VR-002 — v1.1 (+ CARRIED v1.0) — 2026-09-18

> Platform: **mobile** (Appium MCP / UiAutomator2) · emulator-5554
> Environment: **STG** — host app `com.hrisproject.stag` (FoxPro) → icon **FoxEco** · tài khoản **A** (`Đặng Châu Giang`, MNV 00131946)
> Module: **ORD — Đăng tin & Quản lý tin** · SCOPE_TOTAL = **88 TC** = 48 (v1.1) + 40 (CARRIED v1.0)

## Summary

Phiên đầu tiên chạy module ORD. Đã chạy **3 lô / 43 TC**, thu **42 verdict cuối** (**27 PASS · 14 FAIL · 1 BLOCKED** sau recheck + sửa Expected `TC-ORD-070` ngày 2026-09-18; trước recheck: 25/14/3),
1 TC chạy dở (`TC-ORD-001`). **Còn nợ 46/88 TC** ⇒ §8 = **PARTIAL**.
14 FAIL **không phải 14 bug**: **4** là TC v1.0 hết hiệu lực (nợ QC), 10 còn lại quy về **5 ứng viên bug** (`B1`·`B2`·`B4`·`B5`·`B6`) — **`B3` đã bị bác bỏ**, khối ảnh **không còn bug nào**.
Nặng nhất: **chặn im lặng** (5 nhánh validate không báo lỗi, gồm 1 TC **P1**) và **không có popup thoát wizard** (mất dữ liệu soạn dở).

## Scope Coverage ★★

> Mẫu số LUÔN là SCOPE_TOTAL của module (88), không phải số TC đã chạy phiên này.

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module ORD)** | **88** | 100% |
| Chạy **trong run này** (có verdict cuối) | 42 | 48% |
| ✅ PASS từ **run trước** | 0 | 0% |
| ⛔ N-A (cố ý không test qua UI) | 0 | 0% |
| ⏳ **NOT_RUN (còn nợ)** | **46** | **52%** |
| ⚠️ NOT_EVIDENCED (còn nợ) | 0 | 0% |

**Còn nợ = 46 TC → §8 = PARTIAL.**

- Chi tiết từng TC **của module (xuyên run)**: `08_test-runs/vibe/coverage/coverage-ORD.md` ← **xem cái này**
- Chi tiết **run này làm gì**: `scope-ledger.md` trong run folder

## Kết quả các TC chạy trong run này

| Result | Count | % trên 42 |
|--------|-------|---|
| ✅ PASS | 27 | 64% |
| ❌ FAIL | 14 | 33% |
| 🚫 BLOCKED | 1 | 2% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

Theo lô: **lô 1** 12 TC (màn Đăng tin mới + Bước 1 phần chip/banner) · **lô 2** 16 TC (khối ảnh + thoát wizard + email người nhận + địa chỉ trùng) · **lô 3** 15 TC (2 nhánh thiếu tier + ghi chú 300 + ngày/buổi + prefill người gửi).

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | **43/43 (100%)** |
| File ảnh trong `screenshots/` | 55 (1 `_setup` + 1 `_recon` + 53 ảnh TC — **+3 ảnh recheck** khối ảnh 2026-09-18 chiều) |
| TC thiếu evidence (⚠️ NOT_EVIDENCED) | **không có** |
| Gate `.claude/hooks/verify_evidence.py` | **0 vi phạm fabrication** (missing/batched/dangling/misattr/no_citation/orphan/uncited/badname đều rỗng) · chỉ báo *"RUN CHƯA HOÀN TẤT"* vì 46 TC còn nợ ⇒ đúng ca **PARTIAL** |

→ QC lead verify lại từng case bằng `screenshots/TC-ORD-<NNN>__verify*.png` / `__step<N>-FAIL*.png` (1 file riêng/TC).

> 🗂️ **Giữ ảnh `__pre` của 4 TC PASS** (`012` · `062` · `068` · `087`) — lệch luật retention *"ảnh phụ chỉ giữ khi FAIL/BLOCKED"*, **có chủ ý**:
> ảnh `__pre` là chỗ **duy nhất** chứng minh **ảnh/file NÀO trong `SEED-ORD-01` đã được chọn** ở Android Photo Picker
> (mọi thumbnail có `content-desc` giống nhau, chọn theo `.instance(N)`) — thông tin này **không suy lại được** từ ảnh `__verify`.
> ⇒ giữ để retest `TC-ORD-068` (biên 5MB) dùng đúng file cũ. *(Vế `070`/`071` không còn: B3 đã bị bác bỏ, 2 TC đã có verdict — xem khối ♻️ Recheck.)*
>
> ♻️ Trước khi commit: nén ảnh (~0.1–0.15 MB/ảnh sau nén) — ⛔ **không xoá** ảnh đang được trích trong `vibe-log.md` (sẽ tạo link chết ở gate).

## Locator Coverage

| Screens visited | Elements captured | Verified ✅ | Inferred ⚠️ | Not found 🚫 |
|---|---|---|---|---|
| 5 | 62 | 47 | 10 | 5 |

→ `implement-automation` đọc `08_test-runs/vibe/locators/vibe-locators-latest.md` (đã merge 62/62 = 100%).
→ **5 bẫy kỹ thuật MỚI T6–T10** + **5 đính chính** với locator của VR-001 — đọc trước khi code.

## 🐞 Ứng viên bug — gộp theo NGUYÊN NHÂN (⛔ đừng mở 10 bug cho 10 TC)

| # | Ứng viên bug | TC dẫn chứng | Sev đề xuất | Căn cứ oracle |
|---|---|---|---|---|
| **B1** | **Chặn im lặng**: nút `Tiếp theo` bị khoá nhưng KHÔNG báo lỗi ở trường thiếu/sai — 5 nhánh | `TC-ORD-063` **(P1)** · `064` · `066` · `083` · `084` · `077` | **High** | `BR01-01`/`BR01-02` + Expected của từng TC. Đối chứng: app **có** báo lỗi ở 3 nhánh khác (`068`/`058`/`057`) ⇒ là **bỏ sót**, không phải thiếu framework |
| **B2** | **Không có popup "Thoát và bỏ nội dung đã nhập?"** ⇒ back ở bước 1 xoá sạch dữ liệu soạn dở, không cảnh báo | `TC-ORD-053` | **High** | `AC-01.2.01` + `C-ORD-08`. ⚠️ Cùng họ `TC-USR-045` (VR-001) ⇒ đề nghị log ở phạm vi **hệ thống** |
| ~~**B3**~~ | 🚫 **ĐÃ BÁC BỎ — không có bug nào ở khối ảnh.** *"Trần ảnh 4/5"* không có thật (dương tính giả do lazy list). Ứng viên thay thế **B3′** (*mất bộ đếm ở 5/5*) cũng **đã huỷ 2026-09-18**: QC chốt hành vi hiện tại là ĐÚNG ⇒ **sửa Expected `TC-ORD-070`** thay vì log bug | `TC-ORD-070` ✅ PASS · `TC-ORD-071` ✅ PASS | — | `BR18-02` *"ẩn nút thêm khi đủ 5"* — bộ đếm nằm trong ô thêm ảnh nên ẩn theo, **không thể** đồng thời hiện `5/5` |
| **B4** | **Autofill người nhận thiếu ô "Địa chỉ giao hàng"** (chỉ điền tên + SĐT) | `TC-ORD-074` **(P1)** | **Medium** | ⚠️ **Hỏi BA TRƯỚC KHI LOG**: HRIS có địa chỉ ⇒ bug app; spec chỉ autofill 2 ô ⇒ sửa Expected |
| **B5** | **Buổi mong muốn không có giá trị mặc định** (PRD chốt `Sau giờ làm (17–19)`) | `TC-ORD-058` | **Low** | PRD v1.1 `§8.1.4` |
| **B6** | **Cho chọn buổi đã trôi qua trong ngày** (13:44 vẫn chọn được `Sáng 8–12h`) | `TC-ORD-059` | **Medium** | `C-ORD-15(b)` — ⚠️ rule **không có trong PRD**, log bug **phải dẫn CL này** |

### ♻️ Recheck 2026-09-18 (chiều) — huỷ B3, sinh B3′

QC báo test tay **không thấy lỗi trần ảnh** ⇒ chạy lại khối ảnh trên `emulator-5554` (tài khoản MNV `00002352`).
Kết quả: **B3 là dương tính giả do công cụ**, không phải lỗi app.

| Lượt 1 kết luận | Recheck |
|---|---|
| app chỉ tải được **4** ảnh | ❌ sai — nhận **đủ 5 ảnh** |
| `multi-photo-add-button` "biến mất khỏi cây" | ❌ sai ở mức 4 ảnh — tile thêm ảnh ở **cuối dải cuộn ngang**, ngoài viewport ⇒ **lazy list không compose** ⇒ không có trong a11y tree |
| dải ảnh **không cuộn** (3 kiểu swipe đều trượt) | ❌ sai — `input swipe 950→150 @y=1836, 500ms` cuộn tới cuối ngay lần đầu |
| ảnh thứ 4 **không xoá được** | ❌ sai — cuộn tới nơi thì ảnh thứ 4 **và** thứ 5 đều có `×` và xoá được |

**Đổi verdict:** `TC-ORD-071` 🚫 BLOCKED → ✅ **PASS** · `TC-ORD-070` 🚫 BLOCKED → ❌ FAIL → ✅ **PASS**.
> `TC-ORD-070` FAIL tiếp một nhịp vì Expected cũ đòi **đồng thời** `bộ đếm 5/5` **và** `nút thêm ẩn` — hai vế loại trừ nhau (bộ đếm nằm **trong** ô thêm ảnh, xem bẫy `T7`). **QC GiangDC2 chốt 2026-09-18: hành vi hiện tại ĐÚNG — đủ 5 ảnh thì bỏ bộ đếm luôn** ⇒ sửa Expected (bỏ vế `5/5`, assert bộ đếm ở `4/5`) ở `TC-MASTER-v1.1.xlsx` + fragment + `TC-MASTER-LATEST.xlsx`, ⛔ không log bug.
**Kết quả run sau recheck: 27 PASS · 14 FAIL · 1 BLOCKED** (42 verdict, scope/nợ **không đổi**).
📌 **Bài học cho `implement-automation`:** dải ảnh là **lazy horizontal list** — ⛔ không được suy *"không tìm thấy node"* = *"chức năng không có"*; phải cuộn rồi mới assert.

## 🔴 Nợ QC (KHÔNG phải bug) — 4 TC CARRIED v1.0 hết hiệu lực

| TC | Vì sao hết hiệu lực | Đề xuất |
|---|---|---|
| `TC-ORD-006` | `C-ORD-09` chốt app **CÓ** nhãn "Tài liệu"; TC assert phải KHÔNG có | `DESCOPED` + `Skipped` |
| `TC-ORD-007` (step 5) · `TC-ORD-008` (step 6) | v1.1 thêm **3 trường bắt buộc** (TRỌNG LƯỢNG · KÍCH THƯỚC · ẢNH HÀNG) ⇒ điều kiện enable `Tiếp theo` đã đổi | cập nhật `Steps`/`Expected` **hoặc** `DESCOPED` phần navigation |
| `TC-ORD-014` | Mâu thuẫn **trực tiếp** với `TC-ORD-063` (v1.1 P1: thiếu ảnh **phải** chặn) | `DESCOPED` + `Skipped` |
| *(kèm)* `TC-ORD-017` | PASS, nhưng câu chữ *"địa chỉ nơi làm việc"* sai nguồn prefill (thực tế là **địa chỉ mặc định hồ sơ**, `C-ORD-10`) | sửa câu chữ `Steps`/`Expected` |

⛔ **Tuyệt đối không sửa Expected theo app để làm xanh** 6 TC của B1 — chúng là bằng chứng của bug.

## Blocked TCs — ⚠️ KHÔNG automate

| TC ID | Blocked at | Reason | Impact |
|-------|-----------|--------|--------|
| `TC-ORD-069` | step 2 | App chỉ có 2 lối vào ảnh (camera / Android Photo Picker) — picker **lọc sẵn chỉ ảnh**, `.pdf` có thật trong `/sdcard/Pictures` vẫn không hiện ⇒ **không có đường UI** để thử file sai định dạng | 📨 QC chốt: `⛔ N-A (không test được qua UI)` **hoặc** đổi Expected sang *"picker không cho chọn file không phải ảnh"*. Cần BA/dev xác nhận tầng lọc định dạng nằm ở app hay chỉ dựa OS |

## Failed TCs — cần fix app hoặc sửa TC

| TC ID | Failed at | Expected | Actual | Thuộc về |
|-------|----------|----------|--------|---------|
| `TC-ORD-063` **P1** | step 6 | chặn + **lỗi ở khối ẢNH HÀNG** | chặn ✓, **không có lỗi** | 🐞 B1 |
| `TC-ORD-064` | step 6 | chặn + lỗi + 3 nhãn chip | chặn ✓ nhãn ✓, **không có lỗi** | 🐞 B1 |
| `TC-ORD-066` | step 5 | chặn + lỗi + 3 nhãn chip | chặn ✓ nhãn ✓, **không có lỗi** | 🐞 B1 |
| `TC-ORD-083` | step 5 | chặn + lỗi ở ô địa chỉ giao | chặn ✓, **không có lỗi** | 🐞 B1 |
| `TC-ORD-084` | step 5 | chặn + lỗi (biên khoảng trắng) | chặn ✓ (có trim), **không có lỗi** | 🐞 B1 |
| `TC-ORD-077` | step 4 | lỗi định dạng email + 3 ô trống | 3 ô trống ✓, **không có lỗi định dạng** | 🐞 B1 |
| `TC-ORD-053` | step 4 | popup *"Thoát và bỏ nội dung đã nhập?"* | **không có popup**, thoát thẳng + mất dữ liệu | 🐞 B2 |
| `TC-ORD-074` **P1** | step 5 | **3 ô** tên/SĐT/địa chỉ giao tự điền | chỉ **2/3** (địa chỉ giao rỗng) | 🐞 B4 (chờ BA) |
| `TC-ORD-058` | step 2 | mặc định `Sau giờ làm (17–19)` | **không có mặc định nào** | 🐞 B5 |
| `TC-ORD-059` | step 4 | buổi đã qua **không chọn được** | **chọn được** | 🐞 B6 |
| `TC-ORD-006` | step 3 | KHÔNG có chip "Tài liệu" | **có** (và là mặc định) | 🔴 nợ QC |
| `TC-ORD-007` | step 5 | sang bước 2 | ở lại bước 1 | 🔴 nợ QC |
| `TC-ORD-008` | step 6 | `Tiếp theo` enable | vẫn disable | 🔴 nợ QC |
| `TC-ORD-014` | step 4 | không ảnh vẫn sang bước 2 | bị chặn *(đúng v1.1)* | 🔴 nợ QC |

## Passed TCs — sẵn sàng implement automation (27)

`TC-ORD-002` · `005` · `009` · `010` · `011` · `012` · `013` · `015` · `016` · `017` · `018` · `027` · `028` · `030` · `031` · `054` · `055` · `056` · `057` · `062` · `068` · `070` *(recheck)* · `071` *(recheck)* · `075` · `076` · `078` · `087`
→ evidence từng TC: `screenshots/TC-ORD-<NNN>__verify-*.png` · locator: `vibe-locators.md`

## 🧪 Dữ liệu test dựng trong phiên (`SEED-ORD-01`)

Đẩy vào `/sdcard/Pictures/` của emulator-5554 (**không commit vào repo**, tái tạo được bằng PIL):
6 ảnh JPG nhỏ (`seed_jpg_1..6`, ~27KB) · 1 PNG nhỏ · 1 ảnh **đúng 5.242.880 B (=5MB)** · 1 ảnh **6.291.456 B (>5MB)** · 1 file `.pdf`.
- ✅ Dùng rồi: JPG nhỏ (`012`/`064`/`066`/`087`/`070`) · ảnh 6MB (`068`)
- ⏳ **Chưa dùng**: ảnh **đúng 5MB** (biên dưới hợp lệ — dành cho lượt sau) · PNG nhỏ
- ⛔ Không dùng được qua UI: `.pdf` (`TC-ORD-069` BLOCKED)

## 🗂️ Dữ liệu phát sinh trên STG

**Không có.** Phiên này **không đăng tin nào** (chưa tới bước 3) ⇒ ⛔ không thêm đơn rác trên STG.
Tài khoản A giữ nguyên hồ sơ (`363 Nguyễn Hữu Thọ, Cẩm Lệ`, SĐT `0912345670`) — ⛔ không sửa gì ở màn Cá nhân.
3 đơn cũ của VR-001 vẫn còn (2 NEED `Chờ ghép` + 1 OFFER `Đã huỷ`) — dùng được làm `SEED-ORD-04`/`05` ở lượt sau.

## 📨 Phản hồi ngược về analyze-requirements (spec-gap, KHÔNG chỉ ghi MEMORY)

| # | Bề mặt / mâu thuẫn chưa có trong `scenario_map` | Lệnh đề xuất |
|---|---|---|
| 1 | Host app FoxPro **đổi tab** sang THÔNG BÁO sau khi FoxEco đóng photo picker (tái hiện 1 lần, nhánh ảnh > 5MB) | `/analyze-requirements --update "host app đổi tab sau khi đóng photo picker của FoxEco"` |
| 2 | Chuỗi *"Không tìm thấy email này — **vui lòng nhập tay** thông tin bên dưới"* còn câu chữ `BR01-09` v1.0 mà `C-ORD-14` đã đảo | `/analyze-requirements --module ORD` *(+ raise clarification text-defect)* |
| 3 | `TC-ORD-074`: "địa chỉ giao hàng" có nằm trong nhóm autofill từ HRIS hay không — **quyết định B4 là bug app hay TC sai** | `/analyze-requirements --module ORD` *(hỏi BA `AC-04.x`)* |
| 4 | App **không phân biệt** *email ngoài tên miền công ty* với *email không có trên HRIS* (cùng 1 thông báo) | `/analyze-requirements --update "một thông báo dùng chung cho 2 nhánh email invalid"` |
| 5 | `TC-ORD-069`: tầng lọc **định dạng file** thuộc app hay chỉ dựa OS picker (quyết định TC này N-A hay đổi Expected) | `/analyze-requirements --module ORD` |

## Recommendation

- **Automate now:** 25 TC — locator ready trong `locators/vibe-locators-latest.md` (⚠️ đọc T6–T10 trước)
- **Log bug (gộp):** **B1** ✅ `BUG-009` · **B2** ✅ `BUG-010` · **B6** ✅ `BUG-011` · **B5** ✅ `BUG-012` (2026-09-18, **cả 4 chưa push Jira**) · **B4 chờ BA** · ~~**B3**~~ **+** ~~**B3′**~~ **đã bác bỏ cả hai** — khối ảnh ORD ⛔ không log bug nào
- **Fix TC first (QC chốt):** 4 TC hết hiệu lực + 1 TC sai câu chữ → `Project_rule §10.5` (`DESCOPED`, ⛔ giữ nguyên dòng)
- **Wait for app:** `TC-ORD-069` (chờ BA chốt N-A) — ~~`070`/`071`~~ đã có verdict sau recheck
- **Re-run cho evidence:** không có TC nào
- **CHẠY TIẾP phần còn nợ:** **46 TC** — `/vibe-test --module ORD` (bộ lọc pending tự bốc đúng 46 TC này)

**Ưu tiên lô 4 (đề xuất):** bước 3 wizard + đăng tin thành công (`034`–`041`, `065`, `067`, `039`, `049`, `050`, `051`, `052`) — vừa đóng được luồng chính vừa **tự sinh `SEED-ORD-04`** (tin POSTED có 2–5 ảnh) cho nhóm `046`/`060`/`072`/`073`/`088`.
