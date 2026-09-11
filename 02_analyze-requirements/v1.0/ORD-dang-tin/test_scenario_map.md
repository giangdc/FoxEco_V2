---
id: v1.0/ORD-dang-tin/scenario-map
title: Test Scenario Map — v1.0 · Module ORD
type: scenario-map
version: v1.0
sprint: 1
module: ORD
counts:
  req: 22
  sc: 51
  new: 51
  modified: 0
  carried: 0
  deprecated: 0
  p1: 7
  p2: 28
  p3: 16
status: ANALYZED
updated: 2026-09-07
---

# Test Scenario Map — v1.0 · Module ORD

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module ORD.
> ⚠️ **Module lớn nhất dự án.** Đợt v1.0 cũ: `ORD` gồm cả Trang chủ + Hoạt động (33 SC / 161 TC); lượt này chỉ còn Đăng tin & Quản lý tin.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Fan-out mỗi role · state-transition · lớp EP · boundary · nhánh lỗi = 1 SC.
> **Quyết định altitude cho form nhiều trường** (ghi ở `CHANGELOG §2` ràng buộc 8): SC dừng ở mức **rule/hành vi**; EP/BVA **từng trường** là việc của `generate-tc --mode comprehensive` (rubric `B1` Equivalence Partitioning · `B2` Boundary Value Analysis). Vì vậy `SC-ORD-023` là 1 SC "validate field Người nhận" thay vì 4 SC/trường.
> Trần: display-only/Phase-2/duplicate → `coverage-gap-report.md`.

