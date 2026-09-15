# Requirement Traceability — v1.1 · Module TS

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation` của `DOC-v1.1-01` = `FR<NN>` / `BR<FF>-NN` / `AC-{US}.{Scenario}.{Case}` / `NFR-NN` ⇒ **Schema A**.
> Chỉ chứa REQ **NEW** của lượt delta này. REQ v1.0 (`REQ-TS-001..005`) CARRIED nguyên trạng — xem `v1.0/TS-trust-safety/requirement_traceability.md`, KHÔNG lặp lại ở đây.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module TS — DOC-v1.1-01

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-TS-006 | `FR16`, `US31`, `AC-31.1.01`, `AC-31.1.02`, `AC-31.2.01` | `DOC-v1.1-01` §8.16 (trang 50-51) · §6.1 US31 (trang 13) · §6.2 AC-31.x.xx (trang 29-30) | SC-TS-008, SC-TS-009, SC-TS-010, SC-TS-011, SC-TS-012, SC-TS-013, SC-TS-014, SC-TS-015 | — |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-TS-006 · Báo cáo sự cố & hỗ trợ qua Google Form nhúng WebView (`FR16`)
📍 `DOC-v1.1-01 §8.16 "FR16 — Báo cáo sự cố & hỗ trợ" · trang 50-51`  ·  Clarif: —

> Nguồn #1 — Description (§8.16):
> "Kênh tiếp nhận sự cố/góp ý ở Phase 1: mở Google Form trong WebView với ngữ cảnh đơn được điền sẵn, không xây back-office trong ứng dụng."

> Nguồn #2 — US31 (§6.1, trang 13):
> "Là Người gửi/Người vận chuyển/Người nhận, tôi muốn báo sự cố ngay từ màn theo dõi đơn kèm ảnh minh hoạ, để được hỗ trợ mà không phải mô tả lại toàn bộ ngữ cảnh đơn."

> Nguồn #3 — Trigger/Actor (§8.16):
> "Trigger: Bấm button "Báo cáo sự cố" ở góc trên bên phải màn Theo dõi đơn (button bo tròn nền cam nhạt, gồm icon cảnh báo + chữ). Actor: Người gửi · Người vận chuyển · Người nhận · Admin vận hành (xử lý)."

↳ **Ghi chú:** ⭐ **REQ hoàn toàn MỚI, đảo ngược 1 kết luận cũ.** v1.0 đã chốt màn "Báo sự cố" là **out of scope** (`C-CNL-01` Resolved 2026-07-27, home canonical ở `CNL-huy-don/risk_assessment.md`, tham chiếu tại `DLV-giao-nhan/requirement_traceability.md` dòng REQ-DLV-015: *"Màn 'Báo sự cố' chưa có đặc tả — out of scope v1.0"*). PRD v1.1 §8.16 giờ đặc tả đầy đủ luồng này (WebView + Google Form Phase 1, 6 business rule BR16-01..06, đủ Given/When/Then ở 3 AC) ⇒ tính năng NAY **VÀO SCOPE**. ⚠️ **`C-CNL-01` (home ở module `CNL`) đã lỗi thời kể từ v1.1** — nhưng `CNL-huy-don/` KHÔNG có delta ở lượt này (PRD không mang thêm thông tin nào cho CNL, xem quyết định ở `MASTER-MEMORY.md`) nên file đó **không được sửa**; ghi nhận ở đây để trace không đứt, tránh người đọc sau tưởng CNL vẫn đúng khi trích `C-CNL-01`. Fan-out 8 SC theo Scenario Sufficiency Rule: 1 happy path + 1 negative (thiếu trường bắt buộc) + 2 boundary/vế phủ định về ảnh (tuỳ chọn, tối đa 5) + 1 nhánh lỗi mạng + 1 vòng đời phiên (reset) + 1 đặc điểm field prefill (sửa được, khác field chỉ-đọc-từ-SSO ở module khác) + 1 UI vị trí trigger/đa vai trò.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
