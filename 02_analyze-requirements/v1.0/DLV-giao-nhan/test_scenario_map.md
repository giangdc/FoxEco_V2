---
id: v1.0/DLV-giao-nhan/scenario-map
title: Test Scenario Map — v1.0 · Module DLV
type: scenario-map
version: v1.0
sprint: 1
module: DLV
counts:
  req: 16
  sc: 30
  new: 30
  modified: 0
  carried: 0
  deprecated: 0
  p1: 4
  p2: 25
  p3: 1
  req_without_sc: 4
status: ANALYZED
updated: 2026-09-14
---

# Test Scenario Map — v1.0 · Module DLV

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module DLV.
> ⚠️ `req_without_sc: 4` — **gap SC có chủ đích** (`REQ-DLV-011/012/013/014`): duplicate hoặc nhánh phụ PM chưa chốt scope ⇒ ghi ở `CHANGELOG §3`, ⛔ không tạo SC rác.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Fan-out **mỗi role · mỗi state-transition** · lớp EP · boundary · nhánh lỗi = 1 SC.
> ⭐ **Fan-out lớn nhất dự án nằm ở đây:** ma trận nhãn nút `5 trạng thái × 3 vai trò` = **15 SC** (`SC-DLV-001..015`). Mỗi ô là 1 tiền đề dữ liệu riêng (1 trạng thái đơn × 1 tài khoản vai) ⇒ ⛔ không gộp theo trạng thái.
> Trần: display-only/Phase-2/duplicate → `CHANGELOG §3` (chưa chạy `--sweep` nên chưa có `coverage-gap-report.md`).

## Tổng quan
- Tổng số scenarios: **30** (NEW: 30, MODIFIED: 0, CARRIED: 0, DEPRECATED: 0)
- Phân bổ priority: P1: 5 | P2: 22 | P3: 3
- Đợt v1.0 cũ: `DLV` chỉ có **14 SC cho toàn module** trong khi ma trận `KB-DLV-01` đã có **15 ô** ⇒ đây là module thiếu SC rõ rệt nhất.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### DLV — Giao nhận & Theo dõi đơn

