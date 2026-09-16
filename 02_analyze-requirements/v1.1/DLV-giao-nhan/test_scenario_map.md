---
id: v1.1/DLV-giao-nhan/scenario-map
title: Test Scenario Map — v1.1 · Module DLV
type: scenario-map
version: v1.1
sprint: 1
module: DLV
counts:
  req: 23
  sc: 64
  new: 34
  modified: 0
  carried: 30
  deprecated: 0
  p1: 10
  p2: 42
  p3: 12
status: ANALYZED
updated: 2026-09-15
---

# Test Scenario Map — v1.1 · Module DLV

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module DLV **tính tới v1.1** (bao gồm CARRIED từ v1.0).
> Parent: `v1.0/DLV-giao-nhan/` — 30 SC không đổi (CARRIED), 3 SC MODIFIED-context (REQ giữ ID, SC mới gắn REQ đó — xem ghi chú per REQ), 31 SC NEW.

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Delta lần này fan-out theo: nhóm trạng thái mới của state machine (bundle theo hàng bảng PRD, không atomize khi PRD chỉ cho mô tả cấp danh mục) · 4 loại đối tượng nhận · nhánh ưu tiên xử lý không liên lạc được · 2 chế độ cầm hàng về · 6 mẫu câu nhật ký (gộp cặp) · NFR riêng lẻ theo phương pháp đo.

