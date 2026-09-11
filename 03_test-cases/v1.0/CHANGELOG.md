# CHANGELOG — Test Cases v1.0

> **TC Generation Log** — đích write-back của `generate-tc` (⛔ KHÔNG ghi vào version MEMORY `§4`/`§9` — router chỉ trỏ, không chứa nội dung).
> Cột `Review Status` do `review-tc` cập nhật sau; `generate-tc` ghi `⏳`.

## 1. TC Generation Log

| Ngày | Action | DOC ID | Module | Tổng TC | File output | Priority | Mode | Techniques | Review Status |
|---|---|---|---|--:|---|---|---|---|---|
| 2026-09-07 | GENERATE | DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-05 · DOC-v1.0-06 | ACT | 14 | `fragments/TC-ACT-v1.0.md` | P1:0, P2:7, P3:7 | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |
| 2026-09-07 | GENERATE | DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-06 | ASN | 21 | `fragments/TC-ASN-v1.0.md` | P1:6, P2:13, P3:2 | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |
| 2026-09-07 | GENERATE | DOC-v1.0-01 · DOC-v1.0-06 | CNL | 14 | `fragments/TC-CNL-v1.0.md` | P1:4, P2:8, P3:2 | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |
| 2026-09-07 | GENERATE | DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-04 · DOC-v1.0-06 | DLV | 30 | `fragments/TC-DLV-v1.0.md` | P1:4, P2:25, P3:1 | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |
| 2026-09-07 | GENERATE | DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-06 | FEED | 14 | `fragments/TC-FEED-v1.0.md` | P1:2, P2:6, P3:6 | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |
| 2026-09-07 | GENERATE | DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-06 | GIFT | 12 | `fragments/TC-GIFT-v1.0.md` | P1:0, P2:6, P3:6 | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |
| 2026-09-07 | GENERATE | DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-06 | HOME | 24 | `fragments/TC-HOME-v1.0.md` | P1:1, P2:12, P3:11 | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |
| 2026-09-07 | GENERATE | DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-04 · DOC-v1.0-06 | NTF | 16 | `fragments/TC-NTF-v1.0.md` | P1:1, P2:9, P3:6 | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |
| 2026-09-07 | GENERATE | DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-04 · DOC-v1.0-06 | ORD | 54 | `fragments/TC-ORD-v1.0.md` | P1:7, P2:30, P3:17 | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |
| 2026-09-07 | GENERATE | DOC-v1.0-01 · DOC-v1.0-06 | TS | 7 | `fragments/TC-TS-v1.0.md` | P1:1, P2:2, P3:4 | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |
| 2026-09-07 | GENERATE | DOC-v1.0-01 · DOC-v1.0-02 · DOC-v1.0-04 · DOC-v1.0-06 | USR | 13 | `fragments/TC-USR-v1.0.md` | P1:1, P2:5, P3:7 | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |
| 2026-09-07 | — | — | **TỔNG 11 module** | **219** | — | **P1:27, P2:123, P3:69** | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |

| 2026-09-07 | CONSOLIDATE | tất cả DOC-v1.0-01..06 | **11/11 module** | **219** | `TC-MASTER-v1.0.xlsx` (+ `../TC-MASTER-LATEST.xlsx`) | P1:27, P2:123, P3:69 | standard | N/A | ❌ 0/100 REJECTED (2026-09-07) |

> **Consolidate 2026-09-07:** 13 sheet — `Overview` + `ALL` (phẳng canonical, sort Module → Priority → TC ID) + 11 sheet module (tên = `module_name` đầy đủ). 4 module nặng có **section header** `▬▬` gom theo màn/chức năng con: `ORD` 7 nhóm · `DLV` 8 nhóm · `ASN` 6 nhóm · `HOME` 4 nhóm.
> ⚠️ **Sheet của `CNL` phải đổi tên:** `module_name` = *"Huỷ đơn / Huỷ nhận đơn"* chứa ký tự `/` — Excel cấm trong tên sheet ⇒ sheet đặt là **`Huỷ đơn · Huỷ nhận đơn`** (thay `/` bằng `·`). `module_name` trong fragment-meta **giữ nguyên**, ⛔ không sửa fragment theo tên sheet.
> **0 CARRIED** — v1.0 là version đầu của chuỗi phân tích mới (`MASTER-MEMORY §4`) ⇒ không copy TC từ version cha; 0 fragment `.xlsx` legacy cần migrate.

## 2. Ràng buộc còn hiệu lực

