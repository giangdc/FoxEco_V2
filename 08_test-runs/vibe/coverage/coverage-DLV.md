# Coverage — module DLV — SCOPE_TOTAL = 81 TC

> Sổ cái TÍCH LŨY xuyên run cho module **DLV — Giao nhận & Theo dõi đơn** (v1.0 CARRIED + v1.1 delta).
> **Cập nhật lần cuối: VR-012 (2026-09-19)** · Nguồn scope: `03_test-cases/v1.0/TC-MASTER-v1.0.xlsx` (30 CARRIED `001–030`) + `03_test-cases/v1.1/TC-MASTER-v1.1.xlsx` (51 NEW `031–081`)
> **Tổng: có verdict cuối 19/81 · CÒN NỢ 62** (62 NOT_RUN + 0 NOT_EVIDENCED)
> Verdict hợp lệ: ✅ PASS · ❌ FAIL · 🚫 BLOCKED · ⚠️ NOT_EVIDENCED · ⏳ NOT_RUN · ⛔ N-A

> 🆕 **2026-09-19 — sổ cái DLV mở lần đầu ở VR-012.** SCOPE_TOTAL = **81** = **30 TC CARRIED của v1.0** (`TC-DLV-001..030`, v1.1 KHÔNG gộp lại) + **51 TC của v1.1** (`TC-DLV-031..081`). ⚠️ **0 TC ID trùng** giữa 2 file ⇒ hợp nhất là phép cộng thuần, không có ca "lấy bản v1.1".

## Tiến độ theo run

| Run | Ngày | TC chạy trong run | Verdict thu được |
|-----|------|-------------------|------------------|
| VR-012 | 2026-09-19 | 15 | 13P/2F/0B |

## Chi tiết từng TC