#### Nhóm A — Ma trận nhãn nút × 5 trạng thái × 3 vai trò (`SC-DLV-001..015`)

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-DLV-001 | Chờ ghép — Sender | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 1·Sender) · DOC-v1.0-04 dc8cf987… | Đơn ở "Chờ ghép"; đăng nhập bằng tài khoản **Người gửi** | Mở màn Theo dõi đơn | Nhãn "Đang chờ người vận chuyển nhận đơn" — **disable**; có thêm nút "Chỉnh sửa" và "Huỷ đơn" | P2 | UI | NEW |
| SC-DLV-002 | Chờ ghép — Carrier | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 1·Carrier) | Đơn ở "Chờ ghép"; tài khoản **Carrier** chưa ghép đơn nào | Mở Chi tiết tin của đơn đó | Nút "Tôi mang giúp được" — **enable** (⚠ ô này ở màn **Chi tiết tin**, không phải Theo dõi đơn) | P2 | UI | NEW |
| SC-DLV-003 | Chờ ghép — Receiver | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 1·Receiver) | Đơn ở "Chờ ghép"; tài khoản **Người nhận** được khai trong đơn | Mở màn Theo dõi đơn | Nhãn "Đang chờ người vận chuyển nhận đơn" — **disable**; có thêm nút "Huỷ đơn" | P2 | UI | NEW |
| SC-DLV-004 | Đã ghép — Sender | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 2·Sender) | Đơn ở "Đã ghép" (stepper hiển thị "Lấy hàng"); tài khoản **Người gửi** | Mở màn Theo dõi đơn | Nhãn "Đã ghép · chờ shipper lấy hàng" — **disable**; có nút "Huỷ đơn"; ⛔ KHÔNG còn nút "Chỉnh sửa" | P2 | UI | NEW |
| SC-DLV-005 | Đã ghép — Carrier | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 2·Carrier) · DOC-v1.0-04 2e2ff7bc… | Đơn ở "Đã ghép"; tài khoản **Carrier** của đơn | Mở màn Theo dõi đơn | Nút "✓ Tôi đã lấy hàng" — **enable**; có thêm nút "✕ Huỷ nhận đơn" | P2 | UI | NEW |
| SC-DLV-006 | Đã ghép — Receiver | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 2·Receiver) | Đơn ở "Đã ghép"; tài khoản **Người nhận** | Mở màn Theo dõi đơn | Nhãn "Đã có người vận chuyển · chờ lấy hàng" — **disable**; có nút "Huỷ đơn" | P2 | UI | NEW |
| SC-DLV-007 | Đang giao — Sender | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 3·Sender) · DOC-v1.0-04 c8cae4c3… | Đơn ở "Đang giao"; tài khoản **Người gửi** | Mở màn Theo dõi đơn | Nhãn "Đang giao đến người nhận" — **disable**; ⛔ KHÔNG còn nút "Huỷ đơn" | P2 | UI | NEW |
| SC-DLV-008 | Đang giao — Carrier | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 3·Carrier) | Đơn ở "Đang giao"; tài khoản **Carrier** | Mở màn Theo dõi đơn | Nút "Đã giao cho người nhận" — **enable** | P2 | UI | NEW |
| SC-DLV-009 | Đang giao — Receiver | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 3·Receiver) · DOC-v1.0-04 ca5e7239… | Đơn ở "Đang giao"; tài khoản **Người nhận** | Mở màn Theo dõi đơn | Nhãn "✓ Đơn đang trên đường đến bạn" — **disable** | P2 | UI | NEW |
| SC-DLV-010 | Đã giao — Sender | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 4·Sender) · DOC-v1.0-04 8563adc1… | Đơn ở "Đã giao"; tài khoản **Người gửi** | Mở màn Theo dõi đơn | Nhãn "✓ Đã giao · chờ người nhận xác nhận" — **disable** | P2 | UI | NEW |
| SC-DLV-011 | Đã giao — Carrier | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 4·Carrier) · DOC-v1.0-02 §4.3 | Đơn ở "Đã giao"; tài khoản **Carrier** | Mở màn Theo dõi đơn | Nhãn "✓ Đã giao · chờ người nhận xác nhận" — **disable** (quyền chốt đơn đã chuyển sang Người nhận) | P2 | UI | NEW |
| SC-DLV-012 | Đã giao — Receiver | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 4·Receiver) · DOC-v1.0-02 §5.2 | Đơn ở "Đã giao"; tài khoản **Người nhận** | Mở màn Theo dõi đơn | Nút "Xác nhận đã nhận hàng" — **enable (duy nhất trong 3 vai)** | P1 | UI | NEW |
| SC-DLV-013 | Hoàn thành — Sender | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 5·Sender) · DOC-v1.0-04 19490aa9… | Đơn ở "Hoàn thành", Sender **chưa** gửi quà | Mở màn Theo dõi đơn | Nút "✓ Cảm ơn người vận chuyển" — **enable** | P2 | UI | NEW |
| SC-DLV-014 | Hoàn thành — Carrier | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 5·Carrier) · DOC-v1.0-04 2658b17b… | Đơn ở "Hoàn thành"; tài khoản **Carrier** | Mở màn Theo dõi đơn | Nhãn "✓ Đơn đã hoàn thành ✓" — **disable** | P2 | UI | NEW |
| SC-DLV-015 | Hoàn thành — Receiver | REQ-DLV-002 | KP-01 §5.1 KB-DLV-01 (ô 5·Receiver) · DOC-v1.0-04 76e115a2… | Đơn ở "Hoàn thành"; tài khoản **Người nhận** | Mở màn Theo dõi đơn | Nhãn "Đơn đã hoàn thành ✓" — **disable** | P2 | UI | NEW |

