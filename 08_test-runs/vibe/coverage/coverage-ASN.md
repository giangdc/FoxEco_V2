# Coverage — module ASN — SCOPE_TOTAL = 26 TC

> Sổ cái TÍCH LŨY xuyên run cho module **ASN** (Ghép nối) — scope = **v1.1 (13 TC) + CARRIED v1.0 (13 TC)**.
> **Cập nhật lần cuối: **VR-010** (2026-09-19)** · Nguồn scope: `03_test-cases/v1.1/fragments/TC-ASN-v1.1.md` + `03_test-cases/v1.0/fragments/TC-ASN-v1.0.md`
> **Tổng: có verdict cuối 24/26 · CÒN NỢ 2** (2 NOT_RUN + 0 NOT_EVIDENCED)
>
> 🔴🔴 **VR-010 (2026-09-19) — PHÁT HIỆN LỖI CHẶN NHÓM TRẦN: trần 5 thông báo khớp tuyến bị áp theo TÀI KHOẢN, không theo TUYẾN.**
> Hệ quả: `TC-ASN-016` ❌ FAIL (5 tin NEED khớp → chỉ 4 thông báo) · `TC-ASN-025` ❌ FAIL (tuyến OFFER thứ 2 còn trống 5/5 slot vẫn **không** nhận được thông báo nào).
> ⚠️ **`TC-ASN-014` và `TC-ASN-017` PASS nhưng KHÔNG chứng minh được luật trần per-tuyến** — tiền đề "tuyến đã đủ 5" chưa bao giờ đạt vì trần tài khoản chặn trước ⇒ **phải chạy lại cả 2 sau khi fix**.
> Verdict hợp lệ: ✅ PASS · ❌ FAIL · 🚫 BLOCKED · ⚠️ NOT_EVIDENCED · ⏳ NOT_RUN · ⛔ N-A

> 🔢 **SCOPE_TOTAL = 26** = 21 (v1.0) + 13 (v1.1) − 8 ID trùng (`TC-ASN-006/008/011/012/015/016/017/018`, **lấy bản v1.1** theo `CLAUDE.md`). Fragment v1.1 ghi rõ *"Không gỡ TC nào"* ⇒ ⛔ không có TC DEPRECATED phải trừ.
>

