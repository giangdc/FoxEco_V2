# Vibe Test Report — VR-005 — v1.1 (+ CARRIED v1.0) — 2026-09-19

> Platform: **mobile (Appium MCP / UiAutomator2)** · Device `emulator-5554` · Session `55129e7d-a214-4167-a988-d83f2e82c2b7`
> Environment: **STG** — app `com.hrisproject.stag` (host FoxPro → FoxEco) · Tài khoản **A** = `Đặng Châu Giang`
> Module: **HOME** (Trang chủ) · SCOPE_TOTAL: **30 TC**

## Scope Coverage ★★

> Mẫu số LUÔN là SCOPE_TOTAL của module (30), ⛔ không phải số TC chạy phiên này.

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module HOME)** | **30** | 100% |
| Chạy **trong run này** | 14 | 47% |
| ✅ PASS từ **run trước** | 0 | 0% |
| ⛔ N-A (cố ý không test qua UI, có lý do) | 1 | 3% |
| ⏳ **NOT_RUN (còn nợ)** | **15** | **50%** |
| ⚠️ NOT_EVIDENCED (còn nợ) | 0 | 0% |

**Có verdict cuối: 15/30 · Còn nợ = 15 TC → §8 = PARTIAL.**

- Chi tiết từng TC **của module (xuyên run)**: `08_test-runs/vibe/coverage/coverage-HOME.md` ← **xem cái này**
- Chi tiết **run này làm gì**: `scope-ledger.md` trong run folder

### 🔢 Đính chính SCOPE_TOTAL = 30 (⛔ không phải 33)

`TC-HOME-v1.1.md §0.1` ghi *"33 TC = 24 của v1.0 − 2 gỡ + 11 của v1.1"*. Phép tính đó **đếm trùng 3 TC MODIFIED** — `TC-HOME-008/019/021` tồn tại ở **cả hai** file, và `CLAUDE.md` chốt **"LUÔN lấy bản v1.1"**. Hợp nhất theo ID duy nhất:

```
24 (v1.0)  − 2 (TC-HOME-010/024 DEPRECATED, ⛔ không chạy)
           − 3 (TC-HOME-008/019/021 trùng ID → lấy bản v1.1)
           + 11 (v1.1)                                        = 30
```

⛔ **Không sửa fragment** (`Project_rule §10.5` FREEZE Σ TC). Đây là đính chính **cách ĐẾM**, không thêm/bớt TC nào.

## Kết quả các TC chạy trong run này

| Result | Count | % trên 14 |
|--------|-------|---|
| ✅ PASS | 12 | 86% |
| ❌ FAIL | 1 | 7% |
| 🚫 BLOCKED | 1 | 7% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | **14/14 (100%)** |
| File ảnh trong `screenshots/` | 23 (20 ảnh TC + 3 `_setup`/`_recon`) |
| TC thiếu evidence (⚠️ NOT_EVIDENCED) | — không có |
| Gate `verify_evidence.py` (bản **dự án** `.claude/hooks/`) | ✅ **0 vi phạm** — `Evidence 14/14 · Trích dẫn 14/14 (rule 1)`. Chỉ còn **nợ coverage 15/30** ⇒ §8 = **PARTIAL** (đúng luật, không phải lỗi) |

## 🔴 Kết luận quan trọng nhất của phiên

> **STG đang có 0 tin NEED hợp lệ trên toàn hệ thống.** Xác nhận từ **2 bề mặt độc lập** — section "Tin mới" của Trang chủ (`home-news-empty`) và màn Bảng tin (*"Chưa có tin nào"*) ⇒ ⛔ không phải lỗi lọc của riêng Trang chủ.

Hệ quả kép, ngược chiều nhau:

| Chiều | Tác động |
|---|---|
| 🍀 **Mở khoá 1 TC** | `TC-HOME-026` (empty state `EMP-01`) — `fragment §0.3` xếp nó vào nhóm *"không dựng được trên STG dùng chung ⇒ ghi Blocked"*, nhưng phiên này verify được **thật**, đủ 4/4 vế nguyên văn |
| ⛔ **Chặn 8 TC** | `017` `018` `019` `020` `021` `023` `025` `030` — đều cần ≥1 tin do **tài khoản khác** đăng |

🔑 **Vì sao không tự seed được:** *"Tin mới"* **loại trừ tin của chính mình** (`SC-HOME-019`) ⇒ tài khoản A đăng tin cũng **không** làm section này có dữ liệu. Bắt buộc cần **tài khoản B**, mà đăng nhập tài khoản khác đang vướng **OTP nhập tay** — đúng blocker đã ghi ở `VR-001` và `VR-003`.

## Failed TCs — cần review TC hoặc fix app

