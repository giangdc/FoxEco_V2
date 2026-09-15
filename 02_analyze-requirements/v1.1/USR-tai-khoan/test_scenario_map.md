---
id: v1.1/USR-tai-khoan/scenario-map
title: Test Scenario Map — v1.1 · Module USR
type: scenario-map
version: v1.1
sprint: 1
module: USR
counts:
  req: 10
  sc: 20
  new: 8
  modified: 3
  carried: 9
  deprecated: 0
  p1: 3
  p2: 10
  p3: 7
status: ANALYZED
updated: 2026-09-15
---

# Test Scenario Map — v1.1 · Module USR

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module USR **tính tới v1.1** (bao gồm CARRIED từ v1.0).
> Parent: `v1.0/USR-tai-khoan/` — 9 SC không đổi (CARRIED), 3 SC MODIFIED (giữ ID v1.0, bản v1.1 authoritative), 8 SC NEW.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Delta lần này fan-out theo: 1 happy path màn mới · 1 negative (SĐT bắt buộc) · **2 chiều độc lập của rule truy vết** (hồ sơ→đơn ⟷ đơn→hồ sơ) · vùng chỉ-đọc SSO · 2 chi tiết UI (banner tự ẩn · trường không bắt buộc).
> Trần: vế *"wizard nhận đúng giá trị prefill"* có home ở **`ORD`** (`SC-ORD-025`) — ⛔ không nhân bản; ở đây chỉ giữ vế *"hồ sơ có bị ghi đè không"*.

