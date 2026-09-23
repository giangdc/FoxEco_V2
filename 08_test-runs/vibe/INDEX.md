# INDEX — mọi phiên vibe-test

> Registry của tất cả phiên `vibe-test`. Thêm **1 dòng sau mỗi phiên**.
> 📋 Muốn biết **module còn nợ TC nào** → xem `coverage/coverage-<MOD>.md`, **không** đọc INDEX.
> 🔍 Locator cho `implement-automation` → `locators/vibe-locators-latest.md`.

| Run | Ngày | Module | Platform | Scope | Chạy | Kết quả | Evidence | §8 | Folder |
|---|---|---|---|--:|--:|---|---|---|---|
| **VR-001** | 2026-09-18 | **USR** | mobile (Appium) | 46 | 40 | **20P / 14F** / 5B · N-A 2 · NOT_RUN 5 🔄 | 40/40 ✅ | PARTIAL | `VR-001-USR-2026-09-18/` |
| **VR-002** | 2026-09-18 | **ORD** | mobile (Appium) | 88 | 43 | 25P / 14F / 3B · 1 chạy dở | 43/43 ✅ | PARTIAL | `VR-002-ORD-2026-09-18/` |
| **VR-003** | 2026-09-18 | **USR** | mobile (Appium) | 46 | 4 | **2P / 2F** · còn nợ **1** | 4/4 ✅ | PARTIAL | `VR-003-USR-2026-09-18/` |
| **VR-004** | 2026-09-18 | **ORD** | mobile (Appium) | 88 | **46** | **27P / 17F / 2B** · còn nợ **19** → **22** *(♻️ 2026-09-21 QC reset `083`/`084`/`085` về NOT_RUN)* | 46/46 ✅ | PARTIAL | `VR-004-ORD-2026-09-18/` |
| **VR-005** | 2026-09-19 | **HOME** | mobile (Appium) | 30 | **14** | **13P / 0F / 1B** · N-A 1 · còn nợ **15** | 14/14 ✅ | PARTIAL | `VR-005-HOME-2026-09-19/` |
| *(không mở VR)* | 2026-09-19 | **ASN** | mobile (Appium) | 26 | **0** | ⛔ **0 verdict** → chuyển thành phiên **repro** · N-A 2 · còn nợ **24** | n/a *(hợp đồng nhẹ)* | PARTIAL | `repro/RP-ASN-lo-sdt-sau-ghep-2026-09-19/` |
| **VR-007** | 2026-09-19 | **ASN** | mobile (Appium) | 26 | **3** | **3P / 0F / 0B** · N-A 2 · còn nợ **21** | 3/3 ✅ | PARTIAL | `VR-007-ASN-2026-09-19/` |
| **VR-008** | 2026-09-19 | **ASN** | mobile (Appium) | 26 | **5** | **5P / 0F / 0B** *(3 P1)* · N-A 2 · còn nợ **16** | 5/5 ✅ | PARTIAL | `VR-008-ASN-2026-09-19/` |
| **VR-009** | 2026-09-19 | **ASN** | mobile (Appium) | 26 | **7** | **7P / 0F / 0B** · N-A 2 · còn nợ **9** | 7/7 ✅ | PARTIAL | `VR-009-ASN-2026-09-19/` |
| **VR-010** | 2026-09-19 | **ASN** | mobile (Appium) | 26 | **7** | **5P / 2F / 0B** 🐛 *(⚠️ 2026-09-21: 2 FAIL `016`/`025` đã đổi PASS — QC recheck, không phải bug)* · N-A 2 · còn nợ **2** *(QC để lại)* | 7/7 ✅ | PARTIAL | `VR-010-ASN-2026-09-19/` |
| **VR-015** | 2026-09-21 | **ASN** | mobile (Appium · **real device + emulator**) | 26 | **1** | **1P / 0F / 0B** — `TC-ASN-006` *(lần 1 không hợp lệ: bên thua chưa chấp nhận điều khoản; lần 2 hợp lệ)* · sổ ASN: **26/26 có verdict** (sau recheck 016/025: **23P·0F·3 BLOCKED**; chỉ v1.1 **10P·3B/13**) | 1/1 ✅ | COMPLETED-WITH-OPEN-ITEMS | `VR-015-ASN-2026-09-21/` |
| *(không mở VR)* | 2026-09-21 | **FEED** | mobile (Appium) | — | **0** | ⛔ 0 verdict — kiểm tra 1 hành vi theo QC → phiên **repro**: chủ tin mở tin từ **Bảng tin** ra `Chi tiết tin` (không có `Chỉnh sửa`/`Huỷ đơn`), từ **Hoạt động** ra `Theo dõi đơn` · PRD **không có rule** ⇒ bug `BUG-028` / `FE-312` | n/a *(hợp đồng nhẹ)* | — | `repro/RP-FEED-chu-tin-bang-tin-khong-theo-doi-don-2026-09-21/` |
| **VR-011** | 2026-09-19 | **GIFT** | mobile (Appium) | **14** | **12** | **8P / 1F / 2B / 1 NE** 🐛 FE-308 · còn nợ **3** *(♻️ 2026-09-21: `TC-GIFT-012` FAIL→PASS theo QC)* | 11/11 ✅ | PARTIAL | `VR-011-GIFT-2026-09-19/` |
| **VR-012** | 2026-09-19 | **DLV** | mobile (Appium) | **81** | **15** | **13P / 2F / 0B** · N-A 4 · còn nợ **62** 🚫 | 15/15 ✅ | PARTIAL | `VR-012-DLV-2026-09-19/` |
| **VR-016** | 2026-09-21 | **FEED** | mobile (Appium) | 15 | **5** | **4P / 0F / 1B** *(`009` BLOCKED→PASS retest data QC cấp; `015` FAIL→PASS, QC chấp nhận hành vi app + sửa Expected, `BUG-029` rút lại; `007` FAIL→PASS retest account `anhdc4` + data hợp lệ)* · còn nợ **10** *(carried v1.0, ngoài phạm vi — chỉ chạy TC v1.1 theo QC)* | 5/5 ✅ | PARTIAL | `VR-016-FEED-2026-09-21/` |
| **VR-017** | 2026-09-21 | **ACT** | mobile (Appium) | 18 | **10** | **6P / 2F / 2B** 🐞 `BUG-030/031` draft *(chờ QC review)* · `015` FAIL→BLOCKED · `017` FAIL→PASS *(QC chốt 2 case này app đúng; `BUG-032` xoá)* · còn nợ **8** *(CARRIED v1.0, ngoài phạm vi — chỉ chạy TC v1.1 theo QC)* | 10/10 ✅ | PARTIAL | `VR-017-ACT-2026-09-21/` |
| **VR-018** | 2026-09-21 | **CNL** | mobile (Appium) | 22 | **13** | **5P / 6F / 2B** 🐞 4 ứng viên *(chưa log)* · còn nợ **9** *(CARRIED v1.0, ngoài phạm vi — chỉ chạy TC v1.1 theo QC)* | 13/13 ✅ | PARTIAL | `VR-018-CNL-2026-09-21/` |
| **VR-028** | 2026-09-23 | **GIFT** | mobile (Appium) | 14 | **1** | **1P** (`TC-GIFT-008`, tài khoản trắng `stag_minhndn2@`) · QC dừng trước `TC-GIFT-011` · còn nợ **2** (`011` NOT_RUN · `010` NOT_EVIDENCED) | 1/1 ✅ | PARTIAL | `VR-028-GIFT-2026-09-23/` |

## Ghi chú theo phiên

> 🟢 **VR-008 (2026-09-19, 11:32–12:33) — ASN lần đầu chạy được luồng ghép đơn đầu-cuối. Phiên DỪNG GIỮA CHỪNG theo yêu cầu QC ("mai tiếp"), ⛔ không phải đã xong module.**
> **5 TC chạy / 5 PASS** (`001` `002` `003` `004` `009` — trong đó **3 P1**). Coverage ASN: **5/26 → 10/26**, còn nợ **16**.
> 🔑 **Chìa khoá mở được module:** gom việc **theo TÀI KHOẢN** (B → A → B, 2 lượt đổi ~2 phút/lượt bằng OTP cố định) thay vì theo TC — 4 TC đầu xong trong ~20 phút mà ⛔ không đổi tài khoản lần nào.
> 🌱 **Đã seed sẵn 4 tin NEED (`SEED S1..S4`) trên STG**, mỗi tin lệch OFFER của B **đúng 1 chiều** (đủ khớp / lệch điểm giao / lệch ngày / lệch buổi) ⇒ phiên sau chỉ cần **mở chuông + chụp evidence riêng từng TC** là chốt được `010` `011` `012` `022` (~15 phút). ⛔ **ĐỪNG seed lại.**
> 🔑 **Kỹ thuật dùng lại được:** cắm mã seed vào ô **GHI CHÚ** lúc đăng tin ⇒ assert "thông báo trỏ đúng tin nào" bằng chuỗi (`textContains("SEED S1")`), ⛔ không phải suy từ timestamp.
> 🪤 **6 bẫy mới `T-ASN-01..06`** (xem `vibe-locators-latest.md`) — 2 bẫy **đã thực sự chặn phiên này**: ảnh 5 MB bị từ chối **im lặng** (bộ đếm giữ `0/5`, không báo lỗi) và **địa chỉ gõ tay không commit** nếu không tap gợi ý.
> ⚡ **0 `appium_get_page_source` trên 7 màn** — toàn bộ locator lấy từ cache `vibe-locators-latest.md` + `find_element` trực tiếp (đúng luật B1/B2). `appium_screenshot` của MCP tốn ~216k ký tự/lần ⇒ evidence chụp bằng `adb screencap`.
> 📌 **3 việc cho QC/BA:** (1) ảnh quá khổ bị từ chối im lặng — **thuộc ORD**, nên mở bug riêng; (2) màn Thông báo **không tự refresh** (11:44 tưởng mất thông báo, 12:31 hiện đủ) — chưa có SC nào phủ; (3) `TC-ASN-010` Steps ghi nút `Nhận giao` nhưng app hiện `Tôi mang giúp được`.

