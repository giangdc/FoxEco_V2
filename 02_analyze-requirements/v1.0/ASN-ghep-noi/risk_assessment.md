---
id: v1.0/ASN-ghep-noi/risk
title: Risk Assessment — v1.0 · Module ASN
type: risk-assessment
version: v1.0
sprint: 1
module: ASN
counts:
  cl: 2
  risk: 7
  cl_open: 1
  cl_resolved: 0
status: ANALYZED
updated: 2026-09-07
---

# Risk Assessment — v1.0 · Module ASN

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module ASN.
> 🔑 Frontmatter `counts:` = nguồn canonical CL/RISK — **chỉ đếm CL có home ở module này**; CL tham chiếu (home ở module khác) KHÔNG tính vào `counts`. **Layout v2 ⇒ đây là home của Clarification.**
> 📌 **Home canonical của `C-NTF-02`** (định nghĩa "khớp tuyến" + tham số vận hành) đặt ở module này vì rule thuộc engine ghép nối; `NTF` chỉ tham chiếu.

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| ASN | **High** | Module **rủi ro cao nhất dự án**: chứa rule cạnh tranh (double-accept) khó kiểm chứng, rule bảo mật liên hệ, và **engine auto-match còn 3 tham số chưa chốt** (định nghĩa khung giờ phù hợp · chu kỳ quét · ngưỡng gộp thông báo). Thêm nữa BRD **mâu thuẫn nội bộ** về cơ chế ghép (ghép ngay vs chủ tin duyệt) |

