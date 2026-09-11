---
id: v1.0/USR-tai-khoan/risk
title: Risk Assessment — v1.0 · Module USR
type: risk-assessment
version: v1.0
sprint: 1
module: USR
counts:
  cl: 4
  risk: 5
  cl_open: 1
  cl_resolved: 3
status: ANALYZED
updated: 2026-09-07
---

# Risk Assessment — v1.0 · Module USR

> Tạo bởi: analyze-requirements. Đánh giá rủi ro + định hướng test focus cho generate-tc/vibe-test.
> **Structure-lock:** dùng DUY NHẤT bảng 9 cột dưới. File này là nguồn PRIMARY duy nhất cho risk của module.
> 🔑 Frontmatter `counts:` là **nguồn canonical** của số CL/RISK module USR. **Layout v2 ⇒ đây cũng là home của Clarification.**

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| USR | **Low** | Bề mặt view-only, không có state-transition; rủi ro lớn nhất là **không seed được dữ liệu hồ sơ/chỉ số** để verify |

## Chi tiết rủi ro (bảng hợp nhất)
| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-USR-01 | USR / SSO | Đăng nhập SSO thuộc host app FoxPro ⇒ QC **không test trực tiếp** được luồng auth (thất bại đăng nhập, hết hạn JWT, sai domain) | Medium | `USR-01` §A6 L99 + `DOC-v1.0-06` KP-03 §1 (SDK nhúng host app) | Chỉ verify hệ quả: vào được SDK với đúng danh tính | Giới hạn scope SC-USR-001 ở hệ quả; nhánh auth âm tính bàn cho team host app | Pending | REQ-USR-001, SC-USR-001 |
| RISK-USR-02 | USR / Hồ sơ | Doc liệt kê 6 trường hồ sơ nhưng chỉ 4 trường có bằng chứng UI ⇒ dễ viết TC khẳng định trường không tồn tại (đúng lỗi đợt v1.0 cũ) | Medium | `USR-02` §A6 L100 vs `DOC-v1.0-06` KP-01 §2 KB-USR-02 | Assert đúng 4 trường có 2 nguồn; 2 trường còn lại ghi gap | Áp `§Custom Rules §10.1`; đưa SĐT/khu vực/kênh liên hệ về `C-USR-04` | Open | REQ-USR-002, SC-USR-002 |
| RISK-USR-03 | USR / Chỉ số | 2 chỉ số là `Runtime` phụ thuộc lịch sử đơn/quà ⇒ **không seed nhanh được**, assert số tuyệt đối sẽ FAIL oan | Medium | `USR-05` §A6 L102 · `test_data_catalog.md` | Verify **delta +1** sau 1 đơn hoàn tất / 1 quà nhận, không assert số tuyệt đối | Ghi rõ oracle delta trong TC; nhờ dev/QA seed tài khoản có lịch sử | Resolved | REQ-USR-004, SC-USR-005 |
| RISK-USR-04 | USR / Tier | Badge hạng thành viên hiển thị nhưng **không có logic** ⇒ reviewer/tester sau dễ hiểu là tính năng tier đã có và viết TC đổi hạng | Low | `DOC-v1.0-02` §3.9 vs `C-USR-01` Resolved-deferred | Assert badge là text tĩnh; cấm TC đổi hạng | Ghi ràng buộc ở `CHANGELOG §2` | Resolved | REQ-USR-007, SC-USR-007 |
| RISK-USR-05 | USR / Empty state | Chỉ số = 0 và hồ sơ thiếu field (avatar/phòng ban) **chưa có đặc tả UI** ⇒ không có oracle để assert | Low | `C-ORD-06` (Open) nhánh empty state | Ghi nhận hiển thị thực tế, không assert text | Chờ BA trả lời `C-ORD-06`; tạm viết TC dạng ghi nhận | Open | REQ-USR-004, SC-USR-005 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-USR-01 | Tier "Hạng Đồng hành" / Điểm ECO / Điểm uy tín / CO₂ có thuộc v1.0? | ✅ Resolved — Out of scope v1.0 | 2026-07-27 | REQ-USR-004, REQ-USR-007 |
| C-USR-02 | `USR-07` cấu hình kênh liên hệ sẽ lộ — có bề mặt UI không? | ✅ Resolved — Out of scope v1.0 | 2026-07-27 | REQ-USR-005 |
| C-USR-03 | `USR-02` ghi *"Xem/**cập nhật** hồ sơ"* — app có chức năng sửa hồ sơ không? | ✅ Resolved — KHÔNG (view-only) | 2026-07-24 | REQ-USR-002 |
| C-USR-04 | 🔴 Nhãn mục menu thứ hai + 3 trường hồ sơ chưa có bằng chứng UI | 🔴 **Open** | mở 2026-09-07 | REQ-USR-002, REQ-USR-006 |

### C-USR-01 · Tier / Điểm ECO / Điểm uy tín / CO₂

**Source Quote (ambiguous — 2 nguồn xung đột):**
> Nguồn A (`DOC-v1.0-01` §A7 L111): "Không tính điểm, không tier/xếp hạng, không CO₂, không quy đổi tiền / thanh toán in-app"
> Nguồn B (`DOC-v1.0-02` §3.9): "3 chỉ số | Đơn đã giúp (12) · Điểm uy tín (4.8) · Điểm ECO (540)"

