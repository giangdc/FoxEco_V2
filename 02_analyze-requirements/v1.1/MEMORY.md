---
id: v1.1/router
title: Router — Analyze v1.1 sprint-1 (delta)
type: router
version: v1.1
sprint: 1
modules: 11
doc_source:
  - id: DOC-v1.1-01
    file: 00_input/v1.1/FoxEco PRD v1.0 - Gui Hang.pdf
    revision: "PRD v1.0 · mã 1.0-BM/PM/HDCV/FTEL · PRD Standard v1.2 · rev 08/09/2026 \"[A] Bổ sung flow exit giao hàng\" · Active"
    md5: caf8af665163f6c5c2d85daec414efa6
    kind: "PRD chính thức — nguồn nghiệp vụ CHÍNH của v1.1, chi tiết hơn hẳn DOC-v1.0-01/02. ⚠️ CÙNG tính năng \"Gửi Hàng\" đã phân tích ở v1.0 (khớp gần 1:1 qua FR01–FR18), KHÔNG phải sản phẩm mới"
    modules: [HOME, ASN, DLV, NTF, TS]
  - id: DOC-v1.1-02
    file: 00_input/v1.1/FoxEco Demo 3 vai tro (standalone) v4.0 (1).html
    revision: "prototype 3 vai trò bản v4.0 (kế thừa DOC-v1.0-03) · Active · reference-only"
    md5: 0f336205b8c66da40f2741c51d52a6a5
    kind: "KHÔNG PHẢI URD — prototype tương tác, reference-only (⛔ không trích làm nguồn rule)"
    modules: []
status: ANALYZED
updated: 2026-09-15
---

# Router — Analyze v1.1 sprint-1 (delta)

> **File này là BẢN ĐỒ, không phải kho nội dung.** Nội dung thật nằm ở **6 file / module**; router chỉ trả lời 2 câu: *"chức năng này ở module nào"* và *"module này lớn cỡ nào, rủi ro ra sao"*.
> 📜 **Lịch sử từng lượt của mỗi module** → `<module>/CHANGELOG.md §1`. **Lịch sử router bản cũ** → `git show <commit>:<path>`.
> 🔑 **Nguồn canonical của số đếm là FILE MODULE** — xem §Luật `counts` canonical dưới. Bảng §2 là **bản dẫn xuất**: sửa số ở file module trước, rồi mới đồng bộ về đây.
>
> ℹ️ **v1.1 là DELTA — 10/11 module có thư mục ở đây.** Module duy nhất không có delta:
>
> | Module | Vì sao không có delta |
> |---|---|
> | `FEED` | `DOC-v1.1-01` không liệt kê module này ở `MASTER-MEMORY §2`; rà `§7.2 Feature Traceability` cũng không có FR nào thuộc bề mặt Bảng tin ⇒ giữ nguyên v1.0. ⛔ Không dựng thư mục rỗng |
>
> 🔴 **`USR` từng bị khai nhầm là "không có delta" (2026-09-15) — đã sửa cùng ngày.** `FR15` đặc tả hẳn một màn mới (`"Cập nhật thông tin"`), và chính lượt delta trước đã trích `AC-30.1.01` — một AC **thuộc `FR15`** — để resolve `C-ORD-10`, tức đã dùng `FR15` làm căn cứ trong khi tuyên bố nó ngoài phạm vi. Chi tiết: `USR-tai-khoan/CHANGELOG.md §1` dòng `ĐÍNH CHÍNH`.

## 1. Function Register

