# Scope Ledger — VR-007 — module ASN — SCOPE_TOTAL = 26 TC

> Seed từ: `coverage-ASN.md` — trạng thái trước phiên: có verdict **2/26** (0 PASS · 2 `⛔ N-A`).
> Tập chạy phiên này: **24 TC pending**. Không TC nào đã PASS ⇒ ⛔ không phát sinh câu hỏi Step 1.2.
> Lô: **lô 1** — 3 TC chốt. Dừng vì **hết sức phiên**, ⛔ không phải hết TC.

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-ASN-001 | ⏳ NOT_RUN | — | — | **Lý do:** cần tin + **tài khoản thứ 2** thao tác nhận đơn. ⚠️ *(đính chính 08:40: **đăng tin ĐƯỢC** — lý do cũ nhắc bug `B1` đã RÚT LẠI, xem callout đầu file)*; thêm nữa cần tài khoản B nhận đơn (OTP) |
| TC-ASN-002 | ⏳ NOT_RUN | — | — | **Lý do:** cần tin + **tài khoản thứ 2** thao tác nhận đơn. ⚠️ *(đính chính 08:40: **đăng tin ĐƯỢC** — lý do cũ nhắc bug `B1` đã RÚT LẠI, xem callout đầu file)*; cần tài khoản B mở Chi tiết tin của A (OTP) |
| TC-ASN-003 | ⏳ NOT_RUN | — | — | **Lý do:** cần **nhiều tài khoản trên nhiều thiết bị** — chỉ có 1 emulator, và đăng nhập tài khoản khác vướng **OTP nhập tay**. 🔍 Tài khoản đang đăng nhập (`Đặng Châu Anh`) **không có đơn nào ở vai người GỬI + trạng thái `Đã ghép`** (chỉ có `Nhận:`+`Đã ghép`, `Gửi:`+`Đã giao`, `Gửi:`+`Đã huỷ`) ⇒ ⛔ không verify được Expected vốn viết cho **chủ tin** |
| TC-ASN-004 | ⏳ NOT_RUN | — | — | **Lý do:** cần **nhiều tài khoản trên nhiều thiết bị** — chỉ có 1 emulator, và đăng nhập tài khoản khác vướng **OTP nhập tay**. 🟢 **Đã thu được dữ kiện mạnh dù chưa chạy được TC** — xem `vibe-report.md §Đính chính VR-004`: màn Theo dõi đơn của **người NHẬN** hiện đủ `NGƯỜI GIAO HÀNG` = tên + **SĐT** + nút `Gọi`. ⛔ Chưa đủ để kết luận TC vì Expected viết cho **người gửi** (E4) và **người vận chuyển** (E3), không phải người nhận |
| TC-ASN-005 | ⏳ NOT_RUN | — | — | **Lý do:** cần **4 tài khoản** (A chủ tin · B Carrier · C người nhận · D người ngoài) + **lý do:** cần đăng tin need/offer — stg hiện **0 tin** và bug `b1` (vr-004) chặn đăng tin need (`400 req_400`, app im lặng) |
| TC-ASN-006 | ⏳ NOT_RUN | — | — | **Lý do:** cần **2 thiết bị** bấm xác nhận cách nhau <2 giây — chỉ có 1 emulator; kèm **lý do:** cần đăng tin need/offer — stg hiện **0 tin** và bug `b1` (vr-004) chặn đăng tin need (`400 req_400`, app im lặng) |
| TC-ASN-007 | ⏳ NOT_RUN | — | — | **Lý do:** cần tin + **tài khoản thứ 2** thao tác nhận đơn. ⚠️ *(đính chính 08:40: **đăng tin ĐƯỢC** — lý do cũ nhắc bug `B1` đã RÚT LẠI, xem callout đầu file)*. 🔍 Bảng tin hiện **rỗng hoàn toàn** ⇒ ⛔ không phân biệt được *"tin biến mất vì đã ghép"* với *"không có tin nào từ đầu"* — chạy TC này lúc này sẽ cho PASS oan |
| TC-ASN-008 | ⏳ NOT_RUN | — | — | **Lý do:** cần **3 thiết bị** 3 vai cùng mở màn để đo mốc ≤5 giây — chỉ có 1 emulator |
| TC-ASN-009 | ⏳ NOT_RUN | — | — | **Lý do:** cần tin + **tài khoản thứ 2** thao tác nhận đơn. ⚠️ *(đính chính 08:40: **đăng tin ĐƯỢC** — lý do cũ nhắc bug `B1` đã RÚT LẠI, xem callout đầu file)*; cần tin NEED trùng tuyến với 1 tin OFFER có sẵn |
| TC-ASN-010 | ⏳ NOT_RUN | — | — | **Lý do:** cần tin + **tài khoản thứ 2** thao tác nhận đơn. ⚠️ *(đính chính 08:40: **đăng tin ĐƯỢC** — lý do cũ nhắc bug `B1` đã RÚT LẠI, xem callout đầu file)*; cần thông báo khớp tuyến tồn tại trước |
| TC-ASN-011 | ⏳ NOT_RUN | — | — | **Lý do:** cần seed `SEED-ASN-01` (1 tin OFFER của tài khoản B) + 1 tin NEED lệch điểm giao — **lý do:** cần đăng tin need/offer — stg hiện **0 tin** và bug `b1` (vr-004) chặn đăng tin need (`400 req_400`, app im lặng) |
| TC-ASN-012 | ⏳ NOT_RUN | — | — | **Lý do:** cần `SEED-ASN-01` + 1 tin NEED lệch khoảng ngày — **lý do:** cần đăng tin need/offer — stg hiện **0 tin** và bug `b1` (vr-004) chặn đăng tin need (`400 req_400`, app im lặng) |
| TC-ASN-013 | ✅ PASS | 1 | run này | `VR-007-ASN-2026-09-19/screenshots/TC-ASN-013__verify-khong-thong-bao-tin-cua-minh.png` |
| TC-ASN-014 | ⏳ NOT_RUN | — | — | **Lý do:** cần tin + **tài khoản thứ 2** thao tác nhận đơn. ⚠️ *(đính chính 08:40: **đăng tin ĐƯỢC** — lý do cũ nhắc bug `B1` đã RÚT LẠI, xem callout đầu file)*; cần **6 tin NEED** khớp cùng tuyến |
| TC-ASN-015 | ⏳ NOT_RUN | — | — | **Lý do:** cần tin + **tài khoản thứ 2** thao tác nhận đơn. ⚠️ *(đính chính 08:40: **đăng tin ĐƯỢC** — lý do cũ nhắc bug `B1` đã RÚT LẠI, xem callout đầu file)*; cần 1 OFFER + **3 tin NEED** khớp (2 tài khoản) |
| TC-ASN-016 | ⏳ NOT_RUN | — | — | **Lý do:** cần tin + **tài khoản thứ 2** thao tác nhận đơn. ⚠️ *(đính chính 08:40: **đăng tin ĐƯỢC** — lý do cũ nhắc bug `B1` đã RÚT LẠI, xem callout đầu file)*; cần 1 OFFER + **5 tin NEED** khớp (2 tài khoản) |
| TC-ASN-017 | ⏳ NOT_RUN | — | — | **Lý do:** cần tin + **tài khoản thứ 2** thao tác nhận đơn. ⚠️ *(đính chính 08:40: **đăng tin ĐƯỢC** — lý do cũ nhắc bug `B1` đã RÚT LẠI, xem callout đầu file)*; cần 1 OFFER + **6 tin NEED** khớp (2 tài khoản) |
| TC-ASN-018 | ⏳ NOT_RUN | — | — | **Lý do:** cần tin + **tài khoản thứ 2** thao tác nhận đơn. ⚠️ *(đính chính 08:40: **đăng tin ĐƯỢC** — lý do cũ nhắc bug `B1` đã RÚT LẠI, xem callout đầu file)*; cần 1 OFFER + 3 tin NEED đăng ở 3 thời điểm khác nhau |
| TC-ASN-019 | ⏳ NOT_RUN | — | — | **Lý do:** cần tin + **tài khoản thứ 2** thao tác nhận đơn. ⚠️ *(đính chính 08:40: **đăng tin ĐƯỢC** — lý do cũ nhắc bug `B1` đã RÚT LẠI, xem callout đầu file)*; cần thêm 1 tin NEED **đã quá hạn** (dev/QA lùi ngày) |
| TC-ASN-020 | ⏳ NOT_RUN | — | — | **Lý do:** cần tin + **tài khoản thứ 2** thao tác nhận đơn. ⚠️ *(đính chính 08:40: **đăng tin ĐƯỢC** — lý do cũ nhắc bug `B1` đã RÚT LẠI, xem callout đầu file)*; cần tài khoản B nhận rồi huỷ nhận đơn (OTP) |
| TC-ASN-021 | ✅ PASS | 1 | run này | `VR-007-ASN-2026-09-19/screenshots/TC-ASN-021__verify-hai-tin-doc-lap.png` |
| TC-ASN-022 | ⏳ NOT_RUN | — | — | **Lý do:** cần `SEED-ASN-01` + tin NEED trùng ngày nhưng lệch **buổi** — **lý do:** cần đăng tin need/offer — stg hiện **0 tin** và bug `b1` (vr-004) chặn đăng tin need (`400 req_400`, app im lặng) |
| TC-ASN-023 | ✅ PASS | 1 | run này | `VR-007-ASN-2026-09-19/screenshots/TC-ASN-023__verify-thong-bao-khop-tuyen.png` |
| TC-ASN-024 | ⛔ N-A | — | — | **Lý do:** cần công cụ **concurrency/load test gọi thẳng API** (JMeter/k6) bắn 50 request đồng thời — fragment `TC-ASN-v1.1.md` ghi rõ *"⛔ không thực hiện bằng thao tác tay trên UI"*, giao automation/backend. ⛔ Ngoài phạm vi `vibe-test` UI thuần |
| TC-ASN-025 | ⏳ NOT_RUN | — | — | **Lý do:** cần **2 tuyến OFFER độc lập** + 5 tin NEED cho tuyến 1 (tái dùng seed `TC-ASN-016`) — **lý do:** cần đăng tin need/offer — stg hiện **0 tin** và bug `b1` (vr-004) chặn đăng tin need (`400 req_400`, app im lặng) |
| TC-ASN-026 | ⛔ N-A | — | — | **Lý do:** cần **API client** (Postman/tương đương) + token của tài khoản không sở hữu tin, và kiểm **audit log** phía server — fragment ghi rõ *"UI không có đường dẫn tới tin OFFER của người khác"*, giao automation/backend/security test. ⛔ Ngoài phạm vi `vibe-test` UI thuần |

