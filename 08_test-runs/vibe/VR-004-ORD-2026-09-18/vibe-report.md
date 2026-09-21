# Vibe Test Report — VR-004 — v1.1 (+ CARRIED v1.0) — 2026-09-18

> Platform: **mobile** (Appium MCP / UiAutomator2) · emulator-5554 (Android 13, 720x1280)
> Environment: **STG** — host app `com.hrisproject.stag` (FoxPro) → FoxEco · tài khoản **A** (`Đặng Châu Giang`, MNV 00131946)
> Module: **ORD — Đăng tin & Quản lý tin** · SCOPE_TOTAL = **88 TC** = 48 (v1.1) + 40 (CARRIED v1.0)
> Tập chạy: `--all` (user truyền tường minh) ⇒ toàn bộ 88 TC, gồm cả TC đã PASS ở VR-002

## Summary

Phiên chạy **46 TC / 5 lô** — **27 PASS · 17 FAIL · 2 BLOCKED**. Đưa module từ **42/88** lên **69/88 TC có verdict cuối** *(♻️ 2026-09-21: QC reset `083`/`084`/`085` ⇒ 66/88 — xem `coverage-ORD.md`)* (+27).
**Còn nợ 19 TC ⇒ §8 = PARTIAL** — nhưng khác mọi phiên trước: **không TC nào còn nợ vì hết sức phiên**. Đã chạy **hết mọi TC có thể chạy**; 19 TC còn lại **chặn tiền đề** (17 TC cần 1 đơn NEED đăng thành công, 2 TC cần tài khoản B).

**3 kết quả quan trọng nhất của phiên:**

1. 🐞🔴 **P1 BLOCKER MỚI — không đăng được tin NEED** (`TC-ORD-004`): API trả **400 `REQ_400`** và app **im lặng tuyệt đối**. Đây là bug nặng nhất module, **chặn cứng 17 TC** khác.
2. 🔑 **Tìm ra nguyên nhân gốc của "chặn im lặng" ở bước 2**: **cả 2 ô địa chỉ bắt buộc chạm gợi ý dropdown**; gõ tay ⇒ nút khoá vĩnh viễn, không báo gì. Đây là nguồn nhiễu đã làm VR-002 **quy kết sai** 2 TC.
3. ♻️ **Bác bỏ 1 phần kết luận của VR-002**: luật *"địa chỉ giao phải khác địa chỉ lấy"* **CÓ thông báo lỗi đầy đủ** (`TC-ORD-026` PASS) ⇒ `TC-ORD-083`/`084` phải **gỡ khỏi dẫn chứng bug F3/F7**.

## Scope Coverage ★★

> Mẫu số LUÔN là SCOPE_TOTAL của module (88), không phải số TC đã chạy phiên này.
> Bảng dưới là trạng thái **của cả module ORD sau khi merge VR-004**.

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module ORD)** | **88** | 100% |
| Chạy **trong run này** (có verdict cuối) | **46** | 52% |
| Có verdict cuối từ **run trước**, không chạy lại | 23 | 26% |
| ⛔ N-A (cố ý không test qua UI) | 0 | 0% |
| ⏳ **NOT_RUN (còn nợ)** | **19** | **22%** |
| ⚠️ NOT_EVIDENCED (còn nợ) | **0** | 0% |
| **⇒ Tổng có verdict cuối** | **69** | **78%** |

**Còn nợ = 19 TC → §8 = PARTIAL.**

- Chi tiết từng TC **của module (xuyên run)**: `08_test-runs/vibe/coverage/coverage-ORD.md` ← **xem cái này**
- Chi tiết **run này làm gì**: `scope-ledger.md` trong run folder

### 📋 19 TC còn nợ — phân loại theo lý do (không TC nào bị bỏ vì hết phiên)

| Nhóm | Số TC | TC | Gỡ chặn bằng cách nào |
|---|--:|---|---|
| **Chặn bởi bug `TC-ORD-004`** *(cần 1 đơn NEED đăng thành công)* | **17** | `038`·`039`·`040`·`041`·`046`·`048`·`049`·`052`·`060`·`061`·`065`·`067`·`072`·`073`·`080`·`082`·`088` | Dev fix API 400 ⇒ **1 phiên là phủ hết 17 TC** |
| **Thiếu tài khoản B** *(TC đòi 2 CBNV khác nhau)* | **2** | `044`·`045` | QC cấp tài khoản CBNV thứ 2 + phiên OTP |

## Kết quả 46 TC chạy trong run này

| Result | Count | % trên 46 |
|--------|-------|---|
| ✅ PASS | **27** | 59% |
| ❌ FAIL | **17** | 37% |
| 🚫 BLOCKED | **2** | 4% |
| ⚠️ NOT_EVIDENCED | **0** | 0% |

