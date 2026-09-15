# Requirement Traceability — v1.1 · Module ORD

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation` của `DOC-v1.1-01` = `FR<NN>` / `BR<FF>-NN` / `VAL-NN` / `AC-{US}.{Scenario}.{Case}` ⇒ **Schema A**.
> Chỉ chứa REQ **NEW + MODIFIED** của lượt delta này. REQ CARRIED nguyên trạng — xem `v1.0/ORD-dang-tin/requirement_traceability.md`.
> 🔴 **Module có delta nặng nhất về số lượng CL được đóng** — 4 CL Resolved, 1 reopened, 1 mở mới. Xem `risk_assessment.md`.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module ORD — DOC-v1.1-01

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-ORD-023 | `BR01-06`, `AC-05.1.01`, `AC-05.1.02`, `AC-05.2.01` | `DOC-v1.1-01` §8.1.1 BR01-06 (trang 34) · §8.1.4 UI/Field Spec (trang 35) · §6.2 AC-05.x (trang 20) | SC-ORD-061, SC-ORD-062 | — |
| REQ-ORD-024 | `BR01-02`, `AC-02.1.02` | `DOC-v1.1-01` §8.1.1 BR01-02 (trang 34) · §8.1.4 (trang 35) · §6.2 AC-02.1.02 (trang 19) | SC-ORD-052, SC-ORD-053 | — |
| REQ-ORD-025 | `BR18-04` | `DOC-v1.1-01` §8.18.1 BR18-04 (trang 52) | SC-ORD-064 | — |
| REQ-ORD-026 | `BR18-03`, `AC-03.1.01` | `DOC-v1.1-01` §8.18.1 BR18-03 (trang 52) · §6.2 AC-03.1.01 (trang 19) | SC-ORD-057 | — |
| REQ-ORD-027 | `BR18-05` | `DOC-v1.1-01` §8.18.1 BR18-05 (trang 52) | SC-ORD-065 | — |
| REQ-ORD-028 | `§8.1.4` dòng Địa chỉ giao hàng | `DOC-v1.1-01` §8.1.4 UI/Field Spec (trang 35) | SC-ORD-063 | — |
| REQ-ORD-003 *(MODIFIED)* | `§8.1.4` dòng Loại hàng | `DOC-v1.1-01` §8.1.4 (trang 35) · §8.1.1 BR01-07 (trang 34) | SC-ORD-005, SC-ORD-006, SC-ORD-007 | C-ORD-09, C-ORD-04 |
| REQ-ORD-005 *(MODIFIED)* | `BR01-03`, `AC-02.2.01`, `§8.1.4` dòng Giá trị hàng | `DOC-v1.1-01` §8.1.1 BR01-03 · §8.1.4 (trang 35) · §6.2 AC-02.2.01 | SC-ORD-008, SC-ORD-009, SC-ORD-010 | — |
| REQ-ORD-006 *(MODIFIED)* | `BR01-01`, `BR18-01`, `BR18-02`, `VAL-07`, `AC-03.x` | `DOC-v1.1-01` §8.1.1 BR01-01 (trang 33) · §8.18.1 BR18-01/02 (trang 52) · §8.18.2 VAL-07 · §6.2 AC-03.x (trang 19) | SC-ORD-012, SC-ORD-013, SC-ORD-054, SC-ORD-055, SC-ORD-056 | — |
| REQ-ORD-007 *(MODIFIED)* | `BR01-08`, `§8.1.4` dòng SĐT/Địa chỉ lấy hàng, `AC-30.1.01` | `DOC-v1.1-01` §8.1.4 (trang 35) · §8.1.1 BR01-08 · §6.2 AC-30.1.01 (trang 28) | SC-ORD-014, SC-ORD-015, SC-ORD-016, SC-ORD-017 | C-ORD-10 |
| REQ-ORD-008 *(MODIFIED)* | `BR01-09`, `AC-04.1.01`, `AC-04.1.02`, `AC-04.2.01` | `DOC-v1.1-01` §8.1.1 BR01-09 (trang 34) · §8.1.3 bước 4 · §6.2 AC-04.x (trang 20) | SC-ORD-018..021, SC-ORD-058, SC-ORD-059, SC-ORD-060 | C-ORD-13 |
| REQ-ORD-009 *(MODIFIED)* | `§8.1.4` nhóm người nhận | `DOC-v1.1-01` §8.1.4 (trang 35) | SC-ORD-022, SC-ORD-023, SC-ORD-024, SC-ORD-063 | — |
| REQ-ORD-010 *(MODIFIED)* | `§8.1.4` dòng Địa chỉ lấy hàng | `DOC-v1.1-01` §8.1.4 (trang 35) | SC-ORD-025, SC-ORD-026, SC-ORD-027 | C-ORD-11 |
| REQ-ORD-011 *(MODIFIED)* | `BR01-04`, `AC-06.1.02`, `§8.1.4` dòng Từ/Đến ngày | `DOC-v1.1-01` §8.1.1 BR01-04 (trang 34) · §8.1.4 (trang 35-36) · §6.2 AC-06.1.02 | SC-ORD-028 | — |
| REQ-ORD-012 *(MODIFIED)* | `BR01-04`, `BR01-05`, `AC-06.2.01`, `§8.1.4` dòng Buổi mong muốn | `DOC-v1.1-01` §8.1.1 BR01-04/BR01-05 · §8.1.4 (trang 36) · §6.2 AC-06.2.01 | SC-ORD-029, SC-ORD-030 | — |
| REQ-ORD-013 *(MODIFIED)* | `BR01-07`, `VAL-01`, `AC-01.1.02` | `DOC-v1.1-01` §8.1.1 BR01-07 (trang 34) · §8.18.2 VAL-01 · §6.2 AC-01.1.02 | SC-ORD-031..034 | C-ORD-12, C-ORD-04 |
| REQ-ORD-015 *(MODIFIED)* | `AC-07.1.01`, `§8.1.3` bước 8 | `DOC-v1.1-01` §6.2 AC-07.1.01 (trang 18) · §8.1.3 (trang 35) | SC-ORD-036, SC-ORD-037, SC-ORD-038 | C-ORD-05 |
| REQ-ORD-016 *(MODIFIED)* | `FR02`, `BR02-01..04`, `AC-19.1.01`, `AC-20.1.01`, `AC-20.1.02` | `DOC-v1.1-01` §8.2 (trang 36) · §8.2.1 BR02-01..04 · §8.2.2 · §6.2 AC-19/AC-20 (trang 24) | SC-ORD-039..042 | — |
| REQ-ORD-017 *(MODIFIED)* | `BR05-01`, `BR05-02`, `VAL-05`, `AC-08.1.01`, `AC-08.1.02` | `DOC-v1.1-01` §8.5.1 BR05-01/02 (trang 38) · §8.18.2 VAL-05 · §6.2 AC-08.x (trang 18) | SC-ORD-043, SC-ORD-044 | — |
| REQ-ORD-018 *(MODIFIED)* | `BR05-03`, `AC-09.1.01` | `DOC-v1.1-01` §8.5.1 BR05-03 (trang 38) · §6.2 AC-09.1.01 (trang 19) | SC-ORD-045 | C-ORD-03 |
| REQ-ORD-021 *(MODIFIED)* | `AC-01.2.01` | `DOC-v1.1-01` §6.2 AC-01.2.01 (trang 17) | SC-ORD-050 | C-ORD-08 |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-ORD-023 · Khối "người nhận uỷ quyền" khai ngay lúc đăng tin (`BR01-06`)
📍 `DOC-v1.1-01 §8.1.1 BR01-06 · trang 34` · `§8.1.4 UI/Field Spec · trang 35` · `§6.2 AC-05.x · trang 20`  ·  Clarif: —

> Nguồn #1 — BR01-06 (§8.1.1, trang 34):
> "Người nhận uỷ quyền là không bắt buộc; nếu có thì tên 2–60 ký tự, số điện thoại đúng định dạng Việt Nam khi được nhập."

> Nguồn #2 — §8.1.4 UI/Field Spec (trang 35):
> "Tên người được uỷ quyền | Không | Văn bản · trống (khối thu gọn) | 2–60 ký tự; nếu có thì hiện cho người vận chuyển kèm nhãn "Người gửi chỉ định""
> "Quan hệ / ghi chú uỷ quyền | Không | Văn bản · trống | ≤ 60 ký tự (ví dụ: "Đồng nghiệp cùng phòng")"

↳ **Ghi chú:** ⭐ **REQ hoàn toàn MỚI — v1.0 không có khái niệm "người nhận uỷ quyền" ở khâu đăng tin.** Ở v1.0, uỷ quyền chỉ xuất hiện **lúc giao hàng** (`DLV`, người vận chuyển tự khai khi giao cho người khác). v1.1 cho người gửi **chỉ định trước** ngay trong wizard, và dữ liệu đó **hiện cho người vận chuyển kèm nhãn "Người gửi chỉ định"** ⇒ nối thẳng vào `FR07` (`SC-DLV-038` — giao cho người được uỷ quyền). ⚠️ **Đây là khối *thu gọn* và *không bắt buộc*** — 2 thuộc tính sinh ra 2 SC riêng: khai đủ (`SC-ORD-061`) và xoá khối sau khi đã mở (`SC-ORD-062`, `AC-05.2.01`). Validation lai: tên **2–60 ký tự** (bắt buộc *nếu* khối được dùng), SĐT theo định dạng VN **chỉ khi được nhập** ⇒ ⛔ không viết TC kiểu "bỏ trống SĐT thì lỗi".

---

### REQ-ORD-024 · Khối lượng và kích thước là trường bắt buộc (`BR01-02`)
📍 `DOC-v1.1-01 §8.1.1 BR01-02 · trang 34` · `§8.1.4 · trang 35` · `§6.2 AC-02.1.02 · trang 19`  ·  Clarif: —

> Nguồn #1 — BR01-02 (§8.1.1, trang 34):
> "Khối lượng và kích thước là bắt buộc — dùng để người vận chuyển tự lượng sức; ứng dụng không chặn theo ngưỡng."

> Nguồn #2 — §8.1.4 UI/Field Spec (trang 35):
> "Khối lượng | Có | Dropdown · chưa chọn | < 5 kg · 5–10 kg · > 10 kg. Không cho để trống"
> "Kích thước | Có | Dropdown · chưa chọn | Nhỏ · cầm tay · Vừa · khoảng 20×20 cm · Lớn · > 20×20 cm. Không cho để trống"

↳ **Ghi chú:** REQ MỚI — v1.0 biết có 2 field này (`§D8.1`) nhưng **không rõ có bắt buộc không**, nên `SC-ORD-004` chỉ assert sự tồn tại. Nay `BR01-02` nói **bắt buộc** và field spec ghi **"Không cho để trống"** + **"chưa chọn"** là giá trị mặc định ⇒ 2 SC negative riêng (`SC-ORD-052`, `SC-ORD-053`). ⭐ **Mệnh đề thứ hai quan trọng không kém:** *"ứng dụng **không chặn theo ngưỡng**"* — tức chọn *"> 10 kg"* hay *"Lớn · > 20×20 cm"* vẫn đăng được bình thường. Đây là **vế phủ định dễ bị dev làm sai theo hướng "cẩn thận thừa"** (thêm cảnh báo/chặn cho hàng nặng) ⇒ đưa vào Then của `SC-ORD-052`/`053`, ⛔ không tách SC riêng vì cùng một thao tác quan sát.

---

### REQ-ORD-025 · Copy nhanh địa chỉ và số điện thoại (`BR18-04`)
📍 `DOC-v1.1-01 §8.18.1 BR18-04 · trang 52`  ·  Clarif: —

> "BR18-04 | Icon copy đặt cạnh địa chỉ giao và số điện thoại ở màn chi tiết tin và màn theo dõi đơn; sau khi copy, icon đổi trạng thái và màu xanh trong khoảng 1,8 giây."

↳ **Ghi chú:** REQ MỚI — tiện ích dùng chung, v1.0 không có. Đặc tả **đủ chi tiết để assert**: vị trí (cạnh địa chỉ giao **và** SĐT), phạm vi (màn chi tiết tin **và** màn theo dõi đơn), phản hồi (đổi trạng thái + **màu xanh**), thời lượng (**~1,8 giây**). ⚠️ **Thời lượng 1,8s là con số khó verify thủ công chính xác** — TC nên assert *"icon trở về trạng thái cũ sau khoảng 2 giây"* thay vì đo bằng đồng hồ bấm giây; ghi rõ dung sai để tester không đánh FAIL vì lệch 0,2s. ⚠️ **Ranh giới module:** `BR18-04` cũng áp cho **màn theo dõi đơn** (thuộc `DLV`) — `DLV` v1.1 đã ghi `BR18-04` trong `doc_source` của `CHANGELOG`; ở đây giữ phần **màn chi tiết tin**, ⛔ không nhân bản.

---

### REQ-ORD-026 · Carousel + lightbox cho nhiều ảnh (`BR18-03`)
📍 `DOC-v1.1-01 §8.18.1 BR18-03 · trang 52` · `§6.2 AC-03.1.01 · trang 19`  ·  Clarif: —

> "BR18-03 | Nơi hiển thị nhiều ảnh dùng carousel lướt ngang có badge đếm "2/5"; chạm ảnh mở lightbox nền tối giữ đúng tỉ lệ, có nút đóng và chạm nền để đóng."

↳ **Ghi chú:** REQ MỚI. v1.0 chỉ biết *"có ảnh sản phẩm"* (`§D8.1`), không có đặc tả cách hiển thị ⇒ `SC-ORD-013` chỉ assert ảnh hiện ra. Nay có **4 hành vi kiểm được**: carousel lướt ngang · badge đếm dạng `"2/5"` · lightbox nền tối **giữ đúng tỉ lệ** · **2 cách đóng** (nút đóng + chạm nền). Gom vào **1 SC** (`SC-ORD-057`) vì cùng một luồng thao tác liên tục, tách ra sẽ thành 4 TC lặp lại 90% các bước.

---

### REQ-ORD-027 · Ảnh đã gắn vào mốc nhật ký thì không xoá được (`BR18-05`)
📍 `DOC-v1.1-01 §8.18.1 BR18-05 · trang 52`  ·  Clarif: —

> "BR18-05 | Ảnh đã gắn vào một mốc nhật ký thì không xoá được (phục vụ truy vết)."

↳ **Ghi chú:** REQ MỚI — và là **một rule audit nữa cùng họ với `NFR-07`** (log append-only, `SC-DLV-062`) và `BR11-03` (không xoá bản ghi lần ghép, `SC-CNL-010`). Ba rule này cùng nói một điều: **bằng chứng đã ghi thì bất biến**. ⚠️ Đối chiếu với `BR18-02` (*"xoá được từng ảnh **trước khi ghi mốc**"*) ⇒ **ranh giới là thời điểm ghi mốc**, không phải thuộc tính của ảnh. ⇒ `SC-ORD-065` phải kiểm **cả hai phía** của ranh giới trong 1 lượt: xoá được lúc đang soạn, không xoá được sau khi đăng. ⚠️ Cross-ref: nếu `SC-CNL-010` FAIL (app xoá được log) thì rule này **nhiều khả năng cũng FAIL** — chạy cùng lô để gộp bug report.

---

### REQ-ORD-028 · Địa chỉ giao hàng phải khác địa chỉ lấy hàng
📍 `DOC-v1.1-01 §8.1.4 UI/Field Spec, dòng "Địa chỉ giao hàng" · trang 35`  ·  Clarif: —

> "Địa chỉ giao hàng | Có | Văn bản · tự điền từ danh bạ | Không để trống; phải khác địa chỉ lấy hàng"

↳ **Ghi chú:** REQ MỚI — validation **liên-trường** (cross-field) đầu tiên của wizard, v1.0 không có. Cùng họ với `BR02-03` của `FR02` (*"Điểm đến phải khác điểm xuất phát"*) ⇒ 2 form, cùng một loại rule. ⚠️ **Câu hỏi kỹ thuật PRD không trả lời:** so sánh *"khác"* theo chuỗi thô hay có chuẩn hoá (trim, hoa/thường, dấu)? `VAL-03` chỉ nói *"tự cắt khoảng trắng đầu/cuối"* — không nói gì về hoa/thường. ⇒ `SC-ORD-063` lấy **biên gần nhất** làm ô kiểm (2 địa chỉ chỉ khác nhau khoảng trắng đầu/cuối) và **ghi nhận** hành vi với khác-hoa-thường thay vì assert cứng, tránh đánh FAIL cho một hành vi PRD chưa định nghĩa.

---

### REQ-ORD-003 · Loại hàng: 8 giá trị chính thức, mặc định "Tài liệu" *(MODIFIED)*
📍 `DOC-v1.1-01 §8.1.4 UI/Field Spec, dòng "Loại hàng" · trang 35` · `§8.1.1 BR01-07 · trang 34`  ·  Clarif: `C-ORD-09`, `C-ORD-04`

> Nguồn (v1.0) — `DOC-v1.0-01 §D8.1 ORD-01 · L357` + `KP-01 §10.2/§10.3` (quan sát app): **3 nguồn cho 3 danh mục khác nhau**; app STG có 8 chip nhưng chip đầu là **"Giấy tờ, hồ sơ"**, ⛔ **không có chip "Tài liệu"**.

> Nguồn (v1.1) — §8.1.4 UI/Field Spec (trang 35):
> "Loại hàng | Có | Chọn 1 giá trị · mặc định Tài liệu | Tài liệu · Đồ điện tử · Thực phẩm · Hàng nhỏ · Đồ dễ vỡ · Quần áo · Thuốc/Y tế · Khác"

↳ **Ghi chú (diff):** ⭐ **Đây là CL số 1 của dự án (`C-ORD-09`) — và PRD chỉ giải quyết được MỘT NỬA.**
**Nửa đã xong:** phía tài liệu nay có **một** danh mục chính thức, đủ 8 giá trị, kèm **giá trị mặc định** (*"Tài liệu"*) — v1.0 có 3 nguồn mâu thuẫn nên không biết lấy cái nào.
**Nửa còn lại — và nó nặng hơn:** app STG hiển thị chip đầu là **"Giấy tờ, hồ sơ"**, PRD ghi **"Tài liệu"**. Đây **không phải** hai cách gọi của cùng một thứ trong cùng một tài liệu — mà là **doc ⟷ app lệch nhau ở một nhãn xuất hiện trong Steps của rất nhiều TC**. Theo `Project_rule §Custom Rules §10.1`, ⛔ **không được tự chọn bên nào**. ⇒ `C-ORD-09` chuyển **🟡 Partially Resolved**, và **ràng buộc 4 của `03_test-cases/v1.0/CHANGELOG.md §2`** (*"dùng nhãn app, ⛔ tuyệt đối không dùng 'Tài liệu' cho tới khi C-ORD-09 chốt"*) **vẫn còn hiệu lực**.
🔴 **Phát hiện phụ, nghiêm trọng hơn: PRD tự mâu thuẫn với chính nó.** Field spec để **"Thuốc/Y tế"** là 1 trong 8 giá trị hợp lệ, trong khi `BR01-07` viết *"Hàng cấm (**thuốc**, vũ khí, chất nguy hiểm, hàng phi pháp) **không được đăng**"*. ⇒ **`C-ORD-04` (đã Resolved ở v1.0: "KHÔNG chặn") phải MỞ LẠI** — xem `risk_assessment.md`.

---

### REQ-ORD-006 · Ảnh món hàng: từ tuỳ chọn thành BẮT BUỘC ≥ 1 *(MODIFIED)*
📍 `DOC-v1.1-01 §8.1.1 BR01-01 · trang 33` · `§8.18.1 BR18-01/BR18-02 · trang 52` · `§8.18.2 VAL-07` · `§6.2 AC-03.x · trang 19`  ·  Clarif: —

> Nguồn (v1.0) — `DOC-v1.0-01 §D8.1 dòng "Ảnh sản phẩm" · L360`: có field ảnh, **không nêu bắt buộc hay không**, không nêu trần.

> Nguồn (v1.1) #1 — BR01-01 (§8.1.1, trang 33):
> "Ảnh món hàng là bắt buộc ≥ 1, tối đa 5 ảnh; mỗi ảnh ≤ 5MB, chỉ JPG/PNG. Thiếu ảnh thì chặn sang bước 2."

> Nguồn (v1.1) #2 — BR18-02 (§8.18.1, trang 52):
> "Mỗi ảnh ≤ 5MB, chỉ JPG/PNG; xoá được từng ảnh trước khi ghi mốc; ẩn nút thêm khi đủ 5; hiện bộ đếm "n/5"."

↳ **Ghi chú (diff):** 🔴 **Thay đổi hành vi thật, không chỉ thêm chi tiết.** v1.0 không biết ảnh có bắt buộc không ⇒ `SC-ORD-012` chỉ assert *"tải được ảnh"*. v1.1 nói **bắt buộc ≥ 1** và nêu rõ hệ quả: ***"Thiếu ảnh thì chặn sang bước 2"*** — tức đây là **điều kiện chặn luồng**, không phải cảnh báo. ⇒ `SC-ORD-054` **NEW**, **P1** (chặn luồng chính của tính năng chính). Kèm theo 4 ràng buộc kiểm được mà v1.0 không có: **trần 5** · **≤ 5MB/ảnh** · **chỉ JPG/PNG** · **bộ đếm `"n/5"` + ẩn nút thêm khi đủ 5** (`VAL-07` nhắc lại) ⇒ `SC-ORD-055`, `SC-ORD-056`. ⚠️ **Nếu app STG hiện cho đăng tin không ảnh thì đó là gap PRD↔app** — cần vibe-test xác nhận trước `generate-tc`, vì nếu app chưa siết thì 1 SC P1 sẽ FAIL vì lý do "app chưa cập nhật", không phải bug logic.

---

### REQ-ORD-007 · Prefill SĐT người gửi và địa chỉ lấy hàng từ hồ sơ *(MODIFIED)*
📍 `DOC-v1.1-01 §8.1.4 UI/Field Spec · trang 35` · `§8.1.1 BR01-08` · `§6.2 AC-30.1.01 · trang 28`  ·  Clarif: `C-ORD-10`

> Nguồn (v1.0) — `KP-01 §10.5/§10.6/§10.10` (quan sát app): **địa chỉ lấy hàng KHÔNG được pre-fill** ⇒ `C-ORD-10` mở: *"bug hay tài khoản test chưa cấu hình?"*

> Nguồn (v1.1) #1 — §8.1.4 UI/Field Spec (trang 35):
> "Số điện thoại người gửi | Có | Văn bản · prefill từ hồ sơ | Định dạng Việt Nam (10 số, đầu 0); chỉ lộ sau khi ghép"
> "Địa chỉ lấy hàng | Có | Văn bản · prefill địa chỉ mặc định | Không để trống, ≤ 200 ký tự"

> Nguồn (v1.1) #2 — AC-30.1.01 Then (§6.2, trang 28):
> "Hiện banner xanh "Đã lưu thông tin của bạn", banner tự ẩn khi người dùng sửa tiếp. Lần đăng tin sau, hai giá trị này được prefill vào ô số điện thoại người…"

↳ **Ghi chú (diff):** ⭐ **`C-ORD-10` được RESOLVE, và câu trả lời biến nó thành bug.** Câu hỏi v1.0 là *"không pre-fill — bug hay tài khoản test chưa cấu hình?"*. PRD trả lời gián tiếp nhưng dứt khoát: field spec ghi **"prefill địa chỉ mặc định"** là **hành vi đặc tả**, và `FR15` + `AC-30.1.01` đặc tả luôn **nơi người dùng đặt giá trị mặc định đó** (màn "Cập nhật thông tin") kèm cam kết *"lần đăng tin sau, hai giá trị này được prefill"*. ⇒ Nếu hồ sơ **đã có** địa chỉ mặc định mà wizard vẫn trống thì là **BUG**; nếu hồ sơ **chưa có** thì trống là đúng. ⇒ `SC-ORD-025` phải tách tiền đề rõ ràng — ⛔ không chạy trên tài khoản chưa biết trạng thái hồ sơ, vì đúng sự mơ hồ đó đã khiến CL này treo 2 tháng.

---

### REQ-ORD-008 · Tra danh bạ nội bộ theo email công ty người nhận *(MODIFIED)*
📍 `DOC-v1.1-01 §8.1.1 BR01-09 · trang 34` · `§8.1.3 bước 4 · trang 34` · `§6.2 AC-04.x · trang 20`  ·  Clarif: `C-ORD-13`

> Nguồn (v1.0) — `DOC-v1.0-01 §D3 USR-EML L253` + `§D8.1 L366`: có field email người nhận, **autofill** được nhắc nhưng không nêu nguồn dữ liệu.

> Nguồn (v1.1) #1 — BR01-09 (§8.1.1, trang 34):
> "Email công ty người nhận được tra danh bạ nội bộ: tìm thấy thì tự điền tên · số điện thoại · địa chỉ (vẫn sửa được); không thấy thì cho nhập thủ công."

> Nguồn (v1.1) #2 — §8.1.4 UI/Field Spec (trang 35):
> "Email công ty người nhận | Có | Văn bản · trống | Đúng định dạng và thuộc tên miền nội bộ; kích hoạt tra danh bạ"

> Nguồn (v1.1) #3 — §4 SCOPES, Tích hợp với các hệ thống khác (trang 9):
> "Danh bạ nội bộ — tra email công ty người nhận để tự điền tên · số điện thoại · địa chỉ"

↳ **Ghi chú (diff):** ⭐ **Tích hợp hệ thống ngoài được nêu tên lần đầu.** v1.0 biết có autofill nhưng không biết **lấy từ đâu** ⇒ không viết được TC cho nhánh *không tìm thấy*. Nay có đủ **3 nhánh**: tìm thấy → tự điền 3 trường **và vẫn sửa được** (`SC-ORD-058`) · không thấy → cho nhập thủ công (`SC-ORD-059`) · email sai định dạng **hoặc ngoài tên miền nội bộ** → chặn trước khi tra (`SC-ORD-060`). ⚠️ **Rủi ro tiền đề lớn nhất của module:** cần **2 email thật trong danh bạ** và **1 email đúng tên miền nhưng không có trong danh bạ** — loại dữ liệu chỉ môi trường có tích hợp danh bạ thật mới cung cấp được. Nếu STG chưa nối danh bạ thì 3 SC này `BLOCKED`. ⇒ mở `C-ORD-13`.

---

### REQ-ORD-015 · Màn "Đăng tin thành công" — KHÔNG hiển thị mã đơn *(MODIFIED)*
📍 `DOC-v1.1-01 §6.2 AC-07.1.01 · trang 18` · `§8.1.3 bước 8 · trang 35`  ·  Clarif: `C-ORD-05`

> Nguồn (v1.0) — `DOC-v1.0-02 §3.5.4` + `DOC-v1.0-04` (**2 biến thể mockup**) ⇒ `C-ORD-05` Open: *"Màn 'Đăng tin thành công' có 'Mã tin' hay không?"*

> Nguồn (v1.1) #1 — AC-07.1.01 Then (§6.2, trang 18):
> "Chuyển sang màn "Đăng tin thành công" — không hiển thị mã đơn. Có nút về trang chủ và nút xem đơn vừa đăng. Tin xuất hiện ngay ở "Tin mới" trên trang chủ và ở "Đơn của tôi"."

> Nguồn (v1.1) #2 — §8.1.3 bước 8 (trang 35):
> "Tin POSTED; màn "Đăng tin thành công" (không hiển thị mã đơn); tin lên bảng tin và "Đơn của tôi""

↳ **Ghi chú (diff):** ⭐ **`C-ORD-05` RESOLVED — và PRD nói ở 2 chỗ độc lập, cùng dùng đúng cụm *"không hiển thị mã đơn"***, nên không phải suy diễn từ việc mockup thiếu. Câu trả lời là **KHÔNG có mã đơn** ⇒ `SC-ORD-036` chuyển từ *ghi nhận biến thể mockup* sang **assert-absent khẳng định**. `AC-07.1.01` còn cho thêm 3 assert v1.0 không có: **2 nút** (về trang chủ · xem đơn vừa đăng) và **2 nơi tin phải xuất hiện ngay** ("Tin mới" trên trang chủ · "Đơn của tôi") — vế sau nối sang `HOME` (`SC-HOME-019`) và `ACT` (`SC-ACT-004`), ⛔ không nhân bản, chỉ cross-ref.

---

### REQ-ORD-021 · Thoát giữa wizard — có popup xác nhận, không lưu DRAFT *(MODIFIED)*
📍 `DOC-v1.1-01 §6.2 AC-01.2.01 · trang 17`  ·  Clarif: `C-ORD-08`

> Nguồn (v1.0) — `DOC-v1.0-06 KP-02 §5 dòng C-ORD-08` ⇒ Open: *"Thoát/Reset giữa wizard có xoá form?"*

> Nguồn (v1.1) — AC-01.2.01 (§6.2, trang 17):
> "Given: Người dùng đang ở bước 2 và đã điền một phần dữ liệu. When: Người dùng bấm quay lại/đóng wizard. Then: Hiện popup xác nhận "Thoát và bỏ nội dung đã nhập?". Chọn thoát → không tạo tin (trạng thái DRAFT không được lưu). Chọn ở lại → dữ liệu đã nhập giữ nguyên."

↳ **Ghi chú (diff):** ⭐ **`C-ORD-08` RESOLVED, và câu trả lời đầy đủ hơn câu hỏi.** Câu hỏi chỉ là *"có xoá form không"*; AC trả lời **cả ba tầng**: (1) có **popup xác nhận** với chuỗi verbatim `"Thoát và bỏ nội dung đã nhập?"`; (2) chọn thoát → **không tạo tin**, và nói rõ *"trạng thái DRAFT **không được lưu**"* — tức app **không có** cơ chế nháp, một khẳng định kiến trúc chứ không chỉ là hành vi màn hình; (3) chọn ở lại → **dữ liệu giữ nguyên**. ⇒ `SC-ORD-050` hết dạng `[GAP]`, assert đủ 3 nhánh trong 1 SC (cùng một luồng thao tác).

---

### REQ-ORD-016 · Tin OFFER: không công khai, không tiếp cận được từ phía người gửi *(MODIFIED)*
📍 `DOC-v1.1-01 §8.2 · trang 36` · `§8.2.1 BR02-01..04` · `§6.2 AC-20.1.01 / AC-20.1.02 · trang 24`  ·  Clarif: —

> Nguồn (v1.0) — `DOC-v1.0-01 §D8.2 L379-386` + `KP-01 §3 KB-ORD-11`: form OFFER 1 trang, tin không công khai.

> Nguồn (v1.1) #1 — BR02-01 (§8.2.1, trang 36):
> "Tin OFFER không hiển thị công khai trên bảng tin; chỉ hệ thống truy cập để khớp đơn. Người gửi không tìm, không xem, không ngỏ ý được với tin OFFER."

> Nguồn (v1.1) #2 — AC-20.1.02 Then (§6.2, trang 24):
> "Không có kết quả và không mở được chi tiết. Ghép nối chiều OFFER chỉ diễn ra qua thông báo khớp tuyến gửi cho người vận chuyển — đây là con đường duy nhất. Số điện thoại người vận chuyển chỉ lộ sau khi ghép."

> Nguồn (v1.1) #3 — BR02-03 (§8.2.1, trang 36):
> "Điểm đến phải khác điểm xuất phát; khoảng ngày tối đa 7 ngày; tối thiểu 1 buổi di chuyển."

↳ **Ghi chú (diff):** v1.0 biết *"tin OFFER không công khai"* nhưng phát biểu ở dạng **hiển thị** ⇒ `SC-ORD-041` chỉ kiểm *"không thấy trên bảng tin"*. v1.1 nâng thành **thuộc tính bảo mật 3 lớp**: *"không tìm, không xem, không ngỏ ý"*, và `AC-20.1.02` thêm vế **"mở link trực tiếp"** cũng không được ⇒ đây là kiểm **kiểm soát truy cập**, không phải kiểm hiển thị. ⛔ TC không được dừng ở *"không thấy trong danh sách"*. ⚠️ Vế *"mở link trực tiếp"* khó thực hiện trên mobile app (không có URL) — ghi nhận giới hạn ở `test_data_catalog.md`, ⛔ không đánh PASS chỉ vì "không có đường thử". `BR02-03` bổ sung validation liên-trường (điểm đến ≠ điểm xuất phát) — cùng họ `REQ-ORD-028`; đã có `SC-ORD-040` phủ, chỉ siết Then.

---

### REQ-ORD-005 · Giá trị hàng: 3 mức, chọn "Cao" thì cảnh báo nhưng KHÔNG chặn *(MODIFIED)*
📍 `DOC-v1.1-01 §8.1.1 BR01-03 · trang 34` · `§8.1.4 dòng "Giá trị hàng" · trang 35` · `§6.2 AC-02.2.01 · trang 19`  ·  Clarif: —

> Nguồn (v1.0) — `DOC-v1.0-01 §D8.1 dòng "Giá trị hàng" · L359` + `KP-01 §3 KB-ORD-05`: có 3 mức, **không rõ mức cao có chặn hay chỉ cảnh báo**.

> Nguồn (v1.1) #1 — `BR01-03` (§8.1.1, trang 34):
> "Chọn giá trị hàng ở mức cao thì hiện cảnh báo trách nhiệm tự thoả thuận; không chặn đăng tin."

> Nguồn (v1.1) #2 — §8.1.4 (trang 35):
> "Giá trị hàng | Có | Dropdown · chưa chọn | Thấp · Vừa · Cao. Chọn Cao thì hiện cảnh báo trách nhiệm tự thoả thuận"

↳ **Ghi chú (diff):** Chi tiết hoá + **chốt một vế phủ định**. v1.0 biết 3 mức nhưng không rõ *"Cao"* có chặn đăng tin không ⇒ `SC-ORD-009` viết dè dặt. `BR01-03` chốt **cảnh báo, ⛔ không chặn** — vế phủ định này quan trọng vì dev dễ làm "cẩn thận thừa". Field spec thêm giá trị mặc định là **"chưa chọn"** (tức bắt buộc chọn) ⇒ siết Then của `SC-ORD-008`. ⚠️ Không lẫn với `C-ORD-02` (ngưỡng bằng **số tiền**, vẫn Resolved *out of scope*).

---

### REQ-ORD-009 · Nhóm trường người nhận — nay có ràng buộc liên-trường *(MODIFIED)*
📍 `DOC-v1.1-01 §8.1.4 UI/Field Spec, nhóm người nhận · trang 35`  ·  Clarif: —

> Nguồn (v1.0) — `DOC-v1.0-01 §D8.1 L367-369` + `DOC-v1.0-02 §3.5.2`: 3 trường người nhận (tên · SĐT · địa chỉ giao), chưa nêu ràng buộc liên-trường.

> Nguồn (v1.1) — §8.1.4 (trang 35):
> "Tên người nhận | Có | Văn bản · tự điền từ danh bạ | 2–60 ký tự"
> "Số điện thoại người nhận | Có | Văn bản · tự điền từ danh bạ | Định dạng Việt Nam (10 số, đầu 0)"
> "Địa chỉ giao hàng | Có | Văn bản · tự điền từ danh bạ | Không để trống; phải khác địa chỉ lấy hàng"

↳ **Ghi chú (diff):** Ba trường nay có **biên cụ thể** (tên 2–60 · SĐT 10 số đầu 0) thay vì mô tả chung, và **nguồn giá trị đổi**: từ *nhập tay* sang **"tự điền từ danh bạ"** (xem `REQ-ORD-008`). Ràng buộc *"phải khác địa chỉ lấy hàng"* tách riêng thành `REQ-ORD-028` vì là **loại rule khác** (liên-trường, không phải định dạng một trường).

---

### REQ-ORD-010 · Ô địa chỉ lấy hàng là văn bản tự do, ≤ 200 ký tự *(MODIFIED)*
📍 `DOC-v1.1-01 §8.1.4 dòng "Địa chỉ lấy hàng" · trang 35`  ·  Clarif: `C-ORD-11`

> Nguồn (v1.0) — `DOC-v1.0-01 §D3 LOC-03 L246` + `KP-01 §3 KB-ORD-06` ⇒ `C-ORD-11` Open: *"preset 6 văn phòng / không chip gợi ý / autocomplete?"*

> Nguồn (v1.1) — §8.1.4 (trang 35):
> "Địa chỉ lấy hàng | Có | Văn bản · prefill địa chỉ mặc định | Không để trống, ≤ 200 ký tự"

↳ **Ghi chú (diff):** ⭐ **`C-ORD-11` RESOLVED.** Cột `Kiểu` ghi **"Văn bản"** ⇒ **ô nhập tự do**, ⛔ không phải preset danh sách 6 văn phòng, không chip gợi ý, không autocomplete — ba giả thuyết v1.0 nêu đều **bị loại**. Kèm biên rõ: **≤ 200 ký tự**, không để trống. ⇒ `SC-ORD-026` assert kiểu ô + biên 200/201.

---

### REQ-ORD-011 · Khoảng ngày: tối đa 7 ngày, không quá khứ, Đến ≥ Từ *(MODIFIED)*
📍 `DOC-v1.1-01 §8.1.1 BR01-04 · trang 34` · `§8.1.4 · trang 35-36` · `§6.2 AC-06.1.02 · trang 20`  ·  Clarif: —

> Nguồn (v1.0) — `DOC-v1.0-01 §D8.1 L370-371`: có Từ ngày / Đến ngày, **không nêu trần khoảng ngày**.

> Nguồn (v1.1) #1 — `BR01-04` (§8.1.1, trang 34):
> "Khoảng ngày tối đa 7 ngày, không nhận ngày quá khứ, Đến ngày ≥ Từ ngày. Phải chọn tối thiểu 1 buổi; buổi "Giờ nào cũng được" loại trừ các buổi còn lại."

> Nguồn (v1.1) #2 — §8.1.4 (trang 35-36):
> "Từ ngày | Có | Chọn ngày · hôm nay | Không chọn ngày quá khứ"
> "Đến ngày | Có | Chọn ngày · = Từ ngày | ≥ Từ ngày; khoảng tối đa 7 ngày; là mốc chuyển EXPIRED"

↳ **Ghi chú (diff):** **Trần 7 ngày là ràng buộc MỚI** — v1.0 hoàn toàn không có, nên `SC-ORD-028` chưa từng kiểm biên này. ⇒ siết Then với 2 ô biên **đúng 7 ngày (hợp lệ)** ⟷ **8 ngày (chặn)**. Field spec còn chốt **giá trị mặc định**: Từ ngày = *hôm nay*, Đến ngày = *bằng Từ ngày*. ⚠️ Mệnh đề *"là mốc chuyển EXPIRED"* **xác nhận lại `C-ORD-03`** (Resolved v1.0: ngưỡng = "Đến ngày", không phải hằng số) — PRD **không đảo**, chỉ củng cố.

---

### REQ-ORD-012 · Buổi mong muốn: 4 lựa chọn, "Giờ nào cũng được" loại trừ phần còn lại *(MODIFIED)*
📍 `DOC-v1.1-01 §8.1.1 BR01-04 / BR01-05 · trang 34` · `§8.1.4 · trang 36` · `§6.2 AC-06.2.01 · trang 20`  ·  Clarif: —

> Nguồn (v1.0) — `DOC-v1.0-01 §D8.1 dòng "Khung giờ" · L372` + `KP-01 §10.11`: có khung giờ, **chưa rõ enum và quy tắc loại trừ**.

> Nguồn (v1.1) #1 — §8.1.4 (trang 36):
> "Buổi mong muốn | Có | Chọn nhiều · mặc định Sau giờ làm | Sáng (8–12) · Chiều (13–17) · Sau giờ làm (17–19) · Giờ nào cũng được (loại trừ các buổi khác). Tối thiểu 1 buổi"

> Nguồn (v1.1) #2 — `BR01-05` (§8.1.1, trang 34):
> "Luồng đăng tin không dùng giờ chính xác — giờ cụ thể do hai bên chốt qua điện thoại sau khi ghép."

↳ **Ghi chú (diff):** **Enum đầy đủ kèm khung giờ số** (8–12 · 13–17 · 17–19) và **quy tắc loại trừ** — cả hai v1.0 đều chưa có ⇒ `SC-ORD-029` nay assert được hành vi *"chọn 'Giờ nào cũng được' thì các buổi đang chọn tự bỏ chọn"*. Mặc định là **"Sau giờ làm"**. `BR01-05` giải thích **vì sao không có ô giờ chính xác** — hữu ích để ⛔ không viết TC đòi nhập giờ cụ thể. ⚠️ Khung giờ ghi **tương đối so với hiện tại** khi seed data (`Project_rule` · `KP-01 §10.11`), ⛔ không hardcode.

---

### REQ-ORD-013 · Consent điều khoản bắt buộc + tuyên bố hàng cấm *(MODIFIED)*
📍 `DOC-v1.1-01 §8.1.1 BR01-07 · trang 34` · `§8.18.2 VAL-01 · trang 52` · `§6.2 AC-01.1.02 · trang 17`  ·  Clarif: `C-ORD-12`, `C-ORD-04`

> Nguồn (v1.0) — `DOC-v1.0-01 §D3 ORD-09 L245` + `§D8.1 L373` ⇒ `C-ORD-12` Resolved: checkbox **chưa tick** mặc định.

> Nguồn (v1.1) #1 — `BR01-07` (§8.1.1, trang 34):
> "Bắt buộc tick đồng ý điều khoản miễn trừ trách nhiệm mới bật nút đăng tin. Hàng cấm (thuốc, vũ khí, chất nguy hiểm, hàng phi pháp) không được đăng."

> Nguồn (v1.1) #2 — §8.1.4 (trang 36):
> "Xác nhận điều khoản | Có | Checkbox · chưa tick | Bắt buộc tick mới bật nút Đăng tin"

↳ **Ghi chú (diff):** Vế **consent** chỉ là **xác nhận lại** `C-ORD-12` (mặc định *"chưa tick"*) — PRD **không đảo**, củng cố kết luận v1.0. 🔴 **Nhưng vế thứ hai của `BR01-07` mở ra vấn đề nặng nhất lượt này:** *"Hàng cấm (**thuốc**, vũ khí, chất nguy hiểm, hàng phi pháp) **không được đăng**"* — trong khi `§8.1.4` cách đó **1 trang** để **"Thuốc/Y tế"** là 1 trong 8 giá trị hợp lệ của Loại hàng. Hai câu **không thể cùng đúng**, và ⛔ **không phân xử được bằng thứ tự ưu tiên nguồn** (`MASTER-MEMORY §2`) vì cả hai cùng là `DOC-v1.1-01`. ⇒ **`C-ORD-04` MỞ LẠI**; `SC-ORD-031..035` **ghi nhận hành vi thật**, ⛔ không assert chiều nào. Chi tiết + câu hỏi cho BA: `risk_assessment.md §C-ORD-04`.

---

### REQ-ORD-017 · Sửa tin: chỉ khi POSTED, form nạp sẵn, có "Huỷ chỉnh sửa" *(MODIFIED)*
📍 `DOC-v1.1-01 §8.5.1 BR05-01 / BR05-02 · trang 38` · `§8.18.2 VAL-05 · trang 52` · `§6.2 AC-08.1.01 / AC-08.1.02 · trang 18`  ·  Clarif: —

> Nguồn (v1.0) — `DOC-v1.0-01 §D3 ORD-10 L252` · `§D4 BR-EDIT-01 L269` · `§D7 OPR-10 L346`: chỉ sửa khi còn "Chờ ghép".

> Nguồn (v1.1) #1 — `BR05-01` (§8.5.1, trang 38):
> "Chỉ chỉnh sửa được khi đơn còn ở POSTED; từ MATCHED trở đi nút Chỉnh sửa không hiển thị và request sửa bị từ chối."

> Nguồn (v1.1) #2 — `BR05-02` (§8.5.1, trang 38):
> "Form sửa nạp sẵn dữ liệu cũ; có "Cập nhật" và "Huỷ chỉnh sửa" (không lưu)."

> Nguồn (v1.1) #3 — `AC-08.1.02` Then (§6.2, trang 18):
> "Nút "Chỉnh sửa" không hiển thị. Mọi request sửa đơn ở trạng thái này bị từ chối và không ghi mốc vào nhật ký."

↳ **Ghi chú (diff):** v1.0 chốt **ngưỡng** (chỉ sửa khi `POSTED`); v1.1 thêm **ba chi tiết kiểm được**: (1) form **nạp sẵn dữ liệu cũ**; (2) có **2 nút** — "Cập nhật" và **"Huỷ chỉnh sửa" (không lưu)**, nút thứ hai v1.0 hoàn toàn không biết; (3) phía chặn có **2 tầng** — UI ẩn nút **và** backend từ chối request **không ghi mốc nhật ký**. ⚠️ Tầng backend **không verify được qua UI** ⇒ `SC-ORD-044` **ghi nhận**, ⛔ không assert (`§Custom Rules §10.1` bước 3); để dành cho API test ở `implement-automation`.

---

### REQ-ORD-018 · Tin hết hạn: chỉ khi VẪN POSTED, và biến khỏi cả luồng khớp tuyến *(MODIFIED)*
📍 `DOC-v1.1-01 §8.5.1 BR05-03 · trang 38` · `§6.2 AC-09.1.01 · trang 19`  ·  Clarif: `C-ORD-03`

> Nguồn (v1.0) — `DOC-v1.0-01 §D3 ORD-06 L244` + `KP-01 §3 KB-ORD-02` ⇒ `C-ORD-03` Resolved: hạn tin = **giá trị "Đến ngày"** user chọn.

> Nguồn (v1.1) #1 — `BR05-03` (§8.5.1, trang 38):
> "Hết ngày cuối của khoảng ngày mà đơn vẫn POSTED thì chuyển EXPIRED; hiện badge "Hết hạn" kèm lý do "Không có ai nhận mang giúp trong thời gian đăng"."

> Nguồn (v1.1) #2 — `AC-09.1.01` Then (§6.2, trang 19):
> "Tin chuyển sang EXPIRED, biến khỏi bảng tin và khỏi luồng khớp tuyến. Hiện badge "Hết hạn" ở tab Hoàn tất kèm lý do "Không có ai nhận mang giúp trong thời gian đăng". Người đăng nhận thông báo gợi ý gỡ hoặc đăng lại."

↳ **Ghi chú (diff):** `C-ORD-03` **xác nhận lại**, không đảo. Ba bổ sung: **(1) điều kiện *"đơn **vẫn POSTED**"*** — tin đã `MATCHED` rồi mới quá ngày thì **KHÔNG** chuyển `EXPIRED`; v1.0 chưa nêu và đây là ô dev hay làm sai (chỉ kiểm mỗi ngày hết hạn). **(2) hệ quả hai tầng** — biến khỏi **bảng tin** *và* khỏi **luồng khớp tuyến** (`FR04`); v1.0 chỉ biết vế bảng tin, vế sau nối sang `ASN`. **(3) chuỗi lý do verbatim** — home hiển thị ở `ACT` (`SC-ACT-008`), ở đây giữ **vế chuyển trạng thái** (`SC-ORD-045`), ⛔ không nhân bản.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
