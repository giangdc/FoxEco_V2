# Vibe Test Report — VR-014 — module HOME — v1.1 — 2026-09-21

> Platform: **mobile** (Appium MCP / UiAutomator2) · **EMU** `emulator-5554` (máy thật ngắt kết nối) · STG · host app `com.hrisproject.stag` (FoxPro) → FoxEco
> Tập chạy: **`--pending` chỉ TC v1.1** theo yêu cầu QC — 9 TC nợ `008 019 021 025 027 028 029 030 031`. **QC cho phép:** đổi tài khoản + đăng thêm 1 tin NEED. **QC KHÔNG cho phép:** ghép đơn P3 · vòng giao–nhận đến Hoàn thành.

## Summary

## Scope Coverage ★★ (mẫu số = SCOPE_TOTAL của module — sổ gồm cả CARRIED v1.0)

| | Count | % scope |
|---|-------|---------|
| **SCOPE_TOTAL (module HOME)** | **32** | 100% |
| Chạy **trong run này** | **5** | 15,6% |
| ✅ PASS từ **run trước** (không chạy lại) | 13 | 40,6% |
| ❌ FAIL / 🚫 BLOCKED / ⛔ N-A từ **run trước** | 4 *(1 BLOCKED + 3 N-A)* | 12,5% |
| ⏳ **NOT_RUN (còn nợ)** | **10** | 31,3% |
| ⚠️ NOT_EVIDENCED | 0 | 0% |

**Có verdict cuối: 22/32 · CÒN NỢ 10 → §8 = PARTIAL.** Trong 10 TC nợ: **4 là v1.1** (`008 029 030 031`), **6 là CARRIED v1.0** (`004 014 017 018 020 023`) ngoài phạm vi yêu cầu.

**📊 Riêng v1.1 (11 TC hiệu lực): 7/11 có verdict = 64%** *(trước phiên 2/11 = 18%)* · ✅ PASS 3 (`019 021 026`) · ❌ FAIL 2 (`025 027`) · 🚫 BLOCKED 1 (`028`) · ⛔ N-A 1 (`032`) · ⏳ 4 (`008 029 030 031`).

- Sổ tích lũy: `coverage/coverage-HOME.md` · audit phiên: `scope-ledger.md` · lát cắt v1.1: `coverage/PROGRESS-v1.1.md`

## Kết quả các TC chạy trong run này (5 TC)

| Result | Count | % N_run |
|--------|-------|---|
| ✅ PASS | 2 (`019` `021`) | 40% |
| ❌ FAIL | 2 (`025` `027`) | 40% |
| 🚫 BLOCKED | 1 (`028`) | 20% |

## Evidence Coverage ★
| Chỉ số | Giá trị |
|---|---|
| TC có evidence / tổng TC đã chạy | **5/5** |
| Gate `.claude/hooks/verify_evidence.py` | xem mục "Gate" cuối phiên |

## 🐞 2 ứng viên bug mới (⛔ chưa `/log-bug` — chờ QC review)

| TC | Nội dung | Mức | Căn cứ |
|---|---|---|---|
| **`TC-HOME-025`** ❌ | Nút **`Xem thêm trên Bảng tin` hiện khi đúng 5 tin** hợp lệ (Bảng tin xác nhận đúng 5). Còn 4 tin thì không có nút ⇒ app dùng **`≥ 5`** thay vì `> 5` | P3 · Low | `TC-HOME-025__step4-FAIL-*` · `SC-HOME-030` / `C-HOME-03` |
| **`TC-HOME-027`** ❌ | Empty state `Đơn của tôi` **sai `EMP-02`**: chuỗi `Chưa có đơn nào` (spec: *"Bạn chưa có đơn nào đang chạy"*), **thiếu CTA** `Tạo đơn gửi hàng`, **thiếu icon** (section vẫn hiện — đúng `C-HOME-05`) | P3 · Low | `TC-HOME-027__step3-FAIL-*` · `DOC-v1.1-01 §8.17.1` |

⚠️ Cả hai nên kiểm lại với BA nếu Expected có thể đã đổi (`EMP-02`, biên `5`). `TC-HOME-026` (empty state `Tin mới`) đã PASS ⇒ chuỗi `EMP-01` đúng, chỉ `EMP-02` lệch.

