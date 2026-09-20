# Vibe Test Report — VR-009 — v1.1 — 2026-09-19

> Platform: **mobile** (Appium MCP · UiAutomator2) · Device `emulator-5554` (AVD `qa_a33`)
> Environment: **STG** · app `com.hrisproject.stag` (host FoxPro_Stag · FoxEco = SDK nhúng)
> Module: **ASN** (Ghép nối) · Phiên: 14:47 → 15:46 · Tài khoản: `stag_anhdc4@` ↔ `stag_giangdc2@` (3 lượt đổi)

## Scope Coverage ★★

> Mẫu số LUÔN là **SCOPE_TOTAL của module ASN = 26**, ⛔ không phải số TC chạy phiên này.
> Bảng này là trạng thái **của cả module sau khi merge VR-009**.

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module ASN)** | **26** | 100% |
| Chạy **trong run này** | 7 | 27% |
| ✅ PASS từ **run trước** (VR-007/VR-008, không chạy lại theo lựa chọn QC) | 8 | 31% |
| ⛔ N-A (cố ý không test qua UI, có lý do) | 2 | 8% |
| ⏳ **NOT_RUN (còn nợ)** | **9** | **35%** |
| ⚠️ NOT_EVIDENCED (còn nợ) | 0 | 0% |

**Còn nợ = 9 TC → §8 = PARTIAL.**

- Chi tiết từng TC **của module (xuyên run)**: `08_test-runs/vibe/coverage/coverage-ASN.md` ← **xem cái này**
- Chi tiết **run này làm gì**: `scope-ledger.md` trong run folder

## Kết quả các TC chạy trong run này

| Result | Count | % trên 7 |
|--------|-------|---|
| ✅ PASS | **7** | 100% |
| ❌ FAIL | 0 | 0% |
| 🚫 BLOCKED | 0 | 0% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

| Lô | TC | Tài khoản | Ghi chú |
|---|---|---|---|
| **1** | `005` · `007` · `020` | `stag_giangdc2@` (D) | ⛔ không cần seed — tái dùng đơn `Đã ghép` của VR-008. `020` chốt nốt chặng step 6–9 ⇒ **verdict cuối** |
| **2** | `010` · `011` · `012` · `022` | D (OFFER) + B (4 NEED) | seed lại `OFFER-C1` + `N1..N4` trên khung **Chiều (13–17h) CÒN MỞ** |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | **7/7 (100%)** |
| File ảnh trong `screenshots/` | 39 (7 TC × `__verify`/`__pre` + `_setup__*` + `_recon__*`) |
| TC thiếu evidence (⚠️ NOT_EVIDENCED) | **không có** |
| Gate `verify_evidence.py` | xem mục *Gate* cuối báo cáo |

→ QC lead verify lại từng case bằng `screenshots/TC-ASN-<ID>__verify*.png` (mỗi TC ≥1 file RIÊNG).
→ ⚠️ 3 ảnh `__verify` của `011`/`012`/`022` là **3 lần quan sát độc lập** (md5 khác nhau), ⛔ không phải 1 ảnh nhân 3 tên.

## Locator Coverage

| Màn đã harvest | Elements ghi nhận | ✅ Verified | ⚠️ Inferred | 🚫 NOT FOUND (chủ ý) |
|---|--:|--:|--:|--:|
| 9 | 28 | 22 | 3 | 3 |

- **Tổng snapshot: 1** / **9 màn** ⇒ tuân thủ luật **B1/B2** (`SKILL.md §CONTEXT BUDGET`); toàn bộ locator còn lại lấy từ cache `locators/vibe-locators-latest.md`.
- Đã **merge 28/28 = 100%** vào `08_test-runs/vibe/locators/vibe-locators-latest.md` (đã kiểm khớp nguyên văn từng selector).

## Failed TCs

*(không có)*

## Blocked TCs

*(không có)*

## Passed TCs — sẵn sàng implement automation

