# Vibe Test Report — VR-012 — module **DLV** — 2026-09-19

> Platform: **mobile (Appium MCP · UiAutomator2)** · Device `emulator-5554` · App `com.hrisproject.stag` (FoxPro host → FoxEco)
> Environment: **STG** · Tài khoản: **`stag_anhdc4@fpt.com` — Đặng Châu Anh** (MNV `00286248`)
> SCOPE_TOTAL module DLV: **81 TC** = 30 CARRIED v1.0 (`001–030`) + 51 NEW v1.1 (`031–081`) · **0 TC ID trùng** giữa 2 file
> 🆕 **Phiên vibe-test ĐẦU TIÊN của module DLV** — sổ cái `coverage/coverage-DLV.md` mở ở chính phiên này.

## Scope Coverage ★★

> Mẫu số luôn là **SCOPE_TOTAL của module (81)**, không phải số TC chạy trong phiên.

| | Count | % scope |
|---|--:|--:|
| **SCOPE_TOTAL (module DLV)** | **81** | 100% |
| Chạy **trong run này** (có verdict + evidence) | **15** | 18.5% |
| ✅ PASS từ **run trước** | 0 | 0% |
| ⛔ N-A (API-tier, có lý do từng TC) | **4** | 4.9% |
| ⏳ **NOT_RUN (còn nợ)** | **62** | **76.5%** |
| ⚠️ NOT_EVIDENCED (còn nợ) | 0 | 0% |

**Có verdict cuối: 19/81 · CÒN NỢ: 62 TC → §8 = PARTIAL.**

- Chi tiết từng TC **của module (xuyên run)**: `08_test-runs/vibe/coverage/coverage-DLV.md` ← **xem file này**
- Chi tiết **run này làm gì**: `scope-ledger.md` trong run folder

## 🚫 BLOCKER — nguyên nhân của 55/62 TC còn nợ (đọc trước mọi phần khác)

> **Phiên dừng KHÔNG phải vì hết sức, không phải vì MCP hỏng, và không phải vì app lỗi.**
> Lúc **22:15**, thao tác `tap` nút **`Đã giao cho người nhận`** bị **auto-mode classifier của Claude Code từ chối**:
>
> ```
> Permission denied by the Claude Code auto mode classifier.
> Reason: [Modify Shared Resources]
> ```
>
> Thao tác này **đẩy trạng thái thật của một đơn trên STG** (`Đang giao` → `Đã giao`), nên bị xếp vào nhóm *"sửa tài nguyên dùng chung"*.

**Vì sao nó chặn nhiều TC đến vậy:** module DLV là **máy trạng thái**. Hầu hết TC còn lại cần ≥1 trong 4 thao tác đều thuộc nhóm bị chặn:

| Nhóm thao tác bị chặn | Mở khoá được nhóm TC nào | Số TC |
|---|---|--:|
| Đổi trạng thái đơn (`Tôi đã lấy hàng` · `Đã giao cho người nhận` · `Xác nhận đã nhận hàng`) | `017`–`023`, `041`–`053`, `058`–`066`, `068`–`073` | ~35 |
| Mở màn **"Xác nhận đã giao"** (v1.1) — chỉ vào được qua CTA trên | `043`–`056` *(giao tận tay / uỷ quyền / quầy lễ tân / bảo vệ / không liên lạc được)* | ~14 |
| Đăng tin NEED mới để dựng tiền đề | `002`, `003`, `004`–`006`, `030`, `037`–`039` | ~9 |
| Đăng xuất → đăng nhập tài khoản khác | `022` *(P1)*, `030`, `037`–`039` | ~5 |

⇒ **Không có cách vòng tránh nào hợp lệ.** Đọc-only đã được khai thác **hết mức**: 15 TC chạy được trong phiên này **đều** là TC quan sát thuần (nhãn/nút/cụm liên hệ/nhật ký), tận dụng **đơn có sẵn trên STG ở đủ 3 vai × 5 trạng thái** — chính vì tận dụng được kho đơn này mà phiên vẫn chốt được 15 TC thay vì 0.

**Để chạy tiếp cần user quyết 1 trong 2:**
1. **Cấp quyền** cho các thao tác đổi trạng thái đơn trên STG *(khuyến nghị — đây là môi trường staging, và đổi trạng thái đơn chính là **nội dung** của module DLV)*; hoặc
2. **Chạy `/vibe-test --module DLV` ở chế độ permission nới hơn** (vd `acceptEdits`/bypass) cho riêng phiên DLV.

## Kết quả các TC chạy trong run này (15 TC)

