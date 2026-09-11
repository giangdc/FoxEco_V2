# Requirement Traceability — v1.0 · Module HOME

> Tạo bởi: analyze-requirements (INIT 2026-09-07) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation: FR/VR` (doc-native, module-prefixed) ⇒ **Schema A**.
> ⚠️ Module này ở đợt v1.0 cũ bị gộp vào `ORD` (1 scenario / 32 TC) — tách riêng từ 2026-09-07.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module HOME — DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-04 · DOC-v1.0-06

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-HOME-001 | — (bảng §2 không đánh số) | `DOC-v1.0-02` §2 · `DOC-v1.0-06` KP-01 §3 KB-ORD-07 (#8) | SC-HOME-001, SC-HOME-002 | — |
| REQ-HOME-002 | — (bảng §2 không đánh số) | `DOC-v1.0-02` §2 · dòng "Header" | SC-HOME-003, SC-HOME-004, SC-HOME-005, SC-HOME-006 | C-HOME-01 |
| REQ-HOME-003 | — | `DOC-v1.0-02` §2 · dòng "Banner quảng bá" | SC-HOME-007 | — |
| REQ-HOME-004 | `USR-05` | `DOC-v1.0-02` §2 · dòng "Card "Đóng góp của bạn"" · `DOC-v1.0-01` §A6 L102 | SC-HOME-008 | C-USR-01 |
| REQ-HOME-005 | `US-D02` | `DOC-v1.0-02` §3.1 · dòng "Đơn của tôi" · §4.1 · §5.1 · `DOC-v1.0-01` §D1b L165 | SC-HOME-009, SC-HOME-010, SC-HOME-011, SC-HOME-012, SC-HOME-013, SC-HOME-014, SC-HOME-015 | C-HOME-02 |
| REQ-HOME-006 | — | `DOC-v1.0-02` §3.1 · dòng "Xem tất cả" | SC-HOME-016 | — |
| REQ-HOME-007 | `US-D06`, `OPR-01` | `DOC-v1.0-02` §3.1 · dòng "Tin mới" · `DOC-v1.0-01` §D1b L175 · §D7 L337 | SC-HOME-017, SC-HOME-018, SC-HOME-019, SC-HOME-020, SC-HOME-021 | C-HOME-03, C-ORD-07 |
| REQ-HOME-008 | — | `DOC-v1.0-02` §2 · dòng "Nút "Xem bảng tin gửi hàng"" | SC-HOME-022 | — |
| REQ-HOME-009 | — | `DOC-v1.0-02` §4.1 | SC-HOME-023 | — |
| REQ-HOME-010 | — | `DOC-v1.0-06` KP-05 §3 (#4) · `C-ORD-06` | SC-HOME-024 | C-ORD-06 |

> `DOC-v1.0-02` là `.docx` **không đánh số ID requirement** ⇒ phần lớn cột `Maps (Ref DOC)` để `—`, neo bằng `§section` + tên dòng bảng (tra bằng `scripts/doc/search-doc.sh "<tên dòng>"`). Đây là hành vi đúng của `req_notation: FR/VR` khi 1 trong 2 doc không có ID — ⛔ KHÔNG bịa `FR-NNN`.

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-HOME-001 · Bottom nav 5 tab dùng chung cho cả 3 vai trò
📍 `DOC-v1.0-02 §2 "Kiến trúc điều hướng dùng chung cho cả 3 vai trò" · đoạn 1`  ·  Clarif: —

> "Mỗi vai trò có cùng một cấu trúc điều hướng gồm 5 tab dưới cùng: Trang chủ / Bảng tin / Đăng tin (nút "+" nổi bật ở giữa) / Hoạt động / Cá nhân. Các màn hình con (Chi tiết tin, Theo dõi đơn, luồng Đăng tin theo bước, Thông báo, Tặng quà...) không hiển thị thanh tab này — chỉ có nút quay lại (←)."

↳ **Ghi chú:** Hai rule trong một đoạn: **(a)** 5 tab, thứ tự cố định, giống nhau cho cả 3 vai trò; **(b)** màn con **ẩn** bottom nav và chỉ có nút back ⇒ tách thành 2 SC (`SC-HOME-001`, `SC-HOME-002`). `DOC-v1.0-06` KP-01 §3 KB-ORD-07 (#8) xác nhận độc lập cùng 5 tab từ quan sát app STG. Đây là **cửa vào của mọi module khác** ⇒ ưu tiên P1.

---

### REQ-HOME-002 · Header — icon vai trò + lời chào + chuông thông báo
📍 `DOC-v1.0-02 §2 · bảng Thành phần/Mô tả · dòng "Header"`  ·  Clarif: `C-HOME-01`

> "Header | Icon vai trò + "Xin chào, [Tên]" + chuông thông báo (chấm đỏ khi có tin chưa đọc)"

↳ **Ghi chú:** Ba thành phần, **mức bằng chứng khác nhau**: lời chào + chuông có bằng chứng ở cả PRD lẫn Figma; **"icon vai trò"** thì `DOC-v1.0-06` KP-05 §3 (#5) ghi rõ *"Chưa có bằng chứng UI mapping"* ⇒ theo `§Custom Rules §10.1`, icon vai trò chỉ được 1 SC dạng GAP (`SC-HOME-004`), mở `C-HOME-01`. Chấm đỏ chuông fan-out 2 SC (có/không có tin chưa đọc); cơ chế đánh dấu đã đọc thuộc `NTF` (`REQ-NTF-004`).

---

### REQ-HOME-003 · Banner quảng bá tĩnh
📍 `DOC-v1.0-02 §2 · bảng Thành phần/Mô tả · dòng "Banner quảng bá"`  ·  Clarif: —

> "Banner quảng bá | "Tiện đường — Giúp đồng nghiệp" + logo "FOX ECO" — tĩnh, không chức năng"

↳ **Ghi chú:** Doc nói rõ **"tĩnh, không chức năng"** ⇒ SC assert *hiển thị đúng text/logo* + *bấm không phát sinh điều hướng*. Lưu ý tagline ở `DOC-v1.0-01` §A3 L29 là *"Tiện đường — Đồng nghiệp giúp nhau"* — **khác câu chữ** với PRD; assert theo PRD/UI (nguồn bề mặt), ghi lệch ở `C-HOME-01` phần ghi chú.

---

### REQ-HOME-004 · Card "Đóng góp của bạn" — số cá nhân + số cộng đồng
📍 `DOC-v1.0-02 §2 · bảng Thành phần/Mô tả · dòng "Card "Đóng góp của bạn""` · `DOC-v1.0-01 §A6 · L102`  ·  Clarif: `C-USR-01`

> Nguồn #1 — `DOC-v1.0-02` §2:
> "Card "Đóng góp của bạn" | Số đơn đã giúp (lớn) + "Cộng đồng FoxEco: [x] đơn · [y] người" — thống kê cá nhân & cộng đồng"

> Nguồn #2 — `DOC-v1.0-01` §A6 L102:
> "USR-05 | Hiển thị tổng số đơn đã giúp + tổng số quà ảo đã nhận (không tính điểm/CO₂)"

↳ **Ghi chú:** Card Trang chủ hiển thị **số đơn đã giúp** (trùng chỉ số ở màn Cá nhân — `REQ-USR-004`) **+ 2 số cộng đồng** mà BRD không nhắc. Số cộng đồng là `Runtime` toàn hệ thống ⇒ ⛔ không assert giá trị, chỉ assert **có hiển thị + đúng định dạng**. `C-USR-01` liên quan vì dòng cộng đồng của `DOC-v1.0-02` §3.2 có biến thể kèm CO₂ (*"tiết kiệm Y kg CO₂"*) đã bị loại khỏi v1.0.

---

### REQ-HOME-005 · Section "Đơn của tôi" — hiện có điều kiện, nhãn theo vai trò
📍 `DOC-v1.0-02 §3.1 · bảng Trường/Thành phần · dòng "Đơn của tôi"` · §4.1 · §5.1 · `DOC-v1.0-01 §D1b US-D02 · L165`  ·  Clarif: `C-HOME-02`

> Nguồn #1 — `DOC-v1.0-02` §3.1 dòng "Đơn của tôi":
> "Đơn của tôi | Chỉ hiện khi có đơn đang hoạt động. Nhãn "Gửi:" + loại hàng | giá trị; badge trạng thái (Chờ ghép/Đã ghép/Đang giao/Đã giao/Hoàn thành); "Từ:" / "Đến:"; thanh progress 5 bước; "Chạm để theo dõi đơn của bạn""

> Nguồn #2 — `DOC-v1.0-02` §4.1 (vai Carrier):
> "khi chưa nhận đơn nào, KHÔNG có section "Đơn của tôi" — Home đi thẳng xuống "Tin mới" (hiện đầy đủ hơn do không bị chiếm chỗ)"

> Nguồn #3 — `DOC-v1.0-02` §5.1 (vai Receiver):
> "khối "Đơn của tôi" dùng nhãn "Nhận:" thay vì "Gửi:"/"Giao:""

> Nguồn #4 — `DOC-v1.0-01` §D1b `US-D02` L165:
> "tin xuất hiện ở "Đơn của tôi" trên trang chủ"

↳ **Ghi chú:** REQ nặng nhất của module — 4 nguồn, fan-out 7 SC: hiện/ẩn theo điều kiện (2 SC), **nhãn theo vai trò** `Gửi:`/`Giao:`/`Nhận:` (3 SC — 1 SC/role theo Scenario Sufficiency Rule), badge+progress (1 SC), tap → Theo dõi đơn (1 SC). ⚠️ `DOC-v1.0-06` KP-05 §3 (#3) nêu nghi vấn **ẩn theo VAI TRÒ** (Carrier không thấy section) khác với **ẩn theo "có/không có đơn"** như doc viết ⇒ mở `C-HOME-02`; SC-HOME-010 assert theo doc (điều kiện có đơn), không assert theo vai trò.

---

### REQ-HOME-006 · Nút "Xem tất cả" → màn Hoạt động
📍 `DOC-v1.0-02 §3.1 · bảng Trường/Thành phần · dòng "Xem tất cả"`  ·  Clarif: —

> "Xem tất cả | Mở màn Hoạt động"

↳ **Ghi chú:** ⭐ REQ này **giải quyết 1 trong 6 gap "không có nguồn tài liệu"** mà đợt v1.0 cũ ghi ở `DOC-v1.0-06` KP-05 §3 (#1) — nguồn thật nằm ngay ở `DOC-v1.0-02` §3.1. ⇒ Được viết TC khẳng định, không còn là gap.

---

### REQ-HOME-007 · Section "Tin mới" — số lượng tin MÂU THUẪN 1 vs 5
📍 `DOC-v1.0-02 §3.1 · dòng "Tin mới"` · `DOC-v1.0-01 §D1b US-D06 · L175` · §D7 `OPR-01` · L337  ·  Clarif: `C-HOME-03`, `C-ORD-07`

> Nguồn #1 — `DOC-v1.0-02` §3.1 dòng "Tin mới":
> "Tin mới | Rút gọn 1 tin mới nhất của CẢ CỘNG ĐỒNG (không riêng của Người gửi); bấm vào mở Chi tiết tin"

> Nguồn #2 — `DOC-v1.0-01` §D1b `US-D06` L175:
> "Là Carrier, tôi muốn xem tối đa 5 tin cần gửi mới nhất ngay trên trang chủ, để nhanh chóng biết có ai cần giúp mà không cần vào sâu Bảng tin. | Trang chủ hiển thị đúng 5 tin mới nhất; nếu còn tin khác hiện nút "Xem thêm trên Bảng tin" dẫn sang màn Bảng tin"

> Nguồn #3 — `DOC-v1.0-01` §D7 `OPR-01` L337:
> "Trần số tin gợi ý cho 1 carrier | Mỗi người vận chuyển chỉ nhận thông báo tối đa 5 tin cần gửi phù hợp (mới & gần tuyến nhất); tránh làm phiền/spam"

↳ **Ghi chú:** ⭐ **Mâu thuẫn số lượng chưa giải quyết:** PRD = *"1 tin mới nhất"*, BRD `US-D06` = *"đúng 5 tin mới nhất"*. Hai nguồn đồng thuận ở điểm khác: tin là **của cả cộng đồng**, và section này hiển thị cho **cả Sender lẫn Carrier** (`C-ORD-07` Resolved 2026-07-30 — *"viet theo UI luon nha"*), dù `US-D06` viết dưới góc nhìn Carrier. ⇒ `SC-HOME-017/018` assert **sự hiện diện theo vai trò** (2 SC), `SC-HOME-019` là **GAP finding cố ý không assert số lượng**, `SC-HOME-021` assert nút *"Xem thêm trên Bảng tin"* theo `US-D06`. Mở `C-HOME-03` cho vế số lượng. ⚠️ `OPR-01` nói về **trần thông báo gợi ý** (thuộc `ASN`), KHÔNG phải trần hiển thị Trang chủ — đừng trộn 2 rule.

---

### REQ-HOME-008 · Nút "Xem bảng tin gửi hàng" → tab Bảng tin
📍 `DOC-v1.0-02 §2 · bảng Thành phần/Mô tả · dòng "Nút "Xem bảng tin gửi hàng""`  ·  Clarif: —

> "Nút "Xem bảng tin gửi hàng" | Chuyển sang tab Bảng tin"

↳ **Ghi chú:** Khác với nút *"Xem thêm trên Bảng tin"* của `REQ-HOME-007` (nút này thuộc thành phần chung của Trang chủ, luôn có; nút kia gắn với section "Tin mới" và **có điều kiện ≥6 tin**). Nội dung màn Bảng tin verify ở `FEED`.

---

### REQ-HOME-009 · Sau khi Carrier nhận đơn → điều hướng thẳng Theo dõi đơn
📍 `DOC-v1.0-02 §4.1 "Màn hình Trang chủ" (vai Người vận chuyển) · đoạn 1`  ·  Clarif: —

> "Sau khi xác nhận nhận một đơn, ứng dụng điều hướng thẳng sang Theo dõi đơn (không quay về Trang chủ)."

↳ **Ghi chú:** Rule điều hướng **sau hành động ghép** — đích đến thuộc `DLV` nhưng **điểm xuất phát và kỳ vọng "không quay về Trang chủ"** là hành vi của module này. Cross-ref `SC-ASN-001` (hành động ghép) — 2 SC không trùng: SC-ASN assert đổi trạng thái, `SC-HOME-023` assert đích điều hướng.

---

### REQ-HOME-010 · Empty state màn Trang chủ
📍 `DOC-v1.0-06 KP-05 §3 (#4)` · `C-ORD-06`  ·  Clarif: `C-ORD-06`

> "4 | **Empty state màn Trang chủ** | Trùng `C-ORD-06` (Open)"

↳ **Ghi chú:** *(Implicit — không có quote đặc tả trực tiếp.)* Không tài liệu nào mô tả Trang chủ khi tài khoản chưa có đơn nào **và** chưa có tin cộng đồng nào. `C-ORD-06` (text empty state của 3 màn) đang **Open** và từng bị revert Resolved→Open vì đánh dấu Resolved không kèm bằng chứng (`DOC-v1.0-06` KP-02 §6) ⇒ `SC-HOME-024` viết dạng **ghi nhận hiển thị thực tế**, ⛔ không assert text.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
