# Requirement Traceability — v1.0 · Module ORD

> Tạo bởi: analyze-requirements (INIT 2026-09-07) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation: FR/VR` ⇒ **Schema A**.
> ⚠️ **Ranh giới sau khi tách module (2026-09-07):** file này chỉ còn **Đăng tin & Quản lý tin** (wizard NEED · form OFFER · sửa tin · hết hạn · validate form). Màn **Trang chủ** → `HOME` · **Bảng tin/Chi tiết tin** → `FEED` · **Hoạt động** → `ACT`.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module ORD — DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-04 · DOC-v1.0-06

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-ORD-001 | — (bảng §3.5 không đánh số) | `DOC-v1.0-02` §3.5 · `DOC-v1.0-06` KP-01 §3 KB-ORD-10 | SC-ORD-001, SC-ORD-002, SC-ORD-003 | — |
| REQ-ORD-002 | `ORD-02`, `US-D01` | `DOC-v1.0-01` §D3 L240 · §D1b L164 | SC-ORD-004 | — |
| REQ-ORD-003 | `ORD-01` (Loại hàng) | `DOC-v1.0-01` §D8.1 L357 · `DOC-v1.0-02` §3.5.1 · `DOC-v1.0-06` KP-01 §10.2/§10.3 | SC-ORD-005, SC-ORD-006, SC-ORD-007 | C-ORD-01, C-ORD-09 |
| REQ-ORD-004 | — (`D8.1` dòng Ghi chú) | `DOC-v1.0-01` §D8.1 L358 | SC-ORD-011 | — |
| REQ-ORD-005 | — (`D8.1` dòng Giá trị hàng) | `DOC-v1.0-01` §D8.1 L359 · `DOC-v1.0-06` KP-01 §3 KB-ORD-05 · §10.4 | SC-ORD-008, SC-ORD-009, SC-ORD-010 | C-ORD-01 |
| REQ-ORD-006 | — (`D8.1` dòng Ảnh sản phẩm) | `DOC-v1.0-01` §D8.1 L360 · `DOC-v1.0-02` §3.5.1 | SC-ORD-012, SC-ORD-013 | — |
| REQ-ORD-007 | — (`D8.1` nhóm NGƯỜI GỬI) | `DOC-v1.0-01` §D8.1 L362-364 · `DOC-v1.0-06` KP-01 §10.5/§10.6/§10.10 | SC-ORD-014, SC-ORD-015, SC-ORD-016, SC-ORD-017 | C-ORD-10 |
| REQ-ORD-008 | `USR-EML`, `US-D18` | `DOC-v1.0-01` §D3 L253 · §D1b L168 · §D8.1 L366 · `DOC-v1.0-06` KP-01 §10.8/§10.9 | SC-ORD-018, SC-ORD-019, SC-ORD-020, SC-ORD-021 | — |
| REQ-ORD-009 | — (`D8.1` nhóm NGƯỜI NHẬN) | `DOC-v1.0-01` §D8.1 L367-369 · `DOC-v1.0-02` §3.5.2 · §7 dòng 2 | SC-ORD-022, SC-ORD-023, SC-ORD-024 | C-ORD-01 |
| REQ-ORD-010 | `LOC-03` | `DOC-v1.0-01` §D3 L246 · `DOC-v1.0-06` KP-01 §3 KB-ORD-06 | SC-ORD-025, SC-ORD-026, SC-ORD-027 | C-ORD-11 |
| REQ-ORD-011 | — (`D8.1` dòng Từ/Đến ngày) | `DOC-v1.0-01` §D8.1 L370-371 | SC-ORD-028 | — |
| REQ-ORD-012 | — (`D8.1` dòng Khung giờ) | `DOC-v1.0-01` §D8.1 L372 · `DOC-v1.0-06` KP-01 §10.11 | SC-ORD-029, SC-ORD-030 | — |
| REQ-ORD-013 | `ORD-09` | `DOC-v1.0-01` §D3 L245 · §D8.1 L373 · `DOC-v1.0-02` §3.5.3 · `DOC-v1.0-06` KP-01 §10.7 | SC-ORD-031, SC-ORD-032, SC-ORD-033, SC-ORD-034 | C-ORD-12 |
| REQ-ORD-014 | `BR-ORD-04` | `DOC-v1.0-01` §D4 L263 · §A8 L115 · `DOC-v1.0-06` KP-01 §3 KB-ORD-03 | SC-ORD-035 | C-ORD-04 |
| REQ-ORD-015 | `US-D02` | `DOC-v1.0-01` §D1b L165 · `DOC-v1.0-02` §3.5.4 · `DOC-v1.0-04` (2 biến thể) | SC-ORD-036, SC-ORD-037, SC-ORD-038 | C-ORD-05 |
| REQ-ORD-016 | `ORD-01` (OFFER), `US-D10`, `US-D11` | `DOC-v1.0-01` §D3 L240 · §D1b L184-185 · §D8.2 L379-386 · `DOC-v1.0-02` §4.4 · `DOC-v1.0-06` KP-01 §3 KB-ORD-11 | SC-ORD-039, SC-ORD-040, SC-ORD-041, SC-ORD-042 | — |
| REQ-ORD-017 | `ORD-10`, `BR-EDIT-01`, `OPR-10`, `US-D19` | `DOC-v1.0-01` §D3 L252 · §D4 L269 · §D7 L346 · §D1b L169 | SC-ORD-043, SC-ORD-044 | — |
| REQ-ORD-018 | `ORD-06`, `US-D04` | `DOC-v1.0-01` §D3 L244 · §D1b L166 · `DOC-v1.0-06` KP-01 §3 KB-ORD-02 | SC-ORD-045 | C-ORD-03 |
| REQ-ORD-019 | `ORD-04` | `DOC-v1.0-01` §D3 L243 | SC-ORD-046 | — |
| REQ-ORD-020 | `VAL-01`, `VAL-02`, `VAL-03` | `DOC-v1.0-01` §D8.3 L392-394 | SC-ORD-047, SC-ORD-048, SC-ORD-049 | — |
| REQ-ORD-021 | — | `DOC-v1.0-06` KP-02 §5 dòng `C-ORD-08` | SC-ORD-050 | C-ORD-08 |
| REQ-ORD-022 | `BR-ORD-03` | `DOC-v1.0-01` §D4 L262 · §D5 L297 · `DOC-v1.0-06` KP-01 §3 KB-ORD-04 | SC-ORD-051 | C-ORD-02 |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-ORD-001 · Màn "Đăng tin mới" — chọn vai trò đăng
📍 `DOC-v1.0-02 §3.5 "Màn hình Đăng tin mới" · đoạn 1-3` · `DOC-v1.0-06 KP-01 §3 KB-ORD-10`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-02` §3.5:
> "Chọn vai trò đăng tin: Gửi hàng / Nhận giao hàng"
> ""Tôi cần gửi hàng" — Bạn có hàng cần gửi, tìm đồng nghiệp đi thuận đường mang hộ."

