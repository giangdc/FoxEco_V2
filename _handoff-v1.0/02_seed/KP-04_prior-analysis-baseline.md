# KP-04 — Baseline phân tích đợt cũ (⛔ REFERENCE-ONLY)

> ## ⛔ ĐỌC TRƯỚC KHI DÙNG
>
> File này là **kết quả suy luận của đợt phân tích cũ** (bộ skill v1.0, layout flat), KHÔNG phải tài liệu yêu cầu.
>
> **KHÔNG** dùng làm nguồn trích dẫn requirement. **KHÔNG** copy scenario từ đây sang project mới.
> Copy ngược từ file này = tái tạo luôn cả sai sót của đợt cũ (điển hình: toàn bộ TC ghi chip *"Tài liệu"* trong khi app thật là *"Giấy tờ, hồ sơ"* — xem `KP-01 §10.2`).
>
> **Dùng đúng cách:** sau khi `analyze-requirements` ở project mới chạy XONG, mở file này ra **đối chiếu coverage** — scenario nào đợt cũ có mà đợt mới thiếu thì rà lại xem có bỏ sót thật không.

---

## 1. Số liệu tổng quan đợt cũ (chốt 2026-07-30)

| Hạng mục | Số lượng |
|---|---|
| Requirement | **46** |
| Scenario | **92** (91 còn hiệu lực + 1 DEPRECATED `SC-NTF-006`) — P1: 20 · P2: 42 · P3: 29 |
| Test case | **323** / 9 sheet chức năng |
| Clarification | 25 |
| Coverage | **85/92 scenario có TC** (92,4%) |
| TC Review score | **84/100 CONDITIONAL** (0 Critical · 2 Major · 10 Minor · 6 Info — đã fix hết 12 finding) |

### 1.1 Phân bổ theo module

| Module | Req | Tổng SC | P1 | P2 | P3 | Risk |
|---|---:|---:|---:|---:|---:|---|
| USR | 5 | 7 | 1 | 4 | 2 | Low |
| ORD | 15 | 33 | 5 | 18 | 10 | Medium |
| ASN | 10 | 14 | 7 | 5 | 2 | **High** |
| DLV | 6 | 14 | 5 | 4 | 5 | Medium |
| GIFT | 3 | 7 | 0 | 2 | 5 | Low |
| CNL | 3 | 5 | 2 | 3 | 0 | Low |
| NTF | 2 | 9 | 0 | 4 | 4 | Medium |
| TS | 2 | 3 | 0 | 2 | 1 | Low |
| **Tổng** | **46** | **92** | **20** | **42** | **29** | |

### 1.2 Phân bổ test case theo sheet

| Mã CN | Module / Màn hình | Số TC |
|---|---|---:|
| TC_01 | Hoạt động | 20 |
| TC_02 | Cá nhân | 17 |
| TC_03 | Thông báo | 27 |
| TC_04 | Đăng tin | 109 |
| TC_05 | Trang chủ | 32 |
| TC_06 | Bảng tin & Chi tiết tin | 31 |
| TC_07 | Theo dõi đơn | 44 |
| TC_08 | Huỷ đơn | 27 |
| TC_09 | Tặng quà | 16 |
| | **Tổng** | **323** |

> File TC đợt cũ: `03_test-cases/v1.0/ISC_FoxEco_v1.0_TC_v1_R1.xlsx` (template ISC SDLC 42 cột, multi-round R1–R5). Alias: `TC-MASTER-v1.0.xlsx`, `TC-MASTER-LATEST.xlsx`.

### 1.3 Kỹ thuật thiết kế TC đã dùng
Toàn bộ 9 module chạy `--mode comprehensive` với rubric 8 kỹ thuật `B1..B8`:
`B1` Equivalence Partitioning (chiếm ~50%) · `B2` Boundary Value Analysis · `B3` Decision Table · `B4` State Transition · `B5` Pairwise · `B6` Error Guessing · `B7` CRUD Matrix · `B8` Cause-Effect Graph.
Mỗi module có 1 sheet `Coverage Matrix` (heatmap kỹ thuật × scenario).

