# Test Data — Tài khoản test STG (vai A/B/C) · module USR

> Nguồn: `DOC-v1.1-05` — `00_input/v1.1/datatest` (QC GiangDC2 cung cấp 2026-09-18). File nguồn **không commit** (đã thêm vào `.gitignore` vì chứa pass dùng chung).
> Credentials: `~/.foxeco-v2/credentials.env` (`chmod 600`) — biến `FOXECO_STG_USER_<vai>` · `FOXECO_STG_PASS`.
> ⛔ KHÔNG inline pass/SĐT cá nhân vào file này, vào TC, vào evidence hay commit message (`Project_rule §Execution Rules`).
> Dùng cho: `TC-USR-002..046` (v1.1) + `TC-USR-001..011` CARRIED (v1.0) · prefill sang `ORD`/`ASN`/`DLV` · `SEED-ORD-02` ①② (`TC-ORD-074` · `TC-ORD-076`).

## 0. Mở app FoxEco — 3 bước *(QC hướng dẫn 2026-09-18)*

1. Mở **app FoxPro** (`vn.fpt.ftel.sop.stg`) → **đăng nhập thành công** (tài khoản dưới đây + `FOXECO_STG_PASS` + **mã OTP**).
2. Vào menu bar **"Chức năng"**.
3. Nhấn **icon FoxEco**.

🔑 **FoxPro = HRIS** — cùng 1 hệ thống: **HRIS = bản web**, **FoxPro = bản app mobile** (QC chốt 2026-09-18). Test FoxEco luôn đi đường **app FoxPro**; giá trị *"HRIS"* trong §2 dưới đây là dữ liệu của chính hệ thống này.
⚠️ **OTP nhập tay** — AI không lấy được mã ⇒ người chạy mở app + đăng nhập **1 lần đầu phiên** rồi bàn giao cho AI.
> 📌 **Đính chính 2026-09-18:** `00_input/v1.1/datatest` ghi **OTP dùng chung mọi account** (bấm *"Nhập mã OTP"*). Tức về mặt kỹ thuật AI **có thể** tự đăng nhập khi được QC cho phép — nhưng ⛔ **phải hỏi trước**, vì đăng xuất sẽ **huỷ phiên đăng nhập người chạy vừa tạo**, và đăng nhập nhầm vai làm hỏng trạng thái dữ liệu không khôi phục được.
⛔ **Đổi tài khoản** (vd A → B) phải **đăng xuất khỏi app FoxPro** rồi lặp lại 3 bước — thoát riêng FoxEco là chưa đủ. ⇒ TC nào đổi vai giữa chừng (`TC-USR-025` · `TC-ORD-044/047/048/061` · lô 3 vai của `DLV`/`TS`) nên **gom chạy theo tài khoản**, ⛔ đừng nhảy qua lại.

## 1. Mapping vai → tài khoản

🔑 **Hai loại "vai" khác nhau — đừng lẫn (QC chốt 2026-09-18):**
- **Vai trong ĐƠN** (người gửi · người vận chuyển · người nhận): **hoán đổi tự do** giữa mọi tài khoản, mỗi đơn một kiểu. VD đơn 1 = A gửi · B vận chuyển · C nhận; đơn 2 = B gửi · C vận chuyển · A nhận. Bảng dưới chỉ là **gợi ý mặc định** cho TC nào không quan tâm ai đóng vai gì.
- **Vai theo TRẠNG THÁI DỮ LIỆU** (`C` = chưa từng lưu hồ sơ · `BLANK` = 2 chỉ số = 0 · `RESIGNED` = đã nghỉ việc): ⛔ **KHÔNG hoán đổi được** — nó là thuộc tính dữ liệu của chính tài khoản đó, dùng sai tài khoản thì TC mất ý nghĩa và **không khôi phục được** (lưu 1 lần là mất trạng thái).