## Tổng quan
- Tổng số scenarios: **51** (NEW: 51, MODIFIED: 0, CARRIED: 0, DEPRECATED: 0)
- Phân bổ priority: P1: 7 | P2: 28 | P3: 16
- **6 SC dạng `[GAP·bug]` / `[GAP]` sinh từ mâu thuẫn nguồn hoặc nghi vấn bug đã có screenshot** — dự kiến FAIL, và FAIL là kết quả đúng: `SC-ORD-015`, `SC-ORD-016`, `SC-ORD-021`, `SC-ORD-022`, `SC-ORD-033`, `SC-ORD-007`.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### ORD — Đăng tin & Quản lý tin

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-ORD-001 | Màn chọn vai trò đăng | REQ-ORD-001 | DOC-v1.0-02 §3.5 · DOC-v1.0-04 f821ba30… | Đã vào FoxEco | Bấm tab "+ Đăng tin" | Màn "Đăng tin mới" đủ 5 thành phần: subtitle "Bạn muốn làm gì?" · card "Tôi cần gửi hàng" · card "Tôi nhận giao hàng" · banner cam kết (không phí/không chat/không thanh toán/SĐT lộ sau ghép) · cả 2 card bấm được | P2 | UI | NEW |
| SC-ORD-002 | Vào wizard NEED | REQ-ORD-001 | DOC-v1.0-02 §3.5 · DOC-v1.0-01 §D3 ORD-02 | Đang ở màn "Đăng tin mới" | Bấm card "Tôi cần gửi hàng" | Mở wizard Bước 1/3 "Thông tin hàng", có step indicator "Bước 1/3" | P2 | Functional | NEW |
| SC-ORD-003 | Vào form OFFER | REQ-ORD-001 | DOC-v1.0-02 §3.5 · §4.4 | Đang ở màn "Đăng tin mới" | Bấm card "Tôi nhận giao hàng" | Mở form đăng ký chuyến đi 1 trang (KHÔNG có step indicator) | P2 | Functional | NEW |
| SC-ORD-004 | Happy path đăng tin NEED | REQ-ORD-002 | DOC-v1.0-01 §D3 ORD-02 L240 · §D1b US-D01 L164 | Tài khoản hợp lệ; có email nội bộ người nhận tra được | Điền đủ B1 (loại hàng+giá trị) → B2 (người nhận + địa chỉ + ngày + khung giờ) → B3 tick điều khoản → "Đăng tin ngay" | Đăng tin thành công; tin ở trạng thái "Chờ ghép"; vào màn "Đăng tin thành công" | P1 | Functional | NEW |
| SC-ORD-005 | Chip Loại hàng single-select | REQ-ORD-003 | DOC-v1.0-01 §D8.1 L357 · DOC-v1.0-06 KP-01 §10.2/§10.3 | Đang ở Bước 1/3 | Quan sát chip mặc định rồi chọn 1 chip khác | Luôn có đúng 1 chip được chọn; mặc định là "Giấy tờ, hồ sơ"; chọn chip mới thì chip cũ bỏ chọn | P2 | UI | NEW |
| SC-ORD-006 | [GAP] Danh mục Loại hàng | REQ-ORD-003 | DOC-v1.0-01 §D8.1 L357 vs DOC-v1.0-02 §3.5.1 vs app STG | 3 nguồn cho 3 danh mục khác nhau (5 vs 8 vs 8 giá trị; "Tài liệu" không có trên app) | Liệt kê toàn bộ chip thực tế trên app | GHI NHẬN danh mục thật; ⛔ KHÔNG assert nhãn "Tài liệu" (C-ORD-09 Open) | P3 | UI | NEW |
| SC-ORD-007 | [GAP] Rule "Loại hàng bắt buộc" không kiểm chứng được | REQ-ORD-003 | DOC-v1.0-06 KP-01 §10.3 KB-VIBE-02 | Chip luôn có 1 giá trị mặc định; tap lại chip đang chọn không deselect | Thử tạo trạng thái "chưa chọn Loại hàng" rồi bấm "Tiếp theo" | GHI NHẬN: không tái hiện được tiền đề ⇒ rule "Không cho để trống" không kiểm chứng qua UI. ⛔ KHÔNG viết TC negative để trống Loại hàng | P3 | Business Rule | NEW |
| SC-ORD-008 | Giá trị hàng bắt buộc | REQ-ORD-005 | DOC-v1.0-01 §D8.1 L359 · DOC-v1.0-06 KP-01 §10.4 | Đang ở Bước 1/3, chưa chọn Giá trị hàng | Bấm "Tiếp theo" | Nút "Tiếp theo" ở trạng thái disabled/mờ, KHÔNG chuyển bước | P2 | Business Rule | NEW |
| SC-ORD-009 | Cảnh báo Giá trị "Cao" | REQ-ORD-005 | DOC-v1.0-01 §D8.1 L359 · DOC-v1.0-06 KP-01 §3 KB-ORD-05 | Đang ở Bước 1/3 | Chọn Giá trị hàng = "Cao" | Hiện banner nguyên văn: "Hàng giá trị cao: hai bên tự thoả thuận và chịu trách nhiệm với nhau. FoxEco không bảo hiểm, không đứng ra vận chuyển hay bồi thường." | P2 | Business Rule | NEW |
| SC-ORD-010 | Không cảnh báo với Thấp/Vừa | REQ-ORD-005 | DOC-v1.0-06 KP-01 §3 KB-ORD-05 | Đang ở Bước 1/3 | Chọn Giá trị hàng = "Thấp", sau đó = "Vừa" | Cả 2 trường hợp KHÔNG hiện banner cảnh báo | P3 | Business Rule | NEW |
| SC-ORD-011 | Ghi chú — biên 300 ký tự | REQ-ORD-004 | DOC-v1.0-01 §D8.1 L358 | Đang ở Bước 1/3 | Nhập Ghi chú 300 ký tự, rồi thử 301 ký tự | 300 ký tự: hợp lệ, qua bước được. 301: bị chặn/không nhập thêm được | P3 | Business Rule | NEW |
| SC-ORD-012 | Ảnh sản phẩm — ràng buộc | REQ-ORD-006 | DOC-v1.0-01 §D8.1 L360 | Đang ở Bước 1/3 | Thử tải: 1 ảnh JPG 4MB · 1 ảnh PNG 5MB · 1 ảnh >5MB · 1 file không phải JPG/PNG · thử tải ảnh thứ 2 | 3 case đầu (≤5MB, JPG/PNG) được nhận; >5MB và sai định dạng bị chặn; chỉ giữ được 1 ảnh duy nhất | P3 | Business Rule | NEW |
| SC-ORD-013 | Bỏ trống ảnh vẫn qua bước | REQ-ORD-006 | DOC-v1.0-01 §D8.1 L360 | Đang ở Bước 1/3, đã chọn loại hàng + giá trị | Không tải ảnh nào, bấm "Tiếp theo" | Chuyển sang Bước 2/3 bình thường (ảnh là trường tuỳ chọn) | P3 | Business Rule | NEW |
| SC-ORD-014 | Người gửi auto-fill Tên + SĐT | REQ-ORD-007 | DOC-v1.0-01 §D8.1 L362-363 | Tài khoản đăng nhập có tên + SĐT trong hồ sơ nhân viên | Vào Bước 2/3, quan sát nhóm "Người gửi" | Tên và SĐT được điền sẵn đúng giá trị hồ sơ tài khoản | P2 | Functional | NEW |
| SC-ORD-015 | [GAP·bug] Tên người gửi phải read-only | REQ-ORD-007 | DOC-v1.0-01 §D8.1 L362 · DOC-v1.0-06 KP-01 §10.5 | Đang ở Bước 2/3, field Tên người gửi đã pre-fill | Chạm vào field Tên người gửi | Field KHÔNG mở bàn phím, KHÔNG sửa được, giá trị KHÔNG bị xoá (spec: "Chỉ đọc"). ⚠ Dự kiến FAIL — app cho sửa và xoá trắng → log bug | P2 | Business Rule | NEW |
| SC-ORD-016 | [GAP·bug] Địa chỉ lấy hàng phải pre-fill | REQ-ORD-007 | DOC-v1.0-01 §D8.1 L364 · DOC-v1.0-06 KP-01 §10.6 | Tài khoản có nơi làm việc trong hồ sơ | Vào Bước 2/3, quan sát field Địa chỉ lấy hàng | Field được điền sẵn theo nơi làm việc của user. ⚠ Dự kiến FAIL — app để trống, chỉ có placeholder → xác nhận với dev trước khi log bug (C-ORD-10) | P2 | Business Rule | NEW |
| SC-ORD-017 | [GAP] SĐT người gửi tự đổi giá trị | REQ-ORD-007 | DOC-v1.0-06 KP-01 §10.10 KB-VIBE-09 | Đang ở Bước 2/3, SĐT người gửi đã pre-fill | Ghi lại giá trị, thao tác các field khác trong cùng phiên rồi quay lại quan sát SĐT | Giá trị SĐT KHÔNG tự đổi khi user không tác động. ⚠ Đã quan sát 1 lần đổi giá trị — nếu tái hiện → log bug | P3 | Business Rule | NEW |
| SC-ORD-018 | Email nội bộ tra thấy → auto-fill | REQ-ORD-008 | DOC-v1.0-01 §D3 USR-EML L253 · §D1b US-D18 L168 | Có email nội bộ tồn tại trong danh bạ (STG: stag_anhdc4@fpt.com) | Nhập email đó vào ô "Email công ty người nhận", rời ô | Tự điền Tên + SĐT + Địa chỉ người nhận từ danh bạ; hiện thông báo "Đã tìm thấy trong hệ thống nội bộ" | P1 | Functional | NEW |
| SC-ORD-019 | Email không tra thấy | REQ-ORD-008 | DOC-v1.0-01 §D1b US-D18 L168 · §D8.1 L366 | Có email đúng định dạng nội bộ nhưng KHÔNG tồn tại trong danh bạ | Nhập email đó, rời ô | Hiện thông báo "Không tìm thấy · nhập thủ công"; 3 trường người nhận để trống cho user tự nhập | P2 | Functional | NEW |
| SC-ORD-020 | Email sai định dạng / ngoài tên miền | REQ-ORD-008 | DOC-v1.0-01 §D8.1 L366 | Đang ở Bước 2/3 | Nhập email sai định dạng (thiếu @), rồi nhập email đúng định dạng nhưng ngoài tên miền nội bộ | Cả 2 trường hợp bị báo lỗi, KHÔNG tra danh bạ | P2 | Business Rule | NEW |
| SC-ORD-021 | [GAP·bug] App báo lỗi SĐT nó tự điền | REQ-ORD-008 | DOC-v1.0-06 KP-01 §10.9 KB-VIBE-08 | Email nội bộ tra thấy, app tự điền SĐT người nhận từ danh bạ | Không sửa gì, rời ô / bấm "Tiếp theo" | SĐT do app tự điền phải được coi là hợp lệ. ⚠ Dự kiến FAIL — app báo "Số điện thoại không hợp lệ" cho giá trị `0000286248` do chính nó điền → log bug (data hoặc validate) | P2 | Business Rule | NEW |
| SC-ORD-022 | [GAP·bug] Người nhận bắt buộc | REQ-ORD-009 | DOC-v1.0-06 KP-01 §3 KB-ORD-01 · DOC-v1.0-02 §7 dòng 2 | Đang ở Bước 2/3, để trống toàn bộ nhóm "Người nhận" | Bấm "Tiếp theo" | Bị chặn, không qua được Bước 3 (C-ORD-01: rule bắt buộc). ⚠ Dự kiến FAIL nếu app còn hành vi prototype (cho để trống mà vẫn đăng thành công) | P1 | Business Rule | NEW |
| SC-ORD-023 | Validate field Người nhận | REQ-ORD-009 | DOC-v1.0-01 §D8.1 L367-368 | Đang ở Bước 2/3 | Nhập Tên người nhận ở biên 1/2/60/61 ký tự; nhập SĐT 9/10/11 số, số không bắt đầu bằng 0, số có chữ | Tên: 2..60 hợp lệ, 1 và 61 bị chặn. SĐT: đúng 10 số đầu 0 hợp lệ, còn lại bị chặn | P2 | Business Rule | NEW |
| SC-ORD-024 | Địa chỉ giao ≠ địa chỉ lấy | REQ-ORD-009 | DOC-v1.0-01 §D8.1 L369 | Đang ở Bước 2/3, địa chỉ lấy hàng đã có giá trị | Chọn địa chỉ giao hàng **trùng** địa chỉ lấy hàng, bấm "Tiếp theo" | Bị chặn kèm thông báo lỗi (spec: "phải khác địa chỉ lấy hàng") | P2 | Business Rule | NEW |
| SC-ORD-025 | Autocomplete địa chỉ văn phòng | REQ-ORD-010 | DOC-v1.0-06 KP-01 §3 KB-ORD-06 | Đang ở Bước 2/3, DB có danh sách văn phòng | Gõ text tự do vào field địa chỉ, thử cả chữ thường và CHỮ HOA | Hiện dropdown gợi ý các văn phòng khớp; kết quả giống nhau với chữ thường/hoa (không phân biệt hoa/thường) | P2 | Functional | NEW |
| SC-ORD-026 | Phải chạm chọn gợi ý mới lưu | REQ-ORD-010 | DOC-v1.0-06 KP-01 §3 KB-ORD-06 | Dropdown gợi ý đang hiện | (a) Gõ text rồi rời ô mà KHÔNG chọn gợi ý; (b) Gõ text rồi CHẠM chọn 1 gợi ý | (a) Field KHÔNG giữ giá trị; (b) Field lưu đúng giá trị đã chọn | P2 | Business Rule | NEW |
| SC-ORD-027 | [GAP] Preset 6 văn phòng FPT | REQ-ORD-010 | DOC-v1.0-01 §D3 LOC-03 L246 vs §D1b US-D01 L164 vs KB-ORD-06 | 3 nguồn nêu 3 cơ chế cho cùng field (preset 6 văn phòng / không chip gợi ý / dropdown autocomplete) | Quan sát field địa chỉ ở Bước 2/3 | GHI NHẬN cơ chế thật; ⛔ KHÔNG assert có 6 chip preset (C-ORD-11 Open) | P3 | UI | NEW |
| SC-ORD-028 | Từ ngày / Đến ngày | REQ-ORD-011 | DOC-v1.0-01 §D8.1 L370-371 | Đang ở Bước 2/3 | Quan sát giá trị mặc định; thử chọn ngày quá khứ; thử Đến ngày < Từ ngày; thử Đến ngày = Từ ngày | Mặc định cả 2 = hôm nay; ngày quá khứ bị chặn; Đến < Từ bị chặn; Đến = Từ hợp lệ (biên) | P2 | Business Rule | NEW |
| SC-ORD-029 | Khung giờ — biên 30 phút | REQ-ORD-012 | DOC-v1.0-01 §D8.1 L372 | Đang ở Bước 2/3 | Chọn khung giờ cách nhau 29 phút, rồi đúng 30 phút, rồi giờ đến < giờ từ | 29 phút bị chặn; đúng 30 phút hợp lệ (biên); đến < từ bị chặn | P2 | Business Rule | NEW |
| SC-ORD-030 | Khung giờ mặc định hết hạn theo đồng hồ thật | REQ-ORD-012 | DOC-v1.0-06 KP-01 §10.11 KB-VIBE-10 | Mở Bước 2/3 và để form mở >15 phút mà không thao tác | Bấm "Tiếp theo" với khung giờ mặc định đã trôi qua | App báo validate "phải muộn hơn hiện tại" — đây là hành vi ĐÚNG, KHÔNG phải bug | P3 | Business Rule | NEW |
| SC-ORD-031 | B3 tóm tắt đúng dữ liệu | REQ-ORD-013 | DOC-v1.0-02 §3.5.3 | Đã điền đủ B1 + B2 với dữ liệu xác định | Chuyển sang Bước 3/3 | Tóm tắt hiện đúng: loại hàng + giá trị · khung giờ · thông tin người gửi/người nhận · ghi chú — khớp dữ liệu đã nhập ở B1/B2 | P2 | UI | NEW |
| SC-ORD-032 | Banner cảnh báo hàng cấm | REQ-ORD-013 | DOC-v1.0-02 §3.5.3 · DOC-v1.0-01 §A8 L115 | Đang ở Bước 3/3 | Quan sát banner cảnh báo | Hiện banner nội dung "Không được gửi: thuốc, vũ khí, chất nguy hiểm, hàng phi pháp..." | P3 | UI | NEW |
| SC-ORD-033 | [GAP] Mặc định checkbox điều khoản | REQ-ORD-013 | DOC-v1.0-01 §D8.1 L373 vs DOC-v1.0-02 §3.5.3 | 2 nguồn trái nhau: BRD "Chưa tick" · PRD "Mặc định đã tick sẵn" | Vào Bước 3/3 lần đầu, quan sát trạng thái checkbox | Checkbox ở trạng thái CHƯA tick (theo `D8.1` + app STG). ⚠ TC `TC_04.71` đợt cũ expected "tick sẵn" là sai nguồn (C-ORD-12) | P2 | Business Rule | NEW |
| SC-ORD-034 | Không tick điều khoản → chặn đăng | REQ-ORD-013 | DOC-v1.0-01 §D3 ORD-09 L245 · §D8.1 L373 | Đang ở Bước 3/3, đã đủ dữ liệu B1+B2, chưa tick điều khoản | Bấm "Đăng tin ngay" | Nút bị vô hiệu hoá / không đăng được; sau khi tick thì nút bật | P1 | Business Rule | NEW |
| SC-ORD-035 | [GAP] Hàng cấm không bị chặn ở v1.0 | REQ-ORD-014 | DOC-v1.0-01 §D4 BR-ORD-04 L263 · DOC-v1.0-06 KP-01 §3 KB-ORD-03 | Rule `BR-ORD-04` cấm đăng hàng cấm; `C-ORD-04` Resolved: v1.0 KHÔNG chặn | Chọn chip "Thuốc/Y tế" rồi đăng tin đủ bước | GHI NHẬN: tin đăng thành công, không bị chặn (đúng phạm vi v1.0). ⛔ KHÔNG viết TC negative "bị chặn" | P3 | Business Rule | NEW |
| SC-ORD-036 | Tin xuất hiện ở "Đơn của tôi" | REQ-ORD-015 | DOC-v1.0-01 §D1b US-D02 L165 | Vừa đăng tin NEED thành công | Về Trang chủ / mở màn Hoạt động | Tin vừa đăng xuất hiện ở "Đơn của tôi" với trạng thái "Chờ ghép" | P2 | Functional | NEW |
| SC-ORD-037 | Màn "Đăng tin thành công" | REQ-ORD-015 | DOC-v1.0-02 §3.5.4 | Vừa bấm "Đăng tin ngay" thành công | Quan sát màn kết quả | Màn "Đăng tin thành công" có đúng 2 lựa chọn: "Theo dõi đơn" và "Về trang chủ"; cả 2 điều hướng đúng đích | P2 | UI | NEW |
| SC-ORD-038 | [GAP] Mã tin ở màn thành công | REQ-ORD-015 | DOC-v1.0-04 (2 biến thể) vs DOC-v1.0-01 US-D02 L165 | Figma có 2 biến thể (1 bản CÓ "Mã tin", 1 bản KHÔNG); `US-D02` ghi "KHÔNG hiển thị mã đơn" | Quan sát màn "Đăng tin thành công" trên app | GHI NHẬN có/không có mã tin; ⛔ KHÔNG assert (C-ORD-05 Open) | P3 | UI | NEW |
| SC-ORD-039 | Form OFFER 1 trang | REQ-ORD-016 | DOC-v1.0-01 §D1b US-D10 L184 · DOC-v1.0-02 §4.4 · KP-01 §3 KB-ORD-11 | Đã bấm "Tôi nhận giao hàng" | Quan sát toàn form | Form 1 trang, KHÔNG có step indicator; đủ trường: Thông tin của tôi (Tên, SĐT) · Điểm xuất phát (A) · Điểm đến (B) · Khoảng thời gian (ngày) · Thời gian di chuyển · checkbox điều khoản · nút đăng | P2 | UI | NEW |
| SC-ORD-040 | OFFER — điểm xuất phát/đến | REQ-ORD-016 | DOC-v1.0-01 §D8.2 L381-382 | Đang ở form OFFER | Quan sát Điểm xuất phát (pre-fill), thử sửa nó; chọn Điểm đến trùng Điểm xuất phát | Điểm xuất phát pre-fill theo nơi làm việc và **sửa được**; Điểm đến trùng Điểm xuất phát bị chặn | P2 | Business Rule | NEW |
| SC-ORD-041 | Đăng OFFER → màn ghi nhận tuyến | REQ-ORD-016 | DOC-v1.0-01 §D1b US-D11 L185 | Đã điền đủ form OFFER + tick điều khoản | Bấm nút đăng tin | Vào màn "Đã ghi nhận tuyến đường", nội dung giải thích tuyến được lưu (không công khai) + sẽ có thông báo khi khớp | P2 | Functional | NEW |
| SC-ORD-042 | Tuyến OFFER không công khai | REQ-ORD-016 | DOC-v1.0-01 §D1b US-D11 L185 · §D3 ORD-01 L240 | Tài khoản A vừa đăng 1 tin OFFER thành công | Tài khoản B mở tab "Bảng tin" và tìm tin OFFER của A | Tin OFFER KHÔNG xuất hiện trên Bảng tin của bất kỳ ai (chỉ lưu hệ thống chờ khớp) | P1 | Business Rule | NEW |
| SC-ORD-043 | Sửa tin khi "Chờ ghép" | REQ-ORD-017 | DOC-v1.0-01 §D3 ORD-10 L252 · §D1b US-D19 L169 | Có 1 tin của mình đang ở trạng thái "Chờ ghép" | Mở tin đó, bấm "Chỉnh sửa" | Nút "Chỉnh sửa" hiển thị; mở form giống tạo đơn nhưng **đã điền sẵn** dữ liệu cũ; có nút "Cập nhật" và "Huỷ chỉnh sửa"; sửa rồi Cập nhật thì dữ liệu tin đổi theo | P2 | Functional | NEW |
| SC-ORD-044 | Khoá sửa từ "Đã ghép" | REQ-ORD-017 | DOC-v1.0-01 §D4 BR-EDIT-01 L269 · §D7 OPR-10 L346 | Có 1 tin của mình đã ở trạng thái "Đã ghép" (MATCHED) | Mở tin đó, tìm nút "Chỉnh sửa" | Nút "Chỉnh sửa" KHÔNG hiển thị / không bấm được — khoá chỉnh sửa hoàn toàn | P1 | Business Rule | NEW |
| SC-ORD-045 | Tin tự hết hạn theo "Đến ngày" | REQ-ORD-018 | DOC-v1.0-01 §D1b US-D04 L166 · DOC-v1.0-06 KP-01 §3 KB-ORD-02 | Có 1 tin "Chờ ghép" với "Đến ngày" đã trôi qua, chưa ai nhận | Mở màn Hoạt động / xem tin | Tin tự chuyển trạng thái "Hết hạn"; hiện lý do "Không có ai nhận mang giúp trong thời gian đăng" | P1 | Business Rule | NEW |
| SC-ORD-046 | Timeline tin có mốc đăng tin | REQ-ORD-019 | DOC-v1.0-01 §D3 ORD-04 L243 | Vừa đăng tin thành công | Mở Theo dõi đơn của tin đó, xem block Lịch sử | Có mốc "Đăng tin" kèm timestamp đúng thời điểm đăng | P2 | Functional | NEW |
| SC-ORD-047 | VAL-01 — submit disable tới khi hợp lệ | REQ-ORD-020 | DOC-v1.0-01 §D8.3 VAL-01 L392 | Đang ở form đăng tin (NEED B3 và form OFFER) | Để thiếu 1 trường bắt buộc / chưa tick điều khoản | Nút submit vô hiệu hoá; đủ trường + tick điều khoản thì nút bật | P2 | Business Rule | NEW |
| SC-ORD-048 | VAL-02 — lỗi inline on-blur | REQ-ORD-020 | DOC-v1.0-01 §D8.3 VAL-02 L393 | Đang ở Bước 2/3 | Nhập sai 1 trường rồi rời ô (blur); sau đó bấm submit khi còn nhiều lỗi | Lỗi hiện NGAY DƯỚI ô nhập (không popup); khi submit thì màn cuộn tới ô lỗi đầu tiên | P3 | UI | NEW |
| SC-ORD-049 | VAL-03 — trim + chuẩn hoá SĐT | REQ-ORD-020 | DOC-v1.0-01 §D8.3 VAL-03 L394 | Đang ở Bước 2/3 | Nhập tên có khoảng trắng đầu/cuối; nhập SĐT có khoảng trắng và dấu chấm ("090 123.4567") | Giá trị lưu đã cắt khoảng trắng đầu/cuối; SĐT đã bỏ khoảng trắng và dấu chấm | P3 | Business Rule | NEW |
| SC-ORD-050 | [GAP] Thoát giữa wizard | REQ-ORD-021 | DOC-v1.0-06 KP-02 §5 dòng C-ORD-08 | Đã nhập dữ liệu ở B1+B2, chưa đăng | Thoát khỏi wizard (back / đổi tab) rồi vào lại "Tôi cần gửi hàng" | GHI NHẬN: form giữ hay xoá dữ liệu đã nhập; ⛔ KHÔNG assert — chưa có đặc tả (C-ORD-08 Open) | P3 | Functional | NEW |
| SC-ORD-051 | [GAP] Ngưỡng giá trị bằng số tiền | REQ-ORD-022 | DOC-v1.0-01 §D4 BR-ORD-03 L262 · DOC-v1.0-06 KP-01 §3 KB-ORD-04 | `BR-ORD-03` yêu cầu ngưỡng giá trị bằng số tiền; `C-ORD-02` Resolved: out of scope v1.0 | Rà Bước 1/3 tìm field nhập số tiền / ngưỡng | GHI NHẬN GAP: không tồn tại field nhập số tiền ở v1.0 (đúng phạm vi). ⛔ KHÔNG viết TC nhập số tiền | P3 | Business Rule | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-ORD-001 / SC-ORD-002 / SC-ORD-003 — Màn "Đăng tin mới" và 2 nhánh đăng

