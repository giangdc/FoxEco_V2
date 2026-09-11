# TC ↔ Scenario Mapping — VIỆC CÒN THIẾU

> Bộ TC v1.0 sinh bằng template ISC 42 cột — template này **không có cột `Scenario ID`** (bị bỏ khi migrate 2026-07-21).
> Khi convert sang schema 16 cột của `generate-tc` v1.1, cột **B `Scenario ID` để TRỐNG** ở cả 323 TC.
> **Không suy đoán, không bịa** — file này cung cấp dữ liệu đủ để hoàn thiện mapping một cách kiểm chứng được.

## Vì sao mapping này hoàn thiện được

Sheet `Coverage Matrix` của cả 9 module là **phân hoạch chính xác** tập TC — tổng cột `Total TCs` khớp tuyệt đối số TC
thật của từng module (verify 9/9 ✅). Nghĩa là **số TC của mỗi scenario đã biết chắc**, chỉ còn xác định *TC cụ thể nào*
thuộc scenario nào. Dùng bảng dưới làm checksum: gán xong mỗi module, đếm lại phải khớp cột `Số TC`.

## Cách hoàn thiện

1. Mở `fragments/TC-<MODULE>-v1.0.md`, đọc cột `Test Title` + `Notes` (Notes giữ nguyên tên **Block** gốc).
2. Đối chiếu `Scenario Title` ở bảng dưới → điền cột B.
3. Đếm lại: số TC gán cho mỗi SC **phải bằng** cột `Số TC`. Lệch = gán sai.
4. Xoá marker `⚠ SC ID chưa map` khỏi Notes sau khi gán xong.

> 💡 Bỏ qua được bước này nếu bạn định **regenerate toàn bộ TC** ở version mới — `generate-tc` sẽ tự sinh Scenario ID đúng ngay từ đầu.

---

## Hoạt động — `HOATDONG` (TC_01)

Tổng **20 TC** / **13 scenario** · dải ID: `TC_01.1` → `TC_01.20`

| SC ID | Scenario Title | Số TC |
|---|---|---:|
| `SC-ORD-025` | Bottom nav đủ 5 tab, "Hoạt động" highlight đúng | 1 |
| `SC-ORD-015` | Đủ 2 tab "Đang diễn ra"/"Đã hoàn thành" tại Hoạt động | 1 |
| `SC-ORD-016` | Tab mặc định khi mới vào màn Hoạt động | 1 |
| `SC-ORD-017` | Check dữ liệu đúng tại tab "Đang diễn ra" | 3 |
| `SC-ORD-026` | Check dữ liệu đúng tại tab "Đã hoàn thành" | 1 |
| `SC-ORD-018` | Check đầy đủ field trên 1 card đơn (completeness) | 1 |
| `SC-ORD-005` | Tin tự động "Hết hạn" khi quá thời gian không ai ghép | 2 |
| `SC-ORD-019` | Card trạng thái "Hoàn thành" hiển thị đúng, không assert rating | 1 |
| `SC-ORD-020` | Card trạng thái "Chờ ghép" hiển thị tại tab "Đang diễn ra" | 1 |
| `SC-ORD-021` | Tap card trạng thái khác "Hết hạn" → mở Chi tiết tin | 4 |
| `SC-ORD-022` | Tap card "Hết hạn" → không cho thao tác | 1 |
| `SC-ORD-023` | Empty state khi danh sách rỗng (cả 2 tab) | 2 |
| `SC-ORD-024` | Đơn "Đã huỷ" (CNL) không hiển thị tại Hoạt động | 1 |
| | **Tổng** | **20** |

---

## Cá nhân — `CANHAN` (TC_02)

Tổng **17 TC** / **10 scenario** · dải ID: `TC_02.1` → `TC_02.17`

