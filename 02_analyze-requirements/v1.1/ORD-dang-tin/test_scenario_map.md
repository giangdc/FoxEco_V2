---
id: v1.1/ORD-dang-tin/scenario-map
title: Test Scenario Map — v1.1 · Module ORD
type: scenario-map
version: v1.1
sprint: 1
module: ORD
counts:
  req: 28
  sc: 65
  new: 14
  modified: 12
  carried: 39
  deprecated: 0
  p1: 9
  p2: 36
  p3: 20
status: ANALYZED
updated: 2026-09-15
---

# Test Scenario Map — v1.1 · Module ORD

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module ORD **tính tới v1.1** (bao gồm CARRIED từ v1.0).
> Parent: `v1.0/ORD-dang-tin/` — 39 SC không đổi (CARRIED), 12 SC MODIFIED (giữ ID v1.0), 14 SC NEW.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Delta lần này fan-out theo: mỗi **field bắt buộc mới** = 1 SC negative · **3 nhánh** của tra danh bạ · **4 ràng buộc ảnh** (bắt buộc / trần / dung lượng+định dạng / bộ đếm) · validation **liên-trường** · tiện ích dùng chung (`FR18`).
> Trần: PRD liệt kê ~40 dòng field spec cho `FR01` — ⛔ **không tạo 1 SC/field**. Field chỉ chi tiết hoá rule đã có SC ⇒ **siết Then của SC sẵn có**; chỉ field mang **hành vi mới** (bắt buộc / chặn luồng / cross-field) mới sinh SC. Đây là áp `MASTER-MEMORY §9` biện pháp (b) — giảm rác thay vì fan-out máy móc.

