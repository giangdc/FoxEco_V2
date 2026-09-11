---
id: v1.0/router
title: Router — Analyze v1.0 sprint-1
type: router
version: v1.0
sprint: 1
modules: 11
doc_source:
  - id: DOC-v1.0-01
    file: 00_input/v1.0/Doc/FoxEco BRD v3.2.md
    revision: "BRD v3.2 · cập nhật 27/07/2026 · FPT Telecom · Active (bản latest)"
    md5: 4f0b97f5ef62993c9956f0a9958d35f1
    kind: "BRD (Business Requirements Document) — nguồn nghiệp vụ chính, THẮNG khi mâu thuẫn về rule"
    modules: [USR, HOME, FEED, ORD, ACT, ASN, DLV, GIFT, CNL, NTF, TS]
  - id: DOC-v1.0-02
    file: 00_input/v1.0/Doc/tổng hợp từ file demo.docx
    revision: "PRD v1.0 (Nháp) · tái dựng từ bản demo standalone 3 vai trò · Active"
    md5: fc4ea433ebd9c2a643ca8aa0ddeed303
    kind: "KHÔNG PHẢI URD — PRD tái dựng từ demo, THẮNG khi mô tả chi tiết màn hình/field; ⛔ hành vi demo KHÔNG dùng làm oracle"
    modules: [USR, HOME, FEED, ORD, ACT, ASN, DLV, GIFT, NTF]
  - id: DOC-v1.0-03
    file: 00_input/v1.0/Design/FoxEco Demo 3 vai tro (standalone) (2).html
    revision: "prototype tương tác 3 vai trò · Active · reference-only"
    md5: db5808ac77dc27d05bf04431bbf27978
    kind: "KHÔNG PHẢI URD — prototype tương tác, reference-only (⛔ không trích làm nguồn rule)"
    modules: [FEED, ASN, DLV]
  - id: DOC-v1.0-04
    file: 00_input/v1.0/Design/Fox Eco Doc/images/ (82 ảnh)
    revision: "Figma UI design mockup · Active · nguồn thiết kế UI chi tiết nhất hiện có"
    md5: "n/a (82 file — tham chiếu bằng hash từng ảnh trong Source Location)"
    kind: "Figma UI mockup — ⚠ status bar \"9:41\" là mẫu chuẩn Apple, KHÔNG phải screenshot máy thật ⇒ đối chiếu CẤU TRÚC, không đối chiếu giá trị dữ liệu"
    modules: [USR, HOME, FEED, ORD, DLV, GIFT, NTF]
  - id: DOC-v1.0-05
    file: 00_input/v1.0/Design/Screenshot From 2026-07-27 15-23-25.png
    revision: "screenshot màn Hoạt động · Active"
    md5: cb6d5baf815c2c956e749e0ac5424f8d
    kind: "Ảnh mockup màn Hoạt động — ⚠ cùng cảnh báo status bar \"9:41\" như DOC-v1.0-04"
    modules: [ACT]
  - id: DOC-v1.0-06
    file: 00_input/v1.0/_knowledge-pack/ (KP-01, 02, 03, 05, 06, 07 + evidence/)
    revision: "Knowledge pack đóng gói 2026-09-04 từ đợt phân tích v1.0 cũ · Active"
    md5: "KP-01 7eb6a8e0… · KP-02 662b9d82… · KP-03 685c4eea… · KP-05 6e313135… · KP-06 70ee389e… · KP-07 6eda2ea7…"
    kind: "KHÔNG PHẢI URD — kiến thức nghiệp vụ NGOÀI tài liệu (BA-chat · QA-obs · Figma · vibe-test). ⛔ KHÔNG dùng làm nguồn requirement gốc; dùng cho phán quyết clarification + hành vi app thật"
    modules: [USR, HOME, FEED, ORD, ACT, ASN, DLV, GIFT, CNL, NTF, TS]
status: ANALYZED
updated: 2026-09-07
---

# Router — Analyze v1.0 sprint-1

> **File này là BẢN ĐỒ, không phải kho nội dung.** Nội dung thật nằm ở **5 file / module**; router chỉ trả lời 2 câu: *"chức năng này ở module nào"* và *"module này lớn cỡ nào, rủi ro ra sao"*.
> 📜 **Lịch sử từng lượt của mỗi module** → `<module>/CHANGELOG.md §1`. **Lịch sử router bản cũ** → `git show <commit>:<path>`.
> 🔑 **Nguồn canonical của số đếm là FILE MODULE** — xem §Luật `counts` canonical dưới. Bảng §2 là **bản dẫn xuất**: sửa số ở file module trước, rồi mới đồng bộ về đây.

