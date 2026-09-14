---
id: v1.0/HOME-trang-chu/scenario-map
title: Test Scenario Map — v1.0 · Module HOME
type: scenario-map
version: v1.0
sprint: 1
module: HOME
counts:
  req: 10
  sc: 24
  new: 24
  modified: 0
  carried: 0
  deprecated: 0
  p1: 1
  p2: 12
  p3: 11
status: ANALYZED
updated: 2026-09-14
---

# Test Scenario Map — v1.0 · Module HOME

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module HOME.
> ⚠️ Đợt v1.0 cũ: cả màn Trang chủ chỉ có **1 scenario** (`SC-ORD-033` completeness) nhưng **32 TC** — lượt này fan-out đúng luật.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Sàn tối thiểu/REQ: ≥1 positive + ≥1 negative (nếu có rule) + boundary (nếu có range).
> Fan-out mỗi role · mỗi state-transition · mỗi lớp EP · mỗi boundary · mỗi nhánh lỗi = 1 SC.
> Trần: display-only/Phase-2/duplicate → `coverage-gap-report.md`, KHÔNG tạo SC rác.

## Tổng quan
- Tổng số scenarios: **24** (NEW: 24, MODIFIED: 0, CARRIED: 0, DEPRECATED: 0)
- Phân bổ priority: P1: 1 | P2: 11 | P3: 12
- Chiều fan-out chính: **vai trò** (nhãn section "Đơn của tôi" × 3 vai) và **điều kiện hiển thị** (có/không đơn · có/không tin chưa đọc).

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### HOME — Trang chủ

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-HOME-001 | Bottom nav | REQ-HOME-001 | DOC-v1.0-02 §2 | Đã vào SDK FoxEco | Quan sát thanh tab dưới cùng ở màn Trang chủ | Đủ 5 tab đúng thứ tự: Trang chủ · Bảng tin · [+ Đăng tin] · Hoạt động · Cá nhân; tab "Trang chủ" đang active | P1 | UI | NEW |
| SC-HOME-002 | Bottom nav ở màn con | REQ-HOME-001 | DOC-v1.0-02 §2 | Đang ở Trang chủ | Mở lần lượt Chi tiết tin · Theo dõi đơn · wizard Đăng tin · Thông báo · Tặng quà | Mọi màn con KHÔNG hiển thị bottom nav, chỉ có nút quay lại (←) | P3 | UI | NEW |
| SC-HOME-003 | Header — lời chào | REQ-HOME-002 | DOC-v1.0-02 §2 dòng "Header" | Đăng nhập bằng tài khoản có tên hiển thị trong hồ sơ | Mở Trang chủ | Header hiển thị "Xin chào, <tên tài khoản>" đúng tên hồ sơ nhân viên | P2 | UI | NEW |
| SC-HOME-004 | [GAP] Icon vai trò header | REQ-HOME-002 | DOC-v1.0-06 KP-05 §3 (#5) | Doc nêu header có "Icon vai trò" nhưng chưa có mapping icon↔vai trò | Quan sát icon header ở 3 tài khoản đang giữ 3 vai khác nhau | GHI NHẬN icon thực tế của từng vai; KHÔNG assert icon cụ thể (C-HOME-01) | P3 | UI | NEW |
| SC-HOME-005 | Chuông — có tin chưa đọc | REQ-HOME-002 | DOC-v1.0-02 §2 dòng "Header" | Tài khoản có ≥1 thông báo chưa đọc | Mở Trang chủ | Icon chuông hiển thị chấm đỏ | P2 | UI | NEW |
| SC-HOME-006 | Chuông — đã đọc hết | REQ-HOME-002 | DOC-v1.0-02 §2 dòng "Header" | Tài khoản đã đọc hết thông báo | Mở Trang chủ | Icon chuông KHÔNG có chấm đỏ | P3 | UI | NEW |
| SC-HOME-007 | Banner tĩnh | REQ-HOME-003 | DOC-v1.0-02 §2 dòng "Banner quảng bá" | Đang ở Trang chủ | Quan sát rồi bấm vào banner | Banner hiện tagline + logo "FOX ECO"; bấm KHÔNG phát sinh điều hướng/hành vi nào | P3 | UI | NEW |
| SC-HOME-008 | Card "Đóng góp của bạn" | REQ-HOME-004 | DOC-v1.0-02 §2 · DOC-v1.0-01 §A6 L102 | Tài khoản đã giúp N đơn | Mở Trang chủ | Card hiện số đơn đã giúp (cỡ lớn) + dòng "Cộng đồng FoxEco: [x] đơn · [y] người"; KHÔNG hiện CO₂/điểm ECO | P2 | Business Rule | NEW |
| SC-HOME-009 | Section "Đơn của tôi" — có đơn | REQ-HOME-005 | DOC-v1.0-02 §3.1 dòng "Đơn của tôi" | Tài khoản đang có 1 đơn ở trạng thái hoạt động (Chờ ghép..Đã giao) | Mở Trang chủ | Section hiện đủ: nhãn vai + loại hàng\|giá trị · badge trạng thái · "Từ:"/"Đến:" · thanh progress 5 bước · dòng "Chạm để theo dõi đơn của bạn" | P2 | UI | NEW |
| SC-HOME-010 | Section "Đơn của tôi" — không đơn | REQ-HOME-005 | DOC-v1.0-02 §3.1 · §4.1 | Tài khoản KHÔNG có đơn đang hoạt động | Mở Trang chủ | Section "Đơn của tôi" KHÔNG hiển thị; nội dung đi thẳng xuống section "Tin mới" | P2 | Business Rule | NEW |
| SC-HOME-011 | Nhãn vai Sender | REQ-HOME-005 | DOC-v1.0-02 §3.1 | Tài khoản đang là **Người gửi** của đơn đang hoạt động | Mở Trang chủ | Section "Đơn của tôi" dùng nhãn "Gửi:" | P2 | Business Rule | NEW |
| SC-HOME-012 | Nhãn vai Carrier | REQ-HOME-005 | DOC-v1.0-02 §5.1 | Tài khoản đang là **Người vận chuyển** của đơn đang hoạt động | Mở Trang chủ | Section "Đơn của tôi" dùng nhãn "Giao:" | P2 | Business Rule | NEW |
| SC-HOME-013 | Nhãn vai Receiver | REQ-HOME-005 | DOC-v1.0-02 §5.1 | Tài khoản đang là **Người nhận** của đơn đang hoạt động | Mở Trang chủ | Section "Đơn của tôi" dùng nhãn "Nhận:" | P2 | Business Rule | NEW |
| SC-HOME-014 | Badge + progress theo trạng thái | REQ-HOME-005 | DOC-v1.0-02 §3.1 · DOC-v1.0-01 §D2 L232 | Đơn đang hoạt động ở 1 trong 5 trạng thái | Mở Trang chủ, đối chiếu badge và thanh progress | Badge = tên trạng thái hiện tại; thanh progress tô đúng số bước tương ứng trong 5 mốc (Chờ ghép·Lấy hàng·Đang giao·Đã giao·Hoàn thành) | P3 | UI | NEW |
| SC-HOME-015 | Tap section → Theo dõi đơn | REQ-HOME-005 | DOC-v1.0-02 §3.1 | Section "Đơn của tôi" đang hiển thị | Chạm vào section | Mở màn Theo dõi đơn của đúng đơn đó | P2 | Functional | NEW |
| SC-HOME-016 | "Xem tất cả" → Hoạt động | REQ-HOME-006 | DOC-v1.0-02 §3.1 dòng "Xem tất cả" | Section "Đơn của tôi" đang hiển thị | Bấm "Xem tất cả" | Mở màn Hoạt động | P3 | Functional | NEW |
| SC-HOME-017 | "Tin mới" — vai Sender | REQ-HOME-007 | DOC-v1.0-06 KP-01 §3 KB-ORD-08 · C-ORD-07 | Tài khoản đang ở vai Người gửi; cộng đồng có ≥1 tin | Mở Trang chủ | Section "Tin mới" CÓ hiển thị (không phải tính năng riêng của Carrier) | P2 | Business Rule | NEW |
| SC-HOME-018 | "Tin mới" — vai Carrier | REQ-HOME-007 | DOC-v1.0-01 §D1b US-D06 L175 | Tài khoản đang ở vai Người vận chuyển; cộng đồng có ≥1 tin | Mở Trang chủ | Section "Tin mới" hiển thị tin của cả cộng đồng | P2 | Functional | NEW |
| SC-HOME-019 | [GAP] Số lượng tin "Tin mới" | REQ-HOME-007 | DOC-v1.0-02 §3.1 vs DOC-v1.0-01 US-D06 | 2 nguồn ghi 2 con số khác nhau (1 tin vs 5 tin); cộng đồng có ≥6 tin | Đếm số tin thực tế hiển thị ở section "Tin mới" | GHI NHẬN số thật; ⛔ KHÔNG assert 1 hay 5 (C-HOME-03 Open) | P3 | UI | NEW |
| SC-HOME-020 | Tap tin → Chi tiết tin | REQ-HOME-007 | DOC-v1.0-02 §3.1 dòng "Tin mới" | Section "Tin mới" có ≥1 tin | Bấm vào 1 tin | Mở màn Chi tiết tin của đúng tin đó | P3 | Functional | NEW |
| SC-HOME-021 | "Xem thêm trên Bảng tin" | REQ-HOME-007 | DOC-v1.0-01 §D1b US-D06 L175 | Cộng đồng có nhiều tin hơn số tin section hiển thị | Quan sát cuối section "Tin mới" rồi bấm nút | Nút "Xem thêm trên Bảng tin" hiển thị và dẫn sang màn Bảng tin | P3 | Functional | NEW |
| SC-HOME-022 | "Xem bảng tin gửi hàng" | REQ-HOME-008 | DOC-v1.0-02 §2 | Đang ở Trang chủ | Bấm nút "Xem bảng tin gửi hàng" | Chuyển sang tab Bảng tin | P2 | Functional | NEW |
| SC-HOME-023 | Điều hướng sau khi nhận đơn | REQ-HOME-009 | DOC-v1.0-02 §4.1 | Carrier vừa xác nhận "Tôi mang giúp được" cho 1 tin | Quan sát màn hiện ra ngay sau khi xác nhận | Vào thẳng màn Theo dõi đơn; KHÔNG quay về Trang chủ | P3 | Functional | NEW |
| SC-HOME-024 | [GAP] Empty state Trang chủ | REQ-HOME-010 | DOC-v1.0-06 KP-05 §3 (#4) · C-ORD-06 | Tài khoản mới: không có đơn nào VÀ cộng đồng chưa có tin nào | Mở Trang chủ | GHI NHẬN hiển thị thực tế (text/ảnh empty state nếu có); ⛔ KHÔNG assert text — chưa có đặc tả (C-ORD-06 Open) | P3 | UI | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-HOME-001 — Bottom nav đủ 5 tab, Trang chủ active

**Source Quote:**
> "Mỗi vai trò có cùng một cấu trúc điều hướng gồm 5 tab dưới cùng: Trang chủ / Bảng tin / Đăng tin (nút "+" nổi bật ở giữa) / Hoạt động / Cá nhân."

**Source Location:** `DOC-v1.0-02 §2 "Kiến trúc điều hướng dùng chung cho cả 3 vai trò" · đoạn 1`

**Analyst Note:** P1 vì đây là **cửa vào mọi module khác** — nav sai/thiếu tab thì toàn bộ SC của FEED/ACT/USR bị blocked. `DOC-v1.0-06` KP-01 §3 KB-ORD-07 (#8) xác nhận độc lập cùng 5 tab từ app STG ⇒ đủ 2 nguồn theo `§Custom Rules §10.1`.

##### SC-HOME-002 — Màn con ẩn bottom nav

**Source Quote:**
> "Các màn hình con (Chi tiết tin, Theo dõi đơn, luồng Đăng tin theo bước, Thông báo, Tặng quà...) không hiển thị thanh tab này — chỉ có nút quay lại (←)."

**Source Location:** `DOC-v1.0-02 §2 · đoạn 1 · câu 2`

**Analyst Note:** Doc liệt kê 5 màn con **kèm dấu "..."** ⇒ danh sách **không đóng**. Then vì thế assert theo đúng 5 màn được nêu tên, ⛔ không suy rộng "mọi màn con"; màn con phát hiện thêm khi vibe-test thì bổ sung qua `/analyze --update`.

##### SC-HOME-003 — Header hiển thị lời chào đúng tên

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-HOME-002`)*

**Source Location:** `DOC-v1.0-02 §2 · bảng Thành phần/Mô tả · dòng "Header"`

**Analyst Note:** `[Tên]` là placeholder ⇒ oracle là **khớp tên hồ sơ nhân viên** (cùng nguồn với `SC-USR-002`), không phải giá trị hằng. Trên STG tài khoản pre-logged-in hiển thị "Chung Hoàng Liêm" (`DOC-v1.0-06` KP-01 §10.1) — dùng làm giá trị mong đợi khi execute, không hardcode vào TC.

##### SC-HOME-004 — [GAP] Icon vai trò ở header

**Source Quote:**
> "5 | **Icon vai trò ở Header khác nhau** theo Sender/Carrier/Receiver | Chưa có bằng chứng UI mapping"

**Source Location:** `DOC-v1.0-06 KP-05 §3 · bảng "6 nhóm case chưa có nguồn tài liệu" · dòng 5`

**Analyst Note:** PRD nói header **có** "Icon vai trò" nhưng không nơi nào cho biết icon nào ứng với vai nào. Theo `§Custom Rules §10.1` ⇒ SC dạng **GAP finding**: ghi nhận icon thực tế của 3 vai để làm đầu vào cho `C-HOME-01`, ⛔ không assert icon cụ thể. Đây cũng là 1 trong 6 nhóm case đợt cũ **cố ý không viết TC**.

##### SC-HOME-005 / SC-HOME-006 — Chấm đỏ chuông (positive + negative)

**Source Quote:**
> "chuông thông báo (chấm đỏ khi có tin chưa đọc)"

**Source Location:** `DOC-v1.0-02 §2 · bảng Thành phần/Mô tả · dòng "Header" · mệnh đề 3`

**Analyst Note:** Doc chỉ nêu nhánh **có** tin chưa đọc ⇒ nhánh negative (đã đọc hết → hết chấm đỏ) là **suy diễn của analyst từ ngữ nghĩa "khi"**, cần xác nhận khi execute. Cách chuyển từ "có chấm đỏ" sang "hết chấm đỏ" (mark-all hay mark-per-item) **chưa chốt** — `C-NTF-03(a)` Open, thuộc `NTF` ⇒ Given của `SC-HOME-006` dùng tiền đề "đã đọc hết" mà không quy định cách đọc.

##### SC-HOME-007 — Banner tĩnh, bấm không có hành vi

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-HOME-003`)*

**Source Location:** `DOC-v1.0-02 §2 · bảng Thành phần/Mô tả · dòng "Banner quảng bá"`

**Analyst Note:** Tagline ở đây là *"Tiện đường — Giúp đồng nghiệp"*, còn `DOC-v1.0-01` §A3 L29 ghi *"Tiện đường — Đồng nghiệp giúp nhau"* — **khác câu chữ cho cùng một banner**. Assert theo PRD (nguồn mô tả bề mặt UI), lệch này ghi ở `C-HOME-01` để BA chốt text marketing chính thức.

##### SC-HOME-008 — Card "Đóng góp của bạn"

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-HOME-004`)*

**Source Location:** `DOC-v1.0-02 §2 · bảng Thành phần/Mô tả · dòng "Card "Đóng góp của bạn""`

**Analyst Note:** `[x]`/`[y]` là số toàn hệ thống, `Runtime`, không seed được ⇒ Then assert **cấu trúc + định dạng dòng chữ**, không assert giá trị. Mệnh đề "KHÔNG hiện CO₂/điểm ECO" thêm vào theo `DOC-v1.0-01` §A7 L111 + `C-USR-01` — vì biến thể có CO₂ tồn tại trong `DOC-v1.0-02` §3.2.

##### SC-HOME-009 / SC-HOME-010 — Section "Đơn của tôi" hiện/ẩn có điều kiện

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-HOME-005`)*

**Source Location:** `DOC-v1.0-02 §3.1 "Màn hình Trang chủ" · bảng Trường/Thành phần · dòng "Đơn của tôi"`

**Analyst Note:** Điều kiện hiển thị là **"có đơn đang hoạt động"**. ⚠️ `DOC-v1.0-06` KP-05 §3 (#3) nêu nghi vấn khác: Carrier **không thấy** section theo **vai trò** (không phải theo có/không có đơn) ⇒ 2 cách hiểu khác nhau, `C-HOME-02` Open. `SC-HOME-010` assert theo doc; nếu vibe-test cho kết quả khác thì đó là dữ liệu cho `C-HOME-02`, ⛔ không tự đổi kết luận. `DOC-v1.0-02` §4.5 còn ghi bản demo hiện sai (*"vẫn hiển thị sẵn 1 đơn Chờ ghép dù chưa nhận đơn nào — dữ liệu mẫu tĩnh"*) ⇒ hành vi demo **không dùng làm oracle**.

##### SC-HOME-011 / SC-HOME-012 / SC-HOME-013 — Nhãn section theo vai trò (3 SC, 1/role)

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-HOME-005`)*

**Source Location:** `DOC-v1.0-02 §5.1 "Màn hình Trang chủ, Bảng tin, Chi tiết tin, Đăng tin" · đoạn 1`

**Analyst Note:** Câu này là nguồn **duy nhất** cho cả 3 nhãn (nêu `Nhận:` và ám chỉ `Gửi:`/`Giao:`). Fan-out 1 SC/role theo Scenario Sufficiency Rule vì mỗi vai là một tiền đề dữ liệu khác nhau (cùng 1 đơn nhưng xem bằng 3 tài khoản khác nhau) — Given khác nhau ⇒ không gộp. Cross-ref `KB-DLV-01` (ma trận nhãn nút theo vai ở màn Theo dõi đơn — cùng nguyên lý role-aware).

##### SC-HOME-014 — Badge trạng thái + progress 5 bước

**Source Quote:**
> "Timeline theo dõi 5 mốc: Chờ ghép · Lấy hàng · Đang giao · Đã giao · Hoàn thành"

**Source Location:** `DOC-v1.0-01 §D2 "Workflow & Status Flow" · block code 2 · L232`

**Analyst Note:** ⚠️ **Bẫy thuật ngữ:** badge trạng thái ở PRD dùng *"Đã ghép"* còn thanh 5 mốc dùng *"Lấy hàng"* cho **cùng trạng thái backend `MATCHED`** (`DOC-v1.0-06` KP-01 §5.1 ghi rõ). Then vì thế phải nói rõ: **badge** đọc theo tên trạng thái, **progress** đọc theo tên mốc — không đòi 2 chỗ cùng một chữ.

##### SC-HOME-015 / SC-HOME-016 — Tap section · nút "Xem tất cả"

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-HOME-006`)*

**Source Location:** `DOC-v1.0-02 §3.1 · bảng Trường/Thành phần · dòng "Xem tất cả"`

**Analyst Note:** Hai đích khác nhau từ cùng một section: **chạm vào card** → Theo dõi đơn (1 đơn cụ thể), **bấm "Xem tất cả"** → Hoạt động (danh sách). Tách 2 SC để khi FAIL biết ngay nhánh nào sai. ⭐ `SC-HOME-016` đóng gap `KP-05 §3 (#1)` của đợt cũ (đợt cũ tưởng nút này không có nguồn tài liệu).

##### SC-HOME-017 / SC-HOME-018 — "Tin mới" hiển thị cho cả 2 vai

**Source Quote:**
> "BRD mô tả đây là tính năng riêng của Carrier, nhưng UI thực tế cho thấy Trang chủ của Sender cũng có section này. User chốt: *"viet theo UI luon nha"*."

**Source Location:** `DOC-v1.0-06 KP-01 §3 "KB-ORD-08" · đoạn 1` (đối chiếu `DOC-v1.0-01 §D1b US-D06 · L175`)

**Analyst Note:** `C-ORD-07` Resolved 2026-07-30 theo UI: section hiển thị cho **cả Sender lẫn Carrier**. Fan-out 2 SC theo role vì Given khác (tài khoản đang giữ vai khác nhau). Receiver chưa có bằng chứng riêng ⇒ ⛔ không tự thêm SC cho Receiver, đưa vào `coverage-gap-report` khi sweep.

##### SC-HOME-019 — [GAP] Số lượng tin ở "Tin mới"

**Source Quote:**
> Nguồn A (`DOC-v1.0-02` §3.1): "Tin mới | Rút gọn 1 tin mới nhất của CẢ CỘNG ĐỒNG (không riêng của Người gửi); bấm vào mở Chi tiết tin"
> Nguồn B (`DOC-v1.0-01` §D1b `US-D06` L175): "Trang chủ hiển thị đúng 5 tin mới nhất; nếu còn tin khác hiện nút "Xem thêm trên Bảng tin" dẫn sang màn Bảng tin"

**Source Location:** `DOC-v1.0-02 §3.1 · dòng "Tin mới"` ⟷ `DOC-v1.0-01 §D1b · US-D06 · L175`

**Analyst Note:** ⭐ Mâu thuẫn **1 vs 5** chưa ai giải quyết (`DOC-v1.0-06` KP-05 §2.1). Đợt cũ xử lý bằng cách *"TC completeness cố ý không assert số lượng"* — lượt này giữ nguyên cách xử lý nhưng **nâng thành 1 SC độc lập có ID** để gap không bị chôn trong ghi chú của TC khác. Given yêu cầu ≥6 tin để phân biệt được 1/5/all.

##### SC-HOME-020 / SC-HOME-021 — Tap tin · nút "Xem thêm trên Bảng tin"

**Source Quote:**
> "nếu còn tin khác hiện nút "Xem thêm trên Bảng tin" dẫn sang màn Bảng tin"

**Source Location:** `DOC-v1.0-01 §D1b · US-D06 · Acceptance Criteria · L175`

**Analyst Note:** Điều kiện hiện nút = *"còn tin khác"* — phụ thuộc trực tiếp vào số tin section hiển thị, tức phụ thuộc `C-HOME-03` chưa chốt. ⇒ Given viết theo **quan hệ** ("nhiều tin hơn số section hiển thị") thay vì con số cứng ≥6, để SC không chết khi `C-HOME-03` được chốt là 1 hoặc 5. Đây cũng là gap `KP-05 §3 (#2)` của đợt cũ, nay có nguồn `US-D06`.

##### SC-HOME-022 — Nút "Xem bảng tin gửi hàng"

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-HOME-008`)*

**Source Location:** `DOC-v1.0-02 §2 · bảng Thành phần/Mô tả · dòng "Nút "Xem bảng tin gửi hàng""`

**Analyst Note:** Phân biệt rõ với `SC-HOME-021`: nút này **thuộc thành phần chung Trang chủ, luôn có**; nút *"Xem thêm trên Bảng tin"* gắn với section "Tin mới" và **có điều kiện**. Hai nút, hai SC, cùng đích — đừng gộp.

##### SC-HOME-023 — Điều hướng thẳng Theo dõi đơn sau khi nhận đơn

**Source Quote:** *(quote đầy đủ ở `requirement_traceability.md §2 REQ-HOME-009`)*

**Source Location:** `DOC-v1.0-02 §4.1 "Màn hình Trang chủ" (Luồng 2 — Người vận chuyển) · đoạn 1 · câu 2`

**Analyst Note:** SC này chỉ assert **đích điều hướng**; việc đơn đổi sang `MATCHED` và lộ SĐT verify ở `SC-ASN-001`/`SC-ASN-004`. Tách như vậy để khi FAIL phân biệt được "ghép sai" và "điều hướng sai".

##### SC-HOME-024 — [GAP] Empty state Trang chủ

**Source Quote:** *(Implicit — không có quote đặc tả trực tiếp)*

**Source Location:** `DOC-v1.0-06 KP-05 §3 · bảng "6 nhóm case chưa có nguồn tài liệu" · dòng 4` · liên quan `C-ORD-06`

**Analyst Note:** Derivation: `DOC-v1.0-02` §3.1/§4.1 chỉ mô tả Trang chủ **khi có** dữ liệu; trạng thái rỗng hoàn toàn (không đơn + không tin cộng đồng) không nơi nào mô tả. `C-ORD-06` từng bị **revert Resolved→Open** vì đánh dấu Resolved không kèm bằng chứng (`KP-02 §6`) ⇒ SC viết dạng ghi nhận, ⛔ không assert text. Cross-ref `SC-ACT-014`, `SC-NTF-015`, `SC-GIFT-008` (cùng nhóm empty state).

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| — | *(không có — v1.0 là version đầu của chuỗi phân tích mới)* | — | — | — | — |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