| TC ID | Failed at | Expected | Actual |
|-------|----------|----------|--------|
| **TC-HOME-007** | Step 2 / E1 | tagline `Tiện đường — Đồng nghiệp giúp nhau` | `Tiện đường —\nGiúp đồng nghiệp` *(MCP `get_text`, nguyên văn)* |

🐞 **Ứng viên bug H1 — ⛔ CHƯA log bug.** Cần QC/BA chốt **chuỗi nào là oracle** trước: rất có thể đây là **TC/tài liệu lỗi thời** chứ không phải app sai (cùng họ với `TC-ORD-006` ở VR-002 và `KB-VIBE-01`). Vế 2 của TC (*nhấn banner không điều hướng*) **PASS**.
ℹ️ App còn có dòng phụ `Gửi hàng nội bộ · Không phí · Không chat` ngay dưới tagline — **không nằm trong Expected**, đề nghị BA rà khi chốt chuỗi.

## Blocked TCs — ⚠️ KHÔNG automate

| TC ID | Blocked at | Reason | Impact |
|-------|-----------|--------|--------|
| **TC-HOME-002** | Step 2 | Bảng tin **0 tin** ⇒ không mở được màn **Chi tiết tin** | **3/4 màn con đã kiểm và ĐÚNG** (Theo dõi đơn · Wizard · Thông báo — đều không bottom nav, đều có nút quay lại). Chỉ thiếu màn Chi tiết tin ⇒ chạy lại khi STG có ≥1 tin |

## Passed TCs — sẵn sàng implement automation

| TC ID | Steps | Locators captured | Evidence file |
|-------|-------|------------------|---------------|
| TC-HOME-001 | 2 | 5 | `screenshots/TC-HOME-001__verify-bottom-nav-5-tabs.png` |
| TC-HOME-003 | 2 | 2 | `screenshots/TC-HOME-003__verify-greeting-name.png` |
| TC-HOME-005 | 2 | 1 | `screenshots/TC-HOME-005__verify-chuong-cham-do.png` |
| TC-HOME-006 | 4 | 2 | `screenshots/TC-HOME-006__verify-chuong-khong-cham-do.png` |
| TC-HOME-009 | 3 | 2 | `screenshots/TC-HOME-009__verify-6-thanh-phan-don-cua-toi.png` |
| TC-HOME-011 | 3 | 1 | `screenshots/TC-HOME-011__verify-nhan-vai-gui.png` |
| TC-HOME-012 | 3 | 1 | `screenshots/TC-HOME-012__verify-nhan-vai-giao.png` |
| TC-HOME-013 | 3 | 1 | `screenshots/TC-HOME-013__verify-nhan-vai-nhan.png` |
| TC-HOME-015 | 3 | 1 | `screenshots/TC-HOME-015__verify-lo-trinh-khop.png` · `…__verify-loai-hang-khop.png` |
| TC-HOME-016 | 3 | 1 | `screenshots/TC-HOME-016__verify-mo-man-hoat-dong.png` |
| TC-HOME-022 | 2 | 1 | `screenshots/TC-HOME-022__verify-chuyen-tab-bang-tin.png` |
| TC-HOME-026 | 3 | 4 | `screenshots/TC-HOME-026__verify-empty-state-tin-moi.png` |

⚠️ **5 TC PASS kèm khai báo lệch step** (`009` `011` `012` `013` `015`): dùng **đơn có sẵn** thay vì tự đăng tin mới ở step 1, vì **không đăng được tin NEED** (bug `B1` của VR-004). Trong cả 5 ca, Expected **không assert** trạng thái đơn — chỉ assert thành phần/nhãn/điều hướng ⇒ verdict tin được. Chi tiết từng ca ghi trong `vibe-log.md`.

## NOT_EVIDENCED TCs

Không có — **14/14 TC đã chạy đều có ảnh riêng**.

## Locator Coverage

| Màn đã harvest | Elements | ✅ Verified | ⚠️ Inferred | 🚫 NOT FOUND |
|--------------|------------------|------------|-------------|---|
| **8** | **51** | **24** | **23** | **4** |

→ Đã merge **51/51 = 100%** vào `08_test-runs/vibe/locators/vibe-locators-latest.md`.
→ 🚫 4 NOT FOUND đều là **"không có locator"**, ⛔ không phải "locator sai" — xem 3 bẫy mới dưới.

### 🔧 3 bẫy kỹ thuật MỚI (T15–T17) + 1 tái hiện