## Chi tiết rủi ro (bảng hợp nhất)
| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-ASN-01 | ASN / Cơ chế ghép | **BRD mâu thuẫn nội bộ:** `BR-CON-01`+`§A5` nói *ghép ngay không cần duyệt*; `ASN-02`+`§D2`+`§D5` nói *chủ tin chấp nhận* ⇒ nếu chọn nhánh sai thì toàn bộ SC luồng ghép sai tiền đề | **High** | `BR-CON-01` L77 vs `ASN-02` L248 vs `§D2` L209 vs `§D5` L293 | `SC-ASN-003` bảo vệ kết luận "ghép ngay" | Chốt theo `BR-CON-01` + PRD §4.2 (bề mặt thật); ghi ràng buộc `CHANGELOG §2` | Resolved | REQ-ASN-001, SC-ASN-003 |
| RISK-ASN-02 | ASN / Double-accept | Nhánh **cạnh tranh thật** (2 Carrier bấm trong cùng cửa sổ ms) gần như không kiểm chứng được bằng manual 1 tester ⇒ dễ khai coverage cho nhánh chưa thực sự test | **High** | `ASN-03` L249 (*"DB constraint + tx lock"*) · `OPR-03` L339 | Chạy nhánh tuần tự (người 2 bấm sau khi tin đã ẩn); nhánh đồng thời cần 2 thiết bị + phối hợp | ⛔ Ghi rõ nhánh nào đã test; nhánh cạnh tranh thật đề xuất test ở tầng API/backend | Open | REQ-ASN-003, SC-ASN-006 |
| RISK-ASN-03 | ASN / Bảo mật liên hệ | Nếu người thứ ba xem được SĐT của cặp ghép ⇒ lỗ dữ liệu cá nhân nghiêm trọng hơn cả `SC-FEED-010` (ở đó tin còn công khai; ở đây đơn đã là việc riêng của 2 người) | **High** | `BR-CON-02` L78 · `OPR-07` L343 | `SC-ASN-005` — cần tài khoản thứ tư không thuộc cặp | Chạy sớm; FAIL → log bug P1 | Open | REQ-ASN-002, SC-ASN-005 |
| RISK-ASN-04 | ASN / Auto-match | **3 tham số chưa chốt**: định nghĩa *"khung giờ phù hợp"* (trùng hoàn toàn vs có độ lệch) · chu kỳ quét khớp · ngưỡng gộp thông báo ⇒ không viết được TC biên cho điều kiện khớp | **High** | `C-NTF-02` Partially Resolved · BRD tự ghi *"Nháp — chờ BA review & bổ sung"* (§D6 L315, §D7 L333) | `SC-ASN-011` chỉ dùng khung giờ **tách rời hoàn toàn** | Hỏi BA (`C-NTF-02` phần còn thiếu); ⛔ không test độ lệch tới khi có định nghĩa | Open | REQ-ASN-006, REQ-ASN-007, SC-ASN-011 |
| RISK-ASN-05 | ASN / Realtime | Bằng chứng đồng bộ realtime chỉ đến từ **bản demo 1 đơn / 3 khung cùng bộ nhớ** ⇒ không chứng minh được đồng bộ qua backend giữa 3 thiết bị thật | Medium | `DOC-v1.0-02` §4.2 vs §1.4 (*"chỉ mô phỏng MỘT đơn hàng duy nhất cho cả 3 khung xem"*) | `SC-ASN-008` với 3 phiên/thiết bị khác nhau | Nếu cần refresh thủ công → finding cho BA, ⛔ không tự kết luận bug | Open | REQ-ASN-005, SC-ASN-008 |
| RISK-ASN-06 | ASN / Ưu tiên gợi ý | Tiêu chí *"độ gần tuyến"* **không còn thang đo** sau khi `KB-ASN-04` chốt khớp bằng địa chỉ (nhị phân) ⇒ rule `OPR-04` chỉ kiểm được nửa | Medium | `OPR-04` L340 vs `KB-ASN-04` | `SC-ASN-015` chỉ assert thứ tự theo thời gian đăng | Nêu với BA khi trả lời `C-NTF-02`: `OPR-04` còn hiệu lực ở dạng nào | Pending | REQ-ASN-009, SC-ASN-015 |
| RISK-ASN-07 | ASN / Tiền đề dữ liệu | Cần **4 tài khoản** + **2–3 thiết bị/phiên đồng thời** + **6 tin khớp cùng tuyến** + **1 tin quá hạn** ⇒ chi phí thiết lập cao nhất trong 11 module | Medium | `test_data_catalog.md` §Ghi chú chung | Lập kế hoạch seed trước khi execute cả lô | Nhờ dev/QA seed; ưu tiên chạy nhóm P1 trước nếu thiếu thiết bị | Open | REQ-ASN-003, REQ-ASN-006, REQ-ASN-008 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-NTF-02 | 🟡 Định nghĩa "khớp tuyến" & tham số vận hành (**home canonical ở đây**) | 🟡 **Partially Resolved** | 2026-07-27 | REQ-ASN-006, REQ-ASN-007, REQ-ASN-008 |
| C-ASN-03 | 🔴 Wizard đăng tin không tạo listing độc lập trong feed | 🔴 **Open** | kế thừa 2026-07 | REQ-ASN-012 |
| C-ASN-01 · C-ASN-02 | (tham chiếu — home ở `FEED-bang-tin/risk_assessment.md`) | ✅ Resolved | 2026-07-27 | REQ-ASN-002, REQ-ASN-010 |

