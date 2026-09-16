---
id: v1.1/USR-tai-khoan/scenario-map
title: Test Scenario Map — v1.1 · Module USR
type: scenario-map
version: v1.1
sprint: 1
module: USR
counts:
  req: 10
  sc: 24
  new: 12
  modified: 5
  carried: 7
  deprecated: 0
  p1: 3
  p2: 14
  p3: 7
status: ANALYZED
updated: 2026-09-16
---

# Test Scenario Map — v1.1 · Module USR

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module USR **tính tới v1.1** (bao gồm CARRIED từ v1.0).
> Parent: `v1.0/USR-tai-khoan/` — 9 SC không đổi (CARRIED), 3 SC MODIFIED (giữ ID v1.0, bản v1.1 authoritative), 8 SC NEW.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Delta lần này fan-out theo: 1 happy path màn mới · 1 negative (SĐT bắt buộc) · **2 chiều độc lập của rule truy vết** (hồ sơ→đơn ⟷ đơn→hồ sơ) · vùng chỉ-đọc SSO · 2 chi tiết UI (banner tự ẩn · trường không bắt buộc).
> Trần: vế *"wizard nhận đúng giá trị prefill"* có home ở **`ORD`** (`SC-ORD-025`) — ⛔ không nhân bản; ở đây chỉ giữ vế *"hồ sơ có bị ghi đè không"*.

