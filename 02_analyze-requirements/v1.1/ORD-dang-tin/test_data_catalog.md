# Test Data Catalog — v1.1 · Module ORD

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> Chỉ liệt kê data **mới/đổi** của lượt delta. Data v1.0 xem `v1.0/ORD-dang-tin/test_data_catalog.md`.

| Data | Loại data | Valid | Invalid | Boundary | Nguồn |
|------|-----------|-------|---------|----------|-------|
| Ảnh món hàng | Fixture | 1–5 ảnh JPG/PNG, mỗi ảnh ≤ 5MB | 0 ảnh (**chặn sang bước 2**) · ảnh > 5MB · file `.gif`/`.pdf`/`.heic` | ⭐ **0** (chặn) · **1** (tối thiểu hợp lệ) · **5** (đủ trần, ẩn nút thêm) · **6** (vượt trần) · **đúng 5MB** · **5MB + 1 byte** | `DOC-v1.1-01` §8.1.1 BR01-01 · §8.18.1 BR18-02 · §8.18.2 VAL-07 |
| Khối lượng | Master | `< 5 kg` · `5–10 kg` · `> 10 kg` | "chưa chọn" (**không cho để trống**) | `> 10 kg` phải **vẫn đăng được** — `BR01-02` *"không chặn theo ngưỡng"* | `DOC-v1.1-01` §8.1.1 BR01-02 · §8.1.4 |
| Kích thước | Master | `Nhỏ · cầm tay` · `Vừa · khoảng 20×20 cm` · `Lớn · > 20×20 cm` | "chưa chọn" | `Lớn · > 20×20 cm` phải **vẫn đăng được** | `DOC-v1.1-01` §8.1.1 BR01-02 · §8.1.4 |
| Loại hàng | Master | 8 giá trị theo PRD: `Tài liệu · Đồ điện tử · Thực phẩm · Hàng nhỏ · Đồ dễ vỡ · Quần áo · Thuốc/Y tế · Khác`; **mặc định = Tài liệu** | — | 🔴 **Nhãn đầu lệch app** ("Giấy tờ, hồ sơ") ⇒ ⛔ **KHÔNG dùng nhãn "Tài liệu" trong TC** cho tới khi `C-ORD-09` chốt. 🔴 `Thuốc/Y tế` — `C-ORD-04` **mở lại**, PRD tự mâu thuẫn | `DOC-v1.1-01` §8.1.4 · §8.1.1 BR01-07 |
| Email công ty người nhận | **Fixture — cần QTHT cấp** | ① email **CÓ** trong danh bạ nội bộ · ② email **đúng tên miền nội bộ nhưng KHÔNG có** trong danh bạ | email sai định dạng · email **ngoài tên miền nội bộ** | 🔴 **Không tự chế được ① và ②** — cần STG nối danh bạ thật (`C-ORD-13`). Thiếu ⇒ `SC-ORD-058..060` **BLOCKED**, ⛔ không PASS | `DOC-v1.1-01` §8.1.1 BR01-09 · §8.1.4 · §4 SCOPES |
| Tên người được uỷ quyền | Fixture | 2–60 ký tự | 1 ký tự · 61 ký tự | ⭐ **2** và **60** đều hợp lệ; **1** và **61** bị chặn | `DOC-v1.1-01` §8.1.1 BR01-06 · §8.1.4 |
| SĐT người được uỷ quyền | Fixture | Định dạng VN (10 số, đầu 0) — **chỉ validate khi được nhập** | `123` · `84901234567` · chữ | ⛔ **Bỏ trống KHÔNG phải invalid** (khối là không bắt buộc) — đừng viết TC "bỏ trống thì lỗi" | `DOC-v1.1-01` §8.1.1 BR01-06 |
| Quan hệ / ghi chú uỷ quyền | Fixture | ≤ 60 ký tự (vd `"Đồng nghiệp cùng phòng"`) | 61 ký tự | 60 / 61 | `DOC-v1.1-01` §8.1.4 |
| Địa chỉ lấy hàng | Runtime | Prefill từ **địa chỉ mặc định của hồ sơ** — ô văn bản tự do, sửa được | Để trống | ⭐ **200** ký tự (hợp lệ) · **201** (chặn/cắt). ⚠ Tài khoản phải **ĐÃ đặt địa chỉ mặc định** — xác nhận trước khi chạy `SC-ORD-025` | `DOC-v1.1-01` §8.1.4 · §6.2 AC-30.1.01 |
| Địa chỉ giao hàng | Runtime | Khác địa chỉ lấy hàng | **Trùng hệt** địa chỉ lấy hàng | ⭐ Biên gần nhất: chỉ khác **khoảng trắng đầu/cuối** → GHI NHẬN, ⛔ không assert cứng (PRD không định nghĩa phép so sánh) | `DOC-v1.1-01` §8.1.4 |
| Khoảng ngày (Từ–Đến) | Fixture | Không quá khứ; `Đến ≥ Từ`; ≤ 7 ngày | Ngày quá khứ · `Đến < Từ` | ⭐ **đúng 7 ngày** (hợp lệ) · **8 ngày** (chặn) · Từ = Đến (1 ngày) | `DOC-v1.1-01` §8.1.1 BR01-04 · §8.1.4 |
| Buổi mong muốn | Master | `Sáng (8–12)` · `Chiều (13–17)` · `Sau giờ làm (17–19)` · `Giờ nào cũng được`; **mặc định = Sau giờ làm** | Bỏ trống hết (≥ 1 buổi) | ⭐ Chọn `Giờ nào cũng được` khi đang có 2 buổi khác → 2 buổi kia **tự bỏ chọn** | `DOC-v1.1-01` §8.1.1 BR01-04 · §8.1.4 · §6.2 AC-06.2.01 |
| Ghi chú | Fixture | ≤ 300 ký tự | 301 ký tự | 300 / 301 | `DOC-v1.1-01` §8.1.4 |
| Tin đã đăng có ≥ 2 ảnh | Runtime | 1 tin của chính mình, `POSTED`, có 2–5 ảnh | Tin 1 ảnh (không kiểm được carousel) | Dùng cho `SC-ORD-057` (carousel/lightbox) và `SC-ORD-065` (ảnh đã ghi mốc) | `DOC-v1.1-01` §8.18.1 BR18-03 · BR18-05 |
| Tin OFFER của tài khoản khác | Runtime | Tài khoản A đăng 1 tin OFFER; tài khoản B (vai người gửi) đi tìm | — | ⚠ Vế *"mở link trực tiếp"* của `AC-20.1.02` **không thực hiện được trên mobile app** (không có URL) ⇒ GHI NHẬN giới hạn, ⛔ không PASS chỉ vì không có đường thử | `DOC-v1.1-01` §8.2.1 BR02-01 · §6.2 AC-20.1.02 |

