# Requirement Traceability — v1.0 · Module ACT

> Tạo bởi: analyze-requirements (INIT 2026-09-07) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation: FR/VR` ⇒ **Schema A**.
> ⚠️ Module này ở đợt v1.0 cũ bị gộp vào `ORD` (`SC-ORD-015..026`) — tách riêng từ 2026-09-07.
> 📌 **`risk_assessment.md` của module này là home canonical của `C-ORD-06`** (empty state) — CL dùng chung 5 màn.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module ACT — DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-05 · DOC-v1.0-06

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-ACT-001 | — (bảng §2 không đánh số) | `DOC-v1.0-02` §2 dòng "Tab Hoạt động" · §3.7 · `DOC-v1.0-06` KP-01 §3 KB-ORD-07 (#1,#2) | SC-ACT-001, SC-ACT-002, SC-ACT-003 | — |
| REQ-ACT-002 | — | `DOC-v1.0-06` KP-01 §3 KB-ORD-07 (#3) · `DOC-v1.0-05` | SC-ACT-006 | — |
| REQ-ACT-003 | — | `DOC-v1.0-02` §3.7 đoạn 2 | SC-ACT-004 | — |
| REQ-ACT-004 | `US-D04` | `DOC-v1.0-02` §3.7 đoạn 3 · `DOC-v1.0-01` §D1b L166 | SC-ACT-005 | — |
| REQ-ACT-005 | `US-D04` | `DOC-v1.0-06` KP-01 §3 KB-ORD-07 (#4,#6) · `DOC-v1.0-01` §D1b L166 | SC-ACT-008, SC-ACT-009 | — |
| REQ-ACT-006 | — | `DOC-v1.0-06` KP-01 §3 KB-ORD-07 (#5) · `DOC-v1.0-02` §3.7 đoạn 2 | SC-ACT-010, SC-ACT-011 | C-ACT-01 |
| REQ-ACT-007 | — | `DOC-v1.0-06` KP-01 §3 KB-ORD-07 (#7) | SC-ACT-007 | — |
| REQ-ACT-008 | — | `DOC-v1.0-06` KP-02 §5 dòng `C-ORD-06` | SC-ACT-012, SC-ACT-014 | C-ORD-06 |
| REQ-ACT-009 | `RAT-01/02` | `DOC-v1.0-02` §3.7 đoạn 3 · `DOC-v1.0-06` KP-01 §3 KB-ORD-07 (ghi chú) · KP-01 §6 KB-GIFT-02 | SC-ACT-013 | C-GIFT-01 |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-ACT-001 · Hai tab "Đang diễn ra" / "Đã hoàn thành" + tab mặc định
📍 `DOC-v1.0-02 §2 · dòng "Tab Hoạt động"` · `§3.7` · `DOC-v1.0-06 KP-01 §3 KB-ORD-07`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-02` §2 dòng "Tab Hoạt động":
> "Tab Hoạt động | "Đơn của tôi" — 2 tab con: Đang diễn ra / Đã hoàn thành"

> Nguồn #2 — `DOC-v1.0-06` KP-01 §3 `KB-ORD-07` (bảng, dòng 1-2):
> "| 1 | 2 tab | `Đang diễn ra` / `Đã hoàn thành` |"
> "| 2 | Tab mặc định | `Đang diễn ra` |"

↳ **Ghi chú:** **Tab mặc định** chỉ có ở `KB-ORD-07` (`QA-obs` + ảnh `DOC-v1.0-05`), không có trong BRD/PRD ⇒ đây là kiến thức ngoài tài liệu nhưng có bằng chứng ảnh. Theo `Project_rule §Custom Rules §10.2`, **mỗi tab phải có ≥1 SC riêng verify data** và **SC verify cơ chế switch tab giữ độc lập** ⇒ fan-out 3 SC ở REQ này (2 tab tồn tại · tab mặc định · cơ chế switch) và 2 SC data riêng ở `REQ-ACT-003/004`.

---

### REQ-ACT-002 · Cấu trúc card đơn (5 trường)
📍 `DOC-v1.0-06 KP-01 §3 KB-ORD-07 (dòng 3)` · `DOC-v1.0-05`  ·  Clarif: —

> "| 3 | Card (5 trường) | Icon trạng thái · Tên tin · Tuyến `Từ → Đến` · Ngày · Badge trạng thái |"

↳ **Ghi chú:** Nguồn duy nhất là `KB-ORD-07` (`QA-obs` 2026-07-27 + ảnh `DOC-v1.0-05`). ⚠️ Ảnh `DOC-v1.0-05` có status bar **"9:41"** — là **mockup chuẩn Apple, KHÔNG phải screenshot máy thật** (`KP-01` §3 ghi rõ) ⇒ dùng để đối chiếu **cấu trúc**, ⛔ không dùng để đối chiếu giá trị dữ liệu. BRD/PRD **không mô tả** card này ⇒ 1 nguồn + ảnh mockup; đủ để viết TC completeness nhưng phải vibe-test xác nhận (`§Custom Rules §10.1`).

