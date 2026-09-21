# Vibe Test Report — VR-011 — module GIFT — 2026-09-19

> Platform: **mobile (Appium MCP / UiAutomator2)** · Device `emulator-5554` (720×1280)
> Environment: **STG** — SDK **FoxEco** nhúng trong host app **FoxPro** (`com.hrisproject.stag`)
> Tài khoản dùng trong phiên: `stag_taipm@` (chính) → `stag_giangdc2@` → `stag_anhptm17@`
> SCOPE_TOTAL: **14 TC** = hợp 2 file TC-MASTER (v1.1 `Quà cảm ơn` **8 TC** ∪ v1.0 **6 TC** chỉ có ở v1.0)

## Summary

## Scope Coverage ★★

> Mẫu số LUÔN là SCOPE_TOTAL của module GIFT, ⛔ không phải số TC chạy trong phiên.

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module GIFT)** | **14** | 100% |
| Chạy **trong run này** | 12 | 86% |
| ✅ PASS từ **run trước** | 0 | 0% | 
| ⛔ N-A (cố ý không test qua UI) | 0 | 0% |
| ⏳ **NOT_RUN (còn nợ)** | **2** | **14%** |
| ⚠️ **NOT_EVIDENCED (còn nợ)** | **1** | **7%** |

**Còn nợ = 3 TC → §8 = PARTIAL.**

- Chi tiết từng TC **của module (xuyên run)**: `08_test-runs/vibe/coverage/coverage-GIFT.md` ← **xem cái này**
- Chi tiết **run này làm gì**: `scope-ledger.md` trong run folder

> GIFT **chưa từng được vibe-test** trước phiên này ⇒ bảng trên đồng thời là trạng thái đầu tiên của module.
> 🔴 **SCOPE_TOTAL = 14 là HỢP của 2 file** — v1.1 không gộp TC CARRIED (`CLAUDE.md §TC-MASTER`). Lấy chỉ v1.1 sẽ **sót 6 TC**.

## Kết quả các TC chạy trong run này

| Result | Count | % trên 12 |
|--------|-------|---|
| ✅ PASS | **8** | 67% |
| ❌ FAIL | **1** | 8% |
| 🚫 BLOCKED | 2 | 17% |
| ⚠️ **NOT_EVIDENCED** | **1** | 8% |

> 🔁 **ĐÍNH CHÍNH 2026-09-21 — `TC-GIFT-012` ❌ FAIL → ✅ PASS (QC chốt).** `TC-GIFT-012` đổi **❌ FAIL → ✅ PASS** theo quyết định của QC GiangDC2: nhấn thông báo `NTF-07` mở thẳng màn **"Quà đã nhận"** là **ĐÚNG hành vi**, ⛔ không phải bug. Expected step 4 của TC đã sửa cho khớp (fragment `TC-GIFT-v1.0.md` + `TC-MASTER-v1.0.xlsx` 2 sheet `Quà cảm ơn`/`ALL`, số dòng TC không đổi) và **draft `BUG-022` đã xoá**. Evidence: ảnh `TC-GIFT-012__verify-thong-bao-qua-cam-on.png` (slot `verify`, chứng minh thông báo) + `TC-GIFT-012__step4-FAIL-mo-qua-da-nhan-khong-phai-trang-ca-nhan.png` (màn đích; ⛔ **giữ nguyên tên** file vì chụp lúc đang chấm FAIL — nội dung ảnh chính là màn "Quà đã nhận" mà Expected mới yêu cầu). ⚠️ Chưa chụp lại ảnh màn đích ở slot `verify` — cần đăng nhập lại `stag_giangdc2@` trên thiết bị (đang dùng cho phiên VR-013); làm được bằng thông báo thứ 2 ("17 phút trước") nếu QC muốn ảnh đúng slot. ⚠️ Thiếu emoji 🎁 ở thông báo vẫn là quan sát trang trí, không hạ verdict.