| TC ID | Steps | Evidence file |
|-------|-------|---------------|
| TC-ASN-005 | 5 | `screenshots/TC-ASN-005__verify-bangtin-khong-co-tin-da-ghep.png` + `…__verify-hoatdong-khong-co-don-cap-ghep.png` |
| TC-ASN-007 | 5 | `screenshots/TC-ASN-007__verify-bangtin-vang-tin-da-ghep.png` + `…__verify-chuong-khong-co-goi-y.png` |
| TC-ASN-010 | 5 | `screenshots/TC-ASN-010__verify-theo-doi-don-va-sdt-nguoi-gui.png` |
| TC-ASN-011 | 4 | `screenshots/TC-ASN-011__verify-chuong-khong-co-tb-cho-seed-lech-diem-giao.png` |
| TC-ASN-012 | 4 | `screenshots/TC-ASN-012__verify-chuong-khong-co-tb-cho-seed-lech-ngay.png` |
| TC-ASN-020 | 9 | `screenshots/TC-ASN-020__verify-carrier-thu-3-ghep-duoc.png` + `…__verify-vai-carrier-tren-hoat-dong.png` |
| TC-ASN-022 | 2 | `screenshots/TC-ASN-022__verify-chuong-khong-co-tb-cho-seed-lech-buoi.png` |

## 🔴 Phát hiện cần QC/BA xử lý

| # | Phát hiện | Mức | Đề xuất |
|---|---|---|---|
| 1 | **`TC-ASN-010` Steps ghi nút `"Nhận giao"` — nút này KHÔNG tồn tại.** CTA thật = `Tôi mang giúp được` (find phủ định 🚫 NOT FOUND) | sửa tài liệu | Sửa Steps `TC-ASN-010`. ⛔ Không phải bug app — nghiệp vụ đúng hoàn toàn ⇒ TC vẫn PASS |
| 2 | **Thông báo khớp tuyến biến mất hàng loạt khi khung giờ trôi qua** *(giả thuyết, chưa chốt)* — 14:49 mất cả 3 thông báo của khung `Sáng`, `force-stop`+relaunch vẫn mất | ⚠️ cần BA xác nhận **đúng thiết kế hay lỗi** | Nếu **đúng thiết kế** ⇒ bổ sung vào scenario_map (hiện ⛔ **không có** SC nào mô tả vòng đời/hết hiệu lực của thông báo gợi ý) ⇒ route `/analyze-requirements --update`. Nếu **không** ⇒ raise bug |
| 3 | **Autofill SĐT người nhận đúng/sai tuỳ tài khoản** — `stag_huyennhk@` autofill ĐÚNG `0989014863`; VR-008 ghi `stag_thuyntt22@` autofill ra **MNV** rồi app báo *"SĐT không hợp lệ"* | bổ sung bug | `BUG-008` **không phải lỗi toàn cục** mà phụ thuộc HRIS có SĐT hay không ⇒ cập nhật mô tả + điều kiện tái hiện của `BUG-008` |
| 4 | **Nhãn buổi thật `Sáng (8–12h)`** trong khi `TC-ASN-v1.1.md §0` ghi *"Sáng (6–12h)"* | sửa tài liệu | **Lần thứ 3** được xác nhận (VR-007, VR-008, VR-009) ⇒ sửa fragment |
| 5 | **`TC-ASN-012` mô tả khung giờ dạng `08:00–09:00` vs `20:00–21:00`** nhưng app dùng **khoảng NGÀY + tập BUỔI**, ⛔ không nhập giờ tự do | sửa tài liệu | Sửa Steps/Test Data cho khớp mô hình thật của app |
| 6 | **`OTP` có thể trả *"Không thể kết nối mạng!"* giả** ở lần bấm đầu dù mạng OK | lưu ý vận hành | Ghi bẫy `T-ASN-07` — retry 1 lần trước khi kết luận |

## NOT_RUN — 9 TC còn nợ (khai đầy đủ)