### 1.4 7 scenario KHÔNG có TC — đều có lý do chính đáng
| Lý do | Ghi chú |
|---|---|
| Out of scope v1.0 | Các scenario thuộc clarification đã deferred |
| Chờ PM chốt scope auto-match | Xem `KP-03 §3` câu hỏi treo #3 |
| SSO thuộc host app FoxPro | Không test được từ phía SDK |
| DEPRECATED | `SC-NTF-006` (thay bằng `SC-ASN-013`) |

---

## 2. Inventory Requirement (46)

| REQ ID | Maps (Ref DOC) | §Section | Scenarios |
|---|---|---|---|
| REQ-USR-001 | USR-01 | §A6 | SC-USR-001 | — |
| REQ-USR-002 | USR-02 | §A6 | SC-USR-002 | — |
| REQ-USR-003 | USR-04 | §A6 | SC-USR-003 | — |
| REQ-USR-004 | USR-05 | §A6, §A7 + DOC-v1.0-04 | SC-USR-004, SC-USR-006, SC-USR-007 | C-USR-01 (Resolved — Deferred, 2026-07-27) |
| REQ-USR-005 | USR-07 | §A6 | SC-USR-005 | C-USR-02 (Resolved — Deferred, 2026-07-27) |
| REQ-ORD-001 | ORD-01 | §D3 + DOC-v1.0-04 | SC-ORD-001, SC-ORD-002, SC-ORD-003 | C-ORD-05 |
| REQ-ORD-002 | ORD-02 | §D3 | SC-ORD-001, SC-ORD-002, SC-ORD-007 | C-ORD-01 (Resolved, 2026-07-27) |
| REQ-ORD-003 | ORD-04 | §D3 | SC-ORD-004 | — |
| REQ-ORD-004 | ORD-06, US-D04 | §D3, §D1b | SC-ORD-005 | C-ORD-03 (Resolved, 2026-07-27) |
| REQ-ORD-005 | ORD-09 | §D3 | SC-ORD-006 | — |
| REQ-ORD-006 | ORD-10, BR-EDIT-01, OPR-10 | §D3, §D4, §D7 | SC-ORD-008, SC-ORD-009 | — |
| REQ-ORD-007 | LOC-03 | §D3 | SC-ORD-010 | — |
| REQ-ORD-008 | USR-EML, US-D18 | §D3, §D1b | SC-ORD-011, SC-ORD-012 | — |
| REQ-ORD-009 | BR-ORD-03 | §D4 | SC-ORD-013 | C-ORD-02 (Resolved — Deferred, 2026-07-27) |
| REQ-ORD-010 | BR-ORD-04 | §D4 | SC-ORD-014 | C-ORD-04 (Resolved, 2026-07-27) |
| REQ-ORD-011 | Quan sát thực tế app (không có ID doc gốc) | — | SC-ORD-015..026 | — |
| REQ-ORD-012 | D8.1/D8.2 (không có ID row riêng — BRD v3.2 mới) | §D8.1, §D8.2 | SC-ORD-013, SC-ORD-027, SC-ORD-028 | C-ORD-01 (Resolved đầy đủ, 2026-07-28) |
| REQ-ORD-013 | VAL-01..05 | §D8.3 | SC-ORD-029, SC-ORD-030 | — |
| REQ-ORD-014 | Quan sát thực tế app (không có ID doc gốc) | — | SC-ORD-031, SC-ORD-032 | — |
| REQ-ORD-015 | Không có ID doc gốc (bảng "Thành phần chung", không đánh số) | §2, §3.1 | SC-ORD-033 | — |
| REQ-ASN-001 | ASN-01 | §D3 | SC-ASN-001 | — |
| REQ-ASN-002 | ASN-02, BR-CON-01, BR-CON-02 | §D3, §A5 | SC-ASN-002, SC-ASN-003 | C-ASN-01 (Resolved, 2026-07-27) |
| REQ-ASN-003 | ASN-03, OPR-03 | §D3, §D7 | SC-ASN-004, SC-ASN-005 | — |
| REQ-ASN-004 | MTCH-01, BR-MTCH-01 | §D3, §D4 | SC-ASN-006, SC-ASN-007 | — |
| REQ-ASN-005 | OPR-01 | §D7 | SC-ASN-008, SC-ASN-013 | — |
| REQ-ASN-006 | OPR-02 | §D7 | SC-ASN-009 | C-NTF-02 (Partially Resolved, 2026-07-27) |
| REQ-ASN-007 | OPR-04 | §D7 | SC-ASN-010 | — |
| REQ-ASN-008 | OPR-05 | §D7 | SC-ASN-011 | C-ASN-02 (Resolved, 2026-07-27) |
| REQ-ASN-009 | OPR-08 | §D7 | SC-ASN-005, SC-ASN-012 | — |
| REQ-ASN-010 | Không có ID doc gốc (không đánh số) | §3.3 | SC-ASN-014 | — |
| REQ-DLV-001 | PUP-03, BR-CNF-01 | §D3, §D4 | SC-DLV-001, SC-DLV-002 | — |
| REQ-DLV-002 | GPS-01 | §D3 | SC-DLV-003, SC-DLV-004 | C-DLV-02 (Open — default deferred) |
| REQ-DLV-003 | DLV-03, BR-CNF-04, BR-INT-03 | §D3, §D4, §A5 + DOC-v1.0-04 | SC-DLV-005, SC-DLV-006, SC-DLV-007, SC-DLV-011, SC-DLV-012, SC-DLV-013, SC-DLV-014 | C-DLV-01 (Resolved), C-DLV-03 (Resolved 2026-07-27) |
| REQ-DLV-004 | COST-01, BR-COST-01 | §D3, §D4 | SC-DLV-008 | — |
| REQ-DLV-005 | BR-ASN-03 | §D4 | SC-DLV-009 | C-CNL-01 (Resolved — Deferred, 2026-07-27) |
| REQ-DLV-006 | US-D09 | §D1b | SC-DLV-010, SC-DLV-011 | — |
| REQ-GIFT-001 | GIFT-01, BR-GIFT-01 | §D3, §D4 | SC-GIFT-001, SC-GIFT-002, SC-GIFT-003, SC-GIFT-005, SC-GIFT-006, SC-GIFT-007 | C-ORD-06 (Resolved — QA xác nhận empty state text đúng UI thật, 2026-07-28) |
| REQ-GIFT-002 | RAT-01/02 | §D3 + DOC-v1.0-04 | — (Deferred — BA/PO xác nhận 2026-07-27: rating 1-5 sao là phase sau, out of scope v1.0) | C-GIFT-01 (Resolved — Deferred, 2026-07-27) |
| REQ-GIFT-003 | — (Quan sát thực tế app STG, QA GiangDC2) | Quan sát thực tế app STG · 2026-07-24 | SC-GIFT-004 | — |
| REQ-CNL-001 | CNL-01, BR-CNL-01, BR-INT-05, US-D16 | §D3, §D4, §A5, §D1b | SC-CNL-001, SC-CNL-003, SC-CNL-005 | — |
| REQ-CNL-002 | OPR-09 | §D7 | SC-CNL-004 | — |
| REQ-CNL-003 | OPR-11 | §D7 | SC-CNL-002 | — |
| REQ-NTF-001 | NTF-01..09 | §D6 + DOC-v1.0-04 | SC-NTF-001, SC-NTF-002, SC-NTF-003, SC-NTF-004, SC-NTF-005, SC-NTF-007, SC-NTF-008, SC-NTF-009 | C-NTF-01 (Open — bảng unified 3 nguồn bổ sung 2026-07-27, chờ BA chọn); C-ORD-06 (Resolved — QA xác nhận empty state text đúng UI thật, mở rộng sang NTF, 2026-07-28); C-NTF-03 (Resolved — QA xác nhận cơ chế đánh dấu đã đọc + phân trang đúng UI thật, 2026-07-28) |
| REQ-NTF-002 | OPR-06, OPR-07 | §D7 | SC-NTF-006 (DEPRECATED 2026-07-29 — không có ngưỡng ngày) | C-NTF-02 (Partially Resolved, 2026-07-27) |
| REQ-TS-001 | TS-01, TS-02, BR-INT-04 | §A8, §A5 | SC-TS-001, SC-TS-002 | — |
| REQ-TS-002 | TS-03 | §A8 | SC-TS-003 | C-TS-01 (Resolved — Deferred, 2026-07-27) |