#### Nhóm B — Trạng thái, popup, quyền hạn, liên hệ (`SC-DLV-016..030`)

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-DLV-016 | Thanh 5 mốc trạng thái | REQ-DLV-001 | DOC-v1.0-01 §D1b US-D09 L178 · §D2 L232 · DOC-v1.0-02 §3.6 | Đơn ở 1 trong 5 trạng thái | Mở màn Theo dõi đơn, đối chiếu thanh trạng thái | Thanh có đủ 5 mốc đúng thứ tự "Chờ ghép → Lấy hàng → Đang giao → Đã giao → Hoàn thành"; mốc hiện tại được tô đúng | P2 | UI | NEW |
| SC-DLV-017 | Popup "Tôi đã lấy hàng" | REQ-DLV-003 | KP-01 §5.1 (bảng popup) | Đơn "Đã ghép"; tài khoản Carrier | Bấm "✓ Tôi đã lấy hàng" | Popup title "Xác nhận" + nội dung "Bạn xác nhận đã lấy hàng từ người gửi và bắt đầu giao?" + 2 nút Huỷ/Xác nhận; bấm Xác nhận → đơn sang "Đang giao" | P2 | Functional | NEW |
| SC-DLV-018 | Popup "Đã giao cho người nhận" | REQ-DLV-003 | KP-01 §5.1 (bảng popup) | Đơn "Đang giao"; tài khoản Carrier | Bấm "Đã giao cho người nhận" | Popup "Xác nhận" + nội dung "Bạn xác nhận đã giao hàng tận tay người nhận?"; bấm Xác nhận → đơn sang "Đã giao" | P2 | Functional | NEW |
| SC-DLV-019 | Popup "Xác nhận đã nhận hàng" | REQ-DLV-003 | KP-01 §5.1 (bảng popup) · KP-01 §5 KB-DLV-03 | Đơn "Đã giao"; tài khoản Người nhận | Bấm "Xác nhận đã nhận hàng" | Popup "Xác nhận" + nội dung "Bạn xác nhận đã nhận được hàng từ người vận chuyển?"; bấm Xác nhận → đơn sang "Hoàn thành" | P2 | Functional | NEW |
| SC-DLV-020 | Huỷ ở popup xác nhận | REQ-DLV-003 | DOC-v1.0-02 §6 L191 · KP-01 §5.1 | Đang mở popup xác nhận của 1 trong 3 hành động trên | Bấm "Huỷ" | Đơn **KHÔNG** đổi trạng thái; không ghi mốc lịch sử mới | P2 | Business Rule | NEW |
| SC-DLV-021 | Không nhảy bước lấy hàng | REQ-DLV-004 | DOC-v1.0-01 §D1b US-D09 L178 | Đơn ở "Đã ghép" (Carrier chưa bấm "Tôi đã lấy hàng") | Rà mọi bề mặt của Carrier tìm đường bấm "Đã giao" | KHÔNG có đường nào chuyển đơn sang "Đã giao" trước khi qua "Tôi đã lấy hàng" | P1 | Business Rule | NEW |
| SC-DLV-022 | Chỉ Receiver chốt đơn | REQ-DLV-005 | DOC-v1.0-01 §A5 BR-INT-03 L79 · §D1b US-D21 L197 · DOC-v1.0-02 §5.2 | Đơn ở "Đã giao"; có sẵn 3 tài khoản 3 vai | Lần lượt mở màn Theo dõi đơn bằng Sender, Carrier, Receiver | Chỉ Receiver có nút "Xác nhận đã nhận hàng" **enable**; Sender và Carrier chỉ thấy nhãn disabled (⚠ `DLV-03` ghi "RECEIVER/SENDER" — theo `C-DLV-01`: **Receiver-only**) | P1 | Business Rule | NEW |
| SC-DLV-023 | Hoàn thành ngay sau xác nhận | REQ-DLV-006 | DOC-v1.0-02 §5.2 dòng "Sau khi xác nhận" | Receiver vừa xác nhận đã nhận hàng | Quan sát trạng thái đơn ngay sau khi popup đóng | Đơn chuyển "Hoàn thành" **NGAY LẬP TỨC**, không có bước chờ/duyệt nào; ⛔ KHÔNG assert chuỗi "đã đánh giá" (UI leftover) | P1 | Functional | NEW |
| SC-DLV-024 | Nhắc 2 giờ *(vế "→ admin" out of scope v1.1)* | REQ-DLV-007 | DOC-v1.0-01 §D4 BR-CNF-04 L266 · §D1b US-D14 L193 · BA `C-DLV-07` 2026-09-17 | Đơn ở "Đã giao"; Receiver KHÔNG xác nhận | Chờ quá 2 giờ, rồi chờ thêm 2 giờ (hoặc nhờ dev seed timestamp) | Sau 2 giờ: hệ thống **gửi thông báo nhắc** cho Receiver (ghi nhận kênh + nguyên văn — BA không đặc tả). Sau 4 giờ: đơn **KHÔNG tự chuyển "Hoàn thành"**, KHÔNG đổi nhãn/cờ. ⛔ Vế **"chuyển sang admin hỗ trợ" OUT OF SCOPE v1.1** — role admin chưa build phase này (`C-DLV-07` Resolved 2026-09-17, BA: *chỉ gửi remind*) ⇒ **không assert, không log bug**. ⚠ Nếu chưa chạy đủ mốc thời gian → GHI RÕ, ⛔ không khai coverage | P2 | Business Rule | NEW |
| SC-DLV-025 | [GAP] Modal đơn giản, không form đầy đủ | REQ-DLV-008 | DOC-v1.0-02 §5.3 · §7 dòng 11 · KP-01 §5 KB-DLV-03 | Đơn ở "Đã giao"; tài khoản Người nhận | Bấm "Xác nhận đã nhận hàng" và quan sát toàn bộ màn/modal | Dùng **modal đơn giản** (title "Xác nhận" + 1 câu + 2 nút); ⛔ KHÔNG có ảnh bằng chứng, KHÔNG có điểm uy tín carrier (C-DLV-03: form đầy đủ không áp dụng v1.0) | P2 | Business Rule | NEW |
| SC-DLV-026 | Liên hệ — vai Sender | REQ-DLV-009 | DOC-v1.0-02 §3.6 dòng "Liên hệ Người vận chuyển" | Đơn đã "Đã ghép"; tài khoản Người gửi | Mở màn Theo dõi đơn, xem cụm liên hệ | Hiện cụm "Người vận chuyển": tên + SĐT + nút "Gọi"; cụm này KHÔNG hiện trước khi ghép | P2 | Business Rule | NEW |
| SC-DLV-027 | Liên hệ — vai Carrier (2 đầu) | REQ-DLV-009 | DOC-v1.0-02 §4.3 dòng "Liên hệ 2 phía" · DOC-v1.0-01 §D1b US-D08 L177 | Đơn đã "Đã ghép"; tài khoản Carrier | Mở màn Theo dõi đơn, xem cụm liên hệ | Hiện **cả 2 cụm** "NGƯỜI GỬI" và "NGƯỜI NHẬN", mỗi cụm có tên + SĐT + nút "Gọi" | P2 | Business Rule | NEW |
| SC-DLV-028 | Liên hệ — vai Receiver | REQ-DLV-009 | DOC-v1.0-02 §5.2 dòng "Liên hệ" | Đơn đã "Đã ghép"; tài khoản Người nhận | Mở màn Theo dõi đơn, xem cụm liên hệ | Chỉ hiện cụm "NGƯỜI GIAO HÀNG" (tên carrier + SĐT + Gọi); **KHÔNG** hiện thông tin Người gửi | P2 | Business Rule | NEW |
| SC-DLV-029 | Lịch sử timeline mốc sự kiện | REQ-DLV-010 | DOC-v1.0-02 §3.6 dòng "Lịch sử" · DOC-v1.0-01 §D1b US-D09 L178 | Đơn đã đi qua các mốc tới "Hoàn thành" | Mở màn Theo dõi đơn, xem block "Lịch sử" | Timeline có đủ mốc "Đăng tin → Ghép thành công → Lấy hàng → Đã giao → Hoàn thành", **mỗi mốc kèm timestamp** | P2 | Functional | NEW |
| SC-DLV-030 | Nhãn phụ theo vai trò | REQ-DLV-016 | DOC-v1.0-02 §3.6 · §4.3 · §5.2 (tiêu đề section) | Cùng 1 đơn đã ghép, mở bằng 3 tài khoản 3 vai | Mở màn Theo dõi đơn bằng từng vai | Nhãn phụ đúng theo vai: Sender = "Tôi gửi hàng" · Carrier = "Tôi giao hàng" · Receiver = "Tôi nhận hàng" | P3 | UI | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-DLV-001 / SC-DLV-002 / SC-DLV-003 / SC-DLV-004 / SC-DLV-005 / SC-DLV-006 / SC-DLV-007 / SC-DLV-008 / SC-DLV-009 / SC-DLV-010 / SC-DLV-011 / SC-DLV-012 / SC-DLV-013 / SC-DLV-014 / SC-DLV-015 — Ma trận nhãn nút × 5 trạng thái × 3 vai trò