## Tổng quan
- Tổng số scenarios (tính tới v1.1): **64** (NEW: 31, MODIFIED-context: 3 SC mới gắn REQ giữ ID, CARRIED: 30)
- Phân bổ priority: P1: 9 | P2: 33 | P3: 22
- Delta lớn nhất: **`SC-DLV-037..042`** — màn Carrier "Xác nhận giao hàng" (`FR07`) mở rộng từ 1 nút + popup đơn giản sang form đầy đủ 4 loại đối tượng nhận. ⚠️ Không liên quan `C-DLV-03` (CL đó thuộc màn Receiver khác, `FR10`, không đổi). Rủi ro cao: app STG có thể chưa build lại theo PRD mới (`RISK-DLV-08`).

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### DLV — Giao nhận & Theo dõi đơn (delta v1.1)

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-DLV-031 | Ma trận mở rộng — RESCHEDULED | REQ-DLV-002 | DOC-v1.1-01 §8.12.3 | Đơn ở RESCHEDULED (đã hẹn giao lại) | Mở màn theo dõi đơn với từng vai | Sender thấy "Xem lịch hẹn giao lại"; Carrier thấy "Giao lại theo lịch (mở lại màn giao hàng)"; Receiver thấy "Xem lịch hẹn" | P2 | UI | NEW |
| SC-DLV-032 | Ma trận mở rộng — RETURNING | REQ-DLV-002 | DOC-v1.1-01 §8.12.3 | Đơn ở RETURNING (đang hoàn hàng) | Mở màn theo dõi đơn với từng vai | Sender thấy "Xác nhận đã nhận lại hàng" + xem lịch hẹn; Carrier thấy "Xem lịch hẹn trả hàng"; Receiver thấy "Xem lý do hoàn hàng" | P2 | UI | NEW |
| SC-DLV-033 | Ma trận mở rộng — nhóm đóng (RETURNED/CANCELLED/EXPIRED) | REQ-DLV-002 | DOC-v1.1-01 §8.12.3 | Đơn ở 1 trong 3 trạng thái RETURNED / CANCELLED / EXPIRED | Mở màn theo dõi đơn với từng vai | Sender thấy "Xem lý do · đăng lại"; Carrier thấy "Xem lý do"; Receiver thấy "Xem lý do" — giống nhau cho cả 3 trạng thái | P3 | UI | NEW |
| SC-DLV-034 | Đơn INCIDENT không tự về COMPLETED | REQ-DLV-007 | DOC-v1.1-01 §8.10.1 BR10-04 | Đơn đã chuyển sang INCIDENT (báo sự cố sau IN_TRANSIT) | Chờ qua các mốc thời gian bình thường (2h/4h) mà không có thao tác admin | Đơn KHÔNG tự chuyển COMPLETED dù đã qua mốc thời gian; chỉ chuyển khi admin xử lý dựa trên nhật ký + ảnh | P2 | Business Rule | NEW |
| SC-DLV-035 | Ảnh lúc lấy hàng — có đính ảnh | REQ-DLV-012 | DOC-v1.1-01 §8.6.1 BR06-01 | Đơn ở MATCHED, Carrier chuẩn bị bấm "Tôi đã lấy hàng" | Đính 1-5 ảnh trước khi xác nhận | Xác nhận thành công; ảnh được lưu kèm mốc "Tôi đã lấy hàng"; đơn chuyển IN_TRANSIT | P3 | Functional | NEW |
| SC-DLV-036 | Ảnh lúc lấy hàng — bỏ trống (tuỳ chọn) | REQ-DLV-012 | DOC-v1.1-01 §8.6.1 BR06-01 | Đơn ở MATCHED | Bấm "Tôi đã lấy hàng" KHÔNG đính ảnh nào | Xác nhận vẫn thành công (ảnh là tuỳ chọn, không phải điều kiện bắt buộc) | P3 | Boundary | NEW |
| SC-DLV-037 | Xác nhận giao hàng — happy path "Người nhận" | REQ-DLV-017 | DOC-v1.1-01 §8.7.2 | Đơn ở IN_TRANSIT, Carrier mở màn "Xác nhận giao hàng" | Chọn đối tượng nhận = "Người nhận", đính ≥1 ảnh, bấm xác nhận và đồng ý popup | Đơn chuyển DELIVERED; nhật ký ghi "Đã giao tận tay người nhận"; NTF-05 gửi cho Receiver | P1 | Functional | NEW |
| SC-DLV-038 | Xác nhận giao hàng — "Người được uỷ quyền" | REQ-DLV-017 | DOC-v1.1-01 §8.7.1 BR07-03, BR07-04, BR07-05 | Đơn ở IN_TRANSIT | Chọn "Người được uỷ quyền", nhập tên (2-60 ký tự, bắt buộc), SĐT (khuyến nghị), đính ≥1 ảnh, xác nhận | Trường "Uỷ quyền bởi" tự sinh = "Người nhận" (vì đến từ màn Xác nhận giao hàng), chỉ đọc; đơn chuyển DELIVERED; nhật ký ghi tên/SĐT người nhận thay + "uỷ quyền bởi Người nhận" | P1 | Business Rule | NEW |
| SC-DLV-039 | Xác nhận giao hàng — gửi quầy (lễ tân/bảo vệ) | REQ-DLV-017 | DOC-v1.1-01 §8.7.1 BR07-03 | Đơn ở IN_TRANSIT | Chọn "Quầy lễ tân" (hoặc "Quầy bảo vệ"), nhập tên người trực (bắt buộc, không chấp nhận ghi chung chung kiểu "quầy lễ tân"), đính ≥1 ảnh, xác nhận | Đơn chuyển DELIVERED; nhật ký ghi "Đã gửi tại quầy lễ tân — {tên}" (hoặc quầy bảo vệ tương ứng) | P2 | Business Rule | NEW |
| SC-DLV-040 | Xác nhận giao hàng — ảnh bắt buộc ≥1, nút disable | REQ-DLV-017 | DOC-v1.1-01 §8.7.1 BR07-02 | Đơn ở IN_TRANSIT, đã chọn đối tượng nhận nhưng CHƯA đính ảnh | Quan sát nút xác nhận | Nút xác nhận vô hiệu hoá; chỉ bật khi có ≥1 ảnh (tối đa 5) | P2 | Boundary | NEW |
| SC-DLV-041 | Ảnh bằng chứng không xoá được sau khi ghi mốc | REQ-DLV-017 | DOC-v1.1-01 §8.7.1 BR07-07 | Đơn đã DELIVERED, có ảnh bằng chứng đã ghi | Cố xoá ảnh từ màn theo dõi đơn | KHÔNG xoá được — ảnh đã gắn vào mốc nhật ký là bất biến | P2 | Business Rule | NEW |
| SC-DLV-042 | Popup xác nhận nêu hệ quả trước khi ghi mốc | REQ-DLV-017 | DOC-v1.1-01 §8.7.1 BR07-06 | Đã điền đủ điều kiện màn Xác nhận giao hàng | Bấm xác nhận | Popup hiện nêu rõ hệ quả (không thể hoàn tác) trước khi ghi mốc thật; bấm Huỷ ở popup → KHÔNG đổi trạng thái | P2 | Business Rule | NEW |
| SC-DLV-043 | Không liên lạc được — thứ tự ưu tiên 4 nhánh | REQ-DLV-018 | DOC-v1.1-01 §8.8.1 BR08-02 | Đơn ở IN_TRANSIT, Carrier bấm "Không liên lạc được người nhận?" | Quan sát thứ tự các lựa chọn hiển thị trên màn | Đúng thứ tự: (1) giao cho người uỷ quyền đã khai sẵn (nếu có) → (2) liên hệ người gửi xin uỷ quyền → (3) gửi quầy lễ tân/bảo vệ → (4) cầm hàng về. ⚠️ **2026-09-16:** `AC-16.1.01` (modal 2 hướng) và `AC-17.1.01` (bảo vệ trước lễ tân) mô tả khác — **chờ `C-DLV-06`**, tới lúc đó chỉ GHI NHẬN cấu trúc thật | P2 | UI | NEW |
| SC-DLV-044 | Liên hệ người gửi xin uỷ quyền | REQ-DLV-018 | DOC-v1.1-01 §8.8.1 BR08-03 | Từ luồng không liên lạc được, chọn "Liên hệ người gửi" | Mở màn "Liên hệ người gửi" | Ô tên/SĐT người nhận thay ĐỂ TRỐNG (không prefill); dòng "Uỷ quyền bởi: Người gửi"; ảnh bắt buộc; hiển thị SĐT người gửi có nút Gọi | P2 | Business Rule | NEW |
| SC-DLV-045 | Gửi quầy từ luồng không liên lạc được | REQ-DLV-018 | DOC-v1.1-01 §8.8.1 BR08-04 | Từ luồng không liên lạc được, chọn "Gửi tại quầy" | Nhập tên người trực quầy + ≥1 ảnh, xác nhận popup | Đơn chuyển DELIVERED qua nhánh này; bắt buộc đủ ảnh + tên, có popup xác nhận trước khi ghi | P2 | Business Rule | NEW |
| SC-DLV-046 | Không ai ở quầy — buộc chuyển "Cầm hàng về" | REQ-DLV-018 | DOC-v1.1-01 §8.8.1 BR08-07 | Từ luồng gửi quầy, không có ai để ghi tên người trực | Cố xác nhận mà không nhập được tên | KHÔNG xác nhận được ở nhánh gửi quầy; hệ thống buộc chuyển hướng sang "Cầm hàng về" | P3 | Negative | NEW |
| SC-DLV-047 | Cờ "không liên lạc được" hiện cảnh báo trong nhật ký cho cả 3 bên | REQ-DLV-018 | DOC-v1.1-01 §8.8.1 BR08-05 | Đơn đã đi qua luồng không liên lạc được (bất kỳ nhánh nào) | Mở block LỊCH SỬ ở cả 3 vai (Sender/Carrier/Receiver) | Cả 3 vai đều thấy cảnh báo "không liên lạc được người nhận" gắn với mốc tương ứng | P3 | Functional | NEW |
| SC-DLV-048 | Thời hạn giữ hàng tại quầy — 4h nhắc, 24h chuyển admin | REQ-DLV-018 | DOC-v1.1-01 §8.8.1 BR08-06 | Đơn đã gửi tại quầy, chưa được Receiver xác nhận | Chờ 4 giờ, sau đó tới cuối ngày, sau đó 24 giờ | Sau 4h: nhắc Receiver. Cuối ngày: nhắc lần 2. Sau 24h chưa xác nhận: chuyển admin hỗ trợ — GHI DẠNG DEFERRED, cần tiền đề thời gian thực (cùng nhóm khó như `RISK-DLV-04` cũ); chưa chạy đủ mốc thì GHI RÕ, không khai coverage | P3 | Business Rule | NEW |
| SC-DLV-049 | Cầm hàng về — chọn chế độ + field lịch hẹn | REQ-DLV-019 | DOC-v1.1-01 §8.9.2 BR09-02, BR09-03, BR09-04 | Carrier chọn "Cầm hàng về" | Chọn chế độ (retry/return), nhập ngày hẹn (≤+7 ngày), giờ từ-đến (đến > từ, tối thiểu 30 phút), nơi hẹn | Nhãn tiêu đề/địa điểm đổi theo chế độ ("Hẹn giao lại · Nơi giao lại" / "Hẹn trả hàng · Nơi nhận lại hàng"); validate đúng ràng buộc giờ + ngày | P2 | Boundary | NEW |
| SC-DLV-050 | Chế độ retry — quay lại IN_TRANSIT theo lịch hẹn | REQ-DLV-019 | DOC-v1.1-01 §8.9.1 BR09-05 | Đơn ở RESCHEDULED, đã tới lịch hẹn giao lại | Carrier mở lại màn giao hàng theo lịch | Đơn quay lại IN_TRANSIT; giao lại theo đúng luồng `REQ-DLV-017` (FR07). ⚠️ **2026-09-16:** tự chuyển đúng giờ hay Carrier bấm — **chờ `C-DLV-05`** | P2 | Functional | NEW |
| SC-DLV-051 | Chế độ return — Sender xác nhận nhận lại → RETURNED | REQ-DLV-019 | DOC-v1.1-01 §8.9.1 BR09-06 | Đơn ở RETURNING | Sender bấm "Xác nhận đã nhận lại hàng" | Đơn chuyển RETURNED (đóng) | P2 | Functional | NEW |
| SC-DLV-052 | RETURNED — không mở tặng quà, không cộng "Đơn đã giúp" | REQ-DLV-019 | DOC-v1.1-01 §8.9.1 BR09-06 | Đơn vừa chuyển RETURNED | Kiểm tra màn Sender (bước tặng quà) và chỉ số "Đơn đã giúp" của Carrier | KHÔNG mở bước tặng quà cho Sender (khác COMPLETED); chỉ số "Đơn đã giúp" của Carrier KHÔNG tăng; đơn vẫn xuất hiện trong lịch sử/Hoạt động | P1 | Business Rule | NEW |
| SC-DLV-053 | Người nhận từ chối nhận hàng → return + lý do | REQ-DLV-019 | DOC-v1.1-01 §8.9.1 BR09-07 | Carrier tới nơi giao, Receiver từ chối nhận hàng | Carrier chọn chế độ `return`, ghi lý do vào ghi chú | Đơn đi theo luồng return; nhật ký/ghi chú lưu đúng lý do từ chối đã nhập | P2 | Business Rule | NEW |
| SC-DLV-054 | Quá lịch hẹn 24h chưa đóng → chuyển admin | REQ-DLV-019 | DOC-v1.1-01 §8.9.1 BR09-04 | Đơn ở RESCHEDULED hoặc RETURNING, đã quá lịch hẹn | Chờ thêm 24 giờ mà đơn chưa đóng | Chuyển admin hỗ trợ — GHI DẠNG DEFERRED, cần tiền đề thời gian thực; chưa chạy đủ mốc thì GHI RÕ | P3 | Business Rule | NEW |
| SC-DLV-055 | Nhật ký — giao tận tay / uỷ quyền (2 mẫu câu) | REQ-DLV-020 | DOC-v1.1-01 §8.12.4 | Đơn đã DELIVERED qua 2 nhánh: giao trực tiếp Receiver, và giao qua người uỷ quyền | Mở block LỊCH SỬ | Dòng log đúng verbatim: "Đã giao tận tay người nhận" (nhánh 1); "Đã giao cho người được uỷ quyền — {tên · SĐT} — uỷ quyền bởi {người gửi/người nhận}" (nhánh 2) | P2 | Functional | NEW |
| SC-DLV-056 | Nhật ký — 2 quầy (2 mẫu câu) | REQ-DLV-020 | DOC-v1.1-01 §8.12.4 | Đơn đã DELIVERED qua gửi quầy lễ tân, và qua gửi quầy bảo vệ | Mở block LỊCH SỬ | Dòng log đúng verbatim: "Đã gửi tại quầy lễ tân — {tên người trực quầy}"; "Đã gửi tại quầy bảo vệ — {tên người trực}" | P2 | Functional | NEW |
| SC-DLV-057 | Nhật ký — cầm hàng về / trả người gửi (2 mẫu câu) | REQ-DLV-020 | DOC-v1.1-01 §8.12.4 | Đơn ở RESCHEDULED, và đơn ở RETURNED | Mở block LỊCH SỬ | Dòng log đúng verbatim: "Cầm hàng về — hẹn giao lại {ngày · giờ · nơi hẹn}"; "Đã trả lại người gửi". Mọi dòng đều kèm thời điểm + cờ không liên lạc (nếu có) + dấu hiệu có ảnh bằng chứng | P2 | Functional | NEW |
| SC-DLV-058 | Chặn transition không hợp lệ (API-level) | REQ-DLV-021 | DOC-v1.1-01 §8.12.1 BR12-01 | Đơn ở 1 trạng thái bất kỳ (vd POSTED) | Gửi request trực tiếp yêu cầu chuyển sang trạng thái không nằm trong danh sách transition hợp lệ của bảng `§8.12.2` (vd POSTED → DELIVERED) | Request bị từ chối; KHÔNG ghi mốc mới; trạng thái đơn không đổi | P1 | Backend | NEW |
| SC-DLV-059 | Không nhảy bậc — mở rộng sang trạng thái hậu-FR09 | REQ-DLV-021 | DOC-v1.1-01 §8.12.1 BR12-02 | Đơn ở IN_TRANSIT | Cố chuyển thẳng sang RETURNED hoặc COMPLETED mà chưa qua RESCHEDULED/RETURNING/DELIVERED tương ứng | Không thực hiện được — không có đường tắt bỏ qua bước trung gian | P1 | Backend | NEW |
| SC-DLV-060 | Admin can thiệp cũng được ghi log | REQ-DLV-021 | DOC-v1.1-01 §8.12.1 BR12-07 | Đơn đang ở trạng thái cần admin hỗ trợ (vd INCIDENT quá hạn) | Admin thực hiện can thiệp (ngoài phạm vi test — Admin Portal out of scope `C-TS-01`) | GHI NHẬN hệ quả quan sát được phía end-user: có dòng log mới xuất hiện tương ứng với can thiệp — KHÔNG verify được thao tác Admin thật | P3 | Business Rule | NEW |
| SC-DLV-061 | Upload 5 ảnh bằng chứng < 15s (p95) | REQ-DLV-022 | DOC-v1.1-01 §9 NFR-03 | Mạng 4G, đang ở màn xác nhận giao hàng | Tải 5 ảnh, mỗi ảnh ≤5MB | Hoàn tất < 15 giây (p95); có chỉ báo tiến trình; cho phép thử lại từng ảnh riêng lẻ nếu lỗi | P3 | Performance | NEW |
| SC-DLV-062 | Log append-only — không API sửa/xoá | REQ-DLV-022 | DOC-v1.1-01 §9 NFR-07 | Đơn đã có ≥1 mốc nhật ký + ảnh bằng chứng | Thử gọi API sửa/xoá bản ghi nhật ký hoặc ảnh đã ghi (code review + security test) | KHÔNG có API nào cho phép — nếu phát hiện có (như bug hiện tại "huỷ nhận đơn xoá dòng Ghép thành công", cross-ref `RISK-TS-01`) thì đây là vi phạm NFR-07 nghiêm trọng | P1 | Security | NEW |
| SC-DLV-063 | Dữ liệu người nhận thay không xuất hiện ngoài nhật ký đơn | REQ-DLV-022 | DOC-v1.1-01 §9 NFR-12 | Đơn đã có tên/SĐT người nhận thay trong nhật ký | Rà mọi màn báo cáo/thống kê trong scope end-user | Tên/SĐT người nhận thay CHỈ xuất hiện ở nhật ký đơn — GHI NHẬN không thấy màn báo cáo nào khác chứa dữ liệu này (không có bề mặt báo cáo trong scope end-user để test thêm) | P3 | Privacy | NEW |
| SC-DLV-064 | Icon copy nhanh SĐT/địa chỉ ở màn Theo dõi đơn | REQ-DLV-023 | DOC-v1.1-01 §8.18.1 BR18-04 | Màn theo dõi đơn đang hiện SĐT/địa chỉ liên hệ | Bấm icon copy cạnh SĐT hoặc địa chỉ | Nội dung được copy vào bộ nhớ tạm thiết bị; icon đổi trạng thái + màu xanh trong khoảng 1,8 giây rồi trở lại bình thường | P3 | UI | NEW |