---

### REQ-ACT-003 · Dữ liệu tab "Đang diễn ra"
📍 `DOC-v1.0-02 §3.7 · đoạn 2`  ·  Clarif: —

> "Tab "Đang diễn ra": card đơn hiện tại (nếu có) → bấm vào mở Theo dõi đơn."

↳ **Ghi chú:** Định nghĩa nhóm dữ liệu của tab bằng **cụm "đơn hiện tại"** — không liệt kê trạng thái cụ thể. Suy ra từ `DOC-v1.0-01` §D2 L232 (5 mốc) + `KB-ORD-07` (#7: đơn "Đã huỷ" không hiện): tab này chứa `Chờ ghép · Đã ghép · Đang giao · Đã giao`. ⚠️ **`Hoàn thành` thuộc tab nào** thì không nguồn nào nói tường minh — `§3.7` đoạn 3 xếp *"đơn trạng thái Hoàn thành"* vào tab "Đã hoàn thành" ⇒ ranh giới là **Đã giao → Hoàn thành**.

---

### REQ-ACT-004 · Dữ liệu tab "Đã hoàn thành" (gồm cả "Hết hạn")
📍 `DOC-v1.0-02 §3.7 · đoạn 3` · `DOC-v1.0-01 §D1b US-D04 · L166`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-02` §3.7 đoạn 3:
> "Tab "Đã hoàn thành": đơn trạng thái "Hoàn thành" (5 sao + "Đã đánh giá") hoặc "Hết hạn" (không ai nhận mang giúp trong thời gian đăng — tin tự động đóng)."

> Nguồn #2 — `US-D04` (§D1b L166):
> "hiển thị badge "Hết hạn" **ở tab hoàn tất** kèm lý do "Không có ai nhận mang giúp trong thời gian đăng""

↳ **Ghi chú:** **2 nguồn đồng thuận**: tab "Đã hoàn thành" chứa **2 nhóm** — `Hoàn thành` và `Hết hạn`. Đây là điểm dễ sai: tên tab gợi ý chỉ chứa đơn thành công, nhưng đơn **Hết hạn** (thất bại) cũng nằm đây. Phần *"(5 sao + "Đã đánh giá")"* là **UI leftover** của rating đã bị loại khỏi v1.0 ⇒ xem `REQ-ACT-009`.

---

### REQ-ACT-005 · Card "Hết hạn" — dòng lý do + không thao tác được
📍 `DOC-v1.0-06 KP-01 §3 KB-ORD-07 (dòng 4, 6)` · `DOC-v1.0-01 §D1b US-D04 · L166`  ·  Clarif: —

> Nguồn #1 — `DOC-v1.0-06` KP-01 §3 `KB-ORD-07`:
> "| 4 | Card "Hết hạn" có thêm dòng lý do | *"Không có ai nhận mang giúp trong thời gian đăng — tin đã tự động đóng."* |"
> "| 6 | Tap card "Hết hạn" | → không cho thao tác (non-clickable) |"

> Nguồn #2 — `US-D04` (§D1b L166):
> "kèm lý do "Không có ai nhận mang giúp trong thời gian đăng""

↳ **Ghi chú:** ⭐ **Hiếm gặp trong dự án này: text có nguyên văn từ 2 nguồn** ⇒ assert được. Lưu ý 2 nguồn **khác nhau ở phần cuối câu**: `KB-ORD-07` có thêm *"— tin đã tự động đóng."*, `US-D04` dừng ở *"trong thời gian đăng"* ⇒ assert theo `KB-ORD-07` (bản quan sát app, dài hơn), ghi lệch vào `CHANGELOG §2`. Rule **non-clickable** chỉ có ở `KB-ORD-07` ⇒ SC riêng (`SC-ACT-009`).

---

### REQ-ACT-006 · Tap card (≠ "Hết hạn") → mở màn tiếp
📍 `DOC-v1.0-06 KP-01 §3 KB-ORD-07 (dòng 5)` · `DOC-v1.0-02 §3.7 · đoạn 2`  ·  Clarif: `C-ACT-01`

> Nguồn A — `DOC-v1.0-06` KP-01 §3 `KB-ORD-07` dòng 5:
> "| 5 | Tap card ≠ "Hết hạn" | → mở màn "Chi tiết tin" |"

> Nguồn B — `DOC-v1.0-02` §3.7 đoạn 2:
> "Tab "Đang diễn ra": card đơn hiện tại (nếu có) → bấm vào mở **Theo dõi đơn**."

↳ **Ghi chú:** ⚠️ **2 nguồn cho 2 đích khác nhau:** `KB-ORD-07` nói mở **"Chi tiết tin"** (màn public của module `FEED`), PRD nói mở **"Theo dõi đơn"** (màn role-aware của module `DLV`). Đây là 2 màn khác nhau về bản chất (public vs theo vai) ⇒ mở `C-ACT-01`. `SC-ACT-010` assert *"mở màn tiếp của đúng đơn đó"* (không assert tên màn), `SC-ACT-011` ghi nhận đích thật. Lưu ý `HOME` có case tương tự đã rõ: chạm section "Đơn của tôi" → **Theo dõi đơn** (`SC-HOME-015`).

---

### REQ-ACT-007 · Đơn "Đã huỷ" không hiển thị ở cả 2 tab
📍 `DOC-v1.0-06 KP-01 §3 KB-ORD-07 (dòng 7)`  ·  Clarif: —

> "| 7 | Đơn trạng thái "Đã huỷ" | **KHÔNG** hiển thị ở cả 2 tab |"

↳ **Ghi chú:** Rule chỉ có ở `KB-ORD-07` (`QA-obs`), **không có trong BRD/PRD**. Là rule nghiệp vụ đáng chú ý: đơn đã huỷ **biến mất khỏi lịch sử người dùng**, trong khi `TS-01` (§A8 L121) yêu cầu *"Ghi log toàn bộ tương tác… huỷ (kèm lý do + ai huỷ)"* ⇒ log vẫn còn ở backend nhưng **không có bề mặt cho user xem lại đơn đã huỷ**. Cross-ref `SC-CNL-009` (`C-CNL-02`: huỷ đơn phải ghi log LỊCH SỬ).

---

### REQ-ACT-008 · Empty state 2 tab
📍 `DOC-v1.0-06 KP-02 §5 · dòng "C-ORD-06"`  ·  Clarif: `C-ORD-06`

> "**C-ORD-06** | Empty state của 3 màn (Hoạt động · Quà đã nhận · Thông báo) khi không có data | ⚠ **Có lịch sử đảo chiều:** từng Resolved 2026-07-28 với text *"Hiện tại chưa có dữ liệu"*, sau đó **REVERT về Open 2026-07-29** vì rà lại toàn bộ 82 ảnh Figma + BRD + demo docx **không tìm thấy bằng chứng nào**"

**Source Location:** `DOC-v1.0-06 KP-02 §5 · bảng "Nhóm Open" · dòng "C-ORD-06"`

↳ **Ghi chú:** *(Implicit — không có quote đặc tả text empty state.)* Màn Hoạt động là **màn đầu tiên** trong danh sách của `C-ORD-06` ⇒ home canonical của CL này đặt ở module `ACT`. Theo `§Custom Rules §10.2`, **mỗi tab 1 SC empty state riêng** (`SC-ACT-012` + `SC-ACT-014`) vì 2 tab có tiền đề dữ liệu khác nhau. ⚠️ Bài học `KP-02 §6`: ⛔ không ghi `Resolved` dựa trên mô tả chat không kèm bằng chứng.

---

### REQ-ACT-009 · Chuỗi "★★★★★ Đã đánh giá" trên card Hoàn thành — UI leftover
📍 `DOC-v1.0-02 §3.7 · đoạn 3` · `DOC-v1.0-06 KP-01 §3 KB-ORD-07 (ghi chú)` · `KP-01 §6 KB-GIFT-02`  ·  Clarif: `C-GIFT-01`

> Nguồn #1 — `DOC-v1.0-02` §3.7 đoạn 3:
> "Tab "Đã hoàn thành": đơn trạng thái "Hoàn thành" (**5 sao + "Đã đánh giá"**)…"

> Nguồn #2 — `DOC-v1.0-06` KP-01 §3 `KB-ORD-07` (ghi chú cuối):
> "⚠ Trên card "Hoàn thành" có chuỗi `★★★★★ Đã đánh giá` nhưng **rating 1-5 sao đã out-of-scope v1.0** → coi là UI leftover, KHÔNG viết TC assert rating"

↳ **Ghi chú:** `C-GIFT-01` Resolved 2026-07-27: rating 1–5 sao là **phase sau**; v1.0 chỉ có Quà ảo (`GIFT-01`). Chuỗi `★★★★★` trên card là **UI leftover** ⇒ `SC-ACT-013` ghi nhận sự tồn tại, ⛔ **không assert giá trị sao, không assert cơ chế đánh giá**. Cross-ref `SC-USR-006` (không hiện Điểm uy tín), `SC-GIFT-011` (rating out of scope).

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
