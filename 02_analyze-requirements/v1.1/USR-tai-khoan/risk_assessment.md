---
id: v1.1/USR-tai-khoan/risk
title: Risk Assessment — v1.1 · Module USR
type: risk-assessment
version: v1.1
sprint: 1
module: USR
counts:
  cl: 5
  risk: 8
  cl_open: 1
  cl_resolved: 3
status: ANALYZED
updated: 2026-09-15
---

> Tạo bởi: analyze-requirements (DELTA 2026-09-15, **lượt bù thứ hai**) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (5 dòng, `RISK-USR-01..05`) xem `v1.0/USR-tai-khoan/risk_assessment.md` — KHÔNG lặp lại ở đây. **ID mới bắt đầu từ `RISK-USR-06`.**
> ℹ️ `cl_open (1) + cl_resolved (3) = 4 < cl (5)` — **đúng, không lệch cộng**: `C-USR-04` ở trạng thái **🟡 Partially Resolved**, không thuộc 2 ô đó.

## Tổng quan
| Module | Risk Level | Rủi ro chính (delta v1.1) |
|--------|-----------|--------------|
| USR | **Medium** (tăng từ Low) | Từ module *"view-only, ít rủi ro nhất"* thành module có **một màn ghi dữ liệu** và **2 rule truy vết hai chiều**. Ba rủi ro đáng kể: (1) `SC-USR-003` **đảo chiều** — cùng bẫy `SC-CNL-006`; (2) app STG quan sát 2026-07-24 là view-only hoàn toàn ⇒ **8 SC mới có thể BLOCKED**; (3) `BR15-03` là thành viên thứ tư của nhóm rule truy vết mà app **đã vi phạm 1 lần đã live-verify** |

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-USR-06 | USR / Kết luận bị đảo + app chưa build | **(risk mới)** `C-USR-03` (*"hồ sơ view-only hoàn toàn"*, Resolved 2026-07-24 **theo quan sát app**) bị `FR15` đảo. Hai hệ quả: (a) `SC-USR-003` có Then **ngược nhau giữa 2 bản** và **cả hai bản đều chạy được** ⇒ lấy nhầm bản cho kết luận ngược mà không có gì báo lỗi; (b) app STG có thể **chưa build `FR15`** ⇒ 8 SC mới `BLOCKED` chứ không phải FAIL | **High** | `DOC-v1.1-01` §8.15 (trang 48-49) vs `KP-01` §2 KB-USR-01 (live-verify 2026-07-24) | `SC-USR-003` (lật chiều) · `SC-USR-013..020` (8 SC mới) | **Vibe-test 1 lượt trang Cá nhân trước `generate-tc`** — xác nhận mục "Cập nhật thông tin" đã có chưa. Chưa có ⇒ verdict `BLOCKED`, ⛔ không PASS và ⛔ không quay lại kết luận "view-only" của v1.0 | Open | REQ-USR-002, REQ-USR-008, SC-USR-003, SC-USR-013..020 |
| RISK-USR-07 | USR / Rule truy vết hai chiều | **(risk mới)** `BR15-03`/`BR15-04` là **thành viên thứ tư** của nhóm rule *"bằng chứng đã ghi thì bất biến"* (cùng `BR11-03` · `BR18-05` · `NFR-07`) — và app **đã vi phạm nhóm này 1 lần đã live-verify** (`KB-CNL-01`: huỷ nhận đơn **xoá** dòng "Ghép thành công"). Nếu backend lưu đơn bằng **tham chiếu tới hồ sơ** thay vì **chụp giá trị tại thời điểm đăng**, đổi SĐT hồ sơ sẽ **viết lại cả lịch sử đơn** — lỗi **hoàn toàn âm thầm**, không crash, không cảnh báo | **High** | `DOC-v1.1-01` §8.15.1 BR15-03/BR15-04 (trang 49) · §6.2 AC-30.2.02 (trang 28) — dùng đúng cụm *"phục vụ truy vết"* như `BR18-05` | `SC-USR-017` (**P1**, chiều hồ sơ→đơn) · `SC-USR-018` (chiều đơn→hồ sơ) | Chạy `SC-USR-017` **cùng lô** với `SC-CNL-010` · `SC-ORD-065` · `SC-DLV-062`; nếu cùng vỡ thì **1 bug report cho nguyên nhân gốc**, ⛔ không log 4 bug rời | Open | REQ-USR-009, REQ-USR-010, SC-USR-017, SC-USR-018 |
| RISK-USR-08 | USR / Phạm vi sửa hồ sơ thu hẹp | **(risk mới)** `USR-02` của BRD liệt kê **6 trường** sửa được (*"tên, SĐT, avatar, phòng ban, khu vực/văn phòng, kênh liên hệ"*); `FR15` chỉ cho sửa **2** (SĐT · địa chỉ mặc định) và khoá cứng 4 trường SSO. Còn lại **avatar · khu vực/văn phòng · kênh liên hệ** — PRD **không nhắc ở bất kỳ đâu**: không nói sửa được, không nói chỉ đọc, không nói loại bỏ | Medium | `DOC-v1.1-01` §8.15.1 BR15-01 · §8.15.2 (trang 49) — đã rà toàn văn §8.15, không có 3 trường này vs `DOC-v1.0-01` §A6 USR-02 (L100) | — (không assert được) | Mở `C-USR-05`. ⛔ KHÔNG suy diễn *"không nhắc = bị bỏ"* — `KP-01 §2 KB-USR-01` ghi nhận app **có** hiển thị avatar | Open (non-blocking) | REQ-USR-002, REQ-USR-008, SC-USR-002 |
| RISK-USR-03 | USR / Bằng chứng UI trang Cá nhân | *(cập nhật Status)* v1.0: nhãn mục menu thứ hai + 3 trường hồ sơ **chưa có bằng chứng UI** ⇒ `SC-USR-012` treo dạng `[GAP]` | Medium → **Medium (đã đóng 1 nửa)** | `DOC-v1.1-01` §8.15 dòng Trigger (trang 48) | `SC-USR-012` (hết gap, P3→P2) · `SC-USR-002` (vẫn chưa đủ bằng chứng) | ⚠️ ⛔ **KHÔNG lấy `§8.15.2` làm danh sách trường của trang Cá nhân** — đó là field spec của **màn "Cập nhật thông tin"**, một màn khác | Open (`C-USR-04` Partially) | REQ-USR-006, SC-USR-002, SC-USR-012 |
| RISK-USR-01 | USR / Chỉ số đóng góp | *(cập nhật Why)* 2 chỉ số đóng góp nay có **rule loại trừ** (`BR14-04` — không tính đơn `RETURNED`) và cùng con số hiển thị ở **3 màn** (`USR` · `HOME` · `GIFT`) | Medium | `DOC-v1.1-01` §8.14.1 BR14-04 · §6.2 AC-26.1.01 | `SC-USR-005` — cross-check với `SC-GIFT-014` + `SC-HOME-008` | Home của rule ở `GIFT` (`REQ-GIFT-009`) — ⛔ không nhân bản SC; chạy 3 màn **trong 1 lượt** với cùng 1 đơn `RETURNED` | Open | REQ-USR-004, SC-USR-005 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Nội dung | Status | Mở | REQ/SC liên quan |
|-------|----------|--------|-----|-------------------|
| C-USR-03 | `USR-02` ghi *"Xem/**cập nhật** hồ sơ"* — app có chức năng sửa hồ sơ không? | ✅ **Resolved 2026-09-15 — ĐẢO kết luận v1.0: CÓ, qua màn "Cập nhật thông tin", nhưng chỉ 2 trường** | 2026-07-24 | REQ-USR-002, REQ-USR-008 |
| C-USR-05 | Avatar · khu vực/văn phòng · kênh liên hệ — sửa được, chỉ đọc, hay đã bỏ khỏi sản phẩm? | 🔴 **Open (non-blocking)** | 2026-09-15 | REQ-USR-002, REQ-USR-008, SC-USR-002 |
| C-USR-04 | Nhãn mục menu thứ hai + 3 trường hồ sơ chưa có bằng chứng UI | 🟡 **Partially Resolved 2026-09-15** — nhãn menu đã biết; danh sách trường trang Cá nhân vẫn chưa có | mở 2026-09-07 | REQ-USR-002, REQ-USR-006 |
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
**Vì sao non-blocking:** 8 SC mới của `FR15` không đụng 3 trường này; chỉ `SC-USR-002` (trang Cá nhân) bị treo một phần — và nó đã treo sẵn vì `C-USR-04`.

