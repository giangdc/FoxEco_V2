---
id: v1.1/USR-tai-khoan/risk
title: Risk Assessment — v1.1 · Module USR
type: risk-assessment
version: v1.1
sprint: 1
module: USR
counts:
  cl: 7
  risk: 8
  cl_open: 1
  cl_resolved: 6
status: ANALYZED
updated: 2026-09-18
---

> Tạo bởi: analyze-requirements (DELTA 2026-09-15, **lượt bù thứ hai**) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (5 dòng, `RISK-USR-01..05`) xem `v1.0/USR-tai-khoan/risk_assessment.md` — KHÔNG lặp lại ở đây. **ID mới bắt đầu từ `RISK-USR-06`.**
> ℹ️ `cl_open (1) + cl_resolved (6) = cl (7)` — **`C-USR-07` mở lại 2026-09-18** sau khi vibe-test VR-003 có dữ kiện thực nghiệm; 6 CL còn lại đã Resolved (2026-09-16).

## Tổng quan
| Module | Risk Level | Rủi ro chính (delta v1.1) |
|--------|-----------|--------------|
| USR | **Medium** (tăng từ Low) | Từ module *"view-only, ít rủi ro nhất"* thành module có **một màn ghi dữ liệu** và **2 rule truy vết hai chiều**. Ba rủi ro đáng kể: (1) `SC-USR-003` **đảo chiều** — cùng bẫy `SC-CNL-006`; (2) app STG quan sát 2026-07-24 là view-only hoàn toàn ⇒ **8 SC mới có thể BLOCKED**; (3) `BR15-03` là thành viên thứ tư của nhóm rule truy vết mà app **đã vi phạm 1 lần đã live-verify** |

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-USR-06 | USR / Kết luận bị đảo + app chưa build | *(cập nhật Status)* `C-USR-03` (*"hồ sơ view-only hoàn toàn"*, Resolved 2026-07-24 **theo quan sát app**) bị `FR15` đảo. Hai hệ quả: (a) `SC-USR-003` có Then **ngược nhau giữa 2 bản** và **cả hai bản đều chạy được** ⇒ lấy nhầm bản cho kết luận ngược mà không có gì báo lỗi; (b) app STG có thể **chưa build `FR15`** ⇒ 8 SC mới `BLOCKED` chứ không phải FAIL | High → **Partially confirmed** | `DOC-v1.1-01` §8.15 (trang 48-49) vs `KP-01` §2 KB-USR-01 (live-verify 2026-07-24) | `SC-USR-003` (lật chiều) · `SC-USR-013..020` (8 SC mới) | Vibe-check qua demo 2026-09-16 xác nhận màn "Cập nhật thông tin" **tồn tại và đúng field spec** `BR15-01`. **CHƯA verify được thao tác "Lưu thay đổi" có thực sự persist trên STG thật** — demo không có backend. ⛔ Vẫn cần 1 lượt xác nhận trên STG trước `generate-tc`; nếu STG cũng đã build thì hạ hẳn xuống Resolved | Partially confirmed (cấu trúc + field spec khớp qua demo; persist trên STG thật chưa verify) | REQ-USR-002, REQ-USR-008, SC-USR-003, SC-USR-013..020 |
| RISK-USR-07 | USR / Rule truy vết hai chiều | **(risk mới)** `BR15-03`/`BR15-04` là **thành viên thứ tư** của nhóm rule *"bằng chứng đã ghi thì bất biến"* (cùng `BR11-03` · `BR18-05` · `NFR-07`) — và app **đã vi phạm nhóm này 1 lần đã live-verify** (`KB-CNL-01`: huỷ nhận đơn **xoá** dòng "Ghép thành công"). Nếu backend lưu đơn bằng **tham chiếu tới hồ sơ** thay vì **chụp giá trị tại thời điểm đăng**, đổi SĐT hồ sơ sẽ **viết lại cả lịch sử đơn** — lỗi **hoàn toàn âm thầm**, không crash, không cảnh báo | **High** | `DOC-v1.1-01` §8.15.1 BR15-03/BR15-04 (trang 49) · §6.2 AC-30.2.02 (trang 28) — dùng đúng cụm *"phục vụ truy vết"* như `BR18-05` | `SC-USR-017` (**P1**, chiều hồ sơ→đơn) · `SC-USR-018` (chiều đơn→hồ sơ) | Chạy `SC-USR-017` **cùng lô** với `SC-CNL-010` · `SC-ORD-065` · `SC-DLV-062`; nếu cùng vỡ thì **1 bug report cho nguyên nhân gốc**, ⛔ không log 4 bug rời | Open | REQ-USR-009, REQ-USR-010, SC-USR-017, SC-USR-018 |
| RISK-USR-08 | USR / Phạm vi sửa hồ sơ thu hẹp | **(risk mới 2026-09-15)** BRD `USR-02` liệt kê 6 trường sửa được, `FR15` chỉ cho sửa 2; avatar · khu vực/văn phòng · kênh liên hệ PRD không nhắc. **BA 2026-09-16:** kênh liên hệ **bỏ hẳn**; avatar *"load từ HRIS, không cho sửa ??"*; khu vực/văn phòng *"load theo địa chỉ mặc định"* + **rule mới**: địa chỉ lấy hàng/giao hàng/điểm xuất phát load theo địa chỉ mặc định — hai câu sau BA còn để dấu hỏi. ⛔ **Cập nhật 2026-09-16 — BA chốt:** avatar = chữ viết tắt không dấu (chỉ đọc); khu vực/văn phòng = **địa chỉ mặc định** (load HRIS, sửa bằng chọn từ danh sách văn phòng); prefill **CÓ** sang lấy hàng (người gửi) · giao hàng (người nhận) · điểm xuất phát (người vận chuyển) | Medium | `DOC-v1.1-01` §8.15.1 BR15-01 · §8.15.2 vs `DOC-v1.0-01` §A6 USR-02 · BA trả lời 2026-09-16 | `SC-USR-002` · `SC-USR-010` (kênh liên hệ: assert **không tồn tại**) · prefill địa chỉ ở `ORD` (`SC-ORD-025`) | `C-USR-05` gần đóng (còn avatar tên 1 từ); **cập nhật SC prefill ở `ORD` (`SC-ORD-025`/`058`) + điểm xuất phát ở `ASN`** theo rule đã chốt | **Resolved 2026-09-16** | REQ-USR-002, REQ-USR-008, SC-USR-002, SC-USR-010 |
| RISK-USR-03 | USR / Bằng chứng UI trang Cá nhân | *(cập nhật Status)* v1.0: nhãn mục menu thứ hai + 3 trường hồ sơ **chưa có bằng chứng UI** ⇒ `SC-USR-012` treo dạng `[GAP]` | Medium → **Resolved** | `DOC-v1.1-01` §8.15 dòng Trigger (trang 48) · vibe-check demo 2026-09-16 | `SC-USR-012` (hết gap, P3→P2) · `SC-USR-002` (hết gap, có đủ bằng chứng) | Đã có ảnh chụp demo cho cả 2 màn (`00_input/v1.1/design/USR_01..02`) — xem mục Vibe-check bổ sung dưới đây | **Resolved** | REQ-USR-006, SC-USR-002, SC-USR-012 |
| RISK-USR-01 | USR / Chỉ số đóng góp | *(cập nhật Why)* 2 chỉ số đóng góp nay có **rule loại trừ** (`BR14-04` — không tính đơn `RETURNED`) và cùng con số hiển thị ở **3 màn** (`USR` · `HOME` · `GIFT`) | Medium | `DOC-v1.1-01` §8.14.1 BR14-04 · §6.2 AC-26.1.01 | `SC-USR-005` — cross-check với `SC-GIFT-014` + `SC-HOME-008` | Home của rule ở `GIFT` (`REQ-GIFT-009`) — ⛔ không nhân bản SC; chạy 3 màn **trong 1 lượt** với cùng 1 đơn `RETURNED` | Open | REQ-USR-004, SC-USR-005 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-USR-03 | `USR-02` ghi *"Xem/**cập nhật** hồ sơ"* — app có chức năng sửa hồ sơ không? | ✅ **Resolved 2026-09-15 — ĐẢO kết luận v1.0: CÓ, qua màn "Cập nhật thông tin", nhưng chỉ 2 trường** | 2026-07-24 | REQ-USR-002, REQ-USR-008 |
| C-USR-05 | Avatar · khu vực/văn phòng · kênh liên hệ — sửa được, chỉ đọc, hay đã bỏ? | ✅ **Resolved 2026-09-16** — (a) avatar chữ viết tắt không dấu 2 từ cuối, giống nhau 2 màn; (b) khu vực/văn phòng = địa chỉ mặc định (HRIS, chọn từ danh sách văn phòng), prefill CÓ sang lấy hàng/giao hàng/điểm xuất phát; (c) kênh liên hệ bỏ hẳn — BA chốt qua 5 lượt | 2026-09-15 | REQ-USR-002, REQ-USR-008, SC-USR-002, SC-USR-010, SC-USR-020..024 |
| C-USR-06 | Badge **"Hạng Đồng hành"** trên trang Cá nhân — PRD cấm mọi tier/xếp hạng (`BR14-03`, `AC-26.1.01`) nhưng `SC-USR-007` v1.0 assert badge **tồn tại** | ✅ **Resolved 2026-09-16 — KHÔNG hiển thị badge** (BA) | 2026-09-16 | REQ-USR-007, SC-USR-007, SC-USR-011 |
| C-USR-04 | Nhãn mục menu thứ hai + 3 trường hồ sơ chưa có bằng chứng UI | ✅ **Resolved 2026-09-16 — qua demo, xem mục Vibe-check bổ sung** | mở 2026-09-07 | REQ-USR-002, REQ-USR-006 |
| C-USR-07 | **Địa chỉ mặc định để RỖNG có hợp lệ không**, và có đường nào để **xoá** địa chỉ đã lưu? (chính là câu **(v)** của `C-USR-05` — *"còn cho bỏ trống không (PRD ghi Không bắt buộc)?"* — BA **chưa bao giờ trả lời thẳng**, nhưng `C-USR-05` đã bị đóng `Resolved` ⇒ câu hỏi rơi mất) | 🟡 **Open — mở lại 2026-09-18**, nay đã có **dữ kiện thực nghiệm** từ `VR-003` | 2026-09-18 | REQ-USR-008, SC-USR-019, SC-USR-020 |
| C-USR-01 · C-USR-02 | *(giữ nguyên Resolved từ v1.0 — PRD không nhắc, không đảo)* | ✅ Resolved | 2026-07-27 | xem `v1.0/USR-tai-khoan/risk_assessment.md` |

