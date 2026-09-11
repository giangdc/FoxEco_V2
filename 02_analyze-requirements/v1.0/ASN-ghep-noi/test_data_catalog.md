# Test Data Catalog — v1.0 · Module ASN

> Tạo bởi: analyze-requirements (**stage: analyze**).
> **Structure-lock:** giữ nguyên 6 cột `| Field | Loại data | Valid | Invalid | Boundary | Nguồn |`.

## Module ASN — Ghép nối (DOC-v1.0-01 §A5/§D3/§D4/§D7 · DOC-v1.0-06)

| Field | Loại data | Valid | Invalid | Boundary | Nguồn |
|-------|-----------|-------|---------|----------|-------|
| Trạng thái tin trước khi ghép | Fixture | `POSTED` (Chờ ghép) | `MATCHED` · `IN_TRANSIT` · `EXPIRED` · `CANCELLED` (không ghép được) | **`POSTED` → `MATCHED` = transition duy nhất của module** | `OPR-03` L339 · `OPR-08` L344 |
| Quan hệ Carrier ↔ tin | Fixture | Carrier **khác** chủ tin và khác Người nhận | Carrier **là chủ tin** (→ `OPR-05` cấm) · Carrier là Người nhận của đơn | **Carrier là Người nhận được khai** — chủ thể thứ ba, chỉ `§7 dòng 9` nhắc | `OPR-05` L341 · `DOC-v1.0-02` §7 dòng 9 |
| Số Carrier cùng bấm nhận | Runtime | 1 Carrier | — | **2 Carrier bấm gần đồng thời → chỉ 1 người ghép** (`SC-ASN-006`) | `ASN-03` L249 · `OPR-03` L339 |
| SĐT trong cặp ghép | Runtime | lộ cho **đúng 2 người trong cặp** sau `MATCHED`; Carrier thấy cả SĐT Người nhận (`US-D08`) | lộ cho người thứ ba · lộ trước khi ghép (→ bug, xem `SC-FEED-010`) | **ranh giới `POSTED` → `MATCHED` = thời điểm được phép lộ** | `BR-CON-02` L78 · `OPR-07` L343 · `US-D08` L177 |
| Điểm lấy hàng (khớp tuyến) | Fixture | **trùng đúng địa chỉ đã chọn** giữa tin NEED và tuyến OFFER | địa chỉ khác | ⛔ **KHÔNG dùng bán kính GPS / khoảng cách** (`KB-ASN-04`) ⇒ khớp là **nhị phân** | `OPR-02` L338 · KP-01 §4 KB-ASN-04 |
| Điểm giao hàng (khớp tuyến) | Fixture | trùng đúng địa chỉ đã chọn | địa chỉ khác | như trên | `BR-MTCH-01` L270 · `OPR-02` L338 |
| Khung giờ (khớp tuyến) | Fixture | 2 khung **giao nhau** | 2 khung **tách rời hoàn toàn** (vd 08:00–09:00 vs 20:00–21:00) | ⚠ **biên "giao nhau bao nhiêu là đủ" CHƯA CHỐT** (`C-NTF-02`) ⇒ ⛔ không test độ lệch | `OPR-02` L338 · KP-01 §4 KB-ASN-04 |
| Số tin NEED khớp 1 tuyến OFFER | Fixture | 1..5 tin | — | **3 (dưới trần) · 5 (đúng trần) · 6 (vượt trần)** — 3 mốc **BA chốt**, không phải mock | `OPR-01` L337 · KP-01 §4 KB-ASN-03 |
| Số thông báo khớp / tin OFFER | Runtime | ≤ 5 thông báo **cho mỗi tin OFFER** | > 5 cho cùng 1 tin OFFER | **5 (trần) → tin thứ 6 KHÔNG bắn thêm**; ⛔ **KHÔNG cộng dồn theo ngày** | KP-01 §4 KB-ASN-03 (đảo `OPR-06`) |
| Thứ tự gợi ý | Runtime | mới đăng trước | — | ⚠ tiêu chí *"độ gần tuyến"* **không kiểm chứng được** (nhị phân) ⇒ chỉ còn thời gian đăng | `OPR-04` L340 |
| Tin quá hạn trong luồng khớp | Fixture | ⛔ **bị loại khỏi gợi ý** (giá trị assert-absent) | xuất hiện trong gợi ý → sai rule | **đơn có "Đến ngày" vừa trôi qua** — ⛔ không seed được qua UI | `OPR-04` L340 · `US-D04` L166 |
| Số phiên/thiết bị đồng thời | Fixture | 3 phiên (Sender · Carrier · Receiver) trên **3 thiết bị/tài khoản khác nhau** | 1 phiên đổi vai (không kiểm chứng được realtime) | **2 phiên cho `SC-ASN-006`, 3 phiên cho `SC-ASN-008`** | `DOC-v1.0-02` §4.2 · `BR-INT-05` L81 |

## Ghi chú chung
- **`Loại data`:** `Fixture` = QC tạo qua `ORD` (đăng tin NEED/OFFER) + đẩy trạng thái · `Runtime` = engine sinh (quyết định ghép, thông báo, thứ tự gợi ý).
- ⭐ **Module này KHÔNG có trường nhập nào** — mọi dữ liệu là **quan hệ giữa các đơn và tài khoản**. Chi phí thật nằm ở **số lượng tài khoản và thiết bị**: cần tối thiểu **4 tài khoản** (chủ tin A · Carrier B · Carrier C cho double-accept · người thứ ba D cho `SC-ASN-005`) và **2–3 thiết bị/phiên đồng thời**.
- ⚠️ **Biên duy nhất có giá trị BA chốt:** `3 / 5 / 6` tin cho trần gợi ý và trần thông báo (`KB-ASN-03` ghi rõ *"giá trị chốt, không phải mock"*) ⇒ dùng đúng 3 mốc này, ⛔ không tự nghĩ mốc khác.
- ⚠️ **Biên KHÔNG được test:** độ lệch khung giờ khi khớp tuyến — định nghĩa *"khung giờ phù hợp"* chưa chốt (`C-NTF-02` Partially Resolved) ⇒ chỉ dùng 2 khung **tách rời hoàn toàn** cho nhánh negative.
- **Tiền đề khó nhất:** (1) 2 Carrier bấm **gần đồng thời** — với 1 tester chỉ kiểm được nhánh tuần tự; (2) **6 tin NEED khớp cùng 1 tuyến OFFER** để chạm trần; (3) **tin quá hạn** — nhờ dev seed.