#### Source Detail per Scenario (verbatim quotes)

> Ghi chú chung: mọi Source Quote dưới đây trích lại đúng câu đã dẫn ở `requirement_traceability.md §2` cho REQ tương ứng — không diễn giải lại. Analyst Note ở đây tập trung vào **quyết định fan-out/bundle**, không lặp phân tích nghiệp vụ đã có ở traceability.

##### SC-DLV-031/032/033 — Ma trận mở rộng 3 nhóm trạng thái
**Source Quote:** xem `requirement_traceability.md REQ-DLV-002` (bảng `§8.12.3`, 3 hàng RESCHEDULED/RETURNING/nhóm đóng).
**Source Location:** `DOC-v1.1-01 §8.12.3 · trang 45-46`
**Analyst Note:** Bundle theo hàng bảng (1 SC = 1 nhóm trạng thái, 3 nhánh vai trong Then) vì PRD chỉ cho mô tả cấp danh mục, không có microcopy Figma-verified như 15 ô gốc — atomize thêm sẽ tạo SC không có oracle mạnh hơn bundle.

##### SC-DLV-034 — Đơn INCIDENT không tự COMPLETED
**Source Quote:** "BR10-04 | Đơn có báo cáo sự cố (INCIDENT) không tự chuyển về COMPLETED — phải qua admin hỗ trợ dựa trên nhật ký và ảnh."
**Source Location:** `DOC-v1.1-01 §8.10.1 BR10-04 · trang 43`
**Analyst Note:** SC mới gắn `REQ-DLV-007` (giữ ID) — không sửa `SC-DLV-024` cũ (vẫn đúng cho nhánh DELIVERED thường), chỉ thêm nhánh INCIDENT.