## Tổng quan
- Tổng số scenarios (tính tới v1.1): **65** (NEW: 14, MODIFIED: 12, CARRIED: 39)
- Phân bổ priority: P1: 9 | P2: 36 | P3: 20
- Delta lớn nhất: **ảnh món hàng chuyển từ *không rõ* sang *BẮT BUỘC ≥ 1, chặn sang bước 2*** (`SC-ORD-054`, P1) và **tra danh bạ nội bộ** — tích hợp hệ thống ngoài được nêu tên lần đầu (`SC-ORD-058..060`).
- 🔴 CL: **4 Resolved** (`C-ORD-05` `C-ORD-08` `C-ORD-10` `C-ORD-11`) · **1 Partially** (`C-ORD-09`) · **1 MỞ LẠI** (`C-ORD-04` — PRD tự mâu thuẫn) · **1 mở mới** (`C-ORD-13`).

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### ORD — Đăng tin & Quản lý tin (delta v1.1)

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-ORD-052 | Khối lượng bắt buộc — thiếu thì chặn | REQ-ORD-024 | DOC-v1.1-01 §8.1.1 BR01-02 · §8.1.4 · §6.2 AC-02.1.02 | Đang ở bước 1 wizard, đã chọn Loại hàng + Giá trị hàng + có ảnh | Để **Khối lượng** ở trạng thái "chưa chọn", bấm Tiếp tục | Nút Tiếp tục **không bật** / bị chặn, có lỗi ở ô Khối lượng. Chọn `> 10 kg` thì **vẫn đăng được bình thường** (`BR01-02`: *"không chặn theo ngưỡng"*) | P2 | Business Rule | NEW |
| SC-ORD-053 | Kích thước bắt buộc — thiếu thì chặn | REQ-ORD-024 | DOC-v1.1-01 §8.1.1 BR01-02 · §8.1.4 | Như trên, đã chọn Khối lượng | Để **Kích thước** "chưa chọn", bấm Tiếp tục | Bị chặn + lỗi ở ô Kích thước. Chọn `Lớn · > 20×20 cm` thì **vẫn đăng được** | P2 | Business Rule | NEW |
| SC-ORD-054 | Ảnh BẮT BUỘC ≥ 1 — thiếu thì chặn sang bước 2 | REQ-ORD-006 | DOC-v1.1-01 §8.1.1 BR01-01 · §6.2 AC-03.1.02 | Bước 1, đã điền đủ 3 dropdown, **chưa tải ảnh nào** | Bấm Tiếp tục | **Bị chặn sang bước 2** (`BR01-01`: *"Thiếu ảnh thì chặn sang bước 2"*), có lỗi ở ô ảnh | P1 | Business Rule | NEW |
| SC-ORD-055 | Ảnh vượt 5MB hoặc sai định dạng bị từ chối | REQ-ORD-006 | DOC-v1.1-01 §8.1.1 BR01-01 · §8.18.1 BR18-02 · §6.2 AC-03.2.02 | Bước 1, ô tải ảnh sẵn sàng | Lần lượt thử: 1 ảnh **> 5MB**; 1 file **không phải JPG/PNG** | Cả 2 **bị từ chối** kèm thông báo; bộ đếm `n/5` **không tăng** | P2 | Business Rule | NEW |
| SC-ORD-056 | Đủ 5 ảnh → ẩn nút thêm + bộ đếm "n/5" | REQ-ORD-006 | DOC-v1.1-01 §8.18.1 BR18-02 · §8.18.2 VAL-07 · §6.2 AC-03.2.01 | Bước 1 | Tải lần lượt 1→5 ảnh, quan sát bộ đếm sau mỗi lần; rồi thử thêm ảnh thứ 6 | Bộ đếm hiện đúng `1/5`…`5/5`; khi đủ 5 thì **nút thêm bị ẩn**; **xoá được từng ảnh** và bộ đếm giảm tương ứng | P2 | Business Rule | NEW |
| SC-ORD-057 | Carousel + lightbox đa ảnh | REQ-ORD-026 | DOC-v1.1-01 §8.18.1 BR18-03 · §6.2 AC-03.1.01 | 1 tin đã đăng có **≥ 2 ảnh**, đang mở màn chi tiết tin | Lướt ngang dải ảnh; chạm 1 ảnh; đóng bằng nút X; mở lại và đóng bằng chạm nền | Carousel lướt ngang có **badge đếm dạng `"2/5"`**; lightbox **nền tối, giữ đúng tỉ lệ ảnh**; đóng được bằng **cả 2 cách** | P3 | UI | NEW |
| SC-ORD-058 | Tra danh bạ thành công → tự điền 3 trường, vẫn sửa được | REQ-ORD-008 | DOC-v1.1-01 §8.1.1 BR01-09 · §8.1.3 bước 4 · §6.2 AC-04.1.01 | Bước 2 wizard; có sẵn 1 **email công ty CÓ trong danh bạ nội bộ** | Nhập email đó, rời ô | **Tên · số điện thoại · địa chỉ giao** được tự điền; cả 3 ô **vẫn sửa được** (không bị khoá) | P1 | Functional | NEW |
| SC-ORD-059 | Không thấy trong danh bạ → cho nhập thủ công | REQ-ORD-008 | DOC-v1.1-01 §8.1.1 BR01-09 · §6.2 AC-04.1.02 | Bước 2; có 1 email **đúng tên miền nội bộ nhưng KHÔNG có trong danh bạ** | Nhập email đó, rời ô | 3 ô **mở cho nhập tay** (không bị khoá, không báo lỗi chặn); luồng đăng tin vẫn đi tiếp được | P2 | Functional | NEW |
| SC-ORD-060 | Email sai định dạng hoặc ngoài tên miền nội bộ | REQ-ORD-008 | DOC-v1.1-01 §8.1.4 · §6.2 AC-04.2.01 | Bước 2 | Lần lượt nhập: email **sai định dạng**; email đúng định dạng nhưng **ngoài tên miền nội bộ** | Cả 2 **bị chặn** kèm lỗi; **không kích hoạt tra danh bạ** | P2 | Business Rule | NEW |
| SC-ORD-061 | Khai người nhận uỷ quyền — validate tên & SĐT | REQ-ORD-023 | DOC-v1.1-01 §8.1.1 BR01-06 · §8.1.4 · §6.2 AC-05.1.01, AC-05.1.02 | Bước 2, khối "+ Thêm người nhận uỷ quyền" đang **thu gọn** | Mở khối; nhập tên hợp lệ + SĐT **sai định dạng**; sửa lại SĐT đúng; hoàn tất đăng tin | SĐT sai → **báo lỗi, chặn**; SĐT đúng → đăng được; dữ liệu uỷ quyền gắn vào đơn kèm nhãn **"Người gửi chỉ định"**. Biên tên: **2** và **60** ký tự đều hợp lệ | P2 | Business Rule | NEW |
| SC-ORD-062 | Xoá khối uỷ quyền sau khi đã mở | REQ-ORD-023 | DOC-v1.1-01 §6.2 AC-05.2.01 | Bước 2, khối uỷ quyền **đã mở và đã điền** | Xoá/đóng khối rồi hoàn tất đăng tin | Đơn tạo thành công **không mang dữ liệu uỷ quyền**; ⛔ không báo lỗi "thiếu trường" (khối là **không bắt buộc**) | P3 | Business Rule | NEW |
| SC-ORD-063 | Địa chỉ giao phải KHÁC địa chỉ lấy | REQ-ORD-028, REQ-ORD-009 | DOC-v1.1-01 §8.1.4 dòng "Địa chỉ giao hàng" | Bước 2, đã có địa chỉ lấy hàng | Nhập địa chỉ giao **trùng hệt** địa chỉ lấy → quan sát; rồi nhập bản **chỉ khác khoảng trắng đầu/cuối** → quan sát | Trùng hệt → **bị chặn**. Khác mỗi khoảng trắng → GHI NHẬN hành vi (`VAL-03` có trim, nhưng PRD **không định nghĩa** so sánh hoa/thường) — ⛔ không assert cứng | P2 | Business Rule | NEW |
| SC-ORD-064 | Copy nhanh địa chỉ và số điện thoại | REQ-ORD-025 | DOC-v1.1-01 §8.18.1 BR18-04 | Đang ở màn **chi tiết tin** của 1 tin có địa chỉ giao + SĐT | Bấm icon copy cạnh địa chỉ; dán ra ô nhập bất kỳ; lặp với icon copy cạnh SĐT | Nội dung vào clipboard **đúng nguyên văn**; icon **đổi trạng thái + màu xanh** rồi trở lại sau **khoảng 2 giây** (dung sai — ⛔ không bấm giờ đòi đúng 1,8s) | P3 | UI | NEW |
| SC-ORD-065 | Ảnh đã gắn mốc nhật ký thì không xoá được | REQ-ORD-027 | DOC-v1.1-01 §8.18.1 BR18-05 · BR18-02 | Bước 1 đang soạn tin có 2 ảnh (**chưa ghi mốc**) | Xoá 1 ảnh lúc đang soạn → quan sát; đăng tin; mở lại tin đã đăng và thử xoá ảnh | Lúc **đang soạn**: xoá được (`BR18-02`). Sau khi **đã đăng**: ⛔ **không xoá được** (`BR18-05`, *"phục vụ truy vết"*). Ranh giới là **thời điểm ghi mốc** | P3 | Business Rule | NEW |
| SC-ORD-005 | Loại hàng — 8 giá trị, mặc định "Tài liệu" *(doc)* vs app | REQ-ORD-003 | DOC-v1.1-01 §8.1.4 dòng "Loại hàng" | Bước 1 wizard, chưa chạm vào field Loại hàng | Đọc giá trị **mặc định** và liệt kê toàn bộ lựa chọn | Có đúng **8** lựa chọn. ⚠ **Nhãn đầu tiên**: PRD ghi "Tài liệu", app STG hiện "Giấy tờ, hồ sơ" ⇒ **GHI NHẬN, ⛔ KHÔNG assert cứng** cho tới khi `C-ORD-09` chốt (ràng buộc 4, `03_test-cases/v1.0/CHANGELOG.md §2` vẫn hiệu lực) | P2 | UI | MODIFIED |
| SC-ORD-012 | Ảnh món hàng — nay là trường BẮT BUỘC | REQ-ORD-006 | DOC-v1.1-01 §8.1.1 BR01-01 | Bước 1 wizard | Tải 1 ảnh JPG hợp lệ | Ảnh hiện trong ô, bộ đếm `1/5`; luồng đi tiếp được. ⚠ Ô ảnh phải mang dấu hiệu **bắt buộc** (khác v1.0 — v1.0 không rõ có bắt buộc không) | P2 | Functional | MODIFIED |
| SC-ORD-025 | Địa chỉ lấy hàng PHẢI prefill từ hồ sơ | REQ-ORD-007, REQ-ORD-010 | DOC-v1.1-01 §8.1.4 · §6.2 AC-30.1.01 | Tài khoản **ĐÃ đặt địa chỉ mặc định** ở "Cập nhật thông tin" (xác nhận trước khi chạy) | Mở wizard đăng tin, sang bước 2, đọc ô Địa chỉ lấy hàng | Ô **đã điền sẵn** đúng địa chỉ mặc định và **sửa được**. ⚠ Nếu trống → **BUG** (`C-ORD-10` Resolved: prefill là hành vi đặc tả) | P2 | Functional | MODIFIED |
| SC-ORD-026 | Cơ chế ô địa chỉ — văn bản tự do, ≤ 200 ký tự | REQ-ORD-010 | DOC-v1.1-01 §8.1.4 | Bước 2 wizard | Quan sát kiểu ô; nhập chuỗi 200 và 201 ký tự | Là **ô văn bản tự do** (⛔ không phải preset 6 văn phòng, không chip gợi ý — `C-ORD-11` Resolved); 200 ký tự **được**, 201 **bị chặn/cắt** | P3 | Business Rule | MODIFIED |
| SC-ORD-028 | Khoảng ngày ≤ 7 ngày, không quá khứ, Đến ≥ Từ | REQ-ORD-011 | DOC-v1.1-01 §8.1.1 BR01-04 · §8.1.4 · §6.2 AC-06.1.02 | Bước 2 wizard | Thử: ngày quá khứ · Đến ngày < Từ ngày · khoảng **đúng 7 ngày** · khoảng **8 ngày** | 3 trường hợp đầu theo đúng rule (2 đầu bị chặn, 7 ngày **hợp lệ**); **8 ngày bị chặn** | P2 | Business Rule | MODIFIED |
| SC-ORD-029 | Buổi "Giờ nào cũng được" loại trừ các buổi khác | REQ-ORD-012 | DOC-v1.1-01 §8.1.1 BR01-04 · §8.1.4 · §6.2 AC-06.2.01 | Bước 2, đã chọn sẵn "Sáng" và "Chiều" | Chọn thêm **"Giờ nào cũng được"** | 2 buổi đang chọn **tự bỏ chọn**; chỉ còn "Giờ nào cũng được". Mặc định ban đầu của field là **"Sau giờ làm"** | P2 | Business Rule | MODIFIED |
| SC-ORD-036 | Màn "Đăng tin thành công" — KHÔNG có mã đơn | REQ-ORD-015 | DOC-v1.1-01 §6.2 AC-07.1.01 · §8.1.3 bước 8 | Vừa bấm "Đăng tin ngay" với dữ liệu hợp lệ | Quan sát toàn bộ màn thành công | ⛔ **KHÔNG hiển thị mã đơn** (`C-ORD-05` Resolved); có **nút về trang chủ** và **nút xem đơn vừa đăng**; tin xuất hiện ngay ở "Tin mới" (trang chủ) và "Đơn của tôi" | P2 | UI | MODIFIED |
| SC-ORD-043 | Sửa tin khi còn POSTED — form nạp sẵn + Huỷ chỉnh sửa | REQ-ORD-017 | DOC-v1.1-01 §8.5.1 BR05-01/BR05-02 · §8.18.2 VAL-05 · §6.2 AC-08.1.01 | 1 tin của chính mình đang ở `POSTED` | Bấm "Chỉnh sửa", đổi địa chỉ giao, bấm "Cập nhật"; lần 2 vào sửa rồi bấm "Huỷ chỉnh sửa" | Form **nạp sẵn toàn bộ dữ liệu cũ**; sau Cập nhật đơn **giữ `POSTED`** với dữ liệu mới; "Huỷ chỉnh sửa" **trả về dữ liệu cũ, không lưu** | P2 | Functional | MODIFIED |
| SC-ORD-044 | Từ MATCHED trở đi: nút Chỉnh sửa KHÔNG hiển thị | REQ-ORD-017 | DOC-v1.1-01 §8.5.1 BR05-01 · §6.2 AC-08.1.02 | 1 tin đã ở `MATCHED` hoặc muộn hơn | Mở màn theo dõi đơn của tin đó | Nút "Chỉnh sửa" **không hiển thị**. `BR05-01` còn nói *"request sửa bị từ chối"* và `AC-08.1.02` *"không ghi mốc vào nhật ký"* — ⚠ phần request là **backend**, GHI NHẬN, không verify qua UI | P2 | Business Rule | MODIFIED |
| SC-ORD-045 | Tin quá "Đến ngày" mà VẪN POSTED → EXPIRED | REQ-ORD-018 | DOC-v1.1-01 §8.5.1 BR05-03 · §6.2 AC-09.1.01 | 1 tin NEED có "Đến ngày" đã qua VÀ **chưa ai ghép** (vẫn `POSTED`) | Quan sát tin sau khi hết ngày cuối | Tin chuyển `EXPIRED`, **biến khỏi bảng tin và khỏi luồng khớp tuyến**. ⚠ Tin đã `MATCHED` rồi mới quá ngày thì **KHÔNG** chuyển `EXPIRED` (vế *"vẫn POSTED"* — v1.0 chưa nêu) | P2 | Business Rule | MODIFIED |
| SC-ORD-050 | Thoát giữa wizard — popup xác nhận, không lưu DRAFT | REQ-ORD-021 | DOC-v1.1-01 §6.2 AC-01.2.01 | Đang ở **bước 2** và đã điền một phần dữ liệu | Bấm quay lại/đóng wizard; lần 1 chọn "ở lại", lần 2 chọn "thoát"; rồi mở lại wizard | Hiện popup **đúng chuỗi** "Thoát và bỏ nội dung đã nhập?"; chọn **ở lại** → dữ liệu giữ nguyên; chọn **thoát** → không tạo tin và **mở lại là form trắng** (⛔ không có DRAFT) | P2 | Functional | MODIFIED |
| SC-ORD-041 | Tin OFFER: không tìm, không xem, không ngỏ ý được | REQ-ORD-016 | DOC-v1.1-01 §8.2.1 BR02-01 · §6.2 AC-20.1.01, AC-20.1.02 | Tài khoản A đã đăng 1 tin OFFER; đăng nhập tài khoản B (vai người gửi) | B mở bảng tin (cả 2 tab), dùng mọi chức năng tìm kiếm có sẵn để tìm tin OFFER của A | **Không có kết quả** và **không mở được chi tiết**. ⚠ Vế *"mở link trực tiếp"* của `AC-20.1.02` **không thực hiện được trên mobile app** (không có URL) ⇒ GHI NHẬN giới hạn, ⛔ không PASS chỉ vì không có đường thử | P2 | Business Rule | MODIFIED |