Theo lô: **lô 1** 14 TC (*Đăng tin mới* + *Wizard Bước 1*) · **lô 2** 6 TC (*Bước 3* + *OFFER*) · **lô 3** 13 TC (*Bước 2* — người gửi/nhận/email/biên) · **lô 4** 9 TC (*uỷ quyền* + *buổi* + *địa chỉ trùng*) · **lô 5** 4 TC (*chi tiết đơn*).

### 28 TC lần đầu có verdict (VR-002 để NOT_RUN)
`001` · `003` · `004` · `019` · `020` · `021` · `022` · `023` · `024` · `025` · `026` · `029` · `032` · `033` · `034` · `035` · `036` · `037` · `042` · `043` · `047` · `050` · `051` · `055` · `079` · `081` · `085` · `086`

### 1 TC ĐỔI VERDICT so với VR-002
| TC | VR-002 | VR-004 | Vì sao |
|---|---|---|---|
| `TC-ORD-017` | ✅ PASS | ❌ **FAIL** | Ô *Địa chỉ lấy hàng* **mất prefill** — hồ sơ tài khoản A không còn "Địa chỉ mặc định" (gốc: `TC-USR-040` VR-003). **Không phải TC lỗi thời — là lỗi thật.** |

### 18 TC chạy lại theo `--all` — 17 TC verdict KHÔNG đổi
`002`·`005`·`006`·`007`·`008`·`009`·`010`·`011`·`012`·`013`·`014`·`015`·`016`·`018`·`054`·`083`·`084` ⇒ **kết quả VR-002 tin được**; riêng `083`/`084` giữ FAIL nhưng **đổi hẳn nguyên nhân** (xem mục Bug). TC thứ 18 là `017` — **đổi verdict**, xem bảng trên.

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | **46/46 (100%)** |
| File ảnh trong `screenshots/` | **86** (74 ảnh TC + 2 `_setup` + 10 `_recon`) · **6.96 MB** sau nén |
| Nén ảnh | ✅ **lossless** (`PNG optimize`, −3.7%). ⛔ **CỐ Ý KHÔNG dùng nén palette-256** (giảm được ~4×) vì **2 kết luận của phiên dựa trên giá trị pixel chính xác**: `TC-ORD-085` (icon copy `(160,164,175)`) và lượt đính chính *nút disable có làm mờ* (`(253,175,62)` vs `(255,160,0)`). Nén lossy sẽ **phá khả năng QC lead đo lại** |
| Ảnh trùng md5 mang 2 mã TC khác nhau | **0** *(đã phát hiện 5 cặp và chụp lại riêng — xem ghi chú ♻️ đầu `vibe-log.md`)* |
| TC thiếu evidence (⚠️ NOT_EVIDENCED) | **không có** |
| Log phụ trợ | `logcat-TC-ORD-004-REQ_400.txt` — 9 dòng, 3 lần lỗi API |
| Gate `.claude/hooks/verify_evidence.py` | **0 vi phạm fabrication** — missing/batched/dangling/misattributed/no_citation/orphan/uncited/badname/undeclared-session **đều rỗng**; trích dẫn **46/46**. Chỉ báo *"RUN CHƯA HOÀN TẤT"* vì 19 TC còn nợ ⇒ đúng ca **PARTIAL** |

→ QC lead verify từng case bằng `screenshots/TC-ORD-<NNN>__verify*.png` / `__step<N>-FAIL*.png` (1 file riêng/TC).

## Locator Coverage

| Màn harvest | Element MỚI | ✅ Verified | 🚫 NOT FOUND *(verify_absent)* | Đính chính map cũ |
|---|--:|--:|--:|--:|
| 6 | **≈ 41** | 35 | 24 | **4** |

→ `implement-automation` đọc `08_test-runs/vibe/locators/vibe-locators-latest.md` — đã merge **100%** selector của phiên (tự kiểm: 35/35 selector có mặt).
→ **4 bẫy kỹ thuật mới T11–T14** (đặc biệt **T11**: 2 ô địa chỉ bắt buộc chạm gợi ý) — ⛔ đọc trước khi implement bước 2.

## 🐞 Bug & ứng viên bug — phân tích gộp

> ⚠️ **17 FAIL KHÔNG phải 17 bug.** Phân rã:

