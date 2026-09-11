# KP-07 — Ma trận thông báo hợp nhất 3 nguồn (clarification `C-NTF-01`)

> **Trạng thái: 🔴 Open — chờ BA chọn danh sách chính thức.**
>
> Ba nguồn cho ra **ba danh sách thông báo khác nhau**: BRD `§D6` (`NTF-01..09`) · demo `§3.2 Table 4` · ảnh Figma thực tế.
> Bảng dưới xếp cả 3 theo **cùng một hàng sự kiện** để BA chọn một lần thay vì đọc rời rạc.
>
> Trích nguyên văn từ phân tích v1.0 (`MEMORY.md §6.1`). Xem thêm: `KP-01 §8 KB-NTF-03` · `KP-02 §5` · `KP-05 §1` câu hỏi #5.

---

#### C-NTF-01 — Nội dung 9 thông báo demo khác BRD

**Source Quote (ambiguous):**
> "Có người muốn mang giúp đơn của bạn | ... · Bạn nhận được đánh giá 5 sao | Kèm nhận xét từ đối tác đơn hàng · ... · Cộng đồng FoxEco vừa đạt mốc X đơn | Thông điệp 'tiết kiệm Y kg CO₂' — gamification"

**Source Location:** `DOC-v1.0-02 §3.2 "Màn hình Thông báo" · Table 4`

**Analyst Note:** Danh sách 9 loại thông báo trong demo/docx không khớp NTF-01..09 (BRD D6) — đặc biệt có 2 loại liên quan trực tiếp tới các tính năng đã bị BRD loại bỏ (đánh giá sao — xem C-GIFT-01; CO2/gamification — xem C-USR-01). Non-blocking cho REQ-NTF-001 (test theo danh sách BRD D6, đã là nguồn mới hơn) nhưng củng cố thêm bằng chứng cho 2 clarification kia.