| TC | Lý do | Gỡ bằng cách nào |
|---|---|---|
| `014` `015` `016` `017` `018` `025` | **Hết sức phiên** — nhóm trần/thứ tự cần **tuyến OFFER MỚI sạch + 3–6 tin NEED + 3 lượt đổi tài khoản** (~50–60 phút); khung `Chiều` đóng **17:00**, dừng lúc **15:46** ⇒ ⛔ không đủ để chạy TRỌN VẸN | Phiên mới, bắt đầu **đầu khung giờ** (vd 13:05 hoặc 08:05). Xem *Khuyến nghị* bên dưới |
| `006` (2 thiết bị, bấm cách <2s) · `008` (3 thiết bị, đo ≤5s) | Máy chỉ có **1 AVD `qa_a33`**. **QC chốt trong phiên này: giữ `NOT_RUN`**, ⛔ không đầu tư nhân bản AVD | Cần 2–3 emulator/thiết bị thật, hoặc chuyển tier automation |
| `019` | Cần tin NEED trạng thái **Hết hạn** — ⛔ không tạo được qua UI | Nhờ dev/QA lùi `Đến ngày` trong DB |

## Recommendation

- **Automate now:** 7 TC của phiên này + 8 TC các phiên trước — locator đã sẵn trong `locators/vibe-locators-latest.md`
- **Fix tài liệu trước:** `TC-ASN-010` (nhãn `Nhận giao`) · `TC-ASN-012` (mô hình khung giờ) · fragment §0 (nhãn buổi)
- **Chờ BA xác nhận:** vòng đời/hết hiệu lực của thông báo gợi ý (phát hiện #2) → `/analyze-requirements --update`
- **CHẠY TIẾP phần còn nợ:** `/vibe-test --module asn` ← bộ lọc pending tự bốc đúng 9 TC

### 🧭 Khuyến nghị thiết kế cho phiên sau (nhóm trần `014/015/016/017/025`)

```
1. Bắt đầu phiên ở ĐẦU một khung giờ (13:05 cho "Chiều", 08:05 cho "Sáng")
   → có ~4 tiếng trước khi thông báo có nguy cơ hết hiệu lực (phát hiện #2).
2. Seed TUYẾN OFFER MỚI, SẠCH — ⛔ KHÔNG tái dùng `OFFER-C1`:
   nó đã dính 1 thông báo của tin N1 (đã ghép), mà **tin đã ghép VẪN chiếm slot**
   trong danh sách thông báo (quan sát 15:46) ⇒ số đếm sẽ nhiễm bẩn.
3. Đếm bằng kỹ thuật RẺ đã kiểm chứng ở phiên này — ⛔ không cần dump page source:
   dò `textContains("Tìm thấy đơn hàng phù hợp tuyến của bạn — xem chi tiết").instance(k)`
   với k = 0,1,2,… tới khi NOT_FOUND ⇒ số thông báo = k.
4. Thứ tự chạy tiết kiệm nhất (1 chuỗi seed phục vụ 4 TC):
   3 NEED → đếm (TC-015) → +2 NEED → đếm (TC-016) → +1 NEED → đếm lại (TC-017 + TC-014).
   Mỗi lần "đếm" = 1 lượt đổi tài khoản sang chủ OFFER ⇒ gom đúng 3 lượt.
5. LUÔN giữ 1 tin khớp ĐỦ làm **chứng cứ dương đối chứng** — nếu không, mọi kết luận âm
   đều vô nghĩa (đúng cái bẫy suýt mắc lúc 14:49).
6. Dùng `stag_huyennhk@` làm người nhận để ⛔ không vướng bug autofill SĐT (T-ASN-08).
```

## Gate

```bash
python3 .claude/hooks/verify_evidence.py 08_test-runs/vibe/VR-009-ASN-2026-09-19 \
  || python3 ~/.claude/skills/vibe-test/scripts/verify_evidence.py 08_test-runs/vibe/VR-009-ASN-2026-09-19
```
Kết quả: **exit 1 — đúng như mong đợi**, vì `coverage-ASN.md` còn **9 TC `⏳ NOT_RUN`** (nhóm B của Step 6.5: *"CÒN NỢ COVERAGE — KHÔNG phải lỗi cần sửa"*).
⇒ **§8 = PARTIAL**, ⛔ không được ghi COMPLETED. Phần **evidence 7/7 sạch** (0 NOT_EVIDENCED · 0 DANGLING · 0 UNCITED).