## Tổng quan
- Tổng số scenarios (tính tới v1.1): **24** (NEW: 12, MODIFIED: 5, CARRIED: 7)
- Phân bổ priority: P1: 3 | P2: 14 | P3: 7
- Delta lớn nhất: **`C-USR-03` bị ĐẢO** — màn Cá nhân từ *view-only hoàn toàn* thành *có màn "Cập nhật thông tin" sửa được 2 trường*; `SC-USR-003` phải lật chiều.
- ⚠️ **2 SC P1 mới đều thuộc nhóm rule truy vết** (`SC-USR-017` · `SC-USR-014`) — nhóm mà app đã vi phạm 1 lần đã live-verify.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### USR — Tài khoản & Hồ sơ (delta v1.1)

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-USR-013 | Mở màn "Cập nhật thông tin" đúng vị trí | REQ-USR-008, REQ-USR-006 | DOC-v1.1-01 §8.15 dòng Trigger | Đã đăng nhập SSO, đang ở trang Cá nhân | Cuộn hết trang, đọc thứ tự các mục menu | Có mục **"Cập nhật thông tin"** nằm **dưới mục "Quà đã nhận"**; bấm vào mở được màn tương ứng: header có nút **←** + tiêu đề "Cập nhật thông tin"; màn **KHÔNG có thanh tab dưới cùng**. Đây là **lối vào duy nhất** của màn (PRD `Trigger` chỉ nêu 1 lối) | P2 | UI | NEW |
| SC-USR-014 | Sửa SĐT + địa chỉ mặc định → lưu thành công | REQ-USR-008 | DOC-v1.1-01 §8.15.1 BR15-02, BR15-05 · §6.2 AC-30.1.01 | Đang ở màn "Cập nhật thông tin"; ghi lại giá trị SĐT và địa chỉ **hiện tại** | Sửa SĐT sang 1 số VN hợp lệ khác + đổi địa chỉ mặc định (**gõ từ khoá → chọn 1 văn phòng trong danh sách**, `SC-USR-021`), bấm "Lưu thay đổi"; sau đó bấm **←** | Hiện **banner xanh đúng chuỗi** "Đã lưu thông tin của bạn"; sau khi lưu **vẫn ở lại màn** (không tự điều hướng); bấm ← ⇒ về **trang Cá nhân**; mở lại màn thấy **giá trị mới** đã lưu | P1 | Functional | NEW |
| SC-USR-015 | SĐT mặc định bắt buộc: bắt đầu bằng 0, đúng 10 ký tự, tất cả là số | REQ-USR-008 | DOC-v1.1-01 §8.15.1 BR15-02 · §8.15.2 · §6.2 AC-30.1.02 · BA chốt 2026-09-16 | Đang ở màn "Cập nhật thông tin" | Lần lượt nhập rồi bấm Lưu: **trống** · `123` · `0912345` (**9 số**) · `09123456789` (**11 số**) · `1912345678` (**không bắt đầu 0**) · `84901234567` · `+84912345678` · `0912 345 678` (**có khoảng trắng**) · `09123a5678` (**có chữ**) | Tất cả: **KHÔNG lưu**, hiện lỗi **ngay dưới ô số điện thoại**; giá trị đã lưu giữ nguyên. Đối chứng: `0912345678` lưu được | P2 | Business Rule | NEW |
| SC-USR-016 | Trường đồng bộ SSO là chỉ đọc | REQ-USR-008, REQ-USR-002 | DOC-v1.1-01 §8.15.1 BR15-01 · §8.15.2 · §6.2 AC-30.2.01 | Đang ở màn "Cập nhật thông tin" | Thử chạm/sửa lần lượt: Avatar · Tên · Phòng ban · MNV · Email công ty | Cả 4 trường **chỉ đọc, không có ô nhập**; riêng **Email công ty hiển thị kèm icon KHIÊN** (⚠ PRD ghi *"icon khoá"* — BA chốt 2026-09-16 theo UI là **khiên**). Avatar hiện **chữ viết tắt** (cùng rule `SC-USR-002`), **không có control đổi ảnh** | P2 | Business Rule | NEW |
| SC-USR-017 | Sửa hồ sơ KHÔNG làm đổi đơn đã tạo | REQ-USR-009 | DOC-v1.1-01 §8.15.1 BR15-03 · §6.2 AC-30.2.02 | Có **≥ 1 đơn đã tạo trước đó**; ghi lại SĐT + địa chỉ lấy hàng **hiển thị trên đơn đó** | Vào "Cập nhật thông tin", đổi **cả** SĐT và địa chỉ mặc định, lưu; quay lại mở **đúng đơn cũ** | Đơn cũ **giữ nguyên** SĐT/địa chỉ tại thời điểm đăng (*"phục vụ truy vết"*); chỉ đơn **tạo mới** dùng giá trị mới | P1 | Business Rule | NEW |
| SC-USR-018 | Sửa trong từng đơn KHÔNG ghi ngược lại hồ sơ | REQ-USR-010 | DOC-v1.1-01 §8.15.1 BR15-04 · §6.2 AC-30.1.01 | Hồ sơ đã có SĐT mặc định **X** và địa chỉ mặc định **Y** (ghi lại) | Mở wizard đăng tin, sửa ô SĐT người gửi thành **X'** và địa chỉ lấy hàng thành **Y'**, đăng tin xong; quay lại "Cập nhật thông tin" | Hồ sơ **vẫn là X và Y** — ⛔ không bị ghi đè thành X'/Y' (`BR15-04`: *"mà không ghi lại hồ sơ"*) | P2 | Business Rule | NEW |
| SC-USR-019 | Banner tự ẩn khi người dùng sửa tiếp | REQ-USR-008 | DOC-v1.1-01 §8.15.1 BR15-05 | Vừa lưu thành công, banner xanh **đang hiển thị** | Chạm vào ô SĐT hoặc địa chỉ và sửa tiếp | Banner **tự ẩn** khi bắt đầu sửa; ⛔ không cần bấm đóng thủ công | P3 | UI | NEW |
| SC-USR-020 | Gõ tay không chọn từ danh sách → ô rỗng, lưu rỗng | REQ-USR-008 | BA chốt 2026-09-16 (`C-USR-05` rule địa chỉ) · DOC-v1.1-01 §8.15.2 | Đang ở màn "Cập nhật thông tin", SĐT hợp lệ, ô địa chỉ **đang có giá trị** (ghi lại) | Gõ 1 chuỗi bất kỳ (vd `asdfghjkl1`) **nhưng KHÔNG chọn** mục nào trong danh sách → **bấm ra ngoài ô** → bấm "Lưu thay đổi" → thoát ra, mở lại màn | Ra khỏi ô ⇒ ô **bị xoá thành rỗng** (⛔ không giữ chuỗi gõ tay, ⛔ không quay về giá trị cũ); Lưu **thành công** (để trống là hợp lệ); mở lại màn ô địa chỉ **vẫn rỗng** — ⛔ **không tự load lại địa chỉ HRIS** | P2 | Business Rule | NEW |
| SC-USR-021 | Gõ ≥ 3 ký tự → gợi ý văn phòng theo tên (không phân biệt dấu, hoa thường) → chọn | REQ-USR-008 | BA chốt 2026-09-16 (`C-USR-05` rule địa chỉ) | Đang ở màn "Cập nhật thông tin"; có file danh sách văn phòng `DOC-v1.1-04` làm oracle; bộ từ khoá K1–K6 ở `04_test-data/valid/USR-office-catalog.md` | Xoá ô địa chỉ; gõ lần lượt: `fp` (2 ký tự) → `fpt` (3 ký tự); `Lê Thái Tổ`; 3 dạng `Cẩm Lệ` · `cam le` · `CAM LE`; `xyz`; `hcm`; `tan`; cuối cùng chọn 1 mục | `fp`: **chưa gợi ý** · `fpt`: **8** văn phòng · `Lê Thái Tổ`: **1** · 3 dạng Cẩm Lệ: **cùng 2** văn phòng · `xyz`: **không hiện gợi ý** (không có dòng thông báo) · `hcm`: **không hiện gợi ý** (chỉ tìm theo tên, không theo mã tỉnh) · `tan`: **36** (khớp **chứa chuỗi**, gồm cả "Tầng…") · chọn 1 mục ⇒ ô điền **đúng chuỗi `name`** của văn phòng · chọn 1 mục ⇒ ô điền đúng văn phòng đó, giữ nguyên khi ra khỏi ô | P2 | Functional | NEW |
| SC-USR-022 | Địa chỉ mặc định khởi tạo từ HRIS, đã lưu thì ưu tiên giá trị đã lưu | REQ-USR-008 | BA chốt 2026-09-16 · DOC-v1.1-01 §8.15.2 cột Kiểu (*"địa chỉ làm việc trong hồ sơ"*) | (A) Tài khoản **chưa từng lưu** địa chỉ mặc định, HRIS **có** địa chỉ làm việc · (B) chưa từng lưu, HRIS **không có** địa chỉ · (C) tài khoản **đã lưu** 1 văn phòng khác địa chỉ HRIS | Mở màn "Cập nhật thông tin" | (A) Ô hiển thị sẵn **đúng địa chỉ làm việc theo HRIS**, sửa được · (B) Ô **rỗng** · (C) Ô hiển thị **giá trị đã lưu**, ⛔ không bị HRIS ghi đè | P2 | Functional | NEW |
| SC-USR-023 | SĐT mặc định khởi tạo từ HRIS | REQ-USR-008 | BA chốt 2026-09-16 · DOC-v1.1-01 §8.15.2 cột Kiểu (*"số điện thoại hiện tại"*) | (A) Tài khoản **chưa từng lưu** SĐT mặc định, HRIS **có** SĐT · (B) chưa từng lưu, HRIS **không có** SĐT | Mở màn "Cập nhật thông tin"; ở (B) bấm "Lưu thay đổi" luôn | (A) Ô SĐT hiển thị sẵn **đúng SĐT theo HRIS**, sửa được · (B) Ô SĐT **rỗng**; bấm Lưu ⇒ **bị chặn**, lỗi dưới ô (SĐT bắt buộc — `BR15-02`). Trường hợp đã lưu trước đó ⇒ hiện giá trị đã lưu: kiểm ở `SC-USR-014` | P2 | Functional | NEW |
| SC-USR-024 | Thoát màn khi chưa lưu → bỏ thay đổi, không hỏi xác nhận | REQ-USR-008 | BA chốt 2026-09-16 (`C-USR-05`) | Đang ở màn "Cập nhật thông tin"; ghi lại SĐT + địa chỉ **đang lưu** | Sửa SĐT sang số hợp lệ khác + chọn 1 văn phòng khác, **KHÔNG bấm Lưu**, bấm ← quay lại trang Cá nhân; mở lại màn | Bấm ← **quay ra ngay**, ⛔ **không có hộp thoại/cảnh báo** xác nhận nào; mở lại màn thấy **giá trị cũ** — thay đổi chưa lưu **bị bỏ**, ⛔ không được giữ lại dạng bản nháp. ⚠ Demo v4.0 **giữ bản nháp** khi mở lại ⇒ lệch rule; STG giống demo là **defect** | P3 | Functional | NEW |
| SC-USR-003 | Vùng SSO của hồ sơ vẫn chỉ đọc *(lật một phần)* | REQ-USR-002 | DOC-v1.1-01 §8.15.1 BR15-01 · §8.15 Description | Đang ở **trang Cá nhân** (không phải màn "Cập nhật thông tin") | Rà toàn bộ trang tìm control sửa trực tiếp trên từng trường | Tên · phòng ban · MNV · email **không sửa trực tiếp được tại trang Cá nhân**. ⚠ **KHÁC v1.0**: nay **CÓ** lối vào màn sửa qua mục "Cập nhật thông tin" ⇒ ⛔ không assert *"không có bất kỳ control sửa nào"* | P2 | Business Rule | MODIFIED |
| SC-USR-002 | Hồ sơ cá nhân — các trường hiển thị *(hết gap 2026-09-16)* | REQ-USR-002 | Vibe-check demo 2026-09-16 (`00_input/v1.1/design/USR_01...png`) | Đã vào FoxEco bằng tài khoản có hồ sơ đầy đủ | Mở tab "Cá nhân" | Hiển thị đúng: avatar = **chữ viết tắt ghép từ chữ cái đầu của 2 từ cuối trong Tên** (vd "Trần Văn A" → "VA"; "Đồng Công Chí Linh" → "CL"), **không dấu** (vd "Đặng Ánh" → "DA") — ⛔ không phải icon người mặc định; **giống hệt** avatar ở màn "Cập nhật thông tin" · Tên · "[Phòng ban] · MNV: [mã]" · 2 chỉ số "[N] đơn đã giúp" / "[N] quà đã nhận" · 3 mục menu đúng thứ tự "Đơn của tôi" → "Quà đã nhận" → "Cập nhật thông tin". ⛔ KHÔNG gồm SĐT/Email/Địa chỉ — 3 trường đó chỉ ở màn "Cập nhật thông tin" (`SC-USR-013..016`), không lấy `§8.15.2` làm danh sách cho màn này. **KHÔNG có** badge "Hạng Đồng hành" (`C-USR-06` chốt 2026-09-16 — assert ở `SC-USR-007`) | P2 | UI | MODIFIED |
| SC-USR-012 | Nhãn mục menu thứ hai *(hết gap)* | REQ-USR-006 | DOC-v1.1-01 §8.15 dòng Trigger | Đang ở trang Cá nhân | Đọc nhãn và thứ tự các mục menu | Mục thứ hai là **"Cập nhật thông tin"**, nằm **dưới** "Quà đã nhận" — hết dạng ghi-nhận, assert được | P2 | UI | MODIFIED |
| SC-USR-007 | KHÔNG hiển thị badge "Hạng Đồng hành" *(lật chiều)* | REQ-USR-007 | DOC-v1.1-01 §8.14.1 BR14-03 · §6.2 AC-26.1.01 · §4 Out of Scope · BA chốt 2026-09-16 (`C-USR-06`) | Đang ở trang Cá nhân | Rà vùng header dưới Tên + "Phòng ban · MNV" | **KHÔNG có** badge/nhãn "Hạng Đồng hành" hay bất kỳ nhãn hạng/tier nào. ⚠ **KHÁC v1.0** (v1.0 assert badge **tồn tại**). Demo 2026-09-16 vẫn hiện badge ⇒ nếu STG còn hiện là **defect** | P3 | Business Rule | MODIFIED |
| SC-USR-011 | Completeness header trang Cá nhân *(cập nhật cấu trúc)* | REQ-USR-007 | DOC-v1.1-01 §8.15 Trigger · BA chốt 2026-09-16 (`C-USR-05(a)`, `C-USR-06`) · ảnh `USR_01` | Đang ở trang Cá nhân | Đối chiếu từng thành phần header + menu | Đủ và đúng thứ tự: avatar **chữ viết tắt** · Tên · "Phòng ban · MNV" · card 2 chỉ số · **3** mục menu ("Đơn của tôi" → "Quà đã nhận" → "Cập nhật thông tin"). ⛔ **Không** có badge hạng. ⛔ Không assert giá trị số | P3 | UI | MODIFIED |

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