## 1. Function Register

| Module | Dir | Chức năng | DOC Source | Dải REQ | Dải SC |
|---|---|---|---|---|---|
| **USR** | [`USR-tai-khoan/`](USR-tai-khoan/) | Tài khoản & Hồ sơ — màn Cá nhân (view-only), SSO qua host app FoxPro, 2 chỉ số đóng góp, badge hạng | `DOC-v1.0-01` §A6/§A7 · `DOC-v1.0-02` §3.9 | `REQ-USR-001..007` | `SC-USR-001..012` |
| **HOME** | [`HOME-trang-chu/`](HOME-trang-chu/) | Trang chủ — bottom nav 5 tab, header + chuông, banner, card "Đóng góp của bạn", section "Đơn của tôi" (role-aware), section "Tin mới" | `DOC-v1.0-02` §2/§3.1/§4.1/§5.1 · `DOC-v1.0-01` §D1b | `REQ-HOME-001..010` | `SC-HOME-001..024` |
| **FEED** | [`FEED-bang-tin/`](FEED-bang-tin/) | Bảng tin & Chi tiết tin — danh sách tin NEED cộng đồng, badge "Tin của bạn", chi tiết tin + CTA "Tôi mang giúp được" | `DOC-v1.0-02` §3.3/§3.4/§4.2 · `DOC-v1.0-01` §A5/§D7 | `REQ-FEED-001..009` | `SC-FEED-001..014` |
| **ORD** | [`ORD-dang-tin/`](ORD-dang-tin/) | Đăng tin & Quản lý tin — wizard NEED 3 bước, form OFFER 1 trang, validate `§D8`, sửa tin, tin hết hạn | `DOC-v1.0-01` §D3/§D4/§D8 · `DOC-v1.0-02` §3.5 | `REQ-ORD-001..022` | `SC-ORD-001..051` |
| **ACT** | [`ACT-hoat-dong/`](ACT-hoat-dong/) | Hoạt động ("Đơn của tôi") — 2 tab Đang diễn ra / Đã hoàn thành, card đơn 5 trường, rule ẩn đơn "Đã huỷ" | `DOC-v1.0-02` §3.7 · `DOC-v1.0-06` KP-01 §3 · `DOC-v1.0-05` | `REQ-ACT-001..009` | `SC-ACT-001..014` |
| **ASN** | [`ASN-ghep-noi/`](ASN-ghep-noi/) | Ghép nối — ghép ngay, lộ SĐT sau ghép, chống double-accept, auto-match tuyến OFFER↔NEED, trần gợi ý/thông báo | `DOC-v1.0-01` §A5/§D3/§D7 · `DOC-v1.0-02` §4.2 | `REQ-ASN-001..012` | `SC-ASN-001..018` |
| **DLV** | [`DLV-giao-nhan/`](DLV-giao-nhan/) | Giao nhận & Theo dõi đơn — **ma trận nhãn nút 5 trạng thái × 3 vai (15 ô)**, popup xác nhận, quyền chốt đơn của Receiver, liên hệ theo vai | `DOC-v1.0-06` KP-01 §5.1 · `DOC-v1.0-01` §D3/§D4 · `DOC-v1.0-02` §3.6/§4.3/§5.2 | `REQ-DLV-001..016` | `SC-DLV-001..030` |
| **GIFT** | [`GIFT-qua-cam-on/`](GIFT-qua-cam-on/) | Quà cảm ơn — 4 loại quà sau Hoàn thành, nút đổi nhãn "Bạn đã đánh giá", màn "Quà đã nhận" (card đếm `count>0`) | `DOC-v1.0-01` §A7/§D3/§D6 · `DOC-v1.0-02` §3.8 | `REQ-GIFT-001..008` | `SC-GIFT-001..012` |
| **CNL** | [`CNL-huy-don/`](CNL-huy-don/) | Huỷ đơn / Huỷ nhận đơn — lý do bắt buộc ≥5 ký tự, ghi vai người huỷ, log LỊCH SỬ, chặn huỷ từ "Đang giao" | `DOC-v1.0-01` §D3/§D4/§D7/§D8.3 · `DOC-v1.0-06` KP-01 §7 | `REQ-CNL-001..007` | `SC-CNL-001..013` |
| **NTF** | [`NTF-thong-bao/`](NTF-thong-bao/) | Thông báo — 9 sự kiện `NTF-01..09`, nhóm theo mốc thời gian, chấm đỏ theo item, phân trang, SĐT không vào push | `DOC-v1.0-01` §D6/§D7 · `DOC-v1.0-02` §3.2 · `DOC-v1.0-06` KP-07 | `REQ-NTF-001..011` | `SC-NTF-001..016` |
| **TS** | [`TS-trust-safety/`](TS-trust-safety/) | Trust & Safety — log tương tác đầy đủ + **bất biến (audit)**, consent điều khoản, Admin can thiệp (phần lớn ngoài bề mặt test) | `DOC-v1.0-01` §A8/§A5/§D4 · `DOC-v1.0-06` KP-01 §9 | `REQ-TS-001..005` | `SC-TS-001..007` |