> Nguồn #2 — `DOC-v1.0-06` KP-01 §3 KB-ORD-10 (Figma + vibe-test):
> "Subtitle *"Bạn muốn làm gì?"* · card `Tôi cần gửi hàng` (icon hộp cam) · card `Tôi nhận giao hàng` (icon route tím) · banner cam kết nền vàng nhạt icon ⓘ (không phí / không chat / không thanh toán / SĐT lộ sau ghép) · cả 2 card bấm được."

↳ **Ghi chú:** 5 thành phần, có bằng chứng **2 nguồn** (Figma hash `f821ba30…` + vibe-test VR-002 `TC_04.1` PASS) ⇒ đủ điều kiện viết TC khẳng định theo `§Custom Rules §10.1`. Banner cam kết chứa câu *"SĐT lộ sau ghép"* — chính là rule mà `SC-FEED-010` chứng minh app đang vi phạm ở màn Chi tiết tin.

---

### REQ-ORD-002 · Wizard đăng tin NEED — 3 bước
📍 `DOC-v1.0-01 §D3 ORD-02 · L240` · `§D1b US-D01 · L164`  ·  Clarif: —

> Nguồn #1 — `ORD-02` (§D3 L240):
> "ORD-02 | Wizard đăng tin ngắn | B1 Loại tin+hàng → B2 Địa điểm/lộ trình+thời gian → B3 Xác nhận + đồng ý điều khoản"

> Nguồn #2 — `US-D01` (§D1b L164):
> "Wizard 3 bước; mỗi điểm lấy/giao chỉ có 1 input địa chỉ (không chip gợi ý); B3 bắt buộc tick đồng ý điều khoản mới cho phép đăng"

↳ **Ghi chú:** ⚠️ **Xung đột nội bộ BRD:** `US-D01` nói *"chỉ có 1 input địa chỉ (**không chip gợi ý**)"* nhưng `LOC-03` (§D3 L246) lại yêu cầu *"Hiển thị preset 6 văn phòng"* và `KB-ORD-06` xác nhận app **có dropdown autocomplete** ⇒ mở `C-ORD-11`. Wizard 3 bước là xương sống của module: `SC-ORD-004` là happy path P1 phủ cả 3 bước.

---

### REQ-ORD-003 · B1 — Loại hàng (chip single-select, có mặc định)
📍 `DOC-v1.0-01 §D8.1 · dòng "Loại hàng" · L357` · `DOC-v1.0-02 §3.5.1 dòng "Loại hàng"` · `DOC-v1.0-06 KP-01 §10.2/§10.3`  ·  Clarif: `C-ORD-01`, `C-ORD-09`

> Nguồn #1 — `DOC-v1.0-01` §D8.1 L357:
> "Loại hàng | Có | Tài liệu | Chọn 1 trong danh mục: Tài liệu · Đồ điện tử · Thực phẩm · Quà tặng · Khác. Không cho để trống"

> Nguồn #2 — `DOC-v1.0-02` §3.5.1:
> "Loại hàng | Chip chọn 1: Tài liệu (mặc định) · Đồ điện tử · Thực phẩm · Hàng nhỏ · Đồ dễ vỡ · Quần áo · Thuốc/Y tế · Khác"

> Nguồn #3 — `DOC-v1.0-06` KP-01 §10.2 `KB-VIBE-01` (app STG, có screenshot):
> "Chip mặc định được chọn là **`Giấy tờ, hồ sơ`**. Trong 8 lựa chọn thực tế **không tồn tại** chip nào tên "Tài liệu" — trong khi tài liệu/TC đợt cũ đều ghi "Tài liệu"."

> Nguồn #4 — `DOC-v1.0-06` KP-01 §10.3 `KB-VIBE-02`:
> "Tap lại chip đang chọn **không deselect được** → **không thể tái hiện trạng thái "chưa chọn Loại hàng"** qua UI. Thử để trống Loại hàng rồi bấm "Tiếp theo" → **chuyển bước bình thường, không bị chặn**."