##### SC-USR-012 / SC-USR-002 — Menu trang cá nhân có tên; danh sách trường hết gap qua demo 2026-09-16
📍 `DOC-v1.1-01 §8.15 dòng Trigger · trang 48` · `§8.15.2 UI/Field Spec · trang 49` · vibe-check demo 2026-09-16

> Trigger: "Mở "Cập nhật thông tin" trong trang cá nhân (nằm dưới mục "Quà đã nhận")"

> Ảnh `00_input/v1.1/design/USR_01_trangcanhan_fields_CUSR04.png` — trang Cá nhân: avatar (placeholder) · Tên · "Phòng Kỹ thuật · MNV: FTEL2291" · badge "Hạng Đồng hành" (ngoài đặc tả, không assert) · "12 đơn đã giúp" / "8 quà đã nhận" · menu "Đơn của tôi" → "Quà đã nhận" → "Cập nhật thông tin".
> Ảnh `00_input/v1.1/design/USR_02_capnhatthongtin_fields.png` — màn "Cập nhật thông tin": avatar chữ tắt "CL" + Tên + Phòng ban/MNV (đọc) · Số điện thoại mặc định (sửa được) · Email công ty (icon khiên, chỉ đọc) · Địa chỉ mặc định (sửa được) · nút "Lưu thay đổi".

