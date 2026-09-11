---
id: v1.0/HOME-trang-chu/risk
title: Risk Assessment — v1.0 · Module HOME
type: risk-assessment
version: v1.0
sprint: 1
module: HOME
counts:
  cl: 3
  risk: 5
  cl_open: 3
  cl_resolved: 0
status: ANALYZED
updated: 2026-09-07
---

# Risk Assessment — v1.0 · Module HOME

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module HOME.
> 🔑 Frontmatter `counts:` = nguồn canonical CL/RISK. **Layout v2 ⇒ đây là home của Clarification.**

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| HOME | **Medium** | Bề mặt hiển thị nhiều nhưng **đặc tả mỏng và lệch nguồn** — 3 CL đều Open (số tin 1 vs 5 · icon vai trò · điều kiện ẩn section); đợt cũ viết 32 TC trên nền chỉ 1 scenario |

## Chi tiết rủi ro (bảng hợp nhất)
| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-HOME-01 | HOME / Section "Tin mới" | Số tin hiển thị **mâu thuẫn 1 vs 5** giữa PRD và BRD ⇒ mọi TC assert số lượng đều có 50% khả năng sai, và nút "Xem thêm" phụ thuộc chính con số đó | **High** | `DOC-v1.0-02` §3.1 vs `DOC-v1.0-01` `US-D06` L175 (`KP-05` §2.1) | Đếm & ghi nhận số thật; assert quan hệ thay vì số cứng | Hỏi BA (`C-HOME-03`); tới khi đó `SC-HOME-019` chỉ ghi nhận, `SC-HOME-021` dùng Given theo quan hệ | Open | REQ-HOME-007, SC-HOME-019, SC-HOME-021 |
| RISK-HOME-02 | HOME / Section "Đơn của tôi" | **Hai cách hiểu điều kiện ẩn**: theo "có/không có đơn đang hoạt động" (doc) vs theo **vai trò** (nghi vấn `KP-05 §3 #3`) ⇒ TC ẩn/hiện có thể FAIL vì hiểu sai tiền đề | Medium | `DOC-v1.0-02` §3.1 vs `DOC-v1.0-06` KP-05 §3 (#3) | Test cả 2 tiền đề: tài khoản không đơn (mọi vai) + Carrier có đơn | Hỏi BA (`C-HOME-02`); `SC-HOME-010` assert theo doc, kết quả khác → dữ liệu cho CL | Open | REQ-HOME-005, SC-HOME-009, SC-HOME-010 |
| RISK-HOME-03 | HOME / Multi-order | PRD dựng từ bản demo **chỉ có 1 đơn duy nhất** (*"Đăng tin mới sẽ ghi đè đơn đang có"*) ⇒ hành vi Trang chủ khi có **≥2 đơn đang hoạt động** hoàn toàn không có đặc tả | Medium | `DOC-v1.0-02` §7 · bảng "Các điểm cần làm rõ" · dòng 3 | Tạo 2 đơn song song trên STG rồi ghi nhận section hiện đơn nào | Ghi nhận khi execute; nếu app chọn 1 đơn theo quy tắc nào đó → mở CL mới | Open | REQ-HOME-005, SC-HOME-009 |
| RISK-HOME-04 | HOME / Header | "Icon vai trò" có trong doc nhưng **không có mapping icon↔vai** ⇒ dễ viết TC khẳng định icon giả định (đúng lỗi mà `§Custom Rules §10.1` sinh ra để chặn) | Low | `DOC-v1.0-02` §2 dòng "Header" vs `KP-05` §3 (#5) | Ghi nhận icon 3 vai, không assert | `SC-HOME-004` viết dạng GAP finding; hỏi BA `C-HOME-01` | Open | REQ-HOME-002, SC-HOME-004 |
| RISK-HOME-05 | HOME / Dữ liệu demo | Bản demo có **dữ liệu mẫu tĩnh sai** (Carrier chưa nhận đơn vẫn thấy 1 đơn "Chờ ghép"; 3 tài khoản cùng bộ chỉ số 12/4.8/540) ⇒ lấy hành vi demo làm oracle sẽ sinh TC sai từ gốc | Medium | `DOC-v1.0-02` §4.5 · §7 dòng 4 và 7 | Chỉ dùng BRD + Figma + app STG làm oracle; demo chỉ để hiểu luồng | Ghi ràng buộc ở `CHANGELOG §2`; `SC-HOME-010` không lấy demo làm chuẩn | Resolved | REQ-HOME-004, REQ-HOME-005 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-HOME-01 | Icon vai trò ở header (mapping) + lệch tagline banner giữa 2 doc | 🔴 **Open** | mở 2026-09-07 | REQ-HOME-002, REQ-HOME-003 |
| C-HOME-02 | Section "Đơn của tôi" ẩn theo **điều kiện có đơn** hay theo **vai trò**? | 🔴 **Open** | mở 2026-09-07 (từ `KP-05 §3 #3`) | REQ-HOME-005 |
| C-HOME-03 | Section "Tin mới" hiển thị **1 tin** hay **5 tin**? | 🔴 **Open** | kế thừa `KP-05 §2.1` (chưa giải quyết từ 2026-07) | REQ-HOME-007 |

### C-HOME-01 · Icon vai trò header + tagline banner

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-02` §2 dòng "Header"): "Header | Icon vai trò + "Xin chào, [Tên]" + chuông thông báo (chấm đỏ khi có tin chưa đọc)"
> Nguồn B (`DOC-v1.0-06` KP-05 §3 dòng 5): "**Icon vai trò ở Header khác nhau** theo Sender/Carrier/Receiver | Chưa có bằng chứng UI mapping"
> Nguồn C (tagline — `DOC-v1.0-02` §2): "Banner quảng bá | "Tiện đường — Giúp đồng nghiệp"…" ⟷ (`DOC-v1.0-01` §A3 L29): "Tagline: "Tiện đường — Đồng nghiệp giúp nhau""

**Source Location:** `DOC-v1.0-02 §2 · dòng "Header"` và `dòng "Banner quảng bá"` ⟷ `DOC-v1.0-01 §A3 · L29` ⟷ `DOC-v1.0-06 KP-05 §3 · dòng 5`

**Analyst Note:** Hai điểm gộp 1 CL vì cùng bề mặt header/banner Trang chủ và cùng cần 1 lượt BA trả lời: **(a)** icon nào ứng với vai nào (không nguồn nào nói) ⇒ `SC-HOME-004` chỉ ghi nhận; **(b)** tagline chính thức là *"Giúp đồng nghiệp"* (PRD) hay *"Đồng nghiệp giúp nhau"* (BRD §A3)? Ảnh hưởng trực tiếp tới TC assert text và tới locator text nếu automation. **Non-blocking.**

### C-HOME-02 · Section "Đơn của tôi" — ẩn theo điều kiện hay theo vai trò?

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-02` §3.1): "Đơn của tôi | **Chỉ hiện khi có đơn đang hoạt động.** Nhãn "Gửi:" + loại hàng | giá trị…"
> Nguồn B (`DOC-v1.0-02` §4.1): "khi chưa nhận đơn nào, KHÔNG có section "Đơn của tôi" — Home đi thẳng xuống "Tin mới""
> Nguồn C (`DOC-v1.0-06` KP-05 §3 dòng 3): "**Carrier KHÔNG thấy section "Đơn của tôi"** — ẩn theo **VAI TRÒ** | Doc hiện chỉ nói ẩn theo "có/không có đơn đang hoạt động", không nói theo vai trò"

**Source Location:** `DOC-v1.0-02 §3.1 · dòng "Đơn của tôi"` · `§4.1 · đoạn 1` ⟷ `DOC-v1.0-06 KP-05 §3 · dòng 3`

**Analyst Note:** Nguồn A/B nhất quán (**ẩn theo điều kiện có đơn**); nguồn C ghi lại quan sát của đợt merge với QC anhdc4 cho rằng **ẩn theo vai trò**. Hai rule cho ra kết quả khác nhau ở đúng 1 ô: **Carrier ĐANG có đơn** — theo A/B thì phải hiện, theo C thì ẩn. ⇒ `SC-HOME-012` (nhãn "Giao:" của Carrier) chính là ô phân định; chạy nó trước sẽ trả lời được CL này mà không cần BA. **Non-blocking** nhưng nên chạy sớm.

### C-HOME-03 · Section "Tin mới" — 1 tin hay 5 tin?

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-02` §3.1): "Tin mới | Rút gọn **1 tin mới nhất** của CẢ CỘNG ĐỒNG (không riêng của Người gửi); bấm vào mở Chi tiết tin"
> Nguồn B (`DOC-v1.0-01` §D1b `US-D06` L175): "Trang chủ hiển thị **đúng 5 tin mới nhất**; nếu còn tin khác hiện nút "Xem thêm trên Bảng tin" dẫn sang màn Bảng tin"

**Source Location:** `DOC-v1.0-02 §3.1 · bảng Trường/Thành phần · dòng "Tin mới"` ⟷ `DOC-v1.0-01 §D1b · US-D06 · Acceptance Criteria · L175`

**Analyst Note:** Mâu thuẫn **kế thừa nguyên trạng** từ đợt v1.0 cũ (`DOC-v1.0-06` KP-05 §2.1) — `C-ORD-07` chỉ giải quyết vế *"Sender có thấy section không"*, **không** giải quyết vế số lượng. Cách xử lý giữ nguyên: TC completeness **cố ý không assert số lượng**; khác biệt so với đợt cũ là gap nay có **SC riêng có ID** (`SC-HOME-019`) thay vì chỉ nằm trong ghi chú. **Non-blocking** — nhưng chặn việc viết TC biên cho nút *"Xem thêm trên Bảng tin"*.

## Khuyến nghị tổng thể
1. **Resolve trước generate-tc:** không CL nào là blocker cứng, nhưng `C-HOME-03` quyết định có viết được TC biên cho nút *"Xem thêm"* hay không ⇒ ưu tiên hỏi BA cùng lượt với `C-NTF-01`.
2. **Chạy sớm để tự đóng CL:** `SC-HOME-012` (Carrier có đơn) trả lời trực tiếp `C-HOME-02`; `SC-HOME-019` (≥6 tin) trả lời `C-HOME-03` về mặt hành vi thật.
3. **Cần môi trường/dữ liệu:** seed **≥6 tin cộng đồng** + **1 tài khoản trắng (0 đơn)** + **1 đơn cho mỗi vai** ⇒ 3 tài khoản test. Không có bộ này thì 10/24 SC bị blocked.
4. **ID/text cleanup (non-blocking, cần trước automation):** chốt tagline banner (`C-HOME-01(b)`) và thuật ngữ badge *"Đã ghép"* vs mốc progress *"Lấy hàng"* — 2 chữ cho 1 trạng thái `MATCHED`.