##### SC-DLV-035/036 — Ảnh lúc lấy hàng
**Source Quote:** "BR06-01 | Ảnh lúc lấy hàng là tuỳ chọn nhưng được khuyến nghị mạnh; tối đa 5 ảnh."
**Source Location:** `DOC-v1.1-01 §8.6.1 BR06-01 · trang 38`
**Analyst Note:** Resolve gap `PUP-03` cũ — 2 SC (có ảnh / không ảnh) đủ phủ vì rule chỉ có 1 điều kiện (tuỳ chọn), không cần thêm boundary số lượng riêng (dùng chung trần 5 với `BR18-01`, đã test ở `SC-TS-011`/tương đương cho form khác — không lặp SC biên số lượng ở đây).

##### SC-DLV-037..042 — Xác nhận giao hàng (Carrier, FR07 mở rộng)
**Source Quote:** xem `requirement_traceability.md REQ-DLV-017` (BR07-01..07 đầy đủ).
**Source Location:** `DOC-v1.1-01 §8.7, §8.7.1, §8.7.3 · trang 39-41`
**Analyst Note:** `risk_assessment.md RISK-DLV-08` nay **Confirmed qua demo (2026-09-16)** — cấu trúc form + luồng submit end-to-end (đính ảnh, chọn "Giao cho", chuyển DELIVERED) đều chạy đúng. Vẫn khuyến nghị 1 lượt xác nhận nhanh trên STG thật trước khi hardening automation locator, nhưng không còn là rủi ro cao chặn generate-tc. Không liên quan `C-DLV-03` (màn Receiver khác, xem `SC-DLV-025`).

