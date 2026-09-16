---
id: v1.1/ASN-ghep-noi/scenario-map
title: Test Scenario Map — v1.1 · Module ASN
type: scenario-map
version: v1.1
sprint: 1
module: ASN
counts:
  req: 13
  sc: 19
  new: 1
  modified: 5
  carried: 13
  deprecated: 0
  p1: 6
  p2: 11
  p3: 2
status: ANALYZED
updated: 2026-09-15
---

# Test Scenario Map — v1.1 · Module ASN

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module ASN cho v1.1 (delta so với v1.0: req=12/sc=18).
> Parent: `v1.0/ASN-ghep-noi/` — 13 SC không đổi (CARRIED), 5 SC MODIFIED (giữ ID), 1 SC NEW.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Fan-out mỗi role · mỗi state-transition · lớp EP · boundary · nhánh lỗi = 1 SC.
> Delta lần này fan-out theo **tham số auto-match được chốt chính thức** (điều kiện khớp, trần thông báo/ngày, ngưỡng NFR) — không sinh SC rác cho phần PRD chỉ xác nhận lại kết luận cũ.

## Tổng quan
- Tổng số scenarios: **19** (NEW: 1, MODIFIED: 5, CARRIED: 13, DEPRECATED: 0)
- Phân bổ priority: P1: 6 | P2: 11 | P3: 2
- Delta lớn nhất: `SC-ASN-014` bị **đảo kết luận** (trần thông báo: từ "theo từng tin OFFER" sang "theo ngày/người dùng, do admin cấu hình").

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### ASN — Ghép nối

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-ASN-006 | Chống double-accept (bổ sung ngưỡng concurrency) | REQ-ASN-003 | DOC-v1.1-01 §8.3 BR03-02 · §9 NFR-06 | 1 tin NEED "Chờ ghép"; 2 Carrier B và C cùng mở Chi tiết tin của tin đó | (a, manual) B và C bấm "Tôi mang giúp được" tuần tự, C bấm sau khi tin đã ẩn với B; (b, automation/backend) 50 request ghép đồng thời trên cùng 1 tin | (a) Chỉ B ghép được; C nhận thông báo tin đã có người nhận. (b) Tỷ lệ ghép trùng = 0% (khoá giao dịch chặn toàn bộ request thừa) — nhánh (b) BẮT BUỘC test ở tầng API/backend (concurrency test trên staging), không manual | P1 | Business Rule + Backend | MODIFIED |
| SC-ASN-008 | Đồng bộ realtime 3 vai — ngưỡng ≤5 giây | REQ-ASN-005 | DOC-v1.1-01 §9 NFR-08 | 1 đơn "Chờ ghép" mở đồng thời trên 3 phiên/thiết bị khác nhau (Sender · Carrier · Receiver) | Carrier xác nhận mang giúp; đo thời điểm mỗi phiên cập nhật trạng thái | Cả 3 phiên cập nhật trạng thái "Đã ghép" trong vòng **≤5 giây** kể từ thời điểm đổi trạng thái, không cần thao tác làm mới thủ công | P2 | Functional | MODIFIED |
| SC-ASN-011 | Điều kiện khớp tuyến chính thức (điểm + ngày overlap + buổi overlap) | REQ-ASN-007 | DOC-v1.1-01 §8.4 BR04-01, BR04-02 | Carrier B đã đăng tin OFFER (điểm xuất phát P1, điểm đến P2, khoảng ngày D1-D2, tập buổi S) | Đăng lần lượt: (a) tin NEED điểm giao KHÁC P2 → không khớp; (b) tin NEED trùng P1/P2, khoảng ngày KHÔNG giao nhau với D1-D2 → không khớp; (c) tin NEED trùng P1/P2, khoảng ngày có giao nhau nhưng tập buổi KHÔNG có buổi chung → không khớp; (d) tin NEED trùng P1/P2, ngày giao nhau, buổi có ít nhất 1 buổi chung (hoặc chọn "Giờ nào cũng được") → KHỚP, B nhận thông báo trong ≤60s | Nhánh (a)(b)(c): B KHÔNG nhận thông báo khớp tuyến. Nhánh (d): B CÓ nhận thông báo, trong ngưỡng NFR-04 ≤60s (p95) | P2 | Business Rule | MODIFIED |
| SC-ASN-014 | Trần thông báo khớp — **5 thông báo / 1 tin đăng OFFER**, KHÔNG có trần theo ngày *(đảo lần 2 — BA 2026-09-16)* | REQ-ASN-008 | DOC-v1.1-01 §8.4 BR04-04 *(BA xác nhận dư)* · BA trả lời `C-NTF-02` 2026-09-16 | Có **≥ 6** tin NEED ở `POSTED` cùng khớp tuyến P1→P2 (khoảng ngày + buổi giao nhau) | Carrier B đăng 1 tin OFFER P1→P2 | B nhận **tối đa 5** thông báo `NTF-03` cho tin OFFER này; ⛔ KHÔNG assert trần theo ngày. ⚠️ Người nhận / cách chọn 5 tin / chiều NEED-mới **chờ `C-ASN-04`** — tới lúc đó chỉ assert *"không vượt 5 cho 1 tin OFFER"* | P2 | Business Rule | MODIFIED |
| SC-ASN-015 | Thứ tự ưu tiên gợi ý — 2 tầng (độ gần tuyến trước, thời gian đăng sau) | REQ-ASN-009 | DOC-v1.1-01 §8.3 BR03-06 | Có ≥3 tin NEED: 2 tin trùng tuyến của B (đăng ở 2 thời điểm khác nhau) + 1 tin KHÔNG trùng tuyến nhưng đăng sớm nhất | Xem danh sách gợi ý của B | Tầng 1: 2 tin trùng tuyến luôn xếp trước tin không trùng tuyến (dù tin không trùng đăng sớm hơn). Tầng 2: trong 2 tin trùng tuyến, tin đăng sau (mới hơn) xếp trước tin đăng trước | P3 | Business Rule | MODIFIED |
| SC-ASN-019 | [NEW] Chặn truy cập tin OFFER qua API trực tiếp + audit log | REQ-ASN-013 | DOC-v1.1-01 §9 NFR-11 | Tin OFFER đang POSTED, không phải sở hữu của tài khoản D | D gọi trực tiếp API đọc chi tiết tin OFFER đó (không qua UI, vì UI không có đường dẫn tới tin OFFER với người ngoài) | Request bị chặn lỗi (không trả dữ liệu tin OFFER); hệ thống ghi audit log ghi nhận request trái phép này | P2 | Security | NEW |