| Module | Dir | Chức năng | DOC Source | Dải REQ | Dải SC |
|---|---|---|---|---|---|
| **HOME** | [`HOME-trang-chu/`](HOME-trang-chu/) | Trang chủ — section "Tin mới" chốt **5 tin** + 3 lớp lọc, 3 empty state mới `EMP-01..03`, NFR01 hiệu năng | `DOC-v1.1-01` §6.1/§6.2 US11+AC-11.x · §8.17/§8.17.1 FR17 · §9 NFR01 | `REQ-HOME-001..013` | `SC-HOME-001..028` |
| **ASN** | [`ASN-ghep-noi/`](ASN-ghep-noi/) | Ghép nối — PRD chốt phần lớn tham số auto-match (điều kiện khớp, buổi "giờ nào cũng được", trần gợi ý 5, trần thông báo/ngày) | `DOC-v1.1-01` §8.3 FR03 · §8.4 FR04 · §9 NFR-04/06/08/11 | `REQ-ASN-001..013` | `SC-ASN-001..019` |
| **DLV** | [`DLV-giao-nhan/`](DLV-giao-nhan/) | Giao nhận & Theo dõi đơn — **delta lớn nhất**: form "Xác nhận giao hàng" 4 loại đối tượng nhận, nhánh không liên lạc được, 2 chế độ cầm hàng về, state machine mở rộng, log append-only | `DOC-v1.1-01` §8.6 FR06 · §8.7 FR07 · §8.8 FR08 · §8.9 FR09 · §8.10.1 BR10-04 · §8.12 FR12 · §8.18.1 BR18-04 · §9 NFR-03/07/12 | `REQ-DLV-001..023` | `SC-DLV-001..064` |
| **NTF** | [`NTF-thong-bao/`](NTF-thong-bao/) | Thông báo — danh mục chính thức mở rộng **9 → 15 sự kiện** (`NTF-10..15` cho các nhánh mới của `DLV`) | `DOC-v1.1-01` §8.13 FR13 · §8.13.1 Danh mục thông báo (bảng 15 dòng, trang 47-48) | `REQ-NTF-001..012` | `SC-NTF-001..022` |
| **TS** | [`TS-trust-safety/`](TS-trust-safety/) | Trust & Safety — **`FR16` Báo cáo sự cố & hỗ trợ** (tính năng mới: nút trigger + form WebView + trần 5 ảnh) | `DOC-v1.1-01` §8.16 FR16 · §8.16.1 BR16-01..06 · §8.16.2 UI/Field Spec · §6.1 US31 · §6.2 AC-31.x | `REQ-TS-001..006` | `SC-TS-001..015` |
| **USR** | [`USR-tai-khoan/`](USR-tai-khoan/) | Tài khoản & Hồ sơ — **`C-USR-03` ĐẢO**: có màn `"Cập nhật thông tin"` sửa được **2 trường** (SĐT · địa chỉ mặc định); 4 trường SSO vẫn chỉ đọc; +2 rule truy vết hai chiều | `DOC-v1.1-01` §8.15 FR15 · §8.15.1 BR15-01..05 · §8.15.2 · §6.1 US30 · §6.2 AC-30.x | `REQ-USR-001..010` | `SC-USR-001..020` |
| FEED | [`../v1.0/FEED-bang-tin/`](../v1.0/FEED-bang-tin/) | *(không cần delta — PRD không đụng)* Bảng tin & Chi tiết tin | v1.0 | `REQ-FEED-001..009` | `SC-FEED-001..014` |
| **ORD** | [`ORD-dang-tin/`](ORD-dang-tin/) | Đăng tin & Quản lý tin — ảnh **bắt buộc ≥1**, tra **danh bạ nội bộ**, người nhận uỷ quyền khai lúc đăng tin, tiện ích dùng chung `FR18` | `DOC-v1.1-01` §8.1 FR01 · §8.2 FR02 · §8.5 FR05 · §8.18 FR18 · §6.2 AC-01..09/19/20/30 | `REQ-ORD-001..028` | `SC-ORD-001..065` |
| **ACT** | [`ACT-hoat-dong/`](ACT-hoat-dong/) | Hoạt động ("Đơn của tôi") — `EMP-05`/`EMP-06` đóng `C-ORD-06`; kết cục `RETURNED` mới; **home rule hình thức chung của `FR17`** | `DOC-v1.1-01` §8.17 FR17 · §8.17.1/§8.17.2 · §8.5.1 BR05-03 · §6.2 AC-29/AC-09/AC-24 | `REQ-ACT-001..010` | `SC-ACT-001..017` |
| **GIFT** | [`GIFT-qua-cam-on/`](GIFT-qua-cam-on/) | Quà cảm ơn — 4 quà có **tên chính thức**, đơn `RETURNED` **không mở bước tặng quà và không cộng "Đơn đã giúp"**; 3 SC `[GAP]` hết gap | `DOC-v1.1-01` §8.14 FR14 · §8.14.1 BR14-01..04 · §8.17.1 EMP-08 · §6.2 AC-24/AC-26 | `REQ-GIFT-001..009` | `SC-GIFT-001..014` |
| **CNL** | [`CNL-huy-don/`](CNL-huy-don/) | Huỷ đơn / Huỷ nhận đơn — **`C-CNL-01` ĐẢO** (Báo sự cố vào scope), `BR11-03` biến bug audit thành vi phạm đặc tả, ngưỡng được-huỷ phát biểu theo **hành động** | `DOC-v1.1-01` §8.11 FR11 · §8.11.1 BR11-01..04 · §8.18.2 VAL-03/04 · §6.2 AC-25.x | `REQ-CNL-001..009` | `SC-CNL-001..017` |

