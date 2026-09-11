# Requirement Traceability — v1.0 · Module USR

> Tạo bởi: analyze-requirements (INIT 2026-09-07) · layout **module-first v2**.
> Ma trận truy vết REQ ↔ DOC ↔ Scenario ↔ Clarification. **Home của Source Quote per REQ = §2 file này.**
> SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation: FR/VR` (doc-native, module-prefixed) ⇒ dùng **Schema A**, cột `Maps (Ref DOC)` ghi **ID gốc** của doc.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module USR — DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-04 · DOC-v1.0-06

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-USR-001 | `USR-01` | `DOC-v1.0-01` §A6 (L99) | SC-USR-001 | — |
| REQ-USR-002 | `USR-02` | `DOC-v1.0-01` §A6 (L100) · `DOC-v1.0-06` KP-01 §2 KB-USR-01 | SC-USR-002, SC-USR-003 | C-USR-03 |
| REQ-USR-003 | `USR-04` | `DOC-v1.0-01` §A6 (L101) · `DOC-v1.0-02` §1.1 | SC-USR-004 | — |
| REQ-USR-004 | `USR-05`, `US-D20` | `DOC-v1.0-01` §A6 (L102) · §A7 (L110-111) · §D1b (L196) | SC-USR-005, SC-USR-006 | C-USR-01 |
| REQ-USR-005 | `USR-07` | `DOC-v1.0-01` §A6 (L103) | SC-USR-010 | C-USR-02 |
| REQ-USR-006 | `US-D20` | `DOC-v1.0-02` §3.9 · `DOC-v1.0-06` KP-01 §2 KB-USR-04 | SC-USR-008, SC-USR-009, SC-USR-012 | C-USR-04 |
| REQ-USR-007 | — (không có ID doc gốc — bảng §3.9 không đánh số) | `DOC-v1.0-02` §3.9 · `DOC-v1.0-04` (2 ảnh màn Cá nhân) | SC-USR-007, SC-USR-011 | C-USR-01 |

> Cột `Maps (Ref DOC)` dùng ID gốc của doc, KHÔNG quy đổi sang FR/VR chuẩn hoá (`Project_rule.md §DOC Notation`).
> `DOC-v1.0-01` là Markdown ⇒ anchor dùng số dòng `L<n>`; `DOC-v1.0-02` là `.docx` ⇒ anchor dùng `§section` + tên dòng bảng (tra bằng `scripts/doc/search-doc.sh`).

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-USR-001 · Đăng nhập SSO nội bộ FPT
📍 `DOC-v1.0-01 §A6 "Tài khoản & Hồ sơ (USR)" · bảng ID/Yêu cầu · L99`  ·  Clarif: —

> "USR-01 | Đăng nhập SSO nội bộ FPT → JWT, role, profile"

↳ **Ghi chú:** Định danh bằng SSO nội bộ FPT, trả về JWT + role + profile. **Implicit:** FoxEco là SDK nhúng trong host app `FoxPro_Stag` (`DOC-v1.0-06` KP-03 §1) ⇒ bề mặt đăng nhập **thuộc host app**, không nằm trong SDK. Test phía QC chỉ verify được **hệ quả**: vào được SDK với đúng danh tính (tên/phòng ban/MNV hiển thị ở màn Cá nhân). Liên quan `NT-07` (§A2 L19 — "Định danh & tin cậy").

---

### REQ-USR-002 · Hồ sơ cá nhân — view-only, KHÔNG có chức năng sửa
📍 `DOC-v1.0-01 §A6 · L100` · `DOC-v1.0-06 KP-01 §2 KB-USR-01`  ·  Clarif: `C-USR-03`

> Nguồn #1 — `DOC-v1.0-01` §A6 L100:
> "USR-02 | Xem/cập nhật hồ sơ: tên, SĐT, avatar, phòng ban, khu vực/văn phòng, kênh liên hệ"

> Nguồn #2 — `DOC-v1.0-06` KP-01 §2 KB-USR-01 (phán quyết chốt):
> "BRD (`USR-02`) ghi *"Xem/cập nhật hồ sơ"* (tên, SĐT, avatar, phòng ban, khu vực, kênh liên hệ). **Thực tế app STG KHÔNG có bất kỳ chức năng cập nhật/sửa nào** — cả 6 trường đều chỉ để xem."

↳ **Ghi chú:** Doc nêu 6 trường hồ sơ và động từ *"Xem/cập nhật"*; QA xác nhận trực tiếp trên app STG là **view-only hoàn toàn** (`C-USR-03` Resolved 2026-07-24). ⇒ Viết TC cho **hiển thị** 6 trường + TC negative khẳng định **không có control sửa**; ⛔ KHÔNG viết TC luồng edit profile. Áp `Project_rule §Custom Rules §10.1` (UI thắng khi doc mô tả chức năng không tồn tại trên UI).

---

### REQ-USR-003 · Hiển thị phòng ban + khu vực/tỉnh
📍 `DOC-v1.0-01 §A6 · L101` · `DOC-v1.0-02 §1.1 "Bối cảnh & vấn đề"`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-01` §A6 L101:
> "USR-04 | Hiển thị phòng ban + khu vực/tỉnh (tin cậy + ghép địa lý)"