| # | Bẫy | Hệ quả nếu không biết |
|---|---|---|
| **T15** | Chấm đỏ chuông = **ViewGroup ẩn danh** (không text/desc/rid) | assert bằng `find_element` sẽ **không bao giờ** tìm thấy ⇒ phải **đo pixel** (`RGB(244,64,74)`) |
| **T16** | Thanh progress 5 bước **không có node nào** trong tree | ⛔ không đếm được số bước bằng accessibility ⇒ phải **đo pixel** |
| **T17** | `content-desc` của card đơn là **chuỗi gộp cả 5 dòng** | khớp full string sẽ **gãy** mỗi khi badge/địa chỉ đổi ⇒ dùng `descriptionStartsWith("<Vai>: <Loại hàng>")` |
| **T2** *(lần 3)* | `resource-id` có trong source nhưng **không resolve** qua strategy `id` | ca mới: `home-news-empty` ⇒ luôn có đường lui `-android uiautomator resourceId(...)` |

## 📨 Phản hồi ngược → `/analyze-requirements`

| # | Bề mặt gặp trên app thật | Vì sao là spec gap |
|---|---|---|
| 1 | Section "Đơn của tôi" chứa card **`Nhận giao hàng Thuận đường`** — **không có nhãn vai** dạng `<Vai>:` | `SC-HOME-011/012/013` chỉ đặc tả **3 nhãn vai của đơn**; card này là **tin OFFER**, ⛔ chưa được phân tích |
| 2 | Section "Đơn của tôi" hiển thị **cả đơn `Đã huỷ` và `Đã giao`** (6 card) | mọi TC của section này đều nói *"đơn **đang hoạt động**"* ⇒ cần BA chốt phạm vi section |
| 3 | Header Trang chủ **không có node icon vai trò nào** (chỉ `Quay lại` · lời chào · `Thông báo`) | `SC-HOME-004` giả định có icon vai trò ⇒ cần BA xác nhận bề mặt đã build chưa, trước khi chạy `TC-HOME-004` |

## 🗂️ Dữ liệu phát sinh trên STG

| Thay đổi | Ảnh hưởng |
|---|---|
| **Toàn bộ thông báo của tài khoản A → đã đọc** (nút bulk `Đánh dấu đã đọc`, `TC-HOME-006`) | ⚠️ muốn chạy lại `TC-HOME-005` (chuông có chấm đỏ) phải có **sự kiện sinh thông báo mới** |
| Không đăng tin, không nhận/huỷ đơn nào | ✅ số đơn cộng đồng giữ nguyên `317 đơn · 23743 người`; hero giữ `13` |

## Recommendation

- **Automate now:** **12 TC** — locators sẵn trong `vibe-locators-latest.md` (⚠️ 3 TC cần **đo pixel**: `001` trạng thái tab · `005`/`006` chấm đỏ · `009` thanh progress)
- **Cần QC/BA quyết:** **1 TC** — `TC-HOME-007`, chốt chuỗi tagline nào là oracle rồi mới log bug hoặc sửa TC
- **Chờ dữ liệu (tài khoản B + OTP):** **8 TC** — `017` `018` `019` `020` `021` `023` `025` `030`, cộng `002` để đóng nốt
- **Chờ 3 tài khoản + fix bug `B1`:** **5 TC** — `004` `008` `014` `029` `031`
- **Chờ môi trường riêng:** **2 TC** — `027` `028` (riêng `028` ⛔ bất khả trên STG dùng chung)
- **Ngoài phạm vi vibe-test:** **1 TC** — `032` (NFR load-test 1.000 user → skill `k6-load-test`)
- **CHẠY TIẾP phần còn nợ:** `/vibe-test --module HOME` *(bộ lọc pending tự bốc đúng 15 TC còn nợ)*

> 🛑 **Phiên dừng KHÔNG phải vì hết sức** — đã chạy hết mọi TC mà dữ liệu STG hiện tại cho phép.
> 16 TC còn lại chặn ở **tiền đề dữ liệu/môi trường**, ⛔ chạy lâu hơn không gỡ được.

## 🧾 Ghi chú retention (trước khi commit)

| Quyết định | Lý do |
|---|---|
| Giữ `TC-HOME-007__pre-banner-before-tap.png` | TC **FAIL** ⇒ đúng luật giữ ảnh phụ; nó là vế "trước khi tap" của cặp so sánh chứng minh **không điều hướng** |
| Giữ `TC-HOME-015__pre-card-truoc-khi-cham.png` **(ngoại lệ có chủ ý)** | Luật mặc định bỏ ảnh `__pre` của TC **PASS**, nhưng ảnh này là **vế "trước"** của phép đối chiếu card ↔ màn Theo dõi đơn — bỏ đi thì Expected *"trùng khớp"* mất một nửa căn cứ |
| Giữ 3 ảnh `_setup__`/`_recon__` | `_recon__bang-tin-empty-0-tin.png` là **căn cứ chung** cho verdict BLOCKED/NOT_RUN của 9 TC |
| Không có `_snapshots/` để xoá | page source do MCP tự ghi ra **ngoài repo** (thư mục tool-results), ⛔ không lọt vào cây evidence |
| ⛔ Không commit video | không quay video trong phiên này |