**Source Quote:**
> "Chọn vai trò đăng tin: Gửi hàng / Nhận giao hàng"
> "Subtitle *"Bạn muốn làm gì?"* · card `Tôi cần gửi hàng` (icon hộp cam) · card `Tôi nhận giao hàng` (icon route tím) · banner cam kết nền vàng nhạt icon ⓘ (không phí / không chat / không thanh toán / SĐT lộ sau ghép) · cả 2 card bấm được."

**Source Location:** `DOC-v1.0-02 §3.5 "Màn hình Đăng tin mới" · đoạn 1` + `DOC-v1.0-06 KP-01 §3 "KB-ORD-10"`

**Analyst Note:** Bằng chứng 2 nguồn (Figma `f821ba30…` + VR-002 `TC_04.1` PASS) ⇒ assert được cả 5 thành phần. Tách 3 SC: completeness màn · nhánh NEED (có step indicator) · nhánh OFFER (không step indicator) — điểm phân biệt 2 luồng nằm ngay ở đây.

##### SC-ORD-004 — Happy path đăng tin NEED qua 3 bước

**Source Quote:**
> "ORD-02 | Wizard đăng tin ngắn | B1 Loại tin+hàng → B2 Địa điểm/lộ trình+thời gian → B3 Xác nhận + đồng ý điều khoản"

