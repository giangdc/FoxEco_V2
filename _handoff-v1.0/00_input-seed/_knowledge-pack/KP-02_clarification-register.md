# KP-02 — Sổ đăng ký Clarification (25 mục)

> Trạng thái chốt tại **2026-07-30**. Đây là toàn bộ câu hỏi làm rõ đã đặt ra trong đợt phân tích cũ, kèm câu trả lời của BA/PO.
> **Cách dùng ở project mới:** nạp thẳng bảng này làm clarification register khởi điểm. Mục nào `Open` thì mang sang nguyên trạng; mục nào `Resolved` thì dùng câu trả lời làm nguồn viết scenario (trích `DOC-v1.0-05 KP-02 §<mục>`).

## 1. Tổng quan

| Trạng thái | Số lượng |
|---|---|
| ✅ Resolved — có rule áp dụng ngay ở v1.0 | 10 |
| ✅ Resolved — Out of scope v1.0 (deferred phase sau) | 6 |
| 🟡 Partially Resolved | 2 |
| 🔴 Open — chưa có câu trả lời | 7 |
| **Tổng** | **25** |

> 📌 **Không còn BLOCKER cứng nào.** `C-ORD-02` (ngưỡng giá trị hàng) từng là blocker, đã gỡ ngày 2026-07-27 khi BA/PO xác nhận out of scope v1.0.

**Nguồn câu trả lời:** đợt batch lớn nhất là **2026-07-27**, QA GiangDC2 hỏi BA/PO **qua chat trực tiếp** (không có văn bản chính thức). Các mục còn lại trả lời lẻ 2026-07-28 → 2026-07-30.

---

## 2. Nhóm ✅ Resolved — RULE ÁP DỤNG NGAY Ở v1.0

| ID | Vấn đề | Câu trả lời chốt | Ngày |
|---|---|---|---|
| **C-ORD-01** | Wizard đăng tin có field bắt buộc không? maxlength bao nhiêu? | **CÓ** bắt buộc: Loại hàng + Giá trị hàng (B1), Người nhận (B2). Maxlength đã đủ từ **BRD v3.2 §D8.1/D8.2**: Ghi chú ≤300 · Địa chỉ lấy/giao ≤200 · Điểm xuất phát (OFFER) ≤200 · Tên người nhận 2–60 · khung giờ cách nhau tối thiểu 30 phút | 2026-07-27 → 2026-07-28 |
| **C-ORD-03** | Hạn tin mặc định bao lâu? | = giá trị **"Đến ngày"** user chọn lúc đăng, không phải hằng số hệ thống. Đến đúng "Đến ngày" thì tin tự chuyển EXPIRED | 2026-07-27 |
| **C-ORD-04** | Chip "Thuốc/Y tế" có bị chặn không? | **Không chặn ở v1.0** — chọn được mọi loại hàng; banner cảnh báo chỉ là thông tin tĩnh | 2026-07-27 |
| **C-ORD-07** | Section "Tin mới" là riêng của Carrier hay cả Sender? | **Cả Sender lẫn Carrier** — user chốt *"viet theo UI luon nha"* | 2026-07-30 |
| **C-ASN-01** | SĐT lộ lúc nào? | **Chỉ sau khi ghép** (khớp BR-CON-02). Prototype lộ sớm ở "Chờ ghép" là **bug** | 2026-07-27 |
| **C-ASN-02** | Chủ tin có tự nhận mang giúp tin của mình được không? | **Không** (khớp OPR-05). Prototype cho phép là **bug** | 2026-07-27 |
| **C-DLV-01** | Ai được xác nhận "Đã nhận hàng"? | **Chỉ Receiver.** Xác nhận qua 5 ảnh Figma nhất quán | 2026-07-24 |
| **C-DLV-03** | Màn xác nhận nhận hàng dùng bản nào? | **Modal đơn giản** (theo Figma); form đầy đủ có ảnh bằng chứng + điểm uy tín KHÔNG áp dụng v1.0 | 2026-07-27 |
| **C-USR-03** | BRD ghi `USR-02` *"Xem/**cập nhật** hồ sơ"* — app có chức năng sửa hồ sơ không? | **KHÔNG.** QA xác nhận trực tiếp trên app STG: màn Cá nhân **view-only** hoàn toàn, cả 6 trường chỉ để xem | 2026-07-24 |
| **C-CNL-02** | Huỷ đơn / Huỷ nhận đơn có ghi log LỊCH SỬ không? | **PHẢI ghi log** cho cả 2 — user chốt *"huy don va huy nhan don hien tai cu luu log lich su nha"*. Hành vi UI hiện tại (không ghi log, thậm chí xoá dòng "Ghép thành công") là **gap cần dev bổ sung** | 2026-07-30 |

---

## 3. Nhóm ✅ Resolved — OUT OF SCOPE v1.0 (deferred phase sau)

| ID | Vấn đề | Ghi chú |
|---|---|---|
| **C-ORD-02** | Ngưỡng giá trị hàng bằng số tiền (`BR-ORD-03`) + bắt buộc ảnh khi vượt ngưỡng | ⭐ Từng là **BLOCKER cứng**, gỡ 2026-07-27. Lưu ý: cảnh báo theo mức "Cao" thì **CÓ** ở v1.0 (khác với ngưỡng số tiền) |
| **C-USR-01** | Tier "Hạng Đồng hành" / Điểm ECO / Điểm uy tín / CO₂ | Badge chỉ là text tĩnh, không có logic tính |
| **C-USR-02** | Cấu hình kênh liên hệ sẽ lộ (`USR-07`) | Không thuộc scope UI v1.0 |
| **C-GIFT-01** | Rating 1-5 sao (`RAT-01/02`) | v1.0 chỉ có Quà ảo (`GIFT-01`). Kéo theo: "Đánh giá" trong scope Phase 1 = Quà ảo |
| **C-TS-01** | Admin Web Portal | Không có đặc tả UI ở cả 2 doc |
| **C-CNL-01** | Màn "Báo sự cố" (Incident) | Chưa có đặc tả field |

