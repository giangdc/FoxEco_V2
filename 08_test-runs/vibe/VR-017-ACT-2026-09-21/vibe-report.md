# Vibe Test Report — VR-017 — module ACT — v1.1 — 2026-09-21

> Platform: **mobile** (Appium MCP / UiAutomator2) · `emulator-5554` · STG · host app `com.hrisproject.stag` (FoxPro) → FoxEco
> Tập chạy: **chỉ 10 TC v1.1** theo yêu cầu QC (`001 005 008 012 013 014 015 016 017 018`). 🔒 Chế độ **chỉ đọc** — không đổi trạng thái đơn nào trên STG.
> Tài khoản: `stag_anhdc4@` (A — có dữ liệu) · `stag_thuyntt22@` (tab `Đã hoàn thành` rỗng) · `stag_MinhNDN2@` (trắng hoàn toàn — lần đăng nhập đầu tiên)

## Scope Coverage ★★ (mẫu số = SCOPE_TOTAL của module — gồm cả CARRIED v1.0)

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module ACT)** | **18** | 100% |
| Chạy **trong run này** | **10** | 55,6% |
| ✅ PASS từ **run trước** | 0 | 0% |
| ⛔ N-A | 0 | 0% |
| ⏳ **NOT_RUN (còn nợ)** | **8** | 44,4% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

**Còn nợ 8 TC → §8 = PARTIAL.** Cả 8 là **CARRIED v1.0** (`002 003 004 006 007 009 010 011`) — ngoài phạm vi QC yêu cầu, không phải hết sức phiên.

**📊 Riêng v1.1: 10/10 có verdict (100%)** · ✅ 6 · ❌ 2 · 🚫 2.

- Sổ tích lũy: `coverage/coverage-ACT.md` · audit phiên: `scope-ledger.md` · lát cắt v1.1: `coverage/PROGRESS-v1.1.md`

## Kết quả các TC chạy trong run này (10 TC)

| Result | Count | % N_run |
|--------|-------|---|
| ✅ PASS | 6 (`001` `013` `014` `016` `017` `018`) | 60% |
| ❌ FAIL | 2 (`008` `012`) | 20% |
| 🚫 BLOCKED | 2 (`005` `015`) | 20% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|---|---|
| TC có evidence / tổng TC đã chạy | **10/10** |
| File ảnh trong `screenshots/` | 20 (16 ảnh TC + 4 `_setup`/`_recon`) · 0 cặp trùng md5 |
| Gate `.claude/hooks/verify_evidence.py` | xem mục Gate cuối file |

## 🐞 2 bug draft — chờ QC review, ⛔ chưa push Jira

| Bug | TC | Nội dung | Mức | Căn cứ |
|---|---|---|---|---|
| **`BUG-030`** | `TC-ACT-008` ❌ | Chuỗi lý do card `Hết hạn` là bản **dài** `… — tin đã tự động đóng.` | P3 · Low | `DOC-v1.1-01 §8.5.1 BR05-03` + `AC-09.1.01` chốt bản ngắn. ⚠️ nên xác nhận với BA |
| **`BUG-031`** | `TC-ACT-012` ❌ | Empty state tab `Đang diễn ra` **thiếu dòng giải thích** | P3 · Low | `BR17-01` · `EMP-05`. Quan sát kèm: tab `Đã hoàn thành` cũng thiếu |