> 🟢🟢 **2026-09-19 (VR-007) — BLOCKER ĐÃ GỠ, module ASN chạy được.** Callout 🔴 ngay dưới *(ghi lúc 07:58)* khai *"0/26 chạy được vì bug `B1` + OTP nhập tay"* — **CẢ HAI ĐỀU SAI**:
> | Tưởng | Thực tế |
> |---|---|
> | bug `B1` chặn đăng tin | ✅ **đăng được** cả NEED lẫn OFFER — `repro/RP-ORD-B1-dang-tin-duoc-lai-2026-09-19/` |
> | OTP nhập tay ⇒ AI không đổi được tài khoản | ✅ **OTP staging CỐ ĐỊNH** ⇒ AI **tự logout/login**; phiên này đổi **2 lượt** (`stag_taipm@` ↔ `stag_anhdc4@`) |
>
> ⇒ VR-007 chạy **3 TC / 3 PASS** (`013` P1 · `023` P2 · `021` P3). **21 TC còn nợ nay là NỢ CÔNG SỨC**, ⛔ không còn là nợ môi trường.
> 🔑 Tài khoản + OTP: `04_test-data/valid/USR-accounts.md` (secret ở `~/.foxeco-v2/credentials.env`).
> 🔴🔴 **2026-09-19 (bổ sung 08:40) — RÚT LẠI lý do chặn đã ghi ở lượt trước. Đọc kỹ trước khi dùng file này.**
>
> Lượt ghi đầu (07:58) khai *"20 TC chặn bởi bug `B1` — không đăng được tin NEED"*. **Điều đó SAI.**
> QC chất vấn *"tự tạo tin đăng rồi logout, login account khác được mà?"* ⇒ đi kiểm THẬT trên app, kết quả:
>
> | Phép thử (08:26–08:41) | Kết quả |
> |---|---|
> | Đăng tin **OFFER** (*"Tôi nhận giao hàng"*) | ✅ **THÀNH CÔNG** — *"Đã ghi nhận tuyến đường!"*, logcat sạch |
> | Đăng tin **NEED** (*"Tôi cần gửi hàng"*, đủ 3 bước) | ✅ **THÀNH CÔNG** — *"Đăng tin thành công!"*, ⛔ **không có `REQ_400`** |
> | Nút **Đăng xuất** | ✅ **CÓ** — ở **FoxPro host → Cá nhân** (⛔ không nằm trong FoxEco) |
>
> ⇒ **`B1`/VR-004 KHÔNG tái hiện.** Sai lầm của lượt trước là **thừa kế kết luận của phiên khác làm tiền đề mà không tự kiểm lại trong phiên này** — đúng điều `SKILL.md` cấm (*"copy locator/kết luận từ run cũ mà không re-verify"*).
> ⚠️ ⛔ **Chưa kết luận được `B1` đã được fix hay chỉ không tái hiện trên tài khoản này** — VR-004 chạy bằng `Đặng Châu Giang`, phép thử này bằng `Đặng Châu Anh`. Cần retest đúng tài khoản/dữ liệu của VR-004 rồi mới đóng `B1`.
>
> 🟡 **Blocker THẬT còn lại (đã thu hẹp rất nhiều):** không phải "không đăng được tin" mà là **cần tài khoản thứ 2 thao tác nhận đơn**. Đăng xuất thì làm được, nhưng **đăng nhập lại có cần OTP hay không thì CHƯA kiểm** — ⛔ cố tình không thử, vì nếu cần OTP mà không có thì **mất luôn môi trường test** của QC.
>
> 🗂️ **Dữ liệu ĐÃ TẠO trên STG trong phép thử này** (tài khoản `Đặng Châu Anh`, 2026-09-19):
> | Loại | Nội dung |
> |---|---|
> | **OFFER** | tuyến `Tòa V-City, Lê Thái Tổ` → `FPT Cầu Giấy` · Hôm nay–Hôm nay · buổi **Sáng** ⇒ dùng được làm **`SEED-ASN-01`** |
> | **NEED** | `Tài liệu · Giá trị thấp · Nhẹ · Nhỏ` + 1 ảnh · cùng tuyến trên · buổi **Sáng** · người nhận `Nguyễn Thị Thanh Thủy` |
>
> 📌 **2 tin này cùng tuyến + cùng buổi + cùng ngày ⇒ về lý thuyết PHẢI khớp tuyến.** Đây là tiền đề sẵn cho `TC-ASN-023` (thông báo khớp ≤60s) và nhóm `TC-ASN-011/012/022/025`.
>
> 🔧 **2 phát hiện phụ cần QC/BA xem:**
> 1. **Nhãn buổi thật = `Sáng (8–12h)`**, trong khi `TC-ASN-v1.1.md §0` ghi QA-obs là *"Sáng (6–12h)"* ⇒ **sửa fragment**, đúng thứ fragment dặn *"verify lại khi vibe-test"*.
> 2. **Autofill SĐT người nhận trả về MNV** — điền email `stag_thuyntt22@fpt.com` thì ô SĐT tự điền `0000002352` (chính là MNV `00002352` thêm số 0), app lập tức báo *"Số điện thoại không hợp lệ"*. Cùng họ `BUG-008` (không load SĐT từ HRIS).

## Tiến độ theo run

| Run | Ngày | TC chạy trong run | Verdict thu được |
|-----|------|-------------------|------------------|
| `repro/RP-ASN-lo-sdt-sau-ghep-2026-09-19` | 2026-09-19 | 0 | ⛔ 0 verdict — kết luận *"chặn tiền đề"* **sau đó bị bác bỏ** (xem callout 🟢 đầu file) |
| **VR-007** | 2026-09-19 | **3** | **3P** — `013` · `023` · `021` |
| **VR-008** | 2026-09-19 | **5** | **5P** — `001` · `002` · `003` · `004` · `009` *(phiên dừng theo yêu cầu QC lúc 12:33)* |
| **VR-010** | 2026-09-19 | **7** | **5P / 2F** — lô 1: `015`·`016`❌·`017`·`014` *(trần & thứ tự)* · lô 2: `025`❌ *(phép thử tách nguyên nhân)* · lô 3: `018` · lô 4: `019` |
| **VR-009** | 2026-09-19 | **7** | **7P** — lô 1: `005` · `007` · `020` *(chốt nốt chặng step 6–9 của VR-008)* · lô 2: `010` · `011` · `012` · `022` *(seed lại `OFFER-C1`+`N1..N4` trên khung **Chiều** còn mở)* |

## Chi tiết từng TC