**Source Quote:** *(trích 5 hàng trạng thái — quote đầy đủ ở `requirement_traceability.md §2 REQ-DLV-002`)*
> "| 4 | **Đã giao** | `✓ Đã giao · chờ người nhận xác nhận` — disable | `✓ Đã giao · chờ người nhận xác nhận` — disable | `Xác nhận đã nhận hàng` — **enable (duy nhất)** |"
> "| 5 | **Hoàn thành** | `✓ Cảm ơn người vận chuyển` — enable<br>→ sau khi gửi quà đổi thành `Bạn đã đánh giá` (disable) | `✓ Đơn đã hoàn thành ✓` — disable | `Đơn đã hoàn thành ✓` — disable |"

**Source Location:** `DOC-v1.0-06 KP-01 §5.1 "KB-DLV-01 — MA TRẬN NHÃN NÚT × TRẠNG THÁI × VAI TRÒ" · bảng 5 hàng × 3 cột vai` + `DOC-v1.0-04` (15 ô, mỗi ô 1–3 ảnh xác nhận)

**Analyst Note:** ⭐ Nguồn ghi rõ đây là *"mục giá trị nhất của cả bộ pack — hoàn toàn không có trong BRD/PRD/demo docx, do QA cung cấp từ testing trực tiếp rồi **đối chiếu xác nhận độc lập từng ô qua ảnh Figma**"* ⇒ đủ 2 nguồn theo `§Custom Rules §10.1`, assert được **cả nhãn text và trạng thái enable/disable**. **1 ô = 1 SC** vì mỗi ô là 1 tiền đề riêng (1 trạng thái đơn × 1 tài khoản vai) — gộp theo trạng thái sẽ làm FAIL không chỉ ra được vai nào sai nhãn. ⚠️ **Hai ngoại lệ trong ma trận:** (a) ô 1·Carrier nằm ở màn **Chi tiết tin**, không phải Theo dõi đơn (`SC-DLV-002` ghi rõ trong Given); (b) ô 5·Sender có **2 trạng thái** (trước/sau khi gửi quà) — nhánh sau khi gửi quà thuộc `GIFT` (`SC-GIFT-005`). ⚠️ Ma trận ⛔ **KHÔNG áp cho màn Chi tiết tin public** — nơi đó có bug role-aware riêng (`SC-FEED-011`).