## 📝 Ghi nhận
- **`TC-HOME-028` 🚫 BLOCKED** — hero `0 · Chưa có đóng góp nào` **ĐÚNG**; cộng đồng `325 đơn · 23743 người` (STG không thể về 0). Ngoài ra vùng này **vẫn có** nút `Xem bảng tin gửi hàng` trong khi Expected nói không có CTA — chưa rõ do dữ liệu hay app ⇒ cần BA/môi trường sạch.
- **Tiền đề "dọn STG" của `025`/`019`/`021` không làm được** trên STG dùng chung ⇒ thay bằng **đo số tin hiện có rồi bổ sung** (4 → 5 → ≥7). Verdict dựa trên số đo thực ở từng thời điểm.
- **STG bị người khác thao tác song song:** giữa phiên xuất hiện tin lạ `FTEL SG07 → FTEL SG03` (~2 phút trước) và tin `P3` của VR-013 biến mất. Số liệu biên (5/6 tin) dễ đổi.
- **Tài khoản "sạch":** `stag_thuyntt22@` (Thủy) hiện **0 đơn · 0 đóng góp** — dùng được cho `027/028/029` (⚠️ đừng dùng cho việc khác trước khi chạy `029`). `USR-accounts.md §2` đang ghi *"STG không còn tài khoản trắng"* ⇒ **cần đính chính**.

## Còn nợ v1.1 — 4 TC (cần QC cấp quyền / dữ liệu)

| TC | Vì sao chưa chạy | Cần gì |
|---|---|---|
| `TC-HOME-008` P2 | vòng giao–nhận đến Hoàn thành (đổi trạng thái đơn thật) — QC không cho phép ở phiên này. Lý do cũ (bug `B1`, OTP nhập tay) **đã lỗi thời** | quyền đổi trạng thái đơn + 3 tài khoản |
| `TC-HOME-029` P3 | như trên; tài khoản "sạch" đã có (Thủy) | quyền + Thủy đăng NEED khai C nhận |
| `TC-HOME-030` P3 | thiếu 1 tin **đã ghép còn hạn** (cần ghép bằng tài khoản thứ 3 — không được phép); tin hết hạn + tin của chính mình đã có sẵn | quyền ghép 1 tin |
| `TC-HOME-031` P2 | vòng giao–nhận đến Hoàn thành | quyền + 3 tài khoản; mốc nền cộng đồng hôm nay `325 đơn` |

▶️ Chạy tiếp v1.1 HOME: `/vibe-test --module HOME --tc TC-HOME-008,TC-HOME-029,TC-HOME-030,TC-HOME-031`

## Dữ liệu phát sinh trên STG
| Loại | Nội dung |
|---|---|
| **NEED ×2** của Giang (`Chờ ghép`) | `Tài liệu·Thấp·Nhẹ·Nhỏ`, `FTEL Đà Nẵng Cẩm Lệ → Tòa V-City`, người nhận `Đặng Châu Anh`, buổi `Giờ nào cũng được` (⚠️ tin thứ 2 hiển thị `Hôm nay · Sáng` — có thể chọn nhầm buổi, không ảnh hưởng verdict). **Hiện trên Bảng tin công khai** — cân nhắc huỷ |
| **Đổi tài khoản** | Emulator hiện đăng nhập **Nguyễn Thị Thanh Thủy** (Giang đã đăng xuất) |
| **Máy thật** `R58T20PLP8K` | không còn kết nối — cần cắm lại nếu muốn chạy song song 2 tài khoản |

## Locator Coverage
| Pages visited | Elements | Verified ✅ | Not found 🚫 |
|---|---|---|---|
| 3 (Trang chủ · Bảng tin · Đăng tin) | 8 mới | 8 | 2 (`Tạo đơn gửi hàng`, `Bạn chưa có đơn nào đang chạy`) |

## Gate
Chạy `python3 .claude/hooks/verify_evidence.py 08_test-runs/vibe/VR-014-HOME-2026-09-21` — kết quả ghi ở cuối phiên (xem trả lời).
