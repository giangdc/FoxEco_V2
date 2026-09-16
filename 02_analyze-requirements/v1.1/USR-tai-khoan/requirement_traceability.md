# Requirement Traceability — v1.1 · Module USR

> Tạo bởi: analyze-requirements (DELTA 2026-09-15, **lượt bù thứ hai**) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation` của `DOC-v1.1-01` = `FR<NN>` / `BR<FF>-NN` / `AC-{US}.{Scenario}.{Case}` ⇒ **Schema A**.
> Chỉ chứa REQ **NEW + MODIFIED**. REQ CARRIED nguyên trạng — xem `v1.0/USR-tai-khoan/requirement_traceability.md`.
> 🔴 **Module này từng bị khai "không có delta" ngày 2026-09-15 — kết luận đó SAI.** Xem `CHANGELOG.md §1` dòng `ĐÍNH CHÍNH`.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module USR — DOC-v1.1-01

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-USR-008 | `FR15`, `US30`, `BR15-01`, `BR15-02`, `BR15-05`, `AC-30.1.01`, `AC-30.1.02`, `AC-30.2.01` | `DOC-v1.1-01` §8.15 (trang 48-49) · §8.15.1 BR15-01/02/05 · §8.15.2 UI/Field Spec (trang 49) · §6.1 US30 (trang 13) · §6.2 AC-30.1.x/AC-30.2.01 (trang 28) | SC-USR-013, SC-USR-014, SC-USR-015, SC-USR-016, SC-USR-019, SC-USR-020, SC-USR-021, SC-USR-022, SC-USR-023, SC-USR-024 | C-USR-03, C-USR-05 |
| REQ-USR-009 | `BR15-03`, `AC-30.2.02` | `DOC-v1.1-01` §8.15.1 BR15-03 (trang 49) · §6.2 AC-30.2.02 (trang 28) | SC-USR-017 | — |
| REQ-USR-010 | `BR15-04`, `AC-30.1.01` | `DOC-v1.1-01` §8.15.1 BR15-04 (trang 49) · §6.2 AC-30.1.01 (trang 28) | SC-USR-018 | — |
| REQ-USR-002 *(MODIFIED)* | `USR-02` *(v1.0)*, `FR15`, `BR15-01` | `DOC-v1.1-01` §8.15 (trang 48) · §8.15.1 BR15-01 · §8.15.2 (trang 49) | SC-USR-002, SC-USR-003 | C-USR-03, C-USR-05 |
| REQ-USR-006 *(MODIFIED)* | `FR15` Trigger | `DOC-v1.1-01` §8.15 dòng Trigger (trang 48) | SC-USR-008, SC-USR-009, SC-USR-012 | C-USR-04 |

> ℹ️ `REQ-USR-001` · `003` · `004` · `005` · `007` **CARRIED không đổi** — PRD không nhắc tới SSO login, định danh/tin cậy, badge hạng, hay cấu hình kênh liên hệ. ⚠️ `REQ-USR-004` (2 chỉ số đóng góp) **có** chạm gián tiếp qua `BR14-04` (*"Đơn đã giúp" không tính đơn RETURNED*) — nhưng home của rule đó ở `GIFT` (`REQ-GIFT-009`), ⛔ không nhân bản; cross-ref ghi ở `risk_assessment.md RISK-USR-08`.

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-USR-008 · Màn "Cập nhật thông tin" — sửa được SĐT và địa chỉ mặc định (`FR15`)
📍 `DOC-v1.1-01 §8.15 "FR15 — Hồ sơ & cập nhật thông tin" · trang 48-49` · `§8.15.2 UI/Field Spec · trang 49` · `§6.1 US30 · trang 13` · `§6.2 AC-30.1.01 / AC-30.1.02 / AC-30.2.01 · trang 28`  ·  Clarif: `C-USR-03`, `C-USR-05`

> Nguồn #1 — Description + Trigger (§8.15, trang 48):
> "Cho phép sửa số điện thoại và địa chỉ mặc định dùng để prefill khi đăng tin; các trường đồng bộ từ SSO là chỉ đọc."
> "Trigger: Mở "Cập nhật thông tin" trong trang cá nhân (nằm dưới mục "Quà đã nhận")"

> Nguồn #2 — US30 (§6.1, trang 13):
> "Là Người dùng, tôi muốn sửa số điện thoại và địa chỉ mặc định trong hồ sơ, để không phải nhập lại mỗi lần đăng tin."

> Nguồn #3 — `BR15-01` / `BR15-02` / `BR15-05` (§8.15.1, trang 48-49):
> "BR15-01 | Tên, phòng ban · MNV và email công ty là chỉ đọc — đồng bộ từ SSO; email hiển thị kèm icon khoá, không có ô nhập."
> "BR15-02 | Số điện thoại mặc định là bắt buộc, đúng định dạng Việt Nam; không hợp lệ thì không lưu và hiện lỗi ngay dưới ô."
> "BR15-05 | Lưu thành công → banner xanh, tự ẩn khi người dùng sửa tiếp."

> Nguồn #4 — §8.15.2 UI/Field Spec (trang 49):
> "Số điện thoại mặc định | Có | Văn bản · số điện thoại hiện tại | Định dạng Việt Nam (10 số, đầu 0); để trống thì chặn lưu"
> "Địa chỉ mặc định | Không | Văn bản · địa chỉ làm việc trong hồ sơ | ≤ 200 ký tự; dùng làm gợi ý địa chỉ lấy hàng khi đăng tin"

⛔ **Cập nhật 2026-09-16 — đọc *"Văn bản"* thành ô nhập tự do là SAI.** BA chốt: địa chỉ mặc định **load từ HRIS, cho sửa**, sửa bằng **gõ → chọn từ danh sách văn phòng** — xem `risk_assessment.md` · `C-USR-05 · ↳ Rule địa chỉ mặc định`; SC `SC-USR-020..022`.

↳ **Ghi chú:** 🔴 **REQ MỚI, và nó ĐẢO một kết luận v1.0 đã chốt bằng quan sát app.** `C-USR-03` (Resolved 2026-07-24) kết luận màn Cá nhân **view-only hoàn toàn** — căn cứ là QA kiểm trực tiếp app STG, không phải tài liệu. PRD v1.1 đặc tả **một màn riêng** (`"Cập nhật thông tin"`, vị trí cụ thể: *dưới mục "Quà đã nhận"*) với 5 business rule và 4 AC ⇒ **CÓ bề mặt sửa**.
⚠️ **Nhưng không phải "hồ sơ sửa được" — chỉ ĐÚNG 2 TRƯỜNG:** `Số điện thoại mặc định` (bắt buộc) và `Địa chỉ mặc định` (không bắt buộc). 4 trường còn lại mà `USR-02` của BRD liệt kê (*"tên, **avatar**, phòng ban, **khu vực/văn phòng**, **kênh liên hệ**"*) — `BR15-01` khoá cứng tên/phòng ban/MNV/email, còn **avatar · khu vực/văn phòng · kênh liên hệ thì PRD KHÔNG NHẮC Ở ĐÂU** ⇒ mở `C-USR-05`.
⚠️ Phân biệt hai khái niệm dễ lẫn: **"số điện thoại mặc định"** (thuộc hồ sơ, sửa ở đây) ≠ **"số điện thoại người gửi của một đơn"** (thuộc đơn, sửa trong wizard) — `BR15-03`/`BR15-04` nói rõ chúng độc lập; xem `REQ-USR-009`/`REQ-USR-010`.

---

### REQ-USR-009 · Sửa hồ sơ KHÔNG làm thay đổi các đơn đã tạo (`BR15-03`)
📍 `DOC-v1.1-01 §8.15.1 BR15-03 · trang 49` · `§6.2 AC-30.2.02 · trang 28`  ·  Clarif: —

> Nguồn #1 — `BR15-03` (§8.15.1, trang 49):
> "Sửa hồ sơ không làm thay đổi các đơn đã tạo — đơn giữ nguyên số điện thoại/địa chỉ tại thời điểm đăng."

> Nguồn #2 — `AC-30.2.02` (§6.2, trang 28):
> "Given: Người dùng có các đơn đã tạo trước đó. When: Người dùng đổi số điện thoại và địa chỉ mặc định. Then: Các đơn đã tạo giữ nguyên số điện thoại và địa chỉ tại thời điểm đăng (phục vụ truy vết). Chỉ đơn tạo mới dùng giá trị mới."

↳ **Ghi chú:** ⭐ **REQ MỚI — và là thành viên thứ tư của nhóm rule "bằng chứng đã ghi thì bất biến".** Ba thành viên kia: `BR11-03` (không xoá bản ghi lần ghép — `SC-CNL-010`) · `BR18-05` (ảnh đã gắn mốc không xoá được — `SC-ORD-065`) · `NFR-07` (log append-only — `SC-DLV-062`). `AC-30.2.02` dùng đúng cụm **"phục vụ truy vết"** như `BR18-05`, xác nhận đây là cùng một ý đồ thiết kế chứ không phải trùng hợp.
🔴 **Vì sao đáng lo:** app đã **vi phạm** nhóm rule này ít nhất 1 lần đã được live-verify (`KB-CNL-01` — huỷ nhận đơn **xoá** dòng "Ghép thành công"). Nếu backend lưu đơn bằng **tham chiếu tới hồ sơ** thay vì **chụp giá trị tại thời điểm đăng**, thì đổi SĐT hồ sơ sẽ **đổi ngược cả đơn cũ** — lỗi này **âm thầm hoàn toàn**: không crash, không báo gì, chỉ là dữ liệu lịch sử bị viết lại. ⇒ `SC-USR-017` là **P1**.

---

### REQ-USR-010 · Sửa trong từng đơn KHÔNG ghi ngược lại hồ sơ (`BR15-04`)
📍 `DOC-v1.1-01 §8.15.1 BR15-04 · trang 49` · `§6.2 AC-30.1.01 · trang 28`  ·  Clarif: —

> Nguồn #1 — `BR15-04` (§8.15.1, trang 49):
> "Giá trị mặc định được prefill vào ô số điện thoại người gửi và địa chỉ lấy hàng ở lần đăng tin sau; người dùng vẫn sửa trong từng đơn mà không ghi lại hồ sơ."

> Nguồn #2 — `AC-30.1.01` Then (§6.2, trang 28):
> "…Lần đăng tin sau, hai giá trị này được prefill vào ô số điện thoại người gửi và địa chỉ lấy hàng; người dùng vẫn sửa được trong từng đơn mà không ghi lại hồ sơ."

↳ **Ghi chú:** **REQ MỚI — chiều ngược của `REQ-USR-009`, và là chiều dễ bị bỏ sót hơn.** `REQ-USR-009` bảo vệ đơn cũ khỏi bị hồ sơ ghi đè; `REQ-USR-010` bảo vệ hồ sơ khỏi bị từng đơn ghi đè. Hai chiều độc lập, fail độc lập ⇒ 2 SC riêng (`SC-USR-017`, `SC-USR-018`).
⚠️ **Ranh giới module — đây là chỗ dễ nhân bản TC nhất của cả lượt phân tích:** vế *"được prefill vào ô SĐT người gửi và địa chỉ lấy hàng"* có home ở **`ORD`** (`REQ-ORD-007`, `SC-ORD-025` — kiểm **wizard có nhận đúng giá trị prefill không**). Vế ở đây là *"sửa trong đơn **không ghi lại hồ sơ**"* — kiểm **hồ sơ có bị ghi đè không**. ⛔ Hai SC nhìn hai đầu của cùng một sợi dây, đừng gộp và cũng đừng nhân bản.
📌 **Chính `AC-30.1.01` này là nguồn đã dùng để resolve `C-ORD-10` ở lượt delta trước** — trong khi lượt đó lại khai `FR15` ngoài phạm vi. Mâu thuẫn đó là lý do module này phải rà lại; xem `CHANGELOG.md §1`.

---

### REQ-USR-002 · "Xem/cập nhật hồ sơ" — nay CÓ bề mặt sửa, nhưng chỉ 2 trường *(MODIFIED)*
📍 `DOC-v1.1-01 §8.15 · trang 48` · `§8.15.1 BR15-01 · trang 48` · `§8.15.2 · trang 49`  ·  Clarif: `C-USR-03`, `C-USR-05`

> Nguồn (v1.0) — `DOC-v1.0-01 §A6 USR-02 · L100`:
> "USR-02 | Xem/cập nhật hồ sơ: tên, SĐT, avatar, phòng ban, khu vực/văn phòng, kênh liên hệ"
>
> ⇒ `C-USR-03` Resolved 2026-07-24 theo **quan sát app STG**: *"KHÔNG (view-only)"*; `SC-USR-003` là SC negative bảo vệ kết luận đó.

> Nguồn (v1.1) #1 — Description (§8.15, trang 48):
> "Cho phép sửa số điện thoại và địa chỉ mặc định dùng để prefill khi đăng tin; các trường đồng bộ từ SSO là chỉ đọc."

> Nguồn (v1.1) #2 — `BR15-01` (§8.15.1, trang 48):
> "Tên, phòng ban · MNV và email công ty là chỉ đọc — đồng bộ từ SSO; email hiển thị kèm icon khoá, không có ô nhập."

↳ **Ghi chú (diff):** 🔴 **Kết luận v1.0 bị ĐẢO — nhưng đảo một phần, và phần đảo nằm đúng chỗ nguy hiểm.**
v1.0 chốt **view-only hoàn toàn** dựa trên quan sát app 2026-07-24 (⛔ không phải tài liệu). PRD v1.1 nói **CÓ** màn sửa. ⇒ `SC-USR-003` — SC negative *"KHÔNG có bất kỳ control sửa nào; mọi trường chỉ đọc"* — **không còn đúng** và phải lật.
⚠️ **Cẩn thận: không lật thành "hồ sơ sửa được".** Bức tranh đúng của v1.1 là **hồ sơ có 2 vùng**: vùng **SSO chỉ đọc** (tên · phòng ban · MNV · email — `BR15-01` giữ nguyên tinh thần view-only của v1.0) và vùng **người dùng sửa được** (SĐT mặc định · địa chỉ mặc định). ⇒ `SC-USR-003` MODIFIED thành *"vùng SSO vẫn chỉ đọc"* (phần v1.0 đúng, giữ lại) và `SC-USR-016` NEW gánh phần assert `BR15-01` chi tiết (icon khoá, không có ô nhập).
🔴 **Bẫy giống hệt `SC-CNL-006`:** bản v1.0 và v1.1 của `SC-USR-003` có Then **ngược nhau ở phần "có control sửa hay không"**, và **cả hai bản đều chạy được** nên không có gì báo lỗi nếu lấy nhầm bản. Xem ràng buộc ở `CHANGELOG.md §2`.

---

### REQ-USR-006 · Menu trang cá nhân — mục thứ hai nay có tên *(MODIFIED)*
📍 `DOC-v1.1-01 §8.15 dòng Trigger · trang 48`  ·  Clarif: `C-USR-04`

> Nguồn (v1.0) — `DOC-v1.0-02 §3.9` + `KP-01 §2 KB-USR-04` ⇒ `C-USR-04` Open: *"Nhãn mục menu thứ hai + 3 trường hồ sơ chưa có bằng chứng UI"*; `SC-USR-012` là SC dạng `[GAP]`.

> Nguồn (v1.1) — Trigger (§8.15, trang 48):
> "Mở "Cập nhật thông tin" trong trang cá nhân (nằm dưới mục "Quà đã nhận")"

↳ **Ghi chú (diff):** Một dòng `Trigger` trả lời được **một nửa** `C-USR-04`. Trang cá nhân có ít nhất **2 mục menu theo thứ tự xác định**: `"Quà đã nhận"` rồi `"Cập nhật thông tin"` ⇒ `SC-USR-012` hết dạng `[GAP]`, assert được **tên** và **vị trí tương đối** (nâng P3 → P2). ⚠️ **Nửa còn lại vẫn Open**: *"3 trường hồ sơ chưa có bằng chứng UI"* — `§8.15.2` liệt kê trường của **màn Cập nhật thông tin**, ⛔ **không phải** danh sách trường hiển thị trên **trang cá nhân**; hai màn khác nhau. ⇒ `C-USR-04` chuyển **🟡 Partially Resolved**, ⛔ đừng đóng hẳn.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