**Analyst Note (diff):** `SC-USR-012` hết `[GAP]` từ dòng `Trigger` (nâng P3 → P2, không đổi ở lượt này). **`SC-USR-002` hết gap ở lượt 2026-09-16** nhờ 2 ảnh trên — xác nhận trực tiếp trang Cá nhân và màn "Cập nhật thông tin" là **hai màn có hai bộ trường khác nhau**, đúng nghi vấn đã nêu từ 2026-09-15. `§8.15.2` **vẫn chỉ** là field spec của màn "Cập nhật thông tin" — ⛔ không dùng cho `SC-USR-002`, giờ đã có nguồn riêng (ảnh demo) thay vì phải mượn `§8.15.2`. `C-USR-04` **Resolved 2026-09-16** — xem `risk_assessment.md`.
⛔ **Cập nhật 2026-09-16 — mô tả avatar *"(placeholder)"* của ảnh `USR_01` phía trên KHÔNG dùng làm oracle.** BA chốt: avatar trang Cá nhân và màn "Cập nhật thông tin" là **một**, hiện **chữ viết tắt từ 2 từ cuối của Tên** (`C-USR-05(a)`). Demo trang Cá nhân đang hiện icon người ⇒ **lệch rule**; nếu STG cũng hiện icon thì đó là defect, không phải hành vi đúng. Chữ viết tắt hiển thị **không dấu** (BA chốt 2026-09-16: "Đặng Ánh" → "DA"). Tên **luôn có ≥ 2 từ** (BA chốt: "Trần A" → "TA") ⇒ không có trường hợp tên 1 từ.

