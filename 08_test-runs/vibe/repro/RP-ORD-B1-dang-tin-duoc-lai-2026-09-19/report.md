# Repro Report — RP-ORD-B1-dang-tin-duoc-lai — 2026-09-19

> **Hợp đồng NHẸ** (`repro/`): report + ≤3 ảnh, ⛔ KHÔNG per-TC evidence.
> Mục tiêu: **repro lại bug `B1` của VR-004** (*"không đăng được tin NEED, API 400 `REQ_400`"*).
> Platform: mobile (Appium MCP) · `emulator-5554` · app `com.hrisproject.stag`
> Tài khoản: **`Đặng Châu Anh`** (MNV `00286248`) · ⚠️ VR-004 chạy bằng **`Đặng Châu Giang`**

## 🔴 KẾT LUẬN: `B1` KHÔNG TÁI HIỆN — cả OFFER lẫn NEED đều đăng được

| # | Phép thử | Thời điểm | Kết quả |
|---|---|---|---|
| 1 | Đăng **OFFER** — *"Tôi nhận giao hàng"* | 08:26–08:30 | ✅ **"Đã ghi nhận tuyến đường!"** · logcat sạch |
| 2 | Đăng **NEED** — *"Tôi cần gửi hàng"*, đủ 3 bước wizard | 08:33–08:38 | ✅ **"Đăng tin thành công!"** · ⛔ **không có `REQ_400`** |

**Ảnh:** `_recon__offer-dang-thanh-cong.png` · `_recon__need-dang-thanh-cong.png`

**Cách thử NEED (đúng luật v1.1, không đi tắt):** chip `Tài liệu` + `Thấp` + `Dưới 5 kg` + `Nhỏ` + **1 ảnh** từ thư viện ⇒ `Tiếp theo` `enabled=false→true`; bước 2 điền địa chỉ lấy/giao **có chạm `address-suggestion-0`** (bẫy T11), email người nhận `stag_thuyntt22@fpt.com` (autofill `Nguyễn Thị Thanh Thủy`), SĐT, buổi `Sáng`; bước 3 tick điều khoản → `Đăng tin ngay`. `adb logcat -c` ngay trước khi bấm để bắt lỗi sạch — **không có dòng lỗi nào**.

## ⚠️ Chưa đủ để ĐÓNG `B1` — đọc kỹ

⛔ **KHÔNG kết luận "B1 đã được fix".** Mới chứng minh được *"không tái hiện trên tài khoản `Đặng Châu Anh`, ngày 2026-09-19"*. Hai khả năng còn để ngỏ:

| Khả năng | Cách phân định |
|---|---|
| (a) Dev đã fix API | hỏi Dev / kiểm changelog deploy STG |
| (b) `B1` phụ thuộc **dữ liệu tài khoản**, không phải lỗi chung | retest bằng đúng tài khoản `Đặng Châu Giang` + đúng email người nhận VR-004 dùng (`stag_anhdc4@fpt.com`) |

🔍 **Dữ kiện nghiêng về (b):** VR-004 ghi hồ sơ `Đặng Châu Giang` **mất địa chỉ mặc định** (hệ quả `TC-USR-040`), nên ô *Địa chỉ lấy hàng* rỗng. Tài khoản `Đặng Châu Anh` cũng rỗng ô đó mà **vẫn đăng được** ⇒ địa chỉ rỗng **không phải** nguyên nhân. Biến còn khác nhau rõ nhất là **email người nhận** — VR-004 dùng `stag_anhdc4@fpt.com` (chính là tài khoản Anh), tức **tự gửi cho chính mình**; phép thử này gửi cho người khác. **Đây là giả thuyết đáng test trước tiên.**

## 🐞 2 phát hiện phụ (mới, chưa có TC phủ)

| # | Phát hiện | Chi tiết |
|---|---|---|
| 1 | **Autofill SĐT người nhận trả về MNV** | điền email `stag_thuyntt22@fpt.com` → ô SĐT tự điền **`0000002352`** (= MNV `00002352` thêm `0`), app lập tức báo đỏ *"Số điện thoại không hợp lệ"*. Người dùng buộc phải tự sửa. Cùng họ `BUG-008` (không load SĐT từ HRIS) |
| 2 | **Nhãn buổi lệch tài liệu** | app hiện **`Sáng (8–12h)`**; `TC-ASN-v1.1.md §0` ghi QA-obs *"Sáng (6–12h)"* ⇒ **sửa fragment** (chính fragment dặn *"verify lại khi vibe-test"*). 3 nhãn còn lại khớp: `Chiều (13–17h)` · `Sau giờ làm (17–19h)` · `Giờ nào cũng được` |

## ✅ Đăng xuất — CÓ, nhưng ở FoxPro chứ không phải FoxEco

- FoxEco → **Cá nhân**: chỉ 3 mục (`Đơn của tôi` · `Quà đã nhận` · `Cập nhật thông tin cá nhân`) — **không có Đăng xuất**
- **FoxPro host → Cá nhân** (cuộn cuối): **có `Đăng xuất`** — ảnh `_recon__foxpro-co-nut-dang-xuat.png`

⛔ **CỐ TÌNH KHÔNG BẤM.** Đăng xuất là thao tác **khó đảo ngược trên môi trường dùng chung**: nếu đăng nhập lại cần **OTP** mà không có người nhập, môi trường test của QC **mất luôn**. Cần QC xác nhận có sẵn tài khoản + người nhập OTP rồi mới thao tác.

## 🗂️ Dữ liệu đã tạo trên STG (phải biết để khỏi nhiễu phiên sau)

| Loại | Nội dung | Dùng được làm |
|---|---|---|
| **OFFER** | `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` · Hôm nay · buổi **Sáng** | **`SEED-ASN-01`** |
| **NEED** | `Tài liệu · Giá trị thấp · Nhẹ · Nhỏ` + 1 ảnh · cùng tuyến · buổi **Sáng** · người nhận `Nguyễn Thị Thanh Thủy` | tiền đề nhóm `TC-ASN-011/012/022/023/025` |

📌 Hai tin **cùng tuyến + cùng ngày + cùng buổi** ⇒ theo `BR04-01/02` **phải sinh thông báo khớp tuyến**. Chưa kiểm — là việc đầu tiên của phiên ASN tiếp theo (`TC-ASN-023`, mốc ≤60s).

## Việc cần làm

1. **⛔ Chưa đóng `B1`** — retest bằng tài khoản `Đặng Châu Giang` + email `stag_anhdc4@fpt.com` (giả thuyết *tự gửi cho chính mình*).
2. **Cập nhật mọi nơi đang khai "không đăng được tin"** — đã sửa `coverage-ASN.md`, `INDEX.md`, `MASTER-MEMORY §8b`.
3. **Sửa fragment** nhãn buổi `Sáng (6–12h)` → `Sáng (8–12h)`.
4. **Xác nhận tài khoản phụ + OTP** trước khi bấm Đăng xuất.
