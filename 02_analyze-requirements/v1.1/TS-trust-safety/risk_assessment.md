# Risk Assessment — v1.1 · Module TS (DELTA)

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Clarification quote (layout v2).** Bảng risk đầy đủ v1.0 (5 dòng, không đổi) xem `v1.0/TS-trust-safety/risk_assessment.md` — KHÔNG lặp lại ở đây.

## Chi tiết rủi ro (bảng hợp nhất — chỉ risk có delta)

| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-TS-06 | TS / Báo sự cố | **(risk mới)** Tính năng mới đảo ngược kết luận `C-CNL-01` (v1.0: màn "Báo sự cố" out of scope) — nhưng chỉ trong phạm vi `TS` sở hữu; module `CNL` (nơi `C-CNL-01` là home canonical) và `DLV` (nơi `REQ-DLV-015` tham chiếu `C-CNL-01`) **chưa được rà lại** ở lượt delta này ⇒ nguy cơ người đọc sau trích `C-CNL-01` từ `CNL`/`DLV` tưởng vẫn "out of scope" | Medium | `DOC-v1.1-01` §8.16 vs `v1.0/CNL-huy-don/risk_assessment.md` (`C-CNL-01`) | `SC-TS-008..015` chỉ test bề mặt `TS` sở hữu (nút trigger + form + WebView) | Đã ghi cảnh báo chéo ở `requirement_traceability.md §2 REQ-TS-006`; **KHÔNG sửa file `CNL`/`DLV`** vì chưa rà lại chính thức lượt này | Open (ghi nhận, non-blocking) | REQ-TS-006 |
| RISK-TS-07 | TS / Đối chiếu MNV | **(risk mới)** BR16-03 "đối chiếu MNV ở khâu xử lý" là **quy trình phía Admin/vận hành** (ngoài app, ngoài WebView) — không có bề mặt để test qua UI end-user | Low | `DOC-v1.1-01` §8.16.1 BR16-03 | — (không test được qua app) | Ghi nhận là quy trình ngoài phạm vi automation/manual UI test; nêu rõ trong test report nếu có | Open (ghi nhận, non-blocking) | REQ-TS-006 |

## Clarifications (home của CL quote — layout v2)

> Không có CL mới ở lượt delta này — `FR16` được PRD đặc tả đầy đủ (Description/Actor/Trigger/Pre-Post-Conditions/6 BR/2 AC/field spec), không có vùng mơ hồ cần hỏi BA. 5 CL của v1.0 (nếu có) giữ nguyên trạng thái — xem `v1.0/TS-trust-safety/risk_assessment.md`.

## Vibe-check bổ sung 2026-09-15 — xác nhận luồng end-to-end trên demo

Đã chạy thử trực tiếp luồng "Báo cáo sự cố" trên demo `foxeco_demo/FoxEcoQC` (vai Sender), khác với `DLV`/`RISK-DLV-08` ở chỗ ô "Thêm ảnh" ở màn này **hoạt động thật** (mock có tăng đếm, không bị chặn như dropzone bên DLV):
> `00_input/v1.1/design/TS_03_baocaosucos_5anh_hople.png` — đính đủ 5 ảnh, nút "Thêm ảnh khác" tự **disabled** → khớp `SC-TS-011` (trần cứng 5, không cho thêm ảnh thứ 6).
> `00_input/v1.1/design/TS_04_baocaosucos_dudieukien_gui_enabled.png` — điền đủ Loại yêu cầu + Mô tả + SĐT → nút "Gửi" chuyển từ disabled sang enabled, đúng `SC-TS-009` chiều dương.
> `00_input/v1.1/design/TS_05_baocaosucos_daghinhanphanhoi.png` — sau khi Gửi: "Đã ghi nhận phản hồi" + đúng câu "Đội hỗ trợ FoxEco sẽ liên hệ lại số {SĐT} trong vòng 24 giờ làm việc" + nút "Quay lại đơn hàng" — khớp verbatim `SC-TS-008` Then.

↳ **Đây là module duy nhất trong lượt vibe-check này verify được TOÀN BỘ happy path + boundary end-to-end** (không bị chặn kỹ thuật như `DLV`). Nâng độ tin cậy cho `SC-TS-008/009/010/011` trước `generate-tc` — không cần dự phòng "app chưa cập nhật" như `RISK-DLV-08`/`RISK-DLV-11`.

## Khuyến nghị tổng thể
1. **Bề mặt `TS` (nút trigger + form + WebView) test đầy đủ được** — 8 SC phủ happy path, validation, boundary ảnh, mất mạng, vòng đời phiên, field prefill, đa vai trò. **Đã verify thật qua demo 2026-09-15** cho happy path + boundary ảnh + validation (xem mục Vibe-check trên) — mức tin cậy cao nhất trong các module rà đợt này.
2. **KHÔNG mở rộng phạm vi sang xử lý phía Admin** — "liên hệ lại trong 24 giờ làm việc" và "đối chiếu MNV" là quy trình ngoài app, chỉ ghi nhận cam kết hiển thị trên UI (`SC-TS-008`), không verify hành động thật của Admin.
3. **Khi delta `CNL`/`DLV` chạy ở lượt sau:** rà lại `C-CNL-01` và cross-ref `REQ-DLV-015` — hiện tại 2 file đó **chưa sửa**, chỉ có cảnh báo ở `RISK-TS-06` và ở `requirement_traceability.md` module này.