> 📁 **Quy ước tên thư mục (2026-09-07):** `Dir` = `<CODE>-<slug-chức-năng>` (vd `ORD-dang-tin/`) — mã ngắn giữ nguyên để đi vào ID, phần slug chỉ để người đọc biết thư mục làm gì. **`Dir` ≠ token ID**: ID vẫn là `SC-ORD-001`, ⛔ không có `SC-ORD-dang-tin-001`. Bảng nguồn: `Project_rule.md §Module Codes` (cột `Module` = token ID · cột `Dir` = thư mục).
> ⚠️ **Bẫy tra cứu:** ID (`SC-<CODE>-<NNN>`) **không** suy ra được tên thư mục, và thư mục thường **dùng lại qua nhiều sprint** ⇒ phân biệt **BẮT BUỘC bằng dải ID** ở bảng trên (khớp `id_range` trong frontmatter `CHANGELOG.md`).
> 🔴 **Dải ID lượt này KHÔNG map 1-1 với đợt phân tích v1.0 CŨ** (`_handoff-v1.0/04_archive-project-v1.0/`). Đợt cũ dùng **8 module** (`USR ORD ASN DLV GIFT CNL NTF TS`, layout `flat`); lượt này **11 module** — 3 module mới `HOME`/`FEED`/`ACT` tách ra khỏi `ORD`/`ASN`, và dải `SC-ORD-*`, `SC-ASN-*`, `SC-NTF-*` **được đánh lại từ 001**.
> ⛔ **Ví dụ dễ nhầm nhất:** `SC-NTF-006` lượt này = *"NTF-08 — đơn bị huỷ"*; `SC-NTF-006` đợt cũ = *"trần thông báo khớp/ngày"* (đã DEPRECATED 2026-07-29). Hai nội dung khác hoàn toàn ⇒ quy chiếu **bắt buộc bằng đường dẫn sprint**.
> ⛔ Không có module nào bị gộp/xoá ở lượt này.

## 2. Module Summary

> 📐 **Bảng dẫn xuất** — sinh lại / đối chiếu bằng cách đọc `counts:` ở frontmatter từng file module:
> ```bash
> for m in 02_analyze-requirements/v1.0/*/; do
>   echo "== $(basename $m)"
>   sed -n '/^counts:/,/^status:/p' "$m/test_scenario_map.md"
>   sed -n '/^counts:/,/^status:/p' "$m/risk_assessment.md"
> done
> ```