| SC ID | Scenario Title | Số TC |
|---|---|---:|
| `SC-USR-002` | Xem hồ sơ cá nhân (view-only) | 1 |
| `SC-USR-003` | Hiển thị phòng ban + khu vực trên hồ sơ | 1 |
| `SC-USR-006` | Check đầy đủ hiển thị header màn Cá nhân (completeness) | 1 |
| `SC-USR-004` | Hiển thị đúng 2 chỉ số (đơn giúp + quà nhận), không hiện điểm/tier/CO2 | 4 |
| `SC-USR-005` | Cấu hình kênh liên hệ sẽ lộ (GAP — out of scope) | 1 |
| `SC-USR-007` | Menu "Đơn của tôi" điều hướng sang Hoạt động | 1 |
| `SC-GIFT-003` | Card "Quà đã nhận" chỉ load đúng loại đã nhận | 5 |
| `SC-GIFT-005` | Menu "Quà đã nhận" điều hướng sang màn Quà đã nhận | 1 |
| `SC-GIFT-006` | Màn "Quà đã nhận" rỗng khi chưa nhận quà nào | 1 |
| `SC-GIFT-007` | Icon quay lại tại màn "Quà đã nhận" | 1 |
| | **Tổng** | **17** |

---

## Thông báo — `NTF` (TC_03)

Tổng **27 TC** / **9 scenario** · dải ID: `TC_03.1` → `TC_03.27`

| SC ID | Scenario Title | Số TC |
|---|---|---:|
| `SC-NTF-001` | Thông báo khi ghép ngay (NTF-01/02) | 2 |
| `SC-NTF-002` | Thông báo khi khớp tuyến OFFER (NTF-03) | 1 |
| `SC-NTF-003` | Thông báo theo mốc vận chuyển (NTF-04/05/06) | 6 |
| `SC-NTF-004` | Thông báo khi nhận quà cảm ơn (NTF-07) | 1 |
| `SC-NTF-005` | Thông báo khi đơn huỷ (NTF-08) và tin quá hạn (NTF-09) | 4 |
| `SC-ASN-013` | Hệ thống chỉ bắn tối đa 5 thông báo khớp tin cho Carrier, tính riêng theo TỪNG TIN — không cộng | 3 |
| `SC-NTF-007` | Empty state khi chưa có thông báo nào | 1 |
| `SC-NTF-008` | Đánh dấu đã đọc (tap 1 thông báo / nút mark-all) | 4 |
| `SC-NTF-009` | Scroll xuống load thêm dữ liệu (phân trang) | 5 |
| | **Tổng** | **27** |

---

## Đăng tin — `DANGTIN` (TC_04)

Tổng **109 TC** / **20 scenario** · dải ID: `TC_04.1` → `TC_04.109`

