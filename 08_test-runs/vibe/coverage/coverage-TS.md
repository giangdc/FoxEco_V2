# Coverage — module TS — SCOPE_TOTAL = 17 TC

> Sổ cái TÍCH LŨY xuyên run cho module TS (chỉ phạm vi **v1.1**, `TC-TS-008..024`).
> 7 TC CARRIED v1.0 (`TC-TS-001..007`) KHÔNG nằm trong SCOPE_TOTAL này — chưa từng vibe-test, ngoài phạm vi yêu cầu QC (chỉ test case v1.1).
> **Cập nhật lần cuối: VR-029 2026-09-24 (retest 5 TC)** · Nguồn scope: `03_test-cases/v1.1/fragments/TC-TS-v1.1.md`
> **Tổng: có verdict cuối 17/17 · CÒN NỢ 0** — 16 PASS · 0 FAIL · 1 N-A (`TC-TS-017` DESCOPED)

> 🔁 **2026-09-24 — VR-029 retest 5 TC** sau khi sửa Expected theo BA (`C-TS-04`): `009`/`012`/`013`/`021` → ✅ PASS. 🔴 `TC-TS-016` vẫn FAIL nhưng **ngược chiều**: app nay tự vẽ màn lỗi + nút "Thử lại" (đúng spec gốc), lệch Expected vừa sửa sáng cùng ngày — QC đã chốt lại Expected theo app hiện tại ⇒ `TC-TS-016` → ✅ PASS. Chi tiết: `VR-029-TS-2026-09-24/vibe-report.md`.
> Verdict hợp lệ: ✅ PASS · ❌ FAIL · 🚫 BLOCKED · ⚠️ NOT_EVIDENCED · ⏳ NOT_RUN · ⛔ N-A