#### Source Detail per Scenario (verbatim quotes)

##### SC-ORD-054 / SC-ORD-055 / SC-ORD-056 / SC-ORD-012 — Ảnh món hàng: bắt buộc, trần 5, dung lượng, bộ đếm
📍 `DOC-v1.1-01 §8.1.1 BR01-01 · trang 33` · `§8.18.1 BR18-01 / BR18-02 · trang 52` · `§8.18.2 VAL-07 · trang 52` · `§6.2 AC-03.x · trang 19`

> `BR01-01`: "Ảnh món hàng là bắt buộc ≥ 1, tối đa 5 ảnh; mỗi ảnh ≤ 5MB, chỉ JPG/PNG. Thiếu ảnh thì chặn sang bước 2."

> `BR18-02`: "Mỗi ảnh ≤ 5MB, chỉ JPG/PNG; xoá được từng ảnh trước khi ghi mốc; ẩn nút thêm khi đủ 5; hiện bộ đếm "n/5"."

> `VAL-07`: "Ô tải ảnh: ẩn nút "Thêm ảnh" khi đã đủ 5; hiện bộ đếm "n/5"."

**Analyst Note (diff):** 🔴 **Đây là thay đổi hành vi thật, không phải chi tiết hoá.** v1.0 chỉ biết *"có field ảnh sản phẩm"* (`§D8.1 L360`) — **không biết có bắt buộc không** ⇒ `SC-ORD-012` dừng ở *"tải được ảnh"*. v1.1 nói **bắt buộc ≥ 1** kèm hệ quả cụ thể ***"Thiếu ảnh thì chặn sang bước 2"*** ⇒ đây là **điều kiện chặn luồng chính của tính năng chính**, nên `SC-ORD-054` là **P1**.
**Vì sao tách 3 SC mới thay vì gộp:** ba rule ràng buộc **ba thứ khác nhau** và fail độc lập — *bắt buộc* (chặn luồng), *hợp lệ của từng file* (dung lượng/định dạng), *trần tập hợp* (5 ảnh + bộ đếm + ẩn nút). Gộp lại thành 1 TC thì khi FAIL không biết vỡ ở đâu.
⚠️ **Rủi ro tiền đề:** nếu app STG **chưa siết** ảnh bắt buộc thì `SC-ORD-054` (P1) FAIL vì *"app chưa cập nhật"*, không phải lỗi logic — cần **vibe-test xác nhận trước `generate-tc`** (`RISK-ORD-09`).