## Ghi chú phiên

- **Chạy 3/24 pending** → **3 PASS** (`TC-ASN-013` P1 · `TC-ASN-023` P2 · `TC-ASN-021` P3). Module từ **2/26** lên **5/26 có verdict cuối**.
- 🟢 **Phiên đầu tiên của ASN thu được verdict.** Lượt trước (07:58) khai 0/26 vì tưởng bug `B1` chặn đăng tin + OTP nhập tay — **cả hai đã bị bác bỏ** trong ngày.
- 🔑 **AI tự đổi tài khoản 2 lượt** (`stag_taipm@` ↔ `stag_anhdc4@`), mỗi lượt ~2 phút / 14 MCP call — ⛔ không cần người nhập OTP.
- 🛑 **Dừng vì HẾT SỨC PHIÊN**, ⛔ không phải hết TC chạy được. **21 TC còn nợ**, trong đó **18 TC chạy được ngay** với dữ liệu + tài khoản hiện có; chỉ `006`/`008` (cần 2–3 thiết bị) và `019` (cần dev lùi ngày) là còn chặn thật.
- 📌 5 tin sống trên STG + phân nhóm 21 TC còn nợ: xem `coverage-ASN.md` §Tổng hợp.
- ▶️ Chạy tiếp: `/vibe-test --module ASN` — bộ lọc pending tự bốc đúng 21 TC.