---

##### SC-USR-019 — Banner lưu thành công tự ẩn khi sửa tiếp
📍 `DOC-v1.1-01 §8.15.1 BR15-05 · trang 49` · `§6.2 AC-30.1.01 · trang 28`

> ↪ *Quote `BR15-05` — home ở `requirement_traceability.md` · `REQ-USR-008`; quote `AC-30.1.01` Then — ở khối `SC-USR-013 / … / SC-USR-016` phía trên (cùng file)*

**Analyst Note:** Tách khỏi `SC-USR-014` vì là hành vi **sau** khi lưu, fail độc lập (banner có thể hiện đúng nhưng không bao giờ tự ẩn, hoặc ẩn ngay trước khi người dùng đọc được). Điều kiện ẩn theo PRD là *"khi người dùng **sửa tiếp**"* ⇒ TC phân biệt 2 thao tác: **chỉ chạm/focus** vào ô (PRD không nói — ghi nhận) và **thay đổi nội dung** ô (phải ẩn). ⛔ Không assert banner tự ẩn theo thời gian — PRD không có mốc thời gian. Chuỗi banner verbatim *"Đã lưu thông tin của bạn"* assert ở `SC-USR-014`, ⛔ không lặp.

---

##### SC-USR-020 / SC-USR-021 / SC-USR-022 — Địa chỉ mặc định: load HRIS, gợi ý từ 3 ký tự, chọn từ danh sách, rời ô không chọn thì rỗng
📍 BA trả lời · 2026-09-16 (2 lượt) · đối chiếu `DOC-v1.1-01 §8.15.2 dòng "Địa chỉ mặc định" · trang 49`