##### SC-DLV-016 — Thanh 5 mốc trạng thái

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-DLV-001`)*

**Source Location:** `DOC-v1.0-01 §D1b · US-D09 · Acceptance Criteria · L178` (đồng thuận `DOC-v1.0-02 §3.6 · dòng "Thanh 5 bước trạng thái"`)

**Analyst Note:** ⚠️ **Bẫy thuật ngữ:** mốc thứ 2 là *"Lấy hàng"* nhưng badge/trạng thái backend là *"Đã ghép" (`MATCHED`)* — cùng một trạng thái, 2 chữ (`KP-01` §5.1 ghi rõ). Then vì thế assert **tên mốc theo thanh trạng thái**, ⛔ không đòi badge cùng chữ. Cross-ref `SC-HOME-014` (thanh progress ở Trang chủ — cùng 5 mốc).

##### SC-DLV-017 / SC-DLV-018 / SC-DLV-019 / SC-DLV-020 — Popup xác nhận (3 nội dung + nhánh Huỷ)

**Source Quote:** *(3 nội dung popup quote đầy đủ ở `requirement_traceability.md §2 REQ-DLV-003`)*
> "**Popup xác nhận** — mọi hành động "enable" của Carrier/Receiver đều đi qua 1 popup title cố định `Xác nhận` trước khi đổi trạng thái thật (không chuyển ngay khi bấm nút nền)"
> (`DOC-v1.0-02` §6 L191): "Mọi bước chuyển trạng thái (trừ bước đăng tin ban đầu) đều đi qua modal xác nhận 2 nút (Huỷ/Xác nhận) — không có bước nào tự động trôi mà không cần người dùng bấm xác nhận."

**Source Location:** `DOC-v1.0-06 KP-01 §5.1 · bảng "Popup xác nhận"` ⟷ `DOC-v1.0-02 §6 "Tổng kết vòng đời một đơn hàng" · đoạn cuối (L191)`

**Analyst Note:** **2 nguồn đồng thuận + nguyên văn 3 popup** ⇒ assert được text. Tách 3 SC vì 3 nội dung khác nhau (nếu gộp thì FAIL không biết popup nào sai chữ). `SC-DLV-020` (nhánh Huỷ) là SC **an toàn dữ liệu**: mọi transition ở module này **không thể quay lại** sau khi xác nhận ⇒ nếu nút Huỷ vẫn đổi trạng thái thì đơn bị đẩy sai không cách nào lùi.

##### SC-DLV-021 — Không nhảy bước "Đã giao" trước "Tôi đã lấy hàng"

**Source Quote:**
> "Không thể bấm "Đã giao" trước khi "Tôi đã lấy hàng""

**Source Location:** `DOC-v1.0-01 §D1b · US-D09 · Acceptance Criteria · L178`

**Analyst Note:** Trên UI rule này đã được thể hiện bằng chính ma trận nút (ở "Đã ghép" Carrier **chỉ có** nút *"Tôi đã lấy hàng"*) ⇒ `SC-DLV-021` không phải bản sao của `SC-DLV-005`: SC đó assert **nhãn nút đúng**, SC này assert **không tồn tại đường vòng nào** (deep link, điều hướng từ màn khác, nút ẩn). P1 vì nếu nhảy được bước thì đơn "đã giao" mà chưa từng lấy hàng ⇒ timeline mất tính bằng chứng, phá cả `TS-01`.

##### SC-DLV-022 — Chỉ Receiver được chốt đơn

**Source Quote:**
> Mâu thuẫn (`DLV-03` §D3 L255): "DLV-03 | **RECEIVER/SENDER** xác nhận đã nhận | Quá N giờ chưa xác nhận → nhắc → admin hỗ trợ"
> Rule (`BR-INT-03` §A5 L79): "Hoàn thành cần **người nhận** xác nhận đã nhận hàng"
> AC (`US-D21` §D1b L197): "**chỉ Receiver mới thấy & bấm được** "Xác nhận đã nhận hàng""
> PRD (`§5.2`): "⇒ Đây là quyền hạn ĐẶC BIỆT DUY NHẤT của vai trò Người nhận: chỉ Người nhận mới có thể chốt đơn "Hoàn thành""

**Source Location:** `DOC-v1.0-01 §D3 · DLV-03 · L255` ⟷ `§A5 · BR-INT-03 · L79` ⟷ `§D1b · US-D21 · L197` ⟷ `DOC-v1.0-02 §5.2 · đoạn kết`

**Analyst Note:** ⭐ **BRD mâu thuẫn nội bộ:** `DLV-03` ghi *"RECEIVER/SENDER"*; 4 nguồn còn lại (`BR-INT-03` + `US-D21` + PRD §5.2 + **5 ảnh Figma** qua `KB-DLV-02`) chốt **Receiver-only**. `C-DLV-01` Resolved 2026-07-24 theo **Receiver-only**. SC này khác 3 ô ma trận (`SC-DLV-010/011/012`) về **góc nhìn**: 3 ô kia assert *nhãn của từng vai*, SC này assert **tính duy nhất của quyền** trong cùng một lượt so sánh 3 vai ⇒ là SC bảo vệ phán quyết `C-DLV-01`.

##### SC-DLV-023 — "Hoàn thành" ngay sau khi Receiver xác nhận

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-DLV-006`)*