| # | Bug / nhóm | Mức | TC dẫn chứng | Ghi chú |
|---|---|---|---|---|
| **B1** | 🔴 **Không đăng được tin NEED** — API 400 `REQ_400`, app im lặng hoàn toàn | **P1 / Blocker** | `TC-ORD-004` | 3 lần bấm/3 lần lỗi · đã loại trừ giả thuyết ghi chú 300 ký tự · không đơn nào được tạo. **Nên tách 2 bug** nếu Dev API ≠ Dev app: (a) API từ chối payload hợp lệ; (b) client không hiển thị lỗi (`details: undefined`) |
| **B2** | 🔴 **Chặn im lặng** — nút khoá/không đi tiếp mà **không báo lỗi ở đâu** | **P1** | `TC-ORD-023` (P1) · `051` · `021` · `024` · `014` · `008` · `043` *(luồng OFFER)* | ⭐ **Dùng `TC-ORD-051` làm TC đại diện** (mô tả đúng nhất: không lỗi tại ô **và** không cuộn tới ô lỗi). ⛔ **Không được đóng bug bằng lý do "app chưa có cơ chế báo lỗi"** — `TC-ORD-025` và `079` chứng minh app **có** lỗi inline đầy đủ ở ô SĐT; lỗi bị thiếu **theo từng nhánh** |
| **B3** | 🔴 **Ô địa chỉ bắt buộc chọn từ gợi ý nhưng không báo gì** *(nhánh cụ thể, nặng nhất của B2)* | **P1** | `TC-ORD-083` · `084` | ⭐ **Đây là nguyên nhân thật** mà VR-002 quy nhầm cho *"nhánh trùng địa chỉ"*. Gõ tay đủ chữ ⇒ nút khoá vĩnh viễn, 0 thông báo. Người dùng **không có cách nào biết** phải chạm gợi ý |
| **B4** | 🟠 **Prefill địa chỉ từ hồ sơ/HRIS không hoạt động** | **P2** | `TC-ORD-017` · `043` **+ `TC-USR-040`** *(module USR)* | **Gộp 3 TC / 2 module vào 1 bug.** Hậu quả kép: vừa sai kỳ vọng, vừa **kích hoạt B3** (ô rỗng ⇒ buộc gõ tay) |
| **B5** | 🟠 **Autofill người nhận thiếu ô địa chỉ giao** | **P1** *(chờ BA)* | `TC-ORD-019` (P1) **+ `TC-ORD-074`** *(VR-002, P1)* | 2 TC ở 2 version cùng chỉ 1 lỗi. ⚠️ **Cần BA chốt trước khi log**: chính thông báo app nói *"vui lòng bổ sung SĐT/địa chỉ giao còn thiếu"* mà app **lại điền được SĐT** ⇒ hành vi đúng là autofill 3 hay 2 field? |
| ~~B6~~ | ♻️ **ĐÃ RÚT (2026-09-21)** — *lỗi validate không tự xoá khi đã sửa input* | — | phát hiện khi chạy `TC-ORD-083` | **Không phải bug.** Validate chỉ chạy khi **rời ô** (on blur — `VAL-02`); log không có bước rời ô sau khi sửa. `TC-ORD-083`/`084` được QC reset về NOT_RUN để test lại (phải rời ô trước khi đọc lỗi) |
| **B7** | 🟡 **Nút gửi form OFFER luôn `enabled`** dù thiếu trường | **P3** | `TC-ORD-050` | Trái `VAL-01` nên TC FAIL đúng, **nhưng OFFER vẫn không cho đăng và có lỗi inline** ⇒ **UX tốt hơn NEED**. 💡 **Khuyến nghị: đừng fix OFFER cho giống NEED — hãy port cơ chế lỗi inline của OFFER sang NEED** để dứt điểm B2 |
| ~~B8~~ | ♻️ **ĐÃ RÚT (2026-09-21, chờ check lại ở VR kế tiếp)** — *copy không có phản hồi thị giác* | — | `TC-ORD-085` | QC xác nhận bấm icon copy **có** hiện `Đã copy` ~2s. Kết luận cũ đo bằng pixel 2 ảnh `adb screencap` → dễ âm tính giả do độ trễ chụp. **Không phải bug cho tới khi có bằng chứng quay màn hình.** Xem ghi chú ở `coverage-ORD.md` dòng `TC-ORD-085` |
| ~~B9~~ | ♻️ **ĐÃ RÚT LẠI** — *nút disable không làm mờ* | — | `TC-ORD-008` step 3 | **Không phải bug.** Đo pixel: nền disable `(253,175,62)` cam nhạt vs enable `(255,160,0)` cam bão hoà ⇒ **app CÓ làm mờ**. Kết luận ban đầu sai vì **nhìn bằng mắt trên ảnh**; VR-002 (`CHANGELOG ORD §Nợ #3`) đã đúng |

### 🔴 5 TC FAIL là **nợ QC**, ⛔ KHÔNG phải bug — chờ chốt `DESCOPED` (`Project_rule §10.5`)

