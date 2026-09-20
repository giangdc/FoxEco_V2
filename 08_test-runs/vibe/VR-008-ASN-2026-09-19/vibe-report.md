# Vibe Test Report — VR-008 — v1.1 — 2026-09-19

> Platform: **mobile** (Appium MCP / UiAutomator2) · Device `emulator-5554` · Session `482f2d33`
> Environment: app `com.hrisproject.stag` (host **FoxPro_Stag**, FoxEco là SDK nhúng) — **STG**
> Module: **ASN (Ghép nối)** · Thời gian: **11:32 → 12:33** (~1 giờ)
> ⏸️ **Phiên DỪNG GIỮA CHỪNG theo yêu cầu QC** ("dừng và lưu lại data giúp t nhé, mai tiếp") — ⛔ **KHÔNG phải đã chạy xong module.**

## Scope Coverage ★★

> Mẫu số là **SCOPE_TOTAL của module ASN**, không phải số TC chạy phiên này.
> Bảng này là trạng thái **của cả module sau khi merge VR-008** (nguồn: `coverage/coverage-ASN.md`).

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module ASN)** | **26** | 100% |
| Chạy **trong run này** (VR-008) | 5 | 19% |
| ✅ PASS từ **run trước** (VR-007, không chạy lại theo lựa chọn QC) | 3 | 12% |
| ⛔ N-A (cố ý không test qua UI, có lý do) | 2 | 8% |
| ⏳ **NOT_RUN (còn nợ)** | **16** | **62%** |
| ⚠️ NOT_EVIDENCED (còn nợ) | 0 | 0% |

**Còn nợ = 16 TC → §8 = PARTIAL.**

- Chi tiết từng TC **của module (xuyên run)**: `08_test-runs/vibe/coverage/coverage-ASN.md` ← **xem cái này**
- Chi tiết **run này làm gì**: `scope-ledger.md` trong run folder

## Kết quả các TC chạy trong run này

| Result | Count | % trên 5 |
|--------|-------|---|
| ✅ PASS | **5** | 100% |
| ❌ FAIL | 0 | 0% |
| 🚫 BLOCKED | 0 | 0% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

## Evidence Coverage ★

| Chỉ số | Giá trị |
|--------|---------|
| TC có evidence / tổng TC đã chạy | **5/5 (100%)** |
| File ảnh trong `screenshots/` | 19 |
| TC thiếu evidence (⚠️ NOT_EVIDENCED) | — (không có) |
| Gate `verify_evidence.py` | xem §Gate cuối file |

## Passed TCs — sẵn sàng implement automation

| TC ID | Steps | Evidence file |
|-------|-------|---------------|
| TC-ASN-001 (P1) | 6 | `screenshots/TC-ASN-001__verify-card-da-ghep.png` |
| TC-ASN-002 (P2) | 4 | `screenshots/TC-ASN-002__verify-huy-giu-cho-ghep.png` |
| TC-ASN-003 (P1) | 5 | `screenshots/TC-ASN-003__verify-khong-co-nut-duyet.png` |
| TC-ASN-004 (P1) | 5 *(2 tài khoản)* | `screenshots/TC-ASN-004__verify-a-thay-sdt-b.png` |
| TC-ASN-009 (P2) | 5 *(2 tài khoản)* | `screenshots/TC-ASN-009__verify-tro-dung-tin-seed-s1.png` |

> 🟢 **3/5 là P1.** Nhóm nghiệp vụ cốt lõi của module (ghép đơn · không có bước duyệt · lộ SĐT đúng lúc) **đã được kiểm chứng thật**.

## Failed / Blocked TCs

**Không có.** ⛔ Phiên này không ghi nhận FAIL hay BLOCKED nào.

## Locator Coverage

| Màn đã harvest | Elements | ✅ Verified | ⚠️ Inferred | 🚫 NOT FOUND (chủ ý) |
|---|--:|--:|--:|--:|
| 7 | 34 | 25 | 5 | 4 |

→ Đã merge **34/34 (100%)** vào `08_test-runs/vibe/locators/vibe-locators-latest.md` (đã kiểm khớp nguyên văn chuỗi selector).
→ 🪤 Kèm **6 bẫy mới `T-ASN-01..06`** — 2 bẫy đã thực sự chặn phiên này, `implement-automation` **phải đọc trước khi code**.

## 🔎 Phát hiện cần QC/BA xem (⛔ chưa mở bug trong phiên này)

