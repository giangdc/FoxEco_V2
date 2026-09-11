---
id: v1.0/HOME-trang-chu/changelog
title: Changelog — Module HOME
type: changelog
version: v1.0
sprint: 1
module:
  code: HOME
  dir: HOME-trang-chu
  name: Trang chủ
doc_source:
  - id: DOC-v1.0-02
    section: "§2 · §3.1 · §4.1 · §4.5 · §5.1 · §7"
  - id: DOC-v1.0-01
    section: "§A3 (L29) · §A6 (L102) · §D1b (US-D02, US-D06) · §D2 (L232) · §D7 (OPR-01)"
  - id: DOC-v1.0-06
    section: "KP-01 §3 (KB-ORD-07/08) · KP-05 §2.1 · §3 (#1,#2,#4,#5)"
id_range:
  req: REQ-HOME-001..010
  sc: "SC-HOME-001..024 (NEW)"
  cl: C-HOME-01..03
  risk: RISK-HOME-01..05
status: ANALYZED
updated: 2026-09-07
---

# Changelog — Module HOME (`HOME`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-07 | INIT | Phân tích lần đầu §2/§3.1/§4.1/§5.1 — 10 REQ (`001..010`), 24 SC, 3 CL, 5 RISK. Điểm nghiệp vụ đáng chú ý nhất: section "Đơn của tôi" **role-aware 3 nhãn** (`Gửi:`/`Giao:`/`Nhận:`) và mâu thuẫn **1 vs 5 tin** ở section "Tin mới" chưa ai chốt | `DOC-v1.0-02` §2/§3.1/§4.1/§5.1 · `DOC-v1.0-01` §D1b/§D2 · `DOC-v1.0-06` KP-01/KP-05 | Dựng đủ 5 deliverable + `CHANGELOG.md` |
| 2026-09-07 | REFACTOR | **Tách module mới khỏi `ORD`.** Đợt v1.0 cũ nhét toàn bộ màn Trang chủ vào `ORD` với đúng **1 scenario** (`SC-ORD-033` completeness) trong khi bộ TC có **32 TC** (sheet `TC_05`) ⇒ 31 TC không có SC đỡ lưng. Lượt này fan-out **24 SC** theo Scenario Sufficiency Rule | Quyết định QC GiangDC2 2026-09-07 (`Project_rule §Module Codes` ghi chú tách module) | ID cũ `SC-ORD-033` **không carry sang** — nội dung tương ứng nay là `SC-HOME-011..014` + `SC-HOME-008` |
| 2026-09-07 | INIT | Đóng 2 gap "không có nguồn tài liệu" của đợt cũ: nút **"Xem tất cả"** (`KP-05 §3 #1`) có nguồn `DOC-v1.0-02` §3.1 · nút **"Xem thêm trên Bảng tin"** (`KP-05 §3 #2`) có nguồn `US-D06` | Rà lại doc ở lượt INIT | `SC-HOME-016`, `SC-HOME-021` được viết TC khẳng định, không còn là gap |
| 2026-09-07 | INIT | Mở 3 CL: `C-HOME-01` (icon vai trò + tagline lệch) · `C-HOME-02` (ẩn theo điều kiện hay vai trò) · `C-HOME-03` (1 vs 5 tin — kế thừa `KP-05 §2.1`) | Đối chiếu chéo 3 nguồn | 3 SC dạng GAP: `SC-HOME-004`, `SC-HOME-019`, `SC-HOME-024` |
| 2026-09-07 | REFACTOR | Đổi tên thư mục module `HOME/` → `HOME-trang-chu/` — tên gợi nghĩa để người mới đọc thư mục là biết chức năng. Cập nhật kèm: frontmatter `id:` của 5 deliverable + `module.dir` ở file này + mọi cross-ref `HOME/<file>.md` | Yêu cầu QC GiangDC2 2026-09-07 (mã 2–4 chữ không nói lên chức năng) · `Project_rule §Module Codes` nay có cột `Dir` riêng | ⛔ **Mã module `HOME` và toàn bộ ID (`REQ-HOME-*` · `SC-HOME-*`) KHÔNG đổi** — chỉ đường dẫn thư mục đổi. TC chưa sinh nên không TC nào bị ảnh hưởng |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **KHÔNG assert số tin ở section "Tin mới"** (1 hay 5) | `C-HOME-03` Open — 2 nguồn 2 con số | TC chọn 1 con số ⇒ 50% khả năng FAIL và bị log thành bug oan; đợt cũ đã cố ý né đúng điểm này |
| 2 | ⛔ **KHÔNG lấy hành vi bản demo làm oracle** | `DOC-v1.0-02` §4.5/§7 tự khai demo có dữ liệu mẫu **sai** (Carrier chưa nhận đơn vẫn thấy đơn "Chờ ghép"; 3 tài khoản cùng bộ chỉ số 12/4.8/540) | Sinh TC khẳng định hành vi lỗi của demo là đúng ⇒ app đúng lại bị báo FAIL |
| 3 | ⛔ **KHÔNG assert giá trị số** ở card "Đóng góp của bạn" và thống kê cộng đồng | Là `Runtime` toàn hệ thống, không seed được | TC hardcode số ⇒ FAIL ngay lượt chạy sau |
| 4 | ⛔ **KHÔNG assert icon vai trò cụ thể** ở header | Không nguồn nào có mapping icon↔vai (`C-HOME-01`) | Vi phạm `§Custom Rules §10.1` — viết TC khẳng định UI chưa xác nhận |
| 5 | ⚠️ **Badge trạng thái và mốc progress dùng 2 chữ khác nhau cho cùng `MATCHED`** — badge *"Đã ghép"*, progress *"Lấy hàng"* | `DOC-v1.0-06` KP-01 §5.1 ghi rõ lưu ý thuật ngữ này | TC đòi 2 chỗ cùng một chữ sẽ FAIL ở 1 trong 2 chỗ, và người đọc kết luận sai là app hiện sai trạng thái |
| 6 | ⚠️ **`SC-HOME-002` chỉ assert đúng 5 màn con được nêu tên** | Doc kết thúc danh sách bằng `"..."` ⇒ danh sách không đóng | Suy rộng thành "mọi màn con" ⇒ FAIL ở màn con doc không nói tới, không có cơ sở phán quyết |
| 7 | ⛔ **`SC-HOME-011..013` KHÔNG được gộp thành 1 SC "đổi vai trò xem nhãn"** | 3 vai = 3 tiền đề dữ liệu khác nhau (3 tài khoản), theo Scenario Sufficiency Rule | FAIL không chỉ ra được vai nào sai nhãn; lặp lại đúng lỗi mà `§Custom Rules §10.2` sinh ra để chặn |

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 `C-HOME-03` — số tin section "Tin mới" (1 vs 5) | Kế thừa từ 2026-07, BA chưa trả lời | Hỏi BA cùng lượt `C-NTF-01`; hoặc chạy `SC-HOME-019` với ≥6 tin để có số thật rồi `/analyze --update` |
| 2 | 🟡 `C-HOME-02` — điều kiện ẩn section "Đơn của tôi" | Chưa hỏi BA (mới mở 2026-09-07) | **Chạy `SC-HOME-012` trước** (Carrier có đơn) — tự trả lời được, không cần BA |
| 3 | 🟡 `C-HOME-01` — icon vai trò + tagline lệch 2 doc | Chưa hỏi BA | Hỏi BA; vibe-test 3 vai để có ảnh icon làm đầu vào |
| 4 | 🟡 Hành vi Trang chủ khi có **≥2 đơn đang hoạt động** — không có đặc tả (demo chỉ 1 đơn) | `RISK-HOME-03` Open | Tạo 2 đơn song song trên STG khi execute; phát hiện quy tắc chọn đơn → mở CL mới |
| 5 | 🟡 Empty state Trang chủ chưa có oracle | Residual `C-ORD-06` (Open) | Ghi nhận khi execute; đồng bộ cùng `SC-ACT-014`/`SC-NTF-015`/`SC-GIFT-008` |