| Testcase ID | Verdict | Scenario ID | Priority | Title | Run | Evidence | Ghi chú |
|---|---|---|---|---|---|---|---|
| TC-ASN-001 | ✅ PASS |SC-ASN-001 |P1 |Check Carrier xác nhận "Tôi mang giúp được" đưa đơn sang trạng thái "Đã ghép" | VR-008 | `VR-008-ASN-2026-09-19/screenshots/TC-ASN-001__verify-card-da-ghep.png` | Ghép thành công tin của A. 🔑 Oracle vai = **tiền tố card** ở màn Hoạt động: `Giao:` = mình vận chuyển · `Gửi:` = mình là chủ tin. Badge `Đã ghép` MCP-verified. |
| TC-ASN-002 | ✅ PASS |SC-ASN-002 |P2 |Check nhấn "Huỷ" trên modal xác nhận giữ đơn ở "Chờ ghép" và không lộ SĐT | VR-008 | `VR-008-ASN-2026-09-19/screenshots/TC-ASN-002__verify-huy-giu-cho-ghep.png` | Modal `Xác nhận mang giúp` → `Huỷ` đóng modal, giữ nguyên Chi tiết tin. SĐT của A (`0833329408`) 🚫 NOT FOUND, nút `Gọi` mờ, CTA còn nguyên. Đối chứng: cùng tin sau khi ghép thì SĐT hiện (xem TC-ASN-004). |
| TC-ASN-003 | ✅ PASS | SC-ASN-003 | P1 | Check đơn ghép ngay mà chủ tin không phải thực hiện bước duyệt nào | VR-008 | `VR-008-ASN-2026-09-19/screenshots/TC-ASN-003__verify-khong-co-nut-duyet.png` | Chủ tin mở đơn `Đã ghép`: 3 phép find phủ định `Duyệt`/`Chấp nhận`/`Phê duyệt` đều 🚫 NOT FOUND trên **toàn cây**; nút duy nhất = `Huỷ đơn`; dải `Đã ghép · chờ shipper lấy hàng` là nhãn tĩnh ⇒ đúng cơ chế ghép ngay. |
| TC-ASN-004 | ✅ PASS | SC-ASN-004 | P1 | Check sau khi ghép cả người gửi và người vận chuyển đều thấy SĐT của bên còn lại | VR-008 | `VR-008-ASN-2026-09-19/screenshots/TC-ASN-004__verify-a-thay-sdt-b.png` + `VR-008-ASN-2026-09-19/screenshots/TC-ASN-004__verify-b-thay-sdt-a-va-c.png` | Chạy 2 chặng/2 tài khoản. B thấy A `0833329408` + người nhận C `0989014863`; A thấy B `0343439724`, nút `Gọi` bật cả 2 phía. Đối chứng âm trước ghép ở TC-ASN-002. 🆕 SĐT của `stag_huyennhk@` = `0989014863` (trước đây chưa biết). |
| TC-ASN-005 | ✅ PASS | SC-ASN-005 | P2 | Check người ngoài cặp ghép không thấy SĐT của hai bên trong cặp | VR-009 | `VR-009-ASN-2026-09-19/screenshots/TC-ASN-005__verify-bangtin-khong-co-tin-da-ghep.png` + `VR-009-ASN-2026-09-19/screenshots/TC-ASN-005__verify-hoatdong-khong-co-don-cap-ghep.png` | Chạy bằng tài khoản D `stag_giangdc2@` (**Đặng Châu Giang**) ngoài cặp ghép. Tin 2 (`FTEL SG08`) 🚫 NOT FOUND ở **cả** Bảng tin lẫn **2 tab con** Hoạt động; SĐT của A (`0833329408`) và B (`0343439724`) đều 🚫 NOT FOUND trên toàn cây ⇒ chứng cứ trực tiếp, ⛔ không suy từ việc đơn vắng mặt. |
| TC-ASN-006 | ⏳ NOT_RUN | SC-ASN-006 | P1 | Check hai người vận chuyển nhận gần đồng thời chỉ một người ghép được | — | — | **Lý do: QC chốt để lại** — 2026-09-19 16:30 QC yêu cầu *"case nào cần 2 emulator thì để lại giúp t"*. Máy chạy VR-010 chỉ có **1 emulator** (RAM tổng 7GB / trống ~2GB ⇒ bật máy thứ 2 có rủi ro OOM giết emulator đang chạy giữa phiên). ⇒ QC tự chạy nhóm đa thiết bị. |
| TC-ASN-007 | ✅ PASS | SC-ASN-007 | P1 | Check tin đã ghép biến mất khỏi Bảng tin và khỏi luồng gợi ý của Carrier khác | VR-009 | `VR-009-ASN-2026-09-19/screenshots/TC-ASN-007__verify-bangtin-vang-tin-da-ghep.png` + `VR-009-ASN-2026-09-19/screenshots/TC-ASN-007__verify-chuong-khong-co-goi-y.png` | Cùng phiên đăng nhập D. Tin `Đã ghép` vắng khỏi Bảng tin; chuông ⛔ không có `Tìm thấy đơn hàng phù hợp tuyến` nào (danh sách **có** 4 thông báo loại khác ⇒ không phải empty state giả). ⚖️ **Giới hạn đã khai:** D không sở hữu OFFER trùng tuyến nên chưa cô lập được nguyên nhân — muốn chặt hơn phải dùng Carrier CÓ OFFER trùng tuyến. |
| TC-ASN-008 | ⏳ NOT_RUN | SC-ASN-008 | P2 | Check ba phiên ba vai cùng cập nhật "Đã ghép" trong vòng 5 giây | — | — | **Lý do: QC chốt để lại** — cần **3 thiết bị** đo mốc ≤5 giây; cùng quyết định 2026-09-19 16:30 như `TC-ASN-006`. |
| TC-ASN-009 | ✅ PASS | SC-ASN-009 | P2 | Check Carrier nhận thông báo khớp tuyến khi có tin NEED trùng cả hai điểm và giao khung giờ | VR-008 | `VR-008-ASN-2026-09-19/screenshots/TC-ASN-009__verify-tro-dung-tin-seed-s1.png` | Seed S1 (trùng đủ 2 điểm + ngày + buổi với OFFER của B) đăng 12:09:50 → chuông B lúc 12:31 có `HÔM NAY` + mục `20 phút trước`; tap mở đúng tin mang dấu `SEED S1` ở ô Ghi chú (oracle định danh, ⛔ không suy từ thời gian). |
| TC-ASN-010 | ✅ PASS | SC-ASN-010 | P2 | Check nhấn "Nhận giao" ở tin khớp tuyến ghép đơn và mở màn Theo dõi đơn | VR-009 | `VR-009-ASN-2026-09-19/screenshots/TC-ASN-010__verify-theo-doi-don-va-sdt-nguoi-gui.png` | Seed lô 2 (`OFFER-C1` khung **Chiều** còn mở + `N1` khớp đủ). Thông báo khớp tuyến → tap mở đúng tin (header `19 phút trước` + ảnh seed xanh lá) → ghép → `Theo dõi đơn`; §NGƯỜI GỬI hiện `Đặng Châu Anh` **0343439724**, nút `Gọi` bật. 🔴 **Steps sai nhãn:** nút `"Nhận giao"` 🚫 NOT FOUND — CTA thật là `Tôi mang giúp được` ⇒ đề nghị BA/QC sửa Steps (nghiệp vụ vẫn ĐÚNG nên ⛔ không hạ FAIL). |
| TC-ASN-011 | ✅ PASS | SC-ASN-011 | P2 | Check không có thông báo khớp tuyến khi tin NEED lệch điểm giao hàng | VR-009 | `VR-009-ASN-2026-09-19/screenshots/TC-ASN-011__verify-chuong-khong-co-tb-cho-seed-lech-diem-giao.png` + `VR-009-ASN-2026-09-19/screenshots/TC-ASN-011__pre-seed-n3-lech-diem-giao-tren-bang-tin.png` | Seed `N3` lệch **đúng 1 biến** = điểm giao (V-City → **FPT Tân Thuận 1**), cùng ngày cùng buổi. Chuông D: `instance(1)` 🚫 NOT FOUND ⇒ đúng **1** thông báo và nó là `N1`. ✅ **Có đối chứng dương cùng lô** (`N1` vẫn sinh thông báo) nên sự vắng mặt là kết luận được. |
| TC-ASN-012 | ✅ PASS | SC-ASN-011 | P2 | Check không có thông báo khớp tuyến khi khoảng ngày không giao nhau | VR-009 | `VR-009-ASN-2026-09-19/screenshots/TC-ASN-012__verify-chuong-khong-co-tb-cho-seed-lech-ngay.png` + `VR-009-ASN-2026-09-19/screenshots/TC-ASN-012__pre-seed-n4-lech-ngay-tren-bang-tin.png` | Seed `N4` lệch **đúng 1 biến** = khoảng ngày (**22/09/2026**, ⛔ không giao với Hôm nay), trùng cả 2 điểm + buổi Chiều. Chuông D: `instance(1)` 🚫 NOT FOUND. ℹ️ App dùng **khoảng NGÀY + tập BUỔI**, ⛔ không nhập giờ tự do như Steps v1.0 mô tả (`08:00–09:00` vs `20:00–21:00`) — đã hiện thực đúng *ý định* TC. |
| TC-ASN-013 | ✅ PASS | SC-ASN-012 | P1 | Check tài khoản không được gợi ý khớp tuyến cho tin do chính mình đăng | VR-007 | `VR-007-ASN-2026-09-19/screenshots/TC-ASN-013__verify-khong-thong-bao-tin-cua-minh.png` | Tin NEED trùng **tuyệt đối** tuyến+ngày+buổi với OFFER của chính mình ⇒ điều kiện dễ sinh thông báo nhất, app **vẫn loại trừ đúng**. Badge `Tin của bạn` ✅, ⛔ không có CTA nhận đơn |
| TC-ASN-014 | ✅ PASS | SC-ASN-013 | P2 | Check Carrier chỉ được gợi ý tối đa 5 tin khi có 6 tin NEED khớp cùng tuyến | VR-010 | `VR-010-ASN-2026-09-19/screenshots/TC-ASN-014__verify-toi-da-5-goi-y.png` | 6 tin NEED khớp `OFFER-R1` ⇒ gợi ý **4** ≤ trần 5 ⇒ assertion thoả. ⚠️ **PASS trên cận trên CHƯA bị chạm**: app dừng ở 4 vì **trần theo TÀI KHOẢN** (xem `TC-ASN-025` FAIL), ⛔ không phải trần gợi ý per-tuyến ⇒ TC này hiện **không phân biệt được** app đúng/sai ở mốc 5. **Chạy lại sau khi fix.** |
| TC-ASN-015 | ✅ PASS | SC-ASN-014 | P2 | Check tin OFFER có 3 tin NEED khớp nhận đủ 3 thông báo | VR-010 | `VR-010-ASN-2026-09-19/screenshots/TC-ASN-015__verify-dung-3-thong-bao.png` | Seed `OFFER-R1` (`FPT Cầu Giấy → Tòa V-City`, Hôm nay, **Giờ nào cũng được** — chọn buổi này để né bẫy `T-ASN-09` hết hiệu lực khung giờ) + 3 tin NEED khớp. Đếm được **BASELINE 1 + đúng 3 mới**; 3 cái mới còn vạch cam/chấm đỏ (**chưa đọc**), baseline đã đọc ⇒ 2 oracle độc lập. |
| TC-ASN-016 | ❌ FAIL | SC-ASN-014 | P2 | Check tin OFFER có 5 tin NEED khớp nhận đủ 5 thông báo | VR-010 | `VR-010-ASN-2026-09-19/screenshots/TC-ASN-016__step3-FAIL-chi-4-thong-bao-moi.png` + `VR-010-ASN-2026-09-19/screenshots/TC-ASN-016__pre-du-5-tin-need-tren-bang-tin.png` | 🔴 **Expected 5 · Actual 4.** Bảng tin có **đủ 5** tin NEED khớp (6′·11′·23′·28′·32′, kiểm bằng page source 2 vị trí cuộn) nhưng chuông chỉ thêm **4**. Tổng chuông = 5 = 4 mới + 1 baseline ⇒ nghi **trần 5 tính theo TÀI KHOẢN, không theo TUYẾN** (`C-ASN-04(e)`) — tách giả thuyết ở `TC-ASN-025`. 🪤 `T-ASN-10`: `instance(N)` chỉ thấy node đang render, ⛔ không dùng làm phép đếm tuyệt đối. |
| TC-ASN-017 | ✅ PASS | SC-ASN-014 | P2 | Check tin NEED khớp thứ 6 không sinh thêm thông báo khi tuyến đã đủ trần 5 | VR-010 | `VR-010-ASN-2026-09-19/screenshots/TC-ASN-017__verify-so-thong-bao-khong-doi.png` | Tin NEED thứ 6 (`SEED R1-6`) ⇒ số thông báo giữ nguyên 4, ⛔ không có mục mới (đo 2 lần 17:38 & 17:43). ⚠️ **KHÔNG chứng minh `C-ASN-04(d)`**: tuyến `R1` mới có 4 thông báo, thứ chặn tin thứ 6 là **trần theo TÀI KHOẢN** ⇒ tiền đề "tuyến đã đủ 5" chưa bao giờ đạt. **Chạy lại sau khi fix `TC-ASN-025`.** |
| TC-ASN-018 | ✅ PASS | SC-ASN-015 | P3 | Check danh sách gợi ý ưu tiên tin trùng tuyến trước, thời gian đăng sau | VR-010 | `VR-010-ASN-2026-09-19/screenshots/TC-ASN-018__verify-thu-tu-goi-y.png` + `VR-010-ASN-2026-09-19/screenshots/TC-ASN-018__verify-dinh-danh-r3b-tren-cung.png` | Tuyến sạch `OFFER-R3` (`FTEL SG08 Gò Vấp → FPT Tân Thuận 1`) + 3 tin NEED: `X` lệch tuyến 18:25 (sớm nhất) · `R3a` 18:31 · `R3b` 18:39. Chuông: `R3b` **trên** `R3a`; `X` ⛔ **không xuất hiện**. 🔑 Định danh bằng **mã seed đọc trực tiếp ở mục `Ghi chú`** trên Chi tiết tin ⇒ **ĐÍNH CHÍNH VR-009**: mục `Ghi chú` **CÓ tồn tại**. ⚖️ Giới hạn: tin lệch tuyến bị loại hẳn nên ⛔ không đo được vị trí tương đối của nó. |
| TC-ASN-019 | ✅ PASS | SC-ASN-016 | P2 | Check tin NEED đã quá hạn không xuất hiện trong gợi ý và không sinh thông báo khớp tuyến | VR-010 | `VR-010-ASN-2026-09-19/screenshots/TC-ASN-019__verify-thong-bao-chi-tro-tin-con-song.png` + `VR-010-ASN-2026-09-19/screenshots/TC-ASN-019__verify-bangtin-vang-tin-het-han.png` + `VR-010-ASN-2026-09-19/screenshots/TC-ASN-019__pre-tin-need-het-han-ngay-hom-nay.png` | ⛔ **KHÔNG cần dev seed** (Steps/Test Data ghi "không seed được qua UI" — **đã lỗi thời**): STG sẵn có tin NEED `Hết hạn` **đề ngày hôm nay** của `stag_giangdc2@` (`Tòa V-City → FPT Cầu Giấy · 19/9/2026`), xem ở `Đơn của tôi → Đã hoàn thành`. `stag_taipm@` đăng `OFFER-R4` trùng tuyến ⇒ nhận **đúng 2** thông báo, **cả 2 mở ra tin CÒN SỐNG** (9 giờ · 2 giờ, đều còn CTA) ⇒ tin hết hạn sinh **0** thông báo, và **vắng mặt** khỏi Bảng tin. Đối chứng dương nằm ngay trong phép thử. 🪤 `T-ASN-11`: thông báo **biến mất sau khi mở** ⇒ đếm TRƯỚC khi mở. |
| TC-ASN-020 | ✅ PASS | SC-ASN-017 | P2 | Check Carrier huỷ nhận đơn trước khi lấy hàng thì tin trở lại Bảng tin và Carrier khác ghép được | VR-008 + VR-009 | `VR-009-ASN-2026-09-19/screenshots/TC-ASN-020__verify-carrier-thu-3-ghep-duoc.png` + `VR-009-ASN-2026-09-19/screenshots/TC-ASN-020__verify-vai-carrier-tren-hoat-dong.png` | **Đủ 2 chặng ⇒ verdict cuối.** Step 1–5 PASS ở VR-008; step 6–9 chạy ở VR-009 bằng Carrier thứ 3 `stag_giangdc2@`: tin trở lại Bảng tin → ghép được → `Theo dõi đơn` vai carrier + card `Giao:` badge `Đã ghép`. 🔑 Định danh đúng tin giữa 3 card trùng tuyến bằng nhãn tuổi tin `5 giờ trước`. |
| TC-ASN-021 | ✅ PASS | SC-ASN-018 | P3 | Check đăng hai tin NEED liên tiếp tạo ra hai tin độc lập trên Bảng tin | VR-007 | `VR-007-ASN-2026-09-19/screenshots/TC-ASN-021__verify-hai-tin-doc-lap.png` | Đúng 2 tin của A, 2 tuyến độc lập, ⛔ không ghi đè. ⚠️ Steps ghi loại hàng `"Giấy tờ, hồ sơ"` — nhãn **không tồn tại** (app dùng `Tài liệu`, `C-ORD-09`) ⇒ đề nghị QC sửa câu chữ |
| TC-ASN-022 | ✅ PASS | SC-ASN-011 | P2 | Check không có thông báo khớp tuyến khi ngày giao nhau nhưng buổi không chung | VR-009 | `VR-009-ASN-2026-09-19/screenshots/TC-ASN-022__verify-chuong-khong-co-tb-cho-seed-lech-buoi.png` + `VR-009-ASN-2026-09-19/screenshots/TC-ASN-022__pre-seed-n2-lech-buoi-tren-bang-tin.png` | Seed `N2` lệch **đúng 1 biến** = buổi (`Sau giờ làm`, OFFER chỉ có `Chiều` ⇒ không buổi chung), **ngày vẫn giao nhau**, ⛔ không chọn `Giờ nào cũng được`. Chuông D: `instance(1)` 🚫 NOT FOUND ⇒ BR lọc theo buổi chạy đúng. Có đối chứng dương `N1`. |
| TC-ASN-023 | ✅ PASS | SC-ASN-011 | P2 | Check có thông báo khớp tuyến trong vòng 60 giây khi khớp đầy đủ điều kiện | VR-007 | `VR-007-ASN-2026-09-19/screenshots/TC-ASN-023__verify-thong-bao-khop-tuyen.png` | Thông báo *"Tìm thấy đơn hàng phù hợp tuyến của bạn"* trỏ **đúng** tin vừa đăng. 🕐 Độ trễ đo được ∈ **(5s, 65s]** — cận trên vượt 60s **do làm tròn nhãn "3 phút trước"**, ⛔ không phải app chậm. 🔁 Đề nghị đo lại `NFR-04` bằng **2 thiết bị** |
| TC-ASN-024 | ⛔ N-A | SC-ASN-006 | P1 | Check 50 request ghép đồng thời trên cùng 1 tin giữ tỷ lệ trùng 0% | — | — | **Lý do:** cần công cụ **concurrency/load test gọi thẳng API** (JMeter/k6) bắn 50 request đồng thời — fragment `TC-ASN-v1.1.md` ghi rõ *"⛔ không thực hiện bằng thao tác tay trên UI"*, giao automation/backend. ⛔ Ngoài phạm vi `vibe-test` UI thuần |
| TC-ASN-025 | ❌ FAIL | SC-ASN-014 | P2 | Check mỗi tuyến OFFER có trần 5 thông báo độc lập, không cộng dồn | VR-010 | `VR-010-ASN-2026-09-19/screenshots/TC-ASN-025__step3-FAIL-tuyen-2-khong-co-thong-bao.png` + `VR-010-ASN-2026-09-19/screenshots/TC-ASN-025__pre-seed-r2-khop-tuyen-2.png` | 🔴 **`OFFER-R2` (tuyến hoàn toàn khác, 0/5 slot) + 1 tin NEED trùng khít ⇒ KHÔNG sinh thông báo nào; tổng vẫn đúng 5.** Đo 2 lần (17:38 · 17:43), tin đã 2–7 phút ≫ `NFR-04` 60s ⇒ loại trừ "đến chậm". ⇒ **trần 5 áp theo TÀI KHOẢN, không theo tuyến** — đúng rủi ro `C-ASN-04(e)`. Đây cũng là nguyên nhân gốc của `TC-ASN-016` FAIL. **Cần `/log-bug`.** |
| TC-ASN-026 | ⛔ N-A | SC-ASN-019 | P2 | Check request đọc tin OFFER qua API bởi người ngoài bị chặn và ghi audit log | — | — | **Lý do:** cần **API client** (Postman/tương đương) + token của tài khoản không sở hữu tin, và kiểm **audit log** phía server — fragment ghi rõ *"UI không có đường dẫn tới tin OFFER của người khác"*, giao automation/backend/security test. ⛔ Ngoài phạm vi `vibe-test` UI thuần |

