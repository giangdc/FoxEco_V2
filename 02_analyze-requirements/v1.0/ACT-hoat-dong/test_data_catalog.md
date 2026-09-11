# Test Data Catalog — v1.0 · Module ACT

> Tạo bởi: analyze-requirements (**stage: analyze**).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.

## Module ACT — Hoạt động ("Đơn của tôi") · DOC-v1.0-02 §3.7 · DOC-v1.0-06 KP-01 §3

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Tab active | Runtime | `Đang diễn ra` (mặc định) · `Đã hoàn thành` | — | **lần đầu mở màn → phải là `Đang diễn ra`** | KP-01 §3 KB-ORD-07 (#2) |
| Đơn ở tab "Đang diễn ra" | Fixture | trạng thái `Chờ ghép` · `Đã ghép` · `Đang giao` · `Đã giao` | `Hoàn thành` · `Hết hạn` · `Đã huỷ` (không thuộc tab này) | **`Đã giao` = biên cuối của tab 1** · **`Hoàn thành` = biên đầu của tab 2** | `DOC-v1.0-02` §3.7 đoạn 2 · `§D2` L232 |
| Đơn ở tab "Đã hoàn thành" | Fixture | trạng thái `Hoàn thành` · **`Hết hạn`** | đơn đang hoạt động · `Đã huỷ` | **`Hết hạn` — dễ bị bỏ sót vì tên tab gợi ý chỉ chứa đơn thành công** | `DOC-v1.0-02` §3.7 đoạn 3 · `US-D04` L166 |
| Đơn `Đã huỷ` | Fixture | ⛔ **KHÔNG hiển thị ở cả 2 tab** (dùng làm giá trị assert-absent) | hiển thị ở bất kỳ tab nào → sai rule | — | KP-01 §3 KB-ORD-07 (#7) |
| Icon trạng thái (card) | Runtime | icon tương ứng badge trạng thái | icon lệch badge | — | KP-01 §3 KB-ORD-07 (#3) |
| Tên tin (card) | Runtime | tên tin do người đăng nhập ở `ORD` | — | **tên rất dài → tràn/cắt dòng (chưa có đặc tả)** | KP-01 §3 KB-ORD-07 (#3) |
| Tuyến "Từ → Đến" (card) | Runtime | rút gọn địa chỉ lấy → giao | — | **địa chỉ dài → cách rút gọn (chưa có đặc tả)** | KP-01 §3 KB-ORD-07 (#3) |
| Ngày (card) | Runtime | ngày của đơn | — | — (⛔ không assert định dạng — chưa có đặc tả) | KP-01 §3 KB-ORD-07 (#3) |
| Badge trạng thái (card) | Runtime | `{Chờ ghép, Đã ghép, Đang giao, Đã giao, Hoàn thành, Hết hạn}` | `Đã huỷ` (đơn bị ẩn) | **`Hết hạn` → card có thêm dòng lý do + non-clickable** | KP-01 §3 KB-ORD-07 (#3,#4,#6) |
| Dòng lý do card "Hết hạn" | Master | nguyên văn "Không có ai nhận mang giúp trong thời gian đăng — tin đã tự động đóng." | — | ⚠ `US-D04` ghi bản **ngắn hơn** (dừng ở "trong thời gian đăng") — 2 nguồn lệch phần cuối câu | KP-01 §3 KB-ORD-07 (#4) · `US-D04` L166 |
| Chuỗi "★★★★★ Đã đánh giá" | Runtime | ⚠ **UI leftover** — ghi nhận sự tồn tại, ⛔ không assert số sao | — | — | `DOC-v1.0-02` §3.7 · KP-01 §3 KB-ORD-07 ghi chú · `C-GIFT-01` |
| Số đơn trong tab | Runtime | ≥1 đơn | — | **0 đơn → empty state (chưa có đặc tả — `C-ORD-06`)** · **nhiều đơn → scroll/phân trang (chưa có đặc tả)** | `C-ORD-06` · KP-01 §8 KB-NTF-02 (tương tự màn Thông báo) |

## Ghi chú chung
- **`Loại data`:** `Fixture` = QC tạo bằng cách đăng tin + đẩy trạng thái đơn (qua `ORD`/`ASN`/`DLV`/`CNL`) · `Runtime` = app tự sinh theo trạng thái đơn · `Master` = text cố định trong app.
- ⚠️ **Module này KHÔNG có dữ liệu nhập** — toàn bộ là dữ liệu **dẫn xuất từ đơn**. Vì vậy chi phí thật của module nằm ở **thiết lập tiền đề**: để chạy đủ 14 SC cần **đồng thời** tồn tại 6 nhóm đơn: đang hoạt động (≥1), `Hoàn thành` (≥1), `Hết hạn` (≥1), `Đã huỷ` (≥1), tài khoản không có đơn đang hoạt động, tài khoản chưa có đơn kết thúc.
- **Đơn `Hết hạn` và tài khoản "trắng" là 2 tiền đề khó nhất:** `Hết hạn` cần đơn có "Đến ngày" đã trôi qua (⛔ không seed được qua UI — nhờ dev, xem `ORD-dang-tin/risk_assessment.md` `RISK-ORD-06`); tài khoản "trắng" cần tài khoản chưa từng đăng/nhận đơn nào.
- ⛔ **Không assert** định dạng ngày, cách rút gọn địa chỉ dài, và giá trị dữ liệu trong ảnh `DOC-v1.0-05` (ảnh là **mockup Apple status bar "9:41"**, không phải máy thật).