> 📁 **Quy ước tên thư mục giữ nguyên v1.0** (`MASTER-MEMORY §9` quyết định 6): `Dir` = `<CODE>-<slug>`, token ID vẫn là `SC-<CODE>-<NNN>`.
> ⚠️ **Bẫy tra cứu:** ID **không** suy ra được tên thư mục, và thư mục **dùng lại qua nhiều sprint** ⇒ phân biệt **bắt buộc bằng dải ID** ở bảng trên (khớp `id_range` trong frontmatter `CHANGELOG.md`).
> 🔴 **Dải ID v1.1 CHỒNG LÊN v1.0 vì đây là delta cộng dồn, không phải sprint mới:** `SC-DLV-001..030` là SC v1.0 (CARRIED, nội dung ở `../v1.0/`), `SC-DLV-031..064` mới sinh ở v1.1. SC **MODIFIED giữ nguyên ID v1.0** và bản **v1.1 là bản authoritative** — ⛔ không sửa bản v1.0 của chúng. Danh sách SC MODIFIED từng module ở `<module>/CHANGELOG.md` frontmatter `id_range.sc`.
> ⛔ Không module nào bị gộp/xoá ở lượt này.

## 2. Module Summary

> 📐 **Bảng dẫn xuất** — sinh lại / đối chiếu bằng cách đọc `counts:` ở frontmatter từng file module:
> ```bash
> for m in 02_analyze-requirements/v1.1/*/; do
>   echo "== $(basename $m)"
>   sed -n '/^counts:/,/^status:/p' "$m/test_scenario_map.md"
>   sed -n '/^counts:/,/^status:/p' "$m/risk_assessment.md"
> done
> ```

### 2a. Module CÓ delta ở v1.1 (10/11 module — số **tính tới v1.1**, gồm cả CARRIED từ v1.0)

| Module | Req | SC | NEW | MOD | CARRIED | DEPR | P1 | P2 | P3 | CL | RISK | Risk Level |
|---|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|---|
| USR | 10 | 20 | 8 | 3 | 9 | 0 | 3 | 10 | 7 | 5 | 8 | Medium |
| HOME | 13 | 28 | 4 | 2 | 21 | 1 | 1 | 13 | 13 | 3 | 7 | Medium |
| FEED | — | — | — | — | — | — | — | — | — | — | — | *(không delta — xem `../v1.0/`)* |
| ORD | 28 | 65 | 14 | 12 | 39 | 0 | 9 | 36 | 20 | 11 | 12 | **High** |
| ACT | 10 | 17 | 3 | 6 | 8 | 0 | 0 | 11 | 6 | 3 | 8 | Medium |
| ASN | 13 | 19 | 1 | 5 | 13 | 0 | 6 | 11 | 2 | 2 | 8 | **High** |
| DLV | 23 | 64 | 34 | 0 | 30 | 0 | 10 | 42 | 12 | 4 | 11 | **High** |
| GIFT | 9 | 14 | 2 | 6 | 6 | 0 | 0 | 9 | 5 | 3 | 6 | Low |
| CNL | 9 | 17 | 4 | 5 | 8 | 0 | 6 | 9 | 2 | 3 | 8 | **High** |
| NTF | 12 | 22 | 6 | 3 | 13 | 0 | 1 | 15 | 6 | 2 | 7 | Low |
| TS | 6 | 15 | 8 | 0 | 7 | 0 | 2 | 5 | 8 | 1 | 7 | Medium |
| **Tổng (10 module delta)** | **133** | **281** | **84** | **42** | **154** | **1** | **38** | **161** | **81** | **37** | **82** | — |

