# KP-01 — Kiến thức nghiệp vụ xác nhận NGOÀI tài liệu

> **Phạm vi:** những quy tắc nghiệp vụ / hành vi UI đã được xác nhận nhưng **KHÔNG có (hoặc chỉ có một phần) trong BRD/PRD/prototype**. Nguồn: BA/PO trả lời qua chat, QA quan sát app STG, ảnh Figma, và 2 phiên vibe-test trên thiết bị Android thật.
>
> **Cách trích dẫn ở project mới:** `DOC-v1.0-05 KP-01 §<số mục> <KB-ID>`

---

## 1. Quy ước độ tin cậy

| Ký hiệu | Nghĩa | Được viết TC khẳng định? |
|---|---|---|
| 🟢 **XÁC NHẬN** | Có bằng chứng trực tiếp: ảnh Figma cụ thể, screenshot vibe-test, hoặc BA/PO trả lời rõ ràng | ✅ Có |
| 🟡 **QA KHẲNG ĐỊNH** | QA GiangDC2 mô tả qua chat, chưa kèm ảnh/tài liệu | ⚠ Nên vibe-test xác nhận trước |
| 🔴 **CHƯA XÁC NHẬN** | Suy đoán / mâu thuẫn / đang chờ BA | ⛔ KHÔNG — mở clarification (xem KP-03 §4.1) |

**Nguồn viết tắt:**
- `BA-chat` — BA/PO trả lời trực tiếp qua chat (đợt batch 2026-07-27 và các lần lẻ sau đó)
- `QA-obs` — QA GiangDC2 quan sát app STG rồi mô tả lại
- `Figma` — ảnh trong `Fox Eco Doc/images/*` (82 ảnh), có hash cụ thể
- `VIBE` — vibe-test trên thiết bị Android thật `ZPB66PZLPRBMEAZT`, có screenshot (2026-07-31)
- `CA` — merge từ phân tích của QC anhdc4 (project đã xoá, git `6f0b0cd`)

---

## 2. USR — Tài khoản & Hồ sơ

### KB-USR-01 🟢 Màn Cá nhân là VIEW-ONLY, không có chức năng sửa hồ sơ
BRD (`USR-02`) ghi *"Xem/cập nhật hồ sơ"* (tên, SĐT, avatar, phòng ban, khu vực, kênh liên hệ). **Thực tế app STG KHÔNG có bất kỳ chức năng cập nhật/sửa nào** — cả 6 trường đều chỉ để xem.
- Nguồn: `QA-obs` 2026-07-24 · Clarification: `C-USR-03` Resolved
- Ảnh hưởng: không viết TC cho luồng edit profile.

### KB-USR-02 🟢 Badge hạng thành viên chỉ là text tĩnh, KHÔNG có điểm số
Figma màn Cá nhân (`570ad9d32e3dbdf44c72d6140826f0e6f9a3393e`, `e5764b10a94b0d51fab023c1a92b6f25732cb402`) cho kết quả **trung gian** giữa BRD và demo:
- **CÓ** badge pill `🏆 Hạng Đồng hành` (dạng text)
- **KHÔNG** có "Điểm ECO (540)" hay "Điểm uy tín (4.8)" — dù demo/PRD có mô tả
- Card trắng chỉ có 2 số liệu: `12 — đơn đã giúp`, `8 — quà đã nhận`; menu: `Đơn của tôi`, `Quà đã nhận`
- BA/PO xác nhận: cơ chế tính tier là **phase sau**, v1.0 không có logic phân hạng.
- Nguồn: `Figma` + `BA-chat` 2026-07-27 · Clarification: `C-USR-01` Resolved — Out of scope v1.0

### KB-USR-03 🟢 Không có màn cấu hình kênh liên hệ
`USR-07` (BRD) mô tả cấu hình kênh liên hệ sẽ lộ (SĐT bắt buộc / Workplace-email tuỳ chọn) — **không xuất hiện ở bất kỳ ảnh Figma nào** của màn Cá nhân, và không có trên app STG.
- Nguồn: `Figma` + `QA-obs` + `BA-chat` 2026-07-27 · Clarification: `C-USR-02` Resolved — Out of scope v1.0

### KB-USR-04 🟡 Menu "Đơn của tôi" tại màn Cá nhân điều hướng sang màn Hoạt động
- Nguồn: `QA-obs` (sau đó tìm được nguồn văn bản `DOC-v1.0-02 §3.9`)

---

## 3. ORD — Đăng tin & Quản lý tin