## Ghi chú
- 🔴 **Hai loại data KHÔNG tự tạo được, phải xin trước `generate-tc`:** (1) **2 email mẫu danh bạ** (`C-ORD-13`) — thiếu thì 3 SC `BLOCKED` trong đó có 1 P1; (2) **tài khoản đã đặt địa chỉ mặc định** cho `SC-ORD-025`.
- ⚠️ **Nhãn "Tài liệu" là bẫy lặp lại của đợt cũ** — `03_test-cases/v1.0/CHANGELOG.md §2` ràng buộc 4 vẫn hiệu lực. Khi viết Test Data cho TC, ghi nhãn **theo app STG**, ⛔ không copy từ PRD.
- ⚠️ **`Thuốc/Y tế` đang ở vùng tranh chấp** (`C-ORD-04` mở lại) — ⛔ không đưa giá trị này vào Test Data của TC assert chiều nào cho tới khi BA chốt.
- **Ảnh mẫu cần chuẩn bị sẵn 1 bộ dùng chung:** 1 JPG nhỏ · 1 PNG nhỏ · 1 ảnh **đúng 5MB** · 1 ảnh **> 5MB** · 1 file sai định dạng. Bộ này dùng lại cho `DLV` (ảnh giao hàng) và `TS` (ảnh báo sự cố) — `BR18-01` áp cùng trần cho mọi điểm bằng chứng, ⛔ đừng chuẩn bị 3 bộ.
- **Khung giờ chọn TƯƠNG ĐỐI so với hiện tại** (`Project_rule`, `KP-01 §10.11`) — ⛔ không hardcode ngày/giờ trong TC.