## Tổng hợp

| Verdict | Số | TC |
|---|---|---|
| ✅ PASS | 20 | `TC-ASN-001` · `002` · `003` · `004` · `005` · `007` · `009` · `010` · `011` · `012` · `013` · **`014`** · **`015`** · **`017`** · **`018`** · **`019`** · `020` · `021` · `022` · `023` |
| ❌ FAIL | 2 | **`TC-ASN-016`** (5 tin NEED khớp → chỉ 4 thông báo) · **`TC-ASN-025`** (tuyến OFFER thứ 2 không nhận thông báo) — **cùng 1 nguyên nhân gốc** |
| 🚫 BLOCKED | 0 | — |
| ⚠️ NOT_EVIDENCED | 0 | — |
| ⏳ NOT_RUN | 2 | `TC-ASN-006` (2 thiết bị) · `TC-ASN-008` (3 thiết bị) — **QC chốt để lại 2026-09-19 16:30** |
| ⛔ N-A | 2 | `TC-ASN-024` (concurrency 50 request) · `TC-ASN-026` (API + audit log) |
| **Tổng** | **26** | |

**Có verdict cuối: 24/26 · CÒN NỢ: 2** ⇒ §8 = **PARTIAL**.

---

## 🔴 Kết luận nghiệp vụ của VR-010 — 1 lỗi gốc, 4 TC liên đới