---

##### SC-ORD-058 / SC-ORD-059 / SC-ORD-060 — Tra danh bạ nội bộ: 3 nhánh
📍 `DOC-v1.1-01 §8.1.1 BR01-09 · trang 34` · `§8.1.4 dòng "Email công ty người nhận" · trang 35` · `§6.2 AC-04.x · trang 20` · `§4 SCOPES Tích hợp · trang 9`

> `BR01-09`: "Email công ty người nhận được tra danh bạ nội bộ: tìm thấy thì tự điền tên · số điện thoại · địa chỉ (vẫn sửa được); không thấy thì cho nhập thủ công."

> §8.1.4: "Email công ty người nhận | Có | Văn bản · trống | Đúng định dạng và thuộc tên miền nội bộ; kích hoạt tra danh bạ"

> §4 SCOPES: "Danh bạ nội bộ — tra email công ty người nhận để tự điền tên · số điện thoại · địa chỉ"

**Analyst Note:** ⭐ **Tích hợp hệ thống ngoài được nêu tên lần đầu trong cả chuỗi phân tích.** v1.0 biết có autofill (`USR-EML`) nhưng **không biết nguồn dữ liệu** ⇒ không viết được TC cho nhánh *không tìm thấy* — một nhánh chắc chắn xảy ra trong thực tế (người nhận là CBNV mới, hoặc email gõ đúng nhưng chưa có trong danh bạ).
**Ba nhánh, ba SC** vì ba kết cục khác hẳn: tự điền + **vẫn sửa được** (mệnh đề trong ngoặc của `BR01-09`, dễ bị bỏ — nhiều app khoá ô sau autofill) · mở cho nhập tay · **chặn trước khi tra**. Nhánh 3 có **2 điều kiện chặn khác nhau** (sai định dạng ⟷ đúng định dạng nhưng **ngoài tên miền nội bộ**) — gộp 1 SC vì cùng kết cục và cùng thao tác.
🔴 **Rủi ro tiền đề lớn nhất của module:** cần **email thật có trong danh bạ** và **email đúng tên miền nhưng không có trong danh bạ**. Nếu STG chưa nối danh bạ thật thì cả 3 SC `BLOCKED` ⇒ mở `C-ORD-13`.