| Vai | Biến env | MNV | HRIS có SĐT? | HRIS có địa chỉ? | Dùng cho TC |
|---|---|---|:--:|:--:|---|
| **A** — hồ sơ đầy đủ, tài khoản chính | `FOXECO_STG_USER_A` | 00131946 | ✅ | ✅ | 37 TC còn lại (mặc định mọi TC không ghi vai khác) |
| **B** — CBNV thứ 2, người nhận/đối tác đơn | `FOXECO_STG_USER_B` | 00286248 | ✅ | ✅ | `TC-USR-025` · `TC-USR-026` · (v1.0) `TC-USR-005` |
| **C** — chưa từng lưu hồ sơ, HRIS **có** SĐT + địa chỉ | `FOXECO_STG_USER_C` | 00041796 | ✅ | ✅ | `TC-USR-040` · `TC-USR-043` |
| **RESIGNED** — tài khoản **đã nghỉ việc** (chỉ dùng làm **giá trị email nhập vào**, ⛔ không đăng nhập) | `FOXECO_STG_USER_D_CANDIDATE` | 00026682 | — | — | ✅ `TC-ORD-076` (`SEED-ORD-02` ② — email người nghỉ việc ⇒ chặn tạo đơn). 🚫 Vai **D** của USR (`TC-USR-041`/`044`) đã **DESCOPED 2026-09-18**, không cần tài khoản này |
| **BLANK** — ứng viên tài khoản "trắng" (2 chỉ số = 0) | `FOXECO_STG_USER_BLANK1` | 00157112 | ✅ | ✅ | (v1.0) `TC-USR-006` — cần verify 2 chỉ số = 0 tại chỗ |
| **SPARE** — dự phòng / vai thứ 3 | `FOXECO_STG_USER_SPARE` | 00287493 | ✅ | ✅ | (v1.0) `TC-USR-005` (vai thứ 3) · thay thế C nếu C đã lỡ lưu hồ sơ |
| **BLANK2 / C2** — `stag_thuyntt22@fpt.com` · "Nguyễn Thị Thanh Thủy" · Phòng Hành chính phía Bắc ⚠️ **chưa có biến env** (QC cấp trực tiếp 2026-09-18) | *(chưa có)* | 00002352 | ✅ | ❓ | ✅ **Đã dùng ở VR-003**: `TC-USR-006` (2 chỉ số = **0/0**, verify tại chỗ) · `TC-USR-040`/`TC-USR-043` (thay vai C — QC xác nhận **chưa từng lưu hồ sơ**). 🔴 **SAU VR-003 KHÔNG CÒN "chưa từng lưu hồ sơ"** (đã lưu SĐT `0987654322`) ⇒ ⛔ không dùng lại cho TC prefill-HRIS. ⚠️ HRIS **có** SĐT nhưng **không phơi địa chỉ làm việc** trên app ⇒ thiếu oracle cho `TC-USR-040` |

**Đăng nhập:** pass dùng chung (`FOXECO_STG_PASS`) + **nhập mã OTP**. Tất cả tài khoản dạng `stag_*@fpt.com`.

## 2. Giá trị HRIS làm oracle

| Trường | Giá trị | Ghi chú khi assert |
|---|---|---|
| **Địa chỉ làm việc HRIS** (cả 5 tài khoản đang làm việc) | `HCM LôB3,E-Office,KCN TânThuận` | ⚠️ Chuỗi HRIS = **mã tỉnh + tên VP**. Đối chiếu `DOC-v1.1-04`: cột `name` = **`LôB3,E-Office,KCN TânThuận`** · `search_alias_text` = `hcm lob3 e office kcn tanthuan`. ⇒ Kỳ vọng ô "Địa chỉ mặc định" prefill **chuỗi `name`** (không có tiền tố `HCM`). App hiện nguyên `HCM LôB3,...` ⇒ **ghi nhận + hỏi BA**, chưa kết luận bug |
| **SĐT HRIS** từng tài khoản | ⛔ không chép vào repo — đọc `00_input/v1.1/datatest` (local) | Định dạng đã kiểm: **10 số, bắt đầu bằng 0** ⇒ hợp lệ theo `BR15-02` ⇒ `TC-USR-043` kỳ vọng field prefill đúng số này, **không** báo lỗi validate |
| Tên · phòng ban · MNV · email | Đồng bộ SSO, chỉ đọc | MNV dạng 8 số (`00131946`) — ⚠️ khác định dạng `FTEL####` mà `TC-USR-004` (v1.0) đang kỳ vọng; xem §4 |

🕐 **Bẫy thời điểm (QC ghi 2026-09-18):** SĐT trong `DOC-v1.1-05` **mới cập nhật ngày 18/09**, FoxEco có thể **chỉ đồng bộ sau 18/09**. ⇒ Chạy `TC-USR-043` từ **19/09 trở đi**, hoặc đọc giá trị HRIS thực tế ngay trước khi chạy. Chạy đúng 18/09 mà lệch ⇒ **không log bug**, ghi `BLOCKED`.