> **Lỗi:** trần **5 thông báo khớp tuyến** được áp cho **TOÀN TÀI KHOẢN**, ⛔ không phải cho **từng tuyến OFFER**.
> Đúng rủi ro BA đã lường trước ở `C-ASN-04(e)` — *"rủi ro thật nếu backend dùng chung 1 bộ đếm cho cả tài khoản"*.

**Chuỗi số đo khép kín** (tài khoản `stag_giangdc2@`, mọi mốc đều đo bằng page source ghép nhiều vị trí cuộn):

| # | Thời điểm | Việc đã làm | Số thông báo khớp tuyến |
|---|---|---|---|
| 0 | 16:28 | *(chưa seed gì)* | **1** *(tồn dư `OFFER-C1` của VR-009)* |
| 1 | 17:18 | `OFFER-R1` + **5** tin NEED khớp *(đã kiểm đủ 5 trên Bảng tin)* | **5** ⇒ chỉ **+4** ❌ |
| 2 | 17:38 & 17:43 | thêm tin NEED **thứ 6** của `R1` | **5** ⇒ +0 |
| 3 | 17:38 & 17:43 | thêm **`OFFER-R2` (tuyến khác, 0/5 slot)** + 1 tin NEED trùng khít | **5** ⇒ **+0** ❌ **mắt xích quyết định** |

