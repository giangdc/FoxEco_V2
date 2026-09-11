# KP-06 — Danh mục tài liệu gốc & cách xử lý

> Liệt kê **chính xác** những file nào cần copy sang `00_input/v1.0/` của project mới, file nào bỏ, và cạm bẫy kỹ thuật khi đọc từng loại.

---

## 1. ⚠ Cạm bẫy kỹ thuật phải biết trước

### 1.1 File `.html` là "bundler export", KHÔNG phải HTML thường
`FoxEco BRD *.html` và `FoxEco Demo * .html` là bản export dạng bundler — nội dung thật nằm trong thẻ `<script type="__bundler/template">`, **phải giải nén thủ công** mới lấy được HTML gốc. Đợt cũ đã làm bước này bằng tay trước khi phân tích.

> ✅ **Tin tốt:** BRD đã có sẵn bản `.md` đã giải nén — **dùng thẳng `.md`, đừng đụng vào `.html`**.

### 1.2 Prototype HTML render bằng JS — gần như không đọc tĩnh được
`FoxEco Demo 3 vai tro (standalone) (2).html` render toàn bộ nội dung lúc runtime. Đợt cũ chỉ lấy được **duy nhất** literal `orderStatus` state map từ script `Component.renderVals()`. → **reference-only**, đừng kỳ vọng trích được text/field từ file này.

### 1.3 Ảnh Figma là MOCKUP, không phải screenshot máy thật
82 ảnh trong `Fox Eco Doc/images/` có status bar `9:41` — đó là **mẫu chuẩn Apple design**, không phải chụp thiết bị thật. Ảnh `Screenshot From 2026-07-27 15-23-25.png` cũng vậy.
→ Khi cần bằng chứng "app thật hoạt động thế nào", chỉ có **vibe-test** (`KP-01 §10`) mới tính.

### 1.4 Ảnh Figma đặt tên bằng hash, không có nhãn màn hình
Tên file là hash SHA (vd `570ad9d32e3dbdf44c72d6140826f0e6f9a3393e`) — **không biết ảnh nào là màn nào cho tới khi mở ra xem**.
> ⚠ **Bài học đắt giá của đợt cũ:** **59/82 ảnh chưa từng được mở ra xem** trong suốt nhiều phiên phân tích. Khi cuối cùng rà hết (2026-07-29) thì tìm được bằng chứng thật cho nhiều nhóm case vốn đang bị gắn nhãn sai nguồn *"Quan sát thực tế app"*.
> → **Project mới: rà đủ 82 ảnh NGAY từ đầu, lập index `hash → tên màn hình` trước khi viết scenario.**

---

## 2. ✅ Danh sách file CẦN copy sang project mới

> 📦 **Đã đóng gói sẵn:** toàn bộ tài liệu ở bảng dưới nằm trong `_handoff-v1.0/00_input-seed/docs/` — copy thẳng, không cần lần lại project cũ. Cột "File nguồn" giữ để truy xuất xuất xứ.

| Đề xuất DOC ID | File nguồn (đường dẫn trong project cũ) | Loại | Ghi chú |
|---|---|---|---|
| **DOC-v1.0-01** | `00_input/v1.0/27072026/FoxEco BRD v3.2.md` | Markdown | ⭐ **Nguồn chính.** Bản mới nhất. Dùng `.md` này, không dùng `.html` |
| **DOC-v1.0-02** | `00_input/v1.0/FoxEco Demo 3 vai tro (standalone)/tổng hợp từ file demo.docx` | Word | PRD tái dựng từ demo — nguồn bổ trợ chi tiết screen/field |
| **DOC-v1.0-03** | `00_input/v1.0/FoxEco Demo 3 vai tro (standalone)/FoxEco Demo 3 vai tro (standalone) (2).html` | HTML | Prototype tương tác 3 vai trò — **reference-only** |
| **DOC-v1.0-04** | `00_input/v1.0/Fox Eco Doc/images/*` (82 ảnh) + `canvas.fig` | Ảnh | ⭐ Nguồn thiết kế UI text/button **chính xác nhất hiện có** |
| **DOC-v1.0-05** | Thư mục `_knowledge-pack-v1.0/` này | Markdown | Kiến thức phi-tài-liệu (KP-01…KP-06) |

### 2.1 File nên copy kèm (tham khảo / lịch sử)
| File | Lý do giữ |
|---|---|
| `27072026/FoxEco BRD v3.1.md` | Bản trước — để tra khi cần biết điều gì đã đổi |
| `27072026/Screenshot From 2026-07-27 15-23-25.png` | Ảnh màn "Đơn của tôi" — nguồn của `KB-ORD-07`. ⚠ là mockup, không phải máy thật |
| `27072026/FoxEco Design v3.2.html` | Design doc — ⚠ **chưa từng được đăng ký làm DOC ở đợt cũ**; đã xác nhận nội dung không đổi so với `FoxEco Design.html` (chỉ khác UUID bundler). Nên kiểm tra xem có nội dung gì chưa được khai thác không |