### KB-ORD-01 🟢 Field bắt buộc trong wizard đăng tin
BA/PO xác nhận (2026-07-27) **CÓ** rule bắt buộc — trái với prototype (cho để trống tất cả):
- Bước 1: `Loại hàng`, `Giá trị hàng` bắt buộc
- Bước 2: thông tin `Người nhận` bắt buộc
- Nguồn: `BA-chat` · Clarification: `C-ORD-01` Resolved
- ⚠ Bổ sung 2026-07-28: **BRD v3.2 §D8** đã có đủ maxlength — nay là kiến thức có trong tài liệu, xem KP-06 §3.

### KB-ORD-02 🟢 Hạn tin = giá trị "Đến ngày" người dùng tự chọn
BRD `ORD-06` chỉ ghi *"quá hạn cấu hình"* không có con số. BA/PO xác nhận: hạn tin **không phải hằng số hệ thống** — bằng đúng khoảng ngày user chọn ở Bước 2/3; đến đúng **"Đến ngày"** thì tin tự chuyển `EXPIRED`.
- Nguồn: `BA-chat` 2026-07-27 · Clarification: `C-ORD-03` Resolved
- ⚠ Lịch sử: phân tích của CA từng chốt nhầm là "Từ ngày", sau đó user đảo lại thành **"Đến ngày"** (khớp BRD v3.2). Dùng "Đến ngày".

### KB-ORD-03 🟢 v1.0 KHÔNG chặn loại hàng cấm
Chip "Thuốc/Y tế" vẫn chọn được bình thường dù nguyên tắc cấm gửi thuốc. Banner cảnh báo chỉ là **thông tin tĩnh**, không có validate chặn theo danh mục.
- Nguồn: `BA-chat` 2026-07-27 · Clarification: `C-ORD-04` Resolved
- Ảnh hưởng: không viết TC negative "chặn Thuốc/Y tế".

### KB-ORD-04 🟢 Ngưỡng giá trị hàng bằng số tiền — chưa triển khai ở v1.0
`BR-ORD-03` (ngưỡng giá trị + bắt buộc ảnh khi vượt ngưỡng) **chưa làm ở phase này**. Riêng cơ chế cảnh báo theo mức `Cao` thì **CÓ** (xem KB-ORD-05).
- Nguồn: `BA-chat` 2026-07-27 · Clarification: `C-ORD-02` Resolved — Out of scope v1.0 (đây là clarification từng là BLOCKER cứng, nay đã gỡ)

### KB-ORD-05 🟢 Banner cảnh báo khi Giá trị hàng = "Cao" — nguyên văn
Chọn `Thấp` / `Vừa` → **không** có banner. Chọn `Cao` → hiện banner, nguyên văn xác nhận trên app thật:
> *"Hàng giá trị cao: hai bên tự thoả thuận và chịu trách nhiệm với nhau. FoxEco không bảo hiểm, không đứng ra vận chuyển hay bồi thường."*
- Nguồn: `VIBE` VR-002 (TC_04.8/9/10 PASS, có screenshot) 2026-07-31

### KB-ORD-06 🟢 Địa chỉ lấy/giao hàng có autocomplete tra văn phòng
Gõ text tự do → hiện dropdown gợi ý danh sách văn phòng khớp từ DB, **không phân biệt hoa/thường**. **Phải chạm chọn gợi ý** thì giá trị mới được lưu; gõ text mà không chọn thì field không giữ giá trị.
- Nguồn: `BA-chat` 2026-07-29 (xác nhận là BA trả lời, không phải quan sát app) + `VIBE` VR-001 finding #5, VR-002 TC_04.29 PASS
- ⚠ Hệ quả cho automation: script phải tap suggestion tường minh, không chỉ set text.

### KB-ORD-07 🟢 Màn "Hoạt động" (Đơn của tôi) — cấu trúc và rule
| # | Thành phần | Rule |
|---|---|---|
| 1 | 2 tab | `Đang diễn ra` / `Đã hoàn thành` |
| 2 | Tab mặc định | `Đang diễn ra` |
| 3 | Card (5 trường) | Icon trạng thái · Tên tin · Tuyến `Từ → Đến` · Ngày · Badge trạng thái |
| 4 | Card "Hết hạn" có thêm dòng lý do | *"Không có ai nhận mang giúp trong thời gian đăng — tin đã tự động đóng."* |
| 5 | Tap card ≠ "Hết hạn" | → mở màn "Chi tiết tin" |
| 6 | Tap card "Hết hạn" | → không cho thao tác (non-clickable) |
| 7 | Đơn trạng thái "Đã huỷ" | **KHÔNG** hiển thị ở cả 2 tab |
| 8 | Bottom nav | 5 tab: Trang chủ / Bảng tin / [+ Đăng tin] / Hoạt động / Cá nhân |
- Nguồn: `QA-obs` + ảnh `00_input/v1.0/27072026/Screenshot From 2026-07-27 15-23-25.png` (⚠ ảnh này có status bar "9:41" — là **mockup Apple chuẩn, không phải chụp máy thật**) · xác nhận nghiệp vụ qua chat 2026-07-27
- ⚠ Trên card "Hoàn thành" có chuỗi `★★★★★ Đã đánh giá` nhưng **rating 1-5 sao đã out-of-scope v1.0** → coi là UI leftover, KHÔNG viết TC assert rating (xem KB-GIFT-02).