↳ **Ghi chú:** ⭐ **Điểm sai lan rộng nhất của đợt v1.0 cũ.** Ba nguồn cho **3 danh mục khác nhau**: BRD 5 giá trị (có "Tài liệu"), PRD 8 chip (có "Tài liệu"), app STG 8 chip (**không** có "Tài liệu", mặc định `Giấy tờ, hồ sơ`) ⇒ `C-ORD-09` (mới). Thêm nữa, rule *"Không cho để trống"* (`C-ORD-01` Resolved: bắt buộc) **không kiểm chứng được qua UI** vì chip luôn có 1 giá trị mặc định ⇒ `SC-ORD-007` viết dạng GAP finding, ⛔ không viết TC negative "để trống Loại hàng → chặn".

---

### REQ-ORD-004 · B1 — Ghi chú (tuỳ chọn, ≤300 ký tự)
📍 `DOC-v1.0-01 §D8.1 · dòng "Ghi chú" · L358`  ·  Clarif: —

> "Ghi chú | Không | Trống | Tối đa 300 ký tự. Khuyến nghị nêu kích thước/khối lượng ước tính & lưu ý khi cầm giữ"

↳ **Ghi chú:** Boundary rõ: **300 hợp lệ / 301 chặn**. `DOC-v1.0-02` §3.5.1 xác nhận là `Textarea` có gợi ý placeholder. Trường tuỳ chọn ⇒ nhánh rỗng là đường đi thường gặp.

---

### REQ-ORD-005 · B1 — Giá trị hàng (bắt buộc) + cảnh báo khi "Cao"
📍 `DOC-v1.0-01 §D8.1 · dòng "Giá trị hàng" · L359` · `DOC-v1.0-06 KP-01 §3 KB-ORD-05` · `§10.4 KB-VIBE-03`  ·  Clarif: `C-ORD-01`

> Nguồn #1 — `DOC-v1.0-01` §D8.1 L359:
> "Giá trị hàng | Có | Trống (chưa chọn) | Chọn 1: Giá trị thấp / vừa / cao. Chọn Giá trị cao → hiện cảnh báo trách nhiệm tự thoả thuận"

> Nguồn #2 — `DOC-v1.0-06` KP-01 §3 `KB-ORD-05` (nguyên văn banner trên app thật):
> "Chọn `Thấp` / `Vừa` → **không** có banner. Chọn `Cao` → hiện banner, nguyên văn xác nhận trên app thật:"
> "*"Hàng giá trị cao: hai bên tự thoả thuận và chịu trách nhiệm với nhau. FoxEco không bảo hiểm, không đứng ra vận chuyển hay bồi thường."*"

> Nguồn #3 — `DOC-v1.0-06` KP-01 §10.4 `KB-VIBE-03`:
> "Để trống Giá trị hàng → nút "Tiếp theo" chuyển màu nhạt/disabled, không chuyển bước."

↳ **Ghi chú:** Trường **duy nhất ở B1 kiểm chứng được rule "bắt buộc"** (mặc định trống thật, và app chặn thật — VR-002 `TC_04.7` PASS). Banner cảnh báo có **nguyên văn xác nhận trên app** (VR-002 `TC_04.8/9/10` PASS) ⇒ assert được text. Fan-out 3 SC: bắt buộc (negative) · `Cao` → banner · `Thấp`/`Vừa` → không banner.

---

### REQ-ORD-006 · B1 — Ảnh sản phẩm (tuỳ chọn, 1 ảnh ≤5MB JPG/PNG)
📍 `DOC-v1.0-01 §D8.1 · dòng "Ảnh sản phẩm" · L360`  ·  Clarif: —

> "Ảnh sản phẩm | Không | Trống | Chỉ 1 ảnh duy nhất, ≤ 5MB, định dạng JPG/PNG. Khuyến nghị có ảnh để người giao dễ nhận"

↳ **Ghi chú:** 3 ràng buộc kiểm chứng được: **số lượng** (1), **kích thước** (≤5MB), **định dạng** (JPG/PNG). `DOC-v1.0-02` §3.5.1 bổ sung 2 nguồn ảnh (chụp mới / chọn thư viện). Là trường tuỳ chọn ⇒ `SC-ORD-013` assert bỏ trống vẫn qua bước. Ảnh này cũng là nguồn cho `SC-FEED-008` (ảnh mặc định khi không có ảnh).

---

### REQ-ORD-007 · B2 — Nhóm NGƯỜI GỬI (auto-fill từ tài khoản)
📍 `DOC-v1.0-01 §D8.1 · nhóm "NGƯỜI GỬI" · L362-364` · `DOC-v1.0-06 KP-01 §10.5/§10.6/§10.10`  ·  Clarif: `C-ORD-10`

> Nguồn #1 — `DOC-v1.0-01` §D8.1 L362-364:
> "Tên người gửi | Có | Điền sẵn từ tài khoản đăng nhập | Chỉ đọc (lấy từ hồ sơ nhân viên)"
> "SĐT người gửi | Có | Điền sẵn từ tài khoản | SĐT VN hợp lệ; chỉ lộ cho bên còn lại sau khi ghép"
> "Địa chỉ lấy hàng | Có | Tòa nhà Lô B3, KCX Tân Thuận, Q.7 (điền sẵn từ nơi làm việc của user) | Không để trống, tối đa 200 ký tự"