## Tổng quan
- Tổng số scenarios (tính tới v1.1): **20** (NEW: 8, MODIFIED: 3, CARRIED: 9)
- Phân bổ priority: P1: 3 | P2: 10 | P3: 7
- Delta lớn nhất: **`C-USR-03` bị ĐẢO** — màn Cá nhân từ *view-only hoàn toàn* thành *có màn "Cập nhật thông tin" sửa được 2 trường*; `SC-USR-003` phải lật chiều.
- ⚠️ **2 SC P1 mới đều thuộc nhóm rule truy vết** (`SC-USR-017` · `SC-USR-014`) — nhóm mà app đã vi phạm 1 lần đã live-verify.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### USR — Tài khoản & Hồ sơ (delta v1.1)

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-USR-013 | Mở màn "Cập nhật thông tin" đúng vị trí | REQ-USR-008, REQ-USR-006 | DOC-v1.1-01 §8.15 dòng Trigger | Đã đăng nhập SSO, đang ở trang Cá nhân | Cuộn hết trang, đọc thứ tự các mục menu | Có mục **"Cập nhật thông tin"** nằm **dưới mục "Quà đã nhận"**; bấm vào mở được màn tương ứng | P2 | UI | NEW |
| SC-USR-014 | Sửa SĐT + địa chỉ mặc định → lưu thành công | REQ-USR-008 | DOC-v1.1-01 §8.15.1 BR15-02, BR15-05 · §6.2 AC-30.1.01 | Đang ở màn "Cập nhật thông tin"; ghi lại giá trị SĐT và địa chỉ **hiện tại** | Sửa SĐT sang 1 số VN hợp lệ khác + sửa địa chỉ mặc định, bấm "Lưu thay đổi" | Hiện **banner xanh đúng chuỗi** "Đã lưu thông tin của bạn"; mở lại màn thấy **giá trị mới** đã lưu | P1 | Functional | NEW |
| SC-USR-015 | SĐT mặc định bắt buộc + đúng định dạng | REQ-USR-008 | DOC-v1.1-01 §8.15.1 BR15-02 · §8.15.2 · §6.2 AC-30.1.02 | Đang ở màn "Cập nhật thông tin" | Lần lượt: **xoá trắng** ô SĐT → Lưu; nhập **sai định dạng** (`123`, `84901234567`) → Lưu | Cả 2 lần: **KHÔNG lưu**, hiện lỗi **ngay dưới ô số điện thoại**; giá trị cũ giữ nguyên | P2 | Business Rule | NEW |
| SC-USR-016 | Trường đồng bộ SSO là chỉ đọc | REQ-USR-008, REQ-USR-002 | DOC-v1.1-01 §8.15.1 BR15-01 · §8.15.2 · §6.2 AC-30.2.01 | Đang ở màn "Cập nhật thông tin" | Thử chạm/sửa lần lượt: Tên · Phòng ban · MNV · Email công ty | Cả 4 **chỉ đọc, không có ô nhập**; riêng **Email công ty hiển thị kèm icon khoá** | P2 | Business Rule | NEW |
| SC-USR-017 | Sửa hồ sơ KHÔNG làm đổi đơn đã tạo | REQ-USR-009 | DOC-v1.1-01 §8.15.1 BR15-03 · §6.2 AC-30.2.02 | Có **≥ 1 đơn đã tạo trước đó**; ghi lại SĐT + địa chỉ lấy hàng **hiển thị trên đơn đó** | Vào "Cập nhật thông tin", đổi **cả** SĐT và địa chỉ mặc định, lưu; quay lại mở **đúng đơn cũ** | Đơn cũ **giữ nguyên** SĐT/địa chỉ tại thời điểm đăng (*"phục vụ truy vết"*); chỉ đơn **tạo mới** dùng giá trị mới | P1 | Business Rule | NEW |
| SC-USR-018 | Sửa trong từng đơn KHÔNG ghi ngược lại hồ sơ | REQ-USR-010 | DOC-v1.1-01 §8.15.1 BR15-04 · §6.2 AC-30.1.01 | Hồ sơ đã có SĐT mặc định **X** và địa chỉ mặc định **Y** (ghi lại) | Mở wizard đăng tin, sửa ô SĐT người gửi thành **X'** và địa chỉ lấy hàng thành **Y'**, đăng tin xong; quay lại "Cập nhật thông tin" | Hồ sơ **vẫn là X và Y** — ⛔ không bị ghi đè thành X'/Y' (`BR15-04`: *"mà không ghi lại hồ sơ"*) | P2 | Business Rule | NEW |
| SC-USR-019 | Banner tự ẩn khi người dùng sửa tiếp | REQ-USR-008 | DOC-v1.1-01 §8.15.1 BR15-05 | Vừa lưu thành công, banner xanh **đang hiển thị** | Chạm vào ô SĐT hoặc địa chỉ và sửa tiếp | Banner **tự ẩn** khi bắt đầu sửa; ⛔ không cần bấm đóng thủ công | P3 | UI | NEW |
| SC-USR-020 | Địa chỉ mặc định KHÔNG bắt buộc, ≤ 200 ký tự | REQ-USR-008 | DOC-v1.1-01 §8.15.2 | Đang ở màn "Cập nhật thông tin", SĐT đang hợp lệ | Xoá trắng ô **địa chỉ mặc định** → Lưu; rồi nhập chuỗi **200** và **201** ký tự → Lưu | Bỏ trống **vẫn lưu được** (⛔ không phải invalid — cột `Bắt buộc` = *Không*); 200 ký tự **được**, 201 **bị chặn/cắt** | P3 | Business Rule | NEW |
| SC-USR-003 | Vùng SSO của hồ sơ vẫn chỉ đọc *(lật một phần)* | REQ-USR-002 | DOC-v1.1-01 §8.15.1 BR15-01 · §8.15 Description | Đang ở **trang Cá nhân** (không phải màn "Cập nhật thông tin") | Rà toàn bộ trang tìm control sửa trực tiếp trên từng trường | Tên · phòng ban · MNV · email **không sửa trực tiếp được tại trang Cá nhân**. ⚠ **KHÁC v1.0**: nay **CÓ** lối vào màn sửa qua mục "Cập nhật thông tin" ⇒ ⛔ không assert *"không có bất kỳ control sửa nào"* | P2 | Business Rule | MODIFIED |
| SC-USR-002 | Hồ sơ cá nhân — các trường hiển thị | REQ-USR-002 | DOC-v1.1-01 §8.15.2 · DOC-v1.0-01 §A6 | Đã vào FoxEco bằng tài khoản có hồ sơ đầy đủ | Mở tab "Cá nhân" | Hiển thị đủ các trường đọc được: avatar, tên, phòng ban, MNV. ⚠ Danh sách trường của **trang Cá nhân** vẫn chưa có bằng chứng UI đầy đủ (`C-USR-04` còn Open một nửa) — ⛔ không lấy `§8.15.2` làm danh sách cho màn này | P2 | UI | MODIFIED |
| SC-USR-012 | Nhãn mục menu thứ hai *(hết gap)* | REQ-USR-006 | DOC-v1.1-01 §8.15 dòng Trigger | Đang ở trang Cá nhân | Đọc nhãn và thứ tự các mục menu | Mục thứ hai là **"Cập nhật thông tin"**, nằm **dưới** "Quà đã nhận" — hết dạng ghi-nhận, assert được | P2 | UI | MODIFIED |

#### Source Detail per Scenario (verbatim quotes)

##### SC-USR-013 / SC-USR-014 / SC-USR-015 / SC-USR-016 — Màn "Cập nhật thông tin": lối vào, happy path, negative, vùng chỉ đọc
📍 `DOC-v1.1-01 §8.15 · trang 48` · `§8.15.1 BR15-01 / BR15-02 / BR15-05 · trang 48-49` · `§8.15.2 · trang 49` · `§6.2 AC-30.1.01 / AC-30.1.02 / AC-30.2.01 · trang 28`