⇒ `H2` ("thông báo đến chậm") **bị bác bỏ**: đo 2 lần cách nhau 5 phút, tin đã 2–13 phút tuổi ≫ `NFR-04` (≤60s).

**Tác động nghiệp vụ:** CBNV đăng nhiều tuyến sẽ **mất hoàn toàn** thông báo khớp tuyến ở mọi tuyến sau khi **tổng** chạm 5 —
kể cả tuyến vừa đăng chưa có thông báo nào. ⇒ **Cần `/log-bug`** *(chưa log trong phiên này)*.

**4 TC liên đới:**

| TC | Verdict | Quan hệ với lỗi |
|---|---|---|
| `TC-ASN-016` | ❌ FAIL | biểu hiện trực tiếp (thiếu 1 thông báo) |
| `TC-ASN-025` | ❌ FAIL | **phép thử chẩn đoán** — chứng minh trần theo tài khoản |
| `TC-ASN-014` | ✅ PASS ⚠️ | assertion `≤5` thoả nhưng **cận trên chưa bị chạm** ⇒ **chạy lại sau fix** |
| `TC-ASN-017` | ✅ PASS ⚠️ | quan sát đúng expected nhưng **tiền đề "tuyến đủ 5" chưa đạt** ⇒ **chạy lại sau fix** |

