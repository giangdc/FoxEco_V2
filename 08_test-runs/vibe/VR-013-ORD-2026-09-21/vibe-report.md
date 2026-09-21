# Vibe Test Report — VR-013 — module ORD — v1.1 (+ CARRIED v1.0) — 2026-09-21

> Platform: **mobile** (Appium MCP / UiAutomator2) · **2 thiết bị song song, 2 session:** `emulator-5554` (Giang = tài khoản A) + `R58T20PLP8K` Samsung A12s (Đặng Châu Anh = tài khoản B)
> Environment: STG · host app `com.hrisproject.stag` (FoxPro) → FoxEco
> Tập chạy: **QC chỉ định** — 22 TC còn nợ + `TC-ORD-004` (bug `BUG-020` chưa push) + `TC-ORD-068` (bug `BUG-019` chưa push). Không chạy lại TC đã có verdict cuối.

## Summary

## Scope Coverage ★★ (mẫu số = SCOPE_TOTAL của module, trạng thái SAU khi merge run này)

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module ORD)** | **88** | 100% |
| Chạy **trong run này** | **21** | 23,9% |
| ✅ PASS từ **run trước** (không chạy lại) | 40 | 45,5% |
| ❌ FAIL / 🚫 BLOCKED từ **run trước** (không chạy lại) | 24 *(21 FAIL + 3 BLOCKED)* | 27,3% |
| ⛔ N-A | 0 | 0% |
| ⏳ **NOT_RUN (còn nợ)** | **2** (`067` · `082`) | 2,3% |
| ⚠️ NOT_EVIDENCED (còn nợ) | **1** (`080`) | 1,1% |

**Còn nợ = 3 TC → §8 = PARTIAL.** *(trước phiên: nợ 22 → sau phiên: nợ 3)*

- Chi tiết từng TC **của module (xuyên run)**: `08_test-runs/vibe/coverage/coverage-ORD.md` ← xem cái này
- Chi tiết **run này làm gì**: `scope-ledger.md`

> ⚠️ Bảng trên là trạng thái **cả module sau merge**. Không cộng "chạy run này" + "PASS run trước" thành 1 con số.

## Kết quả các TC chạy trong run này (21 TC)

| Result | Count | % trên N_run |
|--------|-------|---|
| ✅ PASS | **20** *(gồm `073` · `088` do QC xác nhận app đúng)* | 95,2% |
| ❌ FAIL | **0** | 0% |
| 🚫 BLOCKED | **1** (`084`) | 4,8% |
| ⚠️ NOT_EVIDENCED | 0 *(+ `080` chạy dở, tính riêng ở bảng trên)* | — |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | **21/21** (100%) |
| File ảnh trong `screenshots/` | 53 *(+ ảnh thêm ở các bước sau — xem gate)* |
| TC thiếu evidence | `TC-ORD-080` (chạy dở — xem §Còn nợ) |
| Gate `.claude/hooks/verify_evidence.py` | xem cuối file §Gate |

> 🧾 Evidence bằng `adb exec-out screencap` (tiền lệ VR-004: `appium_screenshot` không có tham số `filename` và trả ~147k ký tự HTML/call). **Locator + mọi thao tác 100% qua MCP.** Riêng `TC-ORD-085` dùng **burst screencap** (không có ffmpeg/cv2 để tách khung video).

---

## 🐞 KẾT LUẬN CHO 2 BUG CHƯA PUSH JIRA (yêu cầu chính của QC)

### `BUG-020` — *"Đăng tin NEED trả API 400, app không báo gì"* (`TC-ORD-004`, P1) ⇒ **KHÔNG TÁI HIỆN → ⛔ đừng push**