> 🔁 **ĐÍNH CHÍNH TRONG PHIÊN — `TC-GIFT-001` và `TC-GIFT-010` đã đổi ❌ FAIL → ✅ PASS.**
> Lúc chạy, 2 TC bị chấm FAIL vì luồng app khác chữ trong TC. Đối chiếu **tài liệu phân tích của chính dự án** cho thấy chấm vậy **sai quy kết** — app khớp **Then của scenario** và khớp **câu trả lời BA đã `Resolved`**:
>
> | TC | Căn cứ |
> |---|---|
> | `TC-GIFT-001` | `SC-GIFT-001` **Then** = *"Mở màn "Tặng quà" với 4 lựa chọn quà"* → app **đạt**. `C-GIFT-04` **Resolved 2026-09-17** chốt app route **theo trạng thái tặng quà** (chưa tặng → "Tặng quà" · đã tặng → "Theo dõi đơn") |
> | `TC-GIFT-010` | `SC-GIFT-010` **Then** = *"Về đúng màn trước đó **(Theo dõi đơn / Đơn của tôi)**"* → app về `Đơn của tôi`, **nằm trong tập chấp nhận**. `C-GIFT-02` **Resolved 2026-09-16**: rule = *"back về màn hình trước đó"* |
>
> ⇒ Phần lệch còn lại của 2 TC là **chữ trong TC đã lỗi thời** ⇒ **sửa TC**, ⛔ **không log bug**.
> ⚠️ Ảnh evidence **giữ nguyên tên** (`…__step3-FAIL-*`, `…__step4-FAIL-*`) vì chụp lúc đang chấm FAIL — **đổi tên ảnh sau khi chụp là thao tác bị cấm**; nội dung ảnh vẫn đúng.

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | **11/12** — `TC-GIFT-010` có ảnh nhưng **sai slot** (xem dưới) |
| File ảnh trong `screenshots/` | **25** (20 ảnh TC + 4 `_recon__` + 1 `_setup__`) · ⛔ 0 file trùng md5 |
| TC thiếu evidence (⚠️ NOT_EVIDENCED) | `TC-GIFT-010` |
| Gate `verify_evidence.py` | *(xem §Gate cuối report)* |

→ QC lead verify lại từng case bằng `screenshots/TC-GIFT-<NNN>__verify*.png` (file riêng cho từng TC).

## Locator Coverage

| Screens visited | Elements captured | Verified ✅ | Inferred ⚠️ | Not found 🚫 |
|--------------|------------------|------------|---|-------------|
| 8 | **43** | **38** | 1 | 4 |

→ `implement-automation` bắt đầu được ngay với **38 locator đã MCP-verify**, đọc từ
`08_test-runs/vibe/locators/vibe-locators-latest.md` (§MERGE VR-011, hấp thụ 43/43 = 100%).
→ **3/4 mã 🚫 là thử có chủ ý** để chứng minh element **vắng mặt** (assert-absent), không phải locator hỏng.
→ ⚠️ 1 ⚠️ Inferred: **icon chuông** ở header Trang chủ — phiên này tap bằng **toạ độ** `(651,128)`; cần harvest locator thật trước khi automate `TC-GIFT-012`.

## Blocked TCs — ⚠️ KHÔNG automate

| TC ID | Blocked at | Reason | Impact |
|-------|-----------|--------|--------|
| `TC-GIFT-013` | Step 1 | **STG chưa build `FR09`** (luồng hoàn hàng) — không có đơn `RETURNED` nào; thanh trạng thái đơn chỉ **5 bước**, không có nhánh `RETURNING`/`RESCHEDULED`/`RETURNED` | Chờ dev build `FR09`; chạy lại cùng lô `TC-DLV-053..056` |
| `TC-GIFT-014` | Step 3 | Cùng blocker `FR09` — không đẩy được đơn sang `RETURNED` để so chỉ số | Đã ghi sẵn mốc **N = 2** ở step 2 cho lượt sau |

## Failed TCs — Cần fix app hoặc chốt lại spec

| TC ID | Failed at | Expected | Actual |
|-------|----------|----------|--------|
| `TC-GIFT-003` | Step 5 | Popup hiện đúng chuỗi **"Cảm ơn của bạn đã được gửi"** (`BR14-02`) | Tiêu đề **"Đã gửi lời cảm ơn!"** — chuỗi **v1.0 mà v1.1 đã chủ ý thay** |

### 🔗 FAIL còn lại (`TC-GIFT-003`) — đã log **[FE-308](https://foxproject.atlassian.net/browse/FE-308)** (2026-09-21, QC duyệt)

| Gốc | Kéo theo | Bản chất | Cần ai quyết |
|---|---|---|---|
| ~~G2 — Deep-link thông báo `NTF-07` sai đích~~ | ~~`TC-GIFT-012`~~ | **ĐÃ ĐÓNG 2026-09-21 — QC chốt app đúng, không phải bug** (xem khối đính chính đầu mục kết quả) | — |
| **G3 — Copy popup chưa cập nhật theo `BR14-02`** | `TC-GIFT-003` | Lỗi nội dung hiển thị mức thấp — app còn chuỗi v1.0 `"Đã gửi lời cảm ơn!"`. ⚠ Chuỗi `"cảm ơn của bạn đã được gửi"` **có** xuất hiện (nhúng trong câu thân popup) | **BA**: đọc chặt (FAIL, sửa copy) hay đọc lỏng (PASS, sửa Expected)? |