### C-USR-03 · "Xem/cập nhật hồ sơ" — ĐẢO kết luận *(RESOLVED 2026-09-15)*

📍 `DOC-v1.1-01 §8.15 Description + Trigger · trang 48` · `§8.15.2 UI/Field Spec · trang 49` · `§6.1 US30 · trang 13`

> Description: "Cho phép sửa số điện thoại và địa chỉ mặc định dùng để prefill khi đăng tin; các trường đồng bộ từ SSO là chỉ đọc."

> Trigger: "Mở "Cập nhật thông tin" trong trang cá nhân (nằm dưới mục "Quà đã nhận")"

> `US30`: "Là Người dùng, tôi muốn sửa số điện thoại và địa chỉ mặc định trong hồ sơ, để không phải nhập lại mỗi lần đăng tin."

↳ **Ghi chú:** 🔴 **Lần đảo kết luận thứ hai của dự án — và cùng khuôn với `C-CNL-01`.** Điểm chung của cả hai: kết luận v1.0 được Resolved **theo quan sát app**, ⛔ không theo tài liệu (`C-USR-03`: *"QA kiểm trực tiếp app STG 2026-07-24 xác nhận view-only hoàn toàn"*). PRD chính thức lật cả hai. ⇒ **Bài học:** phán quyết dựa trên quan sát app là loại **dễ bị đảo nhất** khi có tài liệu mới — khi ghi CL kiểu này nên đánh dấu rõ để lượt delta sau biết ưu tiên rà lại.
**Phán quyết hiện hành — đọc cho đúng, ⛔ đừng đọc thành "hồ sơ sửa được":** hồ sơ có **2 vùng**. Vùng **SSO chỉ đọc**: tên · phòng ban · MNV · email (`BR15-01`, email kèm **icon khoá**) — phần này v1.0 **đúng**, giữ nguyên. Vùng **sửa được**: đúng **2 trường** — `Số điện thoại mặc định` (bắt buộc) và `Địa chỉ mặc định` (không bắt buộc), qua **một màn riêng** tên `"Cập nhật thông tin"`.
**Bản v1.0 KHÔNG bị sửa** (giữ nguyên làm hồ sơ lịch sử, đúng `Project_rule`); bản hiện hành là dòng này.