| Result | Count | % trên 15 |
|---|--:|--:|
| ✅ PASS | **13** | 86.7% |
| ❌ FAIL | **2** | 13.3% |
| 🚫 BLOCKED | 0 | 0% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|---|---|
| TC có evidence / tổng TC đã chạy | **15/15 (100%)** |
| File ảnh trong `screenshots/` | 27 (18 ảnh TC + 9 `_setup`/`_recon`) |
| TC thiếu evidence (⚠️ NOT_EVIDENCED) | **không có** |
| Gate `verify_evidence.py` | ❌ exit 1 — **chỉ do còn nợ coverage** (62 TC `⏳ NOT_RUN`), ⛔ **0 vi phạm evidence, 0 vi phạm ràng buộc 2 chiều TC↔ảnh** |

## Failed TCs — cần fix app

| TC ID | Failed at | Expected | Actual |
|---|---|---|---|
| **TC-DLV-081** (P3) | step 6b | icon copy cạnh **địa chỉ giao** đổi **màu xanh ~2 giây** rồi trở lại | icon giữ nguyên **xám `(160,164,175)`** ở cả t≈0s và t≈3s. **Nội dung copy ĐÚNG** (`04, 05 Nguyễn Duy Hiệu`) |
| **TC-DLV-080** (P3) | step 6b | icon copy cạnh **SĐT** đổi màu xanh ~2 giây | icon giữ nguyên xám. **Nội dung copy ĐÚNG** (`0900000037`) |

> 🐛 **2 FAIL này + `TC-ORD-085` (VR-004) là MỘT lỗi gốc duy nhất:** component *icon copy* dùng chung **không có state phản hồi thị giác**. ⇒ mở **1 bug cho component**, ⛔ không mở 3 bug riêng. Chức năng copy vẫn đúng ⇒ **severity thấp**, nhưng đã tái hiện ở **2 run độc lập**.

## Passed TCs — sẵn sàng implement automation

| TC ID | Vai · trạng thái | Evidence file |
|---|---|---|
| TC-DLV-001 | gửi · Chờ ghép | `screenshots/TC-DLV-001__verify-nhan-cho-van-chuyen-khoa.png` |
| TC-DLV-008 | vận chuyển · Đang giao | `screenshots/TC-DLV-008__verify-nut-da-giao-cho-nguoi-nhan-bat.png` |
| TC-DLV-009 | nhận · Đang giao | `screenshots/TC-DLV-009__verify-nhan-don-dang-tren-duong.png` |
| TC-DLV-010 | gửi · Đã giao | `screenshots/TC-DLV-010__verify-nhan-cho-nguoi-nhan-xac-nhan.png` |
| TC-DLV-011 | vận chuyển · Đã giao | `screenshots/TC-DLV-011__verify-carrier-nhan-cho-nguoi-nhan-xac-nhan.png` |
| TC-DLV-012 *(P1)* | nhận · Đã giao | `screenshots/TC-DLV-012__verify-nut-xac-nhan-da-nhan-hang-bat.png` |
| TC-DLV-014 | vận chuyển · Hoàn thành | `screenshots/TC-DLV-014__verify-carrier-nhan-don-da-hoan-thanh.png` |
| TC-DLV-015 | nhận · Hoàn thành | `screenshots/TC-DLV-015__verify-nhan-don-da-hoan-thanh.png` |
| TC-DLV-026 | cụm liên hệ theo vai gửi | `screenshots/TC-DLV-026__verify-sau-ghep-co-cum-nguoi-giao-hang.png` |
| TC-DLV-027 | cụm liên hệ vai vận chuyển | `screenshots/TC-DLV-027__verify-cum-nguoi-gui-va-nguoi-nhan.png` |
| TC-DLV-028 | cụm liên hệ vai nhận | `screenshots/TC-DLV-028__verify-chi-cum-nguoi-giao-hang.png` |
| TC-DLV-029 | block LỊCH SỬ đủ 5 mốc | `screenshots/TC-DLV-029__verify-lich-su-du-5-moc.png` |
| TC-DLV-068 | mẫu câu nhật ký giao tận tay | `screenshots/TC-DLV-068__verify-mau-cau-giao-tan-tay.png` |

> 🔶 **6/13 TC PASS có khai sai lệch so với Steps** (`026` · `027` · `028` · `029` · `068` + setup của nhiều TC dùng đơn sẵn có thay vì tự dựng). Mọi sai lệch đều ghi **ngay trong section TC** của `vibe-log.md`, mở đầu bằng `🔶 KHAI SAI LỆCH SO VỚI STEPS`. ⛔ **Không TC nào được chấm PASS mà giấu sai lệch.**

## ⛔ N-A — 4 TC API-tier, cố ý không test qua UI

| TC ID | Lý do |
|---|---|
| **TC-DLV-074** *(P1)* | pre-condition đòi **proxy chặn & phát lại request**; phép thử là **giả mạo request bỏ qua UI** |
| **TC-DLV-075** *(P1)* | như trên |
| **TC-DLV-076** *(P1)* | như trên |
| **TC-DLV-078** *(P1)* | đòi proxy **sửa/xoá dòng nhật ký** rồi phát lại |