## 🪤 Bẫy đo lường mới của VR-010 (ảnh hưởng mọi phiên sau)

| # | Bẫy | Cách xử lý |
|---|---|---|
| **`T-ASN-10`** | `appium_find_element` / `scroll_to_element` với `.instance(N)` **chỉ thấy node ĐANG RENDER**. Màn Thông báo render ~4 mục ⇒ `instance(5)` báo NOT FOUND dù danh sách có 6 mục | ⛔ **Không** dùng `instance(N)` làm phép đếm tuyệt đối cho danh sách dài. ✅ **Dump page source ở nhiều vị trí cuộn rồi ghép theo nhãn tuổi** |
| **`T-ASN-11`** | **Thông báo khớp tuyến BIẾN MẤT khỏi danh sách sau khi MỞ** (quan sát trên `stag_taipm@`: 2 → 1 → 0). ⚠️ Khác `stag_giangdc2@` (mục đã đọc vẫn nằm lại) | **Đếm TRƯỚC khi mở**. Đây nhiều khả năng là lời giải thật cho `T-ASN-09` của VR-009 |
| **`T-ASN-12`** | `stag_huyennhk@` **KHÔNG có icon FoxEco** trong `Chức năng` ⇒ chỉ làm được vai **người nhận**, ⛔ không làm actor. Màn `Cá nhân` của tài khoản này cũng **không render** mục `Đăng xuất` ⇒ phải `adb shell pm clear` để thoát | Chọn actor trong 4 tài khoản còn lại |
| **`T-ASN-13`** *(đính chính)* | `VR-009` ghi *"Chi tiết tin KHÔNG có mục GHI CHÚ"* — **SAI**. Mục `Ghi chú` **có**, chỉ render khi ô Ghi chú khác rỗng | ✅ **Mã seed cắm ở ô Ghi chú = oracle định danh tin MẠNH NHẤT**, hơn hẳn nhãn tuổi tin (bị làm tròn) |

