# Test Data Catalog — v1.0 · Module HOME

> Tạo bởi: analyze-requirements (**stage: analyze**).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.

## Module HOME — Trang chủ (DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-06)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Tên hiển thị ở lời chào | Master | tên hồ sơ nhân viên (STG: "Chung Hoàng Liêm") | — (không nhập được) | **hồ sơ không có tên → chưa có đặc tả** | `DOC-v1.0-02` §2 dòng "Header" |
| Icon vai trò (header) | Master | 3 giá trị theo vai Sender/Carrier/Receiver | — | — | `DOC-v1.0-02` §2 · ⚠ **chưa có mapping** (`C-HOME-01`) |
| Chấm đỏ chuông | Runtime | có ≥1 thông báo chưa đọc → hiện chấm | — | **0 thông báo chưa đọc → KHÔNG hiện chấm** | `DOC-v1.0-02` §2 dòng "Header" |
| Tagline banner | Master | "Tiện đường — Giúp đồng nghiệp" (PRD) | — | ⚠ `DOC-v1.0-01` §A3 L29 ghi **"Tiện đường — Đồng nghiệp giúp nhau"** — 2 nguồn lệch chữ | `DOC-v1.0-02` §2 · `DOC-v1.0-01` §A3 L29 |
| Số đơn đã giúp (card) | Runtime | số nguyên ≥ 0 | — | **0 (tài khoản mới)** | `DOC-v1.0-02` §2 · `USR-05` §A6 L102 |
| Thống kê cộng đồng `[x] đơn · [y] người` | Runtime | số toàn hệ thống, không seed được | — | — (⛔ không assert giá trị) | `DOC-v1.0-02` §2 dòng "Card "Đóng góp của bạn"" |
| Số đơn đang hoạt động của tài khoản | Fixture | 1 đơn ở trạng thái Chờ ghép..Đã giao → section hiện | — | **0 đơn → section ẩn** · **≥2 đơn → chưa có đặc tả hiển thị đơn nào** | `DOC-v1.0-02` §3.1 dòng "Đơn của tôi" |
| Nhãn vai của section | Runtime | `Gửi:` (Sender) · `Giao:` (Carrier) · `Nhận:` (Receiver) | nhãn không khớp vai đang xem | — (tập hữu hạn 3 giá trị) | `DOC-v1.0-02` §3.1 · §5.1 |
| Badge trạng thái | Runtime | `{Chờ ghép, Đã ghép, Đang giao, Đã giao, Hoàn thành}` | `Đã huỷ` / `Hết hạn` (⚠ đơn không còn "đang hoạt động" — xem `SC-ACT-007`) | **`Hoàn thành` = ranh giới còn/không còn "đang hoạt động" — chưa có đặc tả rõ** | `DOC-v1.0-02` §3.1 · `DOC-v1.0-01` §D2 L232 |
| Thanh progress | Runtime | tô 1..5 bước khớp badge | lệch giữa badge và progress | **bước 1 (Chờ ghép)** và **bước 5 (Hoàn thành)** | `DOC-v1.0-01` §D2 L232 |
| Số tin cộng đồng (section "Tin mới") | Fixture | ≥1 tin còn hiệu lực, chưa ghép | — | **0 tin (empty)** · **đúng 5 tin** · **≥6 tin (kích hoạt nút "Xem thêm")** | `US-D06` §D1b L175 · `DOC-v1.0-02` §3.1 |

## Ghi chú chung
- **`Loại data`:** `Master` = từ hồ sơ nhân viên/hệ thống · `Fixture` = QC tự tạo (đăng tin để có đơn/tin) · `Runtime` = sinh khi chạy (badge, progress, số đếm).
- **Boundary quan trọng nhất của module:** dải **số tin cộng đồng** `{0, 5, ≥6}` — nó là boundary duy nhất kích hoạt được nút *"Xem thêm trên Bảng tin"* và là dữ liệu để đo mâu thuẫn **1 vs 5** (`C-HOME-03`). Cần seed ≥6 tin trên STG trước khi execute.
- **Boundary `≥2 đơn đang hoạt động` chưa có đặc tả** — PRD dựng từ bản demo **chỉ mô phỏng 1 đơn duy nhất** (`DOC-v1.0-02` §7 dòng 3: *"Đăng tin mới sẽ ghi đè đơn đang có"*) ⇒ hành vi multi-order **không suy được từ demo**; ghi nhận ở `risk_assessment.md` `RISK-HOME-03`.
- ⛔ **Không assert giá trị số cộng đồng** và **không assert số tin** ở TC completeness (xem `CHANGELOG §2`).