### C-USR-05 · Avatar · khu vực/văn phòng · kênh liên hệ — số phận là gì? *(OPEN)*

📍 `DOC-v1.1-01 §8.15.1 BR15-01 · trang 48` · `§8.15.2 UI/Field Spec · trang 49` ⟷ `DOC-v1.0-01 §A6 USR-02 · L100`

> Nguồn A (v1.0 — BRD `USR-02`): "Xem/cập nhật hồ sơ: tên, SĐT, **avatar**, phòng ban, **khu vực/văn phòng**, **kênh liên hệ**"

> Nguồn B (v1.1 — `BR15-01`): "Tên, phòng ban · MNV và email công ty là chỉ đọc — đồng bộ từ SSO; email hiển thị kèm icon khoá, không có ô nhập."

> Nguồn B (v1.1 — `§8.15.2`, toàn bộ 4 dòng field spec): "Tên · Phòng ban · MNV" · "Email công ty" · "Số điện thoại mặc định" · "Địa chỉ mặc định"

↳ **Ghi chú:** BRD liệt kê **6 trường** trong phạm vi *"xem/cập nhật hồ sơ"*. `FR15` xử lý **5** trong số đó (2 cho sửa, 3 khoá SSO) + thêm `Email`. **Ba trường còn lại — `avatar` · `khu vực/văn phòng` · `kênh liên hệ` — không xuất hiện ở bất kỳ đâu trong `§8.15`** (đã rà toàn văn mục này).
⛔ **KHÔNG suy diễn *"không nhắc = đã bỏ khỏi sản phẩm"***: `KP-01 §2 KB-USR-01` ghi nhận app **có** hiển thị avatar trên trang Cá nhân, và `SC-USR-002` (v1.0) đang assert điều đó. Nếu kết luận sai chiều thì hoặc mất 1 SC đang đúng, hoặc viết TC cho thứ không tồn tại.
**Câu hỏi cho BA/PM:** (a) `avatar` — hiển thị chỉ đọc (lấy từ SSO) hay người dùng đổi được? (b) `khu vực/văn phòng` — có phải chính là `Địa chỉ mặc định` đổi tên, hay là trường riêng? (c) `kênh liên hệ` (`USR-07`) — `C-USR-02` đã chốt *out of scope v1.0*; v1.1 có mở lại không, hay bỏ hẳn?
**Vì sao non-blocking:** 8 SC mới của `FR15` không đụng 3 trường này; `SC-USR-002` (trang Cá nhân) **không còn** bị treo vì lý do thiếu bằng chứng UI (`C-USR-04` đã Resolved 2026-09-16) — phần còn treo bây giờ chỉ là 3 câu hỏi (a)(b)(c) ở trên.

↳ **Cập nhật 2026-09-16 — bằng chứng phụ từ demo (không resolve, chỉ thu hẹp câu hỏi):** Trên cả 2 màn (trang Cá nhân lẫn "Cập nhật thông tin"), avatar chỉ là **icon/chữ viết tắt tĩnh, không có nút hay vùng chạm nào để đổi ảnh** (kiểm bằng accessibility tree — không phải `button`/`textbox`, chỉ là `generic`/text). **"Khu vực/văn phòng" và "kênh liên hệ" không xuất hiện dưới bất kỳ tên gọi nào** ở cả 2 màn — chỉ có "Phòng Kỹ thuật" (phòng ban) và "Địa chỉ mặc định". ⚠️ Đây **không phải bằng chứng đủ để Resolve** — đúng caveat đã nêu ở các module khác (`RISK-DLV-08`/`RISK-DLV-11`): demo có thể đơn giản là **chưa cài đặt** avatar-upload chứ không phải sản phẩm chính thức không có; và có thể trường "khu vực/văn phòng" tồn tại nhưng chỉ hiện ở màn khác chưa xem tới. Giữ **Open**, nhưng câu hỏi cho BA giờ có thể đi thẳng vào (b)/(c) vì (a) gần như chắc chắn không có control đổi ảnh trên bề mặt hiện tại.