> 🔴🔴 **ĐÍNH CHÍNH LỚN 2026-09-19 08:40 — `B1` KHÔNG TÁI HIỆN, RÚT LẠI mọi khai báo "không đăng được tin".**
> QC chất vấn *"tự tạo tin đăng rồi logout, login account khác được mà?"* ⇒ đi kiểm thật: **đăng OFFER ✅ thành công · đăng NEED ✅ thành công** (đủ 3 bước, logcat sạch, ⛔ không `REQ_400`); **nút Đăng xuất ✅ CÓ** ở **FoxPro host → Cá nhân**.
> ⇒ Các dòng `VR-005`/`ASN` bên dưới khai *"bug `B1` chặn N TC"* là **SAI** — lỗi do **thừa kế kết luận của phiên khác làm tiền đề mà không tự re-verify**, đúng điều `SKILL.md` cấm.
> ⚠️ ⛔ **Chưa đóng `B1`**: mới chứng minh không tái hiện trên `Đặng Châu Anh`; VR-004 chạy bằng `Đặng Châu Giang`. Giả thuyết đáng test trước: VR-004 khai **email người nhận = chính tài khoản đang đăng nhập** (tự gửi cho mình).
> 📄 Chi tiết + ảnh: `repro/RP-ORD-B1-dang-tin-duoc-lai-2026-09-19/report.md`


**VR-001 — USR (v1.1 + CARRIED v1.0), tài khoản A, emulator-5554**
- 🔴 **SCOPE_TOTAL = 46 = 38 (v1.1) + 8 (CARRIED v1.0)** — v1.1 không gộp CARRIED ⇒ phải mở **cả 2 fragment**.
- 🔄 **ĐÍNH CHÍNH 2026-09-18 — `B1` RÚT LẠI, còn 7 ứng viên bug.** QC chốt hành vi `TC-USR-015` (lưu xong **không banner** + **về màn Cá nhân**) là **ĐÚNG** ⇒ đã sửa `Expected` của TC (fragment + TC-MASTER v1.1 + LATEST, Σ TC không đổi) và đổi verdict **FAIL → PASS**. ⚠️ `TC-USR-027`/`029` neo vào banner nay đã bỏ ⇒ **chờ QC quyết**; upstream `SC-USR-014`/`AC-30.1.01`/`BR15-05` chưa đồng bộ.
- 🐞 **7 ứng viên bug** (B2..B8) từ 11 TC FAIL; 3 TC FAIL còn lại là **dây chuyền**, ⛔ không mở bug riêng.
  Nặng nhất: **B2** chặn lưu im lặng (SĐT có khoảng trắng/`+84`) · **B4** chuỗi rác được lưu làm địa chỉ (lan sang `ORD` — VR-002 đã xác nhận đường prefill) · **B5** gợi ý tìm theo mã tỉnh.
- 🚫 **6 BLOCKED** — 5 do **master data văn phòng STG ≠ `DOC-v1.1-04`** (cần BA refresh), 1 do dây chuyền B1.
- ⏳ **4 NOT_RUN** — cùng 1 blocker: cần đăng nhập tài khoản khác + **OTP nhập tay** (vai C ×2, BLANK, 3-vai).
- 📨 **2 việc route về `/analyze-requirements`**: `TC-USR-011` mâu thuẫn FR15 · wizard "Đăng tin" có 2 field bắt buộc chưa đặc tả.
- 🗂️ **Dữ liệu phát sinh trên STG**: 2 tin NEED `Chờ ghép` + hồ sơ A bị đổi (xem `vibe-report.md §Dữ liệu phát sinh`).

**VR-002 — ORD (v1.1 + CARRIED v1.0), tài khoản A, emulator-5554**
- 🔴 **SCOPE_TOTAL = 88 = 48 (v1.1) + 40 (CARRIED v1.0)** — v1.1 không gộp CARRIED ⇒ phải mở **cả 2 fragment**. Chạy 3 lô / 43 TC, **còn nợ 46**.
- 🐞 **14 FAIL ≠ 14 bug — gộp về 6 ứng viên (B1..B6)**. Nặng nhất **B1 chặn im lặng**: nút `Tiếp theo` khoá mà **không báo lỗi** ở 5 nhánh (`063` **P1** · `064` · `066` · `083`/`084` · `077`) — đối chứng: app **có** báo lỗi đúng ở 3 nhánh khác (`068`/`058`/`057`) ⇒ **bỏ sót**, không phải thiếu framework. Kế đến **B2** không có popup thoát wizard (mất dữ liệu soạn dở, cùng họ `TC-USR-045`) · **B3** trần ảnh thực tế **4/5** (⇒ `070`/`071` BLOCKED **bởi bug**) · **B4** autofill người nhận thiếu ô địa chỉ giao (`074` **P1**, ⚠️ **hỏi BA trước khi log**) · **B5** buổi không có mặc định · **B6** chọn được buổi đã qua.
- 🔴 **4 TC CARRIED v1.0 HẾT HIỆU LỰC** (`006`/`007`/`008`/`014`) + 1 TC sai câu chữ (`017`) ⇒ **nợ QC**, chờ chốt `DESCOPED` theo `Project_rule §10.5`. ⛔ Không log bug.
- 🟢 **Oracle v1.1 khớp app**: `C-ORD-18` (nhãn Trọng lượng/Kích thước + kiểu chip) · `C-ORD-14` (chặn email lạ/nghỉ việc) · `C-ORD-15(a)` (biên 7/8 ngày) · `C-ORD-10`/`11` (prefill + ô tự do). ❌ `C-ORD-15(b)` **không** được thi hành.
- 🔴 **`KB-VIBE-01` (`KP-01 §10.2`) ĐÃ LỖI THỜI** — app **có** chip "Tài liệu", **không còn** `Giấy tờ, hồ sơ` ⇒ ràng buộc nào dẫn `KB-VIBE-01` (kể cả module khác) phải kiểm lại.
- 🗂️ **Không phát sinh dữ liệu trên STG** (chưa đăng tin nào). 🧪 Tự dựng `SEED-ORD-01` trong `/sdcard/Pictures/` của emulator (ảnh **đúng 5MB** chưa dùng).
- 🔧 **T6–T10** (5 bẫy locator mới) + 5 đính chính VR-001 → đã merge `locators/vibe-locators-latest.md` (62/62 = 100%).

**VR-003 — USR (tiếp phần còn nợ của VR-001), tài khoản `00002352`, emulator-5554**
- Chạy **4/5 TC còn nợ** ⇒ module USR nay **45/46 có verdict cuối, CÒN NỢ 1** (`TC-USR-005`).
- 👤 **Tài khoản mới, chưa có trong `USR-accounts.md` lúc bắt đầu phiên**: `stag_thuyntt22@fpt.com` · MNV `00002352` · "Nguyễn Thị Thanh Thủy". QC xác nhận **chưa từng lưu hồ sơ**; đo tại chỗ **2 chỉ số = 0/0** ⇒ dùng được cho **cả** `TC-USR-006` (vai BLANK) **và** `TC-USR-040/043` (vai C). Đã bổ sung vào `USR-accounts.md §1`.
- ✅ **Đóng gap #2** của `USR-accounts.md §4` — lần đầu có tài khoản được **verify** 2 chỉ số = 0 (trước đó `BLANK1` mới là *ứng viên*).
- 🐞 **1 ứng viên bug mới — B9**: màn "Cập nhật thông tin" **không prefill SĐT và địa chỉ từ HRIS** ở lần mở đầu tiên (`TC-USR-040` + `TC-USR-043`, **gộp 1 bug**). Không phải ca lẻ — VR-001 thấy **y hệt** trên tài khoản A (có địa chỉ HRIS đã biết).
- ✅ `TC-USR-027` PASS theo **bản Steps/Expected sửa 2026-09-18** (kiểm tính nhất quán hành vi không-banner qua 2 lần lưu) ⇒ gỡ nốt hệ quả của việc rút lại `B1`.
- 🙋 **3 việc chờ QC/BA**: Q1 xem lại DESCOPE `TC-USR-044` · Q2 **địa chỉ rỗng vẫn lưu được** (dữ kiện mới cho câu hỏi treo ở `TC-USR-029`) · Q3 `Test Title` của `TC-USR-027` còn chữ "banner tự ẩn" (như case `TC-USR-015`).
- 🔧 **T1–T4** (4 bẫy locator mới) — nguy hiểm nhất **T2**: field rỗng vẫn trả `text` = chuỗi **hint** ⇒ assert `text != ""` sẽ **PASS oan**.
- 🗂️ **Dữ liệu phát sinh**: hồ sơ `00002352` nay có SĐT `0987654322` ⇒ ⚠️ **mất trạng thái "chưa từng lưu"**, không dùng lại tài khoản này để retest B9 (vai **C** `00041796` vẫn còn nguyên).
- 📌 Đính chính bookkeeping: §Tổng hợp của `coverage-USR.md` trước phiên ghi `BLOCKED 6 / NOT_RUN 4`, đếm thật là `5 / 5` (sót lúc `TC-USR-027` đổi BLOCKED→NOT_RUN). Đã sửa; dòng VR-001 ở bảng trên cũng sửa theo.