| Biến | VR-004 (lỗi) | **VR-013 (đăng được)** | Kết luận |
|---|---|---|---|
| Tài khoản gửi | Giang | **Giang** (đăng xuất Thủy → đăng nhập lại, QC duyệt) | ✅ **loại** giả thuyết "khác tài khoản" |
| Payload | Tài liệu·Thấp·Nhẹ·Nhỏ + 1 ảnh, ghi chú `Giao gio hanh chinh`, 2 địa chỉ chạm gợi ý, khoảng 2 ngày, buổi Chiều | **y hệt** | ✅ loại giả thuyết "khác payload/ghi chú" |
| Giờ chạy | ~00:20 ngày 19/09 (theo logcat) | **10:14 ngày 21/09** | ⚠️ **biến duy nhất còn lại** |
| Kết quả | 3/3 lần `REQ_400` | đăng **thành công**; đơn `Chờ ghép`; logcat **0** dòng `REQ_400` | — |

⇒ Củng cố giả thuyết *"lệch ngày quanh nửa đêm"* nhưng **chưa xác nhận**. Mọi TC khác đăng NEED ở phiên này (`038` `065` + đơn của `004`) đều thành công. **Khuyến nghị:** giữ draft, **không push**; nếu muốn chốt: chạy đúng payload đó trong khung **00:00–07:00 giờ VN** (cần chỉnh giờ emulator hoặc chạy ban đêm). Nếu QC quyết định *"chỉ là lỗi tạm thời"* ⇒ đóng draft.

### `BUG-019` — *"Ảnh ~5MB bị từ chối im lặng"* (`TC-ORD-068`, P3) ⇒ **KHÔNG TÁI HIỆN → ⛔ đừng push**

Đo bằng 3 file có **dung lượng byte chính xác**, nhận diện trong Photo Picker bằng timestamp `content-desc`:

| File | Dung lượng | Kết quả | Thông báo |
|---|---|---|---|
| `F2` | **5.242.880 B (đúng 5 MiB)** | ✅ **nhận** (`0/5→1/5`) | — |
| `F4` | 5.600.000 B (≈5,6MB) | ❌ từ chối, bộ đếm giữ nguyên | ✅ **CÓ** `Ảnh vượt quá 5MB, vui lòng chọn ảnh nhỏ hơn.` |
| `F3` | 6.291.456 B (6 MiB) | ❌ từ chối | ✅ **CÓ**, cùng chuỗi |

⇒ Ngưỡng là **`> 5 MiB`**. Thông báo **CÓ ở mọi ca vượt ngưỡng** — nhưng **nằm dưới khối ảnh, bị thanh nút cố định che ở viewport mặc định** (phải cuộn 1 nhịp). Quan sát *"không có thông báo"* trong draft rất có thể do **không cuộn**. *(Điểm UX thật: người dùng cũng có thể không thấy lỗi — nhưng đó không phải "từ chối im lặng".)*

---

## 🆕 Phát hiện trong phiên (2 ứng viên bug đầu **đã huỷ** — QC xác nhận app đúng 2026-09-21)

| # | TC | Nội dung | Mức | Căn cứ |
|--:|---|---|---|---|
| 1 | `TC-ORD-088` ✅ *(đã huỷ `BUG-023` — app đúng, TC sửa theo app)* | **Form sửa tin cho XOÁ ảnh của tin đã đăng**, và việc xoá **được lưu** (5→4 ảnh; máy thật thấy `1/4`). Trái `BR18-05` *"ảnh đã gắn mốc nhật ký thì không xoá được"* | **P3 / Medium** | `TC-ORD-088__step5-FAIL-*` (2 ảnh) · cùng họ `BR11-03` (`SC-CNL-010`) và `NFR-07` (`SC-DLV-062`) ⇒ nên gộp 1 bug |
| 2 | `TC-ORD-073` ✅ *(đã huỷ `BUG-024` — app đúng, TC sửa theo app)* | **Lightbox ảnh KHÔNG đóng khi chạm nền tối** (6 điểm chạm trên emulator + 1 trên máy thật; tap toạ độ nút × đóng được nên phương pháp hợp lệ). Trái `BR18-03` *"…có nút đóng và chạm nền để đóng"* | **P3 / Low** | `TC-ORD-073__step6-FAIL-*` |
| 3 | `TC-ORD-083` (quan sát) | Lỗi `Địa chỉ giao phải khác địa chỉ lấy hàng` **vẫn hiện** sau khi đổi ô giao sang địa chỉ khác **và** chuyển focus sang ô khác (blur thật) — chỉ mất sau khi `Tiếp theo` thành công | Thấp, **chưa kết luận** | QC đối chiếu `VAL-02` có bắt buộc xoá lỗi lúc blur không |

