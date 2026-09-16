# Requirement Traceability — v1.1 · Module HOME

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation` của `DOC-v1.1-01` = `FR<NN>` / `BR<FF>-NN` / `AC-{US}.{Scenario}.{Case}` / `NFR-NN` (khác hẳn v1.0 — xem `Project_rule.md §DOC Notation`) ⇒ **Schema A**.
> ⚠️ Delta này CHỈ chứa REQ mới; 8 REQ carry nguyên trạng từ v1.0 (`REQ-HOME-001..010`) xem `02_analyze-requirements/v1.0/HOME-trang-chu/requirement_traceability.md`.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module HOME — DOC-v1.1-01

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-HOME-011 | `US11`, `AC-11.1.01`, `AC-11.2.01` | §6.1 (trang 12) · §6.2 (trang 19) | SC-HOME-019 (MODIFIED), SC-HOME-021 (MODIFIED), SC-HOME-025 (NEW) | C-HOME-03 (Resolved) |
| REQ-HOME-012 | `FR17`, `BR17-01..03` | §8.17, §8.17.1 (trang 51) | SC-HOME-025, SC-HOME-026, SC-HOME-027 (NEW) | — |
| REQ-HOME-013 | `NFR01` | §9 (trang 53) | SC-HOME-028 (NEW) | — |

> **Cập nhật 2026-09-17 — REQ v1.0 có SC thay đổi theo câu trả lời BA** (REQ quote giữ ở `v1.0/HOME-trang-chu/requirement_traceability.md`, ⛔ không chép lại):
>
> | REQ ID (v1.0) | Thay đổi SC | Clarification |
> |---|---|---|
> | REQ-HOME-004 (card "Đóng góp của bạn") | SC-HOME-008 (MODIFIED) · SC-HOME-029, SC-HOME-030 (NEW) | C-HOME-06 (Partially — vòng 2) |
> | REQ-HOME-005 (section "Đơn của tôi") | SC-HOME-010 (DEPRECATED → thay bằng SC-HOME-026 của REQ-HOME-012) | C-HOME-05 (Resolved 2026-09-17) |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-HOME-011 · "Tin mới" hiển thị đúng 5 tin, loại trừ MATCHED/EXPIRED/của chính mình
📍 `DOC-v1.1-01 §6.1 "Danh sách User Story" · US11 · trang 12` và `§6.2 "Acceptance Criteria" · AC-11.1.01/AC-11.2.01 · trang 19`  ·  Clarif: `C-HOME-03` (Resolved 2026-09-15)

> US11: "Là Người vận chuyển, tôi muốn xem tối đa 5 tin cần gửi mới nhất trên trang chủ, để nhanh chóng thấy tin thuận tuyến mà không phải tìm."
>
> AC-11.1.01 — Given: "Trong khu vực của người dùng có 12 tin NEED đang ở POSTED." — When: "Mở trang chủ." — Then: "Khối 'Tin mới' hiển thị đúng 5 tin mới nhất. Có nút 'Xem thêm trên Bảng tin'. Tin đã MATCHED, EXPIRED hoặc tin của chính người dùng không nằm trong danh sách gợi ý."
>
> AC-11.2.01 — Given: "Không có tin NEED nào ở POSTED trong khu vực của người dùng." — When: "Mở trang chủ." — Then: "Khối 'Tin mới' hiển thị empty state: icon nét mảnh + 'Chưa có tin nào trong khu vực của bạn' + một dòng giải thích + đúng một CTA 'Đăng tin ngay'. Không hiện skeleton kéo dài; phân biệt rõ đang tải và không có dữ liệu."

↳ **Ghi chú:** ⭐ **REQ này RESOLVE `C-HOME-03`** (Open từ 2026-07, kế thừa `KP-05 §2.1` — mâu thuẫn "1 tin" (PRD-demo cũ) vs "5 tin" (BRD `US-D06`) chưa ai chốt). PRD chính thức `DOC-v1.1-01` — độc lập với cả 2 nguồn cũ — xác nhận **5**, đồng thời bổ sung điều kiện lọc mà v1.0 CHƯA có: loại tin đã MATCHED, đã EXPIRED, hoặc do chính người dùng đăng khỏi danh sách gợi ý. US11 khoanh vùng theo góc nhìn "Người vận chuyển" nhưng không mâu thuẫn với kết luận `C-ORD-07` (Resolved — section hiển thị cho cả Sender lẫn Carrier theo UI thật): AC-11.2.01 dùng chủ ngữ trung tính "người dùng", không giới hạn vai trò. Nhánh empty state của AC-11.2.01 trùng khớp với `EMP-01` ở `REQ-HOME-012` — dùng làm 2 nguồn PRD củng cố lẫn nhau cho cùng 1 SC (`SC-HOME-025`).

---

### REQ-HOME-012 · Empty state Trang chủ — đặc tả riêng cho 3 khu vực
📍 `DOC-v1.1-01 §8.17 "FR17 — Trạng thái trống (Empty state)" · §8.17.1 "Danh mục empty state" · trang 51`  ·  Clarif: —

> Description: "Đặc tả nội dung hiển thị khi chưa có dữ liệu, để người dùng mới hiểu cần làm gì thay vì tưởng ứng dụng bị lỗi."
>
> §8.17.1 (bảng, 3 dòng liên quan Trang chủ):
> EMP-01 | Trang chủ — Tin mới | "Chưa có tin nào trong khu vực của bạn" + "Đăng tin để đồng nghiệp nhìn thấy nhu cầu của bạn" | CTA "Đăng tin ngay"
> EMP-02 | Trang chủ — Đơn của tôi | "Bạn chưa có đơn nào đang chạy" | CTA "Tạo đơn gửi hàng"
> EMP-03 | Trang chủ — Hero & cộng đồng | Hero hiện "0 · Chưa có đóng góp nào"; cụm cộng đồng hiện "0 đơn · 0 người" | CTA "—"
>
> BR17-01: "Mỗi empty state gồm: icon nét mảnh màu neutral + một dòng tiêu đề + một dòng giải thích + tối đa một CTA."
> BR17-02: "Không dùng ảnh minh hoạ nặng; không hiện skeleton vô hạn — phân biệt rõ đang tải và không có dữ liệu."
> BR17-03: "Empty state không được che thanh tab dưới và vẫn cuộn được."

↳ **Ghi chú:** ⭐ **REQ này RESOLVE `REQ-HOME-010`/`SC-HOME-024`** (v1.0 — "Empty state màn Trang chủ", Implicit, không có quote đặc tả, ghi dạng GHI NHẬN không assert vì `C-ORD-06` Open). PRD giờ đặc tả RIÊNG cho từng khu vực (Tin mới / Đơn của tôi / Hero-cộng đồng) thay vì 1 trạng thái rỗng gộp chung của cả màn — theo đúng Scenario Sufficiency Rule, đây là 3 REQ/SC atomic khác nhau chứ không phải 1. `SC-HOME-024` gộp cũ HẾT HIỆU LỰC — xem `CHANGELOG.md §2`. ⚠️ Đây chỉ resolve phần **v1.1 sở hữu** (Trang chủ); `C-ORD-06` vẫn còn liên quan tới `ACT`/`FEED`/`GIFT`/`NTF` — các module đó chưa được rà lại trong lượt delta này, `C-ORD-06` KHÔNG được đóng hoàn toàn ở đây.

---

### REQ-HOME-013 · Hiệu năng hiển thị Trang chủ
📍 `DOC-v1.1-01 §9 "Non-Functional Requirements" · NFR01 · trang 53`  ·  Clarif: —

> NFR01 | Performance | "Bảng tin và trang chủ hiển thị nội dung đầu tiên < 2 giây (p95) trên mạng 4G với 1.000 người dùng đồng thời." | Cách đo: "Load test trước go-live."

↳ **Ghi chú:** NFR mới, không có tương đương ở v1.0 (module trước đây không có yêu cầu hiệu năng nào). Cần môi trường load-test (1.000 người dùng đồng thời) — KHÔNG kiểm chứng được bằng manual/vibe-test thông thường; `SC-HOME-028` viết dạng ghi nhận yêu cầu + defer cho automation/load-test, không phải TC manual chạy tay. REQ này dùng chung ngưỡng với `FEED` (cùng NFR01) — `FEED` chưa được rà lại trong lượt delta này nên chưa có REQ tương ứng bên đó.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
> 8 REQ carry (`REQ-HOME-001..010`) xem `v1.0/HOME-trang-chu/requirement_traceability.md` — KHÔNG duplicate ở đây.
