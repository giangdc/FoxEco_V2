---
id: v1.0/ORD-dang-tin/changelog
title: Changelog — Module ORD
type: changelog
version: v1.0
sprint: 1
module:
  code: ORD
  dir: ORD-dang-tin
  name: Đăng tin & Quản lý tin
doc_source:
  - id: DOC-v1.0-01
    section: "§A8 · §D3 (ORD-01/02/04/06/09/10, LOC-03, USR-EML) · §D4 (BR-ORD-03/04, BR-EDIT-01) · §D5 · §D7 (OPR-10) · §D1b (US-D01/D02/D04/D10/D11/D18/D19) · §D8.1 · §D8.2 · §D8.3"
  - id: DOC-v1.0-02
    section: "§3.5 · §3.5.1 · §3.5.2 · §3.5.3 · §3.5.4 · §4.4 · §7 (dòng 2, 3)"
  - id: DOC-v1.0-04
    section: "ảnh màn Đăng tin mới (f821ba30…) · 2 biến thể màn Đăng tin thành công"
  - id: DOC-v1.0-06
    section: "KP-01 §3 (KB-ORD-01..06, 10, 11) · §10.2..§10.11 (KB-VIBE-01..10) · KP-02 §2/§3/§5 · KP-05 §1/§2.2"
id_range:
  req: REQ-ORD-001..022
  sc: "SC-ORD-001..051 (NEW)"
  cl: "C-ORD-01..05, C-ORD-08..12"
  risk: RISK-ORD-01..08
status: ANALYZED
updated: 2026-09-07
---

# Changelog — Module ORD (`ORD`)

> **Đích write-back của LỊCH SỬ.** Mọi lượt chạm module này ghi **1 dòng ở §1**.

## 1. Lịch sử thay đổi

