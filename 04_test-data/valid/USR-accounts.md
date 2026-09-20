# USR-accounts — Tài khoản test STG (bản KHÔNG chứa secret)

> 🔐 **File này CỐ TÌNH không chứa OTP/mật khẩu.** Secret nằm ở **`~/.foxeco-v2/credentials.env`** (`chmod 600`, ngoài repo, đã `.gitignore`).
> Nguồn gốc: QC GiangDC2 cung cấp **2026-09-19** qua `04_test-data/account.txt` *(đã gitignore — ⛔ không commit)*.
> Cập nhật lần cuối: **2026-09-19** · Dùng chung cho **USR · HOME · ORD · ASN · DLV · GIFT · ACT · CNL**.

## §0. Đăng nhập — đọc trước khi đổi tài khoản

| Điểm | Nội dung |
|---|---|
| **Cơ chế** | SSO qua **host app FoxPro** (`FoxPro_Stag`). FoxEco là SDK nhúng ⇒ ⛔ **không có màn đăng nhập riêng trong FoxEco** |
| **Đăng xuất ở đâu** | **FoxPro → tab `Cá nhân` → cuộn xuống cuối → `Đăng xuất`**. ⛔ KHÔNG có trong FoxEco (`Cá nhân` của FoxEco chỉ có 3 mục: Đơn của tôi · Quà đã nhận · Cập nhật thông tin) |
| **Vào lại FoxEco** | FoxPro → tab `Chức năng` → cuộn → icon **`FoxEco`** *(cần `scroll_to_element`, không nằm màn đầu)* |
| **OTP** | 🔑 **CỐ ĐỊNH trên staging, dùng chung cho MỌI account, không đổi theo thời gian** ⇒ AI **tự đăng nhập được**, ⛔ không cần người nhập tay. Giá trị ở `credentials.env` biến `FOXECO_STG_OTP` |
| **Mật khẩu** | ✅ **KHÔNG CẦN** — xác minh 2026-09-19: màn login FoxPro chỉ có **1 ô email** + nút `NHẬN MÃ OTP` → màn `Xác nhận OTP` → `ĐĂNG NHẬP`. ⛔ Không có trường mật khẩu. `FOXECO_STG_PASS` để trống là đúng |

> ✅ **ĐÃ KIỂM CHỨNG THẬT 2026-09-19 09:07–09:11** — AI tự `Đăng xuất` → nhập email → `NHẬN MÃ OTP` → nhập OTP cố định → `ĐĂNG NHẬP` **thành công**, không cần người can thiệp. Luồng đầy đủ ghi ở `§0b`.
>
> 🔴 **ĐÍNH CHÍNH 2026-09-19 — mọi ghi chép cũ nói *"OTP nhập tay, AI không lấy được"* (VR-001 `§0`, VR-003, VR-004 ledger) đều ĐÃ LỖI THỜI.** Chúng viết khi chưa biết OTP staging là cố định. ⇒ Các TC từng bị đánh `NOT_RUN` **chỉ vì lý do OTP** nay **chạy được**.

## §0b. Luồng đổi tài khoản — đã chạy thật, dùng lại được

```
1. FoxPro → tab `Cá nhân` → scroll_to_element `text("Đăng xuất")` → tap
2. Popup "Bạn muốn đăng xuất?" → tap `text("Đồng ý")`
3. Màn login FoxPro (tab `Cán bộ nhân viên` active sẵn):
     set_value  text("Nhập email đăng nhập")  = <email>
     tap        text("NHẬN MÃ OTP")
4. Màn `Xác nhận OTP`:
     adb shell input text "$FOXECO_STG_OTP"     ← ô OTP đã tự focus
     tap        text("ĐĂNG NHẬP")
5. FoxPro Trang chủ → tap `text("Chức năng")`
     → scroll_to_element `text("FoxEco")` (preset small, ~4 nhịp) → tap
```