**Cập nhật 2026-07-24 (DOC-v1.0-04):** Ảnh Figma thực tế cho ra danh sách THỨ BA (xem REQ-NTF-001 §4.1 Source Quote #2) — cũng khác cả BRD D6 lẫn demo Table 4. Trùng với demo Table 4 ở điểm có "đánh giá 5 sao"; KHÔNG có "cộng đồng đạt mốc X đơn" (CO2/gamification) ở bất kỳ đâu trong 82 ảnh — củng cố nhánh "CO2/gamification không có trong scope v1.0" (khớp C-USR-01), nhưng làm YẾU đi nhánh "rating không có trong scope" (đối lập C-GIFT-01). DOC-v1.0-04 nên là nguồn verbatim ưu tiên cho generate-tc vì là artifact thiết kế gốc.

**Update 2026-07-27 (bảng tổng hợp unified — theo yêu cầu user "chưa tổng hợp lại cụ thể có tất cả bao nhiêu loại"):** Dưới đây là toàn bộ nội dung 3 nguồn xếp theo cùng 1 hàng sự kiện, để BA chọn danh sách chính thức 1 lần thay vì đọc rời rạc 3 nguồn.

| # | Sự kiện / Người nhận | BRD D6 (NTF-xx) | Demo Table 4 (§3.2) | Figma thực tế (DOC-v1.0-04, đã xác nhận ảnh) | Ghi chú |
|---|----------------------|------------------|----------------------|-----------------------------------------------|---------|
| 1 | Carrier ngỏ ý/ghép ngay [Sender] | NTF-01: "Đã có người nhận mang giúp đơn của bạn — SĐT đã được lộ để liên hệ" (ghép NGAY, lộ SĐT) | "Có người muốn mang giúp đơn của bạn" — "[Tên] ngỏ ý mang giúp '...'. Xác nhận để lộ SĐT." (chỉ "ngỏ ý", cần xác nhận riêng mới lộ SĐT) | Không quan sát riêng biệt (có thể trùng với hàng #2 dưới) | BRD vs Demo khác nhau về THỜI ĐIỂM lộ SĐT (ghép ngay vs cần xác nhận thêm) — liên quan C-ASN-01 |
| 2 | Ghép thành công [cả 2 bên] | NTF-02: "Đơn gửi tới bạn đã có người vận chuyển nhận giao" [Người nhận] | "Ghép thành công — SĐT đã được lộ" — "Thông báo khi hai bên đã ghép đơn" | "Ghép thành công — SĐT đã được lộ" — "Bạn và Trần Thị Lan đã được kết nối. Liên hệ để sắp xếp..." (khớp GẦN NHƯ Y HỆT text Demo) | Figma khớp Demo, khác câu chữ BRD — dùng Figma/Demo cho verbatim |
| 3 | Khớp tuyến gợi ý [Carrier] | NTF-03: "Tìm thấy đơn hàng phù hợp tuyến của bạn — xem chi tiết để nhận giao" | "Có chuyến đi mới hợp tuyến của bạn" — "Gợi ý chuyến của người khác trùng cung đường" | "Tìm thấy đơn hàng phù hợp tuyến của bạn" — "Có người cần gửi... trùng tuyến bạn đã đăng..." (khớp gần với BRD NTF-03 hơn Demo) | 3 nguồn diễn đạt khác nhau nhưng cùng 1 sự kiện |
| 4 | Carrier đã lấy hàng [Sender+Receiver] | NTF-04: "Người vận chuyển đã lấy hàng và bắt đầu giao" | "Người mang giúp đã nhận hàng" — "Cập nhật khi carrier xác nhận lấy hàng" | Không quan sát trong 82 ảnh đã quét | — |
| 5 | Carrier đã giao (DELIVERED) [Receiver+Sender] | NTF-05: "Đơn đã được giao — vui lòng xác nhận đã nhận hàng" | Không có mục riêng (có thể gộp vào #6) | Không quan sát | — |
| 6 | Receiver xác nhận nhận → COMPLETED [Sender+Carrier] | NTF-06: "Đơn đã hoàn tất — cảm ơn bạn!" | "Đơn đã hoàn thành — đánh giá ngay" — "Nhắc đánh giá sau khi hoàn tất" | "Đơn đã hoàn thành — đánh giá ngay" — ""...đã giao xong. Hãy đánh giá [Carrier]..."" (khớp Y HỆT Demo) | Demo/Figma gắn kèm lời mời ĐÁNH GIÁ — xem C-GIFT-01 (đã Resolved: rating deferred, phase sau) |
| 6b | Nhận được đánh giá 5 sao [Carrier] | Không có mục tương ứng | "Bạn nhận được đánh giá 5 sao" — "Kèm nhận xét từ đối tác đơn hàng" | "Bạn nhận được đánh giá 5 sao" — "[Tên]: 'Đúng giờ, nhiệt tình...'" (khớp Y HỆT Demo) | Loại thông báo MỚI so với BRD — theo C-GIFT-01 (Resolved 2026-07-27: rating out-of-scope v1.0) → loại này KHÔNG áp dụng cho v1.0 |
| 7 | Nhận quà ảo [Carrier] | NTF-07: "Bạn nhận được một món quà cảm ơn 🎁 — mở Trang cá nhân để xem" | Không có mục riêng | "Bạn nhận được một món quà cảm ơn 🎁" — "[Tên] đã gửi tặng bạn một món quà..." (khớp gần BRD) | Dùng cho REQ-GIFT-001 (trong scope v1.0) |
| 8 | Đơn bị huỷ [các bên còn lại] | NTF-08: "Đơn đã bị huỷ bởi [vai trò] — lý do: […]" | Không có mục riêng | "Đơn của bạn đã bị người vận chuyển huỷ" — "Lý do: 'bận họp gấp'. Đơn đang chờ người vận chuyển mới..." | Figma cụ thể hơn BRD (thêm câu "đang chờ người mới"), dùng làm verbatim ưu tiên |
| 9 | Tin quá hạn chưa ghép [Sender] | NTF-09: "Tin của bạn đã quá hạn — gỡ hoặc đăng lại nếu vẫn cần" | Không có mục riêng | Không quan sát | Liên quan REQ-ORD-004/C-ORD-03 (đã Resolved: hạn theo giá trị user chọn) |
| 10 | Nhắc khung giờ hẹn giao [Sender/Receiver] | Không có mục tương ứng | "Sắp đến khung giờ hẹn giao" — "Nhắc lịch giao hàng" | "Sắp đến khung giờ hẹn giao" — "Đơn của bạn hẹn giao trong khung 17:00–18:30 hôm nay." (khớp Y HỆT Demo) | Loại MỚI so với BRD, có mặt cả Demo lẫn Figma → khả năng cao THUỘC scope thật, BRD D6 có thể sót |
| 11 | Cộng đồng đạt mốc X đơn (gamification/CO2) | Không có mục tương ứng | "Cộng đồng FoxEco vừa đạt mốc X đơn" — "Thông điệp 'tiết kiệm Y kg CO₂'" | Không quan sát trong 82 ảnh | Theo C-USR-01 (Resolved 2026-07-27: tier/điểm/CO2 deferred, phase sau) → loại này KHÔNG áp dụng cho v1.0 |
| 12 | Nhắc nguyên tắc an toàn (static) | Không có mục tương ứng | "Nhắc lại nguyên tắc an toàn" — "Không gửi/nhận hàng cấm" | Không quan sát | Thông báo tĩnh, không gắn sự kiện nghiệp vụ cụ thể |

**Khuyến nghị cho BA/PO:** chọn 1 trong 3 hướng — (a) dùng nguyên BRD D6 (9 loại, NTF-01..09) làm chuẩn — đơn giản nhất nhưng thiếu 3 loại đã thấy trên UI thật (#6b, #10 xác nhận có trên Figma; #11/#12 chỉ có ở Demo); (b) dùng Figma + Demo (khớp nhau ở hầu hết các dòng) làm chuẩn, bỏ #6b/#11 vì đã Resolved deferred (rating/tier); (c) hợp nhất cả 3 thành danh sách mới ~10 loại (bỏ #6b, #11 theo 2 clarification đã resolved; giữ lại #10 "nhắc khung giờ" vì có bằng chứng UI thật). Cho tới khi BA chọn, generate-tc tạm dùng hướng (c) làm baseline vì có bằng chứng UI thật nhiều nhất. Status vẫn giữ Open (non-blocking) — chưa chốt chính thức.