| SC ID | Scenario Title | Số TC |
|---|---|---:|
| `SC-ORD-001` | Đăng tin NEED qua wizard 3 bước (happy path + điều hướng) | 7 |
| `SC-ORD-002` | Đăng tin OFFER (form 1 bước) | 3 |
| `SC-ORD-003` | Tin xuất hiện ở 'Đơn của tôi', không hiện mã đơn | 4 |
| `SC-ORD-004` | Timeline tin ghi nhận đầy đủ mốc thời gian (Theo dõi đơn — Sender) | 3 |
| `SC-ORD-005` | Tin tự động 'Hết hạn' khi quá thời gian không ai ghép | _(trống ở nguồn)_ |
| `SC-ORD-006` | Không tick điều khoản → chặn đăng tin (Bước 3) | 3 |
| `SC-ORD-007` | Bỏ trống Loại hàng/Giá trị/Người nhận bị chặn (validate bắt buộc) | 5 |
| `SC-ORD-008` | Chỉnh sửa tin khi 'Chờ ghép' | 4 |
| `SC-ORD-009` | Khoá chỉnh sửa từ 'Đã ghép' trở đi | 4 |
| `SC-ORD-010` | Chọn nhanh 1 trong 6 văn phòng preset FPT | 3 |
| `SC-ORD-011` | Email công ty người nhận có trong hệ thống → tự điền | 2 |
| `SC-ORD-012` | Email công ty người nhận không tồn tại → nhập thủ công | 11 |
| `SC-ORD-013` | Chọn Giá trị hàng 'Cao' → cảnh báo trách nhiệm tự thoả thuận | 3 |
| `SC-ORD-014` | Đăng tin chọn Loại hàng bất kỳ (kể cả Thuốc/Y tế) vẫn thành công | 3 |
| `SC-ORD-027` | Giới hạn ký tự tối đa + định dạng/kích thước ảnh (Ghi chú/Địa chỉ/Tên/Ảnh, NEED+OFFER) | 24 |
| `SC-ORD-028` | Khung giờ (NEED + OFFER) phải cách nhau tối thiểu 30 phút | 9 |
| `SC-ORD-029` | Tự động cắt khoảng trắng + chuẩn hoá SĐT trước khi lưu (VAL-03) | 2 |
| `SC-ORD-030` | Nút submit disabled tới khi hợp lệ; lỗi inline on-blur; cuộn tới lỗi đầu tiên (VAL-01/02) | 6 |
| `SC-ORD-031` | Địa chỉ lấy hàng (Người gửi) — autocomplete + editability (Tên read-only, SĐT bắt buộc/validate | 7 |
| `SC-ORD-032` | Địa chỉ giao hàng (Người nhận) — autocomplete + SĐT bắt buộc/validate | 6 |
| | **Tổng** | **109** |

---

## Trang chủ — `TRANGCHU` (TC_05)

Tổng **32 TC** / **4 scenario** · dải ID: `TC_05.1` → `TC_05.32`

| SC ID | Scenario Title | Số TC |
|---|---|---:|
| `SC-ORD-033` | Completeness màn Trang chủ (Header/Banner/Card/nút/bottom-nav) | 13 |
| `SC-ORD-003` | Card "Đơn của tôi" tại Trang chủ (6 trường + badge trạng thái) | 11 |
| `SC-ASN-008` | Trần 5 tin gợi ý hiển thị tại section "Tin mới" (Trang chủ) | 6 |
| `SC-ASN-010` | Thứ tự ưu tiên tin gợi ý: độ gần tuyến rồi thời gian đăng | 2 |
| | **Tổng** | **32** |

---

## Bảng tin & Chi tiết tin — `BANGTIN` (TC_06)

Tổng **31 TC** / **11 scenario** · dải ID: `TC_06.1` → `TC_06.31`

| SC ID | Scenario Title | Số TC |
|---|---|---:|
| `SC-ASN-014` | Bảng tin hiển thị đủ card list + bấm mở Chi tiết tin (completeness) | 4 |
| `SC-ASN-005` | Tin ẩn khỏi Bảng tin sau khi có người ghép | 3 |
| `SC-ASN-012` | Tin huỷ bởi Carrier (chưa lấy hàng) quay lại "Chờ ghép" và được khớp lại | 2 |
| `SC-ASN-010` | Gợi ý ưu tiên theo độ gần tuyến rồi thời gian đăng (bề mặt Bảng tin) | 2 |
| `SC-ORD-001` | Hiển thị màn Chi tiết tin (Thông tin hàng + Lộ trình & liên hệ) | 6 |
| `SC-ASN-003` | Trước khi ghép, SĐT KHÔNG lộ | 1 |
| `SC-ASN-001` | Carrier bấm "Tôi mang giúp được" → gửi đề nghị | 2 |
| `SC-ASN-011` | Không tự khớp tin của chính mình (ẩn/disable nút hành động) | 4 |
| `SC-ASN-007` | Carrier "Nhận giao" từ thông báo khớp tuyến → MATCHED | 1 |
| `SC-ASN-002` | Ghép ngay khi Carrier xác nhận → MATCHED + lộ SĐT + 3 khung đồng bộ | 5 |
| `SC-ASN-004` | 2 Carrier cùng bấm nhận gần đồng thời → chỉ 1 người ghép (chống double-accept) | 1 |
| | **Tổng** | **31** |

---

## Theo dõi đơn — `THEODOIDON` (TC_07)

Tổng **44 TC** / **14 scenario** · dải ID: `TC_07.1` → `TC_07.44`

| SC ID | Scenario Title | Số TC |
|---|---|---:|
| `SC-DLV-005` | Nút "Xác nhận đã nhận hàng" chỉ kích hoạt khi = Đã giao | 8 |
| `SC-DLV-006` | Nút hành động Carrier bị động ở trạng thái "Đã giao" | 3 |
| `SC-DLV-010` | Không thể bấm "Đã giao" trước khi bấm "Tôi đã lấy hàng" | 5 |
| `SC-DLV-011` | Người nhận xác nhận → đơn "Hoàn thành" ngay lập tức | 5 |
| `SC-DLV-012` | Nhãn nút Sender/Receiver đúng theo trạng thái Đã ghép/Đang giao | 6 |
| `SC-DLV-013` | Tại "Đã giao": Sender/Carrier disable, chỉ Receiver enable | 3 |
| `SC-DLV-014` | Carrier/Receiver thấy nhãn "Đơn đã hoàn thành" sau Hoàn thành | 2 |
| `SC-DLV-009` | Sau khi đã lấy hàng (IN_TRANSIT), huỷ thường bị chặn | 2 |
| `SC-DLV-007` | Quá N giờ chưa xác nhận nhận hàng → nhắc → admin hỗ trợ | 3 |
| `SC-DLV-001` | Carrier chụp ảnh hàng lúc nhận (tuỳ chọn) → lưu, gắn timeline | 2 |
| `SC-DLV-002` | Bỏ qua chụp ảnh lúc nhận vẫn chuyển trạng thái được | 1 |
| `SC-DLV-003` | Carrier bật chia sẻ vị trí khi đang giao | 1 |
| `SC-DLV-004` | Vị trí chia sẻ tự tắt/xoá sau khi đơn đóng | 2 |
| `SC-DLV-008` | Ghi nhận chi phí đối soát offline, không qua app | 1 |
| | **Tổng** | **44** |

---

## Huỷ đơn — `HUYDON` (TC_08)

Tổng **27 TC** / **5 scenario** · dải ID: `TC_08.1` → `TC_08.27`

| SC ID | Scenario Title | Số TC |
|---|---|---:|
| `SC-CNL-001` | Huỷ đơn ở POSTED/MATCHED → popup bắt buộc nhập lý do | 6 |
| `SC-CNL-005` | Lý do huỷ tối thiểu 5 ký tự mới bật nút Xác nhận (VAL-04) | 10 |
| `SC-CNL-003` | Đơn huỷ ghi rõ vai trò người huỷ + lý do, đồng bộ realtime 3 bên | 7 |
| `SC-CNL-004` | Carrier huỷ khi "Đã ghép" (chưa lấy hàng) → đơn về "Chờ ghép" | 2 |
| `SC-CNL-002` | Không cho huỷ khi đơn đã "Đang giao" trở đi | 2 |
| | **Tổng** | **27** |

---

## Tặng quà — `TANGQUA` (TC_09)

Tổng **16 TC** / **3 scenario** · dải ID: `TC_09.1` → `TC_09.16`

| SC ID | Scenario Title | Số TC |
|---|---|---:|
| `SC-GIFT-001` | Sau Hoàn thành, Sender chọn 1/4 loại quà tặng Carrier | 8 |
| `SC-GIFT-002` | Gửi quà không cần Carrier xác nhận → popup cảm ơn | 4 |
| `SC-GIFT-004` | Nút "Cảm ơn người vận chuyển" đổi thành "Bạn đã đánh giá" sau khi gửi quà | 4 |
| | **Tổng** | **16** |

---

## Tổng kết

| | Giá trị |
|---|---|
| Tổng TC | **323** |
| Tổng scenario có TC | **89** |
| Scenario không có TC | 7 (đều có lý do — xem `KP-04 §1.4`) |
| TC đã map Scenario ID | **0 / 323** ← việc cần làm |