### 2.2 File KHÔNG cần copy
| File | Lý do bỏ |
|---|---|
| `FoxEco BRD/FoxEco BRD v3.1 (1).html` · `27072026/FoxEco BRD v3.1.html` · `FoxEco BRD v3.2 .html` | Đã có bản `.md` tương ứng |
| `FoxEco Design.html` | Trùng nội dung với `FoxEco Design v3.2.html` |
| `.~lock.FoxEco_PRD.docx#` | File lock rác của LibreOffice |

---

## 3. Nội dung mới ở BRD v3.2 (so với v3.1)

> Đã diff xác nhận: **toàn bộ §A1–A10 và §D1–D7 giữ nguyên y hệt v3.1.** Khác biệt duy nhất là **thêm §D8**.

### §D8 · Validate & Giá trị mặc định (Form Rules)
| Mục | Nội dung |
|---|---|
| **D8.1** | Form "Đơn cần gửi hàng" (người gửi đăng tin) — Ghi chú **≤300** ký tự · Địa chỉ lấy/giao hàng **≤200** ký tự · Tên người nhận **2–60** ký tự |
| **D8.2** | Form "Tin nhận giao hàng / thuận đường" (OFFER) — Điểm xuất phát **≤200** ký tự · khung giờ tối thiểu cách nhau **30 phút** |
| **D8.3** | Quy tắc chung `VAL-01..05` — trong đó `VAL-04`: lý do huỷ là **text bắt buộc, tối thiểu 5 ký tự** |

**Ý nghĩa:** §D8 **resolve dứt điểm** phần maxlength còn TBD của `C-ORD-01`, và hé lộ cơ chế cảnh báo *"Giá trị hàng = Cao"* (khác với ngưỡng số tiền `BR-ORD-03` vẫn deferred).

---

## 4. Cấu trúc BRD v3.2 — bản đồ section để định vị nhanh

| Section | Nội dung | Nhóm ID requirement |
|---|---|---|
| `§A1` | Tổng quan & Bối cảnh | — |
| `§A2` | Nguyên tắc sản phẩm (áp cho cả 3 chức năng) | `NT-NN` |
| `§A3` | Bộ sản phẩm & Thứ tự ưu tiên | — (nhắc Admin Web Portal) |
| `§A4` | Mô hình "Tin Đăng" 2 chiều NEED/OFFER + **vòng đời status** | — |
| `§A5` | Tương tác 2 chiều & cơ chế kết nối (không chat) | `BR-CON-NN`, `BR-INT-NN` |
| `§A6` | Actors & Hồ sơ | `USR-NN` |
| `§A7` | Phần thưởng — Quà ảo | `GIFT-NN` |
| `§A8` | Pháp lý, Trách nhiệm & Trust/Safety | `TS-NN` |
| `§A10` | KPIs chung & Roadmap | — |
| `§D1` | Tổng quan & hai chiều đăng tin | — |
| **`§D1b`** | ⭐ **User Story — Gửi Hàng (toàn bộ vòng đời)**, có cột Acceptance Criteria riêng. 4 nhóm: Sender · Carrier(NEED) · Carrier(OFFER) · Hoàn tất/ngoài luồng | `US-DNN` |
| `§D2` | Workflow & Status Flow | — |
| `§D3` | Functional Requirements — Gửi Hàng | `ORD/ASN/DLV/GIFT/CNL/MTCH/LOC/RAT-NN` |
| `§D4` | Business Rules & Permission Matrix | `BR-<MODULE>-NN` |
| `§D5` | Edge Cases · Data Model · KPI | — |
| `§D6` | Thông báo (Notifications) | `NTF-NN` |
| `§D7` | Rule vận hành (Operating Rules) | `OPR-NN` |
| **`§D8`** | ⭐ Validate & Giá trị mặc định (**MỚI ở v3.2**) | `VAL-NN` |

---

## 5. Nguồn phi-tài-liệu — quy ước đặt nhãn

> Đợt cũ từng dùng **5 vocabulary khác nhau** cho cùng khái niệm "nguồn không phải tài liệu", bị review flag. Sau đó đã chuẩn hoá 27 dòng về 1 bộ nhãn. **Dùng lại bộ nhãn này ở project mới.**

Mỗi nhãn phải có đủ 3 phần: **(nguồn / ai) + (ngày) + (clarification ID & trạng thái)**

| Nhãn chuẩn | Dùng khi |
|---|---|
| `BA xác nhận qua trao đổi (chat), <ngày>` | BA/PO trả lời trực tiếp |
| `DOC-v1.0-04 — images/<hash>` | Có ảnh Figma cụ thể |
| `DOC-v1.0-02 §<mục>` | Tìm được nguồn văn bản thật |
| `Vibe-test <VR-ID>, <ngày>` | Quan sát trên app thật, có screenshot |
| `UI nền tảng (<loại>)` | Hành vi UI tất yếu, không cần BA chốt (vd scroll-load) |
| `Chờ BA bổ sung` | Chưa có nguồn nào |

⛔ **Tránh nhãn mơ hồ `"Quan sát thực tế app"`** — đợt cũ dùng nhãn này cho 42 dòng TC, khi rà lại thì phần lớn hoá ra là **BA trả lời qua chat** hoặc **có ảnh Figma thật**, chỉ một nhóm nhỏ là quan sát thật. Nhãn mơ hồ khiến không truy được nguồn gốc, phải đi rà lại toàn bộ.