> Nguồn #2 — `DOC-v1.0-06` KP-01 §10.5 `KB-VIBE-04` (🔴 nghi vấn BUG):
> "Chạm vào field → **mở được bàn phím** (không disabled)"
> "Giá trị "Chung Hoàng Liêm" bị **XOÁ TRẮNG ngay sau khi chạm**"

> Nguồn #3 — `DOC-v1.0-06` KP-01 §10.6 `KB-VIBE-05` (🔴):
> "Expected (spec): mặc định `Tòa nhà Lô B3, KCX Tân Thuận, Q.7`. Thực tế: **field trống, chỉ có placeholder**. Tên ✅ và SĐT ✅ vẫn pre-fill đúng."

> Nguồn #4 — `DOC-v1.0-06` KP-01 §10.10 `KB-VIBE-09` (🟡):
> "SĐT Người gửi thay đổi giữa 2 screenshot cùng một phiên (`0000142378` → `0964633313`) mà **không có thao tác nào của user** trên field đó."

↳ **Ghi chú:** ⭐ REQ mang **3 nghi vấn bug đã có screenshot** mà đợt cũ chưa log: (a) Tên **không read-only** và bị xoá trắng khi chạm (VR-002 `TC_04.22` FAIL); (b) Địa chỉ lấy hàng **không pre-fill** (VR-002 `TC_04.21` FAIL — ⚠️ chưa loại trừ khả năng **tài khoản test chưa cấu hình địa chỉ**, cần dev xác nhận ⇒ `C-ORD-10`); (c) SĐT tự đổi giá trị giữa phiên. Cả 3 viết thành SC theo **spec** (dự kiến FAIL) chứ không theo hành vi app.

---

### REQ-ORD-008 · B2 — Email công ty người nhận → tra danh bạ nội bộ
📍 `DOC-v1.0-01 §D3 USR-EML · L253` · `§D1b US-D18 · L168` · `§D8.1 L366` · `DOC-v1.0-06 KP-01 §10.8/§10.9`  ·  Clarif: —

> Nguồn #1 — `USR-EML` (§D3 L253):
> "USR-EML | Tự điền người nhận từ email công ty | Tra danh bạ nội bộ; khớp → tự điền tên/SĐT/địa chỉ; không khớp → nhập tay"

> Nguồn #2 — `US-D18` (§D1b L168):
> "Ô "Email công ty người nhận" nằm đầu mục Người nhận; nhập email có trong hệ thống → tự điền tên/SĐT/địa chỉ + báo "Đã tìm thấy trong hệ thống nội bộ"; không có → báo "Không tìm thấy · nhập thủ công""

> Nguồn #3 — `DOC-v1.0-01` §D8.1 L366:
> "Email công ty người nhận | Có | Trống | Đúng định dạng email & thuộc tên miền nội bộ. Tra danh bạ: tìm thấy → tự điền tên/SĐT/địa chỉ; không thấy → cảnh báo & cho nhập thủ công"

> Nguồn #4 — `DOC-v1.0-06` KP-01 §10.9 `KB-VIBE-08` (🔴 nghi vấn bug):
> "Auto-fill từ `stag_anhdc4@fpt.com` trả về SĐT người nhận `0000286248` → **chính app báo "Số điện thoại không hợp lệ"** cho giá trị do nó tự điền."

↳ **Ghi chú:** **3 nguồn đồng thuận** về cơ chế 2 chiều, và `US-D18` cho **nguyên văn 2 thông báo** ⇒ assert được text. Vibe-test VR-001 #3 + VR-002 `TC_04.24` PASS xác nhận hoạt động đúng cả 2 chiều. Nhưng phát sinh nghịch lý: app **tự điền** SĐT rồi **tự báo lỗi** SĐT đó ⇒ `SC-ORD-021` (P2, dự kiến FAIL). Fan-out 4 SC: tìm thấy · không tìm thấy · sai định dạng/ngoài tên miền · nghịch lý auto-fill.

---

### REQ-ORD-009 · B2 — Nhóm NGƯỜI NHẬN (bắt buộc, validate từng trường)
📍 `DOC-v1.0-01 §D8.1 · nhóm "NGƯỜI NHẬN" · L367-369` · `DOC-v1.0-02 §3.5.2` · `§7 dòng 2`  ·  Clarif: `C-ORD-01`

> Nguồn #1 — `DOC-v1.0-01` §D8.1 L367-369:
> "Tên người nhận | Có | Tự điền từ danh bạ | Không để trống, 2–60 ký tự"
> "Số điện thoại | Có | Tự điền từ danh bạ | Số điện thoại VN hợp lệ (10 số, đầu 0). Chỉ lộ cho bên còn lại sau khi ghép"
> "Địa chỉ giao hàng | Có | Trống — tự điền theo địa chỉ người nhận khi tra được email nội bộ | Không để trống; phải khác địa chỉ lấy hàng"

> Nguồn #2 — HÀNH VI PROTOTYPE (`DOC-v1.0-02` §7 dòng 2):
> "2 | Không có validate bắt buộc | Tên/SĐT/địa chỉ Người nhận có thể để trống hoàn toàn mà vẫn đăng tin thành công."

> Nguồn #3 — PHÁN QUYẾT (`DOC-v1.0-06` KP-01 §3 KB-ORD-01):
> "BA/PO xác nhận (2026-07-27) **CÓ** rule bắt buộc — trái với prototype (cho để trống tất cả): … Bước 2: thông tin `Người nhận` bắt buộc"