### C-USR-04 · Nhãn menu + trường hồ sơ *(PARTIALLY RESOLVED 2026-09-15)*

📍 `DOC-v1.1-01 §8.15 dòng Trigger · trang 48`

> "Mở "Cập nhật thông tin" trong trang cá nhân (nằm dưới mục "Quà đã nhận")"

↳ **Ghi chú:** **Nửa đã xong:** nhãn mục menu thứ hai là **"Cập nhật thông tin"**, và biết luôn **thứ tự tương đối** (dưới "Quà đã nhận") ⇒ `SC-USR-012` hết `[GAP]`, nâng P3 → P2.
**Nửa còn lại — và đây là chỗ rất dễ kết luận sai:** `§8.15.2` liệt kê trường của **màn "Cập nhật thông tin"**, ⛔ **KHÔNG phải** danh sách trường hiển thị trên **trang Cá nhân**. Hai màn khác nhau, hai bộ trường khác nhau. Lấy nhầm sẽ làm `SC-USR-002` assert sai danh sách. ⇒ giữ **Partially Resolved**, ⛔ không đóng hẳn; cần bằng chứng UI (vibe-test hoặc Figma) cho trang Cá nhân.

## Khuyến nghị tổng thể
1. 🔴 **Vibe-test 1 lượt trang Cá nhân TRƯỚC `generate-tc`** — xác nhận mục "Cập nhật thông tin" đã có trên STG chưa. App quan sát 2026-07-24 là **view-only hoàn toàn**; nếu chưa build thì **8/8 SC mới `BLOCKED`** và viết TC lúc này là viết cho một màn chưa tồn tại (`RISK-USR-06`).
2. 🔴 **`SC-USR-003` phải lấy bản `v1.1/`** — bản v1.0 và v1.1 có Then ngược nhau ở phần *"có control sửa hay không"*, và **cả hai bản đều chạy được** nên không có gì báo lỗi khi lấy nhầm. Cùng bẫy `SC-CNL-006`.
3. **Chạy `SC-USR-017` cùng lô với `SC-CNL-010` · `SC-ORD-065` · `SC-DLV-062`** — bốn rule cùng họ *"bằng chứng đã ghi thì bất biến"*, app đã vi phạm nhóm này 1 lần. Cùng vỡ ⇒ **1 bug report cho nguyên nhân gốc** (`RISK-USR-07`).
4. **`SC-USR-014` bắt buộc có bước mở lại màn kiểm giá trị đã persist** — banner xanh chỉ chứng minh app *nói* đã lưu.
5. **`C-USR-05` gộp vào lượt hỏi BA chung** với `C-ORD-04`, `C-ORD-09`, `C-ACT-02` — đều là câu hỏi doc ⟷ app / doc thiếu.
6. **`SC-USR-005` chạy 1 lượt so cả 3 màn** (`USR` · `HOME` · `GIFT`) với cùng 1 đơn `RETURNED` — ⛔ đừng seed 3 lần (`RISK-USR-01`).