### C-USR-04 · Nhãn menu + trường hồ sơ *(RESOLVED 2026-09-16 — qua demo)*

📍 `DOC-v1.1-01 §8.15 dòng Trigger · trang 48` · vibe-check demo 2026-09-16

> ↪ *Quote `Mở "Cập nhật thông tin" trong trang c…` — home ở `requirement_traceability.md` · `REQ-USR-006` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

↳ **Ghi chú (2026-09-15):** **Nửa đã xong:** nhãn mục menu thứ hai là **"Cập nhật thông tin"**, và biết luôn **thứ tự tương đối** (dưới "Quà đã nhận") ⇒ `SC-USR-012` hết `[GAP]`, nâng P3 → P2.

↳ **Cập nhật 2026-09-16 — nửa còn lại đã đóng:** Vibe-check trực tiếp qua demo `https://giangdc.github.io/foxeco_demo/FoxEcoQC` (vai Sender), dùng Playwright, xác nhận **trang Cá nhân** và **màn "Cập nhật thông tin"** là **hai màn khác nhau, hai bộ trường khác nhau** — đúng như cảnh báo ở lượt trước:
> Ảnh `00_input/v1.1/design/USR_01_trangcanhan_fields_CUSR04.png` — **Trang Cá nhân** hiển thị: avatar (icon placeholder, không phải ảnh thật) · Tên · "Phòng Kỹ thuật · MNV: FTEL2291" · badge **"Hạng Đồng hành"** · 2 chỉ số "12 đơn đã giúp" / "8 quà đã nhận" · 3 mục menu **"Đơn của tôi" → "Quà đã nhận" → "Cập nhật thông tin"** (đúng thứ tự PRD).
> Ảnh `00_input/v1.1/design/USR_02_capnhatthongtin_fields.png` — **Màn "Cập nhật thông tin"** hiển thị: avatar chữ viết tắt "CL" + Tên + "Phòng Kỹ thuật · MNV: FTEL2291" (đọc), **Số điện thoại mặc định** (textbox, sửa được), **Email công ty** (kèm icon **khiên** — ⛔ đính chính 2026-09-16, trước ghi nhầm "khoá"; không phải textbox — chỉ đọc), **Địa chỉ mặc định** (textbox, sửa được), nút "Lưu thay đổi". Khớp verbatim `BR15-01`/`§8.15.2`.

⛔ **Cập nhật 2026-09-16 — mô tả avatar *"icon placeholder"* ở ảnh trang Cá nhân phía trên HẾT HIỆU LỰC làm oracle.** Hiện hành: avatar 2 màn là một, hiện chữ viết tắt — xem `C-USR-05 · ↳ Câu (a) avatar`.
⛔ **Cập nhật 2026-09-16 — icon cạnh Email công ty là KHIÊN, không phải khoá** (BA xác nhận; code demo dùng `EcoIcons.Shield`). PRD `BR15-01`/`AC-30.2.01`/`§8.15.2` ghi *"icon khoá"* ⇒ **lệch chữ PRD ↔ UI**; BA chốt oracle theo UI (khiên). Nên báo BA sửa câu chữ PRD.

**Analyst Note:** `SC-USR-002` (trang Cá nhân) giờ có đủ bằng chứng để assert cứng danh sách: Tên, Phòng ban+MNV, 2 chỉ số, 3 mục menu đúng thứ tự — ⛔ **KHÔNG** gồm SĐT/Email/Địa chỉ (những trường đó chỉ ở màn "Cập nhật thông tin"). `RISK-USR-03` đóng theo. Đồng thời, đây cũng là bằng chứng đầu tiên cho thấy màn "Cập nhật thông tin" **tồn tại thật trên 1 môi trường có UI** (không chỉ trên giấy) — hạ `RISK-USR-06` xuống "Partially confirmed" (còn thiếu: xác nhận nút "Lưu thay đổi" persist thật trên STG, vì demo không có backend).

⚠️ **Phát hiện phụ, chưa có ở bất kỳ tài liệu nào — ghi nhận, không assert:** badge **"Hạng Đồng hành"** trên trang Cá nhân là một hệ thống hạng/rank hoàn toàn không xuất hiện trong BRD lẫn PRD v1.1 (`§8.15` không nhắc). Có thể là tính năng chưa đặc tả hoặc dữ liệu giả lập của demo — **không viết TC khẳng định cho badge này**, chỉ ghi nhận nếu SC-USR-002 chạy trên STG thấy nó tồn tại thật.

### C-USR-05 · ↳ BA trả lời 2026-09-16 *(→ PARTIALLY RESOLVED — hỏi vòng 2)*

📍 BA trả lời · `02_analyze-requirements/v1.1/CL-hoi-BA-v1.1.xlsx` sheet `USR` · cột "Câu trả lời BA" · 2026-09-16