#### Source Detail per Scenario (verbatim quotes — `references/quoting-guide.md`)

##### SC-ASN-006 — Chống double-accept (bổ sung ngưỡng concurrency)

**Source Quote (cũ):**
> `DOC-v1.0-01` §D3 `ASN-03` L249: "1 tin chỉ 1 cặp active (DB constraint + tx lock)"

**Source Quote (mới):**
> "BR03-02 | ... chống double-accept bằng khoá giao dịch."
> ↪ *Quote `NFR-06` — home ở `requirement_traceability.md` · `REQ-ASN-003` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

**Source Location:** `DOC-v1.1-01 §8.3 "FR03" · page 37` · `§9 "NFR-06" · page 53`

**Analyst Note:** Nhánh (a) manual giữ nguyên như v1.0 (chỉ kiểm chứng được thứ tự tuần tự). Nhánh (b) là bổ sung mới quan trọng: NFR-06 chỉ định rõ đây là việc của **automation/backend concurrency test** với ngưỡng cụ thể (50 request, 0% trùng) — giải quyết đúng khó khăn đã ghi ở `RISK-ASN-02`, chuyển từ "không kiểm chứng được bằng manual" sang "có phương pháp + ngưỡng rõ ràng, giao cho automation". `risk_assessment.md` cập nhật Solution tương ứng.

---

##### SC-ASN-008 — Đồng bộ realtime 3 vai — ngưỡng ≤5 giây

**Source Quote:**
> ↪ *Quote `NFR-08` — home ở `requirement_traceability.md` · `REQ-ASN-005` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