### KB-ORD-08 🟢 Section "Tin mới" ở Trang chủ hiển thị cho CẢ Sender lẫn Carrier
BRD mô tả đây là tính năng riêng của Carrier, nhưng UI thực tế cho thấy Trang chủ của Sender cũng có section này. User chốt: *"viet theo UI luon nha"*.
- Nguồn: `CA` + user chốt 2026-07-29 · Clarification: `C-ORD-07` Resolved

### KB-ORD-09 🔴 Số lượng tin ở section "Tin mới" — MÂU THUẪN CHƯA GIẢI QUYẾT
`DOC-v1.0-02 §3.1 Table 3` ghi *"Rút gọn 1 tin mới nhất của cả cộng đồng"* vs `DOC-v1.0-01 §D7 OPR-01`/`US-D06` ghi *"Chỉ hiện tối đa 5 tin"* — hai con số khác nhau cho cùng một khối UI.
- Xử lý ở đợt cũ: TC completeness **cố ý không assert số lượng**; TC biên viết theo trần 5 của BRD.
- ⛔ **Cần BA xác nhận.** Xem KP-05 §2.

### KB-ORD-10 🟡 Màn "Đăng tin mới" (chọn vai trò) — 5 thành phần
Subtitle *"Bạn muốn làm gì?"* · card `Tôi cần gửi hàng` (icon hộp cam) · card `Tôi nhận giao hàng` (icon route tím) · banner cam kết nền vàng nhạt icon ⓘ (không phí / không chat / không thanh toán / SĐT lộ sau ghép) · cả 2 card bấm được.
- Nguồn: `Figma` hash `f821ba3087b8cc6e8065fbde6e327274d34482b2` + `VIBE` VR-002 TC_04.1 PASS 🟢

### KB-ORD-11 🟢 Form OFFER (đăng ký tuyến) là form 1 TRANG, không có wizard 3 bước
Bấm `Tôi nhận giao hàng` → form một trang, **không có step indicator "Bước x/3"**. Field quan sát được: `Thông tin của tôi` (Tên, SĐT — read-only auto-fill) · `Điểm xuất phát (A)` · `Điểm đến (B)` · `Khoảng thời gian (ngày)` Từ ngày/Đến ngày · `Thời gian di chuyển` Khởi hành/Đến nơi · nút `Đăng tin ngay`.
- Nguồn: `VIBE` VR-002 TC_04.3 PASS 2026-07-31

---

## 4. ASN — Ghép nối

### KB-ASN-01 🟢 SĐT chỉ lộ SAU KHI ghép
Prototype hiện sẵn SĐT + nút "Gọi ngay" ngay từ trạng thái "Chờ ghép". BA/PO xác nhận **rule chính thức = lộ sau ghép** (khớp `BR-CON-02`); hành vi prototype là **bug**, không phải hành vi mong muốn.
- Nguồn: `BA-chat` 2026-07-27 · Clarification: `C-ASN-01` Resolved

### KB-ASN-02 🟢 Cấm tự nhận mang giúp đơn của chính mình
`OPR-05` cấm tự khớp; prototype lại cho phép chủ tin/Người nhận bấm "Tôi mang giúp được" trên tin của mình. BA/PO xác nhận **không được phép** — hành vi prototype là bug.
- Nguồn: `BA-chat` 2026-07-27 · Clarification: `C-ASN-02` Resolved
- ⚠ Lưu ý phạm vi: bug này ở màn **Chi tiết tin** (public), khác màn **Theo dõi đơn** (đã role-aware đúng).

### KB-ASN-03 🟢 Trần thông báo khớp tin = 5 thông báo cho MỖI tin OFFER
Không phải "5 thông báo/ngày" cộng dồn — tính **riêng theo từng tin**.
- Nguồn: `BA-chat` 2026-07-29 · Thay thế scenario cũ `SC-NTF-006` (đã DEPRECATED)
- ⚠ Giá trị test 3/5/6 tin là **giá trị chốt**, không phải mock.