> Nguồn #2 — `DOC-v1.0-02` §1.1:
> "mỗi tài khoản gắn với Phòng ban và Mã nhân viên (MNV) — ví dụ "Phòng Kỹ thuật · MNV: FTEL2291""

↳ **Ghi chú:** Hai nguồn đồng thuận về phòng ban; `DOC-v1.0-02` bổ sung **MNV** (BRD không nhắc) và cho **định dạng hiển thị** `"<Phòng ban> · MNV: <mã>"`. Mục đích nghiệp vụ theo BRD: tăng tin cậy + phục vụ ghép địa lý (`NT-06` §A2 L18).

---

### REQ-USR-004 · Đúng 2 chỉ số (đơn đã giúp + quà đã nhận) — KHÔNG điểm/tier/CO₂
📍 `DOC-v1.0-01 §A6 · L102` · §A7 · L110-111 · `DOC-v1.0-01 §D1b US-D20 · L196`  ·  Clarif: `C-USR-01`

> Nguồn #1 — `DOC-v1.0-01` §A6 L102:
> "USR-05 | Hiển thị tổng số đơn đã giúp + tổng số quà ảo đã nhận (không tính điểm/CO₂)"

> Nguồn #2 — `DOC-v1.0-01` §A7 L110-111:
> "Trang cá nhân tổng hợp tổng số đơn đã giúp + số quà ảo đã nhận (đếm theo loại) + lịch sử nhận quà"
> "Không tính điểm, không tier/xếp hạng, không CO₂, không quy đổi tiền / thanh toán in-app"

> Nguồn #3 — `DOC-v1.0-02` §3.9 · bảng Trường/Thành phần · dòng "3 chỉ số" (nguồn MÂU THUẪN):
> "3 chỉ số | Đơn đã giúp (12) · Điểm uy tín (4.8) · Điểm ECO (540)"

↳ **Ghi chú:** BRD (`DOC-v1.0-01`, bản mới hơn — 27/07/2026) khẳng định **2 chỉ số** và loại bỏ điểm/tier/CO₂; PRD tái dựng từ demo (`DOC-v1.0-02`) lại mô tả **3 chỉ số** có Điểm uy tín + Điểm ECO. `C-USR-01` Resolved 2026-07-27 theo hướng BRD: **tier/điểm/CO₂ là phase sau**, Figma cho kết quả trung gian (có badge text, không có số — `DOC-v1.0-06` KP-01 §2 KB-USR-02). ⇒ SC positive assert 2 chỉ số; SC negative assert **không hiện** Điểm ECO/Điểm uy tín.

---

### REQ-USR-005 · Cấu hình kênh liên hệ sẽ lộ — KHÔNG có bề mặt UI ở v1.0
📍 `DOC-v1.0-01 §A6 · L103`  ·  Clarif: `C-USR-02`

> "USR-07 | Cấu hình kênh liên hệ sẽ lộ: SĐT (bắt buộc), Workplace/email (tùy chọn)"

