# Requirement Traceability — v1.0 · Module TS

> Tạo bởi: analyze-requirements (INIT 2026-09-07) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation: FR/VR` ⇒ **Schema A**.
> 📌 **Home canonical của `C-TS-01`** (Admin Web Portal).
> ⚠️ Module **phần lớn là backend/Admin, ít bề mặt UI** ⇒ phạm vi test v1.0 chỉ verify **hệ quả quan sát được từ phía end-user**.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module TS — DOC-v1.0-01 · DOC-v1.0-06

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-TS-001 | `TS-01`, `ORD-04`, `US-D09` | `DOC-v1.0-01` §A8 L121 · §D3 L243 · §D1b L178 | SC-TS-001, SC-TS-002 | — |
| REQ-TS-002 | `TS-02`, `BR-INT-04` | `DOC-v1.0-01` §A8 L122 · §A5 L80 · `DOC-v1.0-06` KP-01 §7 KB-CNL-01 | SC-TS-003 | C-CNL-02 |
| REQ-TS-003 | `TS-03`, `BR-CNF-04` | `DOC-v1.0-01` §A8 L123 · §D4 L266 · §D5 L296 · `DOC-v1.0-06` KP-01 §9 KB-TS-01 | SC-TS-006, SC-TS-007 | C-TS-01 |
| REQ-TS-004 | — (blockquote §A8, không đánh số), `ORD-09` | `DOC-v1.0-01` §A8 L115 · §D3 L245 | SC-TS-004 | — |
| REQ-TS-005 | — (§A8 blockquote phạm vi) | `DOC-v1.0-01` §A8 L125 | SC-TS-005 | C-GIFT-01 |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-TS-001 · Ghi log toàn bộ tương tác (`TS-01`)
📍 `DOC-v1.0-01 §A8 TS-01 · L121` · `§D3 ORD-04 · L243` · `§D1b US-D09 · L178`  ·  Clarif: —

> Nguồn #1 — `TS-01` (§A8 L121):
> "TS-01 | Ghi log toàn bộ tương tác: ai đăng, ai nhận, mốc thời gian, đổi trạng thái, huỷ (kèm lý do + ai huỷ)"

> Nguồn #2 — `ORD-04` (§D3 L243):
> "ORD-04 | Tin có timeline trạng thái | Lịch sử đầy đủ với timestamp"

> Nguồn #3 — `US-D09` (§D1b L178):
> "timeline theo dõi 5 mốc (Chờ ghép · Lấy hàng · Đang giao · Đã giao · Hoàn thành), **mỗi bước ghi timestamp**"

↳ **Ghi chú:** **3 nguồn đồng thuận.** `TS-01` liệt kê **5 nhóm thông tin phải log**: ai đăng · ai nhận · mốc thời gian · đổi trạng thái · **huỷ (kèm lý do + ai huỷ)** ⇒ 2 SC: đủ mốc + timestamp (`SC-TS-001`) và **ghi rõ actor** cho mỗi mốc (`SC-TS-002`). ⚠️ Nhóm thứ 5 (**huỷ**) là chỗ app **đang vi phạm** — xem `REQ-TS-002` và `SC-CNL-009`. Bề mặt quan sát duy nhất từ phía user = block **LỊCH SỬ** ở màn Theo dõi đơn (`DLV` `SC-DLV-029`) ⇒ SC ở đây nhìn từ **góc audit**, không nhân bản assert hiển thị.

---

### REQ-TS-002 · Log không sửa được sau khi ghi (`TS-02` / `BR-INT-04`)
📍 `DOC-v1.0-01 §A8 TS-02 · L122` · `§A5 BR-INT-04 · L80` · `DOC-v1.0-06 KP-01 §7 KB-CNL-01`  ·  Clarif: `C-CNL-02`

> Nguồn #1 — `TS-02` (§A8 L122):
> "TS-02 | Log không sửa được sau khi ghi (audit trail)"

> Nguồn #2 — `BR-INT-04` (§A5 L80):
> "BR-INT-04 | Timeline tương tác không sửa được sau khi ghi (audit)"

> Nguồn #3 — HÀNH VI VI PHẠM (`DOC-v1.0-06` KP-01 §7 `KB-CNL-01`, live-verify 2026-07-29):
> "- **Huỷ nhận đơn** (Carrier) → tệ hơn: **XOÁ LUÔN dòng "Ghép thành công"** khỏi LỊCH SỬ"

↳ **Ghi chú:** ⭐ **REQ P1 duy nhất của module** — và là **rule bị app vi phạm rõ ràng nhất của cả dự án**: 2 nguồn BRD yêu cầu log **bất biến**, nhưng live-verify cho thấy huỷ nhận đơn **XOÁ** dòng log đã ghi. ⇒ `SC-TS-003` viết theo rule, **dự kiến FAIL**. ⚠️ **Phân biệt với `SC-CNL-010`:** SC ở `CNL` nhìn từ **luồng huỷ** (sau khi huỷ nhận thì log phải còn + có thêm dòng mới); SC ở đây nhìn từ **thuộc tính audit** (log **bất biến** với mọi hành động, không chỉ huỷ) ⇒ 2 góc nhìn, và SC này còn phải thử **các hành động khác** có làm thay đổi log không.

---

### REQ-TS-003 · Admin can thiệp hỗ trợ dựa trên log (`TS-03`)
📍 `DOC-v1.0-01 §A8 TS-03 · L123` · `§D4 BR-CNF-04 · L266` · `§D5 · L296` · `DOC-v1.0-06 KP-01 §9 KB-TS-01`  ·  Clarif: `C-TS-01`

> Nguồn #1 — `TS-03` (§A8 L123):
> "TS-03 | Admin có quyền can thiệp hỗ trợ khi có vướng mắc (dựa trên log)"

> Nguồn #2 — `BR-CNF-04` (§D4 L266):
> "RECEIVER không xác nhận 2 giờ → nhắc; thêm 2 giờ → **admin hỗ trợ**"

> Nguồn #3 — `DOC-v1.0-01` §D5 L296:
> "Tranh chấp tình trạng hàng | **Admin cung cấp ảnh + timeline**; hai bên tự giải quyết"

> Nguồn #4 — PHÁN QUYẾT (`DOC-v1.0-06` KP-01 §9 `KB-TS-01`):
> "BRD §A3 chỉ nhắc tên nền tảng (*"Mobile App (iOS/Android) + Admin Web Portal"*), không mô tả màn hình/field nào."
> "Phạm vi test v1.0 chỉ verify **hệ quả quan sát được từ phía end-user** (vd đơn quá hạn xác nhận → chuyển "admin hỗ trợ"), không test UI Admin Portal."

↳ **Ghi chú:** `C-TS-01` Resolved 2026-07-27: **Admin Web Portal out of scope v1.0** (không có đặc tả UI). ⇒ 2 SC: `SC-TS-006` verify **hệ quả phía end-user** (trạng thái *"admin hỗ trợ"* sau 4 giờ — trùng tiền đề với `SC-DLV-024`); `SC-TS-007` là **GAP finding** ghi nhận không có bề mặt Admin để test. ⚠️ Cột `Admin` trong permission matrix `§D4` (L279-286) ghi *"✓ override"* ở nhiều dòng — toàn bộ **không test được** ở v1.0.

---

### REQ-TS-004 · Consent điều khoản miễn trừ trước khi đăng/ghép
📍 `DOC-v1.0-01 §A8 · L115` · `§D3 ORD-09 · L245`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-01` §A8 L115 (blockquote pháp lý):
> "Pháp lý (quan trọng): FoxEco là nền tảng kết nối nội bộ, KHÔNG phải đơn vị vận chuyển/giữ trẻ/vận tải. Hai bên tự thỏa thuận & tự chịu trách nhiệm. App không xử lý tiền. Hàng/tài sản giá trị cao → khuyến nghị bảo hiểm bên thứ 3 (phase sau). **App hiển thị điều khoản miễn trừ + buộc consent trước khi đăng/ghép.** Hàng cấm (thuốc, vũ khí, chất nguy hiểm, phi pháp) không được đăng."