##### SC-DLV-043..048 — Không liên lạc được người nhận
**Source Quote:** xem `requirement_traceability.md REQ-DLV-018` (BR08-01..07 đầy đủ).
**Source Location:** `DOC-v1.1-01 §8.8, §8.8.1, §8.8.2 · trang 41-42`
**Analyst Note:** `SC-DLV-048` cùng nhóm tiền đề khó với `RISK-DLV-04` cũ (`SC-DLV-024`, cần chờ giờ thật hoặc seed timestamp) — gộp kế hoạch chạy nếu có thể.

##### SC-DLV-049..054 — Cầm hàng về
**Source Quote:** xem `requirement_traceability.md REQ-DLV-019` (BR09-01..07 đầy đủ).
**Source Location:** `DOC-v1.1-01 §8.9, §8.9.1, §8.9.2 · trang 42-43`
**Analyst Note:** `SC-DLV-052` (P1) là oracle bảo vệ ranh giới `RETURNED` ⟷ `COMPLETED` — dễ bị lập trình sai nhất (nhầm coi return như 1 dạng hoàn thành). Ưu tiên chạy sớm.

##### SC-DLV-055..057 — Nhật ký phân nhánh
**Source Quote:** xem `requirement_traceability.md REQ-DLV-020` (bảng `§8.12.4` đầy đủ 6 mẫu câu + dòng "Mọi dòng").
**Source Location:** `DOC-v1.1-01 §8.12.4 · trang 46`
**Analyst Note:** Mẫu câu là verbatim string — `generate-tc` nên assert nguyên văn, không paraphrase, kể cả dấu gạch ngang và ngoặc nhọn `{}` đại diện biến.