**Source Location:** `DOC-v1.0-02 §5.2 · bảng Trường/Thành phần · dòng "Sau khi xác nhận"`

**Analyst Note:** ⚠️ Chuỗi *"Hoàn thành & đã đánh giá"* nhắc **"đã đánh giá"** trong khi rating 1–5 sao đã bị `C-GIFT-01` loại khỏi v1.0 ⇒ **UI leftover** cùng loại `★★★★★` ở `SC-ACT-013` ⇒ Then assert **trạng thái**, ⛔ không assert chuỗi lịch sử đó. P1 vì đây là điểm đóng đơn — nếu có bước chờ ẩn thì Sender không bao giờ tặng quà được (`GIFT` bị blocked).

##### SC-DLV-024 — Nhắc sau 2 giờ *(vế admin sau 4 giờ: out of scope v1.1)*

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-DLV-007`)*
> "quá 2 giờ không xác nhận → hệ thống nhắc, thêm 2 giờ → admin hỗ trợ"

**Source Location:** `DOC-v1.0-01 §D4 · BR-CNF-04 · L266` và `§D1b · US-D14 · L193` (đồng thuận `§D5 · L295`)

**Analyst Note:** **3 nguồn đồng thuận mốc 2 giờ** (khác `DLV-03` chỉ ghi *"Quá N giờ"*) ⇒ có oracle rõ. Nhưng **chi phí thực thi rất cao**: phải chờ 2 giờ rồi 4 giờ thật, hoặc nhờ dev seed timestamp/đổi giờ hệ thống. ⇒ Then ghi rõ: **nếu chưa chạy đủ mốc thì GHI RÕ**, ⛔ không khai coverage — đây đúng loại SC dễ bị "đánh PASS cho xong". Nhánh *"admin hỗ trợ"* chỉ verify được **hệ quả phía end-user** (Admin Portal out of scope — `C-TS-01`). **Cập nhật 2026-09-17 (BA trả lời `C-DLV-07`, home `v1.1/DLV-giao-nhan/risk_assessment.md`):** BA chốt hệ thống **CHỈ gửi remind**, và *"phase này các chỗ liên quan đến role admin chưa làm"* ⇒ nhánh *"admin hỗ trợ"* **KHÔNG có hệ quả nào quan sát được ở v1.1** — bỏ hẳn khỏi phạm vi assert, **không log bug** khi không thấy; phần còn assert được: **có thông báo nhắc** + **đơn KHÔNG tự chuyển "Hoàn thành"**.

##### SC-DLV-025 — [GAP] Modal đơn giản, không dùng form đầy đủ

**Source Quote:**
> "⚠ Lưu ý: Cần xác nhận với đội thiết kế: bản chính thức dùng form đầy đủ này (có ảnh bằng chứng) hay modal xác nhận đơn giản như ở Mục 5.2 — vì đây là 2 cách triển khai khác nhau cho CÙNG một hành động nghiệp vụ."
> Phán quyết (`KP-01` §5 KB-DLV-03): "BA/PO chốt **theo Figma = modal đơn giản**… Form đầy đủ **không áp dụng ở v1.0**."

**Source Location:** `DOC-v1.0-02 §5.3 · đoạn lưu ý cuối` (và `§7 · dòng 11`) ⟷ `DOC-v1.0-06 KP-01 §5 "KB-DLV-03"`

**Analyst Note:** `C-DLV-03` Resolved 2026-07-27: **modal đơn giản**. Then có **2 mệnh đề**: assert modal đơn giản **và** assert **không có** ảnh bằng chứng/điểm uy tín — vế phủ định quan trọng hơn, vì nếu form đầy đủ xuất hiện thì kéo theo cả `PUP-03` (ảnh) và điểm uy tín (`C-USR-01` đã defer) vào scope. Đây là lý do `REQ-DLV-012` (ảnh hàng) để **gap có chủ đích**.

##### SC-DLV-026 / SC-DLV-027 / SC-DLV-028 — Cụm liên hệ theo 3 vai

**Source Quote:**
> Sender (`DOC-v1.0-02` §3.6): "Liên hệ Người vận chuyển | Chỉ hiện sau khi ghép: tên + SĐT + nút Gọi"
> Carrier (`§4.3`): "Liên hệ 2 phía | Hiển thị cả "NGƯỜI GỬI" và "NGƯỜI NHẬN" (tên + SĐT + nút Gọi) — vai trò trung gian cần liên hệ cả 2 đầu"
> Receiver (`§5.2`): "Liên hệ | Sau khi ghép: chỉ hiện "NGƯỜI GIAO HÀNG" (tên carrier + SĐT + Gọi) — không hiện lại thông tin Người gửi"

**Source Location:** `DOC-v1.0-02 §3.6` · `§4.3` · `§5.2` — bảng Trường/Thành phần, dòng "Liên hệ" của từng vai

**Analyst Note:** 3 vai → **3 tập cụm liên hệ khác nhau** ⇒ 3 SC. Đây cũng là **mặt sau của rule bảo mật** `BR-CON-02`/`OPR-07`: mỗi vai chỉ thấy đúng SĐT cần thiết (Receiver **không** thấy Sender). ⚠️ `US-D05` (§D1b L167) nói Sender thấy *"thông tin người nhận… ở mọi trạng thái"* — **xung đột nhẹ** với `§3.6` (chỉ liệt kê cụm Carrier) ⇒ `SC-DLV-026` assert cụm Carrier (có nguồn rõ), ghi nhận thêm cụm Người nhận nếu có, ⛔ không assert.

##### SC-DLV-029 — Lịch sử timeline mốc sự kiện

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-DLV-010`)*