**VR-004 — ORD (`--all`, chạy lại toàn scope), tài khoản A, emulator-5554**
- Chạy **46 TC / 5 lô** ⇒ module ORD từ **42/88** lên **69/88 có verdict cuối, CÒN NỢ 19**. **Evidence 46/46.** *(♻️ 2026-09-21: QC reset `TC-ORD-083`/`084`/`085` ⇒ nay **66/88, CÒN NỢ 22** — xem `coverage/coverage-ORD.md`.)*
- 🛑 **Còn nợ KHÔNG phải vì hết sức phiên** — đã chạy hết mọi TC chạy được. 19 TC còn lại **chặn tiền đề**: **17** cần 1 đơn NEED đăng thành công (bug B1 dưới), **2** cần tài khoản B.
- 🐞🔴 **B1 — P1 BLOCKER MỚI, nặng nhất module: KHÔNG ĐĂNG ĐƯỢC TIN NEED** (`TC-ORD-004`). Bấm `Đăng tin ngay` với dữ liệu hợp lệ đủ 3 bước ⇒ API trả **400 `REQ_400`** *"Dữ liệu đầu vào không hợp lệ"* và app **im lặng tuyệt đối** (không toast/banner/spinner, nút vẫn bật). 3 lần bấm/3 lần lỗi; đã loại trừ giả thuyết ghi chú 300 ký tự; xác nhận **không đơn nào được tạo**. Log: `logcat-TC-ORD-004-REQ_400.txt`.
- 🔑 **Tìm ra nguyên nhân gốc của "chặn im lặng" ở bước 2 (bẫy T11):** **CẢ HAI ô địa chỉ bắt buộc chạm gợi ý `address-suggestion-N`**; gõ tay đủ chữ ⇒ `Tiếp theo` khoá **vĩnh viễn**, app không báo gì. Mất ~20 MCP call để khoanh vùng. Hồ sơ A **mất địa chỉ mặc định** (gốc `TC-USR-040`) nên ô này nay **rỗng** ⇒ mọi phiên sau **buộc** gõ + chạm gợi ý.
- ♻️ **BÁC BỎ một phần kết luận VR-002:** luật *"địa chỉ giao phải khác địa chỉ lấy"* **CÓ thông báo lỗi đầy đủ** (`TC-ORD-026` PASS) — VR-002 kết luận *"chặn im lặng"* vì gõ tay nên validate **chưa chạy tới** luật đó. ⇒ **gỡ `083`/`084` khỏi dẫn chứng bug chặn-im-lặng nhánh-trùng-địa-chỉ**, chuyển sang bug *"địa chỉ phải chọn gợi ý"*. Ghi chú VR-002 *"so sánh CÓ trim"* là **suy diễn không căn cứ**.
- ⚠️ **1 TC ĐỔI VERDICT:** `TC-ORD-017` PASS → **FAIL** (mất prefill địa chỉ lấy hàng). **Không phải TC lỗi thời — lỗi thật**, gộp 1 bug với `TC-ORD-043` + `TC-USR-040` (2 module).
- 🟢 **Đối chứng mạnh cho bug chặn im lặng:** ô **SĐT người nhận** (`TC-ORD-025`, 5/5 nhánh) và ô **SĐT/tên uỷ quyền** (`079`/`081`) **CÓ** lỗi inline đầy đủ; ô **email** và ô **tên người nhận** thì **không có lỗi nào**. ⇒ ⛔ Dev **không được** đóng bug bằng lý do *"app chưa có cơ chế báo lỗi"*.
- 💡 **Khuyến nghị thiết kế:** form **OFFER** dùng cơ chế *nút luôn bật + lỗi đỏ inline khi submit* — **UX tốt hơn NEED**. Nên **port cơ chế đó sang NEED** thay vì fix OFFER cho giống NEED (`TC-ORD-050`).
- 🐞 **Bug mới khác:** **lỗi validate không tự xoá khi đã sửa input** (bẫy **T13** — suýt tạo verdict PASS sai ngay trong phiên) · **copy không có phản hồi thị giác** (`085`, đo bằng sentinel clipboard + lấy mẫu pixel). ♻️ **1 ứng viên bug TỰ RÚT trong phiên**: *nút disable không làm mờ* (`008`) — đo pixel cho thấy app **CÓ** làm mờ `(253,175,62)` vs `(255,160,0)`; kết luận ban đầu sai vì nhìn bằng mắt, **VR-002 đã đúng**.
- 🔴 **Nợ QC — 5 TC hết hiệu lực** chờ `DESCOPED`: `006` · `014` *(mâu thuẫn TRỰC TIẾP `063` P1)* · `007` · `008` · `033` *(v1.1 bỏ khung giờ mặc định)*. Riêng **`011` chỉ cần bỏ step 4-5** là dùng lại được. **2 TC cần xem lại thiết kế**: `084` (không thực thi được đúng ý đồ trên v1.1) · `034` (spec gap: tóm tắt bước 3 thiếu 3 trường bắt buộc mới).
- 🗂️ **Dữ liệu phát sinh trên STG: KHÔNG có đơn mới nào** (bug B1 chặn). 🧪 `SEED-ORD-01` của VR-002 **đã mất** (`/sdcard` trống) ⇒ dựng lại **`SEED-ORD-02`**, kèm **bản đồ instance** trong Photo Picker (`_recon__photo-picker-seed-ord-02.png`).
- 🔧 **T11–T14** (4 bẫy mới) + **4 đính chính** map VR-002 → đã merge `locators/vibe-locators-latest.md` (**35/35 = 100%**). Màn **Wizard Bước 3/3** lần đầu được harvest.
- 📨 **3 việc route về `/analyze-requirements`** + 1 clarification BA (màn đơn *đã ghép* không lộ SĐT, **trái banner cam kết**).

**VR-005 — HOME (v1.1 + CARRIED v1.0), tài khoản A, emulator-5554**
- 🔢 **SCOPE_TOTAL = 30, ⛔ KHÔNG phải 33** như `TC-HOME-v1.1.md §0.1` ghi. Phép *"24 − 2 + 11"* của fragment **đếm trùng 3 TC MODIFIED** (`TC-HOME-008/019/021` có ở **cả 2 file**, `CLAUDE.md` chốt *"LUÔN lấy bản v1.1"*). Hợp nhất theo ID duy nhất: 24 − 2 (`010`/`024` DEPRECATED) − 3 (trùng) + 11 = **30** = 19 CARRIED + 11 v1.1. ⛔ Không sửa fragment (`§10.5` FREEZE Σ TC) — đây là đính chính **cách ĐẾM**, không thêm/bớt TC.
- 🔴 **Blocker chi phối cả module: STG có 0 tin NEED hợp lệ** — xác nhận **2 bề mặt độc lập** (Trang chủ §Tin mới `home-news-empty` + màn Bảng tin *"Chưa có tin nào"*) ⇒ ⛔ không phải lỗi lọc riêng của Trang chủ. Vì *"Tin mới"* **loại trừ tin của chính mình** (`SC-HOME-019`), tài khoản A ⛔ **không tự seed được** ⇒ **8 TC** phải chờ **tài khoản B + OTP nhập tay** (cùng blocker VR-001/VR-003).
- 🍀 **Chính dữ kiện đó lại MỞ KHOÁ `TC-HOME-026`:** `fragment §0.3` xếp TC này vào nhóm *"không dựng được trên STG dùng chung ⇒ ghi Blocked"*, nhưng STG tình cờ sạch tin nên empty state `EMP-01` verify được **thật**, đủ **4/4 vế nguyên văn** ⇒ 🟢 **xác nhận oracle phản trực giác của `C-HOME-04`**: chuỗi *"…trong khu vực của bạn"* **giữ nguyên** dù tin load toàn quốc, đúng như BA chốt *"giữ nguyên nhé"*. ⚠️ PASS **neo vào 05:59 2026-09-19** — cửa sổ đóng ngay khi có người đăng tin.
- ✅ **Ứng viên bug H1 ĐÃ ĐÓNG (2026-09-21):** `TC-HOME-007` — app hiện `Tiện đường — Giúp đồng nghiệp` (chuỗi PRD, `C-HOME-01(b)`); Expected cũ theo BRD là lỗi thời ⇒ **sửa Expected, FAIL → PASS, không chạy lại, không log bug**. Vế *"nhấn banner không điều hướng"* PASS.
- 🚫 **1 BLOCKED** — `TC-HOME-002` ở step 2 (0 tin ⇒ không mở được Chi tiết tin). **3/4 màn con còn lại đã kiểm và ĐÚNG** (Theo dõi đơn · Wizard · Thông báo: không bottom nav, có nút quay lại) ⇒ ⛔ vẫn **không** khai PASS một phần.
- ⚠️ **5 TC PASS kèm khai báo lệch step** (`009`/`011`/`012`/`013`/`015`): dùng **đơn có sẵn** thay vì tự đăng tin ở step 1 — **bug `B1` của VR-004 vẫn chặn đăng tin NEED**. Cả 5 ca Expected **không assert trạng thái đơn** (chỉ assert thành phần/nhãn/điều hướng) ⇒ verdict tin được. Lệch được ghi rõ trong `vibe-log.md`, ⛔ không giấu.
- 🔧 **3 bẫy locator MỚI T15–T17** + **T2 tái hiện lần 3** → merge `locators/vibe-locators-latest.md` (**51/51 = 100%**), **màn Trang chủ lần đầu harvest đầy đủ** (8 màn).
  **T15** chấm đỏ chuông = **ViewGroup ẩn danh** (không text/desc/rid) · **T16** **thanh progress 5 bước KHÔNG có node nào** trong tree — **cả 2 bắt buộc đo pixel**, ⛔ `find_element` vô vọng · **T17** `content-desc` card đơn là **chuỗi gộp 5 dòng** ⇒ `descriptionStartsWith("<Vai>: <Loại hàng>")` · **T2** ca mới `home-news-empty` (`id` 🚫 / `resourceId(...)` ✅).
- 📨 **3 việc route `/analyze-requirements`:** (1) card OFFER *"Nhận giao hàng"* nằm trong section "Đơn của tôi" nhưng **không có nhãn vai** — `SC-HOME-011/012/013` chưa đặc tả; (2) section hiện **cả đơn `Đã huỷ`/`Đã giao`** (6 card) — mâu thuẫn *"đơn đang hoạt động"*; (3) header Trang chủ **không có node icon vai trò nào** ⇒ nghi `SC-HOME-004` chưa build.
- 🗂️ **Dữ liệu phát sinh:** toàn bộ thông báo của A **đã đọc** (`TC-HOME-006` dùng nút bulk `Đánh dấu đã đọc`) ⇒ ⚠️ retest `TC-HOME-005` cần **sự kiện sinh thông báo mới**. ⛔ Không đăng tin, không nhận/huỷ đơn nào — hero giữ `13`, cộng đồng giữ `317 đơn · 23743 người`.
- 🛑 **Dừng KHÔNG phải vì hết sức phiên** — đã chạy hết mọi TC mà dữ liệu STG hiện tại cho phép. 16 TC còn lại chặn ở **tiền đề dữ liệu/môi trường**: 8 cần tài khoản B · 5 cần 3 tài khoản + fix `B1` · 2 cần môi trường riêng (`028` ⛔ bất khả trên STG dùng chung: cần hệ thống 0 đơn Hoàn thành, đang có 317) · 1 là NFR load-test (`032` → `⛔ N-A`, thuộc skill `k6-load-test`).

