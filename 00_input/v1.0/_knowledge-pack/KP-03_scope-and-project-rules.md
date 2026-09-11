# KP-03 — Scope, Project Rules & Convention

> Nội dung file này dùng để **seed `02_analyze-requirements/Project_rule.md`** của project mới. Đây là các quyết định về phạm vi và quy ước làm việc, **không suy ra được từ tài liệu**.

---

## 1. Thông tin dự án

| Hạng mục | Giá trị |
|---|---|
| Tên dự án | **FoxEco** |
| Loại sản phẩm | **SDK tích hợp vào app mobile FoxPro có sẵn** — KHÔNG phải web app độc lập |
| Mô tả | Mạng xã hội tương trợ nội bộ FPT Telecom: CBNV đăng tin cần gửi hàng (**NEED**) ↔ đồng nghiệp tiện đường nhận mang giúp (**OFFER**). Không thu phí · không chat trong app · không thanh toán trong app |
| Phạm vi v1.0 | Chức năng **Gửi Hàng** (ưu tiên #1 trong bộ 3 chức năng) + Nền tảng chung (Auth/Profile, Actors, Gift, Trust & Safety) |
| Môi trường | **STG** — host app `FoxPro_Stag`, package `vn.fpt.ftel.sop.stg`. Không có URL riêng |
| Loại kiểm thử | Smoke · Functional · Regression |
| QC phụ trách | GiangDC2 (mode: Solo — trước đây có QC anhdc4, đã merge xong) |
| Ngôn ngữ | Test case / mô tả / bước / output terminal: **Tiếng Việt**. Thuật ngữ kỹ thuật, keyword, status: **Tiếng Anh** |
| Automation | Chưa có. Khi cần: archetype **appium-java** (vì là SDK mobile) |

## 2. Module codes

| Code | Tên | Ghi chú |
|---|---|---|
| `USR` | Tài khoản & Hồ sơ | Auth SSO thuộc host app FoxPro, không test được trực tiếp |
| `ORD` | Đăng tin & Quản lý tin | Module lớn nhất |
| `ASN` | Ghép nối (Assignment) | Rủi ro cao nhất |
| `DLV` | Giao nhận (Delivery) | |
| `GIFT` | Quà cảm ơn | |
| `CNL` | Huỷ đơn (Cancel) | |
| `NTF` | Thông báo | |
| `TS` | Trust & Safety | Phần lớn là backend/Admin, ít bề mặt UI |

> Màn hình dùng chung (Trang chủ, Bảng tin) ở đợt cũ được gán vào `ORD`/`ASN`. Project mới có thể cân nhắc tách module riêng cho 2 màn này khi dùng layout `module-first`.

---

## 3. ⭐ Scope Phase 1 (PM chốt 2026-07-24)

PM chốt phạm vi kiểm thử v1.0 chỉ gồm **5 luồng chính**:

| # | Luồng | Module | Trạng thái làm rõ |
|---|---|---|---|
| 1 | Đăng tin (NEED/OFFER) | ORD | ✅ rõ |
| 2 | Bảng tin | ORD | ✅ rõ |
| 3 | Ghép nối | ASN | ⚠ **PM chưa trả lời**: có gồm auto-match OFFER↔NEED hay chỉ luồng thủ công? |
| 4 | Xác nhận nhận hàng / hoàn thành | DLV | ⚠ **PM chưa trả lời**: có gồm ảnh bằng chứng/GPS/chi phí/báo sự cố hay chỉ core confirm? |
| 5 | Đánh giá | GIFT | ✅ Resolved 2026-07-27 — "Đánh giá" = **Quà ảo (`GIFT-01`)**, chấm sao là phase sau |

> ⚠ 2 câu hỏi treo ở #3 và #4 là **câu hỏi về scope test**, khác với clarification `C-xxx` (về nghiệp vụ). Đến 2026-07-30 vẫn chưa có câu trả lời.

### 3.1 Ngoài phạm vi Phase 1 (xác nhận Out of scope v1.0, 2026-07-27)
- `CNL` — Huỷ đơn
- `NTF` — Thông báo
- `TS` — Trust & Safety / Admin Portal
- `USR` chỉ số cá nhân nâng cao (tier / điểm ECO / CO₂)
- Chỉnh sửa tin (`ORD-10`)
- Ảnh bằng chứng / GPS / chi phí / báo sự cố (nhánh phụ của `DLV`)
- Auto-match tuyến OFFER↔NEED (nhánh phụ của `ASN`)

> 📌 **Lưu ý mâu thuẫn thực tế:** dù `CNL`/`NTF` nằm ngoài scope Phase 1, đợt cũ **vẫn viết đầy đủ TC cho 2 module này** (TC_03 Thông báo 27 TC, TC_08 Huỷ đơn 27 TC). Project mới cần chốt lại: viết TC cho toàn bộ hay chỉ 5 luồng Phase 1.

---

## 4. Custom Rules (bắt buộc áp dụng)

### 4.1 ⭐ Rule §10.1 — UI phải khớp Tài liệu mới được viết TC
*(added 2026-07-24, QA GiangDC2 — đây là rule quan trọng nhất của dự án)*

Chỉ viết test case **khẳng định** một field/nút/màn hình/hành vi UI cụ thể khi **cả 2 nguồn khớp nhau**:
- (a) tài liệu yêu cầu (BRD / PRD / US), **và**
- (b) bằng chứng UI thực tế (ảnh Figma hoặc quan sát app STG thật)

Nếu 2 nguồn **KHÔNG khớp** (field có trong tài liệu nhưng không thấy trên UI, hoặc ngược lại) → **KHÔNG tự suy đoán/bịa vị trí hay hành vi UI**. Bắt buộc:
1. Ghi nhận thành clarification mới `C-[MODULE]-NN`, đánh dấu rõ *"chưa xác nhận UI"*
2. **Không viết TC khẳng định** field/hành vi đó tồn tại ở một màn cụ thể cho tới khi có xác nhận (BA/PO hoặc vibe-test trên app thật)
3. Nếu cần, viết 1 TC dạng **"GAP finding"** ghi nhận sự thiếu vắng, thay vì TC test hành vi giả định

Áp dụng cho **mọi** skill sinh/viết TC: `generate-tc`, `vibe-test`, và cả khi trả lời liệt kê case trực tiếp trong chat.

**Case gốc:** `USR-07` "Cấu hình kênh liên hệ" — có trong BRD nhưng không có ở bất kỳ ảnh Figma nào của màn Cá nhân và không thấy trên app STG.

**Hệ quả thực tế đã xảy ra:** ở đợt merge với QC anhdc4, có **6 nhóm case** chỉ tồn tại trong TC của người kia mà project này không có nguồn tài liệu → **cố ý không viết TC**, chỉ ghi lại chờ đợt phân tích sau (xem KP-05 §3).

### 4.2 Rule §10.2 — Màn có tab/segmented-control → mỗi tab 1 TC riêng verify data
*(added 2026-07-27, QA GiangDC2)*

Khi màn hình có tab switcher lọc dữ liệu theo trạng thái (vd `Đang diễn ra`/`Đã hoàn thành`):
- **KHÔNG gộp** verify data của nhiều tab vào chung 1 TC "chuyển tab qua lại"
- Mỗi tab phải có **≥1 TC riêng** verify đúng data khi tab đó active (danh sách chỉ chứa đúng nhóm trạng thái của tab, không lẫn dữ liệu tab khác)
- TC verify **cơ chế switch tab** vẫn được giữ riêng, độc lập với các TC verify-data-theo-tab

**Lý do:** TC gộp nhiều tab khi FAIL không chỉ ra ngay tab nào sai; tách riêng giúp trace lỗi tức thì + khớp nguyên tắc atomic test case.

**Case gốc:** màn "Hoạt động" — tách TC data tab "Đang diễn ra" và tab "Đã hoàn thành" ra khỏi 1 TC gộp ban đầu.

---

## 5. DOC Notation — cách đánh số requirement của tài liệu

`req_notation: FR/VR (doc-native, module-prefixed)`

BRD **CÓ** đánh số requirement, nhưng theo **ID riêng từng domain** chứ không phải một cặp FR/VR thống nhất:

| Nhóm ID | Nguồn trong BRD | Ví dụ |
|---|---|---|
| `ORD-NN`, `ASN-NN`, `DLV-NN` (kèm biến thể `PUP`/`GPS`/`COST` theo bước flow), `GIFT-NN`, `CNL-NN`, `MTCH-NN`, `LOC-NN`, `RAT-NN` | §D3 (bảng chức năng Gửi Hàng) | `ORD-01`, `MTCH-03` |
| `BR-<MODULE>-NN` | §D4 / §A5 (Business Rules) | `BR-CNL-01`, `BR-CON-02`, `BR-INT-03` |
| `NTF-NN` | §D6 (Notifications) | `NTF-05` |
| `OPR-NN` | §D7 (Operating Rules) | `OPR-01`, `OPR-05` |
| `NT-NN`, `USR-NN`, `TS-NN` | §A2 / §A6 / §A8 (Nền tảng chung) | `USR-07`, `TS-03` |
| `US-D<NN>` | §D1b (User Story, có cột Acceptance Criteria riêng) | `US-D06`, `US-D20` |
| `VAL-NN` | §D8 (BRD v3.2 — Validate & Giá trị mặc định) | `VAL-04` |

**Quy tắc traceability:** cột "Maps (Ref DOC)" dùng **TRỰC TIẾP ID gốc** (vd `ORD-01`, `BR-CNL-01`, `US-D16`), **không quy đổi** sang ký hiệu FR/VR chuẩn hoá.

**PRD (`.docx` tái dựng từ demo)** KHÔNG có ID riêng cho từng field → định vị bằng `§section · Table N` (heading + số bảng).

---

## 6. Quality Gates & Priority

| Gate | Ngưỡng |
|---|---|
| G1 | TC Review score ≥ 70 |
| G2 | P1 pass rate = 100% |
| G3 | Overall pass rate ≥ 90% |
| G4 | No P1 bugs open |
| G5 | Bug fix rate ≥ 80% |
| G6 | Blocked ≤ 0 |
| G7 | SRC-TC match score ≥ 70 (nếu có automation) |

- **Priority:** P1 (Highest) · P2 (High) · P3 (Medium) · P4 (Low)
- **Severity:** Critical · High · Medium · Low

---

## 7. Quy ước đếm scenario (rút ra sau health-check)

> Đợt cũ bị `health-check` flag lặp đi lặp lại vì quy ước này chỉ ghi ở `CLAUDE.md` mà không ghi ở nơi skill đọc.

- Cột **"Tổng SC"** đếm **toàn bộ** scenario, **bao gồm cả `DEPRECATED`**
- Breakdown **P1/P2/P3** chỉ đếm scenario **còn hiệu lực** (loại trừ `DEPRECATED`)
- ⇒ `P1+P2+P3` có thể **nhỏ hơn** `Tổng SC` — đây **không phải sai số liệu**

**Khuyến nghị project mới:** ghi thẳng quy ước này vào `Project_rule.md` ngay từ đầu.