---

##### SC-ORD-005 — Loại hàng: PRD chốt được danh mục, nhưng nhãn vẫn lệch app
📍 `DOC-v1.1-01 §8.1.4 UI/Field Spec, dòng "Loại hàng" · trang 35`

> "Loại hàng | Có | Chọn 1 giá trị · mặc định Tài liệu | Tài liệu · Đồ điện tử · Thực phẩm · Hàng nhỏ · Đồ dễ vỡ · Quần áo · Thuốc/Y tế · Khác"

**Analyst Note (diff):** ⭐ **`C-ORD-09` — CL số 1 của dự án — được giải quyết ĐÚNG MỘT NỬA.**
**Nửa xong:** v1.0 có **3 nguồn cho 3 danh mục khác nhau** nên không biết lấy cái nào; nay có **một** danh mục chính thức, đủ 8 giá trị, kèm **giá trị mặc định**.
**Nửa chưa xong, và nặng hơn:** PRD ghi nhãn đầu là **"Tài liệu"**, app STG hiện **"Giấy tờ, hồ sơ"**. Đây là lệch **doc ⟷ app**, ở đúng một nhãn xuất hiện trong Steps của **rất nhiều TC** — chính là **lỗi #1 của đợt phân tích cũ**. Theo `Project_rule §Custom Rules §10.1` ⛔ không tự chọn bên. ⇒ SC assert **số lượng 8** (chắc chắn) và **ghi nhận** nhãn; ràng buộc 4 của `03_test-cases/v1.0/CHANGELOG.md §2` **vẫn hiệu lực**.
🔴 **Phát hiện phụ — PRD tự mâu thuẫn:** field spec để **"Thuốc/Y tế"** là giá trị hợp lệ, `BR01-07` lại viết *"Hàng cấm (**thuốc**, vũ khí, chất nguy hiểm, hàng phi pháp) **không được đăng**"*. Hai câu này **không thể cùng đúng**. ⇒ **`C-ORD-04` MỞ LẠI** (v1.0 đã Resolved *"KHÔNG chặn"*), xem `risk_assessment.md`.