⏱️ Tốn ~14 MCP call + ~90 giây/lượt ⇒ **gom việc theo tài khoản** (xem `§2`).
⚠️ Ô OTP **tự focus** khi vào màn ⇒ `adb shell input text` là đủ, ⛔ không cần find element.
⚠️ Icon `FoxEco` ở `Chức năng` nằm **cuối danh sách** ⇒ bắt buộc `scroll_to_element`.

## §1. Danh sách tài khoản

| # | Biến env | Email | MNV | Tên hiển thị | Độ chắc chắn | Ghi chú |
|---|---|---|---|---|---|---|
| 1 | `FOXECO_STG_USER_1` | `stag_giangdc2@fpt.com` | `00131946` *(?)* | **Đặng Châu Giang** | ✅ **XÁC NHẬN** *(login VR-009, 2026-09-19 15:01)* | Màn chào FoxPro + `Cá nhân` đều hiện **Đặng Châu Giang**; form OFFER autofill SĐT **`0964633310`** ⇒ khớp ghi chép cũ. Ban Giám đốc · ⚠️ **mất địa chỉ mặc định** (VR-003) · địa điểm checkin `HCM LôB3,E-Office,KCN TânThuận` · ⏳ MNV vẫn **chưa** đối chiếu trực tiếp |
| 2 | `FOXECO_STG_USER_2` | `stag_anhdc4@fpt.com` | `00286248` | **Đặng Châu Anh** | ✅ **xác nhận** | App autofill email này ra đúng tên + SĐT `0343439724` (VR-004) và trùng tài khoản đăng nhập 2026-09-19. Phòng Kinh doanh 2 (PNC) · hero 3 đơn · 2 quà |
| 3 | `FOXECO_STG_USER_3` | `stag_anhptm17@fpt.com` | **`00287493`** | **Phan Thị Mỹ Anh** | ✅ **XÁC NHẬN** *(login lần đầu VR-011, 2026-09-19 20:55)* | **Phòng Văn hoá đoàn thể phía Nam** · ✅ vào được FoxEco · 🔴🔴 **KHÔNG CÒN SẠCH: 5 đơn đã giúp / 5 quà đã nhận** (`Ly cà phê` ×3 + `Vương miện` ×2) ⇒ ⛔ **không dùng được cho TC cần tài khoản trắng** (`TC-USR-040/043`, `TC-HOME-027/028/029`, `TC-ACT-012/014/016/017/018`, `TC-GIFT-008`). ⭐ Ngược lại **rất hợp** cho TC cần *5 quà / 2 loại / 3+2* (`TC-GIFT-006`) |
| 4 | `FOXECO_STG_USER_4` = 🔑 **`FOXECO_STG_USER_C`** | `stag_taipm@fpt.com` | **`00041796`** | **Phan Minh Tài** | ✅ **XÁC NHẬN** *(login 2026-09-19 09:09)* | **Phòng Phát triển Phần mềm số 8** · **SĐT `0833329408`** · hero **2 đơn đã giúp** · **1 quà đã nhận** |
| 5 | `FOXECO_STG_USER_5` | `stag_huyennhk@fpt.com` | ? | **Nguyễn Huỳnh Kim Huyền** | ✅ **XÁC NHẬN** *(login lần đầu VR-010, 2026-09-19 17:49)* | **SĐT `0989014863`** · thâm niên 2819 ngày · email hiển thị `stag_HuyenNHK@fpt.com` · ⭐ autofill người nhận **ĐÚNG** (9/9 lần ở VR-010, 4/4 ở VR-009) ⇒ **tài khoản người nhận NÊN DÙNG**. 🔴🔴 **KHÔNG truy cập được FoxEco** — `Chức năng` chỉ có 9 app, ⛔ **không có icon FoxEco**; màn `Cá nhân` cũng **không render** mục `Đăng xuất` (phải `adb shell pm clear com.hrisproject.stag` để thoát). ⇒ **CHỈ đóng vai người nhận**, ⛔ không làm actor được (`T-ASN-12`) |

