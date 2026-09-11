# KP-05 — Câu hỏi treo, mâu thuẫn nguồn & gap chưa xử lý

> Đây là **danh sách việc còn dang dở** của đợt phân tích cũ. Ở project mới, nạp thẳng phần này thành clarification / backlog ngay từ đầu thay vì để phát hiện lại từ đầu.

---

## 1. Câu hỏi treo với PM/BA (ưu tiên hỏi trước khi analyze)

| # | Câu hỏi | Người trả lời | Ảnh hưởng nếu không có |
|---|---|---|---|
| 1 | Scope Phase 1 luồng **Ghép nối** có gồm **auto-match OFFER↔NEED** hay chỉ luồng thủ công? | PM | Không xác định được có viết TC cho auto-match không (đợt cũ: 1 scenario không có TC vì lý do này) |
| 2 | Scope Phase 1 luồng **Xác nhận nhận hàng** có gồm **ảnh bằng chứng / GPS / chi phí / báo sự cố** hay chỉ core confirm? | PM | Ảnh hưởng ~4-6 scenario nhánh phụ DLV |
| 3 | Chip **"Tài liệu"** trong tài liệu vs **"Giấy tờ, hồ sơ"** trên app thật — UI đổi tên hay tài liệu sai? | BA / Dev | ⭐ **Ảnh hưởng lan rộng nhất** — mọi TC nhắc "Tài liệu" đều sai chữ |
| 4 | Địa chỉ lấy hàng có phải pre-fill mặc định không, hay tài khoản test chưa cấu hình? | Dev | Quyết định `TC_04.21` là bug hay TC sai |
| 5 | Danh sách **9 loại thông báo chính thức** (`C-NTF-01`) | BA | Không viết được TC nội dung thông báo |
| 6 | Text **empty state** của 3 màn (Hoạt động / Quà đã nhận / Thông báo) (`C-ORD-06`) | BA | Không assert được text cụ thể |
| 7 | Cơ chế **"Đánh dấu đã đọc"** — mark-all hay mark-per-item (`C-NTF-03a`) | BA | |
| 8 | **"Khung giờ phù hợp"** khi khớp tuyến — trùng hoàn toàn hay có độ lệch? Chu kỳ quét? (`C-NTF-02`) | BA | |
| 9 | Default **bật/tắt chia sẻ vị trí** (`C-DLV-02`) | BA | |
| 10 | Bấm Reset/thoát giữa chừng wizard có xoá form không (`C-ORD-08`) | BA | |

---

## 2. Mâu thuẫn nguồn chưa giải quyết

### 2.1 ⭐ Số lượng tin ở section "Tin mới" (Trang chủ)
| Nguồn | Nội dung |
|---|---|
| `DOC-v1.0-02 §3.1 Table 3` (PRD) | *"Rút gọn **1 tin mới nhất** của CẢ CỘNG ĐỒNG"* |
| `DOC-v1.0-01 §D7 OPR-01` / `US-D06` (BRD) | *"Chỉ hiện **tối đa 5 tin**"* |

**Cách xử lý ở đợt cũ:** TC completeness **cố ý không assert số lượng**; 3 TC biên viết theo trần 5 của BRD. → `C-ORD-07` mở ra từ đây (nhưng chỉ giải quyết được vế "Sender có thấy không", chưa giải quyết vế số lượng).

### 2.2 Màn "Đăng tin thành công!" — 2 biến thể trên cùng board Figma
Một bản **CÓ** trường "Mã tin" (vd `#ECO-2026-0451`), một bản **KHÔNG**. Đồng thời đối lập trực tiếp với `US-D02`: *"KHÔNG hiển thị mã đơn — mã kỹ thuật vô nghĩa với người dùng"*. → `C-ORD-05` Open.

