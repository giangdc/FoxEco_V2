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
    modules: [USR, HOME, ORD, ACT, ASN, DLV, GIFT, CNL, NTF, TS, FEED]
  - id: DOC-v1.1-02
    file: 00_input/v1.1/FoxEco Demo 3 vai tro (standalone) v4.0 (1).html
    revision: "prototype 3 vai trò bản v4.0 (kế thừa DOC-v1.0-03) · Active · reference-only"
    md5: 0f336205b8c66da40f2741c51d52a6a5
    kind: "KHÔNG PHẢI URD — prototype tương tác, reference-only (⛔ không trích làm nguồn rule)"
    modules: []
  - id: DOC-v1.1-03
    file: 00_input/v1.1/design/ (31 ảnh PNG)
    revision: "ảnh chụp demo DOC-v1.1-02 · vibe-check 2026-09-15/16/17 · Active · evidence phụ · +5 ảnh QC bổ sung 2026-09-17"
    kind: "Ảnh bằng chứng UI — ⚠ demo ≠ STG; ⛔ không trích làm nguồn rule. 26 ảnh theo tiền tố module + 5 ảnh KHÔNG theo tiền tố (Goi dien · gia tri hang uoc tinh → ORD · gift_tang_qua_man_doncuatoi → GIFT · ORD_08_card toi nhan giao hang · ORD_08_dangtin_offer_ghide_len_don_dang_co)"
    modules: [ASN, DLV, FEED, GIFT, HOME, NTF, ORD, TS, USR]
  - id: DOC-v1.1-04
    file: 00_input/v1.1/location_address_catalog.xlsx
    revision: "BA cấp 2026-09-16 · Active · danh mục 399 văn phòng FTEL (name · search_text · mã tỉnh · toạ độ)"
    kind: "DỮ LIỆU MASTER, không phải tài liệu rule — nguồn danh sách gợi ý \"Địa chỉ mặc định\". ⚠ 118 name bị cắt 30 ký tự · toàn bộ coordinate_status = MISSING (C-FEED-05: thiếu/sai toạ độ là data lỗi, bỏ qua). Profile: 04_test-data/valid/USR-office-catalog.md"
    modules: [USR, ORD, ASN, FEED]
  - id: DOC-v1.1-05
    file: 00_input/v1.1/datatest
    revision: "QC GiangDC2 cấp 2026-09-18 · Active · 5 tài khoản STG đang làm việc + 1 đã nghỉ việc (email · MNV · SĐT · văn phòng HRIS) · pass dùng chung + OTP"
    md5: 46da8236095ef20ba140d5fffee9b381
    kind: "DỮ LIỆU TÀI KHOẢN TEST, không phải tài liệu rule — nguồn tài khoản vibe-test + oracle prefill HRIS cho TC-USR-040..044. 🔒 chứa credentials ⇒ .gitignore, KHÔNG commit; pass tách sang ~/.foxeco-v2/credentials.env. Mapping vai + gap: 04_test-data/valid/USR-accounts.md. ⚠ địa chỉ HRIS = mã tỉnh + tên VP (khác cột name của DOC-v1.1-04) · 🔴 không có tài khoản HRIS trống ⇒ TC-USR-041/044 BLOCKED"
    modules: [USR, ORD, ASN, DLV, GIFT]
status: ANALYZED
updated: 2026-09-18
---

# Router — Analyze v1.1 sprint-1 (delta)