### §1b. Tài khoản/danh tính biết từ phiên trước — ⚠️ KHÔNG nằm trong danh sách 5 acc trên

| Email / danh tính | MNV | Dùng làm gì | Trạng thái |
|---|---|---|---|
| `stag_thuyntt22@fpt.com` — Nguyễn Thị Thanh Thủy | `00002352` | từng là tài khoản "trắng" | ⚠️ **đã bẩn** — VR-003 lưu SĐT `0987654322`; 2026-09-19 dùng làm người nhận 1 tin NEED |
| `stag_binhnt23@fpt.com` | `00026682` | **email người đã nghỉ việc** → `TC-ORD-076` | ⛔ không đăng nhập được (đã nghỉ) |
| *(email chưa biết)* — **Phan Thị Mỹ Anh** | ? | SĐT `0947153040` · carrier của đơn `Đã ghép` | 🆕 phát hiện 2026-09-19 |
| ✅ `FOXECO_STG_USER_C` = **`stag_taipm@fpt.com`** | `00041796` | vai C — HRIS có SĐT + địa chỉ `HCM LôB3,E-Office,KCN TânThuận` | ✅ **ĐÃ MAP 2026-09-19** → xem `§1` dòng 4. ⚠️ Điều kiện *"chưa từng lưu hồ sơ"* **CHƯA kiểm lại** — ⛔ đừng bấm Lưu ở `Cập nhật thông tin` trước khi chạy `TC-USR-040/043` |
| `FOXECO_STG_USER_BLANK1` | `00157112` | tài khoản trắng, 2 chỉ số = 0 | ❓ email chưa biết |

**Email KHÔNG tồn tại** (test nhánh âm): `stag_khongtontai@fpt.com` · `stag_khongtontai9999@fpt.com`

## §2. Chiến lược luân phiên tài khoản (⭐ đọc trước khi lập kế hoạch phiên)

> **Nguyên tắc: gom theo TÀI KHOẢN, không theo TC.** Mỗi lần đổi account tốn 1 vòng logout→login→vào lại FoxEco (~8–10 MCP call). Chạy rải rác theo TC sẽ đổi hàng chục lần vô ích.

```
Bước 1 — Gom mọi việc cần làm trên account X (cả SEED DATA lẫn chạy TC)
Bước 2 — login X → làm HẾT → ghi log
Bước 3 — đổi sang Y, lặp lại
Bước 4 — quay về account quan sát để chấm verdict cuối
```

**Phân vai khuyến nghị** (giữ ổn định giữa các phiên để dữ liệu không rối):

| Vai | Account | Việc |
|---|---|---|
| **A — quan sát / chủ tin** | `stag_giangdc2@fpt.com` | đăng tin NEED, quan sát Trang chủ/Hoạt động, chấm verdict |
| **B — carrier** | `stag_anhdc4@fpt.com` | nhận đơn (*"Tôi mang giúp được"*), đăng OFFER |
| **C — người nhận** | `stag_taipm@fpt.com` ✅ *Phan Minh Tài*, MNV `00041796` | xác nhận đã nhận hàng. 🔴 **Đây cũng là `FOXECO_STG_USER_C` của `TC-USR-040/043`** ⇒ chạy 2 TC đó **TRƯỚC** khi dùng account này vào việc khác |
| **D — người ngoài cặp** | ~~`stag_huyennhk@fpt.com`~~ → **`stag_giangdc2@fpt.com`** | 🔴 **ĐỔI VAI 2026-09-19 (VR-010):** `stag_huyennhk@` **không có FoxEco** nên ⛔ không đóng vai actor được; `TC-ASN-005` thực tế đã chạy bằng `stag_giangdc2@` ở VR-009. `stag_huyennhk@` nay **chỉ là người nhận** trong form |
| ~~**dự phòng / tài khoản sạch**~~ | ~~`stag_anhptm17@fpt.com`~~ | 🔴🔴 **HUỶ VAI 2026-09-19 (VR-011):** tài khoản này **KHÔNG hề sạch** — đo được **5 đơn đã giúp / 5 quà đã nhận**. Ghi chép cũ (*"giữ chưa lưu hồ sơ càng lâu càng tốt"*) là **sai**. ⇒ **STG hiện KHÔNG CÒN tài khoản trắng nào**, phải **xin dev/QA cấp 1 account mới tinh** dùng chung cho cụm empty state của **GIFT + ACT + HOME** |