### KB-ASN-04 🟡 Định nghĩa "khớp tuyến"
= **trùng địa chỉ giao hàng đã chọn** + **khung giờ phù hợp**. **KHÔNG dùng bán kính GPS / khoảng cách địa lý.**
- Nguồn: `BA-chat` 2026-07-27 · Clarification: `C-NTF-02` **Partially Resolved**
- 🔴 Còn thiếu: "khung giờ phù hợp" là trùng hoàn toàn hay có độ lệch cho phép? Chu kỳ quét khớp? Ngưỡng gộp thông báo? → xem KP-05 §2.

### KB-ASN-05 🔴 Wizard đăng tin không tạo listing độc lập trong feed Carrier/Receiver
Ghi nhận trên prototype. Chưa rõ là giới hạn kiến trúc bản demo (chấp nhận được) hay hành vi cần fix.
- Nguồn: `CA` · Clarification: `C-ASN-03` Open — cần xác nhận lại khi có backend thật

---

## 5. DLV — Giao nhận

### 5.1 KB-DLV-01 🟢 MA TRẬN NHÃN NÚT × TRẠNG THÁI × VAI TRÒ (màn Theo dõi đơn)

> **Đây là mục giá trị nhất của cả bộ pack** — hoàn toàn không có trong BRD/PRD/demo docx, do QA cung cấp từ testing trực tiếp rồi **đối chiếu xác nhận độc lập từng ô qua ảnh Figma** (mỗi ô có 1–3 ảnh xác nhận).

| # | Trạng thái | Người gửi (Sender) | Người vận chuyển (Carrier) | Người nhận (Receiver) |
|---|---|---|---|---|
| 1 | **Chờ ghép** | `Đang chờ người vận chuyển nhận đơn` — disable<br>+ `Chỉnh sửa` / `Huỷ đơn` | `Tôi mang giúp được` — enable *(ở màn Chi tiết tin)* | `Đang chờ người vận chuyển nhận đơn` — disable<br>+ `Huỷ đơn` |
| 2 | **Đã ghép**<br>*(stepper hiển thị "Lấy hàng")* | `Đã ghép · chờ shipper lấy hàng` — disable<br>+ `Huỷ đơn` | `✓ Tôi đã lấy hàng` — enable<br>+ `✕ Huỷ nhận đơn` (→ popup lý do bắt buộc) | `Đã có người vận chuyển · chờ lấy hàng` — disable<br>+ `Huỷ đơn` |
| 3 | **Đang giao** | `Đang giao đến người nhận` — disable | `Đã giao cho người nhận` — enable | `✓ Đơn đang trên đường đến bạn` — disable |
| 4 | **Đã giao** | `✓ Đã giao · chờ người nhận xác nhận` — disable | `✓ Đã giao · chờ người nhận xác nhận` — disable | `Xác nhận đã nhận hàng` — **enable (duy nhất)** |
| 5 | **Hoàn thành** | `✓ Cảm ơn người vận chuyển` — enable<br>→ sau khi gửi quà đổi thành `Bạn đã đánh giá` (disable) | `✓ Đơn đã hoàn thành ✓` — disable | `Đơn đã hoàn thành ✓` — disable |

**Popup xác nhận** — mọi hành động "enable" của Carrier/Receiver đều đi qua 1 popup title cố định `Xác nhận` trước khi đổi trạng thái thật (không chuyển ngay khi bấm nút nền):
| Hành động | Nội dung popup |
|---|---|
| Carrier — Tôi đã lấy hàng | *"Bạn xác nhận đã lấy hàng từ người gửi và bắt đầu giao?"* |
| Carrier — Đã giao cho người nhận | *"Bạn xác nhận đã giao hàng tận tay người nhận?"* |
| Receiver — Xác nhận đã nhận hàng | *"Bạn xác nhận đã nhận được hàng từ người vận chuyển?"* |