**Source Location:** `DOC-v1.1-01 §9 "NFR-08" · page 53`

**Analyst Note:** v1.0 chỉ có yêu cầu định tính, không mốc thời gian — bằng chứng cũ chỉ đến từ demo giả lập 1-đơn/3-khung (`RISK-ASN-05`). NFR-08 cho oracle định lượng rõ ràng (≤5s) khi test thật trên 3 thiết bị, giúp `RISK-ASN-05` chuyển từ "không chứng minh được" sang "có ngưỡng cụ thể để pass/fail".

---

##### SC-ASN-011 — Điều kiện khớp tuyến chính thức

**Source Quote (cũ — vùng chưa chốt):**
> `DOC-v1.0-06` KP-01 §4 `KB-ASN-04`: "🔴 Còn thiếu: "khung giờ phù hợp" là trùng hoàn toàn hay có độ lệch cho phép?"

**Source Quote (mới):**
> ↪ *Quote `BR04-01` — home ở `requirement_traceability.md` · `REQ-ASN-007` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*
> ↪ *Quote `BR04-02` — home ở `requirement_traceability.md` · `REQ-ASN-007` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

**Source Location:** `DOC-v1.1-01 §8.4 "FR04" BR04-01/02 · page 38`

**Analyst Note:** Thay thế nhánh negative "2 khung tách rời hoàn toàn" (né tránh vùng chưa chốt) bằng đúng định nghĩa overlap chính thức. Nhánh (c) (ngày overlap nhưng buổi không chung) là case mới, trước đây không tách được vì chưa có định nghĩa buổi độc lập với ngày. `RISK-ASN-04` chuyển Open→Resolved (xem risk_assessment.md); tham số "chu kỳ quét" đã có NFR-04 ≤60s.

---

##### SC-ASN-014 — Trần thông báo khớp — 5 thông báo / 1 tin OFFER *(đảo lần 2 — BA 2026-09-16)*

**Source Quote (cũ — v1.0, kết luận HẾT HIỆU LỰC):**
> `DOC-v1.0-06` KP-01 §4 `KB-ASN-03`: "Không phải "5 thông báo/ngày" cộng dồn — tính riêng theo từng tin." · "⚠ Giá trị test 3/5/6 tin là giá trị chốt, không phải mock." *(mốc 3/5/6 này vẫn dùng cho SC-ASN-013 "trần gợi ý 5 tin/carrier" — KHÔNG liên quan tới trần thông báo/ngày ở đây.)*

**Source Quote (mới):**
> ↪ *Quote `BR04-04` — home ở `requirement_traceability.md` · `REQ-ASN-008` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

**Source Location:** `DOC-v1.1-01 §8.4 "FR04" BR04-04 · page 38`

**Analyst Note (diff):** ⛔ **Kết luận bị đảo lần 2.** v1.0 (BA, 2026-07-29): trần theo TỪNG TIN OFFER. v1.1 (PRD chính thức): trần theo NGÀY, cho MỘT NGƯỜI DÙNG (gộp tất cả tin OFFER của người đó), giá trị "do admin cấu hình" — không có số cứng trong tài liệu. **Không dùng lại mốc 3/5/6 của v1.0 cho rule này** (mốc đó gắn với "trần gợi ý 5 tin/carrier" của `SC-ASN-013`, một rule độc lập không đổi). Trước khi viết TC boundary cho `SC-ASN-014`, PHẢI hỏi admin/vận hành giá trị cấu hình thật — ghi ở `CHANGELOG §3 Nợ đang mở`.

⛔ **Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC, đừng trích lại:** BA 2026-09-16 bỏ trần theo ngày (`BR04-04` dư) — rule hiện hành **5 thông báo / 1 tin đăng OFFER**; ⛔ không hỏi admin giá trị cấu hình. Đây thực chất là lần đảo **thứ 3** (v1.0 theo tin → PRD theo ngày → BA theo tin đăng). Then hiện hành ở bảng SC phía trên; chi tiết chờ `C-ASN-04`.

---

##### SC-ASN-015 — Thứ tự ưu tiên gợi ý — 2 tầng