## ✅ Xác nhận NGƯỢC với các nghi vấn cũ
- **`TC-ORD-085` (B8 "icon copy không đổi màu") — KHÔNG phải bug.** Burst 26 khung: chip xanh `✓ Đã copy` hiện **~1,6–2,1 s** rồi về icon xám; clipboard = đúng nguyên văn. Bài học: 2 ảnh `adb screencap` rời cách nhau ~1,8 s **dễ hụt cửa sổ**. ⚠️ **`TC-DLV-080/081`** (VR-012, *"icon copy không đổi màu"*) nhiều khả năng **cùng âm tính giả** — nên chạy lại bằng burst trước khi mở bug.
- **`TC-ORD-004`** đăng được (xem trên). **`TC-ORD-038/039/040/041/049/065`** — cả nhóm "chặn bởi bug `TC-ORD-004`" nay **gỡ chặn**.

## 📨 Việc cho QC — TC cần sửa (⛔ AI không tự sửa Expected; cho phép sửa Steps/Test Data theo `Project_rule §10.5`)

| TC | Vấn đề | Đề nghị |
|---|---|---|
| `046` | Test Data `Số 9 Duy Tân` **không có trong danh mục gợi ý** ⇒ nút `Tiếp theo` khoá (T11) | đổi sang địa chỉ có gợi ý (đã chạy bằng `FPT Cầu Giấy`) |
| `083` | Test Data `Số 7 ngõ 12 Trần Duy Hưng` **không chạm gợi ý được** ⇒ nút khoá, không lỗi | đổi sang địa chỉ có gợi ý; verdict PASS dựa trên đường *chạm gợi ý* |
| `084` | **Không dựng được điều kiện**: thêm khoảng trắng vào ô đã chọn gợi ý ⇒ mất trạng thái "đã chọn" ⇒ nút khoá | 🚫 BLOCKED; QC quyết `DESCOPED` hoặc viết lại |
| `044` | Steps nhắc *"hai tab con"* + *"ô tìm kiếm"* của Bảng tin — **v1.1 không có** (1 danh sách duy nhất) | sửa Steps |
| `060` | Có **popup xác nhận** huỷ sửa (`Thay đổi chưa lưu sẽ bị mất…`) mà TC không mô tả | bổ sung step |
| `080` | Step 5 nhắm màn **chủ tin** — màn đó **không hiển thị** khối uỷ quyền; theo `AC-05.1.01` nhãn `Người gửi chỉ định` hiện cho **người vận chuyển** | sửa step 5 sang màn giao hàng của carrier |
| `082` | Cùng vấn đề `080` — kiểm phía chủ tin là **vô nghĩa** (không bao giờ thấy dữ liệu uỷ quyền) | sửa như `080` |
| `004`, `038`… | chip `Giấy tờ, hồ sơ` (nay `Tài liệu`); TC v1.0 thiếu 3 trường bắt buộc mới (trọng lượng/kích thước/ảnh) | cập nhật câu chữ |
| `061` | `Đến ngày` của tin đã ghép **không hiện trên màn** | seed 1 tin đã ghép có `Đến ngày` = hôm qua để có bằng chứng on-screen |

## Còn nợ — 3 TC (§8 = PARTIAL)