- Nguồn: `QA-obs` 2026-07-24 + `Figma` xác nhận đủ 15 ô (hash tiêu biểu: `dc8cf987…` Sender/Chờ ghép · `2e2ff7bc…`+`974b5c52…` Carrier/Lấy hàng · `c8cae4c3…`+`e1699c4f…`+`ca5e7239…` Đang giao 3 vai trò · `8563adc1…`+`91b08fb1…`+`7d8b4a8c…`+`5dc3ce81…`+`82d9aace…` Đã giao 3 vai trò · `19490aa9…`+`2658b17b…`+`76e115a2…` Hoàn thành 3 vai trò)
- ⚠ Ma trận này **chỉ áp dụng cho màn Theo dõi đơn** (role-aware), KHÔNG áp dụng cho màn Chi tiết tin public.
- ⚠ Lưu ý thuật ngữ: cùng một trạng thái backend `MATCHED` nhưng progress-bar dùng chữ **"Lấy hàng"**; "Đã ghép" chỉ dùng khi nói về trạng thái backend/badge.

### KB-DLV-02 🟢 Chỉ Receiver được xác nhận "Đã nhận hàng"
BRD mâu thuẫn nội bộ: `DLV-03` (§D3) ghi RECEIVER/SENDER, nhưng `BR-INT-03` (§A5) + demo docx §5.2 chỉ cho phép Receiver. Ảnh Figma xác nhận nhất quán qua 5 ảnh: nút chỉ active với Receiver; Sender/Carrier cùng bước "Đã giao" chỉ thấy nhãn disabled.
- Nguồn: `Figma` 2026-07-24 · Clarification: `C-DLV-01` Resolved — **Receiver-only**

### KB-DLV-03 🟢 Màn "Xác nhận đã nhận hàng" dùng bản MODAL ĐƠN GIẢN
Tồn tại 2 phiên bản trong tài liệu: modal đơn giản (§5.2) vs form đầy đủ có ảnh bằng chứng + điểm uy tín carrier (§5.3). BA/PO chốt **theo Figma = modal đơn giản** (`Xác nhận` / *"Bạn xác nhận đã nhận được hàng từ người vận chuyển?"* / 2 nút Huỷ–Xác nhận). Form đầy đủ **không áp dụng ở v1.0**.
- Nguồn: `BA-chat` 2026-07-27 · Clarification: `C-DLV-03` Resolved

### KB-DLV-04 🔴 Chia sẻ vị trí (GPS-01) mặc định bật hay tắt — CHƯA CHỐT
BRD tự nêu câu hỏi mở. BA/PO trả lời "phase sau" nhưng **chưa cho giá trị cụ thể**.
- Clarification: `C-DLV-02` Open (non-blocking)

### KB-DLV-05 🟢 Màn "Báo sự cố" chưa có đặc tả — out of scope v1.0
- Nguồn: `BA-chat` 2026-07-27 · Clarification: `C-CNL-01` Resolved — Out of scope v1.0

---

## 6. GIFT — Quà cảm ơn

### KB-GIFT-01 🟢 Luồng "Cảm ơn người vận chuyển" → "Bạn đã đánh giá"
Ở trạng thái Hoàn thành, Sender thấy nút `✓ Cảm ơn người vận chuyển` (enable). Sau khi chọn 1 loại quà và gửi thành công, nút **đổi nhãn thành `Bạn đã đánh giá` (disable, không gửi lại được)**.
- Nguồn: `QA-obs` 2026-07-24 + `Figma` (popup *"Đã gửi lời cảm ơn!"*) — **phát hiện mới, chưa từng có ở BRD/PRD/demo**
- Đã sinh requirement riêng ở đợt cũ (`REQ-GIFT-003`).

### KB-GIFT-02 🟢 Chấm sao 1-5 KHÔNG có ở v1.0
`RAT-01/02` (đánh giá 1-5 sao) mâu thuẫn trực tiếp với `BR-INT-06`/§A7/§A8. BA/PO xác nhận: **phase sau** — v1.0 chỉ có Quà ảo (`GIFT-01`), chưa có màn chấm sao. Chuỗi `★★★★★ Đã đánh giá` trên card là UI leftover.
- Nguồn: `BA-chat` 2026-07-27 · Clarification: `C-GIFT-01` Resolved — Out of scope v1.0
- 📌 Kéo theo: "Đánh giá" trong scope Phase 1 của PM = **Quà ảo**, không phải chấm sao.

### KB-GIFT-03 🟡 Màn "Quà đã nhận" — card đếm số hiển thị CÓ ĐIỀU KIỆN
Card đếm theo 4 loại quà (bông hoa / ly cà phê / gấu bông / vương miện) nhưng **chỉ hiển thị loại đã thực sự nhận (count > 0)** — loại chưa nhận lần nào thì **không load, không hiện dạng "0"**. Ngoài ra có `Danh sách lịch sử` nhận quà và icon quay lại ở header (→ về màn Cá nhân).
- Nguồn: `QA-obs` 2026-07-27 (điều chỉnh so với hiểu ban đầu là "luôn hiện đủ 4 loại") + văn bản `US-D20`
- ⚠ Thành phần "Danh sách lịch sử" **chỉ có bằng chứng văn bản US-D20**, chưa có ảnh Figma/app → **cần vibe-test xác nhận**. Nếu app không có → mở clarification, không im lặng bỏ qua.