**Source Location:** `DOC-v1.0-01 §A7 · bullet 5 · L111` ⟷ `DOC-v1.0-02 §3.9 · bảng Trường/Thành phần · dòng "3 chỉ số"`

**Analyst Note:** BA/PO chốt 2026-07-27 theo nguồn A: cơ chế tier/điểm là **phase sau**. Figma cho kết quả **trung gian** — có badge text, không có số (`DOC-v1.0-06` KP-01 §2 KB-USR-02) ⇒ badge vẫn assert được, điểm số thì không. **Bằng chứng đủ chuẩn Resolved** theo `KP-02 §6` (có ảnh Figma hash cụ thể + câu trả lời BA có ngày).

### C-USR-02 · Cấu hình kênh liên hệ sẽ lộ (`USR-07`)

**Source Quote (ambiguous):**
> "USR-07 | Cấu hình kênh liên hệ sẽ lộ: SĐT (bắt buộc), Workplace/email (tùy chọn)"

**Source Location:** `DOC-v1.0-01 §A6 · bảng ID/Yêu cầu · L103`

**Analyst Note:** Yêu cầu có trong BRD, **không có ở bất kỳ ảnh nào trong 82 ảnh Figma** và không có trên app STG. BA/PO xác nhận out of scope v1.0. Đây là case gốc sinh ra `§Custom Rules §10.1` ⇒ chỉ ghi GAP (`SC-USR-010`).

### C-USR-03 · `USR-02` "Xem/cập nhật hồ sơ" — có sửa được không?

**Source Quote (ambiguous):**
> "USR-02 | Xem/cập nhật hồ sơ: tên, SĐT, avatar, phòng ban, khu vực/văn phòng, kênh liên hệ"

**Source Location:** `DOC-v1.0-01 §A6 · bảng ID/Yêu cầu · L100`

**Analyst Note:** Từ *"cập nhật"* trong doc gợi ý có chức năng sửa; QA kiểm trực tiếp app STG 2026-07-24 xác nhận **view-only hoàn toàn**. Resolved theo UI. Hệ quả: `SC-USR-003` là SC negative bảo vệ kết luận này.

### C-USR-04 · 🔴 Nhãn mục menu thứ hai + 3 trường hồ sơ chưa có bằng chứng UI

**Source Quote (ambiguous — 3 nguồn 3 nhãn):**
> Nguồn A (`DOC-v1.0-02` §3.9): "Menu | "Đơn của tôi" (→ Hoạt động) · "Đánh giá đã nhận" (không có phản hồi khi bấm trong bản demo)"
> Nguồn B (`DOC-v1.0-01` §D1b `US-D20` L196): "Trang cá nhân có mục "Đơn đã giúp" & "Quà đã nhận""
> Nguồn C (`DOC-v1.0-06` KP-01 §2 KB-USR-02, Figma): "menu: `Đơn của tôi`, `Quà đã nhận`"

**Source Location:** `DOC-v1.0-02 §3.9 · dòng "Menu"` ⟷ `DOC-v1.0-01 §D1b · L196` ⟷ `DOC-v1.0-06 KP-01 §2 KB-USR-02`

**Analyst Note:** Hai câu hỏi gộp trong 1 CL vì cùng thuộc bề mặt màn Cá nhân và cùng cần 1 lượt trả lời của BA:
**(a)** Nhãn mục menu thứ hai — *"Đánh giá đã nhận"* (PRD) hay *"Quà đã nhận"* (BRD+Figma)? Tạm dùng **"Quà đã nhận"** vì 2/3 nguồn đồng thuận và nhãn "Đánh giá" thuộc nhánh rating đã deferred (`C-GIFT-01`).
**(b)** Ba trường `SĐT` · `khu vực/văn phòng` · `kênh liên hệ` mà `USR-02` liệt kê **chưa có bằng chứng UI nào** — có trên màn Cá nhân v1.0 hay không? Chưa trả lời ⇒ `SC-USR-002` chỉ assert 4 trường đã xác nhận. **Non-blocking** cho generate-tc.

## Khuyến nghị tổng thể
1. **Resolve trước generate-tc:** `C-USR-04(b)` — quyết định 3 trường hồ sơ có nằm trong TC completeness hay không. Không trả lời thì giữ nguyên 4 trường, ⛔ đừng "đoán thêm cho đủ 6".
2. **Ưu tiên test P1 high-risk:** `SC-USR-001` (là cửa vào của mọi module khác — fail là blocked toàn bộ).
3. **Cần môi trường/dữ liệu:** `SC-USR-005` cần tài khoản có lịch sử đơn/quà + 1 tài khoản trắng ⇒ nhờ dev/QA seed STG trước khi execute.
4. **ID/text cleanup (non-blocking):** nhãn *"Đơn của tôi"* (PRD/Figma) vs *"Đơn đã giúp"* (`US-D20`) — chốt 1 nhãn trước khi automation dùng làm locator text.