> **File này là BẢN ĐỒ, không phải kho nội dung.** Nội dung thật nằm ở **6 file / module**; router chỉ trả lời 2 câu: *"chức năng này ở module nào"* và *"module này lớn cỡ nào, rủi ro ra sao"*.
> 📜 **Lịch sử từng lượt của mỗi module** → `<module>/CHANGELOG.md §1`. **Lịch sử router bản cũ** → `git show <commit>:<path>`.
> 🔑 **Nguồn canonical của số đếm là FILE MODULE** — xem §Luật `counts` canonical dưới. Bảng §2 là **bản dẫn xuất**: sửa số ở file module trước, rồi mới đồng bộ về đây.
>
> ℹ️ **v1.1 là DELTA — 10/11 module có thư mục ở đây.** Module duy nhất không có thư mục v1.1:
>
> | Module | Vì sao không có thư mục v1.1 |
> |---|---|
> | `FEED` | PRD **có** chạm bề mặt Bảng tin/Chi tiết tin (`AC-12.1.01`, `AC-13.1.02`, `EMP-04`, `BR18-04`, `BR01-01`) nhưng module **không dựng thư mục v1.1** — thay đổi 2026-09-16 (`C-FEED-01` Resolved, `SC-FEED-009`/`013` viết lại, `C-FEED-02..04` mở) **sửa tại chỗ ở `v1.0/FEED-bang-tin/`**, xem `CHANGELOG §3`. *(Nhận định cũ "PRD không đụng bề mặt Bảng tin" HẾT HIỆU LỰC 2026-09-16.)* |
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
| FEED | [`../v1.0/FEED-bang-tin/`](../v1.0/FEED-bang-tin/) | Bảng tin & Chi tiết tin — *không có thư mục v1.1*; cập nhật 2026-09-16 (**bản đồ thật**, CTA chỉ ở Chi tiết tin, 3 CL mới) sửa tại chỗ ở v1.0 | v1.0 · `DOC-v1.1-01` AC-12/13 · EMP-04 (chạm) | `REQ-FEED-001..009` | `SC-FEED-001..014` |
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
| USR | 10 | 24 | 12 | 5 | 7 | 0 | 3 | 14 | 7 | 6 | 8 | Medium |
| HOME | 13 | 30 | 6 | 3 | 19 | 2 | 1 | 13 | 14 | 6 | 7 | Medium |
| FEED | — | — | — | — | — | — | — | — | — | — | — | *(không có thư mục v1.1 — số ở `../v1.0/`, xem 2b)* |
| ORD | 28 | 65 | 14 | 12 | 39 | 0 | 9 | 36 | 20 | 16 | 12 | **High** |
| ACT | 10 | 17 | 3 | 6 | 8 | 0 | 0 | 11 | 6 | 5 | 8 | Medium |
| ASN | 13 | 19 | 1 | 5 | 13 | 0 | 6 | 11 | 2 | 5 | 8 | **High** |
| DLV | 23 | 64 | 33 | 0 | 30 | **1** | 10 | 42 | 11 | 8 | 11 | **High** |
| GIFT | 9 | 14 | 2 | 6 | 6 | 0 | 0 | 9 | 5 | 4 | 6 | Low |
| CNL | 9 | 17 | 4 | 5 | 8 | 0 | 6 | 9 | 2 | 3 | 8 | **High** |
| NTF | 12 | 22 | 6 | 3 | 13 | 0 | 1 | 15 | 6 | 4 | 7 | Low |
| TS | 6 | 15 | 8 | 0 | 7 | 0 | 2 | 5 | 8 | 3 | 7 | Medium |
| **Tổng (10 module delta)** | **133** | **287** | **89** | **45** | **150** | **3** | **38** | **165** | **81** | **60** | **82** | — |

### 2b. Toàn bộ v1.1 (10 module delta + 1 module giữ nguyên v1.0)

| Nhóm | Req | SC | P1 | P2 | P3 | CL | RISK |
|---|--:|--:|--:|--:|--:|--:|--:|
| 10 module delta (bảng 2a) | 133 | 287 | 38 | 165 | 81 | 60 | 82 |
| 1 module không có thư mục v1.1 (`FEED`) — đọc `../v1.0/` | 9 | 15 | 2 | 6 | 7 | 7 | 5 |
| **Tổng v1.1** | **142** | **302** | **40** | **171** | **88** | **67** | **87** |