## 3. Thứ tự chạy bắt buộc

1. 🔴 **Chạy `TC-USR-040` + `TC-USR-043` trên vai C TRƯỚC mọi TC có bấm "Lưu thay đổi"** — lưu 1 lần thì tài khoản mất trạng thái "chưa từng lưu", không khôi phục được. Hai TC này chạy **cùng 1 phiên** trên C.
3. `TC-USR-042` chạy trên A **sau** khi A đã lưu `Tòa V-City, Lê Thái Tổ` — điều kiện "HRIS ≠ giá trị đã lưu" ✅ thoả (HRIS của A là `LôB3,E-Office,KCN TânThuận`).
4. ~~(v1.0) `TC-USR-006` chạy trên BLANK **trước** khi dùng tài khoản đó vào bất kỳ đơn nào.~~ ✅ **XONG 2026-09-18 (VR-003)** — chạy trên `00002352`, PASS.
4b. 🔴 **Tài khoản "chưa từng lưu hồ sơ" là tài nguyên TIÊU HAO.** Sau VR-003 chỉ còn **vai C (`00041796`)** giữ được trạng thái này. Muốn retest `TC-USR-040`/`TC-USR-043` sau khi dev fix bug B9 thì **phải dùng C**, hoặc xin QC cấp tài khoản mới — ⛔ đừng bấm "Lưu thay đổi" trên C trước đó.
5. `TC-USR-025` (P1): tạo đơn trên A **trước** khi sửa hồ sơ A; B làm người nhận.

## 3b. Tài khoản dùng làm GIÁ TRỊ NHẬP (không đăng nhập)

| Giá trị | Dùng ở | Ghi chú |
|---|---|---|
| `stag_anhdc4@fpt.com` (vai B) | `TC-ORD-074` · carried `TC-ORD-019/022` | `SEED-ORD-02` ① — có trên HRIS, **đang làm việc** ⇒ autofill 3 trường người nhận |
| `stag_binhnt23@fpt.com` (RESIGNED) | `TC-ORD-076` | `SEED-ORD-02` ② — **đã nghỉ việc** ⇒ nút "Tiếp theo" DISABLE, chặn tạo đơn (`C-ORD-14`) |
| Email `@fpt.com` tự đặt, vd `stag_khongtontai@fpt.com` | `TC-ORD-075` | Không tồn tại trên HRIS — ⛔ không cần xin ai |

## 4. Gap còn lại (chưa đủ data)

| # | Gap | TC bị chặn | Cần ai |
|---|---|---|---|
| 1 | ✅ **ĐÃ ĐÓNG 2026-09-18 — không phải gap data mà là nhánh không tồn tại.** QC chốt: khi tạo nhân viên trên HRIS, **SĐT + địa chỉ làm việc là trường bắt buộc** ⇒ không có CBNV nào HRIS trống 2 trường này. `TC-USR-041`/`TC-USR-044` chuyển `DESCOPED` (Status `Skipped`), giữ trong TC-MASTER để truy vết, ⛔ không chạy, ⛔ không thay bằng tài khoản khác. Coverage `BR15-02` không mất: vế *"SĐT rỗng ⇒ Lưu bị chặn"* đã phủ bởi `TC-USR-017` | ~~`TC-USR-041` · `TC-USR-044`~~ → DESCOPED | — |
| 2 | ✅ **ĐÃ ĐÓNG 2026-09-18 (VR-003).** Tài khoản `00002352` (`stag_thuyntt22@fpt.com`) được **verify tại chỗ** có đúng 2 chỉ số = **0/0** ⇒ `TC-USR-006` đã chạy và **PASS**. `BLANK1` (00157112) **không cần dùng nữa** cho mục đích này và vẫn còn nguyên trạng thái. Lưu ý: việc lưu hồ sơ **không** làm đổi 2 chỉ số ⇒ tài khoản này vẫn dùng lại được cho TC đếm chỉ số | ~~(v1.0) `TC-USR-006`~~ → PASS | — |
| 3 | 🟡 MNV thực tế dạng **8 chữ số** (`00131946`), trong khi `TC-USR-004` (v1.0) kỳ vọng dạng **`FTEL####`** và demo hiện `FTEL4417` | (v1.0) `TC-USR-004` | Hỏi BA định dạng MNV hiển thị trên app — TC có thể sai kỳ vọng, ⛔ đừng vội log bug |
