# Requirement Traceability — v1.1 · Module ASN

> Tạo bởi: analyze-requirements (DELTA 2026-09-15, so với parent v1.0) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation` của `DOC-v1.1-01`: `FR<NN>` / `BR<FF>-NN` / `AC-{US}.{Scenario}.{Case}` / `NFR-NN` (khác hẳn ký hiệu domain-ID của `DOC-v1.0-01`) ⇒ **Schema A**, cột "Maps (Ref DOC)" dùng trực tiếp ID gốc của `DOC-v1.1-01`.
> Chỉ chứa REQ có delta (NEW/MODIFIED) so với `v1.0/ASN-ghep-noi/`. REQ không đổi (REQ-ASN-001..002, 004..006, 010..012) → xem parent, không lặp lại ở đây.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module ASN — DOC-v1.1-01

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-ASN-007 *(MODIFIED)* | `BR04-01`, `BR04-02` | `DOC-v1.1-01` §8.4 (page 38) | SC-ASN-011 | C-NTF-02 |
| REQ-ASN-008 *(MODIFIED)* | `BR04-04` | `DOC-v1.1-01` §8.4 (page 38) | SC-ASN-014 | — |
| REQ-ASN-009 *(MODIFIED)* | `BR03-06` | `DOC-v1.1-01` §8.3 (page 37) | SC-ASN-015 | — |
| REQ-ASN-003 *(MODIFIED — bổ sung NFR)* | `BR03-02`, `NFR06` | `DOC-v1.1-01` §8.3 (page 37) · §9 (page 53) | SC-ASN-006 | — |
| REQ-ASN-005 *(MODIFIED — bổ sung NFR)* | `NFR08` | `DOC-v1.1-01` §9 (page 53) | SC-ASN-008 | — |
| REQ-ASN-013 *(NEW)* | `NFR11` | `DOC-v1.1-01` §9 (page 54) | SC-ASN-019 | — |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-ASN-007 · Điều kiện khớp tuyến chính thức — điểm trùng + khoảng ngày giao nhau + buổi giao nhau *(MODIFIED)*
📍 `DOC-v1.1-01 §8.4 "FR04 — Khớp tuyến OFFER ↔ NEED" · Business Rules · page 38`  ·  Clarif: `C-NTF-02`

**Source Quote (cũ — v1.0, HẾT HIỆU LỰC ở dạng "chưa chốt"):**
> Nguồn v1.0 (`DOC-v1.0-06` KP-01 §4 `KB-ASN-04`): "= trùng địa chỉ giao hàng đã chọn + khung giờ phù hợp. KHÔNG dùng bán kính GPS / khoảng cách địa lý." · "🔴 Còn thiếu: "khung giờ phù hợp" là trùng hoàn toàn hay có độ lệch cho phép? Chu kỳ quét khớp?"

**Source Quote (mới — v1.1):**
> "BR04-01 | Điều kiện khớp: trùng điểm lấy VÀ điểm giao · khoảng ngày của NEED và OFFER có ngày giao nhau · tập buổi có buổi giao nhau."
> "BR04-02 | Buổi "Giờ nào cũng được" khớp với mọi buổi."
> "NFR-04 | Performance | Luồng khớp tuyến OFFER↔NEED chạy và đẩy thông báo trong ≤ 60 giây (p95) sau khi tin NEED được đăng | Cách đo: Timestamp log"

↳ **Ghi chú:** PRD chính thức **chốt định nghĩa "khung giờ phù hợp"** = tập buổi của NEED và OFFER có **ít nhất 1 buổi chung** (không cần trùng toàn bộ), và khoảng ngày chỉ cần **có ngày giao nhau** (overlap, không cần trùng hoàn toàn) — cụ thể hơn "tách rời hoàn toàn" mà `SC-ASN-011` v1.0 dùng để né vùng chưa chốt. `NFR-04` cho thêm ngưỡng **chu kỳ khớp ≤60s** — đây là 2/3 tham số của `C-NTF-02`/`RISK-ASN-04` đã được chốt qua đợt PRD này. Tham số còn lại ("ngưỡng gộp thông báo") xem `REQ-ASN-008`.

---

### REQ-ASN-008 · Trần thông báo khớp — 5 thông báo / 1 tin OFFER, KHÔNG theo ngày *(MODIFIED · đảo lần 2 — BA 2026-09-16)*
📍 `DOC-v1.1-01 §8.4 "FR04 — Khớp tuyến OFFER ↔ NEED" BR04-04 · page 38`  ·  Clarif: —

**Source Quote (cũ — v1.0, ĐÃ BA ĐẢO KẾT LUẬN NGÀY 2026-07-29, giờ PRD đảo LẠI LẦN NỮA):**
> `DOC-v1.0-06` KP-01 §4 `KB-ASN-03`: "Không phải "5 thông báo/ngày" cộng dồn — tính riêng theo từng tin."

**Source Quote (mới — v1.1):**
> "BR04-04 | Trần số thông báo khớp mỗi ngày cho một người dùng do admin cấu hình."

↳ **Ghi chú:** ⛔ **ĐẢO NGƯỢC** kết luận đã được BA chốt ở v1.0 (`KB-ASN-03`, 2026-07-29: "tính riêng theo từng tin OFFER, KHÔNG cộng dồn theo ngày"). PRD v1.1 lại quy định **trần theo NGÀY cho MỘT NGƯỜI DÙNG** (không phải theo từng tin OFFER), và giá trị cụ thể "do admin cấu hình" — KHÔNG có số cứng trong tài liệu. Xem `CHANGELOG.md §2 Kết luận bị đảo`. Vì không có số cứng, đây là **Open non-blocking mới**: cần hỏi vận hành/admin giá trị cấu hình thật trước khi viết TC boundary chính xác.

⛔ **Cập nhật 2026-09-16 — đoạn trên HẾT HIỆU LỰC, đừng trích lại:** BA trả lời `C-NTF-02` 2026-09-16 — *"Không có ngưỡng ngày, tài liệu bị dư → mỗi lần đăng Tôi nhận giao hàng thì bắn 5 thông báo/ 1 tin đăng, không có giới hạn ngày"*. Hiện hành: `BR04-04` **dư**, rule là **5 thông báo cho mỗi tin OFFER**, không có trần theo ngày; `RISK-ASN-08` **Closed**. Chi tiết còn thiếu → `C-ASN-04` (`risk_assessment.md`).

---

### REQ-ASN-009 · Ưu tiên gợi ý — làm rõ 2 tầng (độ gần tuyến trước, thời gian đăng sau) *(MODIFIED)*
📍 `DOC-v1.1-01 §8.3 "FR03 — Ghép nối & lộ liên hệ" BR03-06 · page 37`  ·  Clarif: —

**Source Quote (cũ — v1.0):**
> `DOC-v1.0-01` §D7 `OPR-04` L340: "Sắp xếp theo độ gần tuyến → thời gian đăng (mới trước)" — Analyst Note v1.0 kết luận "độ gần tuyến là nhị phân nên không còn thang để sắp xếp ⇒ tiêu chí duy nhất kiểm chứng được là thời gian đăng".

**Source Quote (mới — v1.1):**
> "BR03-06 | Trần gợi ý cho một người vận chuyển: tối đa 5 tin phù hợp, ưu tiên độ gần tuyến rồi tới thời gian đăng."

↳ **Ghi chú:** PRD **làm rõ (không đảo)** kết luận cũ của `SC-ASN-015`/`RISK-ASN-06`: "độ gần tuyến" **vẫn còn hiệu lực** như tầng ưu tiên số 1, không phải đã bị bỏ hẳn như suy diễn cũ ("không còn thang đo nên chỉ còn thời gian đăng"). PRD xác nhận **2 tầng cùng tồn tại**: (1) độ gần tuyến (nhị phân — trùng/không trùng) lọc trước, (2) trong nhóm trùng tuyến thì tin đăng sớm hơn xếp trước. `SC-ASN-015` cập nhật Then theo đúng 2 tầng này thay vì chỉ nói "chỉ còn thời gian đăng".

---

### REQ-ASN-003 · Chống double-accept — cơ chế khoá giao dịch + ngưỡng concurrency test *(MODIFIED — bổ sung NFR)*
📍 `DOC-v1.1-01 §8.3 "FR03" BR03-02 · page 37` · `§9 NFR-06 · page 53`  ·  Clarif: —

> "BR03-02 | Ghép ngay khi người vận chuyển bấm nhận — không có bước chủ tin duyệt. Một tin chỉ có một cặp ghép active; ghép cho người bấm đầu tiên, chống double-accept bằng khoá giao dịch."
> "NFR-06 | Data Integrity | Một tin chỉ tồn tại một cặp ghép active; tỷ lệ ghép trùng = 0% dưới điều kiện 50 request đồng thời trên cùng một tin | Cách đo: Concurrency test trên staging"

↳ **Ghi chú:** PRD xác nhận lại kết luận v1.0 (first-come, không cần chủ tin duyệt — không đổi), nhưng bổ sung **cơ chế kỹ thuật cụ thể** ("khoá giao dịch" = transaction lock, khớp với ghi nhận cũ "DB constraint + tx lock") và quan trọng nhất: **NFR-06 chỉ định rõ đây là việc của concurrency/backend test** (50 request đồng thời, ngưỡng 0% trùng), không phải test manual — giải quyết trực tiếp khó khăn đã ghi ở `RISK-ASN-02` ("nhánh cạnh tranh thật gần như không kiểm chứng được bằng manual 1 tester").

---

### REQ-ASN-005 · Đồng bộ realtime 3 vai — ngưỡng ≤5 giây *(MODIFIED — bổ sung NFR)*
📍 `DOC-v1.1-01 §9 NFR-08 · page 53`  ·  Clarif: —

> "NFR-08 | Consistency | Ba vai trò thấy cùng một trạng thái đơn trong ≤ 5 giây sau khi trạng thái đổi | Cách đo: Integration test đa thiết bị"

↳ **Ghi chú:** v1.0 chỉ có yêu cầu định tính ("không cần thao tác làm mới thủ công"), không có mốc thời gian, và rủi ro ghi nhận là bằng chứng chỉ đến từ demo giả lập 1-đơn/3-khung (`RISK-ASN-05`). NFR-08 cho **ngưỡng định lượng cụ thể** (≤5 giây) làm oracle rõ ràng khi test trên 3 thiết bị thật, và chỉ định phương pháp (Integration test đa thiết bị — phù hợp cho automation hơn manual thuần).

---

### REQ-ASN-013 · Tin OFFER không truy cập trực tiếp qua API — chặn + audit log *(NEW)*
📍 `DOC-v1.1-01 §9 NFR-11 · page 54`  ·  Clarif: —

> "NFR-11 | Security | Tin OFFER không truy cập được trực tiếp; mọi request đọc tin OFFER bởi người dùng không phải chủ tin phải bị chặn lỗi và ghi audit log | Cách đo: Security test"

↳ **Ghi chú:** Bổ sung mới, mở rộng `BR03-05`/`OPR-03` (tin OFFER không hiển thị công khai trên bảng tin) đã có SC một phần ở `SC-ASN-007` — NFR-11 thêm 2 yêu cầu mới không có ở v1.0: **(1)** test phải thực hiện ở **tầng API trực tiếp** (không chỉ qua UI, vì UI đơn giản là không có link tới tin OFFER — nhưng API có thể vẫn trả dữ liệu nếu không kiểm tra quyền ở backend, đúng dạng lỗi NFR-10/NFR-11 muốn ngăn), **(2)** phải có **audit log** khi có request trái phép. Cross-ref `RISK-ASN-03` (bảo mật liên hệ, cùng nhóm rủi ro lộ dữ liệu qua API thay vì UI).

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
> REQ không có delta (REQ-ASN-001, 002, 004, 006, 009, 010, 011, 012) → xem `v1.0/ASN-ghep-noi/requirement_traceability.md`, không lặp lại quote ở đây.