### 🔴 1 SPEC-GAP tách riêng — ⛔ KHÔNG gắn với TC nào FAIL

Nút **`"✓ Cảm ơn người vận chuyển"`** mà `KB-GIFT-01` (`KP-01 §5.1`, ô 5·Sender) **và `SC-GIFT-001` When** đều mô tả **KHÔNG tồn tại ở bất kỳ đâu trên app** — `textContains("Cảm ơn người vận chuyển")` chỉ khớp **TextView phụ đề** của màn "Tặng quà" (`get_text` xác nhận). Thực tế app **route theo trạng thái tặng quà của đơn**, đúng như `C-GIFT-04` BA đã chốt.
⇒ **Nợ tài liệu**, không phải nợ kiểm thử: `/analyze-requirements --update` để sửa ma trận nhãn nút `KB-GIFT-01` + When của `SC-GIFT-001`.

## Passed TCs — Sẵn sàng implement automation

| TC ID | Steps | Locators captured | Evidence file |
|-------|-------|------------------|---------------|
| `TC-GIFT-001` | 4 | 3 | `screenshots/TC-GIFT-001__verify-man-tang-qua-mo-tu-card.png` |
| `TC-GIFT-002` | 4 | 5 | `screenshots/TC-GIFT-002__verify-4-loai-qua-dung-ten.png` |
| `TC-GIFT-004` | 3 | 0 *(assert-absent)* | `screenshots/TC-GIFT-004__verify-khong-co-thanh-toan.png` |
| `TC-GIFT-005` | 6 | 4 | `screenshots/TC-GIFT-005__verify-nhan-nut-sau-khi-tang-qua.png` |
| `TC-GIFT-006` | 2 | 3 | `screenshots/TC-GIFT-006__verify-card-dem-2-loai-tong-5.png` |
| `TC-GIFT-007` | 2 | 2 | `screenshots/TC-GIFT-007__verify-co-danh-sach-lich-su-nhan-qua.png` |
| `TC-GIFT-009` | 3 | 2 | `screenshots/TC-GIFT-009__verify-ve-man-ca-nhan.png` |

## ⚠️ NOT_EVIDENCED — `TC-GIFT-010`

| TC ID | Đã chạy tới | Lý do thiếu evidence | Chạy lại |
|-------|-------------|----------------------|----------|
| `TC-GIFT-010` | Step 5 (đủ) | **Nội dung ĐẠT** — app về `Đơn của tôi`, **nằm trong Then của `SC-GIFT-010`** (*"Theo dõi đơn **/ Đơn của tôi**"*), và `KB-GIFT-04` **không tái hiện**. Nhưng ảnh chụp lúc đang chấm FAIL nên mang slot `__step4-FAIL`; sau khi verdict được đính chính thì TC **không còn file `__verify*`**. ⛔ **Không đổi tên ảnh** (luật cấm) và ⛔ **không chụp lại được** — STG đã **hết sạch** đơn Hoàn thành chưa tặng quà *(kiểm cả 4 tài khoản vào được FoxEco)* | `/vibe-test --tc TC-GIFT-010` sau khi có 1 đơn đủ điều kiện |

> ⚖️ **Vì sao không "lách" cho xanh:** đổi tên hoặc copy ảnh cho khớp gate là **làm giả evidence** theo luật `vibe-test`. Kết luận nội dung của TC (app đúng · đề nghị hạ `RISK-GIFT-05`) **vẫn dùng được** cho `/analyze-requirements`; chỉ **không được tính là PASS** cho tới khi có ảnh đúng slot.

## NOT_RUN TCs — ⏳ còn nợ, cả hai là **nợ SEED**

| TC ID | P | Thiếu gì | Chạy lại thế nào |
|-------|---|----------|------------------|
| `TC-GIFT-011` | P3 | **1 đơn `Hoàn thành` chưa tặng quà** (`SEED-GIFT-06`, TC tiêu đơn). Phiên này STG chỉ còn **2** đơn đủ điều kiện, đã dùng cho `TC-GIFT-003` + `TC-GIFT-005` (cả hai **P2**, ưu tiên cao hơn) | Tạo 1 đơn Hoàn thành mới qua flow UI (A đăng NEED → B nhận & giao → C xác nhận), rồi `/vibe-test --tc TC-GIFT-011` |
| `TC-GIFT-008` | P3 | **1 tài khoản CBNV "trắng"** (0 đơn / 0 quà). ~~STG không còn cái nào~~ → 🆕 **2026-09-21 QC cấp `stag_MinhNDN2@fpt.com`** *(SĐT HRIS chưa cập nhật; chưa login xác nhận trắng)* | Xin dev/QA cấp account mới tinh — **dùng chung** với `SEED-ACT-02` + `SEED-HOME-01`, chạy hết cụm empty state của 3 module trong 1 lượt |