> ⚠️ **Luật giữ tài khoản sạch:** TC cần *"chưa từng lưu hồ sơ"* / *"0 đơn 0 đóng góp"* phải chạy **TRƯỚC** khi dùng account đó vào bất cứ đơn nào. Dùng sai thứ tự là mất vĩnh viễn (đã xảy ra với `00002352` ở VR-003).

## §3. Dữ liệu đã tạo trên STG (cập nhật mỗi phiên)

| Ngày | Account | Loại | Nội dung |
|---|---|---|---|
| 2026-09-19 | `Đặng Châu Anh` | **OFFER** | `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` · Hôm nay · buổi **Sáng** ⇒ dùng làm **`SEED-ASN-01`** |
| 2026-09-19 | `Đặng Châu Anh` | **NEED** | `Tài liệu · Thấp · Nhẹ · Nhỏ` + 1 ảnh · cùng tuyến trên · buổi **Sáng** · người nhận `Nguyễn Thị Thanh Thủy` |

| 2026-09-19 | Phan Minh Tài | **OFFER** | `FPT Tân Thuận 1` → `FTEL SG08 Quận 12` · Hôm nay · **Chiều** *(VR-007, TC-ASN-013)* |
| 2026-09-19 | Phan Minh Tài | **NEED** | `FPT Tân Thuận 1` → `FTEL SG08 Quận 12` · Hôm nay · **Chiều** *(VR-007, TC-ASN-013)* |
| 2026-09-19 | Phan Minh Tài | **NEED** | `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` · Hôm nay · **Sáng** *(VR-007, TC-ASN-021/023)* |
| 2026-09-19 | *(hệ thống)* | — | Số đơn cộng đồng **317 → 318** giữa 08:26 và 09:10 ⇒ có đơn Hoàn thành mới phát sinh trên STG (⛔ không do phiên này tạo) |

📌 2 tin trên **cùng tuyến + cùng ngày + cùng buổi** ⇒ theo `BR04-01/02` phải sinh **thông báo khớp tuyến** (`TC-ASN-023`, mốc ≤60s) — chưa kiểm.

## §4. Ảnh seed có sẵn trên máy ảo

`/sdcard/Pictures/` — `seed-ord-01..05.jpg` · `seed-ord-06.png` · `seed-ord-oversize-5mb.jpg` *(ảnh quá khổ để test chặn 5MB)*

## §5. Gap còn lại