### C-NTF-02 · 🟡 Định nghĩa "khớp tuyến" & tham số vận hành (home canonical)

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-01` §D7 `OPR-02` L338): "Chỉ khớp khi trùng điểm lấy & điểm giao (cùng khu vực/tuyến) và **giao nhau về khung giờ**"
> Nguồn B (`DOC-v1.0-01` §D6 L329 — chính BRD tự ghi): "Chờ BA bổ sung: ngưỡng thời gian nhắc, gộp/không gộp thông báo, thông báo cho người thứ 3 (VD người nhận khi carrier huỷ), cấu hình bật/tắt theo loại."
> Nguồn C — ĐÃ CHỐT (`DOC-v1.0-06` KP-01 §4 KB-ASN-04): "= **trùng địa chỉ giao hàng đã chọn** + **khung giờ phù hợp**. **KHÔNG dùng bán kính GPS / khoảng cách địa lý.**"
> Nguồn D — CÒN THIẾU (`DOC-v1.0-06` KP-01 §4 KB-ASN-04): "🔴 Còn thiếu: "khung giờ phù hợp" là trùng hoàn toàn hay có độ lệch cho phép? Chu kỳ quét khớp? Ngưỡng gộp thông báo?"

**Source Location:** `DOC-v1.0-01 §D7 · OPR-02 · L338` · `§D6 · L329` ⟷ `DOC-v1.0-06 KP-01 §4 "KB-ASN-04"` · `KP-02 §4`

**Analyst Note:** **Đã chốt:** khớp tuyến = **trùng địa chỉ đã chọn** (khớp chuỗi/ID văn phòng), ⛔ không dùng bán kính GPS. **Còn 3 tham số chưa chốt:** (a) *"khung giờ phù hợp"* — trùng hoàn toàn hay cho độ lệch? (b) **chu kỳ quét khớp** — engine quét ngay khi có tin mới hay theo lịch? (c) **ngưỡng gộp thông báo**. Hệ quả: `SC-ASN-011` chỉ dùng khung giờ **tách rời hoàn toàn** cho nhánh negative; ⛔ không viết TC biên độ lệch; `SC-ASN-009` không assert độ trễ nhận thông báo (phụ thuộc chu kỳ quét). ⚠️ Chính BRD ghi §D6/§D7 là *"Nháp — chờ BA review & bổ sung"* ⇒ đây là **vùng đặc tả chưa hoàn thiện**, không phải thiếu sót của phân tích. **Non-blocking** nhưng giới hạn coverage thật của auto-match.

### C-ASN-03 · 🔴 Wizard không tạo listing độc lập trong feed

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-06` KP-01 §4 `KB-ASN-05`): "Ghi nhận trên prototype. Chưa rõ là giới hạn kiến trúc bản demo (chấp nhận được) hay hành vi cần fix."
> Nguồn B (`DOC-v1.0-02` §7 dòng 3): "Demo chỉ có 1 đơn hàng duy nhất | Đăng tin mới sẽ ghi đè đơn đang có, không tạo song song nhiều đơn — cần lưu ý khi thiết kế kịch bản test đa đơn."

**Source Location:** `DOC-v1.0-06 KP-01 §4 "KB-ASN-05"` ⟷ `DOC-v1.0-02 §7 · bảng · dòng 3`

**Analyst Note:** Nguồn B **giải thích được** nguồn A: bản demo *"chỉ có 1 đơn hàng duy nhất"* và *"đăng tin mới ghi đè đơn đang có"* ⇒ việc không thấy listing độc lập rất có thể là **giới hạn của demo**, không phải đặc tả sản phẩm. ⇒ `SC-ASN-018` ghi nhận với tiền đề **2 tin liên tiếp**; ⛔ không kết luận bug. **Cần xác nhận lại khi có backend thật** — nếu app STG cũng ghi đè đơn thì đó là vấn đề kiến trúc nghiêm trọng cần escalate. **Non-blocking** cho generate-tc.

## Khuyến nghị tổng thể
1. **Resolve trước generate-tc:** `C-NTF-02` phần còn thiếu (định nghĩa *"khung giờ phù hợp"* + chu kỳ quét) — không chốt thì **không viết được TC biên** cho điều kiện khớp, coverage auto-match chỉ ở mức nhánh trùng/không trùng.
2. **Ưu tiên test P1 high-risk:** `SC-ASN-005` (người thứ ba không thấy SĐT — rủi ro dữ liệu cá nhân) · `SC-ASN-012` (engine không tự khớp chính mình) · `SC-ASN-006` (double-accept) · `SC-ASN-004`/`SC-ASN-007` (lộ SĐT đúng cặp · ẩn tin sau ghép).
3. **Cần môi trường/dữ liệu:** **4 tài khoản** + **2–3 thiết bị/phiên đồng thời** + **6 tin khớp cùng 1 tuyến** + **1 tin quá hạn** (nhờ dev). ⛔ Không có 2 thiết bị thì `SC-ASN-006` chỉ chạy được nhánh tuần tự — **ghi rõ trong kết quả**, đừng khai coverage cho nhánh cạnh tranh.
4. **ID/text cleanup (non-blocking, cần trước automation):** phân biệt nghiêm ngặt 2 nhãn nút — **"Tôi mang giúp được"** (luồng NEED thủ công) vs **"Nhận giao"** (luồng OFFER khớp tuyến); dùng lẫn sẽ làm locator automation trỏ sai luồng.