### 2b. Toàn bộ v1.1 (10 module delta + 1 module giữ nguyên v1.0)

| Nhóm | Req | SC | P1 | P2 | P3 | CL | RISK |
|---|--:|--:|--:|--:|--:|--:|--:|
| 10 module delta (bảng 2a) | 133 | 281 | 38 | 161 | 81 | 37 | 82 |
| 1 module không delta (`FEED`) — đọc `../v1.0/` | 9 | 14 | 2 | 6 | 6 | 3 | 5 |
| **Tổng v1.1** | **142** | **295** | **40** | **167** | **87** | **40** | **87** |

> ℹ️ **Δ so với v1.0:** REQ 116 → **142** (+26) · SC 211 → **295** (**+84 NEW**, 42 MODIFIED giữ ID, 1 DEPRECATED) · CL 35 → **40** (+5: `C-DLV-04` · `C-CNL-03` · `C-ACT-02` · `C-ORD-13` · `C-USR-05`) · RISK 64 → **87** (+23).
> ℹ️ **P1+P2+P3 = 40+167+87 = 294 = 295 − 1 DEPRECATED** ⇒ **không lệch cộng**, đúng `Project_rule.md §Quy ước đếm scenario`. SC bị DEPRECATED: `SC-HOME-024`.
> ℹ️ **Cột `CL` chỉ đếm clarification có HOME ở module đó** — CL tham chiếu chéo không cộng lặp. `cl_open + cl_resolved` **nhỏ hơn** `cl`: **4 CL ở trạng thái *Partially Resolved*** (`C-NTF-02` home ASN · `C-NTF-03` home NTF · `C-ORD-09` home ORD · `C-USR-04` home USR) không thuộc 2 ô đó.
> 🟢 **CL còn OPEN — 10/40** (9 ở 10 module delta + 1 của `FEED`), ⛔ **0 BLOCKER chặn execute.**
> **v1.1 chuyển 10 CL từ Open → Resolved:** `C-HOME-01` `C-HOME-02` `C-HOME-03` · `C-NTF-01` · `C-GIFT-03` · `C-ORD-05` `C-ORD-08` `C-ORD-10` `C-ORD-11` · `C-ORD-06`.
> **Nâng cấp / đảo chiều (đã Resolved ở v1.0, nay đổi nội dung):** `C-CNL-01` (out-of-scope → **in-scope**) · `C-USR-03` (view-only hoàn toàn → **có màn sửa 2 trường**) · `C-CNL-02` (override QA → đặc tả PM) · `C-GIFT-01` (out-of-scope *v1.0* → out-of-scope vĩnh viễn).
> **Mở mới 5:** `C-DLV-04` (Resolved ngay) · `C-CNL-03` · `C-ACT-02` · `C-ORD-13` · `C-USR-05`. **Chuyển Partially: 2** (`C-ORD-09` · `C-USR-04`). **MỞ LẠI 1:** `C-ORD-04` — PRD tự mâu thuẫn.
> 🔴 **4 nợ chặn `generate-tc` v1.1** — không phải blocker execute, nhưng chạy TC trước khi xong sẽ FAIL/BLOCKED hàng loạt vì lý do không phải bug:
> | Nợ | Module | Ảnh hưởng |
> |---|---|---|
> | `C-ORD-04` — **PRD tự mâu thuẫn**: `§8.1.4` cho "Thuốc/Y tế" là loại hàng hợp lệ, `BR01-07` xếp "thuốc" vào hàng cấm | ORD | Không phân xử được bằng thứ tự ưu tiên nguồn (cả hai cùng là `DOC-v1.1-01`) ⇒ `SC-ORD-031..035` phải ghi nhận, không assert |
> | `C-ORD-13` — STG đã nối **Danh bạ nội bộ** chưa, có email mẫu không | ORD | 3 SC (1 **P1**) `BLOCKED` nếu thiếu — không tự chế được email mẫu |
> | `RISK-DLV-08` + `RISK-DLV-11` — luồng submit form 4 đối tượng nhận & ảnh lúc lấy hàng chưa verify end-to-end | DLV | Kéo theo `GIFT` (`SC-GIFT-013/014`) và `ACT` (`SC-ACT-015`) vì cùng cần đơn `RETURNED` |
> | `RISK-ORD-09` — app đã siết **ảnh bắt buộc ≥1** chưa | ORD | `SC-ORD-054` là **P1 chặn luồng chính**; chưa siết ⇒ FAIL vì *"app chưa cập nhật"* |
> 🟡 **2 câu hỏi nhãn UI nên gộp 1 lượt hỏi BA** — `C-ORD-09` (nhãn "Tài liệu" ⟷ "Giấy tờ, hồ sơ") và `C-ACT-02` (nhãn 2 tab "Đang chạy/Hoàn tất" ⟷ "Đang diễn ra/Đã hoàn thành"): **cùng bản chất doc ⟷ app**, và nhãn nằm rải trong Steps của rất nhiều TC ⇒ chốt muộn sẽ phải sửa rải rác (đúng lỗi #1 của đợt cũ).

### 🔑 Luật `counts` canonical (v2)

Mỗi chỉ số có **đúng 1 nguồn canonical**; mọi nơi khác chỉ được **trỏ tới**, ⛔ không chép lại số:

| Chỉ số | Nguồn canonical |
|---|---|
| REQ · SC (+ NEW/MOD/CARRIED/DEPR · P1/P2/P3) | `<module>/test_scenario_map.md` — frontmatter `counts:` |
| CL · RISK | `<module>/risk_assessment.md` — frontmatter `counts:` (chỉ CL có home ở module đó) |
| Dải ID (`id_range`) | `<module>/CHANGELOG.md` — frontmatter |

🔴 **NGHĨA của `counts:` ở version delta — chốt 2026-09-15: CUMULATIVE, tính tới version này.**
`sc` = CARRIED + MODIFIED + NEW + DEPRECATED (toàn bộ SC còn thuộc module tính tới v1.1), **KHÔNG** phải chỉ phần delta. Tương tự cho `req` · `cl` · `risk`.
⚠️ Trước lượt UPDATE 2026-09-15, `NTF` dùng nghĩa **delta-only** trong khi 4 module kia dùng cumulative ⇒ cộng ngang 5 module ra **134**, một con số không có nghĩa gì. Đã chuẩn hoá — xem `<module>/CHANGELOG.md §1` dòng `ĐÍNH CHÍNH` của `NTF` · `HOME` · `DLV` · `TS` · `ASN`.

⛔ **Router §2 và MASTER-MEMORY là bản dẫn xuất** — khi lệch, **file module thắng**. Sửa số: sửa ở module trước, đồng bộ lên sau, và ghi 1 dòng `ĐÍNH CHÍNH` ở `<module>/CHANGELOG.md §1`.

### ⛔ Không thuộc router v2

| Từng ở router v1 | Home ở v2 |
|---|---|
| §4 Scenario Index | `<module>/test_scenario_map.md` |
| §5 Test Data Summary | `<module>/test_data_catalog.md` |
| §6 Clarifications | `<module>/risk_assessment.md` (CL section) |
| §9 TC Generation Log | nơi `generate-tc` ghi (`MASTER-MEMORY §6`) |
| Lịch sử từng lượt UPDATE / banner *"Cập nhật lần cuối"* | `<module>/CHANGELOG.md §1` |
| Source Detail (quote REQ) | `<module>/requirement_traceability.md §2` |