> "a. load từ hiris và không cho phép chỉnh sửa ??
> b. Khu vực/văn phòng sẽ load giá trị tại Địa chỉ mặc định, các trường địa chỉ lấy hàng/giao hàng, điểm xuất phát → sẽ load theo địa chỉ mặc định của account ?
> b. Bỏ hẳn nhé"

↳ **Ghi chú:** Dòng thứ ba BA đánh nhãn **"b"** nhưng theo thứ tự là câu **(c)** ⇒ hiểu: **"Kênh liên hệ" bỏ hẳn** — chốt được, `SC-USR-010` assert *không tồn tại* bề mặt cấu hình kênh liên hệ (không còn là GAP chờ). ⚠️ Cần BA xác nhận lại nhãn.
(a) và (b) BA **tự kết thúc bằng dấu hỏi** ⇒ ⛔ chưa đủ làm oracle: (a) avatar **lấy từ HRIS, chỉ đọc** — khớp demo 2026-09-16 (không có control đổi ảnh) nhưng demo chỉ hiện chữ viết tắt, **không hiện ảnh HRIS** ⇒ hỏi: nếu HRIS có ảnh thì app hiện **ảnh** hay **chữ viết tắt**? (b) sinh **rule mới ngoài PRD**: *"địa chỉ lấy hàng / giao hàng / điểm xuất phát load theo địa chỉ mặc định"*. PRD hiện chỉ có: địa chỉ **lấy hàng** prefill địa chỉ mặc định (`§8.1.4`) · địa chỉ **giao hàng** tự điền **từ danh bạ người nhận** (`AC-04.1.01`) · **điểm xuất phát** OFFER prefill **"vị trí làm việc"** (`§8.2.2`).
**Hỏi vòng 2:** (1) Xác nhận (a)(b) — bỏ dấu "?". (2) **Địa chỉ giao hàng**: lấy địa chỉ mặc định **của người gửi** (vô lý — trùng địa chỉ lấy hàng, vi phạm *"phải khác địa chỉ lấy hàng"*), hay địa chỉ mặc định **của người nhận** tra theo email? (3) **Điểm xuất phát** OFFER: địa chỉ mặc định (BA) hay vị trí làm việc (PRD) — nếu hồ sơ chưa đặt địa chỉ mặc định thì lấy gì? (4) "Khu vực/văn phòng" có được dùng để **lọc "Tin mới"/Bảng tin theo khu vực** không (`C-HOME-04`)? (5) Label dòng thứ ba là câu (c)?
⛔ **Cập nhật 2026-09-16 — danh sách "Hỏi vòng 2" trên đã được BA trả lời** (1)(2)(3) ở các khối `↳` bên dưới; (5) coi là câu (c) — kênh liên hệ bỏ hẳn. **Chỉ còn (4)** — khu vực/văn phòng có dùng lọc Bảng tin không — home ở `C-HOME-04`.

### C-USR-05 · ↳ Câu (a) avatar — BA chốt 2026-09-16

📍 BA trả lời · 2026-09-16

> "avatar màn hình cập nhật và màn hình cá nhân là 1, hiển thị tên viết tắt (Ví dụ: Trần Văn A thì hiển thị là VA)"

↳ **Ghi chú:** Câu (a) **đóng**. Rule: avatar = **chữ cái đầu của 2 từ cuối trong Tên**, viết hoa ("Trần Văn A" → `VA`, "Đồng Công Chí Linh" → `CL`); **cùng một avatar** ở trang Cá nhân và màn "Cập nhật thông tin"; chỉ đọc (khớp câu BA *"không cho phép chỉnh sửa"*). ⇒ `SC-USR-002` assert chữ viết tắt trên trang Cá nhân; `SC-USR-016` assert avatar chỉ đọc trên màn "Cập nhật thông tin".
⚠️ **Demo lệch rule:** `USR_01` (trang Cá nhân) hiện **icon người**, còn `USR_02` hiện đúng `CL`. Nếu STG cũng hiện icon ở trang Cá nhân ⇒ **defect**.
Biên chưa có đặc tả: tên **1 từ** · chữ cái đầu **có dấu** ("Đ", "Á") giữ nguyên hay bỏ dấu ⇒ TC chỉ ghi nhận, ⛔ không assert. Có thể gộp vào lượt hỏi BA vòng 2.
⛔ **Cập nhật 2026-09-16 (lượt 3):** chữ cái có dấu ⇒ hiển thị **không dấu** ("Đặng Ánh" → `DA`). Chỉ còn mở: **tên 1 từ**.
⛔ **Cập nhật 2026-09-16 (lượt 5):** tên luôn ≥ 2 từ ("Trần A" → `TA`) ⇒ **không còn biên tên 1 từ**.

### C-USR-05 · ↳ Rule địa chỉ mặc định — BA chốt 2026-09-16

📍 BA trả lời · 2026-09-16

> "mặc định load từ hris và cho phép chỉnh sửa
> nhập hiển thị danh sách văn phòng theo địa chỉ đã nhập -> chọn data load từ danh sách, chứ ko phải muốn nhập gì nhập nhé"

