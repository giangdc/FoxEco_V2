# FoxEco — Knowledge Pack v1.0

> **Mục đích:** đóng gói toàn bộ **kiến thức nghiệp vụ đã tích luỹ** của dự án FoxEco (từ đợt phân tích 2026-07-24 → 2026-07-31) thành tài liệu độc lập, để dùng làm **nguồn đầu vào** cho một project QA mới chạy lại `init-project` + `analyze-requirements` bằng bộ skill mới (qc-claude-v1 **v1.1**, layout `module-first`).
>
> **Ngày đóng gói:** 2026-09-04 · **Người đóng gói:** GiangDC2 (qua Claude Code)
> **Project nguồn:** `/home/giangdc2/AI/FoxEco` (git `main`, commit gần nhất `3be4b01`)

---

## 1. Bộ này giải quyết vấn đề gì

Nếu chỉ copy `00_input/` sang project mới rồi chạy `analyze-requirements --init`, bạn **mất toàn bộ** phần kiến thức KHÔNG nằm trong tài liệu gốc:

| Loại kiến thức | Nằm ở đâu trước đây | Có trong BRD/PRD/Figma? |
|---|---|---|
| 25 clarification + câu trả lời BA/PO (chủ yếu qua chat) | `MEMORY.md §6/§6.1` | ❌ Không |
| Ma trận nhãn nút × trạng thái × vai trò (màn Theo dõi đơn) | `test_scenario_map.md` | ⚠ Một phần (Figma xác nhận sau) |
| Hành vi app STG thật đã vibe-test (2 phiên, thiết bị Android thật) | `08_test-runs/vibe/` (chưa commit) | ❌ Không |
| Scope Phase 1 do PM chốt + danh mục Out-of-scope v1.0 | `Project_rule.md` | ❌ Không |
| Kết quả merge phân tích của QC anhdc4 (project đã xoá) | git `6f0b0cd` | ❌ Không |
| Mâu thuẫn nguồn chưa giải quyết + TC dự kiến FAIL có chủ đích | `CHANGELOG.md`, review report | ❌ Không |

→ Toàn bộ phần trên đã được trích xuất vào bộ này.

## 2. Nội dung bộ

| File | Vai trò khi analyze lại | Dùng làm nguồn trích dẫn? |
|---|---|---|
| `KP-01_business-knowledge.md` | **NGUỒN CHÍNH** — quy tắc nghiệp vụ/hành vi UI đã xác nhận ngoài tài liệu, gom theo module | ✅ Có — trích Source Quote trực tiếp |
| `KP-02_clarification-register.md` | 25 clarification + trạng thái + câu trả lời BA/PO | ✅ Có |
| `KP-03_scope-and-project-rules.md` | Scope Phase 1, Out-of-scope, 2 custom rule, DOC notation, quality gate | ✅ Có — seed cho `Project_rule.md` mới |
| `KP-04_prior-analysis-baseline.md` | Inventory 46 REQ / 92 SC / 323 TC của đợt cũ | ⛔ **REFERENCE-ONLY** — chỉ để đối chiếu coverage sau khi analyze xong, **KHÔNG** trích làm nguồn requirement |
| `KP-05_open-gaps-and-conflicts.md` | Câu hỏi còn treo, mâu thuẫn nguồn, gap chưa có nguồn, TC dự kiến FAIL | ✅ Có — nạp thẳng thành clarification mới |
| `KP-06_source-document-registry.md` | Danh mục 4 tài liệu gốc + đường dẫn + cách xử lý từng loại file | ✅ Có |
| `KP-07_notification-matrix.md` | Ma trận 12 sự kiện thông báo × 3 nguồn (BRD/demo/Figma) — clarification `C-NTF-01` chờ BA chốt | ✅ Có |
| `evidence/` | **Bằng chứng vibe-test gốc** — 25 screenshot + log + 17 locator, copy từ `08_test-runs/vibe/` (ở project cũ chưa commit vào git) | ✅ Có — độ tin cậy cao nhất |

## 3. Cách dùng ở project mới

```
1. /init-project                          # scaffold project mới (bộ skill v1.1)
2. Copy tài liệu gốc  → 00_input/v1.0/    # theo KP-06 §2 (BRD v3.2, PRD docx, prototype, 82 ảnh Figma)
3. Copy CẢ THƯ MỤC NÀY → 00_input/v1.0/_knowledge-pack/    # gồm cả evidence/
4. Seed Project_rule.md từ KP-03          # scope, custom rules, DOC notation, module codes
5. /analyze-requirements --init @00_input/v1.0
6. Đối chiếu kết quả với KP-04 (baseline cũ) → tìm scenario bị bỏ sót
7. Nạp KP-05 thành clarification register của bản mới
```

### Quy ước DOC ID đề xuất cho project mới

| DOC ID mới | Nội dung |
|---|---|
| `DOC-v1.0-01` | FoxEco BRD **v3.2** (bản mới nhất — v3.1 chỉ giữ để tra lịch sử) |
| `DOC-v1.0-02` | PRD tái dựng từ demo (`tổng hợp từ file demo.docx`) |
| `DOC-v1.0-03` | Prototype tương tác 3 vai trò (HTML, reference-only) |
| `DOC-v1.0-04` | Figma UI mockup — 82 ảnh (`Fox Eco Doc/images/*`) |
| `DOC-v1.0-05` | **Knowledge Pack này** — nguồn phi-tài-liệu đã xác nhận |

→ Khi analyze mới cần trích dẫn kiến thức từ bộ này, dùng Source Location dạng:
`DOC-v1.0-05 KP-01 §5.2 KB-DLV-01`

## 4. ⚠ Nguyên tắc bắt buộc khi dùng bộ này

1. **Không coi KP là tài liệu yêu cầu chính thức.** Đây là *ghi chép của QA* về những gì BA/PO đã trả lời và những gì quan sát được trên app/Figma. BRD/PRD vẫn là nguồn ưu tiên khi mâu thuẫn.
2. **Mỗi mục đều ghi rõ Nguồn + Ngày + Độ tin cậy.** Mục nào ghi `⚠ Chưa xác nhận` thì **KHÔNG viết TC khẳng định** — mở clarification (theo custom rule §10.1, xem KP-03).
3. **KP-04 tuyệt đối không dùng làm nguồn requirement.** Nó là kết quả suy luận của đợt cũ; dùng nó để "copy ngược" sẽ tái tạo luôn cả sai sót cũ. Chỉ dùng ở bước đối chiếu coverage cuối cùng.
4. **Kiến thức từ vibe-test (KP-01 §10) có độ tin cậy CAO NHẤT** — quan sát trực tiếp trên thiết bị thật, có screenshot. Khi mâu thuẫn với BRD → đó là **bug hoặc spec đã đổi**, phải mở clarification chứ không im lặng chọn bên nào.