---

##### SC-ORD-025 / SC-ORD-026 — Prefill địa chỉ lấy hàng và cơ chế ô địa chỉ
📍 `DOC-v1.1-01 §8.1.4 UI/Field Spec · trang 35` · `§6.2 AC-30.1.01 · trang 28`

> "Địa chỉ lấy hàng | Có | Văn bản · prefill địa chỉ mặc định | Không để trống, ≤ 200 ký tự"

> `AC-30.1.01`: "…Lần đăng tin sau, hai giá trị này được prefill vào ô số điện thoại người…"

**Analyst Note (diff):** ⭐ **Hai CL đóng cùng lúc bằng một dòng field spec.**
**`C-ORD-10`** hỏi *"không pre-fill — bug hay tài khoản test chưa cấu hình?"*. PRD trả lời: prefill là **hành vi đặc tả**, và `FR15`/`AC-30.1.01` đặc tả luôn **nơi người dùng đặt giá trị mặc định**. ⇒ Nếu hồ sơ **đã có** địa chỉ mặc định mà wizard trống thì là **BUG**; nếu hồ sơ **chưa có** thì trống là đúng. ⇒ Given của `SC-ORD-025` **bắt buộc** nêu rõ *"tài khoản ĐÃ đặt địa chỉ mặc định (xác nhận trước khi chạy)"* — đúng sự mơ hồ này đã làm CL treo 2 tháng, ⛔ đừng lặp lại bằng cách chạy trên tài khoản không rõ trạng thái.
**`C-ORD-11`** hỏi *"preset 6 văn phòng / chip gợi ý / autocomplete?"*. Field spec ghi kiểu ô là **"Văn bản"** với trần **200 ký tự** ⇒ **ô văn bản tự do**, không preset, không chip. ⇒ `SC-ORD-026` assert kiểu ô + biên 200/201.