↳ **Ghi chú:** Rule hiện hành của `Địa chỉ mặc định`: (1) giá trị ban đầu **load từ HRIS**; (2) **cho sửa**; (3) khi gõ ⇒ hiện **danh sách văn phòng lọc theo nội dung đã gõ** ⇒ người dùng **chọn 1 mục**; ⛔ **không nhận text tự do**. ⇒ `SC-USR-020` viết lại (từ chối text gõ tay), thêm `SC-USR-021` (gợi ý + chọn) · `SC-USR-022` (khởi tạo từ HRIS).
⛔ **Hết hiệu lực:** cách đọc `§8.15.2` *"Văn bản · ≤ 200 ký tự"* thành ô nhập tự do với biên 200/201. PRD **không** mô tả danh sách chọn ⇒ nên báo BA bổ sung vào PRD.
⚠️ **Demo lệch rule:** ô địa chỉ demo là `textarea` tự do, không gợi ý, không validate.
🔗 Rule này **khớp một phần** câu BA (b) *"khu vực/văn phòng sẽ load giá trị tại Địa chỉ mặc định"* — địa chỉ mặc định nay chính là **một văn phòng** ⇒ (b) thu hẹp còn phạm vi prefill sang **giao hàng / điểm xuất phát**.
**Câu hỏi mở lúc đầu (đã trả lời phần lớn ở lượt dưới):** (i) danh sách văn phòng lấy từ nguồn nào (HRIS / master data FoxEco)? (ii) gõ bao nhiêu ký tự thì bắt đầu gợi ý; tìm có dấu/không dấu, theo tên hay theo địa chỉ? (iii) không có kết quả thì hiện gì? (iv) gõ tay không chọn rồi bấm Lưu: báo lỗi (text gì) / tự xoá / disable nút Lưu? (v) còn cho **bỏ trống** không (PRD ghi *Không bắt buộc*)? (vi) HRIS không có địa chỉ làm việc thì ô hiện gì?

🔴 **CHỐT 2026-09-18 (QC GiangDC2) — câu (vi) ĐÓNG, và nó biến một "nhánh dữ liệu" thành một BUG:**

> *"địa chỉ data hris luôn luôn có nhé, nếu mặc định, hiện tại ko có do bị bug không load data từ hris ấy"*

