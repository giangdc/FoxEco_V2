# Vibe Test Report — VR-007 — v1.1 (+ CARRIED v1.0) — 2026-09-19

> Platform: **mobile (Appium MCP / UiAutomator2)** · Device `emulator-5554` · Session `55129e7d…`
> Environment: **STG** — app `com.hrisproject.stag` (host FoxPro → FoxEco)
> Module: **ASN** (Ghép nối) · SCOPE_TOTAL: **26 TC**
> Tài khoản: **`stag_taipm@`** (Phan Minh Tài) → **`stag_anhdc4@`** (Đặng Châu Anh) — **AI tự đổi**

## Scope Coverage ★★

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module ASN)** | **26** | 100% |
| Chạy **trong run này** | **3** | 12% |
| ✅ PASS từ **run trước** | 0 | 0% |
| ⛔ N-A (cố ý không test qua UI, có lý do) | 2 | 8% |
| ⏳ **NOT_RUN (còn nợ)** | **21** | **81%** |
| ⚠️ NOT_EVIDENCED (còn nợ) | 0 | 0% |

**Có verdict cuối: 5/26 · Còn nợ = 21 TC → §8 = PARTIAL.**

- Chi tiết từng TC (xuyên run): `08_test-runs/vibe/coverage/coverage-ASN.md` ← **xem cái này**
- Chi tiết run này: `scope-ledger.md`

> ⚠️ **Run ID nhảy VR-005 → VR-007.** `VR-006` đã cấp rồi **rút lại** (phiên 0-verdict, đã xoá, chuyển thành `repro/`); luật *"never reuse"* ⇒ ⛔ không tái dùng số 006.

## 🟢 Phiên ĐẦU TIÊN của ASN thu được verdict — và lý do

Lượt ASN trước (cùng ngày, 07:58) khai **0/26 chạy được**, viện 2 lý do. **Cả hai đã bị bác bỏ trong ngày:**

| Lý do khai lúc 07:58 | Thực tế |
|---|---|
| bug `B1` chặn đăng tin NEED | ✅ **đăng được** cả NEED lẫn OFFER — `repro/RP-ORD-B1-dang-tin-duoc-lai-2026-09-19/` |
| OTP nhập tay ⇒ AI không đổi được tài khoản | ✅ **OTP staging CỐ ĐỊNH** ⇒ AI **tự logout/login**; phiên này đổi **2 lượt** |

🔑 **Gốc rễ của sai lầm cũ:** thừa kế kết luận của phiên khác làm tiền đề mà **không tự kiểm lại trong phiên** — đúng điều `SKILL.md` cấm. QC chất vấn *"tự tạo tin rồi logout đổi account được mà?"* mới lộ ra.

## Kết quả các TC chạy trong run này

| Result | Count | % trên 3 |
|--------|-------|---|
| ✅ PASS | **3** | 100% |
| ❌ FAIL | 0 | 0% |
| 🚫 BLOCKED | 0 | 0% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

| TC | P | Tên | Điểm đáng chú ý |
|---|---|---|---|
| **TC-ASN-013** | **P1** | Không gợi ý khớp tuyến cho tin của chính mình | tin NEED trùng **tuyệt đối** tuyến+ngày+buổi với OFFER của chính mình ⇒ điều kiện dễ sinh thông báo nhất, app **vẫn loại trừ đúng** |
| **TC-ASN-023** | P2 | Có thông báo khớp tuyến ≤60s khi khớp đủ điều kiện | thông báo trỏ **đúng** tin vừa đăng; độ trễ đo được **(5s, 65s]** |
| **TC-ASN-021** | P3 | 2 tin NEED liên tiếp là 2 tin độc lập | đúng 2 tin, 2 tuyến, ⛔ không ghi đè |

### 🟢 Đối chứng chéo mạnh giữa 013 và 023

Cùng cơ chế khớp tuyến, **cùng tuyến `Tòa V-City → FPT Cầu Giấy` buổi Sáng**:

| Ai | Vai với tin NEED | Nhận thông báo? |
|---|---|---|
| Phan Minh Tài | **chủ tin** (`TC-ASN-013`) | ❌ **KHÔNG** — đúng `BR03-06` |
| Đặng Châu Anh | chủ OFFER, **không phải** chủ tin (`TC-ASN-023`) | ✅ **CÓ** |

⇒ Chứng minh app **loại trừ theo chủ sở hữu**, ⛔ không phải *"không gửi thông báo gì cả"*. Một TC đơn lẻ không kết luận được điều này.

## ⚠️ Điểm cần QC lưu ý ở TC-ASN-023 (chạm biên NFR)

```
Đăng NEED      : 09:42:54
Quan sát chuông: 09:46:59   → nhãn "3 phút trước"
⇒ độ trễ thực ∈ (5 giây , 65 giây]
```

