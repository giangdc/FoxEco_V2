# Bug Index — Router

> Chỉ trả lời "cần biết X thì đọc ở đâu". KHÔNG dựng bảng trạng thái/tường thuật ở đây —
> xem `SKILL.md §bug-index` của skill `log-bug`.

## Nguồn chuẩn

| Cần gì | Đọc ở đâu |
|---|---|
| Bug đã push Jira (mirror, trạng thái mới nhất) | `05_bug-reports/jira/<KEY>-*.md` (glob đệ quy) |
| Bug local chưa push Jira | `05_bug-reports/draft/BUG-NNN-*.md` (glob đệ quy) — hiện có **5** file |
| Tổng quan status/aging | `/log-bug --status` (sinh on-demand, không lưu ở đây) |

## Bug → ID local → RUN

> Chỉ để tra `BUG-NNN` cũ khi file đã chuyển sang `jira/` (Jira không giữ thông tin này).

| BUG-NNN (local) | Jira Key | Nguồn (RUN/vibe-test) |
|---|---|---|
| BUG-001 | [FE-291](https://foxproject.atlassian.net/browse/FE-291) | VR-001-USR-2026-09-18 (ứng viên bug B3) |
| BUG-002 | [FE-292](https://foxproject.atlassian.net/browse/FE-292) | VR-001-USR-2026-09-18 (ứng viên bug B4) |
| BUG-003 | [FE-293](https://foxproject.atlassian.net/browse/FE-293) | VR-001-USR-2026-09-18 (ứng viên bug B6) |
| BUG-004 | [FE-294](https://foxproject.atlassian.net/browse/FE-294) | VR-001-USR-2026-09-18 (ứng viên bug B7) |
| BUG-005 | [FE-295](https://foxproject.atlassian.net/browse/FE-295) | VR-001-USR-2026-09-18 (ứng viên bug B8) |
| BUG-006 | [FE-298](https://foxproject.atlassian.net/browse/FE-298) | VR-001-USR-2026-09-18 (ứng viên bug B5, `TC-USR-039`) |
| BUG-007 | [FE-297](https://foxproject.atlassian.net/browse/FE-297) | recheck 2026-09-18 (MNV bị cắt trên màn "Cập nhật thông tin", `TC-USR-024`) — pushed `severity: Low`/`defect_type: Interface` sau khi đổi từ `Suggest` do board bắt buộc Defect Type lúc tạo issue |
| *(không có — xem ghi chú)* | [FE-290](https://foxproject.atlassian.net/browse/FE-290) | VR-001-USR-2026-09-18 (ứng viên bug B2) — push thủ công **trước khi** `/log-bug` được gọi lần đầu trong dự án này, nên không có draft `BUG-NNN` gốc |

## Kiểm kê `draft/`

| File | Lý do còn là draft |
|---|---|
| `BUG-008-khong-load-sdt-dia-chi-tu-hris.md` | **QC GiangDC2 chốt 2026-09-18: chưa push Jira.** Bug đã đủ evidence (2 TC FAIL, 2 tài khoản, 2 phiên) — chỉ chờ QC xác nhận mức `severity` (đang để `Major`, cao hơn nhóm bug câu chữ của VR-001) rồi mới `/log-bug --push-jira BUG-008`. |
| `BUG-009-chan-nhung-khong-hien-loi-o-truong-thieu.md` | **QC GiangDC2 chốt 2026-09-18: chưa push Jira.** Gộp 6 TC FAIL cùng nguyên nhân (B1 của VR-002) — chờ QC chốt có nâng `priority` lên `P1` không (nhóm chứa `TC-ORD-063` P1) rồi mới `/log-bug --push-jira BUG-009`. |
| `BUG-010-thoat-wizard-khong-co-popup-xac-nhan.md` | **QC GiangDC2 chốt 2026-09-18: chưa push Jira.** Nghi cùng component với `TC-USR-045` (VR-001) — chờ QC/dev chốt log theo scope ORD hay phạm vi hệ thống rồi mới push. |
| `BUG-011-chon-duoc-buoi-da-troi-qua.md` | **QC GiangDC2 chốt 2026-09-18: chưa push Jira.** Rule chỉ có ở `C-ORD-15(b)`, không có trong PRD — chờ QC xác nhận giữ căn cứ clarification trước khi push. |
| `BUG-012-buoi-mong-muon-khong-co-gia-tri-mac-dinh.md` | **QC GiangDC2 chốt 2026-09-18: chưa push Jira.** Căn cứ PRD đã xác minh lại tại chỗ (`§8.1.4` + `AC-06.1.01`) — chờ QC gom cùng lô 4 draft ORD/USR rồi push một lượt. |