**Source Location:** `DOC-v1.0-02 §3.6 · bảng Trường/Thành phần · dòng "Lịch sử"`

**Analyst Note:** ⚠️ **Danh sách mốc LỊCH SỬ khác danh sách 5 mốc TRẠNG THÁI**: lịch sử bắt đầu bằng *"Đăng tin"* và có *"Ghép thành công"*, thanh trạng thái bắt đầu bằng *"Chờ ghép"* và mốc 2 là *"Lấy hàng"* ⇒ 2 danh sách, ⛔ đừng dùng lẫn (đây là lỗi dễ mắc khi viết TC completeness). ⚠️ **Rủi ro liên quan:** `C-CNL-02` ghi nhận hành vi hiện tại là **huỷ nhận đơn XOÁ LUÔN dòng "Ghép thành công"** khỏi LỊCH SỬ ⇒ nếu chạy `SC-DLV-029` sau một lượt huỷ nhận thì mốc sẽ thiếu; Given phải là **đơn đi thẳng tới Hoàn thành**.

##### SC-DLV-030 — Nhãn phụ theo vai trò

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-DLV-016`)*

**Source Location:** `DOC-v1.0-02 §3.6 · §4.3 · §5.2` — tiêu đề section (Heading 2)

**Analyst Note:** Nguồn là **3 tiêu đề section**, không phải nội dung bảng ⇒ neo bằng heading. Gộp 1 SC với 3 nhánh vai trong Then vì cùng 1 hành vi hiển thị nguyên tử (nhãn đổi theo vai). Hữu ích làm **oracle phụ** cho 15 SC ma trận: nếu nhãn phụ sai thì đang xem bằng vai khác với vai dự định ⇒ giải thích được nhiều FAIL "nhãn nút không khớp".

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| — | *(không có — v1.0 là version đầu của chuỗi phân tích mới)* | — | — | — | — |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