## 🔴 Phát hiện ngoài phạm vi TC — cần hành động ở bước khác

### 1. Spec-gap → `/analyze-requirements --update` (⛔ không chỉ ghi vào MEMORY)

| # | Surface / hành vi trên app thật | Chưa có trong `scenario_map` |
|---|---|---|
| 1 | Card đơn `Hoàn thành` **chưa tặng quà** mang hint `Chạm để tặng quà` và **tap thẳng vào màn "Tặng quà"**. ⚠️ **Hành vi này ĐÚNG `C-GIFT-04`** (BA Resolved 2026-09-17) — cái thiếu là: `KB-GIFT-01` ô 5·Sender + **When của `SC-GIFT-001`** vẫn mô tả nút `"✓ Cảm ơn người vận chuyển"` **không tồn tại** ⇒ **sửa 2 chỗ đó cho khớp `C-GIFT-04`** | ⚠️ cần **sửa**, không phải thêm |
| 2 | Nút cuối màn "Theo dõi đơn" có **3 biến thể**: `Bạn đã đánh giá` (đã tặng quà, disable) · `Đơn đã hoàn thành ✓` (đơn đóng, không tặng quà) · `Huỷ đơn` (đơn `Đã ghép`) | ✅ mới |
| 3 | **Popup cảm ơn không đóng được bằng nút back hệ thống** — back pop màn nền, popup vẫn nổi trên mọi màn | ✅ mới |
| 4 | Thông báo `NTF-07` deep-link vào **"Quà đã nhận"**, không phải "Trang cá nhân" | ✅ mới |
| 5 | Màn "Quà đã nhận" có **2 khối**: card đếm theo loại + khối `LỊCH SỬ NHẬN QUÀ` (loại quà · người gửi · ngày giờ) | ✅ mới |

### 2. 📝 Đề nghị sửa TC / seed (⛔ KHÔNG log bug)

| TC | Vấn đề | Đề nghị |
|---|---|---|
| `TC-GIFT-009` | Expected ghi *"2 mục menu"* — app có **3** (`Đơn của tôi` · `Quà đã nhận` · `Cập nhật thông tin cá nhân`), khớp ghi chép đã chốt ở `USR-accounts.md §0` | Sửa Expected thành **3 mục** ở lượt bảo trì TC |
| `TC-GIFT-006` / `SEED-GIFT-05` | Seed ràng buộc **tên loại quà** (`3 Bông hoa + 2 Gấu bông`) nhưng mệnh đề cần kiểm chỉ là **5 quà / 2 loại / 3+2** | Nếu BA đồng ý bỏ ràng buộc tên loại ⇒ TC chạy lại được **ngay** bằng `stag_anhptm17@`, ⛔ không cần dev seed |
| `TC-GIFT-012` | Expected chứa emoji 🎁; app hiển thị **đúng verbatim phần chữ** nhưng **không có emoji** | BA chốt: bổ sung emoji vào app, hay bỏ emoji khỏi `NTF-07` + TC |
| `TC-GIFT-001` | Steps 3–4 viết theo luồng **trước** khi `C-GIFT-04` được trả lời (giả định có màn "Theo dõi đơn" trung gian + nút "✓ Cảm ơn người vận chuyển") | Gộp thành 1 step: *"Nhấn card đơn Hoàn thành chưa tặng quà (có hint `Chạm để tặng quà`)"* |
| `TC-GIFT-010` | Expected chỉ nêu *"về màn Theo dõi đơn"* — **hẹp hơn** Then của `SC-GIFT-010` (*"Theo dõi đơn **/ Đơn của tôi**"*) | Sửa Expected cho khớp scenario |

### 3a. 🔑 `RISK-GIFT-05` / `C-GIFT-02` — hành vi cũ KHÔNG tái hiện, đề nghị hạ/đóng