| Ngày | Loại | Thay đổi | Nguồn / Lý do | Ảnh hưởng |
|---|---|---|---|---|
| 2026-09-17 | ĐÍNH CHÍNH | **Gắn cảnh báo HẾT HIỆU LỰC cho `SC-ORD-019`** (*"email không tra thấy → hiện 'Không tìm thấy · nhập thủ công', 3 ô để trống cho user nhập"*). BA `C-ORD-14` (2026-09-17, home `v1.1/ORD-dang-tin/`) chốt ngược: **nút "Tiếp theo" DISABLE, KHÔNG cho tạo đơn**. Bản hiện hành là `SC-ORD-059` ở v1.1 | BA trả lời `C-ORD-14` 2026-09-17 · rà chéo khi QC trả bài | `counts` không đổi (SC vẫn còn để truy vết v1.0). ⚠️ **`TC-ORD-020`** (`03_test-cases/v1.0/fragments/TC-ORD-v1.0.md`) sinh từ SC này ⇒ **sẽ được thay** khi `generate-tc` chạy cho `ORD` v1.1; ⛔ không chạy TC đó cho v1.1 |
| 2026-09-17 | UPDATE | **Bổ sung bằng chứng UI Bước 1/3 vào 5 SC (home ở v1.0), theo ảnh QC cung cấp.** `SC-ORD-008/009/010` — nhãn đầy đủ **"GIÁ TRỊ HÀNG (ƯỚC TÍNH)"**, 3 chip có **mốc tiền** (`Dưới 1 triệu đ` / `1 – 5 triệu đ` / `Trên 5 triệu đ`) — ⛔ **GHI NHẬN, không assert cứng** vì PRD chưa có con số (`C-ORD-18`, home ở `v1.1/ORD-dang-tin/`); kiểu control là **chip**, không phải dropdown. `SC-ORD-011` — ô Ghi chú nằm **block đầu tiên** + placeholder nguyên văn. `SC-ORD-012` — khối **"ẢNH HÀNG \*"** có bộ đếm "0/5" + helper bắt buộc ≥1/tối đa 5 | Ảnh UI demo `00_input/v1.1/design/gia tri hang uoc tinh.png` (`DOC-v1.1-03`), QC GiangDC2 cung cấp 2026-09-17 | `counts` không đổi (không thêm/bớt SC, không đổi priority); chỉ siết Given/Steps + thêm rào GHI NHẬN. `C-ORD-02` **KHÔNG bị đảo** — mốc tiền là nhãn phụ, không phải ngưỡng cấu hình `BR-ORD-03` |
| 2026-09-17 | UPDATE | 🔁 **ĐÍNH CHÍNH dòng ngay trên — rào *"GHI NHẬN, không assert cứng"* cho mốc tiền HẾT HIỆU LỰC cùng ngày.** BA chốt 3 mốc tiền `Dưới 1 triệu đ` / `1 – 5 triệu đ` / `Trên 5 triệu đ` là **CON SỐ CHÍNH THỨC** ⇒ `SC-ORD-008/009/010` **assert cứng**; kiểu control **chip** và vị trí block Ghi chú trên cùng cũng được BA xác nhận đúng thiết kế (*"lấy UI làm chuẩn"*) ⇒ `SC-ORD-011` assert cứng vị trí + **textbox nhập được**. ⛔ Đừng trích lại rào cũ | BA trả lời `C-ORD-18` 2026-09-17 (home ở `../../v1.1/ORD-dang-tin/risk_assessment.md`) · QC GiangDC2 chuyển lời | `counts` không đổi. 4 SC này là **CARRIED** ở v1.1 nên chưa chính thức hoá MODIFIED — ghi nợ ở `../../v1.1/ORD-dang-tin/CHANGELOG.md §3` #7 |
| 2026-09-07 | INIT | Phân tích lần đầu §D3/§D8.1/§D8.2/§D8.3 + §3.5 — 22 REQ (`001..022`), 51 SC, 10 CL (4 mới), 8 RISK. Điểm nghiệp vụ đáng chú ý nhất: **3 mâu thuẫn giá trị mặc định** (chip Loại hàng · checkbox điều khoản · cơ chế field địa chỉ) và **4 nghi vấn bug đã có screenshot** ở nhóm Người gửi / auto-fill người nhận | `DOC-v1.0-01` §D3/§D4/§D8 · `DOC-v1.0-02` §3.5 · `DOC-v1.0-06` KP-01 §3/§10 | Dựng đủ 5 deliverable + `CHANGELOG.md` |
| 2026-09-07 | REFACTOR | **Thu hẹp phạm vi module.** Đợt v1.0 cũ để `ORD` gánh 3 màn (Đăng tin + Hoạt động + Trang chủ): 33 SC / 161 TC. Lượt này `ORD` chỉ còn Đăng tin & Quản lý tin; Trang chủ → `HOME`, Hoạt động → `ACT` | Quyết định QC GiangDC2 2026-09-07 | Dải `SC-ORD-*` được **đánh lại từ 001**; ⛔ ID cũ (`SC-ORD-015..026` = Hoạt động, `SC-ORD-033` = Trang chủ) **KHÔNG** map 1-1 sang dải mới |
| 2026-09-07 | INIT | Mở 4 CL mới: `C-ORD-09` (danh mục Loại hàng — nâng từ câu hỏi `KP-05 §1` #3 thành CL chính thức) · `C-ORD-10` (địa chỉ pre-fill: bug hay dữ liệu tài khoản) · `C-ORD-11` (3 cơ chế field địa chỉ) · `C-ORD-12` (mặc định checkbox) | Đối chiếu chéo BRD ↔ PRD ↔ vibe-test | 4 SC dạng GAP: `SC-ORD-006`, `SC-ORD-016`, `SC-ORD-027`, `SC-ORD-033` |
| 2026-09-07 | UPDATE | **Đóng `C-ORD-12`** — chốt mặc định checkbox điều khoản = **CHƯA tick** theo `D8.1` + quan sát app (VR-001 finding #2), thắng nhánh PRD *"tick sẵn"* | BRD v3.2 mới hơn PRD + có bằng chứng app | `SC-ORD-033` assert "chưa tick"; kỳ vọng của TC `TC_04.71` đợt cũ là **sai nguồn**, phải sửa nếu migrate |
| 2026-09-07 | REFACTOR | Đổi tên thư mục module `ORD/` → `ORD-dang-tin/` — tên gợi nghĩa để người mới đọc thư mục là biết chức năng. Cập nhật kèm: frontmatter `id:` của 5 deliverable + `module.dir` ở file này + mọi cross-ref `ORD/<file>.md` | Yêu cầu QC GiangDC2 2026-09-07 (mã 2–4 chữ không nói lên chức năng) · `Project_rule §Module Codes` nay có cột `Dir` riêng | ⛔ **Mã module `ORD` và toàn bộ ID (`REQ-ORD-*` · `SC-ORD-*`) KHÔNG đổi** — chỉ đường dẫn thư mục đổi. TC chưa sinh nên không TC nào bị ảnh hưởng |

## 2. Ràng buộc còn hiệu lực

| # | Ràng buộc | Vì sao | Hệ quả nếu vi phạm |
|---|---|---|---|
| 1 | ⛔ **KHÔNG dùng nhãn "Tài liệu"** cho chip Loại hàng — app STG có 8 chip, mặc định **"Giấy tờ, hồ sơ"**, và **không có** chip nào tên "Tài liệu" | `KP-01` §10.2 `KB-VIBE-01` (VR-002 `TC_04.5` FAIL, có screenshot) | Lỗi lan rộng nhất của đợt v1.0 cũ: hàng chục TC FAIL vì sai chữ, che mất bug thật, và tester mất niềm tin vào bộ TC |
| 2 | ⛔ **KHÔNG hardcode khung giờ** — chọn tương đối so với "now" | App validate theo đồng hồ thật; mặc định hết hạn nếu form mở ~15 phút (`KP-01` §10.11) | TC FAIL ngẫu nhiên theo thời điểm chạy, bị chẩn đoán sai thành bug app |
| 3 | ⛔ **KHÔNG viết TC negative "chọn Thuốc/Y tế → bị chặn"** | `C-ORD-04` Resolved: v1.0 **không chặn** hàng cấm; banner chỉ là thông tin tĩnh | TC không bao giờ PASS và không ai fix — vì rule chưa được triển khai, không phải bug |
| 4 | ⛔ **KHÔNG viết TC negative "để trống Loại hàng → chặn"** | Chip luôn có 1 giá trị mặc định và **không deselect được** ⇒ precondition không tái hiện được (`KP-01` §10.3) | Đúng lỗi VR-002 `TC_04.6` FAIL của đợt cũ: FAIL vì không lập được tiền đề, không phải vì app sai |
| 5 | ⛔ **`SC-ORD-015/016/017/021/022` viết theo SPEC, không theo hành vi app** — dự kiến FAIL và FAIL là kết quả đúng | 4 nghi vấn bug đã có screenshot (`KP-01` §10.5/§10.6/§10.9/§10.10) + `C-ORD-01` Resolved | "Sửa expected cho PASS" = hợp thức hoá lỗ validate (đơn không có người nhận) và các bug pre-fill; bug sẽ không bao giờ được log |
| 6 | ⚠️ **Khoá chỉnh sửa tin từ `MATCHED`** (theo `BR-EDIT-01`+`OPR-10`), ⛔ KHÔNG theo `US-D19` (*"sau IN_TRANSIT"*) | 2 rule chuyên trách đồng thuận, `US-D19` lệch 1 trạng thái | Cho sửa tin ở MATCHED = sửa đơn sau khi đã có người nhận ⇒ Carrier đi lấy hàng sai địa chỉ/sai hàng |
| 7 | ⚠️ **Tin tự chuyển `EXPIRED`** tại "Đến ngày" (theo `US-D04`), ⛔ KHÔNG theo `ORD-06` (*"hệ thống không tự can thiệp"*) | `C-ORD-03` Resolved theo `US-D04` + app | TC chờ user tự gỡ tin ⇒ không bao giờ quan sát được trạng thái Hết hạn tự động |
| 8 | ⚠️ **Altitude của SC ở form nhiều trường:** SC dừng ở mức **rule/hành vi**; EP/BVA **từng trường** thuộc `generate-tc --mode comprehensive` (`B1`/`B2`) | Nếu fan-out 1 SC/giá trị biên thì riêng ORD đã ~120 SC, scenario map thành bảng dữ liệu chứ không còn là bản đồ hành vi | Hai cách hiểu khác nhau giữa các lượt phân tích ⇒ số SC nhảy loạn giữa các version, `health-check` báo drift |
| 9 | ⚠️ **Địa chỉ phải TAP CHỌN gợi ý mới lưu** — `set text` đơn thuần không lưu giá trị | `KP-01` §3 `KB-ORD-06` (BA + 2 lần vibe-test) | TC/script tưởng đã nhập địa chỉ nhưng field rỗng ⇒ FAIL ở bước submit với lý do khó truy |
| 10 | ⚠️ **Sau `SC-ORD-015` phải reset phiên wizard** — giá trị Tên bị xoá không tự phục hồi trong cùng phiên | `KP-01` §10.5: *"phải thoát ra vào lại từ đầu Bước 1/3 mới load lại tên"* | Các TC chạy sau bị FAIL dây chuyền vì field Tên rỗng, không liên quan tới nội dung TC đó |

### 🔁 Kết luận bị đảo (khi có)

> ⛔ Kết luận **"hạn tin = giá trị Từ ngày"** (bản phân tích trước, nguồn: phân tích của QC anhdc4) **HẾT HIỆU LỰC — đừng trích lại**; hiện hành là **"hạn tin = giá trị Đến ngày user chọn"** (`C-ORD-03` Resolved 2026-07-27, khớp `D8.1` L371 + `KP-01` §3 KB-ORD-02).
> ⛔ Kết luận **"checkbox điều khoản mặc định tick sẵn"** (bản `DOC-v1.0-02` §3.5.3, dùng trong TC `TC_04.71` đợt cũ) **HẾT HIỆU LỰC — đừng trích lại**; hiện hành là **"mặc định CHƯA tick"** (`C-ORD-12` Resolved 2026-09-07, nguồn `D8.1` L373 + app STG).

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | 🔴 `C-ORD-09` — danh mục "Loại hàng" (3 nguồn 3 danh mục, app không có "Tài liệu") | Chờ BA/Dev; là câu hỏi ưu tiên #1 của cả dự án (`KP-05 §1` #3) | Hỏi BA/Dev; tới khi đó `SC-ORD-006` ghi nhận danh mục thật, mọi TC dùng nhãn app |
| 2 | 🔴 `C-ORD-10` — địa chỉ lấy hàng không pre-fill: bug hay tài khoản test chưa cấu hình? | Chờ dev xác nhận hồ sơ tài khoản test | Hỏi dev; hoặc test bằng tài khoản thứ hai **chắc chắn có** nơi làm việc → `/analyze --update` |
| 3 | 🔴 **4 nghi vấn bug chưa log Jira** (Tên không read-only · địa chỉ không pre-fill · SĐT tự đổi · app báo lỗi SĐT nó tự điền) | Đợt v1.0 cũ có screenshot nhưng **chưa log** (`KP-05 §5`) | Chạy `SC-ORD-015/016/017/021` → `/log-bug`; riêng `016` chờ `C-ORD-10` |
| 4 | 🟡 `C-ORD-05` — có "Mã tin" ở màn Đăng tin thành công hay không | Kế thừa từ 2026-07, BA chưa trả lời | Hỏi BA; `SC-ORD-038` ghi nhận, không assert |
| 5 | 🟡 `C-ORD-08` — thoát/Reset giữa wizard có xoá form | Kế thừa, chưa hỏi BA | Hỏi BA; lưu ý liên quan bug `SC-ORD-015` (thoát/vào lại mới load lại tên) |
| 6 | 🟡 `C-ORD-11` — `LOC-03` (preset 6 văn phòng) còn hiệu lực ở v1.0 hay đã bị autocomplete thay thế | Chưa hỏi BA (mới mở 2026-09-07) | Hỏi BA; `SC-ORD-027` ghi nhận cơ chế thật |
| 7 | 🟡 Đơn có **"Đến ngày" đã trôi qua** — không seed được qua UI | `RISK-ORD-06` Open | Nhờ dev/QA seed trên STG trước khi execute `SC-ORD-045` |