↳ **Ghi chú:** `C-ORD-01` Resolved: **CÓ** rule bắt buộc ⇒ `SC-ORD-022` assert chặn khi bỏ trống, **dự kiến FAIL nếu app còn hành vi prototype**. Ba boundary rõ: Tên `2..60`, SĐT `10 số đầu 0`, Địa chỉ giao **phải khác** địa chỉ lấy. Fan-out gộp **validate field** thành 1 SC (`SC-ORD-023`) — EP/BVA từng trường là việc của `generate-tc` (rubric B1/B2), xem `CHANGELOG §2` ràng buộc 8.

---

### REQ-ORD-010 · B2 — Địa chỉ: autocomplete văn phòng + preset 6 văn phòng FPT
📍 `DOC-v1.0-01 §D3 LOC-03 · L246` · `DOC-v1.0-06 KP-01 §3 KB-ORD-06`  ·  Clarif: `C-ORD-11`

> Nguồn #1 — `LOC-03` (§D3 L246):
> "LOC-03 | Quick-select văn phòng FPT | Hiển thị preset 6 văn phòng (+ mở rộng theo tỉnh)"

> Nguồn #2 — `DOC-v1.0-06` KP-01 §3 `KB-ORD-06` (BA + vibe-test):
> "Gõ text tự do → hiện dropdown gợi ý danh sách văn phòng khớp từ DB, **không phân biệt hoa/thường**. **Phải chạm chọn gợi ý** thì giá trị mới được lưu; gõ text mà không chọn thì field không giữ giá trị."

> Nguồn #3 — XUNG ĐỘT (`DOC-v1.0-01` §D1b `US-D01` L164):
> "mỗi điểm lấy/giao chỉ có 1 input địa chỉ (không chip gợi ý)"