> Trigger (§8.15): "Mở "Cập nhật thông tin" trong trang cá nhân (nằm dưới mục "Quà đã nhận")"

> `AC-30.1.01` Then: "Hiện banner xanh "Đã lưu thông tin của bạn", banner tự ẩn khi người dùng sửa tiếp."

> `AC-30.1.02` Then: "Không lưu. Hiện lỗi ngay dưới ô số điện thoại. Số điện thoại mặc định là bắt buộc, đúng định dạng Việt Nam (10 số, đầu 0)."

> `AC-30.2.01` Then: "Các trường này hiển thị chỉ đọc; email công ty kèm icon khoá và không có ô nhập. Dữ liệu đồng bộ từ tài khoản nội bộ (SSO), người dùng không sửa được."

**Analyst Note:** ⭐ **Cả một màn mới xuất hiện ở module mà lượt delta trước khai là "không có delta".** Fan-out 4 SC theo 4 trục fail độc lập: **lối vào** (`SC-USR-013` — có đúng mục menu, đúng vị trí) · **happy path** (`SC-USR-014` — lưu được, banner đúng chuỗi, giá trị thật sự persist) · **negative của trường bắt buộc** (`SC-USR-015` — 2 dạng invalid: trắng và sai định dạng) · **vùng chỉ đọc** (`SC-USR-016` — 4 trường SSO, riêng email có icon khoá).
⚠️ **`SC-USR-014` bắt buộc có bước "mở lại màn để kiểm giá trị đã persist"** — banner xanh chỉ chứng minh app *nói* đã lưu, không chứng minh *đã lưu*. Đây là khác biệt giữa TC bắt được lỗi và TC PASS cho một màn hỏng.
🔴 **Rủi ro tiền đề lớn nhất:** app STG quan sát 2026-07-24 là **view-only hoàn toàn** — nếu chưa build `FR15` thì **cả 8 SC mới `BLOCKED`**, không phải FAIL. Xem `RISK-USR-06`.

---

##### SC-USR-017 / SC-USR-018 — Hai chiều độc lập của rule truy vết
📍 `DOC-v1.1-01 §8.15.1 BR15-03 / BR15-04 · trang 49` · `§6.2 AC-30.2.02 / AC-30.1.01 · trang 28`

> `BR15-03`: "Sửa hồ sơ không làm thay đổi các đơn đã tạo — đơn giữ nguyên số điện thoại/địa chỉ tại thời điểm đăng."

> `AC-30.2.02` Then: "Các đơn đã tạo giữ nguyên số điện thoại và địa chỉ tại thời điểm đăng (phục vụ truy vết). Chỉ đơn tạo mới dùng giá trị mới."

> `BR15-04`: "…người dùng vẫn sửa trong từng đơn mà không ghi lại hồ sơ."

**Analyst Note:** ⭐ **Hai chiều ngược nhau, fail độc lập, và cùng âm thầm** ⇒ ⛔ không gộp 1 SC.
`SC-USR-017` (**P1**) bảo vệ **đơn cũ** khỏi bị hồ sơ ghi đè — nếu backend lưu đơn bằng **tham chiếu** tới hồ sơ thay vì **chụp giá trị tại thời điểm đăng**, thì đổi SĐT hồ sơ sẽ viết lại cả lịch sử đơn. Không crash, không cảnh báo, chỉ là **dữ liệu truy vết bị thay đổi** — đúng loại lỗi mà `AC-30.2.02` viết chữ *"phục vụ truy vết"* để phòng.
`SC-USR-018` bảo vệ **hồ sơ** khỏi bị từng đơn ghi đè — chiều này dễ bị bỏ sót hơn vì nghe như "tiện" (sửa trong đơn rồi nhớ luôn cho lần sau), nhưng PRD nói rõ **không**.
⚠️ **Cả 2 SC bắt buộc có bước "ghi lại giá trị TRƯỚC"** — không có bước đó thì không phát hiện được gì.
🔴 **Nhóm rule truy vết, thành viên thứ tư:** cùng họ `BR11-03` (`SC-CNL-010`) · `BR18-05` (`SC-ORD-065`) · `NFR-07` (`SC-DLV-062`). App **đã vi phạm nhóm này 1 lần đã live-verify** (`KB-CNL-01`) ⇒ chạy `SC-USR-017` **cùng lô** với 3 SC kia, gộp 1 bug report nếu cùng vỡ.

---

##### SC-USR-003 — Lật một phần: "view-only hoàn toàn" không còn đúng
📍 `DOC-v1.1-01 §8.15 Description · trang 48` · `§8.15.1 BR15-01 · trang 48`

> Description: "Cho phép sửa số điện thoại và địa chỉ mặc định dùng để prefill khi đăng tin; các trường đồng bộ từ SSO là chỉ đọc."