**Source Location:** `DOC-v1.0-01 §D3 "Functional Requirements — Gửi Hàng" · bảng ID/Yêu cầu/AC · L240`

**Analyst Note:** SC P1 xương sống — mọi SC khác của `DLV`/`ASN`/`CNL`/`GIFT` đều cần 1 đơn tồn tại nên phụ thuộc SC này. Given yêu cầu **email nội bộ tra được** vì đó là đường ngắn nhất qua B2 (auto-fill 3 trường). Trên STG dùng `stag_anhdc4@fpt.com` (`KP-01` §10.1).

##### SC-ORD-005 / SC-ORD-006 / SC-ORD-007 — Chip Loại hàng (single-select · danh mục · rule bắt buộc)

**Source Quote:**
> Nguồn A (`DOC-v1.0-01` §D8.1 L357): "Loại hàng | Có | Tài liệu | Chọn 1 trong danh mục: Tài liệu · Đồ điện tử · Thực phẩm · Quà tặng · Khác. Không cho để trống"
> Nguồn B (`DOC-v1.0-02` §3.5.1): "Loại hàng | Chip chọn 1: Tài liệu (mặc định) · Đồ điện tử · Thực phẩm · Hàng nhỏ · Đồ dễ vỡ · Quần áo · Thuốc/Y tế · Khác"
> Nguồn C (`DOC-v1.0-06` KP-01 §10.2): "Chip mặc định được chọn là **`Giấy tờ, hồ sơ`**. Trong 8 lựa chọn thực tế **không tồn tại** chip nào tên "Tài liệu""
> Nguồn D (`DOC-v1.0-06` KP-01 §10.3): "Tap lại chip đang chọn **không deselect được** → **không thể tái hiện trạng thái "chưa chọn Loại hàng"** qua UI."