`KB-GIFT-04` ghi nhận (từ bản demo, tái hiện lại 2026-09-16): *back ở màn "Tặng quà" **nhảy sang màn "Xác nhận đã nhận hàng" của đơn KHÁC***, khiến `RISK-GIFT-05` bị nâng Severity **Low → Medium**.
Phiên này thử **2 lần trên đơn thật** (`TC-GIFT-010` · `TC-GIFT-005`): back về **đúng màn đã mở "Tặng quà"**, ⛔ **không** nhảy sang đơn khác, ⛔ **không** mở màn xác nhận nhận hàng.
⇒ Đề nghị **hạ `RISK-GIFT-05` về Low / đóng**, và ghi vào `C-GIFT-02` rằng build STG 2026-09-19 đã **không còn** hành vi đó.
*(⚠️ Quan sát phụ mức thấp: back **reset vị trí cuộn** danh sách về đầu — không có nguồn nào quy định phải giữ, ghi nhận để BA quyết.)*

### 3. 🔑 `KB-GIFT-03` được xác nhận bằng thực nghiệm — đề nghị đưa vào tài liệu chính thức

Quy tắc *"loại quà có count = 0 thì KHÔNG hiện ô trên card đếm"* trước nay **không có nguồn PRD**, chỉ là suy diễn. Phiên này đo được **cả 2 chiều trên 3 tài khoản**:

| Tài khoản | Quà đã nhận | Số ô hiện trên card | Kết luận |
|---|---|---|---|
| `stag_taipm@` | 1 (`Gấu bông` ×1) | **1** | ẩn 3 loại count = 0 ✅ |
| `stag_anhptm17@` | 5 (`Ly cà phê` ×3 · `Vương miện` ×2) | **2** | ẩn 2 loại count = 0 ✅ |
| `stag_giangdc2@` | 13 (3 · 3 · 4 · 3) | **4** | hiện đủ khi cả 4 đều > 0 ✅ |

### 4. 🔴 Dữ liệu test: tài khoản "dự phòng / sạch" đã KHÔNG còn sạch

`stag_anhptm17@fpt.com` = **Phan Thị Mỹ Anh**, MNV `00287493`, Phòng Văn hoá đoàn thể phía Nam — **5 đơn đã giúp / 5 quà đã nhận** *(đo 2026-09-19, ảnh `screenshots/_recon__ca-nhan-anhptm17-5-don-5-qua.png`)*.
`USR-accounts.md §2` vẫn đang giữ tài khoản này làm *"dự phòng / tài khoản sạch"* cho `TC-USR-040/043` và `TC-HOME-027/028/029` ⇒ **ghi chép đó đã sai**. Đã ghi đính chính vào `USR-accounts.md`.
⇒ **Không còn tài khoản trắng nào trên STG** — ảnh hưởng cả cụm empty state của **GIFT · ACT · HOME**.

## Recommendation

- **Automate now:** **8 TC** (`TC-GIFT-001/002/004/005/006/007/009/012`; `012` cần harvest locator icon chuông trước) — 38 locator đã verified trong `vibe-locators-latest.md`, ⛔ không cần mở lại Appium để dò
- **Bug đã log:** `TC-GIFT-003` → **FE-308** (assignee Tuanvm37) — ⏸ QC chốt 2026-09-21: **chờ FE-308 đổi trạng thái rồi tính tiếp** (không hỏi BA riêng); `TC-GIFT-012` ✅ PASS, không có bug
- **Sửa TC (⛔ không log bug):** `TC-GIFT-001` (steps 3–4 lỗi thời) · `TC-GIFT-010` (Expected hẹp hơn `SC-GIFT-010`) · `TC-GIFT-009` (2→3 mục menu) · `SEED-GIFT-05` (bỏ ràng buộc tên loại quà)
- **`/analyze-requirements --update`:** 5 surface chưa có trong `scenario_map` + sửa ma trận nhãn nút `KB-GIFT-01`
- **Wait for app:** 2 TC (`TC-GIFT-013/014`) — chờ dev build `FR09`
- **Re-run cho evidence:** 1 TC — `/vibe-test --tc TC-GIFT-010`
- **CHẠY TIẾP phần còn nợ:** **3 TC** — `/vibe-test --module gift` *(bộ lọc pending tự bốc đúng `TC-GIFT-008` + `TC-GIFT-010` + `TC-GIFT-011`)*, **sau khi** có seed

## Gate

```bash
python3 .claude/hooks/verify_evidence.py 08_test-runs/vibe/VR-011-GIFT-2026-09-19 \
  || python3 ~/.claude/skills/vibe-test/scripts/verify_evidence.py 08_test-runs/vibe/VR-011-GIFT-2026-09-19
```