Cận trên **65s vượt ngưỡng 60s đúng 5 giây** — do **làm tròn nhãn thời gian (độ phân giải 1 phút)**, ⛔ không phải quan sát thấy app chậm. Chỉ có **1 thiết bị** nên không thể *"nhấn chuông theo chu kỳ trong 60s"* như Steps mô tả.
Verdict **PASS** vì: thông báo **đã có sẵn** ngay lần xem đầu, khoảng đo nằm gọn trong spec trừ phần làm tròn, và chính fragment ghi *"⚠️ Đo bằng tay có sai số; ưu tiên automation"*.
🔁 **Đề nghị đo lại chốt `NFR-04` bằng 2 thiết bị** (máy B mở sẵn Thông báo, máy A đăng tin).

## 📨 2 đề nghị sửa tài liệu

| # | Vấn đề | Đề nghị |
|---|---|---|
| 1 | `TC-ASN-021` Steps ghi loại hàng **`"Giấy tờ, hồ sơ"`** — nhãn **không tồn tại** trên app (`C-ORD-09` chốt là **`Tài liệu`**) | sửa câu chữ Steps |
| 2 | `TC-ASN-v1.1.md §0` ghi QA-obs buổi **`"Sáng (6–12h)"`**; app thật là **`Sáng (8–12h)`** | sửa fragment — chính fragment dặn *"verify lại khi vibe-test"* |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | **3/3 (100%)** |
| File ảnh trong `screenshots/` | 8 (7 ảnh TC + 1 `_setup__`) |
| TC thiếu evidence | — không có |
| Gate `.claude/hooks/verify_evidence.py` | ✅ **0 vi phạm** — `Evidence 3/3 · Trích dẫn 3/3` |

## Locator Coverage

| Màn đã harvest | Elements | ✅ Verified | ⚠️ Inferred | 🚫 NOT FOUND |
|---|--:|--:|--:|--:|
| **7** | **34** | **26** | **8** | 0* |

\* 2 lần NOT FOUND là **chủ ý** (chứng cứ âm cho `TC-ASN-013`).

🔑 **Đóng góp lớn nhất: màn đăng nhập FoxPro lần đầu được harvest** — mở khoá nhóm TC đa-tài-khoản của **mọi module**, không riêng ASN. Luồng 5 bước tái sử dụng ở `USR-accounts.md §0b`.

## Recommendation

- **21 TC còn nợ nay là NỢ CÔNG SỨC**, ⛔ không còn là nợ môi trường:

| Nhóm | TC | Trạng thái |
|---|---|---|
| Luồng carrier | `001` `002` `003` `004` `005` `007` `010` `020` | ✅ **chạy được ngay** — Bảng tin đang có 3 tin sống |
| Trần & thứ tự gợi ý | `014` `015` `016` `017` `018` `025` | ✅ chạy được, tốn công seed |
| Nhánh âm khớp tuyến | `009` `011` `012` `022` | ✅ chạy được |
| 🔴 Cần thiết bị 2/3 | `006` · `008` | ⛔ **còn chặn thật** |
| 🔴 Cần dev lùi ngày | `019` | ⛔ còn chặn thật |
| ⛔ N-A | `024` `026` | giao automation/backend/security |

- **CHẠY TIẾP:** `/vibe-test --module ASN` — pending tự bốc đúng 21 TC
- ⚠️ **`stag_taipm@` = `FOXECO_STG_USER_C`** ⇒ chạy `TC-USR-040/043` **trước** khi làm bẩn hồ sơ tài khoản này

> 🛑 **Dừng vì HẾT SỨC PHIÊN**, ⛔ không phải hết TC chạy được — 18/21 TC còn nợ có đủ tiền đề ngay bây giờ.

## 🗂️ Dữ liệu phát sinh trên STG (phiên này tạo)

| Loại | Chủ | Tuyến | Buổi |
|---|---|---|---|
| OFFER | Phan Minh Tài | `FPT Tân Thuận 1` → `FTEL SG08 Quận 12` | Chiều |
| NEED | Phan Minh Tài | `FPT Tân Thuận 1` → `FTEL SG08 Quận 12` | Chiều |
| NEED | Phan Minh Tài | `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` | Sáng |

Cộng 2 tin của Đặng Châu Anh tạo lúc 08:26–08:38 ⇒ **5 tin sống**. ⛔ Lô sau **đừng seed lại**.

## Gate

```
⚠️  RUN CHƯA HOÀN TẤT (không vi phạm, nhưng còn TC nợ) — VR-007-ASN-2026-09-19
   Evidence:  3/3 TC đã chạy · 3 TC có section trong log · 8 file ảnh
   Trích dẫn: 3/3 TC có ảnh THẬT được trích đúng trong section của mình (rule 1)
   Coverage:  5/26 TC có verdict cuối · còn nợ 21
```
✅ **0 vi phạm evidence/trích dẫn.** Mục duy nhất còn đỏ là **nợ coverage** — đúng luật ⇒ §8 = **PARTIAL**, ⛔ không phải lỗi.