> 🔄 **`TC-ACT-017` — không phải bug (QC chốt 2026-09-21):** tab rỗng không cuộn/không phản hồi vuốt là đúng ⇒ Expected sửa theo app, FAIL → ✅ PASS, `BUG-032` xoá.
> 🔄 **`TC-ACT-015` — không phải bug (QC chốt 2026-09-21):** app hiện đơn "Đã huỷ" ở tab "Đang diễn ra" là đúng ⇒ Expected sửa theo app (fragment + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`, `CHANGELOG` REVISE 2026-09-21). Chấm lại: FAIL → 🚫 BLOCKED (vế đơn `RETURNED` thiếu dữ liệu). ⚠️ `TC-ACT-007` (CARRIED v1.0) vẫn assert kỳ vọng cũ.

## 🚫 Blocked

| TC | Blocked at | Lý do | Gỡ bằng cách |
|---|---|---|---|
| `TC-ACT-005` · `TC-ACT-015` | Step 3 · Step 4 | Không tài khoản nào có đơn **đã trả lại người gửi** (`RETURNED`). 2 vế còn lại đúng | Dựng 1 đơn `RETURNED` qua luồng hoàn hàng (`TC-DLV-063`): A đăng NEED → B nhận + lấy hàng → *Không liên lạc được* → *Cầm hàng về* → *Trả về người gửi* → A *Xác nhận đã nhận lại hàng*. **Cần QC cấp quyền đổi trạng thái đơn trên STG.** Nên dựng trên `anhdc4` (đã có sẵn đơn `Đã huỷ`) để gỡ cả 2 TC một lượt |

## 📝 Ghi nhận ngoài Expected

- **Tài khoản `stag_thuyntt22@` KHÔNG còn trắng** (VR-014 ghi là 0 đơn): tab `Đang diễn ra` nay có 1 đơn `Đã ghép` (vai `Giao`) + 1 tin `Chờ ghép` (vai `Gửi`). Tab `Đã hoàn thành` vẫn rỗng, hero vẫn `0`.
- **`stag_MinhNDN2@` đã xác minh:** tên **Nguyễn Đình Nhật Minh**, **có FoxEco**, 0 đơn · 0 đóng góp, cả 2 tab rỗng ⇒ tài khoản trắng dùng được cho `TC-HOME-027/028/029` và `TC-GIFT-008`. Phiên này chỉ đọc nên **vẫn còn trắng**.
- **`stag_anhdc4@` có 1 đơn `Hoàn thành` chưa tặng quà** (`Gửi hàng nhỏ` · FPT Tân Thuận 1 → FPT Tân Thuận 3 · 21/9/2026, hint `Chạm để tặng quà`) ⇒ có thể gỡ nợ `TC-GIFT-010/011` (VR-011 ghi là STG không còn đơn nào như vậy).
- Từ mục nav khác quay lại `Hoạt động` thì app **luôn về tab `Đang diễn ra`**; `back` từ `Đăng tin mới` thì giữ tab đang chọn.

## Locator Coverage

| Màn đã thăm | Element | Verified ✅ | Not found 🚫 |
|---|---|---|---|
| 3 (Đơn của tôi · thanh tab dưới · FoxPro login) | 26 | 25 | 1 (`scrollable(true)` ở tab rỗng — là kết quả kiểm của `017`) |

## Dữ liệu phát sinh trên STG
- **Không có.** Không tạo/sửa/huỷ đơn nào. Chỉ đổi tài khoản đăng nhập trên máy ảo.
- **Trạng thái máy ảo cuối phiên:** `emulator-5554` đăng nhập **`stag_anhdc4@`** (đăng nhập lại để chấm `TC-ACT-015`; `stag_MinhNDN2@` đã đăng xuất, vẫn trắng). Mạng đã trả về bình thường (`speed full` · `delay none`), `show_touches = 0`.

▶️ Chạy nốt nợ của ACT:
- `TC-ACT-005` + `015` sau khi có đơn `RETURNED`: `/vibe-test --retest TC-ACT-005,TC-ACT-015`
- 8 TC CARRIED v1.0 (nếu QC muốn): `/vibe-test --module ACT --tc TC-ACT-002,TC-ACT-003,TC-ACT-004,TC-ACT-006,TC-ACT-007,TC-ACT-009,TC-ACT-010,TC-ACT-011`

## Gate
Xem kết quả `python3 .claude/hooks/verify_evidence.py 08_test-runs/vibe/VR-017-ACT-2026-09-21` ở cuối phiên.
