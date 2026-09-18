# TC-USR-v1.1 — ID Mapping (renumber theo `Project_rule.md §Custom Rules §10.4`)

> Áp dụng `testcase-guide.md §A.2` chiến lược **(b) Renumber liên tục**. Lý do renumber: rule mới (Expected
> Result chỉ neo 1 dòng ở step cuối) buộc tách thêm TC cho 6 SC vốn có nhiều điểm kiểm chứng độc lập
> (`SC-USR-014` · `015` · `020` · `021` · `024`), làm lệch dải ID NEW cũ `TC-USR-014..037` (24 TC).
> TC của 5 SC MODIFIED (`TC-USR-002/003/008/012/013`) **giữ nguyên ID v1.0**, không đổi.

| ID cũ (2026-09-16/17) | ID mới (2026-09-17) | Ghi chú |
|---|---|---|
| TC-USR-014 | TC-USR-014 | Không đổi |
| TC-USR-015 | TC-USR-015 | Nội dung thu hẹp — chỉ giữ điểm kiểm banner (step cuối) |
| *(mới)* | TC-USR-016 | TC mới — tách điểm kiểm persist (mở lại xem giá trị) khỏi `TC-USR-015` cũ |
| TC-USR-016 | TC-USR-017 | Không đổi nội dung |
| TC-USR-017 | TC-USR-018 | Không đổi nội dung |
| TC-USR-018 | TC-USR-019 | Bỏ dòng Expected step giữa (step 5) |
| TC-USR-019 | TC-USR-020 | Không đổi nội dung |
| TC-USR-020 | TC-USR-021 | Thu hẹp — chỉ giữ lớp "khoảng trắng" |
| *(mới)* | TC-USR-022 | TC mới — lớp "+84 prefix" tách khỏi `TC-USR-020` cũ |
| *(mới)* | TC-USR-023 | TC mới — lớp "chứa chữ" tách khỏi `TC-USR-020` cũ |
| TC-USR-021 | TC-USR-024 | Gộp 5 điểm kiểm SSO vào 1 step Check cuối |
| TC-USR-022 | TC-USR-025 | Bỏ steps 14-15 (trùng phạm vi `SC-ORD-025`) |
| TC-USR-023 | TC-USR-026 | Không đổi nội dung |
| TC-USR-024 | TC-USR-027 | Bỏ dòng Expected step giữa (step 6) |
| TC-USR-025 | TC-USR-028 | Thu hẹp — chỉ giữ điểm "rời field ⇒ rỗng" |
| *(mới)* | TC-USR-029 | TC mới — điểm "lưu rỗng thành công" tách khỏi `TC-USR-025` cũ |
| *(mới)* | TC-USR-030 | TC mới — điểm "mở lại vẫn rỗng" tách khỏi `TC-USR-025` cũ |
| TC-USR-026 | TC-USR-031 | Thu hẹp — chỉ giữ vế biên 2 ký tự |
| *(mới)* | TC-USR-032 | TC mới — vế biên 3 ký tự tách khỏi `TC-USR-026` cũ |
| TC-USR-027 | TC-USR-033 | Bỏ dòng Expected step giữa (step 6) |
| TC-USR-028 | TC-USR-034 | Thu hẹp — chỉ giữ biến thể "Cẩm Lệ" có dấu |
| *(mới)* | TC-USR-035 | TC mới — biến thể "cam le" thường tách khỏi `TC-USR-028` cũ |
| *(mới)* | TC-USR-036 | TC mới — biến thể "CAM LE" hoa tách khỏi `TC-USR-028` cũ |
| TC-USR-029 | TC-USR-037 | Không đổi nội dung |
| TC-USR-030 | TC-USR-038 | Không đổi nội dung |
| TC-USR-031 | TC-USR-039 | Không đổi nội dung |
| TC-USR-032 | TC-USR-040 | Đổi thứ tự step 4/5, gộp 2 điểm kiểm |
| TC-USR-033 | TC-USR-041 | Không đổi nội dung |
| TC-USR-034 | TC-USR-042 | Không đổi nội dung |
| TC-USR-035 | TC-USR-043 | Đổi thứ tự step 4/5, gộp 2 điểm kiểm |
| TC-USR-036 | TC-USR-044 | Bỏ dòng Expected step giữa (step 4) |
| TC-USR-037 | TC-USR-045 | Thu hẹp — chỉ giữ điểm "không hộp thoại xác nhận" |
| *(mới)* | TC-USR-046 | TC mới — điểm "giá trị chưa lưu bị bỏ" tách khỏi `TC-USR-037` cũ |

**Không đổi ID (MODIFIED, giữ theo v1.0):** `TC-USR-002` · `TC-USR-003` · `TC-USR-008` · `TC-USR-012` · `TC-USR-013`.