1. ~~Mật khẩu chưa có~~ → ✅ **GỠ 2026-09-19**: login **chỉ cần email + OTP**, không có trường mật khẩu.
2. ~~**1/5 account chưa biết gì** — `stag_anhptm17@`~~ → ✅ **ĐÃ MAP 2026-09-19 (VR-011)**: **Phan Thị Mỹ Anh**, MNV `00287493`, Phòng Văn hoá đoàn thể phía Nam. ⇒ **5/5 account đã biết danh tính**; chỉ còn `stag_huyennhk@` thiếu MNV.
3. **Còn `FOXECO_STG_USER_BLANK1` (`00157112`) chưa map** vào email nào. 🔴 **Loại được 1 ứng viên:** `stag_anhptm17@` = MNV `00287493` ⇒ **KHÔNG phải** `BLANK1`. Ứng viên còn lại: `stag_huyennhk@` *(chưa biết MNV)*.
4. **Không có tài khoản HRIS trống** ⇒ `TC-USR-041/044` vẫn `BLOCKED` (`DOC-v1.1-05`).
5. 🆕 **`BUG-008` (autofill SĐT người nhận) KHÔNG phải lỗi toàn cục** — VR-009 đo được: `stag_huyennhk@` autofill **ĐÚNG** `0989014863` (4/4 lần), trong khi VR-008 ghi `stag_thuyntt22@` trả về **MNV** `0000002352`. ⇒ Phụ thuộc **HRIS có SĐT của người đó hay không**. **Khi seed, ưu tiên `stag_huyennhk@`.**
6. 🆕 **Bẫy `T-ASN-07` khi đổi tài khoản:** nút `NHẬN MÃ OTP` có thể trả dialog *"Không thể kết nối mạng! Vui lòng kiểm tra lại."* **ngay cả khi mạng OK** (`adb shell ping 8.8.8.8` 0% loss). ⇒ **Bấm lại lần 2** trước khi kết luận hỏng; dialog là **in-app** nên đóng được bằng `find text("Đồng ý") + tap`.
| 2026-09-19 | `Phan Minh Tài` | **NEED ×4 (SEED VR-008)** | `SEED S1` V-City→FPT Cầu Giấy · Hôm nay · **Sáng** *(khớp đủ)* · `SEED S2` V-City→**FPT Tân Thuận 1** · Hôm nay · Sáng *(lệch điểm giao)* · `SEED S3` V-City→Cầu Giấy · **22/09** · Giờ nào cũng được *(lệch ngày)* · `SEED S4` V-City→Cầu Giấy · Hôm nay · **Sau giờ làm** *(lệch buổi)*. Mã seed cắm ở ô **GHI CHÚ** để định danh. ⛔ **ĐỪNG seed lại** — dùng cho `TC-ASN-010/011/012/022` |
| 2026-09-19 | `Phan Minh Tài` → `Đặng Châu Anh` | **đơn Đã ghép** | Tin `FPT Tân Thuận 1 → FTEL SG08 Q12` · Chiều · người nhận `Nguyễn Huỳnh Kim Huyền` — dùng làm tiền đề `TC-ASN-005/007` |
| 2026-09-19 | `Đặng Châu Giang` | **OFFER `OFFER-C1`** *(VR-009)* | `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` · Hôm nay · **Chiều (13–17h)** · đăng **15:14**. ⛔ **KHÔNG tái dùng để đếm thông báo** — đã dính 1 thông báo của tin `N1` (nay đã ghép), mà **tin đã ghép VẪN chiếm slot** ⇒ số đếm nhóm trần sẽ nhiễm bẩn |
| 2026-09-19 | `Đặng Châu Anh` | **NEED ×4 (SEED VR-009)** | Tất cả `Tài liệu · Thấp · Nhẹ · Nhỏ` + 1 ảnh **xanh lá**, người nhận `stag_huyennhk@`: **`N1`** V-City→FPT Cầu Giấy · Hôm nay · **Chiều** *(khớp đủ — nay **ĐÃ GHÉP** bởi `stag_giangdc2@` ở `TC-ASN-010`)* · **`N2`** cùng tuyến · Hôm nay · **Sau giờ làm** *(lệch buổi)* · **`N3`** V-City→**FPT Tân Thuận 1** · Hôm nay · Chiều *(lệch điểm giao)* · **`N4`** cùng tuyến · **22/09/2026** · Chiều *(lệch ngày)*. ⛔ **ĐỪNG seed lại** — dùng cho `TC-ASN-010/011/012/022` |
| 2026-09-19 | `Phan Minh Tài` → `Đặng Châu Giang` | **đơn Đã ghép** *(VR-009)* | **Tin 1** `Tòa V-City → FPT Cầu Giấy` · Hôm nay · Sáng *(đăng ~09:43)* — carrier nay là **`stag_giangdc2@`** sau `TC-ASN-020` step 9. ⚠️ Phiên sau ⛔ **đừng coi Tin 1 là tin `Chờ ghép`** nữa |