> ↪ *Quote field spec "Địa chỉ mặc định" (PRD) — home ở `requirement_traceability.md` · `REQ-USR-008`; quote rule BA — home ở `risk_assessment.md` · `C-USR-05 · ↳ Rule địa chỉ mặc định`*

**Analyst Note:** ⛔ **Bản đầu của `SC-USR-020` (*"không bắt buộc, ≤ 200 ký tự"* — biên 200/201) HẾT HIỆU LỰC 2026-09-16**, và bản giữa ngày (*"gõ tay thì mở lại vẫn là địa chỉ cũ"*) cũng **HẾT HIỆU LỰC** — BA chốt: rời ô không chọn ⇒ **ô rỗng, lưu rỗng**.
Fan-out 3 SC theo 3 trục fail độc lập: **nguồn giá trị khi mở màn** (`SC-USR-022` — HRIS có / HRIS trống / đã lưu trước đó) · **gợi ý + chọn** (`SC-USR-021` — biên 2/3 ký tự) · **text gõ tay** (`SC-USR-020` — rời ô ⇒ rỗng).
⚠️ **Bẫy dễ bỏ sót:** `SC-USR-020` mở lại màn phải **vẫn rỗng**. Nếu app coi *"rỗng"* = *"chưa có giá trị"* rồi load lại HRIS thì vi phạm (C) của `SC-USR-022` — kiểu lỗi không crash, chỉ âm thầm đổi dữ liệu người dùng đã chủ động xoá.
✅ **Rule tìm kiếm (BA chốt 2026-09-16):** tìm theo **tên văn phòng** · **không phân biệt dấu** · **không phân biệt hoa thường** · không khớp ⇒ **không hiện gợi ý**.
✅ **Test data đã có (2026-09-16):** `DOC-v1.1-04` — 399 văn phòng; từ khoá + kỳ vọng ở `04_test-data/valid/USR-office-catalog.md`. ⚠ 118 tên bị cắt 30 ký tự và có tên dính chữ (`TânThuận`) — ⛔ đừng coi là lỗi tìm kiếm.
⚠️ **Demo lệch rule:** ô địa chỉ demo là `textarea` tự do, không gợi ý, không validate ⇒ không dùng làm oracle; chạy trên STG.
🔗 **Hệ quả chéo `ORD`:** lưu rỗng ⇒ ô **địa chỉ lấy hàng** lần đăng tin sau (`SC-ORD-025`) không được điền sẵn — ⛔ không nhân bản SC ở đây. Prefill sang **địa chỉ giao hàng / điểm xuất phát**: BA xác nhận **CÓ** (2026-09-16) — home ở `ORD`/`ASN`, ⛔ không tạo SC ở `USR`.

---


##### SC-USR-007 / SC-USR-011 — Badge "Hạng Đồng hành" bị gỡ; header trang Cá nhân cập nhật
📍 `DOC-v1.1-01 §8.14.1 BR14-03 · trang 48` · `§6.2 AC-26.1.01 · trang 27` · BA chốt 2026-09-16

> ↪ *Quote `BR14-03` / `AC-26.1.01` / `§4 Out of Scope` — home ở `risk_assessment.md` · `C-USR-06`*

**Analyst Note (diff):** 🔴 **`SC-USR-007` lật chiều như `SC-USR-003`** — bản v1.0 PASS khi badge **có**, bản v1.1 PASS khi badge **không có**; cả hai đều chạy được ⇒ ⛔ phải lấy bản `v1.1/`. `SC-USR-011` v1.0 liệt kê *"badge hạng · 2 mục menu"* — nay sai 3 chỗ (không badge · 3 mục menu · avatar chữ viết tắt) ⇒ MODIFIED, giữ P3.

---

##### SC-USR-015 / SC-USR-023 — SĐT mặc định: định dạng và nguồn khởi tạo
📍 `DOC-v1.1-01 §8.15.1 BR15-02 · §8.15.2 · trang 49` · BA chốt 2026-09-16

> ↪ *Quote `BR15-02` / field spec SĐT — home ở `requirement_traceability.md` · `REQ-USR-008`; quote BA — home ở `risk_assessment.md` · `C-USR-05 · ↳ BA trả lời lượt 4`*

