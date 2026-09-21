# Tiến độ vibe-test — CHỈ TC v1.1 (dẫn xuất, không thay sổ coverage)

> 🔁 File **sinh tự động** từ `03_test-cases/v1.1/TC-MASTER-v1.1.xlsx` (sheet `ALL`) + `coverage/coverage-<MOD>.md`. **Sổ coverage từng module vẫn giữ nguyên mẫu số cũ** (gồm TC v1.0 CARRIED) để gate `verify_evidence.py` và `§10.5` không lệch; file này chỉ là **lát cắt v1.1**.
> Phạm vi = **toàn bộ TC của TC-MASTER v1.1** (`NEW` + `MODIFIED`), trừ `DESCOPED`. **⛔ KHÔNG gồm** TC v1.0 CARRIED (nằm ở `TC-MASTER-v1.0`).
> Cập nhật: 2026-09-21 · sau VR-013 (ORD) · **hàng ASN sửa tay sau VR-015 (2026-09-21)** · **hàng FEED sửa tay sau VR-016 (2026-09-21)** · **hàng ACT sửa tay sau VR-017 (2026-09-21)** · **hàng CNL sửa tay sau VR-018 (2026-09-21)** · verdict lấy từ sổ coverage mới nhất của từng module.

## Tổng quan

**142/221 TC v1.1 có verdict cuối = 64.3%** · ✅ PASS **82** (37.1%) · ❌ FAIL 36 · 🚫 BLOCKED 19 · ⛔ N-A 5 · ⏳ chưa có verdict **79** (35.7%)

| Module | TC v1.1 | ✅ PASS | ❌ FAIL | 🚫 BLOCKED | ⛔ N-A | ⏳ Chưa xong | **% có verdict** | % PASS | Sổ coverage |
|---|--:|--:|--:|--:|--:|--:|--:|--:|---|
| **ACT** | 10 | 6 | 2 | 2 | 0 | 0 | **100%** | 60% | ✅ có |
| **ASN** | 13 | 10 | 0 | 3 | 0 | 0 | **100%** | 77% | ✅ có |
| **CNL** | 13 | 5 | 6 | 2 | 0 | 0 | **100%** | 38% | ✅ có |
| **DLV** | 51 | 1 | 2 | 0 | 4 | 44 | **14%** | 2% | ✅ có |
| **FEED** | 5 | 4 | 0 | 1 | 0 | 0 | **100%** | 80% | ✅ có |
| **GIFT** | 8 | 3 | 1 | 2 | 0 | 2 | **75%** | 38% | ✅ có |
| **HOME** | 11 | 3 | 2 | 1 | 1 | 4 | **64%** | 27% | ✅ có |
| **NTF** | 9 | 0 | 0 | 0 | 0 | 9 | **0%** | 0% | ❌ chưa có (chưa vibe-test) |
| **ORD** | 48 | 34 | 8 | 3 | 0 | 3 | **94%** | 71% | ✅ có |
| **TS** | 17 | 0 | 0 | 0 | 0 | 17 | **0%** | 0% | ❌ chưa có (chưa vibe-test) |
| **USR** | 36 | 16 | 15 | 5 | 0 | 0 | **100%** | 44% | ✅ có |
| **Σ** | **221** | **82** | 36 | 19 | 5 | **79** | **64.3%** | 37.1% | |

> `DESCOPED` (loại khỏi mẫu số): TC-USR-041, TC-USR-044.

## TC v1.1 chưa xong theo module (⏳ chưa chạy · ⚠️ thiếu ảnh · ❌ FAIL · 🚫 BLOCKED)

- **ACT** — chưa chạy 0: — · FAIL/BLOCKED: 005🚫 008❌ 012❌ 015🚫
- **ASN** — chưa chạy 0: — · FAIL/BLOCKED: 008🚫 024🚫 026🚫
- **CNL** — chưa chạy 0: — · FAIL/BLOCKED: 004❌ 009❌ 010❌ 017❌ 018❌ 019❌ 020🚫 021🚫
- **DLV** — chưa chạy 44: 043 044 064 065 031 032 033 034 035 036 040 045 046 047 048 049 050 051 052 058 059 060 061 062 063 066 069 070 071 072 073 037 038 039 041 042 053 054 055 056 057 067 077 079 · FAIL/BLOCKED: 080❌ 081❌
- **FEED** — chưa chạy 0: — · FAIL/BLOCKED: 013🚫
- **GIFT** — chưa chạy 2: 008 011 · FAIL/BLOCKED: 003❌ 013🚫 014🚫
- **HOME** — chưa chạy 4: 008 031 029 030 · FAIL/BLOCKED: 025❌ 027❌ 028🚫
- **NTF** — chưa chạy 9: 008 005 014 017 018 019 020 021 022
- **ORD** — chưa chạy 3: 067 080 082 · FAIL/BLOCKED: 063❌ 074❌ 053❌ 058❌ 059❌ 064❌ 066❌ 069🚫 077❌ 084🚫 086🚫
- **TS** — chưa chạy 17: 008 009 010 011 012 016 017 020 022 023 024 013 014 015 018 019 021
- **USR** — chưa chạy 0: — · FAIL/BLOCKED: 002❌ 013❌ 017❌ 018❌ 020❌ 021❌ 022❌ 023❌ 024❌ 028❌ 029❌ 030❌ 032🚫 034🚫 035🚫 036🚫 037🚫 039❌ 040❌ 043❌

## Cách dùng
- Lệnh chạy phần còn nợ của 1 module chỉ v1.1: `/vibe-test --module <MOD> --tc <danh sách ID ở trên>` *(skill chưa có cờ lọc version)*.
- Muốn cập nhật file này sau mỗi phiên: chạy lại script sinh (hoặc bảo AI "cập nhật PROGRESS-v1.1").