> `BR15-01`: "Tên, phòng ban · MNV và email công ty là chỉ đọc — đồng bộ từ SSO; email hiển thị kèm icon khoá, không có ô nhập."

**Analyst Note (diff):** 🔴 **SC này có Then NGƯỢC NHAU giữa 2 bản, và cả hai bản đều chạy được nên không có gì báo lỗi nếu lấy nhầm.** Bản v1.0: *"KHÔNG có bất kỳ control sửa nào; mọi trường chỉ đọc"* — PASS nghĩa là **không tìm thấy** đường sửa. Bản v1.1: hồ sơ có **2 vùng** — vùng SSO chỉ đọc (phần v1.0 đúng, **giữ lại**) và vùng sửa được qua màn "Cập nhật thông tin" (phần v1.0 **sai**).
⚠️ **Giữ SC này ở phạm vi hẹp — chỉ trang Cá nhân, không sửa trực tiếp trên từng trường.** Phần assert `BR15-01` chi tiết (icon khoá, không có ô nhập) chuyển sang `SC-USR-016` vì nó thuộc **màn "Cập nhật thông tin"**, một màn khác. Trộn 2 màn vào 1 SC là cách nhanh nhất để TC vừa dài vừa không kết luận được gì.
📌 **Đây là lần đảo kết luận thứ hai của dự án**, cùng khuôn với `SC-CNL-006` (`C-CNL-01`). Điểm chung: cả hai kết luận v1.0 đều Resolved **theo quan sát app**, không theo tài liệu — và PRD chính thức lật cả hai. Bài học ghi ở `CHANGELOG.md §2`.

---

##### SC-USR-012 / SC-USR-002 — Menu trang cá nhân có tên; nhưng danh sách trường vẫn chưa đủ bằng chứng
📍 `DOC-v1.1-01 §8.15 dòng Trigger · trang 48` · `§8.15.2 UI/Field Spec · trang 49`

> Trigger: "Mở "Cập nhật thông tin" trong trang cá nhân (nằm dưới mục "Quà đã nhận")"

**Analyst Note (diff):** Một dòng `Trigger` đóng được **một nửa** `C-USR-04`: trang Cá nhân có ít nhất 2 mục menu **theo thứ tự xác định** ⇒ `SC-USR-012` hết `[GAP]`, nâng **P3 → P2**.
⚠️ **Nửa còn lại vẫn Open, và đây là chỗ dễ kết luận sai:** `§8.15.2` liệt kê trường của **màn "Cập nhật thông tin"** — ⛔ **không phải** danh sách trường hiển thị trên **trang Cá nhân**. Hai màn khác nhau; `SC-USR-002` (trang Cá nhân) **không được** lấy `§8.15.2` làm nguồn. ⇒ `C-USR-04` chuyển **Partially Resolved**, ⛔ không đóng hẳn.

---

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| SC-USR-001 | Đăng nhập SSO | USR | v1.0 | P1 | → `v1.0/USR-tai-khoan/test_scenario_map.md` — PRD §4 xác nhận lại *"đăng nhập bằng SSO nội bộ FTEL"* |
| SC-USR-004 | Định danh & tin cậy | USR | v1.0 | P2 | → như trên |
| SC-USR-005 | Chỉ số đóng góp | USR | v1.0 | P2 | → như trên — ⚠️ `BR14-04` thêm rule *"không tính đơn RETURNED"*, home ở `GIFT` (`SC-GIFT-014`) |
| SC-USR-006 | Loại trừ điểm/tier/CO₂ | USR | v1.0 | P2 | → như trên — `BR14-03` + §4 Out of Scope **củng cố** (nay là loại trừ vĩnh viễn, không phải hoãn) |
| SC-USR-007 | Badge hạng thành viên | USR | v1.0 | P3 | → như trên — `C-USR-01` vẫn Resolved *out of scope*; PRD không nhắc |
| SC-USR-008 | Điều hướng "Đơn của tôi" | USR | v1.0 | P3 | → như trên |
| SC-USR-009 | Điều hướng "Quà đã nhận" | USR | v1.0 | P3 | → như trên — `FR15` Trigger xác nhận mục này **tồn tại và nằm trên** "Cập nhật thông tin" |
| SC-USR-010 | [GAP] Cấu hình kênh liên hệ | USR | v1.0 | P3 | → như trên — `C-USR-02` vẫn Resolved *out of scope*; ⚠️ PRD **cũng không nhắc**, xem `C-USR-05` |
| SC-USR-011 | Completeness header | USR | v1.0 | P3 | → như trên |

> ℹ️ **9 SC CARRIED** — `SC-USR-002` `003` `012` KHÔNG ở bảng này vì đã MODIFIED (xem §NEW & MODIFIED).

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