### KB-GIFT-04 🔴 Nút back ở màn "Tặng quà" nhảy sai màn
Bấm back (←) từ màn "Tặng quà" (mở từ item mẫu tab "Đã hoàn thành") nhảy tới màn "Xác nhận đã nhận hàng" của **một đơn KHÁC không liên quan**, thay vì quay về "Đơn của tôi".
- Nguồn: `CA` quan sát UI 2026-07-29 · Clarification: `C-GIFT-02` Open — nhiều khả năng là giới hạn của bản demo (item mẫu tĩnh chưa wiring back-stack), CA đánh giá không nghiêm trọng.

---

## 7. CNL — Huỷ đơn

### KB-CNL-01 🟢 Huỷ đơn / Huỷ nhận đơn PHẢI ghi log LỊCH SỬ (override hành vi hiện tại)
Live-verify qua Chrome MCP (2026-07-29) cho thấy hành vi hiện tại:
- **Huỷ đơn** (Sender/Receiver) → **không ghi log nào** vào block LỊCH SỬ, chỉ hiện banner đỏ *"Đơn hàng đã bị huỷ"*
- **Huỷ nhận đơn** (Carrier) → tệ hơn: **XOÁ LUÔN dòng "Ghép thành công"** khỏi LỊCH SỬ

User chốt: *"huy don va huy nhan don hien tai cu luu log lich su nha"* → **LỊCH SỬ phải ghi log cho cả 2 hành động; hành vi hiện tại là GAP cần dev bổ sung.**
- Nguồn: `CA` live-verify + user chốt 2026-07-29 · Clarification: `C-CNL-02` Resolved theo hướng override
- 📌 Đợt cũ đã cố ý viết TC bắt gap này (dự kiến FAIL) — xem KP-05 §4.

### KB-CNL-02 🟢 Lý do huỷ bắt buộc, tối thiểu 5 ký tự — nhưng UI hiện KHÔNG enforce
Rule: `VAL-04` (BRD v3.2 §D8.3) — lý do huỷ là text bắt buộc, tối thiểu 5 ký tự.
**Thực tế UI (CA live-verify):** chỉ chặn khi để **rỗng**; nhập 4 ký tự vẫn bật nút, và **không trim khoảng trắng trước khi đếm** (5 dấu cách vẫn qua).
- Nguồn: `CA` live-verify 2026-07-29
- 📌 Đợt cũ đã viết TC bắt 2 gap này (dự kiến FAIL) — xem KP-05 §4.

---

## 8. NTF — Thông báo

### KB-NTF-01 🟡 Chấm đỏ chưa đọc theo TỪNG ITEM (bằng chứng gián tiếp)
Ảnh Figma `3e626d398e3a616a45f5c638df62be830d2f4357`: 2 thông báo mới nhất có chấm đỏ riêng, 2 thông báo cũ hơn **cùng nhóm "Hôm nay"** thì không → gợi ý trạng thái đã-đọc/chưa-đọc theo item.
- 🔴 **Không chứng minh được cơ chế tương tác**: bấm nút "Đánh dấu đã đọc" là mark-all hay mark-per-item? → chờ BA. Clarification `C-NTF-03(a)` Open.

### KB-NTF-02 🟢 Scroll/lazy-load danh sách Thông báo = yêu cầu UI nền tảng
Không có đặc tả phân trang ở bất kỳ tài liệu nào. QA GiangDC2 xác nhận (2026-07-29): đây là **hành vi UI nền tảng bắt buộc** cho danh sách lớn, không cần BA xác nhận riêng như một business rule.
- Clarification: `C-NTF-03(b)` N/A — không phải điểm cần clarification

### KB-NTF-03 🔴 Danh sách loại thông báo chính thức — CHƯA CHỐT
3 nguồn khác nhau: BRD §D6 (`NTF-01..09`) vs demo Table 4 (9 loại, gồm "đánh giá 5 sao", "cộng đồng đạt mốc X đơn") vs Figma. Đợt cũ đã lập **bảng unified 3 nguồn** để BA chọn nhưng **BA chưa trả lời**.
- Clarification: `C-NTF-01` Open · 📌 **Bảng unified đầy đủ 12 hàng sự kiện × 3 nguồn: xem `KP-07_notification-matrix.md`** (đã đóng gói kèm).