---

##### SC-ORD-036 / SC-ORD-050 — Màn thành công không có mã đơn · Thoát wizard không lưu DRAFT
📍 `DOC-v1.1-01 §6.2 AC-07.1.01 · trang 18` · `AC-01.2.01 · trang 17` · `§8.1.3 bước 8 · trang 35`

> `AC-07.1.01`: "Chuyển sang màn "Đăng tin thành công" — không hiển thị mã đơn. Có nút về trang chủ và nút xem đơn vừa đăng. Tin xuất hiện ngay ở "Tin mới" trên trang chủ và ở "Đơn của tôi"."

> `AC-01.2.01`: "Hiện popup xác nhận "Thoát và bỏ nội dung đã nhập?". Chọn thoát → không tạo tin (trạng thái DRAFT không được lưu). Chọn ở lại → dữ liệu đã nhập giữ nguyên."

**Analyst Note (diff):** **Hai CL kế thừa từ 2026-07 đóng cùng lượt.**
`C-ORD-05` (*"có Mã tin hay không"*) treo vì **2 biến thể mockup** mâu thuẫn. PRD nói **KHÔNG** ở **2 chỗ độc lập** (`AC-07.1.01` + `§8.1.3` bước 8), cùng dùng đúng cụm *"không hiển thị mã đơn"* ⇒ không phải suy diễn từ việc mockup thiếu. `SC-ORD-036` chuyển sang **assert-absent khẳng định**, cộng 2 nút và 2 nơi tin phải xuất hiện ngay.
`C-ORD-08` (*"thoát/reset có xoá form?"*) được trả lời **rộng hơn câu hỏi**: có popup **chuỗi verbatim**, và câu *"trạng thái DRAFT không được lưu"* là **khẳng định kiến trúc** — app **không có** cơ chế nháp. ⇒ `SC-ORD-050` assert đủ 3 nhánh (ở lại / thoát / mở lại thấy form trắng) trong 1 SC vì cùng một luồng thao tác.

---

##### SC-ORD-063 / SC-ORD-065 — Validation liên-trường và ranh giới bất biến của ảnh
📍 `DOC-v1.1-01 §8.1.4 dòng "Địa chỉ giao hàng" · trang 35` · `§8.18.1 BR18-05 / BR18-02 · trang 52`

> "Địa chỉ giao hàng | … | Không để trống; phải khác địa chỉ lấy hàng"

> `BR18-05`: "Ảnh đã gắn vào một mốc nhật ký thì không xoá được (phục vụ truy vết)."

> `BR18-02`: "…xoá được từng ảnh **trước khi ghi mốc**…"