↳ **Ghi chú:** Yêu cầu có trong BRD nhưng **không xuất hiện ở bất kỳ ảnh nào trong 82 ảnh `DOC-v1.0-04`** và không có trên app STG (`DOC-v1.0-06` KP-01 §2 KB-USR-03). `C-USR-02` Resolved — Out of scope v1.0. Đây là **case gốc** của `Project_rule §Custom Rules §10.1` ⇒ chỉ viết **1 SC dạng GAP finding** (`SC-USR-010`), ⛔ không viết TC khẳng định màn/field này tồn tại.

---

### REQ-USR-006 · Menu điều hướng tại màn Cá nhân
📍 `DOC-v1.0-02 §3.9 · bảng Trường/Thành phần · dòng "Menu"` · `DOC-v1.0-01 §D1b US-D20 · L196`  ·  Clarif: `C-USR-04`

> Nguồn #1 — `DOC-v1.0-02` §3.9 dòng "Menu":
> "Menu | "Đơn của tôi" (→ Hoạt động) · "Đánh giá đã nhận" (không có phản hồi khi bấm trong bản demo)"

> Nguồn #2 — `DOC-v1.0-01` §D1b `US-D20` L196:
> "Trang cá nhân có mục "Đơn đã giúp" & "Quà đã nhận"; màn Quà đã nhận hiển thị 1 card đếm số bông hoa/ly cà phê/gấu bông/vương miện + danh sách lịch sử nhận quà"

> Nguồn #3 — `DOC-v1.0-06` KP-01 §2 KB-USR-02 (Figma):
> "Card trắng chỉ có 2 số liệu: `12 — đơn đã giúp`, `8 — quà đã nhận`; menu: `Đơn của tôi`, `Quà đã nhận`"

↳ **Ghi chú:** **3 nguồn cho 3 nhãn menu khác nhau** ở mục thứ hai: PRD = *"Đánh giá đã nhận"* (bấm không phản hồi), BRD `US-D20` = *"Quà đã nhận"*, Figma = *"Quà đã nhận"*. BRD + Figma đồng thuận ⇒ lấy **"Quà đã nhận"** làm nhãn hiện hành; mục *"Đánh giá đã nhận"* của PRD nhất quán với `RAT-01/02` đã bị `C-GIFT-01` loại khỏi v1.0. Mở `C-USR-04` để BA chốt nhãn chính thức. Mục "Đơn của tôi" → màn Hoạt động: 2 nguồn đồng thuận (`DOC-v1.0-06` KP-01 §2 KB-USR-04).

---

### REQ-USR-007 · Header + badge hạng thành viên màn Cá nhân
📍 `DOC-v1.0-02 §3.9 · bảng Trường/Thành phần · dòng "Hạng thành viên"` · `DOC-v1.0-04` ảnh `570ad9d3…`, `e5764b10…`  ·  Clarif: `C-USR-01`

> Nguồn #1 — `DOC-v1.0-02` §3.9 dòng "Hạng thành viên":
> "Hạng thành viên | 🔒 "Hạng Đồng hành" — cơ chế tier/gamification, icon khoá gợi ý còn hạng cao hơn"

> Nguồn #2 — `DOC-v1.0-06` KP-01 §2 KB-USR-02 (Figma, xác nhận 2 ảnh):
> "**CÓ** badge pill `🏆 Hạng Đồng hành` (dạng text)"
> "BA/PO xác nhận: cơ chế tính tier là **phase sau**, v1.0 không có logic phân hạng."

↳ **Ghi chú:** Badge **tồn tại trên UI** (Figma xác nhận) nhưng **không có logic tier phía sau** ở v1.0 ⇒ viết TC hiển thị badge dạng text tĩnh, ⛔ KHÔNG viết TC đổi hạng / tính điểm tier. Bảng §3.9 của PRD không đánh số ID ⇒ cột `Maps (Ref DOC)` để `—`, neo bằng `§3.9` + tên dòng bảng.

---

> **Quy ước:** Implicit REQ → thay quote bằng *(Implicit — không có quote trực tiếp)* + derivation ở Ghi chú. Quote >500 ký tự → sidecar `v1.0/quotes/REQ-USR-NNN.md`.
> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