## 🗂️ Dữ liệu VR-010 đã tạo trên STG (2026-09-19) — ⛔ đừng seed lại

| Chủ tin | Loại | Nội dung |
|---|---|---|
| `stag_giangdc2@` | **OFFER ×2** | `OFFER-R1` `FPT Cầu Giấy → Tòa V-City, Lê Thái Tổ` · `OFFER-R2` `FPT Tân Thuận 1 → FTEL SG08 Gò Vấp` — đều Hôm nay · **Giờ nào cũng được** |
| `stag_taipm@` | **OFFER ×2** | `OFFER-R3` `FTEL SG08 Gò Vấp → FPT Tân Thuận 1` · `OFFER-R4` `Tòa V-City, Lê Thái Tổ → FPT Cầu Giấy` — đều Hôm nay · Giờ nào cũng được |
| `stag_anhdc4@` | **NEED ×9** | `SEED R1-1`…`R1-6` *(khớp `R1`)* · `SEED R2-1` *(khớp `R2`)* · `SEED X lech tuyen` *(`FPT Tân Thuận 1 → Tòa V-City`, khớp KHÔNG tuyến nào)* · `SEED R3a dang truoc` + `SEED R3b dang sau` *(khớp `R3`)*. Tất cả: `Tài liệu · Thấp · Dưới 5kg · Nhỏ` + 1 ảnh xanh lá · người nhận `stag_huyennhk@` · Hôm nay · **Giờ nào cũng được** · **mã seed cắm ở ô GHI CHÚ** |

🔑 **Buổi `Giờ nào cũng được` là lựa chọn CÓ CHỦ Ý** cho mọi seed của VR-010 — để tin không bị đóng khi khung giờ trôi qua
(bài học `T-ASN-09`). Phiên sau nên giữ quy ước này khi chạy nhóm thông báo.