| # | Phát hiện | Bằng chứng | Đề xuất |
|---|---|---|---|
| 1 | **Ảnh quá khổ (5 MB) bị từ chối IM LẶNG** ở wizard đăng tin — không thông báo lỗi, bộ đếm giữ `0/5`, nút `Tiếp theo` không phản hồi, người dùng ⛔ không hiểu vì sao | `vibe-log.md §SEED lô 2` + logcat `MediaProvider: ... seed-ord-oversize-5mb.jpg` | Thuộc **module ORD** (wizard đăng tin), ⛔ không thuộc TC ASN nào ⇒ QC mở bug riêng cho ORD |
| 2 | **Màn Thông báo không tự làm mới** — 11:44 danh sách thiếu cả thông báo 09:43 (chỉ có nhóm `HÔM QUA`); sau đăng nhập lại, 12:31 hiện đủ 3 thông báo hôm nay | `_recon__thong-bao-b-1144.png` ⟷ `TC-ASN-009__verify-thong-bao-khop-tuyen.png` | Chưa có TC nào phủ hành vi refresh ⇒ đề nghị `/analyze-requirements --update` bổ sung SC cho **làm mới danh sách thông báo** |
| 3 | **`TC-ASN-010` Steps nói nút `Nhận giao`, app hiện `Tôi mang giúp được`** ở luồng vào từ thông báo khớp tuyến | màn đang mở lúc dừng phiên (ghi ở `vibe-log.md §DỪNG PHIÊN`) | Fragment v1.0 dặn *"giữ đúng nhãn từng luồng, ⛔ không đồng nhất hoá"* ⇒ **chạy `TC-ASN-010` thật** ở phiên sau rồi mới kết luận lệch tài liệu hay lệch app |
| 4 | **Nhãn buổi thật `Sáng (8–12h)`**, fragment ghi *"(6–12h)"* | `_setup__seed-s1-buoc2.png` | Trùng phát hiện VR-007 — **vẫn chưa sửa fragment**, đề nghị sửa `TC-ASN-v1.1.md §0` |
| 5 | Thông báo khớp tuyến `41 phút trước` (≈11:50) trùng đúng mốc B **huỷ nhận đơn** ⇒ nghi **tin trở lại Bảng tin thì bắn lại thông báo** | `TC-ASN-009__verify-thong-bao-khop-tuyen.png` | ⛔ Chưa kiểm chứng — phiên sau tap vào nó xem trỏ tin nào |

## Recommendation

- **Automate now:** 5 TC (locators ready trong `vibe-locators-latest.md`)
- **CHẠY TIẾP phần còn nợ:** **16 TC** — `/vibe-test --module asn` (bộ lọc pending tự bốc đúng 16 TC này)
- **Gần xong nhất (ưu tiên phiên sau):** `TC-ASN-010` · `011` · `012` · `022` — **seed đã đăng đủ**, chỉ cần mở chuông + chụp evidence riêng từng TC (~15 phút)
- **Kế tiếp:** `TC-ASN-005` · `007` · `020` — tiền đề sẵn (Tin 2 `Đã ghép`, Tin 1 `Chờ ghép`), chỉ cần **1 tài khoản thứ 3** (đề xuất `stag_giangdc2@`)
- **Nặng seed:** `014` · `015` · `016` · `017` · `018` · `025` — cần 3–6 tin NEED/tuyến; quy trình seed đã thông, ⛔ không còn rào cản kỹ thuật
- **Chặn hạ tầng thật:** `006` (2 máy) · `008` (3 máy) · `019` (dev lùi ngày) — QC đã chốt **cố chạy thật rồi mới kết luận**, phiên này **chưa kịp thử**

## Gate

```
python3 .claude/hooks/verify_evidence.py 08_test-runs/vibe/VR-008-ASN-2026-09-19 \
  || python3 ~/.claude/skills/vibe-test/scripts/verify_evidence.py 08_test-runs/vibe/VR-008-ASN-2026-09-19
```
Kết quả: **exit 1 — đúng như kỳ vọng**, vì còn **16 TC `⏳ NOT_RUN`** trong `coverage-ASN.md` (trường hợp **(B) CÒN NỢ COVERAGE** của `execute.md §Step 6.5` — *"KHÔNG phải lỗi cần sửa"*, chỉ cần khai đúng).
⇒ **§8 = PARTIAL.** Phần evidence: **5/5 TC đã chạy đều có ảnh riêng**, ⛔ không TC nào thiếu.