**Analyst Note:** `SC-ORD-063` là **validation liên-trường đầu tiên của wizard** (v1.0 không có), cùng họ với `BR02-03` của `FR02`. ⚠️ PRD **không định nghĩa** phép so sánh *"khác"* — `VAL-03` chỉ nói trim, không nói hoa/thường hay dấu. ⇒ SC lấy **biên gần nhất** (chỉ khác khoảng trắng đầu/cuối) làm ô kiểm và **ghi nhận** hành vi hoa/thường, ⛔ không assert cứng một hành vi PRD chưa định nghĩa — assert bừa ở đây sẽ tạo bug report sai và làm mất uy tín cả bộ TC.
`SC-ORD-065`: điểm mấu chốt là **ranh giới nằm ở thời điểm ghi mốc**, không phải ở bản thân tấm ảnh — `BR18-02` cho xoá **trước**, `BR18-05` cấm xoá **sau**. ⇒ 1 SC kiểm **cả hai phía** trong 1 lượt; tách ra thì mất chính khái niệm ranh giới. ⚠️ Cùng họ rule audit với `BR11-03` (`SC-CNL-010`) và `NFR-07` (`SC-DLV-062`) — **nếu 2 cái kia FAIL thì cái này nhiều khả năng cũng FAIL**; chạy cùng lô, gộp bug report.

---

> Các SC MODIFIED còn lại (`SC-ORD-028` · `029` · `041` · `043` · `044` · `045` · `052`/`053` nhóm dropdown) là **siết Then theo giá trị/enum cụ thể** mà PRD bổ sung, không đảo hành vi — quote gắn trực tiếp ở cột `DOC Source` của bảng trên; diff tóm tắt ở `CHANGELOG.md §1`.

---

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| SC-ORD-001..004 | Wizard 3 bước — cấu trúc, điều hướng, thông tin hàng | ORD | v1.0 | P2-P3 | → `v1.0/ORD-dang-tin/test_scenario_map.md` |
| SC-ORD-006..007 | Loại hàng — chọn 1 giá trị, đổi lựa chọn | ORD | v1.0 | P2-P3 | → như trên |
| SC-ORD-008..011 | Giá trị hàng (3 mức + cảnh báo) · Ghi chú ≤ 300 ký tự | ORD | v1.0 | P2-P3 | → như trên — `BR01-03` xác nhận lại *"không chặn đăng tin"* |
| SC-ORD-013 | Hiển thị ảnh đã tải | ORD | v1.0 | P3 | → như trên — bổ sung carousel/lightbox ở `SC-ORD-057` |
| SC-ORD-014..017 | Nhóm người gửi — tên chỉ đọc, SĐT, prefill | ORD | v1.0 | P2-P3 | → như trên — ⚠️ `SC-ORD-014` khi generate TC nhớ vế `BR01-08` *"chỉ lộ sau khi ghép"* |
| SC-ORD-018..021 | Email người nhận — định dạng, autofill (bản v1.0) | ORD | v1.0 | P1-P3 | → như trên — 3 nhánh danh bạ mới ở `SC-ORD-058..060` |
| SC-ORD-022..024 | Nhóm người nhận — tên, SĐT, địa chỉ giao | ORD | v1.0 | P2-P3 | → như trên |
| SC-ORD-027 | Địa chỉ lấy hàng — nhập tay hợp lệ | ORD | v1.0 | P2 | → như trên |
| SC-ORD-030 | Buổi mong muốn — chọn nhiều | ORD | v1.0 | P2 | → như trên |
| SC-ORD-031..035 | Consent điều khoản · hàng cấm (banner) | ORD | v1.0 | P1-P3 | → như trên — ⚠️ `C-ORD-04` **MỞ LẠI**, xem `risk_assessment.md` |
| SC-ORD-037..038 | Màn thành công — điều hướng | ORD | v1.0 | P2-P3 | → như trên |
| SC-ORD-039..040, SC-ORD-042 | Form OFFER — 1 trang, validate tuyến | ORD | v1.0 | P1-P3 | → như trên — `BR02-03` xác nhận lại |
| SC-ORD-046..049 | Quản lý tin · `VAL-01/02/03` chung của form | ORD | v1.0 | P1-P3 | → như trên — `§8.18.2` xác nhận lại nguyên văn |
| SC-ORD-051 | Ngưỡng giá trị hàng bằng số tiền | ORD | v1.0 | P3 | → như trên — `C-ORD-02` vẫn Resolved *out of scope*; PRD không nhắc |

> ℹ️ **39 SC CARRIED**, gom theo cụm để bảng đọc được. Dải ID đầy đủ và priority per-SC: `v1.0/ORD-dang-tin/test_scenario_map.md` (nguồn canonical của bản v1.0).
> ⛔ 12 SC MODIFIED (`005` `012` `025` `026` `028` `029` `036` `041` `043` `044` `045` `050`) **không** nằm trong bảng này — xem §NEW & MODIFIED.

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