**ASN (v1.1 + CARRIED v1.0) — 2026-09-19 · tài khoản `Đặng Châu Anh` · emulator-5554 — ⛔ KHÔNG mở run `VR`, chuyển thành `repro/RP-ASN-lo-sdt-sau-ghep-2026-09-19/`**
- ⛔ **0 VERDICT ⇒ ⛔ KHÔNG mở run `VR-`.** `vibe/VR-*` là hợp đồng ĐẦY ĐỦ, **bắt buộc ≥1 TC chạy kèm evidence per-TC** (`verify_evidence.py`: `log_format_broken = not tc_results`). Phiên 0-verdict **không đủ tư cách** là run `VR` ⇒ phần recon chuyển về `repro/` (hợp đồng nhẹ: report + ≤3 ảnh). **Ledger 26 TC vẫn ghi đủ ở `coverage/coverage-ASN.md`.** SCOPE_TOTAL **26** = 21 (v1.0) + 13 (v1.1) − 8 ID trùng (lấy bản v1.1); fragment ghi rõ *"Không gỡ TC nào"*. Cả **26/26 TC chặn tiền đề**, ⛔ không TC nào chạy được ⇒ ledger = 24 `⏳ NOT_RUN` + 2 `⛔ N-A`, mỗi dòng kèm lý do. ⛔ **Không khai bất kỳ TC nào là đã phủ.**
- 🔴 **Chặn gốc KHÔNG nằm ở ASN** mà ở hạ tầng dùng chung: **20 TC** chặn bởi *0 tin trên STG + bug `B1`* (VR-004, đăng tin NEED trả `400 REQ_400`) · **4 TC** cần 2–4 thiết bị + **OTP nhập tay** (chỉ có 1 emulator) · **2 TC** ngoài phạm vi UI (`024` concurrency tool · `026` API + audit log) ⇒ `⛔ N-A`, giao automation/backend/security.
- 🔴 **ASN là module phụ thuộc seed data nặng nhất dự án** — mọi TC đều là *ghép nối*, cần **≥2 tài khoản và ≥1 tin** mới bắt đầu test được. ⛔ **Đừng lên lịch chạy ASN trước khi fix `B1`**, sẽ lặp lại đúng phiên này.
- 🟢 **ĐÍNH CHÍNH clarification của VR-004 — SĐT CÓ lộ sau khi ghép.** VR-004 ghi *"màn đơn đã ghép không lộ SĐT, trái banner cam kết"*; đo lại trên đúng màn đó thấy cụm `NGƯỜI GIAO HÀNG` = tên `Phan Thị Mỹ Anh` + **SĐT `0947153040`** + nút `Gọi` (MCP verified). ⚠️ Mới kiểm **vai người NHẬN**, còn `TC-ASN-004` đòi vai **gửi**/**vận chuyển** ⇒ TC vẫn `⏳ NOT_RUN` và clarification **phải mở lại kiểm đúng vai**, ⛔ không đóng bằng quan sát này.
- 🔧 **Bẫy mới T18 — nguyên nhân gốc của kết luận sai trên:** màn "Theo dõi đơn" **chỉ cuộn khi bước cuộn NHỎ**. `scroll` mặc định + `swipe` toạ độ đều **báo "Successfully scrolled" nhưng màn đứng yên** (4 lần thử) ⇒ page source thiếu phần dưới nếp gấp ⇒ dễ kết luận *"app không có X"*. Cách đúng: `scroll_to_element(..., scrollDistancePreset="small")`. ⛔ **KHÔNG** dùng `adb shell wm density` để xem vùng bị che — **app restart về host FoxPro, mất ngữ cảnh** (đã dính trong phiên). **T2 tái hiện lần 4**: `accessibility id "Gọi"` 🚫 / `text("Gọi")` ✅.
- 👤 **ĐỔI TÀI KHOẢN giữa VR-005 và phiên ASN này — suýt tạo phát hiện sai.** VR-005 chạy bằng `Đặng Châu Giang` (hero `13`), phiên này là **`Đặng Châu Anh`** (hero `3`) — **không ai báo trước**. Cùng 1 đơn (`Tòa V-City → FPT Cầu Giấy`, `Đã ghép`) hiện **`Gửi:`** ở VR-005 và **`Nhận:`** ở phiên này, nhìn hệt bug *"nhãn vai tính sai"*; kiểm header trước khi kết luận mới thấy là **2 tài khoản khác nhau** ⇒ hành vi **ĐÚNG**, đồng thời là **đối chứng dương** cho `TC-HOME-011/012/013`. 📌 **Bài học: luôn đọc tên tài khoản ở header trước khi so kết quả với phiên trước.**
- 🚦 **Đã thử mở `VR-006` rồi RÚT LẠI — Stop hook chặn đúng.** Vi phạm `log_format_broken`: run `VR` mà **0 TC section** chính là format của những phiên **mất sạch evidence**, gate ⛔ không có ngoại lệ cho phiên 0-verdict. ⛔ **Không bịa section TC để gate xanh**; cách đúng là **không mở run `VR`**. Đã xoá `VR-006-ASN-2026-09-19/` và chuyển sang `repro/RP-ASN-lo-sdt-sau-ghep-2026-09-19/` — `validate-vibe-run.mjs --check` xác nhận **✓ hợp đồng NHẸ OK** (report + 3 ảnh, không video).
- 🗂️ **Không phát sinh dữ liệu trên STG** — không đăng tin, không nhận/huỷ đơn nào.

**VR-007 — ASN (v1.1 + CARRIED v1.0), `stag_taipm@` → `stag_anhdc4@`, emulator-5554**
- 🟢 **Phiên ĐẦU TIÊN của ASN thu được verdict: 3 TC / 3 PASS** — `TC-ASN-013` (**P1**) · `TC-ASN-023` (P2) · `TC-ASN-021` (P3). Module từ **2/26** lên **5/26 có verdict cuối**.
- 🔓 **Hai blocker từng khai đều bị bác bỏ trong ngày:** (1) bug `B1` *"không đăng được tin"* → **đăng được cả NEED lẫn OFFER**; (2) *"OTP nhập tay"* → **OTP staging CỐ ĐỊNH**, AI **tự logout/login**, phiên này đổi **2 lượt**. 🔑 Gốc rễ sai lầm cũ: **thừa kế kết luận phiên khác làm tiền đề mà không tự re-verify** — đúng điều `SKILL.md` cấm; QC chất vấn mới lộ.
- 🟢 **Đối chứng chéo mạnh 013 ⟷ 023** — cùng cơ chế, **cùng tuyến `Tòa V-City → FPT Cầu Giấy` buổi Sáng**: chủ tin (Tài) **KHÔNG** nhận thông báo khớp tuyến, người khác (Anh) **CÓ** ⇒ chứng minh app **loại trừ theo chủ sở hữu**, ⛔ không phải *"không gửi gì cả"*. Một TC đơn lẻ không kết luận được điều này.
- ⚠️ **`TC-ASN-023` chạm biên NFR-04:** đăng `09:42:54`, quan sát `09:46:59`, nhãn *"3 phút trước"* ⇒ **độ trễ ∈ (5s, 65s]**. Cận trên vượt 60s **đúng 5 giây do làm tròn nhãn (độ phân giải 1 phút)**, ⛔ không phải app chậm. PASS vì thông báo **đã có sẵn** ngay lần xem đầu + fragment ghi *"đo tay có sai số"*. 🔁 **Đề nghị đo lại bằng 2 thiết bị.**
- 🔑 **Màn ĐĂNG NHẬP FoxPro lần đầu được harvest** → merge `locators/vibe-locators-latest.md` (**34/34 = 100%**). Đây là thứ **mở khoá nhóm TC đa-tài-khoản của MỌI module**, ⛔ không riêng ASN. Luồng 5 bước: `04_test-data/valid/USR-accounts.md §0b`.
- 📨 **2 đề nghị sửa tài liệu:** `TC-ASN-021` Steps ghi loại hàng **`"Giấy tờ, hồ sơ"`** — nhãn **không tồn tại** (`C-ORD-09` chốt `Tài liệu`) · `TC-ASN-v1.1.md §0` ghi QA-obs buổi *"Sáng (6–12h)"*, app thật **`Sáng (8–12h)`**.
- ℹ️ **OFFER ≠ NEED ở 2 chỗ dễ sập automation:** checkbox điều khoản OFFER **không có** `resourceId` (NEED có `post-n3-consent-checkbox`) · màn thành công khác chuỗi (`Đã ghi nhận tuyến đường!` ⟷ `Đăng tin thành công!`). OFFER cũng **không lên Bảng tin** (*"không hiển thị công khai"*).
- 🗂️ **Dữ liệu phát sinh:** tạo **1 OFFER + 2 NEED** bằng `stag_taipm@`; cộng 2 tin của `stag_anhdc4@` lúc 08:26–08:38 ⇒ **5 tin sống trên STG**. ⛔ Lô sau **đừng seed lại** — bảng chi tiết ở `coverage-ASN.md §Tổng hợp`.
- 🛑 **Dừng vì HẾT SỨC PHIÊN**, ⛔ không phải hết TC. **21 TC còn nợ nay là NỢ CÔNG SỨC**: **18 TC chạy được ngay** với dữ liệu + tài khoản hiện có; chỉ `006`/`008` (cần 2–3 thiết bị) và `019` (cần dev lùi ngày) còn chặn thật.
- ⚠️ **`stag_taipm@` = Phan Minh Tài, MNV `00041796` = `FOXECO_STG_USER_C`** ⇒ chạy `TC-USR-040/043` **TRƯỚC** khi làm bẩn hồ sơ tài khoản này.

> 🔴 **CẢNH BÁO TRÙNG TÊN `VR-002`:** nhãn `VR-002` trong `KP-01 §10.2/§10.3` (`KB-VIBE-01`/`KB-VIBE-02`, `TC_04.5`/`TC_04.6`) là run của **đợt v1.0 CŨ**, **KHÔNG** phải phiên `VR-002-ORD-2026-09-18` ở bảng trên. Hai hệ đánh số độc lập — đọc tài liệu cũ thì đối chiếu theo **ngày**, không theo mã VR.

---

## VR-009 — module **ASN** — 2026-09-19 (mobile · `stag_anhdc4@` ↔ `stag_giangdc2@`)

| | |
|---|---|
| Run folder | `08_test-runs/vibe/VR-009-ASN-2026-09-19/` |
| Sổ cái module | `08_test-runs/vibe/coverage/coverage-ASN.md` |
| Scope / kết quả | **26 TC** · chạy **7** · **7 PASS / 0 FAIL / 0 BLOCKED** · evidence **7/7** · **còn nợ 9** |
| Module sau phiên | **17/26 có verdict cuối** (trước phiên: 10/26) |
| Gate | rule-1 **7/7 sạch** · exit 1 **chỉ vì còn nợ coverage** ⇒ §8 = **PARTIAL** (đúng nhóm B của `execute.md §6.5`) |

- 🟢 **7 TC / 7 PASS:** lô 1 `005` · `007` · `020` *(không cần seed — tái dùng đơn `Đã ghép` của VR-008)* · lô 2 `010` · `011` · `012` · `022` *(seed mới)*. **`TC-ASN-020` chốt verdict cuối** sau khi VR-008 mới chạy được step 1–5 — phiên này chạy nốt step 6–9 bằng **Carrier thứ 3** `stag_giangdc2@`.
- 🔴 **PHÁT HIỆN LỚN NHẤT — thông báo khớp tuyến BIẾN MẤT khi khung giờ trôi qua** *(giả thuyết, chưa chốt)*: 14:49 chuông của B có **3** thông báo khớp tuyến (đều thuộc các tin buổi `Sáng`); sau đó nhóm `HÔM NAY` **rỗng**, **`force-stop` + relaunch vẫn rỗng** ⇒ ⛔ không phải lỗi refresh client (`T-ASN-04`). ⇒ **`010`/`011`/`012`/`022` KHÔNG thể chạy trên seed cũ** — phải seed lại trên khung giờ **CÒN MỞ**.
- 🧪 **Bài học phương pháp (quan trọng hơn cả verdict):** 3 TC âm (`011`/`012`/`022`) mà kết luận từ bề mặt *"chuông không có thông báo"* lúc 14:49 thì **đều "PASS" một cách vô nghĩa**, vì lúc đó **mọi** thông báo đều đã mất — kể cả của tin khớp ĐỦ. ⇒ Phiên này seed **1 OFFER + 4 NEED**, trong đó **N1 khớp đủ làm CHỨNG CỨ DƯƠNG đối chứng**; chỉ khi N1 **thật sự sinh** thông báo thì việc N2/N3/N4 **không** sinh mới có giá trị.
- 🔑 **Kỹ thuật ĐẾM thông báo bằng `.instance(N)`** — dò `textContains("Tìm thấy đơn hàng phù hợp tuyến của bạn — xem chi tiết").instance(k)` tăng dần tới khi NOT_FOUND ⇒ số thông báo = k. ⛔ Không cần dump page source. **Đây là chìa khoá cho nhóm trần `014/015/016/017/025` còn nợ.**
- 🔴 **ĐÍNH CHÍNH `vibe-locators-latest.md` (merge VR-008):** mẹo *"ghi mã `SEED Sx` vào ô GHI CHÚ rồi assert trên Chi tiết tin"* **KHÔNG dùng được** — `appium_get_page_source` đầy đủ cho thấy màn `Chi tiết tin` **không render mục GHI CHÚ**. ✅ Oracle thay thế đã kiểm chứng: **tuổi tin ở header** (`19 phút trước`) + **màu ảnh seed**, và **chữ ký `tuyến + khung giờ`** trên card Bảng tin để tách các tin trùng nhau.
- 📨 **Đề nghị sửa tài liệu:** `TC-ASN-010` Steps ghi nút **`"Nhận giao"`** — **không tồn tại** (find phủ định 🚫 NOT FOUND), CTA thật là `Tôi mang giúp được` · `TC-ASN-012` mô tả giờ `08:00–09:00` vs `20:00–21:00` nhưng app dùng **khoảng NGÀY + tập BUỔI** · nhãn buổi `Sáng (8–12h)` (**lần thứ 3** xác nhận).
- 🐛 **`BUG-008` cần thu hẹp phạm vi:** autofill SĐT người nhận **đúng/sai tuỳ tài khoản** — `stag_huyennhk@` autofill **ĐÚNG** `0989014863`, trong khi VR-008 ghi `stag_thuyntt22@` trả **MNV**. ⇒ ⛔ không phải lỗi toàn cục mà phụ thuộc **HRIS có SĐT hay không**.
- 🪤 **Bẫy mới:** `T-ASN-07` nút `NHẬN MÃ OTP` có thể trả *"Không thể kết nối mạng!"* **giả** ở lần bấm đầu (ping emulator 0% loss) → **retry 1 lần** · `T-ASN-08` autofill SĐT tuỳ tài khoản · `T-ASN-09` thông báo hết hiệu lực theo khung giờ.
- 🗂️ **Dữ liệu phát sinh trên STG:** **1 OFFER + 4 NEED** mới (`OFFER-C1` + `N1..N4`, khung **Chiều**) bằng `stag_giangdc2@` và `stag_anhdc4@`; **2 tin bị ghép thêm** (`TC-ASN-020` Tin 1 → carrier `stag_giangdc2@`; `TC-ASN-010` N1 → carrier `stag_giangdc2@`). ⛔ Phiên sau **đừng seed lại** — chi tiết ở `coverage-ASN.md` + `04_test-data/valid/USR-accounts.md §3`.
- 🛑 **Dừng vì HẾT SỨC PHIÊN** (15:46), ⛔ không phải hết TC. Còn nợ **9**: **6 TC nhóm trần/thứ tự** (`014`–`018`, `025`) cần **tuyến OFFER MỚI sạch + 3–6 NEED + 3 lượt đổi tài khoản** (~50–60 phút) mà khung `Chiều` đóng **17:00** ⇒ chạy dở sẽ nhiễm bẩn số đếm; **`006`/`008`** cần 2–3 thiết bị (**QC chốt trong phiên: giữ NOT_RUN**); **`019`** cần dev lùi ngày.
- 🧭 **Khuyến nghị phiên sau:** bắt đầu **đầu khung giờ** (13:05 / 08:05) · **⛔ KHÔNG tái dùng `OFFER-C1`** (đã dính 1 thông báo của tin đã ghép — mà **tin đã ghép VẪN chiếm slot**, quan sát 15:46) · chuỗi seed tiết kiệm: 3 NEED → đếm (`015`) → +2 → đếm (`016`) → +1 → đếm (`017`+`014`). Chi tiết ở `VR-009-…/vibe-report.md §Khuyến nghị thiết kế`.


## VR-010 — module **ASN** — 2026-09-19 18:45 (mobile · 4 tài khoản, 7 lượt đổi)

| | |
|---|---|
| Run folder | `08_test-runs/vibe/VR-010-ASN-2026-09-19/` |
| Tập chạy | **7 TC pending** — `014` `015` `016` `017` `018` `019` `025` |
| Kết quả | **5 PASS / 2 FAIL** · evidence **7/7** · gate: 0 vi phạm *(exit 1 chỉ vì còn 2 TC NOT_RUN)* |
| Coverage ASN | **17/26 → 24/26** · còn nợ **2** |

- 🔴 **PHÁT HIỆN LỚN NHẤT — trần 5 thông báo khớp tuyến bị áp theo TÀI KHOẢN, không theo TUYẾN.** `TC-ASN-016` ❌ (5 tin NEED khớp → chỉ 4 thông báo) và `TC-ASN-025` ❌ (tuyến OFFER **thứ hai**, còn trống 5/5 slot, vẫn **không** nhận thông báo nào). Đúng rủi ro BA lường trước ở `C-ASN-04(e)`. **Chuỗi số đo 4 mốc, đo 2 lần cách 5 phút ⇒ loại trừ "đến chậm"** *(tin đã 2–13 phút ≫ `NFR-04` 60s)*. ⇒ **cần `/log-bug`** *(chưa log trong phiên này)*.
- ⚠️ **2 ca PASS phải đọc kèm cảnh báo:** `TC-ASN-014` (assertion `≤5` thoả nhưng **cận trên chưa bị chạm**) và `TC-ASN-017` (quan sát đúng expected nhưng **tiền đề "tuyến đủ 5" chưa đạt**) — cả hai **không có khả năng phân biệt** app đúng/sai chừng nào lỗi trần còn đó ⇒ **chạy lại sau khi fix**.
- 🟢 **`TC-ASN-019` gỡ được mà KHÔNG cần dev:** Steps ghi *"nhờ dev/QA seed tin hết hạn"* + Test Data ghi *"⛔ không seed được qua UI"* — **đã lỗi thời**. STG tự sinh tin `Hết hạn` và `Đơn của tôi → Đã hoàn thành` cho biết chính xác tin nào. Phép thử có **đối chứng dương nằm sẵn bên trong** (2 thông báo trỏ tin còn sống, 0 thông báo cho tin hết hạn).
- 🆕 **Cơ chế mới phát hiện:** đăng OFFER mới ⇒ hệ thống **bắn thông báo HỒI TỐ** cho tin NEED **đã có sẵn** khớp tuyến (chuông từ 0 → 2 trong ~2 phút). ⇒ chưa có trong `scenario_map`, cần `/analyze-requirements --update`.
- 🪤 **4 bẫy mới, 2 trong đó ĐÍNH CHÍNH ghi chép cũ:**
  · `T-ASN-10` — **`.instance(N)` KHÔNG đếm được list dài** (chỉ thấy node đang render ~4 mục). 🔴 Ghi đè khuyến nghị nổi bật của VR-009 (*"chìa khoá cho nhóm trần"*). ✅ Cách đúng: dump page source **nhiều vị trí cuộn** → ghép theo nhãn tuổi.
  · `T-ASN-11` — **thông báo biến mất sau khi MỞ** (`stag_taipm@` 2→1→0), nhưng **không** xảy ra ở `stag_giangdc2@` ⇒ **đếm TRƯỚC khi mở**. Nhiều khả năng đây là lời giải thật cho `T-ASN-09`.
  · `T-ASN-12` — **`stag_huyennhk@` KHÔNG có icon FoxEco** ⇒ chỉ làm được vai **người nhận**; màn `Cá nhân` của nó cũng **không render** `Đăng xuất` ⇒ phải `adb shell pm clear` để thoát *(đã làm, không mất dữ liệu STG)*.
  · `T-ASN-13` *(đính chính)* — **màn Chi tiết tin CÓ mục `Ghi chú`** (chỉ render khi khác rỗng). 🔴 Ngược với VR-009. ✅ **Mã seed ở ô Ghi chú = oracle định danh MẠNH NHẤT**.
- 🧪 **Thiết kế phiên:** buổi **`Giờ nào cũng được`** cho *mọi* seed — cố ý, để tin không bị đóng khi khung giờ trôi qua (bài học `T-ASN-09`); nhờ đó chạy thông suốt 16:29 → 18:45 xuyên 2 khung giờ. Đổi chủ tin OFFER sang `stag_taipm@` (chuông 0/5 slot) cho `018`/`019` vì `stag_giangdc2@` đã dính trần.
- 🗂️ **Dữ liệu phát sinh trên STG:** **4 OFFER** (`R1`,`R2` của `stag_giangdc2@`; `R3`,`R4` của `stag_taipm@`) + **9 NEED** của `stag_anhdc4@` (`R1-1..R1-6`, `R2-1`, `X lech tuyen`, `R3a`, `R3b`) — tất cả **Hôm nay · Giờ nào cũng được**, **mã seed cắm ở ô GHI CHÚ**. ⛔ Phiên sau đừng seed lại; chi tiết ở `coverage-ASN.md §Dữ liệu VR-010`.
- 🛑 **Dừng vì HẾT TC trong tập chạy**, ⛔ không phải hết sức phiên. 2 TC còn nợ (`006` 2 máy · `008` 3 máy) là **QC chủ động để lại** (16:30: *"2 emulator thôi nhé, case nào cần 2 emulator thì để lại giúp t"*).
- 🧭 **Khuyến nghị phiên sau:** (1) `/log-bug` lỗi trần trước tiên; (2) sau khi DEV fix → chạy lại **`014` `016` `017` `025`** như một cụm (cùng 1 tuyến sạch + 6 NEED); (3) `/analyze-requirements --update` cho 2 hành vi chưa có trong scenario_map (thông báo hồi tố · thông báo biến mất sau khi mở).

---

## VR-011 — GIFT — 2026-09-19 — **lần đầu vibe-test module GIFT**

- 📋 **Scope 14 TC = HỢP của 2 file TC-MASTER** (v1.1 `Quà cảm ơn` 8 TC ∪ v1.0 6 TC chỉ có ở v1.0: `001/004/005/009/010/012`). ⚠️ Chỉ đọc v1.1 sẽ **sót 6 TC**.
- ✅ **11/14 có verdict cuối trong 1 phiên** — **8 PASS · 1 FAIL · 2 BLOCKED** (+ 1 ⚠️ NOT_EVIDENCED) *(♻️ 2026-09-21: `TC-GIFT-012` FAIL→PASS theo QC chốt; `TC-GIFT-003` đã log FE-308)*. Dừng vì **hết tiền đề dữ liệu**, ⛔ không phải hết sức phiên.
- 🔁 **ĐÍNH CHÍNH TRONG PHIÊN — `TC-GIFT-001` + `TC-GIFT-010` đổi ❌ FAIL → ✅ PASS.** Lúc chạy bị chấm FAIL vì luồng app khác chữ trong TC; đối chiếu **tài liệu phân tích của chính dự án** thì chấm vậy là **sai quy kết**:
  · `SC-GIFT-001` **Then** = *"Mở màn "Tặng quà" với 4 lựa chọn quà"* → app **đạt**; `C-GIFT-04` **Resolved 2026-09-17** chốt app route **theo trạng thái tặng quà** (chưa tặng → "Tặng quà" · đã tặng → "Theo dõi đơn").
  · `SC-GIFT-010` **Then** = *"Về đúng màn trước đó **(Theo dõi đơn / Đơn của tôi)**"* → app về `Đơn của tôi` **nằm trong tập chấp nhận**; `C-GIFT-02` **Resolved 2026-09-16**: rule = *"back về màn hình trước đó"*.
  ⇒ Phần lệch còn lại là **chữ trong TC đã lỗi thời** ⇒ **sửa TC**, ⛔ không log bug.
- 🧾 **Cái giá của việc đính chính — `TC-GIFT-010` xuống ⚠️ NOT_EVIDENCED:** ảnh của nó chụp lúc đang chấm FAIL (slot `__step4-FAIL`), đổi verdict xong thì **không còn file `__verify*`**. Luật cấm đổi tên/copy ảnh cho khớp gate, mà **chụp lại bất khả thi**: STG đã **hết sạch** đơn Hoàn thành chưa tặng quà *(kiểm đủ 4 tài khoản vào được FoxEco)*. ⇒ TC ở lại danh sách nợ, `/vibe-test --tc TC-GIFT-010`. **Kết luận nội dung vẫn dùng được** cho `/analyze-requirements` — chỉ không tính PASS.
- 🔗 **2 FAIL còn lại — cả hai CHỜ BA CHỐT trước khi `/log-bug`:**
  · **G2** *(→ `TC-GIFT-012`)* — thông báo `NTF-07` viết *"mở Trang cá nhân để xem"* nhưng deep-link mở **"Quà đã nhận"**: app tự mâu thuẫn với chính câu chữ của nó.
  · **G3** *(→ `TC-GIFT-003`)* — popup gửi quà còn chuỗi **v1.0** `"Đã gửi lời cảm ơn!"` thay vì chuỗi `BR14-02`.
- 🔴 **1 spec-gap TÁCH RIÊNG, ⛔ không gắn với TC nào FAIL:** nút `"✓ Cảm ơn người vận chuyển"` mà `KB-GIFT-01` (ô 5·Sender) **và When của `SC-GIFT-001`** mô tả **KHÔNG tồn tại trên app** ⇒ sửa 2 chỗ đó cho khớp `C-GIFT-04` → `/analyze-requirements --update`.
- 🔑 **`RISK-GIFT-05` / `C-GIFT-02` — đề nghị HẠ/ĐÓNG:** hành vi `KB-GIFT-04` (*back nhảy sang màn "Xác nhận đã nhận hàng" của **đơn khác***) **KHÔNG tái hiện** qua **2 lượt thử trên đơn thật**; back về đúng màn đã mở "Tặng quà".
- 🔑 **Đóng `C-GIFT-03` vế (b):** màn "Quà đã nhận" **CÓ** khối `LỊCH SỬ NHẬN QUÀ` (loại quà · người gửi · ngày giờ), số dòng khớp số quà ⇒ `AC-26.1.01` được đáp ứng. v1.0 dự kiến FAIL vế này.
- 🔑 **`KB-GIFT-03` có bằng chứng thực nghiệm 3 tài khoản** (trước nay chỉ là suy diễn, không nguồn PRD): loại quà count = 0 **bị ẩn** (`taipm` 1/4 ô · `anhptm17` 2/4 ô) và **hiện đủ khi > 0** (`giangdc2` 4/4 ô, tổng khớp `3+3+4+3=13`). ⇒ đề nghị BA đưa vào tài liệu.
- 🔒 **2 BLOCKED (`013`/`014`) do STG chưa build `FR09`** — thanh trạng thái đơn chỉ **5 bước**, ⛔ không có nhánh `RETURNING`/`RESCHEDULED`/`RETURNED`; hành động duy nhất của Người gửi ở đơn `Đã ghép` là `Huỷ đơn`. Chạy lại **cùng lô** `TC-DLV-053..056` sau khi dev build.
- 🔴 **Dữ liệu test — `stag_anhptm17@` KHÔNG còn sạch:** = **Phan Thị Mỹ Anh**, MNV `00287493`, **5 đơn đã giúp / 5 quà đã nhận**. `USR-accounts.md §2` vẫn đang giữ nó làm *"dự phòng / tài khoản sạch"* ⇒ ghi chép đó **sai**, đã đính chính. ⇒ **STG không còn tài khoản trắng nào** — chặn cụm empty state của **GIFT `008` · ACT `SEED-ACT-02` · HOME `SEED-HOME-01`**.
- 🪤 **4 bẫy kỹ thuật mới (`T18`–`T21`)**, đã gộp vào `locators/vibe-locators-latest.md`:
  · `T18` — `resource-id` màn "Tặng quà" **không kèm package** ⇒ strategy `id` luôn NOT FOUND; dùng `accessibility id` hoặc `resourceIdMatches`.
  · `T19` — **popup cảm ơn không đóng được bằng `back`** (back chỉ pop màn nền, popup vẫn nổi) ⇒ bắt buộc tap `text("Về trang chủ")`; `accessibility id` **không** khớp nút này.
  · `T20` — danh sách "Đã hoàn thành" **không cuộn ngược** bằng `scroll(up)`/`swipe(down)` (báo success nhưng không đổi) ⇒ phải **swipe toạ độ tường minh**.
  · `T21` — trạng thái **disable** không đọc được qua `get_element_attribute(enabled)` (TextView luôn `true`) ⇒ kiểm bằng **vắng mặt tổ tiên clickable** (`xpath ancestor::*[@clickable="true"]`).
- ⚡ **Ngân sách context:** **2 snapshot / 7 màn harvest** — toàn bộ 12 TC của Pha B chạy **0 snapshot** (thuần `find_element` từ `locator_map`). Đúng luật B1/B2.
- 🗂️ **Dữ liệu phát sinh trên STG:** **2 quà đã gửi** từ `stag_taipm@` → `stag_giangdc2@` (`Bông hoa` 20:33 · `Ly cà phê` 20:37). ⇒ `stag_taipm@` **hết sạch** đơn Hoàn thành chưa tặng quà; `stag_giangdc2@` lên **13 quà**.
- 🧭 **Khuyến nghị phiên sau:** (1) `/analyze-requirements --update` cho **5 surface** chưa có trong `scenario_map` (xem `vibe-report.md §Phát hiện ngoài phạm vi TC`); (2) BA chốt **G2** + **G3** trước khi `/log-bug`; (3) xin dev **1 account trắng dùng chung** cho GIFT `008` + ACT + HOME; (4) nếu BA bỏ ràng buộc **tên loại quà** ở `SEED-GIFT-05` thì `TC-GIFT-006` chạy lại được ngay bằng `stag_anhptm17@`.

## VR-012 — module **DLV** — 2026-09-19 22:15 (mobile · 1 tài khoản, **0 lượt đổi**)

> 🚫 **PHIÊN DỪNG VÌ BLOCKER QUYỀN, ⛔ KHÔNG PHẢI HẾT SỨC VÀ KHÔNG PHẢI APP LỖI.** Lúc **22:15**, `tap` nút `Đã giao cho người nhận` bị **auto-mode classifier** từ chối: `Reason: [Modify Shared Resources]` — vì thao tác đẩy trạng thái thật của đơn trên STG.
> **15 TC chạy / 13 PASS / 2 FAIL**, coverage DLV **0/81 → 19/81** (13P + 2F + 4 N-A), còn nợ **62** *(55 trong số đó chặn trực tiếp bởi blocker)*.
> ▶️ **Muốn chạy tiếp phải để user gỡ quyền trước** — chi tiết + bảng "nhóm thao tác bị chặn ↔ nhóm TC" ở `VR-012-DLV-2026-09-19/vibe-report.md §BLOCKER`.
>
> 🔑 **Chìa khoá mở được 15 TC mà 0 lần đổi tài khoản:** tài khoản `stag_anhdc4@` tình cờ có sẵn đơn ở **đủ 3 vai × 5 trạng thái** ⇒ cả ma trận nhãn `TC-DLV-001..015` đọc được từ **một** tài khoản. Bài học dùng lại: **trước khi seed, hãy kiểm kê tồn kho đơn của tài khoản đang đăng nhập** (dump `content-desc` ở nhiều vị trí cuộn) — rẻ hơn nhiều so với dựng đơn mới.
> 🔑 **Oracle "nhãn khoá vs nút thật"** (dùng chung cho cả nhóm `001–015`): nhãn khoá = băng `clickable=false` + **không** `resource-id`/`content-desc`; nút thật = `ViewGroup clickable=true` + **có** `content-desc`. ⛔ **KHÔNG dùng `enabled`** — đo được `true` trên **cả hai** (bẫy `T4`, tái xác nhận lần 5).
> 🪤 **4 bẫy mới `T-DLV-01..04`** — 2 bẫy **đã thực sự làm hỏng thao tác trong phiên**: **bản đồ Google nuốt gesture cuộn**, và **`scroll_to_element` dừng khi card mới chạm mép dưới** ⇒ card cao 5px nằm dưới FAB ⇒ `tap` **trúng nút `Đăng tin`** (dính 2 lần). ✅ Cách chắc: `get_attribute("bounds")` trước khi tap; cuộn quá rồi `scroll_to_element` **ngược lên**.
> ⚡ **`appium_get_page_source` của app này ~135–252k ký tự ⇒ MCP tự ghi RA FILE, không vào context** (`T-DLV-03`) ⇒ dump page source **gần như miễn phí**; `grep` bằng script. 🔴 Điều này **đổi hẳn cách tính chi phí** so với VR-008/009 — cột `Snapshot?` không còn là đồng hồ đo context.
> 📌 **4 việc cho QC/BA:** (1) 🔴 **người nhận MẤT cụm liên hệ ở `Đang giao`** — có ở `Đã ghép`, có lại ở `Đã giao`, **mất đúng khoảng giữa**; chưa SC nào phủ ⇒ `/analyze-requirements --update`; (2) 🐛 icon copy **không đổi màu** (`080`+`081`) — **cùng lỗi gốc `TC-ORD-085`/VR-004**, mở **1 bug component**; (3) ⚠️ **`TC-DLV-017/018/019` (CARRIED v1.0) có thể đã LỖI THỜI** — chúng tả popup 2 nút, còn v1.1 (`043`–`053`) tả **cả một màn "Xác nhận đã giao"** cho **cùng một nút**; phiên sau FAIL ở đây thì ⛔ **đừng log bug**, route về `review-tc`; (4) **4 TC P1 (`074`–`076`, `078`) là API-tier** — đánh `⛔ N-A` ở tier vibe, cần chạy ở tier security/API.

## VR-013 — module **ORD** — 2026-09-21 (mobile · 2 thiết bị song song: emulator=Giang, máy thật=Anh)

> **Retest theo chỉ định QC:** 22 TC còn nợ + `TC-ORD-004` (`BUG-020`) + `TC-ORD-068` (`BUG-019`). **21 TC chạy: 20 PASS · 0 FAIL · 1 BLOCKED (`084`)** *(đính chính 2026-09-21: `073` lightbox chạm nền · `088` xoá được ảnh tin đã đăng — ban đầu FAIL, QC xác nhận app đúng ⇒ PASS, TC sửa theo app; `BUG-023/024` đã huỷ)*. Coverage ORD **66/88 → 85/88**, còn nợ **3** (`067` `080` `082`) — §8 = PARTIAL. Dừng theo yêu cầu QC (sắp hết hạn mức).
> 🔑 **`BUG-020` KHÔNG tái hiện** (cùng Giang, cùng payload, đăng được ban ngày ⇒ còn giả thuyết lệch ngày nửa đêm) · **`BUG-019` KHÔNG tái hiện** (5 MiB được nhận; >5 MiB có thông báo nhưng **nằm dưới viewport**) ⇒ **đề nghị không push cả hai**.
> ✅ **`TC-ORD-085` xác nhận KHÔNG phải bug** (chip xanh `Đã copy` ~1,6–2,1 s, đo bằng burst screencap) ⇒ nghi `DLV-080/081` cùng âm tính giả.
> 📁 `VR-013-ORD-2026-09-21/vibe-report.md` (kết luận + việc cho QC) · sổ cái `coverage/coverage-ORD.md`.

> 📊 **Tiến độ chỉ TC v1.1:** `coverage/PROGRESS-v1.1.md` (dẫn xuất từ `TC-MASTER-v1.1` + sổ coverage; sổ từng module vẫn giữ mẫu số gồm CARRIED v1.0).

## VR-014 — module **HOME** — 2026-09-21 (mobile · emulator · chỉ TC v1.1)

> **`/vibe-test --module Home` chỉ TC v1.1 đang nợ (9 TC).** Chạy **5**: **2 PASS** (`019` `021`) · **2 FAIL** (`025` nút `Xem thêm` hiện khi đúng 5 tin · `027` empty state `Đơn của tôi` sai `EMP-02`) · **1 BLOCKED** (`028` STG không thể về 0 đơn). Giữ nợ **4** (`008 029 030 031`) vì QC không cho ghép đơn / vòng giao–nhận. **v1.1 HOME: 2/11 → 7/11 có verdict (64%).** Coverage HOME 17→22/32, nợ 10 (6 trong đó là CARRIED v1.0 ngoài phạm vi).
> 🔑 Tài khoản "sạch" nay có: `stag_thuyntt22@` (0 đơn · 0 đóng góp) — `USR-accounts.md §2` cần đính chính. STG bị người khác thao tác song song (tin lạ giữa phiên).
> 📁 `VR-014-HOME-2026-09-21/vibe-report.md`

## VR-016 — module **FEED** — 2026-09-21 (mobile · emulator · chỉ TC v1.1)

> **`/vibe-test --module feed` chỉ TC thuộc v1.1 theo yêu cầu QC** (`TC-FEED-002/007/009/013/015` — 5/15 TC của module; 10 TC carried v1.0 chưa từng vibe-test, ngoài phạm vi phiên này). Kết quả ban đầu: **1 PASS · 2 FAIL · 2 BLOCKED**.
> 🔁 **Retest cùng ngày:** QC cấp 2 địa chỉ cụ thể có toạ độ hợp lệ → tự tạo 1 tin NEED → `TC-FEED-009` BLOCKED → **✅ PASS** (bản đồ Google Maps thật + "17.2 km · 15 phút"). Phát hiện kèm: `location_address_catalog.xlsx` không đáng tin làm oracle (100% dòng gắn `MISSING` kể cả toạ độ hợp lệ) ⇒ đính chính `TC-FEED-007` **không cùng root cause** với `TC-FEED-015` như ghi nhận lúc đầu — `007` nghi do chọn nhầm data (chưa log bug).
> ✅ **QC review `BUG-029` (`TC-FEED-015`) cùng ngày — chấp nhận hành vi hiện tại, không phải bug.** Expected Result sửa lại theo app (fragment + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`), verdict FAIL → **PASS**, `BUG-029` rút khỏi `draft/`, không push Jira.
> ✅ **Retest `TC-FEED-007` cùng ngày (QC yêu cầu):** đăng xuất → đăng nhập `stag_anhdc4@fpt.com` → mở tin của Giang (data hợp lệ) → **PASS đủ 4/4 sub-clause**, xác nhận FAIL lần 1 chỉ do chọn nhầm data. 🔍 Phát hiện kèm: CTA "Tôi mang giúp được" vắng mặt **chọn lọc theo tin** (2/3 tin khác vẫn có CTA, chỉ 1 tin không) — khớp `OPR-05`/`SC-FEED-012`, không phải bug, data hữu ích cho `TC-FEED-012`.
> **Kết quả cuối: 4 PASS (`002`,`007`,`009`,`015`) / 0 FAIL / 1 BLOCKED (`013`)**. Coverage FEED: 0 → **5/15** có verdict — cả 4 TC chạy được đều PASS.
> 🔑 App đã đăng nhập sẵn (`stag_giangdc2@fpt.com`) từ đầu phiên; retest `009` cần tạo tin mới qua wizard Đăng tin; retest `007` cần đổi tài khoản qua FoxPro (FoxEco không có nút đăng xuất).
> 🎯 **Không còn case v1.1 nào cần hành động của QC** (`013` là case xác nhận BLOCKED, chờ dev/QA — không phải nợ kiểm thử).
> 📁 `VR-016-FEED-2026-09-21/vibe-report.md` · sổ cái `coverage/coverage-FEED.md`.

## VR-019 — module **TS** — 2026-09-22 (mobile · 2 thiết bị song song: emulator=Giang, máy thật=Tài → tạm Mỹ Anh → về Tài, chỉ TC v1.1)

> **`/vibe-test --module TS` chỉ 17 TC thuộc v1.1** (`TC-TS-008..024`; 7 TC CARRIED v1.0 ngoài phạm vi). Chạy hết **17/17**: **3 PASS** (`018` `022` `023`) · **1 FAIL** (`016`) · **13 BLOCKED**. Coverage TS: 0 → **17/17** có verdict — §8 = **COMPLETED**.
> 🐞 **Phát hiện 2 vấn đề chặn phần lớn scope:** `BUG-037` — nút "Báo cáo sự cố" mở WebView nhưng **luôn dừng ở màn đăng nhập Microsoft**, tái hiện 100% ở cả 3 vai (A/B/C) và mọi trạng thái đơn đã thử trên tài khoản test STG (`stag_*@fpt.com` không có danh tính Microsoft tương ứng) ⇒ chặn 12 TC. 🔁 **Dev phản hồi cùng ngày: nguyên nhân là form có trường tải file ⇒ Microsoft Forms bắt buộc đăng nhập (quy định nền tảng, không phải lỗi code)** — đổi từ P1/Critical sang **Suggestion P2**: đề xuất bỏ bắt buộc đăng nhập, vì đây là khảo sát nhanh và bắt đăng nhập dễ khiến người dùng bỏ dở. `BUG-038` (P2, bug thật) — mất mạng hiện trang lỗi Chromium kỹ thuật, không có nút "Thử lại" ⇒ FAIL `TC-TS-016` + BLOCKED `TC-TS-017`.
> 🔑 **Phát hiện quan trọng khi điều tra thêm:** trên thiết bị thật, WebView từng **auto-sign-in bằng 1 tài khoản Microsoft 365 THẬT đã cache sẵn ở cấp hệ điều hành** (không liên quan tài khoản FoxEco/STG đang dùng), lộ ra đúng **Microsoft Forms thật** phía sau — xác nhận giả thuyết `BUG-037` (form yêu cầu đăng nhập tổ chức) nhưng KHÔNG điền/gửi gì để tránh dùng danh tính thật; đồng thời gợi ý 1 vấn đề thiết kế độc lập: form dường như không xác thực người gửi khớp với tài khoản/đơn hàng trong app. Chi tiết đầy đủ: `VR-019-TS-2026-09-22/vibe-log.md` mục "⚠️ Phát hiện quan trọng".
> ✅ **3 TC PASS không phụ thuộc nội dung form** (chỉ cần nút hiện+nhấn được hoặc hành vi đóng WebView): `TC-TS-018` (đóng WebView quay đúng màn), `TC-TS-022` (nút hiện đủ 3 trạng thái, vai người gửi), `TC-TS-023` (nút hiện đủ 2 trạng thái, vai vận chuyển).
> 🎯 **13 BLOCKED không phải nợ kiểm thử.** 12 TC chờ BA/Dev chốt hướng xử lý `BUG-037` (Suggestion), `TC-TS-017` chờ fix `BUG-038`. Retest sau khi có hướng: `/vibe-test --retest TC-TS-008,009,010,011,012,013,014,015,016,017,019,020,021,024`.
> 📁 `VR-019-TS-2026-09-22/vibe-report.md` · sổ cái `coverage/coverage-TS.md` · bug draft `05_bug-reports/draft/BUG-037-*.md` + `BUG-038-*.md`.
>
> 🆕 **Follow-up 2026-09-22 (cùng ngày, cùng folder):** QC tự đăng nhập tài khoản Microsoft **thật**
> trên thiết bị thật, yêu cầu retest 12 TC bị chặn ở màn login. **Bypass thành công** — 12 TC đảo
> verdict thành 9 PASS / 3 FAIL. 🔁 **Hiệu chỉnh cùng ngày sau khi log bug:** `TC-TS-010`/`011` FAIL
> vì giả định "nút Gửi disable" sai — QC xác nhận không phải bug (`BUG-040` xoá), sửa Expected theo
> hành vi thật (inline error) ⇒ đảo tiếp **FAIL → PASS**. Kết quả CUỐI CÙNG module TS: **11 PASS · 5
> FAIL · 1 BLOCKED** (`TC-TS-017`, chờ `BUG-038`, không liên quan màn login). 🔴 3 phát hiện đảo
> ngược clarification "Resolved" trước đó (`C-TS-03(b)` mã đơn hàng sửa được · `C-TS-03(d)` màn xác
> nhận là mặc định MS Forms · giả định ảnh không bắt buộc) — cần `/analyze-requirements --update`.
> Đã log 4 bug mới (`BUG-039/041/042/043`, draft, chưa push Jira). Chi tiết:
> `VR-019-TS-2026-09-22/vibe-log.md` §"🆕 Follow-up 2026-09-22" · coverage đã cập nhật ở
> `coverage/coverage-TS.md`.

## VR-020 — module **DLV** — 2026-09-22 (mobile · thiết bị thật `R58T20PLP8K`, chỉ TC v1.1 còn nợ)

> ⚠️ **Phiên dừng SỚM theo yêu cầu user** (lo hết token giữa chừng) — chỉ seed 4 đơn mới
> (`SEED-DLV-VR020-01..04`, A `giangdc2`→C `taipm`, carrier B `anhptm17`) rồi phát hiện **BLOCKER lớn**:
> form "Xác nhận đã giao" mở rộng (FR07, 4 loại đối tượng nhận) mà PRD v1.1 giả định **không tồn tại**
> trên STG — bấm nút chính ra thẳng popup đơn giản y hệt v1.0. Kiểm chéo 2 đơn độc lập, cùng kết quả.
> Chạy `TC-DLV-043` tới verdict `🚫 BLOCKED` (evidence đầy đủ). 13 TC khác cùng nhóm (`TC-DLV-044..053`,
> `069..071`) nhiều khả năng cũng BLOCKED vì cùng nguyên nhân nhưng **giữ `NOT_RUN`** — chưa verify riêng
> từng TC, không tự nhận verdict thiếu evidence (mâu thuẫn với `RISK-DLV-08`/`TC-CNL-018` cần QC đối
> chiếu trước, không log bug mới). Thu thêm 1 ảnh evidence mới củng cố `BUG-044`.
> Coverage DLV: 19/81 → **20/81 có verdict**, còn nợ 61. 4 đơn seed còn sống, dùng tiếp được ở phiên sau
> (2/4 cần soát lại trạng thái trước) — xem `coverage/coverage-DLV.md` §"4 đơn seed còn sống".
> 📁 `VR-020-DLV-2026-09-22/vibe-report.md`.

## VR-021 — module **DLV** — 2026-09-22 (mobile · thiết bị thật `R58T20PLP8K`, tiếp nối VR-020, chỉ TC v1.1 còn nợ)

> 🔴 **ĐÍNH CHÍNH 2026-09-22 (QC chỉ ra trực tiếp, follow-up cùng ngày):** verdict `🚫 BLOCKED` ban đầu
> của `TC-DLV-043` (VR-020) và `TC-DLV-050` (VR-021) đều **SAI**. Nguyên nhân: cả 2 lần test dừng ở
> popup quick-confirm lớp 1 ("Bạn xác nhận đã giao hàng...?") rồi bấm **Huỷ** để giữ đơn, chưa từng bấm
> **Xác nhận** để thấy màn đầy đủ **"Xác nhận đã giao"** — form FR07 (GIAO CHO 4 lựa chọn + ảnh bắt
> buộc) **và** link "Không thể liên lạc cho người nhận?" đều nằm ngay ở màn này, **CÓ tồn tại trên
> STG**. Retest thật: `TC-DLV-043` **✅ PASS** (giao "Người nhận", log đúng mẫu câu), `TC-DLV-050`
> **✅ PASS** (bottom sheet 2 lựa chọn đúng thứ tự spec). ⇒ **~40 TC family `044..053`/`069..071`/
> `031..039`/`051..056`/`058..067`/`072..073` không còn nghi cascade** — vẫn `NOT_RUN` (chưa test
> thật) nhưng KHÔNG còn bị chặn bởi build, chạy pending bình thường ở phiên sau.
> `TC-DLV-041`/`042` (luồng "Tôi đã lấy hàng") → cả 2 **✅ PASS** — đính chính `RISK-DLV-11`: ô ảnh
> bằng chứng lúc lấy hàng CÓ tồn tại (ở lớp popup thứ 2 "Xác nhận đã lấy hàng", trước đây chưa harvest kỹ).
> **Bài học chung:** nút hành động chính trên Theo dõi đơn luôn có ≥2 lớp popup — bấm Huỷ ở lớp 1 để
> giữ đơn không được dùng để kết luận BLOCKED, phải bấm Xác nhận đi tiếp ít nhất 1 lần (dùng đơn phụ).
> Coverage DLV: 20/81 → **23/81 có verdict**, còn nợ 58 (không còn nghi blocker build).
> 📁 `VR-021-DLV-2026-09-22/vibe-report.md`.

## VR-027 — module **DLV** — 2026-09-23 (mobile · emulator-5554 · RETEST bug In review)

> Retest 5 bug Jira DLV đang In review (carrier `stag_anhptm17@`), chỉ comment + đính kèm ảnh, **không đổi trạng thái**.
> ✅ **FE-327** (nút "Đã đến địa điểm giao hàng", vào thẳng form) · ✅ **FE-334** (validate SĐT ở 3 lựa chọn) ·
> ❌ **FE-331** / ❌ **FE-338** (Hẹn giao lại: lịch sử, nút, block vẫn sai, kể cả với lịch hẹn mới tạo) ·
> ❌ **FE-337** (Đang hoàn hàng: nút đã có, lịch sử vẫn sai). Ngoài phạm vi: Quầy bảo vệ nhận SĐT trống; màn không tự refresh sau khi xử lý.
> 📁 `VR-027-DLV-2026-09-23/vibe-report.md`.