> ℹ️ **Δ so với v1.0:** REQ 116 → **142** (+26) · SC 211 → **302** (**+89 NEW** ở 10 module delta + 1 NEW sửa tại chỗ `FEED`, **45 MODIFIED** giữ ID, **3 DEPRECATED** — ⚠️ **đính chính 2026-09-17 lượt 2:** `SC-ORD-059` **giữ `NEW`**; nhãn `MODIFIED` gán cùng ngày là SAI vì SC này sinh ở v1.1, không có ID ở v1.0. Phép kiểm + chứng cứ: `MASTER-MEMORY §3`) · CL 35 → **66** (+1 `C-FEED-05` 2026-09-17) (+5 lượt delta 2026-09-15: `C-DLV-04` · `C-CNL-03` · `C-ACT-02` · `C-ORD-13` · `C-USR-05`; **+25 lượt UPDATE 2026-09-16** sau khi BA trả lời — xem `<module>/CHANGELOG.md §1`) · RISK 64 → **87** (+23).
> ℹ️ **P1+P2+P3 = 40+171+88 = 299 = 302 − 3 DEPRECATED** ⇒ **không lệch cộng**, đúng `Project_rule.md §Quy ước đếm scenario`. SC bị DEPRECATED: `SC-HOME-024` · `SC-HOME-010` (2026-09-17, thay bằng `SC-HOME-026`) · **`SC-DLV-060`** (2026-09-17 — descope role admin, xem `MASTER §3`).
> ℹ️ **Cột `CL` chỉ đếm clarification có HOME ở module đó** — CL tham chiếu chéo không cộng lặp. `cl_open + cl_resolved` **nhỏ hơn** `cl` ở 3 module: **5 CL *Partially Resolved — chờ BA vòng 2*** (`C-ORD-04` · `C-ORD-13` · `C-HOME-04` · `C-HOME-06` · `C-GIFT-04`) không thuộc 2 ô đó. *(`C-USR-05` → Resolved 2026-09-16.)* ⛔ **HẾT HIỆU LỰC từ 2026-09-17** — cả 5 CL này đã đóng; hiện chỉ còn **1 module** lệch (`DLV`: 0 + 7 < 8) vì `C-DLV-08` Partially.
> 🟡 **Trạng thái CL sau lượt BA trả lời 2026-09-17 (sáng) — 66 CL: 43 Resolved · 5 Partially (vòng 2) · 18 Open** (tính từ `counts:` các module),
> **BA trả lời lượt 2026-09-17 (sáng):** ✅ `C-HOME-05` (hiện empty state `EMP-02` ⇒ `SC-HOME-010` DEPRECATED) · `C-FEED-02` (placeholder + "0km", ảnh tĩnh vẽ tuyến) · `C-FEED-03` (1 danh sách, không tab/lọc) · `C-FEED-04` (trước ghép chỉ ẩn SĐT) · USR chuỗi lỗi SĐT theo demo + PRD sẽ cập nhật sau. 🟡 Partially: `C-HOME-04` (BA nói tin **toàn quốc** ⟷ PRD lọc khu vực) · `C-HOME-06` (+`SC-HOME-029/030`) · `C-GIFT-04` (tặng 1 lần; "tặng sau" mâu thuẫn `C-ACT-01`). 🔴 Mới: `C-FEED-05` (toạ độ văn phòng lỗi). Chi tiết: `<module>/CHANGELOG.md §1` dòng 2026-09-17.
> 🟢 **Cập nhật 2026-09-17 (chiều) — vibe-check demo QA GiangDC2 (Playwright MCP, đi lần lượt các mục BA yêu cầu "vào demo xem") + đồng bộ nốt các câu trả lời BA của `ORD-14/15/17`, `ACT-03`, `GIFT-04(vòng2)`, `TS-02` vào `<module>/risk_assessment.md` (trước đó chỉ có ở `CL-hoi-BA-v1.1.xlsx`, chưa ghi vào canonical).** Trạng thái mới: **49 Resolved · 10 Partially (vòng 2) · 7 Open** (49+10+7=66). Đóng thêm: `C-ORD-14/15/17` · `C-ACT-03` · `C-GIFT-04(vòng2)` · `C-TS-02`. Vòng 2 mới/cập nhật: `C-ORD-16` · `C-ACT-04` · `C-DLV-05/06/08` (đã map rõ cấu trúc UI qua demo, gồm phát hiện field "Người nhận tại quầy" chưa có trong PRD ở `C-DLV-06/08`) · `C-TS-03` (còn (c) kỹ thuật nhúng). Ghi nhận **giới hạn demo** (không tự verify được, đã đặt lại câu hỏi cho BA thay vì suy diễn): `C-ORD-16-c`/`C-ACT-04-c` (đăng OFFER ghi đè lên đơn NEED thay vì tạo card riêng — demo dùng chung 1 đơn toàn cục) · `C-GIFT-04-ý2` (ô tải ảnh bằng chứng không mở được file picker, không tới được màn "Hoàn thành"). Ảnh mới: `00_input/v1.1/design/ORD_08_dangtin_offer_ghide_len_don_dang_co.png`. Chi tiết: `<module>/CHANGELOG.md §1` dòng 2026-09-17 (bản ghi thứ 2 trong ngày) + `CL-hoi-BA-v1.1.xlsx`.
> 🟢 **Cập nhật 2026-09-17 (tối) — rà soát TOÀN BỘ workbook `CL-hoi-BA-v1.1.xlsx` theo yêu cầu QC (quét từng dòng mọi sheet, không chỉ mục nhắc demo).** Phát hiện 12 dòng trong xlsx đã có câu trả lời BA đầy đủ nhưng chưa được đóng sổ (thiếu KẾT LUẬN + đổi trạng thái) — 1 dòng (`C-ACT-03`) hoá ra đã đóng sổ đúng ở `risk_assessment.md` từ lượt chiều, chỉ riêng xlsx bị sót; 11 dòng còn lại (`C-ORD-04(v2)` · `C-ORD-13(v2)` · `C-HOME-04(v2)` · `C-HOME-06(v2)` · `C-ASN-04/05/06` · `C-NTF-04/05` · `C-FEED-05`) chưa có ở cả xlsx lẫn canonical — nay đã đồng bộ cả hai, đóng **10/11** (chỉ `C-HOME-04` giữ 1 câu con — chuỗi empty state khi không lọc khu vực). **Trạng thái CUỐI CÙNG: 58 Resolved · 7 Partially (vòng 2) · 1 Open** (58+7+1=66, tính từ `counts:` từng module — xem lệnh đối chiếu ở đầu §2). **6 module HẾT điểm hỏi BA:** USR · CNL · GIFT · ASN · NTF · FEED. Chỉ còn **1 CL Open thật sự trong toàn bộ v1.1: `C-DLV-07`** ("nhắc"/"chuyển admin hỗ trợ" — rule time-based, demo tĩnh không mô phỏng được, cần BA/Dev trả lời trực tiếp bằng lời). 7 CL Partial còn lại đều chỉ còn **đúng 1 câu con nhỏ**, trừ 3 CL của `DLV` (`C-DLV-05/06/08`) cần BA xác nhận cấu trúc UI đã map qua demo: `C-ORD-16(c)` · `C-ACT-04(c)` · `C-HOME-04(3)` · `C-TS-03(c)` · `C-DLV-05(d)` · `C-DLV-06` · `C-DLV-08`. Chi tiết từng dòng: `<module>/CHANGELOG.md §1` dòng 2026-09-17 (bản ghi mới nhất trong ngày) + `CL-hoi-BA-v1.1.xlsx`.
> 🟢 **Cập nhật 2026-09-17 (vòng cuối) — BA trả lời 3 điểm treo còn lại (QC GiangDC2 chuyển lời).** ✅ `C-DLV-07` (*"không chỉ gởi remind thôi nhé"* = **"Không, chỉ gửi remind thôi"** — mọi mốc 2h/4h/cuối ngày/24h chỉ **gửi thông báo nhắc**, đơn KHÔNG đổi trạng thái/nhãn/cờ) · ✅ `C-HOME-04` (*"giữ nguyên nhé"* — chuỗi empty state `EMP-01`/`EMP-04` **giữ nguyên chữ PRD** dù tin load toàn quốc) · 🟡 `C-DLV-08` câu (d) đóng theo *"phase này các chỗ liên quan đến role admin chưa làm nhé"*. ⇒ **`cl_open` = 0 ở CẢ 11/11 module** — **hết CL Open trong toàn bộ v1.1**. 🔑 **Kết luận scope mới, áp cho mọi module:** mọi bề mặt **role admin** (*"chuyển admin hỗ trợ"* ở `AC-23.2.01`/`BR08-06`/`BR09-04`, hạn giữ hàng tại quầy 4h/24h) là **OUT OF SCOPE v1.1** — không viết assert, **không log bug** khi không thấy. Đã sửa: `SC-DLV-024` (v1.0) · `SC-DLV-039/045/048/054` · `SC-HOME-019/025` · `SC-FEED-013` + `TC-FEED-013`. **CL duy nhất chưa đóng: `C-DLV-08` (a)(b)** — cờ "không liên lạc được" + `NTF-05`⟷`NTF-11` khi chọn quầy trực tiếp — **KHÔNG hỏi BA nữa**, QA tự xác minh bằng **vibe-check block LỊCH SỬ** (BA đã chỉ chỗ ở vòng 3). **10/11 module HẾT điểm hỏi BA** (thêm `HOME`; chỉ `DLV` còn 1 việc tự làm).
> ⛔ **DÒNG NÀY LỖI THỜI (bản 2026-09-17 trưa) — đừng trích; số hiện hành ở dòng ℹ️ cuối §2.** ~~Đối chiếu máy đếm được: Σ`cl` = **66** · Σ`cl_open` = **0** · Σ`cl_resolved` = **65**~~ ⇒ đúng **1 CL** không nằm trong 2 ô = `C-DLV-08` (Partially). ⚠️ Các con số kể-lại ở 2 dòng 🟢 phía trên (*"58 Resolved · 7 Partially · 1 Open"* và danh sách 7 CL Partial) **đã lỗi thời**: `C-DLV-05`/`C-DLV-06` ĐÓNG HẲN 2026-09-17, `C-HOME-04`/`C-DLV-07` đóng ở lượt này. Cần con số chính xác theo từng trạng thái ⇒ chạy `/health-check` để đếm lại, **đừng trích 2 dòng đó**.
> 🔴 **Cập nhật 2026-09-17 (chiều muộn) — MỞ LẠI 1 điểm hỏi BA: `C-ORD-18`.** ⛔ *Trạng thái này đã HẾT HIỆU LỰC cùng ngày — `C-ORD-18` **Resolved** tối 2026-09-17, xem dòng ✅ ngay dưới; giữ lại đây làm hồ sơ vì sao CL được mở.* QC cung cấp ảnh UI thật wizard **Bước 1/3 "Thông tin hàng"** (`00_input/v1.1/design/gia tri hang uoc tinh.png`, demo ⇒ `DOC-v1.1-03`); đối chiếu `DOC-v1.1-01 §8.1.4` phát hiện **4 điểm lệch**: (1) 🔴 "GIÁ TRỊ HÀNG (ƯỚC TÍNH)" có **mốc tiền** `Dưới 1 triệu đ` / `1 – 5 triệu đ` / `Trên 5 triệu đ` — **không nguồn nào từng có con số này** (⚠️ KHÔNG lẫn `C-ORD-02` ngưỡng cấu hình + bảo hiểm, vẫn out of scope: đây chỉ là nhãn phụ của 3 mức định tính) · (2) nhãn UI **"TRỌNG LƯỢNG"** ⟷ PRD **"Khối lượng"**, option thêm *Nhẹ/Trung bình/Nặng* · (3) kiểu control **3 chip** ⟷ PRD **Dropdown** · (4) block **Ghi chú nằm trên cùng**, trước "Thông tin hàng". ⇒ `ORD` `cl` 15→**16**, `cl_open` 0→**1**; **10/11 module hết điểm hỏi BA**. ✅ Đồng thời ảnh **xác nhận** khối "ẢNH HÀNG \*" đã có dấu `*` + bộ đếm **"0/5"** + helper ≥1/≤5 ⇒ `BR01-01`/`BR18-02` **đã build ở tầng UI**, thu hẹp `RISK-ORD-09` (chỉ còn verify hành vi chặn thật). ⚠️ Nút "Tiếp theo" trên ảnh vẫn cam khi chưa chọn gì — nghi **giới hạn ảnh tĩnh**, ⛔ chưa kết luận, **không log bug**. Chi tiết: `v1.1/ORD-dang-tin/risk_assessment.md` mục `C-ORD-18`.
> ✅ **Cập nhật 2026-09-17 (tối, lượt cuối) — `C-ORD-18` Resolved ⇒ HẾT CL Open trong TOÀN BỘ v1.1.** BA trả lời đủ 4 câu: (a) 3 mốc tiền `Dưới 1 triệu đ`/`1 – 5 triệu đ`/`Trên 5 triệu đ` là **con số chính thức** (b) nhãn chuẩn **"Trọng lượng"**, **giữ** nhãn phụ Nhẹ/Trung bình/Nặng (c) ***"lấy UI làm chuẩn"*** ⇒ 3 trường Bước 1/3 là **chip**, PRD ghi Dropdown là sai (d) block Ghi chú đặt trên "Thông tin hàng" là **đúng thiết kế**, là **textbox nhập được**.
> 🔑 **Kết luận scope mới:** với 3 trường Bước 1/3 wizard đăng tin, **UI là nguồn chốt, ⛔ KHÔNG phải PRD `§8.1.4`** — 3 điểm của PRD hết hiệu lực (nhãn "Khối lượng" · kiểu Dropdown · thiếu mốc tiền). App hiện theo PRD ⇒ **defect UI**. Đã sửa: `ORD/risk_assessment.md` (`C-ORD-18` Resolved + ràng buộc) · `ORD/CHANGELOG.md` (§1 · §2 Kết luận bị đảo · §3) · `ORD/test_scenario_map.md` (`SC-ORD-052/053` bỏ rào ghi-nhận → **assert cứng**).
> ℹ️ **Số liệu CL sau lượt này (đếm lại từ `counts:` của 11 module):** Σ`cl` = **67** · Σ`cl_open` = **0** · Σ`cl_resolved` = **66** ⇒ đúng **1 CL** Partially = `C-DLV-08`. **11/11 module hết điểm hỏi BA.**
>
> 🟡 **Cập nhật 2026-09-18 — MỞ LẠI 1 CL: `C-USR-07`. Σ`cl` = 68 · Σ`cl_open` = 1 · Σ`cl_resolved` = 66 · 1 Partially (`C-DLV-08`).** ⇒ Câu *"hết CL Open trong TOÀN BỘ v1.1"* ở 2 dòng ngay trên **hết hiệu lực từ 2026-09-18**; nay là **10/11 module** hết điểm hỏi BA (`USR` có lại 1 điểm).
> **Vì sao mở lại:** `C-USR-07` chính là **câu (v) của `C-USR-05`** (*"địa chỉ mặc định còn cho bỏ trống không — PRD ghi Không bắt buộc?"*) — **BA chưa bao giờ trả lời thẳng câu này**, nhưng `C-USR-05` vẫn bị đóng `Resolved` ở lượt 5 (2026-09-16) ⇒ câu hỏi **rơi mất**. `vibe-test VR-003` (2026-09-18) làm nó nổi lại bằng **dữ kiện thực nghiệm**: lưu hồ sơ **2 lần liên tiếp với ô địa chỉ để TRỐNG**, app **cho lưu cả 2 lần**, không chặn, không báo lỗi.
> 🔬 **Bài học rút ra (đáng ghi hơn chính cái CL):** đóng một CL **gộp nhiều câu hỏi con** (`C-USR-05` có tới 6 câu (i)–(vi) qua 5 lượt hỏi) thì rất dễ **đóng nhầm cả câu chưa được trả lời** — không có gì trong quy trình bắt phải đối chiếu từng câu con trước khi set `Resolved`. Lượt `analyze-requirements` sau nên **tách CL nhiều câu thành CL con** hoặc thêm phép kiểm *"mọi câu (a)(b)(c)… đều có câu trả lời trích dẫn được"* trước khi đóng.
> 🔴 **Ngược lại, câu (vi) thì ĐÓNG ĐƯỢC 2026-09-18 (QC GiangDC2):** *"địa chỉ data hris luôn luôn có nhé, nếu mặc định, hiện tại ko có do bị bug không load data từ hris ấy"* ⇒ nhánh *"HRIS không có địa chỉ làm việc"* **không tồn tại**, và ô địa chỉ rỗng quan sát được ở `VR-001`/`VR-003` là **triệu chứng của `BUG-008`**, không phải nhánh dữ liệu. ⇒ `SC-USR-022`/`SC-USR-023` (*"prefill từ HRIS"*) **được xác nhận ĐÚNG** — ⛔ **không** sửa 2 SC này theo hành vi app. Chi tiết: `USR-tai-khoan/risk_assessment.md §C-USR-05 ↳ Rule địa chỉ mặc định`.
> ℹ️ **2 việc QA còn treo — tự làm, KHÔNG hỏi BA:** vibe-check block LỊCH SỬ (`C-DLV-08` (a)(b)) · vibe-check bấm thật wizard Bước 1 (nút "Tiếp theo" cam khi chưa chọn gì — nghi giới hạn ảnh tĩnh, gộp luôn với verify hành vi chặn ảnh bắt buộc của `RISK-ORD-09`).
> ⚠️ **SC ngoài `id_range` bị chạm:** `SC-ORD-008/009/010/011` (CARRIED, nội dung ở `../v1.0/ORD-dang-tin/`) nay assert mạnh hơn nhờ mốc tiền chính thức + vị trí block Ghi chú — ghi nợ ở `ORD/CHANGELOG.md §3`, ⛔ KHÔNG sửa file v1.0.
> ⛔ **0 BLOCKER chặn execute.** Nguồn câu hỏi gửi BA: `v1.1/CL-hoi-BA-v1.1.xlsx` (bản dẫn xuất từ CL section các module).
> **BA trả lời 13 CL ngày 2026-09-16 → 10 Resolved:** `C-ORD-09` (nhãn "Tài liệu") · `C-ACT-02` (nhãn tab theo app) · `C-ACT-01` (+ nhánh "chưa tặng quà → Tặng quà") · `C-ASN-03` · `C-NTF-02` (**không có trần/ngày** — "5 thông báo / 1 tin OFFER") · `C-CNL-03` (không có tool admin) · `C-DLV-02` (không có GPS) · `C-NTF-03` (mark-all) · `C-GIFT-02` (lỗi demo) · `C-FEED-01` (**có bản đồ thật**). **3 Partially:** `C-ORD-04` · `C-ORD-13` · `C-USR-05`.
> **Mở mới 25 (2026-09-16):** ORD `14..17` · ACT `03/04` · USR `06` · ASN `04..06` · DLV `05..08` · NTF `04/05` · GIFT `04` · HOME `04..06` · TS `02/03` · FEED `02..04`. **Kết luận bị đảo:** trần thông báo khớp (đảo lần 2) · `SC-FEED-009` (placeholder → bản đồ thật) · ràng buộc *"không dùng nhãn Tài liệu"* · `KB-ORD-07` #5 (Chi tiết tin → Theo dõi đơn).
> 🔴 **Nợ chặn `generate-tc` v1.1** (cập nhật 2026-09-16) — không phải blocker execute, nhưng chạy TC trước khi xong sẽ FAIL/BLOCKED hàng loạt vì lý do không phải bug:
> | Nợ | Module | Ảnh hưởng |
> |---|---|---|
> | `C-ORD-04` vòng 2 — chip "Thuốc/Y tế" đã chốt **không chặn**; còn banner hàng cấm + nội dung điều khoản | ORD | `SC-ORD-031..035` phần banner/điều khoản vẫn ghi nhận |
> | `C-ORD-13` vòng 2 — nguồn đã rõ (**HRIS**, chỉ nhân sự đang làm việc); còn **email mẫu 3 loại** + tên miền | ORD | 3 SC (1 **P1**) `BLOCKED` nếu thiếu — không tự chế được email mẫu |
> | `C-ASN-05` — "trùng điểm lấy/giao" với địa chỉ văn bản tự do chưa có phép so | ASN | Không dựng được data 4 nhánh `SC-ASN-011` |
> | ~~`C-HOME-05`~~ ✅ Resolved 2026-09-17 · `C-DLV-06` · `C-USR-06` — SC trong dự án đang cho kết luận **ngược nhau** (~~`SC-HOME-010`⟷`026`~~ · `SC-DLV-043`⟷`AC-16/17` · ~~`SC-USR-007`⟷`BR14-03`~~ ✅ `C-USR-06` Resolved 2026-09-16 — badge không hiện) | HOME · DLV · USR | Viết TC theo 1 chiều ⇒ FAIL oan hoặc PASS giả |
> | `C-FEED-05` (mới 2026-09-17) — file toạ độ văn phòng: 399 `MISSING`, 61 thiếu lat/lng, 34 ngoài VN | FEED | Không dựng được Given bản đồ thật `SC-FEED-009` |
> | `C-ACT-03`/`C-ACT-04` — đích tap card + 12 trạng thái chia 2 tab + đơn Đã huỷ ẩn/hiện | ACT | Nằm trong Steps của `SC-ACT-004/005/007/009/010/015` |
> | `RISK-DLV-08` + `RISK-DLV-11` — luồng submit form 4 đối tượng nhận & ảnh lúc lấy hàng chưa verify end-to-end | DLV | Kéo theo `GIFT` (`SC-GIFT-013/014`) và `ACT` (`SC-ACT-015`) vì cùng cần đơn `RETURNED` |
> | `RISK-ORD-09` — app đã siết **ảnh bắt buộc ≥1** chưa | ORD | `SC-ORD-054` là **P1 chặn luồng chính**; chưa siết ⇒ FAIL vì *"app chưa cập nhật"* |
> ✅ **2 câu hỏi nhãn UI đã chốt 2026-09-16** — `C-ORD-09` theo **PRD** ("Tài liệu"; app khác = defect) và `C-ACT-02` theo **app** ("Đơn của tôi" · "Đang diễn ra"/"Đã hoàn thành" · nav "Hoạt động"; PRD chưa cập nhật). ⚠️ BA quyết **từng nhãn**, không có luật chung "PRD thắng" hay "app thắng".

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