↳ **Ghi chú:** ⚠️ **Ba cơ chế khác nhau cho cùng 1 field:** `LOC-03` = **preset 6 văn phòng** (quick-select), `KB-ORD-06` = **dropdown autocomplete tra DB**, `US-D01` = **chỉ 1 input, không chip gợi ý**. `KB-ORD-06` có bằng chứng mạnh nhất (BA trả lời 2026-07-29 + VR-001 #5 + VR-002 `TC_04.29` PASS) ⇒ SC viết theo autocomplete; **preset 6 văn phòng** chỉ được 1 SC dạng GAP (`SC-ORD-027`). Mở `C-ORD-11`. ⚠️ **Hệ quả automation:** phải tap suggestion tường minh, không set text.

---

### REQ-ORD-011 · B2 — Từ ngày / Đến ngày
📍 `DOC-v1.0-01 §D8.1 · dòng "Từ ngày"/"Đến ngày" · L370-371`  ·  Clarif: —

> "Từ ngày | Có | Ngày hiện tại | Thời gian bắt đầu có thể gửi hàng. Không chọn ngày trong quá khứ"
> "Đến ngày | Có | Ngày hiện tại | Thời hạn cuối cùng để gửi hàng. Phải ≥ Từ ngày. Quá ngày này mà chưa ghép → tin tự chuyển trạng thái Hết hạn (xem OPR-04 & NTF-09)"

↳ **Ghi chú:** 3 rule: default = hôm nay · không quá khứ · `Đến ≥ Từ` (biên: **bằng nhau = hợp lệ**). Dòng "Đến ngày" đồng thời là **nguồn của `REQ-ORD-018`** (hết hạn) — khớp `C-ORD-03` Resolved (hạn tin = giá trị "Đến ngày" user chọn, không phải hằng số hệ thống).

---

### REQ-ORD-012 · B2 — Khung giờ mong muốn
📍 `DOC-v1.0-01 §D8.1 · dòng "Khung giờ (từ – đến)" · L372` · `DOC-v1.0-06 KP-01 §10.11`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-01` §D8.1 L372:
> "Khung giờ (từ – đến) | Có | 17:00 – 18:30 | đến > từ; khoảng tối thiểu 30 phút"

> Nguồn #2 — `DOC-v1.0-06` KP-01 §10.11 `KB-VIBE-10`:
> "Giá trị mặc định (vd 11:10–11:40) **hết hạn** khi form mở lâu (~15 phút), app tự bật validate *"phải muộn hơn hiện tại"*. **Không phải lỗi app.**"

↳ **Ghi chú:** ⚠️ **Hai rule, hai nguồn:** doc cho biên **≥30 phút** (biên: 29 chặn / 30 hợp lệ); vibe-test phát hiện thêm rule **"phải muộn hơn hiện tại"** không có trong doc. Lưu ý mặc định của doc (`17:00–18:30`) khác PRD (`05:00 PM–06:30 PM` — cùng giá trị, khác cách viết) và khác app (`11:10–11:40` trong 1 phiên) ⇒ **⛔ không hardcode giờ**, chọn khung tương đối so với "now" (`Project_rule §Test Data Rules`).

---

### REQ-ORD-013 · B3 — Tóm tắt + banner hàng cấm + consent điều khoản
📍 `DOC-v1.0-01 §D3 ORD-09 · L245` · `§D8.1 L373` · `DOC-v1.0-02 §3.5.3` · `DOC-v1.0-06 KP-01 §10.7`  ·  Clarif: `C-ORD-12`

> Nguồn #1 — `ORD-09` (§D3 L245):
> "ORD-09 | Consent điều khoản trước khi đăng | Bắt buộc tick "đồng ý tự chịu trách nhiệm""

> Nguồn #2 — `DOC-v1.0-01` §D8.1 L373:
> "Xác nhận điều khoản | Có | **Chưa tick** | Bắt buộc tick mới bật được nút Đăng tin (tự thoả thuận, app không bảo hiểm/không vận chuyển)"

> Nguồn #3 — `DOC-v1.0-02` §3.5.3 (MÂU THUẪN):
> "Checkbox điều khoản | **Mặc định đã tick sẵn** — "Tôi tự chịu trách nhiệm về hàng hoá và thoả thuận với người mang giúp""

> Nguồn #4 — `DOC-v1.0-06` KP-01 §10.7 `KB-VIBE-06` (app thật):
> "Quan sát thực tế ở Bước 3/3: **chưa tick**, phải chạm tay mới bật được nút "Đăng tin ngay"."

↳ **Ghi chú:** ⭐ **Mâu thuẫn giá trị mặc định:** `D8.1` + app STG = **chưa tick**; PRD demo = **đã tick sẵn**. BRD (mới hơn) + app (bằng chứng thật) đồng thuận ⇒ chốt **chưa tick**; TC `TC_04.71` của đợt cũ expected *"tick sẵn"* là **sai nguồn** (`KP-04 §4` đã ghi nhận). Mở `C-ORD-12` để BA xác nhận chính thức. `SC-ORD-034` (P1) assert không tick → chặn đăng.

---

### REQ-ORD-014 · Hàng cấm — KHÔNG bị chặn ở v1.0
📍 `DOC-v1.0-01 §D4 BR-ORD-04 · L263` · `§A8 · L115` · `DOC-v1.0-06 KP-01 §3 KB-ORD-03`  ·  Clarif: `C-ORD-04`

> Nguồn #1 — RULE (`BR-ORD-04` §D4 L263):
> "BR-ORD-04 | Hàng cấm không được đăng"

> Nguồn #2 — RULE (`DOC-v1.0-01` §A8 L115):
> "Hàng cấm (thuốc, vũ khí, chất nguy hiểm, phi pháp) không được đăng."

> Nguồn #3 — PHÁN QUYẾT (`DOC-v1.0-06` KP-01 §3 `KB-ORD-03`):
> "Chip "Thuốc/Y tế" vẫn chọn được bình thường dù nguyên tắc cấm gửi thuốc. Banner cảnh báo chỉ là **thông tin tĩnh**, không có validate chặn theo danh mục."

↳ **Ghi chú:** `C-ORD-04` Resolved 2026-07-27: **v1.0 không chặn** — banner chỉ là thông tin tĩnh. ⇒ ⛔ **KHÔNG viết TC negative "chọn Thuốc/Y tế → bị chặn"** (đợt cũ đã tránh đúng chỗ này). `SC-ORD-035` ghi nhận trạng thái: chọn chip hàng cấm **vẫn đăng được**, để version sau có mốc so sánh nếu rule được bật.

---

### REQ-ORD-015 · Màn "Đăng tin thành công" — mã tin 2 biến thể
📍 `DOC-v1.0-01 §D1b US-D02 · L165` · `DOC-v1.0-02 §3.5.4` · `DOC-v1.0-04` (2 biến thể trên cùng board)  ·  Clarif: `C-ORD-05`

> Nguồn #1 — `US-D02` (§D1b L165):
> "Sau khi bấm "Đăng tin ngay" → màn "Đăng tin thành công" (**KHÔNG hiển thị mã đơn** — mã kỹ thuật vô nghĩa với người dùng); tin xuất hiện ở "Đơn của tôi" trên trang chủ"

> Nguồn #2 — `DOC-v1.0-02` §3.5.4:
> "Đăng tin thành công — 2 lựa chọn: Theo dõi đơn / Về trang chủ"

> Nguồn #3 — MÂU THUẪN (`DOC-v1.0-06` KP-05 §2.2):
> "Một bản **CÓ** trường "Mã tin" (vd `#ECO-2026-0451`), một bản **KHÔNG**. Đồng thời đối lập trực tiếp với `US-D02`"

↳ **Ghi chú:** `C-ORD-05` **Open** — mâu thuẫn **ngay trong nguồn thiết kế** (2 biến thể trên cùng board Figma) và đối lập với `US-D02`. ⇒ `SC-ORD-037` (2 lựa chọn điều hướng) viết TC khẳng định; `SC-ORD-038` (mã tin) là GAP finding **cố ý không assert có/không có mã**. `SC-ORD-036` assert tin xuất hiện ở "Đơn của tôi" (bề mặt thuộc `HOME`/`ACT`, nhưng **hệ quả của hành động đăng tin** nên giữ ở `ORD`).

---

### REQ-ORD-016 · Form OFFER 1 trang + màn "Đã ghi nhận tuyến đường"
📍 `DOC-v1.0-01 §D3 ORD-01 · L240` · `§D1b US-D10/US-D11 · L184-185` · `§D8.2 · L379-386` · `DOC-v1.0-02 §4.4` · `DOC-v1.0-06 KP-01 §3 KB-ORD-11`  ·  Clarif: —

> Nguồn #1 — `US-D10` (§D1b L184):
> "Màn đăng tin OFFER 1 màn duy nhất, các trường: Điểm xuất phát, Điểm đến, Khung giờ, Tên, SĐT + tick đồng ý điều khoản; có dòng chú thích mô tả đang di chuyển & có thể nhận giao hộ"

> Nguồn #2 — `US-D11` (§D1b L185):
> "Sau khi đăng → màn "Đã ghi nhận tuyến đường" giải thích: tuyến được lưu (không công khai), khi có người cần gửi trùng điểm lấy & điểm giao hệ thống sẽ gửi thông báo để bạn xem xét"

> Nguồn #3 — `DOC-v1.0-01` §D8.2 L381-382:
> "Điểm xuất phát | Có | Điền sẵn vị trí làm việc của người giao (lấy từ hồ sơ nhân viên); để trống nếu hệ thống chưa có thông tin | Không để trống khi submit, tối đa 200 ký tự. User sửa được"
> "Điểm đến | Có | Trống | Không để trống; phải khác điểm xuất phát"

> Nguồn #4 — `DOC-v1.0-06` KP-01 §3 `KB-ORD-11` (app thật):
> "Bấm `Tôi nhận giao hàng` → form một trang, **không có step indicator "Bước x/3"**."

↳ **Ghi chú:** Luồng OFFER khác NEED ở 3 điểm: **1 trang** (không wizard) · **không lên bảng tin** · **màn kết quả khác** ("Đã ghi nhận tuyến đường"). Đáng chú ý: `D8.2` cho phép **user sửa được** Điểm xuất phát (khác `D8.1` nơi Tên người gửi là *"Chỉ đọc"*) và cho phép **để trống nếu hệ thống chưa có thông tin** — tức spec **đã lường trước** việc pre-fill có thể không có, khác với `D8.1` Địa chỉ lấy hàng (`SC-ORD-016`). Fan-out 4 SC.

---

### REQ-ORD-017 · Sửa tin — chỉ khi "Chờ ghép", khoá từ "Đã ghép"
📍 `DOC-v1.0-01 §D3 ORD-10 · L252` · `§D4 BR-EDIT-01 · L269` · `§D7 OPR-10 · L346` · `§D1b US-D19 · L169`  ·  Clarif: —

> Nguồn #1 — `ORD-10` (§D3 L252):
> "ORD-10 | Chỉnh sửa tin khi "Chờ ghép" | Form điền sẵn; chỉ trạng thái POSTED; có "Cập nhật" & "Huỷ chỉnh sửa""

> Nguồn #2 — `BR-EDIT-01` (§D4 L269):
> "BR-EDIT-01 | Chỉ được chỉnh sửa tin khi còn "Chờ ghép" (POSTED); đã MATCHED trở đi khoá chỉnh sửa"

> Nguồn #3 — `OPR-10` (§D7 L346):
> "OPR-10 | Điều kiện chỉnh sửa đơn | Chỉ được sửa đơn khi chưa có ai nhận (trạng thái "Chờ ghép"); ngay khi đã có người nhận (Đã ghép trở đi) → khoá chỉnh sửa hoàn toàn"

> Nguồn #4 — `US-D19` (§D1b L169):
> "Nút "Chỉnh sửa" chỉ hiện ở trạng thái Chờ ghép (POSTED); mở màn giống tạo đơn nhưng đã điền sẵn; có nút "Cập nhật" & "Huỷ chỉnh sửa"; sau IN_TRANSIT không cho sửa"

↳ **Ghi chú:** **4 nguồn đồng thuận** — rule mạnh nhất module. ⚠️ Nhưng `US-D19` ghi *"sau **IN_TRANSIT** không cho sửa"* trong khi 3 nguồn kia ghi *"từ **MATCHED** trở đi khoá"* ⇒ **lệch 1 trạng thái**; lấy `BR-EDIT-01`+`OPR-10` (rule chuyên trách, 2 nguồn) làm chuẩn: **khoá từ MATCHED**. Ghi lệch vào `CHANGELOG §2`. Lưu ý `ORD-10` thuộc nhóm **out of scope Phase 1** theo PM (`KP-03 §3.1`) nhưng scope lượt này = **toàn bộ 11 module** (quyết định 2026-09-07) ⇒ vẫn phân tích.

---

### REQ-ORD-018 · Tin tự hết hạn theo "Đến ngày"
📍 `DOC-v1.0-01 §D3 ORD-06 · L244` · `§D1b US-D04 · L166` · `DOC-v1.0-06 KP-01 §3 KB-ORD-02`  ·  Clarif: `C-ORD-03`

> Nguồn #1 — `ORD-06` (§D3 L244):
> "ORD-06 | Tin hết hạn | Quá hạn chưa ghép → gửi thông báo để người đăng tự gỡ/đăng lại; hệ thống không tự can thiệp ở phase này"

> Nguồn #2 — `US-D04` (§D1b L166):
> "Quá hạn cấu hình mà chưa MATCHED → tự chuyển EXPIRED, hiển thị badge "Hết hạn" ở tab hoàn tất kèm lý do "Không có ai nhận mang giúp trong thời gian đăng""

> Nguồn #3 — PHÁN QUYẾT (`DOC-v1.0-06` KP-01 §3 `KB-ORD-02`):
> "BRD `ORD-06` chỉ ghi *"quá hạn cấu hình"* không có con số. BA/PO xác nhận: hạn tin **không phải hằng số hệ thống** — bằng đúng khoảng ngày user chọn ở Bước 2/3; đến đúng **"Đến ngày"** thì tin tự chuyển `EXPIRED`."

↳ **Ghi chú:** ⚠️ **`ORD-06` và `US-D04` mô tả 2 hành vi khác nhau:** `ORD-06` nói *"hệ thống **không tự can thiệp**"* (chỉ gửi thông báo để user tự gỡ), `US-D04` nói *"**tự chuyển** EXPIRED"*. `C-ORD-03` Resolved chốt theo `US-D04` + app: tin **tự chuyển** Hết hạn tại "Đến ngày". Ghi lệch vào `CHANGELOG §2` ràng buộc 7. Lý do hiển thị có **nguyên văn** ở `US-D04` và `KB-ORD-07` (#4) ⇒ assert được text. Bề mặt badge/lý do ở tab "Đã hoàn thành" thuộc `ACT` (`SC-ACT-008`).

---

### REQ-ORD-019 · Timeline tin ghi nhận mốc thời gian
📍 `DOC-v1.0-01 §D3 ORD-04 · L243`  ·  Clarif: —

> "ORD-04 | Tin có timeline trạng thái | Lịch sử đầy đủ với timestamp"

↳ **Ghi chú:** Rule ngắn, nhưng là **nền của cả traceability nghiệp vụ** — cross-ref `TS-01`/`TS-02` (`REQ-TS-001/002`: log không sửa được) và `US-D09` (5 mốc). Bề mặt hiển thị timeline ở màn Theo dõi đơn thuộc `DLV` (`REQ-DLV-010`); SC ở đây assert **đơn vừa đăng đã có mốc "Đăng tin" kèm timestamp**.

---

### REQ-ORD-020 · Quy tắc chung cho form (`VAL-01`/`VAL-02`/`VAL-03`)
📍 `DOC-v1.0-01 §D8.3 · L392-394`  ·  Clarif: —

> "VAL-01 | Nút submit vô hiệu hoá đến khi mọi trường bắt buộc hợp lệ + đã tick điều khoản"
> "VAL-02 | Lỗi hiện ngay dưới ô nhập khi rời ô (on blur), không dùng popup; cuộn tới ô lỗi đầu tiên khi bấm submit"
> "VAL-03 | Tự cắt khoảng trắng đầu/cuối; chuẩn hoá SĐT (bỏ khoảng trắng, dấu chấm) trước khi lưu"

↳ **Ghi chú:** 3 rule **cross-field**, áp cho **cả 2 form** (NEED wizard + OFFER) ⇒ 3 SC riêng, mỗi SC nêu rõ áp cho form nào. `VAL-01` đã được vibe-test xác nhận đúng ở B1 (`KB-VIBE-03`: để trống Giá trị hàng → nút disabled). `VAL-04` (lý do huỷ ≥5 ký tự) **không** thuộc module này — home ở `CNL` (`REQ-CNL-002`).

---

### REQ-ORD-021 · Reset / thoát giữa wizard
📍 `DOC-v1.0-06 KP-02 §5 · dòng "C-ORD-08"`  ·  Clarif: `C-ORD-08`

> "**C-ORD-08** | Bấm Reset/thoát giữa chừng wizard có xoá dữ liệu form đã nhập không? | Chưa hỏi BA. Không có mô tả trong BRD/PRD"

↳ **Ghi chú:** *(Implicit — không có quote đặc tả.)* Không doc nào mô tả hành vi khi thoát giữa wizard 3 bước. Đây là hành vi **thường gặp trong thực tế sử dụng** nên không bỏ qua được ⇒ `SC-ORD-050` viết dạng ghi nhận. Liên quan `KB-VIBE-04`: Tên người gửi bị xoá trắng và *"**không tự phục hồi** trong cùng phiên wizard — phải thoát ra vào lại từ đầu Bước 1/3"* ⇒ hành vi thoát/vào lại **có** ảnh hưởng dữ liệu form, càng cần chốt.

---

### REQ-ORD-022 · Ngưỡng giá trị hàng bằng số tiền — out of scope v1.0
📍 `DOC-v1.0-01 §D4 BR-ORD-03 · L262` · `§D5 · L297` · `DOC-v1.0-06 KP-01 §3 KB-ORD-04`  ·  Clarif: `C-ORD-02`

> Nguồn #1 — `BR-ORD-03` (§D4 L262):
> "BR-ORD-03 | Giá trị hàng trong ngưỡng cấu hình; trên ngưỡng → cảnh báo nên mua bảo hiểm (phase sau)"

> Nguồn #2 — `DOC-v1.0-01` §D5 L297:
> "Hàng giá trị cao | Cảnh báo nên mua bảo hiểm bên thứ 3 (phase sau)"

> Nguồn #3 — PHÁN QUYẾT (`DOC-v1.0-06` KP-01 §3 `KB-ORD-04`):
> "`BR-ORD-03` (ngưỡng giá trị + bắt buộc ảnh khi vượt ngưỡng) **chưa làm ở phase này**. Riêng cơ chế cảnh báo theo mức `Cao` thì **CÓ** (xem KB-ORD-05)."

↳ **Ghi chú:** ⚠️ **Phân biệt 2 thứ dễ lẫn:** ngưỡng **bằng số tiền** (`BR-ORD-03`) = **out of scope v1.0** (`C-ORD-02` Resolved — từng là BLOCKER cứng, gỡ 2026-07-27) ≠ cảnh báo theo **mức định tính "Cao"** (`REQ-ORD-005`) = **CÓ ở v1.0**. `SC-ORD-051` chỉ ghi nhận gap, ⛔ không viết TC nhập số tiền.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