| TC | Lý do | Cần gì để chạy |
|---|---|---|
| `TC-ORD-067` ⏳ | **Chưa kịp** (hết sức phiên) — không còn bị chặn bởi bug | 1 lần đăng NEED chip `Lớn · > 20×20 cm` (~30 call) |
| `TC-ORD-080` ⚠️ | Đã chạy 4/5 step, **thiếu màn chứng minh** | **tài khoản thứ 3 làm carrier** (`stag_taipm@`/`stag_anhptm17@`) ghép đơn `P3` rồi xem màn giao hàng. ⚠️ ghép không đảo ngược |
| `TC-ORD-082` ⏳ | Chưa chạy — kiểm phía chủ tin là vô nghĩa | như `080`, thêm 1 đơn uỷ quyền **rồi xoá khối** |

▶️ **Chạy tiếp:** `/vibe-test --module ORD` *(bộ lọc pending tự bốc đúng 3 TC)* hoặc `/vibe-test --tc TC-ORD-067,TC-ORD-080,TC-ORD-082`.

## Dữ liệu phát sinh trên STG / máy test (⛔ đừng seed lại)

| Loại | Nội dung |
|---|---|
| **NEED ×3** của Giang (`Chờ ghép`) | `P1` `FTEL Đà Nẵng Cẩm Lệ → FPT Cầu Giấy` (đã sửa địa chỉ giao ở `TC-046`) · `P2` `Thuốc/Y tế` cùng tuyến `→ Tòa V-City` · `P3` `Trên 10 kg` + **uỷ quyền `Nguyễn Văn Bảy/0912345678`**, nay còn **4 ảnh** (đã xoá 1 ảnh ở `TC-088`). Người nhận cả 3 = `Đặng Châu Anh`. **Hiện trên Bảng tin công khai** — cân nhắc huỷ nếu không cần |
| **OFFER ×1** của Giang | `363 Nguyễn Hữu Thọ, Cẩm Lệ → Tòa V-City` · `Giờ nào cũng được` (11:28) |
| **Emulator** | +4 ảnh `vr013_f1..f4_*.jpg` ở `/sdcard/Pictures/` (4,8MB · **đúng 5 MiB** · 6 MiB · 5,6MB) — dùng lại cho `TC-ORD-068/069` |
| **Đổi tài khoản** | Emulator: `Nguyễn Thị Thanh Thủy` → **`Đặng Châu Giang`** (QC duyệt 10:05). Máy thật giữ `Đặng Châu Anh` |

## 🪤 Ghi nhận kỹ thuật
- `~/.foxeco-v2/credentials.env` **không có biến `FOXECO_STG_OTP`** như `CLAUDE.md`/`USR-accounts.md` khai; mã dùng chung nằm ở **`FOXECO_STG_PASS`** (đối chiếu `00_input/v1.1/datatest`). → nên sửa 1 trong 2.
- SĐT người gửi của Giang nay `0912345670` (VR-004 ghi `0964633310`) — HRIS đã đổi.
- Emulator đổi độ phân giải (1080×2400, VR-004: 720×1280) và **bộ ảnh seed đổi tên** (`seed_jpg_*.jpg`, không còn `seed-ord-*`).
- `appium_get_page_source` trả **inline** khi cây nhỏ (màn thành công/lightbox ~18k ký tự → tốn context), chỉ ghi ra file khi cây lớn. Dùng `find_element` cho màn nhỏ.
- **Hai session Appium chạy song song hoạt động tốt** (`sessionId` truyền vào từng call) — cho phép kiểm 2 tài khoản không cần đăng xuất (`TC-044/045/048`).

## Locator Coverage

| Pages visited | Elements captured | Verified ✅ | Not found 🚫 |
|--------------|------------------|------------|-------------|
| 14 màn | xem `vibe-locators.md` | mọi entry đều qua MCP trong run này | 6 (nêu trong file) |

## Gate
Chạy `python3 .claude/hooks/verify_evidence.py 08_test-runs/vibe/VR-013-ORD-2026-09-21` — xem kết quả cuối phiên ở `mcp-session-log.md §Gate`.