1. **Mode `standard`** (QC GiangDC2 chốt 2026-09-07) ⇒ fragment **KHÔNG có** section `## Coverage Matrix`, Notes `Technique:` là tuỳ chọn. Đổi sang `comprehensive` phải chạy `/generate-tc --regenerate` cho toàn bộ module, ⛔ không trộn 2 mode trong cùng version.
2. **Scope = toàn bộ 11 module / 211 SC**, gồm cả `CNL` · `NTF` · `TS` mà PM xếp out-of-scope Phase 1. ⚠️ Xác nhận PM cho **execute** vẫn treo (`RISK-CNL-06` / `RISK-NTF-06` Pending) — nếu PM giữ nguyên out-of-scope thì **37 TC** của 3 module này (`CNL` 14 + `NTF` 16 + `TS` 7) không được đưa vào mẫu số pass-rate.
3. **Priority lấy theo từng dòng SC**, ⛔ không lấy theo aggregate `counts:` — 4 module (`DLV` `FEED` `HOME` `NTF`) đang drift giữa frontmatter và bảng SC (health-check `B-06`, xem `09_reports/health-check/health-check-2026-09-07.md`). Sau khi `/analyze-requirements --update` sửa aggregate thì **không cần** sửa TC.
4. **Nhãn loại hàng dùng theo app STG** (`Giấy tờ, hồ sơ`, 8 chip) — ⛔ tuyệt đối không dùng nhãn "Tài liệu" của tài liệu cho tới khi `C-ORD-09` được chốt.
5. **Khung giờ chọn TƯƠNG ĐỐI so với hiện tại** — ⛔ không hardcode giờ trong bất kỳ TC nào (`KP-01 §10.11`).
6. **13 TC dự kiến FAIL có chủ đích** (viết theo rule, app lệch ⇒ log bug, ⛔ KHÔNG sửa TC): `TC-FEED-010/011/012` · `TC-ORD-016/017/022/023` · `TC-CNL-004/009/010/012` · `TC-TS-003` · `TC-GIFT-007/010`. Đây là hiện thân của `KP-05 §4` (4 TC cố ý FAIL đợt cũ) + `KP-05 §5` (≥9 bug chưa log).
7. **`REQ-DLV-015` không xuất hiện ở cột `Req ID` của TC nào** — REQ này được phủ qua `SC-CNL-005` ⇒ `TC-CNL-005` (cột `Req ID` mang `REQ-CNL-003`). Đây là **coverage chéo module**, không phải gap; ⚠️ RTM dựng theo cột `Req ID` sẽ báo `REQ-DLV-015` trắng — cần `export-tc-rp`/`review-tc` xử lý bằng ghi chú, ⛔ không nhồi 2 REQ ID vào 1 ô.

## 3. Nợ đang mở

| # | Nợ | Trạng thái | Đích xử lý |
|---|---|---|---|
| 1 | ✅ ~~Chưa consolidate~~ — **đã consolidate 2026-09-07** | `MASTER-MEMORY §8` = COMPLETED · `§6` đã đăng ký | — |
| 2 | 🔴 **Review FAIL — G1 0/100 REJECTED (2026-09-07)**, 0 Critical · 36 Major · 36 Minor · 17 Info; block downstream tới khi fix. Chi tiết + fix routing: `11_tc-review/review-report-v1.0.md`. ~~Chưa review~~ — `review-tc` chưa chạy, gate G1 (score ≥70) chưa có số | Cột `Review Status` = ⏳ toàn bộ | `/review-tc`. 📌 **Đính chính:** persona reviewer **CÓ tồn tại** ở `~/.claude/skills/review-tc/references/reviewer-agent.md`; đường dẫn `review-agent/AGENT.md` mà `KP-05 §6` (đợt cũ) báo thiếu là **vị trí cũ đã bị bỏ** (không đúng Agent Skills spec). Ràng buộc thật của score cap là **thiếu `ANTHROPIC_API_KEY`** ⇒ không gọi được API instance |
| 3 | 🟡 **6 CL ưu tiên còn Open** ảnh hưởng assert của 13 TC vùng tranh chấp: `C-ORD-09` · `C-NTF-01` · `C-ORD-06` · `C-HOME-03` · `C-ORD-10` · `C-NTF-02` | Open | Hỏi BA; chốt xong ⇒ `/analyze --update` rồi `/generate-tc --regenerate --module <M>` |
| 4 | 🟡 **Tiền đề seed nặng chưa có**: đơn `Hết hạn` · timestamp 2h/4h · ≥6 tin cộng đồng · 3 phiên đồng thời · tài khoản "trắng" · 3 trạng thái quà 0/2/4 loại · đơn qua đủ 5 trạng thái với 3 vai | Chưa có | Nhờ dev/QA seed STG trước khi execute; thiếu bộ này thì ~40 TC blocked |
| 5 | 🟡 **`ACT` + `DLV` nên vibe-test trước execute** — nguồn nhãn/hành vi lấy từ `QA-obs` 2026-07 | `RISK-ACT-01` · `RISK-DLV-03` Open | `/vibe-test` 2 module này trước lô execute |