| Testcase ID | Verdict | Scenario ID | Priority | Title | Run | Evidence | Ghi chú |
|---|---|---|---|---|---|---|---|
| TC-DLV-001 | ✅ PASS | SC-DLV-001 | P2 | Check người gửi ở trạng thái "Chờ ghép" thấy nhãn chờ vận chuyển bị khoá kèm nút Chỉnh sửa và Huỷ đơn | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-001__verify-nhan-cho-van-chuyen-khoa.png` |  |
| TC-DLV-002 | ⏳ NOT_RUN | SC-DLV-002 | P2 | Check người vận chuyển ở trạng thái "Chờ ghép" thấy nút "Tôi mang giúp được" bật trên màn Chi tiết tin | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-003 | ⏳ NOT_RUN | SC-DLV-003 | P2 | Check người nhận ở trạng thái "Chờ ghép" thấy nhãn chờ vận chuyển bị khoá kèm nút Huỷ đơn | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-004 | ⏳ NOT_RUN | SC-DLV-004 | P2 | Check người gửi ở trạng thái "Đã ghép" thấy nhãn chờ lấy hàng bị khoá và không còn nút Chỉnh sửa | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-005 | ⏳ NOT_RUN | SC-DLV-005 | P2 | Check người vận chuyển ở trạng thái "Đã ghép" thấy nút "✓ Tôi đã lấy hàng" bật kèm nút huỷ nhận đơn | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-006 | ⏳ NOT_RUN | SC-DLV-006 | P2 | Check người nhận ở trạng thái "Đã ghép" thấy nhãn đã có người vận chuyển bị khoá kèm nút Huỷ đơn | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-007 | ⏳ NOT_RUN | SC-DLV-007 | P2 | Check người gửi ở trạng thái "Đang giao" thấy nhãn đang giao bị khoá và không còn nút Huỷ đơn | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-008 | ✅ PASS | SC-DLV-008 | P2 | Check người vận chuyển ở trạng thái "Đang giao" thấy nút "Đã giao cho người nhận" bật | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-008__verify-nut-da-giao-cho-nguoi-nhan-bat.png` |  |
| TC-DLV-009 | ✅ PASS | SC-DLV-009 | P2 | Check người nhận ở trạng thái "Đang giao" thấy nhãn đơn đang trên đường bị khoá | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-009__verify-nhan-don-dang-tren-duong.png` |  |
| TC-DLV-010 | ✅ PASS | SC-DLV-010 | P2 | Check người gửi ở trạng thái "Đã giao" thấy nhãn chờ người nhận xác nhận bị khoá | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-010__verify-nhan-cho-nguoi-nhan-xac-nhan.png` |  |
| TC-DLV-011 | ✅ PASS | SC-DLV-011 | P2 | Check người vận chuyển ở trạng thái "Đã giao" thấy nhãn chờ người nhận xác nhận bị khoá | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-011__verify-carrier-nhan-cho-nguoi-nhan-xac-nhan.png` |  |
| TC-DLV-012 | ✅ PASS | SC-DLV-012 | P1 | Check người nhận ở trạng thái "Đã giao" thấy nút "Xác nhận đã nhận hàng" bật | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-012__verify-nut-xac-nhan-da-nhan-hang-bat.png` |  |
| TC-DLV-013 | ⏳ NOT_RUN | SC-DLV-013 | P2 | Check người gửi ở trạng thái "Hoàn thành" thấy nút "✓ Cảm ơn người vận chuyển" bật khi chưa gửi quà | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-014 | ✅ PASS | SC-DLV-014 | P2 | Check người vận chuyển ở trạng thái "Hoàn thành" thấy nhãn đơn đã hoàn thành bị khoá | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-014__verify-carrier-nhan-don-da-hoan-thanh.png` |  |
| TC-DLV-015 | ✅ PASS | SC-DLV-015 | P2 | Check người nhận ở trạng thái "Hoàn thành" thấy nhãn đơn đã hoàn thành bị khoá | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-015__verify-nhan-don-da-hoan-thanh.png` |  |
| TC-DLV-016 | ⏳ NOT_RUN | SC-DLV-016 | P2 | Check thanh trạng thái có đủ năm mốc đúng thứ tự và tô đúng mốc hiện tại | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-017 | ⏳ NOT_RUN | SC-DLV-017 | P2 | Check popup xác nhận lấy hàng đúng nội dung và chuyển đơn sang "Đang giao" | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-018 | ⏳ NOT_RUN | SC-DLV-018 | P2 | Check popup xác nhận đã giao đúng nội dung và chuyển đơn sang "Đã giao" | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-019 | ⏳ NOT_RUN | SC-DLV-019 | P2 | Check popup xác nhận đã nhận hàng đúng nội dung và chuyển đơn sang "Hoàn thành" | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-020 | ⏳ NOT_RUN | SC-DLV-020 | P2 | Check nhấn "Huỷ" ở popup xác nhận không đổi trạng thái đơn và không ghi mốc lịch sử mới | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-021 | ⏳ NOT_RUN | SC-DLV-021 | P1 | Check không có đường nào chuyển đơn sang "Đã giao" khi chưa xác nhận lấy hàng | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-022 | ⏳ NOT_RUN | SC-DLV-022 | P1 | Check chỉ người nhận chốt được đơn ở trạng thái "Đã giao" | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-023 | ⏳ NOT_RUN | SC-DLV-023 | P1 | Check đơn chuyển "Hoàn thành" ngay sau khi người nhận xác nhận, không có bước chờ duyệt | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-024 | ⏳ NOT_RUN | SC-DLV-024 | P2 | Check đơn ở "Đã giao" quá hai giờ chưa xác nhận thì người nhận được nhắc và quá bốn giờ thì chuyển admin hỗ trợ | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-025 | ⏳ NOT_RUN | SC-DLV-025 | P2 | Check luồng xác nhận nhận hàng dùng modal đơn giản không có ảnh bằng chứng và điểm uy tín | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-026 | ✅ PASS | SC-DLV-026 | P2 | Check người gửi thấy cụm liên hệ người vận chuyển sau khi ghép và không thấy trước khi ghép | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-026__verify-sau-ghep-co-cum-nguoi-giao-hang.png` | 2 đơn thay vì before/after 1 đơn |
| TC-DLV-027 | ✅ PASS | SC-DLV-027 | P2 | Check người vận chuyển thấy cả cụm liên hệ người gửi và người nhận | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-027__verify-cum-nguoi-gui-va-nguoi-nhan.png` | ⚠️ chạy trên đơn `Đang giao` thay vì `Đã ghép` |
| TC-DLV-028 | ✅ PASS | SC-DLV-028 | P2 | Check người nhận chỉ thấy cụm liên hệ người giao hàng và không thấy thông tin người gửi | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-028__verify-chi-cum-nguoi-giao-hang.png` | ⚠️ chạy trên đơn `Đã giao` thay vì `Đã ghép` · 2026-09-21: QC xác nhận `BUG-022` không phải bug (app đúng) — TC giữ bản gốc, verdict PASS không đổi |
| TC-DLV-029 | ✅ PASS | SC-DLV-029 | P2 | Check block Lịch sử có đủ năm mốc sự kiện kèm timestamp trên đơn đi thẳng tới hoàn thành | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-029__verify-lich-su-du-5-moc.png` | ⚠️ xem bằng vai C thay vì vai A |
| TC-DLV-030 | ⏳ NOT_RUN | SC-DLV-030 | P3 | Check nhãn phụ màn Theo dõi đơn đổi đúng theo vai của tài khoản đang xem | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-031 | ⏳ NOT_RUN | SC-DLV-031 | P2 | Check người gửi thấy nhãn xem lịch hẹn giao lại khi đơn hẹn giao lại | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-032 | ⏳ NOT_RUN | SC-DLV-031 | P2 | Check người vận chuyển thấy nhãn giao lại theo lịch khi đơn hẹn giao lại | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-033 | ⏳ NOT_RUN | SC-DLV-031 | P2 | Check người nhận thấy nhãn xem lịch hẹn khi đơn hẹn giao lại | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-034 | ⏳ NOT_RUN | SC-DLV-032 | P2 | Check người gửi thấy nút xác nhận đã nhận lại hàng khi đơn đang hoàn hàng | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-035 | ⏳ NOT_RUN | SC-DLV-032 | P2 | Check người vận chuyển thấy nhãn xem lịch hẹn trả hàng khi đơn đang hoàn hàng | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-036 | ⏳ NOT_RUN | SC-DLV-032 | P2 | Check người nhận thấy nhãn xem lý do hoàn hàng khi đơn đang hoàn hàng | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-037 | ⏳ NOT_RUN | SC-DLV-033 | P3 | Check người gửi thấy nhãn xem lý do và đăng lại ở ba trạng thái đóng | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-038 | ⏳ NOT_RUN | SC-DLV-033 | P3 | Check người vận chuyển chỉ thấy nhãn xem lý do ở ba trạng thái đóng | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-039 | ⏳ NOT_RUN | SC-DLV-033 | P3 | Check người nhận chỉ thấy nhãn xem lý do ở ba trạng thái đóng | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-040 | ⏳ NOT_RUN | SC-DLV-034 | P2 | Check đơn có báo cáo sự cố không tự chuyển sang hoàn thành sau các mốc nhắc | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-041 | ⏳ NOT_RUN | SC-DLV-035 | P3 | Check đính ảnh lúc lấy hàng lưu được kèm mốc và đơn chuyển đang giao | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-042 | ⏳ NOT_RUN | SC-DLV-036 | P3 | Check xác nhận đã lấy hàng vẫn thành công khi không đính ảnh nào | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-043 | ⏳ NOT_RUN | SC-DLV-037 | P1 | Check giao tận tay người nhận chuyển đơn sang đã giao và ghi đúng mốc nhật ký | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-044 | ⏳ NOT_RUN | SC-DLV-038 | P1 | Check giao cho người được uỷ quyền tự sinh uỷ quyền bởi người nhận và ghi đúng nhật ký | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-045 | ⏳ NOT_RUN | SC-DLV-039 | P2 | Check gửi quầy lễ tân bắt buộc hai ô người trực quầy và ghi đúng tên vào nhật ký | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-046 | ⏳ NOT_RUN | SC-DLV-039 | P2 | Check gửi quầy bảo vệ ghi đúng mẫu câu nhật ký riêng của quầy bảo vệ | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-047 | ⏳ NOT_RUN | SC-DLV-040 | P2 | Check nút xác nhận đã giao hàng chỉ bật sau khi đính ảnh bằng chứng đầu tiên | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-048 | ⏳ NOT_RUN | SC-DLV-041 | P2 | Check ảnh bằng chứng đã gắn mốc nhật ký không xoá được từ màn theo dõi đơn | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-049 | ⏳ NOT_RUN | SC-DLV-042 | P2 | Check huỷ ở popup xác nhận giao hàng không ghi mốc và giữ nguyên trạng thái đơn | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-050 | ⏳ NOT_RUN | SC-DLV-043 | P2 | Check luồng không liên lạc được đi đúng bốn tầng và ba phương án đúng thứ tự | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-051 | ⏳ NOT_RUN | SC-DLV-044 | P2 | Check màn liên hệ người gửi để trống ô người nhận thay và tự sinh uỷ quyền bởi người gửi | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-052 | ⏳ NOT_RUN | SC-DLV-045 | P2 | Check gửi quầy từ màn xử lý đơn hàng chuyển đơn sang đã giao khi nhập đủ tên và ảnh | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-053 | ⏳ NOT_RUN | SC-DLV-046 | P3 | Check không nhập được tên người trực quầy thì buộc chuyển sang cầm hàng về | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-054 | ⏳ NOT_RUN | SC-DLV-047 | P3 | Check người gửi thấy cảnh báo không liên lạc được người nhận trong nhật ký | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-055 | ⏳ NOT_RUN | SC-DLV-047 | P3 | Check người vận chuyển thấy cảnh báo không liên lạc được người nhận trong nhật ký | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-056 | ⏳ NOT_RUN | SC-DLV-047 | P3 | Check người nhận thấy cảnh báo không liên lạc được người nhận trong nhật ký | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-057 | ⏳ NOT_RUN | SC-DLV-048 | P3 | Check người nhận nhận đủ hai thông báo nhắc sau bốn giờ và cuối ngày giữ hàng tại quầy | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-058 | ⏳ NOT_RUN | SC-DLV-049 | P2 | Check chọn giao lại sau đổi nhãn khối lịch hẹn sang hẹn giao lại và nơi giao lại | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-059 | ⏳ NOT_RUN | SC-DLV-049 | P2 | Check chọn trả về cho người gửi đổi nhãn khối lịch hẹn sang hẹn trả hàng và nơi nhận lại hàng | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-060 | ⏳ NOT_RUN | SC-DLV-049 | P2 | Check ngày hẹn nhận đúng bảy ngày và chặn ngày thứ tám | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-061 | ⏳ NOT_RUN | SC-DLV-049 | P2 | Check khoảng giờ hẹn nhận đúng ba mươi phút và chặn khoảng hai mươi chín phút | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-062 | ⏳ NOT_RUN | SC-DLV-050 | P2 | Check người vận chuyển mở lại màn giao hàng đưa đơn hẹn giao lại về đang giao | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-063 | ⏳ NOT_RUN | SC-DLV-051 | P2 | Check người gửi xác nhận đã nhận lại hàng đóng đơn ở trạng thái đã trả người gửi | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-064 | ⏳ NOT_RUN | SC-DLV-052 | P1 | Check đơn đã trả người gửi không mở bước tặng quà cho người gửi | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-065 | ⏳ NOT_RUN | SC-DLV-052 | P1 | Check đơn đã trả người gửi không làm tăng chỉ số đơn đã giúp của người vận chuyển | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-066 | ⏳ NOT_RUN | SC-DLV-053 | P2 | Check lý do người nhận từ chối nhận hàng được lưu vào nhật ký đơn | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-067 | ⏳ NOT_RUN | SC-DLV-054 | P3 | Check đơn quá lịch hẹn hai mươi bốn giờ không tự chuyển sang hoàn thành | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-068 | ✅ PASS | SC-DLV-055 | P2 | Check nhật ký ghi đúng nguyên văn mẫu câu giao tận tay người nhận | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-068__verify-mau-cau-giao-tan-tay.png` | kiểm trên mốc có sẵn, không tự sinh mốc |
| TC-DLV-069 | ⏳ NOT_RUN | SC-DLV-055 | P2 | Check nhật ký ghi đúng nguyên văn mẫu câu giao cho người được uỷ quyền | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-070 | ⏳ NOT_RUN | SC-DLV-056 | P2 | Check nhật ký ghi đúng nguyên văn mẫu câu gửi tại quầy lễ tân | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-071 | ⏳ NOT_RUN | SC-DLV-056 | P2 | Check nhật ký ghi đúng nguyên văn mẫu câu gửi tại quầy bảo vệ | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-072 | ⏳ NOT_RUN | SC-DLV-057 | P2 | Check nhật ký ghi đúng nguyên văn mẫu câu cầm hàng về kèm lịch hẹn giao lại | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-073 | ⏳ NOT_RUN | SC-DLV-057 | P2 | Check nhật ký ghi đúng nguyên văn mẫu câu đã trả lại người gửi | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-074 | ⛔ N-A | SC-DLV-058 | P1 | Check chuyển thẳng đơn chờ ghép sang đã giao bị từ chối và không ghi mốc | VR-012 | — | **API-tier theo thiết kế của chính TC** — pre-condition đòi *"công cụ proxy chặn và phát lại request"*; phép thử là **giả mạo request bỏ qua UI**, nên ⛔ không thể phủ bằng vibe-test. Chuyển tier API/security test. |
| TC-DLV-075 | ⛔ N-A | SC-DLV-059 | P1 | Check chuyển thẳng đơn đang giao sang đã trả người gửi bị từ chối | VR-012 | — | **API-tier theo thiết kế của chính TC** — đòi proxy chặn & phát lại request để ép chuyển trạng thái trái luồng. ⛔ Không phủ được qua UI. |
| TC-DLV-076 | ⛔ N-A | SC-DLV-059 | P1 | Check chuyển thẳng đơn đang giao sang hoàn thành bị từ chối | VR-012 | — | **API-tier theo thiết kế của chính TC** — đòi proxy chặn & phát lại request để ép chuyển trạng thái trái luồng. ⛔ Không phủ được qua UI. |
| TC-DLV-077 | ⏳ NOT_RUN | SC-DLV-061 | P3 | Check tải năm ảnh bằng chứng trên mạng 4G hoàn tất dưới mười lăm giây | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-078 | ⛔ N-A | SC-DLV-062 | P1 | Check nhật ký đơn không mất dòng mốc nào sau khi huỷ nhận đơn | VR-012 | — | **API-tier theo thiết kế của chính TC** — đòi proxy sửa/xoá dòng nhật ký rồi phát lại. ⛔ Không phủ được qua UI. |
| TC-DLV-079 | ⏳ NOT_RUN | SC-DLV-063 | P3 | Check tên và số điện thoại người nhận thay chỉ xuất hiện trong nhật ký đơn | — | — | **Lý do:** chưa tới lượt — VR-012 là phiên DLV đầu tiên |
| TC-DLV-080 | ❌ FAIL | SC-DLV-064 | P3 | Check icon copy cạnh số điện thoại sao chép đúng nội dung và đổi màu xanh | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-080__step6-FAIL-icon-khong-doi-mau.png` | icon copy không đổi màu xanh; nội dung copy ĐÚNG |
| TC-DLV-081 | ❌ FAIL | SC-DLV-064 | P3 | Check icon copy cạnh địa chỉ giao sao chép đúng nội dung và đổi màu xanh | VR-012 | `VR-012-DLV-2026-09-19/screenshots/TC-DLV-081__step6-FAIL-icon-khong-doi-mau.png` | icon copy không đổi màu xanh; nội dung copy ĐÚNG |

## Tổng hợp

| Verdict | Số | TC |
|---|---|---|
| ✅ PASS | 13 | `TC-DLV-001` · `TC-DLV-008` · `TC-DLV-009` · `TC-DLV-010` · `TC-DLV-011` · `TC-DLV-012` · `TC-DLV-014` · `TC-DLV-015` · `TC-DLV-026` · `TC-DLV-027` · `TC-DLV-028` · `TC-DLV-029` · `TC-DLV-068` |
| ❌ FAIL | 2 | `TC-DLV-080` · `TC-DLV-081` |
| 🚫 BLOCKED | 0 | — |
| ⚠️ NOT_EVIDENCED | 0 | — |
| ⏳ NOT_RUN | 62 | *(toàn bộ phần còn lại)* |
| ⛔ N-A | 4 | `TC-DLV-074` · `TC-DLV-075` · `TC-DLV-076` · `TC-DLV-078` |
| **Tổng** | **81** | |

**Có verdict cuối: 19/81 · CÒN NỢ: 62** ⇒ §8 = **PARTIAL**.