---

## §3b. Dữ liệu VR-010 tạo trên STG — 2026-09-19 16:29–18:45 (⛔ ĐỪNG SEED LẠI)

🔑 **Tất cả seed của VR-010 dùng buổi `Giờ nào cũng được` + ngày `Hôm nay`** — cố ý, để tin **không bị đóng** khi khung giờ trôi qua (bài học `T-ASN-09`). Mã seed **cắm ở ô GHI CHÚ** của wizard NEED.

| Chủ tin | Loại | Nội dung |
|---|---|---|
| `stag_giangdc2@` | **OFFER `R1`** | `FPT Cầu Giấy` → `Tòa V-City, Lê Thái Tổ` *(16:34)* — ⛔ **đã dính trần 5, không tái dùng để đếm** |
| `stag_giangdc2@` | **OFFER `R2`** | `FPT Tân Thuận 1` → **`FTEL SG08 Gò Vấp`** *(16:37)* — ⛔ cùng lý do |
| `stag_taipm@` | **OFFER `R3`** | `FTEL SG08 Gò Vấp` → `FPT Tân Thuận 1` *(18:01)* — chuông đã dùng 2/5 slot |
| `stag_taipm@` | **OFFER `R4`** | `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` *(18:04)* |
| `stag_anhdc4@` | **NEED ×9** | `SEED R1-1`…`R1-6` *(khớp `R1`)* · `SEED R2-1` *(khớp `R2`)* · `SEED X lech tuyen` = `FPT Tân Thuận 1 → Tòa V-City` *(khớp **không** tuyến nào)* · `SEED R3a dang truoc` + `SEED R3b dang sau` *(khớp `R3`)*. Tất cả `Tài liệu · Thấp · Dưới 5kg · Nhỏ` + 1 ảnh **xanh lá**, người nhận `stag_huyennhk@` |
| `stag_giangdc2@` | *(có sẵn)* **tin NEED `Hết hạn`** | `Gửi tài liệu` · `Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy` · **19/9/2026** · badge `Hết hạn` ⇒ 🔑 **tiền đề sẵn của `TC-ASN-019`, ⛔ không cần dev seed** |

⚠️ **Trạng thái chuông sau VR-010:** `stag_giangdc2@` **5/5 (ĐẦY — dính trần)** · `stag_taipm@` **2/5** · `stag_anhdc4@` chưa đo.
⇒ Phiên sau cần đếm thông báo thì **⛔ đừng dùng `stag_giangdc2@`**.

## §6. Bẫy tài khoản — bổ sung VR-010

| # | Bẫy | Xử lý |
|---|---|---|
| **`T-ASN-12`** | **FoxEco không bật cho mọi CBNV** — `stag_huyennhk@` đăng nhập FoxPro OK nhưng `Chức năng` **không có icon FoxEco**; màn `Cá nhân` cũng **không render** `Đăng xuất` ⇒ kẹt, không thoát được bằng UI | Trước khi giao vai actor cho 1 tài khoản mới: **kiểm icon FoxEco trước**. Nếu đã kẹt: `adb shell am force-stop com.hrisproject.stag && adb shell pm clear com.hrisproject.stag` rồi relaunch → về màn login *(⛔ không mất dữ liệu STG; phải cấp lại quyền **thông báo** + **vị trí**)* |
| **`T-ASN-11`** | Thông báo khớp tuyến **biến mất sau khi MỞ** trên `stag_taipm@` (2→1→0) — nhưng **không** trên `stag_giangdc2@` | **Đếm TRƯỚC khi mở** bất kỳ thông báo nào |
| — | Gõ `FTEL SG08` ⇒ gợi ý-0 trả **`FTEL SG08 Gò Vấp`**, ⛔ không phải `Quận 12` như ghi chép cũ | Gõ **đủ chuỗi** chi nhánh khi cần đúng địa điểm |
| ✅ | `T-ASN-07` *(dialog lỗi mạng giả ở `NHẬN MÃ OTP`)* — **0/7 lượt** đăng nhập gặp ở VR-010 | Vẫn giữ luật retry 1 lần, nhưng tần suất thấp |