---

## 3. Inventory Scenario (92)

> Cột **Nguồn** cho biết scenario đó suy ra từ đâu — chú ý các dòng ghi `Quan sát thực tế app` / `BA xác nhận qua chat`: đó chính là phần kiến thức đã được đóng gói lại ở **KP-01**.

| SC ID | Mô tả | Module | Nguồn | Priority | Loại | Lifecycle | TC Status |
|---|---|---|---|---|---|---|---|
| SC-USR-001 | Đăng nhập SSO thành công | USR | DOC-v1.0-01 | P1 | Functional | NEW | — |
| SC-USR-002 | Xem hồ sơ cá nhân (view-only — xác nhận không có update, C-USR-03) | USR | DOC-v1.0-01 | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-USR-003 | Hiển thị phòng ban + khu vực trên hồ sơ | USR | DOC-v1.0-01 | P2 | UI | NEW | ✅ Đã tạo TC |
| SC-USR-004 | Hiển thị đúng 2 chỉ số (đơn giúp + quà nhận), không hiện điểm/tier/CO2 | USR | DOC-v1.0-01, DOC-v1.0-02 | P2 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-USR-005 | Cấu hình kênh liên hệ sẽ lộ | USR | DOC-v1.0-01 | P3 | Functional | NEW | ✅ Đã tạo TC |
| SC-USR-006 | Check đầy đủ hiển thị header màn Cá nhân (completeness) | USR | DOC-v1.0-01, DOC-v1.0-04 | P2 | UI | NEW | ✅ Đã tạo TC |
| SC-USR-007 | Menu "Đơn của tôi" tại Cá nhân điều hướng sang màn Hoạt động | USR | Quan sát thực tế app | P3 | Functional | NEW | ✅ Đã tạo TC |
| SC-ORD-001 | Đăng tin NEED "Cần gửi" qua wizard 3 bước | ORD | DOC-v1.0-01, DOC-v1.0-02 | P1 | Functional | NEW | ✅ Đã tạo TC | ✅ PASS (R1, TC_04.2+TC_04.73) | 2026-07-31 |
| SC-ORD-002 | Đăng tin OFFER "Nhận giao hàng" (form 1 bước) | ORD | DOC-v1.0-01, DOC-v1.0-02 | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-ORD-003 | Tin xuất hiện ở "Đơn của tôi" ngay sau đăng, không hiện mã đơn | ORD | DOC-v1.0-02 | P2 | UI | NEW | ✅ Đã tạo TC |
| SC-ORD-004 | Timeline tin ghi nhận đầy đủ mốc thời gian | ORD | DOC-v1.0-01 | P1 | Functional | NEW | ✅ Đã tạo TC |
| SC-ORD-005 | Tin tự động "Hết hạn" khi quá thời gian không ai ghép | ORD | DOC-v1.0-01, DOC-v1.0-02 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ORD-006 | Không tick điều khoản → chặn đăng tin (Bước 3) | ORD | DOC-v1.0-01 | P2 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ORD-007 | [Gap] Bỏ trống Loại hàng/Giá trị Bước 1 vẫn qua Bước 2 | ORD | DOC-v1.0-02 | P3 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ORD-008 | Chỉnh sửa tin khi đang "Chờ ghép" | ORD | DOC-v1.0-01, DOC-v1.0-02 | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-ORD-009 | Khoá chỉnh sửa khi đã "Đã ghép" trở đi | ORD | DOC-v1.0-01, DOC-v1.0-02 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ORD-010 | Chọn nhanh 1 trong 6 văn phòng preset FPT | ORD | DOC-v1.0-01 | P3 | UI | NEW | ✅ Đã tạo TC |
| SC-ORD-011 | Email công ty người nhận có trong hệ thống → tự điền | ORD | DOC-v1.0-01, DOC-v1.0-02 | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-ORD-012 | Email công ty người nhận không có → báo nhập thủ công | ORD | DOC-v1.0-01, DOC-v1.0-02 | P2 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ORD-013 | Chọn Giá trị hàng "Cao" → cảnh báo trách nhiệm tự thoả thuận (⚠ MODIFIED 2026-07-28, un-deferred — xem C-ORD-02) | ORD | DOC-v1.0-01 (BRD v3.2 §D8.1) | P2 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ORD-014 | Đăng tin chứa hàng cấm → hệ thống chặn | ORD | DOC-v1.0-01 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ORD-015 | Đủ 2 tab "Đang diễn ra"/"Đã hoàn thành" tại Hoạt động | ORD | Quan sát thực tế app | P2 | UI | NEW | ✅ Đã tạo TC |
| SC-ORD-016 | Tab mặc định khi mới vào màn Hoạt động | ORD | Quan sát thực tế app | P2 | UI | NEW | ✅ Đã tạo TC |
| SC-ORD-017 | Check dữ liệu đúng tại tab "Đang diễn ra" | ORD | Quan sát thực tế app | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-ORD-018 | Check đầy đủ field trên 1 card đơn (completeness) | ORD | Quan sát thực tế app | P2 | UI | NEW | ✅ Đã tạo TC |
| SC-ORD-019 | Card trạng thái "Hoàn thành" hiển thị đúng, không assert rating | ORD | Quan sát thực tế app | P3 | UI | NEW | ✅ Đã tạo TC |
| SC-ORD-020 | Card trạng thái "Chờ ghép" hiển thị tại tab "Đang diễn ra" | ORD | Quan sát thực tế app | P3 | UI | NEW | ✅ Đã tạo TC |
| SC-ORD-021 | Tap card trạng thái khác "Hết hạn" → mở Chi tiết tin | ORD | Quan sát thực tế app | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-ORD-022 | Tap card "Hết hạn" → không cho thao tác | ORD | Quan sát thực tế app | P3 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ORD-023 | Empty state khi danh sách rỗng (cả 2 tab, C-ORD-06 Resolved) | ORD | Quan sát thực tế app | P3 | UI | NEW | ✅ Đã tạo TC |
| SC-ORD-024 | Đơn "Đã huỷ" (CNL) không hiển thị tại Hoạt động | ORD | Quan sát thực tế app | P2 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ORD-025 | Bottom nav đủ 5 tab, "Hoạt động" highlight đúng | ORD | Quan sát thực tế app | P3 | UI | NEW | ✅ Đã tạo TC |
| SC-ORD-026 | Check dữ liệu đúng tại tab "Đã hoàn thành" | ORD | Quan sát thực tế app | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-ORD-027 | Giới hạn ký tự tối đa các trường text + định dạng/kích thước ảnh sản phẩm (⚠ NEW 2026-07-28) | ORD | DOC-v1.0-01 (BRD v3.2 §D8.1/D8.2) | P3 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ORD-028 | Khung giờ (NEED + OFFER) phải cách nhau tối thiểu 30 phút (⚠ NEW 2026-07-28) | ORD | DOC-v1.0-01 (BRD v3.2 §D8.1/D8.2) | P2 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ORD-029 | Tự động cắt khoảng trắng + chuẩn hoá SĐT trước khi lưu (VAL-03, ⚠ NEW 2026-07-28) | ORD | DOC-v1.0-01 (BRD v3.2 §D8.3) | P3 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ORD-030 | Nút submit vô hiệu hoá tới khi hợp lệ; lỗi hiện inline on-blur; cuộn tới lỗi đầu tiên khi submit (VAL-01/02, ⚠ NEW 2026-07-28) | ORD | DOC-v1.0-01 (BRD v3.2 §D8.3) | P2 | UI | NEW | ✅ Đã tạo TC |
| SC-ORD-031 | Địa chỉ lấy hàng (Người gửi) — nhập text tự do hiển thị danh sách văn phòng phù hợp từ DB, không phân biệt hoa/thường (⚠ NEW 2026-07-29) | ORD | Quan sát thực tế app | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-ORD-032 | Địa chỉ giao hàng (Người nhận) — nhập text tự do hiển thị danh sách văn phòng phù hợp từ DB, không phân biệt hoa/thường (⚠ NEW 2026-07-29) | ORD | Quan sát thực tế app | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-ORD-033 | Check đầy đủ hiển thị Trang chủ: Header + Banner + Card "Đóng góp của bạn" + nút "Xem bảng tin" + bottom nav (completeness) (⚠ NEW 2026-07-29) | ORD | DOC-v1.0-02 | P3 | UI | NEW | ✅ Đã tạo TC |
| SC-ASN-001 | Carrier bấm "Tôi mang giúp được" → gửi đề nghị | ASN | DOC-v1.0-01, DOC-v1.0-02 | P1 | Functional | NEW | ✅ Đã tạo TC |
| SC-ASN-002 | Ghép ngay khi Carrier nhận (không cần chủ tin duyệt) → MATCHED + lộ SĐT | ASN | DOC-v1.0-01, DOC-v1.0-02 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ASN-003 | Trước khi ghép, SĐT KHÔNG lộ | ASN | DOC-v1.0-01, DOC-v1.0-02 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ASN-004 | 2 Carrier cùng bấm nhận gần đồng thời → chỉ 1 người ghép (chống double-accept) | ASN | DOC-v1.0-01 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ASN-005 | Tin ẩn khỏi Bảng tin sau khi có người ghép | ASN | DOC-v1.0-01 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ASN-006 | Hệ thống tự khớp tuyến OFFER với tin NEED trùng điểm lấy/giao | ASN | DOC-v1.0-01, DOC-v1.0-02 | P1 | Functional | NEW | — |
| SC-ASN-007 | Carrier bấm "Nhận giao" từ thông báo khớp tuyến → MATCHED | ASN | DOC-v1.0-01, DOC-v1.0-02 | P2 | Functional | NEW | ✅ Đã tạo TC (⚠ nhánh auto-match — Phase 1 Scope chờ PM chốt) |
| SC-ASN-008 | Carrier chỉ nhận tối đa 5 tin gợi ý cùng lúc | ASN | DOC-v1.0-01 | P3 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ASN-009 | Tin không trùng điểm lấy/giao hoặc khung giờ không giao nhau → không gợi ý | ASN | DOC-v1.0-01 | P2 | Business Rule | NEW | — |
| SC-ASN-010 | Gợi ý ưu tiên theo độ gần tuyến rồi thời gian đăng mới nhất | ASN | DOC-v1.0-01 | P2 | Business Rule | NEW | ✅ Đã tạo TC (bề mặt Trang chủ tại TC-TRANGCHU + bề mặt Bảng tin tại TC-BANGTIN) |
| SC-ASN-011 | Không tự khớp tin của chính mình | ASN | DOC-v1.0-01 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ASN-012 | Tin huỷ bởi Carrier (chưa lấy hàng) quay lại "Chờ ghép" và được khớp lại | ASN | DOC-v1.0-01 | P2 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-ASN-013 | Hệ thống chỉ bắn tối đa 5 thông báo khớp tin cho Carrier, tính riêng theo từng tin — không cộng dồn theo ngày (⚠ NEW 2026-07-29, BA xác nhận rõ, thay thế SC-NTF-006) | ASN | DOC-v1.0-01, BA xác nhận qua chat | P2 | Business Rule | NEW | ✅ Đã tạo TC (TC_03.1-3, sheet NTF) |
| SC-ASN-014 | Bảng tin hiển thị đủ card list (badge "Tin của bạn", loại hàng/giá trị, khung giờ...) + bấm mở Chi tiết tin (completeness) (⚠ NEW 2026-07-29) | ASN | DOC-v1.0-02 | P3 | UI | NEW | ✅ Đã tạo TC |
| SC-DLV-001 | Carrier chụp ảnh hàng lúc nhận (tuỳ chọn) → lưu, gắn timeline | DLV | DOC-v1.0-01 | P2 | Functional | NEW | ✅ Đã tạo TC (⚠ nhánh phụ — Phase 1 Scope chờ PM chốt) |
| SC-DLV-002 | Bỏ qua chụp ảnh lúc nhận vẫn chuyển trạng thái được | DLV | DOC-v1.0-01 | P3 | Business Rule | NEW | ✅ Đã tạo TC (⚠ nhánh phụ — Phase 1 Scope chờ PM chốt) |
| SC-DLV-003 | Carrier bật chia sẻ vị trí khi đang giao | DLV | DOC-v1.0-01 | P3 | Functional | NEW | ✅ Đã tạo TC (⚠ nhánh phụ — Phase 1 Scope chờ PM chốt) |
| SC-DLV-004 | Vị trí chia sẻ tự tắt/xoá sau khi đơn đóng | DLV | DOC-v1.0-01 | P3 | Business Rule | NEW | ✅ Đã tạo TC (⚠ nhánh phụ — Phase 1 Scope chờ PM chốt) |
| SC-DLV-005 | Nút "Xác nhận đã nhận hàng" chỉ kích hoạt khi = Đã giao | DLV | DOC-v1.0-01, DOC-v1.0-02 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-DLV-006 | Nút hành động Carrier bị động ở trạng thái trước "Đã giao" | DLV | DOC-v1.0-02 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-DLV-007 | Quá N giờ chưa xác nhận nhận hàng → nhắc → admin hỗ trợ | DLV | DOC-v1.0-01 | P2 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-DLV-008 | (Tuỳ chọn) Ghi nhận chi phí đối soát offline, không qua app | DLV | DOC-v1.0-01 | P3 | Functional | NEW | ✅ Đã tạo TC (⚠ nhánh phụ — Phase 1 Scope chờ PM chốt) |
| SC-DLV-009 | Sau khi đã lấy hàng (IN_TRANSIT), huỷ thường bị chặn → chỉ tạo được sự cố | DLV | DOC-v1.0-01 | P2 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-DLV-010 | Không thể bấm "Đã giao" trước khi bấm "Tôi đã lấy hàng" | DLV | DOC-v1.0-01 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-DLV-011 | Người nhận xác nhận → đơn "Hoàn thành" ngay lập tức | DLV | DOC-v1.0-01, DOC-v1.0-02 | P1 | Functional | NEW | ✅ Đã tạo TC |
| SC-DLV-012 | Nhãn nút Sender/Receiver đúng theo trạng thái Đã ghép/Đang giao | DLV | Quan sát thực tế app | P2 | UI | NEW | ✅ Đã tạo TC |
| SC-DLV-013 | Tại "Đã giao": Sender/Carrier disable, chỉ Receiver enable | DLV | Quan sát thực tế app | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-DLV-014 | Carrier/Receiver thấy nhãn "Đơn đã hoàn thành" sau Hoàn thành | DLV | Quan sát thực tế app | P3 | UI | NEW | ✅ Đã tạo TC |
| SC-GIFT-001 | Sau Hoàn thành, Sender chọn 1/4 loại quà tặng Carrier | GIFT | DOC-v1.0-01, DOC-v1.0-02 | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-GIFT-002 | Gửi quà không cần Carrier xác nhận → popup cảm ơn | GIFT | DOC-v1.0-01, DOC-v1.0-02 | P3 | Functional | NEW | ✅ Đã tạo TC |
| SC-GIFT-003 | Card "Quà đã nhận" chỉ load đúng loại đã nhận (không hiện loại chưa nhận) | GIFT | Quan sát thực tế app | P3 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-GIFT-004 | Nút "Cảm ơn người vận chuyển" đổi thành "Bạn đã đánh giá" sau khi gửi quà | GIFT | Quan sát thực tế app | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-GIFT-005 | Menu "Quà đã nhận" tại Cá nhân điều hướng sang màn Quà đã nhận | GIFT | Quan sát thực tế app | P3 | Functional | NEW | ✅ Đã tạo TC |
| SC-GIFT-006 | Màn "Quà đã nhận" rỗng khi chưa nhận quà nào | GIFT | Quan sát thực tế app | P3 | UI | NEW | ✅ Đã tạo TC |
| SC-GIFT-007 | Icon quay lại tại màn "Quà đã nhận" | GIFT | Quan sát thực tế app | P3 | UI | NEW | ✅ Đã tạo TC |
| SC-CNL-001 | Huỷ đơn ở POSTED/MATCHED → popup bắt buộc nhập lý do | CNL | DOC-v1.0-01, DOC-v1.0-02 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-CNL-002 | Không cho huỷ khi đơn đã "Đang giao" trở đi | CNL | DOC-v1.0-01 | P1 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-CNL-003 | Đơn huỷ ghi rõ vai trò người huỷ + lý do, đồng bộ realtime 3 bên | CNL | DOC-v1.0-01, DOC-v1.0-02 | P2 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-CNL-004 | Carrier huỷ khi "Đã ghép" (chưa lấy hàng) → đơn về "Chờ ghép" | CNL | DOC-v1.0-01 | P2 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-CNL-005 | Lý do huỷ tối thiểu 5 ký tự mới bật nút Xác nhận (VAL-04, ⚠ NEW 2026-07-28) | CNL | DOC-v1.0-01 (BRD v3.2 §D8.3) | P2 | Business Rule | NEW | ✅ Đã tạo TC |
| SC-NTF-001 | Thông báo khi ghép ngay (NTF-01/02) | NTF | DOC-v1.0-01 | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-NTF-002 | Thông báo khi khớp tuyến OFFER (NTF-03) | NTF | DOC-v1.0-01 | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-NTF-003 | Thông báo theo mốc vận chuyển: lấy hàng/đã giao/hoàn tất (NTF-04/05/06) | NTF | DOC-v1.0-01 | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-NTF-004 | Thông báo khi nhận quà cảm ơn (NTF-07) | NTF | DOC-v1.0-01 | P3 | Functional | NEW | ✅ Đã tạo TC |
| SC-NTF-005 | Thông báo khi đơn huỷ (NTF-08) và tin quá hạn (NTF-09) | NTF | DOC-v1.0-01 | P2 | Functional | NEW | ✅ Đã tạo TC |
| SC-NTF-006 | Carrier bị giới hạn trần thông báo khớp/ngày (⚠ SUPERSEDED 2026-07-29 — BA xác nhận không có ngưỡng ngày, xem SC-ASN-013) | NTF | DOC-v1.0-01 | P3 | Business Rule | DEPRECATED | — |
| SC-NTF-007 | Empty state khi chưa có thông báo nào (mở rộng C-ORD-06, Resolved) | NTF | Quan sát thực tế app | P3 | UI | NEW | ✅ Đã tạo TC |
| SC-NTF-008 | Đánh dấu đã đọc (tap 1 thông báo / nút mark-all, C-NTF-03 Resolved) | NTF | DOC-v1.0-04 / Quan sát thực tế app | P3 | Functional | NEW | ✅ Đã tạo TC |
| SC-NTF-009 | Scroll xuống load thêm dữ liệu (phân trang, C-NTF-03 Resolved) | NTF | Quan sát thực tế app | P3 | Functional | NEW | ✅ Đã tạo TC |
| SC-TS-001 | Mọi tương tác được ghi log đầy đủ mốc thời gian | TS | DOC-v1.0-01 | P2 | Functional | NEW | — |
| SC-TS-002 | Log tương tác không thể sửa/xoá sau khi ghi | TS | DOC-v1.0-01 | P2 | Business Rule | NEW | — |
| SC-TS-003 | Admin can thiệp hỗ trợ dựa trên log khi có vướng mắc | TS | DOC-v1.0-01 | P3 | Functional | NEW | — |