### 2.3 Ai xác nhận "Đã nhận hàng" (đã giải quyết, ghi lại để không lặp)
`DLV-03` (§D3) ghi RECEIVER/**SENDER** vs `BR-INT-03` (§A5) + demo §5.2 chỉ Receiver. → Figma xác nhận **Receiver-only** (`C-DLV-01` Resolved).

### 2.4 Tier / điểm số ở màn Cá nhân (đã giải quyết)
BRD nói không có điểm/tier/CO₂ · demo nói có đủ · Figma cho kết quả **trung gian** (có badge text, không có số). → `C-USR-01` Resolved out-of-scope.

---

## 3. 6 nhóm case chưa có nguồn tài liệu (từ đợt merge với QC anhdc4)

> Các case này **có trong bộ TC của QC anhdc4** nhưng project GiangDC2 **không tìm được nguồn tài liệu** → theo custom rule §10.1 đã **cố ý KHÔNG viết TC**, để lại chờ đợt phân tích sau. **Đây chính là "đợt phân tích sau" đó.**

| # | Case | Vấn đề |
|---|---|---|
| 1 | Nút **"Xem tất cả"** tại section "Đơn của tôi" (Trang chủ) | Không có mô tả trong BRD/PRD |
| 2 | Nút **"Xem thêm trên Bảng tin"** + rule hiện/ẩn theo 5 vs ≥6 tin | Không có mô tả |
| 3 | **Carrier KHÔNG thấy section "Đơn của tôi"** — ẩn theo **VAI TRÒ** | Doc hiện chỉ nói ẩn theo "có/không có đơn đang hoạt động", không nói theo vai trò |
| 4 | **Empty state màn Trang chủ** | Trùng `C-ORD-06` (Open) |
| 5 | **Icon vai trò ở Header khác nhau** theo Sender/Carrier/Receiver | Chưa có bằng chứng UI mapping |
| 6 | Nút back (←) ở màn Thông báo quay về Trang chủ | Thuộc bề mặt màn Thông báo |

---

## 4. 4 test case CỐ Ý viết để FAIL (bắt gap thật)

> Đây **không phải TC sai** — là TC viết theo rule đúng để chứng minh hành vi app hiện tại là gap cần dev fix. Project mới nên viết lại tương đương.

| TC ID (đợt cũ) | Nội dung | Rule bị vi phạm |
|---|---|---|
| `TC_08.7` | Lý do huỷ **4 ký tự** vẫn bật được nút | `VAL-04` yêu cầu tối thiểu 5 ký tự — UI chỉ chặn rỗng |
| `TC_08.10` | Lý do huỷ **5 dấu cách** vẫn bật được nút | Không trim khoảng trắng trước khi đếm độ dài |
| `TC_08.22` | **Huỷ đơn** không ghi log LỊCH SỬ | `C-CNL-02` — user chốt PHẢI ghi log |
| `TC_08.23` | **Huỷ nhận đơn** không ghi log LỊCH SỬ (còn xoá dòng "Ghép thành công") | `C-CNL-02` |

> ⚠ Lịch sử: tài liệu đợt cũ từng ghi nhầm ID là `TC_08.24/25`, đã sửa lại đúng thành `TC_08.22/23` ngày 2026-07-30.

---

## 5. Bug / nghi vấn bug phát hiện trên app thật — CHƯA LOG

> Thư mục `05_bug-reports/` của project cũ **trống** — chưa bug nào được log chính thức. Danh sách dưới đây là findings từ vibe-test cần được xử lý ở project mới.

| # | Nghi vấn | Mức | Bằng chứng | Xem thêm |
|---|---|---|---|---|
| 1 | **Tên Người gửi edit được và bị xoá trắng khi chạm** — không tự phục hồi trong phiên | 🔴 Cao | VR-002 `TC_04.22` FAIL + screenshot | `KP-01 §10.5` |
| 2 | **Địa chỉ lấy hàng không pre-fill** | 🟠 TB | VR-002 `TC_04.21` FAIL | `KP-01 §10.6` |
| 3 | **Checkbox điều khoản không tick sẵn** (trái expected) | 🟠 TB | VR-001 finding #2 | `KP-01 §10.7` |
| 4 | **App báo "SĐT không hợp lệ" cho giá trị chính nó auto-fill** (`0000286248`) | 🟠 TB | VR-002 `TC_04.24` note | `KP-01 §10.9` |
| 5 | **SĐT Người gửi tự đổi giá trị giữa phiên** (`0000142378` → `0964633313`) | 🟡 Thấp | VR-001 finding #4 | `KP-01 §10.10` |
| 6 | **SĐT lộ sớm ở "Chờ ghép"** trên prototype | 🟠 TB | BA xác nhận là bug (`C-ASN-01`) | `KP-01 §4` |
| 7 | **Cho phép tự nhận mang giúp tin của mình** trên prototype | 🟠 TB | BA xác nhận là bug (`C-ASN-02`) | `KP-01 §4` |
| 8 | **Huỷ đơn / Huỷ nhận đơn không ghi log LỊCH SỬ** | 🟠 TB | CA live-verify + user chốt (`C-CNL-02`) | `KP-01 §7` |
| 9 | **Nút back màn "Tặng quà" nhảy sang đơn khác** | 🟡 Thấp | CA quan sát (`C-GIFT-02`) | `KP-01 §6` |

---

## 6. Việc dở dang khác

| Việc | Trạng thái |
|---|---|
| Vibe-test module Đăng tin (TC_04) | Dừng ở `TC_04.25` do thiết bị đen màn hình — **~58 TC High+Medium còn lại chưa chạy** |
| Vibe-test 8 module còn lại (TC_01, 02, 03, 05–09) | **Chưa chạy TC nào** |
| `TC_04.89`, `TC_04.106` | BLOCKED — cần đơn ở trạng thái `Đã ghép` (phải nhờ seed data) |
| `TC_02.16`, `TC_02.17` (màn "Quà đã nhận") | Viết dựa trên **bằng chứng văn bản `US-D20`** thôi, chưa có ảnh Figma/app → **cần vibe-test xác nhận**. `TC_02.17` đã ghi rõ: nếu app không có danh sách lịch sử thì FAIL + mở clarification |
| 2 Block Definition mới (Trang chủ, Bảng tin) thêm 2026-07-29 | **Chưa cross-check** với ảnh Figma / app STG |
| Convention technique tag | 213 tag dùng dạng `EP-…` thay vì `B1-EP-…` — nhất quán 100% nhưng nên chốt convention ở skill trước khi sửa hàng loạt |
| `review-tc` chạy Direct mode | Thiếu `review-agent/AGENT.md` → score cap 85, mang bias self-review. **Project mới nên đảm bảo có file này** để review độc lập thật |