↳ **Ghi chú:** HRIS **luôn** có địa chỉ làm việc mặc định cho mọi CBNV ⇒ nhánh *"HRIS không có địa chỉ"* **không tồn tại trong thực tế** (khớp với việc `TC-USR-041` đã DESCOPED và gap #1 của `USR-accounts.md §4` đã đóng). ⇒ Việc `VR-003` quan sát ô địa chỉ **rỗng** ở lần mở màn đầu tiên **KHÔNG phải** nhánh dữ liệu thiếu, mà là **lỗi app không nạp dữ liệu từ HRIS** — đã log `BUG-008` (ứng viên `B9`, `TC-USR-040` + `TC-USR-043`).
⇒ **Hệ quả cho `TC-USR-044`:** giữ nguyên `⛔ N-A / DESCOPED`. Lập luận *"ô SĐT rỗng khi mở lần đầu CÓ xảy ra thật nên `TC-USR-044` nên sống lại"* (nêu ở `VR-001`/`VR-003`) **BỊ BÁC** — ô rỗng đó là **triệu chứng của `BUG-008`**, không phải trạng thái *"HRIS trống SĐT"* mà TC mô tả. Đúng như nhận định: **TC mô tả sai nguyên nhân**, và nguyên nhân thật đã có bug riêng.
⚠️ **Rule `SC-USR-022`/`SC-USR-023` (*"prefill từ HRIS"*) được QC xác nhận là ĐÚNG** ⇒ ⛔ **không** sửa 2 SC này theo hành vi app; app phải sửa cho khớp spec.

### C-USR-05 · ↳ Rule địa chỉ mặc định — BA trả lời chi tiết 2026-09-16

📍 BA trả lời · 2026-09-16

> "danh sách văn phòng lấy từ file data, để t gởi sau
> 3 ký tự thì gợi ý
> ra khỏi textbox sẽ là rỗng, lưu rỗng
> cho phép để trông
> hris ko có địa chỉ thì để trống thôi(ý là default thôi nha) chứ đã cập nhật trước đó vào lại sẽ thấy data cũ"

↳ **Ghi chú:** (i) nguồn danh sách = **file data** ⇒ ✅ đã nhận 2026-09-16: `DOC-v1.1-04` `location_address_catalog.xlsx` (399 văn phòng). (ii) **gõ ≥ 3 ký tự** mới gợi ý — phần *có dấu/không dấu, theo tên hay địa chỉ* **vẫn mở**. (iii) *không có kết quả hiện gì* — **vẫn mở**. (iv) gõ tay không chọn ⇒ **rời ô thì ô rỗng, bấm Lưu thì lưu rỗng**. (v) **cho phép để trống**. (vi) HRIS không có địa chỉ ⇒ **mặc định rỗng**; **thứ tự ưu tiên khi mở màn: giá trị đã lưu > địa chỉ HRIS > rỗng**.
⛔ **Hết hiệu lực:** Then *"gõ tay không chọn ⇒ mở lại vẫn là địa chỉ cũ"* của `SC-USR-020` (viết cùng ngày trước lượt này).
⛔ **Cập nhật lượt 3:** phần *"vẫn mở"* của (ii) và (iii) ở trên **đã trả lời** — tìm theo tên, không phân biệt dấu/hoa thường; không khớp ⇒ không gợi ý.

### C-USR-05 · ↳ BA trả lời các câu còn mở — 2026-09-16 (lượt 3)

📍 BA trả lời · 2026-09-16

> "1. không dấu có dấu đều được, không phân biệt hoa thường , tìm theo tên văn phòng ,
> 2. không có thì ko gợi ý thôi
> 3.hiển thị không dâu nhé ,
> 4. có nhé"

↳ **Ghi chú:** (1) Gợi ý văn phòng tìm theo **tên**, **không phân biệt dấu** và **hoa thường**. (2) Không khớp ⇒ **không hiện gợi ý**, không có thông báo. (3) Avatar chữ viết tắt **không dấu** ("Đặng Ánh" → `DA`); còn mở: tên 1 từ. (4) **Câu (b) CHỐT: CÓ** — địa chỉ mặc định được điền sẵn sang **địa chỉ lấy hàng · địa chỉ giao hàng · điểm xuất phát**.
✅ **(4) chủ thể prefill — BA xác nhận đúng 2026-09-16:** giao hàng = địa chỉ mặc định **của người nhận** (tra theo email qua danh bạ — khớp `AC-04.1.01` *"Tự điền tên người nhận, số điện thoại và địa chỉ giao hàng"*); điểm xuất phát OFFER = địa chỉ mặc định **của người vận chuyển đăng tin** (thay cho *"vị trí làm việc"* của `§8.2.2`). ⛔ Không hiểu là địa chỉ mặc định **của người gửi** cho ô giao hàng — sẽ trùng địa chỉ lấy hàng.
🔗 **Home ở module khác, ⛔ chưa sửa:** `SC-ORD-025` (lấy hàng) · `SC-ORD-058` (giao hàng từ danh bạ) · SC điểm xuất phát OFFER ở `ASN`. Cần 1 lượt update `ORD`/`ASN` riêng.

### C-USR-05 · ↳ BA trả lời lượt 4 — 2026-09-16

📍 BA trả lời · 2026-09-16

> "1 đùng r nhé
> 2, chứa chuỗi nhé
> Hạng đồng hành ko hiện nhé
> sdt mặc định từ hrishris
> SDT bắt buộc từ 0 và 10 ky tự là sooss"

↳ **Ghi chú:** (1) Chọn văn phòng ⇒ ô điền **đúng chuỗi `name`** của `DOC-v1.1-04`. (2) Gợi ý khớp kiểu **chứa chuỗi** (`tan` ra cả "Tầng…"). (3) Badge "Hạng Đồng hành" **không hiện** ⇒ `C-USR-06` Resolved. (4) **SĐT mặc định khởi tạo từ HRIS** ⇒ thêm `SC-USR-023`. (5) SĐT: **bắt đầu bằng 0, đúng 10 ký tự, cả 10 là số** ⇒ khoảng trắng / `+84` / chữ đều invalid (`SC-USR-015` mở rộng lớp invalid).
**Còn mở:** avatar khi tên **1 từ** · bấm ← thoát màn khi **chưa lưu** (mất thay đổi hay hỏi xác nhận).

### C-USR-05 · ↳ BA trả lời lượt 5 — 2026-09-16 *(→ RESOLVED)*

📍 BA trả lời · 2026-09-16

> "1. Luôn luôn có 1 từ (Ví dụ :Trần A thì hiển thị là TA )
> 2. Không lưu, không hiện bất kỳ xác nhận nào"

↳ **Ghi chú:** (1) Tên luôn đủ để lấy 2 từ cuối — ví dụ ngắn nhất "Trần A" → `TA` ⇒ **không có trường hợp tên 1 từ**. (2) Bấm ← khi chưa lưu ⇒ **không lưu, không hỏi xác nhận** ⇒ thêm `SC-USR-024`. ⛔ Dòng *"Còn mở"* ngay trên hết hiệu lực — **`C-USR-05` Resolved**.

### C-USR-07 · Địa chỉ mặc định RỖNG — hợp lệ hay không? *(OPEN — mở lại 2026-09-18)*

📍 Nguồn: quan sát thực nghiệm khi chạy `TC-USR-027` · `VR-003-USR-2026-09-18` · tài khoản MNV 00002352

↳ **Dữ kiện (không phải suy diễn):** trong 1 phiên đã bấm **"Lưu thay đổi" 2 lần liên tiếp** với ô **"Địa chỉ mặc định" để TRỐNG hoàn toàn**. Cả 2 lần app **lưu thành công**: không chặn, không báo lỗi dưới field, không hiện cảnh báo, và điều hướng về màn "Cá nhân" đúng như khi dữ liệu đầy đủ. Mở lại màn thì SĐT persist đúng, địa chỉ vẫn rỗng.

**Vì sao đây là câu hỏi chứ không phải bug:** PRD `§8.15.2` ghi địa chỉ mặc định là **"Không bắt buộc"** ⇒ cho lưu rỗng **có thể là đúng spec**. Nhưng `SC-USR-020`/`SC-USR-022` lại được viết theo tinh thần *"luôn có một địa chỉ"* (load HRIS, chọn từ danh sách), và `TC-USR-029` đang **FAIL** một phần vì điểm này ⇒ hai hướng đọc cho ra 2 verdict ngược nhau.

**Câu hỏi cho BA/PM:**
(a) Địa chỉ mặc định **rỗng** có phải trạng thái hợp lệ của hồ sơ không? Nếu có, các màn tiêu thụ nó (`ORD` địa chỉ lấy hàng · `ASN` điểm xuất phát) xử lý thế nào khi rỗng?
(b) Người dùng **có đường nào để XOÁ** địa chỉ đã lưu về rỗng không (ô chỉ nhận giá trị chọn từ danh sách gợi ý — `C-USR-05` chốt ⛔ không nhận text tự do)?
(c) Nếu **không** cho rỗng thì app phải chặn ở đâu — disable nút Lưu, hay báo lỗi dưới field như `BR15-02` làm với SĐT?

**Ảnh hưởng nếu để treo:** `TC-USR-029` không kết luận dứt điểm được (đang FAIL kép, 1 vế đã hết hiệu lực sau khi bug `B1` bị rút lại) · `TC-USR-030` cùng dải cũng dính.

⚠️ **Đừng lẫn với `BUG-008`:** `BUG-008` là *app không NẠP dữ liệu HRIS vào form*; `C-USR-07` là *có được phép LƯU rỗng hay không*. Hai việc khác nhau — fix `BUG-008` xong thì `C-USR-07` **vẫn còn** cần BA trả lời.

### C-USR-06 · Badge "Hạng Đồng hành" — giữ hay bỏ? *(RESOLVED 2026-09-16 — không hiện)*

📍 `DOC-v1.1-01 §8.14.1 BR14-03 · trang 48` · `§6.2 AC-26.1.01 · trang 27` · `§4 SCOPES Out of Scope · trang 9` ⟷ `DOC-v1.0-02 §3.9` · ảnh `00_input/v1.1/design/USR_01_trangcanhan_fields_CUSR04.png`

> ↪ *Quote `BR14-03` — home ở `../GIFT-qua-cam-on/test_scenario_map.md` (không chép lại — tránh lặp home, health-check G-03 2026-09-17)*

> `AC-26.1.01`: "…Không có điểm, tier, xếp hạng hay quy đổi tiền."

> `§4 Out of Scope`: "Đánh giá sao 1–5 và mọi hình thức xếp hạng/tier/điểm thưởng — thay bằng quà ảo"

↳ **Ghi chú:** Phát hiện khi rà `SC-USR-007` (CARRIED từ v1.0): v1.0 coi badge text *"Hạng Đồng hành"* là **ngoại lệ có chủ đích** của `C-USR-01` (tier bị *hoãn* nhưng badge vẫn hiện) và **assert badge tồn tại**. PRD v1.1 cấm **mọi hình thức** xếp hạng/tier **vĩnh viễn** — cùng lý do đã đổi `★★★★★` thành defect (`SC-ACT-013`, `C-GIFT-01`). Demo 2026-09-16 **vẫn hiện** badge. ⇒ Hai SC của cùng dự án đang cho kết luận ngược: `SC-USR-007` PASS khi badge **có**, `SC-GIFT-011`/`SC-USR-006` tinh thần PASS khi **không có** tier.
**Câu hỏi cho BA:** badge "Hạng Đồng hành" là (a) **defect** cần gỡ theo `BR14-03`, hay (b) **nhãn trang trí cố định** (không phải hạng) được giữ — nếu (b) thì PRD cần ghi ngoại lệ. ⛔ Chưa chốt thì `SC-USR-007` **không assert** badge tồn tại lẫn không tồn tại.

↳ **BA chốt 2026-09-16:**
> "Hạng đồng hành ko hiện nhé"

⇒ Phương án (a): badge **không hiển thị**, khớp `BR14-03`. `SC-USR-007` **lật chiều** (assert KHÔNG có badge) và `SC-USR-011` cập nhật cấu trúc header — cả hai chuyển **MODIFIED**. Demo còn hiện badge ⇒ nếu STG còn hiện là **defect**. ⛔ Ghi chú *"không assert"* ở trên hết hiệu lực.

## Khuyến nghị tổng thể
1. 🟡 **Vibe-check qua demo 2026-09-16 đã xác nhận màn "Cập nhật thông tin" tồn tại + đúng field spec** (`RISK-USR-06` hạ xuống Partially confirmed) — vẫn cần **1 lượt xác nhận trên STG thật** trước `generate-tc` để verify nút "Lưu thay đổi" thực sự persist (demo không có backend). Nếu STG cũng khớp thì hạ hẳn xuống Resolved, ⛔ không quay lại kết luận "view-only" của v1.0.
2. 🔴 **`SC-USR-003` phải lấy bản `v1.1/`** — bản v1.0 và v1.1 có Then ngược nhau ở phần *"có control sửa hay không"*, và **cả hai bản đều chạy được** nên không có gì báo lỗi khi lấy nhầm. Cùng bẫy `SC-CNL-006`.
3. **Chạy `SC-USR-017` cùng lô với `SC-CNL-010` · `SC-ORD-065` · `SC-DLV-062`** — bốn rule cùng họ *"bằng chứng đã ghi thì bất biến"*, app đã vi phạm nhóm này 1 lần. Cùng vỡ ⇒ **1 bug report cho nguyên nhân gốc** (`RISK-USR-07`).
4. **`SC-USR-014` bắt buộc có bước mở lại màn kiểm giá trị đã persist** — banner xanh chỉ chứng minh app *nói* đã lưu.
5. ✅ **`C-USR-05` + `C-USR-06` Resolved 2026-09-16** — toàn bộ rule màn "Cập nhật thông tin" đã chốt (xem các khối `↳` của `C-USR-05`). Việc tiếp: cập nhật SC prefill ở `ORD` (`SC-ORD-025`/`058`) + điểm xuất phát ở `ASN`; kiểm trên STG 3 điểm demo lệch rule (badge · avatar trang Cá nhân · ô địa chỉ tự do).
6. **`SC-USR-005` chạy 1 lượt so cả 3 màn** (`USR` · `HOME` · `GIFT`) với cùng 1 đơn `RETURNED` — ⛔ đừng seed 3 lần (`RISK-USR-01`).
