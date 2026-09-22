# Vibe Test Report — VR-020 — module **DLV** — 2026-09-22

> Platform: mobile (Appium MCP · UiAutomator2) · Device `R58T20PLP8K` (thật) · App `com.hrisproject.stag`
> ⚠️ **Phiên dừng SỚM theo yêu cầu user** (lo hết token, ~80% đã dùng giữa chừng) — hoàn tất bước seed
> data + chạy **1 TC tới verdict chính thức** (`TC-DLV-043`, BLOCKED) và phát hiện 1 blocker lớn.

## Scope Coverage ★★

| | Count | % scope |
|---|--:|--:|
| **SCOPE_TOTAL (module DLV)** | **81** | 100% |
| Chạy trong run này (BLOCKED, có evidence) | **1** | 1.2% |
| Có verdict cuối luỹ kế (mọi run) | **20** | 24.7% |
| ⏳ NOT_RUN (còn nợ) | **61** | 75.3% |

**Có verdict cuối: 20/81 · CÒN NỢ: 61 TC → §8 = PARTIAL**.

## Việc đã làm

1. Seed 4 đơn NEED mới (`SEED-DLV-VR020-01..04`, A→C), B nhận + lấy hàng cả 4 (2/4 xác nhận chắc chắn
   `IN_TRANSIT`, 2/4 cần soát lại đầu phiên sau — nghi tap bị stale element).
2. Chạy `TC-DLV-043` trên `SEED-DLV-VR020-01` → phát hiện **BLOCKER**: form "Xác nhận đã giao" mở rộng
   (FR07, 4 loại đối tượng nhận) mà PRD v1.1 giả định **KHÔNG tồn tại** trên STG hiện tại — bấm nút chính
   chỉ ra popup đơn giản y hệt v1.0. Verdict: 🚫 BLOCKED, evidence đầy đủ. Kiểm tra chéo (không tính
   verdict riêng) trên `SEED-DLV-VR020-02` — cùng kết quả.
3. Ghi chú trong `coverage/coverage-DLV.md`: 13 TC khác cùng nhóm (`TC-DLV-044..053`, `069..071`) nhiều
   khả năng cũng BLOCKED vì cùng nguyên nhân, nhưng **giữ `NOT_RUN`** vì chưa verify riêng từng TC (đúng
   luật evidence-per-TC, không tự nhận verdict không có bằng chứng). Đề xuất QC/dev xác nhận build trước
   khi retest — mâu thuẫn với `RISK-DLV-08` ("Confirmed qua demo") và `TC-CNL-018`/`VR-018` hôm qua.
   **Không log bug mới** cho phát hiện này.
4. Thu thêm 1 ảnh evidence MỚI (tạo hôm nay, độc lập với `VR-018`) củng cố `BUG-044` (nút vẫn tên cũ
   "Đã giao cho người nhận").

## Chưa làm được (còn nợ, ưu tiên phiên sau)

- Nhóm RESCHEDULED/RETURNING (`TC-DLV-031..036`, `072`, `073`) — **nên kiểm tra nhánh "Không thể liên
  lạc được" TRƯỚC** trên 1 trong 4 đơn có sẵn, để biết nhánh này còn sống hay cũng bị ảnh hưởng bởi cùng
  gap vừa phát hiện.
- Nhóm "3 trạng thái đóng" (`TC-DLV-037..039`), cụm cảnh báo nhật ký (`054..056`), cụm lịch hẹn
  (`057..061`), và các TC còn lại — xem danh sách đầy đủ ở `coverage/coverage-DLV.md`.
- 3 TC time-based (`040`, `057`, `067`) cần rule 2h/4h/24h — không test được trong 1 phiên live, cần bàn
  cách mô phỏng (đổi giờ hệ thống?) hoặc chấp nhận NOT_RUN dài hạn.

## Đường dẫn

- Sổ cái tích luỹ: `08_test-runs/vibe/coverage/coverage-DLV.md`
- Log chi tiết phiên: `vibe-log.md` · Audit trail: `scope-ledger.md`
- Evidence: `screenshots/` (2 ảnh: `TC-DLV-043__step3-BLOCKED-form-mo-rong-khong-ton-tai.png` là evidence
  chính thức của `TC-DLV-043`, `BUG-044__verify-nut-van-cu-2026-09-22.png` củng cố bug đã log)