##### SC-DLV-058..060 — State machine transitions
**Source Quote:** xem `requirement_traceability.md REQ-DLV-021` (BR12-01, 02, 03, 07).
**Source Location:** `DOC-v1.1-01 §8.12.1 · trang 44-45`
**Analyst Note:** `SC-DLV-058`/`059` là **API-level test** (bypass UI) — khác `SC-DLV-004`/`REQ-DLV-004` (v1.0, chỉ verify UI không cho nhảy bước qua ma trận nút). Cả 2 tầng đều cần test độc lập vì UI chặn không đảm bảo backend cũng chặn.

##### SC-DLV-061..063 — NFR hiệu năng/bảo mật/privacy
**Source Quote:** xem `requirement_traceability.md REQ-DLV-022` (NFR-03, NFR-07, NFR-12).
**Source Location:** `DOC-v1.1-01 §9 · trang 53-54`
**Analyst Note:** `SC-DLV-062` (P1) là SC quan trọng nhất của cả lượt delta này về mặt rủi ro nghiệp vụ — trực tiếp đối chiếu với bug đã biết ở `RISK-TS-01`/`KP-05 §5`. Nếu chưa fix, SC này **dự kiến FAIL có chủ đích** (giống pattern `SC-TS-003` ở v1.0).

##### SC-DLV-064 — Icon copy nhanh
**Source Quote:** "BR18-04 | Icon copy đặt cạnh địa chỉ giao và số điện thoại ở màn chi tiết tin và màn theo dõi đơn; sau khi copy, icon đổi trạng thái và màu xanh trong khoảng 1,8 giây."
**Source Location:** `DOC-v1.1-01 §8.18.1 BR18-04 · trang 52`
**Analyst Note:** Chỉ phủ instance màn Theo dõi đơn (`DLV`); instance màn Chi tiết tin thuộc `FEED`, chưa rà lại lượt này.

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| SC-DLV-001..015 | Ma trận nhãn nút × 5 trạng thái × 3 vai (15 ô) | DLV | v1.0 | P1-P3 | → `v1.0/DLV-giao-nhan/test_scenario_map.md` |
| SC-DLV-016 | Thanh 5 mốc trạng thái | DLV | v1.0 | P2 | → xem v1.0 |
| SC-DLV-017..020 | Popup xác nhận (4 SC) | DLV | v1.0 | P2 | → xem v1.0 |
| SC-DLV-021 | Không bỏ qua bước "Tôi đã lấy hàng" | DLV | v1.0 | P1 | → xem v1.0 |
| SC-DLV-022 | Chỉ Receiver xác nhận "Đã nhận hàng" | DLV | v1.0 | P1 | → xem v1.0 |
| SC-DLV-023 | Xác nhận → "Hoàn thành" ngay | DLV | v1.0 | P2 | → xem v1.0 |
| SC-DLV-024 | Mốc 2h/4h nhắc → admin (nhánh thường) | DLV | v1.0 | P3 | → xem v1.0 |
| SC-DLV-025 | Modal xác nhận "Đã nhận hàng" đơn giản (Receiver, FR10) | DLV | v1.0 | P2 | → xem v1.0 — không đổi, khác màn Carrier "Xác nhận giao hàng" (`FR07`/`REQ-DLV-017`, xem `RISK-DLV-08`) |
| SC-DLV-026..028 | Cụm liên hệ theo vai (3 SC) | DLV | v1.0 | P2 | → xem v1.0 |
| SC-DLV-029 | Lịch sử timeline mốc sự kiện (chung) | DLV | v1.0 | P2 | → xem v1.0 |
| SC-DLV-030 | Nhãn phụ màn Theo dõi đơn theo vai | DLV | v1.0 | P3 | → xem v1.0 |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