---

## 9. TS — Trust & Safety

### KB-TS-01 🟢 Admin Web Portal — không có đặc tả UI, out of scope v1.0
BRD §A3 chỉ nhắc tên nền tảng (*"Mobile App (iOS/Android) + Admin Web Portal"*), không mô tả màn hình/field nào.
- Nguồn: `BA-chat` 2026-07-27 · Clarification: `C-TS-01` Resolved — Out of scope v1.0
- Phạm vi test v1.0 chỉ verify **hệ quả quan sát được từ phía end-user** (vd đơn quá hạn xác nhận → chuyển "admin hỗ trợ"), không test UI Admin Portal.

---

## 10. 🟢 Kiến thức từ VIBE-TEST trên thiết bị thật (2026-07-31)

> **Độ tin cậy cao nhất trong cả bộ pack** — thao tác trực tiếp trên Android thật `ZPB66PZLPRBMEAZT`, SDK FoxEco trong host app `FoxPro_Stag` (STG), có screenshot từng case. 2 phiên: **VR-001** (sáng, 4 TC) và **VR-002** (chiều, ~13 TC trước khi thiết bị hỏng màn hình).

### 10.1 Thông tin kỹ thuật môi trường
| Hạng mục | Giá trị |
|---|---|
| **App package (STG)** | `vn.fpt.ftel.sop.stg` ← xác nhận ở VR-002 (VR-001 chưa biết, phải điều hướng tay qua host app) |
| Thiết bị | Android thật, serial `ZPB66PZLPRBMEAZT` |
| Tài khoản test | Pre-logged-in, tên hiển thị "Chung Hoàng Liêm" |
| Email nội bộ test auto-fill | `stag_anhdc4@fpt.com` |

### 10.2 KB-VIBE-01 🟢 Chip "Loại hàng" — app có 8 chip, KHÔNG có chip tên "Tài liệu"
Chip mặc định được chọn là **`Giấy tờ, hồ sơ`**. Trong 8 lựa chọn thực tế **không tồn tại** chip nào tên "Tài liệu" — trong khi tài liệu/TC đợt cũ đều ghi "Tài liệu".
- Bằng chứng: VR-001 finding #1, VR-002 `TC_04.5` **FAIL** (có screenshot)
- ⛔ **Hành động bắt buộc ở project mới:** xác nhận với BA/dev đây là **UI đã đổi tên** hay **tài liệu sai**, rồi mới viết TC. Đây là lỗi lan rộng — mọi TC nhắc "Tài liệu" ở đợt cũ đều sai chữ.

### 10.3 KB-VIBE-02 🟢 Chip Loại hàng là single-select, LUÔN có 1 chip được chọn
Tap lại chip đang chọn **không deselect được** → **không thể tái hiện trạng thái "chưa chọn Loại hàng"** qua UI. Thử để trống Loại hàng rồi bấm "Tiếp theo" → **chuyển bước bình thường, không bị chặn**.
- Bằng chứng: VR-002 `TC_04.6` **FAIL** (precondition không thiết lập được)
- 📌 Hệ quả: rule "Loại hàng bắt buộc" (KB-ORD-01) **không kiểm chứng được qua UI** — chip mặc định đã thoả điều kiện sẵn. Cần viết lại scenario theo hướng khác.

### 10.4 KB-VIBE-03 🟢 "Giá trị hàng" bắt buộc thật — chặn đúng
Để trống Giá trị hàng → nút "Tiếp theo" chuyển màu nhạt/disabled, không chuyển bước.
- Bằng chứng: VR-002 `TC_04.7` PASS

### 10.5 KB-VIBE-04 🔴 Tên Người gửi KHÔNG read-only như spec — **nghi vấn BUG**
Spec/TC ghi field Tên (Người gửi) là read-only. Thực tế:
- Chạm vào field → **mở được bàn phím** (không disabled)
- Giá trị "Chung Hoàng Liêm" bị **XOÁ TRẮNG ngay sau khi chạm**
- **Không tự phục hồi** trong cùng phiên wizard — phải thoát ra vào lại từ đầu Bước 1/3 mới load lại tên
- Bằng chứng: VR-002 `TC_04.22` **FAIL** (có screenshot)
- ⛔ **Đề xuất log bug riêng.** Rủi ro: user vô tình xoá tên khi chạm nhầm.