> 🔁 **2026-09-22 follow-up — retest 12 TC sau khi bypass được màn đăng nhập Microsoft:** QC tự đăng
> nhập tài khoản Microsoft **thật** trên thiết bị thật `R58T20PLP8K` rồi yêu cầu dùng thiết bị này để
> retest các TC từng BLOCKED bởi `BUG-037`. WebView tải được **form Microsoft Forms thật**.
> 🔴 **3 phát hiện đảo ngược các clarification đã "Resolved" trước đó** (các clarification đó dựa
> trên quan sát demo/phân tích TRƯỚC KHI từng đăng nhập qua được màn Microsoft):
> - `TC-TS-009` FAIL — màn xác nhận sau khi gửi là màn **mặc định của Microsoft Forms**, không có
>   cam kết "24 giờ làm việc" / nút "Quay lại đơn hàng" như `C-TS-03(d)` (Resolved) từng kết luận.
> - `TC-TS-013` FAIL — trường "Hình ảnh đính kèm" **THỰC RA bắt buộc** (có `*`, chặn submit khi 0
>   ảnh), ngược hẳn giả định "biên dưới hợp lệ" của `SC-TS-010`.
> - `TC-TS-021` FAIL — ô "Mã đơn hàng" **THỰC RA sửa được** (bàn phím bật, ký tự chèn vào được),
>   ngược `C-TS-03(b)` (Resolved: "nhãn tĩnh, không sửa được").
> `TC-TS-014` PASS nhưng cơ chế chặn ảnh thứ 6 là **nút biến mất** chứ không phải "disable".
>
> 🔁 **Cập nhật 2026-09-22 (sau khi log bug):** `TC-TS-010`/`TC-TS-011` ban đầu ghi FAIL vì Expected
> giả định "nút Gửi disable" trong khi thực tế MS Forms dùng inline error — QC xác nhận đây **không
> phải bug** (`BUG-040` đã xoá), nghiệp vụ vẫn chặn đúng submit khi thiếu trường bắt buộc. Đã **sửa
> lại Expected** của `TC-TS-010`/`TC-TS-011`/`TC-TS-012` theo đúng cơ chế thật
> (`fragments/TC-TS-v1.1.md` + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx`) ⇒ `TC-TS-010`/`011`
> đảo verdict **FAIL → ✅ PASS**. `TC-TS-012` **vẫn FAIL** — lý do hẹp lại còn đúng 1 vế: SĐT sai định
> dạng phải bị chặn nhưng thực tế **không** bị chặn (`BUG-041`, còn giữ, chưa xoá).
> Chi tiết đầy đủ từng TC: `08_test-runs/vibe/VR-019-TS-2026-09-22/vibe-log.md` §"🆕 Follow-up 2026-09-22".
> 🔴 **CẦN `/analyze-requirements --update`** để mở lại `C-TS-03(b)`/`C-TS-03(d)`, sửa
> `test_data_catalog.md`/`test_scenario_map.md` của TS theo hành vi thật.

## Tiến độ theo run

| Run | Ngày | Tier | TC chạy trong run | Verdict thu được |
|-----|------|------|-------------------|------------------|
| VR-019 | 2026-09-22 | vibe-test | 17 | 3P/1F/13B |
| VR-019 follow-up | 2026-09-22 | vibe-test (retest) | 12 (đảo verdict từ BLOCKED) | 9P/3F |
| VR-029 | 2026-09-24 | vibe-test (retest) | 5 (`009` `012` `013` `016` `021`) | 4P/1F → **5P** sau khi QC chốt lại Expected `016` |

## Chi tiết từng TC

| Testcase ID | Verdict | Scenario ID | Priority | Title | Run | Evidence | Ghi chú |
|---|---|---|---|---|---|---|---|
| TC-TS-008 | ✅ PASS | SC-TS-008 | P1 | Check form báo cáo sự cố mở trong WebView và chỉ điền sẵn mã đơn hàng | VR-019 follow-up | `VR-019-TS-2026-09-22/screenshots/TC-TS-008__verify-only-madon-prefilled.png` · `TC-TS-008__verify-2-mota-sdt-empty.png` | Đảo từ BLOCKED — đúng Expected, chỉ 1/4 trường prefill |
| TC-TS-009 | ✅ PASS | SC-TS-008 | P1 | Check gửi báo cáo sự cố hợp lệ hiện màn ghi nhận kèm cam kết liên hệ lại | VR-029 | `VR-029-TS-2026-09-24/screenshots/TC-TS-009__pre-form-filled-2-anh.png` · `TC-TS-009__verify-man-xac-nhan-mac-dinh-ms-forms.png` | Retest 2026-09-24: FAIL → PASS — Expected sửa theo BA `FE-323` (màn mặc định MS Forms) |
| TC-TS-010 | ✅ PASS | SC-TS-009 | P2 | Check nút Gửi vô hiệu hoá khi chưa chọn loại yêu cầu | VR-019 follow-up | `VR-019-TS-2026-09-22/screenshots/TC-TS-010__verify-gui-empty-required-behavior.png` | Expected đã sửa theo cơ chế thật (inline error) 2026-09-22 — nay khớp Actual; `BUG-040` đã xoá |
| TC-TS-011 | ✅ PASS | SC-TS-009 | P2 | Check nút Gửi vô hiệu hoá khi chưa nhập mô tả chi tiết | VR-019 follow-up | `VR-019-TS-2026-09-22/screenshots/TC-TS-011__verify-mota-empty-blocks-submit.png` | Cùng cơ chế TC-TS-010, cùng lý do đảo verdict |
| TC-TS-012 | ✅ PASS | SC-TS-009 | P2 | Check nút Gửi vô hiệu hoá khi số điện thoại sai định dạng | VR-029 | `VR-029-TS-2026-09-24/screenshots/TC-TS-012__pre-sdt-0912abc-form-filled.png` · `TC-TS-012__verify-sdt-0912abc-gui-thanh-cong.png` | Retest 2026-09-24: FAIL → PASS — Expected sửa theo BA `FE-324` (không validate định dạng SĐT) |
| TC-TS-013 | ✅ PASS | SC-TS-010 | P3 | Check gửi báo cáo sự cố thành công khi không đính ảnh nào | VR-029 | `VR-029-TS-2026-09-24/screenshots/TC-TS-013__pre-form-filled-0-anh.png` · `TC-TS-013__verify-0-anh-gui-thanh-cong.png` | Retest 2026-09-24: FAIL → PASS — `FE-325` Fixed, 0 ảnh gửi được |
| TC-TS-014 | ✅ PASS | SC-TS-011 | P3 | Check đính đủ năm ảnh thì nút thêm ảnh khác bị vô hiệu hoá | VR-019 follow-up | `VR-019-TS-2026-09-22/screenshots/TC-TS-014__verify-5-anh-them-anh-bi-vo-hieu.png` | Đảo từ BLOCKED — đúng tinh thần nghiệp vụ; cơ chế thật là nút BIẾN MẤT chứ không disable |
| TC-TS-015 | ✅ PASS | SC-TS-011 | P3 | Check xoá được từng ảnh đính kèm riêng lẻ và mở lại chỗ thêm ảnh | VR-019 follow-up | `VR-019-TS-2026-09-22/screenshots/TC-TS-015__verify-xoa-anh-3-con-4-anh.png` | Đảo từ BLOCKED — khớp đúng Expected |
| TC-TS-016 | ✅ PASS | SC-TS-012 | P2 | Check mất mạng khi mở báo cáo sự cố thì app hiện lỗi kèm nút thử lại | VR-029 | `VR-029-TS-2026-09-24/screenshots/TC-TS-016__step6-FAIL-app-ve-man-loi-co-nut-thu-lai.png` · `TC-TS-016__verify-mat-mang-man-loi-app.png` | Retest VR-029 2026-09-24: app vẽ màn lỗi + nút "Thử lại"; QC chốt lại Expected theo hành vi hiện tại cùng ngày ⇒ FAIL → PASS (không chạy lại, evidence `__verify` VR-029 khớp Expected mới) |
| TC-TS-017 | ⛔ N-A | SC-TS-012 | P2 | Check thử lại sau khi có mạng mở đúng form của đơn cũ không mất ngữ cảnh | VR-019 | `VR-019-TS-2026-09-22/screenshots/TC-TS-017__step6-BLOCKED-no-retry-button.png` | DESCOPED 2026-09-24 (BA bỏ vế mất mạng `BR16-04`, `FE-322`). ⚠️ Recon VR-029: nút "Thử lại" đã có và giữ đúng mã đơn — đề xuất QC bỏ DESCOPED |
| TC-TS-018 | ✅ PASS | SC-TS-013 | P3 | Check đóng WebView quay về đúng màn theo dõi đơn trước đó | VR-019 | `VR-019-TS-2026-09-22/screenshots/TC-TS-018__verify-quay-lai-dung-man-in-transit.png` | Không phụ thuộc nội dung form |
| TC-TS-019 | ✅ PASS | SC-TS-013 | P3 | Check mở lại báo cáo sự cố là phiên mới không giữ dữ liệu nhập dở | VR-019 follow-up | `VR-019-TS-2026-09-22/screenshots/TC-TS-019__verify-reopen-la-phien-moi-khong-giu-du-lieu.png` · `TC-TS-019__verify-2-mota-empty-newsession.png` | Đảo từ BLOCKED — đúng Expected (áp dụng khi phiên trước CHƯA submit; xem ghi chú riêng về hành vi sau-khi-đã-submit trong vibe-log) |
| TC-TS-020 | ✅ PASS | SC-TS-015 | P2 | Check gửi báo cáo sự cố không làm đơn đổi trạng thái | VR-019 follow-up | `VR-019-TS-2026-09-22/screenshots/TC-TS-020__verify-trang-thai-khong-doi-sau-gui.png` | Đảo từ BLOCKED — verify lệch tài khoản/trạng thái so với script gốc (account B thay vì A, IN_TRANSIT thay vì POSTED), xem ghi chú trong vibe-log |
| TC-TS-021 | ✅ PASS | SC-TS-014 | P3 | Check ô mã đơn hàng là nhãn tĩnh chỉ đọc không sửa được | VR-029 | `VR-029-TS-2026-09-24/screenshots/TC-TS-021__verify-madon-sua-duoc-chen-x.png` | Retest 2026-09-24: FAIL → PASS — Expected sửa theo BA `FE-326` (ô mã đơn sửa được) |
| TC-TS-022 | ✅ PASS | SC-TS-015 | P2 | Check người gửi thấy nút báo cáo sự cố ở cả ba trạng thái đơn | VR-019 | `VR-019-TS-2026-09-22/screenshots/TC-TS-022__verify-observation3-intransit.png` | Đủ 3 checkpoint, không phụ thuộc nội dung form |
| TC-TS-023 | ✅ PASS | SC-TS-015 | P2 | Check người vận chuyển thấy nút báo cáo sự cố ở cả hai trạng thái sau khi nhận đơn | VR-019 | `VR-019-TS-2026-09-22/screenshots/TC-TS-023__verify-observation2-intransit.png` | Đủ 2 checkpoint |
| TC-TS-024 | ✅ PASS | SC-TS-015 | P2 | Check người nhận thấy nút báo cáo sự cố và mở được form giống hai vai kia | VR-019 follow-up | `VR-019-TS-2026-09-22/screenshots/TC-TS-024__verify-form-loaded-after-ms-login.png` | Đảo từ BLOCKED — khớp đúng Expected, giống hệt vai A/B |

## Tổng hợp

| Verdict | Số | TC |
|---|---|---|
| ✅ PASS | 11 | `TC-TS-008`, `TC-TS-010`, `TC-TS-011`, `TC-TS-014`, `TC-TS-015`, `TC-TS-018`, `TC-TS-019`, `TC-TS-020`, `TC-TS-022`, `TC-TS-023`, `TC-TS-024` |
| ❌ FAIL | 5 | `TC-TS-009`, `TC-TS-012`, `TC-TS-013`, `TC-TS-016` (`BUG-038`), `TC-TS-021` |
| 🚫 BLOCKED | 1 | `TC-TS-017` (`BUG-038` — thiếu nút "Thử lại", không liên quan màn login) |
| ⚠️ NOT_EVIDENCED | 0 | |
| ⏳ NOT_RUN | 0 | |
| ⛔ N-A | 0 | |
| **Tổng** | **17** | |

**Có verdict cuối: 17/17 · CÒN NỢ: 0** ⇒ §8 = **COMPLETED** (mọi TC có verdict cuối + evidence).

> 🔴 **Việc cần làm tiếp (ngoài phạm vi vibe-test):**
> 1. `/analyze-requirements --update` — mở lại `C-TS-03(b)` (mã đơn hàng sửa được) và `C-TS-03(d)`
>    (màn xác nhận là mặc định MS Forms), sửa `test_data_catalog.md`/`test_scenario_map.md` §TS theo
>    hành vi thật (Hình ảnh đính kèm bắt buộc, SĐT không validate định dạng, Gửi không disable).
> 2. `review-tc`/`generate-tc` cập nhật lại Expected của `TC-TS-008/009/013/019/020/021` trong
>    `TC-MASTER-v1.1.xlsx` sau khi có clarification mới — vibe-test không tự sửa TC-MASTER.
>    (`TC-TS-010/011/012` **đã sửa xong** 2026-09-22, xem mục cập nhật ở trên.)
> 3. `TC-TS-017` còn `BLOCKED` chờ fix `BUG-038` (thêm nút "Thử lại") — không liên quan màn login
>    Microsoft nên KHÔNG nằm trong đợt retest 12 TC của follow-up này.
> 4. ✅ **Đã log 2026-09-22:** `BUG-039` (màn xác nhận mặc định MS Forms) · `BUG-041` (SĐT không
>    validate định dạng) · `BUG-042` (ảnh đính kèm bắt buộc, ngược giả định) · `BUG-043` (mã đơn
>    hàng sửa được, ngược `C-TS-03(b)`) — 4 bug ở `draft/`, **chưa push Jira**, chờ QC review.
>    🗑️ `BUG-040` (nút Gửi không disable) **đã xoá** — QC xác nhận không phải bug, đã sửa Expected
>    thay vì log bug (xem mục cập nhật ở trên + `bug-index.md`).
