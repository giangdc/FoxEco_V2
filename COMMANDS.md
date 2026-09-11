
# COMMANDS — foxeco-v2

> Cheat sheet copy-paste. Không nhớ cú pháp thì cứ gõ tiếng Việt, Claude tự route
> (vd "phân tích yêu cầu v1.0", "viết test case cho module AUTH").
> Sơ đồ pipeline + prerequisite: `PIPELINE.md`. Quy ước riêng: `02_analyze-requirements/Project_rule.md`.

## 0. Mở đầu mỗi phiên

```bash
# Nạp credentials (1 lần / session) — prefix ! để env sống suốt phiên
! source ~/.foxeco-v2/credentials.env

# Đang ở đâu trong pipeline?
/health-check
```

## 1. Chuẩn bị

| Việc | Lệnh |
|---|---|
| Khởi tạo project (đã chạy rồi) | `/init-project` |
| Tạo Test Plan | `/create-test-plan --create` |
| Xuất Test Plan bản FPT | `/create-test-plan --export` |

## 2. Phân tích yêu cầu

| Việc | Lệnh |
|---|---|
| Phân tích lần đầu | `/analyze-requirements --init @00_input/v1.0/` |
| Version mới (so với version trước) | `/analyze-requirements --delta --version v1.0 @00_input/v1.0/` |
| Cập nhật theo feedback BA | `/analyze-requirements --update "<nội dung BA chốt>"` |
| Rà lượt 2 tìm requirement bỏ sót | `/analyze-requirements --sweep --version v1.0` |
| Xem tổng quan (không sửa file) | `/analyze-requirements --review` |

## 3. Test case

| Việc | Lệnh |
|---|---|
| Sinh TC 1 module | `/generate-tc --module <MODULE>` |
| Sinh TC đầy đủ kỹ thuật thiết kế | `/generate-tc --module <MODULE> --mode comprehensive` |
| Chỉ vài kỹ thuật | `/generate-tc --techniques EP,BVA,EG` |
| Gộp fragment → TC-MASTER | `/generate-tc --consolidate` |
| Đồng bộ lại TC-MASTER | `/generate-tc --sync` |
| Review chất lượng TC (gate G1 ≥ 70) | `/review-tc --version v1.0` |
| Xuất bản thiết kế TC bản FPT | `/export-tc-rp --phase design` |

## 4. Chạy test bằng AI (vibe-test)

| Việc | Lệnh |
|---|---|
| Chạy TC chưa chạy của 1 module | `/vibe-test --module <MODULE>` |
| Chạy lại TOÀN BỘ TC (kể cả đã PASS) | `/vibe-test --all` |
| Retest sau khi dev fix | `/vibe-test --retest <TC-ID\|BUG-ID>` |
| Xem tiến độ vibe | `/vibe-test --status` |

> Mỗi TC phải có **≥1 ảnh riêng** tại điểm verify. Không có ảnh ⇒ không được ghi PASS.

## 5. Bug

| Việc | Lệnh |
|---|---|
| Tạo bug từ fail | `/log-bug` |
| Cập nhật trạng thái | `/log-bug --update BUG-001 --status "Fixed"` |
| Đóng bug (đã verify) | `/log-bug --close BUG-001` |
| Xem tổng quan bug | `/log-bug --status` |

## 6. Báo cáo

| Việc | Lệnh |
|---|---|
| Report sprint | `/test-report --sprint` |
| Report release (GO/NO-GO) | `/test-report --release --version v1.0` |
| So sánh 2 version | `/test-report --cross-version` |
| Xuất báo cáo kết quả bản FPT | `/export-tc-rp --phase report --round R1` |

## 7. Kiểm tra sức khoẻ dữ liệu

| Việc | Lệnh |
|---|---|
| Nhanh (< 30s) | `/health-check` |
| Đầy đủ (parse Excel, ghi file report) | `/health-check --full` |
| 1 version cụ thể | `/health-check --version v1.0` |

## 8. Commit

```bash
/commit-code          # sinh commit message chuẩn Conventional Commits (ISC) + self-review trước khi commit
```

## Thứ tự chạy điển hình

```
/init-project → /create-test-plan → /analyze-requirements --init
→ /generate-tc → /generate-tc --consolidate → /review-tc
→ /vibe-test → /log-bug → /test-report
```

Sau mỗi bước lớn: `/health-check`.

---

## Chưa bật ở project này

| Mục | Trạng thái | Bật lại bằng cách |
|---|---|---|
| **Automation** (`/init-source-code`, `/scan-source-code`, `/implement-automation`, `/execute-maintain`, `/review-src-tc`) | SKIPPED — project chạy manual | `/init-source-code --archetype <playwright-ts\|selenium-java\|appium-java>` rồi cập nhật `PIPELINE.md §4` |
| **Jira** (`/fetch-us`, `/log-bug --push-jira`, `/sync-jira-bugs`) | BLOCKED — chưa có link Jira | Thêm block `## Jira Integration` vào `02_analyze-requirements/Project_rule.md` (có sẵn khung comment ở cuối file) |