### 10.6 KB-VIBE-05 🔴 Địa chỉ lấy hàng KHÔNG được pre-fill
Expected (spec): mặc định `Tòa nhà Lô B3, KCX Tân Thuận, Q.7`. Thực tế: **field trống, chỉ có placeholder**. Tên ✅ và SĐT ✅ vẫn pre-fill đúng.
- Bằng chứng: VR-002 `TC_04.21` **FAIL**
- ⚠ Chưa loại trừ khả năng **tài khoản test chưa cấu hình địa chỉ mặc định** → cần xác nhận với dev.

### 10.7 KB-VIBE-06 🔴 Checkbox điều khoản KHÔNG tick sẵn
TC đợt cũ (`TC_04.71`) expected *"Checkbox điều khoản mặc định đã tick sẵn"*. Quan sát thực tế ở Bước 3/3: **chưa tick**, phải chạm tay mới bật được nút "Đăng tin ngay".
- Bằng chứng: VR-001 finding #2 (quan sát trực tiếp, TC_04.71 không nằm trong scope run đó)
- ⛔ Cần chạy riêng TC này để chốt, nhiều khả năng **FAIL → log bug**.

### 10.8 KB-VIBE-07 🟢 Auto-fill người nhận theo email nội bộ hoạt động đúng 2 chiều
- Email **không tồn tại** trong hệ thống → hiện thông báo *"không tìm thấy, nhập thủ công"*
- Email **có trong hệ thống** (`stag_anhdc4@fpt.com`) → auto-fill đầy đủ **tên / SĐT / địa chỉ** từ danh bạ nội bộ
- Bằng chứng: VR-001 finding #3, VR-002 `TC_04.24` PASS

### 10.9 KB-VIBE-08 🔴 App tự báo lỗi cho chính giá trị nó auto-fill
Auto-fill từ `stag_anhdc4@fpt.com` trả về SĐT người nhận `0000286248` → **chính app báo "Số điện thoại không hợp lệ"** cho giá trị do nó tự điền.
- Bằng chứng: VR-002 `TC_04.24` note
- ⛔ Nghi vấn bug data hoặc bug validate — cần xác nhận.

### 10.10 KB-VIBE-09 🟡 SĐT Người gửi tự đổi giá trị giữa phiên
SĐT Người gửi thay đổi giữa 2 screenshot cùng một phiên (`0000142378` → `0964633313`) mà **không có thao tác nào của user** trên field đó. Chưa điều tra thêm.
- Bằng chứng: VR-001 finding #4 · ⚠ Cần theo dõi, nếu tái hiện thì log bug.

### 10.11 KB-VIBE-10 🟢 Khung giờ mong muốn validate theo đồng hồ thật
Giá trị mặc định (vd 11:10–11:40) **hết hạn** khi form mở lâu (~15 phút), app tự bật validate *"phải muộn hơn hiện tại"*. **Không phải lỗi app.**
- 📌 Hệ quả cho automation/TC: phải chọn khung giờ **tương đối so với "now"**, không hardcode giờ.

### 10.12 Ràng buộc thực thi cần biết trước
| Vấn đề | Chi tiết | Cách xử lý |
|---|---|---|
| TC cần đơn ở trạng thái `Đã ghép` | Cần **bên thứ 2 nhận đơn** — nằm ngoài tầm kiểm soát của tester | Nhờ dev/QA seed dữ liệu trên STG, hoặc chờ ghép tự nhiên |
| Locator không ổn định | Dropdown gợi ý địa chỉ + bánh xe time-picker native **không expose locator phân biệt** cho `appium_find_element` | Fallback tap theo toạ độ (phải derive lại theo từng thiết bị/độ phân giải) |
| Thiết bị tự khoá màn hình | Auto-lock cắt ngang 2 lần | `adb` set `screen_off_timeout` = 30 phút trước khi chạy |

### 10.13 Kết quả 2 phiên
| Phiên | Scope | PASS | FAIL | BLOCKED / dở dang |
|---|---|---|---|---|
| VR-001 (sáng) | 4 TC High của TC_04 | 2 (`TC_04.2`, `TC_04.73`) | 0 | 2 (`TC_04.89`, `TC_04.106` — thiếu đơn MATCHED) |
| VR-002 (chiều) | High+Medium của TC_04 | 7 | 4 (`TC_04.5`, `TC_04.6`, `TC_04.21`, `TC_04.22`) | dừng ở `TC_04.25` — thiết bị đen màn hình; ~58 TC còn lại chưa chạy |

- Locator đã capture: 17 element / 6 màn (14 verified, 3 toạ độ, 2 chưa verify) — xem `evidence/VR-001-2026-07-31/vibe-locators.md` trong chính bộ pack này.