---

## 4. Ghi chú về chất lượng baseline này

**Đã biết là SAI / cần sửa ở đợt mới:**
1. Mọi TC/scenario nhắc chip **"Tài liệu"** đều sai chữ — app thật là **"Giấy tờ, hồ sơ"** (`KP-01 §10.2`)
2. Scenario về "Loại hàng bắt buộc" **không kiểm chứng được qua UI** vì chip luôn có default (`KP-01 §10.3`)
3. TC `TC_04.71` expected "checkbox điều khoản tick sẵn" — thực tế **không tick sẵn** (`KP-01 §10.7`)
4. Scenario về Tên Người gửi "read-only" — thực tế **edit được và bị xoá trắng** (`KP-01 §10.5`)
5. Scenario về Địa chỉ lấy hàng pre-fill — thực tế **không pre-fill** (`KP-01 §10.6`)

**Hạn chế phương pháp của đợt cũ:**
- `review-tc` chạy ở **Direct mode** (thiếu `review-agent/AGENT.md`) → score bị **cap 85** và mang **bias self-review**. Điểm 84/100 vì vậy không phải đánh giá độc lập.
- Chỉ **~17/323 TC** từng được chạy thật trên app (2 phiên vibe-test dở dang). 306 TC còn lại **chưa từng đối chiếu với app thật**.