| Module | Req | SC | NEW | MOD | CARRIED | DEPR | P1 | P2 | P3 | CL | RISK | Risk Level |
|---|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|---|
| USR | 7 | 12 | 12 | 0 | 0 | 0 | 1 | 5 | 6 | 4 | 5 | Low |
| HOME | 10 | 24 | 24 | 0 | 0 | 0 | 1 | 11 | 12 | 3 | 5 | Medium |
| FEED | 9 | 14 | 14 | 0 | 0 | 0 | 2 | 7 | 5 | 3 | 5 | **High** |
| ORD | 22 | 51 | 51 | 0 | 0 | 0 | 7 | 28 | 16 | 10 | 8 | **High** |
| ACT | 9 | 14 | 14 | 0 | 0 | 0 | 0 | 7 | 7 | 2 | 5 | Medium |
| ASN | 12 | 18 | 18 | 0 | 0 | 0 | 6 | 10 | 2 | 2 | 7 | **High** |
| DLV | 16 | 30 | 30 | 0 | 0 | 0 | 5 | 22 | 3 | 3 | 7 | **High** |
| GIFT | 8 | 12 | 12 | 0 | 0 | 0 | 0 | 6 | 6 | 3 | 5 | Low |
| CNL | 7 | 13 | 13 | 0 | 0 | 0 | 4 | 7 | 2 | 2 | 6 | Medium-High |
| NTF | 11 | 16 | 16 | 0 | 0 | 0 | 1 | 8 | 7 | 2 | 6 | Medium |
| TS | 5 | 7 | 7 | 0 | 0 | 0 | 1 | 2 | 4 | 1 | 5 | Medium |
| **Tổng** | **116** | **211** | **211** | **0** | **0** | **0** | **28** | **113** | **70** | **35** | **64** | — |

> ℹ️ **P1+P2+P3 = 28+113+70 = 211 = Tổng SC** ⇒ **không lệch cộng**: v1.0 là version đầu của chuỗi phân tích mới nên **0 DEPRECATED**, và mọi SC đều được gán Priority (kể cả SC dạng `[GAP]`). Quy ước đếm ở `Project_rule.md §Quy ước đếm scenario` cho phép `P1+P2+P3 < Tổng SC` khi có DEPRECATED — lượt này chưa phát sinh.
> ℹ️ **Cột `CL` chỉ đếm clarification có HOME ở module đó** (35 CL duy nhất). CL tham chiếu chéo (vd `C-ORD-06` xuất hiện ở 5 module) **không** cộng lặp — xem bảng CL ở từng `<module>/risk_assessment.md`.
> ℹ️ **`req_without_sc` (gap SC có chủ đích):** `DLV` = 4 (`REQ-DLV-011/012/013/014`) · `CNL` = 1 (`REQ-CNL-007`) ⇒ **111/116 REQ có ≥1 SC**. Lý do từng REQ ghi ở `<module>/CHANGELOG.md §3`.
> 🔴 **CL còn OPEN — 17/35**, ⛔ **KHÔNG có BLOCKER chặn execute**. Nhóm cần ưu tiên hỏi BA (ảnh hưởng nhiều TC nhất):
> | CL | Home | Vấn đề | Vì sao ưu tiên |
> |---|---|---|---|
> | `C-ORD-09` | ORD | Danh mục "Loại hàng" — 3 nguồn 3 danh mục; app **không có** chip "Tài liệu" | ⭐ Lan rộng nhất: mọi TC nhắc "Tài liệu" đều sai chữ (lỗi #1 của đợt cũ) |
> | `C-NTF-01` | NTF | Danh sách loại thông báo chính thức (12 hàng ứng viên ở `KP-07`) | Chặn assert nội dung của toàn bộ 8 SC thông báo |
> | `C-NTF-02` | ASN | 3 tham số auto-match (khung giờ phù hợp · chu kỳ quét · ngưỡng gộp) | Chặn TC biên của điều kiện khớp tuyến |
> | `C-ORD-06` | ACT | Text empty state — **5 màn / 6 SC** | Từng bị revert `Resolved → Open` vì chốt không kèm bằng chứng |
> | `C-HOME-03` | HOME | Section "Tin mới" hiển thị **1 tin** hay **5 tin** | Chặn TC biên của nút "Xem thêm trên Bảng tin" |
> | `C-ORD-10` | ORD | Địa chỉ lấy hàng không pre-fill: **bug hay tài khoản test chưa cấu hình?** | Quyết định log bug hay sửa TC |

### 🔑 Luật `counts` canonical (v2)

Mỗi chỉ số có **đúng 1 nguồn canonical**; mọi nơi khác chỉ được **trỏ tới**, ⛔ không chép lại số:

| Chỉ số | Nguồn canonical |
|---|---|
| REQ · SC (+ NEW/MOD/CARRIED/DEPR · P1/P2/P3) | `<module>/test_scenario_map.md` — frontmatter `counts:` |
| CL · RISK | `<module>/risk_assessment.md` — frontmatter `counts:` (chỉ CL có home ở module đó) |
| Dải ID (`id_range`) | `<module>/CHANGELOG.md` — frontmatter |

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