**Source Location:** `DOC-v1.0-01 §D8.1 · bảng Trường/Bắt buộc/Mặc định/Validate · L357` ⟷ `DOC-v1.0-02 §3.5.1 · bảng · dòng "Loại hàng"` ⟷ `DOC-v1.0-06 KP-01 §10.2 "KB-VIBE-01"` · `§10.3 "KB-VIBE-02"`

**Analyst Note:** ⭐ **Điểm sai lan rộng nhất của bộ TC cũ.** 3 nguồn → 3 danh mục; app STG là nguồn có bằng chứng mạnh nhất (screenshot VR-002 `TC_04.5` FAIL). Ba SC tách theo 3 câu hỏi khác nhau: *chip có single-select không* (assert được) · *danh mục gồm gì* (GAP, chờ `C-ORD-09`) · *rule bắt buộc có kiểm chứng được không* (GAP — **tiền đề không tái hiện được**, nên `KP-04 §4` xếp là 1 trong 5 lỗi đã biết của đợt cũ).

##### SC-ORD-008 / SC-ORD-009 / SC-ORD-010 — Giá trị hàng (bắt buộc · banner "Cao" · không banner Thấp/Vừa)

**Source Quote:**
> Nguồn A (`DOC-v1.0-01` §D8.1 L359): "Giá trị hàng | Có | Trống (chưa chọn) | Chọn 1: Giá trị thấp / vừa / cao. Chọn Giá trị cao → hiện cảnh báo trách nhiệm tự thoả thuận"
> Nguồn B (`DOC-v1.0-06` KP-01 §3 KB-ORD-05): "*"Hàng giá trị cao: hai bên tự thoả thuận và chịu trách nhiệm với nhau. FoxEco không bảo hiểm, không đứng ra vận chuyển hay bồi thường."*"
> Nguồn C (`DOC-v1.0-06` KP-01 §10.4): "Để trống Giá trị hàng → nút "Tiếp theo" chuyển màu nhạt/disabled, không chuyển bước."

**Source Location:** `DOC-v1.0-01 §D8.1 · L359` + `DOC-v1.0-06 KP-01 §3 "KB-ORD-05"` + `§10.4 "KB-VIBE-03"`

**Analyst Note:** Trường **duy nhất ở B1 kiểm chứng được rule "bắt buộc"** (mặc định trống thật + app chặn thật, VR-002 `TC_04.7` PASS). Banner có **nguyên văn xác nhận trên app** (VR-002 `TC_04.8/9/10` PASS) ⇒ assert được text đầy đủ. Nhánh negative (Thấp/Vừa **không** banner) tách riêng vì đó là nơi lỗi "banner hiện sai điều kiện" sẽ lộ ra.

##### SC-ORD-011 — Ghi chú biên 300 ký tự

**Source Quote:**
> "Ghi chú | Không | Trống | Tối đa 300 ký tự. Khuyến nghị nêu kích thước/khối lượng ước tính & lưu ý khi cầm giữ"

**Source Location:** `DOC-v1.0-01 §D8.1 · bảng · dòng "Ghi chú" · L358`

**Analyst Note:** Boundary 300/301 là ứng viên BVA (`B2`) cho generate-tc. Doc **không nói** app chặn bằng cách nào (không cho nhập thêm vs báo lỗi khi submit) ⇒ Then viết mở ("bị chặn/không nhập thêm được"), ghi nhận cơ chế thật khi execute.

##### SC-ORD-012 / SC-ORD-013 — Ảnh sản phẩm (ràng buộc · tuỳ chọn)

**Source Quote:**
> "Ảnh sản phẩm | Không | Trống | Chỉ 1 ảnh duy nhất, ≤ 5MB, định dạng JPG/PNG. Khuyến nghị có ảnh để người giao dễ nhận"

**Source Location:** `DOC-v1.0-01 §D8.1 · bảng · dòng "Ảnh sản phẩm" · L360`

**Analyst Note:** 3 ràng buộc trong 1 dòng (số lượng · kích thước · định dạng) ⇒ gộp 1 SC theo quyết định altitude (EP/BVA từng ràng buộc là việc của generate-tc). `SC-ORD-013` tách riêng vì "tuỳ chọn" là **rule khác** (không phải validate) và là tiền đề của `SC-FEED-008` (ảnh mặc định).

##### SC-ORD-014 / SC-ORD-015 / SC-ORD-016 / SC-ORD-017 — Nhóm NGƯỜI GỬI (auto-fill + 3 nghi vấn bug)

**Source Quote:**
> Spec (`DOC-v1.0-01` §D8.1 L362-364): "Tên người gửi | Có | Điền sẵn từ tài khoản đăng nhập | Chỉ đọc (lấy từ hồ sơ nhân viên)" · "Địa chỉ lấy hàng | Có | Tòa nhà Lô B3, KCX Tân Thuận, Q.7 (điền sẵn từ nơi làm việc của user) | Không để trống, tối đa 200 ký tự"
> App (`DOC-v1.0-06` KP-01 §10.5): "Chạm vào field → **mở được bàn phím** (không disabled)" · "Giá trị "Chung Hoàng Liêm" bị **XOÁ TRẮNG ngay sau khi chạm**"
> App (`DOC-v1.0-06` KP-01 §10.6): "Expected (spec): mặc định `Tòa nhà Lô B3, KCX Tân Thuận, Q.7`. Thực tế: **field trống, chỉ có placeholder**."
> App (`DOC-v1.0-06` KP-01 §10.10): "SĐT Người gửi thay đổi giữa 2 screenshot cùng một phiên (`0000142378` → `0964633313`) mà **không có thao tác nào của user**"

**Source Location:** `DOC-v1.0-01 §D8.1 · nhóm "▸ Nhóm: NGƯỜI GỬI" · L362-364` ⟷ `DOC-v1.0-06 KP-01 §10.5 "KB-VIBE-04"` · `§10.6 "KB-VIBE-05"` · `§10.10 "KB-VIBE-09"`