---

## 4. Nhóm 🟡 Partially Resolved

### C-NTF-02 — Định nghĩa "khớp tuyến" & tham số vận hành
- ✅ **Đã chốt:** khớp tuyến = **trùng địa chỉ giao hàng đã chọn** + **khung giờ phù hợp**. KHÔNG dùng bán kính GPS/khoảng cách địa lý.
- 🔴 **Còn thiếu:** "khung giờ phù hợp" là trùng hoàn toàn hay có độ lệch cho phép? · chu kỳ quét khớp? · ngưỡng nhắc/gộp thông báo?
- Ghi chú: chính BRD tự ghi *"Chờ BA bổ sung"* cho nhóm tham số này (§D6/§D7).

### C-NTF-03 — Đánh dấu đã đọc & phân trang màn Thông báo
- **(a) 🔴 Open:** nút "Đánh dấu đã đọc" + chấm đỏ có trên Figma nhưng **không có mô tả cơ chế** — mark-all hay mark-per-item? Ảnh `3e626d39…` chỉ là bằng chứng **gián tiếp** (2 item mới có chấm đỏ, 2 item cũ cùng nhóm "Hôm nay" không có).
- **(b) ✅ N/A:** scroll/lazy-load được QA xác nhận là **hành vi UI nền tảng**, không phải business rule cần BA chốt.

---

## 5. Nhóm 🔴 Open — CHƯA CÓ CÂU TRẢ LỜI

| ID | Vấn đề | Vì sao quan trọng |
|---|---|---|
| **C-ORD-05** | Màn "Đăng tin thành công!" có 2 biến thể ngay trên cùng board Figma — 1 bản **CÓ** trường "Mã tin" (vd `#ECO-2026-0451`), 1 bản **KHÔNG**. Đồng thời đối lập với `US-D02` (*"KHÔNG hiển thị mã đơn — mã kỹ thuật vô nghĩa với người dùng"*) | Mâu thuẫn nội bộ ngay trong nguồn thiết kế |
| **C-ORD-06** | Empty state của 3 màn (Hoạt động · Quà đã nhận · Thông báo) khi không có data | ⚠ **Có lịch sử đảo chiều:** từng Resolved 2026-07-28 với text *"Hiện tại chưa có dữ liệu"*, sau đó **REVERT về Open 2026-07-29** vì rà lại toàn bộ 82 ảnh Figma + BRD + demo docx **không tìm thấy bằng chứng nào** — nhãn "Resolved" cũ chỉ dựa trên mô tả qua chat không kèm nguồn. QA xác nhận đang nhờ BA bổ sung text chính thức |
| **C-ORD-08** | Bấm Reset/thoát giữa chừng wizard có xoá dữ liệu form đã nhập không? | Chưa hỏi BA. Không có mô tả trong BRD/PRD |
| **C-NTF-01** | Danh sách **9 loại thông báo chính thức** — 3 nguồn khác nhau (BRD §D6 `NTF-01..09` vs demo Table 4 vs Figma) | Đã lập **bảng unified 3 nguồn** để BA chọn (BA chưa trả lời) → **`KP-07_notification-matrix.md`** |
| **C-DLV-02** | Chia sẻ vị trí (`GPS-01`) mặc định bật hay tắt | BA trả lời "phase sau" nhưng **chưa cho giá trị** |
| **C-ASN-03** | Wizard đăng tin không tạo listing độc lập trong feed Carrier/Receiver | Chưa rõ là giới hạn bản demo hay hành vi cần fix |
| **C-GIFT-02** | Nút back ở màn "Tặng quà" nhảy sang màn "Xác nhận đã nhận hàng" của **đơn khác** | Nhiều khả năng là giới hạn demo (item mẫu tĩnh) |

> 📌 Nhánh **`C-NTF-03(a)`** (cơ chế "Đánh dấu đã đọc" — mark-all hay mark-per-item) cũng đang Open, nhưng được đếm ở nhóm **Partially Resolved** (§4) vì nhánh (b) của cùng clarification đã đóng.

---

## 6. ⚠ Bài học từ đợt cũ về chất lượng clarification

Đợt cũ có **2 lần phải revert trạng thái Resolved → Open** (`C-ORD-06`, `C-NTF-03`) vì lý do giống nhau: **đánh dấu Resolved dựa trên mô tả qua chat mà không kèm bằng chứng ảnh/tài liệu cụ thể**.

**Quy tắc đề xuất cho project mới:** chỉ ghi `Resolved` khi có **ít nhất một** trong:
1. Câu trả lời BA/PO ghi rõ ngày + nội dung nguyên văn, HOẶC
2. Ảnh Figma có hash cụ thể, HOẶC
3. Screenshot vibe-test trên app thật.

Chat mô tả suông → ghi `Partially Resolved` kèm ghi chú "chưa có bằng chứng", không ghi `Resolved`.