**Analyst Note:** Rule SĐT chốt: **bắt đầu bằng 0 · đúng 10 ký tự · cả 10 là số** ⇒ khoảng trắng, `+84`, chữ đều **invalid**. ⚠️ Demo hiển thị `0912 345 678` (có khoảng trắng) — nếu STG cũng **hiển thị** có khoảng trắng thì đó là định dạng hiển thị; chỉ assert: **gõ** chuỗi có khoảng trắng thì bị chặn. Text lỗi: PRD không có ⇒ ⛔ không assert chuỗi (demo: *"Vui lòng nhập số điện thoại"* / *"Số điện thoại không hợp lệ (10 số, bắt đầu bằng 0)"*).
`SC-USR-023` tách khỏi `SC-USR-022` (địa chỉ) vì 2 trường khởi tạo độc lập, fail độc lập; nhánh (B) HRIS không có SĐT ⇒ ô rỗng và **Lưu bị chặn** — người dùng buộc phải nhập SĐT trước khi lưu được địa chỉ.

---

##### SC-USR-024 — Thoát màn khi chưa lưu
📍 BA trả lời · 2026-09-16

> ↪ *Quote BA — home ở `risk_assessment.md` · `C-USR-05 · ↳ BA trả lời lượt 5`*

**Analyst Note:** PRD không mô tả hành vi thoát màn. BA chốt: **không lưu, không hiện xác nhận**. Assert 2 vế độc lập: (1) không có hộp thoại chặn đường ra; (2) giá trị chưa lưu **không** bị lưu ngầm. ⚠️ Vế (2) phải có bước **ghi lại giá trị TRƯỚC** — cùng lý do `SC-USR-014`. Nếu dùng tài khoản đang ở trạng thái "chưa lưu" (giá trị từ HRIS) thì mở lại phải vẫn thấy giá trị HRIS.
🔴 **Demo lệch rule (phát hiện 2026-09-16 khi đọc code `DOC-v1.1-02`):** handler nút ← (`goProfile`) và mở màn (`goEditProfile`) **không xoá** state nháp `profilePhone`/`profileAddr` ⇒ sửa → bấm ← → mở lại vẫn thấy **giá trị chưa lưu**. Đây là hành vi dễ bị copy sang app thật — nhìn giống "đã lưu" dù chưa bấm Lưu. ⛔ Không dùng demo làm oracle; STG giống demo ⇒ log defect.

---

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| SC-USR-001 | Đăng nhập SSO | USR | v1.0 | P1 | → `v1.0/USR-tai-khoan/test_scenario_map.md` — PRD §4 xác nhận lại *"đăng nhập bằng SSO nội bộ FTEL"* |
| SC-USR-004 | Định danh & tin cậy | USR | v1.0 | P2 | → như trên |
| SC-USR-005 | Chỉ số đóng góp | USR | v1.0 | P2 | → như trên — ⚠️ `BR14-04` thêm rule *"không tính đơn RETURNED"*, home ở `GIFT` (`SC-GIFT-014`) |
| SC-USR-006 | Loại trừ điểm/tier/CO₂ | USR | v1.0 | P2 | → như trên — `BR14-03` + §4 Out of Scope **củng cố** (nay là loại trừ vĩnh viễn, không phải hoãn) |
| SC-USR-008 | Điều hướng "Đơn của tôi" | USR | v1.0 | P3 | → như trên |
| SC-USR-009 | Điều hướng "Quà đã nhận" | USR | v1.0 | P3 | → như trên — `FR15` Trigger xác nhận mục này **tồn tại và nằm trên** "Cập nhật thông tin" |
| SC-USR-010 | [GAP] Cấu hình kênh liên hệ | USR | v1.0 | P3 | → như trên — ✅ **2026-09-16 BA: "Kênh liên hệ" bỏ hẳn** (`C-USR-05` câu c) ⇒ Then assert **không tồn tại** bề mặt cấu hình kênh liên hệ, hết dạng GAP chờ |

> ℹ️ **7 SC CARRIED** — `SC-USR-002` `003` `007` `011` `012` KHÔNG ở bảng này vì đã MODIFIED (xem §NEW & MODIFIED).

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