| TC | Vì sao hết hiệu lực | Khuyến nghị |
|---|---|---|
| `TC-ORD-006` | `C-ORD-09` chốt **CÓ** nhãn "Tài liệu"; `TC-ORD-005` (v1.1) là bản thay thế | DESCOPED |
| `TC-ORD-014` | **Mâu thuẫn TRỰC TIẾP** `TC-ORD-063` (v1.1 **P1**: thiếu ảnh PHẢI chặn) | DESCOPED — **bắt buộc**, 2 TC không thể cùng đúng |
| `TC-ORD-007` · `008` | v1.1 thêm 3 trường bắt buộc ⇒ vế điều hướng sai *(điểm kiểm chính của `007` vẫn PASS)* | DESCOPED hoặc sửa vế điều hướng |
| `TC-ORD-011` | chỉ **step 4-5** lỗi thời; **biên 300/301 PASS trọn** | ⭐ **chỉ cần bỏ step 4-5** là dùng lại được — không cần DESCOPED |
| `TC-ORD-033` *(BLOCKED)* | v1.1 bỏ "khung giờ", thay bằng chip BUỔI **không có mặc định** ⇒ không dựng được tiền đề | DESCOPED — rule đã được `TC-ORD-059` phủ |

### ⚠️ 2 TC cần QC xem lại THIẾT KẾ (không phải bug app)

| TC | Vấn đề |
|---|---|
| `TC-ORD-084` | Không thực thi được đúng ý đồ trên v1.1: **không thể vừa "chạm chọn gợi ý" vừa "thêm khoảng trắng đầu/cuối"** ⇒ biên trim **không kiểm được**. Ghi chú VR-002 *"so sánh CÓ trim"* là **suy diễn không căn cứ** |
| `TC-ORD-034` | Expected không đòi TRỌNG LƯỢNG/KÍCH THƯỚC/ảnh trong tóm tắt bước 3 — mà v1.1 đã thêm 3 trường **bắt buộc** này. **Không TC nào của v1.1 assert chúng xuất hiện ở bước 3** ⇒ spec gap |

## 🔁 Phản hồi ngược → analyze-requirements

| Surface phát hiện trên app | Route |
|---|---|
| Tóm tắt Bước 3/3 **thiếu** TRỌNG LƯỢNG + KÍCH THƯỚC + ảnh *(3 trường bắt buộc v1.1)* | `/analyze-requirements --update "Bước 3/3 tóm tắt đơn thiếu TRỌNG LƯỢNG + KÍCH THƯỚC + ảnh hàng"` |
| **2 ô địa chỉ bước 2 là autocomplete BẮT BUỘC chọn gợi ý** — hành vi này **không có trong scenario_map** | `/analyze-requirements --update "Ô địa chỉ lấy/giao ở Bước 2 bắt buộc chọn từ dropdown gợi ý; gõ tay không được chấp nhận"` |
| Màn chi tiết đơn **đã ghép** không lộ SĐT — **trái banner cam kết** *"sau khi ghép SĐT hai bên sẽ được lộ"* | Clarification cho BA *(đã ghi ở `TC-ORD-086`)* |
| Email **ngoài tên miền** nhận thông báo *"không tìm thấy… nhập tay"* thay vì *"sai tên miền"* | raise cùng **F5** (câu chữ v1.0 còn sót) |

## Recommendation

- **🔴 Ưu tiên tuyệt đối — `/log-bug` bug B1** (P1 Blocker): không đăng được tin NEED. **17/19 TC còn nợ của module phụ thuộc bug này.**
- **`/log-bug` gộp** B2+B3+B9 thành 1 bug chặn-im-lặng (TC đại diện `TC-ORD-051`), B4 gộp 3 TC / 2 module, B7 log dạng `Suggest` (draft `BUG-016`) *(B6, B8, B9 đã rút — không phải bug; B8 chờ check lại)*.
- **Chờ BA** trước khi log B5 (`TC-ORD-019`/`074`).
- **QC chốt DESCOPED** 5 TC hết hiệu lực + xem lại thiết kế `TC-ORD-084`, `TC-ORD-034`.
- **Cấp tài khoản B** để gỡ `TC-ORD-044`/`045`.
- **CHẠY TIẾP sau khi B1 được fix:** `/vibe-test --module ORD` → bộ lọc pending tự bốc đúng 19 TC còn nợ.
- **Chưa nên `/implement-automation` cho ORD**: luồng đăng tin đang vỡ ở API; nhưng **41 locator + 4 bẫy T11–T14 đã sẵn** trong `vibe-locators-latest.md` để dùng khi mở automation.