## §3c. Dữ liệu VR-011 tạo/tiêu trên STG — 2026-09-19 20:15–21:15 (module GIFT)

| Ngày | Account | Loại | Nội dung |
|---|---|---|---|
| 2026-09-19 | `Phan Minh Tài` → `Đặng Châu Giang` | **quà `Bông hoa`** | Tặng cho đơn `Gửi khác` · `ITD Bld, Tân Thuận, Q7 → L29B-31B-33B KCX Tân Thuận` · 9/8/2026 — lúc **20:33** *(`TC-GIFT-003`)* |
| 2026-09-19 | `Phan Minh Tài` → `Đặng Châu Giang` | **quà `Ly cà phê`** | Tặng cho đơn `Gửi thuốc/y tế` · cùng tuyến · 9/8/2026 — lúc **20:37** *(`TC-GIFT-005`)* |

🔴 **HAI ĐƠN TRÊN LÀ 2 ĐƠN "HOÀN THÀNH CHƯA TẶNG QUÀ" CUỐI CÙNG** mà QC tìm được trên STG.
⇒ Sau VR-011, **cả 4 tài khoản vào được FoxEco đều KHÔNG còn đơn nào có hint `Chạm để tặng quà`**
*(kiểm trực tiếp: `taipm` · `giangdc2` · `anhptm17` · `anhdc4`)*.
⇒ ⛔ **Mọi TC cần màn "Tặng quà" nay KHÔNG chạy được** cho tới khi có đơn Hoàn thành mới:
`TC-GIFT-011` *(NOT_RUN)* · `TC-GIFT-010` *(NOT_EVIDENCED — cần chụp lại ảnh đúng slot)*.

**Cách tạo lại 1 đơn Hoàn thành (qua UI thật, ⛔ không nhờ dev seed DB):**
A đăng tin NEED khai C là người nhận → B nhấn *"Tôi mang giúp được"* → B *"Tôi đã lấy hàng"* → B giao → **C xác nhận đã nhận hàng** ⇒ đơn sang `Hoàn thành`, card của **A** hiện hint `Chạm để tặng quà`.

### Chỉ số quà/đơn đo được ở VR-011 (dùng làm mốc cho phiên sau)

| Account | Đơn đã giúp | Quà đã nhận | Chi tiết loại quà |
|---|--:|--:|---|
| `stag_taipm@` — Phan Minh Tài | 2 | 1 | `Gấu bông` ×1 |
| `stag_giangdc2@` — Đặng Châu Giang | 13 | **13** | `Bông hoa` 3 · `Ly cà phê` 3 · `Gấu bông` 4 · `Vương miện` 3 *(đã gồm 2 quà VR-011 tặng)* |
| `stag_anhptm17@` — Phan Thị Mỹ Anh | 5 | **5** | `Ly cà phê` 3 · `Vương miện` 2 ⭐ **đúng hình dạng `SEED-GIFT-05`** (5 quà / 2 loại / 3+2) |
| `stag_anhdc4@` — Đặng Châu Anh | 3 | 2 | *(chưa mở màn "Quà đã nhận")* |

⚠️ **Chuông `stag_giangdc2@` có thêm 2 thông báo quà** *(`NTF-07`, lúc 20:33 và 20:37)* — phiên sau đếm thông báo trên account này phải trừ ra.