> ⚠️ **N-A ở đây KHÔNG có nghĩa "khỏi test"** — 4 TC này là **P1 về bảo mật/bất biến nhật ký**, chỉ là **sai tier**: phải chạy ở tầng **API/security test**, ⛔ không phải vibe-test. Đề nghị QC lead route sang tier phù hợp.

## 🔎 3 phát hiện cần BA/QC quyết (⛔ chưa tự chấm FAIL)

1. 🔴 **Người nhận MẤT cụm liên hệ khi đơn ở `Đang giao`.** Đo được ở `TC-DLV-009`: toàn màn chỉ có stepper + `LỘ TRÌNH` + bản đồ + nhãn khoá — **không** `NGƯỜI GIAO HÀNG`, **không** `ẢNH SẢN PHẨM`, **không** `THÔNG TIN HÀNG`. Đã loại trừ "ẩn dưới nếp gấp" bằng **4 phép cuộn khác nhau** + quét chuỗi page source. 🔴 **Ngược** với `repro/RP-ASN-lo-sdt-sau-ghep-2026-09-19` (ở `Đã ghép` **có** đủ cụm + SĐT) và ngược với chính `TC-DLV-028` (ở `Đã giao` **có** lại). ⇒ cụm liên hệ **biến mất đúng ở khoảng giữa** — giai đoạn người nhận **cần gọi shipper nhất**. **Chưa SC nào phủ** ⇒ route `/analyze-requirements --update`.
2. ⚠️ **Block `LỊCH SỬ` hiển thị MỚI→CŨ**, ngược thứ tự mà `TC-DLV-029` liệt kê. Nội dung và timestamp **đúng tuyệt đối** ⇒ đã chấm PASS, nhưng nếu BA muốn cũ→mới thì là lệch cần sửa app.
3. ⚠️ **Lệch thuật ngữ TC ↔ app:** TC gọi cụm là **"Người vận chuyển"**, app hiển thị **"NGƯỜI GIAO HÀNG"** (`TC-DLV-026`). Đề nghị chốt 1 thuật ngữ rồi đồng bộ cả TC lẫn app.

## ⚠️ Rủi ro đã nhận diện cho phiên sau: TC v1.0 CARRIED có thể đã LỖI THỜI so với app v1.1

`TC-DLV-018` (CARRIED v1.0) kỳ vọng nhấn `Đã giao cho người nhận` sẽ hiện **popup 2 nút** *"Bạn xác nhận đã giao hàng tận tay người nhận?"*.
Nhưng `TC-DLV-043`–`053` (v1.1) mô tả cùng nút đó mở **cả một màn "Xác nhận đã giao"** (chọn `Giao cho`, đính ảnh bắt buộc, link *"Không thể liên lạc cho người nhận?"*).
⇒ **Hai TC mô tả hai hành vi khác nhau cho cùng một nút.** Phiên này ⛔ **chưa kiểm được** (tap bị chặn) nên **không chấm** `018`.
🔴 **Cảnh báo cho phiên sau:** nếu app chạy theo v1.1 thì `TC-DLV-017`/`018`/`019` sẽ **FAIL do TC lỗi thời**, ⛔ **không phải lỗi app** — đừng log bug vội, hãy route về `review-tc`/`analyze-requirements`.

## Locator Coverage

| Màn đã harvest | Elements | ✅ Verified | 🚫 NOT FOUND |
|---|--:|--:|--:|
| 3 | **33** | **33** | 0 |

→ `implement-automation` bắt đầu được với **33 locator đã verify**, đã merge **33/33 = 100%** vào `locators/vibe-locators-latest.md`.
→ 🔑 Giá trị lớn nhất: **oracle "nhãn khoá vs nút thật"** (`clickable` + có/không `resource-id`) — dùng chung cho cả ma trận `TC-DLV-001..015`, thay cho việc đoán màu từ ảnh; và **4 bẫy mới `T-DLV-01..04`**.

## Recommendation

- **Automate now:** 13 TC — locator sẵn trong `vibe-locators-latest.md`
- **Fix app:** 1 bug component icon copy (`TC-DLV-080` + `081` + `TC-ORD-085`) → `/log-bug`
- **Route sang tier khác:** 4 TC P1 API/security (`074` `075` `076` `078`)
- **Chờ dev/QA hỗ trợ:** 4 TC (`040` `057` `067` cần lùi timestamp · `077` cần thiết bị 4G thật)
- **Route về analyze-requirements:** spec-gap "người nhận mất cụm liên hệ ở `Đang giao`"
- **CHẠY TIẾP 55 TC còn nợ:** `/vibe-test --module DLV` — ⚠️ **chỉ chạy được sau khi user gỡ blocker quyền** (xem §BLOCKER)