**Source Quote (cũ):**
> `DOC-v1.0-01` §D7 `OPR-04` L340: "Sắp xếp theo độ gần tuyến → thời gian đăng (mới trước)"

**Source Quote (mới):**
> ↪ *Quote `BR03-06` — home ở `requirement_traceability.md` · `REQ-ASN-009` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

**Source Location:** `DOC-v1.1-01 §8.3 "FR03" BR03-06 · page 37`

**Analyst Note (diff):** Không phải đảo mà là **làm rõ**: v1.0 kết luận "độ gần tuyến không còn thang đo nên vô hiệu, chỉ còn thời gian đăng" (`RISK-ASN-06` Pending). PRD xác nhận độ gần tuyến (dù nhị phân) **vẫn là tầng lọc số 1** — chỉ khi 2 tin cùng vượt qua tầng 1 (cùng trùng tuyến) thì mới xét tầng 2 (thời gian đăng). Cập nhật Given/Then để test đúng 2 tầng thay vì chỉ 1 tầng thời gian.

---

##### SC-ASN-019 — [NEW] Chặn truy cập tin OFFER qua API trực tiếp + audit log

**Source Quote:**
> ↪ *Quote `NFR-11` — home ở `requirement_traceability.md` · `REQ-ASN-013` (không chép lại — tránh lặp home, health-check G-03 2026-09-16)*

**Source Location:** `DOC-v1.1-01 §9 "NFR-11" · page 54`

**Analyst Note:** Mở rộng `BR03-05`/`SC-ASN-007` (tin OFFER không hiển thị công khai trên UI) sang tầng API — yêu cầu kiểm tra quyền ở **tầng máy chủ**, không chỉ ẩn trên giao diện (cùng nguyên tắc với NFR-10 của `RISK-ASN-03`). Đây là SC cho **security/API test**, không phải luồng UI thông thường; đề xuất giao cho automation/backend test khi có công cụ gọi API trực tiếp.

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| SC-ASN-001 | Ghép qua "Tôi mang giúp được" | ASN | v1.0 | P1 | → `v1.0/ASN-ghep-noi/test_scenario_map.md` |
| SC-ASN-002 | Huỷ ở modal xác nhận | ASN | v1.0 | P2 | → xem v1.0 |
| SC-ASN-003 | Ghép ngay, không cần chủ tin duyệt | ASN | v1.0 | P1 | → xem v1.0 |
| SC-ASN-004 | Lộ SĐT cho 2 người trong cặp | ASN | v1.0 | P1 | → xem v1.0 |
| SC-ASN-005 | Người thứ ba không thấy SĐT | ASN | v1.0 | P2 | → xem v1.0 |
| SC-ASN-007 | Tin ẩn khỏi bảng tin + luồng gợi ý | ASN | v1.0 | P1 | → xem v1.0 |
| SC-ASN-009 | Auto-match sinh thông báo | ASN | v1.0 | P2 | → xem v1.0 |
| SC-ASN-010 | "Nhận giao" từ tin khớp tuyến | ASN | v1.0 | P2 | → xem v1.0 |
| SC-ASN-012 | Không tự khớp tin của chính mình | ASN | v1.0 | P1 | → xem v1.0 |
| SC-ASN-013 | Trần 5 tin gợi ý / carrier | ASN | v1.0 | P2 | → xem v1.0 |
| SC-ASN-016 | Tin quá hạn bị loại khỏi luồng khớp | ASN | v1.0 | P2 | → xem v1.0 |
| SC-ASN-017 | Carrier huỷ nhận → tin khớp lại được | ASN | v1.0 | P2 | → xem v1.0 |
| SC-ASN-018 | [GAP] Wizard không tạo listing độc lập | ASN | v1.0 | P3 | → xem v1.0 — ✅ **2026-09-16 BA: ghi đè chỉ là giới hạn demo; app không giới hạn đăng tin** (`C-ASN-03` Resolved) ⇒ hết `[GAP]`, Then assert đăng tin thứ 2 **không ghi đè** tin thứ 1 (cả 2 cùng tồn tại) |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