**Analyst Note:** ⭐ **3 nghi vấn bug đã có screenshot mà đợt cũ chưa log** (`KP-05 §5`). Cả 3 SC viết theo **spec** ⇒ dự kiến FAIL. Mức chắc chắn khác nhau: `SC-ORD-015` (VR-002 `TC_04.22` FAIL) và `SC-ORD-017` (VR-001 #4, 🟡 chỉ 1 lần) là **hành vi app**, còn `SC-ORD-016` **chưa loại trừ khả năng tài khoản test chưa cấu hình địa chỉ** ⇒ phải xác nhận với dev trước khi log bug (`C-ORD-10`). ⚠️ Bẫy vận hành: sau khi field Tên bị xoá trắng, *"**không tự phục hồi** trong cùng phiên wizard — phải thoát ra vào lại từ đầu Bước 1/3"* ⇒ SC sau `SC-ORD-015` cần reset phiên.

##### SC-ORD-018 / SC-ORD-019 / SC-ORD-020 / SC-ORD-021 — Email công ty người nhận (tra danh bạ)

**Source Quote:**
> Spec (`DOC-v1.0-01` §D1b `US-D18` L168): "Ô "Email công ty người nhận" nằm đầu mục Người nhận; nhập email có trong hệ thống → tự điền tên/SĐT/địa chỉ + báo "Đã tìm thấy trong hệ thống nội bộ"; không có → báo "Không tìm thấy · nhập thủ công""
> Spec (`DOC-v1.0-01` §D8.1 L366): "Email công ty người nhận | Có | Trống | Đúng định dạng email & thuộc tên miền nội bộ. Tra danh bạ: tìm thấy → tự điền tên/SĐT/địa chỉ; không thấy → cảnh báo & cho nhập thủ công"
> App (`DOC-v1.0-06` KP-01 §10.9): "Auto-fill từ `stag_anhdc4@fpt.com` trả về SĐT người nhận `0000286248` → **chính app báo "Số điện thoại không hợp lệ"** cho giá trị do nó tự điền."

**Source Location:** `DOC-v1.0-01 §D1b · US-D18 · Acceptance Criteria · L168` · `§D8.1 · L366` ⟷ `DOC-v1.0-06 KP-01 §10.9 "KB-VIBE-08"`

**Analyst Note:** `US-D18` cho **nguyên văn 2 thông báo** ⇒ assert được text (khác đa số trường hợp trong dự án này). Cơ chế đã được vibe-test xác nhận đúng 2 chiều (VR-001 #3, VR-002 `TC_04.24` PASS) ⇒ `SC-ORD-018` để **P1** vì là đường đi chính của B2. `SC-ORD-021` là nghịch lý app tự sinh dữ liệu rồi tự từ chối — nghi vấn **bug data hoặc bug validate**, chưa xác định nhánh nào ⇒ Then ghi rõ cả 2 khả năng.

##### SC-ORD-022 / SC-ORD-023 / SC-ORD-024 — Nhóm NGƯỜI NHẬN (bắt buộc · validate · địa chỉ khác nhau)

**Source Quote:**
> Rule (`DOC-v1.0-06` KP-01 §3 KB-ORD-01): "BA/PO xác nhận (2026-07-27) **CÓ** rule bắt buộc — trái với prototype (cho để trống tất cả): … Bước 2: thông tin `Người nhận` bắt buộc"
> Hành vi (`DOC-v1.0-02` §7 dòng 2): "Không có validate bắt buộc | Tên/SĐT/địa chỉ Người nhận có thể để trống hoàn toàn mà vẫn đăng tin thành công."
> Spec (`DOC-v1.0-01` §D8.1 L367-369): "Tên người nhận | Có | Tự điền từ danh bạ | Không để trống, 2–60 ký tự" · "Số điện thoại | Có | … | Số điện thoại VN hợp lệ (10 số, đầu 0)…" · "Địa chỉ giao hàng | Có | … | Không để trống; phải khác địa chỉ lấy hàng"

**Source Location:** `DOC-v1.0-01 §D8.1 · nhóm "▸ Nhóm: NGƯỜI NHẬN" · L366-369` ⟷ `DOC-v1.0-02 §7 · bảng · dòng 2` ⟷ `DOC-v1.0-06 KP-01 §3 "KB-ORD-01"`

**Analyst Note:** `C-ORD-01` Resolved: **CÓ** rule bắt buộc ⇒ `SC-ORD-022` (P1) viết theo rule, **dự kiến FAIL nếu app còn hành vi prototype**. `SC-ORD-023` gộp validate 2 trường theo **quyết định altitude** (xem `CHANGELOG §2` ràng buộc 8) — generate-tc sẽ fan-out EP/BVA thành nhiều TC. `SC-ORD-024` tách riêng vì là rule **cross-field** (so 2 trường với nhau), khác bản chất với validate 1 trường.

##### SC-ORD-025 / SC-ORD-026 / SC-ORD-027 — Địa chỉ: autocomplete · phải chọn gợi ý · preset 6 văn phòng

**Source Quote:**
> Nguồn A (`DOC-v1.0-06` KP-01 §3 KB-ORD-06): "Gõ text tự do → hiện dropdown gợi ý danh sách văn phòng khớp từ DB, **không phân biệt hoa/thường**. **Phải chạm chọn gợi ý** thì giá trị mới được lưu; gõ text mà không chọn thì field không giữ giá trị."
> Nguồn B (`DOC-v1.0-01` §D3 `LOC-03` L246): "LOC-03 | Quick-select văn phòng FPT | Hiển thị preset 6 văn phòng (+ mở rộng theo tỉnh)"
> Nguồn C (`DOC-v1.0-01` §D1b `US-D01` L164): "mỗi điểm lấy/giao chỉ có 1 input địa chỉ (không chip gợi ý)"

**Source Location:** `DOC-v1.0-06 KP-01 §3 "KB-ORD-06"` ⟷ `DOC-v1.0-01 §D3 · L246` ⟷ `§D1b · US-D01 · L164`

**Analyst Note:** ⚠️ **3 nguồn, 3 cơ chế cho cùng 1 field.** `KB-ORD-06` có bằng chứng mạnh nhất (BA trả lời 2026-07-29 + VR-001 #5 + VR-002 `TC_04.29` PASS) ⇒ 2 SC assert theo autocomplete; `LOC-03` chỉ được SC dạng GAP. ⚠️ **Hệ quả automation** (ghi sẵn cho `implement-automation`): phải **tap suggestion tường minh**, `set text` đơn thuần sẽ không lưu giá trị — và dropdown gợi ý *"không expose locator phân biệt"* (`KP-01` §10.12) nên có thể phải tap theo toạ độ.

##### SC-ORD-028 / SC-ORD-029 / SC-ORD-030 — Ngày và khung giờ

**Source Quote:**
> Spec (`DOC-v1.0-01` §D8.1 L370-372): "Từ ngày | Có | Ngày hiện tại | … Không chọn ngày trong quá khứ" · "Đến ngày | Có | Ngày hiện tại | … Phải ≥ Từ ngày…" · "Khung giờ (từ – đến) | Có | 17:00 – 18:30 | đến > từ; khoảng tối thiểu 30 phút"
> App (`DOC-v1.0-06` KP-01 §10.11): "Giá trị mặc định (vd 11:10–11:40) **hết hạn** khi form mở lâu (~15 phút), app tự bật validate *"phải muộn hơn hiện tại"*. **Không phải lỗi app.**"

**Source Location:** `DOC-v1.0-01 §D8.1 · L370-372` ⟷ `DOC-v1.0-06 KP-01 §10.11 "KB-VIBE-10"`

**Analyst Note:** Biên quan trọng: `Đến ngày = Từ ngày` **hợp lệ** (spec dùng "≥") và khung giờ cách **đúng 30 phút hợp lệ / 29 phút chặn**. `SC-ORD-030` ghi nhận rule **không có trong doc** (phải muộn hơn hiện tại) — quan trọng cho automation: ⛔ **không hardcode giờ**, chọn tương đối so với "now" (`Project_rule §Test Data Rules`). Lưu ý mặc định 3 nguồn khác nhau (`17:00–18:30` BRD · `05:00 PM–06:30 PM` PRD · `11:10–11:40` app) ⇒ ⛔ không assert giá trị mặc định cứng.

##### SC-ORD-031 / SC-ORD-032 / SC-ORD-033 / SC-ORD-034 — Bước 3/3 (tóm tắt · banner · checkbox · consent)

**Source Quote:**
> Spec (`DOC-v1.0-01` §D3 `ORD-09` L245): "ORD-09 | Consent điều khoản trước khi đăng | Bắt buộc tick "đồng ý tự chịu trách nhiệm""
> Spec (`DOC-v1.0-01` §D8.1 L373): "Xác nhận điều khoản | Có | **Chưa tick** | Bắt buộc tick mới bật được nút Đăng tin (tự thoả thuận, app không bảo hiểm/không vận chuyển)"
> Mâu thuẫn (`DOC-v1.0-02` §3.5.3): "Checkbox điều khoản | **Mặc định đã tick sẵn** — "Tôi tự chịu trách nhiệm về hàng hoá và thoả thuận với người mang giúp""
> App (`DOC-v1.0-06` KP-01 §10.7): "Quan sát thực tế ở Bước 3/3: **chưa tick**, phải chạm tay mới bật được nút "Đăng tin ngay"."

**Source Location:** `DOC-v1.0-01 §D3 · L245` · `§D8.1 · L373` ⟷ `DOC-v1.0-02 §3.5.3 · bảng · dòng "Checkbox điều khoản"` ⟷ `DOC-v1.0-06 KP-01 §10.7 "KB-VIBE-06"`

**Analyst Note:** ⭐ Mâu thuẫn **giá trị mặc định checkbox**: `D8.1` + app STG = **chưa tick** ⟷ PRD demo = **tick sẵn**. BRD (mới hơn, 27/07) + bằng chứng app thắng ⇒ chốt **chưa tick**; TC `TC_04.71` của đợt cũ expected *"tick sẵn"* là **sai nguồn** (`KP-04 §4` liệt là lỗi #3). `SC-ORD-034` (P1) là rule cứng có 2 nguồn BRD đồng thuận. Banner hàng cấm ở `SC-ORD-032` chỉ là **thông tin tĩnh** — không kèm validate (xem `SC-ORD-035`).

##### SC-ORD-035 — [GAP] Hàng cấm không bị chặn ở v1.0

**Source Quote:**
> Rule (`DOC-v1.0-01` §A8 L115): "Hàng cấm (thuốc, vũ khí, chất nguy hiểm, phi pháp) không được đăng."
> Phán quyết (`DOC-v1.0-06` KP-01 §3 KB-ORD-03): "Chip "Thuốc/Y tế" vẫn chọn được bình thường dù nguyên tắc cấm gửi thuốc. Banner cảnh báo chỉ là **thông tin tĩnh**, không có validate chặn theo danh mục."

**Source Location:** `DOC-v1.0-01 §A8 · blockquote pháp lý · L115` (và `§D4 BR-ORD-04 · L263`) ⟷ `DOC-v1.0-06 KP-01 §3 "KB-ORD-03"`

**Analyst Note:** `C-ORD-04` Resolved 2026-07-27: **v1.0 không chặn**. ⇒ SC ghi nhận **trạng thái hiện tại** để version sau có mốc so sánh; ⛔ **KHÔNG viết TC negative "chọn Thuốc/Y tế → bị chặn"** (đợt cũ đã tránh đúng — `KB-ORD-03` ghi rõ "không viết TC negative"). Đây là ví dụ mẫu của việc **rule tồn tại trong doc nhưng chưa triển khai** — khác hoàn toàn với bug.

##### SC-ORD-036 / SC-ORD-037 / SC-ORD-038 — Sau khi đăng (Đơn của tôi · màn thành công · mã tin)

**Source Quote:**
> Spec (`DOC-v1.0-01` §D1b `US-D02` L165): "Sau khi bấm "Đăng tin ngay" → màn "Đăng tin thành công" (**KHÔNG hiển thị mã đơn** — mã kỹ thuật vô nghĩa với người dùng); tin xuất hiện ở "Đơn của tôi" trên trang chủ"
> PRD (`DOC-v1.0-02` §3.5.4): "Đăng tin thành công — 2 lựa chọn: Theo dõi đơn / Về trang chủ"
> Mâu thuẫn (`DOC-v1.0-06` KP-05 §2.2): "Một bản **CÓ** trường "Mã tin" (vd `#ECO-2026-0451`), một bản **KHÔNG**. Đồng thời đối lập trực tiếp với `US-D02`"

**Source Location:** `DOC-v1.0-01 §D1b · US-D02 · Acceptance Criteria · L165` ⟷ `DOC-v1.0-02 §3.5.4` ⟷ `DOC-v1.0-06 KP-05 §2.2` (nguồn gốc: `DOC-v1.0-04`, 2 biến thể cùng board)

**Analyst Note:** `C-ORD-05` **Open** — mâu thuẫn **ngay trong nguồn thiết kế**. ⇒ `SC-ORD-037` assert 2 lựa chọn điều hướng (có nguồn rõ); `SC-ORD-038` **cố ý không assert** có/không có mã tin. `SC-ORD-036` giữ ở `ORD` (không đẩy sang `HOME`) vì nó là **hệ quả của hành động đăng tin**, oracle thuộc luồng đăng.

##### SC-ORD-039 / SC-ORD-040 / SC-ORD-041 / SC-ORD-042 — Luồng OFFER (form 1 trang · điểm A/B · ghi nhận tuyến · không công khai)

**Source Quote:**
> Spec (`DOC-v1.0-01` §D1b `US-D10` L184): "Màn đăng tin OFFER 1 màn duy nhất, các trường: Điểm xuất phát, Điểm đến, Khung giờ, Tên, SĐT + tick đồng ý điều khoản; có dòng chú thích mô tả đang di chuyển & có thể nhận giao hộ"
> Spec (`DOC-v1.0-01` §D1b `US-D11` L185): "Sau khi đăng → màn "Đã ghi nhận tuyến đường" giải thích: tuyến được lưu (không công khai), khi có người cần gửi trùng điểm lấy & điểm giao hệ thống sẽ gửi thông báo để bạn xem xét"
> Spec (`DOC-v1.0-01` §D8.2 L381-382): "Điểm xuất phát | Có | Điền sẵn vị trí làm việc của người giao …; để trống nếu hệ thống chưa có thông tin | Không để trống khi submit, tối đa 200 ký tự. **User sửa được**" · "Điểm đến | Có | Trống | Không để trống; **phải khác điểm xuất phát**"
> App (`DOC-v1.0-06` KP-01 §3 KB-ORD-11): "form một trang, **không có step indicator "Bước x/3"**"

**Source Location:** `DOC-v1.0-01 §D1b · US-D10/US-D11 · L184-185` · `§D8.2 · L379-386` ⟷ `DOC-v1.0-02 §4.4` ⟷ `DOC-v1.0-06 KP-01 §3 "KB-ORD-11"`

**Analyst Note:** ⚠️ Đáng chú ý: `D8.2` **cho phép** Điểm xuất phát *"để trống nếu hệ thống chưa có thông tin"* và *"User sửa được"* — **khác `D8.1`** nơi Tên người gửi là *"Chỉ đọc"* và Địa chỉ lấy hàng phải pre-fill. Tức spec luồng OFFER **đã lường trước** việc pre-fill có thể thiếu, luồng NEED thì không ⇒ củng cố việc `SC-ORD-016` là gap thật của luồng NEED. `SC-ORD-042` để **P1** vì đó là rule quyền riêng tư (tuyến không công khai), và là mặt đối của `SC-FEED-001`.

##### SC-ORD-043 / SC-ORD-044 — Sửa tin (cho phép ở Chờ ghép · khoá từ Đã ghép)

**Source Quote:**
> "BR-EDIT-01 | Chỉ được chỉnh sửa tin khi còn "Chờ ghép" (POSTED); đã MATCHED trở đi khoá chỉnh sửa"
> "OPR-10 | Điều kiện chỉnh sửa đơn | Chỉ được sửa đơn khi chưa có ai nhận (trạng thái "Chờ ghép"); ngay khi đã có người nhận (Đã ghép trở đi) → khoá chỉnh sửa hoàn toàn"
> "Nút "Chỉnh sửa" chỉ hiện ở trạng thái Chờ ghép (POSTED); mở màn giống tạo đơn nhưng đã điền sẵn; có nút "Cập nhật" & "Huỷ chỉnh sửa"; **sau IN_TRANSIT không cho sửa**"

**Source Location:** `DOC-v1.0-01 §D4 · BR-EDIT-01 · L269` · `§D7 · OPR-10 · L346` · `§D1b · US-D19 · L169` (và `§D3 ORD-10 · L252`)

**Analyst Note:** **4 nguồn** — rule mạnh nhất module. ⚠️ Nhưng `US-D19` ghi *"sau **IN_TRANSIT** không cho sửa"* trong khi `BR-EDIT-01`+`OPR-10` ghi *"từ **MATCHED** trở đi khoá"* ⇒ **lệch 1 trạng thái**. Chọn rule chuyên trách (2 nguồn, dùng từ "khoá hoàn toàn") ⇒ `SC-ORD-044` assert khoá **từ MATCHED**. Nếu app cho sửa ở MATCHED thì đó là bug theo `BR-EDIT-01`, ⛔ đừng viện `US-D19` để hợp thức hoá.

##### SC-ORD-045 — Tin tự hết hạn theo "Đến ngày"

**Source Quote:**
> Spec A (`DOC-v1.0-01` §D3 `ORD-06` L244): "Tin hết hạn | Quá hạn chưa ghép → gửi thông báo để người đăng tự gỡ/đăng lại; **hệ thống không tự can thiệp ở phase này**"
> Spec B (`DOC-v1.0-01` §D1b `US-D04` L166): "Quá hạn cấu hình mà chưa MATCHED → **tự chuyển EXPIRED**, hiển thị badge "Hết hạn" ở tab hoàn tất kèm lý do "Không có ai nhận mang giúp trong thời gian đăng""
> Phán quyết (`DOC-v1.0-06` KP-01 §3 KB-ORD-02): "hạn tin **không phải hằng số hệ thống** — bằng đúng khoảng ngày user chọn ở Bước 2/3; đến đúng **"Đến ngày"** thì tin tự chuyển `EXPIRED`."

**Source Location:** `DOC-v1.0-01 §D3 · L244` ⟷ `§D1b · US-D04 · L166` ⟷ `DOC-v1.0-06 KP-01 §3 "KB-ORD-02"`

**Analyst Note:** ⚠️ **Hai spec mô tả 2 hành vi trái nhau** trong cùng BRD: `ORD-06` *"hệ thống không tự can thiệp"* ⟷ `US-D04` *"tự chuyển EXPIRED"*. `C-ORD-03` Resolved chốt theo `US-D04` + app. Lý do hiển thị có **nguyên văn** ở 2 nguồn (`US-D04` và `KB-ORD-07` #4) ⇒ assert được text. ⚠️ Lịch sử: phân tích trước từng chốt nhầm là **"Từ ngày"**, sau đảo lại thành **"Đến ngày"** — dùng **"Đến ngày"**. Given cần đơn có "Đến ngày" đã trôi qua ⇒ khó seed, xem `RISK-ORD-06`.

##### SC-ORD-046 — Timeline tin có mốc đăng tin

**Source Quote:**
> "ORD-04 | Tin có timeline trạng thái | Lịch sử đầy đủ với timestamp"

**Source Location:** `DOC-v1.0-01 §D3 · bảng ID/Yêu cầu/AC · L243`

**Analyst Note:** SC ở đây chỉ phủ **mốc đầu tiên** ("Đăng tin" + timestamp) — các mốc còn lại (Ghép thành công · Lấy hàng · Đã giao · Hoàn thành) thuộc `DLV` (`REQ-DLV-010`) vì phát sinh theo state-transition của giao nhận. Cross-ref `TS-01`/`TS-02` (log không sửa được).

##### SC-ORD-047 / SC-ORD-048 / SC-ORD-049 — Quy tắc chung form (`VAL-01`/`VAL-02`/`VAL-03`)

**Source Quote:**
> "VAL-01 | Nút submit vô hiệu hoá đến khi mọi trường bắt buộc hợp lệ + đã tick điều khoản"
> "VAL-02 | Lỗi hiện ngay dưới ô nhập khi rời ô (on blur), không dùng popup; cuộn tới ô lỗi đầu tiên khi bấm submit"
> "VAL-03 | Tự cắt khoảng trắng đầu/cuối; chuẩn hoá SĐT (bỏ khoảng trắng, dấu chấm) trước khi lưu"

**Source Location:** `DOC-v1.0-01 §D8.3 "Quy tắc chung cho form" · bảng ID/Quy tắc · L392-394`

**Analyst Note:** 3 rule **cross-field**, áp cho **cả 2 form** (NEED wizard + OFFER) ⇒ Given của `SC-ORD-047` nêu rõ cả 2 form. `VAL-01` đã có bằng chứng đúng một phần (`KB-VIBE-03`: nút disabled khi thiếu Giá trị hàng). `VAL-03` cần verify **giá trị đã lưu** (không chỉ giá trị hiển thị) ⇒ oracle là dữ liệu tin sau khi đăng, xem lại ở Chi tiết tin. `VAL-04` (lý do huỷ ≥5 ký tự) **không** ở module này — home `CNL`.

##### SC-ORD-050 — [GAP] Thoát giữa wizard

**Source Quote:**
> "**C-ORD-08** | Bấm Reset/thoát giữa chừng wizard có xoá dữ liệu form đã nhập không? | Chưa hỏi BA. Không có mô tả trong BRD/PRD"

**Source Location:** `DOC-v1.0-06 KP-02 §5 · bảng "Nhóm Open" · dòng "C-ORD-08"`

**Analyst Note:** *(Implicit — không có quote đặc tả.)* Hành vi thoát/vào lại **đã được chứng minh có ảnh hưởng dữ liệu form**: `KB-VIBE-04` ghi giá trị Tên bị xoá *"**không tự phục hồi** trong cùng phiên wizard — phải thoát ra vào lại từ đầu Bước 1/3 mới load lại tên"* ⇒ tức là thoát/vào lại **có** reset một phần dữ liệu. Cần chốt để biết đó là thiết kế hay hệ quả của bug `SC-ORD-015`.

##### SC-ORD-051 — [GAP] Ngưỡng giá trị hàng bằng số tiền

**Source Quote:**
> "BR-ORD-03 | Giá trị hàng trong ngưỡng cấu hình; trên ngưỡng → cảnh báo nên mua bảo hiểm (phase sau)"

**Source Location:** `DOC-v1.0-01 §D4 "Business Rules & Permission Matrix" · bảng Rule/Mô tả · L262`

**Analyst Note:** `C-ORD-02` Resolved — Out of scope v1.0 (**từng là BLOCKER cứng**, gỡ 2026-07-27). ⚠️ Phân biệt rõ: ngưỡng **bằng số tiền** = out of scope ≠ cảnh báo theo **mức định tính "Cao"** (`SC-ORD-009`) = **CÓ ở v1.0**. Đây là cặp dễ trộn nhất của module; SC này tồn tại để chốt ranh giới, ⛔ không viết TC nhập số tiền.

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| — | *(không có — v1.0 là version đầu của chuỗi phân tích mới)* | — | — | — | — |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