> Nguồn #2 — `ORD-09` (§D3 L245):
> "ORD-09 | Consent điều khoản trước khi đăng | Bắt buộc tick "đồng ý tự chịu trách nhiệm""

↳ **Ghi chú:** ⚠️ **Rule §A8 rộng hơn `ORD-09`:** yêu cầu consent **trước khi đăng VÀ trước khi ghép**; nhưng `ORD-09` + `D8.1`/`D8.2` chỉ có checkbox ở **luồng đăng tin**. Ở **luồng ghép** (`SC-ASN-001`) chỉ có **modal xác nhận** (*"SĐT hai bên sẽ được lộ sau khi xác nhận"*) — **không phải consent điều khoản**. ⇒ `SC-TS-004` ghi nhận: consent có ở luồng đăng (2 luồng NEED+OFFER), còn ở luồng ghép thì **chỉ có modal xác nhận**, ⛔ không assert có checkbox điều khoản khi ghép. Banner cam kết ở màn "Đăng tin mới" (`KB-ORD-10`) là **thông tin tĩnh**, không phải consent.

---

### REQ-TS-005 · Phạm vi Trust & Safety v1.0 — không chấm sao, không chặn user
📍 `DOC-v1.0-01 §A8 · L125`  ·  Clarif: `C-GIFT-01`

> "Phạm vi hiện tại: chỉ ghi log + admin can thiệp hỗ trợ. KHÔNG có chấm sao/đánh giá, **KHÔNG có chặn (block) người dùng**."

↳ **Ghi chú:** Câu này **định nghĩa phạm vi module** và loại 2 tính năng: **(a)** chấm sao/đánh giá — đã có SC ở `GIFT` (`SC-GIFT-011`) ⇒ ⛔ không nhân bản; **(b)** **chặn (block) người dùng** — chưa có SC ở module nào ⇒ `SC-TS-005` assert-absent. Đây là ranh giới cần chốt vì `TS` (Trust & Safety) thường được kỳ vọng có báo cáo/chặn user; v1.0 **chỉ có log + admin**.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
