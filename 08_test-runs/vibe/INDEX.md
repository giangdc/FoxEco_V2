# INDEX — mọi phiên vibe-test

> Registry của tất cả phiên `vibe-test`. Thêm **1 dòng sau mỗi phiên**.
> 📋 Muốn biết **module còn nợ TC nào** → xem `coverage/coverage-<MOD>.md`, **không** đọc INDEX.
> 🔍 Locator cho `implement-automation` → `locators/vibe-locators-latest.md`.

| Run | Ngày | Module | Platform | Scope | Chạy | Kết quả | Evidence | §8 | Folder |
|---|---|---|---|--:|--:|---|---|---|---|
| **VR-001** | 2026-09-18 | **USR** | mobile (Appium) | 46 | 40 | **20P / 14F** / 5B · N-A 2 · NOT_RUN 5 🔄 | 40/40 ✅ | PARTIAL | `VR-001-USR-2026-09-18/` |
| **VR-002** | 2026-09-18 | **ORD** | mobile (Appium) | 88 | 43 | 25P / 14F / 3B · 1 chạy dở | 43/43 ✅ | PARTIAL | `VR-002-ORD-2026-09-18/` |
| **VR-003** | 2026-09-18 | **USR** | mobile (Appium) | 46 | 4 | **2P / 2F** · còn nợ **1** | 4/4 ✅ | PARTIAL | `VR-003-USR-2026-09-18/` |

## Ghi chú theo phiên

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

> 🔴 **CẢNH BÁO TRÙNG TÊN `VR-002`:** nhãn `VR-002` trong `KP-01 §10.2/§10.3` (`KB-VIBE-01`/`KB-VIBE-02`, `TC_04.5`/`TC_04.6`) là run của **đợt v1.0 CŨ**, **KHÔNG** phải phiên `VR-002-ORD-2026-09-18` ở bảng trên. Hai hệ đánh số độc lập — đọc tài liệu cũ thì đối chiếu theo **ngày**, không theo mã VR.
